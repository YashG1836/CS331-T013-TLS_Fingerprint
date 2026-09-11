# Prompt 2 — implementation specification (sent to Claude Code)

The main prompt. This is the specification we wrote: scope, technology,
architecture, correctness rules, testing, documentation and the development phases.
Reproduced verbatim.

---

You are my senior Computer Networks + Python engineer helping me build my CN course
project.

## PROJECT

I need to build:

**TLS Fingerprinting using JA3/JA3S**

The project requirement is:

> Build a tool that passively captures TLS ClientHello and ServerHello messages and
> computes JA3/JA3S fingerprints to identify the client or server application/library
> generating the traffic. Curate a small reference database and demonstrate
> distinguishing real clients such as browsers, curl, and custom scripts purely from
> their handshake fingerprint.

Expected outcome:

* working JA3/JA3S extractor
* validation against reliable published/reference fingerprints where possible
* reference database
* at least 5 distinct clients/tools
* demonstration distinguishing curl, browser, Python/custom TLS client, etc.
* explanation of TLS fingerprinting in security monitoring
* explanation of limitations and fingerprint randomization/evasion

I am working primarily on **macOS** and I currently have very little Computer
Networks knowledge.

---

# VERY IMPORTANT SCOPE RULE

Build the **MVP first**.

The MVP consists ONLY of:

1. passive TLS packet capture OR reading PCAP files
2. TLS ClientHello parsing
3. TLS ServerHello parsing
4. JA3 calculation
5. JA3S calculation
6. local fingerprint reference database
7. fingerprint lookup/matching
8. CLI output
9. experiments with at least 5 clients/tools
10. unit/integration tests
11. complete beginner-friendly documentation

Do NOT unnecessarily implement:

* eBPF
* XDP
* TRex
* Redis
* Valkey
* raw sockets
* JA4
* JA4S

unless the MVP is completely working and I explicitly ask for stretch goals.

These technologies appear in the course description, but they are NOT all required
for the core project.

---

# TECHNOLOGY CHOICE

Prefer:

* Python
* Scapy for packet parsing/capture
* PCAP files for reliable/reproducible testing
* JSON or SQLite for the small fingerprint database

Do not add unnecessary frameworks.

The project should be simple enough for a student to understand and explain in a viva.

---

# FIRST: PLAN THE PROJECT

Before implementing, briefly determine:

1. exact MVP
2. architecture
3. project folder structure
4. dependencies
5. macOS-specific issues
6. experiments required
7. what counts as a successful final demo

Then implement it.

Do not create an enormous architecture.

---

# CORE ARCHITECTURE

Use a simple architecture such as:

```text
PCAP / Live Capture
        |
        v
Packet Parser
        |
        v
TLS ClientHello / ServerHello
        |
        v
JA3 / JA3S Generator
        |
        v
Fingerprint Database
        |
        v
Fingerprint Matcher
        |
        v
CLI Output
```

Keep modules separated and easy to understand.

---

# IMPLEMENTATION REQUIREMENTS

The program must be able to:

### Input

* read a `.pcap` file
* optionally perform live packet capture

### Processing

* identify TCP traffic
* identify TLS handshake packets
* identify ClientHello
* identify ServerHello
* extract fields required for JA3/JA3S
* construct JA3/JA3S strings
* calculate hashes
* lookup fingerprints in the database

### Output

For example:

```text
Flow
--------------------------------
Source: 192.168.1.10:53124
Destination: example.com:443

TLS
--------------------------------
Version: TLS 1.3

JA3
--------------------------------
String: ...
Hash: ...

Identification
--------------------------------
Likely Client: curl
Match: Reference database
```

Clearly distinguish:

* known match
* possible match
* unknown fingerprint

Do not claim that fingerprints provide absolute identity.

---

# JA3 / JA3S CORRECTNESS

Implement JA3 and JA3S according to the actual published specifications/reliable
technical references.

Do not invent the algorithms.

Be careful about:

* TLS version
* cipher suites
* extensions
* elliptic curves / supported groups
* EC point formats where applicable
* ordering
* GREASE handling
* formatting
* hashing

Explain the implementation in comments and documentation.

Create unit tests for JA3/JA3S string construction and hashing.

---

# PCAP-FIRST DESIGN

The most reliable demonstration path should be:

```text
generate TLS traffic
        ↓
capture/save PCAP
        ↓
run analyzer
        ↓
JA3 / JA3S
        ↓
database lookup
```

This must work even without live capture.

Live capture can be an additional feature.

---

# REFERENCE DATABASE

Create a small local database, preferably JSON initially.

Target at least 5 distinct client/tool examples.

Possible sources of traffic:

* curl
* Python TLS client
* browser
* OpenSSL
* another/custom TLS implementation

Do not fabricate fingerprints.

Store useful metadata such as:

```json
{
  "hash": "...",
  "name": "curl",
  "type": "client",
  "library": "...",
  "source": "...",
  "notes": "..."
}
```

Clearly distinguish experimentally measured fingerprints from externally
published/reference fingerprints.

