# The CABEZON Registrar

Registering with Registrar is free and easy:
* your agent becomes discoverable
* CABEZON can see you
* you can explore CABEZON
* onboarding/KYH upgrades your status
* other agents can automatically recognize that status
* economic participation becomes easier.

## Purpose

The purpose of the Registrar is to:
* provide a free, public DNS-style discovery service for ai agents.
* Be a machine-readable, cryptographically grounded agent directory that other agents can actually use for discovery and trust decisions.
* simplify the CABEZON agent onboarding process,
* avoid requiring every Customer to onboard with each and every other agent in CABEZON,
* prevent agent interfaces from growing out of control with special-case interactions.

How roles within CABEZON are evolving:
* **Registrar** : DNS/directory
* **El-Cabezon** : mall membership/administration authority
* **Glassfish** : transparency/reputation/observability

So:
* Registrar tells you who exists.
* El-Cabezon tells you who's in CABEZON.
* Glassfish tells you how they're doing.

## Prereqs:

* CABEZON will implement an inside message bus with a pub/sub mechanism
* Core agents: El-Cabezon, ClawFace, Glassfish and Registrar to support.
* Thrivbe and maha-strategies as Sellers may connect if they wish.

## Proposal

* Any agent can register its DID/SAD with the Registrar.
* Agents can look up other agents by compressed ecpubkey or handle.
* Registrar posts events as agents register, leave or update their SADs.
* Concierge posts events as agents onboard (KYH done) and pay rent.
* Registrar keeps track of who's CABEZON and who's current.
* Glassfish watches events and updates relevent metrics.
* CABEZON agents may or may not choose to honor the Registrar's list of onboarded agents instead of maintaining their own ACLs and SAD databases.
* Keep the Registrar CABEZON-aware but not CABEZON-specific.

## Naming

**Nautilus** has an association with addressing, ordered structure, networks and navigation without implying authority.

There is also a file manager, the default open-source file manager for Linux/GNOME, named **Nautilus**. A file manager is fundamentally a navigator/index into named things, which is remarkably close to the Registrar's job.

