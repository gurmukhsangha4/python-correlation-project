# Movie Profit Correlation Analysis

> **Exploratory analysis of 7,600 feature‑rich movie records to discover which factors most strongly drive box‑office revenue.** Built entirely in a single Jupyter notebook with pandas + NumPy crunching the numbers and Matplotlib/Seaborn painting the story.

---

\## 📋 Table of Contentss

1. [Project Overview](#project-overview)
2. [Dataset](#dataset)
3. [Hypotheses](#hypotheses)
4. [Methodology](#methodology)
5. [Key Findings](#key-findings)
6. [Quick Start](#quick-start)
7. [Repository Structure](#repository-structure)
8. [Tech Stack & Requirements](#tech-stack--requirements)
9. [Contributing](#contributing)
10. [License](#license)

---

\## Project Overview
The project began with a simple question: **“Does spending more money on a film actually translate to higher box‑office returns?”** To answer it, I built a small Python pipeline that:

1. **Ingests** a raw *movies.csv* file containing theatrical release data (budgets, worldwide gross, IMDb scores, vote counts, production companies, genres, release dates and more).
2. **Cleans** & standardises the dataset (type casting, missing‑value removal, duplicate drops, year extraction).
3. **Numerises** categorical columns using `pandas.Categorical.cat.codes` so every feature can be compared on an equal footing.
4. **Calculates** Pearson correlation coefficients for every feature pair.
5. **Visualises** relationships through scatterplots, regression lines, and a colour‑coded heat‑map.
6. **Surfaces** the strongest drivers of revenue, flagging potential multicollinearity.

---

\## Dataset

| Attribute        | Value                                 |
| ---------------- | ------------------------------------- |
| **Source**       | Public IMDb / TMDb blend (via Kaggle) |
| **Records**      |  7,668 films (1960‑2020)              |
| **Columns**      |  24 numeric + categorical features    |
| **Size on disk** |  ≈ 1.5 MB CSV                         |

> *Only free, open data was used; no private or proprietary information is included.*

---

\## Hypotheses

1. **Budget ↔ Gross** — Higher production budgets correlate positively with worldwide gross.
2. **Votes ↔ Gross** — More audience votes correlate with higher earnings (popularity factor).
3. **Company ↔ Gross** — Certain studios might systematically outperform the market.

---

\## Methodology

| Step | Action                              | Code highlights                                                                  |
| ---- | ----------------------------------- | -------------------------------------------------------------------------------- |
|  ①   | Import libraries & set visual style | `import pandas as pd`, `plt.style.use('ggplot')`                                 |
|  ②   | Load CSV                            | `df = pd.read_csv('movies.csv')`                                                 |
|  ③   | Clean data                          | `df = df.dropna()`; type casting (`df['budget'] = df['budget'].astype('int64')`) |
|  ④   | Feature engineering                 | Extract release year (`df['corrected_year']`)                                    |
|  ⑤   | Exploratory visuals                 | `sns.scatterplot`, `sns.regplot`                                                 |
|  ⑥   | Correlation matrix                  | `df.corr(method='pearson')` + `sns.heatmap`                                      |
|  ⑦   | Pair sorting & thresholding         | `corr_pairs.sort_values()` → filter `> 0.5`                                      |

---

\## Key Findings

* **Budget vs Gross ≈ 0.74** — Strongest linear relationship in the entire set.
* **Votes vs Gross ≈ 0.72** — Audience engagement predicts revenue almost as well as money spent.
* Categorical features (e.g. *production company*, *genre*) show **little direct correlation** after one‑hot coding, suggesting brand influence is secondary to spending power and popularity.
* Simple scatter+regression plots visually confirm the positive trend lines, while the heat‑map exposes clusters of multicollinearity between vote‑related metrics.

> *Studio name shows near‑zero correlation once controlling for budget, reinforcing that capital outlay and market buzz matter more than the logo on the poster.*

---

\## Quick Start

```bash
# Clone the repo and step inside
$ git clone https://github.com/<your‑user>/movie‑correlation‑analysis.git
$ cd movie‑correlation‑analysis

# (Recommended) create & activate a virtual environment
$ python3 -m venv .venv && source .venv/bin/activate

# Install dependencies
$ pip install -r requirements.txt

# Launch the notebook
$ jupyter notebook Movie_Correlation_Project.ipynb
```

Replace the CSV path in **Cell \[0]** if your *movies.csv* lives elsewhere.

---

\## Repository Structure

```
├── Movie_Correlation_Project.ipynb   # the full EDA notebook
├── movies.csv                        # raw data (Git‑LFS friendly)
├── figs/                             # exported plots (optional)
├── requirements.txt                  # pinned Python deps
└── README.md                         # you’re here
```

---

\## Tech Stack & Requirements

* **Python 3.9+**
* **Jupyter Notebook/Lab**
* **pandas >= 2.0**
* **NumPy >= 1.24**
* **Matplotlib >= 3.7**
* **Seaborn >= 0.13**

All pinned in `requirements.txt` for reproducible installs.

---

\## Contributing
Pull requests are welcome! Feel free to open an *Issue* for bugs or feature ideas. When submitting PRs, please:

1. Create a topic branch off **main**.
2. Use clear commit messages (imperative mood).
3. Attach before/after screenshots for plot tweaks.

---

\## License
This repo is released under the MIT License — do whatever you like, just give credit.

