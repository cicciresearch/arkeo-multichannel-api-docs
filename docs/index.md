# Introduction

This API facilitates remote control of the Arkeo Multichannel using TCP on port ```6340```, enabling users to perform a variety of commands manage measurements.

A command must sent as a JSON string in the form  
```json
{'command': command, 'parameter': parameter}
```

Each command must be preceded by a 4-byte integer indicating the total length of the command. After each command, a reply is always sent back. Its format depends on the command (see list below). If an unknown command is sent, the string “Not a valid command” is send instead.

---
# Summary of available commands
| **Command**                                                | **Description**                                                 |
| ---------------------------------------------------------- | --------------------------------------------------------------- |
| [SetActiveChannel](commands.md#setactivechannel)           | Set the channel upon which all subsequent actions are performed |
| [GetActiveChannel](commands.md#getactivechannel)           | Get the active channel                                          |
| [SetChannelSettings](commands.md#setchannelsettings)       | Modify the settings                                             |
| [GetChannelSettings](commands.md#getchannelsettings)       | Retrieve the settings                                           |
| [StartChannel](commands.md#startchannel)                   | Start measurement                                               |
| [StopChannel](commands.md#stopchannel)                     | Stop the measurement process                                    |
| [ForceJV](commands.md#forcejv)                             | Force a JV measurement                                          |
| [GetChannelState](commands.md#getchannelstate)             | Retrieve the current state                                      |
| [GetLatestJV](commands.md#getlatestjv)                     | Get the voltage and current of last performed JV                |
| [GetIV](commands.md#getiv)                                 | Get the live voltage and current of all channels                |
| [GetSensorsInfo](commands.md#getsensorsinfo)               | Retrieve sensor configuration                                   |
| [GetSensors](commands.md#getsensors)                       | Get the live sensor values of all connected sensors             |
| [SetChannelEnvironment](commands.md#setchannelenvironment) | Associate a channel to an environment                           |
