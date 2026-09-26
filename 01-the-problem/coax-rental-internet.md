# The Problem: Rental Internet & Physical Layer

## The Situation
When I moved into the apartment, every room had both a coax outlet and a Cat5e+ Ethernet jack. After setting up the ISP router using the coax connection, I tested the Ethernet jacks in every room (Bedrooms 1–4, Kitchen, Living Room) and found no signal coming through any of them. A patch box in the master bedroom is where all the coax and Ethernet lines from every room terminate.

## The Symptom
WiFi speeds off the router were fast and matched the ISP-provided plan (1000Mbps), but every Ethernet jack in the apartment carried no signal at all. This mattered because the XB10 router was located on the second floor, while the living room — where I most needed a wired connection — was on the first floor, on the opposite side of the home. Relying on WiFi alone across that distance capped speeds at around 100Mbps in a WiFi speed test. Since WiFi worked fine, that told me the problem was downstream of the router itself — something in the in-wall wiring or patch box, not the internet connection coming in.

## What I Checked
I started by tracing each Cat5e run back to the patch box and found they were all connected to a Legrand Telephone Input Module (TM1045) — a module designed for distributing telephone lines, not Ethernet data. Plugging its input into the XB10 didn't provide any Ethernet signal to the rooms, which made sense once I recognized it wasn't built to pass Ethernet traffic in the first place.

## Root Cause
There were two separate problems stacked on top of each other:

1. **Wrong device on the Ethernet side.** The in-wall Ethernet jacks were wired into a telephone input module instead of a network switch, so no Ethernet signal could pass through at all, regardless of the coax/MoCA setup.

2. **Insertion loss on the coax side.** After replacing the telephone module with an actual switch fed by a MoCA adapter, speeds in each room still capped around 50Mbps. The splitter, while technically rated for a wide enough frequency range, wasn't MoCA-certified and had high insertion loss at the higher end of that range — the exact frequencies MoCA relies on. That loss was capping throughput even though the splitter's spec sheet looked adequate at a glance.

## The Fix
I restructured the setup so the coax from the street feeds into Amphenol MoCA 2.5–rated splitters (certified for low insertion loss at MoCA frequencies) before reaching the patch box. From there, the MoCA adapter converts the signal to Ethernet and feeds into an uplink port on a TL-SG108E unmanaged switch. The Ethernet jacks that were previously wired into the telephone module now connect into the remaining ports on that switch, delivering Ethernet to every room.

After testing, I found the upstairs jacks (Rooms 1–4) negotiate at 100BASE-TX, capping them at 100Mbps, while the downstairs jacks negotiate at full 1000BASE-T. The downstairs speed is fine for now; the upstairs cap is a separate, still-open question — likely an older cable run or a damaged/miswired pair, since Gigabit requires all four wire pairs while Fast Ethernet only needs two.

## What I'd Do Differently
If I ran into this again, I'd start by replacing the ISP's all-in-one router/modem combo with a separate modem and my own router, placed directly in the patch box. That would let me connect the switch and every room's wiring straight into the router in one location, rather than relying on MoCA to bridge Ethernet from a router in a different room. It would also make testing and isolating individual ports much simpler from the start.
