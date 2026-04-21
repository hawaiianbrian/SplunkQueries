index=network sourcetype=firewall OR sourcetype=proxy
| bucket _time span=5m
| stats count by src_ip, dest_ip, _time
| stats avg(count) as avg_count, stdev(count) as stdev_count by src_ip, dest_ip
| where stdev_count < 2
