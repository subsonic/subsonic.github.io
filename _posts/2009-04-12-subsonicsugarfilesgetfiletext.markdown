---
layout: post
title: "SubSonic.Sugar.Files.GetFileText"
---

# SubSonic.Sugar.Files.GetFileText



<h2>Summary== Loads the text from the specified file as a string  ==Example==string fileText=SubSonic.Sugar.Files.GetFileText(@"C:\MyFile.txt");  ==Unit Test</h2>

 
public void GetFileText_Should_Read_Text_From_Existing_File() {  //sorry for this test  string fileText = @"C:\testfile.txt".GetFileText();  //it's the only way I can think of to do it  Assert.Equal(fileText, "this is a stupid test"); }  

<h2>Comments</h2>

 SubSonic 3.0 implements this as an extension on System.String - 2.x uses a static method on SubSonic.Sugar.Files.
