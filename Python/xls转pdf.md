



```python
o = win32com.client.Dispatch("Excel.Application")
o.Visible = False
o.DisplayAlerts = False
wb = o.Workbooks.Open("test.xlsx")))
wb.WorkSheets("sheet1").Select()
wb.ActiveSheet.ExportAsFixedFormat(0, "test.pdf")
o.Quit()
```

