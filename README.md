# Warp Drives - Post-Apocalypse Remake
Reimplements warp travel within the confines of post-Cherryh/Apocalypse Stellaris.

# Features
* Simulates warp travel, complete with variable travel time based on travel distance (minimum 10 days).
* Fleet arrival timers - implemented as situations, has the option to rush jumps (for a possibility of failure).
    * Notifications for when a fleet has arrived or gone MIA. (Currently reuses ESN alerts to avoid overwriting alerts.txt.)
* Five tiers of warp drives, each with longer range and faster warp speeds.
* New trait: Warp FTL Theory - enhanced warp drives for empire species, and AI will prefer warp drives over hyper drives.

# Limitations
The warp system is implemented within the confines of post-Cherryh/Apocalypse Stellaris. Specifically, version 3.8. The last version with built-in warp drive code was 1.9. Unsurprisingly, some workarounds had to be done.
* The warp drives have been implemented as jump drives, meaning jumps are instant and warp has to be simulated.
* So, when a fleet with warp drives executes a "warp" jump, it is immediately event-locked and a flag set. (As a fallback, the event-lock is released if the flag is not cleared in a different event.)
    * The event lock is done in the event triggered by the jump to block all other orders from being executed until the ship is event-unlocked.
* A situation is used to show how long until a fleet "arrives" at the destination (read: the current system it is in).
    * Approaches exist to either speed up the warp while risking possible failures, or just keep warping as normal.
* For some reason, only civilian ships (and possibly single-ship fleets - need testing) can trigger the on_ship_order on-action. An event that triggers on daily (with checks to make sure only a fleet that is jumping is eligible) is used as a workaround.
    * This may affect performance if a large number of fleets are using warp drives.
* To avoid overwriting files too much, only "No Drive" and "Bio-Drive" options have been overwritten. For now, due to ongoing rewrite, countries will start with Warp Drives alongside Hyper Drives.
    * This is a compromise done to maximize mod compatibility. As of Grand Archive (3.14), most of the affected drives are used by space fauna.
* Some builds have FTL enabled to allow the AI to use warp drives in a limited capacity since **the AI just. Doesn't. Know. How. To. Pathfind. Using. Only. Jump. Drives.** (Except in wartime, apparently.) After some back-and-forth, I decided on keeping hyper FTL on the warp drives since disabling it also causes bypasses to be unusable for normal players for some reason.
