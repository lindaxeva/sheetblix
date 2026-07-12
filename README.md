# Sheetblix

**Sheetblix turns your spreadsheet-style CSV file into a clear data-quality audit snapshot.** 

It shows whether the data is current, what values appear in repeated-category columns, how frequently those values occur, and where missing or inconsistently entered information may require review.

Sheetblix was developed for the **GLOCAL Foundation of Canada** to help volunteers, staff, researchers, and non-technical users reduce repetitive spreadsheet checks and identify outdated, missing, or inconsistently entered data before it affects summaries, dashboards, reports, or administrative work.

Sheetblix supports human review. It identifies possible issues without automatically changing the original CSV file.

---

## Live Demos

| Demo | Main Capabilities | Access |
|---|---|---|
| Browser Application | Upload a CSV and view the file dimensions, overall freshness, date-column analysis, stale-row counts, categorical glossaries, missing values, frequencies, and percentages. | [Open Sheetblix](https://lindaxeva.github.io/sheetblix/) |
| Python Command-Line Tool | Analyze CSV files locally, customize freshness thresholds, generate focused reports, and export results as text, Markdown, or JSON. | [View the Repository](https://github.com/lindaxeva/sheetblix) |

---

## Project Snapshot

| Area | Summary |
|---|---|
| Business Need | Make routine CSV data checks faster, more consistent, and easier for non-technical users to understand. |
| Primary Challenge | Outdated records, missing values, and inconsistent category labels can remain hidden inside spreadsheets and quietly affect reporting. |
| Primary Users | Volunteers, administrative staff, researchers, students, and other users working with spreadsheet-style data. |
| Organization | GLOCAL Foundation of Canada |
| Solution Lead & Developer | Linda Eva Seuna |
| Current Stage | Functional prototype |
| Input | Spreadsheet-style CSV files |
| Browser Output | File summary, overall freshness, date-column details, stale-row counts, categorical glossary cards, missing-value information, counts, percentages, and visual frequency bars |
| Command-Line Output | Text, Markdown, or JSON data-quality reports |
| In Scope | CSV analysis; row and column counts; date detection; freshness summaries; stale-row reporting; categorical glossaries; missing-value reporting; capitalization and spacing checks; browser-based local processing; configurable command-line reports |
| Out of Scope | Direct Excel or Google Sheets analysis; automatic factual verification; automatic correction of source data; advanced typo detection; semantic matching; database storage; user accounts; multi-user collaboration; formal approval workflows |

---

## Current State and Future State

| Current State Challenge | Future State With Sheetblix |
|---|---|
| Users manually count rows and inspect spreadsheet columns. | File dimensions are displayed automatically. |
| Date columns must be reviewed row by row to determine whether data is current. | Sheetblix summarizes the oldest date, newest date, days since the newest date, and overall freshness. |
| Individual outdated records can be difficult to identify. | Stale rows are counted and displayed as a number and percentage. |
| Users may not immediately understand what values exist in a column. | Categorical glossary cards show the values contained in repeated-category columns. |
| Category distributions must be calculated manually. | Counts, percentages, and visual frequency bars are generated automatically. |
| Blank cells may remain unnoticed. | Missing values and their percentages are clearly reported. |
| Values such as `Active`, `active`, and ` ACTIVE ` may be counted separately. | Possible capitalization and surrounding-space variations can be identified for review. |
| Spreadsheet checks may be performed differently by different people. | The same repeatable checks can be applied whenever a CSV is reviewed. |
| Command-line tools may be difficult for non-technical users. | A browser version provides a simple visual interface. |
| Package installation can prevent users from running small automation tools. | The Python version uses only the standard library and requires no external packages. |
| Users may be concerned about uploading operational data. | The browser version analyzes files locally on the user’s device. |

---

## Project Objectives

Sheetblix was designed to:

- Reduce repetitive manual CSV inspection.
- Provide an immediate summary of a file’s rows and columns.
- Identify recognizable date columns.
- Show the oldest and newest valid dates in each detected date column.
- Determine whether the newest data is fresh, aging, or old.
- Count rows that exceed the stale-data threshold.
- Create a readable glossary of categorical values.
- Display category counts and percentages.
- Make missing categorical values easier to notice.
- Surface possible capitalization and spacing inconsistencies.
- Present findings in a format that non-technical users can understand.
- Preserve the original CSV file.
- Support human review rather than automatic correction.
- Produce reusable text, Markdown, and JSON reports.
- Keep browser-based analysis on the user’s device.

---

## Key Requirements

| Requirement Type | Requirement |
|---|---|
| Business Requirement | Reduce the time and effort required to perform routine data-quality checks on CSV files. |
| Stakeholder Requirement | Present findings clearly enough for volunteers, staff, researchers, and non-technical users to understand and act on. |
| Functional Requirement | Analyze CSV files for structure, date freshness, stale records, categorical values, missing entries, and possible formatting inconsistencies. |
| Usability Requirement | Provide both a visual browser application and a Python command-line interface. |
| Non-Functional Requirement | Run with Python 3.8 or newer without requiring third-party Python packages. |
| Privacy Requirement | Process browser-selected files locally without intentionally uploading them to an external server. |
| Transparency Requirement | Explain what was found without silently changing the original file. |
| Human-Review Requirement | Leave corrections and final data-quality decisions to the user. |

---

## Core Functional Requirements

| ID | Requirement | Expected Behaviour |
|---|---|---|
| FR-01 | Accept CSV input | The user can select a CSV in the browser or provide a CSV filepath through the command line. |
| FR-02 | Display file details | Sheetblix shows the file name, number of data rows, and number of columns. |
| FR-03 | Inspect column contents | The populated values in each column are examined. |
| FR-04 | Classify columns | Columns are classified as date, number, category, text, or empty. |
| FR-05 | Detect date columns | Columns containing mostly recognizable date values are selected for freshness analysis. |
| FR-06 | Calculate overall freshness | The most recent valid date across the detected date columns is used to determine the overall freshness status. |
| FR-07 | Summarize date columns | Sheetblix displays the oldest date, newest date, days since the newest date, and freshness status for each detected date column. |
| FR-08 | Count stale rows | The number and percentage of rows older than the stale-data threshold are displayed. |
| FR-09 | Detect categorical columns | Columns containing a relatively small set of repeated values are treated as categorical. |
| FR-10 | Create categorical glossaries | Each detected categorical column is summarized using its distinct values, counts, percentages, and visual frequency bars. |
| FR-11 | Report missing values | Blank entries are counted and displayed as a number and percentage. |
| FR-12 | Identify possible variations | Values that differ only by capitalization or surrounding spaces can be surfaced for human review. |
| FR-13 | Support focused reports | Command-line users can request only the freshness analysis or only the categorical glossary. |
| FR-14 | Support configurable thresholds | Command-line users can change fresh-day, stale-day, category, and reference-date settings. |
| FR-15 | Produce reusable outputs | Command-line reports can be displayed or saved as text, Markdown, or JSON. |
| FR-16 | Preserve the source file | Sheetblix analyzes the CSV without automatically modifying it. |
| FR-17 | Protect browser-file privacy | Browser analysis occurs locally on the user’s device. |
| FR-18 | Support repeated analysis | Users can select **Analyze another file** and review a different CSV. |

---

## Business Rules

| Rule | System Response |
|---|---|
| The input must be a readable CSV file. | Sheetblix attempts to read the file and reports an error when it cannot be processed. |
| The first row of the CSV is treated as the column-header row. | Column names are used throughout the report. |
| A column must contain mostly recognizable date values to be classified as a date column. | Unsupported or highly inconsistent date columns may be treated as text. |
| Data no more than 30 days old is considered fresh by default. | The date column receives a **Fresh** status. |
| Data between 31 and 90 days old is considered aging by default. | The date column receives an **Aging** status. |
| Data more than 90 days old is considered stale or old by default. | The date column receives an **Old** status. |
| Stale-row calculations use the selected reference date and stale-day threshold. | Sheetblix displays the stale-row count and percentage. |
| A categorical column must remain within the configured distinct-value limit. | High-cardinality columns may be classified as text instead. |
| Blank entries in categorical columns must be reported. | The missing count and percentage are displayed. |
| Capitalization and surrounding spaces are ignored when comparing possible category variations. | Similar-looking values can be grouped or surfaced for review. |
| Semantic meaning must not be assumed. | Sheetblix does not automatically treat `ON` and `Ontario` as the same value. |
| The original CSV must remain unchanged. | Findings are reported without automatically correcting the source file. |
| Final decisions must remain with the user. | Sheetblix supports review but does not replace human judgment. |

Automated findings identify possible issues. Users should confirm the context before updating, deleting, combining, or standardizing records.

---

## Solution Workflow

| Step | User Action | System Response |
|---|---|---|
| 1. Prepare | Save the spreadsheet-style data as a CSV file. | The file becomes compatible with Sheetblix. |
| 2. Open | Visit the browser application or open the command-line tool. | Sheetblix becomes ready to receive a CSV. |
| 3. Select | Choose a CSV in the browser or provide its filepath in the command line. | The file is read locally. |
| 4. Summarize | Begin the analysis. | Sheetblix displays the file name, row count, and column count. |
| 5. Inspect Dates | Review the overall freshness and date-column table. | The oldest date, newest date, days since, status, and stale-row results are displayed. |
| 6. Inspect Categories | Review the categorical glossary cards or report. | Values, counts, percentages, frequency bars, and missing entries are shown. |
| 7. Review Findings | Examine outdated records, missing values, and possible category variations. | Sheetblix provides evidence without changing the source file. |
| 8. Decide | Determine which records or values require correction, updating, removal, or standardization. | Final decisions remain with the user. |
| 9. Export | Select an output format when using the command-line version. | A text, Markdown, or JSON report is displayed or saved. |
| 10. Recheck | Analyze the corrected file again. | The same repeatable checks are applied to the updated CSV. |

---

## Command-Line Usage

The Python version requires Python 3.8 or newer and uses only built-in Python libraries.

Clone the repository:

```bash
git clone https://github.com/lindaxeva/sheetblix.git
cd sheetblix
```

Run the included sample file:

```bash
python3 sheetblix.py sample_data.csv
```

On some Windows installations, use:

```bash
python sheetblix.py sample_data.csv
```

The general command structure is:

```bash
python3 sheetblix.py YOUR_FILE.csv [options]
```

### Complete report

```bash
python3 sheetblix.py sample_data.csv
```

### Freshness analysis only

```bash
python3 sheetblix.py sample_data.csv --freshness-only
```

### Categorical glossary only

```bash
python3 sheetblix.py sample_data.csv --glossary-only
```

### Save a Markdown report

```bash
python3 sheetblix.py sample_data.csv --format markdown --output report.md
```

### Produce JSON output

```bash
python3 sheetblix.py sample_data.csv --format json
```

### Use a custom stale threshold and reference date

```bash
python3 sheetblix.py sample_data.csv --stale-days 60 --today 2026-06-26
```

### Command Options

| Option | What It Does | Default |
|---|---|---|
| `--format` | Selects `text`, `markdown`, or `json` output. | `text` |
| `--output` | Saves the report to a file instead of displaying it on screen. | Screen |
| `--freshness-only` | Displays only the freshness analysis. | Off |
| `--glossary-only` | Displays only the categorical glossary. | Off |
| `--max-categories` | Sets the maximum number of distinct values allowed for a categorical column. | `20` |
| `--top` | Sets the maximum number of common values shown for each categorical column. | `10` |
| `--fresh-days` | Sets the maximum age for data to be considered fresh. | `30` |
| `--stale-days` | Sets the age after which data is considered old. | `90` |
| `--today` | Sets the reference date used for freshness calculations. | Current date |

---

## Testing and Acceptance

The project includes automated tests that use Python’s built-in `unittest` framework.

Run the tests from the repository folder:

```bash
python3 -m unittest -v
```

A successful test run should finish with:

```text
OK
```

Testing covers areas such as:

- CSV file reading
- Row and column counts
- Column-type identification
- Date-format recognition
- Oldest and newest date detection
- Freshness calculations
- Custom reference dates
- Custom freshness thresholds
- Stale-row counts
- Categorical value counts
- Category percentages
- Missing-value detection
- Capitalization variations
- Spacing variations
- Text output
- Markdown output
- JSON output
- Freshness-only mode
- Glossary-only mode
- Invalid input and error handling

Sheetblix meets its acceptance criteria when:

- A valid CSV can be analyzed.
- The correct file name, row count, and column count are displayed.
- Recognizable date columns are identified.
- Oldest and newest dates are summarized correctly.
- An overall freshness status is produced.
- Stale rows are counted and displayed as a percentage.
- Categorical columns are summarized.
- Category values, counts, and percentages are displayed.
- Missing categorical values are reported.
- Possible capitalization and spacing variations are surfaced.
- The original CSV remains unchanged.
- Browser-selected files remain on the user’s device.
- The Python version runs without third-party packages.
- Automated tests complete successfully.

Test outcomes depend on the supplied file and its formatting. Unusual dates, malformed CSV structures, or highly distinct columns may affect how information is classified.

---

## Value Delivered

| Value | Outcome |
|---|---|
| Efficiency | Reduces the time spent manually inspecting CSV files. |
| Consistency | Applies the same basic data-quality checks whenever a file is reviewed. |
| Visibility | Makes outdated records, missing values, and category distributions easier to notice. |
| Clarity | Presents file dimensions, counts, percentages, and statuses in an understandable format. |
| Reliability | Helps users identify issues that may affect filters, summaries, charts, dashboards, and reports. |
| Accessibility | Provides both browser-based and command-line ways to use the tool. |
| Privacy | Keeps browser-selected files on the user’s device. |
| Transparency | Reports findings without silently changing the original data. |
| Reusability | Produces text, Markdown, and JSON reports that can support different workflows. |
| Maintainability | Uses Python’s standard library without third-party package dependencies. |
| Human Oversight | Leaves corrections and final data-quality decisions to the user. |

---

## Tools

Python · HTML · CSS · JavaScript · CSV · JSON · Markdown · Git · GitHub · GitHub Pages · GitHub Actions

---

## Privacy

Users should avoid including confidential, restricted, or personally identifiable information in public sample files, screenshots, repositories, documentation, or shared reports.
