---
layout: post
title: "Automating SubSonic's Magic"
---

# Automating SubSonic's Magic

Let's face it - it sucks to write XML and do any kind of configuration ... period. This is why we lean on Conventions, and if we all follow conventions, we can build on that to make some more magic happen. Magical Automation is fun.  

<h2>Using the Build Provider</h2>

 This will only work with Web Sites - it WILL NOT WORK with Web Applications or MVC. 
.  Install SubSonic as described in 
 and make sure to add a reference to the SubSonic DLL. Once that's completed, edit your Web.config to add the following line:<compilation debug="true" defaultLanguage="C#">                     <buildProviders>         <add extension=".abp" type="SubSonic.BuildProvider, SubSonic"/>       </buildproviders>  Next, create a file with the extension "abp" - you can put whatever you like in the file; it's not read and it doesn't matter. The only thing that matters is the file extension.  Add this file to the App_Code directory. BAM. You now have a Data Access Layer.
