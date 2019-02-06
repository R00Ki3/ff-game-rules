# ff-game-rules
Modular game rules for fortress forever servers.


## How to Install
 * **game_rules**
 
   Unzip this into your *FortressForever/maps/* folder. These are the basic game rules files that will tell the server which scripts you    want to run. You can comment out the ones you don't want to use with a double dash "--" in front of that IncludeScript.

   **Example:**
   ```lua
   -- For CTF game mode put the include script here
   if GAMEMODE == "CTF" then
	   -- IncludeScript("game_force_ovd") -- Won't be used
	   IncludeScript("game_auto_balance")
   end
   
   -- For all game modes put the include script here
   IncludeScript("game_afk")
   --IncludeScript("game_spawn_safety") -- Don't use this
   ```
   To activate game_rules on your server use the CVAR below. Also make sure it is added to your server config file.
   ```
   sv_globalluascript game_rules
   ```
* *Note: base_ctf & base_ctf4*

   These are base files included with Fortress Forever, I added a single variable to them that I can detect for use with other files.   Their main function remains unchanged and can be overwritten.

## Adding Mods

Put all mods in your *FortressForever/maps/includes/* folder and add the appropriate IncludeScript("Game_name") To your game_rules.lua. There is an example above.
 * **game_afk**

   Will send a player to spectator after about 2 minutes of not moving. Can be used in any game mode.
   ```lua
   local CHECK_AFK = 30 -- How often in seconds it checks to see if a player is AFK
   local IDLE_TIME = 120 -- How long in seconds it takes to go AFK
   local MESSAGE_TIMER = 10 -- Starts counting down when the timer reaches this number
   ```
* **game_spawn_safety**

   Makes a player Immune to damage for a few seconds after spawning or until they attack another player. Can be used in any game mode.
   ```lua
   local IMMUNE_TIME = 3
   ```
* **game_auto_balance**

   Prevents a player from joining a team that will make it unbalanced. Currently set up to only work on CTF with Red and Blue teams.   Unknown what will happen if you try to use it in any other game modes.

* **game_force_ovd**

   Forces an Offense vs Defense game mode. With Blue as Offense and Red as Defense. The Red team will be unable to touch the Blue flag until the player threshold is met. Used in CTF game mode with Red and Blue teams. 
   ```lua
   local PLAYERS_NEEDED = 10
   ```
   ![Screenshot](http://i58.tinypic.com/k3181s.png)

* **game_ff_armor**

   Armor-Only friendly fire. Mirror damage or Team only damage available.
   ```lua
   TEAM_DAMAGE_ALLOWED = true
   TEAM_DAMAGE = 5 -- Divide damage by this much for less armor removed.
   
   MIRROR_DAMAGE_ALLOWED = true
   MIRROR_DAMAGE = 5 -- Divide damage by this much for less armor removed.
   ```
   
* **game_readyup**

   Puts players on a ready screen, in which they must type "r" (Or other modified chat messages) to indicate they are ready to play.  Begins a countdown when all players on both teams are ready. Only works during prematch.
   ```lua
   local PrematchTime = 999
   local UsefulTip = "Type 'r' when you are ready to start the match."
   local ChatStrings = { "r", "ready", "start", "go" }  -- Strings to use for a player to accept being ready
   ```
   ![screenshot](http://oi57.tinypic.com/eh0hgh.jpg)
   
* **game_duels**

   When two enemy players are within melee range of each other and hold "use" simultaneously. They will engage in a one on one duel. They will restock life and ammo. Outsiders can't interrupt them and they cant hurt outsiders until the duel is over. The first player to kill the other; wins, or until 30 seconds is up then a random winner is chosen. 
   ```lua
   local REQUEST_RADIUS = 128
   local FIGHT_TIME = 30

   local USE_OBJECTIVEICON = true
   local RESTOCK_PLAYER = true
   ```
   
* **Other Mods**

   Other mods might exist in the repository. They are unfinished or works in progress. Use at your own risk. 
