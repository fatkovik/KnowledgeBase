Simple states for game can be this:
	Bootstrap -> Game Loop -> Dispose

### Problem
During game initialization or deinitialization, there can be instabilities (e.g. race conditions). Without control these processes can hard to maintain and scale.

Different architectures try to solve that problem, to give developer more space, control and flexibility over game's lifecycle -  to streamline the development

## State machine
