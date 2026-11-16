<a href="https://gola.apimart.ai/k-w1HAwH"><img src="https://raw.githubusercontent.com/fujc683/awesome-seedance-2-5-flash-prompts/main/banner.jpg" alt="Seedance 2.5 Flash" width="100%" /></a>

# Seedance 2.5 Flash API — text-to-video endpoint, parameters and errors

> How to call Seedance 2.5 Flash: async task API, ratio/resolution rules and real costs.

[![Awesome](https://awesome.re/badge.svg)](https://github.com/sindresorhus/awesome) [![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg)](LICENSE)

**[👉 Try Seedance 2.5 Flash on APIMart](https://gola.apimart.ai/k-w1HAwH)**

`https://gola.apimart.ai/k-w1HAwH`

[💰 Pricing](https://gola.apimart.ai/k-fLan2T) · [🔑 Get an API key](https://gola.apimart.ai/k-CFrbeF)

---

## Quick start

```bash
curl -X POST https://api.apimart.ai/v1/videos/generations \
  -H "Authorization: Bearer $APIMART_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "seedance-2-5-flash",
    "prompt": "a red apple rolling on a wooden table, soft window light, cinematic",
    "duration": 4,
    "ratio": "16:9",
    "resolution": "720p"
  }'
```

The call is asynchronous: you get a `task_id`, then poll it.

```bash
curl https://api.apimart.ai/v1/tasks/<task_id> -H "Authorization: Bearer $APIMART_API_KEY"
```

On success `data.result.videos[0].url` holds an MP4 (72h validity) and
`data.cost` holds the **final** charge in USD.

## Parameters

| Field | Type | Notes |
|---|---|---|
| `model` | string | `seedance-2-5-flash` |
| `prompt` | string | motion + subject + camera description |
| `duration` | int | seconds, 4-30 |
| `ratio` | string | `16:9`, `4:3`, `1:1`, `3:4`, `9:16`, `21:9`, `adaptive` |
| `resolution` | string | `480p` or `720p` — **1080p returns 400** |
| `reference_image` | url | optional first frame |
| `reference_video` | url | optional motion reference (separate rate) |

## Errors we actually hit

| Message | Cause |
|---|---|
| `This model only supports ratio ...` | you passed `720p` as `ratio` |
| `Seedance 2.5 Flash does not offer 1080p` | resolution too high |
| `task_failed` | upstream refused; check `error.message` |

## Pricing

Billed **per second of output video**:

| Resolution | List price | Measured |
|---|---:|---:|
| 480p | $0.1836/s | ~$0.11/s |
| 720p | $0.1836/s | **$0.143/s** |

A 4-second 720p clip measured **$0.5737** end to end.

---

## Related

- Prompt library: [awesome-seedance-2-5-flash-prompts](https://github.com/fujc683/awesome-seedance-2-5-flash-prompts)
- Other video models: [all collections](https://github.com/fujc683?tab=repositories)

## License

CC BY 4.0
