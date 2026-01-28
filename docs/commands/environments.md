The following commands are related to the sensor environments.

**Response root:** `environments`

---

### **GetEnvironments**
**Description**  
Retrieve a list of all configured environments. `"sensor_channels"` contains an array of all associated sensor channels. Use the channel index from the [Sensor JSON String](../jsons/sensor-json.md) to associate the channel to the correct sensor.

**Example Request**

``` json
{"command": "GetEnvironments"}
```
**Example Response**
```json
{
  "status":"ok",
  "environments":[
    {
      "name":"Env1",
      "sensor_channels":[0,1]
    }
  ]
}
```