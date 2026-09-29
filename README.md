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

### 2026-09-28 — structured speaker label, style kept to delivery

Two live syntheses through the branch's provider after the maintainer review (head `827bcda`):
`speakerName` now rides in `speech_metadata.speaker`; `Persona:` and `Speaker name:` lines are
gone from `style`. Four direct probes established which request shapes Google accepts for a
single voice with a speaker label. Keys are not in any file; audio base64 is elided.

| File | What it shows |
| --- | --- |
| [gemini-3.8-flash-lite-tts-speaker-alex-20260928.wav](openclaw-gemini-tts/157331/2026-09-28/gemini-3.8-flash-lite-tts-speaker-alex-20260928.wav) | 8.48 s WAV, `speakerName: Alex`, `audioProfile` + `personaPrompt` as `style`, persona label `Alfred` set but not sent. Transcript spoken verbatim including `<short pause>` |
| [trace-redacted-speaker-alex-20260928.json](openclaw-gemini-tts/157331/2026-09-28/trace-redacted-speaker-alex-20260928.json) | Request with `annotations[{type:"speech_metadata", speaker:"Alex", style:"warm, calm, unhurried\n\nKeep a close-mic feel."}]` and `speech_config:[{voice:"Kore"}]`; HTTP 200 in 3.3 s, `steps[]` audio |
| [gemini-3.8-flash-lite-tts-no-speaker-20260928.wav](openclaw-gemini-tts/157331/2026-09-28/gemini-3.8-flash-lite-tts-no-speaker-20260928.wav) | 7.0 s WAV with no speaker label and no style: no `annotations` key at all, `<laugh>` tag spoken as a vocal burst |
| [trace-redacted-no-speaker-20260928.json](openclaw-gemini-tts/157331/2026-09-28/trace-redacted-no-speaker-20260928.json) | Plain single-voice request and HTTP 200 response in 2.9 s |
| [speaker-shape-probes-20260928.json](openclaw-gemini-tts/157331/2026-09-28/speaker-shape-probes-20260928.json) | Direct `curl` probes: a `speaker` inside a `speech_config` array entry is mapped to `multi_speaker_voice_config` and rejected unless exactly 2 speakers; `{speakers:[one]}` with or without `mode` is HTTP 400 "Invalid input received"; single-voice array plus `speech_metadata.speaker` is HTTP 200 |

## openclaw/openclaw#157465 — Gemini 3.8 two-voice dialogue

Lane: [openclaw/openclaw#157465](https://github.com/openclaw/openclaw/pull/157465) (stacked on #157331)

One live synthesis on 2026-09-28 through the rebuilt branch's provider (head `707ab55`,
`gemini-3.8-flash-lite-tts`, speakers Puck and Kore, `store: false`, `audio/l16` at 24 kHz).
The transcript deliberately contains ordinary colon-prefixed prose (`Budget: 10 dollars`) and an
unconfigured label (`Alice: Hi.`) after Puck's turn; both stay inside Puck's turn and Kore still
starts her own turn. Keys are not in any file; audio base64 is elided.

| File | What it shows |
| --- | --- |
| [gemini-3.8-flash-lite-tts-dialogue-budget-alice-20260928.wav](openclaw-gemini-tts/157465/2026-09-28/gemini-3.8-flash-lite-tts-dialogue-budget-alice-20260928.wav) | 8.68 s WAV: Puck says "Hello from the gate. <laugh> Budget: 10 dollars Alice: Hi.", Kore says "Understood. <short pause> See you there." Neither speaker name is spoken |
| [trace-redacted-dialogue-budget-alice-20260928.json](openclaw-gemini-tts/157465/2026-09-28/trace-redacted-dialogue-budget-alice-20260928.json) | Two `content[]` text blocks with `speech_metadata {speaker, style}` (`style` = cast style + `audioProfile`), `speech_config {mode: conversational, speakers: [Puck, Kore]}`; HTTP 200 in 4.0 s, `steps[]` audio |

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

## saariuslystoned/phone-lab#3 — Slice 2, cross-display element refs

Lane: [saariuslystoned/phone-lab#3](https://github.com/saariuslystoned/phone-lab/pull/3)
Writeup: `proof/slice-2-element-refs/PROOF.md` in that repo. Both images are
`screencap -d` of Cua's virtual display on the Pixel 10 Pro Fold (the
synthetic fixture only; no status bar, no personal content).

| File | What it shows |
| --- | --- |
| [slice2-toast-on-cua-display.png](phone-lab/3/2026-09-27/slice2-toast-on-cua-display.png) | Toast raised by phone-lab's treedump lands on the Cua display (Count: 2) |
| [slice2-toast-during-api-capture.png](phone-lab/3/2026-09-27/slice2-toast-during-api-capture.png) | Toast during the ten `GET /api/tree` captures (Count: 22); the increment ref stayed `e7f67h` |

## openclaw/openclaw#159947 — Gemini custom voices from Control UI

