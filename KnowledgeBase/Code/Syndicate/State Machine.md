[[K-Syndicate]] [[Code Core]]
Simple states for game can be something like this:
	Bootstrap -> Game Loop -> Dispose

### Problem
During game initialization or deinitialization, there can be instabilities (e.g. race conditions). Without control these processes can be hard to maintain and scale.

Different architectures try to solve that problem, to give developer more space, control and flexibility over game's lifecycle - to streamline the development

## State machine (in multiscene architecture)

#### Interfaces:
``` c#
public interface IState : IExitableState  
{  
    void Enter();  
}  
  
public interface IPayloadedState<TPayload> : IExitableState  
{  
    void Enter(TPayload payload);  
}  
  
public interface IExitableState  
{  
    void Exit();  
}
```


#### States controller

##### Fields and constructor
	Storing all states and current active state. In this example the states registering happens here, but it can be integrated with DI as well 

``` c#
public class GameStateMachine  
{  
    private Dictionary<Type, IExitableState> _states;  
    private IExitableState _activeState;  
  
    public GameStateMachine(SceneLoader sceneLoader, LoadingCurtain loadingCurtain, AllServices services)  
    {        
	    _states = new Dictionary<Type, IExitableState>()  
        {  
            [typeof(BootstrapState)] = 
            new BootstrapState(this, sceneLoader, services),  
            
            [typeof(LoadLevelState)] = 
            new LoadLevelState(this, sceneLoader, loadingCurtain,  
                services.Single<IGameFactory>(), services.Single<IPersistentProgressService>()),  
                
            [typeof(LoadProgressState)] = new LoadProgressState(this, services.Single<IPersistentProgressService>(), services.Single<ISaveLoadService>()),  
            [typeof(GameLoopState)] = new GameLoopState(this)  
        };    
    }
}
```


##### States changing
	We have two methods for Entering the state. The second one takes Payload as configuration, so one state could send data to another. Also there are some auxiliary methods to make code clean and readable
``` c#
    public void Enter<TState>() where TState : class, IState  
    {  
        TState newState = ChangeState<TState>();  
        newState.Enter();  
    }
      
    public void Enter<TState, TPayload>(TPayload payload) where TState : class, IPayloadedState<TPayload>  
    {        
	    TState newState = ChangeState<TState>();  
        newState.Enter(payload);  
    }
      
    private TState ChangeState<TState>() where TState : class, IExitableState  
    {  
        _activeState?.Exit();  
        TState newState = GetState<TState>();  
        _activeState = newState;  
        return newState;  
    }  
    private TState GetState<TState>() where TState : class, IExitableState  
    {  
        return _states[typeof(TState)] as TState;  
    }}
```


#### Examples of states
	 Initial state that setups dependencies and enters LoadProgressState 
``` c#
public class BootstrapState : IState  
{  
    private const string Initial = "Initial";  
    private readonly GameStateMachine _stateMachine;  
    private SceneLoader _sceneLoader;  
    private AllServices _services;  
  
    public BootstrapState(GameStateMachine gameStateMachine, SceneLoader sceneLoader, AllServices allServices)  
    {        
	    _stateMachine = gameStateMachine;  
        _sceneLoader = sceneLoader;  
        _services = allServices;  
        RegisterServices();  
    }  
    
    public void Enter()  
    {
        _sceneLoader.Load(Initial, onLoaded: EnterLoadLevel);  
    }  
    
    private void EnterLoadLevel()  
    {
        _stateMachine.Enter<LoadProgressState>();  
    }  
    
    private void RegisterServices()  
    {        
	    _services.RegisterSingle<IInputService>(GetInputService());  
        _services.RegisterSingle<IAssets>(new AssetProvider());  
        _services.RegisterSingle<IPersistentProgressService>(new PersistentProgressService());  
        _services.RegisterSingle<IGameFactory>(new GameFactory(_services.Single<IAssets>()));  
        _services.RegisterSingle<ISaveLoadService>(  
            new SaveLoadService(_services.Single<IPersistentProgressService>(), _services.Single<IGameFactory>()));  
    }  
    
    private IInputService GetInputService()  
    {        
	    if (Application.isEditor)
	    {
            return new StandaloneInputService();  	    
	    }  
        return new MobileInputService();  
    }  
    public void Exit()  
    {    }
}
```

---

	State that loads progress using saveLoadService and after that enters LoadLevelState and passes argument as paylaod
``` C#
public class LoadProgressState : IState  
{  
    private readonly GameStateMachine _gameStateMachine;  
    private readonly IPersistentProgressService _progressService;  
    private readonly ISaveLoadService _saveLoadService;  
  
    public LoadProgressState(GameStateMachine gameStateMachine, IPersistentProgressService progressService, ISaveLoadService saveLoadService)  
    {        _gameStateMachine = gameStateMachine;  
        _progressService = progressService;  
        _saveLoadService = saveLoadService;  
    }  
    public void Enter()  
    {        LoadProgressOrInitNew();  
        _gameStateMachine.Enter<LoadLevelState, string>(_progressService.Progress.WorldData.PositionOnLevel.Level);  
    }  
    private void LoadProgressOrInitNew()  
    {        var progressServiceProgress = _saveLoadService.LoadProgress() ?? NewProgress();  
        _progressService.Progress = progressServiceProgress;  
    }  
    private PlayerProgress NewProgress()  
    {        
	    return new PlayerProgress("Main");  
    }  
    public void Exit()  
    {            }  
}
```

---
	This state using loading curtain, changes the scene, after that create objects(view factory) initializes loaded data, and enters GameLoopState 
``` c#
public class LoadLevelState : IPayloadedState<string>  
{  
    private const string InitialPoint = "InitialPoint";  
  
    private readonly GameStateMachine _gameStateMachine;  
    private readonly SceneLoader _sceneLoader;  
    private readonly LoadingCurtain _loadingCurtain;  
    private readonly IGameFactory _gameFactory;  
    private readonly IPersistentProgressService _progressService;  
  
  
    public LoadLevelState(GameStateMachine gameStateMachine, SceneLoader sceneLoader, LoadingCurtain loadingCurtain,  
        IGameFactory gameFactory, IPersistentProgressService progressService)  
    {        
	    _loadingCurtain = loadingCurtain;  
        _gameFactory = gameFactory;  
        _progressService = progressService;  
        _gameStateMachine = gameStateMachine;  
        _sceneLoader = sceneLoader;  
    }  
    public void Enter(string payload)  
    {        
	    _loadingCurtain.Show();  
        _gameFactory.Cleanup();  
        _sceneLoader.Load(payload, OnLoaded);  
    }  
    public void Exit()  
    {        
	    _loadingCurtain.Hide();  
    }  
    private void InformProgressReaders()  
    {        
	    foreach (ISavedProgressReader progressReader in _gameFactory.ProgressReaders)  
        {            
	        progressReader.ApplyProgressData(_progressService.Progress);  
        }    
    }  
    
    private void OnLoaded()  
    {        
	    InitGameWorld();  
        InformProgressReaders();  
        _gameStateMachine.Enter<GameLoopState>();  
    }
      
    private void InitGameWorld()  
    {        
	    var hero = _gameFactory.CreateHero(GameObject.FindWithTag(InitialPoint));  
        _gameFactory.CreateHud();  
        CameraFollow(hero);  
    }  
    
    private void CameraFollow(GameObject gameObject)  
	{  
	    Camera.main.GetComponent<CameraFollow>().Follow(gameObject);  
	}
}
```

