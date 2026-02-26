# Heating ROI Calculator

Client‑side interactive calculator for comparing heating solutions (investment + operating costs) with a physics‑based heat loss model and an ROI timeline chart.

## Features
- Heat loss calculation from building parameters (area, insulation, windows) with Plzeň design ΔT.
- Heating season model using HDD + days in season + “22°C when present / 10°C tempering otherwise”.
- Economic model with energy price growth, service costs, ETS2 gas surcharge, DHW load.
- Chart.js cost trajectories + live updates.
- Table split into energy vs service costs + CSV export.
- Language switch (CZ/EN) and currency switch (CZK/EUR/USD).
- Shareable URL state for all variable inputs.

## Tech Stack
- Tailwind CSS via CDN
- Vanilla JS (ES6+)
- Chart.js via CDN
- Lucide icons

## Run Locally
Open `index.html` in a browser:

```
open /Users/jan/dev/heating/index.html
```

## URL Parameters
All inputs are persisted into the URL so you can share a full configuration.

Example:
```
index.html?currency=EUR&language=en&area=80&horizon=10&days=20&ceiling=0&walls=0&windows=1&investGas=100000&investElectric=40000&investPump=269686&investAc=144737
```

### Supported Params
- `language`: `cs` or `en`
- `currency`: `CZK`, `EUR`, `USD`
- `area`: floor area (m²)
- `horizon`: years
- `days`: days in heating season at 22°C
- `ceiling`: `1` or `0` (insulated)
- `walls`: `1` or `0` (insulated)
- `windows`: `1` or `0` (triple glazing)
- `investGas`, `investElectric`, `investPump`, `investAc`: investment costs (in selected currency)

## Notes
- Currency conversion uses fixed 2025 averages:
  - 1 EUR = 24.693 CZK
  - 1 USD = 21.914 CZK
- If the page is opened via `file://`, language toggle uses `?language=` instead of `/en`.

## Files
- `index.html` – app UI + logic
- `PLAN.md` – original plan
