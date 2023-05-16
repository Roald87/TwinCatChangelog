# TwinCAT 3 HMI: TE2000

## Known bugs

-   PLC properties can only be used explicitly in the HMI by linking the property individually to a control attribute. If the entire function block is linked to a control attribute, the property is not called. This is the case when a function block is used as the source data of the DataGrid or as a user control parameter.

## Version 1.12.760.37
-   Fixed a crash when loading symbols from a .tmc file

## Version 1.12.758

-   Add recipe management control to create and edit recipes.
-   New themed symbol type which responds to HMI theme changes
-   Improved TcHMI nuget package version management.
    -   Old version numbering:
        -   HMI Product version 1.12.756.1 (`Major.Minor.Build.Patch`)
        -   nuget Package version 12.756.1 (`Major.Minor.Patch`)
    -   New:
        -   Server API Version (`Server_API_Version.Minor.Patch`)
    -   Breaking changes increase `Server_API_Version`.
    -   Meta package describe the dependencies.
-   EtherCAT diagnostics template for HMI project generator.
-   Add a scale factor for all HMI charts in the `GraphDescription` property.
-   Add stacked axis for bar charts.
-   Add support for x/y triggers in TcHmiScope.
-   EtherCAT diagnostics for Tc/BSD.
-   Add toggle for advanced settings of HMI server. Enable by right click the server in the HMI project.
-   Add pragma's to automatically map PLC symbols.

```
VAR
	{ attribute 'TcHmiSymbol.AddSymbol' }
	{ attribute 'TcHmiSymbol.AddSymbol.UserGroups' := 'test' }
	temperature : LREAL;
END_VAR
```

## Version 1.12.756.1

-   EtherCAT Diagnostics has now graphs for process data, similar to the online view in the IO tree in a TwinCAT project.
-   Scope control has new feature to download/upload recordings.
-   Added functions
    -   Locale/GetLocalizedText: Returns a localized text by key.
-   Pin HMI project to a specific TcHMI version. Disables auto migration to new HMI version.
-   Alarms can be created directly from ADS, OPC UA or a custom server extension. Includes EventGrid & EventLine support, localized text and integrated in the HMI server.
-   Directly download or upload scope records to and from HMI server.
-   Set min and max values for ENUMs and to define a value range.
-   It is possible to ignore escape sequences. Option `ignoreEscapeSequences` in the properties of for example a text block.
    − On `C:\TwinCAT\Functions`
    − Off `C:TwinCATFunctions`
-   Added `TcHmi.Functions.Beckhoff.GetLocalizedText()` to get the localized text of a symbol.
-   The maximum estimated database size and record time is added to HMI server config page on the tab TcHmiSqliteHistorize tab.

## Version 1.12.754.4

-   EtherCAT Diagnostics can be used to write/force values
-   New 'File Explorer' control
    -   Access the server's file system
    -   Access virtual directories outside of the working directory
    -   User management is integrated
    -   Upload and download files
-   New service webpage to manage multiple server instances. Accessible through right click HMI server > Service configuration.
-   New TC2049 "Time Based Clients" license. For 30 minute single client access if maximum clients are reached or for maintenance.
-   Event logger now supports Comment, Description URL and Description Text of an event.
-   Symbol `ClearLoggedEvents` is added to delete database entries from HMI client.
-   Extension SDK license is now included in the engineering server. A license is no longer required during development & publishing.

## Version 1.12.752.0

-   New EtherCAT Diagnostics

## Version 1.12.750.1

-   Important optimizations
-   New TwinCAT HMI Project Generator template

## Version 1.12.748.0

-   Resolving of references, pointers and interface pointers. See [InfoSys](https://infosys.beckhoff.com/content/1033/te2000_tc3_hmi_engineering/10740011531.html?id=3958689380699327712).

## Version 1.12

-   Black or whitelisting of symbols through the use of pragmas. See [InfoSys](https://infosys.beckhoff.com/content/1033/te2000_tc3_hmi_engineering/10740009611.html).
-   Support for properties and method calls. See [InfoSys](https://infosys.beckhoff.com/content/1033/te2000_tc3_hmi_engineering/10740006667.html?id=1586893120692980090). (Note: Properties have worked before in older version in a similar way. Not sure what has changed other than an icon difference.)
-   Multiple server instances on one system. See [InfoSys](https://infosys.beckhoff.com/content/1033/tf2000_tc3_hmi_server/10740576267.html).
-   Automatic closing of HMI server instances during installation.
-   TwinCAT HMI server registered as a service. It doesn't need to be started manually anymore.
-   Added NuGet package manager.

## Version 1.10.1336.203

### Bug fix

-   The HMI doesn't randomly write values into function block. Note: It is unclear if it was fixed in this version, or one between 1.10.1171.165 and 1.10.1336.203.

## Version 1.10.1336.0

-   The CreateBinding action is replaced by a CreateBinding function. See [InfoSys: CreateBinding](https://infosys.beckhoff.com/content/1033/te2000_tc3_hmi_engineering/5097942027.html?id=3579488638660561854). (Unknown if this cause issues during upgrade.)

## Version 1.10.1171.165

<!-- prettier-ignore-start -->
!!! warning
	Do not use this version. It contains a serious bug, where sometimes the HMI would randomly write default values into function blocks.
<!-- prettier-ignore-end -->
