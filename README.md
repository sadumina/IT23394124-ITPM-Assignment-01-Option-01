# Test Automation

This project runs Excel-driven UI tests against the Singlish-to-Sinhala translator using Playwright and writes the results back into the Excel workbook.

## Prerequisites

- Python 3.11 or newer
- Windows PowerShell
- Internet access for the target website under test

## Project Files

- [test_automation.py](/C:/Users/Sadumina.Rathnayaka/Desktop/test_automation/test_automation/test_automation.py): main test runner
- [Assignment 1 - Test cases.xlsx](/C:/Users/Sadumina.Rathnayaka/Desktop/test_automation/test_automation/Assignment%201%20-%20Test%20cases.xlsx): original test case workbook

## Install Dependencies

Open PowerShell in the project folder and run:

```powershell
python -m pip install --upgrade pip
python -m pip install playwright openpyxl
python -m playwright install chromium
```

## Run The Tests

Important: close `Assignment 1 - Test cases.xlsx` before running the script.

If the Excel file is open, Windows locks it and the script may save to a fallback results file instead of updating the original workbook.

### Run Against The Original Excel File Only

This command updates only `Assignment 1 - Test cases.xlsx`:

```powershell
python test_automation.py --excel "Assignment 1 - Test cases.xlsx" --output "Assignment 1 - Test cases.xlsx"
```

### Run Only The First 50 Selected Test Cases

```powershell
python test_automation.py --excel "Assignment 1 - Test cases.xlsx" --output "Assignment 1 - Test cases.xlsx" --limit 50
```

### Run In Headless Mode

Use this if you do not want the browser window to be shown:

```powershell
python test_automation.py --excel "Assignment 1 - Test cases.xlsx" --output "Assignment 1 - Test cases.xlsx" --limit 50 --headless
```

## Helpful Options

- `--limit 50`: run only 50 selected rows
- `--headless`: run without showing the browser
- `--url "<site-url>"`: override the default website URL
- `--sheet " Test cases"`: choose the Excel sheet name
- `--keep-open`: keep the browser open after the run

## Notes

- The script reads test data from the Excel file and writes `Actual output` and `Status` back into the workbook.
- The script also auto-fills `Singlish input types covered` and `Evidence or rationale for the input type covered` based on the input text.
- If `Expected output` is empty, the script marks the row as `COLLECTED`.
- If `Expected output` has a value, the script marks the row as `PASS` or `FAIL`.
- The default target site is `https://www.pixelssuite.com/chat-translator`.

## Troubleshooting

### Excel file is not updated

Make sure:

- the workbook is closed in Excel
- the temporary lock file `~$Assignment 1 - Test cases.xlsx` does not exist
- you passed both `--excel` and `--output` as the same file name if you want to update only the original workbook

### Browser does not start

Reinstall the Playwright browser:

```powershell
python -m playwright install chromium
```

### Missing package errors

Install dependencies again:

```powershell
python -m pip install playwright openpyxl
```
