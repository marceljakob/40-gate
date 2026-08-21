### Debug:
```
  _diagnose debug reset_  
  _diagnose ip router bgp all enable_  
  _diagnose ip router bgp level info_  
  _diagnose debug enable_
```
<br/><br/>
### Get Overview:
```
  _get router info bgp summary_  
  _get router info bgp neighbors_
```
  
  - Idle: Initial state
  - Connect: Waiting for a successful three-way TCP connection
  - Active: Unable to establish the TCP session
  - OpenSent: Waiting for an OPEN message from the peer
  - OpenConfirm: Waiting for the keepalive message from the peer
  - Established: Peers have successfully exchanged OPEN and keepalive messages.
<br/><br/>
### Checking Received and Advertised Prefixes:
```
_get router info bgp neighbors "IP address of neighbor" received-routes_  
_get router info bgp neighbors "IP address of neighbor" advertised-routes_
```
<br/><br/>
### Restart BGP:
To force a full exchange of BGP routing tables between peers:
It’s also possible to perform a soft reset (without interruptions) by using the following command:
```
_execute router clear bgp ip "IP address of neighbor>"_    
_execute router clear bgp all soft (in/out)_  
_execute router clear bgp ip "IP address of neighbor" soft (in/out)_
```
  - in: refresh only received BGP routes.
  - out: refresh only advertised BGP routes.
