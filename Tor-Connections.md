#  TOR Connections: Unique Source
```yaml

index=FW (app="Tor*" OR app=Tor-Relay.Node) OR apprisk=critical 
| dedup srcip
| stats count by src_ip
| stats sum(count)
