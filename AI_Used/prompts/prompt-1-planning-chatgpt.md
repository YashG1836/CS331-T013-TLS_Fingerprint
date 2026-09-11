# Prompt 1 (given to ChatGPT)

This is what i sent to chatgpt at the start, to get a plan and a proper prompt i
could give to claude. copied as i typed it.

---

Project brief from the course sheet:

TLS Fingerprinting. Build a tool that passively captures TLS ClientHello and
ServerHello messages and computes JA3/JA3S fingerprints (with JA4/JA4S as a stretch
goal) to identify the client or server application/library generating the traffic.
Curate a small reference database and demonstrate distinguishing real clients
(browsers, curl, custom scripts) purely from their handshake fingerprint.
Tools/Technologies: libpcap/Scapy (or raw sockets) for capture; fingerprint
computation per the JA3/JA4 specifications, eBPF/XDP, Packet/Flow Generators like
TRex, KV-stores (Redis, Valkey). Expected Outcome: working JA3/JA3S extractor,
validated against published reference JA3 hashes; a curated database identifying at
least 5 distinct clients/tools by fingerprint alone; distinguishing curl vs a
browser vs a custom TLS client on the wire; understanding of fingerprinting's role
in security monitoring and its limitations including fingerprint randomization.

---

this is my CN project , i need to do the above whole thing using claude

1) I do not have any idea about CNs and what all these above topics are so along with
the project i need a simple language written complete end to end guide md file where
i can study myself these all topics individually , thne about the project structure
what is req what is made, all of that in simple easy language propeerly so i need a
good md file for all this, a very good documnetation

2) i want claude to do this everything end to end jitna possible , like after that if
i need to run things on my end then i need a full step by step guid to execute it on
my mac, like every terminal command or what so ever is req by me to do, properly

3) U need to give me good proer prompt for the above thing so i can give the same to
claude so it start proerly working on it and do the task without any mistake in one
go pura aache se, any software that is req i need to have a proper guide that i need
to implement step by step in point 2 , like libpcap/Scapy (or raw sockets) for
capture; fingerprint computation implemented per the JA3/JA4 specifications,
eBPF/XDP, Packet/Flow Generators like TRex, KV-stores (Redis, Valkey).

so give a very good prompt for the above and also tell me which model and complexity
of thinking i should turn on in laude i have pro verisom
