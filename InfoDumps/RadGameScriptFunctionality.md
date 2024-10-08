# RadGameScriptFunctionality
NOTE: There's always more to discover, and not everything is currently fully known or possibly presented the best. The point is to make information available and improve when I can over time.

Credit to Donut Team/community for years of information and tools, not just me.
Specific thanks to friends Borb and maz who have helped greatly with information and testing.

## Introduction

### What?
This document is about RadGameScript, an unofficial name to refer to the text-based function scripts used in the game to set up different things. These files apper to be UTF-8 encoded (if not plain ASCII) and any text editor should be able to handle them.

### Where?
This table assumes vanilla use cases; with mods things *can* be made different.
| Path | Usage |
| ---- | ----- |
| /scripts/cars/*.con | Vehicle statistics configuration for vehicle of internal name *. |
| /scripts/cars/*/.con | Vehicle statistics configuration for computer-controlled vehicles - loaded by set name in missions. |
| /scripts/missions/rewards.mfk | Unlockable vehicles/clothings setup, in addition to definition of Level Progress wasp/gag counts for each level. |
| /scripts/ss.mfk | Bonus Game load script. |
| /scripts/ssi.mfk | Bonus Game initialisation script. |
| /scripts/missions/level0#/level.mfk | Level # load script. |
| /scripts/missions/level0#/leveli.mfk | Level # initialisation script. |
| /scripts/missions/level0#/m#sdl.mfk | Level # Mission # Sunday Drive/pre-mission load script. |
| /scripts/missions/level0#/m#sdi.mfk | Level # Mission # Sunday Drive/pre-mission initialisation script. |
| /scripts/missions/level0#/m#l.mfk | Level # Mission # main mission load script. |
| /scripts/missions/level0#/m#i.mfk | Level # Mission # main mission initialisation script. |
| /scripts/missions/level0#/bm1l.mfk | Level # Bonus Mission load script. |
| /scripts/missions/level0#/bm1i.mfk | Level # Bonus Mission initialisation script. |
| /scripts/missions/level0#/sr#l.mfk | Level # Street Race # load script. |
| /scripts/missions/level0#/sr#i.mfk | Level # Street Race # initialisation script. |
| /scripts/missions/level0#/gr1l.mfk | Level # Wager Race load script. |
| /scripts/missions/level0#/gr1i.mfk | Level # Wager Race initialisation script. |
| /scripts/missions/level0#/demo.mfk | Level # demo load script. |
| /scripts/missions/level0#/demoi.mfk | Level # demo initialisation script. |
| /scripts/missions/level0#/d1l.mfk | Level # demo mission load script
| /scripts/missions/level0#/d1i.mfk | Level # demo mission initialisation script. |

Level load/setup scripts and Bonus Game load/setup scripts are the same thing, however less functions will have effect (because of the hardcoded nature of the Bonus Game, if nothing else).

Load scripts are mainly used to load files containing data for the relevant purpose and/or referenced by the accompanying initialisation script, which actually sets things up (by defining the gameplay of a mission, for example). Very few functions are incompatible when used in the opposite file, however it is best practice to put things where they should be.

Level # refers to any level. Street Race # refers to any Street Race (1-3). Mission # refers to any mission (0-8, where 0 is Level 1 Mission 0/Tutorial and 8 is a dummy/supported mission used to end some levels with cutscenes and tweaks).

All Story Missions have "Sunday Drive"/pre-mission segments, encompassing gameplay prior to the blue mission briefing screen. For example, in the pre-mission of Level 1 Mission 1 (S-M-R-T), Homer spawns outside the Simpson household, and his first (and only) task is to converse with Marge.

### How?
Scripts are just text lists of functions with arguments. Invalid syntax and argument use will often (but not always) lead to errors/crashes, however usage of non-existent functions is ignored. The syntax is based on C/C++ and is quite loose; see below for an example of valid script, with the exception that all functions do not exist in the game.

```
StartHere("Me");
SetMode(4); // Comment here!
  Timer(80);
  Fail("Timer", 0); EndFail();
  Fail("Jump",5); EndFail();
  FadeAtEnd(0.66);
  FadeAtEnd(0.65);
  DoSomeStuff(0, "", 1);
  DoSomeStuff("0", "", "1");
  DoOtherStuff(a,b,j);
EndHere();
```

Whitespace between functions/arguments doesn't usually matter (it is recommended to leave argument spaces at least with floating point/decimal point values), multiple functions can be on the same line, and repeat arguments (if repetition is unsupported) override each other, latest first.

Functions **must** be expressed as `FunctionName(Arg1,Arg2);` however - name, open bracket, arguments (subject to rules specified above), close bracket, semi-colon. Some functions are context-sensitive and cause errors/crashes if used in the wrong context.

This document will label each argument with a given type: **int** (integer, like 1; negative values accepted)/**float** (floating point, like 1.2)/**str** (like "THIS"). Some functions do not accept arguments and have one set effect.

## Functions and Arguments
The vanilla game supports **245** functions. The Donut Team/Lucas' Mod Launcher "Additional Script Functionality" (ASF) hack adds **71** extra functions (totalling **316** overall) whilst also altering the usage of **4** vanilla functions. If a function is added or changed by ASF, it will be noted in this document. Some vanilla game functions have no/broken effects but are still recognised as valid functions; this will also be noted. Most functions are optional in any given context - usage of "must" here assumes you want to use them and refers to the ideal function positioning relative to other functions, in those cases.

### SetMass
```
SetMass(float:Mass);
SetMass(1200);
```
Used in vehicle configurations.
Sets a vehicle's mass - how heavy it is.
Default is `1000.0`.

### SetGasScale
```
SetGasScale(float:GasScale);
SetGasScale(12.0);
```
Used in vehicle configurations.
Sets a vehicle's gas scale - the rate of standard acceleration.
Default is `4.0`.

### SetHighSpeedGasScale
```
SetHighSpeedGasScale(float:HighSpeedGasScale);
SetHighSpeedGasScale(24.0);
```
Used in vehicle configurations.
Sets a vehicle's high speed gas scale - the alternative rate of acceleration active whilst at higher speed.
Default is `2.0`.

### SetGasScaleSpeedThreshold
```
SetGasScaleSpeedThreshold(float:GasScaleSpeedThreshold);
SetGasScaleSpeedThreshold(0.81);
```
Used in vehicle configurations.
Sets a vehicle's speed threshold for alternating between the two main acceleration rates.
Typical/valid range is `0.0` to `1.0` (representing the vehicle's least and most speed with standard accelertion, respectively).
Default is `1.0`.

### SetSlipGasScale
```
SetSlipGasScale(float:SlipGasScale);
SetSlipGasScale(5.0);
```
Used in vehicle configurations.
Sets a vehicle's acceleration rate whilst spinning out/"slipping"/E-braking.
Default is `4.0`.

### SetBrakeScale
```
SetBrakeScale(float:BrakeScale);
SetBrakeScale(2.0);
```
Used in vehicle configurations.
Sets a vehicle's deceleration rate whilst braking.
Default is `3.0`.

### SetTopSpeedKmh
```
SetTopSpeedKmh(float:TopSpeedKmh);
SetTopSpeedKmh(95.5);
```
Used in vehicle configurations.
Sets a vehicle's top speed, in KM/H.
Default is `220.0`.

### SetMaxWheelTurnAngle
```
SetMaxWheelTurnAngle(float:MaxWheelTurnAngle);
SetMaxWheelTurnAngle(50.0);
```
Used in vehicle configurations.
Sets the maximum range with which a vehicle can steer horizontally.
Default is `35.0`.

### SetHighSpeedSteeringDrop
```
SetHighSpeedSteeringDrop(float:HighSpeedSteeringDrop);
SetHighSpeedSteeringDrop(5.0);
```
Used in vehicle configurations.
Sets a vehicle's steering impairment at high speed.
Default is `0.0`.

### SetTireGrip
```
SetTireGrip(float:TireGrip);
SetTireGrip(12.0);
```
Used in vehicle configurations.
Sets a vehicle's tire grip - grounded-ness.
Default is `4.0`.

### SetNormalSteering
```
SetNormalSteering(float:NormalSteering);
SetNormalSteering(15.0);
```
Used in vehicle configurations.
Sets a vehicle's steering capacity under normal circumstances.
Default is `110.0`.

### SetSlipSteering
```
SetSlipSteering(float:SlipSteering);
SetSlipSteering(150.0);
```
Used in vehicle configurations.
Sets a vehicle's steering capacity whilst spinning out/"slipping"/E-braking.
Default is `35.0`.

### SetEBrakeEffect
```
SetEBrakeEffect(float:EBrakeEffect);
SetEBrakeEffect(5.0);
```
Used in vehicle configurations.
Sets the severity of the effect of E-braking with a vehicle.
Default is `0.5`.

### SetCMOffsetX
```
SetCMOffsetX(float:CMOffsetX);
SetCMOffsetX(0.0);
```
Used in vehicle configurations.
Sets a vehicle's centre of mass X position offset - important for physics.
Default is `0.0`.

### SetCMOffsetY
```
SetCMOffsetY(float:CMOffsetY);
SetCMOffsetY(0.0);
```
Used in vehicle configurations.
Sets a vehicle's centre of mass Y position offset - important for physics.
Default is `0.0`.

### SetCMOffsetZ
```
SetCMOffsetZ(float:CMOffsetZ);
SetCMOffsetZ(0.0);
```
Used in vehicle configurations.
Sets a vehicle's centre of mass Z position offset - important for physics.
Default is `0.0`.

### SetSuspensionLimit
```
SetSuspensionLimit(float:SuspensionLimit);
SetSuspensionLimit(3.0);
```
Used in vehicle configurations.
Sets a vehicle's suspension limit - how much suspension is applied.
Default is `0.4`.

### SetSpringK
```
SetSpringK(float:SpringK);
SetSpringK(2.0);
```
Used in vehicle configurations.
Sets vehicle Spring K; higher values make the vehicle stiffer.
Default is `0.5`.

### SetDamperC
```
SetDamperC(float:DamperC);
SetDamperC(12.0);
```
Used in vehicle configurations.
Sets vehicle damping coefficient; higher values make the vehicle less bouncy.
Default is `0.2`.

### SetSuspensionYOffset
```
SetSuspensionYOffset(float:SuspensionYOffset);
SetSuspensionYOffset(1.0);
```
Used in vehicle configurations.
Sets a vehicle's wheels' Y position offset for suspension.
Default is `0.0`.

### SetHitPoints
```
SetHitPoints(float:HitPoints);
SetHitPoints(4.0);
```
Used in vehicle configurations.
Sets a vehicle's health.
Default is `2.0`.

### SetBurnoutRange
```
SetBurnoutRange(float:BurnoutRange);
SetBurnoutRange(0.9);
```
Used in vehicle configurations.
Sets a vehicle's burnout range. ~~ADDYNOKNOW~~
Default is `0.3`.

### SetMaxSpeedBurstTime
```
SetMaxSpeedBurstTime(float:MaxSpeedBurstTime);
SetMaxSpeedBurstTime(2.0);
```
Used in vehicle configurations.
Sets the amount of seconds of speed boost a vehicle gets when using burnout.
Default is `1.0`.

### SetDonutTorque
```
SetDonutTorque(float:DonutTorque);
SetDonutTorque(1.55);
```
Used in vehicle configurations.
Sets a vehicle's "spin-in-circle" ability/shape wide-ness.
Default is `10.0`.

### SetSlipSteeringNoEBrake
```
SetSlipSteeringNoEBrake(float:SlipSteeringNoEBrake);
SetSlipSteeringNoEBrake(45.0);
```
Used in vehicle configurations.
Sets a vehicle's steering ability whilst slipping without E-brake use.
Default is `50.0`.

### SetSlipEffectNoEBrake
```
SetSlipEffectNoEBrake(float:SlipEffectNoEBrake);
SetSlipEffectNoEBrake(12.0);
```
Used in vehicle configurations.
Sets the vehicle's slipping effect without E-brake use.
Default is `0.1`.

### SetWeebleOffset
```
SetWeebleOffset(float:WeebleOffset);
SetWeebleOffset(-0.2);
```
Used in vehicle configurations.
Set the vehicle's weeble offset.
This is applied in addition to **SetCMOffsetY** whilst in the air in order to make the vehicle more (negative) or less (positive) stable.
Default is `-1.0`.

### SetWheelieRange
```
SetWheelieRange(float:WheelieRange);
SetWheelieRange(0.5);
```
Used in vehicle configurations.
Set a vehicle's required speed to make a wheelie happen.
Default is `0.0`.

### SetWheelieOffsetY
```
SetWheelieOffsetY(float:WheelieOffsetY);
SetWheelieOffsetY(0.5);
```
Used in vehicle configurations.
Set a vehicle's centre of mass Y offset position when in a wheelie.
Default is `0.0`.

### SetWheelieOffsetZ
```
SetWheelieOffsetZ(float:WheelieOffseZ);
SetWheelieOffsetZ(-0.5);
```
Used in vehicle configurations.
Set a vehicle's centre of mass Z offset position when in a wheelie.
Default is `0.0`.

### SetShadowAdjustments
```
SetShadowAdjustments(float:FrontX, float:FrontY, float:MiddleFrontX, float:MiddleFrontY, float:MiddleBackX, float:MiddleBackY, float:BackX, float:BackY);
SetShadowAdjustments(1, 2, 3, 4, 5, 6, 7, 8)
```
Used in vehicle configurations.
Sets the vehicle's shadow position offsets for different vehicle-relative points, as seen in the argument names.
Default is `0`,`0`,`0`,`0`,`0`,`0`,`0`,`0`.

### SetShininess
```
SetShininess(float:Shininess)
SetShininess(5.0);
```
Used in vehicle configurations.
Sets a vehicle's shine effect severity.
Default is `0.251`.

### SetDriver
```
SetDriver(str:Driver);
SetDriver("moleman");
```
Used in vehicle configurations.
Sets a vehicle's driver by their internal character name.
If set to `none`, there is an invisible/traffic driver in the driver's seat.
If set to `phantom`, there is no driver and the player takes the driver's seat.
Otherwise, is set to a character internal name to use as a driver when the vehicle is called from a Phone Booth (via the **BindReward** function) or used as a level default vehicle (via the **InitLevelPlayerVehicle** function), so long as that character driver is not suppressed in the active level via the **SuppressDriver** function.
If the vehicle is being set as a mission forced car via the **InitLevelPlayerVehicle** function, the **SetDriver** function is honoured *even when* the character driver is suppressed in the active level via the **SuppressDriver** function.
Mission AI vehicles ignore **SetDriver** and use of it prevents vanilla mission-set drivers (via the **AddStageVehicle**/**MoveStageVehicle**/**ActivateVehicle** functions) from working. ~~ADDYNOKNOW~~ Any others besides those two? AddDriver/RemoveDriver outside of that? What about ASF functions?
Bonus Game AI vehicles do something. ~~ADDYNOKNOW~~
Default is `phantom`.

### SetGamblingOdds
```
SetGamblingOdds(float:GamblingOdds);
SetGamblingOdds(2);
```
Used in vehicle configurations.
Sets a vehicle's assigned Wager Race difficulty level/thus payout.
If set to a value below `2.0`, gives EASY difficulty/2x payout..
If set to a value of at least `2.0` but below `3.0`, gives NORMAL difficulty/3x payout..
If set to a value of at least `3.0` or above, gives HARD difficulty/4x payout.
Default is `1.0`.

### SetHasDoors
```
SetHasDoors(int:HasDoors);
SetHasDoors(1);
```
Used in vehicle configurations.
Sets if or not a vehicle's door/associated animations are used on entry/exit.
If set to `0`, a different, door-less animation plays.
If set to `1`, the door animations play.
Neither animation mode is used if the same vehicle calls `SetIrisTransition` with an argument/value of `1`.
Default is `1`.

### SetCharactersVisible
```
SetCharactersVisible(int:CharactersVisible);
SetCharactersVisible(1);
```
Used in vehicle configurations.
Sets the visibility of the vanilla set player/driver characters.
If set to `0`, characters are invisible whilst in the vehicle.
If set to `1`, characters are visible whilst in the vehicle.
~~ADDYNOKNOW~~ Effects both really?
Default is `1`.

### SetIrisTransition
```
SetIrisTransition(int:IrisTransition);
SetIrisTransition(0);
```
Used in vehicle configurations.
Sets if or not the iris wipe + teleport effect is used to enter/exit the vehicle.
If set to `0`, the iris wipe is disabled and entry/exit animations are used.
If set to `1`, the iris wipe is enabled and entry/exit animations are unused.
Default is `0`.

### SetAllowSeatSlide
```
SetAllowSeatSlide(int:AllowSeatSlide);
SetAllowSeatSlide(1);
```
Used in vehicle configurations.
Sets if or not the player character can slide into the driver's seat (from the passenger seat side) on vehicle entry.
If set to `0`, they cannot.
If set to `1`, they can.
Default is `1`.

### SetHighRoof
```
SetHighRoof(int:HighRoof);
SetHighRoof(0);
```
Used in vehicle configurations.
Sets if or not the vehicle's roof is considered high or non-existent.
If set to `0`, Marge's hair gets forcibly bent over whilst in the vehicle.
If set to `1`, Marge's hair is left as usual whilst in the vehicle.
Default is `0`.
By default works for all `m_` characters; Custom Character Support hack's `IsMarge` toggle can also make characters arbitrarily compatible.

### SetCharacterScale
```
SetCharacterScale(float:CharacterScale);
SetCharacterScale(1.2);
```
Used in vehicle configurations.
Sets the scale of the player and driver characters whilst in the vehicle.
~~ADDYNOKNOW~~ Effects both really?
Default is `1.0`.

### SuppressDriver
```
SuppressDriver(str:Driver);
SuppressDriver("bart");
```
Used in level/mission load/initialisation scripts.
Adds the driver character specified as `str:Driver` (internal name) to the level's suppressed drivers list; that character cannot appear as a driver in any player-controlled vehicles (via level default or Phone Booth) in the given level. Forced vehicles in forced car missions are excluded from this, and the driver will appear; same if ASF functions are used to selectively override this function at different points.
There is a limit of thirty-two concurrently suppressed drivers. There is no way to unsuppress a driver aside from exiting the level (if added in a level script) or fully reloading the level (if added in a mission script). ~~ADDYNOKNOW~~ Level reload works or mission ones? Do they independantly unsuppress?

### InitLevelPlayerVehicle
```
InitLevelPlayerVehicle(str:Vehicle, str:Locator, str:Type, str:CON);
InitLevelPlayerVehicle("famil_v","level1_carstart","DEFAULT");
InitLevelPlayerVehicle("marge_v","m6_carstart","OTHER");
InitLevelPlayerVehicle("tt","newlocator","AI","custom\notrubbish.con");
```
Used in level/mission initialisation scripts.
If used in a level initialisation script, sets the level's default vehicle.
If used in a mission initialisation script, sets up a forced car. Must be used alongside the **SetForcedCar** function and be called between **SelectMission** and **CloseMission**.
The *Vehicle* argument is the vehicle's internal name. The vehicle should be loaded.
The *Locator* argument specifies a Locator Type 3 which is used to position the level's default vehicle if a forced car mission is cancelled (if called in a level initialisation script) or to place the mission's forced vehicle on at the start of the mission, overwriting the **SetMissionResetPlayerOutCar**/**SetMissionResetPlayerInCar** functions (if called in a mission initialisation script). The locator should be loaded. ~~ADDYNOKNOW~~ Does it overwrite?
The *Type* argument specifies vehicle type:
- `DEFAULT` for level default vehicle;
- `OTHER` for forced vehicle;
- `AI` to act like a player-controllable AI vehicle; ~~ADDYNOKNOW~~
- `CHASE` to act like ?; ~~ADDYNOKNOW~~

The *CON* Argument optionally provides a filepath (rooted in "/scripts/cars/") to use as a vehicle configuration file for the vehicle. This defaults to the value given to the *Vehicle* argument with ".con" at the end.

### PlacePlayerCar
```
PlacePlayerCar(str:Vehicle, str:Locator);
PlacePlayerCar("current", "race_carstart");
```
Used in mission initialisation scripts.
Must be called between **SelectMission** and **CloseMission**.
Teleports the player's vehicle (specified by *Vehicle*) to a Locator Type 3 (specified by *Locator*). The locator should be loaded. **This occurs at the very start of the mission, overwriting the SetMissionResetPlayerOutCar/SetMissionResetPlayerInCar/InitLevelPlayerVehicle functions. *Vehicle* may be set to `current` to target the most recently set/used player vehicle, or alternatively to a specific vehicle name, so long as the vehicle is loaded and player-controllable. ~~ADDYNOKNOW~~ Does override ILPV?

### AddPurchaseCarReward
```
AddPurchaseCarReward(str:Type, str:NPC, str:AnimationSet, str:NPCLocator, float:NPCActionRadius, str:CarLocator);
AddPurchaseCarReward("gil", "gil", "gil_spot", 1.0, "car_buy_spot");
AddPurchaseCarReward("simpson", "barney", "barney_spot", 0.5, "plow_king_got");
```
Used in level initialisation scripts.
Adds a vehicle vendor to a level. There are two types and there can be one vendor for each.
The vehicle vendor type is set by *Type*:
- `gil` is Gil, with no conversation but instead a "w_carbuy" dialogue entry on converse;
- `simpson` is any other character, with a hardcoded/CustomShopSupport-set conversation on converse;

