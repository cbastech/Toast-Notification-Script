# Toast Notification Script  
  
## Current version: 2.4.6  
  
Toast Notification Script version 2.3.0 by [Martin Bengtsson](https://www.imab.dk).  
Version 2.4.0 through 2.4.6 modifications done by [Eric Scholl](https://github.com/cbastech/)  
  
Blog posts, documentation as well as if any questions, please use: https://www.imab.dk/windows-10-toast-notification-script/  
  
## What's New  
  
### 2.4.0
         
* Reworked RestartDevice command to install pending updates prior to restart.  https://github.com/imabdk/Toast-Notification-Script/issues/30  
* Reworked PendingReboot registry keys to work with Windows 10 20H2 and later.  https://github.com/imabdk/Toast-Notification-Script/issues/43   
* Reworked Toast object to add ExpiresOnReboot = $true.  https://github.com/imabdk/Toast-Notification-Script/issues/28
* Added check to avoid displaying notifications for apps that are already installed. https://github.com/imabdk/Toast-Notification-Script/issues/13  
* Added parameter switch for ID [Application, SoftwareUpdate, or PackageID]  
* Added parameter switch for Title [SoftwareUpdate Title]  
* Added ToastRebootAfterhours protocol to schedule reboots afterhours  
* Added check to suppress notification on disconnected user sessions (people technically 'logged in' but State = Disc in 'query user')  
* Modified XML to support Afterhours reboot deadline  
* Modified ActionButton2Enabled to NOT enable Dismiss button and override config settings; XML doesn't mention this.  
* Added verbiage differences for $BodyText1 depending on whether $DeadlineContent exists (required vs. available deployments)  
* Modified ADPasswordExpiration to display days pending  
* Added 'Windows Update' Feature to handle monthly cumulative updates 

### 2.4.1
* Modified ADPasswordExpiration to show 'today', 'day', and 'days' for 0, 1, and 2+ days remaining  
* Changed method to check for disconnected user sessions due to inaccurate results. Now uses logonui (lockscreen) detection  
* Added 'TestDev' mode that logs to Test-ToastNotification.log if enabled.  
* Added check for deployment deadlines in the past; if detected, no deadline is displayed (avoids user confusion)
  
### 2.4.2
* Found and corrected two bugs in afterhours reboot which 1) didn't overwrite old scheduled tasks and 2) failed to correctly detect if a future reboot was already scheduled and displayed the reboot notification anyways.  
* Changed exit codes to work better with SCCM (using [System.Environment::Exit() instead of 'Exit') and implemented more granular exit codes to assist in troubleshooting:
  
            0 - Success (working as intended, including exit due to purposeful safeguards)  
            1 - Error in actual running of script (undefined error)  
            3 - Error in setup of script (setting necessary registry keys, making directories, etc.)  
            4 - Error in XML file (cannot be located, read, or parsed)  
            5 - Error in commandline or XML parameters (missing data or conflicting data)  
         
### 2.4.3
* New method of detecting active user sessions to try to compensate for RDS and RDP sessions.  
### 2.4.4
* Force a reboot for that night if the user has exceeded $ForceRebootAfterMaxUptimeDays.  This uses shutdown.exe so that it will clear itself if the user restarts beforehand.  
### 2.4.5
* Added ability to restrict reboots only to specified days of the week  
### 2.4.6
* Reverted https://github.com/imabdk/Toast-Notification-Script/issues/30 - USOClient is not working on Windows 11 23H2  
