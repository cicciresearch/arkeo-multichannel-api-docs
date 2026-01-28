The following commands affect the SMU channels.

**Response root:** `channels`

---

### **SetChannelSettings**
**Description**  
Set the JSON configuration string for the active channel. See [The JSON settings string](../jsons/settings-json.md) for more details.

**Example Request**
``` json
{
  "command": "SetChannelSettings",
  "indices":[0,1,2],
  "parameter": {
    "settings": "{... JSON settings string ...}"
  }
}
```

**Example Response**
```json
{ "status":"ok" }
```

```json
{
  "status":"error",
  "error":{"code":5001,"message":"Invalid JSON"}
}
```

---
### **GetChannelSettings**
**Description**  
Retrieve the JSON configuration string of the active channel. See [The JSON settings string](../jsons/settings-json.md) for more details.

**Example Request**

``` json
{"command": "GetChannelSettings", "indices":[0,1,2]}
```
**Example Response**
```json
{
  "status":"ok",
  "channels":[
    { ... JSON settings string index i ...},
    { ... JSON settings string index i+1 ...}
  ]
}
```

---
### **StartMeasurement**
**Description**  
Start the measurement process.
???+ note
    This command should only be used once to start the measurement process. If a channel is configured while a measurement is running, it will start automatically

**Example Request**
``` json
{"command": "StartMeasurement"}
```
  **Example Response**
```json
{ "status":"ok" }
```

```json
{
  "status":"error",
  "error":{"code":5005,"message":"Already running"}
}
```

```json
{
  "status":"error",
  "error":{"code":5006,"message":"No channel running, enable at least 1 channel"}
}
```

---
### **StopChannel**
**Description**  
Stop the measurement process for the selected channels. 
!!! note "Invalid command"
    If a channel is already stopped or is not enabled, no state change occurs. The `"result"` key will have the value `"ignored"`

**Example Request**
``` json
{"command": "StopChannel", "indices":[0,1,2]}
```

**Example Response**
```json
{
  "status":"ok",
  "channels":[
    {
      "index":0,
      "enabled":true,
      "previous_state":"running",
      "new_state":"stopped",
      "result":"stopped"
    }
  ]
}
```

---

### **ForceJV**
**Description**  
Force a JV measurement on the selected channels.

**Example Request**
``` json
{"command": "ForceJV", "indices":[0,1,2]}
```

**Example Response**
```json
{
  "status":"ok",
  "channels":[
    {
      "index":0,
      "enabled":true,
      "state":"running",
      "measurement":"jv",
      "result":"ok"
    }
  ]
}
```

The `ForceJV` command is ignored if the channel is:

- not enabled  
- not running  
- already in JV  

In that case `"result"` will return `"ignored"`, with an additional `"reason"` key stating one of the above reasons.

**Example Response**
```json
{
  "status":"ok",
  "channels":[
    {
      "index":0,
      "enabled":true,
      "state":"stopped",
      "measurement":"jv",
      "result":"ignored",
      "reason":"not running"
    }
  ]
}
```

---
### **GetChannelState**
**Description**  
Retrieve the current state of the selected channels. See [The JSON state string](../jsons/state-json.md) for more details.

**Example Request**
``` json
{"command": "GetChannelState", "indices":[0,1,2]}
```
**Example Response**
```json
{
  "status":"ok",
  "channels":[
    {"index":0,"enable":true,"user":"Cicci Research","device":"Sample","measurement":"jv","direction":"forward","state":"running"}
  ]
}
```

---
### **GetLatestJV**
**Description**  
Retrieve the voltage and current values of the latest JV measurement as an array of JSON object.
See: [`JV JSON object`](../jsons/jv-json.md)

**Example Request**
``` json
{"command": "GetLatestJV", "indices":[0,1,2]}
```
**Example Response**
``` json
{
  "status":"ok",
  "channels":[
    { ... JV JSON object 1 ... },
    { ... JV JSON object 2 ... },
    ...
  ]
}



```
---
### **GetIV**
**Description**  
Retrieve the live voltage and current values of all channels.

**Example Request**

``` json
{"command": "GetIV"}
```
**Example Response**

```json
{
  "status":"ok",
  "schema":[
    {"name":"Voltage","unit":"V"},
    {"name":"Current","unit":"A"}
  ],
  "data":[
    [-8.52843206071149,-0.00816152902459247],
    [-7.57741630298776,-0.00708037023781523],
    [-6.40744244717755,-0.00580657492001222],
    ...
  ],
  "timestamp":"2026-01-24T09:14:09.685Z"
}
```

---
### **SetDeviceEnvironment**
**Description**  
Associate an environment to a device.

**Example Request**
``` json
{
 "command":"SetDeviceEnvironment",
 "indices":[0,1,2],
 "parameters":{"environment":"env1"}
}
```
**Example Response**
```json
{"status":"ok"}
```

If an invalid environment name is provided, an error object is returned
```json
{
  "status":"error",
  "error":{
    "code":5002,
    "message":"Invalid Environment: indoor.\nUse 'GetEnvironments' to get a list of valid environment names."
  }
}
```