The vendor NPC is set by character internal name via `NPC`. They will animate using the animation set specified by `AnimationSet` and spawn on the Locator Type 3 specified by `NPCLocator`, which should be loaded.
The spherical radius within which conversation/ACTION pressing to interact with the vendor is possible is set by `NPCActionRadius`, and centred on the NPC's character model.
If a vehicle is purchased from the NPC, it will spawn on the Locator Type 3 specified by `CarLocator`, replacing the formerly current player vehicle. This locator should be loaded.

### SetPostLevelFMV
```
SetPostLevelFMV(str:RMV);
SetPostLevelFMV("fmv1a.rmv");
```
Used in level initialisation scripts.
In theory, sets the name (*RMV*, rooted in "/movies/") of a movie file to play on level completion.
Doesn't seem to do anything in practice.

### CreatePedGroup
```
CreatePedGroup(int:ID);
CreatePedGroup(0);
```
Used in level initialisation scripts.
Begins the definition of a pedestrian group of index *ID*. Each level can have ten pedestrian groups (0-9).

### AddPed
```
AddPed(str:Character, int:Amount);
AddPed("joger1", 1);
```
Used in level initialisation scripts.
Adds a pedestrian character to an implied pedestrian group - must be called between **CreatePedGroup** and **ClosePedGroup**.
Set *Character* to the character's internal name. Set *Amount* to the amount that should be active at once. Each pedestrian group has seven "active pedestrian" slots, which all need to be filled, and any given pedestrian can appear more than once. **The sum of all AddPed calls' second argument should be seven within a single pedestrian group.** So, for example, the group could have seven unique characters, or three characters (two who appear twice and one who appears once), or so forth.

### ClosePedGroup
```
ClosePedGroup();
ClosePedGroup();
```
Used in level initialisation scripts.
Ends the definition of a pedestrian group.

### UsePedGroup
```
UsePedGroup(int:ID);
UsePedGroup(0);
```
Used in mission initialisation scripts.
Sets a pedestrian group within the level by index (*ID*) to set as active when the containing Sunday Drive/main mission segment is warped to (either via Main Menu or Mission Select). This pedestrian group should exist.

### BindReward
```
BindReward(str:InternalName, str:FilePath, str:Type, str:Condition, int:Level, int:CoinPrice, str:VendorType);
BindReward("famil_v", "art\cars\famil_v.p3d", "car", "defaultcar", 1);
BindReward("cDuff", "art\cars\cDuff.p3d", "car", "forsale", 1, 125, "gil")
BindReward("homer", "art\chars\homer_m.p3d", "skin", "defaultskin", 1);
BindReward("h_fat", "art\chars\h_fat_m.p3d", "skin", "forsale", 1, 100, "interior");
```
Used in the rewards script.
Adds a reward to a level (either a Phone Booth vehicle or a interior shop Clothing).
*InternalName* sets the internal vehicle/clothing name of the reward.
*FilePath* provides the filepath to the reward's P3D file, rooted in the game's root directory.
*Type* sets the reward type - `car` for vehicles or `skin` for clothing.
*Condition* sets the unlock condition:
- `defaultcar` unlocks the vehicle if the level is unlocked and accessed;
- `defaultskin` unlocks the skin if the vehicle is unlocked and an alternative clothing is worn on shop acces;
- `forsale` allows the vehicle/clothing to be unlocked by purchase from a vendor - see below;
- `bonusmission` unlocks the vehicle if the level Bonus Mission is completed - cannot be used for clothing;
- `streetrace` unlocks the vehicle if the level's three Street Races are completed - cannot be used for clothing;
- `cards` unlocks the vehicle if all seven level Collector Cards have been found and the game is reloaded. Cannot be used for clothing. ~~ADDYNOKNOW~~

*Level* sets the level ID (1-7) that the reward is assigned to.
*CoinPrice* sets the coin cost for a reward with a `Condition` of `forsale`.
*VendorType* sets the vendor that sells the reward:
- `gil` for the level's Gil character for vehicles;
- `simpson` for the level's unique character for vehicles;
- `interior` for clothing;

Definition of no/incorrect rewards leads to crashes on entering the Phone Booth/interior shops.
A reward can only be assigned once - subsequent call attempts are ignored (as opposed to most other functions where later calls override the prior ones).

### CreateTrafficGroup
```
CreateTrafficGroup(int: ID);
CreateTrafficGroup(0);
```
Used in level initialisation scripts.
Begins definition of the level traffic group specified by *ID*. Each level only has one traffic group, `0`, unless the Custom Traffic Support hack is in use, in which case other traffic groups can be made and accessed.

### AddTrafficModel
```
AddTrafficModel(str:Vehicle, int:Amount, int:DisableParkedAppearances);
AddTrafficModel("sportsB", 2, 0);
AddTrafficModel("IStruck", 1, 1);
```
Used in level initialisation scripts.
Add a (loaded) traffic vehicle by internal name (*Vehicle*) to an implied traffic group - must be called between **CreateTrafficGroup** and **CloseTrafficGroup**.
*Amount* sets the amount that are allocated to the "road traffic" pool at once - this pool is shared by all traffic vehicles in the group and has a capacity of five; the sum of all **AddTrafficModel** calls' second arguments should be 5. So, there could be two vehicles that appear twice, and one that appears once. The valid range is 0-5.
*DisableParkedAppearances*, if set to `1`, prevents the vehicle from randomly spawning at the level's preset "parked traffic vehicle" locators.
A traffic vehicle can be made parked-spot-only by setting both *Amount* and *DisableParkedAppearances* to `0`.

### CloseTrafficGroup
```
CloseTrafficGroup();
CloseTrafficGroup();
```
Used in level initialisation scripts.
Ends the definition of a traffic group.

### SetCarAttributes
```
SetCarAttributes(str:Vehicle, float:TopSpeed, float:Acceleration, float:Toughness, float:Handling);
SetCarAttributes("tt", 4, 0.5, 1.5, 5);
```
Used in the rewards script.
Set the Phone Booth/vendor star counts for a vehicle (specified as *Vehicle*) in order: *TopSpeed*, *Acceleration*, *Toughness*, and *Handling*.
A vehicle can have 1-5 stars, and half-stars are supported (example: 2.5 = two-and-a-half stars).
If a vehicle this function is *not* called for is viewed in the Phone Booth, it will either default to no stars for every category or copy those from the last viewed vehicle in the Phone Booth.

### SetTotalGags
```
SetTotalGags(int:Level, int:GagCount);
SetTotalGags(5, 6);
```
Used in the rewards script.
Set the number of total Gags counted (*GagCount*) in a level's (*Level*) Level Progress screen.

### SetTotalWasps
```
SetTotalWasps(int:Level, int:WaspCount);
SetTotalWasps(7, 20);
```
Used in the rewards script.
Set the number of total Wasps counted (*WaspCount*) in a level's (*Level*) Level Progress screen.

### AddGlobalProp
```
AddGlobalProp(str:Prop);
AddGlobalProp("abcdef");
```
Used in level initialisation scripts.
Adds a prop name to the global table of prop names in theory.

### CreateChaseManager
```
CreateChaseManager(str:Vehicle, str:CON, int:SpawnRate);
CreateChaseManager("cPolice", "AIL1cops.con", 2);
```
Used in level initialisation scripts.
Sets up the "Hit & Run!" chase vehicle.
*Vehicle* should be the vehicle's internal name, and loaded.
*CON* optionally gives a path to a configuration file to use (rooted in "/scripts/cars/") - defaults to the argument for *Vehicle* with ".con" at the end.
*SpawnRate* optionally sets the chase vehicle's spawn rate; only relevant if there will be more than one active at once via other functions such as **SetNumChaseCars** and **SetStageNumChaseCars**.
If this function is ommitted, getting "Hit & Run!" is impossible. ~~ADDYNOKNOW~~

### DisableHitAndRun
```
DisableHitAndRun();
DisableHitAndRun();
```
Used in mission initialisation scripts.
Must be called between **AddStage** and **CloseStage**.
Enforces two effects for the duration of the stage/objective:
- The "Hit & Run!" meter stays at 0 at all times;
- Regular props do not give coins when hit;

If an interior is entered whilst the effects are active, they deactivate.

### EnableHitAndRun
```
EnableHitAndRun();
EnableHitAndRun();
```
Used in mission initialisation scripts.
Must be called between calls to **AddStage** and **CloseStage**.
In theory enables the "Hit & Run!" system.
Doesn't seem to do anything, even if used in the same stage as **DisableHitAndRun**.

### SetHitAndRunMeter
```
SetHitAndRunMeter(float:Fill);
SetHitAndRunMeter(50.0);
```
Used in mission initialisation scripts.
Must be called between calls to **AddStage** and **CloseStage**.
In theory sets the fill level of the "Hit & Run" meter.
Doesn't seem to do anything.

### SetNumChaseCars
```
SetNumChaseCars(int:Amount);
SetNumChaseCars(2);
```
Used in level initialisation scripts.
Sets the amount of active "Hit & Run!" police chasers in the level. Valid range is 0-5 (values above three can lead to crashes). If set to zero, there's still a "Hit & Run!", but no chase. ~~ADDYNOKNOW~~ The default is 1. ~~ADDYNOKNOW~~

### SetChaseSpawnRate
```
SetChaseSpawnRate(str:Vehicle, int:Rate);
SetChaseSpawnRate("cPolice", 2);
```
Used in mission initialisation scripts.
Must be called between calls to **AddStage** and **CloseStage**.
Sets the spawn rate (*Rate*) for *Vehicle* (internal name), which should be the level "Hit & Run!" chaser vehicle.

### KillAllChaseAI
```
KillAllChaseAI(str:Vehicle);
KillAllChaseAI("cPolice");
```
Used in mission initialisation scripts.
Must be called between calls to **AddStage** and **CloseStage**.
Must be used with the level "Hit & Run!" chaser vehicle as parameter *Vehicle* (internal name).
Doesn't seem to do anything.

### ResetHitAndRun
```
ResetHitAndRun();
ResetHitAndRun();
```
Unknown context.
In theory resets the "Hit & Run!" meter or system.
Doesn't seem to do anything.

### SetHitAndRunDecay
```
SetHitAndRunDecay(float:Decay);
SetHitAndRunDecay(5);
```
Used in level initialisation scripts.
Set the amount to change the "Hit & Run!" meter by per second whilst in "decay"/emptying, via *Decay*. Relevant values range from -100.0 (fill meter immediately) to 0 (no change) to 100.0 (empty meter immediately).

### SetHitAndRunDecayInterior
```
SetHitAndRunDecayInterior(float:Decay);
SetHitAndRunDecayInterior(20);
```
Used in level initialisation scripts. Changed by ASF.
This function exists both in the vanilla game and as an ASF-altered function.
In the vanilla game, this function is a (seemingly-broken) alias for the **KillAllChaseAI** function.
With ASF active, *Decay* sets the amount to change the "Hit & Run!" meter by per second whilst in an interior. Relevant values range from -100.0 (fill meter immediately) to 0 (no change) to 100.0 (empty meter immediately). ~~ADDYNOKNOW~~

### AddMission
```
AddMission(str:ID);
AddMission("m1");
```
Used in level load scripts.
Add a mission (*ID*) to a level. ~~ADDYNOKNOW~~
Valid mission IDs include `m0` (Level 1 only), `m1`, `m2`, `m3`, `m4`, `m5`, `m6`, `m7`, and `d1`.

### AddBonusMission
```
AddBonusMission(str:ID);
AddBonusMission("bm1");
```
Used in level load scripts.
Add a bonus/side mission to a level. ~~ADDYNOKNOW~~
Valid bonus/side mission IDs include `bm1` (Bonus Mission), `sr1`, `sr2`, `sr3` (Street Races 1-3), `gr1` (Wager Race), and `ismovie` (hardcode for the Bonus Movie/setup ~~ADDYNOKNOW~~).

### SetMissionNameIndex
```
SetMissionNameIndex(str:Index);
SetMissionNameIndex("MISSION_TITLE_L1_M1");
```
Used in mission initialisation scripts.
Must be called between calls to **SelectMission** and **CloseMission**.
In theory sets the textbible index for the mission's title string.
In practice seems to do nothing.

### SelectMission
```
SelectMission(str:ID);
SelectMission("m1sd");
```
Used in mission initialisation scripts.
Begins the definition of a mission segment (either Sunday Drive/pre-mission or main).
Confirm the mission identity/ID of the script. If this doesn't match the file the game is opening, infinite loading screens can occur.
Valid mission IDs include `m0sd`, `m0` (Level 1 only), `m1sd`, `m1`, `m2sd`, `m2`, `m3sd`, `m3`, `m4sd`, `m4`, `m5sd`, `m5`, `m6sd`, `m6`, `m7sd`, `m7`, `bm1`, `sr1`, `sr2`, `sr3`, `gr1`, and `d1`.

### SetMissionResetPlayerInCar
```
SetMissionResetPlayerInCar(str:Locator);
SetMissionResetPlayerInCar("level1_carstart");
```
Used in mission initialisation scripts.
Must be called between **SelectMission** and **CloseMission**.
Sets up the mission so that upon warping via Main Menu/Mission Select, or restarting manually or via mission fail, the player will be in their vehicle, and their vehicle will be positioned on the Locator Type 3 *Locator* (which should be loaded).
Overwritten in missions which use the **InitLevelPlayerVehicle* function. ~~ADDYNOKNOW~~

### SetMissionResetPlayerOutCar
```
SetMissionResetPlayerOutCar(str:PlayerLocator, str:VehicleLocator);
SetMissionResetPlayerOutCar("m2_homer_start","level1_carstart");
```
Used in mission initialisation scripts.
Must be called between **SelectMission** and **CloseMission**.
Sets up the mission so that upon warping via Main Menu/Mission Select, or restarting manually or via mission fail, the player will be out of their vehicle (positioned on the (loaded) Locator Type 3 *PlayerLocator*) and their vehicle will be positioned on the (loaded) Locator Type 3 *VehicleLocator*.
Overwritten in missions which use the **InitLevelPlayerVehicle** function. ~~ADDYNOKNOW~~

### SetDynaLoadData
```
SetDynaLoadData(str:DynaLoadDataString, str:Interior);
SetDynaLoadData("l1z1.p3d;l1r1.p3d;l1r7.p3d;");
```
Used in mission initialisation scripts.
Must be called between **SelectMission** and **CloseMission**.
Uses *DynaLoadDataString* when the mission is warped to/restarted to load required "regions"/map chunks (and possibly perform other world tasks). At least one region must be loaded for a mission not to either crash or infinitely load.
See the "Specific notes" -> "Dyna Load Data String format" section later for more information.
The argument *Interior* optionally provides the name of an interior's internal name, if the previously given Dyna Load Data String loads one.

### AddBonusObjective
```
AddBonusObjective(str:Type, int:Parameter);
AddBonusObjective("time", 10000);
AddBonusObjective("position", 1);
AddBonusObjective("no_damage");
AddBonusObjective("no_harass");
```
Used in mission initialisation scripts.
Must be called between **SelectMission** and **CloseMission**.
Adds a bonus objective to the mission.
These are mostly broken/unfinished, but the save file *does* track them.
Each mission can only have one bonus objective, with a complete/not flag.
The bonus objective completion is only measured for the stage in the mission that contains a call to **SetBonusMissionStart**, if any.
*Type* sets the type:
- `time` theoretically requires completing the objective within or with so much time (*Parameter*) remaining on the stage timer, but in practice seems to always get set to complete;
- `position` requires the player to win with a position in a `race` objective - the only effectively valid *Parameter* is `1`;
- `no_damage` theoretically requires the player to avoid taking vehicle damage, but in practice seems to always get set to incomplete;
- `no_harass` theoretically requires the player to avoid getting a "Hit & Run!" (or avoid putting fill into the meter), but in practice seems to always get set to incomplete;

### SetForcedCar
```
SetForcedCar();
SetForcedCar();
```
Used in mission initialisation scripts.
Must be called between **SelectMission** and **CloseMission**.
Enforce the mission as a forced vehicle mission and remove usable Phone Booths from the world - must be used with **InitLevelPlayerVehicle** to avoid crashes.

### CloseMission
```
CloseMission();
CloseMission();
```
Used in mission initialisation scripts.
Ends the definition of a mission segment (Sunday Drive/pre-mission or main).

### SetDemoLoopTime
```
SetDemoLoopTime(int:Time);
SetDemoLoopTime(60);
```
Used in mission initialisation scripts.
Must be called between calls to **AddStage** and **CloseStage**.
In theory sets the amount of *Time* unused demo mode missions run for.
In practice seems to do nothing.

### StreetRacePropsLoad
```
StreetRacePropsLoad(str:DynaLoadDataString);
StreetRacePropsLoad("l1m7_door.p3d;")
```
Used in mission initialisation scripts.
Must be called between **SelectMission** and **CloseMission**.
Executes a Dyna Load Data string when the mission starts, if valid.
See the "Specific notes" -> "Dyna Load Data String format" section later for more information.

### StreetRacePropsUnload
```
StreetRacePropsUnload(str:DynaLoadDataString);
StreetRacePropsUnload("l1m7_door.p3d:")
```
Used in mission initialisation scripts.
Must be called between **SelectMission** and **CloseMission**.
Executes a Dyna Load Data string when the mission completes or cancels, if valid.
See the "Specific notes" -> "Dyna Load Data String format" section later for more information.

### UseElapsedTime
```
UseElapsedTime();
UseElapsedTime();
```
Used in mission initialisation scripts.
Must be called between **AddStage** and **CloseStage**.
Makes the stage timer (if present) count up instead of down.
~~ADDYNOKNOW~~

### AttachStatePropCollectible
```
AttachStatePropCollectible(str:Vehicle, str:StatePropCollectible);
AttachStatePropCollectible("snake_v", "bombbarrel");
```
Used in mission initialisation scripts.
Must be called between **AddStage** and **CloseStage**.
Makes it so that *Vehicle* is carrying *StatePropCollectible* on stage/objective reach. *Vehicle* cannot be `current` and must be an `OTHER`-type vehicle.
Does not work when ASF is enabled, but not counted here as an altered function. ~~ADDYNOKNOW~~

### ShowHUD
```
ShowHUD(int:HUD);
ShowHUD(1);
```
Used in mission initialisation scripts.
Must be called between **SelectMission** and **CloseMission**.
Disables the HUD display (ingame interface) if set to `0`.
~~ADDYNOKNOW~~

### SetNumValidFailureHints
```
SetNumValidFailureHints(int:MaxHintNum);
SetNumValidFailureHints(3);
```
Used in mission initialisation scripts.
Must be called between **SelectMission** and **CloseMission**.
*MaxHintNum* must be a number between 1 and 8 inclusively.
This is used to limit the number of mission fail hints randomly shown, regardless of condition. Each mission has eight hints, indexed as zero through to seven in the textbible.
So, if called with a parameter of 3, hints 1-3 (0-2 in the textbible) will be allowed to appear, but not hints 4-8/2-7.
If set to zero, the game will crash on mission failure.

