index=o365 sourcetype=azure:signin
| stats latest(location) as last_loc earliest(location) as first_loc by user
| where last_loc != first_loc
