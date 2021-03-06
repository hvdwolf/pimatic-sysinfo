pimatic-sysinfo
===============

Plugin for displaying  system and process information such as CPU and Memory usage 
 for pimatic setups on Linux and Windows. MacOS should also work, but has not been tested. 
 
The plugin is based on the 
 [systeminformation project](https://github.com/sebhildebrandt/systeminformation) 
 developed by Sebastian Hildebrandt which realizes a lightweight abstraction layer 
 for the acquisition of system information on various operating systems.

### Supported values:

* CPU usage (percent): `"cpu"`
* Memory usage (bytes): `"memoryUsed"`
* Memory usage (percent): `"memoryUsedPercent"`
* Memory free (bytes): `"memoryFree"`
* Memory free (percent): `"memoryFreePercent"`
* Disk usage (percent) for a single mount point: `"diskUsage"`
* Number of processes: `"processes"`
* System temperature (Celsius ℃): `"temperature"`
* System temperature (Fahrenheit ℉): `"temperatureF"`
* System uptime in seconds: `"systemUptime"`
* System uptime in Days Hours Minutes: `"systemUptimeDHM"`
* WiFi received signal level (dBm): `wifiSignalLevel` 
* Network interface throughput received (bps): `nwThroughputReceived` 
* Network interface throughput sent (bps): `nwThroughputSent` 
* Pimatic SQLite database size (bytes): `"dbSize"`
* Pimatic process RSS memory (bytes): `"pimaticRss"`
* Pimatic process used heap memory (bytes): `"pimaticHeapUsed"`
* Pimatic process total heap memory (bytes): `"pimaticHeapTotal"`
* Pimatic process uptime (seconds): `"pimaticUptime"`
* Pimatic process uptime (Days Hours Minutes): `"pimaticUptimeDHM"`

Notes:
* Database size is only applicable if builtin SQLite database
  is being used
* RSS is the amount of space occupied in the main memory device 
  (that is a subset of the total allocated memory) for the 
  process, which includes the heap, code segment and stack
* The attribute `wifiSignalLevel` is currently only supported on Linux
* The spelling for some attributes has been changed in release 0.9.5. The device 
  configuration setup for earlier releases will be transformed 
  automatically. However, you may need to update references in rule and
  variable definitions. See table below.

| old | new |
|:----|-----|
| diskusage | diskUsagePercent |
| dbsize | dbSize |
| uptime | systemUptime |
| memory | memoryUsed |
| memoryRss | pimaticRss |
| heapUsed | pimaticHeapUsed |
| heapTotal | pimaticHeapTotal |
  
### Plugin Configuration

```
{ 
  "plugin": "sysinfo"
}
```

### Device Configuration

#### Examples:

```json
{
  "class": "SystemSensor",
  "id": "system-info",
  "name": "System",
  "attributes": [
    {
      "name": "cpu"
    },
    {
      "name": "memoryUsed"
    },
    {
      "name": "diskUsagePercent",
      "path": "/"
    }
  ]
}
```


```json
{
  "class": "SystemSensor",
  "id": "system-temp",
  "name": "System Temp.",
  "attributes": [
    {
      "name": "temperature",
      "interval": 5000
    }
  ]
}
```

### Trouble Shooting

* The value for `temperature` is -1
    
  On Windows, admin privileges are required in some setups to query the 
  temperature with the underlying `wmic` tool. If you're running on Linux,
  please report an issue with the Linux distribution, version and hardware 
  used.
  
* I would like to display the uptime in a human readable format

  You can set the `displayFormat xAttributeOption` for attribute `systemUptime`
  or `pimaticUptime` to the value `uptime`. 

### Credits

<div>Icon made by <a href="http://www.freepik.com" title="Freepik">Freepik</a> is licensed under <a href="http://creativecommons.org/licenses/by/3.0/" title="Creative Commons BY 3.0">CC BY 3.0</a></div>