### AddStage
```
AddStage(str:SpecialType, str:LockedType, str:LockedCondition);
AddStage();
AddStage("final");
AddStage("locked", "car", "plowk_v");
AddStage("locked", "skin", "b_football");
```
Used in mission initialisation scripts. Can be repeated.
Must be called between **SelectMission** and **CloseMission**.
Adds a stage to a mission segment. Mission segments need at least one stage. Every stage needs at least one objective, composed at least of a valid **AddObjective**/**CloseObjective** pair (inclusive of other functions if required).
Arguments are entirely optional.
*SpecialType*, if present and valid, gives the stage special properties:
- `final` does the "MISSION COMPLETE" routine when the stage completes, and marks the mission as complete on the save data (if in the main segment);
- `locked` will auto-complete/skip over the stage/objective on reach only if the conditions set by *LockedType* and *LockedCondition* are met; if they are not, the stage will not feature a HUD icon, and a big message box featuring the textbible "INGAME_MESSAGE_#" entry for the ID called by **SetStageMessageIndex** in the stage (if present) will display on stage completion;

*LockedType* can be `car` (a vehicle is required to skip) or `skin` (a clothing is required to skip).
*LockedCondition* specifies the internal name of the vehicle/clothing the player must currently be using to skip.

### SetStageMessageIndex
```
SetStageMessageIndex(int:StageMessageIndex);
SetStageMessageIndex(0);
```
Used in mission initialisation scripts.
Must be used between calls to **AddStage** and **CloseStage**.
Sets the current stage/objective's task message, shown on reach and in the pause menu. Specify by numeric ID (*StageMessageIndex*) in the textbible, where the strings are named as "MISSION_OBJECTIVE_#".

### SetStageTime
```
SetStageTime(int:Seconds);
SetStageTime(45);
```
Used in mission initialisation scripts.
Must be used between calls to **AddStage** and **CloseStage**.
Adds a timer to the stage, and forcibly sets it to the given number of *Seconds*.
If the stage features a call to **StartCountdown**, *Seconds* will be +1.

### AddStageTime
```
AddStageTime(int:Seconds);
AddStageTime(15);
```
Used in mission initialisation scripts.
Must be used between calls to **AddStage** and **CloseStage**.
Adds a timer to the stage, and sets it to remaining time from the previous stage's timer (if there was one) + the given number of *Seconds*.
If the stage features a call to **StartCountdown**, an extra second is added.
If *Seconds* is `0`, one second is added.
If *Seconds* is a negative value like `-1`, no seconds are added.
~~ADDYNOKNOW~~

### AddStageVehicle
```
AddStageVehicle(str:Vehicle, str:Locator, str:Behaviour, str:CON, str:Driver);
AddStageVehicle("bart_v", "m6_bart_begins", "NULL", "AI\M6bart.con", "bart");
AddStageVehicle("cCellA", "m6_cell_ram", "chase");
```
Used in mission initialisation scripts. Can be repeated.
Must be used between calls to **AddStage** and **CloseStage**.
Adds a (loaded) AI vehicle by internal name (*Vehicle*) to the world, positioned at a locator Type 3 (*Locator*). This vehicle can be accessed by other relevant stage functions later, such as **SetVehicleAIParams**.
*Behaviour* sets the AI type. See the later section "Specific notes" -> "AI vehicle behaviours".
*CON* optionally assigns a CON filepath to use for vehicle configuration, rooted in "/scripts/cars/". Defaults to the argument for *Vehicle* with ".con" at the end. The CON a vehicle is first created with stays assigned that way for the rest of the mission, and attempts to change it via later function calls will be ignored.
*Driver* optionally gives the vehicle a driver character by internal name - if the vehicle's CON contains the **SetDriver** function, neither that nor this will work. If a vehicle with a driver is destroyed in gameplay and the sme vehicle is re-added later through this/similar functions, the driver will not be present.
Vehicle radar icon visibility and pointed-to-ness varies depending upon the active stage/objective type and number of vehicles active.
Up to four vehicles can be active in a stage at once, or five if all have `chase` behaviour.
Only so many unique vehicles can be added/activated per-mission; if the limit is exceeded the game will throw errors and crash.
~~ADDYNOKNOW~~ AddDriver/RemoveDriver stuff.

### MoveStageVehicle
```
MoveStageVehicle(str:Vehicle, str:Locator, str:Behaviour, str:Driver);
MoveStageVehicle("cBone", "", "chase");
```
Used in mission initialisation scripts. Can be repeated.
Must be used between calls to **AddStage** and **CloseStage**.
This function seems identical to the **ActivateVehicle** function seen below; read there. Exceptions:
- `NULL`/blank is not accepted for *Locator*;
- Prior to the stage which calls the function, the driver (is specified by it) spawns floating at *Locator* without the vehicle;

Repeatable for multiple vehicles.

### ActivateVehicle
```
ActivateVehicle(str:Vehicle, str:Locator, str:Behaviour, str:Driver);
ActivateVehicle("skinn_v", "NULL", "race");
```
Used in mission initialisation scripts. Can be repeated.
Must be used between calls to **AddStage** and **CloseStage**.
This function is a cut-down version of the **AddStageVehicle** function and is best used with a vehicle active in a recent/previous stage/objective (but can function as a replacement without the ability to set a custom CON/configuration file).
*Vehicle* is the (loaded) vehicle's internal name.
*Locator* is **optional** this time; if present the vehicle is teleported to the given/loaded Locator Type 3. If left empty or set to `NULL`, the vehicle **resumes from where it last was** if it is still active from the previous/a prior stage/objective. If this location does not exist, the vehicle spawns at coordinites **0**,**0**,**0**.
*Behaviour* sets the vehicle AI behaviour type. See the later section "Specific notes" -> "AI vehicle behaviours" for information.
*Driver* optionally adds a driver character to the vehicle by internal name. However, this overwrites any previous call for a driver through mission functions and takes place *before* the holding stage, so is probably useless outside of situations where this function is serving as a replacement for **AddStageVehicle** (for example, in an ASF **IfCurrentCheckpoint** block).
Repeatable for multiple vehicles.

### AddStageWaypoint
```
AddStageWaypoint(str:Locator);
AddStageWaypoint("m1_skinner_path_01");
```
Used in mission initialisation scripts. Can be repeated.
Must be used between calls to **AddStage** and **CloseStage**.
Adds a waypoint Locator Type 0/3 (*Locator*) to the stage waypoint list for active AI vehicles of types to follow/path loop.
There is a limit of thirty-two waypoints per stage. ~~ADDYNOKNOW~~

### AddStageCharacter
```
AddStageCharacter(str:Character, str:CharacterLocator, str:?, str:Vehicle, str:VehicleLocator);
AddStageCharacter("homer", "homer_home", "", "current", "level1_carstart");
AddStageCharacter("marge", "", "", "marge_v", "level4_carstart");
```
Used in mission initialisation scripts.
Must be used between calls to **AddStage** and **CloseStage**.
On stage/objective reach, teleports *Character* to loaded Locator Type 3 *CharacterLocator* (if present) whilst placing *Vehicle* (which can be `current` to refer to the player's last used vehicle, or the name of any loaded `OTHER`/`AI`-type vehicle) at *VehicleLocator*. If *CharacterLocator* is omitted, the player is placed into the vehicle.
The effect of *?* is unknown.
~~ADDYNOKNOW~~ Third parameter, placed in as a driver or passenger or depends?

### AddStageMusicChange
```
AddStageMusicChange();
AddStageMusicChange();
```
Used in mission initialisation scripts.
Must be used between calls to **AddStage** and **CloseStage**.
So long as various gameplay conditions are met in the stage/objective, triggers the `m#_drama` level music event on stage reach/play, if it exists.
Otherwise has no effect.
~~ADDYNOKNOW~~

### SetStageMusicAlwaysOn
```
SetStageMusicAlwaysOn();
SetStageMusicAlwaysOn();
```
Used in mission initialisation scripts.
Must be used between calls to **AddStage** and **CloseStage**.
Keeps in-vehicle music (event is variable) playing when the player gets out of vehicle during the stage/objective.

### SetCompletionDialog
```
SetCompletionDialog(str:Noboxconv, str:InitialSpeakerCharacter);
SetCompletionDialog("gotitem");
SetCompletionDialog("gotcha","lisa");
```
Used in mission initialisation scripts.
Must be used between calls to **AddStage** and **CloseStage**.
If valid and possible, plays the noboxconv dialogue sequence name specified by *Noboxconv* (see also the later section "Specific notes" -> "Referencing sound resources in scripts").
*InitialSpeakerCharacter* specifies the internal name of an involved and present NPC/driver, if applicable.
Completion dialogue sequences override each other if possible - if one begins playing whilst another already is, the previous one's playback is cancelled entirely.
~~ADDYNOKNOW~~ Second argument stuff.

### StageStartMusicEvent
```
StageStartMusicEvent(str:Event);
StageStartMusicEvent("M2_drama");
```
Used in mission initialisation scripts.
Must be used between calls to **AddStage** and **CloseStage**.
Sets the current music event (from the loaded RMS file) to the one given as *Event*, but **only if the given event is hardcodedly supported, such as M#_main/M#_drama**. Existent but unsupported events crash; non-existent events are ignored.
~~ADDYNOKNOW~~

### SetMusicState
```
SetMusicState(str:State, str:Value);
SetMusicState("Mission1", "Stage1");
```
Used in mission initialisation scripts.
Must be used between calls to **AddStage** and **CloseStage**.
Set music state *State* in the current RMS file to value *Value*, if both exist.
Allows for alternative, interruption-proof, all-event-encompassing music changes throughout missions.

### SetStageCamera
```
SetStageCamera(str:Mode, int:Cut, int:Transition);
SetStageCamera("walker", 0, 0);
SetStageCamera("follow", 0, 0);
```
Used in mission initialisation scripts.
Must be used between calls to **AddStage** and **CloseStage**.
Force a camera *Mode* on stage start (the user can switch out):
- `walker` force sets the on-foot "Walker Cam", as long as the player's current camera was accessed via the "Unlock All Cameras" cheat code and not through control settings' Mouselook option - either *Cut* or *Transition* can be set to `1` for a rougher or smoother switch;
- `follow` force sets the vehicle "Far Follow Cam", as long as the player is not driving the vehicle on call;

### RESET_TO_HERE
```
RESET_TO_HERE();
RESET_TO_HERE();
```
Used in mission initialisation scripts.
Must be used between calls to **AddStage** and **CloseStage**.
If used in a Sunday Drive/pre-mission segment, sets the containing stage/objective as the one to start at when at all warping to the mission.
If used in a main mission segment, sets the containing stage/objective as the one to start at following a restart/fail.
Only one call is supported per-mission segment.
One of the mission segment types is fine without one, and the other crashes if there isn't one. ~~ADDYNOKNOW~~

### SetMaxTraffic
```
SetMaxTraffic(int:Amount);
SetMaxTraffic(4);
```
Used in mission initialisation scripts.
Must be used between calls to **AddStage** and **CloseStage**.
Sets the maximum concurrently present road traffic vehicles via *Amount* - valid range is 0-5.
When the traffic level gets changed during gameplay, vehicles gracefully spawn/despawn off-screen as/when required.

### AddSafeZone
```
AddSafeZone(str:Locator, float:Radius);
AddSafeZone("cutscene_area", 25.0);
```
Used in mission initialisation scripts.
Must be used between calls to **AddStage** and **CloseStage**.
Creates a trigger centred at *Locator* (loaded, type 3) and sized *Radius*.
This trigger cannot be viewed with the Debug Test hack.
The area the trigger encompasses is considered as a *safe zone*.
If in a "Hit & Run!", *entering* the trigger causes the relevant chase vehicles to stop in place, which they will continue to do until the trigger is left or the "Hit & Run!" ends.
~~ADDYNOKNOW~~ Repeatable? IsRect = ?

### SetBonusMissionStart
```
SetBonusMissionStart();
SetBonusMissionStart();
```
Used in mission initialisation scripts.
Must be used between calls to **AddStage** and **CloseStage**.
When used in a mission that calls **AddBonusObjective**, sets the containing stage as the one in which bonus objective completion will be measured.
Does nothing if there is not a call to **AddBonusObjective**.

### ShowStageComplete
```
ShowStageComplete();
ShowStageComplete();
```
Used in mission initialisation scripts.
Must be used between calls to **AddStage** and **CloseStage**.
On completion of the containing stage/objective, shows the textbible entry "STAGE_COMPLETE", plays a sound, and makes the player character do a celebration animation.

### SetHUDIcon
```
SetHUDIcon(str:Icon);
SetHUDIcon("simpsons");
```
Used in mission initialisation scripts.
Must be used between calls to **AddStage** and **CloseStage**.
Set the icon for the stage/objective, shown in the upper-left corner except during stages that call **AddStage** with a first argument of `locked`.
Must be a loaded sprite of the name given as *Icon*.
Non-existent sprite calls are ignored.
In a stage/objective, the HUD icon does not show unless **SetStageMessageIndex** is also called.

### SetIrisWipe
```
SetIrisWipe(int:IrisWipe);
SetIrisWipe(1);
```
Used in mission initialisation scripts.
Must be used between calls to **AddStage** and **CloseStage**.
If set to `1`, does the iris wipe effect on stage/objective completion.

### SetFadeOut
```
SetFadeOut(int:FadeOut);
SetFadeOut(1);
```
Used in mission initialisation scripts.
Must be used between calls to **AddStage** and **CloseStage**.
If set to `1`, does a fade out effect on stage/objective completion.
Restarting the mission during this effect can crash the game.

### CloseStage
```
CloseStage();
CloseStage();
```
Used in mission initialisation scripts.
Must be used between calls to **SelectMission** and **CloseMission**.
Ends definition of a stage.

### SetVehicleAIParams
```
SetVehicleAIParams(str:Vehicle, int:MinIntelligence, int:MaxIntelligence);
SetVehicleAIParams("cVan", 50, 99); // All non-route-avoided shortcuts.
SetVehicleAIParams("ship", 0, 5); // No non-route-set shortcuts.
```
Used in mission initialisation scripts.
Must be used between calls to **AddStage** and **CloseStage**.
Defines shortcut intelligence range/usage for *Vehicle*, which should be a loaded and active AI vehicle in the stage/objective.
The vehicle is assigned a random intelligence value between *MinIntelligence* and *MaxIntelligence*.
Every explicit shortcut path/road in the game has an assigned intelligence value. The vehicle cannot take shortcut roads/paths that its own assigned intelligence is below.
This excludes cases where the vehicle will avoid shortcuts if its waypoint path deliberately routes around them, or take shortcuts if its assigned waypoint path deliberately routes on them. This may also exclude cases where the objective type and/or other parameters force the vehicle to sometimes avoid shortcuts if the player is behind.
This excludes `chase` behaviour vehicles. ~~ADDYNOKNOW~~
Repeatable for multiple vehicles.
If unspecified, defaults to `15`, `25`.
Values that are too high or low break. ~~ADDYNOKNOW~~
Ignored sometimes. ~~ADDYNOKNOW~~

### PlacePlayerAtLocatorName
```
PlacePlayerAtLocatorName(str:Locator);
PlacePlayerAtLocatorName("m2_bart_start");
```
Used in mission initialisation scripts.
Must be used between calls to **AddStage** and **CloseStage**.
Teleports the player to Locator Type 3 *Locator* on stage reach, which should be loaded.
Does not work if the player is within an interior at execution time.
~~ADDYNOKNOW~~

### msPlacePlayerCarAtLocatorName
```
msPlacePlayerCarAtLocatorName(str:Locator);
msPlacePlayerCarAtLocatorName("m2_carstart");
```
Used in mission initialisation scripts.
Must be used between calls to **AddStage** and **CloseStage**.
Teleports the player's current vehicle to Locator Type 3 *Locator* on stage reach, which should be loaded.

### SwapInDefaultCar
```
SwapInDefaultCar();
SwapInDefaultCar();
```
Used in mission initialisation scripts.
Must be used between calls to **AddStage** and **CloseStage**.
When used correctly at the endpoint of a forced vehicle mission, swaps out the forced vehicle and swaps in the level default vehicle on stage/objective completion.
Must be used alongside correct uses of the functions **SetFadeOut** (with argument of `1`), **SetSwapPlayerLocator**, **SetSwapDefaultCarLocator**, and **SetSwapForcedCarLocator** for any of this to have any effect.

### SetSwapPlayerLocator
```
SetSwapPlayerLocator(str:Locator);
SetSwapPlayerLocator("end_lisa_loc");
```
Used in mission initialisation scripts.
Must be used between calls to **AddStage** and **CloseStage**.
Sets Locator Type 3 (*Locator*) to teleport player character to at stage/objective completion for forced vehicle disposal/vehicle swap.
Must be used alongside **SetFadeOut**/**SwapInDefaultCar**/**SetSwapDefaultCarLocator**/**SetSwapForcedCarLocator**.

### SetSwapDefaultCarLocator
```
SetSwapDefaultCarLocator(str:Locator);
SetSwapDefaultCarLocator("end_def_car");
```
Used in mission initialisation scripts.
Must be used between calls to **AddStage** and **CloseStage**.
Sets Locator Type 3 (*Locator*) to teleport level default vehicle to at stage/objective completion for forced vehicle disposal/vehicle swap.
Must be used alongside **SetFadeOut**/**SwapInDefaultCar**/**SetSwapPlayerLocator**/**SetSwapForcedCarLocator**.

### SetSwapForcedCarLocator
```
SetSwapForcedCarLocator(str:Locator);
SetSwapForcedCarLocator("end_lisa_loc");
```
Used in mission initialisation scripts.
Must be used between calls to **AddStage** and **CloseStage**.
Sets Locator Type 3 (*Locator*) to teleport forced vehicle to at stage/objective completion for forced vehicle disposal/vehicle swap.
Must be used alongside **SetFadeOut**/**SwapInDefaultCar**/**SetSwapPlayerLocator**/**SetSwapDefaultCarLocator**.

### NoTrafficForStage
```
NoTrafficForStage();
NoTrafficForStage();
```
Used in mission initialisation scripts.
Must be used between calls to **AddStage** and **CloseStage**.
Disables/removes all traffic for the duration of the stage/objective.
Even if on-screen, active traffic vehicles are immediately purged on reach.

### ClearTrafficForStage
```
ClearTrafficForStage();
ClearTrafficForStage();
```
Used in mission initialisation scripts.
Must be used between calls to **AddStage** and **CloseStage**.
Removes all active traffic immediately (even if on-screen) at stage reach.
Traffic is then re-enabled at the same density as set prior.
Useful for clearing the road (for instance, to teleport in vehicle for a task start).

### SetStageAIRaceCatchupParams
```
SetStageAIRaceCatchupParams(str:Vehicle, float:Radius, float:Ahead, float:Near, float:Behind);
SetStageAIRaceCatchupParams("smith_v", 0.5, 101.0, 101.0, 101.0);
```
Used in mission initialisation scripts.
Must be used between calls to **AddStage** and **CloseStage**.
*Radius* is the catchment zone size for being near to (active AI) *Vehicle*.
In accordance with the stage waypoints, objective, and road network:
- If *Vehicle* is ahead of the player *and* the player is external to *Radius*, target the speed set as *Ahead*.
- If *Vehicle* is falling behind the player *and* the player is external to *Radius*, target the speed set as *Behind*.
- If neither of the above are correct and the player is within *Radius*, target the speed set as *Near*.

The vehicle must be of `race` behaviour type for this to have effect.
Repeatable for multiple vehicles.
If unspecified, defaults to `80.0`, `0.5`, `1.1`, `1.7`.

### SetStageAIEvadeCatchupParams
```
SetStageAIEvadeCatchupParams(str:Vehicle, float:Fast, float:Slow);
SetStageAIEvadeCatchupParams("carhom_v", 10.0, 25.5);
```
Used in mission initialisation scripts.
Must be used between calls to **AddStage** and **CloseStage**.
*Vehicle* must be an active AI vehicle.
In accordance with the stage waypoints, objective, and road network:
- If *Vehicle* is *Fast* close to the player, target the vehicle's own maximum speed.
- If *Vehicle* is *Slow* ahead of the player, target a slower speed that is relative to the AI vehicle's own top speed.

The vehicle must be of `evade` behaviour type for this to have effect.
Repeatable for multiple vehicles.
If unspecified, defaults to `20.0`, `70.0`.

### SetStageAITargetCatchupParams
```
SetStageAITargetCatchupParams(str: Vehicle, float:Fast, float:Slow);
SetStageAITargetCatchupParams("pizza", 50.0, 600.0);
```
Used in mission initialisation scripts.
Must be used between calls to **AddStage** and **CloseStage**.
*Vehicle* must be an active AI vehicle.
In accordance with the stage waypoints, objective, and road network:
- If *Vehicle* is *Fast* close to the player, target the player's own maximum speed.
- If *Vehicle* is *Slow* ahead of the player, target a slower speed that is relative to the player's own maximum speed.

The vehicle must be of `target` behaviour type for this to have effect.
Repeatable for multiple vehicles.
If unspecified, defaults to `20.0`, `70.0`.

### SetCharacterToHide
```
SetCharacterToHide(str:Character);
SetCharacterToHide("apu");
```
Used in mission initialisation scripts.
Must be used between calls to **AddStage** and **CloseStage**.
On completion of the stage/objective, if existent, the player character (specified as internal name by *Character*) will be made invisible.
~~ADDYNOKNOW~~ Persistence? General effect? If invalid/non-existent?

### SetLevelOver
```
SetLevelOver();
SetLevelOver();
```
Used in mission initialisation scripts.
Must be used between calls to **AddStage** and **CloseStage**.
Shows the Level Progress screen upon stage/objective completion.

### SetGameOver
```
SetGameOver();
SetGameOver();
```
Used in mission initialisation scripts.
Must be used between calls to **AddStage** and **CloseStage**.
Shows the Level Progress screen (followed by the credits and exit to Main Menu sequence) upon stage/objective completion.

### StayInBlack
```
StayInBlack();
StayInBlack();
```
Used in mission initialisation scripts.
Must be used between calls to **AddObjective** and **CloseObjective**.
Compatible with `timer` objective type.
Keeps the screen blacked out during a `timer` stage/objective.
The preceeding stage **must** have featured **SetFadeOut** with argument `1`.
~~ADDYNOKNOW~~ SetIrisWipe is compatible?

### AllowMissionAbort
```
AllowMissionAbort(int:MissionAbort);
AllowMissionAbort(0);
```
Used in mission initialisation scripts.
Must be used between calls to **AddStage** and **CloseStage**.
In theory enables/disables mission cancelling.
In practice seems to do nothing.

### SetParTime
```
SetParTime(int:Seconds);
SetParTime(50);
```
Used in mission initialisation scripts.
Must be used between calls to **AddObjective** and **CloseObjective**.
Sets the time-to-beat for a Wager Race (`"race", "gamble"`) stage/objective/mission, specified as *Seconds*.
~~ADDYNOKNOW~~ Incorrect/zero use results? Must be between AO and CO?

