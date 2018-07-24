> Note: By default, telnet server will disallow connections in STA mode.

## Description

Basic telnet server. Supports all serial connection terminal commands.

## Build settings

| Build flag | Description | Default value |
| --- | --- | --- |
| `TELNET_SUPPORT` | Enable Telnet module | `1` (on) |
| `DEBUG_TELNET_SUPPORT` | Show debug messages | `1` (on) |
| `TELNET_STA` | Allow connections when in STA mode | `0` (off)` |

## Configuration

|Key|Description|Possible values|Default value|
| --- | --- | --- | --- |
| telnetSTA | Allow connections in STA mode | 0 (no) or 1 (yes) | 0 (no) |