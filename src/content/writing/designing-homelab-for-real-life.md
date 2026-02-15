---
title: "Designing My Homelab for Real Life"
description: "How I designed my homelab to run real-life infrastructure — with network segmentation, Proxmox, DNS redundancy, and layered backups."
pubDate: 2026-02-12
heroImage: "/images/homelab-for-real-life-hero.png"
draft: false
tags: ["infrastructure", "homelab", "self-hosting", "network", "proxmox", "backup"]
---
Most homelabs start as experimentation.

Mine did too.

It began as a place to learn — to break things, rebuild them, and understand how everything fits together.

But over time it stopped being just a lab.

It became where my family’s photos live.  
Our backups.  
My media library.  
Our DNS.  
Our VPN.  
Our internal services.

If it breaks, it’s not just a fun Saturday project.

It’s a household meltdown when your wife and kids’ devices suddenly stop working.

---

## The Philosophy

Before talking about VLANs and hypervisors, here’s the mindset that shaped everything:

I want things to fail gracefully.

If one service dies:

- DNS should still work.
- Backups should still exist.
- The network should still function.
- My family should still be able to use their devices without even noticing something broke.

That way, problems become maintenance tasks — not emergencies I have to deal with at inconvenient times.

---

## Network Architecture

I run network segmentation across the house.

Once you start hosting sensitive data and critical services at home, you can’t really treat everything as “just another device” on the network.

I don’t want a random smart plug or budget IoT gadget having visibility into the same space as my servers.

### VLAN Layout

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

Each VLAN has:

- Controlled firewall rules
- Explicit access paths
- No unnecessary lateral movement

IoT devices stay isolated.  
Guest devices stay contained.  
Infrastructure stays separate.

That way if something behaves strangely, it’s contained — and I don’t have to worry about one device causing problems for everything else.

---

## Compute Layer — Proxmox

The entire lab runs on:

**Proxmox Virtual Environment**

Why Proxmox?

- ZFS support
- Lightweight containers
- Full VMs when isolation matters
- Easy backups
- A web UI that doesn’t get in the way

It does what I need without friction.

### How I Actually Run Things

I’m not precious about LXC vs VM.

I use whatever causes the least headaches.

- **LXCs** for lightweight services

  - Pi-hole  
  - Reverse proxy  
  - Small infrastructure services  

- **VMs** for isolation-heavy workloads and anything Docker-related

  - Media stack  
  - Nextcloud  
  - Monitoring  
  - Authentication services  

I tried the whole “Docker in LXC” thing.

It works… until it doesn’t.

Permissions get weird.  
Networking gets weird.  
Mounts get weird.

Running Docker inside its own VM is just simpler.

---

## DNS — The Quiet Hero

If DNS breaks, everything breaks.

Nothing loads.  
Nothing connects.  
It just feels like “the internet is down”.

So I don’t treat DNS like an afterthought.

It’s critical infrastructure.

I run Pi-hole for filtering, with Unbound on the router so I’m not sending all my DNS queries to someone else.

My primary Pi-hole runs on the main server.

Which is fine — until I need to reboot that server.

And I don’t want the whole house losing connectivity just because I’m doing maintenance.

So I run a secondary Pi-hole as a fallback, with a virtual IP for failover.

If one node goes down:

- Devices keep resolving
- The network doesn’t feel offline
- Nobody in the house notices

---

## Storage Strategy

Storage has been the biggest lesson so far.

When I first built the system, everything lived on the same pool.

Media.  
Photos.  
Nextcloud.

All treated equally.

At the time it felt clean and simple.

In reality, not all data deserves the same protection.

Some data is replaceable.

Some data isn’t.

So the layout is changing.

The plan going forward looks like this:

- `/tank` — striped storage for replaceable data (mostly media)
- `/flash` — fast NVMe for root disks and databases
- `/vault` — mirrored ZFS for things that actually matter

Media can be rebuilt.

My Immich library, polished music collection, and Nextcloud data cannot.

The system assumes drives will fail.

Because eventually they do.

I’ll write properly about the RAID decisions and why I’m restructuring in another post — that one deserves its own deep dive.

---

## Backup Overview

Backups aren’t one-size-fits-all.

Some data follows the classic 3-2-1 rule.

Some doesn’t.

It depends what it is.

VMs and containers are backed up to a separate machine running Proxmox Backup Server.

That machine then syncs to OneDrive.

For most workloads, that’s more than enough.  
I’d be very unlucky to lose the main server, the backup server, and the cloud copy all at the same time.

Photos are treated differently.

My photo library lives on the main server.  
It’s backed up to Proxmox Backup Server.  
That backup is synced to OneDrive.

But I don’t stop there.

I also keep:

- A manual photo archive on an old external HDD
- A second cloud copy using my Proton Drive storage

Because some data isn’t just “data”.

It’s memories.

And those deserve layers.

---

## The Big Picture

None of this is particularly flashy.

It’s just structured.

Some parts evolved.  
Some parts were rebuilt.  
Some parts I’d do differently if I started again.

But everything now has:

- A purpose
- Clear boundaries
- A way to recover when it breaks

None of it is there for the sake of it.

It’s there because it solves a problem, or makes something more reliable.

And when other people in the house rely on it, you naturally think a bit more carefully about how it’s put together.

---

### What’s Next

I’ll go deeper into each part over the next few posts.

This was just the structure.
