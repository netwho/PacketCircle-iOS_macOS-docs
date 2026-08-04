# PacketCircle iOS — Known issues (1.0.0)

<p align="center">
  <img src="../assets/logo.png" alt="PacketCircle" width="140" />
</p>

**Status:** Archive of limitations that shipped with **1.0.0**.  
**Resolved in:** **[Release notes 1.1.0](./RELEASE-NOTES-1.1.0.md)**

These items were documented while 1.0.0 was in App Store review. None were treated as show-stoppers for the first release; 1.1.0 was planned to close them.

| Version | Intent |
|---------|--------|
| **1.0.0** | First App Store release |
| **1.1.0** | Fixes below + Gauges quality panels + host names + broader decode → [release notes](./RELEASE-NOTES-1.1.0.md) |

---

## Known issues in 1.0.0

### KI-1 — Unnamed / backchannel TCP ports under-represented on Circle & Talkers

**Example:** Metasploit-style FTP exploit capture: FTP on **21**, HTTP on **80**, backchannel on **4444**.

| View | What you saw in 1.0.0 |
|------|------------------------|
| **Decode** | Port **4444** frames present, labeled generic **TCP**. |
| **Circle / Talkers** | Pair often emphasized well-known services; the **4444** socket was easy to miss. |

**Impact:** Exploit / lab backchannels were easy in Decode, harder in conversation-first views.  
**→ Fixed in 1.1.0** — see [release notes](./RELEASE-NOTES-1.1.0.md).

---

### KI-2 — Talkers rows omit port numbers

Talkers showed IP pair, protocol badges, counts, and quality, but **not TCP/UDP ports**. You often opened Session just to learn which sockets belonged to the conversation.  
**→ Fixed in 1.1.0** (ports when a socket is selected).

---

### KI-3 — Conversation summary is one-way and light on ports

Summaries used a one-directional `A → B` arrow even though aggregates are bi-directional, and did not put per-side packets/ports at a glance.  
**→ Fixed in 1.1.0** (bi-directional shared summary).

---

### KI-4 — Conversation summary panels not fully consistent

Circle, Talkers, Session, and related drill-downs each summarized a pair slightly differently.  
**→ Fixed in 1.1.0** (shared conversation summary block).

---

### KI-5 — Guided tour leaves filters / view state behind

After the tour, the circle could still carry tour-driven filters or selections.  
**→ Fixed in 1.1.0** (Finish/Skip → clean Circle).

---

### KI-6 — Talkers Top‑N can hide pairs

Talkers felt capped like Circle Top‑N (**10 / 25 / 50**). For triage, Talkers should list all analyzed conversations.  
**→ Fixed in 1.1.0** (Talkers = all pairs; Circle keeps Top‑N).

---

## Other 1.0.0 notes (still relevant as product limits)

| Note | Detail |
|------|--------|
| Decode frame count vs status bar | Decode may show a capped list while the file bar reports analyzed packets — different scopes. |
| Follow TCP Stream budget | Reassembly is Options-capped ([Limitations](./LIMITATIONS.md)). |
| Native decode depth | Not Wireshark-class ([Limitations](./LIMITATIONS.md)); broader in 1.1.0 but same philosophy. |
| No live capture on iOS | Offline PCAP/PCAPNG only ([Privacy](../PRIVACY.md)). |

---

## Feedback

Comments on LinkedIn or issues on this docs repo help prioritize the next release.

---

*PacketCircle — conversation-first triage on iPhone.*
