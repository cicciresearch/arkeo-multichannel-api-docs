# The Sensor JSON String

Sensor data is retrieved as a JSON string containing an array of all configured sensors. The specific section contains sensor specific configuration and/or calibration data. It can be an empty array.

```json
[
  {
    "type":"Pyranometer",
    "common":{
      "Channel":2,
      "Type":"Luminosity",
      "Unit":"W/m2",
      "Custom Name":"Pyranometer (ai2)"
    },
    "specific":{
      "Calibration (V/(W/m2))":9.13E-6,
      "Gain":200
    }
  },
  {
    "type":"SHT3x-ARP Temperature",
    "common":{
      "Channel":1,
      "Type":"Temperature",
      "Unit":"degC",
      "Custom Name":""
    },
    "specific":{
    }
  }
]
```