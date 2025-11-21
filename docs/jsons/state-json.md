# The JSON state string

The state of a channel is represented in a JSON string. This string is read-only and is obtained using the **Command: GetChannelState**.

Below is an example of a state string. 
```json
{
	"Enable":false,
	"Channel":0,
	"User":"User",
	"Measurement":"JV",
	"Direction":"Forward",
	"State":"Running",
}
```

**Description**


| **Parameter** | **Description**                                                                                                                                       | **Example** | **Data Type** |
| ------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------- | ----------- | ------------- |
| Enable        | Enables or disables the channel                                                                                                                       | true        | Boolean       |
| Channel       | ID of the channel                                                                                                                                     | 0           | Integer       |
| User          | Name of the user                                                                                                                                      | User        | String        |
| Measurement   | State of the Measurement                                                                                                                              | JV          | String        |
| Direction     | Current direction of the JV                                                                                                                           | Forward     | String        |
| State         | Current state of the channel<br>-        Idle<br>-        Ready to start<br>-        Running<br>-        Paused<br>-        Stopped<br>-        Error | Running     | String        |
