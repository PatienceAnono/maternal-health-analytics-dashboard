# Kenya Maternal and Child Health Analytics

**Kenya's MMR fell from 708 to 355 in 22 years. The SDG target is 70. Mandera's ANC4+ coverage is 18%. Nyeri's is 91%. This project maps the distance between where Kenya is and where it committed to be — county by county, indicator by indicator.**

---

## What this is

A maternal and child health analytics project tracking Kenya's progress on eight SDG 3 indicators from 2000 to 2022, disaggregated to county level and broken down by wealth quintile, education and urban/rural residence. The data comes from the Kenya Demographic and Health Survey (KDHS) 2022, WHO Global Health Observatory modelled estimates and Kenya KHIS facility reporting.

I built this because MCH is one of the most heavily funded areas in Kenya's health sector and also one of the most unequal. The national ANC4+ average of 67% conceals a county range from 18% to 93%. The wealth quintile gradient runs from 38% in the poorest households to 92% in the richest. Those numbers have real consequences — the eight counties below 40% ANC4+ collectively generate approximately 55,000 unattended home deliveries per year, each carrying significantly elevated maternal and neonatal mortality risk.

---

## The SDG 3 framework

Kenya is a signatory to the Sustainable Development Goals and has committed to specific health targets by 2030. This project tracks all three core MCH targets:

| SDG Indicator | Target by 2030 | Kenya 2022 | Distance |
|:---|:---|:---|:---|
| 3.1.1 Maternal Mortality Ratio | < 70 per 100,000 live births | 355 | 285 points |
| 3.2.1 Under-5 Mortality Rate | < 25 per 1,000 live births | 41 | 16 points |
| 3.2.2 Neonatal Mortality Rate | < 12 per 1,000 live births | 21 | 9 points |

None of these are on track. The analysis documents the pace of improvement needed versus the pace observed, indicator by indicator.

---

## The data

**Kenya Demographic and Health Survey (KDHS)**

The KDHS is the primary nationally representative household survey for health indicators in Kenya. Conducted by KNBS with USAID/ICF funding, it is the most credible source for maternal and child health at national and subnational level. I used survey years 2003, 2008/09, 2014 and 2022 as anchor points.

> Download pre-aggregated county-level indicators at `data.humdata.org/dataset/dhs-data-for-kenya` (no registration needed). Microdata with individual-level records available at `dhsprogram.com` with free registration.

**WHO Global Health Observatory**

Annual modelled estimates for MMR, U5MR and NMR — filling the intercensal years between KDHS surveys. Accessed via the WHO GHO OData API:

```
MMR   : https://ghoapi.azureedge.net/api/MDG_0000000026
U5MR  : https://ghoapi.azureedge.net/api/MDG_0000000007
ANC4+ : https://ghoapi.azureedge.net/api/RMNCH_ANC4
```

No authentication required. Power BI can connect directly to these URLs via Get Data → OData Feed.

**UN MMEIG**

The UN Maternal Mortality Estimation Inter-Agency Group produces the internationally agreed MMR estimates used here. Kenya's MMR figures use MMEIG methodology rather than raw survey figures because DHS survey-based MMR estimates have wide confidence intervals.

---

## Five datasets

| Sheet | Rows | What it covers |
|:---|:---|:---|
| `Kenya_National_MCH_Trend` | 23 | Annual national figures 2000–2022: ANC1, ANC4, SBA, PNC, institutional delivery, MMR, U5MR, NMR, IMR, contraceptive prevalence |
| `Kenya_County_MCH_2022` | 46 | Every county: ANC4 coverage category, SBA coverage, institutional delivery, estimated home births, region |
| `East_Africa_Regional_MCH` | 10 | MMR, ANC4, SBA, U5MR for 10 East African countries — Rwanda, Nigeria, Ethiopia, Tanzania, Uganda, Ghana, Zambia, Malawi, DRC, Kenya |
| `SDG3_Progress_Tracker` | 8 | Each indicator: 2000 baseline, 2022 value, 2030 target, % of journey completed, annual rate of change needed, on-track status |
| `Equity_Analysis` | 11 | ANC4, SBA, PNC and institutional delivery disaggregated by urban/rural, 5 wealth quintiles and 4 maternal education levels |

