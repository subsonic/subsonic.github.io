---
layout: post
title: "SubSonic.Extensions.WriteToFile"
---

# SubSonic.Extensions.WriteToFile



<h2>Summary== Writes out a string to a file, pretty much the same as CreateToFile  ==Namespace</h2>

 
  

<h2>Example=="Lorem Ipsem My Test to Save".WriteToFile(@"C:\MyFile.txt");  ==Unit Test</h2>

 
[Fact] public void WriteToFile_Should_SaveText_To_File() {     //sorry for this test     "this is a stupid test".CreateToFile("C:\\testfile4.txt");     //it's the only way I can think of to do it     Assert.Equal("C:\\testfile4.txt".GetFileText(), "this is a stupid test"); }  

<h2>Comments</h2>

 SubSonic 3.0 implements this as an extension on System.String - 2.x uses a static method on SubSonic.Sugar.Files.
