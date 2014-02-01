---
layout: post
title: "SubSonic.Extensions.UpdateFileText"
---

# SubSonic.Extensions.UpdateFileText



<h2>Summary== Update text within a file by replacing a substring within the file.  ==Namespace</h2>

 
  

<h2>Example=="C:\\myfile.txt".UpdateFileText("find me","replace with");  ==Unit Test</h2>

 
public void UpdateFileText_Should_Replace_Existing_File_Text() {     //sorry for this test     "this is a stupid test".CreateToFile("C:\\testfile3.txt");      "C:\\testfile3.txt".UpdateFileText("stupid", "really stupid");          //it's the only way I can think of to do it     Assert.Equal("C:\\testfile3.txt".GetFileText(), "this is a really stupid test"); }  

<h2>Comments</h2>

 SubSonic 3.0 implements this as an extension on System.String - 2.x uses a static method on SubSonic.Sugar.Files.
