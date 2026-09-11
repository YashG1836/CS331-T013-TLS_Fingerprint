# AI Usage Documentation

This folder records how AI tools were used while building the TLS fingerprinting
project, as required for the submission. The prompts we actually used are kept
verbatim in `prompts/`.

## Tools

Two tools were used, at different stages.

ChatGPT was used once, at the planning stage. Its job was to take the single-line
project brief from the course sheet and help turn it into a scoped, ordered
specification we could then hand to a coding tool. It did not write any project
code.

Claude Code was used for the coding part. It wrote the TLS parser,
the JA3, JA3S and JA4 modules, the reference database and matcher, the CLI, and
the test suite. Specifications for the same were given by us. 

## Prompts

All prompts are stored in `prompts/`, in the order they were sent.

`prompt-1-planning-chatgpt.md`  given to ChatGPT.

`prompt-2-implementation-spec.md`  given to Claude Code. 

`prompt-3-documentation-simplification.md`  given to Claude Code 

`prompt-4-followup-questions.md` given to Claude Code

## Thought process

The project decisions were fixed before code generation: build the MVP first, Scapy, pcap files, JSON, and a simple modular pipeline. JA3/JA3S had to follow the published specifications, with no invented data or results. The work was divided into ten tested phases, with JA4 added later as a stretch goal. The tool implemented and documented these decisions, while we ran, checked, and corrected everything against real output. The documentation was later simplified in prompt-3 to make it easier to study and defend.

## Step-by-step details

1. Planning. We read the brief, listed the concepts we did not yet know, and used
ChatGPT to turn the brief into an ordered specification. The specification was then
edited by us into `prompt-2`.

2. Structure and parser. We specified the module layout and the pcap-first design; the
tool wrote the TCP reassembly and TLS handshake parser. We checked it by parsing our
own captures and comparing the fields against what Wireshark showed for the same
packets.

3. JA3 and JA3S. We specified the exact fields, the GREASE and ordering rules, and the
hashing step; the tool implemented the string construction and hashing. We checked
the values against the reference database and against `tshark`'s own JA3 output.

4. Database and matcher. We decided on JSON, the metadata fields, and the rule that
measured fingerprints be kept distinct from any published ones; the tool wrote the
loader and the lookup. We populated it from our own captures.

5. CLI and output. We specified the output format and the known / possible / unknown
distinction; the tool wrote the command-line interface.

6. Tests. We required unit tests for JA3/JA3S construction and hashing and parser edge
cases, plus an integration test for the full pcap-to-lookup path; the tool wrote the
suite. We ran `pytest` and treated the MVP as incomplete until it passed.

7. Experiments. The five captures, curl, OpenSSL, Python `ssl`, headless Chrome, and a
hand-built ClientHello, were generated and captured by us on macOS. The tool wrote
the helper scripts, but the traffic, the pcaps and the resulting fingerprints are
from our runs.
