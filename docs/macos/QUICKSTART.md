# PacketCircle macOS: Quickstart

<img src="../assets/logo.png" alt="PacketCircle" width="64" />

> Note: macOS code is not yet available publicly. Keep checking for updates.

PacketCircle macOS is a native SwiftUI app for visualizing communication pairs from PCAP/PCAPNG captures.

## Requirements

- macOS 14+
- Optional: Wireshark installed if you want to use "Open in Wireshark" actions

## 1) Build / run (for development)

From the main repository:

```bash
cd /Users/walterh/Cursor/PacketCircleNative
./build.sh
```

## 2) Open a capture

1. Open PacketCircle.
2. Import `*.pcap` or `*.pcapng`.
3. PacketCircle loads the full trace for analysis and visualization.
4. Use the bottom capture status bar:
   - `<file name> · <X pkts> · <Y pairs>`

## 3) Replay original timing (optional)

To replay with original packet timing:
1. Tap the bottom capture status bar.
2. Confirm "Replay".

## 4) Explore results

- **Circle**: communication graph of endpoints and pairs.
- **Gauges**: traffic + protocol summaries.
- **Conversations**: list of pairs and quick drill-down.

Select a pair to open Session Details.

## 5) Follow TCP Stream (optional)

In Session Details (or via the associated controls), use **Follow TCP Stream** to reassemble and view a capped payload for one direction.

If it feels truncated or slow, open **Options** and adjust **Follow TCP Stream budget (KB)**.

