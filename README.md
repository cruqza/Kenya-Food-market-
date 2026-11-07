# Kenya food prices (maize, 2006–2019)

Analysis of WFP Kenya food-price data (Humanitarian Data Exchange, CC BY-IGO 3.0) for **white maize** and **dry beans**.

## What's in the repository

- `data/food_prices_kenya.csv` — the cleaned extract: **2,742 rows, 9 columns**.
  - **Wholesale:** 90-kg bags, 5 markets (Nairobi, Mombasa, Kisumu, Eldoret, Nakuru), 721 rows.
  - **Retail:** 1 kg, 9 county markets (Garissa, Hola, Kajiado, Kilifi, Kitui, Lodwar, Mandera, Marigat, Marsabit), 2,021 rows.
  - Date is a real date (15th of each month) with `year` and `month` columns added. Wholesale and retail are deliberately kept in separate dataframes.
- `analysis.ipynb` — the worked-out analysis (see below). Do not edit unless you intend to change the analysis.
- `pamoja-note.md` — a one-page note with advice for farmers (3) and county officers (1), each backed by a number from the notebook, with data credit.
- `src/kenya_food_2/` — the Python package. Currently contains only the package init (`__init__.py`); `main()` is the console entry point declared in `pyproject.toml`.

## What the notebook does

1. Loads and cleans the CSV — real dates, plus `year` and `month` columns.
2. Fills the missing region/county for **Hola** (Tana River County, Coast) — 59 rows.
3. Splits the data into **wholesale** (90-kg bags) and **retail** (1 kg) so the two kinds of price are never averaged together.
4. Converts wholesale prices to per-kg (`price_kes / 90`) for apples-to-apples comparison.
5. Annual averages with year-over-year change; monthly averages (cheapest = January, dearest = June).
6. Storage test: January vs June wholesale maize per 90-kg bag, year by year, by market (a five-month storage window).
7. Box plot of wholesale maize by market and summary statistics (mean, median, min, max).
8. Retail maize (2015–2019) market ranking: most expensive = Lodwar (KES 75.85/kg), cheapest = Kitui (36.19), and the only two markets in the top three every year (Lodwar and Mandera).

## Key figures at a glance

| Metric | Value |
| --- | --- |
| Wholesale maize price/kq, 2006–2019 | 28.54 KES/kg (mean, 721 rows) |
| Retail maize price/kq, 2015–2019 | 47.92 KES/kg (mean) |
| January vs June wholesale maize | 2,329.52 → 2,839.47 KES/90-kg bag (+22%) |
| Storage test | 73.33% of market-years profitable; median gain 356 KES/bag |
| Most expensive retail market (2015–2019) | Lodwar — 75.85 KES/kg |
| Cheapest retail market (2015–2019) | Kitui — 36.19 KES/kg (2.1× cheaper than Lodwar) |

## Data credit

WFP Kenya – Food Prices, Humanitarian Data Exchange (HDX), licence **CC BY-IGO 3.0**, downloaded 24 October 2026. Wholesale markets in Nairobi, Mombasa, Kisumu, Eldoret and Nakuru; retail markets in nine counties.
