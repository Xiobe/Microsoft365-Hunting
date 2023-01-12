# Looking for incoming connections

```
DeviceNetworkEvents
| where RemoteIP in ("<IP_address_1>","<IP_address_2>",...,"<IP_address_n>")
| where ActionType == "InboundConnectionAccepted"
| where Timestamp > ago(30d)
| project Timestamp, DeviceID, DeviceName, RemoteIP, RemotePort, LocalIP, LocalPort, InitiatingProcessFileName
```
