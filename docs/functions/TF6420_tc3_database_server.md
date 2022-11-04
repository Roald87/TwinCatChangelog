# TF6420 | TwinCAT 3 database server

## Version 3.3.35.0
- Database Configurator
    - New design of DocumentDB in SQL Query Editor
    - Added Find, Insert, Update, Aggregate and Drop/Delete for NoSQL
- Database Server
    - New support of InfluxDB2
        - Connection Token support
        - Support of Flux language – also in SQL Query Editor
        - Support of all Function Blocks 
            - For NoSQL FBs please use Time Series Query Builder
            - Only Stored Procedure FBs are not supported
    - Type System improvements for InfluxDB1.x support
    - Optimized multiple calls of RunOnce method on WinCE

- Database Library
  - New disable option to clear memory of FB_PLCDBCmdEvt via property

## Version 3.3.34.5

-   Fixes failure to load TF6420 license with auto boot enabled on system startup. A Start/Restart was required to reload the license. Issue seemed to be for newer TF6420 versions running with TwinCAT v3.1.4022 or older.

## Version 3.3.34.0

-   TwinCAT/BSD support added
-   New Query Editor