---

## What the data showed

**The progress is real, the gap is large**

Maternal mortality halved in 22 years. Under-5 mortality fell 64%. Skilled birth attendance nearly doubled. These are genuine achievements — the Linda Mama free maternity programme (2016), facility expansion and GAVI vaccine coverage all contributed. But halving MMR while starting at 708 still leaves Kenya at 355. The SDG target is 70. The remaining distance is larger than the distance already covered.

**The SDG pace problem**

For MMR, Kenya reduced by approximately 22 points per year in the most recent period (2014–2022). Reaching 70 by 2030 required 35 points per year. For ANC4+, recent improvement was 0.6 percentage points per year. Reaching 95% by 2030 required 3.5 per year. Every indicator I examined was Off Track. This was not a failure of the programme — progress continued and would continue. It was a realistic read of the mathematics.

**The county picture**

Eight counties had ANC4+ below 40%: Mandera (18%), Wajir (22%), Garissa (26%), Turkana (28%), Samburu (32%), Marsabit (35%), West Pokot (36%) and Tana River (38%). These counties collectively generated approximately 55,000 unattended home deliveries per year.

The scatter chart of ANC4+ versus SBA coverage showed something specific about North Eastern counties that I had not expected: their SBA rates were higher than their ANC4+ rates. Everywhere else in Kenya, these two indicators moved together — women who engaged with antenatal care also delivered in facilities. In Mandera and Wajir, women were more likely to show up at a facility in an emergency than to attend antenatal care earlier in pregnancy. That pattern pointed to emergency-only health-seeking behaviour and had different intervention implications than low coverage driven purely by geographic access.

**The equity gradient**

The wealth quintile ANC4+ gradient ran from 38% (poorest) to 92% (richest) — a 54 percentage point gap. The maternal education gradient ran from 28% (no education) to 94% (higher education) — a 66 point gap. The education gap was the largest equity gap in the dataset.

The urban-rural gap (82% urban, 59% rural) was significant but smaller than the wealth and education gaps. This told me geographic access was not the primary constraint. The women furthest from target were in households with multiple compounding disadvantages — low income, low maternal education, high barriers to navigating a health system not designed for them.

**Rwanda**

98% ANC4+. 95% SBA. MMR at 160 per 100,000. With a lower GDP per capita than Kenya. The argument that better MCH outcomes simply required more money did not survive contact with Rwanda's numbers.

---

## Charts produced

- `mch_national_trend.png` — two-panel: service coverage indicators (ANC4, SBA, institutional delivery, PNC) with SDG target line and COVID band; mortality indicators (U5MR, NMR, IMR) with MMR on secondary axis
- `sdg_progress.png` — SDG progress bars (% of journey covered) + remaining gap to target for all 8 indicators with on-track status
- `county_anc_sba.png` — all 46 counties ranked by ANC4+ with category colouring; ANC4 vs SBA scatter by region
- `county_regional.png` — regional average ANC4 vs SBA; annual home deliveries by region
- `equity_analysis.png` — urban vs rural grouped bar; wealth quintile connected line chart; maternal education diverging bar
- `regional_mch.png` — East Africa MMR comparison; ANC coverage vs MMR scatter with trend line

---

## Technical approach

```python
# Python stack
pandas · numpy · matplotlib · seaborn · openpyxl

# SDG progress calculation
df_sdg['Progress_to_2022_pct'] = (
    (df_sdg['Value_2022'] - df_sdg['Value_2000']).abs() /
    (df_sdg['Target_2030'] - df_sdg['Value_2000']).abs() * 100
)

# Annual rate of change needed
years_remaining = 2030 - 2022
df_sdg['Annual_Change_Needed_2030'] = (
    df_sdg['Target_2030'] - df_sdg['Value_2022']
) / years_remaining

# County estimated home births
df_county['Est_Home_Births'] = (
    df_county['Est_Annual_Births'] *
    (1 - df_county['Institutional_Delivery'] / 100)
).round(0).astype(int)
```

