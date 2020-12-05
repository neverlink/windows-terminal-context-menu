## Context menu options to launch Windows Terminal in a directory.

### 1. Removing the default "Open in Windows Terminal"
By default, such an option exists, but only in the left pane of Explorer.

Get rid of it with the following registry key. [Source](https://github.com/microsoft/terminal/issues/8105#issuecomment-726789079)

```
Windows Registry Editor Version 5.00

[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Shell Extensions\Blocked]
"{9F156763-7844-4DC4-B2B1-901F640F5155}"="Windows Terminal"
```

### 2. Adding the new keys

Replace the path to Windows Terminal with your own, as it differs between versions.

You can also set `Position` to either `Top` or `Bottom`.
```
Windows Registry Editor Version 5.00

; Left Pane
[HKEY_CLASSES_ROOT\Directory\shell\WindowsTerminalMenu]
"Icon"="C:\\Program Files\\WindowsApps\\Microsoft.WindowsTerminalPreview_1.5.3242.0_x64__8wekyb3d8bbwe\\wt.exe"
@="Windows Terminal"
"Position"=""

[HKEY_CLASSES_ROOT\Directory\shell\WindowsTerminalMenu\command]
@="C:\\Program Files\\WindowsApps\\Microsoft.WindowsTerminalPreview_1.5.3242.0_x64__8wekyb3d8bbwe\\wt.exe -d \"%V \""

; Right Pane
[HKEY_CLASSES_ROOT\Directory\Background\shell\WindowsTerminalMenu]
"Icon"="C:\\Program Files\\WindowsApps\\Microsoft.WindowsTerminalPreview_1.5.3242.0_x64__8wekyb3d8bbwe\\wt.exe"
@="Windows Terminal"
"Position"=""

[HKEY_CLASSES_ROOT\Directory\Background\shell\WindowsTerminalMenu\command]
@="C:\\Program Files\\WindowsApps\\Microsoft.WindowsTerminalPreview_1.5.3242.0_x64__8wekyb3d8bbwe\\wt.exe -d \"%V \""
```
### 3. Removal
```
reg delete HKEY_CLASSES_ROOT\Directory\shell\WindowsTerminalMenu /f &
reg delete HKEY_CLASSES_ROOT\Directory\Background\shell\WindowsTerminalMenu /f
```
