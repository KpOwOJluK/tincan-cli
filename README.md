# Tincan — FakeDiscord modified fork

This repository is a **modified fork of [bilalyazicioglu/tincan-cli](https://github.com/bilalyazicioglu/tincan-cli)** and serves as the networking/audio core used by **FakeDiscord**.

It preserves Tincan's peer-to-peer terminal voice/text architecture while adding persistent private-server admission, direct file transfer, configurable/global PTT support, additional audio cues, and a number of reliability fixes.

> Fork version: **0.3.2-fd14**

## Why this fork exists

FakeDiscord needed several features beyond upstream Tincan:
- persistent private servers instead of reusable room passwords;
- one-time device admission and a host-side allowlist;
- direct peer-to-peer file transfer;
- configurable push-to-talk suitable for desktop launchers and games;
- stronger cross-platform integration with Windows and Arch Linux;
- regression fixes found while embedding the core in a native launcher.

The complete desktop application and launchers live in:
**https://github.com/KpOwOJluK/FakeDiscord**

## Major modifications

### Private-server access model
- persistent coordinator/server identity;
- one-time invite codes for first-time admission;
- authorized-device allowlist stored by the host;
- revoke/list operations for authorized devices;
- no reusable room password embedded in a public client binary.

### Direct P2P file transfer
- dedicated file-transfer ALPN over iroh/QUIC;
- streaming transfer rather than loading whole files into memory;
- BLAKE2s-256 integrity verification;
- temporary `.part` writes plus atomic rename on success;
- overwrite protection;
- public file offers and recipient-only private offers;
- image preview metadata;
- `/send`, `/sendto`, `/files`, `/get`;
- path and offer completion.
### Push-to-talk
- configurable key: F1-F12, A-Z, 0-9, Space or CapsLock;
- press/release semantics rather than toggle-only PTT;
- terminal keyboard enhancement support;
- Linux global PTT reader using read-only evdev input events;
- fail-safe handling for missing release support;
- microphone-open and microphone-close notification sounds.

The Windows desktop launcher adds its own Raw Input background listener and forwards PTT state into this core.

### Reliability fixes
- host-only commands such as invite/list/revoke are handled locally and never reach an unreachable serialization path;
- clients receive a normal host-only notice instead of crashing;
- PTT event handling avoids repeated transitions and duplicate sounds;
- file-transfer channel/privacy checks have dedicated regression coverage.

## Protocol additions

The fork currently uses:
- control protocol: `tincan/control/4`;
- file transfer protocol: `tincan/file/1`.

These additions make this fork **not protocol-identical to stock upstream Tincan**.

## Building

Standard Rust tooling is used:

```bash
cargo build --release
cargo test --lib
```

On Arch Linux, FakeDiscord also runs dedicated end-to-end file-transfer tests as part of its build script.

## Relationship to upstream

This repository remains a GitHub fork of the original Tincan project so the upstream history and attribution stay visible.

The original upstream README is preserved as [README_UPSTREAM.md](README_UPSTREAM.md).

Upstream:
**https://github.com/bilalyazicioglu/tincan-cli**

Modified fork:
**https://github.com/KpOwOJluK/tincan-cli**
## Development with ChatGPT

The modifications in this fork were implemented with extensive assistance from **ChatGPT by OpenAI**, under the direction and review of the repository owner.

ChatGPT was used for:
- Rust implementation and refactoring;
- protocol and state-machine changes;
- debugging cross-platform PTT behavior;
- file-transfer implementation and regression fixes;
- test creation;
- build/release integration;
- documentation.

See [AI_ASSISTED_DEVELOPMENT.md](AI_ASSISTED_DEVELOPMENT.md).

## License

This fork preserves the upstream project's MIT License. See [LICENSE](LICENSE).

Upstream copyright and attribution remain applicable to the original Tincan code.
