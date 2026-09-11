# Prompt 2 — implementation specification (sent to Claude Code)

The main prompt. This is the specification we wrote: scope, technology,
architecture, correctness rules, testing, documentation and the development phases.
Reproduced verbatim.

---
Build a simple, beginner-friendly **TLS Fingerprinting using JA3/JA3S** project in Python with Scapy.

**Scope:** Build the MVP first: PCAP/live capture, ClientHello/ServerHello parsing, JA3/JA3S, a small JSON fingerprint database, matching, CLI, 5 client experiments, tests, and documentation. Do not add JA4/JA4S, eBPF/XDP, TRex, Redis/Valkey, or other unnecessary technologies until the MVP works.

**Architecture:** Keep a simple modular pipeline:

`PCAP/Capture → Parser → ClientHello/ServerHello → JA3/JA3S → Database → Matcher → CLI`

Use PCAPs as the main reproducible input. Follow the published JA3/JA3S specifications exactly, including GREASE, ordering, formatting, and hashing. Never invent fingerprints, captures, results, or benchmarks; mark anything not executed as `USER MUST VERIFY` or `NOT EXECUTED`.

Create reproducible experiments for curl, browser, Python TLS, OpenSSL, and another/custom client. Clearly distinguish measured results from published references.

Add unit and integration tests and ensure `pytest` passes. Keep documentation beginner-friendly: study guide, macOS setup, experiments, viva questions, project report, README, and project status.

Work incrementally in tested phases. Keep the implementation **small, reliable, understandable, and academically defensible**.
