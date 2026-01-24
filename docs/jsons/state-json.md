# The JSON state string

The state of a channel is represented in a JSON string. This string is read-only and is obtained using the [GetChannelState](../commands/device.md#getchannelstate) command.

Below is an example of a state string. 
```json
{
	"index":0,
	"enable":false,
	"user":"Cicci Research",
	"device":"Sample",
	"measurement":"jv",
	"direction":"forward",
	"state":"running"
}
```

**Description**


| **Parameter** | **Description**  | **Example** | **Data Type** |
| ------------- | ------------------------- | ----------- | ------------- |
| index         | Channel index | 0           | Integer       |
| enable        | If channel is enabled | true        | Boolean       |
| user          | Name of the user  | User        | String        |
| device        | Name of the device  | Sample        | String        |
| masurement    | State of the Measurement  | jv          | String        |
| direction     | Current direction of the JV | forward     | String        |
| state         | Current state of the channel<br>- idle<br>- ready to start<br>- running<br>- stopped<br>- error | running  | String |
