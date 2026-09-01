# GOBI Export to Excel Converter

This workspace converts tab-delimited GOBI export files into Excel workbooks with a consistent 15-column layout.

## Files

- `GOBI_to_excel_converter.ipynb`: the conversion notebook.
- `requirements.txt`: required Python package list.
- `EXPORTS/`: source GOBI exports.
- `CONVERSIONS/`: converted Excel workbooks.

## Setup

The notebook requires Python 3.10 or newer and `openpyxl`.

```bash
python3 -m venv .venv
.venv/bin/python -m pip install -r requirements.txt ipykernel
.venv/bin/python -m ipykernel install --user --name gobi-excel-converter --display-name "GOBI Excel Converter"
```

In VS Code, open `GOBI_to_excel_converter.ipynb`, select **GOBI Excel Converter** from **Select Kernel**, then run the cells in order.

## Converting Files

The notebook scans the directory it is running in for `.txt`, `.tsv`, and `.tab` files. File names do not matter. A file is treated as a GOBI export only when its header row contains all required columns.

The converter creates an `.xlsx` workbook next to each source file. To keep the current folder structure, run the notebook with `EXPORTS` as its working directory, then move completed workbooks to `CONVERSIONS` if needed.

## Output Columns

Each workbook contains these columns, in this order:

`Title`, `Author`, `Editor`, `Pub_Year`, `ISBN`, `LCCN`, `LC/NLM/Dewey_Class`, `Subaccount`, `Fund_Code`, `PO_Number`, `Supplier`, `Purchase_Option`, `Quantity`, `Initials`, `YBP_Order_Key`

## Safeguards

- Validates the required columns before converting a file.
- Prints every missing required column for incomplete GOBI-style files.
- Skips unreadable or empty text files.
- Does not overwrite or duplicate an `.xlsx` file that already exists with the same base name.
- Removes NUL characters from source rows before parsing.

To re-create an existing workbook after changing its source file, delete the matching `.xlsx` file first and rerun the notebook.