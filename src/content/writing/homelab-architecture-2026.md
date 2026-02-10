---
title: "My Homelab in 2026: Architecture, Goals, and Design Rules"
description: "A practical overview of my home infrastructure: VLANs, Proxmox, DNS, media, and backups — plus the rules I try to follow."
pubDate: 2026-02-09
heroImage: ""
draft: false
tags: ["homelab", "proxmox", "networking", "opnsense", "self-hosted"]
---

## What problem I was solving

I wanted a home setup that’s reliable for family use, secure by default, and easy to expand without everything turning into spaghetti.

## Constraints

- Family services need to “just work” (Jellyfin, DNS, general internet)
- I don’t want random apps exposed to the public internet
- Backups must be testable and restorable, not just “I have a copy somewhere”
- I want segmented networks (VLANs) so IoT/guest stuff can’t wander

## The design

At a high level:

- **OPNsense** as the router/firewall with VLANs
- **Pi-hole** for filtering + a VIP for resilience
- **Unbound** for local DNS / overrides
- **Proxmox** for VMs/LXCs (apps live here, not on random boxes)
- **PBS + off-site** for backups
- Media stack (Jellyfin + *arr) with VPN-routed downloads

## Network / diagram

VLANs (simplified):

**VLAN 10 – Admin**  
Management devices + my main clients

**VLAN 20 – Family**  
Family devices

**VLAN 30 – Servers**  
Proxmox, LXCs, VMs, infrastructure

**VLAN 40 – IoT**  
TVs, smart devices, anything untrusted

**VLAN 50 – Mgmt**  
Network gear / AP management

**VLAN 99 – Guest**  
Guest access to internet only

(Next: I’ll add a proper diagram and a service map.)

## Key config

My “rules of the road”:

- Default deny between VLANs; allow only what’s needed
- DNS is a critical dependency, so it gets redundancy
- Anything exposed remotely goes through a tunnel + authentication
- Backups are only real if I can restore them

## What went wrong

Plenty — I’ll document the mistakes as separate posts because they’re usually the most useful part.

## How I tested it

- Failover tests (DNS VIP)
- Network isolation checks between VLANs
- Restore drills for critical data

## Lessons learned

Simple beats clever. Build the network and DNS foundations first — apps are the easy part.

## What I’d improve next

- Publish the full diagram + list of hosted services
- Write up the Pi-hole VIP setup
- Document remote access (tunnels + SSO) properly
