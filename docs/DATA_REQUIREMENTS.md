# Input Data and Reproducibility Notes

This repository **does not include** the study's raw survey CSV, market history CSV, or completed human-evaluation records.

## 1. Financial and behavioral survey CSV

Upload the source survey CSV at the first `files.upload()` prompt. The code accesses these original column labels, among others:

- `Timestamp`
- `Age`
- `Number of Dependents`
- `Do you have a monthly gross income range between ₱24,060–₱144,360?`
- `1. Average Monthly Gross Income`
- `2. Average Monthly Expenses`
- `3. Average Monthly Net Savings`
- `4. Total Average Educational Expenses (for further studies or of dependents)`
- `5. Do you have current loans/debts? (If yes, please specify the estimated total amount)`

Two additional, long open-ended questions are required. Their exact labels in the supplied source are:

```text
7. How do you feel about investing in high-risk, high-reward platforms (like Crypto or Stocks) compared to keeping your money in a traditional bank? (Do you strictly prefer one over the other, or do you prefer to put half in the bank and half in investments?)
9. Imagine you invested ₱10,000, and after one week, its value dropped to ₱7,000. What would you do and how would you feel? (e.g., Would you panic and sell everything, buy more because it's cheap, or just observe and wait?)
```

The program expects **the original survey schema**, not just these listed columns. Additional fields may be used in descriptive and reporting steps. Do not publish responses or full participant data without explicit authorization, appropriate consent, and privacy review.

## 2. Historical Philippine Stock Exchange Index CSV

Upload at the separate PSEi prompt. Minimum required headers:

```csv
Date,Close
```

`Date,Price` is also supported; the script renames `Price` to `Close`. Date formats need to be parseable by `pandas.to_datetime`, and closing prices must be numerical or convertible to numbers. Historical prices are user-provided; the notebook does not fetch them automatically.

## 3. Researcher-consensus validation sheet

The notebook creates an annotation CSV for a sample of behavioral responses, with independent reviewer label fields `Researcher_1_Label`, `Researcher_2_Label`, `Researcher_3_Label`. Later cells prompt you to upload the **completed** file. Human labels should use the three categories specified in the notebook.

## 4. Qualitative evaluation sheet

The notebook exports an evaluation worksheet for reviewers with fields such as `Clarity_Rating`, `Transparency_Rating`, `Relevance_Rating`, and `Perceived_Usefulness_Rating`. A later cell expects the completed worksheet to be uploaded.

## Sharing outputs safely

The notebook creates respondent-level intermediate and final reports (`filtered_respondents.csv`, `output_results/`, annotation records, etc.). These are intentionally ignored by Git. **Git ignore rules are not a substitute for a privacy review**; check filenames and file contents before publishing.

### Reproducibility status

The notebook's code was reconstructed from the provided Colab-exported Python file. Its cells were checked for Python syntax (with the Colab `!pip` command handled separately), but **no full research execution or results verification** was performed, because original inputs and review sheets were not provided.
