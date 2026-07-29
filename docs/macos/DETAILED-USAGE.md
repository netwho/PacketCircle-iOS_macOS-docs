# PacketCircle macOS: Detailed Usage

This document describes typical workflows in PacketCircle macOS: open/replay, options, exploring session details, and following TCP streams.

## App navigation

- **Circle**: visual communication graph.
- **Gauges**: traffic/protocol summaries.
- **Conversations**: browse and select communication pairs.
- **Decode**: application decode list for selected traffic (frame capped).

## Open vs Replay

### Default behavior: load entire trace

When you import a capture, PacketCircle macOS loads the full trace for analysis and visualization.

### Replay: original timing

If you want time-accurate playback:
1. Tap the bottom capture status bar.
2. Confirm "Replay".

## Options (gear icon)

Key configuration:

### Quality thresholds preset

Choose how TCP session quality maps to grade labels:
- Easy
- Balanced
- Tough

This affects edge coloring and quality summaries.

### Session details focus

Choose what TCP health is shown while inspecting a pair:

- **Conversation (IP pair)**: aggregated TCP health across all TCP ports between the two IPs.
- **Sockets (TCP ports)**: port-specific TCP health for the selected TCP port.

If you suspect only one service is slow (for example multiple ports between the same IPs), switch to **Sockets** and pick the relevant "TCP socket".

### Follow TCP Stream budget (performance cap)

Follow TCP Stream reassembles payload and can be expensive on large captures.
Adjust:
- Follow TCP Stream budget (KB)

The UI will indicate if reassembly output is truncated.

## Session Details pagination

To keep large sessions usable:

- TCP Exchange shows 20 lines by default; use "Show more" to load the next 20.
- Application decode shows 20 lines by default; use "Show more" to load the next 20.

## Follow TCP Stream

Follow TCP Stream can display either:

- Client -> Server direction
- Server -> Client direction

Client/server coloring is direction-aware:
- The client side is colored as "Client".
- The server side is colored as "Server".

If the SYN is not present in the capture, direction uses a best-effort heuristic (well-known port / port ordering).

