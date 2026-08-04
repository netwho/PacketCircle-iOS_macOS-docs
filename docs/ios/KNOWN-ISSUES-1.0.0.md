# PacketCircle iOS — 1.1.0 notes & 1.0.0 known issues (archive)

<p align="center">
  <img src="../assets/logo.png" alt="PacketCircle" width="140" />
</p>

**Status:** **1.1.0** delivers the fixes and Gauges features planned while **1.0.0** was in review. This page keeps the original 1.0.0 known-issue descriptions for history and marks what shipped in 1.1.0.

| Version | Intent |
|---------|--------|
| **1.0.0** | First App Store release |
| **1.1.0** | Conversation UX fixes + Gauges quality panels + host names + broader native decode |

---

## What’s new in 1.1.0

### Conversation & Talkers

- **Bi-directional** conversation summary (Circle card, Talkers, Session): both hosts, packets each way, protocol chips.
- **Whole conversation** shows **no ports**; pick a **socket** to show one port on each side (`TCP/80 HTTP`, unknown as `TCP/4444`).
- **Unnamed / backchannel** listeners (e.g. **4444**) stay first-class sockets beside FTP/HTTP.
- **Talkers** lists **all** analyzed pairs; **Circle** keeps Top‑N (**10 / 25 / 50**) for the ring.

### Guided tour

- Walks **Circle → Session → Gauges**.
- **Finish / Skip** closes sheets and leaves a **clean, unfiltered Circle** (no summary alert).

### Gauges

1. **Degraded Quality Conversations** — Fair & Poor only, worst first; tap → Session.  
2. **Quality timeline** — graded bars over capture time; large idle gaps compressed; tap → ± slice → **Talkers**.

### Options

- **Show host names** — prefer shortened DNS / mDNS / LLMNR / NetBIOS names on Circle, Talkers, and Session (addresses still used for filters / Decode).
- **Quality thresholds** — Lenient / Balanced / Strict (unchanged idea; documented in tour help).

### Decode depth (native, not Wireshark)

Friendlier labels (no bare “Opcode = 3”), plus deeper coverage for popular infra protocols where the capture allows it, including:

- **IPsec** (ESP / AH / IKE), **BGP**, **OSPF**, **MPLS**, **VXLAN**, **NetFlow / IPFIX**
- **mDNS / LLMNR**, **LLDP**, **802.1X (EAPOL)**, **STP BPDU**
- Improved **ARP**, **IGMP**, **DNS** answers

Still **not** Wireshark-class — intentional for App Store / offline native Swift.

---

## 1.1.0 checklist (shipped)

| ID | Item | Status |
|----|------|--------|
| FIX-1 | Unnamed / backchannel sockets on Circle & Talkers | Done |
| FIX-2 | Ports / sockets visible when a socket is selected | Done |
| FIX-3 | Bi-directional conversation summary | Done |
| FIX-4 | Shared summary panel consistency | Done |
| FIX-5 | Tour ends on a clean Circle | Done |
| FIX-6 | Talkers = all pairs; Circle keeps Top‑N | Done |
| FEAT-1 | Degraded Quality Conversations + quality timeline | Done |
| FEAT-2 | Show host names (DNS / mDNS / NetBIOS) | Done |
| FEAT-3 | Broader infra / friendly decode labels | Done |

---

## Archive — known issues that were in 1.0.0

These described **1.0.0** behavior. They are addressed in **1.1.0** as noted above.

### KI-1 — Unnamed / backchannel TCP ports under-represented on Circle & Talkers

Metasploit-style FTP + HTTP + **4444**: Decode showed 4444; Circle/Talkers often emphasized well-known services only.  
**→ 1.1.0:** unnamed listeners remain first-class sockets.

### KI-2 — Talkers rows omit port numbers

**→ 1.1.0:** whole-conversation rows stay clean; socket selection surfaces `TCP/port` labels on summaries.

### KI-3 — Conversation summary one-way / light on ports

**→ 1.1.0:** bi-dir layout; ports when a socket is selected.

### KI-4 — Inconsistent summary panels

**→ 1.1.0:** shared `ConversationSummaryBlock` across Circle, Talkers, Session.

### KI-5 — Guided tour left filters behind

**→ 1.1.0:** Finish/Skip → clean desk on Circle.

### KI-6 — Talkers Top‑N hid pairs

**→ 1.1.0:** Talkers shows all pairs; Circle keeps Top‑N.

### Other notes (still true)

| Note | Detail |
|------|--------|
| Decode frame count vs status bar | Decode may show a capped list while the file bar reports analyzed packets — different scopes. |
| Follow TCP Stream budget | Reassembly is Options-capped ([Limitations](./LIMITATIONS.md)). |
| Native decode depth | Broader in 1.1.0, still not Wireshark-class. |
| No live capture on iOS | Offline PCAP/PCAPNG only ([Privacy](../PRIVACY.md)). |

---

## Feedback

Comments on LinkedIn or issues on this docs repo help prioritize the next release — especially real captures where names, infra decode, or summary panels still mislead.

---

*PacketCircle — conversation-first triage on iPhone.*
