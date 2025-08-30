# UnusedVehicleSounds

## Unused sound resources
These sound resources exist and are linked to an RSD file, but are not assigned to any vehicle's sound setup.

 - A sound resource being unused does not inherently mean that the RSD file linked to it also is - other sound resources may still reference that RSD file.
 - At least some of the entries here from `carsound.spt` are false positives, and instructed to play by the game via hardcode.

Format: containing SPT file: sound resource name (linked RSD file)

 - `carsound.spt`: `ferrari` (`sound/carsound/cellcar.rsd`)
 - `carsound.spt`: `gearshift` (`sound/carsound/common/gearshft.rsd`)
 - `carsound.spt`: `car_jump` (`sound/carsound/car_jump_02.rsd`)
 - `carsound.spt`: `nuke_truck` (`sound/carsound/nuke_truck_02.rsd`)
 - `carsound.spt`: `amb_siren` (`sound/carsound/amb_siren.rsd`)
 - `carsound.spt`: `fire_siren` (`sound/carsound/fire_siren.rsd`)
 - `carsound.spt`: `klaxon` (`sound/carsound/fire_siren.rsd`)
 - `carsound.spt`: `dirt_skid` (`sound/carsound/common/dirt_skid.rsd`)
 - `carsound.spt`: `mission_ai_vehicle` (`sound/carsound/sportscarB.rsd`)
 - `cblbart.spt`: `cBlbart` (`sound/carsound/bartcar.rsd`)
 - `cblbart.spt`: `cBlbart_horn` (`sound/carsound/ferrini_horn.rsd`)
 - `cbone.spt`: `cBone_v_horn` (`sound/carsound/horn-truck02.rsd`)
 - `cfire_v.spt`: `cfirecar_horn` (`sound/carsound/fire_horn.rsd`)
 - `chears.spt`: `cHears_horn` (`sound/carsound/horn-hearse.rsd`)
 - `chears.spt`: `cHears_overlay` (`sound/carsound/siren.rsd`)
 - `cpolice.spt`: `cPolice_car_horn` (`sound/carsound/common/horn.rsd`)
 - `csedan.spt`: `cSedan_horn` (`sound/carsound/horn-horn06.rsd`)
 - `csedan.spt`: `cSedan_overlay` (`sound/carsound/siren.rsd`)
 - `glastruc.spt`: `glastruc_v_horn` (`sound/carsound/horn-truck02.rsd`)
 - `hbike_v.spt`: `hbike_horn` (`sound/carsound/horn-frink.rsd`)
 - `hbike_v.spt`: `hbike_skid` (`sound/carsound/frinkskid.rsd`)
 - `istruck.spt`: `istruck_horn` (`sound/carsound/horn-bmw.rsd`)
 - `mono_v.spt`: `mono_overlay` (`sound/carsound/monorail_car_overlay.rsd`)
 - `wiggu_v.spt`: `wiggum_horn` (`sound/carsound/common/horn.rsd`)
 
 ## Unused RSD files
 These RSD sound files are never referenced by any sound resource, and therefore never assigned to a vehicle's sound setup.
 Format: RSD file
 
 - `sound/carsound/common/smash.rsd`
 - `sound/carsound/common/thud.rsd`
 - `sound/carsound/homer/ferrari.rsd`
 - `sound/carsound/homer/snake202.rsd`
 - `sound/carsound/apu_car.rsd`
 - `sound/carsound/bat_loop.rsd`
 - `sound/carsound/beeman_enter_01.rsd`
 - `sound/carsound/bigbus.rsd`
 - `sound/carsound/bmw_horn.rsd`
 - `sound/carsound/book_fire.rsd`
 - `sound/carsound/book_van.rsd`
 - `sound/carsound/frinkbike.rsd`
 - `sound/carsound/garbage_truck.rsd`
 - `sound/carsound/generator.rsd`
 - `sound/carsound/generic01.rsd`
 - `sound/carsound/ghost_ship_overlay.rsd`
 - `sound/carsound/glow1.rsd`
 - `sound/carsound/gti_starter.rsd`
 - `sound/carsound/homer_car.rsd`
 - `sound/carsound/horn-broken.rsd`
 - `sound/carsound/horn-broken_02.rsd`
 - `sound/carsound/horn-clown.rsd`
 - `sound/carsound/horn-ghostboat.rsd`
 - `sound/carsound/horn-rocket.rsd`
 - `sound/carsound/horn-siren.rsd`
 - `sound/carsound/horn-vanagon.rsd`
 - `sound/carsound/hoverbike.rsd`
 - `sound/carsound/hoverbike3.rsd`
 - `sound/carsound/klaxxon.rsd`
 - `sound/carsound/kremlin.rsd`
 - `sound/carsound/loud_ice_cream_truck.rsd`
 - `sound/carsound/marge.rsd`
 - `sound/carsound/monorail_skid_02.rsd`
 - `sound/carsound/nuctruck_glow.rsd`
 - `sound/carsound/nuke_truck.rsd`
 - `sound/carsound/rocket.rsd`
 - `sound/carsound/rocket1.rsd`
 - `sound/carsound/rocket2.rsd`
 - `sound/carsound/rocket_car_01.rsd`
 - `sound/carsound/rocket_car_02.rsd`
 - `sound/carsound/rocket_car_05.rsd`
 - `sound/carsound/rocket_car_06.rsd`
 - `sound/carsound/scratchy.rsd`
 - `sound/carsound/siren_01.rsd`
 - `sound/carsound/skytrain_skid.rsd`
 - `sound/carsound/sputter.rsd`
 - `sound/carsound/startup.rsd`
 - `sound/carsound/steam.rsd`
 - `sound/carsound/suv.rsd`
 - `sound/carsound/swoosh1.rsd`
 - `sound/carsound/swoosh2.rsd`
 - `sound/carsound/taxi.rsd`

## Non-existent sound resources
Some vehicle sound setups make reference to sound resources that don't exist.
Format: containing SPT file: sound resource name

 - `famil_v.spt`/`skinn_v.spt`/`smith_v.spt`/`moe_v.spt`: `famil_open`
 - `famil_v.spt`/`skinn_v.spt`/`smith_v.spt`/`moe_v.spt`: `famil_close`
 - `huskA.spt`: `huskaV_horn`
 - `mono_v.spt`: `generator`
 - `tt.spt` : `tt`

#
