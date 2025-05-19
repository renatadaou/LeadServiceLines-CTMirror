# LeadServiceLines-CTMirror

## Step 1 - Putting the sheets together 

1) In the folder called all_files, we can see the eaw files that were obtained by FOIA requests by our investigative reporter Andrew Brown. There are a total of 701 files.

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

4) The outcome is a sheet called all_files_initial_material that has 889,624 rows
