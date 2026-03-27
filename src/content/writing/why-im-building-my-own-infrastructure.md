---
title: "Why I’m Building My Own Infrastructure"
description: "Why I'm building my own infrastructure at home - replacing big tech services with something reliable enough for real life."
pubDate: 2026-02-09
heroImage: "/images/why-infrastructure.png"
draft: false
tags: ["infrastructure", "homelab", "self-hosting", "design", "foundations"]
---
For a long time, I relied on the mainstream services for everything.

Netflix for films.  
iCloud for photos.  
Google for email.  
Spotify for music.  

It was convenient. It worked. I didn’t think about it much.

Until one day our family’s shared iCloud storage started creeping towards the limit. We were on the 2TB plan at £8.99 per month. The next upgrade tier was 6TB at £26.99 per month.

That was the moment it clicked.

Photo and video sizes only increase over time. More devices. Higher resolutions. More memories. The trajectory was obvious: either keep paying more every few years, or accept that our entire family archive lived behind a subscription I didn’t control.

Over time I realised something: I had built my digital life on services I didn’t control. If pricing changed, features were removed, an account was locked, or a product was discontinued — that was it. I had no say.

That didn’t sit right with me.

This site documents what I’m doing about it.

---

## What I’m Trying to Build

I’m not trying to reinvent the internet. I just want a home setup that works properly.

It needs to be:

- Reliable enough for real family use  
- Secure by default  
- Not exposing random services to the public internet  
- Able to survive hardware failure  
- Able to survive me making mistakes  

Most importantly, it has to feel invisible.

If my wife and kids notice the infrastructure, I’ve failed.

---

## The Real Challenge

The hardest part wasn’t technical. It was practical.

Replacing Netflix, Disney+, and iCloud Photos only works if what I build is genuinely better — or at least indistinguishable in day-to-day use.

It has to be fast.
It has to be simple.
It has to just work.

If something buffers, breaks, or needs explaining, the experiment is over. Nobody in my house cares about network diagrams or design principles. They just want to watch something or find a photo.

That constraint shapes every decision I make.

---

## It Didn’t Start Like This

None of this began as “infrastructure”.

It started with downloading films onto a USB stick and plugging it into the TV.

Then I discovered network streaming and ran Jellyfin on a Raspberry Pi. That worked — until it didn’t. The hardware struggled, transcoding was painful, and I’d clearly outgrown it.

So I repurposed an old gaming PC. Removed the GPU, upgraded the RAM, added some hard drives. It wasn’t elegant, but it worked.

Only later — as things grew — did I start thinking about proper segmentation, firewalls, redundancy, and backup strategy.

The principles came after the friction.

---

## What This Site Is

As things evolved, there was more and more to remember.  
How something was configured. Why I made a particular decision. What broke last time — and how I fixed it.

Trying to revisit something months later without notes was painful.

So I started writing things down in Obsidian. Not polished guides — just notes for future me.

Eventually I realised I might as well publish them. If they’re useful to me, they might be useful to someone else too.

This is where I document:

- The architecture  
- The mistakes  
- The trade-offs  
- The improvements  

Some posts will be technical.  
Some will be reflections.  
Some will simply capture things I’ve learned along the way.

I’m building the infrastructure anyway.  
This is where I write it down.

---

## The Goal

At the end of all this, I want:

- My family’s photos stored on infrastructure I control  
- Media streaming without stacking subscriptions
- Backups that I’ve actually restored and verified  
- A network that contains problems instead of spreading them  

Not because it’s trendy or extreme. 

Because it feels better knowing it works — and knowing I built it deliberately.

---

This is the starting point.

Next, I’ll document the actual architecture and design decisions behind the system.
