# FakeDiscord fork changes

This file summarizes the main changes from upstream Tincan that are currently carried by this fork.

## Access and admission

- Replaced the reusable-room-password model used by the FakeDiscord integration with persistent server identity and device admission.
- Added one-time invite tokens.
- Added host-side persistent device allowlisting.
- Added authorized-device listing and revocation.
- Hardened host-only commands so they cannot enter network serialization paths that expect remote commands.

## File transfer

- Added a dedicated file-transfer protocol over iroh/QUIC.
- Added direct peer-to-peer transfer between clients.
- Added public and recipient-only private offers.
- Added streaming downloads with `.part` temporary files and atomic completion.
- Added BLAKE2s-256 integrity validation.
- Added overwrite protection and bounded metadata.
- Added image preview support.
- Added `/send`, `/sendto`, `/files`, `/get` and completion helpers.

## Audio and PTT

- Added configurable hold-to-talk PTT.
- Added configurable keys covering F1-F12, letters, digits, Space and CapsLock.
- Added terminal press/release event support.
- Added Linux global read-only evdev PTT listener for Wayland/game-focus scenarios.
- Added microphone open/close notification sounds tied to actual microphone state.

## Integration work

- Added APIs/behavior expected by the FakeDiscord Win32 and Qt launchers.
- Added notification and launcher-facing settings hooks.
- Added regression tests for the modified control plane, PTT behavior and file transfer.

## Compatibility

The modified protocol is not guaranteed to interoperate with an unmodified upstream Tincan build.

For the complete desktop experience, use the FakeDiscord repository:
https://github.com/KpOwOJluK/FakeDiscord
