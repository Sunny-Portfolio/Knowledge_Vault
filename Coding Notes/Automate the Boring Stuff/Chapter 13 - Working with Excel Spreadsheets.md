### Install OpenPyXL Module
```sh
pip install --user -U openpyxl==2.6.2
```


### Reading Excel Documents
| A             | B            | C   |
| ------------- | ------------ | --- |
| 4/5/15 13:34  | Apples       | 73  |
| 4/5/15 3:41   | Cherries     | 85  |
| 4/6/15 12:46  | Pears        | 14  |
| 4/8/15 8:59   | Oranges      | 52  |
| 4/10/15 2:07  | Apples       | 152 |
| 4/10/15 18:10 | Bananas      | 23  |
| 4/10/15 2:40  | Strawberries | 98  |

##### Opening Excel Documents with OpenPyXL
You can check your current working directory with `os.getcwd()`.
You an change your CWD using `os.chdir()`.
```py
>>> import openpyxl
>>> wb = openpyxl.load_workbook('example.xlsx')
>>> type(wb)
<class 'openpyxl.workbook.workbook.Workbook'>

>>> wb.sheetnames # The workbook's sheets' names.
['Sheet1', 'Sheet2', 'Sheet3']
>>> sheet = wb['Sheet3'] # Get a sheet from the workbook.
>>> sheet
<Worksheet "Sheet3">
>>> type(sheet)
<class 'openpyxl.worksheet.worksheet.Worksheet'>
>>> sheet.title # Get the sheet's title as a string.
'Sheet3'
>>> anotherSheet = wb.active # Get the active sheet.
>>> anotherSheet
<Worksheet "Sheet1">
```

##### Getting Cells from the Sheets
Accessing Worksheet object to access Cell object:
```py
>>> import openpyxl
>>> wb = openpyxl.load_workbook('example.xlsx')
>>> sheet = wb['Sheet1'] # Get a sheet from the workbook.
>>> sheet['A1'] # Get a cell from the sheet.
<Cell 'Sheet1'.A1>
>>> sheet['A1'].value # Get the value from the cell. <- datetime value
datetime.datetime(2015, 4, 5, 13, 34, 2)
>>> c = sheet['B1'] # Get another cell from the sheet.
>>> c.value
'Apples'
>>> # Get the row, column, and value from the cell.
>>> 'Row %s, Column %s is %s' % (c.row, c.column, c.value)
'Row 1, Column B is Apples'
>>> 'Cell %s is %s' % (c.coordinate, c.value)
'Cell B1 is Apples'
>>> sheet['C1'].value
73
```
OpenPyXL automatically interpret dates in column A and return them as *datetime* values rather than strings.

Dealing with two letter column can be tricky (AA, AB, AC). You can get a cell using `cell()` method and pass int for its row and column keyword arguments:
```py
>>> sheet.cell(row=1, column=2)
<Cell 'Sheet1'.B1>
>>> sheet.cell(row=1, column=2).value
'Apples'
>>> for i in range(1, 8, 2): # Go through every other row:
		print(i, sheet.cell(row=i, column=2).value)


1 Apples
3 Pears
5 Apples
7 Strawberries
```

Get the highest row and column number:
```py
>>> sheet = wb['Sheet1']
>>> sheet.max_row # Get the highest row number.
7
>>> sheet.max_column # Get the highest column number.
3
```

##### Converting Between Column Letters and Numbers
To convert from letters to numbers, call `openpyxl.utils.column_index_from_string()`.
To convert from numbers to letters, call `openpyxl.utils.get_column_letter()`.
```py
>>> import openpyxl
>>> from openpyxl.utils import get_column_letter, column_index_from_string
>>> get_column_letter(1) # Translate column 1 to a letter.
'A'
>>> get_column_letter(27)
'AA'
>>> wb = openpyxl.load_workbook('example.xlsx')
>>> sheet = wb['Sheet1']
>>> get_column_letter(sheet.max_column)
'C'
>>> column_index_from_string('A') # Get A's number.
1
>>> column_index_from_string('AA')
27
```

##### Getting Rows and Columns from the Sheets

```py
>>> import openpyxl
>>> wb = openpyxl.load_workbook('example.xlsx')
>>> sheet = wb['Sheet1']
>>> tuple(sheet['A1':'C3']) # Get all cells from A1 to C3.
((<Cell 'Sheet1'.A1>, <Cell 'Sheet1'.B1>, <Cell 'Sheet1'.C1>), (<Cell
'Sheet1'.A2>, <Cell 'Sheet1'.B2>, <Cell 'Sheet1'.C2>), (<Cell 'Sheet1'.A3>,
<Cell 'Sheet1'.B3>, <Cell 'Sheet1'.C3>))
>>> for rowOfCellObjects in sheet['A1':'C3']:
		for cellObj in rowOfCellObjects:
			print(cellObj.coordinate, cellObj.value)
		print('--- END OF ROW ---')

A1 2015-04-05 13:34:02Working with Excel Spreadsheets   307
B1 Apples
C1 73
--- END OF ROW ---
A2 2015-04-05 03:41:23
B2 Cherries
C2 85
--- END OF ROW ---
A3 2015-04-06 12:46:51
B3 Pears
C3 14
--- END OF ROW ---
```

To access the values of cells in particular row or column:
```py
>>> import openpyxl
>>> wb = openpyxl.load_workbook('example.xlsx')
>>> sheet = wb.active
>>> list(sheet.columns)[1] # Get second column's cells.
(<Cell 'Sheet1'.B1>, <Cell 'Sheet1'.B2>, <Cell 'Sheet1'.B3>, <Cell 'Sheet1'.
B4>, <Cell 'Sheet1'.B5>, <Cell 'Sheet1'.B6>, <Cell 'Sheet1'.B7>)
>>> for cellObj in list(sheet.columns)[1]:
		print(cellObj.value)

Apples
Cherries
Pears
Oranges
Apples
Bananas
Strawberries
```