Because fingerprints can vary by software/platform/version, document this limitation.

---

# EXPERIMENTS

Create reproducible experiments for at least 5 clients/tools.

At minimum demonstrate:

1. curl
2. browser
3. Python TLS client
4. OpenSSL
5. custom/another TLS client

For each experiment document:

* how traffic is generated
* how it is captured
* command used
* resulting JA3
* resulting JA3S where available
* lookup result
* comparison with other clients

The important demonstration is:

**different TLS implementations can produce different fingerprints.**

---

# TESTING

Create:

### Unit tests

* JA3 construction
* JA3 hashing
* JA3S construction
* JA3S hashing
* parser edge cases

### Integration tests

```text
PCAP -> parser -> JA3 -> database lookup
```

The project should support:

```bash
pytest
```

and all tests should pass before calling the MVP complete.

---

# DOCUMENTATION

I need documentation because I currently have weak CN knowledge.

Do NOT create a huge number of documents.

Create these only:

## 1. docs/STUDY_GUIDE.md

Teach me from zero:

* networks
* IP
* ports
* TCP
* sockets
* TCP handshake
* packets
* packet capture
* TLS
* certificates
* TLS handshake
* ClientHello
* ServerHello
* TLS extensions
* cipher suites
* passive monitoring
* TLS fingerprinting
* JA3
* JA3S
* security applications
* fingerprint limitations
* GREASE/randomization

For every topic explain:

* simple definition
* simple analogy
* small example
* how it relates to this project

At the end include a short "what I should remember" section.

Also add a section explaining the complete project from:

```text
packet
→ TCP
→ TLS
→ ClientHello
→ JA3
→ fingerprint database
→ client identification
```

Use simple language.

---

## 2. docs/SETUP_MAC.md

Give exact step-by-step macOS instructions.

Assume I am a beginner.

Include commands for:

* checking Python
* installing dependencies
* creating virtual environment
* installing Scapy
* setting up project
* running tests
* finding network interfaces
* capturing traffic
* saving PCAP
* analyzing PCAP

For every important command explain what it does.

---

## 3. docs/EXPERIMENTS.md

Give exact commands for all experiments.

I should be able to follow the file line by line.

---

## 4. docs/VIVA.md

Create around 30–40 likely viva questions.

Include:

* CN basics
* TCP
* TLS
* ClientHello
* ServerHello
* JA3
* JA3S
* fingerprint database
* passive capture
* security applications
* limitations

Answers should be short enough to speak during a viva.

---

## 5. docs/PROJECT_REPORT.md

Create a report skeleton covering:

* Introduction
* Motivation
* Background
* TLS
* TLS fingerprinting
* JA3
* JA3S
* Architecture
* Implementation
* Experiments
* Results
* Security applications
* Limitations
* Future work
* Conclusion

Do not fabricate experimental results.

Use placeholders where I must run experiments myself.

---

# ROOT README

Create a concise professional README.md containing:

* project description
* motivation
* architecture
* features
* installation
* quick start
* example output
* experiments
* testing
* limitations
* future work

---

# MACOS CONSTRAINT

I am using macOS.

Do not assume Linux-only networking features work on macOS.

Do not add eBPF/XDP to the MVP.

Do not require Linux virtualization for the core project.

If a feature is Linux-only, explicitly mark it as optional/stretch.

---

# STRETCH GOALS

After the MVP is fully working, you may suggest:

1. JA4/JA4S
2. eBPF/XDP on Linux
3. Redis/Valkey
4. TRex

But do NOT implement these before the core project is complete.

---

# NO FAKE RESULTS

This is extremely important.

Never invent:

* fingerprints
* hashes
* benchmark numbers
* test results
* packet captures
* browser behavior

If something cannot be tested in your environment, mark it clearly as:

`USER MUST VERIFY`

or

`NOT EXECUTED`

---

# DEVELOPMENT PROCESS

Work incrementally.

### Phase 1

Create project structure.

### Phase 2

Implement packet/TLS parser.

### Phase 3

Implement JA3.

### Phase 4

Implement JA3S.

### Phase 5

Implement fingerprint database and matching.

### Phase 6

Implement CLI.

### Phase 7

Create tests.

### Phase 8

Create experiments and sample workflow.

### Phase 9

Write documentation.

### Phase 10

Run a final audit.

After each major phase, test what was implemented before moving on.

---

# FINAL SUCCESS CRITERIA

Do not consider the project complete until:

* the code runs
* tests pass
* PCAP analysis works
* ClientHello is detected
* ServerHello is detected
* JA3 works
* JA3S works
* reference database works
* at least 5 client/tool experiments are documented
* macOS setup instructions are complete
* beginner study guide exists
* viva questions exist
* final demo procedure exists
* limitations are explained

At the end, create:

`PROJECT_STATUS.md`

with:

| Requirement | Status | Evidence |
| ----------- | ------ | -------- |

Clearly show what is complete and what I still need to execute myself.

Start with the MVP. Keep the implementation small, reliable, understandable, and
academically defensible.
