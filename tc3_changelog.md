# TwinCAT 3 changelog

## Version 4024.10

### Features

- Support of Visual Studio 2019

## Version 4024.4

### Features

- Spline interpolation for NCI GST Interpreter [Infosys](https://infosys.beckhoff.com/english.php?content=../content/1033/tf5100_tc3_nc_i/8250797579.html&id=2443170267198973234)

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
