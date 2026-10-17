# termux-emulator-image

The ready-made Android emulator for Claude Code cloud sessions: **Termux (F-Droid 0.118.3),
Ubuntu in proot-distro, and Claude Code 2.1.301** already installed. Restore it; never rebuild it.

How to use it, and every rule learned building it: **MANTRA_MANIFEST, `modules/cloud-android.md` §9**.
The tool: MANTRA_MANIFEST `tools/cloud-android/termux-emulator.sh` (`restore`, `start`, `tx`, `type`, `save`).

| | |
|---|---|
| AVD | `termux`: Android 11 `system-images;android-30;aosp_atd;x86_64` (Pkg.Revision 2), x86_64, software emulation |
| Contents | `parts/termux-avd.tar.zst.000…053`: `tar --sparse` of `~/.android/avd/termux.avd` + `termux.ini`, zstd, split at 95 MB |
| Check | `SHA256SUMS` |
| Size | 5.0 GB. Android encrypts `/data` file by file, so the disk does not compress or trim smaller |
| Built | 16.10.2026, while testing CLAUDE_CODE_TERMUX in the cloud |

Restore it with the tool (attach this repository to the session first):

```bash
bash tools/cloud-android/termux-emulator.sh restore     # in a MANTRA_MANIFEST checkout
```

**Do not `git clone` this repository** in a cloud session: one 5 GB pack through the session proxy is
cut off after about a minute (`RPC failed`, `early EOF`). The tool fetches each piece by itself through
the GitHub contents API, four at a time, checks `SHA256SUMS` and unpacks: 95 s in all (17.10.2026).

It is x86_64: it proves installers, Termux packages, proot and Claude Code's x64 build, and nothing
about ARM. Never put a key, token or login inside the image: Claude Code in it is **not logged in**.
