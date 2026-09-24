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
