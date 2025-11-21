## Device Commands

The following commands affect the SMU channels. Before each command the SetActiveChannel command should be called to specify on which SMU channel the operation should be performed.

---
### **SetActiveChannel**

**Description**  
Set the channel upon which all succeeding actions are performed.

**Example Request**
```json
{"command": "SetActiveChannel", "parameter": { "channel_id": 0 } }
```
**Example Response**
```json
0
```
  
---
### **GetActiveChannel**

**Description**
Get the active channel.

**Example Request**

``` json
{"command": "GetActiveChannel", "parameter": { } }
```
**Example Response**
```json
0
```

---
### **SetChannelSettings**
**Description**
Set the JSON configuration string for the active channel. See [The JSON settings string](jsons/settings-json.md) for more details.

**Example Request**
``` json
{
  "command": "SetChannelSettings",
  "parameter": {
    "settings": "{... JSON settings string ...}"
  }
}
```
**Example Response**
```json
OK
```

---
### **GetChannelSettings**
**Description**
Retrieve the JSON configuration string of the active channel. See [The JSON settings string](jsons/settings-json.md) for more details.

**Example Request**

``` json
{"command": "GetChannelSettings", "parameter": { } }
```
**Example Response**
```json
{ ... JSON settings string ...}
```

---
### **StartChannel**
**Description**
Start the measurement process for the active channel.

**Example Request**
``` json
{"command": "StartChannel", "parameter": { } }
```
  **Example Response**
```json
OK
```

---
### **StopChannel**
**Description**
Stop the measurement process for the active channel.

**Example Request**
``` json
{"command": "StopChannel", "parameter": { } }
```

  **Example Response**
```json
OK
```
--
### **ForceJV**
**Description**
Force a JV measurement on the active channel when in tracking mode.

**Example Request**
``` json
{"command": "ForceJV", "parameter": { "channel_id": 0 } }
```
**Example Response**
```json
OK
```

---
### **GetChannelState**
**Description**
Retrieve the current state of the active channel. See [The JSON state string](jsons/state-json.md) for more details.

**Example Request**
``` json
{"command": "GetChannelState", "parameter": { } }
```
**Example Response**
```json
{... JSON state string ...}
```

---
### **GetLatestJV**
**Description**
Retrieve the voltage and current values of the latest JV measurement.

**Example Request**
``` json
{"command": "GetLatestJV", "parameter": { } }
```
**Example Response**

    v_fw1|j_fw1|...|v_fwn|j_fwn||v_rv1|j_rv1|...|v_rvn|j_rvn


---
### **GetIV**
**Description**
Retrieve the live voltage and current values of all channels.

**Example Request**

``` json
{"command": "GetIV", "parameter": { } }
```
**Example Response**

v1|j1|...|vn|jn

---
### **GetSensorsInfo**
**Description**
Retrieve sensor configuration (JSON with channels, names, types, units, and sensor-specific settings). See: [Sensor JSON String](jsons/sensor-json.md) for more details.

**Example Request**
``` json
{"command": "GetSensorsInfo", "parameter": { } }
```
**Example Response**

    [ ... Sensor JSON String ... ]

---
### **GetSensors**
**Description**
Retrieve the live values of all sensors. The order of the values and their units are the same as the order from the [Sensor JSON String](jsons/sensor-json.md).

**Example Request**

``` json
{"command": "GetSensors", "parameter": { } }
```
**Example Response**
```
1|s2|...|sn|
```

---
### **SetChannelEnvironment**
**Description**
Associate a channel to an environment

**Example Request**
``` json
{"command": "GetSensorsInfo", "parameter": {"environment":"Env1"} }
```
**Example Response**
```json
OK
```