The equity analysis used a diverging bar chart for maternal education to simultaneously show ANC4+ (right-facing bars) and SBA (left-facing bars) against the same education categories on a single axis. This format is common in equity analysis presentations and communicates both the absolute level and the direction of the gap more efficiently than separate charts.

---

## Project structure

```
mch-analytics/
├── MCH_Analytics_EDA_v2.ipynb          # Main analysis notebook
├── MCH_Dashboard_Dataset.xlsx          # Five-sheet dataset
│   ├── Kenya_National_MCH_Trend        # 23-year national trend
│   ├── Kenya_County_MCH_2022           # 46-county snapshot
│   ├── East_Africa_Regional_MCH        # 10-country comparison
│   ├── SDG3_Progress_Tracker           # 8 indicators vs 2030 targets
│   └── Equity_Analysis                 # Wealth, residence, education breakdowns
├── outputs/
│   ├── mch_national_trend.png
│   ├── sdg_progress.png
│   ├── county_anc_sba.png
│   ├── county_regional.png
│   ├── equity_analysis.png
│   └── regional_mch.png
└── README.md
```

---

## Running the notebook

```bash
pip install pandas numpy matplotlib seaborn openpyxl
jupyter notebook MCH_Analytics_EDA_v2.ipynb
```

All data loads from the Excel file. No API calls required for the core analysis. The WHO GHO OData URLs in Section 9 are production-ready for Power BI connections.

---

## Power BI dashboard structure

| Page | Source sheet | Primary visuals |
|:---|:---|:---|
| Executive Overview | All | MMR, U5MR, NMR, ANC4%, SBA% KPI tiles against SDG targets; regional MMR comparison |
| Kenya National Trends | Kenya_National_MCH_Trend | Service coverage multi-line; mortality dual-axis; COVID band |
| SDG Progress Tracker | SDG3_Progress_Tracker | Progress bars, on-track flags, pace vs required pace |
| County Analysis | Kenya_County_MCH_2022 | Choropleth map, ranked bar, ANC vs SBA scatter, home births |
| Equity Analysis | Equity_Analysis | Wealth quintile gradient, urban/rural comparison, education diverging bar |

---

## Skills this project demonstrates

- **Survey data literacy** — KDHS methodology, DHS indicator definitions, MMEIG MMR estimation approach, intercensal interpolation
- **SDG progress analytics** — distance-to-target calculation, pace vs required pace framing, on-track classification
- **Sub-national disaggregation** — 46-county analysis, regional aggregation, critical threshold identification
- **Equity analysis** — wealth quintile gradients, education-stratified coverage, urban/rural decomposition, diverging bar chart for dual-indicator display
- **Public health framing** — translating coverage gaps into absolute numbers (home births) that make the equity stakes operationally concrete
- **Multi-source data integration** — KDHS survey anchors + WHO modelled estimates + facility data unified into a single analytical framework

---

## Key definitions

| Term | Definition |
|:---|:---|
| ANC4+ | At least 4 antenatal care visits during pregnancy (WHO minimum recommendation) |
| SBA | Skilled Birth Attendance — delivery attended by a doctor, nurse or trained midwife |
| MMR | Maternal Mortality Ratio — maternal deaths per 100,000 live births |
| U5MR | Under-5 Mortality Rate — deaths of children under 5 per 1,000 live births |
| NMR | Neonatal Mortality Rate — deaths in the first 28 days of life per 1,000 live births |
| Linda Mama | Kenya's free maternity programme launched 2016, covering all public facility deliveries |
| KDHS | Kenya Demographic and Health Survey — nationally representative household survey |

---

## Data sources

- Kenya Demographic and Health Survey 2022: `dhsprogram.com`
- County-level pre-aggregated data: `data.humdata.org/dataset/dhs-data-for-kenya`
- WHO Global Health Observatory API: `ghoapi.azureedge.net/api`
- UN MMEIG maternal mortality estimates: `who.int/data/maternal-newborn-child-adolescent-ageing`
- Kenya KHIS 2023: `hiskenya.org`
- UNICEF State of the World's Children 2023

---

**Patience Anono** · PA Data Analytics · [padataanalytics.com](https://padataanalytics.com) · hello@padataanalytics.com · @pa_analytics
