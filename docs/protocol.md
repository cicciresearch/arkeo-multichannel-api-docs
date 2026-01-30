# API Protocol

The Arkeo Multichannel API uses a **TCP-based request-response protocol** with **length-prefixed JSON messages**.

External clients connect to a running ARKEO application and exchange structured JSON commands to control measurements, query state, and configure hardware-related subsystems.

This page describes the **wire-level protocol**, independent of any specific target or command.

---

## Transport and connection model

- **Transport**: TCP  
- **Default port**: `6340`  
- **Connection type**: persistent  

The Arkeo Multichannel application acts as a TCP server. Clients establish a connection and keep it open for the duration of their interaction. The protocol is strictly **sequential**: One request is sent and one response is received. Only then may the next request be sent.

---

## Message framing

Every message exchanged (both from and to the client) over the connection is framed as:

```
[4-byte length][JSON payload]
```

The 4-byte length prefix is:

- **Unsigned**
- **Big-endian**
- Specifies the number of bytes of the JSON payload only  
- Does **not** include the 4 bytes of the length field itself

After reading the length prefix, the receiver reads exactly that number of bytes and interprets them as a UTF-8 encoded JSON object.

---

## Request message format

Each request requires the `command` field with a valid command name.  
If a payload is required by the command (for example the `SetChannelSettings` requires a settings JSON), then a `parameter` field must be added.  
Most [device commands](commands/device.md) require the `indices` field to specify on which channels the command should act.

**Example Request**
```json
{
  "command": "SetChannelSettings",
  "indices":[0,1,2],
  "parameter": {
    "settings": "{... JSON settings string ...}"
  }
}
```

**Request fields**

| Field        | Required | Description |
|-------------|----------|-------------|
| `command`    | Yes      | Command name for the selected target |
| `parameter`  | No      | Command payload |
| `indices` | No       | SMU channel indices |

---

## Response message format

Each request always return exactly one response. Every response always includes the `status` field indicating if the request was succesful or not.

If the request was successful, the response can include a payload. The field name depends on the [domain](commands/index.md#command-domain-overview) of the request.

**Example Response**
```json
{
  "status":"ok",
  "channels":[
    {
      "index":0,
      "enabled":true,
      "previous_state":"running",
      "new_state":"stopped",
      "result":"stopped"
    }
  ]
}
```

If a request was **not** successful, an error object is returned. Error objects always include the error code and description.

```json
{
  "status":"error",
  "error":{
    "code":5006,
    "message":"No channel running, enable at least 1 channel"
    }
}
```