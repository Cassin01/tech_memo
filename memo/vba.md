```yaml
title: VBA
date: 2023-09-03
categories: [programming]
tags: [VBA, LibreOffice]
```

# Excel



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
