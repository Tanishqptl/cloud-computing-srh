# SHP05 (Vertex Auto Parts) — Lane Reliability Metrics

**Launch Customer Targets:**
- **Freshness:** 2 minutes
- **Reliability:** 65% on time (≤ 24h late) on ocean lanes; 95% on time on air lanes
- **Budget:** $50 / month

## Delay & On-Time Rate per Lane (October 2026)

| Mode | Origin | Destination | Trade Lane | Shipments | Avg Delay (hrs) | On-Time Rate | Target | Status |
| :--- | :--- | :--- | :--- | ---: | ---: | ---: | ---: | :--- |
| OCEAN | SGSIN | BEANR | Asia-North Europe | 18 | 62.3 | 44.4% | 65.0% | **MISS** (-20.6%) |
| OCEAN | NLRTM | USHOU | Transatlantic | 18 | 48.7 | 50.0% | 65.0% | **MISS** (-15.0%) |
| OCEAN | CNNGB | DEHAM | Asia-North Europe | 25 | 44.6 | 60.0% | 65.0% | **MISS** (-5.0%) |
| OCEAN | CNSHA | ITGOA | Asia-Mediterranean | 14 | 25.3 | 71.4% | 65.0% | **MEET** (+6.4%) |
| AIR | DXB | FRA | Middle East-Europe | 30 | 1.8 | 93.3% | 95.0% | **MISS** (-1.7%) |
| AIR | HKG | AMS | Asia-Europe | 31 | 3.3 | 96.8% | 95.0% | **MEET** (+1.8%) |
| AIR | ICN | FRA | Asia-Europe | 32 | 1.0 | 100.0% | 95.0% | **MEET** (+5.0%) |

## Carrier Breakdown on Missed Lanes

- **SGSIN → BEANR (44.4% on-time):** `ATL` (0.0%, 2 shipments), `KST` (25.0%, 4), `ORS` (25.0%, 4), `BLC` (33.3%, 3), `NWL` (100.0%, 4), `HRZ` (100.0%, 1).
- **NLRTM → USHOU (50.0% on-time):** `ATL` (0.0%, 1), `KST` (0.0%, 2), `ORS` (20.0%, 5), `BLC` (33.3%, 3), `HRZ` (100.0%, 4), `NWL` (100.0%, 3).
- **CNNGB → DEHAM (60.0% on-time):** `ATL` (0.0%, 3), `NWL` (33.3%, 6), `KST` (50.0%, 4), `ORS` (75.0%, 4), `BLC` (100.0%, 6), `HRZ` (100.0%, 2).
- **DXB → FRA (93.3% on-time):** `FAL` (83.3%, 6), `SKY` (93.3%, 15), `AQL` (100.0%, 5), `MER` (100.0%, 4).

## Key Takeaway
4 of 7 lanes miss reliability targets (3 of 4 ocean lanes and 1 air lane), driven heavily by `ATL`, `KST`, and `ORS` on ocean and `FAL` on air. Because Vertex Auto Parts runs just-in-time factory supply, late ocean shipments must be detected within 2 minutes so planners can trigger emergency air bookings before assembly lines stop.
