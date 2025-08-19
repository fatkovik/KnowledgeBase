[[Code Core]] [[K-Syndicate]]
### Infrastructure
- Have an **entry point** (bootstrapper lets say)
	- Also in editor when using **multiple scenes architecture** use this code snippet to always start from the same scene (Despite what scene is currently opened) 
``` c#
#if UNITY_EDITOR  
    [RuntimeInitializeOnLoadMethod(RuntimeInitializeLoadType.BeforeSceneLoad)]  
    static void InitialSceneAutoLoad()  
    {            
	    if (SceneManager.GetActiveScene().name == "Initial") return;  
            
            SceneManager.LoadScene("Initial");  
            Debug.Log("Auto scene load");  
    }
    #endif
```
---
- Create "**Services**" with *interfaces* to be able to use **IoT (DI)**... So those can be easily replaced if necessary, also it is useful and good when everything connected to that "service" goes through one point
- Awake is used for initializations
- General services that are used in games
	- Input
	- Player progress (save/load)
	- Asset management
	- Game Factory
	- Configs (static data)
	- Ads
---
### Helper classes
#### SceneLoader
``` c#
public class SceneLoader  
{  
    private readonly ICoroutineRunner _coroutineRunner;  
  
    public SceneLoader(ICoroutineRunner coroutineRunner) =>  
        _coroutineRunner = coroutineRunner;  
  
    public void Load(string name, Action onLoaded = null) =>  
        _coroutineRunner.StartCoroutine(LoadScene(name, onLoaded));  
  
    private IEnumerator LoadScene(string name, Action onLoaded = null)  
    {  
        if (SceneManager.GetActiveScene().name == name)  
        {            onLoaded?.Invoke();  
            yield break;  
        }        
        
        AsyncOperation waitNextScene = SceneManager.LoadSceneAsync(name);  
  
        while (!waitNextScene.isDone)  
            yield return null;  
  
        onLoaded?.Invoke();  
    }}
```
---
#### LoadingCurtain
``` c#
public class LoadingCurtain : MonoBehaviour  
{  
    public CanvasGroup Curtain;  
  
    private void Awake()  
    {        
	    DontDestroyOnLoad(this);  
    }  
    public void Show()  
    {        
	    gameObject.SetActive(true);  
        Curtain.alpha = 1;  
    }  
    public void Hide() => StartCoroutine(FadeIn());  
  
    private IEnumerator FadeIn()  
    {        
	    while (Curtain.alpha > 0)  
        {            
	        Curtain.alpha -= 0.03f;  
            yield return new WaitForSeconds(0.03f);  
        }  
        gameObject.SetActive(false);  
    }}
```
### Misc
- Use the **features** (e.g. refactoring tools, hotkeys for quick actions etc.) of **IDE**, its not just an text editor
- There are **Script Execution Order** window in Unity... It's recommended to use it only for bootstrappers, and maybe for plugins/packages... Anyway in most of the time you're not gonna need this
- You can multiply quaternion with vector3, to **rotate the the vector**!![[Quatertion multiplication with Vector3.png]]
- 