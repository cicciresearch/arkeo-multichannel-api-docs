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

| **Parameter** | **Description**  				| **Example** | **Data Type** |
| ------------- | ----------------------------- | ----------- | ------------- |
| index         | Channel index 				| 0           | Integer       |
| enable        | If channel is enabled 		| true        | Boolean       |
| user          | Name of the user  			| User        | String        |
| device        | Name of the device  			| Sample      | String        |
| measurement   | State of the Measurement  	| jv[^1]      | String        |
| direction     | Current direction of the JV 	| forward[^2] | String        |
| state         | Current state of the channel	| running[^3] | String 		  |


[^1]: Options: `jv`, `tracking`
[^2]: Options: `forward`, `reverse`
[^3]: Options: `idle`, `ready to start`, `running`, `stopped`, `error`
