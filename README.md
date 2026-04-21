# Earnings Quality Inspector: Python Analysis of Cash Flow and Accruals for Tech Stocks

## 1. Problem & User
How can investors use only publicly available financial statement data to detect early warning signs of earnings quality deterioration in Microsoft, Amazon, and Google? Reported net income can be inflated by non-cash accruals or one-time items. This project provides a multi-dimensional assessment of earnings quality by examining cash flow support, accrual intensity, working capital trends, and earnings persistence. The target users are accounting and finance students and fundamental investors who seek to move beyond headline EPS.

## 2. Data
Data are sourced exclusively from WRDS Compustat – Fundamentals Annual (table `comp.funda`), accessed in April 2026. The sample covers fiscal years 2019–2025 for Microsoft (MSFT), Amazon (AMZN), and Alphabet (GOOGL), yielding 21 firm-year observations after cleaning. Key fields extracted include net income (`ni`), operating cash flow (`oancf`), capital expenditures (`capx`), accounts receivable (`rect`), inventory (`invt`), accounts payable (`ap`), revenue (`revt`), total assets (`at`), total liabilities (`lt`), and total equity (`teq`). A valid WRDS account is required to replicate the data extraction.

## 3. Methods
The analysis is implemented in a Jupyter Notebook using Python 3.8+ with `pandas`, `numpy`, `matplotlib`, `seaborn`, and the `wrds` package. The workflow proceeds as follows: (1) SQL query to extract financials from WRDS; (2) data cleaning by dropping rows with missing critical fields; (3) calculation of year-over-year growth rates for revenue, net income, receivables, inventory, and payables; (4) computation of four categories of earnings quality metrics: cash flow quality (`cfo_to_ni`, `fcf_to_ni`), accrual intensity (`total_accruals / at`), working capital red flags (`rect_growth - rev_growth` with a 10% threshold), and earnings persistence (rolling 5-year coefficient of variation of net income); (5) generation of a 2×2 visual dashboard; and (6) a heuristic scoring function that assigns points based on threshold values and maps the total to a letter grade (A–F).

## 4. Key Findings
- **Microsoft (MSFT): Grade A** – Operating cash flow consistently exceeds net income (CFO/NI > 1.2), accruals are below 2% of total assets, and earnings volatility is the lowest among peers.
- **Alphabet (GOOGL): Grade A** – Strong cash conversion (CFO/NI > 1.0), minimal accruals, and moderate earnings volatility reflect a high-quality earnings profile.
- **Amazon (AMZN): Grade D** – Despite exceptionally strong cash flow (latest CFO/NI = 1.80) and negative accruals, the model penalises Amazon for high earnings volatility (CV = 0.77) and a persistent receivables–revenue growth gap exceeding 10%. The D grade highlights the model's sensitivity to volatility rather than fundamental earnings manipulation.

## 5. How to run
Launch Jupyter Notebook and open `earnings_quality_analysis.ipynb`. In the WRDS connection cell, replace `'your_username'` with your own WRDS credentials. Run all cells sequentially to reproduce the full analysis. Users without WRDS access can still view the pre-executed outputs and follow the analytical narrative.

## 6. Submission contents
This submission includes the following deliverables as required for Track 2: (a) a public GitHub repository containing the complete Jupyter Notebook, README file, requirements.txt, and output figures; (b) a 1–3 minute demonstration video walking through the analysis workflow and key findings; and (c) a 500–800 word reflection report addressing problem definition, dataset selection, Python methods, insights, limitations, and AI use disclosure.

## 7. Limitations & next steps
The analysis has several limitations: a small peer group of only three firms restricts generalisability; annual data frequency may obscure intra-year accrual reversals; heuristic scoring thresholds are not empirically calibrated; outliers are not winsorised; and fiscal year-ends are not aligned (Microsoft ends in June, others in December). Future improvements could expand the sample, apply winsorisation, align fiscal periods, and incorporate established models such as Dechow-Dichev (2002) to measure accrual quality more rigorously.
