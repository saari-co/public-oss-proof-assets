# public-oss-proof-assets

Sanitized immutable screenshots and recordings for open-source issue and
pull-request proof. Do not store tokens, cookies, or dashboard URLs here.

## Layout

```text
<lane>/<issue>/<YYYY-MM-DD>/<filename>
```

## NVIDIA/OpenShell#2742 — Grok subscription OAuth

Lane: [saariuslystoned/OpenShell-grok](https://github.com/saariuslystoned/OpenShell-grok)
Writeup: `proof/openclaw-grok-20260814.md` in that repo.

| File | What it shows |
| --- | --- |
| [openclaw-conversation-grok-20260814.png](openshell-grok/2742/2026-08-14/openclaw-conversation-grok-20260814.png) | New OpenClaw session: `GROKSUB-PROOF-20260814` reply, footer `inference/grok-4.6` |
| [openclaw-conversation-20260814.png](openshell-grok/2742/2026-08-14/openclaw-conversation-20260814.png) | Earlier empty Main Session still showing leftover `qwen3.6:latest` chrome |
| [openclaw-01-before-swap.png](openshell-grok/2742/2026-08-14/openclaw-01-before-swap.png) | Before model swap: `nemotron-3.5-lightning` |
| [openclaw-02-new-session.png](openshell-grok/2742/2026-08-14/openclaw-02-new-session.png) | New session after click |
| [openclaw-03-model-picker.png](openshell-grok/2742/2026-08-14/openclaw-03-model-picker.png) | Model picker still on Nemotron |
| [openclaw-04-after-model.png](openshell-grok/2742/2026-08-14/openclaw-04-after-model.png) | After swap attempt, still Nemotron until new session + saved Grok default |


## openclaw/openclaw#150610 — Talk gateway-relay duplicate user transcripts

Lane: [openclaw/openclaw#153739](https://github.com/openclaw/openclaw/pull/153739)

| File | What it shows |
| --- | --- |
| [pixel-talk-one-user-row-20260920.png](openclaw-talk-relay/150610/2026-09-20/pixel-talk-one-user-row-20260920.png) | Pixel 10 Pro Fold on a branch-built Gateway: one spoken sentence renders as a single user bubble with the complete text, where six `talkFinal` transcripts reached the relay |

## openclaw/openclaw#157331 — Gemini 3.8 TTS over the Interactions API

Lane: [openclaw/openclaw#157331](https://github.com/openclaw/openclaw/pull/157331)

One live synthesis through the branch's Google speech provider on 2026-09-24
(`gemini-3.8-flash-lite-tts`, voice `Kore`, `store: false`, `audio/l16` at 24 kHz).
The API key is not in the trace; the audio base64 is elided.

| File | What it shows |
| --- | --- |
| [gemini-3.8-flash-lite-tts-20260924.wav](openclaw-gemini-tts/157331/2026-09-24/gemini-3.8-flash-lite-tts-20260924.wav) | 6.72 s WAV the provider wrote from Google's L16 response. Transcript spoken verbatim, including the `<short pause>` tag; the `speech_metadata.style` note ("warm, calm, unhurried", "Speaker name: Alex") is not read aloud |
| [trace-redacted-20260924.json](openclaw-gemini-tts/157331/2026-09-24/trace-redacted-20260924.json) | Request body sent to `POST /v1beta/interactions` and the HTTP 200 response: `steps[].content[{type:"audio", mime_type:"audio/l16; rate=24000; channels=1"}]`, 23 input / 216 output tokens |

## trycua/cua#3673 — Android driver baseline on Pixel 10 Pro Fold

Lane: [trycua/cua#3673](https://github.com/trycua/cua/issues/3673) (draft [trycua/cua#3674](https://github.com/trycua/cua/pull/3674) at `271d2e46`)

Upstream `scripts/smoke.py` on a physical Pixel 10 Pro Fold (Android 17 / API 37, unfolded, inner display).
It fails on a fresh install because the demo's first-launch notification-permission dialog takes display-0
focus (`lifecycle-smoke.py` pre-grants the permission; `smoke.py` does not). It passes with the same pre-grant.
The driver side was correct in both runs. Status bar cropped; no device serial recorded.

| File | What it shows |
| --- | --- |
| [fold-display0-fresh-install-permission-dialog.png](cua-android/3673/2026-09-26/fold-display0-fresh-install-permission-dialog.png) | Display 0 after a fresh demo install: the permission dialog covers the synthetic "Human input" field that `smoke.py` types into |
| [fold-display0-after-one-back.png](cua-android/3673/2026-09-26/fold-display0-after-one-back.png) | Same screen after one BACK; demo focused, permission still not granted |
| [fold-cua-virtual-display-fixture-count5.png](cua-android/3673/2026-09-26/fold-cua-virtual-display-fixture-count5.png) | Cua snapshot of its virtual display: fixture counter at 5 after five Cua taps |
| [fold-baseline-summary.json](cua-android/3673/2026-09-26/fold-baseline-summary.json) | Source revision, APK/CLI digests, both smoke outcomes, failure classification, what is not proven |

### PR 1 — explicit exported Activity selection

`app launch --activity` on the rebased Android driver; `scripts/smoke.py --runs 2` passes on the API 37 emulator and the Fold.

| File | What it shows |
| --- | --- |
| [pr1-fold-fixture-detail-activity-taps1.png](cua-android/3673/2026-09-26/pr1-fold-fixture-detail-activity-taps1.png) | Cua snapshot of the fixture's non-launcher `DetailActivity`, opened by explicit Activity, after one Cua tap (`Taps: 1`) and a refused conflicting selection |
| [pr1-fold-repoglance-widget-gallery.png](cua-android/3673/2026-09-26/pr1-fold-repoglance-widget-gallery.png) | Cua snapshot of RepoGlance's debug widget gallery opened directly with `--activity`, no launcher overlay. Sample data only; the low-contrast digits are a RepoGlance theme issue |
| [pr1-summary.json](cua-android/3673/2026-09-26/pr1-summary.json) | Candidate revision, artifact digests, local gates, both device runs, every selection call and refusal code from the Fold run |

### PR 2 — emulator → physical Pixel qualification harness

`scripts/qualify.py` receipts. Devices are named by role only; home paths are replaced with `~`.

| File | What it shows |
| --- | --- |
| [pr2-receipt-final-924591f28.json](cua-android/3673/2026-09-26/pr2-receipt-final-924591f28.json) | Final head after OpenClaw review fixes, from fresh installs: `qualification: full`; emulator (deploy, smoke, lifecycle) and Fold (deploy, smoke) pass, installed bytes match, cleanup clean |
| [pr2-receipt-final-cf41cfbd3.json](cua-android/3673/2026-09-26/pr2-receipt-final-cf41cfbd3.json) | Superseded head, before the review fixes. From fresh installs: emulator (deploy, smoke, lifecycle) and Fold (deploy, smoke) pass, installed bytes match, cleanup clean, not-run checks and Driver-unsupported capabilities listed |
| [pr2-receipt-first-run.json](cua-android/3673/2026-09-26/pr2-receipt-first-run.json) | First run before the lifecycle fix: `smoke.py` passes on a fresh install, `lifecycle-smoke.py` fails on the collapsed notification, the phone phase is `blocked`, cleanup residue recorded (pre-amend local revision) |

### Physical-device evidence: background use on the Fold

A local build of `271d2e46` + #4247 + #4249 on a Pixel 10 Pro Fold (Android 17). Only Cua's synthetic apps are driven. Effects are checked through the fixture's own state, not through Cua's acknowledgement.

| File | What it shows |
| --- | --- |
| [evidence-dual-before-set-text.png](cua-android/3673/2026-09-26/evidence-dual-before-set-text.png) | Both displays at once: the human's editor and keyboard on display 0, and Cua's display captured independently with `screencap` |
| [evidence-dual-after-set-text.png](cua-android/3673/2026-09-26/evidence-dual-after-set-text.png) | After shell-UID UiAutomation read Cua's display tree and ran `ACTION_SET_TEXT`: the text appears on Cua's display, and the human's focus and keyboard are untouched |
| [evidence-fold-lock-cua-display.png](cua-android/3673/2026-09-26/evidence-fold-lock-cua-display.png) | A simulated fold raises the lock screen on Cua's display too. The session survives, but taps are accepted and never reach the app |
| [evidence-real-human-typing-dual.png](cua-android/3673/2026-09-26/evidence-real-human-typing-dual.png) | A real human typing with Gboard on display 0 while the agent set `AgentText04` and tapped (count 4) on Cua's display. Agent: 7/7 set-text and 7/7 taps; the human's 216 characters arrived intact; the keyboard stayed on display 0 |
| [evidence-termux-refused.png](cua-android/3673/2026-09-26/evidence-termux-refused.png) | Real Termux (`untrusted_app_27`) running Cua's phone CLI from its own session. It can list Cua's folder. `doctor` and `session create` are refused but reported as `uncertain` (exit 4), and writing into Cua's folder is denied |
| [evidence-summary.json](cua-android/3673/2026-09-26/evidence-summary.json) | Latency, snapshot frame age against idle time, IME focus isolation, accessibility visibility, the UiAutomation spike, rotation, 3-minute soak, fold (simulated, tabletop, physical) and power-button lock results, real human typing, ordinary-app refusal |
