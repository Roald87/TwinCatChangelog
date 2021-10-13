# TE2000: TwinCAT 3 HMI 

## Version 1.12.750.1

- Important optimizations 
- New TwinCAT HMI Project Generator template

## Version 1.10.1336.203

### Bug fix

- The HMI doesn't randomly write values into function block. Note: I'm not 100% sure if it was fixed in this version, or one between 1.10.1171.165 and 1.10.1336.203.

## Version 1.10.1336.0
- The CreateBinding action is replaced by a CreateBinding function. See [Infosys: CreateBinding](https://infosys.beckhoff.com/content/1033/te2000_tc3_hmi_engineering/5097942027.html?id=3579488638660561854). (Unknow if this cause issues during upgrade.)

## Version 1.10.1171.165

**Warning: DO NOT USE THIS VERSION. It contains a serious bug, where sometimes the HMI would randomly write default values into function blocks.**
