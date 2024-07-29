# TwinCAT 3

## Known issues

-   Sudden error message "The operation could not be completed. Unspecified error" in a TwinCAT project. Function block files, would have yellow triangle symbols with an exclamation mark next to them. Starting a new project would result in `_3S.CoDeSys.UserManagement.UserAuthentication`. Issue and fix reported [here](https://stackoverflow.com/questions/71649887/twincat-project-build-fails-with-unspecified-error)
-   All versions of TwinCAT 3 have issues rendering dialogs and visual elements that rely on WinForms on high-DPI monitors. A work-around is to turn off DPI awareness for WinForms using the registry, see [here](https://www.mking.net/blog/using-the-winforms-designer-on-high-dpi-systems). Issues related to this:
    -   Some dialogs are not displayed correctly when using a 4K monitor (Add POU, Library Manager, Prepare Value)
    -   HighDpi: Content of WebVisu object is not displayed correctly, when using a display zoom > 100%
    -   UML, HighDpi: Diagrams are not shown properly if display zoom > 100% (improper position relations, transition conditions/relation identifiers overlay other elements)
    -   HighDpi: Elements in toolbox get unclear/cannot be identified if display zoom > 100% (UML SC, UML CD, Visu)
    -   With high dpi the dialog 'Details' of the library manager is not displayed correctly
    -   Many tables in the IDE such as the "Startup parameter list" under I/O devices are collapsed such that not all the content is displayed unless the column is manually resized
-   Keywords such as `bool` inside of `TcLinkTo` attributes are auto-capitalized. Work-around: turn off the "Convert keywords to uppercase automatically" option under `PLC Environment > Smart coding`. This is an issue because TcLinkTo is case-sensitive and some devices use keywords for the channel names, such as `bool` inside of an IO-link input channel.
-   The use of complex data types such as structures is not supported in the RecipeManager. Attempting to use them results in an 'Invalid Type' warning in the Type column and a compile error.
-   Variables inside library function blocks are not subject to the implicit bounds checking provided by the 'CheckBounds' feature. This can result in accessing invalid indices, causing exceptions if bounds are not properly checked. It is also assumed that other implicit checks are not active.
-   TwinCAT's design does not allow paths length greater than 255 characters. It's possible to exceed this limit by renaming root folders, which may result in a compilation error.
-   If a folder is renamed such that a method/FB/program/etc. has a path exceeding 255 characters, TwinCAT usually still compiles. However, clicking on an error message in the error list can cause TwinCAT to crash.
-   TwinCAT allows the installation of a library containing a file with a path exceeding 255 characters without issue. However, attempting to compile this file results in an error message that is essentially useless.
-   Despite using `__ISVALIDREF()` to validate a reference, the static analysis rule SA0145 does not recognize it as valid and continues to give an error.
-   The Static Analysis rule SA0002 generates an empty object warning for an empty object even if it contains a '// Not needed' comment. This rule cannot be used with Function Blocks via methods only.
-   TwinCAT allows setting a stack size that is too large for a controller, which can cause it to crash without any error message or indication.
-   When typing a type from a library in TwinCAT, it tries to insert the library namespace, which is not valid for the library.
-   Events added to an EventClass in the type system must be successfully compiled to be saved. If changes are made and the project is saved without building it, the changes are not saved. Similarly, if there is a compile error, the changes are not saved.

## Version 3.1.4024.56

### Bug fixes

-   TwinCAT automation interfaces: fixes bug when configuring Boot settings, the example in [InfoSys](https://infosys.beckhoff.com/english.php?content=../content/1033/tc3_automationinterface/2489005451.html&id=) can be run now

## Version 3.1.4024.47

### Bug fixes

-   TcXaeShell: Message 'Project has been modified outside the environment' during export of Control plus Studio fixed
-   Support of Visual Studio 2019 improved (Search, Find all References/Cross Reference List)
-   TwinCAT Project Compare: Fixed a crash when comparing a SFC chain
-   'Go to definition [F12]' was sometimes not visible in the context menu of a variable in previous 4024 versions

### Features

-   New tool/User interface for `Emergency Scan`. Located in IO -> EtherCAT master -> Advanced Settings -> Emergency -> Scan. More information in [InfoSys](https://infosys.beckhoff.com/english.php?content=../content/1033/tc3_io_intro/1446585227.html&id=1449419436157771945)

## Version 3.1.4024.40

### Features

-   `MC_Halt`/`MC_Stop` switches automatically to cyclic synchronous velocity (velocity control) (CSV) cyclic synchronous position (position control) (CSP) after recovering from and error where the previous state was Cyclic Synchronous Torque Mode (CST). [InfoSys](https://infosys.beckhoff.com/content/1033/tcplclib_tc2_mc2/7617393803.html?id=6677792901421113137).

## Version 3.1.4024.35

### Bug fixes

-   `FB_Exit` is called again when `PLC_Reset` is used.
-   "Find all references" and "Go to definition" menu was sometimes missing.
-   TwinCAT no longer crashes when a cold reset is done via a Visual Basic script and a `Tc3_EventLogger.FB_TcMessage` is used.

### Features

-   `MC_GearInVelo` now supports `SyncMode := TIMEBASE` with negative gains.
-   `MC_MoveVelocity`, `MC_MoveAbsolute` and `MC_Halt` ran into error when frequently called with changing dynamics and `BufferMode := MC_Aborting`.
-   The user interface for task sorting is updated.
-   The `ContinuousUpdate` input of [`MC_TorqueControl`](https://infosys.beckhoff.com/content/1033/tcplclib_tc2_mc2/7617393803.html?id=6677792901421113137) works. Note: you need to update your run time to version 3.1.4024.35 for it to work.
-   [`MC_TorqueControl`](https://infosys.beckhoff.com/content/1033/tcplclib_tc2_mc2/7617393803.html?id=6677792901421113137) works in [simulation mode](https://infosys.beckhoff.com/content/1033/tf50x0_tc3_nc_ptp/2834717323.html?id=8250271195349757571). Note: you need to update your run time to version 3.1.4024.35 for it to work.

## Version 3.1.4024.32

### [Bug fixes](https://github.com/Roald87/TwinCatChangelog/files/9169772/Changelist_4024.29_to_4024.32_1.pdf)

#### XAE

-   Link between two TcCom objects created invalid mapping object.
-   TMC Editor: DoubleQuotes were doubled while re-import translations for events.
-   Status of the option "Swap LOBYTE and HIBYTE" were not stored.
-   Converter: If the PLC project could not be build, the change of the GVL variable links was not executed.
-   Wrong IEC code for ‘qualified only’ `ENUM` type used in struct with default value.
-   XAE had problems after reloading TMC on an object.
-   If there was an old TMC file after updating the local copy of a specific project via Git, an unrestored link was not restored after compiling this project.
-   `__FileName__` was not set to (error) message if the "source" was saved as an independent project file.
-   Renaming the PLC project leads to names of all its instances were changed except of first default one.
-   When using the Automation Interface to add variant specific setting and then add a new variant config, the variant specific settings were lost.
-   An error in serializing RPC method calls is fixed.
-   Automation Interface: TwinCAT XAE problems when specifying ImplementationCode in `ITcSmTreeItem::CreateChild` `TreeItemType.PlcPropertySet` or `TreeItemType.PlcPropertyGet`.

#### IO

-   Adapter IP incompatible warning staid and causes problems.
-   An AMP8000 EtherCAT device could be erroneously inserted.
-   IoT Driver: problems with tlsv1.3 version.
-   EtherCAT: When inserting a device before a device with connector, the connector was not checked.
-   A device which only has an A-Port cannot be inserted multiple times.
-   It is now possible to add an AMP8000 to a port if there is a disabled AMP8000 connected.
-   BACnet Rev14: ReadProperty was not working with ArrayIndex, also not working with RPM.
-   BACnet Extension: Adjusted structured view creation to use setting in BACnet_Param.eView_SubordinateAnnotationMode to generate structure.
-   Profinet Controller: wrong record alignment during fragmentation.
-   EtherNet/IP: Communication Interruption on Explicit Messaging once every 24—48 hours.
-   In a specific third party drive it was not possible to change specific PDO settings.
-   TwinCAT XAE had problems after rescanning a BK9100.
-   Dynamic PLC Objects can now not deleted from BACnet.
-   EtherCAT: a problem occurred when an emergency was sent by the EPP3632-0001.
-   BACnet Rev14 : COV-U was not working correctly if client/object is configured statically.
-   Sometimes a problem occurred when one restarts TwinCAT and the HMI EtherCAT Topology Control is active.
-   EthernetIP: Master might use invalid Destination IP for Output UDP-IO Frames depending on FwdOpen reply of remote node.
-   Warning about EtherCAT address appeared for disabled terminals although it is not possible to change the address.
-   In the memory view of an EtherCAT slave PHY MIO Address was not displayed correctly.
-   Different values in startup with and without ESI.

#### PLC

-   Breakpoint handling: second PLC did not start anymore if a breakpoint was set in first PLC and the code of the first PLC was changed via online change.
-   Busy Hangup during Build of special TwinCAT Project with PLC.
-   After update from one version to the next one a problem appeared after a TwinCAT restart.
-   ‘Find All’ in Visual Studio 2019 jumps now to correct line in PLC.
-   Automation Interface: Export/ProduceXml was not possible for PLC functions without return type (void).
-   TcDocGen: internal variables now also rendered in documentation.
-   Standalone PLC: Parameter (0x08500005) mismatch error appeared while online change in a specific project
-   Project Compare problem occurred while comparing two SFC POUs.

#### NC

-   'ContinuousUpdate' feature added to `MC_TorqueControl` for fast communication to change the commanded target torque value (like a cyclic controller app).
-   New NC simulation mode for `MC_TorqueControl` (equal to the existing NC simulation axis with simulation encoder).
-   Automation Interface: Include axis links in encoder device XML.
-   `MC_MoveModulo` improved to prevent seldom run-time error when new modulo command is requested during active movement.
-   Improvement switching drive operation mode from TorqueCtrl into Pos/Velo-Ctrl.
-   If TcNcAxis attribute in PLC could not be resolved an error message appears.
-   Jerk adjustment in a special situation during the decoupling phase of an accelerating slave axis with a new motion command to minimize unexpected overshoot.
-   Encoder Sub Mask with value 0xFFFFFFFF is now leading to correct velocity scaling for example Bode plot.
-   XFC time cam shorter than cycle time is supported.
-   `Tc2_MC2_XFC digital` cam is considering direction parameter when turning on (`MC_DigitalCamSwitch`).

#### System

-   Changed ‘hint’ to ‘error’ dialog when a task dump is (or might be) written.
-   Problems when accessing last byte of an array of `BITARR4` with an uneven number of elements.
-   EventLogger lead to problems on CX8200.
-   TwinCAT/BSD: Evaluates now UserPath from TcRegistry.xml in SystemService.
-   TwinCAT/RTOS: MQTT receive error in combination with CX7000 fixed.
-   Expanded exception window text with the last four version numbers. For example 3.1.4548.6.
-   TcEventLogger: Required LoggedEvents.db to be closed in CONFIG Mode.
-   TwinCAT/BSD: EventLogger problems on C6017/CX5120 fixed.
-   TcEventLoggerAdsProxy: Alignment error in GetSourceGuid fixed.
-   TcEventLogger: AdsLogMessages might be malformed.
-   `Tc3_JsonXml`: `FB_JsonSaxPrettyWriter` EXTENDS `FB_JsonSaxWriter` again so function blocks are interchangeable again for things dependent on the interface like `FB_JsonReadWriteDatatype`. This broke between 4024.15-29.

### Features

#### IO

-   Added ADS service to the EtherCAT master to write data to the EEprom of an EtherCAT slave.
-   Added support of Intel I225 network adapter on Windows CE.

#### NC

-   Added write access via PID for synchronous torque pre-control (additive torque offset for drive nOutData3).

## Version 3.1.4024.29

### Features

-   Added: [`Tc2_Utilities.E_HashMode`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/12674322571.html?id=1394075611762795497)
-   Added: [`Tc2_Utilities.F_GetClassIdVersioned`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/12674393611.html?id=2848447897774806889)
-   Added: [`Tc2_Utilities.F_GenerateHashValue`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/12674358283.html?id=4370544162846202285)
-   Added: [`Tc2_Utilities.FB_CalcHashValue`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/12674253067.html?id=2119009142677043780)

### [Bug fixes](https://github.com/Roald87/TwinCatChangelog/files/9206317/Changelist_4024.25_to_4024.29.pdf)

#### XAE

-   Import `.tnzip` files lead to incorrect paths
-   XAE had problems after working with a specific project for some time.
-   Auto generated type could be changed in editor.
-   VariantManagement: Network adapter was not saved correctly variant specifically, if 'Virtual Device Names' was activated.
-   XAE had problems if a percent sign (%) was used with attribute `'TcLinkTo'`.
-   Automation Interface: Change of encrypt file did not change the encryption of the file.
-   Automation Interface: ConsumeXml changes were overridden by closing tab dialog.
-   Converting of TwinCAT 2 `.tsm` did not work properly, reference was not set to an instance of an object if adding task reference to PLC.
-   Task got allocated port number.

#### IO

-   TC/BSD: USB dongle occasionally caused "Send Mbx Communication Warning" error.
-   MQTT retain flag for ‘last will’ was not set correctly when the MQTT client sends the ‘last will’ when the socket is closed.
-   Profibus: Some modules with `' ('` in name, were not accessible.
-   EthernetIP: Timeout multiplier combo-box was not working correct.
-   EthernetIP: Sending of UDP IO frames was disturbed.

#### PLC

-   Variables of structure `ST_LibVersion` were missing in automatically generated
    function `F_GetVersion`.
-   UML SC library 4.2.2.0 was not properly installed, although it was part of the "ManagedLibraries" folder.
-   Online change after a change of the mapping lead to problems.
-   `FB_Reinit` of sub-instance was not called during Online Change.

#### NC

-   NC configuration decimal values missing / change in decimal symbol.
-   Small modifications on NC SAF and SVB task interrupt handling to prevent race
    conditions.

#### System

-   TC/BSD: OS Version in "Add Route Dialog" shows now correct TwinCAT/BSD.
-   Secure ADS: Host name was limited to 32 bytes, longer FQDN could not connect

### [Features](https://github.com/Roald87/TwinCatChangelog/files/9206317/Changelist_4024.25_to_4024.29.pdf)

#### IO

-   EtherCAT Slave: `m_guidTComEvent` readable via ADS.
-   Object name is used for EtherCAT emergency messages.
-   System Manager checks now if the same NIC is used for standard EtherCAT and for Redundancy.
-   Support implemented for disabling sending of cyclic EtherCAT frames, that only have commands directed to disabled slaves.

#### NC

-   "add to scope" functionality for NC axis.

## Version 3.1.4024.25

### Features

-   TF6281 Ethernet/IP Scanner - EDS Parser version updated to 1.9 - Overhaul of UI interface and optimization of Config Instance handling
-   Exceptions within `FB_init`, `FB_reinit` & `FB_exit` now result in a core dump [InfoSys](https://infosys.beckhoff.com/english.php?content=../content/1033/tc3_plc_intro/5094414603.html&id=)

## Version 3.1.4024.24

### Features

-   Added: [`Tc2_Utilities.RealIsNaN`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/11506311563.html?id=242917297032427132)
-   Added: [`Tc2_Utilities.RealIsFinite`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/11506278283.html?id=1461230831771457831)

## Version 3.1.4024.23

### Features

-   Limitation of decimal places with `Tc3_IotCommunicator`. [InfoSys](https://infosys.beckhoff.com/../content/1033/tf6730_tc3_iot_communicator/11268269707.html?id=2544377694223424412)

## Version 3.1.4024.22

### Features

-   Maximum router memory increased from 1024 MB to 4095 MB [InfoSys](https://infosys.beckhoff.com/english.php?content=../content/1033/tf7xxx_tc3_vision/18014405306596491.html&id=)
-   Added: [`FB_CoEDriveEnable`](https://infosys.beckhoff.com/content/1033/tcplclib_tc2_drive/10731917067.html?id=7592382315255221170)
-   Added: [`FB_CoEDriveMoveVelocity`](https://infosys.beckhoff.com/content/1033/tcplclib_tc2_drive/10731918987.html?id=2982660607506303008)
-   Function block added: `FB_SoEDriveEnable`
    [InfoSys](https://infosys.beckhoff.com/content/1033/tcplclib_tc2_drive/10731920907.html?id=8376906030662804724)
-   Function block added: `FB_SoEDriveMoveVelocity`
    [InfoSys](https://infosys.beckhoff.com/content/1033/tcplclib_tc2_drive/10731923211.html?id=3237529037083558957)
-   Added: [`Tc2_System.FB_ResetTaskExceedCounter`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/11107119115.html?id=1948900602695240988)
-   Added: [`Tc2_System.FB_ReadTaskExceedCounter`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/11267603979.html?id=6554750661018839478)
-   Added: [`Tc2_SystemCX.FB_CX70xx_RW_EEPROM`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_systemcx/11009227147.html?id=6115162706063450010)
-   Added: [`Tc2_SystemCX.FB_CX7080_LED_WD`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_systemcx/11282066699.html?id=7675427565773653776)
-   Added: [`Tc2_SystemCX.FB_CX7080_LED_ERR`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_systemcx/11106577163.html?id=7926964141089837001)
-   Added: [`Tc2_SystemCX.FB_CX7000_LED_WD`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_systemcx/11106572811.html?id=8700534653695887465)
-   Added: [`Tc2_SystemCX.FB_CX7000_LED_ERR`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_systemcx/11010087691.html?id=3523059685327517438)
-   Added: [`Tc2_SystemCX.FB_CXReadKBusError`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_systemcx/11107098635.html?id=6360225868475216389)
-   Added: [`Tc2_SystemCX.FB_CXReadKBusCycleUpdateTime`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_systemcx/11107094923.html?id=8135264835800328354)

### Fix

-   `Find All References` (Cross Reference List) broken in v4024.20 solved.
-   'Symbolic Mapping' bug fixed. Prior to this release, if Symbolic Mapping was enabled, some mapped links could become non-functional if there was certain ADS communications during an activation or restart.

## Version 3.1.4024.17

### Features

-   In addition to the initial values of the parameters, the contexts can be assigned to tasks for the specific variant on the Context tab [InfoSys](https://infosys.beckhoff.com/content/1033/variant_management/6325850379.html?id=1933378558029834697)
-   The status of the licenses on the Manage Licenses tab, which can be manually changed, is only changed for the active project variant or group [InfoSys](https://infosys.beckhoff.com/content/1033/variant_management/6325850379.html?id=1933378558029834697)
-   The settings for the axis type and unit on the Settings tab are only saved for the active project variant or group. [InfoSys](https://infosys.beckhoff.com/content/1033/variant_management/6325852299.html?id=1663031461212356401)
-   The Modulo scaling of a SERCOS encoders on the Sercos tab is only saved for the selected project variant or group. [InfoSys](https://infosys.beckhoff.com/content/1033/variant_management/6325852299.html?id=1663031461212356401)
-   The axis type set on the Configuration tab is only saved for the active project variant or group. [InfoSys](https://infosys.beckhoff.com/content/1033/variant_management/6325852299.html?id=1663031461212356401)
-   The variant of the stand-alone PLC project selected on the Project tab is only saved for the active project variant or group. [InfoSys](https://infosys.beckhoff.com/content/1033/variant_management/6325854219.html?id=7183010108179338387)
-   The device set on the General NOV-DP-RAM device tab is only set for the active project variant or group. [InfoSys](https://infosys.beckhoff.com/content/1033/variant_management/6325868939.html?id=5362468858073827180)
-   The NOV-DP-RAM device is only inactive for the active project variant or group. [InfoSys](https://infosys.beckhoff.com/content/1033/variant_management/6325868939.html?id=5362468858073827180)
-   Added: [`Tc3_EventLogger.FB_TcEventCsvExportSettings`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc3_eventlogger/9956771211.html?id=8771111572755601179)

## Version 3.1.4024.15

### Bug fix

-   A faulty driver in 4024.10-4024.12 can lead to Visual Studio crashes during a stand-alone project build. Specifically during the "Import symbol information" build step if a .TPR refactor file is present. Should be fixed in > 4024.12 (Source: Beckhoff support CH. See also [StackOverflow](https://stackoverflow.com/a/69926305/6329629).)

### Features

-   Automatic Accurate Stop for NCI GST Interpreter [InfoSys](https://infosys.beckhoff.com/english.php?content=../content/1033/tf5100_tc3_nc_i/10038263179.html&id=270450158997902620)
-   Added: [`Tc2_MC2.MC_TorqueControl`](https://infosys.beckhoff.com/content/1033/tcplclib_tc2_mc2/7617393803.html?id=6677792901421113137). Requires Tc3 3.1.4024.15 on both XAE and XAR. Requires firmware 2.14 or later for AX5000 and firmware 1.03 Build 002 or later for AX8000.

## Version 3.1.4024.12

### Features

-   Change in path dynamics for NCI GST Interpreter [InfoSys](https://infosys.beckhoff.com/english.php?content=../content/1033/tf5100_tc3_nc_i/9237585035.html&id=8344109939385622623)

## Version 3.1.4024.11

<!-- prettier-ignore-start -->
!!! warning 
    Usage of this version is not recommended due to some issues. [Bosch TwinCAT changelog](https://community.developer.bosch.com/t5/Knowledge-base/TwinCAT-XAE-version-overview/ta-p/48982#EN).
<!-- prettier-ignore-end -->

### Features

-   Error analysis with core dump [InfoSys](https://infosys.beckhoff.com/english.php?content=../content/1033/tc3_plc_intro/6884133515.html&id=9193305343691095620)
-   The license dongle is only disabled for the active project variant or group [InfoSys](https://infosys.beckhoff.com/content/1033/variant_management/6325850379.html?id=1933378558029834697)
-   Added: [`Tc2_Utilities.FindAndSplitChar`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/8245507851.html?id=9180678329069202236)
-   Added: [`Tc2_Utilities.FindAndSplit`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/8235976331.html?id=3438267492659948266)
-   Added: [`Tc2_System.ST_CpuCoreInfo`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/8831111051.html?id=1453441570984770172)
-   Added: [`Tc2_System.F_GetTaskTotalTime`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/8830227851.html?id=9031864548778018881)
-   Added: [`Tc2_System.F_GetCpuCoreInfo`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/8824297099.html?id=985625989999487283)
-   Added: [`Tc2_System.F_GetCpuCoreIndex`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/8824208779.html?id=557299053114329889)

## Version 3.1.4024.10

<!-- prettier-ignore-start -->
!!! warning
    Usage of this version is not recommended due to some issues. [Bosch TwinCAT changelog](https://community.developer.bosch.com/t5/Knowledge-base/TwinCAT-XAE-version-overview/ta-p/48982#EN).
<!-- prettier-ignore-end -->

### Features

-   Support of Visual Studio 2019
-   The TcCom object is only disabled for the active project variant or group [InfoSys](https://infosys.beckhoff.com/content/1033/variant_management/6325850379.html?id=1933378558029834697)
-   The initial values of the parameters listed on the Parameter (Init) tab can be enabled for the variant management [InfoSys](https://infosys.beckhoff.com/content/1033/variant_management/6325850379.html?id=1933378558029834697)
-   The C++ project/instance is only disabled for the active project variant or group. [InfoSys](https://infosys.beckhoff.com/content/1033/variant_management/8843640971.html?id=4959120427343912986)
-   C++ instance: The initial values of the parameters listed on the Parameter (Init) tab can be enabled for the variant management. [InfoSys](https://infosys.beckhoff.com/content/1033/variant_management/8843640971.html?id=4959120427343912986)
-   C++ instance: The interface pointers listed on the Interface Pointer tab can be enabled for the variant management. [InfoSys](https://infosys.beckhoff.com/content/1033/variant_management/8843640971.html?id=4959120427343912986)

## Version 3.1.4024.7

### Features

-   The settings for Divider and Modulo on the Settings tab are only saved for the active project variant or group. [InfoSys](https://infosys.beckhoff.com/english.php?content=../content/1033/variant_management/6325876619.html&id=)
-   Added: [`Tc3_IPCDiag.FB_IPCDiag_Register`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc3_ipcdiag/1475282443.html?id=3808476523660178266)
-   Added: [`Tc3_IPCDiag.FB_IPCDiag_WriteParameter`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc3_ipcdiag/1475174283.html?id=8807221228960915222)
-   Added: [`Tc3_IPCDiag.FB_IPCDiag_ReadParameterPeriodic`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc3_ipcdiag/3247738891.html?id=2874010479901942233)
-   Added: [`Tc3_IPCDiag.FB_IPCDiag_ReadParameter`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc3_ipcdiag/1475107083.html?id=6018047503593977550)
-   Added: [`Tc3_IPCDiag.F_IPCDiag_GetMdpIdx`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc3_ipcdiag/3247854219.html?id=1778209108281298078)
-   Added: [`Tc3_IPCDiag.FB_IPCDiag_WriteParameterByMdpIdx`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc3_ipcdiag/3248682891.html?id=4587069311276018651)
-   Added: [`Tc3_IPCDiag.FB_IPCDiag_ReadParameterByMdpIdx`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc3_ipcdiag/3247811979.html?id=8711842893576625995)
-   Added: [`Tc3_DynamicMemory.FB_DynMem_Manager2`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc3_dynamicmemory/8846845195.html?id=7453149925464657306)
-   Added: [`Tc3_DynamicMemory.FB_DynMem_Manager`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc3_dynamicmemory/8846834443.html?id=273899389167963679)
-   Added: [`Tc3_DynamicMemory.FB_DynMem_Buffer`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc3_dynamicmemory/8844514315.html?id=8241497333647833217)
-   Added: [`Tc3_JsonXml.FB_JsonDynDomParser`](https://infosys.beckhoff.com/content/1033/tcplclib_tc3_jsonxml/8101725835.html?id=4882529747495611578)

## Version 3.1.4024.4

### Features

-   Spline interpolation for NCI GST Interpreter [InfoSys](https://infosys.beckhoff.com/english.php?content=../content/1033/tf5100_tc3_nc_i/8250797579.html&id=2443170267198973234)
-   Change in axis dynamics for NCI GST Interpreter [InfoSys](https://infosys.beckhoff.com/english.php?content=../content/1033/tf5100_tc3_nc_i/8405470603.html&id=745347749354607281)
-   The links selected via the Link to I/O button and Link To PLC on the Settings tab are only saved for the active project variant or group. [InfoSys](https://infosys.beckhoff.com/english.php?content=../content/1033/variant_management/6325876619.html&id=)
-   The links to the process data objects (PDOs) of the EtherCAT device are only saved for the active project variant or group. [InfoSys](https://infosys.beckhoff.com/content/1033/variant_management/6325868939.html?id=5362468858073827180)

## Version 3.1.4024.0

### [Features](https://www.beckhoff.com/en-en/products/automation/twincat/twincat-3-build-4024/)

-   Integration of Visual Studio® 2017 Shell (TcXaeShell).
-   New home page, including new RSS feed with TwinCAT information.
-   Variant management. Simple configuration of machine options. Version-specific deactivation/activation of components. Version-specific parameterization. Mapped through ‘conditional compilation’ in the PLC.
-   Multi-user PLC capability. Several programmers can work on the same PLC project simultaneously.
-   Corrected time stamps for data records, for example via NTP protocol.
-   Improved overview in the I/O configuration mapping dialog
-   'Go To Definition' from the PLC process image to the PLC code in the I/O configuration
-   'Secure ADS' Extension (uses TCP port 8016): encrypted ADS communication
-   Detection of failure to free up dynamically allocated memory. See also this [StackOverflow question](https://stackoverflow.com/q/68709572/6329629).
-   SFC steps may have integrated actions (new property Duplicate on copy) that are renamed automatically together with the step (works already with 3.1.4022 but without automatic renaming). This makes the renaming and copy and paste of steps much easier.
-   Added: [`Tc2_Utilities.T_FILETIME64`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/10462547339.html?id=1736794131572696041)
-   Added: [`Tc2_Utilities.ST_AmsRouteEntryEx`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/9682664203.html?id=4450318543653888095)
-   Added: [`Tc2_Utilities.LWORD_TO_BASE36STR`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/10943539851.html?id=7453948431444796808)
-   Added: [`Tc2_Utilities.SYSTEMTIME_TO_ISO8601`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/10686615819.html?id=987846697612946657)
-   Added: [`Tc2_Utilities.SYSTEMTIME_TO_FILETIME64`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/10501106571.html?id=5646165147131094852)
-   Added: [`Tc2_Utilities.FILETIME64_TO_SYSTEMTIME`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/10501062667.html?id=267106869469058574)
-   Added: [`Tc2_Utilities.FILETIME64_TO_ISO8601`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/10686718475.html?id=106005877054630778)
-   Added: [`Tc2_Utilities.FILETIME64_TO_DT`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/10501013003.html?id=2387775026043421082)
-   Added: [`Tc2_Utilities.F_TranslateFileTime64Bias`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/10500926731.html?id=4787993297403188665)
-   Added: [`Tc2_Utilities.DT_TO_FILETIME64`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/10500987275.html?id=2767023879435760174)
-   Added: [`Tc2_Utilities.FB_TzSpecificLocalTimeToFileTime64`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/10500798219.html?id=1031280571104318808)
-   Added: [`Tc2_Utilities.FB_GetAdaptersInfoEx`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/11309317259.html?id=6980676768203801212)
-   Added: [`Tc2_Utilities.FB_FileTime64ToTzSpecificLocalTime`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/10500868619.html?id=2175943120680441081)
-   Added: [`Tc2_Utilities.FB_AddRouteEntryEx`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/9682603019.html?id=518382000701176094)
-   Added: [`Tc2_EtherCAT.FILETIME64_TO_DCTIME64`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/10501953035.html?id=6364488115705130388)
-   Added: [`Tc2_EtherCAT.DCTIME64_TO_FILETIME64`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/10501992459.html?id=5144094238682126626)

#### PLC properties

-   Improvements in the cross-reference list (new filter, performance enhancements).
-   New keyword: ABSTRACT for abstract FB/method/property definition.
-   Improved monitoring of interface variables.
-   Small icons in the solution tree show access modifiers.
-   ENUMs now also available as strings in the PLC.
-   Exception handling via TRY-CATCH for 32-bit systems.
-   Simplified commenting function in the PLC using CTRL + K and then either CTRL + C or CTRL + U to comment or uncomment.
-   'Released' flag is used during library creation.
-   Conditional compilation also available in the declaration section (in addition to implementation part).
-   Multi-line support in pragma declarations.
-   New, optional Base64 memory format for graphical PLC objects.
-   Events stored in a separate .TMC file are formatted with line breaks.
-   New pragma `{attribute 'to_string'}`, which makes the ENUM states available in string format. [InfoSys](https://infosys.beckhoff.com/content/1033/tc3_plc_intro/5725733771.html?id=7792079828149116810)

#### PLC HMI properties

-   Automatic local start of the PLC HMI client at runtime.
-   Dynamic scaling for the operating elements of the measuring equipment category.
-   Offline rotation of elements.
-   Performance improvements during opening of dialogs.
-   Automatic transfer of scaling options of the TargetVisu object to the Tc3PlcHmi.ini file.

#### C++ & MATLAB properties

-   Exchange of TcCOM modules for C++ and MATLAB®/Simulink® while the machine is running.
-   Repository for versioned C++ projects.
-   New way of signing TcCOM modules.

#### AML data exchange

-   Based on the AutomationML format.
-   Bidirectional exchange of I/O topologies with ECAD tools.
-   Incremental import of I/O topologies.
-   Fully integrated in TwinCAT.

#### Safety-related properties

-   User-defined function blocks can be created and instantiated as often as required (including GoToDefinition, Online View, nesting up to 2 levels).
-   Multiple use of variables.
-   Global variables.

#### Scope properties

-   Project wizard facilitates Scope configuration.
-   New single bar and digital charts.
-   Dynamic style for dynamic display switching, depending on variables.
-   Shapes: display of geometric shapes in x/y plots.
-   Vision trigger: inserts images with time stamp into the Scope data stream.
-   Headless mode: allows the view to be disconnected from the server during recording.
-   Marker: with docking function on the x-axis and label feature.
-   Integrated dictionary with physical units.
-   Clear display option for clearing the chart after the display time has elapsed.

## Version 3.1.4022.32

### Features

-   When using Integrated Robotics with Stäubli robots the uniVALplc Client Library is installed correctly with OES and Control plus Studio. This is important in case of a new development/service computer. [Bosch TwinCAT changelog](https://community.developer.bosch.com/t5/Knowledge-base/TwinCAT-XAE-version-overview/ta-p/48982#EN).
-   TMC-Editor: black screen for Choose Language.
-   One-Click PDO-Mapping: a PDO can now be displayed as a structured variable, which may contain sub-structures.

#### IO

-   EthernetIP: new features "CoEoverCIP" and "FwdMsgToAmsPort" and implemented 16 bit Class/Instance/Attribute support.
-   Added support for installing adapter via MAC address.
-   EthernetIP: Forwarding of Class3-Messages to AmsPort (for example PLC) is now implemented.
-   Extension of the diag history for some slaves.
-   Multiple SafetyLogic-devices are now supported.
-   EK9300 and EL6631-0010: support up to 4 ARs in parallel.
-   Profinet: supports feature 'discard IOXS' for the device simulation.
-   EthernetIP: Eth Statistics and IpStack Statistics are now available.
-   Creating a warning if `attribute 'hide'` is used for persistent variables.
-   Initialization via Attribute `'TcInitSymbol'`: Added opportunity to define min and max values in PLC editor which are observed regarding the defined init value in init-table.

#### NC

-   Disable/reduce NC logger messages for flying saw (for example calculate extrema for `MC_GearInVelo`, `MC_GearInPos`) if switching the NC logger level from 2 (SMART) down to 1 (MINIMUM).
-   The "NC Axis Name" can now be longer than 31 characters for more extended information.
-   `MC_GearInMultiMaster` oversampling factor changed down to 10 to get a lower real time usage.
-   Improvement for large master values of splines.
-   New parameter for total covered distance.

### Bug fixes

#### XAE

-   In the RM setup of this version the file TcXaeVsx.15.0.dll is missing. Therefore no TwinSAFE project can be opened (the TwinSAFE are is empty). Manually install this file into the Windows GAC. [Bosch TwinCAT changelog](https://community.developer.bosch.com/t5/Knowledge-base/TwinCAT-XAE-version-overview/ta-p/48982#EN).
-   Tc3Eventlogger: Selection of language keys needed two clicks instead of one.
-   CoE-Online: CoE-Entries of type Octet-String are now displayable up to 0x1000 bytes.
-   Tc Live Watch: Depending on Symbol Selection sometimes an increment was executed twice.
-   Compare tool: compare with target without PLC was not possible.
-   EthernetIP: EDS-Files with a Parameter-Value > INT64 and EDS-Files without Assembly were rejected.
-   Automation Interface: TcXaeShell froze while importing a XTI file of an EL6652.
-   When a Tc2 Runtime was active and TwinCAT 3.1 XAE was trying to activate to configuration on the local hardware no error message was pointing to this error.
-   Axes might not be automatically renamed when copied and pasted between different folder levels.
-   Import of a device via XTI-File named "Device 0" lead to Visual Studio problem.

#### PLC

-   Library content was only shown in Library Manager after reopening the solution.
-   Support of initial values for TcInitSymbol in attribute declaration context.
-   Automation Interface: LibraryManager: Adding a library with three-digit version number contained ".\*" on fourth place.
-   PLC HMI: `VISU_TASK` was duplicated under certain conditions when opening solution.
-   Output Pane "Build" was not cleared before "Check all objects".
-   Error might appear when installing lib from TNZIP archive ("Failed to open managed library (Reason: Object reference not set to an instance of an object)").

## Version 3.1.4022.31

### Features

-   Added: [`Tc2_IoFunctions.FB_TcTouchLock_AcquireFocus`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/6811367563.html?id=3366609942436337282)

## Version 3.1.4022.30

### Bug fixes

-   POUs can be removed from a PLC project in visual studio again.
-   Project compare tool works again. [Bosch TwinCAT changelog](https://community.developer.bosch.com/t5/Knowledge-base/TwinCAT-XAE-version-overview/ta-p/48982#EN).

## Version 3.1.4022.29

### Features

-   Added: [`Tc2_System.FB_IecCriticalSection`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/2326017163.html?id=3047524173527813729)

## Version 3.1.4022.27

### Features

-   Multi dongle support. [Bosch TwinCAT changelog](https://community.developer.bosch.com/t5/Knowledge-base/TwinCAT-XAE-version-overview/ta-p/48982#Header20_en).
-   Zoom function in Structured Text (ST) editor. [Bosch TwinCAT changelog](https://community.developer.bosch.com/t5/Knowledge-base/TwinCAT-XAE-version-overview/ta-p/48982#Header20_en).
-   Supports 'region' to collapse code segments. [Bosch TwinCAT changelog](https://community.developer.bosch.com/t5/Knowledge-base/TwinCAT-XAE-version-overview/ta-p/48982#Header20_en).

### Bugs

-   The Beckhoff project compare tool of this version does not work. [Bosch TwinCAT changelog](https://community.developer.bosch.com/t5/Knowledge-base/TwinCAT-XAE-version-overview/ta-p/48982#EN).

## Version 3.1.4022.20

### Features

-   Added: [`Tc3_EventLogger.FB_TcEvent`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc3_eventlogger/5002372619.html?id=2064727979885894279)
-   Added: [`Tc3_EventLogger.TcEventEntry_TO_HRESULTAdsErr`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc3_eventlogger/5001658763.html?id=367832685679076854)
-   Added: [`Tc3_EventLogger.TcEventEntry_TO_AdsErr`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc3_eventlogger/5001614987.html?id=5482085554043709405)
-   Added: [`Tc3_EventLogger.HRESULTAdsErr_TO_TcEventEntry`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc3_eventlogger/5001571211.html?id=416119473222843714)
-   Added: [`Tc3_EventLogger.AdsErr_TO_TcEventEntry`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc3_eventlogger/5001527435.html?id=7365520287724282087)
-   Added: [`Tc3_EventLogger.F_GetEventText`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc3_eventlogger/5001474059.html?id=1074155452490234211)
-   Added: [`Tc3_EventLogger.F_GetEventClassName`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc3_eventlogger/4278877579.html?id=7811962780376528483)

## Version 3.1.4022.16

### Bug fixes

-   Sometimes the Microsoft patch for Spectre/Meltdown would prevent you from activating the configuration on a local runtime. [See also](https://stackoverflow.com/questions/51185052/twincat-running-on-isolated-cores-failed).

## Version 3.1.4022

### Features

-   Added: [`Tc2_Utilities.F_STRINGEx`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/5780438923.html?id=6928518594785789589)
-   Added: [`Tc2_Utilities.LcomplexAbs`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/3535240971.html?id=826556108380960842)
-   Added: [`Tc2_Utilities.WSTRNCPY`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/3483063563.html?id=3178942571482947329)
-   Added: [`Tc2_Utilities.WSTRING_TO_UTF8`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/3483049227.html?id=1615333347779599462)
-   Added: [`Tc2_Utilities.WSTRING_TO_STRING2`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/3483047691.html?id=2220736197141714813)
-   Added: [`Tc2_Utilities.wsLiteral_TO_UTF8`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/5780535435.html?id=3788526581188074016)
-   Added: [`Tc2_Utilities.WLEN2`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/3483045003.html?id=908431530916067418)
-   Added: [`Tc2_Utilities.WCONCAT2`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/3483043467.html?id=6477035735369982799)
-   Added: [`Tc2_Utilities.WCHAR_TO_CHAR`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/3483040395.html?id=3572446996165722911)
-   Added: [`Tc2_Utilities.UTF8Len`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/3483035787.html?id=5152018493670823258)
-   Added: [`Tc2_Utilities.UTF8_TO_WSTRING`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/3483038859.html?id=6293447896088538757)
-   Added: [`Tc2_Utilities.UTF8_TO_STRING`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/3483037323.html?id=7153306779533761382)
-   Added: [`Tc2_Utilities.STRNCPY`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/3483034251.html?id=6415054610264989739)
-   Added: [`Tc2_Utilities.STRING_TO_WSTRING2`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/3483030795.html?id=4355496359005380414)
-   Added: [`Tc2_Utilities.STRING_TO_UTF8`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/3483029259.html?id=8258377475100135580)
-   Added: [`Tc2_Utilities.sLiteral_TO_UTF8`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/5780471691.html?id=3996529178600600803)
-   Added: [`Tc2_Utilities.REPLACE2`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/6200692747.html?id=309792110435626821)
-   Added: [`Tc2_Utilities.LEN2`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/3483027723.html?id=7966711455956053090)
-   Added: [`Tc2_Utilities.INSERT2`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/6200668299.html?id=6412063259184688465)
-   Added: [`Tc2_Utilities.FindAndReplaceChar`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/6200643851.html?id=6444635135431152359)
-   Added: [`Tc2_Utilities.FindAndReplace`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/6200619403.html?id=5472984639162228823)
-   Added: [`Tc2_Utilities.FindAndDeleteChar`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/6200594955.html?id=3023452241284604042)
-   Added: [`Tc2_Utilities.FindAndDelete`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/6200570507.html?id=3275570602994103116)
-   Added: [`Tc2_Utilities.FIND2`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/6200546059.html?id=8124448501256565351)
-   Added: [`Tc2_Utilities.F_StringIsASCII`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/3483026187.html?id=6403710968972101316)
-   Added: [`Tc2_Utilities.DELETE2`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/6200521611.html?id=1692054860927445572)
-   Added: [`Tc2_Utilities.CONCAT2`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/3483024651.html?id=5935001660749708670)
-   Added: [`Tc2_Utilities.CHAR_TO_WCHAR`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/3482945931.html?id=5128214655345699760)
-   Added: [`Tc2_Utilities.FB_LicFileRead`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/4579085323.html?id=1940182520793325016)
-   Added: [`Tc2_Utilities.FB_LicFileGetStorageInfo`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/4579079563.html?id=3904551008063323022)
-   Added: [`Tc2_Utilities.FB_LicFileDelete`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/4579083403.html?id=6667775283406021036)
-   Added: [`Tc2_Utilities.FB_LicFileCreate`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/4579081483.html?id=3031798484988331324)
-   Added: [`Tc2_Utilities.FB_LicFileCopyToDongle`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/4579189259.html?id=918041785061474232)
-   Added: [`Tc2_Utilities.FB_LicFileCopyFromDongle`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/4579190795.html?id=7323222936363407890)
-   Added: [`Tc2_Utilities.FB_GetLicensesEx`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/4401062667.html?id=2961109817772863253)
-   Added: [`Tc2_Utilities.FB_GetLicenseDongles`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/4400937483.html?id=2696036852839688)
-   Added: [`Tc2_Utilities.FB_GetDongleSystemID`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/4401006475.html?id=3795013013564158743)
-   Added: [`Tc2_Utilities.FB_FormatString2`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/6206471435.html?id=5556582112958115161)
-   Added: [`Tc2_Utilities.FB_CheckLicense`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/4400766091.html?id=5157666698728179333)
-   Added: [`Tc2_System.E_TcMemoryArea`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/4012983947.html?id=388198589678573187)
-   Added: [`Tc2_System.F_CheckMemoryArea`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/4012887435.html?id=1489036489025421628)
-   Added: [`Tc2_System.F_GetStructMemberAlignment`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/31021579.html?id=243854104101513882)
-   Added: [`Tc2_System.FB_FileLoad`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/7083988875.html?id=5357302780541448503)
-   [PLC Static Analyses](https://infosys.beckhoff.com/content/1033/te1200_tc3_plcstaticanalysis/3472333323.html?id=4292646479033383042) is now available.

### Remarks

-   TwinCAT 3.1.4022 handles I/O variables (`%I*`,`%Q*`) differently from all previous versions. If an I/O variable has the attributes `{attribute 'hide'}` or `{attribute 'hide_all_locals'}` (directly or indirectly), this variable is no longer included in the I/O image of the task and therefore cannot be linked any more. [Bosch TwinCAT changelog](https://community.developer.bosch.com/t5/Knowledge-base/TwinCAT-XAE-version-overview/ta-p/48982#EN).

## Version 3.1.4020.56

### Bug fixes

-   Solves many crashes that occurred with XAE 3.1.4020.28. [Bosch TwinCAT changelog](https://community.developer.bosch.com/t5/Knowledge-base/TwinCAT-XAE-version-overview/ta-p/48982#EN).

## Version 3.1.4020.32

### Features

-   Added: [`Tc2_EnOcean.STR_Teach`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_enocean/3266759563.html?id=3118338756872132117)
-   Added: [`Tc2_EnOcean.FB_Rec_Teach_In_Ex`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_enocean/3265337739.html?id=1791501473281069457)

## Version 3.1.4020.28

### Features

<!-- prettier-ignore-start -->
!!! note
    Some of these features were likely already added in an earlier 4020.x release, but it is not known at this point.
<!-- prettier-ignore-end -->

-   Installs Visual Studio Shell 2013. [Bosch TwinCAT changelog](https://community.developer.bosch.com/t5/Knowledge-base/TwinCAT-XAE-version-overview/ta-p/48982#Header26_en).
-   Supports Visual Studio 2015. [Bosch TwinCAT changelog](https://community.developer.bosch.com/t5/Knowledge-base/TwinCAT-XAE-version-overview/ta-p/48982#Header26_en).
-   Supports the Beckhoff license terminal EL6070. [Bosch TwinCAT changelog](https://community.developer.bosch.com/t5/Knowledge-base/TwinCAT-XAE-version-overview/ta-p/48982#Header26_en).
-   Refactoring for easy renaming of variables in the whole project. [Bosch TwinCAT changelog](https://community.developer.bosch.com/t5/Knowledge-base/TwinCAT-XAE-version-overview/ta-p/48982#Header26_en).
-   View any memory areas in an online view. [Bosch TwinCAT changelog](https://community.developer.bosch.com/t5/Knowledge-base/TwinCAT-XAE-version-overview/ta-p/48982#Header26_en).
-   Graphical editor for network variables. [Bosch TwinCAT changelog](https://community.developer.bosch.com/t5/Knowledge-base/TwinCAT-XAE-version-overview/ta-p/48982#Header26_en).
-   Improved cross reference list view. [Bosch TwinCAT changelog](https://community.developer.bosch.com/t5/Knowledge-base/TwinCAT-XAE-version-overview/ta-p/48982#Header26_en).
-   Static code analysis can be activated in the PLC project properties (for example search unused variables). [Bosch TwinCAT changelog](https://community.developer.bosch.com/t5/Knowledge-base/TwinCAT-XAE-version-overview/ta-p/48982#Header26_en).
-   VAR_INST declares variables in methods that don't lose their values. [Bosch TwinCAT changelog](https://community.developer.bosch.com/t5/Knowledge-base/TwinCAT-XAE-version-overview/ta-p/48982#Header26_en).
-   The 'Add Method' dialog shows methods that are available in the interface/base FB. [Bosch TwinCAT changelog](https://community.developer.bosch.com/t5/Knowledge-base/TwinCAT-XAE-version-overview/ta-p/48982#Header26_en).
-   Compiler version can be set in PLC project properties. [Bosch TwinCAT changelog.](https://community.developer.bosch.com/t5/Knowledge-base/TwinCAT-XAE-version-overview/ta-p/48982#Header26_en)
-   Standard placeholder name must be set for library. [Bosch TwinCAT changelog](https://community.developer.bosch.com/t5/Knowledge-base/TwinCAT-XAE-version-overview/ta-p/48982#Header26_en).

## Version 3.1.4020.14

### Features

-   Added: [`Tc2_EnOcean.STREnOceanTurnSwitch`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_enocean/173325451.html?id=8344751103332958602)
-   Added: [`Tc2_EnOcean.str_Teach_In`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_enocean/173323915.html?id=1645475926228910640)
-   Added: [`Tc2_EnOcean.str_KL6581`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_enocean/173322379.html?id=1849350874114595867)
-   Added: [`Tc2_EnOcean.str_EnOceanSwitch`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_enocean/173320843.html?id=967133331712998084)
-   Added: [`Tc2_EnOcean.ar_EnOceanWindow`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_enocean/173316235.html?id=4497504061131638061)
-   Added: [`Tc2_EnOcean.KL6581_Output`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_enocean/173314699.html?id=8314498764829653227)
-   Added: [`Tc2_EnOcean.KL6581_INPUT`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_enocean/173313163.html?id=476066818838415942)
-   Added: [`Tc2_EnOcean.E_KL6581_Err`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_enocean/173319307.html?id=2177669722732776314)
-   Added: [`Tc2_EnOcean.E_ENOCEAN_ORG`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_enocean/173317771.html?id=4340887063652098337)
-   Added: [`Tc2_EnOcean.ST_EnOceanOutData`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_enocean/173303947.html?id=4377393554685815497)
-   Added: [`Tc2_EnOcean.ST_EnOceanInData`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_enocean/173302411.html?id=405068264313064699)
-   Added: [`Tc2_EnOcean.ST_EnOceanReceivedData`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_enocean/173308555.html?id=7540305275148465981)
-   Added: [`Tc2_EnOcean.E_EnOceanRotarySwitch`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_enocean/173305483.html?id=4944000783206766326)
-   Added: [`Tc2_EnOcean.E_EnOceanSensorType`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_enocean/173307019.html?id=7211802311611651249)
-   Added: [`Tc2_EnOcean.FB_KL6581`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_enocean/173271691.html?id=2018704066526963358)
-   Added: [`Tc2_EnOcean.F_Byte_to_TurnSwitch`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_enocean/173296267.html?id=1037290777254805412)
-   Added: [`Tc2_EnOcean.F_Byte_to_Temp : REAL`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_enocean/173294731.html?id=1737968386670885878)
-   Added: [`Tc2_EnOcean.FB_Rec_Teach_In`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_enocean/173291659.html?id=3977267665892819984)
-   Added: [`Tc2_EnOcean.FB_EnOcean_Search`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_enocean/173290123.html?id=7040304177183103980)
-   Added: [`Tc2_EnOcean.FB_Send_RPS_SwitchAuto`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_enocean/173287051.html?id=1270903652977417213)
-   Added: [`Tc2_EnOcean.FB_Send_RPS_Switch`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_enocean/173285515.html?id=351705534079193646)
-   Added: [`Tc2_EnOcean.FB_Send_4BS`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_enocean/173283979.html?id=4782298309082697193)
-   Added: [`Tc2_EnOcean.FB_Send_Generic`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_enocean/173282443.html?id=647830454839166271)
-   Added: [`Tc2_EnOcean.FB_Rec_RPS_Window_Handle`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_enocean/173279371.html?id=4686396558067360307)
-   Added: [`Tc2_EnOcean.FB_Rec_RPS_Switch`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_enocean/173277835.html?id=392505539603118572)
-   Added: [`Tc2_EnOcean.FB_Rec_1BS`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_enocean/173276299.html?id=7378271872182580324)
-   Added: [`Tc2_EnOcean.FB_Rec_Generic`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_enocean/173274763.html?id=6797398776960182165)
-   Added: [`Tc2_EnOcean.FB_EnOceanReceive`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_enocean/173259531.html?id=1369144730198496585)
-   Added: [`Tc2_EnOcean.FB_EnOceanSTM250`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_enocean/173268747.html?id=8297698902080423397)
-   Added: [`Tc2_EnOcean.FB_EnOceanSTM100Generic`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_enocean/173267211.html?id=7118851703692596416)
-   Added: [`Tc2_EnOcean.FB_EnOceanSTM100`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_enocean/173265675.html?id=4218480928603569422)
-   Added: [`Tc2_EnOcean.FB_EnOceanPTM200`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_enocean/173264139.html?id=7967709273063239379)
-   Added: [`Tc2_EnOcean.FB_EnOceanPTM100`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_enocean/173262603.html?id=8645358322841840689)

## Version 3.1.4020

### Features

-   Added: [`Tc2_Utilities.LcomplexIsNaN`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/2572609163.html?id=6044264011573247633)
-   Added: [`Tc2_Utilities.LrealIsNaN`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/2572585227.html?id=2372301365200231803)
-   Added: [`Tc2_Utilities.LrealIsFinite`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/2570925451.html?id=7196312205168836986)
-   Added: [`Tc2_System.EPlcMappingStatus`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/2311319051.html?id=3465373249780383475)
-   Added: [`Tc2_System.F_GetMappingStatus`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/2284515083.html?id=684169368415701977)
-   Added: [`Tc2_System.F_GetMappingPartner`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/2284517003.html?id=7947956587606470653)

## Version 3.1.4018.26

### Features

-   Added: [`Tc2_IoFunctions.ST_KL3228OutData`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/2089267979.html?id=5656335580876414190)
-   Added: [`Tc2_IoFunctions.ST_KL3228InData`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/2089238283.html?id=713835624597037823)
-   Added: [`Tc2_IoFunctions.ST_KL3208OutData`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/2089076235.html?id=4857640062192595820)
-   Added: [`Tc2_IoFunctions.ST_KL3208InData`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/2089074315.html?id=8605529518157709704)
-   Added: [`Tc2_IoFunctions.ST_KL320xOutData`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/2088746123.html?id=8512988496742093284)
-   Added: [`Tc2_IoFunctions.ST_KL320xInData`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/2088742027.html?id=1032412485831878947)
-   Added: [`Tc2_IoFunctions.ST_KL27x1OutData`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/2086569483.html?id=5839773933410659770)
-   Added: [`Tc2_IoFunctions.ST_KL27x1InData`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/2086383115.html?id=8894321869386542373)
-   Added: [`Tc2_IoFunctions.ST_KL1501OutData`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/2085793931.html?id=6048066777263751203)
-   Added: [`Tc2_IoFunctions.ST_KL1501InData`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/2085789835.html?id=2837453486903490695)
-   Added: [`Tc2_IoFunctions.FB_KL3228Config`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/2084386699.html?id=1430169788192964615)
-   Added: [`Tc2_IoFunctions.FB_KL3208Config`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/2084384779.html?id=744984473151509137)
-   Added: [`Tc2_IoFunctions.FB_KL320xConfig`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/2084382859.html?id=166311612032330740)
-   Added: [`Tc2_IoFunctions.FB_KL27x1Config`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/2084380939.html?id=166107339342627340)
-   Added: [`Tc2_IoFunctions.FB_KL1501Config`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/2084379019.html?id=5228753612861554565)

## Version 3.1.4018

### Features

-   Added: [`Tc2_Utilities.FB_GetVolumeId`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/2220215051.html?id=788353785489284857)
-   Added: [`Tc2_Utilities.FB_GetLicenses`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/1876715915.html?id=928231625113806812)
-   Added: [`Tc2_Utilities.ST_TcOnlineLicensesInfoData`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/1876880907.html?id=3739149647499681467)

## Version 3.1.4013

### Features

-   Added: [`Tc2_MDP.FB_MDP_ReadIndex`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_mdp/178718603.html?id=1682933375785172630)

## Version 3.1.0

<!-- prettier-ignore-start -->
!!! warning
    While converting TwinCAT 3.0 projects into the TwinCAT 3.1 unexpected Negations and Edge Detection can occur in FBD/LD. Please check your app after the conversion process.
<!-- prettier-ignore-end -->

### Features

-   Added: [`Tc2_Utilities.Global variables`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35395979.html?id=8384408792737751163)
-   Added: [`Tc2_Utilities.Scope Server error codes`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35406091.html?id=5719100329143363550)
-   Added: [`Tc2_Utilities.Format error codes`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35404555.html?id=1770040212223908565)
-   Added: [`Tc2_Utilities.Library version`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35397515.html?id=7459432748981184301)
-   Added: [`Tc2_Utilities.TIMESTRUCT`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35393035.html?id=8702657298802174446)
-   Added: [`Tc2_Utilities.T_ULARGE_INTEGER`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35391499.html?id=903057947372500828)
-   Added: [`Tc2_Utilities.T_UHUGE_INTEGER`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35389963.html?id=7203960545252469009)
-   Added: [`Tc2_Utilities.T_LinkedListEntry`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35388427.html?id=1382431520910497628)
-   Added: [`Tc2_Utilities.T_LARGE_INTEGER`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35386891.html?id=7916491647829655535)
-   Added: [`Tc2_Utilities.T_HUGE_INTEGER`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35385355.html?id=3950098776479849856)
-   Added: [`Tc2_Utilities.T_HLINKEDLIST`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35383819.html?id=6463166586288794433)
-   Added: [`Tc2_Utilities.T_HHASHTABLE`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35382283.html?id=1314201873944421901)
-   Added: [`Tc2_Utilities.T_HashTableEntry`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35380747.html?id=6484631637881566512)
-   Added: [`Tc2_Utilities.T_FIX16`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35379211.html?id=6836442093029631718)
-   Added: [`Tc2_Utilities.T_FILETIME`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35377675.html?id=7765283772809288862)
-   Added: [`Tc2_Utilities.T_Arg`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35376139.html?id=4303460770811510149)
-   Added: [`Tc2_Utilities.SYMINFOSTRUCT`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35374603.html?id=8910182120536424650)
-   Added: [`Tc2_Utilities.ST_TimeZoneInformation`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35373067.html?id=2892811750112150085)
-   Added: [`Tc2_Utilities.ST_TcRouterStatusInfo`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35368459.html?id=3560183768341915186)
-   Added: [`Tc2_Utilities.ST_IPAdapterInfo`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35369995.html?id=4297716681872320508)
-   Added: [`Tc2_Utilities.ST_IPAdapterHwAddr`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35371531.html?id=5982141052673159009)
-   Added: [`Tc2_Utilities.ST_FindFileEntry`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35363851.html?id=2306276416492527815)
-   Added: [`Tc2_Utilities.ST_FileRBufferHead`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35366923.html?id=2589851144449731204)
-   Added: [`Tc2_Utilities.ST_FileAttributes`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35365387.html?id=6209988741843175450)
-   Added: [`Tc2_Utilities.ST_DeviceIdentificationEx`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35362315.html?id=3229467194388972446)
-   Added: [`Tc2_Utilities.ST_DeviceIdentification`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35360779.html?id=452745701272899130)
-   Added: [`Tc2_Utilities.ST_AmsRouteEntry`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35359243.html?id=7858700389071522190)
-   Added: [`Tc2_Utilities.REMOTEPCINFOSTRUCT`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35357707.html?id=7199590905995204173)
-   Added: [`Tc2_Utilities.REMOTEPC`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35356171.html?id=340597287862758198)
-   Added: [`Tc2_Utilities.PROFILERSTRUCT`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35354635.html?id=6934659945430697843)
-   Added: [`Tc2_Utilities.OTSTRUCT`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35353099.html?id=8265378500365774535)
-   Added: [`Tc2_Utilities.GUID`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35351563.html?id=7636427912872503858)
-   Added: [`Tc2_Utilities.FLOAT`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/943979659.html?id=5652135896164183944)
-   Added: [`Tc2_Utilities.E_TypeFieldParam`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35350027.html?id=4367383807024774516)
-   Added: [`Tc2_Utilities.E_TimeZoneID`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35348491.html?id=2833211600178520825)
-   Added: [`Tc2_Utilities.E_ScopeServerState`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/940189707.html?id=6121204461511790439)
-   Added: [`Tc2_Utilities.E_SBCSType`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35346955.html?id=5528768705598737103)
-   Added: [`Tc2_Utilities.E_RouteTransportType`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35345419.html?id=4874223551761370592)
-   Added: [`Tc2_Utilities.E_RegValueType`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35343883.html?id=7414914988885001789)
-   Added: [`Tc2_Utilities.E_PersistentMode`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35342347.html?id=5134531873383837677)
-   Added: [`Tc2_Utilities.E_NumGroupTypes`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35340811.html?id=8629188097575161459)
-   Added: [`Tc2_Utilities.E_MIB_IF_Type`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35339275.html?id=7119332669458084866)
-   Added: [`Tc2_Utilities.E_EnumCmdType`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35337739.html?id=2812609428987641783)
-   Added: [`Tc2_Utilities.E_DbgDirection`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35336203.html?id=543645103038010161)
-   Added: [`Tc2_Utilities.E_DbgContext`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35334667.html?id=7401714136491538740)
-   Added: [`Tc2_Utilities.E_ArgType`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35333131.html?id=5990470506210755342)
-   Added: [`Tc2_Utilities.E_AmsLoggerMode`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35331595.html?id=1516874025933751557)
-   Added: [`Tc2_Utilities.ADSDATATYPEID`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35330059.html?id=512680895141484868)
-   Added: [`Tc2_Utilities.WORD_TO_OCTSTR`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/934166923.html?id=6841565986598965682)
-   Added: [`Tc2_Utilities.WORD_TO_LREALEX`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/2212661387.html?id=916044469910681049)
-   Added: [`Tc2_Utilities.WORD_TO_HEXSTR`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/934165003.html?id=1329115840627595534)
-   Added: [`Tc2_Utilities.WORD_TO_DECSTR`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/934163083.html?id=6494099606803731303)
-   Added: [`Tc2_Utilities.WORD_TO_BINSTR`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/934161163.html?id=4886154460641569722)
-   Added: [`Tc2_Utilities.USINT_TO_LREALEX`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/2213035787.html?id=430141970236187168)
-   Added: [`Tc2_Utilities.ULINT_TO_ULARGE`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/934159243.html?id=3999767363785127373)
-   Added: [`Tc2_Utilities.UINT_TO_LREALEX`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/2213074827.html?id=7751544911208402078)
-   Added: [`Tc2_Utilities.UDINT_TO_LREALEX`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/2213114763.html?id=7038826774994224979)
-   Added: [`Tc2_Utilities.STRING_TO_PVOID`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35105291.html?id=1951851232975809582)
-   Added: [`Tc2_Utilities.STRING_TO_GUID`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/934149643.html?id=4271930352343599436)
-   Added: [`Tc2_Utilities.STRING_TO_CSVFIELD`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35151371.html?id=6736970882974784292)
-   Added: [`Tc2_Utilities.ROUTETRANSPORT_TO_STRING`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35149835.html?id=6253308102615836486)
-   Added: [`Tc2_Utilities.REGSTRING_TO_GUID`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/934147723.html?id=2744331275923345698)
-   Added: [`Tc2_Utilities.RAD_TO_DEG`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35148299.html?id=6943900450932540605)
-   Added: [`Tc2_Utilities.PVOID_TO_STRING`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35103755.html?id=5792338378170752675)
-   Added: [`Tc2_Utilities.PVOID_TO_OCTSTR`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35102219.html?id=4629565546002748600)
-   Added: [`Tc2_Utilities.PVOID_TO_HEXSTR`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35100683.html?id=5255756717611263149)
-   Added: [`Tc2_Utilities.PVOID_TO_DECSTR`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35099147.html?id=2822889885615817394)
-   Added: [`Tc2_Utilities.PVOID_TO_BINSTR`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35097611.html?id=360901508631302635)
-   Added: [`Tc2_Utilities.MAXSTRING_TO_BYTEARR`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35145227.html?id=1019793702447535112)
-   Added: [`Tc2_Utilities.LWORD_TO_OCTSTR`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35096075.html?id=7946377347477324601)
-   Added: [`Tc2_Utilities.LWORD_TO_HEXSTR`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35094539.html?id=9056152593524926659)
-   Added: [`Tc2_Utilities.LWORD_TO_DECSTR`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35093003.html?id=1400482357682585457)
-   Added: [`Tc2_Utilities.LWORD_TO_BINSTR`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35091467.html?id=6799369531520514133)
-   Added: [`Tc2_Utilities.LREAL_TO_FMTSTR`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35143691.html?id=6720667818939867763)
-   Added: [`Tc2_Utilities.LINT_TO_DECSTR`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35106827.html?id=4937145758280264800)
-   Added: [`Tc2_Utilities.HEXSTR_TO_DATA`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35140619.html?id=5205741653811515604)
-   Added: [`Tc2_Utilities.HEXCHRNIBBLE_TO_BYTE`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/934088715.html?id=1243586613113493913)
-   Added: [`Tc2_Utilities.HEXASCNIBBLE_TO_BYTE`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/934086795.html?id=6254177949920459264)
-   Added: [`Tc2_Utilities.GuidsEqualByVal`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/934084875.html?id=1910294614486467239)
-   Added: [`Tc2_Utilities.GUID_TO_STRING`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35275147.html?id=1054964383492008964)
-   Added: [`Tc2_Utilities.GUID_TO_REGSTRING`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/934082955.html?id=2176650956471423670)
-   Added: [`Tc2_Utilities.F_ToUCase`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35132939.html?id=5823016739829411369)
-   Added: [`Tc2_Utilities.F_ToLCase`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35131403.html?id=7280265313049733054)
-   Added: [`Tc2_Utilities.F_SwapRealEx`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35129867.html?id=7670828056657445794)
-   Added: [`Tc2_Utilities.F_RTrim`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35128331.html?id=2288903806933995037)
-   Added: [`Tc2_Utilities.F_LTrim`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35126795.html?id=6101918998057981211)
-   Added: [`Tc2_Utilities.F_FormatArgToStr`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35116043.html?id=2457253001707641518)
-   Added: [`Tc2_Utilities.F_DATA_TO_CRC16_CCITT`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35114507.html?id=7066859934994163966)
-   Added: [`Tc2_Utilities.F_CreateLinkedListHnd`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35112971.html?id=6596879855765228279)
-   Added: [`Tc2_Utilities.F_CreateHashTableHnd`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35111435.html?id=4939351379059099055)
-   Added: [`Tc2_Utilities.F_CheckSum16`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35109899.html?id=7036600283175449285)
-   Added: [`Tc2_Utilities.F_BYTE_TO_CRC16_CCITT`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35108363.html?id=9078255097492717812)
-   Added: [`Tc2_Utilities.DWORD_TO_OCTSTR`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35089931.html?id=4257840501587214463)
-   Added: [`Tc2_Utilities.DWORD_TO_LREALEX`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/2212972555.html?id=7836732529653262275)
-   Added: [`Tc2_Utilities.DWORD_TO_HEXSTR`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35088395.html?id=3527210939858050100)
-   Added: [`Tc2_Utilities.DWORD_TO_DECSTR`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35086859.html?id=7925826810357311250)
-   Added: [`Tc2_Utilities.DWORD_TO_BINSTR`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35085323.html?id=706052573839393671)
-   Added: [`Tc2_Utilities.DINT_TO_DECSTR`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35080715.html?id=4892355979349687241)
-   Added: [`Tc2_Utilities.DEG_TO_RAD`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35079179.html?id=4591030159474850646)
-   Added: [`Tc2_Utilities.DATA_TO_HEXSTR`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35077643.html?id=9121987706364969128)
-   Added: [`Tc2_Utilities.CSVFIELD_TO_STRING`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35074571.html?id=991884904230780528)
-   Added: [`Tc2_Utilities.CSVFIELD_TO_ARG`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35076107.html?id=3737290851128154983)
-   Added: [`Tc2_Utilities.BYTEARR_TO_MAXSTRING`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35073035.html?id=6681435453889039356)
-   Added: [`Tc2_Utilities.BYTE_TO_OCTSTR`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/934062475.html?id=5738221260973610397)
-   Added: [`Tc2_Utilities.BYTE_TO_LREALEX`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/2211114507.html?id=6820365430001345953)
-   Added: [`Tc2_Utilities.BYTE_TO_HEXSTR`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/934060555.html?id=6236458730093908414)
-   Added: [`Tc2_Utilities.BYTE_TO_DECSTR`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/934058635.html?id=1618789017430222093)
-   Added: [`Tc2_Utilities.BYTE_TO_BINSTR`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/934054283.html?id=2355405401787121303)
-   Added: [`Tc2_Utilities.ARG_TO_CSVFIELD`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35071499.html?id=9126412392431262291)
-   Added: [`Tc2_Utilities.FLOATIsNaN`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/943967755.html?id=1838464149590219465)
-   Added: [`Tc2_Utilities.FLOATIsFinite`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/943965835.html?id=4915550531319593734)
-   Added: [`Tc2_Utilities.FUNCTION F_GetVersionTcUtilities`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35327115.html?id=3459898951448964355)
-   Added: [`Tc2_Utilities.SYSTEMTIME_TO_FILETIME`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35154443.html?id=3449046629778963404)
-   Added: [`Tc2_Utilities.FILETIME_TO_SYSTEMTIME`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35139083.html?id=6985172120444651838)
-   Added: [`Tc2_Utilities.FILETIME_TO_DT`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35137547.html?id=714857431038582720)
-   Added: [`Tc2_Utilities.F_TranslateFileTimeBias`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35134475.html?id=4505695018305923649)
-   Added: [`Tc2_Utilities.DT_TO_FILETIME`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35083787.html?id=712153201765866519)
-   Added: [`Tc2_Utilities.IsFinite`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35142155.html?id=1043882056502967499)
-   Added: [`Tc2_Utilities.F_PVOID`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/1045719307.html?id=883146580170063410)
-   Added: [`Tc2_Utilities.F_WORD`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35246091.html?id=7009039060622253461)
-   Added: [`Tc2_Utilities.F_USINT`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35253771.html?id=4023657696478255295)
-   Added: [`Tc2_Utilities.F_ULINT`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/934081035.html?id=6947094128907291163)
-   Added: [`Tc2_Utilities.F_ULARGE`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35266059.html?id=1488778765125905570)
-   Added: [`Tc2_Utilities.F_UINT`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35255307.html?id=6518471884665964321)
-   Added: [`Tc2_Utilities.F_UHUGE`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35267595.html?id=480652504517157631)
-   Added: [`Tc2_Utilities.F_UDINT`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35256843.html?id=5681504186896032553)
-   Added: [`Tc2_Utilities.F_STRING`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35258379.html?id=3106323875140785277)
-   Added: [`Tc2_Utilities.F_SINT`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35249163.html?id=2764904603582094293)
-   Added: [`Tc2_Utilities.F_REAL`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35243019.html?id=8982232529778322456)
-   Added: [`Tc2_Utilities.F_LWORD`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/934079115.html?id=168538439331959484)
-   Added: [`Tc2_Utilities.F_LREAL`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35241483.html?id=8366189779638536047)
-   Added: [`Tc2_Utilities.F_LINT`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/934064395.html?id=8141791499014565689)
-   Added: [`Tc2_Utilities.F_LARGE`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35262987.html?id=4594031828251190436)
-   Added: [`Tc2_Utilities.F_INT`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35250699.html?id=6018671144943405334)
-   Added: [`Tc2_Utilities.F_HUGE`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35264523.html?id=3711961633556049615)
-   Added: [`Tc2_Utilities.F_DWORD`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35247627.html?id=205138728064578746)
-   Added: [`Tc2_Utilities.F_DINT`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35252235.html?id=4048487626881792371)
-   Added: [`Tc2_Utilities.F_BYTE`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35244555.html?id=2229644544680865904)
-   Added: [`Tc2_Utilities.F_BOOL`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35259915.html?id=1773570001873970249)
-   Added: [`Tc2_Utilities.F_BIGTYPE`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35261451.html?id=4246224379346462247)
-   Added: [`Tc2_Utilities.F_ARGISZERO`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35272203.html?id=8866936713706229316)
-   Added: [`Tc2_Utilities.F_ARGCPY`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35269131.html?id=1094494038130169711)
-   Added: [`Tc2_Utilities.F_ARGCMP`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35270667.html?id=8363936404629481328)
-   Added: [`Tc2_Utilities.ULARGE_TO_LWORD`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/934155403.html?id=6416846161733105283)
-   Added: [`Tc2_Utilities.ULARGE_TO_ULINT`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/934157323.html?id=8599215117081378247)
-   Added: [`Tc2_Utilities.ULARGE_INTEGER`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35161995.html?id=3128035529337445572)
-   Added: [`Tc2_Utilities.UInt64Xor`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35181963.html?id=2106972245632462505)
-   Added: [`Tc2_Utilities.UInt64Sub64`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35166603.html?id=1289296020658697402)
-   Added: [`Tc2_Utilities.UInt64Shr`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35191179.html?id=8537389838484242959)
-   Added: [`Tc2_Utilities.UInt64Shl`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35189643.html?id=6800277673562024796)
-   Added: [`Tc2_Utilities.UInt64Ror`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35194251.html?id=2728485763345449011)
-   Added: [`Tc2_Utilities.UInt64Rol`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35192715.html?id=2567307711739500816)
-   Added: [`Tc2_Utilities.UInt64Or`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35180427.html?id=2852322177096801522)
-   Added: [`Tc2_Utilities.UInt64Not`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35183499.html?id=8878036784472504495)
-   Added: [`Tc2_Utilities.UInt64Mul64Ex`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35171211.html?id=7175833395589010626)
-   Added: [`Tc2_Utilities.UInt64Mul64`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35169675.html?id=5868848726325631160)
-   Added: [`Tc2_Utilities.UInt64Mod64`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35175819.html?id=1232209458534102039)
-   Added: [`Tc2_Utilities.UInt64Min`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35185035.html?id=6031925429663501634)
-   Added: [`Tc2_Utilities.UInt64Max`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35186571.html?id=1705275296937486086)
-   Added: [`Tc2_Utilities.UInt64Limit`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35188107.html?id=1257027336043069180)
-   Added: [`Tc2_Utilities.UInt64isZero`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35195787.html?id=1535310518263227025)
-   Added: [`Tc2_Utilities.UInt64Div64Ex`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35174283.html?id=6475950224674757927)
-   Added: [`Tc2_Utilities.UInt64Div64`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35172747.html?id=2797743446202223990)
-   Added: [`Tc2_Utilities.UInt64Div16Ex`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/934153483.html?id=2480514477408574505)
-   Added: [`Tc2_Utilities.UInt64Cmp64`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35177355.html?id=4337932291555986996)
-   Added: [`Tc2_Utilities.UInt64And`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35178891.html?id=8126930828474828741)
-   Added: [`Tc2_Utilities.UInt64Add64Ex`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35165067.html?id=1528227693291443152)
-   Added: [`Tc2_Utilities.UInt64Add64`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35163531.html?id=4620736216237798909)
-   Added: [`Tc2_Utilities.UINT64_TO_STRING`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35201931.html?id=5281928101444194996)
-   Added: [`Tc2_Utilities.UINT64_TO_LREAL`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35200395.html?id=1649303133953636941)
-   Added: [`Tc2_Utilities.UInt32x32To64`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35168139.html?id=8414926393061992093)
-   Added: [`Tc2_Utilities.STRING_TO_UINT64`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35198859.html?id=1510435236053910249)
-   Added: [`Tc2_Utilities.LWORD_TO_ULARGE`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/934116875.html?id=6671432503746471938)
-   Added: [`Tc2_Utilities.LREAL_TO_UINT64`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35197323.html?id=854115184427313292)
-   Added: [`Tc2_Utilities.ULARGE_TO_LARGE`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35221771.html?id=1189768079091945050)
-   Added: [`Tc2_Utilities.LREAL_TO_INT64`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35218699.html?id=9137569552693668427)
-   Added: [`Tc2_Utilities.LINT_TO_LARGE`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/934107275.html?id=2674888564092284429)
-   Added: [`Tc2_Utilities.LARGE_TO_ULARGE`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35223307.html?id=5591451167417512812)
-   Added: [`Tc2_Utilities.LARGE_TO_LINT`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/934103435.html?id=4029054312141802115)
-   Added: [`Tc2_Utilities.LARGE_INTEGER`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35204875.html?id=8125500571766213108)
-   Added: [`Tc2_Utilities.Int64Sub64`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35209483.html?id=1549224722020523166)
-   Added: [`Tc2_Utilities.Int64Not`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35214091.html?id=400265801186335991)
-   Added: [`Tc2_Utilities.Int64Negate`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35215627.html?id=2081408890574471178)
-   Added: [`Tc2_Utilities.Int64IsZero`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35217163.html?id=3254188185657117492)
-   Added: [`Tc2_Utilities.Int64Div64Ex`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35211019.html?id=7359198786671461766)
-   Added: [`Tc2_Utilities.Int64Cmp64`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35212555.html?id=3134549235916072298)
-   Added: [`Tc2_Utilities.Int64Add64Ex`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35207947.html?id=6069414738064228838)
-   Added: [`Tc2_Utilities.Int64Add64`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35206411.html?id=6488246879817240831)
-   Added: [`Tc2_Utilities.INT64_TO_LREAL`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35220235.html?id=4311457723733125390)
-   Added: [`Tc2_Utilities.WORD_TO_FIX16`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35229323.html?id=9065019551025122960)
-   Added: [`Tc2_Utilities.LREAL_TO_FIX16`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35226251.html?id=8778565072916566522)
-   Added: [`Tc2_Utilities.FIX16Sub`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35238539.html?id=2273337295236478150)
-   Added: [`Tc2_Utilities.FIX16Mul`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35237003.html?id=9051460318846130861)
-   Added: [`Tc2_Utilities.FIX16Div`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35235467.html?id=7109694394042473223)
-   Added: [`Tc2_Utilities.FIX16Align`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35233931.html?id=2815224582117820559)
-   Added: [`Tc2_Utilities.FIX16Add`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35232395.html?id=4834915343913620324)
-   Added: [`Tc2_Utilities.FIX16_TO_WORD`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35230859.html?id=7697330003548602202)
-   Added: [`Tc2_Utilities.FIX16_TO_LREAL`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35227787.html?id=7508484843146611388)
-   Added: [`Tc2_Utilities.PUINT64_TO_UINT64`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/2220223371.html?id=5772113000564842953)
-   Added: [`Tc2_Utilities.PWORD_TO_WORD`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35302795.html?id=2718166055622092660)
-   Added: [`Tc2_Utilities.PUSINT_TO_USINT`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35301259.html?id=8921171465142541397)
-   Added: [`Tc2_Utilities.PULINT_TO_ULINT`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/934122635.html?id=263407774263203474)
-   Added: [`Tc2_Utilities.PULARGE_TO_ULARGE`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35307403.html?id=8297975004347427103)
-   Added: [`Tc2_Utilities.PUINT_TO_UINT`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35299723.html?id=6044453740033084238)
-   Added: [`Tc2_Utilities.PUHUGE_TO_UHUGE`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35308939.html?id=1309614677342840482)
-   Added: [`Tc2_Utilities.PUDINT_TO_UDINT`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35298187.html?id=71069949523359218)
-   Added: [`Tc2_Utilities.PTOD_TO_TOD`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35296651.html?id=3753369561874503500)
-   Added: [`Tc2_Utilities.PTIME_TO_TIME`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35295115.html?id=5957165953486369103)
-   Added: [`Tc2_Utilities.PSTRING_TO_STRING`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35293579.html?id=4195909348948855622)
-   Added: [`Tc2_Utilities.PSINT_TO_SINT`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35292043.html?id=35068633702410481)
-   Added: [`Tc2_Utilities.PREAL_TO_REAL`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35290507.html?id=8149517492878201452)
-   Added: [`Tc2_Utilities.PMAXSTRING_TO_MAXSTRING`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35288971.html?id=6168275541109155476)
-   Added: [`Tc2_Utilities.PLWORD_TO_LWORD`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/934120715.html?id=4762649928700892500)
-   Added: [`Tc2_Utilities.PLREAL_TO_LREAL`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35287435.html?id=7217531594164391720)
-   Added: [`Tc2_Utilities.PLINT_TO_LINT`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/934118795.html?id=8724964637342310934)
-   Added: [`Tc2_Utilities.PLARGE_TO_LARGE`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35304331.html?id=6644328869881696034)
-   Added: [`Tc2_Utilities.PINT_TO_INT`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35285899.html?id=7354578959822593704)
-   Added: [`Tc2_Utilities.PHUGE_TO_HUGE`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35305867.html?id=4054720417472016362)
-   Added: [`Tc2_Utilities.PDWORD_TO_DWORD`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35284363.html?id=3378965930051685988)
-   Added: [`Tc2_Utilities.PDT_TO_DT`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35282827.html?id=4337200904347058488)
-   Added: [`Tc2_Utilities.PDINT_TO_DINT`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35281291.html?id=4256490369626721716)
-   Added: [`Tc2_Utilities.PDATE_TO_DATE`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35279755.html?id=4574350570122305698)
-   Added: [`Tc2_Utilities.PBYTE_TO_BYTE`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35278219.html?id=5195754968778398006)
-   Added: [`Tc2_Utilities.PBOOL_TO_BOOL`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35276683.html?id=6992940055273629608)
-   Added: [`Tc2_Utilities.UINT_TO_FLOAT`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/943733771.html?id=8351098378597626570)
-   Added: [`Tc2_Utilities.UDINT_TO_FLOAT`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/943731851.html?id=5501931882767486999)
-   Added: [`Tc2_Utilities.TIME_TO_FLOAT`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/943729931.html?id=8194013308775969060)
-   Added: [`Tc2_Utilities.SINT_TO_FLOAT`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/943728011.html?id=8731904582595666724)
-   Added: [`Tc2_Utilities.INT_TO_FLOAT`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/943726091.html?id=4545076421052762660)
-   Added: [`Tc2_Utilities.FLOAT_TO_UINT`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/943724171.html?id=393302490095892601)
-   Added: [`Tc2_Utilities.FLOAT_TO_UDINT`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/943722251.html?id=4981662138545824744)
-   Added: [`Tc2_Utilities.FLOAT_TO_TIME`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/943669131.html?id=3993837365865625041)
-   Added: [`Tc2_Utilities.FLOAT_TO_STRING`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/943667211.html?id=6377304107891600372)
-   Added: [`Tc2_Utilities.FLOAT_TO_SINT`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/943665291.html?id=4823370286741197895)
-   Added: [`Tc2_Utilities.FLOAT_TO_INT`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/943662987.html?id=583816791166690909)
-   Added: [`Tc2_Utilities.FLOAT_TO_DINT`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/943661067.html?id=7097733729241137194)
-   Added: [`Tc2_Utilities.FLOAT_TO_BOOL`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/943659147.html?id=1330944428227804622)
-   Added: [`Tc2_Utilities.DINT_TO_FLOAT`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/943260427.html?id=2601904494790478660)
-   Added: [`Tc2_Utilities.BOOL_TO_FLOAT`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/943258507.html?id=3030576808662329875)
-   Added: [`Tc2_Utilities.BE128_TO_HOST`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35324171.html?id=6552972504423238717)
-   Added: [`Tc2_Utilities.BE64_TO_HOSTEX`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/1045676555.html?id=6647565358516035954)
-   Added: [`Tc2_Utilities.BE64_TO_HOST`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35322635.html?id=2967976195496426596)
-   Added: [`Tc2_Utilities.BE32_TO_HOST`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35321099.html?id=1298415622273328742)
-   Added: [`Tc2_Utilities.BE16_TO_HOST`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35319563.html?id=59904381359465393)
-   Added: [`Tc2_Utilities.HOST_TO_BE128`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35318027.html?id=8175914231875433279)
-   Added: [`Tc2_Utilities.HOST_TO_BE64EX`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/1045651723.html?id=2289128778885172732)
-   Added: [`Tc2_Utilities.HOST_TO_BE64`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35316491.html?id=2662853526703802139)
-   Added: [`Tc2_Utilities.HOST_TO_BE32`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35314955.html?id=5354152328814139814)
-   Added: [`Tc2_Utilities.HOST_TO_BE16`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35313419.html?id=659151316484953777)
-   Added: [`Tc2_Utilities.TIME_TO_OTSTRUCT`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35159051.html?id=715092067058852467)
-   Added: [`Tc2_Utilities.SYSTEMTIME_TO_STRING`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35155979.html?id=6637749211967406032)
-   Added: [`Tc2_Utilities.SYSTEMTIME_TO_DT`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35152907.html?id=4134052663805984271)
-   Added: [`Tc2_Utilities.STRING_TO_SYSTEMTIME`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35157515.html?id=4045416622601602973)
-   Added: [`Tc2_Utilities.OTSTRUCT_TO_TIME`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35146763.html?id=7421131295625244336)
-   Added: [`Tc2_Utilities.F_YearIsLeapYear`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35136011.html?id=6869414046637521502)
-   Added: [`Tc2_Utilities.F_GetWeekOfTheYear`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35123723.html?id=8505300351759711250)
-   Added: [`Tc2_Utilities.F_GetMonthOfDOY`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35120651.html?id=2072276066944645961)
-   Added: [`Tc2_Utilities.F_GetMaxMonthDays`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35117579.html?id=1671476201832300855)
-   Added: [`Tc2_Utilities.F_GetDOYOfYearMonthDay`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35119115.html?id=3670299393488615030)
-   Added: [`Tc2_Utilities.F_GetDayOfWeek`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35122187.html?id=8566554814036540955)
-   Added: [`Tc2_Utilities.F_GetDayOfMonthEx`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35125259.html?id=6650246604038981253)
-   Added: [`Tc2_Utilities.DT_TO_SYSTEMTIME`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35082251.html?id=5771960863019550498)
-   Added: [`Tc2_Utilities.WritePersistentData`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35068555.html?id=5808091726951961717)
-   Added: [`Tc2_Utilities.TC_SysLatency`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35067019.html?id=4076558575770605053)
-   Added: [`Tc2_Utilities.TC_Stop`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35065483.html?id=563113409583266283)
-   Added: [`Tc2_Utilities.TC_Restart`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35063947.html?id=7621848372650717543)
-   Added: [`Tc2_Utilities.TC_CpuUsage`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35062411.html?id=2867378847037993375)
-   Added: [`Tc2_Utilities.TC_Config`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35060875.html?id=2743519983327691286)
-   Added: [`Tc2_Utilities.RTC_EX2`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35057803.html?id=3496302990382559954)
-   Added: [`Tc2_Utilities.RTC_EX`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35056267.html?id=5214209714939984270)
-   Added: [`Tc2_Utilities.RTC`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35054731.html?id=8923129215205489819)
-   Added: [`Tc2_Utilities.Profiler`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35053195.html?id=1344160655692967299)
-   Added: [`Tc2_Utilities.PLC_Stop`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35047051.html?id=8726266713454962575)
-   Added: [`Tc2_Utilities.PLC_Start`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35045515.html?id=3643975377693650589)
-   Added: [`Tc2_Utilities.PLC_Reset`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35043979.html?id=1868200634473488282)
-   Added: [`Tc2_Utilities.PLC_ReadSymInfoByNameEx`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35051659.html?id=4749947154059678748)
-   Added: [`Tc2_Utilities.PLC_ReadSymInfoByName`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35050123.html?id=3003880563607590699)
-   Added: [`Tc2_Utilities.PLC_ReadSymInfo`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35048587.html?id=5440793265206539582)
-   Added: [`Tc2_Utilities.NT_StartProcess`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35042443.html?id=1762541397744069181)
-   Added: [`Tc2_Utilities.NT_Shutdown`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35040907.html?id=8996938627204650941)
-   Added: [`Tc2_Utilities.NT_SetTimeToRTCTime`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35039371.html?id=1493501426295575313)
-   Added: [`Tc2_Utilities.NT_SetLocalTime`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35037835.html?id=9197494637274260336)
-   Added: [`Tc2_Utilities.NT_Reboot`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35036299.html?id=784025525586272890)
-   Added: [`Tc2_Utilities.NT_GetTime`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35034763.html?id=3547263991294963657)
-   Added: [`Tc2_Utilities.NT_AbortShutdown`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35033227.html?id=1054670348771327336)
-   Added: [`Tc2_Utilities.GetRemotePCInfo`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35031691.html?id=2736177499454633208)
-   Added: [`Tc2_Utilities.FB_WritePersistentData`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35030155.html?id=118377046089916014)
-   Added: [`Tc2_Utilities.FB_TzSpecificLocalTimeToSystemTime`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35028619.html?id=1839078549382949049)
-   Added: [`Tc2_Utilities.FB_SystemTimeToTzSpecificLocalTime`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35025547.html?id=9112298492461199801)
-   Added: [`Tc2_Utilities.FB_StringRingBuffer`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35024011.html?id=8307984304756907353)
-   Added: [`Tc2_Utilities.FB_SetTimeZoneInformation`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35022475.html?id=8734707644101127254)
-   Added: [`Tc2_Utilities.FB_ScopeServerControl`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35059339.html?id=146323714276683940)
-   Added: [`Tc2_Utilities.FB_RemoveRouteEntry`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35020939.html?id=6230157382149465386)
-   Added: [`Tc2_Utilities.FB_RegSetValue`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35019403.html?id=2511812654306270404)
-   Added: [`Tc2_Utilities.FB_RegQueryValue`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35017867.html?id=5234035379075813044)
-   Added: [`Tc2_Utilities.FB_MemStackBuffer`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35016331.html?id=2931491216353070439)
-   Added: [`Tc2_Utilities.FB_MemRingBufferEx`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35011723.html?id=7702053077911678829)
-   Added: [`Tc2_Utilities.FB_MemRingBuffer`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35010187.html?id=3943553403480138280)
-   Added: [`Tc2_Utilities.FB_MemBufferSplit`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35014795.html?id=845302195729933119)
-   Added: [`Tc2_Utilities.FB_MemBufferMerge`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35013259.html?id=5334119937977618983)
-   Added: [`Tc2_Utilities.FB_LocalSystemTime`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35008651.html?id=8493962399582191557)
-   Added: [`Tc2_Utilities.FB_LinkedListCtrl`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35007115.html?id=7635738877459116525)
-   Added: [`Tc2_Utilities.FB_HashTableCtrl`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35005579.html?id=6201160189975135721)
-   Added: [`Tc2_Utilities.FB_GetTimeZoneInformation`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35004043.html?id=63191963117751641)
-   Added: [`Tc2_Utilities.FB_GetSystemId`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35002507.html?id=954955109690383914)
-   Added: [`Tc2_Utilities.FB_GetRouterStatusInfo`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35000971.html?id=1502597181926739830)
-   Added: [`Tc2_Utilities.FB_GetLocalAmsNetId`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/34999435.html?id=3387145386817586554)
-   Added: [`Tc2_Utilities.FB_GetHostName`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/34997899.html?id=8819645533257292806)
-   Added: [`Tc2_Utilities.FB_GetHostAddrByName`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/34996363.html?id=831283297901541391)
-   Added: [`Tc2_Utilities.FB_GetDeviceIdentificationEx`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/34994827.html?id=1737612710838449769)
-   Added: [`Tc2_Utilities.FB_GetAdaptersInfo`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/34991755.html?id=2979034166648063123)
-   Added: [`Tc2_Utilities.FB_FormatString`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/34990219.html?id=1443593117929724847)
-   Added: [`Tc2_Utilities.FB_FileRingBuffer`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/34987147.html?id=3376994142945806623)
-   Added: [`Tc2_Utilities.FB_FileProperties`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/10047843595.html?id=5945624679416558681)
-   Added: [`Tc2_Utilities.FB_EnumStringNumbers`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/34985611.html?id=4992977576434084778)
-   Added: [`Tc2_Utilities.FB_EnumRouteEntry`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/34984075.html?id=7637337685162133919)
-   Added: [`Tc2_Utilities.FB_EnumFindFileList`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/34981003.html?id=7414402746647434562)
-   Added: [`Tc2_Utilities.FB_EnumFindFileEntry`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/34982539.html?id=5692657966202396328)
-   Added: [`Tc2_Utilities.FB_CSVMemBufferWriter`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/34979467.html?id=1113952616781398655)
-   Added: [`Tc2_Utilities.FB_CSVMemBufferReader`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/34977931.html?id=7903313200164417832)
-   Added: [`Tc2_Utilities.FB_BasicPID`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/34976395.html?id=2244329174811805838)
-   Added: [`Tc2_Utilities.FB_AmsLogger`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/34974859.html?id=485111417207987958)
-   Added: [`Tc2_Utilities.FB_AddRouteEntry`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/34973323.html?id=7125755829478175260)
-   Added: [`Tc2_Utilities.DEC_TO_BCD`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/34968715.html?id=6773913810235823934)
-   Added: [`Tc2_Utilities.DCF77_TIME_EX`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/34971787.html?id=5938573437686923495)
-   Added: [`Tc2_Utilities.DCF77_TIME`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/34970251.html?id=3591229341022860770)
-   Added: [`Tc2_Utilities.BCD_TO_DEC`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/34967179.html?id=5353025221798434097)
-   Added: [`Tc2_Utilities.FB_TzSpecificLocalTimeToFileTime`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/35027083.html?id=382128294193619295)
-   Added: [`Tc2_Utilities.FB_FileTimeToTzSpecificLocalTime`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/34988683.html?id=9070712735698353997)
-   Added: [`Tc2_Utilities.FB_GetDeviceIdentification`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_utilities/34993291.html?id=7312024828870822729)
-   Added: [`Tc2_System.Library version`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/31086731.html?id=2396685972982851303)
-   Added: [`Tc2_System.Constants`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/31084171.html?id=6993501996476522053)
-   Added: [`Tc2_System.TcEvent`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/31081227.html?id=6547697951809802698)
-   Added: [`Tc2_System.T_MaxString`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/31062795.html?id=1344144423144662247)
-   Added: [`Tc2_System.T_IPv4AddrArr`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/31067403.html?id=4141626950322792975)
-   Added: [`Tc2_System.T_IPv4Addr`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/31065867.html?id=3097782112885405293)
-   Added: [`Tc2_System.T_AmsPort`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/31064331.html?id=9222201567644391707)
-   Added: [`Tc2_System.T_AmsNetIdArr`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/31061259.html?id=5188578381467207688)
-   Added: [`Tc2_System.T_AmsNetId`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/31059723.html?id=7392932421247258531)
-   Added: [`Tc2_System.ST_AmsAddr`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/31068939.html?id=4530928490636706298)
-   Added: [`Tc2_System.E_TcEventStreamType`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/31078155.html?id=2804686591404761550)
-   Added: [`Tc2_System.E_TcEventPriority`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/31076619.html?id=6783093151605455235)
-   Added: [`Tc2_System.E_TcEventClearModes`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/31075083.html?id=6589343953937016052)
-   Added: [`Tc2_System.E_TcEventClass`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/31073547.html?id=593053326783954795)
-   Added: [`Tc2_System.E_SeekOrigin`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/31072011.html?id=6348673178966772640)
-   Added: [`Tc2_System.E_OpenPath`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/31070475.html?id=3989261379943860360)
-   Added: [`Tc2_System.E_IOAccessSize`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/31079691.html?id=3398692014117094467)
-   Added: [`Tc2_System.GETTASKTIME`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/30962443.html?id=4699733184777213219)
-   Added: [`Tc2_System.GETSYSTEMTIME`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/30960907.html?id=1079336208528573034)
-   Added: [`Tc2_System.F_GetVersionTcSystem`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/31051659.html?id=5620467006068287664)
-   Added: [`Tc2_System.MEMSET`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/31042699.html?id=278790706976054714)
-   Added: [`Tc2_System.MEMMOVE`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/31044235.html?id=1372592622524456455)
-   Added: [`Tc2_System.MEMCPY`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/31041163.html?id=1342802077509225213)
-   Added: [`Tc2_System.MEMCMP`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/31039627.html?id=70338148166301145)
-   Added: [`Tc2_System.F_IOPortWrite`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/31027595.html?id=1632460381725298073)
-   Added: [`Tc2_System.F_IOPortRead`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/31026059.html?id=3821416166087680189)
-   Added: [`Tc2_System.F_ToASC`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/31048715.html?id=2848404728059713842)
-   Added: [`Tc2_System.F_ToCHR`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/31047179.html?id=7941927800504137344)
-   Added: [`Tc2_System.F_ScanAmsNetIds`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/31036683.html?id=7973316741305006172)
-   Added: [`Tc2_System.F_CreateAmsNetId`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/31035147.html?id=5959351732453319241)
-   Added: [`Tc2_System.ADSLOGSTR`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/31033611.html?id=9189897725322916238)
-   Added: [`Tc2_System.ADSLOGLREAL`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/31032075.html?id=4483740810094395756)
-   Added: [`Tc2_System.ADSLOGDINT`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/31030539.html?id=6955783330714401435)
-   Added: [`Tc2_System.TestAndSet`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/31023115.html?id=3648203211166238553)
-   Added: [`Tc2_System.LPTSIGNAL`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/31020043.html?id=648815986689813014)
-   Added: [`Tc2_System.GETCURTASKINDEXEX`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/31018507.html?id=103554021675037415)
-   Added: [`Tc2_System.CLEARBIT32`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/31016971.html?id=4991390180253774446)
-   Added: [`Tc2_System.GETBIT32`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/31015435.html?id=1585281004611539670)
-   Added: [`Tc2_System.CSETBIT32`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/31013899.html?id=5425451146231741595)
-   Added: [`Tc2_System.SETBIT32`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/31012363.html?id=490301268723897032)
-   Added: [`Tc2_System.F_SplitPathName`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/31007755.html?id=4427337671596610969)
-   Added: [`Tc2_System.F_ScanIPv4AddrIds`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/31010827.html?id=8900454348874325558)
-   Added: [`Tc2_System.F_CreateIPv4Addr`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/31009291.html?id=7184938184414641376)
-   Added: [`Tc2_System.F_CmpLibVersion`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/31006219.html?id=2441219256652772049)
-   Added: [`Tc2_System.GETCPUCOUNTER`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/30963979.html?id=7780791847081551873)
-   Added: [`Tc2_System.GETCPUACCOUNT`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/30965515.html?id=7376378058605908954)
-   Added: [`Tc2_System.FB_PcWatchDog_BAPI`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/2220165643.html?id=1576087786783718110)
-   Added: [`Tc2_System.FB_PcWatchdog`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/30968459.html?id=8419827613069214007)
-   Added: [`Tc2_System.SFCActionControl`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/30992779.html?id=2568808911502678947)
-   Added: [`Tc2_System.AppendErrorString`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/30997387.html?id=8243287517307048547)
-   Added: [`Tc2_System.AnalyzeExpressionCombined`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/30995851.html?id=2899976169773424660)
-   Added: [`Tc2_System.AnalyzeExpressionTable`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/2239489675.html?id=2743244861986277983)
-   Added: [`Tc2_System.AnalyzeExpression`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/30994315.html?id=604524845774221209)
-   Added: [`Tc2_System.FB_SimpleAdsLogEvent`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/796919691.html?id=7572293929576704962)
-   Added: [`Tc2_System.ADSCLEAREVENTS`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/31001867.html?id=8448183770513650707)
-   Added: [`Tc2_System.ADSLOGEVENT`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/31000331.html?id=7131473434119365719)
-   Added: [`Tc2_System.FB_RemoveDir`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/30989835.html?id=1997100600453107497)
-   Added: [`Tc2_System.FB_CreateDir`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/30988299.html?id=2667162487971609572)
-   Added: [`Tc2_System.FB_FileRename`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/30982155.html?id=1824555993381398073)
-   Added: [`Tc2_System.FB_FileDelete`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/30974475.html?id=394326815599778743)
-   Added: [`Tc2_System.FB_FileTell`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/30985227.html?id=5593924331837202314)
-   Added: [`Tc2_System.FB_FileSeek`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/30983691.html?id=8233380726918996109)
-   Added: [`Tc2_System.FB_FileWrite`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/30986763.html?id=8084078722597421664)
-   Added: [`Tc2_System.FB_FileRead`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/30980619.html?id=5534719005648537303)
-   Added: [`Tc2_System.FB_FilePuts`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/30979083.html?id=4443798793635907668)
-   Added: [`Tc2_System.FB_FileGets`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/30976011.html?id=7142624840958888920)
-   Added: [`Tc2_System.FB_FileClose`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/30972939.html?id=1997985466515001449)
-   Added: [`Tc2_System.FB_FileOpen`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/30977547.html?id=4702287923023522286)
-   Added: [`Tc2_System.FB_EOF`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/30971403.html?id=1624015476829386435)
-   Added: [`Tc2_System.ADSRDWRTRES`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/30953483.html?id=8987476070419037549)
-   Added: [`Tc2_System.ADSWRITERES`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/30951947.html?id=3524663419407027687)
-   Added: [`Tc2_System.ADSREADRES`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/30950411.html?id=1662378633002109269)
-   Added: [`Tc2_System.ADSRDWRTIND`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/30948875.html?id=1093743819590217906)
-   Added: [`Tc2_System.ADSWRITEIND`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/30947339.html?id=8017999144374321246)
-   Added: [`Tc2_System.ADSREADIND`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/30945803.html?id=1555569090574268850)
-   Added: [`Tc2_System.ADSRDDEVINFO`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/30938251.html?id=2415220487216832998)
-   Added: [`Tc2_System.ADSWRTCTL`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/30936715.html?id=4259785717366623640)
-   Added: [`Tc2_System.ADSRDSTATE`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/30935179.html?id=7246198192778696045)
-   Added: [`Tc2_System.ADSRDWRTEX`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/30941323.html?id=1144527587528753085)
-   Added: [`Tc2_System.ADSRDWRT`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/30869643.html?id=2320621842203604685)
-   Added: [`Tc2_System.ADSWRITE`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/30868107.html?id=1102723425013969593)
-   Added: [`Tc2_System.ADSREADEX`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/30939787.html?id=3519928155200352058)
-   Added: [`Tc2_System.ADSREAD`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/30866571.html?id=5907741325719745777)
-   Added: [`Tc2_System.GETCURTASKINDEX`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/30957963.html?id=2338887505708092959)
-   Added: [`Tc2_System.FB_SetLedColor_BAPI`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/4566933899.html?id=2684610655829531814)
-   Added: [`Tc2_System.DRAND`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_system/30956427.html?id=6634697633993752644)
-   Added: [`Tc2_SystemCX.ST_CX_ProfilerStruct`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_systemcx/185900555.html?id=1868222789980298300)
-   Added: [`Tc2_SystemCX.ST_CxDeviceIdentificationEx`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_systemcx/2249667979.html?id=735120032932118460)
-   Added: [`Tc2_SystemCX.ST_CX_DeviceIdentification`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_systemcx/185899019.html?id=4180452786057755424)
-   Added: [`Tc2_SystemCX.F_CXNaviSwitch`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_systemcx/185876235.html?id=2032497683823283392)
-   Added: [`Tc2_SystemCX.F_CX9010SetWatchdog`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_systemcx/185880843.html?id=5986098621786910454)
-   Added: [`Tc2_SystemCX.F_CX9000SetWatchdog`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_systemcx/185879307.html?id=4617716829128300095)
-   Added: [`Tc2_SystemCX.F_CX1000SetWatchdog`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_systemcx/185877771.html?id=80937226136231613)
-   Added: [`Tc2_SystemCX.FB_CX5020SetWatchdog`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_systemcx/185871755.html?id=5810814013769200589)
-   Added: [`Tc2_SystemCX.FB_CX5010SetWatchdog`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_systemcx/185870219.html?id=4073891947374647716)
-   Added: [`Tc2_SystemCX.FB_CXSimpleUps`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_systemcx/185864075.html?id=5739214096196204070)
-   Added: [`Tc2_SystemCX.FB_CXSetTextDisplay`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_systemcx/185862539.html?id=4607036684138679546)
-   Added: [`Tc2_SystemCX.FB_CX1030SetWatchdog`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_systemcx/185868683.html?id=8000171912883525586)
-   Added: [`Tc2_SystemCX.FB_CX1020SetWatchdog`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_systemcx/185867147.html?id=6341632827419752566)
-   Added: [`Tc2_SystemCX.FB_CX1010SetWatchdog`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_systemcx/185865611.html?id=3406331232880036198)
-   Added: [`Tc2_MDP.E_MDP_ErrCodesPLC`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_mdp/178771467.html?id=5872575796676486967)
-   Added: [`Tc2_MDP.E_MDP_ErrGroup`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_mdp/178769931.html?id=4136406291899253404)
-   Added: [`Tc2_MDP.Error codes overview`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_mdp/178768395.html?id=8794289068898136294)
-   Added: [`Tc2_MDP.FB_MDP_TwinCAT_Read`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_mdp/178741515.html?id=6776118503127890531)
-   Added: [`Tc2_MDP.FB_MDP_SW_Read_MdpVersion`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_mdp/178739979.html?id=3462053663858802373)
-   Added: [`Tc2_MDP.FB_MDP_SiliconDrive_Read`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_mdp/178738443.html?id=2282913957387672090)
-   Added: [`Tc2_MDP.FB_MDP_NIC_Write_IP`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_mdp/178736907.html?id=6666189413915906046)
-   Added: [`Tc2_MDP.FB_MDP_NIC_Read`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_mdp/178735371.html?id=5214272168102069525)
-   Added: [`Tc2_MDP.FB_MDP_IdentityObj_Read`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_mdp/178733835.html?id=2084722919633899496)
-   Added: [`Tc2_MDP.FB_MDP_Device_Read_DevName`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_mdp/178732299.html?id=4870951697139025874)
-   Added: [`Tc2_MDP.FB_MDP_CPU_Read`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_mdp/178730763.html?id=8494033132200132525)
-   Added: [`Tc2_MDP.FB_MDP_SplitErrorId`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_mdp/178727819.html?id=8412158913111401377)
-   Added: [`Tc2_MDP.FB_MDP_ScanModules`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_mdp/178726283.html?id=8403569140323933670)
-   Added: [`Tc2_MDP.FB_MDP_ReadModuleHeader`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_mdp/178724747.html?id=2508196882866854022)
-   Added: [`Tc2_MDP.FB_MDP_ReadModuleContent`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_mdp/178723211.html?id=2912052482688124251)
-   Added: [`Tc2_MDP.FB_MDP_ReadModule`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_mdp/178721675.html?id=5642233096393218184)
-   Added: [`Tc2_MDP.FB_MDP_ReadElement`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_mdp/178720139.html?id=816573703253488814)
-   Added: [`Tc2_MDP.FB_MDP_Write`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_mdp/178717067.html?id=7140987820192724576)
-   Added: [`Tc2_MDP.FB_MDP_Read`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_mdp/178715531.html?id=5176561919886359433)
-   Added: [`Tc2_IoFunctions.SERCOS file format of the backup file`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59223563.html?id=7881709655085813337)
-   Added: [`Tc2_IoFunctions.Library version`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59267851.html?id=5027465776941942787)
-   Added: [`Tc2_IoFunctions.ST_UPSStatus`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59234315.html?id=870383754195989439)
-   Added: [`Tc2_IoFunctions.ST_SercosParamList`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/946213387.html?id=2419765479221471814)
-   Added: [`Tc2_IoFunctions.ST_SercosParamErrList`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/946215307.html?id=3945237066667379153)
-   Added: [`Tc2_IoFunctions.ST_SercosParamAttrib`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59222027.html?id=62973187889961539)
-   Added: [`Tc2_IoFunctions.ST_RAIDStatusRes`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59264907.html?id=4828356599321970609)
-   Added: [`Tc2_IoFunctions.ST_RAIDInfo`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59263371.html?id=3063638603320001175)
-   Added: [`Tc2_IoFunctions.ST_RAIDDriveStatus`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59260299.html?id=287806057109277053)
-   Added: [`Tc2_IoFunctions.ST_RAIDConfigReq`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59261835.html?id=5304527974377061966)
-   Added: [`Tc2_IoFunctions.ST_RAIDCntlrFound`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59258763.html?id=1461769706683130369)
-   Added: [`Tc2_IoFunctions.ST_PZD_OUT`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59226635.html?id=1582380644903534074)
-   Added: [`Tc2_IoFunctions.ST_PZD_IN`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59225099.html?id=2814465822899810801)
-   Added: [`Tc2_IoFunctions.ST_PNIOState`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59249675.html?id=4690742264028495233)
-   Added: [`Tc2_IoFunctions.ST_PNIORecord`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59248139.html?id=2032359713457749208)
-   Added: [`Tc2_IoFunctions.ST_PNIOConfigRecord`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59246603.html?id=1368309014301434964)
-   Added: [`Tc2_IoFunctions.ST_PNET_CCDSTS`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59245067.html?id=2042721072412638003)
-   Added: [`Tc2_IoFunctions.ST_PD_Dpv1Error`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/948623499.html?id=4895269030695816442)
-   Added: [`Tc2_IoFunctions.ST_ParameterBuffer`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59231243.html?id=2373889777582414326)
-   Added: [`Tc2_IoFunctions.ST_Parameter_OUT`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59229707.html?id=7889226202681910915)
-   Added: [`Tc2_IoFunctions.ST_Parameter_IN`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59228171.html?id=5970707795906570902)
-   Added: [`Tc2_IoFunctions.ST_NovRamAddrInfoEx`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/2287971467.html?id=6040943648800917410)
-   Added: [`Tc2_IoFunctions.ST_NovRamAddrInfo`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59232779.html?id=1439718635487507872)
-   Added: [`Tc2_IoFunctions.ST_Dpv1ValueHeaderEx`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59243531.html?id=2880011653958721786)
-   Added: [`Tc2_IoFunctions.ST_Dpv1ParamAddrEx`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59241995.html?id=2619344632373877580)
-   Added: [`Tc2_IoFunctions.ST_AdsTecSysData`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59240459.html?id=3753880638908036866)
-   Added: [`Tc2_IoFunctions.IODEVICETYPES`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59217419.html?id=3130045667377127736)
-   Added: [`Tc2_IoFunctions.E_UpsPowerStatus`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59238923.html?id=6447189444360631604)
-   Added: [`Tc2_IoFunctions.E_UpsCommStatus`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59237387.html?id=1839508648446640754)
-   Added: [`Tc2_IoFunctions.E_SercosAttribType`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59220491.html?id=8399303561475175063)
-   Added: [`Tc2_IoFunctions.E_SercosAttribLen`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59218955.html?id=8899253857261165094)
-   Added: [`Tc2_IoFunctions.E_RAIDType`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59257227.html?id=5929644966959521130)
-   Added: [`Tc2_IoFunctions.E_RAIDStatus`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59255691.html?id=7582353235660364320)
-   Added: [`Tc2_IoFunctions.E_RAIDDriveUsage`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59254155.html?id=5363159254110837283)
-   Added: [`Tc2_IoFunctions.E_RAIDDriveStatus`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59252619.html?id=5545201599467774222)
-   Added: [`Tc2_IoFunctions.E_PD_Datatype`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/948619403.html?id=7187300193779562696)
-   Added: [`Tc2_IoFunctions.E_BatteryStatus`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59235851.html?id=4552902538332092730)
-   Added: [`Tc2_IoFunctions.E_PD_Dpv1Error`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/948627211.html?id=9030002404499077046)
-   Added: [`Tc2_IoFunctions.F_GetVersionRAIDController`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/948887051.html?id=3996421168911916077)
-   Added: [`Tc2_IoFunctions.F_GetVersionTcIoFunctions`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59214475.html?id=1791191340358649745)
-   Added: [`Tc2_IoFunctions.FB_ReadAdsTecSysData`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59205515.html?id=8727616615610988943)
-   Added: [`Tc2_IoFunctions.SCIT_ConfDevErrAll`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59202571.html?id=6580818816616319111)
-   Added: [`Tc2_IoFunctions.SCIT_GetErrorInfo`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59201035.html?id=1594758226643042767)
-   Added: [`Tc2_IoFunctions.SCIT_ControlActiveConfiguration`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59199499.html?id=7978707931512437356)
-   Added: [`Tc2_IoFunctions.SCIT_AlarmStop`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59197963.html?id=686829769877017348)
-   Added: [`Tc2_IoFunctions.SCIT_StopDataTransfer`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59196427.html?id=7143948184405577317)
-   Added: [`Tc2_IoFunctions.SCIT_StartDataTransfer`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59194891.html?id=7699653258878134510)
-   Added: [`Tc2_IoFunctions.SCIT_DeactivateConfiguration`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59193355.html?id=513281230869234019)
-   Added: [`Tc2_IoFunctions.SCIT_ActivateConfiguration`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59191819.html?id=5099464308041835986)
-   Added: [`Tc2_IoFunctions.IOF_SER_DRIVE_Reset`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59128459.html?id=5917705844304551181)
-   Added: [`Tc2_IoFunctions.IOF_SER_DRIVE_BackupEx`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59126923.html?id=4149809723631767962)
-   Added: [`Tc2_IoFunctions.IOF_SER_DRIVE_Backup`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59125387.html?id=960775827665682468)
-   Added: [`Tc2_IoFunctions.IOF_SER_IDN_Write`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59123851.html?id=5978032092053655978)
-   Added: [`Tc2_IoFunctions.IOF_SER_IDN_Read`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59122315.html?id=1410064853445610597)
-   Added: [`Tc2_IoFunctions.IOF_SER_SetPhase`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59120779.html?id=3880962790324375720)
-   Added: [`Tc2_IoFunctions.IOF_SER_ResetErr`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59119243.html?id=5721439343407240881)
-   Added: [`Tc2_IoFunctions.IOF_SER_SaveFlash`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59117707.html?id=8431677713582289247)
-   Added: [`Tc2_IoFunctions.IOF_SER_GetPhase`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59116171.html?id=7269842912942227518)
-   Added: [`Tc2_IoFunctions.FB_RAIDGetStatus`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59211531.html?id=360472774925485745)
-   Added: [`Tc2_IoFunctions.FB_RAIDGetInfo`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59209995.html?id=4673101986256208550)
-   Added: [`Tc2_IoFunctions.FB_RAIDFindCntlr`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59208459.html?id=8960827325378050044)
-   Added: [`Tc2_IoFunctions.FB_Dpv1WritePNET`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59180043.html?id=9029653716188629991)
-   Added: [`Tc2_IoFunctions.FB_Dpv1ReadPNET`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59175435.html?id=6443262543048649037)
-   Added: [`Tc2_IoFunctions.F_SplitDpv1WriteResPkgPNET`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59181579.html?id=7849786899723563906)
-   Added: [`Tc2_IoFunctions.F_SplitDpv1ReadResPkgPNET`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59176971.html?id=1823512990255567560)
-   Added: [`Tc2_IoFunctions.F_CreateDpv1WriteReqPkgPNET`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59178507.html?id=3153123037376224447)
-   Added: [`Tc2_IoFunctions.F_CreateDpv1ReadReqPkgPNET`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59173899.html?id=6324774269007287723)
-   Added: [`Tc2_IoFunctions.FB_Dpv1Write`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59169419.html?id=8567708141464396544)
-   Added: [`Tc2_IoFunctions.FB_Dpv1Read`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59164811.html?id=8932410784160242931)
-   Added: [`Tc2_IoFunctions.F_SplitDpv1WriteResPkg`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59170955.html?id=8983298599066999041)
-   Added: [`Tc2_IoFunctions.F_SplitDpv1ReadResPkg`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59166347.html?id=3837833131807616227)
-   Added: [`Tc2_IoFunctions.F_CreateDpv1WriteReqPkg`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59167883.html?id=2523961850755291579)
-   Added: [`Tc2_IoFunctions.F_CreateDpv1ReadReqPkg`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59163275.html?id=4125791007446191787)
-   Added: [`Tc2_IoFunctions.FB_GetDPRAMInfoEx`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/2217659019.html?id=5695739639898429746)
-   Added: [`Tc2_IoFunctions.FB_GetDPRAMInfo`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59134475.html?id=1957996852211801615)
-   Added: [`Tc2_IoFunctions.FB_NovRamReadWriteEx`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59132939.html?id=8007342586059935937)
-   Added: [`Tc2_IoFunctions.FB_NovRamReadWrite`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59131403.html?id=8526951604785748661)
-   Added: [`Tc2_IoFunctions.IOF_CAN_Layer2Command`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59113227.html?id=9155952391546318983)
-   Added: [`Tc2_IoFunctions.FB_GetUPSStatus`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59184523.html?id=2474773387187865285)
-   Added: [`Tc2_IoFunctions.IOF_LB_ParityCheckWithReset`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59110283.html?id=5041199112424734391)
-   Added: [`Tc2_IoFunctions.IOF_LB_ParityCheck`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59108747.html?id=919476178648687721)
-   Added: [`Tc2_IoFunctions.IOF_LB_BreakLocationTest`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59107211.html?id=3118305393459870243)
-   Added: [`Tc2_IoFunctions.FB_AX200X_Profibus`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59145099.html?id=505876296565547244)
-   Added: [`Tc2_IoFunctions.FB_AX2000_Reference`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59143563.html?id=7766553372508736249)
-   Added: [`Tc2_IoFunctions.FB_AX2000_Parameter`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59142027.html?id=7699892407294224474)
-   Added: [`Tc2_IoFunctions.FB_AX2000_JogMode`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59140491.html?id=2141305664277120889)
-   Added: [`Tc2_IoFunctions.FB_AX2000_AXACT`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59138955.html?id=4688995745176664691)
-   Added: [`Tc2_IoFunctions.FB_WriteOutput_analog`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59160331.html?id=1727064209817024549)
-   Added: [`Tc2_IoFunctions.FB_ReadInput_analog`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59158795.html?id=4770391306075797703)
-   Added: [`Tc2_IoFunctions.FB_ASI_ParameterControl`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59157259.html?id=7734938861700618778)
-   Added: [`Tc2_IoFunctions.FB_ASI_Processdata_digital`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59155723.html?id=156844443513837796)
-   Added: [`Tc2_IoFunctions.FB_ASI_WriteParameter`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59154187.html?id=7515898917881730808)
-   Added: [`Tc2_IoFunctions.FB_ASI_ReadParameter`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59152651.html?id=7649232421468164076)
-   Added: [`Tc2_IoFunctions.FB_ASI_SlaveDiag`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59151115.html?id=4428764155696083088)
-   Added: [`Tc2_IoFunctions.FB_ASI_Addressing`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59149579.html?id=5485085193189280367)
-   Added: [`Tc2_IoFunctions.IOF_GetDeviceType`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59102731.html?id=3023660364922819255)
-   Added: [`Tc2_IoFunctions.IOF_GetDeviceNetId`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59101195.html?id=8873375447854419927)
-   Added: [`Tc2_IoFunctions.IOF_GetDeviceName`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59099659.html?id=751605432359830339)
-   Added: [`Tc2_IoFunctions.IOF_GetDeviceInfoByName`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59104267.html?id=6394173433374038995)
-   Added: [`Tc2_IoFunctions.IOF_GetDeviceIDs`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59098123.html?id=9007140653734747476)
-   Added: [`Tc2_IoFunctions.IOF_GetDeviceIDByName`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59096587.html?id=2324380000819895794)
-   Added: [`Tc2_IoFunctions.IOF_GetDeviceCount`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59095051.html?id=1930247938383289337)
-   Added: [`Tc2_IoFunctions.IOF_GetBoxNetId`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59093515.html?id=806259507513004115)
-   Added: [`Tc2_IoFunctions.IOF_GetBoxNameByAddr`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59091979.html?id=4238707285426453434)
-   Added: [`Tc2_IoFunctions.IOF_GetBoxCount`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59090443.html?id=7322803856934463258)
-   Added: [`Tc2_IoFunctions.IOF_GetBoxAddrByNameEx`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59088907.html?id=1585265463288465135)
-   Added: [`Tc2_IoFunctions.IOF_GetBoxAddrByName`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59087371.html?id=1697320149449402419)
-   Added: [`Tc2_IoFunctions.IOF_DeviceReset`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_iofunctions/59085835.html?id=1048048840999409173)
-   Added: [`Tc2_EtherCAT.EtherCAT mailbox protocol error codes`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/57141771.html?id=6579623810862286620)
-   Added: [`Tc2_EtherCAT.Global constants`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/57137675.html?id=1723237164594483054)
-   Added: [`Tc2_EtherCAT.T_HFoe`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/57131659.html?id=1136012839415289864)
-   Added: [`Tc2_EtherCAT.T_DCTIME`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/57133195.html?id=7756496070795220426)
-   Added: [`Tc2_EtherCAT.T_DCTIME64`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/2267609355.html?id=6012195953297160703)
-   Added: [`Tc2_EtherCAT.T_DCTIME32`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/57134731.html?id=3467113964669420223)
-   Added: [`Tc2_EtherCAT.DCTIMESTRUCT`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/57102475.html?id=4368620692019970874)
-   Added: [`Tc2_EtherCAT.ST_TopologyDataEx`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/2297198091.html?id=6821385266954877597)
-   Added: [`Tc2_EtherCAT.ST_EcSlaveStateBitsEx`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/3259666315.html?id=2776523129212393887)
-   Added: [`Tc2_EtherCAT.ST_EcSlaveStateBits`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/57123979.html?id=1956092918048442292)
-   Added: [`Tc2_EtherCAT.ST_EcSlaveState`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/57122443.html?id=7416832768208506712)
-   Added: [`Tc2_EtherCAT.ST_EcSlaveScannedData`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/57120907.html?id=8394230170631205264)
-   Added: [`Tc2_EtherCAT.ST_EcSlaveIdentity`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/57119371.html?id=5756703890210533212)
-   Added: [`Tc2_EtherCAT.ST_EcSlaveConfigData`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/57117835.html?id=1698785118554055179)
-   Added: [`Tc2_EtherCAT.ST_EcMasterStatistic`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/57116299.html?id=3140601435908172227)
-   Added: [`Tc2_EtherCAT.ST_EcLastProtErrInfo`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/57114763.html?id=2840699895414934391)
-   Added: [`Tc2_EtherCAT.ST_EcCrcErrorEx`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/57113227.html?id=7899325562203274922)
-   Added: [`Tc2_EtherCAT.ST_EcCrcError`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/57111691.html?id=7471467744475852463)
-   Added: [`Tc2_EtherCAT.E_EcMbxProtType`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/57107083.html?id=3534847361935330002)
-   Added: [`Tc2_EtherCAT.E_EcFoeMode`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/57105547.html?id=6582050644970401137)
-   Added: [`Tc2_EtherCAT.E_EcAdressingType`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/57104011.html?id=5111214795420028775)
-   Added: [`Tc2_EtherCAT.F_GetVersionTcEtherCAT`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/57099531.html?id=5280271314081445036)
-   Added: [`Tc2_EtherCAT.FILETIME_TO_DCTIME64`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/2267414027.html?id=3087103749918293304)
-   Added: [`Tc2_EtherCAT.DCTIME64_TO_FILETIME`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/2267404427.html?id=3492355111957719602)
-   Added: [`Tc2_EtherCAT.FB_EcExtSyncCheck`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/2285537547.html?id=58768279346914815)
-   Added: [`Tc2_EtherCAT.FB_EcExtSyncCalcTimeDiff`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/2285535627.html?id=5832651186995919455)
-   Added: [`Tc2_EtherCAT.F_GetCurExtTime`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/2285085707.html?id=3517100904415010297)
-   Added: [`Tc2_EtherCAT.F_GetCurDcTickTime`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/57085835.html?id=5702078204221586223)
-   Added: [`Tc2_EtherCAT.F_GetCurDcTaskTime`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/57087371.html?id=7927893291510268558)
-   Added: [`Tc2_EtherCAT.F_GetActualDcTime`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/57088907.html?id=949860617194207381)
-   Added: [`Tc2_EtherCAT.F_ConvTcTimeToExtTime`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/2285529867.html?id=8190559637627950982)
-   Added: [`Tc2_EtherCAT.F_ConvTcTimeToDcTime`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/2285531787.html?id=1938278822835741728)
-   Added: [`Tc2_EtherCAT.F_ConvExtTimeToDcTime`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/2285533707.html?id=4356151041091973315)
-   Added: [`Tc2_EtherCAT.FB_EcDcTimeCtrl`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/57082891.html?id=1462580992001182954)
-   Added: [`Tc2_EtherCAT.SYSTEMTIME_TO_DCTIME`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/57070603.html?id=3420244455302723538)
-   Added: [`Tc2_EtherCAT.STRING_TO_DCTIME`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/57067531.html?id=7936121479178409083)
-   Added: [`Tc2_EtherCAT.FILETIME_TO_DCTIME`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/57069067.html?id=5828648914341934300)
-   Added: [`Tc2_EtherCAT.DCTIMESTRUCT_TO_DCTIME`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/57072139.html?id=1430678193512985748)
-   Added: [`Tc2_EtherCAT.DCTIME_TO_SYSTEMTIME`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/57064459.html?id=7493090668942512996)
-   Added: [`Tc2_EtherCAT.DCTIME_TO_STRING`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/57061387.html?id=9080258636454418029)
-   Added: [`Tc2_EtherCAT.DCTIME_TO_FILETIME`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/57062923.html?id=2410424058227796245)
-   Added: [`Tc2_EtherCAT.DCTIME_TO_DCTIMESTRUCT`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/57065995.html?id=1591168658226354774)
-   Added: [`Tc2_EtherCAT.FB_EcExtSyncCheck64`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/2285554187.html?id=1801420710402675526)
-   Added: [`Tc2_EtherCAT.FB_EcExtSyncCalcTimeDiff64`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/2285552267.html?id=5145810983043386042)
-   Added: [`Tc2_EtherCAT.F_GetCurExtTime64`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/2285087627.html?id=4303037545037571004)
-   Added: [`Tc2_EtherCAT.F_GetCurDcTickTime64`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/2267607435.html?id=3927880765762026379)
-   Added: [`Tc2_EtherCAT.F_GetCurDcTaskTime64`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/2268414091.html?id=9011615869011302582)
-   Added: [`Tc2_EtherCAT.F_GetActualDcTime64`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/2268416395.html?id=1556300426252137789)
-   Added: [`Tc2_EtherCAT.F_ConvTcTimeToExtTime64`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/2285559947.html?id=3317133272470539914)
-   Added: [`Tc2_EtherCAT.F_ConvTcTimeToDcTime64`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/2285558027.html?id=8370964029261550056)
-   Added: [`Tc2_EtherCAT.F_ConvExtTimeToDcTime64`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/2285556107.html?id=3688701711524934354)
-   Added: [`Tc2_EtherCAT.FB_EcDcTimeCtrl64`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/2267412107.html?id=5733187670824448722)
-   Added: [`Tc2_EtherCAT.SYSTEMTIME_TO_DCTIME64`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/2267418251.html?id=5289681717911221099)
-   Added: [`Tc2_EtherCAT.STRING_TO_DCTIME64`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/2267415947.html?id=6989402477759435732)
-   Added: [`Tc2_EtherCAT.DCTIMESTRUCT_TO_DCTIME64`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/2267410187.html?id=3126004403004622252)
-   Added: [`Tc2_EtherCAT.DCTIME64_TO_SYSTEMTIME`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/2267881483.html?id=4675186351884583017)
-   Added: [`Tc2_EtherCAT.DCTIME64_TO_STRING`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/2267406347.html?id=6169424304031718909)
-   Added: [`Tc2_EtherCAT.DCTIME64_TO_DCTIMESTRUCT`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/2267402507.html?id=6917478134950798301)
-   Added: [`Tc2_EtherCAT.DCTIME64_TO_DCTIME`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/2267336587.html?id=1810877026239338007)
-   Added: [`Tc2_EtherCAT.DCTIME_TO_DCTIME64`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/2267334667.html?id=9157610278007611580)
-   Added: [`Tc2_EtherCAT.ConvertPathPosToDcTime`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/57095051.html?id=279959967329247990)
-   Added: [`Tc2_EtherCAT.ConvertDcTimeToPathPos`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/57093515.html?id=282136983773191282)
-   Added: [`Tc2_EtherCAT.ConvertPosToDcTime`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/57091979.html?id=4184044799586807286)
-   Added: [`Tc2_EtherCAT.ConvertDcTimeToPos`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/57090443.html?id=4906745277743881395)
-   Added: [`Tc2_EtherCAT.F_ConvStateToString`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/57081355.html?id=3327883492774925381)
-   Added: [`Tc2_EtherCAT.F_ConvSlaveStateToBitsEx`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/3259681163.html?id=822057614787939366)
-   Added: [`Tc2_EtherCAT.F_ConvSlaveStateToBits`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/57079819.html?id=1631013332318388299)
-   Added: [`Tc2_EtherCAT.F_ConvSlaveStateToString`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/57078283.html?id=8514505304181890456)
-   Added: [`Tc2_EtherCAT.F_ConvProductCodeToString`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/57076747.html?id=2912497619857050242)
-   Added: [`Tc2_EtherCAT.F_ConvMasterDevStateToString`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/57075211.html?id=6646364599408186539)
-   Added: [`Tc2_EtherCAT.F_ConvBK1120CouplerStateToString`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/57073675.html?id=4301816588433478952)
-   Added: [`Tc2_EtherCAT.FB_SoEWrite_ByDriveRef`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/57049355.html?id=163326623524607501)
-   Added: [`Tc2_EtherCAT.FB_SoERead_ByDriveRef`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/57050891.html?id=3356548166570152861)
-   Added: [`Tc2_EtherCAT.FB_EcSoeWrite`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/57047819.html?id=1219153289241228603)
-   Added: [`Tc2_EtherCAT.FB_EcSoeRead`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/57046283.html?id=305129201947289187)
-   Added: [`Tc2_EtherCAT.FB_EcFoeReadFile`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/9859439755.html?id=3183368327319748339)
-   Added: [`Tc2_EtherCAT.FB_EcFoeOpen`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/57043339.html?id=3897756563783863650)
-   Added: [`Tc2_EtherCAT.FB_EcFoeLoad`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/57041803.html?id=5704611576063541907)
-   Added: [`Tc2_EtherCAT.FB_EcFoeClose`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/57040267.html?id=2518955579643902327)
-   Added: [`Tc2_EtherCAT.FB_EcFoeAccess`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/57038731.html?id=4234199304255238483)
-   Added: [`Tc2_EtherCAT.FB_CoEWrite_ByDriveRef`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/2217657099.html?id=2701325325255340500)
-   Added: [`Tc2_EtherCAT.FB_CoERead_ByDriveRef`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/2217655179.html?id=3684734861924142283)
-   Added: [`Tc2_EtherCAT.FB_EcCoeSdoWriteEx`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/57000843.html?id=587967191719163978)
-   Added: [`Tc2_EtherCAT.FB_EcCoeSdoWrite`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/56999307.html?id=6760296804767806782)
-   Added: [`Tc2_EtherCAT.FB_EcCoeSdoReadEx`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/56997771.html?id=365735131548854682)
-   Added: [`Tc2_EtherCAT.FB_EcCoeSdoRead`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/56996235.html?id=8819525962871771824)
-   Added: [`Tc2_EtherCAT.FB_EcSetSlaveState`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/57034251.html?id=6529596141134489199)
-   Added: [`Tc2_EtherCAT.FB_EcSetMasterState`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/57035787.html?id=852323042170652234)
-   Added: [`Tc2_EtherCAT.FB_EcReqSlaveState`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/57031179.html?id=1247126537675471030)
-   Added: [`Tc2_EtherCAT.FB_EcReqMasterState`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/57032715.html?id=7355631526548495622)
-   Added: [`Tc2_EtherCAT.FB_EcGetSlaveState`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/57028107.html?id=1869078629752574323)
-   Added: [`Tc2_EtherCAT.FB_EcGetMasterState`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/57026571.html?id=5049806479451228695)
-   Added: [`Tc2_EtherCAT.FB_EcGetAllSlaveStates`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/57029643.html?id=7320897480379524041)
-   Added: [`Tc2_EtherCAT.F_CheckVendorId`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/57096587.html?id=3588392878918819808)
-   Added: [`Tc2_EtherCAT.FB_EcMasterFrameStatisticClearTxRxErr`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/57058443.html?id=1831667648277843322)
-   Added: [`Tc2_EtherCAT.FB_EcMasterFrameStatisticClearFrames`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/57056907.html?id=9131220030086955746)
-   Added: [`Tc2_EtherCAT.FB_EcMasterFrameStatisticClearCRC`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/57055371.html?id=4156187223259443239)
-   Added: [`Tc2_EtherCAT.FB_EcMasterFrameStatistic`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/57053835.html?id=2955422267384002664)
-   Added: [`Tc2_EtherCAT.FB_EcMasterFrameCount`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/2895330059.html?id=2695367209384614789)
-   Added: [`Tc2_EtherCAT.FB_EcGetSlaveTopologyInfo`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/2239485707.html?id=8606406373960132122)
-   Added: [`Tc2_EtherCAT.FB_EcGetSlaveIdentity`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/57017483.html?id=4881401981915843587)
-   Added: [`Tc2_EtherCAT.FB_EcGetSlaveCrcErrorEx`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/2239483787.html?id=510883678732926140)
-   Added: [`Tc2_EtherCAT.FB_EcGetSlaveCrcError`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/57014411.html?id=2547537279829557146)
-   Added: [`Tc2_EtherCAT.FB_EcGetSlaveCount`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/57015947.html?id=7631966020193195027)
-   Added: [`Tc2_EtherCAT.FB_EcGetScannedSlaves`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/57020555.html?id=6574827625768498981)
-   Added: [`Tc2_EtherCAT.FB_EcGetMasterDevState`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/2895328139.html?id=7792674512447829325)
-   Added: [`Tc2_EtherCAT.FB_EcGetLastProtErrInfo`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/57023627.html?id=575185642061626850)
-   Added: [`Tc2_EtherCAT.FB_EcGetConfSlaves`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/57019019.html?id=1545842977842173400)
-   Added: [`Tc2_EtherCAT.FB_EcGetAllSlavePresentStateChanges`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/2239481867.html?id=3066401104283976152)
-   Added: [`Tc2_EtherCAT.FB_EcGetAllCrcErrors`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/57012875.html?id=1927548479392246412)
-   Added: [`Tc2_EtherCAT.FB_EcGetAllSlaveAddr`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/57011339.html?id=8927310348121390302)
-   Added: [`Tc2_EtherCAT.FB_EcGetAllSlaveAbnormalStateChanges`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/2239479947.html?id=1761312682463201731)
-   Added: [`Tc2_EtherCAT.FB_EcLogicalWriteCmd`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/57008395.html?id=2872634582182116261)
-   Added: [`Tc2_EtherCAT.FB_EcLogicalReadCmd`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/57006859.html?id=8971386316833211807)
-   Added: [`Tc2_EtherCAT.FB_EcPhysicalWriteCmd`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/57005323.html?id=4795046190451459415)
-   Added: [`Tc2_EtherCAT.FB_EcPhysicalReadCmd`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_ethercat/57003787.html?id=5414131081651389994)
-   Added: [`Tc2_DataExchange.E_AdsComMode`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_dataexchange/1801691403.html?id=8330595141272503247)
-   Added: [`Tc2_DataExchange.FB_WriteAdsSymByName`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_dataexchange/1783921547.html?id=2139300129517202015)
-   Added: [`Tc2_DataExchange.FB_ReadAdsSymByName`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_dataexchange/1783919627.html?id=4947182374671618141)
-   Added: [`Tc2_Coupler.ST_FlashCode`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_coupler/42610955.html?id=2941218891386618606)
-   Added: [`Tc2_Coupler.ST_CouplerTable`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_coupler/42609419.html?id=5482306675259183856)
-   Added: [`Tc2_Coupler.ST_CouplerReg`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_coupler/42607883.html?id=7058535891579847280)
-   Added: [`Tc2_Coupler.ST_CouplerDiag`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_coupler/42606347.html?id=1994330772861109512)
-   Added: [`Tc2_Coupler.E_CouplerErrType`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_coupler/42604811.html?id=6845569431481975811)
-   Added: [`Tc2_Coupler.PLCINTFSTRUCT`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_coupler/42603275.html?id=7566696171309827053)
-   Added: [`Tc2_Coupler.F_GetVersionTcPlcCoupler`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_coupler/42600331.html?id=6362065393329470331)
-   Added: [`Tc2_Coupler.FB_WriteCouplerRegs`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_coupler/42597387.html?id=116904641330114048)
-   Added: [`Tc2_Coupler.FB_ReadCouplerRegs`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_coupler/42595851.html?id=8090904770520786892)
-   Added: [`Tc2_Coupler.FB_ReadCouplerDiag`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_coupler/42594315.html?id=3826489383443943666)
-   Added: [`Tc2_Coupler.CouplerReset`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_coupler/42592779.html?id=8709580392896105157)
-   Added: [`Tc2_Coupler.ReadWriteTerminalReg`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_coupler/42591243.html?id=7275193739490913707)

## Version 3.0.0

### Features

-   Added: [`Tc2_SystemC69xx.Introduction`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_systemc69xx/33439371.html?id=6260313291299739414)
-   Added: [`Tc2_SystemC69xx.F_GetVersionTcSystemC69xx`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_systemc69xx/33448203.html?id=7764496600018324112)
-   Added: [`Tc2_SystemC69xx.FB_C69xxSetWatchdog`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_systemc69xx/33443851.html?id=708222400761789552)
-   Added: [`Tc2_SystemC69xx.FB_C69xxSetLedColor`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_systemc69xx/33442315.html?id=5245365147276490369)
-   Added: [`Tc2_SUPS.F_GetVersionTcSUPS`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_sups/30502923.html?id=3242701461492151327)
-   Added: [`Tc2_SUPS.FB_NT_QuickShutdown`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_sups/30497035.html?id=6766415496240034724)
-   Added: [`Tc2_Standard.WRIGHT`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_standard/2260779147.html?id=381709618143922899)
-   Added: [`Tc2_Standard.WREPLACE`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_standard/2260777227.html?id=3506612230231411214)
-   Added: [`Tc2_Standard.WMID`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_standard/2260775307.html?id=5035747066483694025)
-   Added: [`Tc2_Standard.WLEN`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_standard/2260773387.html?id=5043866234088497158)
-   Added: [`Tc2_Standard.WLEFT`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_standard/2260771467.html?id=3696264996820623246)
-   Added: [`Tc2_Standard.WINSERT`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_standard/2260756747.html?id=5106620319933646641)
-   Added: [`Tc2_Standard.WFIND`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_standard/2260754827.html?id=2649583724707393001)
-   Added: [`Tc2_Standard.WDELETE`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_standard/2260752907.html?id=3219406437151749085)
-   Added: [`Tc2_Standard.WCONCAT`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_standard/2260750603.html?id=7101651603543101778)
-   Added: [`Tc2_Standard.RIGHT`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_standard/74423307.html?id=6967431909433980590)
-   Added: [`Tc2_Standard.REPLACE`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_standard/74421771.html?id=7007948245843702675)
-   Added: [`Tc2_Standard.MID`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_standard/74420235.html?id=22196133143246964)
-   Added: [`Tc2_Standard.LEN`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_standard/74418699.html?id=9152423183890501320)
-   Added: [`Tc2_Standard.LEFT`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_standard/74417163.html?id=6105127686094901693)
-   Added: [`Tc2_Standard.INSERT`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_standard/74415627.html?id=3080814905139265859)
-   Added: [`Tc2_Standard.FIND`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_standard/74414091.html?id=2152057911054988057)
-   Added: [`Tc2_Standard.DELETE`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_standard/74412555.html?id=1981646208249579943)
-   Added: [`Tc2_Standard.CONCAT`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_standard/74411019.html?id=147199721235531983)
-   Added: [`Tc2_Standard.R_TRIG`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_standard/74391563.html?id=2005587076592354672)
-   Added: [`Tc2_Standard.F_TRIG`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_standard/74390027.html?id=4042171645720455890)
-   Added: [`Tc2_Standard.LTP`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_standard/2261457803.html?id=5936550721515429456)
-   Added: [`Tc2_Standard.LTON`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_standard/2261455883.html?id=5792489106728084699)
-   Added: [`Tc2_Standard.LTOF`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_standard/2260730123.html?id=7882599680715545892)
-   Added: [`Tc2_Standard.TP`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_standard/74408075.html?id=7033170488447230146)
-   Added: [`Tc2_Standard.TON`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_standard/74406539.html?id=4250055966004209897)
-   Added: [`Tc2_Standard.TOF`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_standard/74405003.html?id=3683385772284534474)
-   Added: [`Tc2_Standard.CTUD`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_standard/74402059.html?id=5492544457860885206)
-   Added: [`Tc2_Standard.CTU`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_standard/74400523.html?id=3518659922652226515)
-   Added: [`Tc2_Standard.CTD`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_standard/74398987.html?id=565748032096893654)
-   Added: [`Tc2_Standard.SR`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_standard/74396043.html?id=731847196321796323)
-   Added: [`Tc2_Standard.RS`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_standard/74394507.html?id=2006013710248644288)
-   Added: [`Tc2_Math.F_GetVersionTcMath`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_math/68452363.html?id=9190123706788487018)
-   Added: [`Tc2_Math.MODTURNS`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_math/68449419.html?id=8912612634186732863)
-   Added: [`Tc2_Math.MODABS`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_math/68447883.html?id=1090163243389373794)
-   Added: [`Tc2_Math.LTRUNC`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_math/68446347.html?id=71387294442119971)
-   Added: [`Tc2_Math.LMOD`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_math/68444811.html?id=4508680757675684404)
-   Added: [`Tc2_Math.FRAC`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_math/68443275.html?id=6601927354937060161)
-   Added: [`Tc2_Math.FLOOR`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_math/68441739.html?id=3621922158533565644)
-   Added: [`Tc2_DataExchange.FB_WriteWatchdog`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_dataexchange/54804235.html?id=85146906305293695)
-   Added: [`Tc2_DataExchange.FB_CheckWatchdog`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_dataexchange/54802699.html?id=2233981294453593019)
-   Added: [`Tc2_DataExchange.FB_WriteLRealOnDelta`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_dataexchange/54799755.html?id=2153622439128161341)
-   Added: [`Tc2_DataExchange.FB_WriteRealOnDelta`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_dataexchange/54798219.html?id=4744412787628250664)
-   Added: [`Tc2_DataExchange.FB_WriteDWordOnDelta`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_dataexchange/54796683.html?id=1425720878032136659)
-   Added: [`Tc2_DataExchange.FB_WriteWordOnDelta`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_dataexchange/54795147.html?id=2662190263377611544)
-   Added: [`Tc2_DataExchange.FB_WriteByteOnDelta`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_dataexchange/54793611.html?id=6442744372477081479)
-   Added: [`Tc2_DataExchange.FB_WriteBoolOnDelta`](https://infosys.beckhoff.com/../content/1033/tcplclib_tc2_dataexchange/51771275.html?id=1377321760559972755)
