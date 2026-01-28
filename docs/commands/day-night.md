The following commands are related to the global Day-Night cycling.

**Response root:** `day_night`

---

### **GetGlobalDayNight**
**Description**  
Returns the global day-night cycling values and settings

**Example Request**
``` json
{"command": "GetGlobalDayNight"}
```
**Example Response**
```json
{
  "status":"ok",
  "day_night":{
    "status":{
      "isDay":true,
      "DelayTimer":"2026-01-24T09:12:56.667Z",
      "Elapsed Time (s)":154.133176803589,
      "Sensor Value":100
    },
    "settings":{
      "enable":false,
      "sensor":0,
      "threshold_value":10,
      "threshold_duration":8,
      "night_algorithm":"Open Circuit",
      "night_jv":false
    }
  }
}
```

---
### **SetGlobalDayNight**
**Description**  
Set the global day-night cycling settings.

**Example Request**
``` json
{
  "command":"SetGlobalDayNight",
  "parameter":{
    "settings":{
      "enable":true,
      "sensor":0,
      "threshold_value":10,
      "threshold_duration":8,
      "night_algorithm":"MPPT",
      "night_jv":false
    }
  }
}
```
**Example Response**
```json
{"status":"ok"}
```