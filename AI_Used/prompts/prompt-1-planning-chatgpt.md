# Prompt 1 — planning (sent to ChatGPT)

Used to turn the course brief into an ordered specification and to decide what to
study. No project code came out of this step.

---

**Course brief (from the project sheet):**

> TLS Fingerprinting. Build a tool that passively captures TLS ClientHello and
> ServerHello messages and computes JA3/JA3S fingerprints (with JA4/JA4S as a
> stretch goal) to identify the client or server application/library generating
> the traffic. Curate a small reference database and demonstrate distinguishing
> real clients (browsers, curl, custom scripts) purely from their handshake
> fingerprint.
>
> Tools/Technologies: libpcap/Scapy (or raw sockets) for capture; fingerprint
> computation implemented per the JA3/JA4 specifications, eBPF/XDP, Packet/Flow
> Generators like TRex, KV-stores (Redis, Valkey).
>
> Expected Outcome: Demonstrate the working JA3/JA3S fingerprint extractor,
> validated against published reference JA3 hashes for known clients; a curated
> database correctly identifying at least 5 distinct clients/tools by fingerprint
> alone. Demonstrate distinguishing, e.g., curl vs. a browser vs. a custom TLS
> client on the wire. Understanding of the fingerprinting's role in security
> monitoring (malware C2 detection, client identification) and its limitations,
> including fingerprint randomization in modern browsers as an evasion technique.

**Our request:**

This is my CN project. I need to do the above whole thing.

1. I do not have any idea about CNs and what all these above topics are, so along
   with the project I need a simple-language, complete end-to-end guide (md file)
   where I can study these topics individually myself, then the project structure —
   what is required, what is built, all of it — in simple, proper language. A good,
   well-organised md file, good documentation.
2. I want this done end to end as far as possible, and then a full step-by-step
   guide to execute it on my Mac — every terminal command required, properly laid
   out. Any software that is required should come with a proper step-by-step install
   guide (libpcap/Scapy or raw sockets for capture; fingerprint computation per the
   JA3/JA4 specs; eBPF/XDP; packet/flow generators like TRex; KV-stores like Redis,
   Valkey).
3. Give me a good, proper prompt for the above so I can hand it to a coding tool and
   have it work through the task cleanly in one go. Also tell me which model and
   thinking level I should use (I have the Pro version).
