# Tuning Windows 10 Privacy Settings

[![view - Documentation](https://img.shields.io/badge/view-Documentation-blue?style=for-the-badge)](/docs/ "Go to project documentation")

Settings to apply to your Windows 10 instance to limit Microsoft privacy intrusion. 

## Before/During Installation

- Do **not** use *Express Settings*. Hit *Customize*, and make sure everything is turned off.
-	It's strongly preferred that you use a **local account** with Windows 10.


## After Installation

-	Head to *Settings > Privacy*, and disable **everything**, unless there are some things you really need.
-	While within the Privacy page, go to *Feedback*, select *Never* in the first box, and *Basic* in the second box.
-	Head to *Settings > Update and Security > Advanced Options > Choose how updates are delivered*, and turn the first switch off.
-	Disable Cortana by clicking the *Search* bar/icon.
-	(Optional) Disable web search in Search by going to Settings, and turning off *Search online and include web results*.
- Change the name of your PC by going to Start (or hitting the Windows key), typing *About PC*, and clicking *Rename PC*.

## Configuration

### Deleting some services

Open up the Command Prompt by launching cmd as an administrator, and enter the following:
```
  sc delete DiagTrack
  sc delete dmwappushservice
  echo "" > C:\ProgramData\Microsoft\Diagnosis\ETLLogs\AutoLogger\AutoLogger-Diagtrack-Listener.etl
```

### Policies
-	Open up the *Group Policy Editor* by launching `gpedit.msc` as an administrator. Go through *Computer Configuration > Administrative Templates > Windows Components > Data Collection and Preview Builds*. Double click *Telemetry*, hit *Disabled*, then apply. *NOTE: This only truly works in the Enterprise edition, but the final step provides a decent enough workaround for Pro users.*
-	While still in the *Group Policy Editor*, go through *Computer Configuration > Administrative Templates > Windows Components > OneDrive*, double click *Prevent the usage of OneDrive for file storage*, hit *Enabled*, then apply.
- While still in the *Group Policy Editor*, go through *Computer Configuration > Administrative Templates > Windows Components > Windows Defender*, double click *Turn Off Windows Defender*, hit *Enabled*, then apply.
-	Open up the *Registry Editor* by launching `regedit` as an administrator. Go through HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection, select *AllowTelemetry*, change its value to 0, then apply.
-	First, download the [Take Ownership tweak](http://www.howtogeek.com/howto/windows-vista/add-take-ownership-to-explorer-right-click-menu-in-vista/) and enable it. Then, head to the Hosts File by going through C:\Windows\System32\Drivers\Etc, take ownership of the hosts file, and add [all of the IPs from this page](http://paste2.org/A1sv86VF) into the file.

### Delete packages Xbox
```
  Get-AppxPackage -name *Xbox* | Remove-AppxPackage  
```
### Scheduled Tasks

Right click Start Menu > Computer Management :
- Expand 'Task Scheduler'
- Expand 'Task Scheduler Library'
- Expand 'Microsoft'
- Expand 'Windows'
- Click on 'Application Experience'
- Disable all Tasks in Folder
- Click on 'Customer Experience Improvement Program'
- Disable **all** Tasks in Folder

### Disable Cortana
1.	Press Win + R keyboard accelerator to open Run dialog box.
2.	Type *GPedit.msc* and hit *Enter* or OK to open *Local Group Policy Editor*. Navigate to *Local Computer Policy -> Computer Configuration -> Administrative Templates -> Windows Components -> Search*.
3.	In the right pane, double click on policy named *Allow Cortana*.
4.	Select the *Disabled* radio button.
5.	Restart the PC and Cortana and Bing Search will be disabled.
