# Uptime-Kuma-Docker

## Docker config:


1) Change GATEWAY, SUBNET, and IP variables to suit environment availability.

2) If running HAProxy on same system as docker containers, set the exp port variable to 127.0.1.1:port

3) If running IPTables firewall in Drop all by default with HAProxy on the same system, make sure to add the following:
```text
# This ensures communication because HAProxy and Docker don't play nice with Drop all by default
-A INPUT -i uptimekuma -p tcp -m tcp --sport 3001 -m conntrack --ctstate NEW,ESTABLISHED -j ACCEPT
-A INPUT -i uptimekuma -m conntrack --ctstate RELATED,ESTABLISHED -j ACCEPT
-A OUTPUT -o uptimekuma -m conntrack --ctstate NEW,ESTABLISHED,RELATED -j ACCEPT
```
