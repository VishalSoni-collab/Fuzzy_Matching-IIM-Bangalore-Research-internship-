# IIM-Bangalore-Research-internship-
I worked on a research internship at IIM Bangalore, focusing on fuzzy matching systems for company stock analysis, applying machine learning techniques to enhance financial data accuracy and deepen my understanding of AI in financial analysis.


# Fuzzy Match Project

This project implements fuzzy matching between two datasets to identify entries that are approximately similar, specifically matching brand names with company names. This is achieved through the `fuzzymatcher` library, which uses similarity algorithms to match non-identical but similar strings.

## Project Purpose

Matching entries across datasets is often complicated by inconsistencies in naming conventions, spellings, or abbreviations. This project solves that problem by leveraging fuzzy matching—a technique that finds close matches based on calculated similarity scores rather than requiring exact matches.

This README provides a full conceptual summary of each element within the code to help users understand the methodology, underlying mechanisms, and specific logic applied in each step.

## Key Concepts and Workflow

### 1. Data Loading and Initial Setup
- **Objective:** Prepare datasets and inspect initial data structures.
- **Implementation:**
  - Two CSV files are loaded into `pandas` DataFrames: one containing brand information (`brand_manufacturer.csv`) and the other containing NSE (Equity) information (`EQUITY_L.csv`).
  - **Inspect Data:** The `.head()` method is used to display the initial rows, ensuring data integrity and format compatibility.
- **Key Libraries:**
  - `pandas`: Essential for data loading and manipulation.
  - `fuzzymatcher`: Provides robust fuzzy join capabilities.

### 2. Matching Configuration
- **Objective:** Specify the columns to use for matching.
- **Implementation:**
  - Define columns intended for comparison:
    - `left_on`: `brand_name` from the Brand dataset.
    - `right_on`: `NAME OF COMPANY` from the NSE dataset.
  - **ID Columns:** `left_id_col` and `right_id_col` are set to uniquely identify each record, providing the flexibility to match records accurately back to the source.
- **Conceptual Insight:**
  - **Fuzzy Matching Requirements:** For effective fuzzy matching, the algorithm requires clearly defined columns that will be used to assess similarity. By specifying the matching columns (`left_on` and `right_on`), we ensure that the algorithm targets relevant fields, increasing matching accuracy.

### 3. Fuzzy Matching Execution
- **Objective:** Apply fuzzy matching to identify approximate matches between datasets.
- **Implementation:**
  - **Fuzzy Left Join:** Using `fuzzymatcher.fuzzy_left_join`, the project performs a left join based on approximate matching criteria. This method aligns records based on a similarity score rather than requiring exact text matches.
  - **Similarity Scoring:** Each potential match is assigned a `best_match_score`, which quantifies the level of similarity between the two entries (values range from 0 to 1, where scores close to 1 indicate higher similarity).
- **Mechanism Insight:**
  - **How It Works:** `fuzzymatcher` uses a blend of tokenization, word vectorization, and similarity algorithms (like Levenshtein Distance) to compute the best match score. The score indicates how closely two strings resemble each other by comparing character sequences, word orders, and other factors.
  - **Advantages of Fuzzy Matching:** This approach is beneficial in cases of inconsistent naming, minor typos, or abbreviations that would prevent traditional joins from succeeding.

### 4. Result Filtering and Column Selection
- **Objective:** Filter and select the most relevant columns to display matched records clearly.
- **Implementation:**
  - **Column Filtering:** After performing the fuzzy join, only essential columns (`best_match_score`, `brand_name`, and `NAME OF COMPANY`) are retained. This allows for easy analysis of the results.
  - **Sorting by Match Score:** The output is sorted by `best_match_score` in descending order, prioritizing the most confident matches.
- **Conceptual Insight:**
  - **Importance of Filtering and Sorting:** By selecting only the necessary columns and sorting by similarity, the output becomes more interpretable, making it easier to evaluate the effectiveness of matches. High scores near 1 signify close matches, which helps users focus on the most relevant data.

### 5. Output Interpretation and Further Applications
- **Objective:** Display and interpret the final matching results.
- **Implementation:**
  - **Data Display:** The notebook concludes with a preview of the final, sorted matches. This output format is designed to allow users to evaluate and verify the quality of the matches.
  - **Example Applications:**
    - **Data Cleaning and Deduplication:** Fuzzy matching can help identify and resolve near-duplicate entries in data cleansing tasks.
    - **Record Linkage:** Useful in applications where entries from disparate sources need to be aligned or merged.
- **Conceptual Insight:**
  - **Interpretation of Scores:** The `best_match_score` serves as an accuracy measure, with scores closer to 1 indicating strong matches. Users can apply thresholds based on their tolerance for false positives, allowing flexible use cases.

## Complete Code Walkthrough

The code's structure emphasizes clarity and efficiency by defining each component with precision. Below is a consolidated summary of each block.

### Data Loading and Libraries
- Imports `pandas` and `fuzzymatcher`.
- Loads the `brand_manufacturer.csv` and `EQUITY_L.csv` files, storing them in DataFrames `df` and `NSE`, respectively.

### Matching Setup
- Defines `left_on`, `right_on`, `left_id_col`, and `right_id_col` to align `brand_name` with `NAME OF COMPANY`.

### Fuzzy Matching Execution
- Performs a fuzzy join with `fuzzymatcher.fuzzy_left_join()`.
- Generates `best_match_score` to quantify the similarity between `brand_name` and `NAME OF COMPANY`.

### Filtering and Sorting Results
- Retains columns (`best_match_score`, `brand_name`, `NAME OF COMPANY`) and sorts by `best_match_score` for easy analysis.

## Example Output

The output includes `best_match_score`, `brand_name`, and `NAME OF COMPANY`, with high scores signifying strong matches. This setup is effective for use cases like:

- **Data Deduplication:** Identifying and merging near-duplicate entries to maintain clean data.
- **Record Linkage:** Linking records across different datasets based on approximate matching.
- **Standardizing Entries:** Ensuring consistency across datasets with slight variations in naming conventions.

A sample output might look like this:

| best_match_score | brand_name      | NAME OF COMPANY                   |
|------------------|-----------------|-----------------------------------|
| 0.95             | Example Brand A | Example Company A                 |
| 0.89             | Sample Brand B  | Sample Company B                  |
| 0.85             | Demo Brand C    | Demonstration Company C           |

In this table:
- **High `best_match_score` values** (close to 1) indicate stronger matches.
- **Lower scores** may indicate weaker matches or potential mismatches, depending on the threshold you choose.

## Usage Instructions

### Installation
Ensure `pandas` and `fuzzymatcher` are installed:
```bash
pip install pandas fuzzymatcher


