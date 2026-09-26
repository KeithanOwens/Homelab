# Homelab

My Homelabbing experience.

Documenting how I built and troubleshooted my home network and server infrastructure, from the physical wiring up through the services running on top of it.

## Contents

- [Internet Setup & Solution](01-the-problem/coax-rental-internet.md)
  Diagnosing and fixing a throughput bottleneck across coax, MoCA, and in-wall Ethernet wiring at a rental.

- [Hardware](02-hardware/hardware-overview.md)
  What's actually running the network and homelab right now, and why I picked each piece.

- [Network Architecture](03-network-foundation/network-topology.md)
  Current network diagram plus the planned OPNsense migration.

## What's next

The current phase is running self-hosted services (Pi-hole, Vaultwarden, Caddy, Uptime Kuma, Grafana) on a Proxmox host behind the ISP's stock router. The next phase is replacing that stock router with OPNsense for real firewall rules and VLAN segmentation. More sections will get added here as that work happens.
