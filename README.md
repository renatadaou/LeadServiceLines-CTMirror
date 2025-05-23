# Lead Service Lines - CTMirror

Note: Used ChatGPT and Claude to clean and improve code 

## Step 1 - Putting the sheets together 

1) In the folder called `all_files`, we can see the raw files that were obtained by FOIA requests by our investigative reporter Andrew Brown. There are a total of 701 files.

2) The spreadsheets have the “Initial Material Inventory” tab. To make analysis easier, we wanted to combine all spreadsheets into one, based on the “Initial Material Inventory” tab. We selected a few columns of interest such as:
 - SITE ID
 - LOCATION IDENTIFIER
 - STREET ADDRESS
 - TOWN	
 - STATE
 - ENTIRE SERVICE LINE MATERIAL CLASSIFICATION
 - BUILDING TYPE
 - SOURCE FILE
 - Because some water systems changed the “street address” column, we need to add STREET NUMBER and STREET NAME

3) I had to pay extra attention to empty rows under the column names: na_values=['#REF!', '#N/A', '#NAME?', '#DIV/0!', '#NULL!', '#NUM!', '#VALUE!', '#ERROR!']
   
4) Jupyter notebook file (`lead-step1-allfiles.ipynb`)
- Reads Excel files from a specified folder.
- Searches for sheets matching a given pattern (e.g., "Initial Material Inventory").
- Tries to detect the header row dynamically (if not always the first row).
- Extracts and standardizes a list of required columns (like "SITE ID", "STREET ADDRESS", etc.).
- Optionally combines "STREET NUMBER" and "STREET NAME" into a single "STREET ADDRESS".
- Cleans and filters the data (removes empty rows, renames columns, removes partial header rows, etc.).
- Returns a cleaned, unified DataFrame.

5) The outcome is a sheet called `all_files_initial_material` that has 889,624 rows

## Step 2 - Verifying that code worked

1) Get random files to test and see if the outcome for those files only matched the outcome in `all_files_initial_material`
- Test the code on the random files and then manually check if the outcome on the combined fiel is the same as the original file

2) Random files, round 1 of testing: Passed 100%
- CT0210023 LCRR SL Material Inventory State Review Checklist.xlsx  \\ Did not run - did not have an initial material page
- CT0210023__LCRR_Inventory_Initial_09-10-24.xlsx
- CT0235033_LCRR_Inventory_Initial 10 16 2024.xlsx
- CT0240262_LCRR_Inventory_Initial_101824 .xlsx
- CT0261081_LCRR_Inventory_Initial_10.16.24.xlsx
- CT0780081_LCRR_Inventory_Initial_10.16.24.xlsx
- CT0780121_LCRR_Inventory_Initial_10.16.24.xlsx
- CT0960224_LCRR_Inventory_Initial 10 16 2024.xlsx
- CT1680041_LCRR_Inventory_Initial_09-27-24.xlsx
- CT1680071_LCRR_Inventory_Initial 10 15 2024.xlsx
3) Random files, round 2 of testing, using the heaviest files: Passed 100%
- 2024-10-15_CT1510011 Waterbury_LCRR_initial_material_inventory.xlsx
- CT0150011_LCRR_Inventory_Initial_10.16.24.xlsx \\ Skipped two lines, but those two lines did not have any information in the desired column, so the code didn’t read them
- CT0473011_LCRR_Inventory_Initial_10.16.24.xlsx
- CT0580031_LCRR_Inventory_Initial 10 15 2024.xlsx
- CT0608011_LCRR_Inventory_Initial_10.16.24.xlsx
- CT0800011_LCRR_Inventory_Initial_10.15.24.xlsx
- CT0880011_LCRR_Inventory_Initial_10.16.24.xlsx
- CT0930011_LCRR_Inventory_Initial_10.16.24.xlsx
- CT1090221_LCRR_Inventory_Initial_10-01-24.xlsx
- CT1510011_LCRR_Inventory_Initial_10.15.24.xlsx

## Step 3 - Doing the same process for Updated Material Inventory
 
1) I did the same thing as step 1, just with the “Updated Material Inventory” tab. Some water systems updated the material of their water lines after the first inspection. Some changed, some didn’t.

2) The code is more complicated for this tab, because the content in the rows are not as standardized and not following the same patterns across spreadsheets. 

3) One of the code updates is that it detects common Excel error strings (#REF!, #VALUE!, etc.). Instead of deleting these rows, it blanks out the SITE ID value and adds a flag column to mark the issue.

4) It also drops rows with SITE ID = 0 and all other columns empty. This is the only place where rows are actually removed. Only deletes rows where SITE ID is zero, and every other field is empty.

5) Flags rows where SITE ID exists but there's no corresponding location, address, or town.

6) Uses fuzzy/variant matching
   
8) This file is not used as much. Outcome in the `updated_material_inventory` file with 525,508 rows


