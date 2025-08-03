[[Code Core]]
### Infrastructure
- Have an **entry point** (bootstrapper lets say)
- Create "services" with interfaces to be able to use IoT (DI)... So those can be easily replaced if necessary, also it is useful and good when everything connected to that "service" goes through one point
- Awake is used for initializations
- General Services that are used in games
	- Input
	- Player progress (save/load)
	- Asset management
	- Game Factory
	- Configs (static data)
	- Ads
### Misc
- Use the features (e.g. refactoring tools, hotkeys for quick actions etc.) of IDE, its not just an text editor
- There are **Script Execution Order** window in Unity... It's recommended to use it only for bootstrappers, and maybe for plugins/packages... Anyway in most of the time you're not gonna need this
- You can multiply quaternion with vector3, to **rotate the the vector**!![[Quatertion multiplication with Vector3.png]]

[[Things to remember]]