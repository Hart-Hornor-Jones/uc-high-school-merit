# data/ — curated derived datasets

Derived from public UC and CDE records (see repo `README.md` → "Data sources"). Raw downloads
(≈12 GB) are not committed. Full column notes for the legacy panel are in
[`../docs/DATA_DICTIONARY.md`](../docs/DATA_DICTIONARY.md).

| File | Grain | Notes |
|---|---|---|
| `panel_all9_by_year.csv` | campus × school × year | **Master per-year panel**, all 9 campuses, 2015–2025. Funnel + covariates. Powers the site. |
| `dv_admissions_all9.csv` | campus × school × year | Admissions funnel only (applicants/admits/enrollees + admit GPA), all 9 campuses, **1994–2025**. |
| `cross_section_all9.csv` | campus × school | Tidy pooled cross-section for the default period (2023–2025) with every rate computed. |
| `components/` | school × year | Per-year covariates: `caaspp_YYYY.csv` (gr-11 % met), `ag_eligibility.csv` (cohort + UC/CSU-eligible), `upp_lcff.csv` (UPP % + grade 9–12 enrollment). |
| `ceeb_cds_crosswalk.csv` | school | UC CEEB ↔ CDE CDS bridge (~98% hand-verified). |
| `school_year_panel.csv` | campus × school × year | Berkeley & San Diego long panel (verified; includes admit GPA). Superseded for the site by the all-9 panel. |
| `cross_section_summary.csv` | campus | Published per-campus correlations / OLS — the **verification target**. |
| `then_vs_now_*.csv`, `yearly_trend.csv` | campus (× era/year) | Prior published correlation trends. |
| `elwr_school_year_wide.csv` | school × year | ELWR/AWPE writing-requirement rates (UC **enrollees** only; keyed by CEEB). |

## `panel_all9_by_year.csv` columns

`ceeb, cds14, campus, year, school_name, city, county, applicants, admits, enrollees, admit_rate,`
`adm_gpa, ela_pct_met, math_pct_met, avg_pct_met, ag_cohort, ag_met_uccsu_count, enroll_9_12,`
`upp_pct, lcff_plus, match_method, match_score`

- The funnel (`applicants/admits/enrollees`) is UC; covariates are CDE, joined per year via the
  crosswalk. **Blank ≠ 0** (UC suppresses small cells). CAASPP 2020 is absent (cancelled) and
  2021 is excluded (COVID, non-representative); those years carry funnel + A–G/UPP only.
- Year alignment (matches the original build): CAASPP uses the same year; A–G uses grad cohort
  `(year-1)-(year)`; UPP uses pupil year `(year-1)-(year)`.

## `cross_section_all9.csv` columns (default period 2023–2025)

`campus, ceeb, cds14, school_name, city, county, applicants, admits, enrollees, admit_rate, yield,`
`application_rate, admits_per_eligible, enr_per_eligible, apps_per_enrollment, admits_per_enrollment,`
`enr_per_enrollment, caaspp_ela_pct_met, caaspp_math_pct_met, caaspp_avg_pct_met, ag_completion_pct,`
`upp_pct, lcff_plus, awpe_writing_met_pct, awpe_year`

All rates are ratio-of-sums over jointly-observed years in the period. `admit_rate`/`yield` are %;
the `÷eligible` and `÷enrollment` ratios are unitless.

## Regenerate

```bash
python3 ../scripts/build_panel_all9.py     # → panel_all9_by_year.csv
python3 ../scripts/make_site_data.py       # → ../data.js (+ cross_section_all9.csv)
```
