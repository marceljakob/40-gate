1. Routing table check
2. 	Verify services are open (traffic to the FortiGate)
3. 	Check forward traffic logs
4. 	Sniffer trace
5. 	Debug flow
6. 	Session list

### Routing
```
get router info routing-table all
get router info routing-table details <destination-ip>
```
### FortiGate Itself
Only relevant for traffic terminating on the box (management, VPN, BGP on loopback).
```
show system interface <interface>          # look at set allowaccess
diagnose sys tcpsock                       # listening sockets
show firewall local-in-policy
diagnose firewall iprope list 100024       # local-in policy table
```
Local-in policies are a frequent silent blocker. They do not appear in forward traffic logs.

### Logs

### Sniffer
```
diagnose sniffer packet <interface|any> '<filter>' <verbosity> <count> <timestamp>
```
**Verbosity levels:**
- (1) print header of packets
- (2) print header and data from IP of packets
- (3)print header and data from Ethernet of packets
- (4) print header of packets with interface name
- (5) print header and data from IP of packets with interface name
- (6) print header and data from Ethernet of packets with interface name
- Timestamp: a = absolute UTC, l = absolute local time.

**Practical examples:**
```
Basic - is the packet arriving at all, on which interface
diagnose sniffer packet any 'host 10.1.1.10' 4 0 l

Full capture for Wireshark conversion
diagnose sniffer packet any 'host 10.1.1.10 and host 8.8.8.8' 6 0 l

ICMP only
diagnose sniffer packet any 'icmp and host 10.1.1.10' 4 0 l

Specific port
diagnose sniffer packet any 'host 10.1.1.10 and port 443' 4 0 l

One direction only
diagnose sniffer packet port1 'src host 10.1.1.10' 4 0 l

Exclude your own SSH session from the output
diagnose sniffer packet any 'not port 22' 4 0 l
```
if you see the packet arrive on the ingress interface but never leave on the expected egress interface,
the FortiGate dropped it — move to debug flow to find out why.

### Debug Flow
