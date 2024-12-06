# UnusedMusicTracks

## Unused
These music tracks are completely unused.

### bart_chase02_end_sus1
- Initialised in Levels 2, 4, and 6 as alias `Bart_Chase02_End_Sus1`.
- Never assigned to any region. An alternative vehicle exit cue is used instead.

### collection01d_drama_pickup_b3
- Initialised in Level 3 as alias `Collection01d_Drama_Pickup`.
- Assigned to region `M2_drama_region`; this region is never called, but would be if unused functionality (Chase Sedan escape sequences) commented out in the L3 M2 mission script was in use.

### fe_trans01
- Initialised in Levels 1-7 as alias `FE_trans01`.
- Assigned to region `FE_trans01`; this region is never called due to music script unload timing, however it is supposed to occur on exit to Main Menu.

### fe_trans02
- Initialised in all Levels as alias `FE_trans02`.
- Assigned to region `FE_trans01`; this region is never called due to music script unload timing, however it is supposed to occur on exit to Main Menu.

### fe_trans03
- Initialised in all Levels as alias `FE_trans03`.
- Assigned to region `FE_trans01`; this region is never called due to music script unload timing, however it is supposed to occur on exit to Main Menu.

### generic\of_time_out01
- Initialised in Levels 2-6 as alias `OF_time_out01`.
- Assigned to region `OF_time_out_region` (except in Level 5); this region is never called.

### generic\of_time_out02
- Initialised in Levels 2-6 as alias `OF_time_out02`.
- Assigned to region `OF_time_out_region` (except in Level 5); this region is never called.

### gogo_drama_pickup
- Initialised in Level 1 as alias `Gogo_Drama_Pickup`.
- Assigned to region `M2_drama_region`; this region is never called, however the "TALK TO NED" objective at the end of the mission does feature a correct but ineffective call to `AddStageMusicChange`.

### halloween\organ_music
- Initialised in Level 7 as alias `Organ_Music`.
- Assigned to region `StoneCutters_Tunnel_region`; this region is never called in Level 7 as the trigger is out-of-bounds.

### homer\homer_reward01
- Initialised in Levels 1 and 7 as alias `Homer_Reward01`.
- Never assigned to any region. Alternative card collection cues are used instead.

### homer\homer_reward02
- Initialised in Levels 1 and 7 as alias `Homer_Reward02`.
- Never assigned to any region. Alternative card collection cues are used instead.

### homer\tuba_044
- Initialised in Level 1 as alias `Tuba_044`.
- Assigned to region `OF_time_out_region`; this region is never called. Shares naming scheme with Homer's on-foot explore cues.

### homer\tuba_053
- Initialised in Levels 1 and 7 as alias `Tuba_053`.
- Never assigned to any region. Shares naming scheme with Homer's on-foot explore cues.

### homer\tuba_059
- Initialised in Level 1 as two aliases, both of which are `Tuba_059`.
- Never assigned to any region. Shares naming scheme with Homer's on-foot explore cues.

### homer\tuba_061
- Initialised in Level 1 as two aliases, both of which are `Tuba_061`.
- Never assigned to any region. Shares naming scheme with Homer's on-foot explore cues.

### land_of_choc_end_neg
- Initialised in Level 7 as alias `Land_of_Choc_End_Neg`.
- Assigned to region `M4_S2_end_Neg_region`; this region is typically never called as it is only callable after a music state change, during which the mission (L7 M4) has no fail conditions (though there is unused functionality for one, a timer); can technically be heard if the mission is restarted post-music state switch and then failed in the earlier stage, due to a bug/oversight where music state is not reset on mission restart.

### marge\lounge010
- Initialised in Level 4 as alias `Lounge010`.
- Never assigned to any region. Shares naming scheme with Marge's on-foot explore cues.

### marge\lounge_trans06
- Initialised in Level 4 as alias `Lounge_Trans06`.
- Never assigned to any region. Shares naming scheme with Marge's interior entry cues.

### marge\tuba_024
- Initialised in Level 4 as alias `Tuba_024`.
- Never assigned to any region. Shares naming scheme with Homer's on-foot explore cues, but is in same directory as Marge's on-foot explore cues.

### nick_end_sus
- Initialised in Levels 2 and 4 as alias `Nick_End_Sus`.
- Never assigned to any region in Level 2; assigned to region `M6_end_Sus_region` in Level 4 (this region is never called - the mission (L2 M6) forcibly keeps the mission theme playing whilst on-foot).

