# Warp Drives - Post-Apocalypse Remake
Reimplements warp travel within the confines of post-Cherryh/Apocalypse Stellaris.

# Features
* Simulates warp travel, complete with variable travel time based on travel distance (minimum 20 days).
* Fleet arrival timers - implemented as situations, has the option to rush jumps (for a possibility of failure).
    * Notifications for when a fleet has arrived or gone MIA. (Currently reuses ESN alerts to avoid overwriting alerts.txt.)
* Four tiers of warp drives, each with longer range and faster warp speeds.
* New civic: Warp FTL Theory - increased chance to receive warp drive tech research choices, and AI will prefer warp drives over hyper drives.
    * An event at game start will give the option to take the civic if you haven't already have one. The AI will never take it.
    * Alternatively, adding the `uses_warp_drives` to an empire will force the mod to give it (and overlord, allies, and vassals, if any) the civic at game start, and only at game start.
        * Note that only direct relations are affected, though any potential indirect relations are a moot point because usually an empire can be independent, in a federation, or a vassal, but not any combination of the three (except for hegemonic federations, but those are direct relations and thus moot), at game start.

# Limitations
The warp system is implemented within the confines of post-Cherryh/Apocalypse Stellaris. Specifically, version 3.8. The last version with built-in warp drive code was 1.9. Unsurprisingly, some workarounds had to be done.
* The warp drives have been implemented as jump drives, meaning jumps are instant and warp has to be simulated.
* So, when a fleet with warp drives executes a "warp" jump, it is immediately event-locked and a flag set. (As a fallback, the event-lock is released if the flag is not cleared in a different event.)
    * The event lock is done in the event triggered by the jump to block all other orders from being executed until the ship is event-unlocked.
* A situation is used to show how long until a fleet "arrives" at the destination (read: the current system it is in).
    * Approaches exist to either speed up the warp while risking possible failures, or just keep warping as normal.
* For some reason, only civilian ships (and possibly single-ship fleets - need testing) can trigger the on_ship_order on-action. An event that triggers on daily (with checks to make sure only a fleet that is jumping is eligible) is used as a workaround.
    * This may affect performance if a large number of fleets are using warp drives.
* To avoid overwriting files too much, only "No Drive" and "Bio-Drive" options have been overwritten. This means countries will start with __both__ hyper drives and warp drives, unless they have __Eager Explorers__ or an equivalent civic.
    * This is a compromise done to maximize mod compatibility. The affected drives are also not commonly used by playable countries anyway (Bubbles excepting).
* A previous build has FTL disabled, but it has since been re-enabled because __the AI just. Doesn't. Know. How. To. Pathfind. Using. Only. Jump. Drives.__ You will have to press J and target a system to make a  warp jump.
