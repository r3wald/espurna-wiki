# InfluxDB integration

## Basic configuration

### Build settings

InfluxDB is not included/compiled/supported/enabled by default.

To add it to all your modules, an easy way is to add the following defines in the custom.h and to add the compilation flag USE_CUSTOM_H.

| Defines | Description | Sample value |
| --- | --- | --- |
| `INFLUXDB_SUPPORT` | Include InfluxDB module | `1` |
| `INFLUXDB_ENABLED` | Enable InfluxDB module | `1` |
| `INFLUXDB_HOST` | Hostname | `db.acme.com` |
| `INFLUXDB_PORT` | IP Port | `8090` |
| `INFLUXDB_DATABASE` | Database | `dev_db` |
| `INFLUXDB_USERNAME` | Username | `dev_usr` |
| `INFLUXDB_PASSWORD` | Passwword | `*******` |

For example I add them in the following way:

#ifdef INFLUXDB_SUPPORT

    #undef INFLUXDB_SUPPORT

#endif

#define INFLUXDB_SUPPORT       1

#ifdef INFLUXDB_ENABLED

    #undef INFLUXDB_ENABLED

#endif

#define INFLUXDB_ENABLED       1


#ifdef INFLUXDB_HOST

    #undef INFLUXDB_HOST

#endif

#define INFLUXDB_HOST       "db.acme.com"


[...]


## Transmitted values

### All devices

|Value name|Description|
| --- | --- |
|uptime|in seconds|
|freeheap||
|rssi||

### Basic, RF, POW

|Value name|Description|
| --- | --- |
|relay|relay state (0,1)|

### POW

|Value name|Description|
| --- | --- |
|current||
|voltage||
|power||
|reactive||
|apparent||
|factor||
|energy||

