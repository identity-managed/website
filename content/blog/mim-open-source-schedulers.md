---
title: 'MIM Open Source Schedulers'
date: 2018-12-17T22:25:00.000-07:00
draft: false
url: /2018/12/mim-open-source-schedulers.html
tags: 
- #SQL
- #FIM
- #MIM
---

Your MIM installation is in, the config is done, programming all set and now to automate the running of the Management Agents.  
  
Options? Most people use Windows Task Scheduler with a PowerShell script or VBScript -- which works but can get cumbersome to maintain. With my SQL Server background, I often use SQL Server Agent Jobs because it has much better follow up and executing database commands.  

*   Task Scheduler -- runs as a windows service

*   Can launch a job based on multiple triggers: 

*   scheduled
*   CPU idle  
*   an event in the event log
*   startup
*   user logon 

*   Step Types

*   Command line

*   What it lacks is follow up -- it doesn't write to the event log, it doesn't have email capability, it doesn't do a good job of storing the results.

*   SQL Agent -- also runs as a windows service

*   Schedule types:

*   Recurring -- recur every x hours, x min or x seconds

*   Daily
*   Weekly
*   Monthly

*   One time
*   SQL Agent Starts
*   CPU idle

*   Step Types

*   SQL
*   Command Line
*   PowerShell
*   SSIS

*   Follow up is pretty good -- 

*   Write to the event log
*   It automatically records the results of each step -- I find it much easier to troubleshoot a SQL Agent job as opposed to a Task Scheduler job.

*   You can control the level of detail recorded

*   Send an email on failure or success
*   Can even have a pager schedule
*   You can jump from one step to another on success or failure

A search of GitHub reveals a few Open Source options that provide features more specific to MIM.

  

**Open Source options:**

*   [Aseand's RunScript](https://github.com/aseand/RunScript) is a PowerShell script. How does that help? It has all kinds of pre-built functions that are commonly needed in your own PowerShell script -- so this isn't really a scheduler as you still need to use Task Scheduler, but not a bad place to start your own PowerShell script.

*   AnyInProgress Ma's
*   Clearrunhistory
*   MSSQLExecute
*   export-count
*   import-count
*   stage-count
*   start-agent -- runs an Agent asynchronously
*   Runagent -- runs an Agent and waits -- looks to have some great error handling
*   getRunHistory
*   getRunHistoryOld
*   WriteXmlToScreen -- for printing out the CSEntry data
*   SaveChangeCS -- get the pending CS changes
*   Aseand also created a [PowerShell script that does some pretty nice Sync engine documentation](https://github.com/aseand/MIM.syncservice.documentation.html) by querying the Sync engine database

*   Fellow MVP [Ryan Newington (lithnet)'s miis-autosync](https://github.com/lithnet/miis-autosync) \-- runs as a windows service 

*    Schedule

*   Recurring schedules 
*   events such as changes to AD, HR etc

*   The other key feature is it can be set up to only run if there is work to be done. It can also run as many profiles in parallel as possible. This is one of the best ways to cut a sync cycle as short as possible. 
*   Send emails when job fails
*   Clear Run History

*   [Wim Beck's FIM Scheduler](https://github.com/wim-beck/IS4U-FIM-Scheduler/wiki) -- uses XML config files, can run linear sequences and parallel sequences. It also runs as a Windows Service
*   Former MVP [Soren Granfeldt's MA Run Scheduler](https://github.com/sorengranfeldt/marunscheduler/wiki) -- was built as a replacement for the MASequencer from the MIIS Toolkit. 
*   [Traxion Solutions also has an MIIS Sequencer](http://www.traxionsolutions.com/miissequencer/Help/index.html?singlestep_text_result.htm) to replace the MA Sequencer

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices