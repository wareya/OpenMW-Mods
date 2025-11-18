# OpenMW-Mods
Random small mods for OpenMW. Might be outdated or unnecessary.

LICENSE: CC0, but only for the changes from the original data, not for the full data files.

`chestfix2` - Fix the contents of Com_Chest_11_k01 to match what they were before Bloodmoon, rather than being nearly empty. For many dungeons, a few copies of this chest is basically all the reward you get.

`crescent_crash_workaround` - At some point in the game you gain access to an item with "Crescent" in its name that causes you to teleport to another scene. For some reason, when doing this content, at some point during it, I crashed. I debugged the issue and made this addon for myself so that I could finish that content. I *do not* remember the details, or even what point in the content the crash happened. I do not know whether this addon is still needed.

`Late DB Attack` - Delay Dark Brotherhood attacks in a relatively simple way:

```
; Index 5 of this quest is the earliest point in the main
; quest that the protagonist is expected to talk to anyone
; about the Nerevarine prophecies.
; However, if a newbie gets assaulted by assassins on the
; way to the dungeon, and they never got assaulted by
; assassins before, it'd be SUPER janky, so I'll use the
; "gave the puzzle box to Antabolis" index instead.
if ( GetJournalIndex A1_2_AntabolisInformant >= 10 )
	set goodtogo to 1
endif
; We can also do it if they're doing the backdoor.
if ( GetJournalIndex CX_BackPath > 0 )
	set goodtogo to 1
endif
; If they somehow completed the main quest without
; doing any of the above (which is entirely possible)
; we should account for that, too.
if ( GetJournalIndex C3_DestroyDagoth == 50 )
	set goodtogo to 1
endif
; Alternatively, we can assume the protagonist is "good to go"
; if they're high enough level.
if ( player->GetLevel >= 5 )
	set goodtogo to 1
endif

if ( goodtogo == 0 )
	return
endif
```

