The [`GetLatestJV`](../commands/device.md#getlatestjv) command retrieves the latest JV scan acquired from the device under test, together with derived photovoltaic parameters.

---

## Request

```json
{ "command": "GetLatestJV" }
```

---

## Response structure

```json
{
  "user": "string",
  "device": "string",
  "area": {
    "value": number,
    "unit": "cm^2"
  },
  "time": "ISO-8601 timestamp",
  "data_schema": [ ... ],
  "parameter_schema": [ ... ],
  "scans": [ ... ]
}
```

### Top-level fields

| Field              | Type   | Description                                             |
| ------------------ | ------ | ------------------------------------------------------- |
| `user`             | string | Operator or organisation performing the measurement     |
| `device`           | string | Device or sample identifier                             |
| `area`             | object | Active device area                                      |
| `time`             | string | Timestamp when the JV data was acquired (UTC, ISO‑8601) |
| `parameter_schema` | array  | Schema describing extracted JV parameters               |
| `scans`            | array  | List of JV scans (forward, reverse)     |

---

## Scans

Each entry in the `scans` array represents one JV scan.

```json
{
  "name": "forward",
  "data_schema": [ ... ],
  "data": [ ... ],
  "parameters": { ... }
}
```

### Scan fields

| Field        | Type   | Description                                            |
| ------------ | ------ | ------------------------------------------------------ |
| `name`       | string | Scan identifier (`forward`, `reverse`) |
| `data_schema`| array  | Schema describing JV data columns                      |
| `data`       | array  | JV data points following `data_schema`                 |
| `parameters` | object | Extracted photovoltaic parameters (resolved form)      |

---

## Data schema

The `data_schema` defines the meaning and units of each column in the JV data arrays.

```json
"data_schema": [
  { "name": "voltage", "unit": "V" },
  { "name": "current", "unit": "mA/cm^2" }
]
```

Each entry in a scan’s `data` array follows the same column order as defined in `data_schema`.

---

## JV data

JV data is provided as an array of numeric arrays for compactness and performance.

```json
"data": [
  [ -0.10,  0.00012 ],
  [  0.00,  0.00011 ],
  [  0.30, -0.00002 ]
]
```

Each inner array corresponds to one measurement point:

```text
[ voltage, current_density ]
```

The meaning and units of each column are defined by `data_schema`.

---

## Resolved parameters

Extracted parameters are provided as a resolved object with explicit units.

```json
"parameters": {
  "voc":         { "value": 0.00290,  "unit": "V" },
  "jsc":         { "value": 0.32602,  "unit": "mA/cm^2" },
  "v_mpp":       { "value": 0.11531,  "unit": "V" },
  "j_mpp":       { "value": 0.21741,  "unit": "mA/cm^2" },
  "p_mpp":       { "value": 0.08436,  "unit": "mW/cm^2" },
  "r_series":    { "value": 764.41,   "unit": "Ohm" },
  "r_shunt":     { "value": 107060.3, "unit": "Ohm" },
  "fill_factor": { "value": 48.78,    "unit": "%" },
  "efficiency":  { "value": 1.834,    "unit": "%" }
}
```

---

## Full Response Example

Below is a typical response for a full JV scan. Including a forward and reverse scan.

```json
{
  "user":"Cicci Research",
  "device":"Sample",
  "area_cm2":1,
  "acquisition_time":"2026-01-26T12:22:07.461Z",
  "scans":[
    {
      "name":"forward",
      "data_schema":[
        {"name":"Voltage","unit":"V"},
        {"name":"Current","unit":"mA/cm^2"}
      ],
      "data":[
        [-0.10164886713028,1.17926585553872E-4],
        [-0.0819301605224609,1.18105399488199E-4],
        [-0.0628146529197693,1.16118577995686E-4],
        [-0.0403454899787903,1.15959632276285E-4],
        [-0.0203907489776611,1.16234475916082E-4],
        [-0.00229477882385254,1.15277490230522E-4],
        [0.0187844038009644,1.15794063818575E-4],
        [0.0362935662269592,1.13459548564872E-4],
        [0.0591135025024414,1.12403221804686E-4],
        [0.0792485475540161,1.10724357643513E-4],
        [0.0972986221313477,1.12336994421602E-4],
        [0.118472874164581,1.07737502666435E-4],
        [0.137853920459747,1.06078506720186E-4],
        [0.158887207508087,1.03141322280421E-4],
        [0.177071690559387,9.6313279084485E-5],
        [0.197567343711853,9.06740174149022E-5],
        [0.217912197113037,8.41605542886137E-5],
        [0.236381888389587,7.64914233275134E-5],
        [0.25864452123642,6.53056183246651E-5],
        [0.276517570018768,4.92454779268515E-5],
        [0.297675430774689,3.19965560026843E-5],
        [0.317564606666565,1.06382249581693E-5],
        [0.338299572467804,-1.70514439091538E-5],
        [0.357877314090729,-5.28804581574719E-5],
        [0.375337302684784,-1.02587420530994E-4]
      ],
      "parameters":{
        "voc":{"value":0.326015792543873,"unit":"V"},
        "jsc":{"value":0.115310649809229,"unit":"mA/cm^2"},
        "v_mpp":{"value":0.217405427060398,"unit":"V"},
        "j_mpp":{"value":0.0843552348199183,"unit":"mA/cm^2"},
        "p_mpp":{"value":0.0183392858508045,"unit":"mW/cm^2"},
        "r_series":{"value":764.409924295598,"unit":"Ohm"},
        "r_shunt":{"value":107060.329453377,"unit":"Ohm"},
        "fill factor":{"value":48.7836579615014,"unit":"%"},
        "efficiency":{"value":0.0183392858508045,"unit":"%"}
      }
    },
    {
      "name":"reverse",
      "data_schema":[
        {"name":"Voltage","unit":"V"},
        {"name":"Current","unit":"mA/cm^2"}
      ],
      "data":[
        [0.375275015830994,-1.03358969543919E-4],
        [0.356238186359406,-5.41851376042222E-5],
        [0.336988270282745,-1.99588260265312E-5],
        [0.31677782535553,9.65143695022121E-6],
        [0.298252403736115,3.27614822773018E-5],
        [0.276038944721222,4.8831556782578E-5],
        [0.257329940795898,6.42294233495539E-5],
        [0.239083170890808,7.60079634310019E-5],
        [0.21613210439682,8.56572931463068E-5],
        [0.197472274303436,9.06044786626642E-5],
        [0.177068412303925,9.52105931561403E-5],
        [0.156969428062439,9.96279596078275E-5],
        [0.139247179031372,1.05005623114229E-4],
        [0.116850137710571,1.07118276634602E-4],
        [0.0983411073684692,1.09764060588798E-4],
        [0.0770717859268188,1.09906449462428E-4],
        [0.0582841038703918,1.14234408946952E-4],
        [0.0381425023078918,1.14267522638494E-4],
        [0.0166600942611694,1.13376764336018E-4],
        [-8.78572463989258E-4,1.15198017370821E-4],
        [-0.0227215886116028,1.13833733279296E-4],
        [-0.0415584444999695,1.16145068948919E-4],
        [-0.0621262192726135,1.17290802676268E-4],
        [-0.0819596648216248,1.18234542885212E-4],
        [-0.101848840713501,1.17469616610594E-4]
      ],
      "parameters":{
        "voc":{"value":0.323545980753277,"unit":"V"},
        "jsc":{"value":0.115167594537622,"unit":"mA/cm^2"},
        "v_mpp":{"value":0.222084747509015,"unit":"V"},
        "j_mpp":{"value":0.0836156568083621,"unit":"mA/cm^2"},
        "p_mpp":{"value":0.0185697620300856,"unit":"mW/cm^2"},
        "r_series":{"value":705.15973836992,"unit":"Ohm"},
        "r_shunt":{"value":87558.7731630702,"unit":"Ohm"},
        "fill factor":{"value":49.8356392236295,"unit":"%"},
        "efficiency":{"value":0.0185697620300856,"unit":"%"}
      }
    }
  ]
}
```