# InfluxDB integration

## Basic configuration

### Build settings

| Build flag | Description | Default value |
| --- | --- | --- |
| `INFLUXDB_SUPPORT` | Enable InfluxDB module | `0` |

## Transmitted values

### All devices

|Value name|Description|
| --- | --- |
|uptime||
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