### powerplant_10sec
- Initialised in Levels 1 and 4 as alias `PowerPlant_10sec`.
- Assigned to region `M4_10sec_region` in Level 1 and region `Bonus_10sec_region` in Level 4; these regions are never called.

### scarymusic01
- Initialised in Level 7 as alias `ScaryMusic01`.
- Assigned to region `OF_Apu_Oasis_region`; this region is never called in Level 7 due to an incorrect trigger event ID.

### stone_cutter_spoof
- Initialised in Levels 1-7 as alias `Stone_Cutter_Spoof`.
- Assigned to region `StoneCutters_region`; this region is never called except through an out-of-bounds trigger in Level 7 (prior to removal, and as seen in the late-stage PlayStation 2 prototype, this music track would originally play outside of the StoneCutter mansion in Levels 1, 4, and 7).

## Uncalled
These music tracks are used in the game, but have unused scripted occurances.

### banjo_end_pos
- Initialised in Level 2 as alias `Banjo_End_Pos`, and assigned to region `M5_S1_end_Pos_region`; however, the mission (L2 M5) doesn't assign this region to its music state 1 mission completion theme (one is not set at all for this state).

### bollywood02_end_pos
- Initialised in Level 2 as alias `Bolloywood02_End_Pos`, and assigned to region `M5_S2_end_Pos_region`; however, the mission (L2 M5) switches from music state 2 to 1 before the mission completion event can occur.

### collection01d_drama
- Initialised in Level 3 as alias `Collection01d_Drama`, and assigned to region `M2_drama_region`; however, this region is never called by the mission (L3 M2) - unused functionality for Chase Sedan escape sequences would've called it if enabled.

### collection01d_end_pos
- Initialised in Level 2 as alias `Collection01d_End_Pos`, and assigned to region `M2_S1_end_Pos_region`; however, the mission (L2 M2) switches from music state 1 to 2 before the mission completion event can occur.

### gogo_drama
- Initialised in Level 1 as alias `Gogo_Drama`, and assigned to region `M2_drama_region`; however, this region is never called by the mission (L1 M2) - thought there is a correct but ineffective call to `AddStageMusicChange` during the final "TALK TO NED" objective.
- Initialised in Level 7 as alias `Gogo_Drama`, and assigned to region `M6_drama_region`; however, the mission (L7 M6) has a mission script typo that prevents the region from being called when it is supposed to be (at the Alien Car escape objective).

### hallsballs_end_pos2
- Initialised in Level 7 as alias `Halls_Balls_End_Pos`, and assigned to region `M4_S1_end_Pos`; however, the mission (L7 M4) switches from music state 1 to 2 before the mission completion event can occur.

### homer\tuba_028
- Initialised in Level 7 as alias `Tuba_028`, but never assigned to any region.

### homer\tuba_062
- Initialised in Level 1 as alias `Tuba_062`, and assigned to region `OF_time_out_region`; however, this region is never called.

### homer\tuba_063
- Initialised in Level 1 as alias `Tuba_063`, and assigned to region `OF_time_out_region`; however, this region is never called.

### motown_end_sus
- Initialised in Level 1 as alias `M5_End_Sus`, and assigned to region `M5_end_Sus_region`; however, the mission (L1 M5) assigns/continues the main mission theme itself for the vehicle exit event.

### orch_chase01_drama
- Initialised in Level 4 as alias `Orch_Chase01_Drama`, and assigned to region `M4_drama_region`; however, the mission (L4 M4) has a mission script typo that prevents the region from being called when it is supposed to be (at the Chief Wiggum race objective).
- Initialised in Level 7 as alias `Orch_Chase01_Drama`, and assigned to region `M7_drama_region`; however, the mission (L7 M7) has a mission script typo that prevents the region from being called when it is supposed to be (at the Alien Car escape objective).

### orch_chase01_drama_pickup_b3
- Initialised in Level 4 as alias `Orch_Chase01_Drama_Pickup`, and assigned to region `M4_drama_region`; however, the mission (L4 M4) has a mission script typo that prevents the region from being called when it is supposed to be (at the Chief Wiggum race objective).
- Initialised in Level 7 as alias `Orch_Chase01_Drama_Pickup`, and assigned to region `M7_drama_region`; however, the mission (L7 M7) has a mission script typo that prevents the region from being called when it is supposed to be (at the Alien Car escape objective).

### sunday_drive_intro
- Initialised in Level 5 as alias `Sunday_Drive_Intro`, but never assigned to any region.
  
---
