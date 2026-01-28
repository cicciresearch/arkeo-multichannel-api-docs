The following commands are related to the sensors.

**Response root:** `sensors`

---

### **GetSensorsInfo**
**Description**  
Retrieve sensor configuration (JSON with channels, names, types, units, and sensor-specific settings). See: [Sensor JSON String](../jsons/sensor-json.md) for more details.

**Example Request**
``` json
{"command": "GetSensorsInfo"}
```
**Example Response**
```json
{
  "status":"ok",
  "sensors":[
    {
      "model":"SHT3x-ARP Humidity",
      "common":{
        "group":"",
        "name":"Humidity",
        "channel":2,
        "type":"Humidity",
        "unit":"%",
        "origin":{
          "chamber":false,
          "external":false
        }
      },
      "specific":{
      }
    }
  ]
}
```

---
### **GetSensorsData**
**Description**  
Retrieve the live values of all sensors. Use the channel index from the [Sensor JSON String](../jsons/sensor-json.md) to associate the value to the correct sensor.

**Example Request**

``` json
{"command": "GetSensorsData"}
```
**Example Response**
```json
{
  "status":"ok",
  "schema":[
    {"name":"channel","type":"uint16"},
    {"name":"value","type":"float64"}
  ],
  "sensors":[
    [0,56.83]
    [1,23.56]
    [2,945.13]
  ]
}
```