---
title: "Segmenting My Home Network (Without Overcomplicating It)"
description: "How I segment my home network using VLANs without turning it into an over-engineered mess."
pubDate: 2026-03-14
heroImage: "/images/network-explained.png"
draft: false
tags: ["infrastructure", "homelab", "self-hosting", "network", "VLANs"]
---
Network segmentation is one of those things that can get complicated very quickly.

You start off wanting a bit of separation, and before you know it you’ve got dozens of VLANs, firewall rules everywhere, and no idea how anything actually connects.

---

## What I was trying to achieve

I wasn’t trying to build an enterprise network.

I just wanted:

- My devices separated from everything else  
- IoT devices isolated  
- Services not exposed unnecessarily  
- Something I could actually understand and maintain  

---

## How I’ve split things

I keep it simple.

### Admin network
This is where my personal devices live:

- Laptop  
- Phone  
- iPad  

This network has access to everything.

---

### Family network
Devices used by the rest of the house:

- TVs  
- Consoles  
- General use devices  

More restricted, but still usable without friction.

---

### IoT network
Everything I don’t fully trust:

- Smart plugs  
- Cameras  
- Smart TV's and speakers
- Random Wi-Fi devices  

This network is heavily restricted.

---

### Server network
Where the homelab lives:

- Proxmox  
- Services  
- Containers  

Only accessible where needed.

---

## The important part: rules

The goal isn’t just separation.

It’s controlled access.

I default to:

> deny everything, then allow what’s needed

Examples:

- Admin → full access  
- IoT → no access to other networks  
- Family → limited access to services  

---

## What I’ve avoided

I’ve deliberately avoided:

- Too many VLANs  
- Overly complex firewall rules  
- Trying to solve every edge case  

The more complex it gets, the harder it is to trust and maintain.

---

## What this looks like in practice

Most of the time, I don’t think about it.

Things just work.

And when I do need to change something, I understand exactly where to do it.

---

## Final thought

Network segmentation isn’t about building something impressive.

It’s about building something you can live with.

Simple, predictable, and easy to adjust when you need it.

That’s what I’ve aimed for.
