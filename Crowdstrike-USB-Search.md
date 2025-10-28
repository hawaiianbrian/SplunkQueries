#  Crowdstrike USB Search
```yaml

ComputerName=ComputerNAME event_simpleName=RemovableMediaVolumeMounted 
VolumeDeviceType_decimal=8 
| table _time,ComputerName,VolumeDriveLetter,VolumeFileSystemDriver,VolumeName,
VolumeFuleSystemDevice,VolumeFileSystemDriver,VolumeMountPoint
