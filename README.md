# GPU rental prices — open dataset

**Daily-verified cloud GPU rental prices across 18+ providers, in one open dataset. Updated every day. CC BY 4.0.**

Covers on-demand and spot/community pricing for **H100, H200, B200, A100, L40S, RTX 4090/5090, MI300X, GH200** and more, from providers including RunPod, Lambda, CoreWeave, Nebius, Hyperstack, DataCrunch, Voltage Park, Crusoe, OVH, AWS, Azure, Together, Modal, fal, Vultr, and others.

> 🔎 **Browse it live, sortable, with per-cell source + timestamp, history charts and a rent-vs-buy calculator:**
> ## → [gpurentalprices.com](https://gpurentalprices.com)

Every price on the live site links to the provider's own source and shows the exact fetch time. This repo is the raw, machine-readable version of the same data.

---

## What's in here

| File | Contents |
|------|----------|
| [`data/latest.json`](data/latest.json) | The most recent snapshot: every offer (provider, GPU, VRAM, $/hr, on-demand vs spot, source URL, fetch timestamp). |
| [`data/snapshots/YYYY-MM-DD.json`](data/snapshots) | Append-only daily snapshots. Price history can't be backfilled, which is exactly why we record it. |

This mirror keeps a rolling window of recent daily snapshots. The **full multi-year price history** is maintained on [gpurentalprices.com](https://gpurentalprices.com/data).

### Record schema (`offers[]`)

```json
{
  "provider": "runpod",              // provider slug
  "gpu": "h100-sxm",                 // normalized GPU id
  "vram_gb": 80,                     // GPU memory
  "usd_hr": 2.79,                    // price per GPU per hour, USD
  "kind": "secure",                  // "secure"/on-demand (firm) or "community"/spot (interruptible)
  "source_url": "https://...",       // the provider page/API the price came from
  "fetched_at": "2026-07-08T07:42Z"  // exact fetch time
}
```

## How the data is collected

Once per day each provider's own pricing source is fetched (a public API where one exists, the official pricing page otherwise). Prices are normalized to **USD per GPU per hour**, excluding storage, egress and networking. When a fetch fails, that provider's rows are carried forward and flagged with their last-verified date — never silently presented as today's price. Full method: [gpurentalprices.com/methodology](https://gpurentalprices.com/methodology).

## Use it

Free to use under **CC BY 4.0** — build dashboards, notebooks, research, price alerts, whatever. The one ask the license makes: **attribute it with a link to [gpurentalprices.com](https://gpurentalprices.com)**.

```bash
curl -s https://raw.githubusercontent.com/adriannutiu/gpu-prices-data/main/data/latest.json
```

There's also a live JSON API and CSV export on the site: [gpurentalprices.com/data](https://gpurentalprices.com/data).

## License

[Creative Commons Attribution 4.0 International (CC BY 4.0)](LICENSE). Attribution: "GPU rental price data by [gpurentalprices.com](https://gpurentalprices.com), CC BY 4.0."
