# Reliance Digital Product Data Analysis

An end-to-end data project: **scrape** product listings from Reliance Digital, **clean** the raw data, **analyze** pricing and discount patterns, and **visualize** the findings.

- **Source:** [Reliance Digital](https://www.reliancedigital.in/)
- **Scraped on:** 08-09-2023 (as recorded in the `Date` column)
- **Size:** 2,803 products across 6 categories
- **Tools:** Python, Requests, BeautifulSoup, Pandas, NumPy, Matplotlib, Seaborn

---

## Project Workflow

```
Scrape (Requests + BeautifulSoup)  ->  Clean (Pandas)  ->  Analyze (Pandas)  ->  Visualize (Matplotlib)
        dataset.csv                     clean_dataset.csv     Analysis.ipynb        Visualization.ipynb
```

### 1. Data Collection (Web Scraping)
Product listings were collected with the `requests` and `beautifulsoup4` libraries. For each product the scraper captured:

| Field | Description |
|---|---|
| Product Name | Full product title as listed |
| Prices | Listed price (₹) |
| Discount | Discount label such as `60% OFF` |
| Category | Mobile, Laptop, TV, Tablets, Watches, Refrigerator |
| Date | Date of scraping |
| Source | Reliance Digital |

The raw output is saved as `dataset.csv`.

### 2. Data Cleaning
Done in `Analysis.ipynb`:

- **Split product name:** `Product Name` is split into `Product_Name` (first two words, usually brand + model) and `Description` (the rest).
- **Discount:** removed the `OFF` and `%` text, converted to integers, and filled missing discounts with `0`.
- **Prices:** stripped currency symbols and commas (`[^\d.]`) and converted to numeric.
- **Column order:** rearranged to `Product Name, Product_Name, Description, Prices, Discount, Category, Date, Source`.
- **Validation:** checked for missing values, duplicate rows, prices <= 0, and discounts outside 0-100. No invalid prices or discounts were found.

The result is saved as `clean_dataset.csv`.

### 3. Analysis
Also in `Analysis.ipynb`. It covers:

- Price statistics (mean, min, max, median, quartiles, skewness)
- Category analysis (product counts, average price and discount per category)
- Product analysis (most and least expensive, highest discounts)
- Price vs discount correlation
- Data quality checks

### 4. Visualization
Charts are created in `Visualization.ipynb` (images below are saved in `charts/`).

---

## Key Findings

| Metric | Value |
|---|---|
| Average price | ₹62,987.75 |
| Median price | ₹37,999 |
| Minimum price | ₹195 (JioBook sleeve carry case) |
| Maximum price | ₹18,89,990 (LG 97" OLED evo AI TV) |
| Price quartiles (25% / 50% / 75%) | ₹16,994 / ₹37,999 / ₹80,997 |
| Price-discount correlation | -0.158 (weak negative) |

**By category**

| Category | Products | Avg price (₹) | Avg discount (%) |
|---|---:|---:|---:|
| Mobile | 888 | 52,419 | 13.2 |
| Laptop | 636 | 79,345 | 13.7 |
| TV | 348 | 91,325 | 29.3 |
| Tablets | 348 | 85,280 | 9.5 |
| Watches | 348 | 22,046 | 24.0 |
| Refrigerator | 235 | 44,308 | 25.3 |

- **Mobile** has the most products; **Refrigerator** has the fewest.
- **TV** has both the highest average price and the highest average discount.
- **Watches** have the lowest average price, and **Tablets** the lowest average discount.
- The biggest single discounts are on smartwatches (Fire-Boltt, up to **95% off**).
- Price and discount are only weakly related, so expensive products are not discounted much more or less than cheap ones.

---

## Charts

### Product Count by Category
<img width="1200" height="750" alt="image" src="https://github.com/user-attachments/assets/3ec1570e-990f-4970-9810-6835c8367162" />

### Average Price by Category
<img width="1200" height="750" alt="image" src="https://github.com/user-attachments/assets/2c5f2fc0-4aed-4375-8c8e-bb0cc7179283" />

### Average Discount by Category
<img width="1200" height="750" alt="image" src="https://github.com/user-attachments/assets/b6f30709-84e9-41d3-9b39-6fbbed196533" />

### Price vs Discount
Most products sit in the lower price range, and there is no strong linear relationship.

<img width="1200" height="750" alt="image" src="https://github.com/user-attachments/assets/1c564ef1-9aa9-4dde-bab1-4b4336b46465" />

### Top 5 Most Expensive Products
<img width="1500" height="750" alt="image" src="https://github.com/user-attachments/assets/7f719512-1490-4c0a-8d29-c5bcde455cce" />


---

## Repository Structure

```
.
├── README.md
├── scraper.py               # Requests + BeautifulSoup scraper
├── dataset.csv              # Raw scraped data
├── clean_dataset.csv        # Cleaned data
├── Analysis.ipynb           # Cleaning + analysis
├── Visualization.ipynb      # Charts
└── charts/                  # Exported chart images
```

## Getting Started

```bash
git clone <your-repo-url>
cd <your-repo-folder>
pip install requests beautifulsoup4 pandas numpy matplotlib seaborn jupyter
```

1. Run the scraper (`python scraper.py`) to produce `dataset.csv`.
2. Open `Analysis.ipynb` to clean the data and run the analysis.
3. Open `Visualization.ipynb` to reproduce the charts.

## Known Limitations

- `Product_Name` takes only the first two words of the title, so for some products it is a weak identifier (for example `LG 210` appears for two different TVs). Use `Product Name` for the full title.
- Accessories (laptop stands, cases, adapters) are included under their parent category, which lowers category averages.
- The data is a single-day snapshot (08-09-2023), so it shows no price trends over time.
- `clean_dataset.csv` includes three empty trailing columns (`Unnamed: 9-11`) that can be dropped.
- Scraped data may be subject to the website's terms of use. Check them before reusing it.

👤 Author
Shyam Singh

🌐 Connect With Me

🌍 Portfolio: shyam-tech.vercel.app

💻 GitHub: github.com/1m-shyam01

🔗 LinkedIn: linkedin.com/in/shyam-singh-190b7a2a6


⭐ If you found this project useful, consider giving it a star!
