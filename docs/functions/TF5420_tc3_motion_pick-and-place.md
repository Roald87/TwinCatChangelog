# TF5420 | TwinCAT 3 motion pick-and-place

[Source](https://infosys.beckhoff.com/content/1033/tf5420_tc3_advanced_pick_and_place/8891897355.html?id=6886016567551031097)

## Version 3.1.10.64

_Requires TwinCAT V3.1.4024.24 or higher_

-   New: In a CM group with Geo Blending, a blocker, that is triggered early enough before it becomes active, blends over and passed on without interruption.

## Version 3.1.10.14

-   New MC Group for Coordinated Motion
-   Consistent further development of PnP Group and for compatibility reasons launched in a new MC Group
-   Choice between Geo Blending and Super Positioning Blending within the new Coordinated Motion Group
-   Uses same PLC library (`Tc3_McCoordinatedMotion`)

## Version 3.1.10.1

_Requires TwinCAT V3.1.4024.7 or higher_

-   New group type MC Group Coordinated Motion is available.
-   Cyclic interface is extended for MC Group Coordinated Motion.
-   New function blocks for MC Group Coordinated Motion:
    -   `MC_BlockerPreparation`
    -   `MC_ReleaseBlocker`
    -   `MC_GroupReadBlockerStatus`
    -   `MC_DwellTimePreparation`
-   `MC_GroupHalt` is implemented for MC Group Coordinated Motion.
-   `mcTransModeCornerDistance`, `mcCircPathchoiceShortSegment` and `mcCircPathchoiceLongSegment` are implemented for MC Group Coordinated Motion.

## Version 3.1.6.27

_Requires TwinCAT V3.1.4022.0 or higher_

-   The remaining time and distance of the current segment can be read via ADSREAD.

## Version 3.1.6.3

-   New function blocks for spatial transformations, that is for changing the reference system (`MC_SetCoordinateTransform`) and for conveyor tracking (`MC_TrackConveyorBelt`).
-

## Version 3.1.4.4

-   New: `MC_MAXIMUM` is supported as input value from software version 3.1.4.4. For more detailed information please refer to the documentation for the respective function block.
-

## Version 3.1.2.47

-   New function block `MC_MoveCircularAbsolutePreparation`.
