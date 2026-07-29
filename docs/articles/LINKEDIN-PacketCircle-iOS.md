# LinkedIn article draft — PacketCircle for iPhone

> **Status:** Draft for LinkedIn  
> **Images:** Upload the files under `docs/assets/` where marked `[IMAGE: …]` (LinkedIn does not embed GitHub paths — paste screenshots manually when publishing).  
> **Tone:** Personal engineering story → product → use cases. Soften or cut anything that feels too long for your audience.

---

## Suggested title options

1. From a Wireshark plugin to an iPhone packet circle  
2. PacketCircle on iOS: conversation graphs in your pocket  
3. Why I built a native Swift packet analyzer for iPhone (and what it can’t do)

**Suggested subtitle / first line:**  
Native Swift. Shared core with macOS. Offline PCAP/PCAPNG — no live capture on device (and why).

---

## Article body

[IMAGE: logo.png — small, optional]

### From Wireshark plugin to iPhone

It started with **[PacketCircle](https://github.com/netwho/PacketCircle)** — an open-source **Wireshark plugin** that draws communication pairs as a circle: who talks to whom, which protocols, how “hot” the edges are. That mental model stuck with me.

Out of curiosity I began a **standalone macOS** version: native **Swift** libraries for PCAP/PCAPNG (no Wireshark wiretap/dumpcap in the default build) and **SwiftUI** for the UI. With a lot of experimentation — and yes, some AI help on the build and plumbing — I eventually got a Mac app that opens captures and draws the circle. The GUI already feels cleaner than the Qt-ish plugin chrome. Functionality-wise, though, the native Mac build is still **far behind** the plugin and **not ready to share** as a finished product.

Then I got deeper into Xcode and Swift and had the slightly crazy idea: **what about iPhone?**  
The analysis engine — pair aggregation, protocol coloring, TCP session health, stream follow — could be a **shared core** between macOS and iOS. I still had an Apple Developer account from years of wrapping and signing apps for mobile device management. So I tried it.

### The hard lesson: no live capture on iOS

One thing became clear quickly: **forget capturing Wi‑Fi / the network interface from a normal App Store iPhone app.**

People sometimes talk about “cheating” with VPN/tunnel APIs to see packets. Even if you get that working technically, the **only** realistic path to users is the **App Store** — and Apple’s review will not bless a capture hack like that. So PacketCircle for iOS is honest about the boundary:

- **Open** PCAP / PCAPNG from Files / AirDrop  
- Or run the **built-in demo** capture and watch the circle build  
- **No** on-device live sniffing  

I’m looking at a future path for “almost live” analysis: **remote capture delivery**, for example **ERSPAN** (mirrored traffic inside GRE) landing as PCAP streams you can open on the phone — still without pretending the phone is a tap.

[IMAGE: ios-home.jpg — Home: Open Capture / Demo Mode]

### What it is today

**PacketCircle iOS** is an offline conversation analyzer: load a capture, see talkers on a **circle**, drill into **session health**, skim **decode**, and **follow a TCP stream** — on a phone, with a UI built for touch.

The same **PacketCircleCore** powers both Apple platforms. iOS is the shareable, reviewable slice of that work while the Mac app catches up in features.

[IMAGE: ios-readme-hero.jpg or ios-circle.jpg — Circle + conversation card + LIVE DEMO]

---

### How to use it (2-minute tour)

1. **Open** a capture or start **Demo Mode**.  
2. Explore the **Circle**: tap a node or edge; use the protocol chips as a legend/filter.  
3. Check **Gauges** for rates, top talkers, top protocols.  
4. Open **Talkers** for a list of pairs, or **Decode** for a frame list + details/hex.  
5. Open **Session details** for TCP health, exchange ladder, and application decode.  
6. Use **Follow TCP Stream** when you need the reassembled payload (ASCII/hex), with a budget so the phone doesn’t freeze on huge streams.  
7. Tap the **status bar** (filename · packets · pairs) if you want to **replay** with original timing.  
8. Open **Options** (gear) for quality thresholds, session focus (IP pair vs TCP socket), and stream budget.

[IMAGE: ios-gauges.jpg]  
[IMAGE: ios-decode.jpg]  
[IMAGE: ios-options.jpg]

---

### Feature list (v1)

| Area | What you get |
|------|----------------|
| **Open** | PCAP / PCAPNG from Files / share sheet |
| **Demo** | Bundled demo capture, ~1‑minute loop |
| **Circle** | Communication graph, protocol colors, Top‑N style focus |
| **Gauges** | Packets/bytes/errors style rates, top talkers & protocols |
| **Talkers** | Conversation list |
| **Decode** | Packet list, details tree, hex/ASCII (capped frames) |
| **Session details** | Pair summary, TCP session health score & metrics |
| **TCP exchange** | Client↔server ladder of segments/ACKs |
| **Application decode** | Lightweight previews (e.g. DNS/HTTP) |
| **Follow TCP Stream** | Reassembly, direction filters, ASCII/hex (budget-capped) |
| **Replay** | Tap status bar → replay with original timing |
| **Options** | Quality bands (lenient/balanced/strict), IP-pair vs socket focus, stream budget |
| **Privacy** | Analysis stays **on device** — we don’t collect or upload your captures |

[IMAGE: ios-session-health.jpg]  
[IMAGE: ios-tcp-exchange.jpg]  
[IMAGE: ios-follow-tcp-stream.jpg]  
[IMAGE: ios-app-decode.jpg]

---

### Use cases

**1. Field / change window — “show me the talkers”**  
You grabbed a PCAP on a span/TAP/laptop. On the way back (or in a meeting), open it on the phone: who is chatting with whom, which protocols dominate, which pair looks sick (retransmits, RSTs, poor score).

**2. Teaching & demos**  
Demo Mode is a story in a circle: HTTP, DNS, SSH, etc., without needing a lab network on the phone. Great for explaining conversation-centric troubleshooting to juniors or non-Wireshark specialists.

**3. Pre-filter before Wireshark**  
Use the circle and Talkers to find the interesting IP pair / port, then jump to full Wireshark on a laptop with a display filter. PacketCircle is the map; Wireshark remains the microscope.

**4. TCP health triage**  
Session details surface a **native** health estimate (not Wireshark `tcp.analysis`): window, retransmissions, RST, SYN/FIN. Optionally focus **per TCP socket** when several services share the same IP pair — so one slow HTTPS port doesn’t hide behind a healthy SSH session.

**5. Payload peek without a laptop**  
Follow TCP Stream for Telnet/HTTP-ish text, with client/server coloring. Caps exist on purpose — phones aren’t desktops; Options lets you raise the budget when you need more.

**6. Air-gapped / customer site**  
No cloud account, no upload of customer PCAPs to “our” servers. Open the file, analyze locally, delete when done. (See our privacy policy in the docs repo.)

---

### What it is *not*

- Not a replacement for Wireshark’s full dissector tree  
- Not a live Wi‑Fi sniffer on iPhone  
- Not the mature Mac product (yet) — Mac UI is nicer than the plugin’s Qt feel; **feature parity is still behind**  
- Not GPL: the **plugin** stays GPL; the **Native** apps are free to use but proprietary (see license in the docs)

---

### Status & links

- **iOS:** under **App Store review** — should be available soon  
- **macOS Native:** private / work-in-progress teaser only  
- **Docs (public):** https://github.com/netwho/PacketCircle-iOS_macOS-docs  
- **Original Wireshark plugin:** https://github.com/netwho/PacketCircle  

Made with love for the packet community.

---

### Closing line options for LinkedIn

- “If you’ve ever wanted the PacketCircle view without booting a laptop — this is the experiment.”  
- “Curious what a conversation-first analyzer looks like on a phone? Happy to hear feedback once it’s on the Store.”  
- “Plugin → Swift Mac → Swift iPhone. Same idea: see the conversations first.”

---

## Hashtag suggestions

`#Wireshark` `#PacketAnalysis` `#NetworkEngineering` `#iOS` `#Swift` `#SwiftUI` `#CyberSecurity` `#NetOps` `#PacketCircle`

## Publishing checklist

- [ ] Paste title + body into LinkedIn Article (or long post)  
- [ ] Upload screenshots at each `[IMAGE: …]` mark (order above works well)  
- [ ] Link docs + plugin repos  
- [ ] Mention App Store “coming soon” / under review  
- [ ] Decide whether to name AI assistance (honest, short — as in the draft) or soft-pedal it  
- [ ] Proof names: PacketCircle, PCAP/PCAPNG, ERSPAN, GRE
