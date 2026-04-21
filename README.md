# Earnings Quality Inspector: Python Analysis of Cash Flow and Accruals for Tech Stocks
## 1. Problem & User
**Problem:** How can investors use only publicly available financial statement data to detect early warning signs of earnings quality deterioration in Microsoft, Amazon, and Google?
**User:** Accounting and finance students, and fundamental investors who want to look beyond headline net income and assess whether reported profits are backed by sustainable cash flows and conservative accounting.
## 2. Data
- **Source:** WRDS Compustat – Fundamentals Annual
- **Access Date:** April 2026
- **Tickers:** MSFT, AMZN, GOOGL
- **Period:** Fiscal Years 2019–2025
- **Key Fields:** Net Income (`ni`), Operating Cash Flow (`oancf`), Capital Expenditures (`capx`), Accounts Receivable (`rect`), Inventory (`invt`), Accounts Payable (`ap`), Revenue (`revt`), Total Assets (`at`), Total Liabilities (`lt`), Total Equity (`teq`)
## 3. Methods
The analysis is implemented in Python within a Jupyter Notebook. Main steps include:
1. **Data Acquisition:** SQL query via `wrds` package to extract financial statements from Compustat.
2. **Data Cleaning:** Removal of rows with missing critical values, sorting by ticker and date.
3. **Metric Calculation:** Cash flow quality: `cfo_to_ni`, `fcf_to_ni`; Accrual intensity: total accruals (NI – CFO) scaled by total assets; Working capital red flags: receivables growth minus revenue growth; Earnings persistence: rolling coefficient of variation of net income.
4. **Visualisation:** Four-panel dashboard using `matplotlib` and `seaborn`.
5. **Composite Scoring:** A rule-based scoring function aggregates metrics into a final letter grade (A–F).
## 4. Key Findings
- **Microsoft (MSFT): Grade A** – Strong cash flow conversion (CFO/NI > 1.2), very low accruals, stable earnings.
- **Alphabet (GOOGL): Grade A** – Healthy cash flow backing, minimal accruals, moderate volatility.
- **Amazon (AMZN): Grade D** – Exceptionally strong cash flow but high earnings volatility and a persistent receivables–revenue gap trigger scoring penalties. The low grade reflects model sensitivity to volatility rather than earnings manipulation.
*The analysis highlights that mechanical scoring models should be interpreted in light of a firm's business model.*
## 5. How to Run
1. Clone the repository: `git clone https://github.com/yourusername/earnings-quality-inspector.git` then `cd earnings-quality-inspector`
2. Install dependencies: `pip install -r requirements.txt`
3. Launch Jupyter Notebook: `jupyter notebook earnings_quality_analysis.ipynb`
4. In the notebook, replace `'your_username'` with your own WRDS username in the connection cell.
*If you do not have WRDS access, you can still review the analysis logic and pre-computed outputs shown in the notebook.*
## 7. Limitations & Next Steps
- **Peer group size:** Only three companies are compared; a broader industry sample would improve benchmarking.
- **Data frequency:** Annual data may obscure intra-year accrual reversals; quarterly data would be more granular.
- **Scoring thresholds:** Heuristic cut-offs are not empirically validated; future work could use percentile ranks.
- **Methodological enhancements:** Winsorisation of outliers, fiscal-year alignment (Microsoft's June year-end vs. December), deduplication of Alphabet's dual-class shares, and incorporation of the Dechow-Dichev accrual quality model would strengthen academic rigour.
---
*Submitted by: Yulin Ke (Student ID: 2472203)*  
*Date: 20 April 2026*
