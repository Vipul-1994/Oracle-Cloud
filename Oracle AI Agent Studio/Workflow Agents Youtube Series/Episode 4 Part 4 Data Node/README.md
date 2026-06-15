# Episode 4 Part 4 — Data Node

This folder contains configurations for integrating Oracle AI Agent Studio Workflow Agents with Oracle Analytics / OTBI SOAP Web Services.

## Files

| File | Description |
|---|---|
| `SessionID External REST.md` | Generates Oracle Analytics Session ID using SOAP `logon` operation |
| `Run OTBI External REST.md` | Executes OTBI reports using SOAP `executeXMLQuery` operation |

## Workflow

```text
Generate Session ID → Execute OTBI Report → Parse SOAP Response → Use Data in Workflow Agent
```

## Oracle Analytics SOAP Endpoint

```text
/analytics-ws/saw.dll/wsdl/v12
```

## Notes

- Session ID generation is mandatory before report execution.
- Report paths must exactly match OTBI catalog paths.
- Preserve SOAP namespaces exactly as documented.