### SetRaceEnteryFee
```
SetRaceEnteryFee(int:CoinPrice);
SetRaceEnteryFee(50);
```
Used in mission initialisation scripts.
Must be used between calls to **AddStage** and **CloseStage**.
Sets the payout for a Wager Race (`"race", "gamble"`) stage/objective/mission. Specified as *CoinPrice*, which is multiplied by 2 if the Wager Race is played on EASY difficulty, 3 for NORMAL, and 4 for HARD.
This function does *not* set the race entry fee - see **SetCoinFee**.
~~ADDYNOKNOW~~ Weird Wager Race stuff.

### PutMFPlayerInCar
```
PutMFPlayerInCar();
PutMFPlayerInCar();
```
Used in mission initialisation scripts.
Must be used between calls to **AddStage** and **CloseStage**.
Instantly places the player within and driving their most recent vehicle on stage/objective reach.
If used in the same stage as a `dialogue` objective, the player ends up in a bugged state where the player character is teleported and out of the vehicle but the player remains in control of the vehicle.

### SetStatepropShadow
```
SetStatepropShadow(str:Stateprop, str:Shadow);
SetStatepropShadow("tree1", "shadow55");
```
Used in level load scripts.
Assigns *Stateprop* object a (loaded) specific shadow effect specified as *Shadow*.
Is repeatable for different objects.

### AddObjective
```
AddObjective(str:MainType, str:Parameter, str:RoadArrowControl);
AddObjective("timer");
AddObjective("goto", "both");
AddObjective("race", "gamble", "nearest road");
```
Used in mission initialisation scripts. Changed by ASF.
Must be used between calls to **AddStage** and **CloseStage**.
Begins definition of an objective - the stage's completion task.
Each mission stage can only contain one objective.
Each objective should be ended with **CloseObjective** and relevant objective context functions should go between.
*MainType* sets the objective type - controls gameplay and HUD.
Valid *MainType* arguments and relevant inclusive (objective context-*only*) functions are listed below:
- In the vanilla game:
- `buycar` requires current player vehicle to be *Parameter*;
- `buyskin` requires current player clothing to be *Parameter*;
- `coins` requires coin payment/is Wager Race only - see **SetCoinFee**;
- `delivery` requires collection of 1-30 set items or destruction of props - see **AddCollectible** and optionally **SetCollectibleEffect** and **SetCollectibleSoundEffect (ASF)**;
- `destroy` requires destroying an active AI vehicle - see **SetObjTargetVehicle**;
- `destroyboss` requires destruction of a flying actor - see **SetObjTargetBoss**;
- `dialogue` plays out a convinit conversation between player and NPC - see **SetDialogueInfo**, and optionally **SetDialogueInfo**/the **AmbientAnimation** and **ConversationCam**-named functions as well as **CharacterIsChild**;
- `dump` functions as a hit+collect, follow+collect, or destroy+collect - see **SetObjTargetVehicle**, **AddCollectible**, and **BindCollectibleTo**;
- `fmv` plays a RMV video file - see **SetFMVInfo**
- `follow` requires that an active AI vehicle reaches the end of the stage waypoint trail - see **SetObjTargetVehicle**;
- `getin` requires the player to enter the vehicle specified as *Parameter* (if valid) or any vehicle otherwise;
- `gooutside` requires the player to enter a given trigger - see **SetDestination**;
- `goto` requires the player to enter a given trigger with an optional graphic/thus radar guidance (and interact if **MustActionTrigger** is used; and hear a random "arrive" dialogue line if **TurnGotoDialogOff** is unused) - see **SetDestination** and optionally **SetCollectibleEffect**;
- `interior` requires the player to enter an interior - see **SetDestination**;
- `losetail` requires the player to be a far enough distance away from an active AI vehicle - see **SetObjTargetVehicle** and **SetObjDistance**;
- `pickupitem` requires the player to collect a loaded/initialised/thus active stateprop locator (if the player already has it, it will be taken away) - see **SetPickupTarget**;
- `race` requires the player to pass (optionally graphically/thus radar shown) triggers in order to progress, with optional laps and tracking of/dialogue for optional AI opponents - see **AddCollectible**, **SetCollectibleEffect**, **SetRaceLaps**, and **SetParTime (Wager Races**);
- `talkto` requires the player to interact with an NPC, with optional parameters - see **SetTalkToTarget**;
- `timer` requires that an amount of seconds passes - see **SetDurationTime** and **StayInBlack**; ~~ADDYNOKNOW~~ SetLevel/GameOver stuff
- `loadvehicle` is supported but does not appear to work - see **SetVehicleToLoad**;
- Also available when using ASF:
- `camera` plays a camera animation - see **SetObjCameraName**, **SetObjMulticontName**, **SetObjCanSkip**, **SetObjNoLetterbox**, and **SetObjUseCameraPosition**;
- `collectcoins` requires the player to collect coin(s) - see **SetObjTotal**;
- `collectwrench` requires the player to collect wrench(es) - see **SetObjTotal**;
- `completedwasps` requires the player to have destroyed a given amount of the level's Wasp Cameras - see **SetObjTotal**;
- `destroycars` requires a variable number of (loaded/non-loaded/active/non-active) vehicles to be destroyed - see **SetObjTotal** and **AddObjTargetModel**;
- `hitandrun` requires the player to get a "Hit & Run!";
- `hitandruncaught` requires the player to get "Busted!" in a "Hit & Run!";
- `hitandrunlost` requires the player to escape a "Hit & Run!" *only* via meter drain;
- `hitandrunrage` requires the player to nearly fill up the "Hit & Run!" meter;
- `hitpeds` requires the player to kick other active/non-active characters - see **SetObjTotal** and **AddObjTargetModel**;
- `insidetrigger` requires the player to be within a trigger, with optional extras/parameters - see **SetObjTrigger**, **SetObjThreshold**, **SetObjMessageIndex**, **SetObjDecay**, and **SetObjSound**;
- `outsidetrigger` requires the player to be external to a trigger, with optional extras/parameters - see **SetObjTrigger**, **SetObjThreshold**, **SetObjMessageIndex**, **SetObjDecay**, and **SetObjSound**;
- `jump` requires the player to execute jump(s) - see **SetObjTotal**;
- `reachspeed` requires the player to reach a speed whilst driving - see **SetObjSpeedKMH**;
- `spring` requires the player to hit bounce trigger(s);

*Parameter* is optional, and has a few variable use cases:
- if *MainType* is `race`, *Parameter* can optionally be set to `gamble` to enable Wager Race stuff; ~~ADDYNOKNOW~~
- if *MainType* is `buycar` or `buyskin`, *Parameter* must be set to the internal name of the required vehicle/skin;
- if *MainType* is `getin`, *Parameter* can optionally be set to the internal name of a specific vehicle that the player is required to enter (must be loaded at mission start to actually work - blank/invalid completes the objective on entry of any vehicle);
- if *Parameter* is not set to any of the above, it can be set to any of the below arguments that *RoadArrowControl* supports, for the same effect as seen there.

