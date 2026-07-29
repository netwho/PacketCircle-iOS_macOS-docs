# PacketCircle iOS: Detailed Usage

<p align="center">
  <img src="../assets/logo.png" alt="PacketCircle" width="180" />
</p>

> **Disclaimer:** the iOS release is currently under review by the Apple App Store and should be available soon.

This document covers open/replay, Options, Session Details, and Follow TCP Stream.

## Screenshots

| Session overview | TCP health | TCP exchange |
|:---:|:---:|:---:|
| ![Session](../assets/ios-session-overview.jpg) | ![TCP health](../assets/ios-session-health.jpg) | ![TCP exchange](../assets/ios-tcp-exchange.jpg) |

| Application decode | Follow TCP Stream | Options |
|:---:|:---:|:---:|
| ![App decode](../assets/ios-app-decode.jpg) | ![Follow](../assets/ios-follow-tcp-stream.jpg) | ![Options](../assets/ios-options.jpg) |

## App navigation

- **Circle** — endpoints and pairs on a ring
- **Gauges** — packets/bytes/errors rates + top talkers/protocols
- **Talkers** — pair list and drill-down
- **Decode** — capped frame list with details/hex

## Open vs Replay

Import always loads the **full** trace. Tap the bottom status bar to **Replay** at original inter-frame timing.

## Options (gear)

### TCP health focus

- **Conversation (IP pair)** — one aggregated TCP health summary for the IP pair
- **Sockets (TCP ports)** — pick a TCP port; health is port-specific

### Quality thresholds

Maps the 0–100 session score to Excellent / Good / Fair / Poor:

- **Lenient** — more sessions look healthy
- **Balanced** — default PacketCircle bands
- **Strict** — only clean sessions look Excellent

The score itself does not change — only the grade coloring does.

### Follow TCP Stream budget

Caps reassembly payload (and scan) so large streams don’t freeze the UI. Raise carefully if you need more data.

## Session Details

- **TCP Session Health** — score, window, retransmissions, RST, zero-window, SYN/FIN
- **TCP Exchange** — client↔server ladder (20 rows, then Show more)
- **Application decode** — DNS/HTTP/… previews (20 rows, then Show more)

## Follow TCP Stream

Directions: Entire / Client→Server / Server→Client. Formats: ASCII / Hex / Hex+ASCII.

- **Client** = red · **Server** = blue  
- Without SYN, direction uses a well-known-port heuristic
