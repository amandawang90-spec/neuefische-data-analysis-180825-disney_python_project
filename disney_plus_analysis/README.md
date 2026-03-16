# 🎬 Disney+ Content Analysis

> A pure-Python data analysis project exploring Disney+ movies and TV shows — uncovering trends in content ratings, genres, directors, durations, and regional availability to support strategic investment decisions.

---

## 📌 Table of Contents

- [Project Overview](#-project-overview)
- [Dataset](#-dataset)
- [Project Structure](#-project-structure)
- [Setup & Installation](#-setup--installation)
- [Usage](#-usage)
- [Function Reference](#-function-reference)
- [Sample Output](#-sample-output)
- [Key Insights](#-key-insights)
- [Skills Demonstrated](#-skills-demonstrated)

---

## 📖 Project Overview

This project analyses a combined dataset of movies and TV shows to answer critical business questions for the Content Manager. The findings influence future content investments and release strategies.

**Core questions addressed:**
- What are the unique content ratings, and how is content distributed across them?
- What is the average duration of movies vs. TV shows?
- How many titles are available in Germany, broken down by year?
- Which director has the highest output, and in which genre?

---

## 📦 Dataset

| Property | Details |
|----------|---------|
| **Source** | [Kaggle — Disney Movies and TV Shows](https://www.kaggle.com/datasets/shivamb/disney-movies-and-tv-shows) |
| **File** | `data/disney_plus_titles.csv` |
| **Records** | 1,450+ titles |
| **Format** | CSV |

### Data Dictionary

| # | Column | Description |
|---|--------|-------------|
| 1 | `show_id` | Unique identifier |
| 2 | `type` | Movie or TV Show |
| 3 | `title` | Title of the content |
| 4 | `director` | Director(s) |
| 5 | `cast` | Main cast members |
| 6 | `country` | Country of production |
| 7 | `date_added` | Date added to Disney+ |
| 8 | `release_year` | Original release year |
| 9 | `rating` | Content rating (e.g. PG, TV-G) |
| 10 | `duration` | Runtime (minutes or seasons) |
| 11 | `listed_in` | Genre(s) |
| 12 | `description` | One-line synopsis |

---

## 🗂 Project Structure

```
disney-plus_analysis/
│
├── data/
│   └── disney_plus_titles.csv       # Raw dataset
│
├── disney_content_analysis.ipynb    # Main analysis notebook
├── README.md                        # Project documentation
```

---

## ⚙️ Setup & Installation

### Prerequisites

- Python 3.8 or higher
- Jupyter Notebook or JupyterLab

### Steps

1. **Clone the repository**
   ```bash
   git clone https://github.com/amandawang90-spec/neuefische-data-analysis-180825-disney_python_project/tree/main/disney_plus_analysis
   cd disney-analysis
   ```

2. **Create and activate a virtual environment** *(optional but recommended)*
   ```bash
   python -m venv venv
   source venv/bin/activate        # macOS/Linux
   venv\Scripts\activate           # Windows
   ```

3. **Install dependencies**
   ```bash
   pip install notebook
   ```
   > No third-party data libraries required — this project uses only Python's built-in `csv` module.

4. **Download the dataset**
   - Download from [Kaggle](https://www.kaggle.com/datasets/shivamb/disney-movies-and-tv-shows)
   - Place `disney_plus_titles.csv` inside the `data/` folder

5. **Launch the notebook**
   ```bash
   jupyter notebook disney_content_analysis.ipynb
   ```

---

## 🚀 Usage

The notebook is structured step-by-step:

1. **Read & split data** — Load the CSV and separate the header from the data rows
2. **Explore & clean** — Inspect values, handle inconsistencies
3. **Analyse** — Apply reusable functions to answer business questions
4. **Filter & count** — Slice the dataset by country, year, rating, genre, and more

---

## 📚 Function Reference

### `filter_data(data, filter_criteria)`

Filters the dataset based on one or more column conditions. Supports both exact matches and comma-separated multi-value fields (e.g. multiple countries or genres).

| Parameter | Type | Description |
|-----------|------|-------------|
| `data` | `list` | Full dataset as a list of lists |
| `filter_criteria` | `dict` | `{col_index: value}` pairs to filter by |

**Returns:** `list` — filtered rows matching all criteria

```python
# Example: titles from Germany released in 2004
filter_criteria = {5: "Germany", 7: "2004"}
filtered = filter_data(data, filter_criteria)
```

---

### `elements_count(data, col_index, sep=None, filters={})`

Counts and ranks occurrences of values in a given column. Supports optional delimiter splitting (e.g. splitting `"Comedy, Family"` into individual genres) and pre-filtering.

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `data` | `list` | — | Full dataset |
| `col_index` | `int` | — | Column index to count values in |
| `sep` | `str` | `None` | Delimiter to split multi-value cells |
| `filters` | `dict` | `{}` | Optional filter criteria (same format as `filter_data`) |

**Returns:** `dict` — `{value: count}` sorted by count descending

```python
# Example: genre distribution for German titles from 2004
result = elements_count(data, col_index=10, sep=",", filters={5: "Germany", 7: "2004"})
# Output: {'Comedy': 2, 'Action-Adventure': 1, 'Family': 1, 'Coming of Age': 1}
```

---

## 📊 Sample Output

### Content filtered by country and year
```
filter_criteria = {5: "Germany", 7: "2004"}

['s629', 'Movie', 'Around the World in 80 Days', 'Frank Coraci', ...]
['s799', 'Movie', 'Confessions of a Teenage Drama Queen', 'Sara Sugarman', ...]
```

### Genre breakdown for German titles (2004)
```python
{'Comedy': 2, 'Action-Adventure': 1, 'Family': 1, 'Coming of Age': 1}
```

---

## 💡 Key Insights

- **Ratings:** The most common content ratings on Disney+ are `TV-G` and `TV-PG`, reflecting the platform's family-friendly focus.
- **Duration:** Movies average around 90 minutes; TV shows are typically listed by season count rather than runtime.
- **Germany:** A small but consistent selection of titles are associated with German production, spread across multiple years.
- **Directors:** Certain directors appear repeatedly, especially in animation and family genres.

---

## 🧠 Skills Demonstrated

| Skill | Application |
|-------|-------------|
| Python strings | Parsing, splitting, and cleaning cell values |
| Descriptive statistics | Counting, averaging, and ranking content attributes |
| Reusable functions | Modular, docstring-documented functions usable by non-technical stakeholders |
| CSV handling | Using Python's built-in `csv` module without pandas |
| Data filtering | Multi-condition filtering with support for multi-value fields |

---

*Project completed as part of a data analytics training programme.*