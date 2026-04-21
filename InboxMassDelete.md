index=o365 sourcetype=exchange
| search operation="HardDelete" OR operation="SoftDelete"
| stats count by user
| where count > 100
