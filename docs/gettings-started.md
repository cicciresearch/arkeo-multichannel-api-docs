The following sequence of commands can be used to perform a basic MPPT measurement. In this example, channels 0, 1 and 2 are configured and measured. Note that most [device commands](commands/device.md) require the `indices` field.

```json
{ "command": "GetIV"} //ensure IV channels are read correctly
{ "command": "SetChannelSettings", "indices":[0,1,2], "parameter": { ... JSON settings string ...}  }
{ "command": "GetChannelState", "indices":[0,1,2]} //Ensure settings are loaded. State should be "ready to start"
{ "command": "StartMeasurement"} //Ensure settings are loaded. State should be "ready to start"
{ "command": "GetChannelState", "indices":[0,1,2]} //Poll until "measurement" == "Tracking"
{ "command": "GetLatestJV", "indices":[0,1,2]} 
{ "command": "GetIV"} //Poll periodically during tracking phase to monitor device
{ "command": "StopChannel", "indices":[0,1,2]} 
```

## Notes
`#!json "GetIV"` can be periodically polled in the background. It doesn't affect any device channels. It can be used as a sanity check to ensure that ADCs are running.

`#!json "SetChannelSettings"` Can be used both before and during a measurement to change the settings of a channel. Note that any fields not included in the JSON are ignored and those settings will not be affected.

`#!json "GetChannelState"` Use this to monitor the measurement state of the device. If no measurements are running, after applying settings, the `"state"` field will be `"ready to start"`. Whereas, if a measurement was already running and another channel is added, the state will immediately go to `"running"`.

`#!json "StartMeasurement"` This command should only be called if no channels are currently running.

`#!json "GetChannelState"` If tracking is not enabled, the channel will stop automatically after a JV

`#!json "GetLatestJV"` Retrieves the JV scans as an array of all selected channels. Can be called during a JV to retrieve the incomplete scan.

`#!json "GetIV"` Monitor the tracking state (voltage, current and power) with this command