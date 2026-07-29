# PacketCircle iOS: Limitations

<p align="center">
  <img src="../assets/logo.png" alt="PacketCircle" width="180" />
</p>

> **Disclaimer:** the iOS release is currently under review by the Apple App Store and should be available soon.

PacketCircle iOS favors responsiveness on phone. Several areas are capped or heuristic-based.

![TCP health (native estimate)](../assets/ios-session-health.jpg)

## Performance caps

### Follow TCP Stream

Reassembly is limited by **Options → Follow TCP Stream budget (KB)**. Truncation is indicated in the UI.

### Decode list

Decode stops after a maximum frame count. Narrow by pair/port and reopen for more.

## Data scope & heuristics

- **Conversation vs Sockets** focus changes whether TCP health is IP-pair aggregated or port-specific
- Client/server without SYN uses a well-known-port heuristic
- TCP health is a **native estimate** — not Wireshark `tcp.analysis`

## iOS constraints

- No live capture (offline PCAP/PCAPNG only)
- Very large files may feel slow or hit memory pressure on older devices

## Tips

1. Prefer smaller / filtered captures for deep decode and follow  
2. Raise the Follow budget only when needed  
3. Use **Sockets** focus to isolate a slow service/port
