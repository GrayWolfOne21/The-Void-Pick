# The-Void-Pick
An open-source, non-custodial Stratum V2 mining orchestrator featuring asynchronous shadow-routing, Tor obfuscation, and local block template construction
# The Void Pick

**A Decentralized, Non-Custodial Stratum V2 Mining Orchestrator**

## Overview
The cryptocurrency mining ecosystem is currently facing a critical centralization and regulatory crisis. Over 90% of global block templates are constructed by a handful of centralized mining pools, creating an immediate vulnerability to transaction censorship. Furthermore, these pools operate on custodial payout models, exposing independent miners to KYC/AML regulatory overreach and sudden asset freezes. 

The Void Pick resolves both vulnerabilities. It is an open-source, local mining orchestrator governed by a strict state-machine architecture that automatically hunts for hardware profitability while enforcing Stratum V2 Job Negotiation and non-custodial payouts. By stripping block-building power away from centralized pool operators and routing rewards directly to cold storage, The Void Pick restores censorship resistance and privacy to the independent miner.

## Core Architectural Innovations
The orchestrator operates as a localized hardware management "brain" via a lightweight Python backend and HTML/JS frontend, utilizing the following advanced feature sets:

* **Stratum V2 Template Override:** The system runs a local mempool, constructing its own block templates to negotiate with the pool. This explicitly strips the pool operator of the ability to censor transactions.
* **Non-Custodial Payout Routing:** The state machine filters out custodial pools, prioritizing protocols (e.g., Ocean, P2Pool) that write the miner's wallet address directly into the block coinbase transaction, completely bypassing third-party ledger platforms.
* **Network Obfuscation (Tor Integration):** All outbound Stratum connections are automatically routed through a local Tor proxy (SOCKS5) or VPN interface to shield the hardware's IP address and physical location.
* **Asynchronous Shadow-Routing:** To eliminate switching latency, the orchestrator evaluates market profitability concurrently. When a pivot is required, it pre-compiles execution arguments and pre-warms the pool connection, terminating the active subprocess only the exact millisecond the new one launches.
* **Graph-Theoretic Edge Trimming:** The system actively prioritizes memory-hard algorithms (e.g., Cuckoo Cycle) capable of mathematical edge trimming, discarding dead computational paths before fully processing them to maximize hardware efficiency without draining raw CPU/GPU power.

## Technical Framework
The project repository is structured for immediate modular deployment and community contribution. 
1. **Backend State Machine:** A localized server executing a continuous, fault-tolerant loop transitioning between dynamic states (`[EVALUATE]`, `[EXECUTE_MINER]`, `[VOID_DREDGE]`, `[THERMAL_THROTTLE]`). 
2. **Live Mainframe UI:** A single-file HTML/CSS dashboard utilizing WebSockets to stream real-time `stdout`/`stderr` terminal output from the mining subprocess, featuring live thermal monitoring and a manual hardware kill switch.
3. **Agent-Ready Skill Configuration:** The logic is packaged with an autonomous agent skill file (`void_pick_skill.yaml`), allowing the state machine to be seamlessly ingested into local LLM frameworks for autonomous management.

## Project Roadmap & Funding Milestones
**Phase 1: Architecture Validation & UI Integration**
* Finalize the state machine transitions and local HTML dashboard telemetry.
* Deploy backend hardware monitoring (thermal limits, load balancing).
* Open-source the foundational GitHub repository for community review.

**Phase 2: Stratum V2 & Obfuscation Deployment**
* Integrate the Tor proxy routing directly into the execution subprocess.
* Finalize the Stratum V2 Job Negotiation logic to allow local block template construction.
* Launch public beta and extensive stress testing across varying hardware profiles.

## Core Team
* **Andrew** — Lead Architect & Systems Engineer. Specializes in strict state-machine architecture, system directives, and compliance engines. Founder and developer of Loretta Compliance, utilizing advanced logic frameworks to dictate hardware and software operational routing. 
* **Danny Marshall** — Lead Software Developer. Manages application programming, database integration, and code repository structuring, ensuring the Python backend and JavaScript frontend operate seamlessly with the architectural state machine.
