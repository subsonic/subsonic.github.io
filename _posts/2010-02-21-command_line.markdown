---
layout: post
title: "Command line"
---

# Command line



<h2>Summary== This is a walkthrough of how to setup Visual Studio to call our command-line tool, sonic.exe. This tool is designed to help you along in your day and hopefully do the heavy-lifting for you. Please note that with SubSonic 3.0, we're using T4 templates to do most of the code generation stuff here.  ==Configuration== SubCommander will always try and find a configuration file in its executing directory (Web.Config or App.Config). If it does, it will look for config information for itself there, and set itself up accordingly. You can override this by using the /config switch, and then telling it where it can find the config file:      sonic.exe generate /config "c:\myproject\App.config"   If you're working with a project and you want to use our generated code, just add an App.config file to the project, then you can run SubCommander in that directory.  ==Manual Configuration==  All of the config options can be passed in as switches ("/includeTableList table1, table2, table4" e.g.) to SubCommander. This is handy for when you want to use a BAT file.  ==Scripting Schema and Data==  You can script out your schema and data (and then version it in your favorite source control system) using SubCommander. Simply use the command "version" and tell SubCommander where to put the data:    sonic.exe version /out Scripts This will output a script file (.sql) to the local scripts directory of your project  ==Command Reference==  Here are the commands you can use currently with SubCommander:  *version:  Scripts out the schema/data of your db to file *scriptdata:  Scripts the data to file for your database *scriptschema:  Scripts your Database schema to file *generate:  Generates output code for tables, views, and SPs *generatetables: Generates output code for your tables *generateODS: Generates and ObjectDataSource controller for each table *generateviews:  Generates output code for your views *generatesps: Generates output code for your SPs  ==Screencast</h2>

 <ag>SubCommander.flv</ag>
