# PacketCircle iOS: Quickstart

<p align="center">
  <img src="../assets/logo.png" alt="PacketCircle" width="180" />
</p>

> **Disclaimer:** the iOS release is currently under review by the Apple App Store and should be available soon.

PacketCircle iOS is an offline analyzer for PCAP/PCAPNG files. Open a capture, explore communication pairs on the circle, and optionally follow TCP streams.

## Screenshots

| Home | Circle | Gauges |
|:---:|:---:|:---:|
| ![Home](../assets/ios-home.jpg) | ![Circle](../assets/ios-circle.jpg) | ![Gauges](../assets/ios-gauges.jpg) |

| Options | Follow TCP Stream | Decode |
|:---:|:---:|:---:|
| ![Options](../assets/ios-options.jpg) | ![Follow TCP Stream](../assets/ios-follow-tcp-stream.jpg) | ![Decode](../assets/ios-decode.jpg) |

## Requirements

- iOS 17+ (device or Simulator)
- Offline PCAP/PCAPNG only — **no live capture** on device

## 1) Open a capture

1. Open PacketCircle iOS.
2. Tap **Open Capture** and pick a `*.pcap` / `*.pcapng` (or use **Demo Mode**).
3. The app loads the entire trace.
4. The bottom status bar shows: `<file> · <X pkts> · <Y pairs>`

## 2) Explore

- **Circle** — visual map of talkers and pairs
- **Gauges** — rates, top talkers, top protocols
- **Talkers** — conversation list
- **Decode** — packet list + hex/details

## 3) Replay (optional)

Tap the bottom capture status bar → confirm **Replay** for original timing.

## 4) Session details

Select a pair → **Session details** for TCP health, exchange ladder, and application decode.

## 5) Follow TCP Stream

From Session details, open **Follow TCP Stream** for a capped ASCII/hex reassembly (client = red, server = blue). Adjust the budget under **Options** (gear) if needed.
