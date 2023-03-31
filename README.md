# Warp Drives - Post-Apocalypse Remake
Reimplements warp travel within the confines of post-Cherryh/Apocalypse Stellaris.

# Features
* Simulates warp travel, complete with variable travel time based on travel distance (minimum 20 days).
* Fleet arrival timers - implemented as situations, can perform fleet diagnostics (for a buff on-arrival) or rush jumps (for a debuff on-arrival and possibility of failure at low values).
  * Notifications for when a fleet has arrived or gone MIA.
* Three tiers of warp drives, each with longer range and faster warp speeds.
* New civic: Warp FTL Theory - increased chance to receive warp drive tech research choices, and AI will prefer warp drives over hyper drives.

# Implementation
The warp system is implemented within the confines of post-Cherryh/Apocalypse Stellaris. Specifically, version 3.7. The last version with built-in warp drive code was 1.9. Unsurprisingly, some workarounds had to be done.
* The warp drives have been implemented as jump drives without any hyper jumping capability, meaning jumps are instant and warp has to be simulated.
* So, when a fleet with warp drives executes a "warp" jump, it is immediately event-locked and a flag set. (As a fallback, the event-lock is released if the flag is not cleared in a different event.)
  * It does not however prevent the fleet from executing any queued orders, and other pitfalls still exist (currently under testing).
* To prevent the fleet from executing orders while "warping", _all_ of the fleet's orders are cleared following a jump.
  * This is a rather... hardcore decision, but the only one I have to stop the fleet from moving until it finishes "warping". Attempting to zero out the fleet's speed via a static modifier causes it to move at a snail's pace... somehow. Even if every ship has a stated speed of 0.
  * The obvious downside is that orders have to be re-issued to a fleet that just finished "warping", which can be a hassle in the late game.
* A situation is used to show how long until a fleet "arrives" at the destination (read: the current system it is in).
  * Approaches exist to either speed up the warp while risking debuffs and possible failures, or perform diagnostics and get a buff, or just keep warping as normal.
  * Currently exists largely as a placeholder until I figure out what to do with it.
  