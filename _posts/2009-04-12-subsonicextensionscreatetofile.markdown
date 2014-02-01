---
layout: post
title: "SubSonic.Extensions.CreateToFile"
---

# SubSonic.Extensions.CreateToFile



<h2>Summary== Creates or opens a file for writing and writes text to it.  ==Namespace</h2>

 
  

<h2>Example=="Lorem Ipsem My Test to Save".CreateToFile(@"C:\MyFile.txt");  ==Unit Test</h2>

 
public void CreateToFile_Should_SaveText_To_File() {     //sorry for this test     "this is a stupid test".CreateToFile("C:\\testfile2.txt");     //it's the only way I can think of to do it     Assert.Equal("C:\\testfile2.txt".GetFileText(), "this is a stupid test"); }  

<h2>Comments</h2>

 SubSonic 3.0 implements this as an extension on System.String - 2.x uses a static method on SubSonic.Sugar.Files.
