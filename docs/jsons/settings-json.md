# JSON Settings string

The settings of a channel are represented in a JSON string. When using [SetChannelSettings](../commands/device.md#setchannelsettings), this is value that the software expects. It is recommended to use [GetChannelSettings](../commands/device.md#getchannelsettings) to read the actual settings and modify those settings.

Below is an example of a channel settings string. 

```json
{
  "Index":0,
  "Enable":false,
  "User":"User",
  "Device":"Sample",
  "Channel":{
    "VoltageLimit":"10 V",
    "CurrentLimit":0,
    "Inverted":false
  },
  "JV":{
    "Vmin (V)":-0.1,
    "Vmax (V)":0.5,
    "Step (mV)":20,
    "ScanRate (mV/s)":200,
    "VocDetect":true,
    "Overvoltage (%)":0,
    "ScanOrder":"RV then FW"
  },
  "Tracking":{
    "TrackEnable":true,
    "Algorithm":"MPPT",
    "Perturbation (V)":0.02,
    "ConstantOutput":0.2,
    "SaveInterval (s)":10,
    "jvInterval":{"Value":1,"Unit":"min"},
    "TestDuration":{"Value":100,"Unit":"hours"}
  },
  "Cell":{
    "Type":"Cell",
    "Area (cm2)":1,
    "NrCells":1,
    "NrW cells":1,
    "W-cellArea (cm2)":1
  },
  "Day-Night":{
    "Use Global":false,
    "Settings":{
      "enable":true,
      "sensor":2,
      "threshold_value":50,
      "threshold_duration":5,
      "night_algorithm":"Open circuit",
      "night_jv":false
    }
  },
  "Light":{"Irradiance":100,"Unit":"mW/cm2"},
  "Note":""
}
```

---

# JSON Settings — Parameter Description Table

### Description of all settings fields

| **Parameter** | **Description**                 | **Example** | **Unit** | **Type** |
| ------------- | ------------------------------- | ----------- | -------- | -------- |
| Index         | Unique channel identifier       | 0           | —        | integer  |
| Enable        | Enables or disables the channel | true        | —        | boolean  |
| User          | Name of the user                | User        | —        | string   |
| Device        | Device name                     | Sample      | —        | string   |

## **Channel** (object)

| **Parameter**     | **Description**             | **Example** | **Unit** | **Type** |
| ----------------- | --------------------------- | ----------- | -------- | -------- |
| VoltageLimit¹     | Maximum voltage             | 10 V        | V        | string   |
| CurrentLimit      | Current range               | 0           | —        | integer  |
| InvertedStructure | Inverts the applied voltage | false       | —        | boolean  |
??? info "¹ Voltage Limit"
	The voltage limit of each board is 10 V. 20 V can be reached by connecting two boards in series and wiring the positive contacts to the device and the negative contacts together.
## **JV** (object)

| **Parameter**   | **Description**                  | **Example** | **Unit** | **Type** |
| --------------- | -------------------------------- | ----------- | -------- | -------- |
| Vmin (V)        | Minimum voltage                  | -0.1        | V        | float    |
| Vmax (V)        | Maximum voltage                  | 2           | V        | float    |
| Step            | Voltage increment per step       | 20          | mV       | integer  |
| ScanRate (mV/s) | Rate at which voltage is applied | 100         | mV/s     | float    |
| VocDetect       | Enable open-circuit detection    | true        | —        | boolean  |
| ScanOrder²      | Order of scanning                | FW then RV  | —        | string   |
??? note "² ScanOrder enum"
    - `0`: FW then RV  
    - `1`: RV then FW  
    - `2`: Forward only  
    - `3`: Reverse only  
## **Tracking** (object)

| **Parameter**      | **Description**                   | **Example** | **Unit** | **Type** |
| ------------------ | --------------------------------- | ----------- | -------- | -------- |
| TrackEnable        | Enables tracking                  | true        | —        | boolean  |
| Algorithm³         | Algorithm used for tracking       | MPPT        | —        | string   |
| Perturbation (V)   | Voltage differential for tracking | 0.01        | V        | float    |
| ConstantOutput     | Maintain a constant output        | 0.2         | *        | float    |
| SaveInterval (s)   | Time between saved data points    | 10          | s        | integer  |
| jvInterval.Value   | Time between JV scans             | 10          | —        | float    |
| jvInterval.Unit⁴   | Unit for JV interval              | min         | —        | string   |
| TestDuration.Value | Duration of tracking test         | 100         | —        | float    |
| TestDuration.Unit⁴ | Unit for test duration            | hours       | —        | string   |
??? note "³ Tracking Algorithm enum"
    - `0`: Open circuit  
    - `1`: Short circuit  
    - `2`: MPPT  
    - `3`: MPPT-Stab  
    - `4`: MPPT INC  
    - `5`: Fixed Voltage  
    - `6`: Fixed Voltage (no track)  
    - `7`: Fixed Current  
    - `8`: JV  
??? note "⁴ Time Unit enum"
    - `0`: seconds  
    - `1`: minutes  
    - `2`: hours  
## **Cell** (object)

| **Parameter**    | **Description**     | **Example** | **Unit** | **Type** |
| ---------------- | ------------------- | ----------- | -------- | -------- |
| Type⁵            | Cell type           | Cell        | —        | string   |
| Area (cm2)       | Area of the cell    | 1           | cm²      | float    |
| NrCells          | Number of cells     | 1           | —        | integer  |
| NrW cells        | Number of W-cells   | 1           | —        | integer  |
| W-cellArea (cm2) | Area of each W-cell | 1           | cm²      | float    |
??? note "⁵ Cell Type enum"
    - `0`: Cell  
    - `1`: Parallel Module  
    - `2`: Z Module  
    - `3`: W Module   

## **Day-Night** (object)

| **Parameter**      | **Description**                 | **Example**  | **Unit** | **Type** |
| ------------------ | ------------------------------- | ------------ | -------- | -------- |
| Use Global         | Use the global settings         | false        | —        | boolean  |
| enable             | Enable the day-night cycling    | true         | —        | boolean  |
| sensor             | Channel of the sensor           | 1            | —        | integer  |
| threshold_value    | Threshold between day and night | 50           | —        | float    |
| threshold_duration | Delay after threshold is reach  | 5            | min      | float    |
| night_algorithm    | Algorithm during night time     | Open-circuit | —        | string   |
| night_jv           | Perform JV during night time    | false        | —        | boolean  |
???+ Note
	The settings object is ignore if the "Use Global" is enabled
## **Note**

| Parameter | Description                    | Example | Unit | Type   |
| --------- | ------------------------------ | ------- | ---- | ------ |
| Note      | Free-to-use field for comments | —       | —    | string |
|           |                                |         |      |        |

---