# Attack Surface Categories

## Visualization of last 7 days

This query considers the categorization of attack surface rules. It is a query that is supposed to run on a daily basis for reporting purposes.
source: [https://github.com/Azure/Azure-Sentinel/tree/master/Hunting%20Queries](https://github.com/Azure/Azure-Sentinel/blob/master/Hunting%20Queries/Microsoft%20365%20Defender/ASR%20rules/ASR-rules-categorized-detection-graph.yaml)

```Text
DeviceEvents
   | where Timestamp > ago(7d)
   | where ActionType startswith "asr"
   | extend Parsed = parse_json(AdditionalFields)
   // | where Parsed.IsAudit == "true" 
   | where Parsed.IsAudit == "false" 
   | summarize Email = countif(ActionType in ("AsrExecutableEmailContentBlocked", "AsrOfficeCommAppChildProcessBlocked")),
               Script = countif(ActionType in ("AsrObfuscatedScriptBlocked", "AsrScriptExecutableDownloadBlocked")),
               WMI = countif(ActionType in ("AsrPersistenceThroughWmiBlocked", "AsrPsexecWmiChildProcessBlocked")),
               OfficeApp = countif(ActionType in ("AsrOfficeChildProcessBlocked", "AsrOfficeMacroWin32ApiCallsBlocked", "AsrExecutableOfficeContentBlocked", "AsrOfficeProcessInjectionBlocked")),
               3rdPartyApp = countif(ActionType == "AsrAdobeReaderChildProcessBlocked"),
               WindowsCredentials = countif(ActionType == "AsrLsassCredentialTheftBlocked"),
               PolymorphicThreats = countif(ActionType in ("AsrUntrustedExecutableBlocked", "AsrUntrustedUsbProcessBlocked", "AsrRansomwareBlocked", "AsrVulnerableSignedDriverBlocked")) by bin(Timestamp, 1d)
   | render columnchart
```
