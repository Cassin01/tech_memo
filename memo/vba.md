```yaml
title: VBA
date: 2023-09-03
categories: [programming]
tags: [VBA, LibreOffice]
```

# LibreOffice

## Using VBA on LibreOffice

Write "Option VBASupport 1" down to header.

```vbnet
Option VBASupport 1
REM  *****  BASIC  *****

Sub Main
 ' ...
End Sub
```

## Debug.Print

LibreOffice does not provide "Debug.Print".
You can use "ScriptForge" instead of "Debug.Print".


```vbnet
GlobalScope.BasicLibraries.loadLibrary("ScriptForge")
createscriptservice("Exception")
SF_Exception.consoleClear()
for x = 0 to 100
    SF_Exception.debugprint(x)
next x
SF_Exception.console()
```

## Open and Write File

```vbnet
GlobalScope.BasicLibraries.LoadLibrary("ScriptForge")
Dim FSO As Object
Set FSO = CreateScriptService("FileSystem")
FSO.FileNaming = "SYS"
Set f = FSO.OpenTextFile("~/tech-memo/memo/products/bench.md", FSO.ForWriting)
If Not IsNull(f) Then
    f.WriteLine("hoge")
    f.CloseFile()
End If
```

## Save as markdown table

```vbnet
Sub Main2()
	Dim ws As Worksheet
	Set ws = ThisWorkbook.worksheets("Sheet1")
	Call genmd(ws, 2, "J")
End Sub
Function genmd(ws As Worksheet, row As Integer, col As String)
	GlobalScope.BasicLibraries.LoadLibrary("ScriptForge")
	Dim FSO As Object
	Set FSO = CreateScriptService("FileSystem")
	FSO.FileNaming = "SYS"
	Set f = FSO.OpenTextFile("~/tech-memo/memo/products/bench.md", FSO.ForWriting)
	If Not IsNull(f) Then
		Dim head As String
		head = "|"
		sep = "|"
		For j = 1 To c2n(col)
			head = head & ws.Cells(row, j).Value & "|"
			sep = sep & "-|"
		Next
		f.WriteLine(head)
		f.WriteLine(sep)
		For i = row + 1 To EOL(ws, 3, 1)
			Dim cont As String
			cont = "|"
			For j = 1 To c2n("J")
				cont = cont & ws.Cells(i, j).Value & "|"
			Next
			f.WriteLine(cont)
		Next
		f.CloseFile()
	End If
End Function
```


