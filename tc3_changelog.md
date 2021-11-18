# TwinCAT 3 changelog

## Version 4024.22
### Features

- Maximum router memory increased from 1024 MB to 4095 MB [Infosys](https://infosys.beckhoff.com/english.php?content=../content/1033/tf7xxx_tc3_vision/18014405306596491.html&id=)

### Fix
- `Find All References` (Cross Reference List) broken in v4024.20 solved. 
- 'Symbolic Mapping' bug fixed.  Prior to this release, if Symbolic Mapping was enabled, some mapped links could become non-functional if there was certain ADS communications during an activation or restart.

### Known issues

- In VS2019 `Find` and `Find and Replace` does not work properly in TwinCAT files, related issue is tracked [here](https://developercommunity.visualstudio.com/content/problem/1168181/find-in-ivstextimage-does-not-work-in-visuastusio.html) .

## Version 4024.17

- In addition to the initial values of the parameters, the contexts can be assigned to tasks for the specific variant on the Context tab [InfoSys](https://infosys.beckhoff.com/content/1033/variant_management/6325850379.html?id=1933378558029834697)
- The status of the licenses on the Manage Licenses tab, which can be manually changed, is only changed for the active project variant or group [InfoSys](https://infosys.beckhoff.com/content/1033/variant_management/6325850379.html?id=1933378558029834697)
- The settings for the axis type and unit on the Settings tab are only saved for the active project variant or group. [InfoSys](https://infosys.beckhoff.com/content/1033/variant_management/6325852299.html?id=1663031461212356401)
- The Modulo scaling of a SERCOS encoders on the Sercos tab is only saved for the selected project variant or group. [InfoSys](https://infosys.beckhoff.com/content/1033/variant_management/6325852299.html?id=1663031461212356401)
- The axis type set on the Configuration tab is only saved for the active project variant or group. [InfoSys](https://infosys.beckhoff.com/content/1033/variant_management/6325852299.html?id=1663031461212356401)
- The variant of the stand-alone PLC project selected on the Project tab is only saved for the active project variant or group. [InfoSys](https://infosys.beckhoff.com/content/1033/variant_management/6325854219.html?id=7183010108179338387)
- The device set on the General NOV-DP-RAM device tab is only set for the active project variant or group. [InfoSys](https://infosys.beckhoff.com/content/1033/variant_management/6325868939.html?id=5362468858073827180)
- The NOV-DP-RAM device is only disabled for the active project variant or group. [InfoSys](https://infosys.beckhoff.com/content/1033/variant_management/6325868939.html?id=5362468858073827180)

## Version 4024.15

### Bug fix
- A faulty driver in 4024.10-4024.12 can lead to Visual Studio crashes during a stand-alone project build. Specifically during the "Import symbol information" build step if a .tpr refactor file is present. Should be fixed in > 4024.12 (Source: Beckhoff support CH. See also [StackOverflow](https://stackoverflow.com/a/69926305/6329629).)

### Features

- Automatic Accurate Stop for NCI GST Interpreter [Infosys](https://infosys.beckhoff.com/english.php?content=../content/1033/tf5100_tc3_nc_i/10038263179.html&id=270450158997902620)

## Version 4024.12

### Features

- Change in path dynamics for NCI GST Interpreter [Infosys](https://infosys.beckhoff.com/english.php?content=../content/1033/tf5100_tc3_nc_i/9237585035.html&id=8344109939385622623)

## Version 4024.11

### Features

- Error analysis with core dump [Infosys](https://infosys.beckhoff.com/english.php?content=../content/1033/tc3_plc_intro/6884133515.html&id=9193305343691095620)
- Function added: F_GetCpuCoreIndex [Infosys](https://infosys.beckhoff.com/english.php?content=../content/1033/tcplclib_tc2_system/8824208779.html&id=557299053114329889)
- Function added: F_GetCpuCoreInfo [Infosys](https://infosys.beckhoff.com/english.php?content=../content/1033/tcplclib_tc2_system/8824297099.html&id=985625989999487283)
- Function added: F_GetTaskTotalTime [Infosys](https://infosys.beckhoff.com/english.php?content=../content/1033/tcplclib_tc2_system/8830227851.html&id=9031864548778018881)
- Function added: FindAndSplit [Infosys](https://infosys.beckhoff.com/english.php?content=../content/1033/tcplclib_tc2_utilities/8235976331.html&id=3438267492659948266)
- Function added: FindAndSplitChar [Infosys](https://infosys.beckhoff.com/english.php?content=../content/1033/tcplclib_tc2_utilities/8245507851.html&id=9180678329069202236)
- The license dongle is only disabled for the active project variant or group [InfoSys](https://infosys.beckhoff.com/content/1033/variant_management/6325850379.html?id=1933378558029834697)

## Version 4024.10

### Features

- Support of Visual Studio 2019
- The TcCom object is only disabled for the active project variant or group [InfoSys](https://infosys.beckhoff.com/content/1033/variant_management/6325850379.html?id=1933378558029834697)
- The initial values of the parameters listed on the Parameter (Init) tab can be enabled for the variant management [InfoSys](https://infosys.beckhoff.com/content/1033/variant_management/6325850379.html?id=1933378558029834697)
- The C++ project/instance is only disabled for the active project variant or group. [InfoSys](https://infosys.beckhoff.com/content/1033/variant_management/8843640971.html?id=4959120427343912986)
- C++ instance: The initial values of the parameters listed on the Parameter (Init) tab can be enabled for the variant management. [InfoSys](https://infosys.beckhoff.com/content/1033/variant_management/8843640971.html?id=4959120427343912986)
- C++ instance: The interface pointers listed on the Interface Pointer tab can be enabled for the variant management. [InfoSys](https://infosys.beckhoff.com/content/1033/variant_management/8843640971.html?id=4959120427343912986)

## Version 4024.7

### Features

- The settings for Divider and Modulo on the Settings tab are only saved for the active project variant or group. [InfoSys](https://infosys.beckhoff.com/english.php?content=../content/1033/variant_management/6325876619.html&id=)

## Version 4024.4

### Features

- Spline interpolation for NCI GST Interpreter [Infosys](https://infosys.beckhoff.com/english.php?content=../content/1033/tf5100_tc3_nc_i/8250797579.html&id=2443170267198973234)
- Change in axis dynamics for NCI GST Interpreter [Infosys](https://infosys.beckhoff.com/english.php?content=../content/1033/tf5100_tc3_nc_i/8405470603.html&id=745347749354607281)
- The links selected via the Link to I/O button and Link To PLC on the Settings tab are only saved for the active project variant or group. [InfoSys](https://infosys.beckhoff.com/english.php?content=../content/1033/variant_management/6325876619.html&id=)
- The links to the process data objects (PDOs) of the EtherCAT device are only saved for the active project variant or group. [InfoSys](https://infosys.beckhoff.com/content/1033/variant_management/6325868939.html?id=5362468858073827180)

## Version 4024.0 

### [Features](https://www.beckhoff.com/en-en/products/automation/twincat/twincat-3-build-4024/)

- Integration of Visual Studio® 2017 Shell (TcXaeShell).
- New home page, including new RSS feed with TwinCAT information.
- Variant management. Simple configuration of machine options. Version-specific deactivation/activation of components. Version-specific parameterization. Mapped through ‘conditional compilation’ in the PLC.
- Multi-user PLC capability. Several programmers can work on the same PLC project simultaneously.
- Corrected time stamps for data records, e.g. via NTP protocol.
- Improved overview in the I/O configuration mapping dialog
- 'Go To Definition' from the PLC process image to the PLC code in the I/O configuration
- 'Secure ADS' Extension (uses TCP port 8016): encrypted ADS communication
- Detection of failure to free up dynamically allocated memory. See also this [StackOverflow question](https://stackoverflow.com/q/68709572/6329629).

#### PLC properties

- Improvements in the cross-reference list (new filter, performance enhancements).
- New keyword: ABSTRACT for abstract FB/method/property definition.
- Improved monitoring of interface variables.
- Small icons in the solution tree show access modifiers.
- ENUMs now also available as strings in the PLC.
- Exception handling via TRY-CATCH for 32-bit systems.
- Simplified commenting function in the PLC.
- 'Released' flag is used during library creation.
- Conditional compilation also available in the declaration section (in addition to implementation part).
- Multi-line support in pragma declarations.
- New, optional Base64 memory format for graphical PLC objects.
- Events stored in a separate .tmc file are formatted with line breaks.

#### PLC HMI properties

- Automatic local start of the PLC HMI client at runtime.
- Dynamic scaling for the operating elements of the measuring equipment category.
- Offline rotation of elements.
- Performance improvements during opening of dialogs.
- Automatic transfer of scaling options of the TargetVisu object to the Tc3PlcHmi.ini file.

#### C++ & MATLAB properties

- Exchange of TcCOM modules for C++ und MATLAB®/Simulink® while the machine is running.
- Repository for versioned C++ projects.
- New way of signing TcCOM modules.

#### AML data exchange

- Based on the AutomationML format.
- Bidirectional exchange of I/O topologies with ECAD tools.
- Incremental import of I/O topologies.
- Fully integrated in TwinCAT.

#### Safety-related properties

- User-defined function blocks can be created and instantiated as  often as required (including GoToDefinition, Online View, nesting up to 2 levels).
- Multiple use of variables.
- Global variables.

#### Scope properties

- Project wizard facilitates Scope configuration.
- New single bar and digital charts.
- Dynamic style for dynamic display switching, depending on variables.
- Shapes: display of geometric shapes in x/y plots.
- Vision trigger: inserts images with time stamp into the Scope data stream.
- Headless mode: allows the view to be disconnected from the server during recording.
- Marker: with docking function on the x-axis and label feature.
- Integrated dictionary with physical units.
- Clear display option for clearing the chart after the display time has elapsed.

## Version 4022.30

### Bugfixes

- POUs can be removed from a PLC project in visual studio again.

## Version 4022.16

### Bugfixes

- Sometimes the Microsoft patch for Spectre/Meltdown would prevent you from activating the configuration on a local runtime. [See also](https://stackoverflow.com/questions/51185052/twincat-running-on-isolated-cores-failed). 
