# deleteMicroUpdates
cmd commands

paste after line
===================================================================================================

@echo off
echo
 
echo Step 1: Delete Updates...
echo Delete KB3075249 (telemetry for Win7/8.1)
start /w wusa.exe /uninstall /kb:3075249
echo Delete KB3080149 (telemetry for Win7/8.1)
start /w wusa.exe /uninstall /kb:3080149
echo Delete KB3021917 (telemetry for Win7)
start /w wusa.exe /uninstall /kb:3021917
echo Delete KB3022345 (telemetry)
start /w wusa.exe /uninstall /kb:3022345
echo Delete KB3068708 (telemetry)
start /w wusa.exe /uninstall /kb:3068708
echo Delete KB3044374 (Get Windows 10 for Win8.1)
start /w wusa.exe /uninstall /kb:3044374
echo Delete KB3035583 (Get Windows 10 for Win7sp1/8.1)
start /w wusa.exe /uninstall /kb:3035583
echo Delete KB2990214 (Get Windows 10 for Win7 without sp1)
start /w wusa.exe /uninstall /kb:2990214
echo Delete KB2990214 (Get Windows 10 for Win7)
start /w wusa.exe /uninstall /kb:2990214
echo Delete KB2952664 (Get Windows 10 assistant)
start /w wusa.exe /uninstall /kb:2952664
echo Delete KB3075853 (update for "Windows Update" on Win8.1/Server 2012R2)
start /w wusa.exe /uninstall /kb:3075853
echo Delete KB3065987 (update for "Windows Update" on Win7/Server 2008R2)
start /w wusa.exe /uninstall /kb:3065987
echo Delete KB3050265 (update for "Windows Update" on Win7)
start /w wusa.exe /uninstall /kb:3050265
echo Delete KB971033  (license validation)
start /w wusa.exe /uninstall /kb:971033
echo Delete KB2902907 (description not available)
start /w wusa.exe /uninstall /kb:2902907
echo Delete KB2976987 (description not available)
start /w wusa.exe /uninstall /kb:2976987
 
echo Step 2: Blocking Routes...
route -p add 23.218.212.69 MASK 255.255.255.255 0.0.0.0
route -p add 65.55.108.23 MASK 255.255.255.255 0.0.0.0
route -p add 65.39.117.230 MASK 255.255.255.255 0.0.0.0
route -p add 134.170.30.202 MASK 255.255.255.255 0.0.0.0
route -p add 137.116.81.24 MASK 255.255.255.255 0.0.0.0
route -p add 204.79.197.200 MASK 255.255.255.255 0.0.0.0
route -p add 23.218.212.69 MASK 255.255.255.255 0.0.0.0
 
echo Step 3: Disabling tasks...
schtasks /Change /TN "\Microsoft\Windows\Application Experience\AitAgent" /DISABLE
schtasks /Change /TN "\Microsoft\Windows\Application Experience\Microsoft Compatibility Appraiser" /DISABLE
schtasks /Change /TN "\Microsoft\Windows\Application Experience\ProgramDataUpdater" /DISABLE
schtasks /Change /TN "\Microsoft\Windows\Autochk\Proxy" /DISABLE
schtasks /Change /TN "Microsoft\Windows\Customer Experience Improvement Program\Consolidator" /DISABLE
schtasks /Change /TN "Microsoft\Windows\Customer Experience Improvement Program\KernelCeipTask" /DISABLE
schtasks /Change /TN "Microsoft\Windows\Customer Experience Improvement Program\UsbCeip" /DISABLE
schtasks /Change /TN "\Microsoft\Windows\DiskDiagnostic\Microsoft-Windows-DiskDiagnosticDataCollector" /DISABLE
schtasks /Change /TN "\Microsoft\Windows\Maintenance\WinSAT" /DISABLE
schtasks /Change /TN "\Microsoft\Windows\Media Center\ActivateWindowsSearch" /DISABLE
schtasks /Change /TN "\Microsoft\Windows\Media Center\ConfigureInternetTimeService" /DISABLE
schtasks /Change /TN "\Microsoft\Windows\Media Center\DispatchRecoveryTasks" /DISABLE
schtasks /Change /TN "\Microsoft\Windows\Media Center\ehDRMInit" /DISABLE
schtasks /Change /TN "\Microsoft\Windows\Media Center\InstallPlayReady" /DISABLE
schtasks /Change /TN "\Microsoft\Windows\Media Center\mcupdate" /DISABLE
schtasks /Change /TN "\Microsoft\Windows\Media Center\MediaCenterRecoveryTask" /DISABLE
schtasks /Change /TN "\Microsoft\Windows\Media Center\ObjectStoreRecoveryTask" /DISABLE
schtasks /Change /TN "\Microsoft\Windows\Media Center\OCURActivate" /DISABLE
schtasks /Change /TN "\Microsoft\Windows\Media Center\OCURDiscovery" /DISABLE
schtasks /Change /TN "\Microsoft\Windows\Media Center\PBDADiscovery" /DISABLE
schtasks /Change /TN "\Microsoft\Windows\Media Center\PBDADiscoveryW1" /DISABLE
schtasks /Change /TN "\Microsoft\Windows\Media Center\PBDADiscoveryW2" /DISABLE
schtasks /Change /TN "\Microsoft\Windows\Media Center\PvrRecoveryTask" /DISABLE
schtasks /Change /TN "\Microsoft\Windows\Media Center\PvrScheduleTask" /DISABLE
schtasks /Change /TN "\Microsoft\Windows\Media Center\RegisterSearch" /DISABLE
schtasks /Change /TN "\Microsoft\Windows\Media Center\ReindexSearchRoot" /DISABLE
schtasks /Change /TN "\Microsoft\Windows\Media Center\SqlLiteRecoveryTask" /DISABLE
schtasks /Change /TN "\Microsoft\Windows\Media Center\UpdateRecordPath" /DISABLE
 
echo Step 4: Killing Diagtrack-service (if it still exists)...
sc stop Diagtrack
sc delete Diagtrack
 
echo Final Step: Stop remoteregistry-service (if it still exists)...
sc config remoteregistry start= disabled
sc stop remoteregistry
 
echo All done, go to reboot!
pause
