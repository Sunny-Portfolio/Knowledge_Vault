### Install openpyxl Module
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
```py
>>> import openpyxl
>>> wb = openpyxl.load_workbook('example.xlsx')
>>> sheet = wb['Sheet1'] # Get a sheet from the workbook.
>>> sheet['A1'] # Get a cell from the sheet.
<Cell 'Sheet1'.A1>
>>> sheet['A1'].value # Get the value from the cell.
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

