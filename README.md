# OMSI Errors
This repository ~~contains~~ aims to contain information for end-users and developers about various errors which may occur in OMSI 2 Bus Simulator.

Currently a **very** early work-in-progress - information is mostly missing, mainly of technical nature, and could be incorrect or misleading.

Feel free to contribute by creating your own (or replying to an existing) [issue](https://github.com/brokenphilip/OMSI_Errors/issues?q=is%3Aissue). The title should ideally be the error itself, and the description should contain any known information about said error - when/how/why it happens and similar. Bonus points if the error is reproducible!
###### SELF-TODO: should I use discussions instead of issues for this?

## Address `00000000` reading/writing `00000000`
This error is incredibly vague, applies to all versions of OMSI 2 and can be caused in numerous ways.

When a plugin fails to load ("LoadLibrary failed!" in the log file), this error appears when trying to close the game. You must close it irregularly (eg. Task Manager).

## Address `00624BAC` writing `00000004`
On the latest `2.3.004` OMSI 2 version, in `THumanBeing.LoadFromFile`, a human being's complex object pointer (`THumanBeing.ComplObj:TComplObj`) was null.

Indicates an issue with the `humans.txt` file of a map, likely incorrectly formatted or contains humans that don't exist (which are also written in the logfile).

## Address `007C5CC6` reading `00000000`
On the latest `2.3.004` OMSI 2 version, in `TD3DMeshFileObject.LoadMeshFromPreMesh`, a mesh object was invalid (`TD3DMeshFileObject.mesh:ID3DXMesh` was null).

Seems to occur upon map load when opening the main menu after a failed Direct3D device reset, which is a fatal error, at the end of gameplay, accompanied by a bunch of `Direct9 Error: D3DERR_INVALIDCALL` in the logfile. Most dialogs will fail to open or otherwise be unresponsive. The game must be closed irregularly (eg. Task Manager).

## AMSAV.LI.R [^amsav]
Function: `TLoadingInfo.Refresh`

## AMSAV.SV.CTLIML and AMUAV.CNAVO.CTLIML [^amsav][^amuav]
Function: `TRVList.CopyTempListIntoMainList`

## AMSAV.TTM.RATE [^amsav]
Function: `TTimeTableMan.RefreshAllTagErledigt` (Erledigt = Completed)

## AMSAV.TTM.RAVI [^amsav]
Function: `TTimeTableMan.RefreshAllVehicleIndizes` (Indices)

## AMUAV.CNAVO.GGP [^amuav]
Function: `TTrafficPathManager.GetGlobalPosition`

## AMUAV.CNAVO.MV.[A-U] (...) [^amuav]
Function: `TProgMan.MakeVehicle`

**AMUAV.CNAVO.MV.C** (and potentially others) occurs when the game tries to spawn a bus with no name, which could be a sign of (but not necessarily) a poorly formatted `ailists.cfg`. Needs more research.

## AMUAV.RSAS [^amuav]
Function: `TProgMan.RefreshSoundpacksAISwitch`

## "Black Bus" / "Black Textures"
See [this Twitter/X thread](https://twitter.com/brokenphilip/status/1766429278487343264) for more insight.

However, it is also possible for .dds textures to have the wrong alpha format, as explained by [Anonim17PL](https://github.com/Anonim17PL) a while back in [this video](https://www.youtube.com/watch?v=h8PMKOXWOFw).[^2] They should have a separate alpha channel & should be in texconv's "dx9" format. The wrongly formatted textures show up as black as OMSI mis-interprets the non-existent alpha channel as a mipmap channel. Additionally, some users had luck by ticking (or unticking?) the "Generate Mip Maps" in Paint.NET, but this is likely a worse solution as it removes mipmaps entirely from textures, rather than formatting them correctly. After export from editing softare, they can be converted as follows:

`texconv *.dds -alpha -sepalpha -dx9 -y -ft dds`

## CHAD - [Humans, Drivers] (...)
Function: `TProgMan.CalcMovingObjects` (`CalcHumansAndDrivers`)

## CKS.[x]
Function: `TProgMan.CheckKachelSprung` (`CheckTileJump`?)

## CMO_[x], CMO.[x]
Function: `TProgMan.CalcMovingObjects`

## CMOI.R.[x]
Function: `TComplMapObjInst.Render`

Sometimes, when OMSI hangs (during graphics loading?), using a debugger will cause **CMOI.R.3** on your currently driven bus. Needs more research.

## CSV.[x]
Function: `RS.CheckSunVisible` (see **RS.[x]**)

## CV.Calculate - [A-Y]
Function: `TRoadVehicleInst.Calculate`

**CV.Calculate - J[1-3]** appear to indicate vehicle script errors. Needs more research.

**CV.Calculate - J2** at addresses `007D97B6` (for 2.3.004) or `007D9546` (for 2.2.032) indicates a null `TPathSegment` (reading from address `00000150`, which is the startOffsetX).

## MM.LM.[x].[x]
Function: `TMaterialMan.LoadMaterial`

Seems to happen when using "Limit all textures (apart from own bus) to 256x256" under the Advanced Graphics options. Needs more research.

Sometimes, when OMSI hangs (during graphics loading?), using a debugger will cause **MM.LM.13**. Needs more research.

## P.KNNC.KM
Function: `TRVList_KillMarked` (from `TProgMan.KillNotNeededCars`)

## P.MCINN.KV
Function: `TProgMan_KillVeh` (from `TProgMan.MarkCarIfNotNeeded`)

## P.Render
Function: `TProgMan.Render`

A loop of this error can occur if a savegame ("situation") with rainy weather is restored, where the street conditions are wet (i.e, reflections visible, WetLane sounds playing) and where there also is a possibility of water sprays being generated by a moving vehicle immediately upon load.[^1]

## P.TL - [1-14]
Function: `TProgMan.Translate`

## POI.GHAA - [A-D]
Function: `TPhysObjInstance.GetHeightAboveAll`

Sometimes, when OMSI hangs (during graphics loading?), using a debugger will cause **POI.GHAA - C** on your currently driven bus. Needs more research.

## "Reduced multithreading"
This error appears when the game starts after a crash. You can find more information about this error, as well as how to silence it, in [this Steam Guide](https://steamcommunity.com/sharedfiles/filedetails/?id=3061921380).

## RHIMB
Function: `RS.HumansInMyBus` (see **RS.[x]**)

## RHO.[1-5]
Function: `RS.HumansOutside` (see **RS.[x]**)

## RMUV.[1-3]
Function: `RS.RenderMyUserVehs` (see **RS.[x]**)

## RS.[x]
Various rendering functions - needs more research (what is RS?).

## RV.[1-4]
Function used by `RS.RenderAIVeh` and `RS.RenderOtherUserVeh` (see **RS.[x]**)

## SPS.[1-5]
Function: (`TSoundPack`?) `SoundPackSort`

## T.PlugInRefrVars
An error within the `Access[x]Variable` function of a plugin. Find the plugin causing the issue (eg. binary search - disable half of your plugins recursively) and contact their developers.

## TPM.CABAD.[x]
Function: `TTrafficPathManager.ClearAllBelegungenAndDens` (Belegungen = Occupancies?)

## TPM.GSC.[A-Z, AA, AB]
Function: `TTrafficPathManager.GetStreetConditions`

## TUV [x]
*todo*

[^1]: See [issue #1](https://github.com/brokenphilip/OMSI_Errors/issues/1)
[^2]: See [issue #2](https://github.com/brokenphilip/OMSI_Errors/issues/2)
[^amsav]: **AMSAV:** `TProgMan.AddMissingScheduledAIVehicles`
[^amuav]: **AMUAV:** `TProgMan.AddMissingUnscheduledAIVehicles`
