---
title: "Macros with Examples"
seoTitle: "VBA"
seoDescription: "Macros or VBA script"
datePublished: Wed May 03 2023 17:36:52 GMT+0000 (Coordinated Universal Time)
cuid: clh7zd88l00000amc1pxb70li
slug: macros-with-examples
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/2EJCSULRwC8/upload/2dc2ea46257081fa49aae2c6922e8861.jpeg
tags: macros, vba, excel

---

We already introduced what macros are in my article: [Macro, an Excel feature](https://hashnode.com/post/clh1owv2b000r09ji0s50ay9e). Click for a quick intro.

Now going even further, we will see a few practical real-life tasks which can be achieved with macros, and go into detail about how to actually achieve that.

## Hide rows/columns with zero value.

Let's say you have an Excel report which gives you monthly, weekly or daily reports of what tasks an employee did in their total 9-5 Job. Ideally, we only wish to see the values where the efforts are not zero, you can go ahead and manually hide those columns, but why do manual work again and again, when you can write a script and just forget about it, now let's assume the hours mentioned are in column K, you can utilize the following Macro VBA to achieve the same.

* Demo code snippet:
    
    `Sub HideRowsWithValueZero()`
    
    `Dim lastRow As Long`
    
    `Dim i As Long`
    
    `'Activate the sheet you want to work with`
    
    `Sheets("Sheet1").Activate`
    
    `'Get the last row of the sheet`
    
    `lastRow = ActiveSheet.Cells(Rows.Count, "K").End(xlUp).Row`
    
    `'Loop through each row in the range`
    
    `For i = 2 To lastRow`
    
    `If Cells(i, "K").Value = 0 Then`
    
    `'Hide the row if the value in column K is 0`
    
    `Rows(i).EntireRow.Hidden = True`
    
    `End If`
    
    `Next i`
    
    `End Sub`
    
* The first line `Sub HideRowsWithValueZero()` starts the macro and gives it a name.
    
* The next two lines `Dim lastRow As Long` and `Dim i As Long` declare variables for later use.
    
* The line `Sheets("Sheet1").Activate` activates the sheet that you want to work with. In this case, it's named "Sheet1," but you can replace that with the name of the sheet you want to hide rows in.
    
* The line `lastRow = ActiveSheet.Cells(Rows.Count, "K").End(xlUp).Row` finds the last row of data in the sheet by starting at the bottom and moving up until it reaches a non-empty cell in column K. The `Rows.Count` property returns the total number of rows in the sheet, so `ActiveSheet.Cells(Rows.Count, "K")` refers to the last cell in column K. The `xlUp` argument tells Excel to look up from that cell until it finds the last non-empty cell. Finally, the `Row` property returns the row number of that cell.
    
* The `For` the loop starts on the second row (`i = 2`) and goes up to the last row of data (`lastRow`).
    
* The `If` statement checks whether the value in column K for the current row is equal to zero. If it is, the code inside the `If` statement is executed.
    
* The line `Rows(i).EntireRow.Hidden = True` hides the entire row for the current iteration of the loop, since the value in column K is zero.
    
* Finally, the `Next i` statement ends the loop and the `End Sub` statement marks the end of the macro.
    
    ## Converting values of a column.
    
    For this, let's take the example of employee data again, for simplicity let's take a simple case of converting seconds to Hours.
    
    Suppose your data is getting recorded in seconds instead of hours. To process the data you need it to be in hours, you can find a formula to do it, but if you are going to automate tasks, you need to find a solution with scripts, Plus once you write a script, you can set a shortcut while creating it and reuse it every time needed.
    
    Let's take pointers we would need to do in order to achieve the above,
    
    Need to identify the column of data, select the row for pasting the data into (always better to paste data into a new column, that way we always have a backup to go back to), create the formula, and apply it to all rows of the new column.
    
* Demo code snippet:
    
    `Sub ConvertToHours()`
    
    `Dim lastRow As Long`
    
    `Dim i As Long`
    
    `Dim cellValue As Variant`
    
    `Dim lastColumn As Long`
    
    `' Activate sheet "Sheet1"`
    
    `Sheets("Sheet1").Activate`
    
    `' Get the last row in column A`
    
    `lastRow = ActiveSheet.Cells(Rows.Count, "A").End(xlUp).Row`
    
    `' Get the index of the last column`
    
    `lastColumn = ActiveSheet.Cells(1, Columns.Count).End(xlToLeft).Column`
    
    `' Write to cell in the new column`
    
    `ActiveSheet.Cells(1, lastColumn + 1).Value = "Converted Hours"`
    
    `' Loop through each cell in column A and convert the value to hours`
    
    `For i = 1 To lastRow`
    
    `cellValue = ActiveSheet.Cells(i, "A").Value`
    
    `If IsNumeric(cellValue) Then`
    
    `ActiveSheet.Cells(i, lastColumn + 1).Value = Round(cellValue / 3600, 2)`
    
    `Else`
    
    `ActiveSheet.Cells(i, lastColumn + 1).Value = "Invalid value"`
    
    `End If`
    
    `Next i`
    
    `' Auto-fit the width of the new column`
    
    `ActiveSheet.Columns(lastColumn + 1).AutoFit`
    
    `End Sub`
    
* `Dim lastRow As Long, Dim lastColumn As Long` and `Dim i As Long` declare variables for later use.
    
* `Dim cellValue As Variant`: Declare a variable to hold the value of each cell in column A during the loop.
    
* `Sheets("Sheet1").Activate`: Activate the "Sheet1" worksheet.
    
* `lastRow = ActiveSheet.Cells(Rows.Count, "A").End(xlUp).Row`: Determine the last row of data in column A by finding the last cell that has a value and moving up to the first non-blank cell in the column.
    
* `lastColumn = ActiveSheet.Cells(1, Columns.Count).End(xlToLeft).Column`: Determine the last column in the worksheet by finding the first cell in the first row that has a value and moving left to the last non-blank cell in the row.
    
* `ActiveSheet.Cells(1, lastColumn + 1).Value = "Converted Hours"`: Write the label "Converted Hours" to the first cell in the new column, which is the column immediately to the right of the last column of data.
    
* `For i = 1 To lastRow`: Loop through each row in column A.
    
* `cellValue = ActiveSheet.Cells(i, "A").Value`: Get the value of the cell in column A for the current row.
    
* `If IsNumeric(cellValue) Then`: Check if the cell value is numeric.
    
* `ActiveSheet.Cells(i, lastColumn + 1).Value = Round(cellValue / 3600, 2)`: If the cell value is numeric, divide it by 3600 to convert it to hours and write the result to the corresponding cell in the new column. Round the result to 2 decimal places.
    
* `Else`: If the cell value is not numeric, write the text "Invalid value" to the corresponding cell in the new column.
    
* `Next i`: Move on to the next row in column A.
    
* `ActiveSheet.Columns(lastColumn + 1).AutoFit`: Auto-fit the width of the new column to accommodate the converted values.
    
    ## Getting all distinct values of a column.
    
    Taking forward our previous example, suppose now you have to identify unique tasks or group the tasks we will understand by the below code.
    
* Demo code snippet:
    
    `Sub ExtractDistinctGroups()`
    
    `Dim primarySheet As Worksheet`
    
    `Dim secondarySheet As Worksheet`
    
    `Dim lastRow As Long`
    
    `Dim i As Long`
    
    `Dim cellValue As Variant`
    
    `Dim uniqueGroups As Variant`
    
    `Dim dict As Object`
    
    `' Attempt to set the primary sheet`
    
    `On Error Resume Next`
    
    `Set primarySheet = Worksheets("Primary")`
    
    `On Error GoTo 0`
    
    `If primarySheet Is Nothing Then`
    
    `MsgBox "Unable to find sheet named 'Primary'."`
    
    `End If`
    
    `' Set the secondary sheet`
    
    `Set secondarySheet = Worksheets("Secondary")`
    
    `' Get the last row in column "Group" of the primary sheet`
    
    `lastRow = primarySheet.Cells(primarySheet.Rows.Count, "A").End(xlUp).Row`
    
    `' Create a dictionary to store the unique group names`
    
    `Set dict = CreateObject("Scripting.Dictionary")`
    
    `' Loop through each cell and add the unique group names to the dictionary`
    
    `For i = 1 To lastRow`
    
    `cellValue = primarySheet.Cells(i, "A").Value`
    
    `If Not IsError(cellValue) And Not IsEmpty(cellValue) And Not dict.exists(cellValue) Then`
    
    `dict.Add cellValue, True`
    
    `End If`
    
    `Next i`
    
    `' Convert the dictionary keys to a variant array`
    
    `uniqueGroups = dict.keys`
    
    `' Write the unique group names to column A of the secondary sheet`
    
    `secondarySheet.Cells(1, "A").Resize(UBound(uniqueGroups) + 1, 1).Value = Application.Transpose(uniqueGroups)`
    
    `End Sub`
    
* This VBA macro extracts the unique values in column A of a worksheet named "Primary" and writes them to column A of a worksheet named "Secondary". The macro works as follows:
    
* Declare variables for the primary worksheet, secondary worksheet, the last row of the primary worksheet, an index variable, a cell value variable, a dictionary object, and an array to store the unique group names.
    
* Attempt to set the primary worksheet using On Error Resume Next and On Error GoTo 0 statements. If the sheet "Primary" is not found, the macro displays a message box and exits.
    
* Set the secondary worksheet to the worksheet named "Secondary".
    
* Get the last row of column A in the primary worksheet.
    
* Create a new dictionary object to store the unique group names.
    
* Loop through each cell in column A of the primary worksheet from row 1 to the last row. For each cell, check if its value is not an error, not empty, and not already in the dictionary. If the value satisfies these conditions, add it to the dictionary.
    
* Convert the dictionary keys to a variant array to extract the unique group names.
    
* Write the unique group names to column A of the second sheet, starting from cell A1 and extending to the number of unique groups plus one row.
    
* Overall, this macro allows users to extract the unique values in column A of one sheet and write them to another sheet, which can be useful for data analysis and management purposes.
    
    ### **The above ones are only a few examples. I have tried to keep it as detailed as possible. The possibilities are endless for what you can do with it, play with it.**
    
* Thanks for coming this far in the article. I hope I was able to explain the concept well enough. If you face any issues, please feel free to reach out to me; I'd be happy to help.
    
    ## 🔗 Let’s stay connected!
    
    [🌐 Linktree](https://linktr.ee/shishirsrivastav)| [🐦 X](https://x.com/shishir_who)| [📸 Instagram](https://www.instagram.com/programmatic.ly)| [▶️ YouTube](https://www.youtube.com/channel/UCCZiCzPtg9pmDwChJ4ROIpA) [✍️ Hashnode](https://hashnode.com/@ShishirSrivastav)| [💻 GitHub](https://github.com/Shishir420-GIT)| [🔗 LinkedIn](https://www.linkedin.com/in/shishir-srivastav)| [🤝 Topmate](https://topmate.io/shishir_srivastav) [🏅 Credly](https://www.credly.com/users/shishir-srivastav-who)
    
    © 2025 Shishir Srivastav. All rights reserved.