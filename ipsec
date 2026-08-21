1. Is Phase 1 up?
diagnose vpn ike gateway list name <p1>
2. Is Phase 2 up (SA=1)?
	diagnose vpn tunnel list name <p1>
3. Is it flapping?
	check created: timers, event log
4. Routing present?
	get router info routing-table all
5. Policy present?
	diagnose debug flow
6. Counters incrementing?
diagnose vpn tunnel list → npu_flag / bytes

*** Summary of all tunnels
get vpn ipsec tunnel summary
get vpn ipsec tunnel details
get vpn ipsec stats tunnel
get vpn ipsec stats crypto

*** Phase 1 (IKE SA)
diagnose vpn ike gateway list
diagnose vpn ike gateway list name <phase1-name>

Look for state: established. If the gateway is missing entirely,
the FortiGate never even started negotiating — check the peer IP,
the interface binding and whether the remote is reaching you at all.

*** Phase 2 (IPsec SA)
diagnose vpn tunnel list
diagnose vpn tunnel list name <phase1-name>
diagnose vpn ike status

Key fields:
- SA: created 1/1 — Phase 2 is up
- SA: created 0/0 — Phase 1 may be up but Phase 2 never completed
- npu_flag=03 — both directions offloaded to NPU
- npu_flag=00 — no offload (expected on VM, or when offload is disabled)
- dec:/enc: counters — if only one side increments, traffic is one-way

*** VPN Troubleshooting:

**get vpn ipsec tunnel summary**

https://community.fortinet.com/t5/FortiGate/Troubleshooting-Tip-IPsec-VPNs-tunnels/ta-p/195955

diagnose debug application ike -1 (Phase 1)

diagnose debug application ike -1 (Phase 2)

diag debug en (aktivieren)

diag debug dis (deaktivieren)


IKE Troubleshooting:

Filter the IKE debugging log by using this command.

**diag vpn ike log-filter name Tunnel_1**

Here are the other options for the IKE filter:

**diag debug app ike -1**

**diag debug enable**




https://community.fortinet.com/fortigate-3/troubleshooting-tip-troubleshooting-bgp-over-ipsec-196409
