# PacketCircle macOS: Limitations

<img src="../assets/logo.png" alt="PacketCircle" width="64" />

> Note: macOS code is not yet available publicly. Keep checking for updates.

PacketCircle macOS is optimized for interactive exploration, but several features trade completeness for responsiveness.

## Performance caps

### Follow TCP Stream truncation

Follow TCP Stream reassembles and displays a capped amount of payload.

- Controlled by **Options -> Follow TCP Stream budget (KB)**.
- When the budget is reached, the UI indicates truncation.

### Decode list caps

Application decode lists are frame-capped. If you need deeper decode, narrow the selection (pair/port/filter) and reopen.

## Data scope and heuristics

### Session Details TCP health scope

- **Conversation (IP pair)**: aggregated TCP health across all TCP ports between the two IPs.
- **Sockets (TCP ports)**: TCP health computed for the selected TCP port.

### Follow TCP Stream direction (client/server)

Client/server direction is derived from SYN when available.

If the capture does not include SYN for that connection, direction uses a best-effort heuristic (well-known port / port ordering).

## Live capture considerations

If you use live/modeled capture workflows (growing captures), PacketCircle may re-run analysis as the file grows. For very long continuous captures, CPU cost increases over time.

## Practical recommendations

1. Use filters or smaller captures when doing deep decode or follow.
2. Raise Follow TCP Stream budget only when needed.
3. Use Sockets focus to identify which specific service/port is slow.

