# Hardware

This is what's actually running my homelab and home network right now.

| Component | Role |
|---|---|
| Lenovo ThinkStation P710 | Proxmox host, runs all self-hosted services |
| Xfinity XB10 Gateway | Modem/router (stock mode) |
| TP-Link TL-SG108E | Unmanaged switch, distributes Ethernet to each room |
| MoCA Adapter + Amphenol MoCA 2.5 Splitters | Bridges Ethernet over coax between rooms |

---

## Lenovo ThinkStation P710
This is the main box everything runs on. It's running **Proxmox VE** as the hypervisor, and every self-hosted service I have lives on it as its own isolated container or VM instead of being spread across separate machines:

- Pi-hole
- Vaultwarden
- Caddy
- Uptime Kuma
- Prometheus / Grafana

I picked this route because it lets me experiment with new services without risking anything else breaking, and it's a lot more resume-relevant than just running everything directly on one OS.

## Xfinity XB10 Gateway
This is the ISP-provided modem/router combo, currently running in its **normal stock mode**. It's handling routing, DHCP, and WiFi for the whole house right now.

> This is a known limitation. It means the ISP's hardware is making the routing decisions instead of me, which is exactly why the next phase of this project is replacing its routing role with OPNsense.

## TP-Link TL-SG108E Switch
An unmanaged 8-port switch that takes the Ethernet signal coming out of my MoCA adapter and fans it out to the wall jacks in each room through the patch box.

I originally had these jacks wired into a telephone input module that couldn't pass Ethernet at all, so swapping in this switch was part of actually getting wired internet working around the apartment. Full story: [Incident Report](../01-the-problem/coax-rental-internet.md).

## MoCA Adapter + Amphenol MoCA 2.5 Splitters
Since my router and the patch box are in different rooms, I use a **MoCA adapter** to send an Ethernet signal over the existing coax wiring instead of running new cable through the walls.

The splitters matter more than I expected here:

- The original splitters could technically pass the right frequency range **on paper**
- They weren't actually rated for MoCA
- That mismatch was quietly killing a lot of throughput
- Swapping to **Amphenol** splitters that are properly MoCA-rated fixed it

---

## Planned additions
*Not part of the current setup yet. Coming as part of the OPNsense project:*

- [ ] Managed switch with VLAN support
- [ ] USB-to-Ethernet adapter (third NIC for the ThinkStation)
- [ ] Access points via Omada controller

None of this is built yet. It's the next phase after everything listed above.
