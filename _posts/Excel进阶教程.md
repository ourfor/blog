---
title: Excel进阶教程
date: 2017-09-10 16:01:10
category: "APP"  #
tags: [office]  #
---
同一文件下如何合并相同类型的表格，相信大家对这个问题困惑了很久，如何如何合并这些表格呢？合并之后是否会得到我们想要的表格呢？  
通常情况下我们如果要使用Excel来合并同一类型的表格，我们一般将每个表格文件打开剪切我们需要的单元格，并一一粘贴到目标表格中，你会发现其中有很多重复的步骤，特别是当表格文件数量相当多的时候，这工作量就很大了，既然重复相同的步骤是麻烦的根源，那么我们为何不把这项工作交给计算机做呢？其实微软公司出品的办公软件Excel中就有这个功能，不过要实现这个功能，我们就要用到“宏”这个东西，简单的说“宏”就是帮你完成重复的操作，如何打开，使用宏呢？  
<!-- more -->  
  

<img src="http://ozkg680jm.bkt.clouddn.com/%E5%AE%8F%E6%9F%A5%E7%9C%8B%E4%BB%A3%E7%A0%81.png" width="70%" height="30%" />

```bash 
Sub 合并当前目录下所有工作簿的全部工作表()  
Dim MyPath, MyName, AWbName  
Dim Wb As Workbook, WbN As String  
Dim G As Long
Dim Num As Long  
Dim BOX As String  
Application.ScreenUpdating = False
MyPath = ActiveWorkbook.Path
MyName = Dir(MyPath & "\" & "*.xls")
AWbName = ActiveWorkbook.Name
Num = 0
Do While MyName <> ""
If MyName <> AWbName Then
Set Wb = Workbooks.Open(MyPath & "\" & MyName)
Num = Num + 1
With Workbooks(1).ActiveSheet
.Cells(.Range("B65536").End(xlUp).Row + 2, 1) = Left(MyName, Len(MyName) - 4)
For G = 1 To Sheets.Count
Wb.Sheets(G).UsedRange.Copy .Cells(.Range("B65536").End(xlUp).Row + 1, 1)
Next
WbN = WbN & Chr(13) & Wb.Name
Wb.Close False
End With
End If
MyName = Dir
Loop
Range("B1").Select
Application.ScreenUpdating = True
MsgBox "共合并了" & Num & "个工作薄下的全部工作表。如下：" & Chr(13) & WbN, vbInformation, "提示"
End Sub 
``` 

首先复制代码，然后在文件夹中新建一个表格文件，然后使用Excel打开!  
<img src="http://ozkg680jm.bkt.clouddn.com/%E7%B2%98%E8%B4%B4%E4%BB%A3%E7%A0%81.png" width="70%" height="30%" />  
关闭窗口，点击运行>宏   

<img src="http://ozkg680jm.bkt.clouddn.com/%E8%BF%90%E8%A1%8C.png" width="70%" height="30%" />  
一会儿就合并好了，但是这个表格并不符合我们的要求，这时善用排序功能，就行了。  
<img src="http://ozkg680jm.bkt.clouddn.com/%E5%88%9D%E9%9F%B3%E6%9C%AA%E6%9D%A5.jpg" width="70%" height="30%" />      
