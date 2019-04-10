netstat-based-network-map
=========================

#### Runs netstat (it actually access /proc/net/tcp and /proc/net/tcp6 directly) on client machines and send results to an aggregator server, which then builds a network-map based on the private-network connections. ####

*netstat_monitor.py* should be installed on machines to be monitored. This version is configured to collect TCP connections (IPv4 and IPv6) each 2 seconds, consolidate them, and send to the aggregator server each 10 seconds.  
For now data are being saved locally in a berkleydb key-value file for each client.  
**TODO:** timeouts, retries, failure detection, minimum connections

*netstat_aggregator.py* is the HTTP server that receives data from all clients and builds the network-map (currently also using berkleydb).  
**TODO:** this should be behind a VIP/load balancer, and use a distributed database

*netstat_ui.py* is a PoC HTTP server that displays the network-map build by the aggregator. A stronger line is used based on how many connections have been detected in the period.  
**TODO:** so much

Notes: 
- excited to found someone who had same idea as me about utilizing netstat as a source of information on server hierarcy. While this solution is client - server oriented, I think towards agentless (a.k.a. pull) realization, when there is an ssh connection from server to client, information gathering and fetch process, with further accumulation it on server. After that it can be visualized;
- read that graphviz can visualize arbitrary data : https://www.linuxquestions.org/questions/linux-networking-3/build-graphical-network-map-from-netstat-output-710199/

