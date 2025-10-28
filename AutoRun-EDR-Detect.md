#  EDR Detections
```yaml

index="EDR"  detectionSource!=CustomerTI  evidence{}.fileName!="Autorun.inf" 
| dedup evidence{}.evidenceCreationTime   
| stats count by evidence{}.evidenceCreationTime 
|  stats sum(count)
