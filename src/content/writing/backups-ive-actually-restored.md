---
title: "Backups That I’ve Actually Restored"
description: "How I back up my homelab in a way that actually works — simple, reliable, and tested through real restores."
pubDate: 2026-03-02
heroImage: "/images/backups.png"
draft: false
tags: ["infrastructure", "homelab", "self-hosting", "network", "proxmox", "backup"]
---
Most backup setups look good until you actually need them.

That’s the problem.

It’s easy to feel safe when everything is automated and ticking along quietly in the background. Jobs are running, storage is filling up, and dashboards are green.

But none of that really matters unless you’ve restored from it.

That’s the only test that counts.

---

## What I care about

I’m not trying to build the most complex or “enterprise-like” backup system.

I just want something that:

- Works reliably without constant attention  
- Survives hardware failure  
- Survives me making mistakes  
- Can be restored quickly without stress  

If restoring data is confusing or fragile, the backup isn’t good enough.

---

## What I’m backing up

I split things into two categories.

### Critical data

Stuff I actually care about losing:

- Photos  
- Documents  
- Nextcloud data  
- Anything personal or irreplaceable  

This is the stuff that needs multiple copies.

---

### Replaceable data

- Media library  
- Downloads  
- Anything I can get again  

This doesn’t get backed up at all.

Everything on `/tank` falls into this category. If I lose it, I lose it.

The main reason is scale. `/tank` is large, and duplicating it would require a significant amount of additional storage for data that can be downloaded again.

It would be annoying and time-consuming to rebuild, but it’s not irreplaceable. I’d rather keep the setup simple than spend money and complexity protecting data I can replace.

---

## How it’s set up

At a high level:

- **Primary server** → running everything day to day  
- **Backup server (PBS)** → separate machine  
- **Cloud backup** → encrypted copy off-site  

Backups run automatically, but I don’t rely on that alone.

---

## The important part: restores

I’ve restored:

- Entire VMs  
- Individual files  
- Configurations after breaking things  

And every time I do it, I learn something.

Usually:

- What took longer than expected  
- What I forgot to include  
- What would be stressful under pressure  

That feedback loop is the whole point.

---

## What I’ve learned

### 1. Backups are only real if you’ve restored them

If you’ve never tested a restore, you don’t have a backup.

You have a theory.

---

### 2. Simplicity wins

The more moving parts involved, the harder it is to trust under pressure.

Simple systems are easier to:

- Understand  
- Debug  
- Restore quickly  

---

### 3. Separation matters

If your backups live on the same machine as your data, you don’t have backups.

You have copies.

---

### 4. Off-site is non-negotiable

Hardware failure is one thing.

Fire, theft, or corruption is another.

You need at least one copy somewhere else.

---

## Where this is now

At this point, I trust it.

I’ve restored enough times — entire VMs, individual files, and configurations — that I know it works when I need it to.

The only thing I’d improve is adding an off-site backup that isn’t tied to a big tech provider. Right now, that’s the only real gap.

Everything else does what it’s supposed to do.

---

## Final thought

Backups shouldn’t feel impressive.

They should feel boring.

Quietly working in the background, and when something goes wrong, you restore what you need and move on.

No panic. No guessing.

That’s where this setup is now.
