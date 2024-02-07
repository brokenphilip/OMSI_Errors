# OMSI Errors
This repository ~~contains~~ aims to contain information for end-users and developers about various errors which may occur in OMSI 2 Bus Simulator.

Currently a **very** early work-in-progress - information is mostly missing, mainly of technical nature, and could be incorrect or misleading.

## Address `00000000` and `00000000`
This error is incredibly vague and can be caused in numerous ways.

When a plugin fails to load ("LoadLibrary failed!" in the log file), this error appears when trying to close the game. You must close it irregularly (eg. Task Manager).

## Address `00624BAC` (...)
Indicates an issue with the `humans.txt` file of a map, likely incorrectly formatted or contains humans that don't exist (which are also written in the logfile).

## AMUAV.CNAVO.MV.[A-U] (...)
Function: `TProgMan.MakeVehicle`

**AMUAV.CNAVO.MV.C** (and potentially others) occurs when the game tries to spawn a bus with no name, which could be a sign of (but not necessarily) a poorly formatted `ailists.cfg`. Needs more research.

## CHAD - [Humans, Drivers] (...)
Function: `TProgMan.CalcMovingObjects` (`CalcHumansAndDrivers`)

## CKS.[x]
Function: `TProgMan.CheckKachelSprung` (`CheckTileJump`?)

## CMO_[x], CMO.[x]
Function: `TProgMan.CalcMovingObjects`

## CV.Calculate - [A-Y]
Function: `TRoadVehicleInst.Calculate`

**CV.Calculate - J[1-3]** appear to indicate vehicle script errors. Needs more research.

## MM.LM.[x].[x]
Function: `TMaterialMan.LoadMaterial`

Seems to happen when using "Limit all textures (apart from own bus) to 256x256" under the Advanced Graphics options. Needs more research.

## POI.GHAA - [A-D]
Function: `TPhysObjInstance.GetHeightAboveAll`

Sometimes, when OMSI hangs (during graphics loading?), using a debugger will cause **POI.GHAA - C** on your currently driven bus. Needs more research.

## P.Render
Function: `TProgMan.Render`

## P.TL - [1-14]
Function: `TProgMan.Translate`

## "Reduced multithreading"
This error appears when the game starts after a crash. You can find more information about this error, as well as how to silence it, in [this Steam Guide](https://steamcommunity.com/sharedfiles/filedetails/?id=3061921380).

## RS.[x]
Errors related to the shader?

## SPS.[1-5]
Function: (`TSoundPack`?) `SoundPackSort`

## T.PlugInRefrVars
An error within the `Access[x]Variable` function of a plugin. Find the plugin causing the issue (eg. binary search - disable half of your plugins recursively) and contact their developers.

## TPM.CABAD.[x]
Function: `TTrafficPathManager.ClearAllBelegungenAndDens` (Belegungen = Occupancies?)

## TPM.GSC.[A-Z, AA, AB]
Function: `TTrafficPathManager.GetStreetConditions`

## TUV [x]
