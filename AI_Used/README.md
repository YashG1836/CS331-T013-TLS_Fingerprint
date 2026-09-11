# AI Usage

We used AI to help build this project. This folder has the tools we used, the
prompts we gave, and how we used it. The prompts are saved as we actually sent them,
in the prompts folder.

## Tools

ChatGPT - used once at the start, to turn the one line project brief into a proper
plan and a detailed prompt we could work from. It did not write project code.

Claude Code - used to write the code from that prompt: the packet/TLS parser, the
JA3, JA3S and JA4 modules, the reference database, the matcher, the CLI and the
tests. It also wrote the first drafts of the docs, which we then cut down and
corrected.

## Prompts

All in the prompts folder, in order:

prompt-1 - what we sent ChatGPT to get a plan and a prompt.

prompt-2 - the detailed brief we then gave Claude Code to build from. Longer and
more structured because it came out of ChatGPT before we edited it.

prompt-3 - asking it to make the docs simpler because the first set was too heavy.

prompt-4 - questions we asked so we could understand what was built and run it
ourselves.

## Thought process

The design decisions were ours and we gave them to the tool as fixed rules, not open
questions. The main ones:

Scope - build the core first (read a pcap, parse ClientHello and ServerHello, JA3,
JA3S, a JSON reference database, the matcher, the CLI, five client experiments and
tests) and leave JA4/JA4S, eBPF/XDP, TRex, Redis and Valkey out until the core
worked. Those extra ones are in the course list but not all needed, and adding them
early would have made it too big to understand.

Tech - Python with Scapy, pcap files as the main input so results are reproducible,
and JSON for the database. Chosen so a student can read it and explain it in a viva.

Correctness - JA3 and JA3S had to follow the published spec, with GREASE, extension
ordering and formatting handled properly. We called these out in the brief because a
wrong hash only shows up much later.

No fake data - it was not allowed to invent any fingerprint, hash, capture or
result. Anything it could not run itself had to be marked so we would run it. The
fingerprints and pcaps in the repo are from our own runs.

Then we asked for the code in phases and checked each one before moving on. JA4 was
added later once the core was done.

## Step by step

Where AI actually did the work:

We wrote the brief (prompt-2) and Claude Code wrote the code from it - parser, JA3,
JA3S, JA4, database, matcher, CLI and the test suite.

The five captures (curl, OpenSSL, Python ssl, headless Chrome, a hand-built
ClientHello) were generated and captured by us on macOS. The pcaps and the
fingerprints in the database are from those runs, not from the model. We checked the
JA3 values against tshark and Wireshark on the same packets.

We ran pytest ourselves and did not treat the project as done until it passed.

The docs were first drafted by the tool, then we simplified them (prompt-3) and read
them against the code and the real command output.
