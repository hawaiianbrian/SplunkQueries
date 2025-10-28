#  MS Exchange Errors
```yaml

index=MSexchange host=NAME tag=error
| timechart span=15m count by host
