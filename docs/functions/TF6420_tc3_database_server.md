# TF6420 | TwinCAT 3 database server

## Version 3.3.35.0

-   Database Configurator
    -   New design of DocumentDB in SQL Query Editor
    -   Added Find, Insert, Update, Aggregate and Drop/Delete for NoSQL
-   Database Server

    -   New support of InfluxDB2
        -   Connection token support
        -   Support of Flux language—also in SQL Query Editor
        -   Support of all function blocks
            -   For NoSQL function blocks use the Time Series Query Builder
            -   Only stored procedure function blocks are not supported
    -   Type system improvements for InfluxDB1.x support
    -   Optimized multiple calls of RunOnce method on WinCE

-   Database Library
    -   New option to turn off the clear memory of `FB_PLCDBCmdEvt` via property

## Version 3.3.34.5

-   Fixes failure to load TF6420 license with auto boot enabled on system startup. A Start/Restart was required to reload the license. Issue seemed to be for newer TF6420 versions running with TwinCAT v3.1.4022 or older.

## Version 3.3.34.0

-   TwinCAT/BSD support added
-   New Query Editor
