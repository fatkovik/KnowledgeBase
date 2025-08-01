[[Unity]]

What is Prefab?
Prefab is template of an Unity game object.

How it's works?
Simply you can have the main game object prefab ( the papa) then you can create of it many of other instances of the same game object (the child). You can change the child and it will affect only to that exact game object. But when you change the papa game object all the children change the same way with him.

How to create prefab in Unity?
Simply. Just drag and drop the game object in your assets folder or right click on it and choose "prefab".

**How to work with prefabs?**

	How to know what I changed in child?
		When you make some changes in child and want to know what it is overriding in the top of inspector you can see "overrides" and watch there your changes.
		
	What if I want the papa to be changed the same way?
		You can Apply changes to the papa prefab when your child prefab changed and it will affect all other child prefabs too.
	
	What if I want to make child prefab to be another new prefab(new the papa pr
	efab)?
		When tou want to make child new prefab you drag and drop it and then decide its a new original prefab or a variant 
		
	What if I dont want to child and the papa to be related to each other?
	
		Yor right click on child game object ->Prefab->Unpack or Unpack completly.
			
			What is a difference between "Unpack" and "Unpack Completly"
				I will write it  in the next section.


What is Nested Prefabs?
When you attach a prefab to another prefab ( for example House prefab have a door prefab inside of it) it called Nested prefab.
Various of prefabs can be nested inside of each other.(a prefab in prefab in prefab in prefab...)

So what is a difference between "Unpack" and "Unpack Completely"?
When you have nested prefab in your child only your child will affect to unpacking.
But if you do "Unpack Completely" all the prefabs (nested prefabs too) will affect to that unpacking.
