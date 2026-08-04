# PacketCircle iOS — Release notes 1.1.0

<p align="center">
  <img src="../assets/logo.png" alt="PacketCircle" width="140" />
</p>

**Release:** **1.1.0**  
**Follows:** [Known issues in 1.0.0](./KNOWN-ISSUES-1.0.0.md) (documented while 1.0.0 was shipping)

1.1.0 closes the conversation UX gaps called out for 1.0.0, adds the Gauges quality panels, host-name display, and broader native decode — still offline PCAP/PCAPNG only, still not a mobile Wireshark.

---

## Highlights

| Area | What you get |
|------|----------------|
| **Conversation UI** | Bi-directional hosts; ports when a **socket** is selected; unnamed listeners stay visible |
| **Talkers** | **All** analyzed pairs (Circle keeps Top‑N **10 / 25 / 50**) |
| **Gauges** | Degraded Fair/Poor list + quality timeline → Talkers time slice |
| **Tour** | Circle → Session → Gauges; Finish leaves a **clean Circle** |
| **Host names** | Options → Show host names (DNS / mDNS / LLMNR / NetBIOS) |
| **Decode** | Friendlier labels; IPsec, BGP, OSPF, MPLS, VXLAN, NetFlow, LLDP, EAPOL, STP, … |
| **MAC mode** | Named ethertypes / LLC (not hex spam); Session shows STP BPDUs; IP-on-link TTL/frag when IPv4 rides the MACs |

---

## Fixed from 1.0.0 known issues

| ID | Was (1.0.0) | Now (1.1.0) |
|----|-------------|-------------|
| KI-1 | Backchannel ports easy to miss on Circle/Talkers | Unnamed listeners are first-class sockets |
| KI-2 | Talkers omitted ports | Ports appear when a socket is selected |
| KI-3 | One-way conversation summary | Bi-directional summary shared across Circle / Talkers / Session |
| KI-4 | Inconsistent summary panels | Shared conversation summary block |
| KI-5 | Tour left filters behind | Finish/Skip → clean, unfiltered Circle |
| KI-6 | Talkers felt Top‑N capped | Talkers lists all pairs; Circle keeps Top‑N |

Full descriptions remain in [KNOWN-ISSUES-1.0.0.md](./KNOWN-ISSUES-1.0.0.md).

---

## What’s new

### Conversation & Talkers

- **Bi-directional** conversation summary: both hosts, packets each way, protocol chips.
- **Whole conversation** shows **no ports**; pick a **socket** for `TCP/80 HTTP` / `TCP/4444`-style labels.
- **Unnamed / backchannel** listeners stay beside well-known services on the same pair.
- **Talkers** = full analyzed list; **Circle** drawing budget stays Top‑N.

### Guided tour

- Walks **Circle → Session → Gauges**.
- **Finish / Skip** closes sheets and restores a clean desk (no closing announcement screen).

### Gauges

1. **Degraded Quality Conversations** — Fair & Poor only, worst first; tap → Session.  
2. **Quality timeline** — graded bars over capture time; idle gaps compressed; tap → ± slice → **Talkers**.

### Options

- **Show host names** — shortened names from DNS / mDNS / LLMNR / NetBIOS on Circle, Talkers, Session (addresses still used for filters / Decode).
- **Quality thresholds** — Lenient / Balanced / Strict (grade bands only).

### Decode & MAC mode

- Readable labels instead of bare opcodes.
- Infra peeks where present: **IPsec**, **BGP**, **OSPF**, **MPLS**, **VXLAN**, **NetFlow / IPFIX**, **mDNS / LLMNR**, **LLDP**, **802.1X**, **STP BPDU**, plus improved ARP / IGMP / DNS.
- MAC-mode legend names ethertypes and LLC (STP, IPX, AppleTalk, RARP, …); unknown types collapse to **Other**.
- Session for STP shows **BPDU details**; MAC conversations that carry IPv4 can show an **IP on this link** summary (TTL, DF, fragmentation).

Still **not** Wireshark-class — intentional for App Store / offline native Swift. See [Limitations](./LIMITATIONS.md).

### Demo capture

Bundled `PacketCircleDemo.pcap` includes LAN DNS A/PTR + mDNS so **Show host names** has labels in Demo / tour.

---

## Checklist (shipped)

| ID | Item | Status |
|----|------|--------|
| FIX-1 | Unnamed / backchannel sockets | Done |
| FIX-2 | Ports when a socket is selected | Done |
| FIX-3 | Bi-directional conversation summary | Done |
| FIX-4 | Shared summary consistency | Done |
| FIX-5 | Tour clean desk | Done |
| FIX-6 | Talkers = all pairs; Circle Top‑N | Done |
| FEAT-1 | Degraded Quality + quality timeline | Done |
| FEAT-2 | Show host names | Done |
| FEAT-3 | Broader infra / friendly decode | Done |
| FEAT-4 | MAC ethertype naming + STP Session + IP-on-link | Done |

---

## Still true (not regressions)

| Note | Detail |
|------|--------|
| Decode list vs status bar | Decode may show a capped frame count while the file bar reports analyzed packets |
| Follow TCP Stream | Options-capped reassembly ([Limitations](./LIMITATIONS.md)) |
| No live capture on iOS | Offline PCAP/PCAPNG only ([Privacy](../PRIVACY.md)) |

---

## Docs & screenshots

Quickstart, detailed usage, and the user manual describe the 1.1.0 workflow. Screenshots (including LinkedIn assets) were refreshed in **dark mode**.

---

*PacketCircle — conversation-first triage on iPhone.*
