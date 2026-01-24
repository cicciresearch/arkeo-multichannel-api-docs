# Sensor JSON Object

Sensors represent **physical or virtual measurement inputs** (e.g. temperature, humidity, irradiance) that are sampled independently from device channels.

Sensors are:

- globally defined
- uniquely identified by a `channel` index
- referenced by other API components (environments, day–night logic)

---

## Sensor object structure

Each sensor is described by a JSON object composed of two parts:

- `model`: The physical model of the sensor
- `common`: generic metadata shared by all sensors
- `specific`: sensor-dependent configuration fields

```json
{
  "model": "SHT3x-ARP Humidity",
  "common": { ... },
  "specific": { ... }
}
```

---

## `common` (object)

```json
"common": {
    "group": "Chamber",
    "name": "Humidity",
    "channel": 2,
    "type": "Humidity",
    "unit": "%",
    "origin": {
        "chamber": false,
        "external": false
}
```

The `common` object contains fields that are **present for all sensor types**.

| **Field** | **Description** | **Example** | **Type** |
|---------|-----------------|------------|---------|
| `group` | Logical group name | `"Chamber"` | string |
| `name` | Human-readable sensor name | `"Humidity"` | string |
| `channel` | Unique sensor identifier | `2` | integer |
| `type` | Sensor quantity type | `"Humidity"` | string |
| `unit` | Measurement unit | `"%"` | string |
| `origin` | Sensor origin metadata | object | object |

### `origin` (object)

| **Field** | **Description** | **Example** | **Type** |
|---------|-----------------|------------|---------|
| `chamber` | Sensor belongs to a chamber | `false` | boolean |
| `external` | Sensor is externally connected | `false` | boolean |

---

## `specific` (object)

The `specific` object contains **sensor-specific configuration fields**.

- Its content depends on the sensor model and type
- It may be empty if no additional configuration is required
- Its schema is **not shared** across sensor types

```json
"specific": {
  "offset": 0.2,
  "calibration_date": "2025-10-01"
}
```

Clients should treat this object as **opaque unless the sensor type is known**.

---

## Sensor identity and indexing

Each sensor is uniquely identified by its `channel` field.

```json
"channel": 2
```

This index is used consistently across the API:

| Usage | Field |
|----|----|
| Sensor configuration | `common.channel` |
| Live sensor data | `GetSensorsData → sensors[][0]` |
| Environments | `sensor_channels[]` |
| Day–Night logic | `sensor` |

---

## Relation to sensor data (`GetSensorsData`)

Live sensor values are returned separately from the sensor definition.

```json
{
  "schema":[
    {"name":"channel","type":"uint16"},
    {"name":"value","type":"float64"}
  ],
  "sensors":[
    [2, 56.83]
  ]
}
```

To associate a value with a sensor:
1. Read the `channel` index
2. Match it with `common.channel` from the sensor definition

---

## Design rules

!!! note "Design principles"
    - Sensor definitions are **static** (configuration)
    - Sensor data is **dynamic** (measurements)
    - Commands never mix configuration and live data in the same response

---
