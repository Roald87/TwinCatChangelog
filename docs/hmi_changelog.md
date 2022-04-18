# TwinCAT 3 HMI: TE2000

## Known bugs

- PLC properties can only be used explicitly in the HMI by linking the property individually to a control attribute. If the entire function block is linked to a control attribute, the property is not called. This is the case when a function block is used as the source data of the DataGrid or as a user control parameter.

## Version 1.12.754.4

- EtherCAT Diagnostics can be used to write/force values
- New 'File Explorer' control

## Version 1.12.752.0

- New EtherCAT Diagnostics

## Version 1.12.750.1

- Important optimizations
- New TwinCAT HMI Project Generator template

## Version 1.12.748.0

- Resolving of references, pointers and interface pointers. See [InfoSys](https://infosys.beckhoff.com/content/1033/te2000_tc3_hmi_engineering/10740011531.html?id=3958689380699327712).

## Version 1.12

- Black or whitelisting of symbols through the use of pragmas. See [InfoSys](https://infosys.beckhoff.com/content/1033/te2000_tc3_hmi_engineering/10740009611.html).
- Support for properties and method calls. See [InfoSys](https://infosys.beckhoff.com/content/1033/te2000_tc3_hmi_engineering/10740006667.html?id=1586893120692980090). (Note: Properties have worked before in older version in a similar way. Not sure what has changed other than an icon difference.)
- Multiple server instances on one system. See [InfoSys](https://infosys.beckhoff.com/content/1033/tf2000_tc3_hmi_server/10740576267.html).
- Automatic closing of HMI server instances during installation.
- TwinCAT Hmi server registered as a service. It doesn't need to be started manually anymore.
- Added NuGet package manager.

## Version 1.10.1336.203

### Bug fix

- The HMI doesn't randomly write values into function block. Note: I'm not 100% sure if it was fixed in this version, or one between 1.10.1171.165 and 1.10.1336.203.

## Version 1.10.1336.0

- The CreateBinding action is replaced by a CreateBinding function. See [Infosys: CreateBinding](https://infosys.beckhoff.com/content/1033/te2000_tc3_hmi_engineering/5097942027.html?id=3579488638660561854). (Unknow if this cause issues during upgrade.)

## Version 1.10.1171.165

**Warning: DO NOT USE THIS VERSION. It contains a serious bug, where sometimes the HMI would randomly write default values into function blocks.**
