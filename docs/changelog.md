### v0.1  
Initial version

### v0.2  
Added ForceJV and GetChannelState

### v0.3  
Added GetLatestJV, GetIV and GetSensors

### v0.4  
Reorganized the settings JSON and clarified the documentation  
Added JSON schema validation

### v0.4.1  
Now allows multiple connections in parallel  
Added GetSensorsInfo command  
GetSensors now sends physical values instead of raw voltages  
GetSensors no longer sends all sensor channels, but only configured channels  
Index field in the settings JSON changed from string to integer

### v0.4.2
Added GetEnvironments  
Added SetChannelEnvironment

### v0.4.3  
Added Day-Night object to json settings  
Added GetGlobalDayNight and SetGlobalDayNight