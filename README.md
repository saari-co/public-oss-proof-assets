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

