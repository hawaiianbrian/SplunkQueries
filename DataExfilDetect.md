index=network sourcetype=firewall
| stats sum(bytes_out) as total_bytes by src_ip, dest_ip
| where total_bytes > 1000000000
