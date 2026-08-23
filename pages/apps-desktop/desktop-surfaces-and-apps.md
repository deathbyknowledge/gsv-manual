# Surfaces, Desktop Host & Local Helpers

[Web & Desktop](index.md)

## Personal Chat

Chat is fixed to the canonical Personal Process. A recently active Work Process cannot silently
become the apparent assistant. Starting or opening Work creates a separate Work Session with an
explicit banner and Back action.

Committed Messages synchronize across signed-in clients. Only the client that started a run receives
its transient Message stream. Opening Process activity explicitly subscribes that client to raw
reasoning, drafts, tools, and lifecycle signals.

## Messages, Files, Terminal, And Repositories

- **Messages** shows canonical Conversation content.
- **Files** browses and edits authorized filesystem targets.
- **Terminal** runs the shell on the selected target.
- **Repositories** inspects ripgit-backed source, history, diffs, and updates.
- **Work** lists non-Personal Processes and opens their activity or explicit Work Sessions.

Attachments are uploaded as files, converted to exact resource references, and resolved lazily. The
client does not embed base64 in a protocol frame.

## Desktop And `gsvd`

Desktop is a user client. `gsvd` is a separate machine driver with a driver-bound credential. On
first use Desktop can ask the user to name the computer, derive a stable normalized machine ID,
persist its credential/configuration, install the per-user service, and verify the daemon through a
versioned same-user control protocol.

Closing Desktop does not disconnect the machine. Signing out of Desktop and explicitly revoking the
machine are separate actions.

The `gsv` CLI uses the same narrow daemon-control protocol for status, reload, reconnect, diagnostics,
and lifecycle actions. It does not duplicate the machine runtime.

## Voice And Gestures

Desktop supervises platform-native helpers:

- `gsv-transcribe` owns microphone capture and local speech inference;
- `gsv-vision` owns camera capture, tract inference for palm/landmark models, gesture recognition,
  and temporal gesture policy.

Camera frames, landmarks, and audio stay local and do not cross the Gateway control plane. Helpers
send bounded, versioned semantic events to Desktop. Desktop owns the active voice request, draft,
send/delete/clear behavior, armed gesture state, and stale-event fencing.

The gesture helper starts disarmed. The two-hand arming and scroll chords, action-hand number
commands, tracking-loss rules, and freshness checks are designed so a stale or partially recognized
gesture cannot act on a later voice request.

Desktop exposes one optional system status item for machine connectivity, voice, and gesture state.
`gsvd` remains headless; it does not create a competing tray icon.

## Platform Boundaries

The lifecycle contract is cross-platform. OS-specific implementation stays behind narrow boundaries:

| Concern | macOS | Linux | Windows |
| --- | --- | --- | --- |
| Background service | per-user launch service | systemd user service/XDG fallback | per-user startup task |
| Local control | Unix socket | Unix socket | named pipe |
| Protected credentials | Keychain-capable boundary | Secret Service/protected file | Credential Manager/DPAPI |
| Media permissions | TCC | portals/PipeWire/device access | privacy APIs |

Current host configuration uses a private, atomically replaced `config.toml`; the storage boundary can
be hardened per platform without changing enrollment or daemon IPC.

## Development Builds

The Rust workspace is rooted at `host/`. Build all host applications with:

```bash
cd host
cargo build --workspace
```

On macOS, `host/scripts/package-macos.sh` assembles the development `GSV.app` bundle and ZIP. Gesture
models are checksum-pinned and embedded in `gsv-vision`, so a packaged application does not fetch or
build MediaPipe, Java, or Bazel at runtime.

## For Agents

Do not route raw camera/audio through generic IPC, and do not make the Desktop tray or CLI own daemon
state. Ask the component that owns the state through its typed control protocol.