Lane: [openclaw/openclaw#159947](https://github.com/openclaw/openclaw/pull/159947)

One real voice replication on 2026-09-29 through a branch-built Gateway (head `3e6dc02`, build
`2026.9.6-3e6dc02fc227`, fresh profile, loopback only). The PR author recorded the consent
sentence (9.4 s) and the reference take (28.3 s) in the Control UI's **Create from my voice**
dialog and clicked **Store voice** once. The Gateway's `tts.replicateVoice` answered in 5.7 s after
one `POST /v1beta/voices` to Google, HTTP 200, no retry. Read back through `tts.voices`, the
project went from 11 to 12 stored voices; the new one is type `replicated`.

Images are cropped to the dialog or the page viewport. Other voices in the project are blacked
out and the new id is partly masked. No key, pairing token, or audio is in any file.

| File | What it shows |
| --- | --- |
| [voice-lab-01-dialog-before-recording-3e6dc02-20260929.png](openclaw-voice-lab/159947/2026-09-29/voice-lab-01-dialog-before-recording-3e6dc02-20260929.png) | The dialog before recording: voice name, Google's consent sentence, the reference script, both takes empty |
| [voice-lab-02-consent-take-recorded-3e6dc02-20260929.png](openclaw-voice-lab/159947/2026-09-29/voice-lab-02-consent-take-recorded-3e6dc02-20260929.png) | Consent take recorded (9.4 s) with its playback control. Store stays locked and says why until the reference take exists |
| [voice-lab-03-stored-success-3e6dc02-20260929.png](openclaw-voice-lab/159947/2026-09-29/voice-lab-03-stored-success-3e6dc02-20260929.png) | Success: both takes recorded, green "Stored PR159947 UI proof", Store locked against a second send |
| [voice-lab-04-custom-voices-list-3e6dc02-20260929.png](openclaw-voice-lab/159947/2026-09-29/voice-lab-04-custom-voices-list-3e6dc02-20260929.png) | Custom voices after the store: the new voice listed first with its `voice_…1ckp` id, footer `2026.9.6 · git@3e6dc02`. The red "Could not list stored voices." is the branch's incomplete-listing marker: Google returned 1000 catalog entries over 10 pages with more pending, so the list is shown with a warning |

## openclaw/openclaw#143466 — Android flat large-screen navigation

Lane: [openclaw/openclaw#143466](https://github.com/openclaw/openclaw/pull/143466)

Pixel 10 Pro Fold (Android 17), debug builds of head `1e971aa7` and merge-base `9e9944cd` in
OpenClaw's synthetic screenshot fixture (no Gateway), driven by
[phone-lab](https://github.com/saariuslystoned/phone-lab) trails.

| File | What it shows |
| --- | --- |
| [fold-inner-flat-base-vs-head-1e971aa7-20260929.png](openclaw-android-ui/143466/2026-09-29/fold-inner-flat-base-vs-head-1e971aa7-20260929.png) | Fold inner display open flat (852×883 dp): base keeps the drawer, head shows the permanent sidebar. Status bar cropped |
| [resize-matrix-base-vs-head-1e971aa7-20260929.png](openclaw-android-ui/143466/2026-09-29/resize-matrix-base-vs-head-1e971aa7-20260929.png) | One activity on a Cua virtual display resized live: compact, 832 and 848 dp wide, 315 and 325 dp tall. Head switches to the sidebar at ≥840 dp wide and ≥320 dp tall; the typed draft survives every size |

## openclaw/openclaw#155918 — Android Jump to latest above the composer

Lane: [openclaw/openclaw#155918](https://github.com/openclaw/openclaw/pull/155918)

Pixel 10 Pro Fold, head `8ccd7a95` vs merge-base `43d85e5f`, screenshot fixture `chat` scene on
Cua virtual displays.

| File | What it shows |
| --- | --- |
| [jump-to-latest-base-vs-head-540x960dp-8ccd7a95-20260929.png](openclaw-android-ui/155918/2026-09-29/jump-to-latest-base-vs-head-540x960dp-8ccd7a95-20260929.png) | 540×960 dp: scrolled-up history and the result of tapping Jump to latest. Base: header arrow; head: floating button above the composer. Both return to the latest reply |
| [jump-to-latest-short-and-wide-8ccd7a95-20260929.png](openclaw-android-ui/155918/2026-09-29/jump-to-latest-short-and-wide-8ccd7a95-20260929.png) | Base and head at 540×380 dp, head at 960×540 dp: the floating button stays visible and clear of the composer |

## openclaw/openclaw#147282 — Android chat switching transitions (partial)

Lane: [openclaw/openclaw#147282](https://github.com/openclaw/openclaw/pull/147282)

Pixel 10 Pro Fold display 0, head `791fd912` vs merge-base `4aacaa0e`, screenshot fixture;
drawer chat switches filmed with `screenrecord` and sampled at fixed offsets from the switch.
Fixture mode cannot show cold reopen, persisted model names or the schema upgrade.

| File | What it shows |
| --- | --- |
| [chat-switch-frames-base-vs-head-791fd912-20260929.png](openclaw-android-ui/147282/2026-09-29/chat-switch-frames-base-vs-head-791fd912-20260929.png) | Rows: base/head × first visit, second (unseen) chat, return to a viewed chat; columns −30 to +300 ms. Base: sliding drawer, "Loading thread" card, pop-in; head: drawer gone in one frame, fade-in, same-frame restore followed by a scroll jump. Status bar band cropped |

### 2026-09-29 — live Gateway run

Pixel 10 Pro XL, base installed fresh then head installed over it, paired to a throwaway 2026.9.6
Gateway on loopback with a mock model ("Mock Luna", "Mock Sol") and three synthetic sessions.
Status bar band cropped.

| File | What it shows |
| --- | --- |
| [live-model-chip-base-vs-head-791fd912-20260929.png](openclaw-android-ui/147282/2026-09-29/live-model-chip-base-vs-head-791fd912-20260929.png) | Composer model chip from −50 to +300 ms around each switch. Base: "Model" → raw `mock-luna` → "Mock Luna"; head: the friendly name from the first frame |
| [live-switch-frames-base-vs-head-791fd912-20260929.png](openclaw-android-ui/147282/2026-09-29/live-switch-frames-base-vs-head-791fd912-20260929.png) | Frames −100 to +300 ms for first visits, a return, and two switches after an offline cold start. Base: sliding drawer, "Loading thread", pop-in, "Model" chip offline; head: drawer gone in one frame, fade-in, cached friendly names offline |
