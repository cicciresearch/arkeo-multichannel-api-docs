# Environments JSON
The configured environments are retrieved as a JSON array. The `sensors_id` field contains an array of the included sensors. Cross-reference them with the [Sensor JSON String](sensor-json.md).
```json
[
  {
    "name":"Env1",
    "sensors_id":[
      "Pyro;2;Luminosity",
      "Temp;1;Temperature"
    ]
  }
]
```