*RoadArrowControl* optionally controls the display of the navigation system road arrows, if the user has them enabled in game settings:
- `neither` disables road arrows (they're still processed, but not shown);
- `nearest road` only places road arrows on the closest road at reach;
- `intersection` only places road arrows on road intersections;
- `both` combines the behaviour of `nearest road` and `intersection`;

The default behaviour (if unspecified) seems to be `both`.
Road arrow display is only enabled in `delivery`, `goto`, `interior`, `race`, and `talkto` objectives.
~~ADDYNOKNOW~~ Road arrow short codes, default arrow mode, supported objs.
In the vanilla game, if `MainType` is set to something invalid, or blank, an empty/unwinnable objective is made instead - some of Radical's unused scripts do this by setting it to `dummy`. When ASF is in use, `dummy` **must** be used to achieve the same effect, and invalid/blank uses throw errors.

### CloseObjective
```
CloseObjective();
CloseObjective();
```
Used in mission initialisation scripts.
Must be used between calls to **AddStage** and **CloseStage**.
Ends definition of an objective.

### SetDestination
```
SetDestination(str:Locator, str:Drawable);
SetDestination("m1_shops", "carsphere");
```
Used in mission initialisation scripts.
Must be used between calls to **AddObjective** and **CloseObjective**.
Compatible with `goto`, `interior`, and `gooutside` objective types.
The player will complete the objective when they ender the trigger(s) tied to *Locator*, which should be of Type 0 and loaded.
Optionally, a (loaded) drawable (*Drawable*) can be placed at the primary position of the Locator Type 0. This also enables the radar to show the objective marker and point to it.
*RoadArrowControl* (see **AddObjective**) is supported (in `goto` and `interior` objective types ~~ADDYNOKNOW~~ gooutside) but does not rely upon *Drawable*.

### AddNPC
```
AddNPC(str:Character, str:Locator, str:Interior);
AddNPC("lisa", "mX_lisa");
AddNPC("bart", "mX_bart", "bartroom");
```
Used in mission initialisation scripts.
Must be used between calls to **AddObjective** and **CloseObjective**.
Compatible with any objective type.
Adds NPC *Character* to position *Locator* (Type 3).
Teleports them if they are already present/residual as an NPC.
Optionally specify an *Interior* (internal name) the NPC is in.
NPCs despawn once far away enough if the current stage does not call **AddNPC** for them.
This function can be called a maximum of four unique times per objective; successive calls crash the game.
~~ADDYNOKNOW~~ Interior effect, pre-existing level characters.

### RemoveNPC
```
RemoveNPC(str:Character);
RemoveNPC("joger2");
```
Used in mission initialisation scripts.
Must be used between calls to **AddObjective** and **CloseObjective**.
Compatible with any objective type.
Removes NPC *Character*, so long as the game believes they exist as an NPC.
If they don't, the game crashes.
Detection rules for existence may be unusual and it is probably always safer to call **AddNPC** with a hidden/out-of-bounds *Locator*.
~~ADDYNOKNOW~~ Exact brokenness/limits unknown. Repeatable?

### AddDriver
```
AddDriver(str:Character, str:Vehicle);
```
Used in mission initialisation scripts.
Must be used between calls to **AddObjective** and **CloseObjective**.
Compatible with any objective type.
Adds driver *Character* to mission AI *Vehicle*, which should be loaded and active.
They will be added in the driver's seat.
~~ADDYNOKNOW~~ Stage function? If driver already there? Repeatable?

### RemoveDriver
```
RemoveDriver(str:Character);
```
Used in mission initialisation scripts.
Must be used between calls to **AddObjective** and **CloseObjective**.
Compatible with any objective type.
Removes driver *Character* from a loaded/active AI vehicle, if valid/possible.
Unknown integration in scenarios where multiple vehicles have the same driver.
Unknown integration with CON/ASF-set drivers in all those forms.
~~ADDYNOKNOW~~ Stage function? Multiple of same? ASF stuff? Repeatable?

### SetTalkToTarget
```
SetTalkToTarget(str:Character, int:Drawable, float:DrawableOffset, float:Radius);
SetTalkToTarget("krusty");
SetTalkToTarget("krusty", 0, 0.2, 5.0);
SetTalkToTarget("krusty", 0, 0.2);
```
Used in mission initialisation scripts.
Must be used between calls to **AddObjective** and **CloseObjective**.
Compatible with `talkto` objective type.
The objective will be completed when the player talks to *Character*, who should be active either as a level or mission NPC at stage/objective reach.
*Drawable* optionally sets a numeric value that binds to a hardcoded index of drawables to place above *Character*. If incorrect, the game crashes.
- `0` gives the "!" - default;
- ~~ADDYNOKNOW~~

*DrawableOffset* optionally allows specifying a height offset (negative or plus) for the *Drawable* - useful with shorter/taller characters.
*Radius* optionally sets the spherical radius size within which the player can talk to the *Character*.
*RoadArrowControl* (see **AddObjective**) is supported.

### SetDialogueInfo
```
SetDialogueInfo(str:Player, str:NPC, str:Convinit, int:?);
SetDialogueInfo("homer", "patty", "racestart", 0);
SetDialogueInfo("homer", "selma", "racestart");
```
Used in mission initialisation scripts.
Must be used between calls to **AddObjective** and **CloseObjective**.
Compatible with `dialogue` objective type.
Establishes that the conversation is between *Player* character and *NPC* character, using the *Convinit* dialogue sequence. See the later section "Specific notes" -> "Referencing sound resources in scripts".
The effect of *?* is unknown. Is optional.
~~ADDYNOKNOW~~

### SetDialoguePositions
```
SetDialoguePositions(str:Player, str:NPC, str:Vehicle, int:?);
SetDialoguePositions("bart", "lisa", "v_extr");
```
Used in mission initialisation scripts.
Must be used between calls to **AddObjective** and **CloseObjective**.
Compatible with `dialogue` objective type.
Places the player/NPC/current vehicle at (loaded) Locator Type 3s *Player*, *NPC*, and *Vehicle* respectively.
If current vehicle is far enough away from the conversation spots at conversation start, it will not be teleported. ~~ADDYNOKNOW~~
If current vehicle does get teleported, it is returned at the end of the conversation.
The effect of *?* is unknown. ~~ADDYNOKNOW~~

### SetRaceLaps
```
SetRaceLaps(int:Amount);
SetRaceLaps(6);
```
Used in mission initialisation scripts.
Must be used between calls to **AddObjective** and **CloseObjective**.
Compatible with `race` objective type.
Makes the race loop for *Amount* laps, for both the player and AI vehicles.
A HUD counter displays the current player lap and total number of laps.
Values that are too high break. ~~ADDYNOKNOW~~

### TurnGotoDialogOff
```
TurnGotoDialogOff();
TurnGotoDialogOff();
```
Used in mission initialisation scripts.
Must be used between calls to **AddObjective** and **CloseObjective**.
Compatible with `goto` and `gooutside` objective types. ~~ADDYNOKNOW~~
Disables "arrive" dialogue upon stage/objective completion.

### MustActionTrigger
```
MustActionTrigger();
MustActionTrigger();
```
Used in mission initialisation scripts.
Must be used between calls to **AddObjective** and **CloseObjective**.
Compatible with `goto` objective type.
Requires the player to PRESS ACTION/interact with the target of **SetDestination** (which should be a Locator Type 0 **with Event 2**).

### SetCoinFee
```
SetCoinFee(int:CoinCost);
SetCoinFee(50);
```
Used in mission initialisation scripts.
Must be used between calls to **AddObjective** and **CloseObjective**.
Compatible with `coins` objective type.
Gates the player from Wager Race entry unless *CoinCost* coins can/will be paid. 
Should not be used (nor should the `coins` objective type) outside of `gr1` type missions.

### SetDurationTime
```
SetDurationTime(int/float:Seconds);
SetDurationTime(3);
SetDurationTime(3.5);
```
Used in mission initialisation scripts. Changed by ASF.
Must be used between calls to **AddObjective** and **CloseObjective**.
Compatible with `timer` objective type.
Makes the objective wait for *Seconds* seconds to complete.
In the vanilla game *Seconds* is treated without decimal precision.
If ASF is enabled, decimal precision is honoured.

### AddCollectible
```
AddCollectible(str:Locator, str:Drawable, str:Noboxconv, str:NPCSpeaker);
AddCollectible("meal22", "kmeal");
AddCollectible("meal23", "kmeal", "getback", "fem3");
```
Used in mission initialisation scripts.
Must be used between calls to **AddObjective** and **CloseObjective**.
Compatible with `delivery`, `dump`, and `race` objective types.
Sets Locator Type 0 *Locator* as one of the collectibles, with an optional drawable/thus radar presence *Drawable*.
Optionally specify a *Noboxconv* dialogue sequence to play on item/target acquisition, possibly spoken by specified active NPC *NPCSpeaker*. See the later section "Specific notes" -> "Referencing sound resources in scripts".
In `delivery`/`dump` objectives with more than one **AddCollectible**, an item counter is displayed on the HUD.
In `dump` objectives:
- The position of *Locator* is ignored, and the collectible is teleported/activated when/where required;
- If there is only one call to **AddCollectible** and none to **BindCollectibleTo**, the objective becomes a destroy-and-collect;
- If there is more than one call to **AddCollectible** and none to **BindCollectibleTo**, the objective becomes a hit-and-collect;
- If there are any calls to **BindCollectibleTo**, the objective becomes a follow-and-collect, regardless of the number of **AddCollectible** calls (so long as there is at least one);

In `race` objectives, calls to **AddCollectible** are used as successive player-hit-required checkpoints.
A compatible objective can feature up to 30 collectibles/targets.
Radar pointer order in `delivery` objectives is determined by order of definition in script.
*RoadArrowControl* (see **AddObjective**) is supported.
~~ADDYNOKNOW~~ Optional Drawable, Speaker, prop support i.e L1M4 vanilla.

### SetCollectibleEffect
```
SetCollectibleEffect(str:Effect);
SetCollectibleEffect("explodebox");
```
Used in mission initialisation scripts.
Must be used between calls to **AddObjective** and **CloseObjective**.
Compatible with `delivery`, `dump`, `goto`, and `race` objective types.
Set the particle/sprite effect for collecting item(s)/target(s) to *Effect*, which should be loaded.
Can either be specified once to affect all collectibles or multiple times to successively affect individual collectibles.
~~ADDYNOKNOW~~ Weird goto, multiple stuff stuff.

### BindCollectibleTo
```
BindCollectibleTo(int:CollectibleID, int:WaypointID);
BindCollectibleTo(0, 2);
```
Used in mission initialisation scripts.
Must be used between calls to **AddObjective** and **CloseObjective**.
Compatible with `dump` objective type.
Turns a dump objective into a follow-and-collect - must be called for as many calls to **AddCollectible** the objective contains.
When the target vehicle reaches the *WaypointID* in the stage waypoint list, it will wait a random few seconds before dropping *CollectibleID* in the objective collectible list.
These lists are zero-based: in a stage with three calls to **AddStageWaypoint**, `2` refers to the third call.

### AllowUserDump
```
AllowUserDump();
AllowUserDump();
```
Used in mission initialisation scripts.
Must be used between calls to **AddObjective** and **CloseObjective**.
Compatible with `delivery` objective type.
Allows active mission AI vehicles to make the player drop collected items on the spot upon collision.
~~ADDYNOKNOW~~ Needs more looking into...

### SetVehicleToLoad
```
SetVehicleToLoad(str:Path, str:Vehicle, str:Locator);
SetVehicleToLoad("art\cars\taxiA.p3d", "taxiA", "taxi_locat");
```
Used in mission initialisation scripts.
Must be used between calls to **AddObjective** and **CloseObjective**.
Compatible with `loadvehicle` objective type.
Sets the *Path* (rooted in game root directory), *Vehicle* (internal name), and *Locator* (loaded, Type 3) of a vehicle to load and assign a position for.
Doesn't seem to work; results in a "Composite drawable `NULL` not found" error.

### SetObjTargetVehicle
```
SetObjTargetVehicle(str:Vehicle);
SetObjTargetVehicle("oblit_v");
```
Used in mission initialisation scripts.
Must be used between calls to **AddObjective** and **CloseObjective**.
Compatible with `destroy`, `dump`, `follow`, and `losetail` objectives.
Sets *Vehicle* (which should be loaded/active) as the objective target vehicle.
In `destroy` objectives this means they must be destroyed, and a health meter will be displayed on the HUD.
In `dump` objectives this means they are the subject of a destroy-and-collect (with aforementioned health meter), hit-and-collect, or follow-and-collect.
In `follow` objectives this means they must reach the end of the stage waypoint trail.
In `losetail` objectives this means they must be escaped from, and a distance meter will be displayed on the HUD.

### SetObjDistance
```
SetObjDistance(float:Distance);
SetObjDistance(178.0);
```
Used in mission initialisation scripts.
Must be used between calls to **AddObjective** and **CloseObjective**.
Compatible with `losetail` objectives.
Set the distance away from the AI vehicle the player must be to escape and complete the objective, as *Distance*.

### SetObjTargetBoss
```
SetObjTargetBoss(str:Boss);
SetObjTargetBoss("Planet Express Ship");
```
Used in mission initialisation scripts.
Must be used between calls to **AddObjective** and **CloseObjective**.
Compatible with `destroyboss` objective type.
Requires the player to deliver stateprop collectible to Flying Actor Boss *Boss* (instance name), typically the `Planet Express Ship` spaceship in Level 7.
~~ADDYNOKNOW~~ Specific/tailorable?

### AddCollectibleStateProp
```
AddCollectibleStateProp(str:StateProp, str:Locator, int:ATCType);
AddCollectibleStateProp("bombbarrel", "barrel_loc", 2);
```
Used in mission initialisation scripts.
Must be used between calls to **SelectMission** and **CloseMission**.
Allows a collectible/carryable StateProp to exist throughout the mission. It can then be accessed through the `pickupitem` objective type/**SetPickupTarget**.
*StateProp* sets the (loaded) StateProp name.
*Locator* sets the (loaded) Locator Type 0 spawn spot name, for when activated.
*ATCEntry* sets the ATC prop/physics object type behaviour entry the State Prop assumes - Radical use `2`.

### SetPickupTarget
```
SetPickupTarget(str:StateProp);
SetPickupTarget("bombbarrel");
```
Used in mission initialisation scripts.
Must be used between calls to **AddObjective** and **CloseObjective**.
Compatible with `pickupitem` objective type.
Sets (loaded/active) *StateProp* as the target pickup prop. It will spawn and behave as specified via **AddCollectibleStateProp**.

### AllowRockOut
```
AllowRockOut();
AllowRockOut();
```
Used in mission initialisation scripts.
Must be used between calls to **?** and **?**.
Under specific circumstances (still/in passenger seat?), allows the player character to "rock out" during the stage/objective.
The player character will repeat their "small task complete" animation to the tempo of the current music track.
~~ADDYNOKNOW~~ Circumstances? Stage/obj function? Obj type limitation?

### AddCondition
```
AddCondition(str:Type, int:Parameter);
AddCondition("timeout");
AddCondition("keepbarrel", 1);
```
Used in mission initialisation scripts. Changed by ASF.
Must be used between calls to **AddStage** and **CloseStage**.
Adds a fail condition to a mission stage. Each stage can have multiple.
*Parameter* and/or inclusive functions (speciied below) should be given, followed by **CloseCondition**.
When ASF is enabled, more conditions are available.
Available conditions/inclusive functions include:
- In the vanilla game:
- `damage` fails if the player's vehicle gets destroyed;
- `followdistance` fails if an active AI vehicle gets too far away - see **SetCondTargetVehicle** and **SetFollowDistances**;
- `keepbarrel` allows a carried StateProp (if any) to be dropped and jumps *Parameter* stages if that happens, only in some objective types ~~ADDYNOKNOW~~ (positive numbers jump backwards, negative numbers jump forwards, `0` doesn't jump and just continues, stages that don't exist crash);
- `outofbounds` fails if the player enters/respawns via a death trigger - residual frame flash occurs after the fail screen;
- `outofvehicle` fails the player for leaving their vehicle (or entering it if they begin the stage/objective outside and the prior stage/objective did not contain the condition) - see **SetCondTime**;
- `position` fails the player if any active AI vehicles reach the end of the stage waypoint list/laps - see **SetConditionPosition**; ~~ADDYNOKNOW~~
- `race` fails the player if one AI vehicle reaches the end of the stage waypoint list - see **SetCondTargetVehicle**;
- `timeout` fails the player if the stage timer runs out - if there isn't one, the stage/objective instantly fails;
- `carryingspcollectible` works like `keepbarrel` but does not allow any stage/objective jumping and just continues on loss;
- `getcollectibles` does not appear to work;
- `hitandruncought` does not appear to work;
- `invalid` does not appear to work;
- `leaveinterior` locks all controls (including pause) on stage/objective completion (if the player left an interior during it) - exiting the game window to force a pause and then unpausing continues as normal;
- `notabducted` fails if the player reaches the UFO death trigger and respawns, but does not use its hint texts;
- `playerhit` does not appear to work;
- With ASF enabled:
- `collectcoins` fails the player if they collect coin(s) - see **SetCondTotal**;
- `collectwrench` fails the player if they collect wrench(es) - see **SetCondTotal**;
- `destroycars` fails the player if variable vehicles are destroyed - see **SetCondTotal** and **AddCondTargetModel**;
- `hitandrun` fails if the player gets a "Hit & Run!";
- `hitandruncaught` fails if the player gets "Busted!" in a "Hit & Run!";
- `hitandrunlost` fails if the player loses a "Hit & Run!" by meter drain;
- `hitandrunrage` fails if the player fills up the "Hit & Run!" meter to blinking state;
- `hitpeds` fails if the player kicks active/non-active characters - see **SetCondTotal** and **AddCondTargetModel**;
- `insidetrigger` fails if the player is within a trigger, with optional extras/parameters - see **SetCondTrigger**, **SetCondThreshold**, **SetCondMessageIndex**, **SetCondDecay**, and **SetCondSound**;
- `outsidetrigger` fails if the player is external to a trigger, with optional extras/parameters - see **SetCondTrigger**, **SetCondThreshold**, **SetCondMessageIndex**, **SetCondDecay**, and **SetCondSound**;
- `jump` fails if the player executes jump(s) - see **SetCondTotal**;
- `reachspeed` fails if the player goes above/below speeds whilst driving - see **SetCondSpeedRangeKMH**;
- `spring` fails if the player hits bounce trigger(s);

### CloseCondition
```
CloseCondition();
CloseCondition();
```
Used in mission initialisation scripts.
Must be used between calls to **AddStage** and **CloseStage**.
Ends definition of a condition.

### SetFollowDistances
```
SetFollowDistances(float:Min, float:Max);
SetFollowDistances(0, 300);
```
Used in mission initialisation scripts.
Must be used between calls to **AddCondition** and **CloseCondition**.
Set how far away (*Max*) the player is allowed to be from the condition vehicle before failing in a stage with a 'followdistance' condition.
*Min* is possibly ignored and should always be `0`.

### SetCondTargetVehicle
```
SetCondTargetVehicle(str:Vehicle);
SetCondTargetVehicle("cletu_v");
```
Used in mission initialisation scripts.
Must be used between calls to **AddCondition** and **CloseCondition**.
Compatible with `followdistance` and `race` conditions.
Sets *Vehicle* by internal name as the condition vehicle for a condition.
In `followdistance` conditions, the player fails if too far away from *Vehicle*.
In `race` conditions, the player fails if *Vehicle* reaches the last waypoint in the waypoint list (or if *Vehicle* is still/waiting on the player for too long and failsafe check+fail occurs).

### SetConditionPosition
```
SetConditionPosition(int:Position);
SetConditionPosition(1);
```
Used in mission initialisation scripts.
Must be used between calls to **AddCondition** and **CloseCondition**.
Sets *Position* as the minimum position the player must theoretically be able to finish in (in a race) to not fail a `position` condition.
In reality, appears bugged or unfinished and should always be `1`.

### SetCondTime
```
SetCondTime(int:Milliseconds);
SetCondTime(10000);
```
Used in mission initialisation scripts.
Must be used between calls to **AddCondition** and **CloseCondition**.
Sets how many *milliseconds*/seconds the player has to return to vehicle before failure in an *outofcar* condition.

### SetHitNRun
```
SetHitNRun();
SetHitNRun();
```
Used in mission initialisation scripts.
Must be used between calls to **AddCondition** and **CloseCondition**.
Compatible with `timeout` conditions.
In theory starts a "Hit & Run!" on time out instead of failing.
In practice seems to do nothing.

### EnableTutorialMode
```
EnableTutorialMode(int:TutorialMode);
EnableTutorialMode(1);
```
Used in level initialisation scripts.
If set to `1`, Bart tutorials/the option for them are allowed in the level.
if set to `0`, this is not the case.
Defaults to `0` if uncalled in a level.
More of a console version option. Unknown if any Windows releases ever use. ~~ADDYNOKNOW~~
Tutorial dialogue has the level index in the file names, which must match.
If the game can't find the file/name, the line won't play and the continue option won't appear, forcing use of "Disable Tutorial" to progress.

### SetConversationCamName
```
SetConversationCamName(str:ConversationCamMode);
SetConversationCamName("pc_near");
```
Used in mission initialisation scripts.
Must be used between calls to **AddObjective** and **CloseObjective**.
Compatible with `dialogue` objectives.
Sets the default conversation camera mode to *ConversationCamMode*;
- `pc_near`;
- `pc_far`;

~~ADDYNOKNOW~~ Sure?

### SetConversationCamPcName
```
SetConversationCamPcName(str:ConversationCamMode);
SetConversationCamPcName("pc_far");
```
Used in mission initialisation scripts.
Must be used between calls to **AddObjective** and **CloseObjective**.
Compatible with `dialogue` objectives.
Sets the conversation camera mode to *ConversationCamMode*;
- `pc_near`;
- `pc_far`;

~~ADDYNOKNOW~~ Sure?

### SetConversationCamNpcName
```
SetConversationCamNpcName(str:ConversationCamMode);
SetConversationCamNpcName("npc_near");
```
Used in mission initialisation scripts.
Must be used between calls to **AddObjective** and **CloseObjective**.
Compatible with `dialogue` objectives.
Sets the conversation camera mode to *ConversationCamMode*:
- `npc_near`;
- `npc_far`;

~~ADDYNOKNOW~~ Sure?

### SetConversationCam
```
SetConversationCam(int:DialogueLineID, str:ConversationCamMode, str:BonusMissionType);
SetConversationCam(0, "pc_near");
SetConversationCam(2, "npc_far", "bm1");
```
Used in level/mission initialisation scripts.
If being called in a mission, is compatible with `dialogue` objective type and should be between calls to **AddObjective** and **CloseObjective**.
Controls the conversation camera during a conversation.
Can be repeated for multiple/any dialogue lines.
Sets the conversation camera for *DialogueLineID* (zero-based) to *ConversationCamMode*:
- `pc_near`;
- `pc_far`;
- `npc_near`;
- `npc_far`;

If being called in a level, *BonusMissionType* should be specified to bind the conversation camera control to the conversation relevant to starting a particular Bonus Mission type: `bm1`, `sr1`, `sr2`, or `sr3`.
~~ADDYNOKNOW~~ Handling of +10 line convs?

### SetConversationCamDistance
```
SetConversationCamDistance(int:?, float:Distance);
SetConversationCamDistance("pc_far", 12);
SetConversationCamDistance(4, 15);
```
Sets how far away the conversation camera is (*Distance*) during *?*, which is unknown. It may be a camera type (as set through other dialogue functions like **SetConversationCam**) or a line number in the conversation or neither.
~~ADDYNOKNOW~~ Dialogue function weirdness.

### AmbientAnimationRandomize
```
AmbientAnimationRandomize(int:Character, int:Random);
AmbientAnimationRandomize(0, 1);
AmbientAnimationRandomize(1, 1);
```
Used in mission initialisation scripts.
Must be used between calls to **AddObjective** and **CloseObjective**.
Compatible with `dialogue` objective type..
Enables/disables random animations during dialogue sequence for player/NPC.
Can be called once for either character.
*Character* can be set to `0` to refer to the player, or `1` for the NPC.
*Random* can be set to `0` to disable random animations, or `1` to enable.

### ClearAmbientAnimations
```
ClearAmbientAnimations(str:BonusMissionType);
ClearAmbientAnimations("sr3");
```
Used in level initialisation scripts.
Must be used between calls to **AddObjective** and **CloseObjective**.
Clears ambient animations for the character hosting the Bonus Mission *BonusMissionType* (`bm1`, `sr1`, `sr2`, `sr3`).
~~ADDYNOKNOW~~ What do?

### AddAmbientPcAnimation
```
AddAmbientPcAnimation(str:Animation, str:BonusMissionType);
AddAmbientPcAnimation("dialogue_cross_arms");
AddAmbientPcAnimation("none", "bm1");
```
Used in level/mission initialisation scripts. Can be repeated.
Must be between calls to **AddObjective** and **CloseObjective** if used in a mission.
Compatible with `dialogue` objective type.
Makes the player character do *Animation* (must be in the "npd" animation set) on an inferred dialogue line in the conversation.
If being called in a level, *BonusMissionType* should be set to the relevant Bonus Mission type/conversation (`bm1`, `sr1`, `sr2`, `sr3`).
The line is inferred by the number of calls made to the function - the first call sets the animation for line one, the second for line two, and so forth. ~~ADDYNOKNOW~~ Inclusive of player lines only?
*Animation* can be set to `none` to skip/default animation on a line.

### AddAmbientNpcAnimation
```
AddAmbientNpcAnimation(str:Animation, str:BonusMissionType);
AddAmbientNpcAnimation("dialogue_cross_arms");
AddAmbientNpcAnimation("none", "bm1");
```
Used in level/mission initialisation scripts. Can be repeated.
Must be between calls to **AddObjective** and **CloseObjective** if used in a mission.
Compatible with `dialogue` objective type.
Makes the NPC character do *Animation* (must be in the "npd" animation set) on an inferred dialogue line in the conversation.
If being called in a level, *BonusMissionType* should be set to the relevant Bonus Mission type/conversation (`bm1`, `sr1`, `sr2`, `sr3`).
The line is inferred by the number of calls made to the function - the first call sets the animation for line one, the second for line two, and so forth. ~~ADDYNOKNOW~~ Inclusive of NPC lines only?
*Animation* can be set to `none` to skip/default animation on a line.
~~ADDYNOKNOW~~ Sure?

### CharacterIsChild
```
CharacterIsChild();
CharacterIsChild();
```
Used in mission initialisation scripts.
Must be used between calls to **AddObjective** and **CloseObjective**.
Compatible with `dialogue` objective type.
In theory pans the conversation camera lower during `dialogue` objectives.
In practice seems to do nothing.

### SetPresentationBitmap
```
SetPresentationBitmap(str:BitmapPath);
SetPresentationBitmap("art\frontend\dynaload\images\mis01_00.p3d");
```
Used in mission initialisation scripts.
Must be used between calls to **SelectMission** and **CloseMission**.
Sets the image to show on the mission briefing screen.
*BitmapPath* sets path (relative to the game's root directory) to a P3D file containing the relevant sprite (of the same name plus ".png") to show.
The game keeps one bitmap in memory and swaps it when given the function.
If no bitmap has yet been set, one will not be shown.

### SetAnimCamMulticontName
```
SetAnimCamMulticontName(str:AnimCamMulticontName);
SetAnimCamMulticontName("intro_camera");
```
Used in mission initialisation scripts.
Must be used between calls to **SelectMission** and **CloseMission**.
Set the multicontroller name for the optional mission start camera as *AnimCamMulticontName*. Must be loaded.

### SetAnimatedCameraName
```
SetAnimatedCameraName(str:AnimatedCameraName);
SetAnimatedCameraName("intro_cameraShape");
```
Used in mission initialisation scripts.
Must be used between calls to **SelectMission** and **CloseMission**.
Set the animated camera name for the optional mission start camera as *AnimatedCameraName*. Must be loaded.

### SetMissionStartMulticontName
```
SetMissionStartMulticontName(str:MissionStartMulticontName);
SetMissionStartMulticontName("intro_camera");
```
Used in mission initialisation scripts.
Must be used between calls to **SelectMission** and **CloseMission**.
Set the multicontroller name for the optional mission start camera as *MissionStartMulticontName*. Must be loaded.

### SetMissionStartCameraName
```
SetMissionStartCameraName(str:MissionStartCameraName);
SetMissionStartCameraName("intro_cameraShape");
```
Used in mission initialisation scripts.
Must be used between calls to **SelectMission** and **CloseMission**.
Set the optional mission start camera name as *MissionStartCameraName*. Must be loaded.

### SetCamBestSide
```
SetCamBestSide(str:Locator);
SetCamBestSide("m7_bestside");
```
Used in mission initialisation scripts.
Must be used between calls to **AddObjective** and **CloseObjective**.
Compatible with `dialogue` objective type.
Uses Locator Type 3 *Locator* to better position/point the conversation camera during dialogue.

### SetFMVInfo
```
SetFMVInfo(str:RMV, str/float/int:StopMusic);
SetFMVInfo("fmv1A.rmv");
```
Used in mission initialisation scripts.
Must be used between calls to **AddObjective** and **CloseObjective**.
Compatible with `fmv` objective type.
Sets RMV movie file to play to *RMV* path (rooted in "/movies/").
If a second argument (*StopMusic*) is at all present, regardless of *what* it is, the game stops execution of the most recently set music event (typically the level explore cues one).
~~ADDYNOKNOW~~ 2nd argument limits? Specifics?

### StartCountdown
```
StartCountdown(str:Noboxconv);
StartCountdown("");
StartCountdown("count");
```
Used in mission initialisation scripts.
Must be used between calls to **AddStage** and **CloseStage**.
Adds a countdown to the stage - see also **AddToCountdownSequence**.
Player control is mostly locked (besides pausing/thus vehicle exit) during the countdown.
*Noboxconv* sets the name of a noboxconv dialogue sequence to start alongside the countdown. See also "Specific notes" -> "Referencing sound resources in scripts".
This argument is not optional, but can be left blank or invalid without error/crash.

### AddToCountdownSequence
```
AddToCountdownSequence(str:Text, int:Milliseconds);
AddToCountdownSequence("3", 1000);
AddToCountdownSequence("2", 1000);
AddToCountdownSequence("1", 1000);
AddToCountdownSequence("GO", 500);
```
Used in mission initialisation scripts. Repeatable.
Must be used between calls to **AddStage** and **CloseStage**.
Must be used alongside **StartCountdown**.
Adds a paused time duration (*Milliseconds*) and text display (*Text*, if possible with the font) to the stage countdown.

### SetCarStartCamera
```
SetCarStartCamera(str:CarStartCamera);
SetCarStartCamera("mission6cam");
```
Unknown context.
In theory sets a camera for a vehicle spawn.
Seems to do nothing.

### GoToPsScreenWhenDone
```
GoToPsScreenWhenDone();
GoToPsScreenWhenDone();
```
Used in mission initialisation scripts.
Must be used between calls to **AddStage** and **CloseStage**.
Shows the "# OF 3 RACES COMPLETE" screen after the containing mission completes.

### SetPlayerCarName
```
SetPlayerCarName(int:PlayerIndex, str:VehicleName);
SetPlayerCarName(0, "ccar_v");
```
Unknown context.
In theory sets the *VehicleName* (internal name) for *PlayerIndex* (zero based, 0-3/1-4).
In practice seems to do nothing.

### SetCondMinHealth
```
SetCondMinHealth(float:MinHealth);
SetCondMinHealth(0.0);
```
Used in mission initialisation scripts.
Must be used between calls to **AddCondition** and **CloseCondition**.
Used by Radical a lot. In theory sets minimum health before failure with a `damage` condition active.
In reality does absolutely nothing but supported.

### LoadP3DFile
```
LoadP3DFile(str:Path, str:MemoryAllocator, str:Slot);
LoadP3DFile("art\missions\level03\level.p3d");
```
Used in Bonus Game/level/mission load scripts. Repeatable.
Loads the contents of a P3D file (*Path*, rooted in game root directory) into memory for game/script use. Unloads when the Bonus Game/level/mission segment does, though in some cases not entirely or properly.
Best practice is to load more persistent/trigger-y things as Dyna Load zones only, only call **LoadP3DFile** in load scripts, and not load mission vehicles (if they aren't already level-loaded vehicles) via **LoadP3DFile**.
*MemoryAllocator* assigns the file/load a memory allocator (use unknown):
- `GMA_DEFAULT`;
- `GMA_TEMP`;
- `GMA_PERSISTENT`;
- `GMA_LEVEL`;
- `GMA_LEVEL_MOVIE`;
- `GMA_LEVEL_FE`;
- `GMA_LEVEL_ZONE`;
- `GMA_LEVEL_OTHER` is often used for the level-loaded "l0#_fx.p3d" files;
- `GMA_LEVEL_HUD`;
- `GMA_LEVEL_MISSION`;
- `GMA_LEVEL_AUDIO`;
- `GMA_DEBUG`;
- `GMA_SPECIAL`;

*Slot* can optionally assign the slot `Global` (use unknown).

### LoadDisposableCar
```
LoadDisposableCar(str:Path, str:Vehicle, str:Type);
LoadDisposableCar("art\cars\cSedan.p3d","cSedan","AI");
```
Used in level/mission load scripts. Repeatable.
Loads a vehicle for usage and then disposal.
*Path* sets the P3D filepath (rooted in game root directory).
*Vehicle* sets the vehicle's internal name.
*Type* sets the vehicle's intended type/usage:
- `DEFAULT` for the level default vehicle;
- `OTHER` for a forced vehicle in a forced car mission;
- `AI` for a mission-controlled AI vehicle;
- `CHASE` is unknown/unused; ~~ADDYNOKNOW~~

### SetRespawnRate
```
SetRespawnRate(str:Type, float:Seconds);
SetRespawnRate("wrench", 15.0);
SetRespawnRate("nitro", 10.0);
```
Used in Bonus Game/level/mission initialisation scripts. Repeatable.
Allows setting the respawn rate for Wrenches/Nitros in *Seconds*.
*Type* can be `wrench` for Wrenches or `nitro` for Nitros.
If an instance of either object is unloaded/reloaded, it reappears regardless as the timer is cancelled in that case.

### AddCharacter
```
AddCharacter(str:Character, str:AnimationSet);
AddCharacter("homer", "homer");
```
Used in level initialisation scripts.
Sets the level's player character by internal name *Character*, using animation set of internal name *AnimationSet* - these typically match.

### AddNPCCharacterBonusMission
```
AddNPCCharacterBonusMission(str:Character, str:AnimationSet, str:Locator, str:BonusMissionType, str:NormalDrawable, str:Convinit, int:Unreplayable, str:CompleteDrawable);
AddNPCCharacterBonusMission("nelson", "npd", "nel_loc", "sr2", "checkered", "race2", 0, "checkeredfinish");
```
Used in level initialisation scripts. Repeatable.
Adds a Bonus Mission (*BonusMissionType*: `bm1`, `sr1`, `sr2`, `sr3`, `gr1`) host (*Character*, using *AnimationSet*) by internal name to the level at Locator Type 3 *Locator* (should be loaded). Talking with them starts convinit sequence *Convinit*, unless *BonusMissionType* is `gr1` (see "Specific notes" -> "Referencing sound resources in scripts").
*NormalDrawable* appears above the host if the mission is incomplete.
If the mission is complete and *Unreplayable* is `0`, *CompleteDrawable* is instead used.
Either drawable should be loaded.
If *Unreplayable* is set to `1`, the mission cannot be replayed once completed.

### SetBonusMissionDialoguePos
```
SetBonusMissionDialoguePos(str:BonusMissionType, str:PlayerCharacter, str:Host, str:Vehicle);
SetBonusMissionDialoguePos("bm1", "hom_loc", "clt_loc", "car_oob");
```
Used in level initialisation scripts. Repeatable.
During the conversation to start Bonus Mission *BonusMissionType* (`bm1`, `sr1`, `sr2`, `sr3`), moves player character to Locator Type 3 *PlayerCharacter*, host to Locator Type 3 *Host*, and player current vehicle to Locator Type 3 *Vehicle* (if the vehicle is too close).
The vehicle is returned afterwards.
All Locator Type 3s should be loaded.
~~ADDYNOKNOW~~ Vehicle stuff.

### AddAmbientCharacter
```
AddAmbientCharacter(str:Character, str:Locator, float:Radius);
AddAmbientCharacter("jimbo", "mX_jimbo", 0);
AddAmbientCharacter("ralph", "mX_ralph", 1.5);
```
Used in level initialisation scripts. Repeatable.
Adds *Character* (internal name) to the level as an ambient character, at position *Locator* (loaded, Type 3).
If *Radius* is greater than `0`, it is the radius within which the character can be talked to.
Dialogue use varies:
- If the character doesn't have reply lines, they will not speak.
- If the character is not `apu` or `teen`, player character will use a `w_greeting` line, and ambient character will use a `w_idlereply` line.
- If the character is `apu` or `teen`, player character will use a `w_askfood` line, and ambient character will use a `w_foodreply` line.
- Lines are chosen at random.

### AddBonusMissionNPCWaypoint
```
AddBonusMissionNPCWaypoint(str:Character, str:Locator);
AddBonusMissionNPCWaypoint("milhouse", "milhouse_walkto");
```
Used in level initialisation scripts.
Assigns Bonus Mission host *Character* (internal name) a waypoint for their walk path, *Locator* (Type 3, loaded).
Repeatable to build up a path.
Waypoint paths are optional.
~~ADDYNOKNOW~~ Returns to first or start point?

### AddObjectiveNPCWaypoint
```
AddObjectiveNPCWaypoint(str:Character, str:Locator);
AddObjectiveNPCWaypoint("wiggum", "wiggum_walkto");
```
Used in mission initialisation scripts.
Must be used between calls to **AddObjective** and **CloseObjective**.
Assigns stage/objective **AddNPC** NPC *Character* (internal name) a waypoint for their walk path, *Locator* (Type 3, loaded).
Repeatable to build up a path.
Waypoint paths are optional.
~~ADDYNOKNOW~~ Returns to first or start point?

### AddAmbientNPCWaypoint
```
AddAmbientNPCWaypoint(str:Character, str:Locator);
AddAmbientNPCWaypoint("otto", "otto_walkto");
```
Used in level initialisation scripts.
Assigns ambient character *Character* (internal name) a waypoint for their walk path, *Locator* (Type 3, loaded).
Repeatable to build up a path.
Waypoint paths are optional.
~~ADDYNOKNOW~~ Returns to first or start point?

### AddPurchaseCarNPCWaypoint
```
AddPurchaseCarNPCWaypoint(str:Character, str:Locator);
AddPurchaseCarNPCWaypoint("kearney", "kearney_walkto");
```
Used in level initialisation scripts.
Assigns vendor *Character* (internal name) a waypoint for their walk path, *Locator* (Type 3, loaded).
Repeatable to build up a path.
Waypoint paths are optional.
~~ADDYNOKNOW~~ Returns to first or start point?

### ActivateTrigger
```
ActivateTrigger(str:Locator);
ActivateTrigger("abc");
```
Used in mission initialisaton scripts.
Must be called between **AddStage** and **CloseStage**.
In theory activates the triggers of a *Locator* (loaded, Type 0).
In practice seems to do nothing.

### DeactivateTrigger
```
DeactivateTrigger(str:Locator);
DeactivateTrigger("def");
```
Used in mission initialisaton scripts.
Must be called between **AddStage** and **CloseStage**.
In theory deactivates the triggers of a *Locator* (loaded, Type 0).
In practice seems to do nothing.

### CreateAnimPhysObject
Unknown context.
Unknown use.
~~ADDYNOKNOW~~

### CreateActionEventTrigger
Unknown context.
Unknown use.
~~ADDYNOKNOW~~

### LinkActionToObjectJoint
Unknown context.
Unknown use.
~~ADDYNOKNOW~~

### LinkActionToObject
Unknown context.
Unknown use.
~~ADDYNOKNOW~~

### SetCoinDrawable
```
SetCoinDrawable(str:Drawable);
SetCoinDrawable("coinShape_000");
```
Used in level initialisation scripts.
Sets the drawable used to represent coins to loaded *Drawable*.

### SetParticleTexture
```
SetParticleTexture(int:Type, str:Texture);
SetParticleTexture(0, "scratch2.bmp");
```
Used in level initialisation scripts. Repeatable.
Sets the particle effect texture for effect *Type* to loaded *Texture*.
*Type* can be:
- `0` for sparkles;
- `1` for vehicle collison sparks;
- `2` for player character run/jump dust cloud;
- `3` for leaf effects for leafy props.
- `4` for static collision stars;
- `5` for vehicle damage paint chips;
- `6` for shock wave ring;

~~ADDYNOKNOW~~

### SetCharacterPosition
```
SetCharacterPosition(str:Character, float:X, float:Z);
SetCharacterPosition("homer", 0, 0);
```
Unknown context.
In theory sets the *X* and *Z* positions for a player *Character* (internal name).
In practice seems to do nothing.

### ResetCharacter
```
ResetCharacter(str:Character, str:Locator);
ResetCharacter("apu", "m1_apu_start");
```
Used in mission initialisation scripts.
Must be called between **SelectMission** and **CloseMission**.
Teleports player *Character* (internal name) to *Locator* (loaded, Type 3) on stage/objective reach.
Only occurs on *natural reach* - if called in the script for Mission 3's main segment, it would execute only when Mission 2 is completed, or when Mission 3 is cancelled.
If the player is in a vehicle when the teleport occurs, they end up in a bugged state where the player character is teleported and out of the vehicle but the player remains in control of the vehicle.

### AddTeleportDest
```
AddTeleportDest(str:Text, float:X, float:Y, float:Z, str:DynaLoadDataString);
AddTeleportDest("Origin", 0, 0, 0, "l1z1.p3d;");
```
Used in level load scripts. Repeatable.
Adds a teleport destination to the level, accessible with the debug Phone Booth teleport menu.
The destination is set as coordinites - *X*/*Y*/*Z*.
*DynaLoadDataString* is executed to load world chunks and all loaded prior are unloaded. See "Specific notes" -> "Dyna Load Data String format".
The menu item will have the text *Text*, so long as the font can represent it.

### SetInitialWalk
```
SetInitialWalk(str:Locator);
SetInitialWalk("gotohererun");
```
Used in mission initialisation scripts.
Locks controls and makes player character walk to position *Locator* (Type 3/loaded) when the mission is warped to.
~~ADDYNOKNOW~~ Start in car, normal mission segment.

### AddVehicleSelectInfo
```
AddVehicleSelectInfo(str:Path, str:Vehicle, str:Driver);
AddVehicleSelectInfo("art\cars\snake_v.p3d", "snake_v", "snake");
```
Used in level load scripts.
In theory adds vehicle selection information for *Vehicle* (internal name), including that, its *Path* (rooted in game root directory), and its *Driver* (internal name).
In practice seems to do nothing.

### ClearVehicleSelectInfo
```
ClearVehicleSelectInfo();
ClearVehicleSelectInfo();
```
Used in level load scripts.
In theory undoes previous calls to **AddVehicleSelectInfo**.
In practice seems to do nothing.

### AddFlyingActor
```
AddFlyingActor(str:Actor, str:Instance, float:X, float:Y, float:Z);
AddFlyingActor("spaceship", "FloatyOne", 0, 0, 0);
```
Used in level initialisation scripts.
In theory adds a Flying Actor (*Actor*) with an instance name (*Instance*) to the world at position *X*/*Y*/*Z*.
In practice seems to do nothing.

### AddFlyingActorByLocator
```
AddFlyingActorByLocator(str:Actor, str:Instance, str:Locator, str:Parameter);
AddFlyingActorByLocator("spaceship", "FloatyOne", "sship", "NEVER_DESPAWN");
```
Used in level initialisation scripts.
Adds a Flying Actor (*Actor*) with an instance name (*Instance*) to the world at position *Locator* (loaded, Type 3).
*Parameter* is optional; can be set to `NEVER_DESPAWN`.
If this is unset, the Flying Actor only spawns in if the player spawns close - once/if too far away, it does not spawn or return until a full level reload where closeness is also correct.

### AddBehaviour
```
AddBehaviour(str:Actor, str:Mode, float/str:Attribute1, float/str:Attribute2, float/str:Attribute3, float/str:Attribute4, float/str:Attribute5);
AddBehaviour("beecamera", "ATTRACTION", 5.0, 10.0, 10.0);
AddBehaviour("beecamera", "ATTACK_PLAYER", 15.0, 0.0, 4.0);
AddBehaviour("beecamera", "EVADE_PLAYER", 10.0, 10.0, 10.0, 10.0, 7.0);
AddBehaviour("myStaticBee", "ATTRACTION", -1.0, -1.0, -1.0); // Make this one stay still...
```
Used in level initialisation scripts. Repeatable.
Sets behaviour attributes for `beecamera` or `spaceship` actor modes.
These must be preallocated and added prior via **PreallocateActors**/**AddSpawnPointByLocatorScript**/**AddFlyingActorByLocator/AddSpawnPoint**.
**For `beecamera` actors/instances:**
*Actor* should be set to `beecamera` or a specific instance added via **AddSpawnPointByLocatorScript** to target.
If *Mode* is `ATTRACTION`:
- *Attribute1* sets the *close* distance the player must be to the Wasp for it to exit `ATTRACTION` behaviour mode;
- *Attribute2* sets the *far* distance the player must be from the Wasp for it to enter `ATTRACTION` behaviour mode;
- *Attribute3* sets the Wasp's travel speed;
- *Attribute4*/*Attribute5* are disused;

If *Mode* is `ATTACK_PLAYER`:
- *Attribute1* sets the radius close to the Wasp within which it will charge/shoot projectiles at the player;
- *Attribute2* sets the arc that fired projectiles take;
- *Attribute3* sets the number of seconds the Wasp waits before going to `EVADE_PLAYER` behaviour following a projectile shoot;
- *Attribute4*/*Attribute5* are disused;

If *Mode* is `EVADE_PLAYER`:
- *Attribute1* is the Wasp's minimum horizontal evasion attempt distance;
- *Attribute2* is the Wasp's maximum horizontal evasion attempt distance;
- *Attribute3* is the Wasp's minimum vertical evasion attempt distance;
- *Attribute4* is the Wasp's maximum vertical evasion attempt distance;
- *Attribute5* is the Wasp's evasion attempt speed;

**For `spaceship` actors/instances:**
If *Mode* is `UFO_BEAM_ALWAYS_ON`:
- *Attribute1* is the UFO Beam name, typically `UfoBeam`;

~~ADDYNOKNOW~~ Flying Actor/spaceship/move/active stuff.

### SetCollisionAttributes
```
SetCollisionAttributes(str:Instance, float:Friction, float:Mass, float:Elasticity);
SetCollisionAttributes("a", 1, 2, 3);
```
Unknown context.
Unknown use.
Doesn't appear to work.

### AddSpawnPoint
```
AddSpawnPoint(str:SpawnPoint, str:Actor, str:Instance, float:X, float:Y, float:Z, float:Radius);
```
Adds a Wasp Camera spawn point, positioned at *X*/*Y*/*Z* (loaded Locator Type 3s) and sized as a *Radius*-size sphere.
*SpawnPoint* is a name for the spawn point; it can later be referenced via *AddBehaviour* to define behaviour for this Wasp Camera.
*Actor* is the actor name, typically `beecamera`.
*Instance* is the instance name, typically `Shelley`.

### AddSpawnPointByLocatorScript
```
AddSpawnPointByLocatorScript(str:Locator, str:Actor, str:Name, str:Locator, float:Radius, float:Radius);
AddSpawnPointByLocatorScript("myWasp", "beecamera", "Shelley", "myWasp", 10.0, 10.0);
```
Used in level initialisation scripts. Repeatable.
Adds a Wasp Camera spawn point.
The Wasp spawns at *Locator* (loaded/Type 2 or 3).
The spherical trigger to spawn the Wasp is centred there and *Radius* big.
*Actor* should be `beecamera` and *Name* should be `Shelley`.
~~ADDYNOKNOW~~ Double Locator/Radius? Name?

### SetProjectileStats
```
SetProjectileStats(str:Name, float:Speed, int:Capacity);
SetProjectileStats("waspray", 10.0, 3);
```
Used in level initialisation scripts.
Define the Wasp's projectile shooting.
*Name* should be `waspray`.
*Speed* sets the projectile travel speed - negative values go backwards.
*Capacity* sets how many concurrently active (but **not** shot in the same burst) projectiles can be processed - too high crashes game.

### PreallocateActors
```
PreallocateActors(str:ActorType, int:Amount);
PreallocateActors("beecamera", 3);
PreallocateActors("spaceship", 1);
```
Used in level initialisation scripts.
Allocates *Amount* of *ActorType*. That many can exist at once.
For example, if the level called **PreallocateActors** with arguments `beecamera` and `1`, and one Wasp was chasing the player, and the player entered a trigger to spawn a different Wasp, that second wasp cannot and will not spawn at that time.
Actors should be loaded.

### SetActorRotationSpeed
```
SetActorRotationSpeed(str:ActorName, float:RotationSpeed);
SetActorRotationSpeed("beecamera", 50.0);
```
Used in level initialisation scripts.
Sets the rotation speed for *ActorName* to *RotationSpeed*.
Values too high can be buggy.

### AddShield
```
AddShield(ActorType, ShieldName);
AddShield("beecamera", "beeshield");
```
Used in level initialisation scripts.
Makes instances of *ActorType* spawn with a shield, specified as *ShieldName*.
*ActorType* should usually be `beecamera` and *SheldName* should usually be `beeshield`.
~~ADDYNOKNOW~~ Can shield specific Wasps? Can shield spaceship?

### ClearGagBindings
```
ClearGagBindings();
ClearGagBindings();
```
Used in level load/initialisation scripts.
Ignores any *prior* calls to **AddGagBinding** in the script.

### AddGagBinding
```
AddGagBinding(str:Interior, str:Gag, str:AnimationMode, str:SoundResource, float:Weight);
AddGagBinding("Android", "gag0300.p3d", "cycle", "gag_vroom", 1.0);
```
Used in level load/initialisation scripts.
Binds gag *Gag* (P3D path rooted in "/art/nis/gags/") to interior *Interior* (internal name). Coordinites are P3D-set/absolute.
Interior-bound gags load/activate whenever the interior does.
If multiple exist for a single interior, the used gag is randomised.
*Weight* can override randomity weight/chance; non-specified weights are inferred.
*AnimationMode* can be set to:
- `single` plays the gag animation once;
- `reset` is broken compared to as in **GagSetCycle**;
- `cycle` loops the gag animation repeatedly;

*SoundResource* is the name of a sound resource to play whilst the gag is active. See also "Specific notes" -> "Referencing sound resources in scripts".

### GagBegin
```
GagBegin(str:Gag);
GagBegin("gag_jar.p3d");
```
Used in level initialisation scripts.
Begins definition of a gag.
Must be followed by **GagEnd**; optionally between them other setup functions.
*Gag* sets the gag's P3D path, rooted in "/art/nis/gags/".

### GagSetInterior
```
GagSetInterior(str:Interior);
GagSetInterior("SimpsonsHouse");
```
Used in level initialisation scripts.
Must be called between **GagBegin** and **GagEnd**.
Sets *Interior* (internal name) as the gag's native interior space.
If **GagSetRandom** is called with `1`, all gags with the same **GagSetInterior** are considered one randomisation pool.
Gags that use **GagSetInterior** load/unload with the interior space.
Gags that are not slated to appear via randomity outcome are not loaded, however.

### GagSetCycle
```
GagSetCycle(str:AnimationMode);
GagSetCycle("reset");
```
Used in level initialisation scripts.
Must be called between **GagBegin** and **GagEnd**.
Sets the gag's *AnimationMode*, once triggered:
- `single` allows the trigger/animation once;
- `reset` allows the trigger/animation repeatedly;
- `cycle` loops the animation repeatedly on trigger;

### GagSetWeight
```
GagSetWeight(float:Weight);
GagSetWeight(0.5);
```
Used in level initialisation scripts.
Must be called between **GagBegin** and **GagEnd**.
Sets randomity weight (*Weight*) for a gag that also calls **GagSetRandom**.
This controls the chance of the gag spawning relative to others.
Unspecified weights are inferred.

### GagSetSound
```
GagSetSound(str:SoundResource);
GagSetSound("gag_lvl2_dumpster");
```
Used in level initialisation scripts.
Must be called between **GagBegin** and **GagEnd**.
Sets the sound resource to play on gag trigger as *SoundResource*.
See also "Specific notes" -> "Referencing sound resources in scripts".

### GagSetTrigger
```
GagSetTrigger(str:Type, float/str:Parameter1, float:Parameter2, float:Parameter3, float:Parameter4);
GagSetTrigger("touch", 0, 0, 0, 5);
GagSetTrigger("action", "GTrig", 5);
```
Used in level initialisation scripts.
Must be called between **GagBegin** and **GagEnd**.
Sets up the trigger mode/position/size for the gag.
The mode is set by *Type*:
- `touch` triggers the gag when within the set spherical trigger radius;
- `action` triggers the gag when ACTION is pressed within the set spherical trigger radius;

The remaining arguments can be provided in two different ways:
- Method 1 uses *Parameter1* to set trigger X position, *Parameter2* for Y position, *Parameter3* for Z position, and *Parameter4* for radius/size;
- Method 2 uses *Parameter1* to set a Locator Type 2 (must be loaded) that holds the gag's positions and *Parameter2* to set radius/size;

~~ADDYNOKNOW~~ M2 LT2 loaded weirdness/picky.

### GagPlayFMV
```
GagPlayFMV(str:RMV);
GagPlayFMV("tele.rmv");
```
Used in level initialisation scripts.
Must be called between **GagBegin** and **GagEnd**.
Makes the gag play movie *RMV* (rooted in "/movies") on trigger.
If the gag *also* calls **GagSetSound**, the latter is ignored.

### GagSetPosition
```
GagSetPosition(float/str:X, float:Y, float:Z);
GagSetPosition(0, 0, 0);
GagSetPosition("scope");
```
Used in level initialisation scripts.
Must be called between **GagBegin** and **GagEnd**.
Sets the gag's spawn position as coordinites *X*/*Y*/*Z*.
If *X* is set to a loaded Locator Type 2 name, that is used instead.
~~ADDYNOKNOW~~ LT2 loaded weirdness/picky.

### GagSetRandom
```
GagSetRandom(int:Random);
GagSetRandom(0);
```
Used in level initialisation scripts.
Must be called between **GagBegin** and **GagEnd**.
Sets of the gag is part of a random pool (`1`) or not (`0`) via *Random*.
Randomity pool encompasses nearby gags, or is limited to all that call **GagSetRandom** with `1` in addition to sharing the same parameter for **GagSetInterior**.

### GagSetIntro
```
GagSetIntro(int:EndFrame);
GagSetIntro(30);
```
Used in level initialisation scripts.
Must be called between **GagBegin** and **GagEnd**.
Makes the gag play every animation frame up to *EndFrame* prior to trigger.

### GagSetOutro
```
GagSetOutro(int:StartFrame);
GagSetOutro(110);
```
Used in level initialisation scripts.
Must be called between **GagBegin** and **GagEnd**.
Makes the gag play every animation frame after *StartFrame* post-trigger.

### GagSetCameraShake
```
GagSetCameraShake(float:WaitSeconds, float:?, float:ShakeSeconds);
GagSetCameraShake(0.0, 1.0, 5.0);
```
Used in level initialisation scripts.
Must be called between **GagBegin** and **GagEnd**.
Makes the gag shake the camera for *ShakeSeconds*, after waiting *WaitSeconds* post-trigger.
*ShakeSeconds* can be set to a negative value like `-1` for infinite length.
Shake is forcibly disabled upon entering a vehcle or camera trigger.
The purpose of *?* is unknown. ~~ADDYNOKNOW~~

### GagSetCoins
```
GagSetCoins(int:Coins, float:Delay);
GagSetCoins(1, -1);
```
Used in level initialisation scripts.
Must be called between **GagBegin** and **GagEnd**.
Makes the gag give *Coins* coins to the player *Delay* seconds post-trigger.
*Delay* can be set to a negative value like `-1` to automatically give coins when the gag animation completes, however this will *never* occur if **GagSetCycle** is called as `cycle` or **GagSetOutro** is at all called.
If **GagSetPersist** is called as `1`, any given level gag only rewards coins for first trigger on save file.

### GagSetSparkle
```
GagSetSparkle(int:Sparkle);
GagSetSparkle(1);
```
Used in level initialisation scripts.
Must be called between **GagBegin** and **GagEnd**.
Places a blue sparkle effect at the gag's trigger spot that disappears post-trigger.
If **GagSetPersist** is called as `1`, any given level gag only features the sparkle up until first trigger on save file.

### GagSetAnimCollision
```
GagSetAnimCollision(int:AnimCollision);
GagSetAnimCollision(1);
```
Used in level initialisation scripts.
Must be called between **GagBegin** and **GagEnd**.
Enables (`1`) or disables (`0`) gag collision changes in accordance with the animation, if possible.

### GagEnd
```
GagEnd();
GagEnd();
```
Used in level initialisation scripts.
Ends definition of a level gag.

### GagSetLoadDistances
```
GagSetLoadDistances(float:Distance, float:Distance);
GagSetLoadDistances(50.0, 50.0);
```
Used in level initialisation scripts.
Must be called between **GagBegin** and **GagEnd**.
Sets *Distance* as how close the player must be to load in the gag.
~~ADDYNOKNOW~~ Same distance?

### GagSetSoundLoadDistances
```
GagSetLoadDistances(float:Distance, float:Distance);
GagSetLoadDistances(50.0, 50.0);
```
Used in level initialisation scripts.
Must be called between **GagBegin** and **GagEnd**.
In theory, sets *Distance* as how close the player must be to load in the gag sound.
In practice, all gag sounds are streamed, and setting the only alternative is to entirely preload sounds for the whole game run.
~~ADDYNOKNOW~~ Same distance?

### GagSetPersist
```
GagSetPersist(int:Persist);
GagSetPersist(1);
```
Used in level initialisation scripts.
Must be called between **GagBegin** and **GagEnd**.
Enables (`1`) or disables (`0`) persistence for a level gag.
If enabled, the gag is tracked in save data and contributes to Level Progress.
As side-effects of being enabled, the application of behaviour relevant to **GagSetCoins** and **GagSetSparkle** is altered; see those functions.

### GagCheckCollCards
```
GagCheckCollCards(str:NPC, str:PC, str:ConvinitSecond, str:ConvinitFirst, str:ConvinitDone);
GagCheckCollCards("cbg", "lisa", "b", "a", "c");
```
Used in level initialisation scripts.
Must be called between **GagBegin** and **GagEnd**.
Makes the gag check Bonus Movie look state if the player has all fourty-nine Collector Cards on trigger, and reacts to the outcome by starting a conversation. See also "Specific notes" -> "Referencing sound resources in scripts".
*NPC* and *PC* set the internal names of conversation NPC and player character respectively.
*ConvinitFirst* sets the conversation name for first interacting with the gag, without all cards.
*ConvinitSecond* sets the conversation name for subsequent gag interactions, without all cards.
*ConvinitDone* sets the conversation name for interacting with the gag, with all cards.
~~ADDYNOKNOW~~ ISMovie hardcode rubbish, look into. Also, what if first trigger is with all?

### GagCheckMovie
```
GagCheckMovie(str:NPC, str:PC, str:RMV, str:ConvinitFail);
GagCheckMovie("teen", "lisa", "fmv8.rmv", "ticket");
```
Used in level initialisation scripts.
Must be called between **GagBegin** and **GagEnd**.
Makes the gag check if the player has unlocked the Bonus Movie, and react.
*RMV* is the movie file to play if Bonus Movie is unlocked (path rooted in "/movies/").
*NPC* and *PC* set the internal name of the characters involved in conversation if the Bonus Movie is not unlocked.
*ConvinitFail* sets the conversation name for if the Bonus Movie is not unlocked. See "Specific notes" -> "Referencing sound resources in scripts".
~~ADDYNOKNOW~~ ISMovie hardcode rubbish, look into. Multi convs/lines?

### AddVehicleCharacter
```
AddVehicleCharacter(str:Character, str:Joint, int:Rotation);
AddVehicleCharacter("homer", "pl", 190);
```
Used in vehicle configurations. Repeatable.
Exclusive to ASF.
Adds *Character* (internal name) to skeleton *Joint* on the vehicle, rotated by *Rotation* degrees (180 faces forwards).
*Joint* and *Rotation* are optional, defaulting to `pl` and `180` respectively.
*Joint* must exist within the vehicle's skeleton - common examples include `dl` (driver's seat), `pl` (passenger seat; not always present), and `sl` (smoke spawn spot).
~~ADDYNOKNOW~~ Subject to SuppressDriver?

### AddVehicleCharacterSuppressionCharacter
```
AddVehicleCharacterSuppressionCharacter(str:SuppressCharacter, str:ConditionCharacter);
```
Used in vehicle configurations. Repeatable.
Exclusive to ASF.
Compatible only with characters added via **AddVehicleCharacter**.
If *ConditionCharacter* is suppressed in the level via **SuppressDriver**, then *SuppressCharacter* will be too.
If *ConditionCharacter* is `none`, *SuppressCharacter* will not be subject to **SuppressDriver** suppression.
Uses internal names for characters.

### SetConditionalParameter
```
SetConditionalParameter(str:Parameter, str:Value1, str/float/int:Value2, str/float/int:Value3, str/float/int:Value4);
SetConditionalParameter("drawableVisibility", "myCarOddProp", "level", 1);
SetConditionalParameter("hasdoors", "vehicleHealth", 1.0, 1.5);
SetConditionalParameter("highroof", "level", 4);
```
Used in vehicle configurations. Repeatable.
Exclusive to ASF.
Allows limited vehicle parameters to change based on conditions.
If *Parameter* is `drawableVisibility`:
- *Value1* sets the name of the drawable to control visibility of;
- *Value2* sets the condition, which will control if the drawable is visible or not: `vehicleHealth` (based on hit points) or `level` (based on current level);
- *Value3* sets minimum vehicle health to show drawable if *Value2* is `vehicleHealth`, or level ID (1-7) to show drawable if *Value2* is `level`;
- *Value4* sets maximum vehicle health to show drawable if *Value2* is `vehicleHealth`, but has no use if *Value2* is `level`;

If *Parameter* is `hasdoors`:
- *Value1* sets the condition which will control if the drawable is visible or not: `vehicleHealth` (based on hit points) or `level` (bsed on current level);
- *Value2* sets minimum vehicle health to have doors if *Value1* is `vehicleHealth`, or level ID (1-7) to have doors if *Value2* is `level`;
- *Value3* sets maximum vehicle health to have doors if *Value1* is `vehicleHealth`, but has no use if *Value1* is `level`;
- *Value4* goes disused;

If *Parameter* is `highroof`:
- *Value1* sets the condition which will control if the roof is considered high or not, as in **SetHighRoof** - `vehicleHealth` (based on hit points) or `level` (based on current level);
- *Value2* sets minimum vehicle health to have high roof if *Value1* is `vehicleHealth`, or level ID (1-7) to have high roof if *Value1* is `level`;
- *Value3* sets maximum vehicle health to have high roof if *Value1* is `vehicleHealth`, but has no use if *Value1* is `level`;
- *Value4* goes disused;

### SetVehicleCharacterAnimation
```
SetVehicleCharacterAnimation(str:Character, str:Animation, int:InVehicleAnimations);
SetVehicleCharacterAnimation("bart", "flail");
```
Used in vehicle configurations. Repeatable.
Exclusive to ASF.
Compatible only with characters added via **AddVehicleCharacter**.
Makes *Character* (internal name) repeat *Animation*, which must be within the "npd" animation set.
*InVehicleAnimations* is optional and defaults to `0`; if set to `1`, the vehicle character is allowed to animate as drivers/passengers normally do and bob up/down (in addition to swaying left/right if the Bug Fix/hack is enabled).

### SetVehicleCharacterJumpOut
```
SetVehicleCharacterJumpOut(str:Character, int:Rotation);
SetVehicleCharacterJumpOut("bart", 55);
```
Used in vehicle configurations. Repeatable.
Exclusive to ASF.
Compatible only with characters added via **AddVehicleCharacter**.
Makes *Character* (internal name) jump out of the vehicle at angle *Rotation* on vehicle explode.

### SetVehicleCharacterScale
```
SetVehicleCharacterScale(str:Character, float:Scale);
SetVehicleCharacterScale("lenny", 1.5);
```
Used in vehicle configurations. Repeatable.
Exclusive to ASF.
Compatible only with characters added via **AddVehicleCharacter**.
Makes *Character* (internal name) appear as size *Scale* in the vehicle.

### SetVehicleCharacterVisible
```
SetVehicleCharacterVisible(str:Character);
SetVehicleCharacterVisible("lenny");
```
Used in vehicle configurations. Repeatable.
Exclusive to ASF.
Compatible only with characters added via **AddVehicleCharacter**.
Forces *Character* (internal name) to be visible, even if the vehicle configuration also calls **SetCharactersVisible** with `0`.

### SetWheelieOffsetX
```
SetWheelieOffsetX(float:WheelieOffsetX);
SetWheelieOffsetX(0.1);
```
Used in vehicle configurations.
Exclusive to ASF.
Set a vehicle's centre of mass X offset position when in a wheelie.
~~ADDYNOKNOW~~ Default?

### SetCarChangeHitAndRunChange
```
SetCarChangeHitAndRunChange(float:Change);
SetCarChangeHitAndRunChange(-100);
```
Used in level initialisation scripts.
Exclusive to ASF.
Changes how much the Hit & Run meter fills (positive value) or changes (negative value) when the player switches vehicle.
In the vanilla game this is `-100`.

### SetHitAndRunDecayHitAndRun
```
SetHitAndRunDecayHitAndRun(float:Decay);
SetHitAndRunDecayHitAndRun(6.0);
```
Used in level initialisation scripts.
Exclusive to ASF.
Set the amount to change the “Hit & Run!” meter by per second whilst in a "Hit & Run!"", via Decay. Relevant values range from -100.0 (fill meter) to 0 (no change) to 100.0 (empty meter).
In the vanilla game this is `6.0`.

### SetHitAndRunFine
```
SetHitAndRunFine(int:CoinFine);
SetHitAndRunFine(50);
```
Used in level initialisation scripts.
Exclusive to ASF.
Set *CoinFee* as the number of coins lost on being "Busted!" in a "Hit & Run!".
In the vanilla game this is `50`.

### AddParkedCar
```
AddParkedCar(str:Vehicle);
AddParkedCar("sportsB");
```
Used in level initialisation scripts. Repeatable.
Exclusive to ASF.
Makes it so that *Vehicle* (internal name, should be loaded) can randomly appear at parked vehicle spots throughout the level.

### SetHUDMapDrawable
```
SetHUDMapDrawable(str:Drawable);
SetHUDMapDrawable("l1hudmap");
```
Used in mission initialisation scripts.
Exclusive to ASF.
Must be used between calls to **SelectMission** and **CloseMission**.
Sets the radar map to *Drawable* on mission begin. Should be loaded.
Does *not* automatically reset the radar map on any mission exit event.

### SetParkedCarsEnabled
```
SetParkedCarsEnabled(int:ParkedCarsEnabled);
SetParkedCarsEnabled(0);
```
Used in mission initialisation scripts.
Exclusive to ASF.
Must be used between calls to **SelectMission** and **CloseMission**.
Enables (`1`) or disables (`0`) random parked traffic vehicles at parked vehicle spots throughout the level for the duration of the mission.
The default behaviour in the vanilla game is `0` in missions that call **StreetRacePropsLoad** and `1` everywhere else.

### SetPedsEnabled
```
SetPedsEnabled(int:PedsEnabled);
SetPedsEnabled(0);
```
Used in mission initialisation scripts.
Exclusive to ASF.
Must be used between calls to **SelectMission** and **CloseMission**.
Enables (`1`) or disables (`0`) pedestrians for the duration of the mission.
The default behaviour in the vanilla game is `0` in missions that call **StreetRacePropsLoad** and `1` everywhere else.

### UseTrafficGroup
```
UseTrafficGroup(int:GroupID);
UseTrafficGroup(1);
```
Used in mission initialisation scripts.
Exclusive to ASF.
Must be used between calls to **SelectMission** and **CloseMission**.
Force sets traffic group *GroupID* as the current/active on any mission restart.
Best used with the Custom Traffic Support hack/multiple groups.

### DisableTrigger
```
DisableTrigger(str:Locator);
DisableTrigger("SpringfieldElementaryEntry");
```
Used in mission initialisation scripts. Repeatable.
Exclusive to ASF.
Must be used between calls to **AddStage** and **CloseStage**.
Makes the triggers of (loaded) Locator Type 0 *Locator* ineffective for the duration of the stage/objective.
~~ADDYNOKNOW~~ Picky on when/where LT0 was created?

### AddStageVehicleCharacter
```
AddStageVehicleCharacter(str:Vehicle, str:Character, str:Joint, int:Rotation);
AddStageVehicleCharacter("snake_v", "captain", "pl", 180);
```
Used in mission initialisation scripts. Repeatable.
Exclusive to ASF.
Must be used between calls to **AddStage** and **CloseStage**.
Adds a character to a vehicle *for the duration of the stage*.
Works the same was as **AddVehicleCharacter**, except for that *Vehicle* exists to specify a vehicle internal name (or `current`) to use player current/most recent vehicle.

### RemoveStageVehicleCharacter
```
RemoveStageVehicleCharacter(str:Vehicle, str:Character);
RemoveStageVehicleCharacter("snake_v", "captain");
```
Used in mission initialisation scripts. Repeatable.
Exclusive to ASF.
Must be used between calls to **AddStage** and **CloseStage**.
Removes a *Character* from a *Vehicle*, if previously added via **AddStageVehicleCharacter**.
*Vehicle* can be set to `current`, which binds (if possible) to the vehicle the player was using when **AddStageVehicleCharacter** was previously called.

### SetStageVehicleCharacterAnimation
```
SetStageVehicleCharacterAnimation(str:Vehicle, str:Character, str:Animation, int:InVehicleAnimations);
SetStageVehicleCharacterAnimation("snake_v", "captain", "flail", 0);
```
Used in mission initialisation scripts. Repeatable.
Exclusive to ASF.
Must be used between calls to **AddStage** and **CloseStage**.
Control a character added via **AddStageVehicleCharacter**'s animations.
Works as with **SetVehicleCharacterAnimation**, except that *Vehicle* (internal name) should specify a vehicle (`current` for player current/most recent vehicle).

### SetStageVehicleCharacterJumpOut
```
SetStageVehicleCharacterJumpOut(str:Vehicle, str:Character, int:Angle);
SetStageVehicleCharacterJumpOut("snake_v", "captain", 2);
```
Used in mission initialisation scripts. Repeatable.
Exclusive to ASF.
Must be used between calls to **AddStage** and **CloseStage**.
Set the direction a character added via **AddStageVehicleCharacter** will jump out at when the vehicle explodes.
Works as with **SetVehicleCharacterJumpOut**, except that *Vehicle* (internal name) should specify a vehicle (`current` for player current/most recent vehicle).

### SetStageVehicleCharacterScale
```
SetStageVehicleCharacterScale(str:Vehicle, str:Character, float:Scale);
SetStageVehicleCharacterScale("snake_v", "captain", 0.5);
```
Used in mission initialisation scripts. Repeatable.
Exclusive to ASF.
Must be used between calls to **AddStage** and **CloseStage**.
Set the scale of a character added via **AddStageVehicleCharacter**.
Works as with **SetVehicleCharacterScale**, except that *Vehicle* (internal name) should specify a vehicle (`current` for player current/most recent vehicle).

### SetStageVehicleCharacterVisible
```
SetStageVehicleCharacterVisible(str:Vehicle, str:Character);
SetStageVehicleCharacterVisible("snake_v", "captain");
```
Used in mission initialisation scripts. Repeatable.
Exclusive to ASF.
Must be used between calls to **AddStage** and **CloseStage**.
Set the visibility of a character added via **AddStageVehicleCharacter**, overriding the vehicle configuration's **SetCharactersVisible** call.
Works as with **SetVehicleCharacterVisible**, except that *Vehicle* (internal name) should specify a vehicle (`current` for player current/most recent vehicle).

### ResetStageVehicleAbductable
```
ResetStageVehicleAbductable(str:Vehicle);
ResetStageVehicleAbductable("homer_v");
```
Used in mission initialisation scripts. Repeatable.
Exclusive to ASF.
Must be used between calls to **AddStage** and **CloseStage**.
Sets *Vehicle*'s spaceship-abductable state to its default, overriding any previous **SetStageVehicleAbductable** calls.
*Vehicle* must be an internal name, or `current` to refer to the vehicle the player was using when **SetStageVehicleAbductable** was called prior.

### SetStageVehicleAbductable
```
SetStageVehicleAbductable(str:Vehicle, int:Abductable);
SetStageVehicleAbductable("homer_v", 0);
```
Used in mission initialisation scripts. Repeatable.
Exclusive to ASF.
Must be used between calls to **AddStage** and **CloseStage**.
Makes *Vehicle* (internal name. or `current` refers to current/most recent) immune (`0`) or vulnerable (`1`) to the spaceship tractor beam pull via *Abductable*, overriding the default.

### SetStageVehicleAllowSeatSlide
```
SetStageVehicleAllowSeatSlide(str:Vehicle, int:AllowSeatSlide);
SetStageVehicleAllowSeatSlide("cArmor", 0);
```
Used in mission initialisation scripts. Repeatable.
Exclusive to ASF.
Must be used between calls to **AddStage** and **CloseStage**.
Enables (`1`) or disables (`0`) seat-slide entry animations for *Vehicle* via *AllowSeatSlide* (internal name or `current` for current/most recent).

### SetStageVehicleNoDestroyedJumpOut
```
SetStageVehicleDestroyedJumpOut(str:Vehicle);
SetStageVehicleNoDestroyedJumpOut("cCola");
```
Used in mission initialisation scripts. Repeatable.
Exclusive to ASF.
Must be used between calls to **AddStage** and **CloseStage**.
Makes the driver of *Vehicle* (internal name) not jump out of their vehicle on explosion.
Usable on loaded/active AI vehicles and player vehicles, however the effect sticks to player vehicles until a large reload.
Has a problem of some kind when the vehicle has a driver added via **AddDriver**. ~~ADDYNOKNOW~~

### SetStageVehicleReset
```
SetStageVehicleReset(str:Vehicle, int:AllowAutoReset);
SetStageVehicleReset("cCurator", 1);
```
Used in mission initialisation scripts. Repeatable.
Exclusive to ASF.
Must be used between calls to **AddStage** and **CloseStage**.
Sets it so that *Vehicle* (internal name, loaded, active AI) is allowed to automatically reset if stuck for long enough (`1`) or not (`0`) via *AllowAutoReset*, overriding the default which is decided by the vehicle's AI/behaviour type.

### ResetStageHitAndRun
```
ResetStageHitAndRun();
ResetStageHitAndRun();
```
Used in mission initialisation scripts.
Exclusive to ASF.
Must be used between calls to **AddStage** and **CloseStage**.
Resets "Hit & Run!" state on stage/objective reach.
Any existing meter fill/chasers will be removed.

### SetNoHitAndRunMusicForStage
```
SetNoHitAndRunMusicForStage();
SetNoHitAndRunMusicForStage();
```
Used in mission initialisation scripts.
Exclusive to ASF.
Must be used between calls to **AddStage** and **CloseStage**.
Disables "Hit & Run!" music for the duration of the stage/objective.

### SetStageCarChangeHitAndRunChange
```
SetStageCarChangeHitAndRunChange(float:Change);
SetStageCarChangeHitAndRunChange(-100);
```
Used in mission initialisation scripts.
Exclusive to ASF.
Must be used between calls to **AddStage** and **CloseStage**.
Sets vehicle change "Hit & Run!" meter change on a per-stage basis.
Functions as does **SetCarChangeHitAndRunChange**.

### SetStageHitAndRun
```
SetStageHitAndRun(float:Fill);
SetStageHitAndRun(50);
```
Used in mission initialisation scripts.
Exclusive to ASF.
Must be used between calls to **AddStage** and **CloseStage**.
Sets the "Hit & Run!" meter to *Fill* fullness on stage/objective reach.
A value of `0` represents an empty meter.
A value of `100` represents a full meter.

### SetStageHitAndRunDecay
```
SetStageHitAndRunDecay(float:Decay);
SetStageHitAndRunDecay(0);
```
Used in mission initialisation scripts.
Exclusive to ASF.
Must be used between calls to **AddStage** and **CloseStage**.
Works as **SetHitAndRunDecay** does but on a per-stage basis.

### SetStageHitAndRunDecayHitAndRun
```
SetStageHitAndRunDecayHitAndRun(float:Decay);
SetStageHitAndRunChangeHitAndRun(6);
```
Used in mission initialisation scripts.
Exclusive to ASF.
Must be used between calls to **AddStage** and **CloseStage**.
Works as **SetHitAndRunDecayHitAndRun** does but on a per-stage basis.

### SetStageHitAndRunDecayInterior
```
SetStageHitAndRunDecayInterior(float:Decay);
SetStageHitAndRunDecayInterior(-100);
```
Used in mission initialisation scripts.
Exclusive to ASF.
Must be used between calls to **AddStage** and **CloseStage**.
Works as the ASF-enabled **SetHitAndRunDecayInterior** does but on a per-stage basis.

### SetStageHitAndRunFine
```
SetStageHitAndRunFine(int:CoinFine);
SetStageHitAndRunFine(50);
```
Used in mission initialisation scripts.
Exclusive to ASF.
Must be used between calls to **AddStage** and **CloseStage**.
Works as **SetHitAndRunFine** does but on a per-stage basis.

### SetStageNumChaseCars
```
SetStageNumChaseCars(int:NumChaseCars);
SetStageNumChaseCars(3);
```
Used in mission initialisation scripts.
Exclusive to ASF.
Must be used between calls to **AddStage** and **CloseStage**.
Set the number of "Hit & Run!" chasers on a per-stage basis as *NumChaseCars*.
Valid range is 0-5 (values above three can lead to crashes).

### SetStageAllowMissionCancel
```
SetStageAllowMissionCancel(int:AllowMissionCancel);
SetStageAllowMissionCancel(0);
```
Used in mission initialisation scripts.
Exclusive to ASF.
Must be used between calls to **AddStage** and **CloseStage**.
Enables (`1`) or disables (`0`) mission cancelling from the Pause Menu for the duration of the stage/objective.
Vanilla game default is `0`.

### SetStageCharacterModel
```
SetStageCharacterModel(str:Character, str:AnimationSet);
SetStageCharacterModel("homer", "homer");
```
Used in mission initialisation scripts.
Exclusive to ASF.
Must be used between calls to **AddStage** and **CloseStage**.
Sets the player character (inclusive of model and dialogue) to *Character* (internal name) for the duration of the stage/objective.
Optionally, *AnimationSet* specifies an animation set to use (defaults to tht of *Character*); this can lead to bugs/crashes if another character's is used.

### SetStagePayout
```
SetStagePayout(int:Coins);
SetStagePayout(52);
```
Used in mission initialisation scripts.
Exclusive to ASF.
Must be used between calls to **AddStage** and **CloseStage**.
Gives the player a number of coins (*Coins*) upon stage/objective completion.

### AddObjTargetModel
```
AddObjTargetModel(str:InternalName);
AddObjTargetModel("fishtruc");
AddObjTargetModel("mobster");
```
Used in mission initialisation scripts. Repeatable.
Exclusive to ASF.
Must be used between calls to **AddObjective** and **CloseObjective**.
Compatible with `destroycars` and `hitpeds` objective types.
Adds a target vehicle or character by internal name (*InternalName*).

### SetObjExplosion
```
SetObjExplosion(int:ExplosionEffectID, float:XZScale, float:YScale);
SetObjExplosion(24, 2.0, 2.0);
```
Used in mission initialisation scripts.
Exclusive to ASF.
Must be used between calls to **AddObjective** and **CloseObjective**.
Compatible with `hitpeds` objective type.
Explodes kicked characters (if they are called by **AddObjTargetModel**) and removes them from play.
*ExplosionEffectID* sets the explosion effect, such as `24`.
*XZScale* sets the size of the explosion effect.
*YScale* sets the height of the explosion effect.
~~ADDYNOKNOW~~ Always removes? Level chars?

### SetCollectibleSoundEffect
```
SetCollectibleSoundEffect(str:SoundResource);
SetCollectibleSoundEffect("beep");
```
Used in mission initialisation scripts.
Exclusive to ASF.
Must be used between calls to **AddObjective** and **CloseObjective**.
Compatible with `delivery`, `dump`, and `race` objective types.
Overrides default sound resource to play when picking up a collectible via *SoundResource*. See "Specific notes" -> "Referencing sound resources in scripts".
The defaults vary:
- `level_#_pickup_sfx` for Levels 1-6;
- `monkey_collect` for Level 2 Mission 6 specifically;
- `nuclear_waste_collect` for Level 7;

### SetObjCameraName
```
SetObjCameraName(str:CameraName);
SetObjCameraName("cammy");
```
Used in mission initialisation scripts.
Exclusive to ASF.
Must be used between calls to **AddObjective** and **CloseObjective**.
Compatible with `camera` objective type.
Sets the camera's internal name to use as *CameraName* (must be loaded).

### SetObjMulticontName
```
SetObjMulticontName(str:MulticontName);
SetObjMulticontName("m_cammy");
```
Used in mission initialisation scripts.
Exclusive to ASF.
Must be used between calls to **AddObjective** and **CloseObjective**.
Compatible with `camera` objective type.
Sets the camera's multicontroller name to use as *MilticontName* (must be loaded).

### SetObjCanSkip
```
SetObjCanSkip(int:CanSkip);
SetObjCanSkip(0);
```
Used in mission initialisation scripts.
Exclusive to ASF.
Must be used between calls to **AddObjective** and **CloseObjective**.
Compatible with `camera` objective type.
Enable (`1`) or disable (`0`) optional user skipping of the stage/objective.
Default is `0`.

### SetObjNoLetterbox
```
SetObjNoLetterbox(int:NoLetterbox);
SetObjNoLetterbox(0);
```
Used in mission initialisation scripts.
Exclusive to ASF.
Must be used between calls to **AddObjective** and **CloseObjective**.
Compatible with `camera` objective type.
Enable (`0`) or disable (`1`) letterboxing during the stage/objective.
Default is `0`.

### SetObjUseCameraPosition
```
SetObjUseCameraPosition(int:UseCameraPosition);
SetObjUseCameraPosition(1);
```
Used in mission initialisation scripts.
Exclusive to ASF.
Must be used between calls to **AddObjective** and **CloseObjective**.
Enable (`1`) or disable (`0`) the camera acting as the player location during the stage/objective, notably effecting sound and the spawning of pedestrians/traffic on camera.
Set via *UseCameraPosition*.

### SetObjDecay
```
SetObjDecay(float:Decay, float:Delay);
SetObjDecay(5.0, 0.0);
```
Used in mission initialisation scripts.
Exclusive to ASF.
Must be used between calls to **AddObjective** and **CloseObjective**.
Compatible with `insidetrigger` and `outsidetrigger` objective types.
Must be used alongside **SetObjThreshold**.
*Decay* sets how much/fast the threshold meter empties when the player is within/outside of the trigger(s) specified via **SetObjTrigger**.
*Delay* sets how much safe time the player has before this takes effect, after entering/leaving the trigger(s).
By default there is no decay.
~~ADDYNOKNOW~~ Negative values?

### SetObjMessageIndex
```
SetObjMessageIndex(int:StageMessageIndex);
SetObjMessageIndex(202);
```
Used in mission initialisation scripts.
Exclusive to ASF.
Must be used between calls to **AddObjective** and **CloseObjective**.
Compatible with `insidetrigger` and `outsidetrigger` objective types.
Show a stage message when the player is within/outside of the trigger(s).
Specify by numeric ID (*StageMessageIndex*) in the textbible, where the strings are named as “MISSION_OBJECTIVE_#”.

### SetObjThreshold
```
SetObjThreshold(float:Time);
SetObjThreshold(5);
```
Used in mission initialisation scripts.
Exclusive to ASF.
Must be used between calls to **AddObjective** and **CloseObjective**.
Compatible with `insidetrigger` and `outsidetrigger` objective types.
Requires that the player be within/outside of the trigger(s) for *Time* (a fill meter is shown on the HUD) to complete the stage/objective.
~~ADDYNOKNOW~~ Negative values?

### SetObjSound
```
SetObjSound(str:SoundResource, str:Event, float:Gap, float:Delay);
SetObjSound("uhoh");
SetObjSound("shine", "inside_trigger", 1, 0.5);
```
Used in mission initialisation scripts. Repeatable.
Exclusive to ASF.
Compatible with `hitpeds`, `insidetrigger`, and `outsidetrigger` objective types.
Must be used between calls to **AddObjective** and **CloseObjective**.
Makes a sound (*SoundResource*) play on a given event, with some parameters.
See also "Specific notes" -> "Referencing sound resources in scripts".
*Event*, if not in  `hitpeds` objective, can be:
- `enter_trigger` to play the sound on trigger entry;
- `exit_trigger` to play the sound on trigger exit;
- `inside_trigger` to play the sound whilst inside the trigger in an `insidetrigger` objective;
- `outside_trigger` to play the sound whilst outside the trigger in an `outsidetrigger` objective;

*Gap* sets the number of seconds between sound plays if *Event* is set to `inside_trigger` or `outside_trigger`. Disused in `hitpeds` objectives.
*Delay* sets the delay time before the sound begins playing. Disused in `hitpeds` objectives.

### SetObjTrigger
```
SetObjTrigger(str:Locator);
SetObjTrigger("badplace7");
```
Used in mission initialisation scripts.
Exclusive to ASF.
Must be used between calls to **AddObjective** and **CloseObjective**.
Compatible with `insidetrigger` and `outsidetrigger` objective types.
Sets the name of a Locator Type 0 (*Locator*, loaded) that the player must be within or external to in order to complete the stage/objective.

### SetObjSpeedKMH
```
SetObjSpeedKMH(float:Speed);
SetObjSpeedKMH(40);
```
Used in mission initialisation scripts.
Exclusive to ASF.
Must be used between calls to **AddObjective** and **CloseObjective**.
Compatible with `reachspeed` objective type.
Sets the required speed in KM/H as *Speed*.

### SetObjTotal
```
SetObjTotal(int:Num);
SetObjTotal(10);
```
Used in mission initialisation scripts.
Exclusive to ASF.
Must be used between calls to **AddObjective** and **CloseObjective**.
Compatible with `collectcoins`, `collectwrench`, `completedwasps`, `destroycars`, `hitpeds`, `jump`, and `spring` objective types.
Sets how many of whatever action are required as *Num*.

### AddCondTargetModel
```
AddCondTargetModel(str:InternalName);
AddCondTargetModel("krust_v");
```
Used in mission initialisation scripts. Repeatable.
Exclusive to ASF.
Compatible with `hitpeds` and `destroycars` condition types.
Must be used between calls to **AddCondition** and **CloseCondition**.
Works in the same way as **AddObjTargetModel**, but relevant to *failing* the condition.

### SetCondDecay
```
SetCondDecay(float:Decay, float:Delay);
SetCondDecay(1, 1);
```
Used in mission initialisation scripts.
Exclusive to ASF.
Compatible with `insidetrigger` and `outsidetrigger` condition types.
Must be used between calls to **AddCondition** and **CloseCondition**.
Works in the same way as **SetObjDecay**, but relevant to *failing* the condition.

### SetCondDelay
```
SetCondDelay(float:Seconds);
SetCondDelay(1.0);
```
Used in mission initialisation scripts.
Exclusive to ASF.
Must be used between calls to **AddCondition** and **CloseCondition**.
Compatible with `collectcoins`, `collectwrench`, `destroycars`, `hitandrun`, `hitandruncaught`, `hitandrunrage`, `hitpeds`, `jump`, and `spring` condition types.
Sets the delay (as *Seconds*) between failing the condition and showing the fail screen.
Defaults vary:
- 1 second for `collectcoins`, `collectwrench`, `destroycars`, `hitandrunrage`, `hitpeds`, `jump`, and `spring` conditions;
- 2 seconds for `hitandrun` and `hitandruncaught` conditions;

### SetCondDisplay
```
SetCondDisplay(str:Display);
SetCondDisplay("none");
```
Used in mission initialisation scripts.
Exclusive to ASF.
Must be used between calls to **AddCondition** and **CloseCondition**.
Compatible with any ASF-exclusive condition that changes the HUD.
Sets ASF-exclusive condition HUD element mode to *Display:
- `none` is usable in all supported conditions and disables the unique HUD elements;
- `fill` is usable only in `maintainspeed` conditions and fills the meter more, even if the player is only going at around the median required speed;
- `midpoint` is usable only in `maintainspeed` conditions and is the default, filling the meter in a way that more accurately represents the difference between minimum and maximum required speeds;

~~ADDYNOKNOW~~ List of supported conditions... ?

### SetCondMessageIndex
```
SetCondMessageIndex(int:StageMessageIndex);
SetCondMessageIndex(5);
```
Used in mission initialisation scripts.
Exclusive to ASF.
Compatible with `insidetrigger` and `outsidetrigger` condition types.
Must be used between calls to **AddCondition** and **CloseCondition**.
Works in the same way as **SetObjMessageIndex**, but relevant to *failing* the condition.

### SetCondSound
```
SetCondSound(str:SoundResource, str:Event, float:Gap, float:Delay);
SetCondSound("ohuh");
SetCondSound("ohuh2", "enter_trigger");
```
Used in mission initialisation scripts.
Exclusive to ASF.
Compatible with `insidetrigger` and `outsidetrigger` condition types.
Must be used between calls to **AddCondition** and **CloseCondition**.
Works in the same way as **SetObjSound**, but relevant to *failing* the condition.

### SetCondSpeedRangeKMH
```
SetCondSpeedRangeKMH(float:Min, float:Max);
SetCondSpeedRangeKMH(0, 80);
```
Used in mission initialisation scripts.
Exclusive to ASF.
Must be used between calls to **AddCondition** and **CloseCondition**.
Compatible with `maintainspeed` condition type.
Fails the player if their speed goes below *Min* or above *Max*.

### SetCondThreshold
```
SetCondThreshold(float:Time);
SetCondThreshold(10.0);
```
Used in mission initialisation scripts.
Exclusive to ASF.
Compatible with `insidetrigger` and `outsidetrigger` condition types.
Must be used between calls to **AddCondition** and **CloseCondition**.
Works in the same way as **SetObjThreshold**, but relevant to *failing* the condition.

### SetCondTotal
```
SetCondTotal(int:Num);
SetCondTotal(5);
```
Used in mission initialisation scripts.
Exclusive to ASF.
Compatible with `collectcoins`, `collectwrench`, `destroycars`, `jump`, and `spring` condition types.
Must be used between calls to **AddCondition** and **CloseCondition**.
Works in the same way as **SetObjTotal**, but relevant to *failing* the condition.

### SetCondTrigger
```
SetCondTrigger(str:Locator);
SetCondTrigger("loc02");
```
Used in mission initialisation scripts.
Exclusive to ASF.
Compatible with `insidetrigger` nd `outsidetrigger` condition types.
Must be used between calls to **AddCondition** and **CloseCondition**.
Works in the same way as **SetObjTrigger**, but relevant to *failing* the condition.

### CHECKPOINT_HERE
```
CHECKPOINT_HERE();
CHECKPOINT_HERE();
```
Used in mission initialisation scripts.
Exclusive to ASF.
Must be used between calls to **AddStage** and **CloseStage**.
Adds a checkpoint/restart point to the stage/objective.

### IfCurrentCheckpoint
```
IfCurrentCheckpoint()
        {
            AddStageVehicle("dune_v", "dunev2", "target", "dunevM.con", "");
        }
!IfCurrentCheckpoint()
        {
            ActivateVehicle("dune_v", "", "target", "");
        }
```
Used in mission initialisation scripts.
Exclusive to ASF.
Must be used between calls to **AddStage** and **CloseStage**.
Can be used as either **IfCurrentCheckpoint**/**!IfCurrentCheckpoint** solely, or both at once.
Functions nested by **IfCurrentCheckpoint** only execute if the player is resuming at that stage/objective via a checkpoint.
Functions nested by **!IfCurrentCheckpoint** only execute if the player reaches the stage/objective as part of typical progression.

### SetCheckpointDynaLoadData
```
SetCheckpointDynaLoadData(str:DynaLoadDataString);
SetCheckpointDynaLoadData("l1z1.p3d;");
```
Used in mission initialisation scripts.
Exclusive to ASF.
Must be used between calls to **AddStage** and **CloseStage**.
Sets a *DynaLoadDataString* to execute on restarting at that stage/objective via checkpoint.
See also "Specific notes" -> "Dyna Load Data String format".

~~ADDYNOKNOW~~ 2nd argument interior like usual?

### SetCheckpointPedGroup
```
SetCheckpointPedGroup(int:GroupID);
SetCheckpointPedGroup(1);
```
Used in mission initialisation scripts.
Exclusive to ASF.
Must be used between calls to **AddStage** and **CloseStage**.
Sets the pedestrian group (*GroupID*) to force as active on restarting at that stage/objective via checkpoint.

### SetCheckpointResetPlayerInCar
```
SetCheckpointResetPlayerInCar(str:Vehicle);
SetCheckpointResetPlayerInCar("level4_carstart");
```
Used in mission initialisation scripts.
Exclusive to ASF.
Must be used between calls to **AddStage** and **CloseStage**.
Places the player in their vehicle and their vehicle at position *Vehicle* (loaded Locator Type 3) on restarting at that stage/objective via checkpoint.

### SetCheckpointResetPlayerOutCar
```
SetCheckpointResetPlayerOutCar(str:Player, str:Vehicle);
SetCheckpointResetPlayerOutCar("marge_loc", "level4_carstart");
```
Used in mission initialisation scripts.
Exclusive to ASF.
Must be used between calls to **AddStage** and **CloseStage**.
Places the player out of their vehicle at position *Player* and their vehicle at position *Vehicle* (both loaded Locator Type 3s) on restarting at that stage/objective via checkpoint.

### SetCheckpointTrafficGroup
```
SetCheckpointTrafficGroup(int:GroupID);
SetCheckpointTrafficGroup(1);
```
Used in mission initialisation scripts.
Exclusive to ASF.
Must be used between calls to **AddStage** and **CloseStage**.
Sets the traffic group (*GroupID*) to force as active on restarting at that stage/objective via checkpoint.
Best used with the Custom Traffic Support hack/multiple potential traffic groups.

## Specific notes
Information relevant to many functions is placed here to avoid a lot of redundancy.

### Dyna Load Data String format
Dyna Load Data Strings are text strings (executed by functions, in many cases) that tell the game to do certain things to the game world:
A single string takes the format of `<File><Action>` (either once or repeatedly for different files), where both are strings, `File` is always rooted in "/art/", and `Action` is an ASCII symbol character.
Possible actions include:
- `;` loads an exterior world region chunk - an area of map;
- `:` unloads an exterior world region chunk;
- `@` loads an interior world region chunk - an interior space;
- `$` unloads an interior world region chunk;
- `*` activates a World Sphere - a skybox (should be loaded);
- `&` deactivates a World Sphere;

As an example, `l1z1.p3d;l1r1.p3d:skybxA*` loads the `l1z1` region, unloads the `l1r1` region, and activates the loaded `skybxA` World Sphere.
Incorrect formatting is ignored.
Redundant actions (for example, to load an already loaded area) are ignored.
~~ADDYNOKNOW~~ Load/unload TERRA, needs art/*?

### Referencing sound resources in scripts
Some things to take note of:
- Functions that want to work with a Convinit/Noboxconv *will not work with anything else*, only a correctly defined dialogue line or line sequence.
- Sound resource/Convinit/Noboxconv names are **case-sensitive**, relative to the SPT. If in the SPT your conversation is named `c_Churn`, calls in functions should reflect that as `churn`. Every line should follow the same naming style, if there are multiple.
- When referencing a general purpose sound resource and not dialogue, it seems anything goes. The game dumps every SPT sound resource from a list of hardcoded files at startup, and from then on all of them are referable.

### AI vehicle behaviours
When using functions to work with AI vehicles, they can be assigned behaviours.
- The `NULL`/default AI does nothing but sit still. No driving, waypoints, targetting, or parameters. Setting a vehicle's behaviour to `NULL` in a `race` stage/objective crashes the game.
- The `chase` AI targets the player character/vehicle, depending on which is in use. No waypoints or parameters.
- The `race` AI targets waypoints in the order set by the stage waypoint list (calls to **AddStageWaypoint**). Use of non-waypoint-routed shortcuts can be controlled via **SetVehicleAIParams**, and speed control relative to the player's state can be controlled via **SetStageAIRaceCatchupParams**.
- The `waypoint` AI seems to be an alias for the `race` AI.
- The `evade` AI targets waypoints in the order set by the stage waypoint list (calls to **AddStageWaypoint**). Use of non-waypoint-routed shortcuts can be controlled via **SetVehicleAIParams**, and speed control relative to the player's state can be controlled via **SetStageAIEvadeCatchupParams**.
- The `target` AI targets waypoints in the order set by the stage waypoint list (calls to **AddStageWaypoint**). Use of non-waypoint-routed shortcuts can be controlled via **SetVehicleAIParams**, and speed control relative to the player's state can be controlled via **SetStageAITargetCatchupParams**.

### CustomFiles hack/game.lua
The Custom Files/CustomFiles hack allows missions to be crafted in the lua programming language and possibly altered before handing to the game for reading, giving greater freedom and customisability.

Outside of handing scripts to the game as strings, there is also Donut Team's `game.lua` script (formerly `mfk.lua`), which provides functionality to store a script as lua and simply redirect to that. Quirks/changes relevant to this method include:
- Function calls must be preceeded with `Game.` (this can be changed by editing `game.lua`, though);
- Comments must be lua-style (`-- comment` / `--[[ comment ]]--`);
- Function calls no longer need to end with a semi-colon (`;`);
- Instances of `\` for filepaths need to be escaped/set to `\\`;
- Any calls to function with `str`-type arguments now need quotations surrounding those arguments;

~~ADDYNOKNOW~~ IfCurrentCheckpoint rubbish.

---
