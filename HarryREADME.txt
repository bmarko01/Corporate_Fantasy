--------OBJECTIVES--------
Objectives are an array of EObjective structs inside MainCharacter_BP. The only two variables they have are a description and a completed boolean. 
You can add additional attributes inside the EObjective struct and they will still be saved.

Maximum Objectives can be set through the variable in MainCharacter_BP

To give the player a new objective, use ‘TryAddObjective’ function inside MainCharacter_BP. 
It will return false if the player already has that objective or they are holding the maximum amount.

To complete an objective, use ‘CompleteObjective’ function in MainCharcter_BP. 
It will return true if the player had that objective and could finish it.

On the HUD, objectives are listed in a vertical box. Widgets (of class WBP_Objectives) spawn into the box and clear when the objective is completed.


--------SAVING--------
There is now one SaveGame class called BP_SaveData. Saving is done through it and the Game Instance.

To save the game, call ‘SaveGame_Env’ from the game instance.
There is currently one save slot, called ‘Slot1’. 
To create new saves slots, change the ‘CurrentSaveSlot’ string inside the game instance to a different name, and call ‘SaveGame_Env’ again.

To Load a game, call the ‘LoadGame’ function in the Game Instance.
Loading the Game will only download the data from the save file. 
To finish loading, each map will need to call ‘ApplyLoadedData_Env’ from the game instance. The two maps in the game currently are set up to do this.

You can think of the saving/loading paradigm as:

               STORE------------ -->    SAVE,                                 LOAD       ---------------->      APPLY
     (Get all the information)   (Write info to file)                   (Get info from file)        (Change game variables to match)

There is a function called Store Level Data within the Game Instance that will need to be expanded as you determine additional variables that need saving within a given level.
When you destroy an item, you can use ‘NoteDestroyedItem’ in the game instance to add it to the save data.


-------LEVEL GENERATION--------
The SaveGame contains an array of ‘SpawnParams’. Which are structs denoting the likelihood of a given character spawning on a tile.

Spawn params are made up of a class, a spawn chance (between 0 & 1), a Minimum and maximum in dungeon.
Min and Max allow you to hard set or cap the number of characters in the procedural level should you wish.

Generating characters in the procedural level is done though ‘RandomLevelgenerator’ in the ‘SpawnCharacters’ function.

After each tile is spawn, the function goes the list of possible characters, and for each, rolls to determine whether or not is should spawn one on the tile.
The chance that a character will spawn is determined by the ‘SpawnChance’.

If you wish to edit the spawn params, use the ‘SetSpawnParams’ function in the game instance.
If you use as an argument for this function, a class which already has Spawn params, it will override the existing one.


Any questions feel free to ask me on Discord @ hg.exe#0877

Harry Greenaway


 

