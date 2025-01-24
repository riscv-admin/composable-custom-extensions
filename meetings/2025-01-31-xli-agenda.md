# Meeting Agenda 2025-01-31: CX TG ad hoc meeting: Extension Logic Interface Workshop

When/where: 2025-01-31 7a-10a PT, Zoom

This is an ad hoc 2-3 hour CX TG meeting "workshop" to survey various
RISC-V extension/coprocessor logic interfaces and their user communities.

## Purpose

The TG will create ISA and non-ISA specifications that enable practical
reuse, within a system, of multiple composable custom extensions (CXs),
CX libraries, and modular CX unit (CXU) hardware. The TG deliverables
include an optional logic interface spec. Previously (2019-2024) Soft
CPU SIG designed such an interface, CXU-LI. Now the CX TG will draft
a new extension logic interface spec, informed by this, and by other
RISC-V extension logic interfaces, to be discussed in this workshop.

The meeting will consist of a series of 20 minute talks + 5 minutes
Q&A. Each talk will showcase one extension logic interface: its purpose,
highlights, signaling (channels, port maps), state model, kinds of
custom instructions supported, what architectural state (e.g., vector
registers) is accessible to extensions, any pipeline issues, and also,
the logic interface’s current ecosystem, user community, CPU cores
that support it, and exemplary uses in industry.

Following these talks will be up to 75 minutes of open
discussion and synthesis. Potential topics might include:

- How do these interfaces compare and contrast?
- Support for composition of custom extensions?
- Support for arbitrary, or fixed, custom instruction encodings?
- Support for optional "pay as you go" capabilities?
- Value of "modular composability" (composition without changing CPU or extension unit RTL)?
- Might you bridge one interface to another?
- ...

## Meeting agenda (details TBD)

RISC-V Extension Logic Interface Workshop
(An LFX RV Composable Custom Extensions TG Meeting)
Fri Jan 31, 2025, 7a-10a PT

Agenda:
- 7:00: RV disclaimers.
- 7:05: Jerry Zhao, ROCC (20 mins + 5 mins Q&A)
- 7:30: Christian Herber, CV-X-IF (")
- 7:55: Andreas Koch, SCAIE-V (")
- 8:20: Jan Gray, CXU-LI (")
- 8:45: Open discussion and synthesis (up to 75 mins)
- 10:00: End
