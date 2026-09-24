# Swedish broker and fund comparisons

Open `world_fund_comparison.ipynb` in Jupyter and run the cells from top to bottom. It includes the original single-fund comparisons and a World + Emerging Markets portfolio comparison: two iShares ETFs on IBKR versus DNB Global Indeks S and DNB Global Emerging Markets Indeks S on Avanza. The portfolio uses an editable 90/10 World/EM split by default. Set `REFRESH_DATA = True` in the download cell to request updated histories. The Länsförsäkringar Global Index NAV history is downloaded automatically when its source CSV is missing.

## Data files

- `data/dnb_global_indeks_a_nav_nok.csv` — DNB Global Indeks A daily NAV series in NOK (Morningstar history ID `F00000JORS`, ISIN `NO0010582984`).
- `data/lansforsakringar_global_index_nav_sek.csv` — Länsförsäkringar Global Index daily NAV in SEK (Morningstar history ID `F00000PYZ6`, ISIN `SE0005188836`); fetched by the notebook if missing.
- `data/ishares_core_msci_world_eunl_xetra_eur.csv` — EUNL Xetra daily EUR market prices (Yahoo Finance chart data; ETF ISIN `IE00B4L5Y983`).
- `data/ecb_daily_rates_source.csv` — ECB Data Portal daily EUR reference rates for SEK and NOK, in original CSV format.
- `data/ecb_daily_eur_fx.csv` — compact ECB history in SEK and NOK per EUR.
- `data/aligned_performance_sek.csv` — comparison series aligned to weekdays and converted to SEK.
- `data/eunl_vs_lansforsakringar_global_index_sek.csv` — EUNL and Länsförsäkringar Global Index series aligned over their shared history and rebased for comparison.
- `data/ishares_core_msci_em_imi_is3n_xetra_eur.csv` — IS3N Xetra daily EUR market prices for iShares Core MSCI Emerging Markets IMI (ISIN `IE00BKM4GZ66`); downloaded by the added portfolio section when missing.
- `data/dnb_global_index_s_nav_sek.csv` and `data/dnb_global_em_index_s_nav_sek.csv` — Avanza SEK return histories rebased to an index level of 100 for the DNB S share classes; downloaded by the added section when missing.
- `data/world_em_portfolio_performance_sek.csv` — aligned SEK portfolio performance series.
- `data/world_em_portfolio_performance_summary.csv` — cumulative and annualized returns over the shared period.
- `data/world_em_monthly_simulation_results.csv` and `data/world_em_monthly_trades.csv` — contribution simulation results and trade-level estimates for the two-fund portfolio.

Data and cost references: [DNB Global Indeks A](https://m.dnb.no/en/saving/mutual-funds/fund-list/d/dnb-global-indeks-a-NO0010582984), [iShares fund page](https://www.ishares.com/uk/individual/en/products/251882/ishares-core-msci-world-ucits-etf), [ECB SDMX API](https://data.ecb.europa.eu/help/api/data-examples), [IBKR European stock/ETF commissions](https://www.interactivebrokers.com/en/pricing/commissions-stocks.php), and [IBKR FX commissions](https://brokerage.ibkr.com/en/pricing/commissions-spot-currencies.php).

The combined history starts on 24 September 2010, the first date with a DNB A NAV observation, and runs through 21 September 2026, the latest date common to all three price/rate sources in the downloaded files. Weekday prices and FX values are carried forward over source-market holidays for the aligned chart; monthly purchases use the latest available observation on or before month-end.

## Cost model notes

IBKR commission and automatic FX conversion defaults are based on the published schedules linked in the notebook. The ETF spread is an editable estimate rather than a historical bid/ask series. DNB and iShares ongoing cost rates are shown for disclosure and sensitivity analysis, but are not charged a second time because the observed fund NAV / ETF price series already reflect fund-level expenses. ISK tax and sale/liquidation costs are excluded.

The original DNB A history is quoted in NOK. Its SEK conversion is included in performance, but the DNB route has no separate FX transaction fee by default, following the chosen assumption. In the new portfolio section, “DNB Global” is interpreted as DNB Global Indeks S to match the index-fund comparison; the section uses Avanza SEK price histories and models no Avanza FX fee. Both simulations share the monthly contribution, broker commission, FX, and ETF spread assumptions defined near the start of the notebook. The World/EM weights and fund-cost disclosures are set there too.

Historical results are not forecasts or exact broker statements. Prices and ECB reference rates are end-of-day proxies, and the DNB and ETF portfolios are similar developed-market exposures rather than identical portfolios.
