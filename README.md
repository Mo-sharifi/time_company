# Time Company Analysis

This repository contains a data analysis project based on a fictional company called **"Time Company"**.  
The goal was to process three CSV datasets, apply a set of business rules, and generate a final table of employees with their updated hourly wages.

---

## Problem Description
- Each employee can work in multiple units (departments).
- Every unit has a fixed **hourly wage**.
- Each employee has an **importance factor** per unit that determines their effective hourly pay.
- For every employee–unit pair, the company defines a minimum **expected monthly working hours**.

**Termination rule:**
- If an employee, in any unit, works fewer hours than expected in a given month, that month is considered *lost*.
- If an employee loses 6 or more months over the year, they are terminated.

**Importance update rule (for non-terminated employees):**

- Calculate the yearly ratio:

  $$
  ratio = \frac{\text{worked hours in year}}{12 \times \text{expected monthly hours}}
  $$

- Update importance based on the ratio:
  - `1 < ratio ≤ 1.25` → +0.25  
  - `1.25 < ratio ≤ 1.5` → +0.5  
  - `ratio > 1.5` → +1.0  

- The new hourly wage is:

$$
new\_wage = ⌊ importance_{new} \times hourly_wage ⌋
$$

---

## Input Data
Three CSV files were provided:
1. **table1.csv** – employees, units, importance, and expected monthly hours  
2. **table2.csv** – unit IDs and their hourly wage  
3. **table3.csv** – monthly working hours of each employee per unit  

---

## Output
The program generates a CSV file named **`submission.csv`** with the following format:

| 0 (employee_id) | 1 (unit_id) | 2 (new_wage) |
|-----------------|-------------|--------------|
| 67              | 1           | 31680        |
| 844             | 1           | 19800        |
| 908             | 1           | 29880        |

Notes:
- Terminated employees are excluded from the output.
- The order of rows follows the order of the first input table.
- Column headers must be exactly `0,1,2`.

---

## Steps Implemented
1. Load and clean the data (rename Persian column headers to English).
2. Identify terminated employees based on lost months.
3. For the remaining employees, calculate performance ratios and update importance.
4. Compute new hourly wages and build the final output table.
5. Save the result as `submission.csv`.

---

## How to Run
Clone the repo and install dependencies:

```bash
git clone https://github.com/yourusername/time-company-task.git
cd time-company-task
pip install -r requirements.txt
