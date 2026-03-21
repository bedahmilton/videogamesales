# 🎮 Video Game Sales: Data Cleaning & Optimization Project

This project transforms a raw dataset of over 64,000 video game records into a clean, memory-optimized format ready for analysis. The pipeline is implemented in Python using the `pandas` library.

---

## 📂 Data Source
The data is sourced from **Kaggle**:
- **Dataset:** [Video Game Sales and Industry Data (1980-2024)](https://www.kaggle.com/datasets/bhushandivekar/video-game-sales-and-industry-data-1980-2024)
- **File:** `Video Games Sales (1980-2024) - Raw.csv`

---

## 🧹 Data Cleaning Pipeline
The following steps were performed to ensure data integrity:

* **Standardizing Dates:** `release_date` and `last_update` were converted to `datetime64` objects with `dayfirst=True` to resolve parsing ambiguities.
* **Missing Value Imputation:** * Filled missing `critic_score` values with the **global median**.
    * Filled missing `total_sales` with the **column median**.
* **Text Normalization:** * Converted all game `title` entries to **Uppercase**.
    * Used **Regex** to identify and replace the string `"Unknown"` in the `publisher` column with `NaN`.
    * **Stripped whitespace** from the `developer` column to prevent duplicate grouping.
* **Duplicate Removal:** Identified and dropped 144 records with identical `title`, `console`, and `release_date`.
* **Logical Filtering:** Removed records with `total_sales` of 0 to focus on commercially released titles.

---

## 💾 Memory Optimization
A key focus of this project was reducing the RAM footprint of the DataFrame:

* **Categorical Encoding:** Converted `genre` and `console` columns to `category` dtypes.
* **Column Reduction:** Dropped the `img` column, which contained high-memory string URLs irrelevant to numerical analysis.
* **Index Management:** Performed a `reset_index(drop=True)` to convert the index back into a memory-efficient `RangeIndex`.

**Result:** Reduced memory usage from **6.8 MB** to **5.4 MB** (approx. 20% reduction) while maintaining all critical data.

---

## 🚀 Technical Summary
```python
# Final DataFrame Structure
# - 62,530 rows
# - 13 optimized columns
# - Cleaned CSV saved as: 'videogame_cleaned.csv'