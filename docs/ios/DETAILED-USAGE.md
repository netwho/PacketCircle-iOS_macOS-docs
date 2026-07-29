# PacketCircle iOS: Detailed Usage

This document explains the main workflows in PacketCircle iOS: open/replay, options, session details, TCP follow, and how the UI choices affect results.

## Screenshots

![Follow TCP Stream](../assets/ios-follow-tcp-stream.jpg)
![Session Details](../assets/ios-session-details.jpg)

## App navigation

- **Circle tab**: visual layout of endpoints and communication pairs.
- **Gauges tab**: protocol/quality and traffic summaries.
- **Conversations tab**: pair list and drill-down entry point.
- **Decode tab** (if available): application decode list (frames capped).

## Open vs Replay

### Default behavior: load entire trace

When you import a capture, PacketCircle iOS loads the full trace for analysis and visualization.

### Replay: original timing

You can replay the trace at the original packet timing:
1. Tap the bottom capture status bar.
2. Confirm "Replay".

This keeps exploration responsive while still giving you time-accurate playback when you want it.

## Options (gear icon)

The **Options** sheet controls a few key analysis and UX settings:

### Quality thresholds preset

Choose how TCP session quality scores are mapped to grade bands:
- **Easy**
- **Balanced**
- **Tough**

This affects what you see for "quality" coloring and grade labeling (for example in edges and session quality summaries).

### Session details focus (TCP health scope)

Choose what TCP health is shown as you inspect a pair:

- **Sockets (TCP ports)** (default for identifying slow services)
  - If multiple TCP ports exist between the same two IPs, you can pick a specific "TCP socket" (port).
  - RTT/retrans/RST/zero-window and other TCP health metrics will be computed for that port.

- **Conversation (IP pair)**
  - TCP health is aggregated across the entire IP pair.
  - Port-level differences are not shown in health metrics.

### Follow TCP Stream budget (performance cap)

Follow TCP Stream reassembles payload and builds an ASCII/HEX view.

To prevent UI freezing on large captures, PacketCircle caps how much data it will reassemble and how much it will scan.
Adjust:
- **Follow TCP Stream budget (KB)**

If the displayed stream is truncated, the UI will indicate it.

## Session Details: TCP Exchange and Application Decode

Some sections use pagination by default:

- **TCP Exchange**: 20 lines shown, with **Show more** to load additional items.
- **Application decode**: 20 lines shown, with **Show more** to load additional items.

This makes navigation usable on large sessions.

## Follow TCP Stream: directions and colors

Follow TCP Stream shows a single direction at a time:
- **Client -> Server**
- **Server -> Client**

The view uses a direction-aware client/server split:
- Client side text uses the "Client" color.
- Server side text uses the "Server" color.

If a capture does not contain the SYN packet, PacketCircle uses a heuristic to decide which side is the server/client so colors and direction remain intuitive.

