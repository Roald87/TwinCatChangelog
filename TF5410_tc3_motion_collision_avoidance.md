# TF5410 | TwinCAT 3 Motion Collision Avoidance

## Version 3.1.10.1 

### [Notes](https://github.com/Roald87/TwinCatChangelog/issues/5)

The TF5410 version 3.1.10 is not a functional compatible update to version 3.1.6 of the TF5410 Collision Avoidance Software. It is a standalone release.  

Due to continuous development and close integration with other software components, the release version 3.1.10 may result in functional changes in the motion path compared to the operation of version 3.1.6 of the software. 

The TF5410 version 3.1.6 of Collision Avoidance will continue to be maintained as a functional compatible update for further availability. 

Software affected:  Beckhoff TwinCAT 3 TF5410 | TC3 Collision Avoidance version 3.1.10 

Effect in application:  Motion behaviour under TF5410 version 3.1.10 may differ from those under version 3.1.6 of the software. 

Fix, Avoidance: For a functional compatible update, the TF5410 version 3.1.6 branch should still be used, which will continue to be available via support. 

For systems with TF5410 version 3.1.6, an installation of TF5410 version 3.1.10 is possible, but requires a new functional check of the mechanical system during the following startup. 

### [Changes](https://github.com/Roald87/TwinCatChangelog/issues/5)

- Improvements on gap controller when enabling the group, commanding the first movement or changing the gap with queued movers. If any gap is violated, the last mover (n) in the line is driven out first. Only when this mover (n) has reached the target gap, the previous mover (n-1) starts to correct further gap violations. This new behavior prevents too small gaps while driving out and can cause a different timing behavior to the previous version. 
- Improvements on gap controller prevent discontinuities of the velocity profile when the target gap is almost reached. Especially in case of high dynamics this could result in oscillations of velocity or acceleration caused by the gap controller. 
- Improvements on MC_GearInPosCA prevent violations of position and dynamics. If violations are unavoidable, the PLC command may be rejected with an error at the function block. 
- Improvements on MC_GearInPosCA with SyncStrategySlow prevent dynamics 
violation. Changing master dynamics or influence of the gap controller during synchronization phase can lead to a run-time error at the function block.
- Improvements on MC_GroupHalt in combination with active gap control. If MC_GroupHalt is triggered and the target gap is not yet reached, MC_GroupHalt has priority. So with MC_GroupHalt. Done it is possible that the target gap is not yet driven out. 
- New feature: target position monitoring is implemented for collision avoidance. For updated projects this can lead to a different timing behavior in case that target position monitoring was activated.  
- New feature: MC_MoveAbsoluteCA supports modulo movements. For this purpose, a new input of type MC_Direction is introduced. This could cause a compiler error (ambiguous use of name ‘MC_Direction’) in case this type is used with the Tc2_MC2 PLC library. In this case namespaces must be used. 