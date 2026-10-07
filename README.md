# GS1 Weight Fixer

Fills in zero carton weights in inbound shipment spreadsheets using the
weight encoded in each carton's GS1-128 barcode.

## Live App

**URL:** `https://lavertoncoldstorage.github.io/gs1-weight-fixer/`

## What it does

Some suppliers' shipment files (e.g. the JUN / LEAKS RD files that arrive by
email) contain cartons with an **Expected Weight of 0**, even though the real
weight is in the barcode in the **Expected Serial Number** column. This page:

- Finds the weight column and the GS1 barcode column automatically (can be
  overridden under "Columns used")
- For every row with a weight of 0, reads the net weight from AI **310n**
  (net kg, n = decimal places), e.g. `3102 001570` = 15.70 kg.
  Falls back to 330n (gross kg) or 320n (lb, converted) and flags it.
- Lists every change with the row number, item and highlighted barcode
- Flags zero weights it couldn't fix (no weight in the barcode) so they can be
  fixed by hand
- Optionally fills blank weights, and optionally corrects non-zero weights
  that disagree with the barcode (both off by default)
- **Download CSV for Thomax** gives `<original name>.csv` in exactly the format the
  Thomax SFTP `GenericASN` folder takes (UTF-8 with BOM, CRLF, dates dd/mm/yyyy),
  with only the weight cells changed. A fixed `.xlsx` is also available.

No login, no server - files are read and written entirely in the browser.

## How to Use

1. Save the attachment from the email
2. Open the page and drop the file in (several at once is fine)
3. Check the list of changes
4. Click **Download CSV for Thomax** and save it to
   `S:\Production\ToWMS\PurchaseOrder\GenericASN`

## Files

- `index.html` - the whole app (uses SheetJS from cdnjs for reading/writing Excel)
- `Chilled-LavertonCS-1.png` - Laverton Cold Storage logo

## Questions / changes

Contact Matt Rowe.
