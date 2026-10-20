# Lower-cost NovaNova Studio image and video guide

Conversations, image/video generation and a reusable creative canvas.

[中文](README_zh-CN.md) · [Model & pricing](https://go2v.toapis.com/1020_nv_g) · [Upstream](https://github.com/Swayingleaves/novanova-studio)

**Independent ToAPIs community guide, not an upstream-endorsed edition.** This validates API cases and configuration/module boundaries; full upstream product acceptance is pending.

## Demo

![Images and case prices](screenshots/en/image-cases.png)

Video status: the seedance-2-5 submission returned no task ID. Outcome and charge are unconfirmed; no duplicate POST was made and no successful video case is claimed.

## Case amounts and model rates (ascending)

2026-10-20.

| Model / preset | Type | Case amount / quote | Applicable model rate | Fee evidence |
|---|---|---:|---|---|
| gpt-image-2(VIP)<br>low / 1K | image | Quoted $0.0019 | $0.0019/image | Configured rate; task billing unavailable |
| gpt-image-2<br>1K | image | Quoted $0.015 | $0.015/image | Configured rate; task billing unavailable |
| gpt-image-2.5-flare<br>high / 1K | image | Quoted $0.0225 | $0.0225/image | Configured rate; task billing unavailable |

gpt-image-2(VIP) starts at $0.0019/image; this low/1K case is $0.0019/image. Images retain quote labels when task billing is unavailable. Three image models use the same project prompt with different quality presets. Video USD/s is a measured case ratio, not a fixed tariff.

## Project-specific reuse

1. Start the loopback bridge on the same self-hosted server. Configure a custom channel at http://127.0.0.1:8769/v1 with the separate bridge token.
2. For each image model copy the matching text-to-image group fields from integration/novanova-custom-image-groups.json. The wrapper is documentation, not a claimed import endpoint.
3. CustomProviderAdapter only polls VIDEO tasks in the pinned code; the bridge waits for ToAPIs image completion and returns the expected data[0].url synchronously.
4. The native references placeholder is an array, while each ToAPIs image_with_roles item needs a scalar URL. The native poller also needs explicit terminal-status handling. integration/novanova-video-plan.json records both gaps instead of offering a broken paste-ready template.
5. The Spring/Java app, channel persistence, media registration and complete image/video UI workflows remain unverified.

## Run the independent API cases

```powershell
$env:TOAPIS_API_KEY="your_private_key"
python run_case.py --job jobs/gpt-image-2-vip.json
python run_case.py --job jobs/gpt-image-2-vip.json --live
python run_case.py --job jobs/video.json
python run_case.py --job jobs/video.json --live
```

Without --live, only the current key rate is queried. Set a budget locally; the recipe enforces per-request caps, not a hosted-account global spend limit. After errors/timeouts, reconcile the saved task before another submission.

## Optional synchronous compatibility bridge

```powershell
$env:BRIDGE_TOKEN="replace_with_a_separate_random_token_at_least_24_chars"
$env:BRIDGE_PORT="8769"
python bridge.py
```

Binds to 127.0.0.1 only. UI credentials use the separate bridge token. Keep the real generation key in the bridge environment. Preserve upstream outbound/SSRF rules; this is not a public hosted-service endpoint. Image edits are not enabled.

## Original inputs and outputs

```text
An original cinematic product storyboard still: an unbranded amber glass perfume bottle on a pale travertine pedestal, warm peach backdrop, a single translucent fabric ribbon suspended beside it, soft studio sunlight and realistic caustics, refined commercial photography, clear single composition, 16:9 landscape, no lettering, no logos, no watermark.
```

[Jobs](jobs/) · [Original media](examples/) · [Sanitized evidence](evidence/) · [Acceptance](ACCEPTANCE.md) · [Upstream and protocol evidence](UPSTREAM.md)

## License and scope

Original guide/adapter code: MIT. Upstream source and trademarks keep their own license and ownership. The OpenShorts fork retains its upstream MIT license. No existing sponsor/referral links were replaced. No audio integration claim is made.
