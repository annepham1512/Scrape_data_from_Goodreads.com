```markdown
# Goodreads Data Scraping & Analysis

Welcome to the **Goodreads Data Scraping & Analysis** repository! This project demonstrates how to scrape, clean, and analyze book data from [Goodreads.com](https://www.goodreads.com) using **Python**, **Selenium**, and **BeautifulSoup**. 

We focus on:
1. **Task 1:** Exploring the "Best Books of \<Year\>" (e.g., 2023).
2. **Task 2:** Performing an **author-level** analysis by scraping an entire bibliography (example: Stephen King).

---

## Features

- **Automated Web Scraping**
  - Single-pass or batch-based approach to handle large lists or prolific authors.
  - Robust error handling and logging via Selenium.

- **Data Cleaning & Transformation**
  - Converts strings like `"12.5k"` or `"2,500"` into proper integers.
  - Handles missing fields, normalizes date/time for publication, and more.

- **Exploratory Analyses**
  - Genre-based rating comparisons.
  - Scatter plots for popularity vs. average rating.
  - Author-level insights (language distribution, age vs. page count, etc.).

---

## Repository Structure

Below is a suggested organization (feel free to adapt to your needs):

```
.
├── data
│   ├── books_data_1.csv              # "Best Books" raw dataset
│   ├── books_data_2.csv              # Author-level raw dataset
│   └── cleaned_data
│       ├── books_data_1_cleaned.csv  # Cleaned CSV (Task 1)
│       └── books_data_2_cleaned.csv  # Cleaned CSV (Task 2)
├── notebooks
│   └── final_analysis.ipynb          # Jupyter notebook demonstrating full E2E analysis
├── scripts
│   ├── scraping_functions.py         # Selenium-based scraping functions
│   ├── data_cleaning.py              # Functions for data cleaning & parsing
│   └── data_analysis.py              # Visualizations & summary analyses
├── log
│   ├── scraping_log.txt              # Log file from scraping (Task 1)
│   └── scraping_log_2.txt            # Log file from scraping (Task 2)
├── README.md                         # Project overview and instructions
└── requirements.txt
```

- **`data/`**: Holds both raw CSV outputs (`books_data_1.csv`, `books_data_2.csv`) and final cleaned versions.  
- **`scripts/`**: Where the main scraping and data-processing code resides.  
- **`notebooks/`**: Example Jupyter notebook(s) for an end-to-end demonstration.  
- **`log/`**: Run-time logs with error or progress messages.  
- **`requirements.txt`**: Dependencies for Python environment.

---

## Getting Started

### 1. Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/username/goodreads-scraping.git
   cd goodreads-scraping
   ```

2. Create a **virtual environment** (optional but recommended):
   ```bash
   python -m venv venv
   source venv/bin/activate  # Or venv\Scripts\activate on Windows
   ```

3. Install requirements:
   ```bash
   pip install -r requirements.txt
   ```

4. Ensure you have a **Selenium WebDriver** (ChromeDriver or GeckoDriver) installed or placed in your `PATH`.

---

### 2. Usage

#### Task 1: Best Books Scraping

1. **Set the target URL** (e.g., `"https://www.goodreads.com/list/best_of_year/2023"`) in your scraping code.  
2. Run the scraper:
   ```bash
   python scripts/scraping_functions.py --task best_books --year 2023
   ```
3. The raw output (e.g., `books_data_1.csv`) will be saved in the `data` folder.  
4. **Clean and analyze**:
   ```bash
   python scripts/data_cleaning.py --input data/books_data_1.csv --output data/cleaned_data/books_data_1_cleaned.csv
   python scripts/data_analysis.py --input data/cleaned_data/books_data_1_cleaned.csv
   ```

#### Task 2: Author-Level Analysis

1. **Fetch all book links** for an author’s bibliography:
   ```bash
   python scripts/scraping_functions.py --task author_links --authorid 3389  # Example: Stephen King
   ```
2. **Batch scrape** to handle large bibliographies:
   ```bash
   python scripts/scraping_functions.py --task author_scrape --batch 1 --start 0 --end 100
   python scripts/scraping_functions.py --task author_scrape --batch 2 --start 100 --end 200
   # etc.
   ```
3. **Combine partial CSVs** and clean:
   ```bash
   python scripts/data_cleaning.py --merge data/book_scrape_2/*.csv --output data/books_data_2.csv
   python scripts/data_cleaning.py --input data/books_data_2.csv --output data/cleaned_data/books_data_2_cleaned.csv
   ```
4. **Analyze**:
   - Language distribution
   - Page count vs. rating
   - Author’s age vs. publication trends
   ```bash
   python scripts/data_analysis.py --input data/cleaned_data/books_data_2_cleaned.csv
   ```

---

### 3. Examples in Notebooks

Open the Jupyter notebook for a step-by-step demo:
```bash
jupyter notebook notebooks/final_analysis.ipynb
```

The notebook showcases:

- A quick run-down of scraping (with sample code).  
- Cleaning numeric fields (`"1.2k" => 1200`, `"2,500" => 2500`).  
- Visual exploration (scatter plots, histograms, etc.).  

---

## Key Analyses

**1. Genre-Based Ratings**  
- For “Best Books of \<Year\>,” compare average ratings across genres, investigate popularity vs. rating.

**2. Language Distribution**  
- In author-level scraping, see how many translations exist and in which languages.

**3. Author’s Age & Book Attributes**  
- Plot the relationship between age at publication and page counts or average ratings.

**4. Popularity vs. Ratings**  
- Scatter/Regression plots to see if more popular (high number of ratings) books also rank higher.

---

## Contributing

Contributions are welcome! Please open an **issue** or submit a **pull request** with any changes or suggestions. For major updates, start a discussion first to ensure alignment with the project’s goals.

---

## License

This project is licensed under the [MIT License](LICENSE). You’re free to use, modify, and distribute it as long as you retain the license and attributions.
```
