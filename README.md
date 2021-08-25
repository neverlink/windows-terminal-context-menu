## Context menu entry for Windows Terminal

### 1. Removing the default "Open in Windows Terminal"
By default, such an option exists only in the left Explorer pane.

Get rid of it with the following registry key via cmd:

```
REG ADD "HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Shell Extensions\Blocked" /v "{9F156763-7844-4DC4-B2B1-901F640F5155}" /d "WindowsTerminal"
```

### 2. Adding the new keys

Replace the path to Windows Terminal with your own.

Most easily found via Task Manager, but you could simply replace the version number with your own. 

**Note!** Path must point to `wt.exe`, not `WindowsTerminal.exe` Also, WindowsTerminal and WindowsTerminalPreview differ by folder name.

You can also set `Position` value to either `Top` or `Bottom`, blank by default.
```
SET "TerminalPath=C:\Program Files\WindowsApps\Microsoft.WindowsTerminal_1.9.1942.0_x64__8wekyb3d8bbwe\wt.exe"

SET "Key=HKCR\Directory\shell\WindowsTerminal"
REG ADD "%Key%" /f /ve /d "Windows Terminal"
REG ADD "%Key%" /f /v "Position" /d ""
REG ADD "%Key%" /f /v "Icon" /d "%TerminalPath%"
REG ADD "%Key%\command" /f /ve /d "%TerminalPath%"

SET "Key=HKCR\Directory\Background\shell\WindowsTerminal"
REG ADD "%Key%" /f /ve /d "Windows Terminal"
REG ADD "%Key%" /f /v "Position" /d ""
REG ADD "%Key%" /f /v "Icon" /d "%TerminalPath%"
REG ADD "%Key%\command" /f /ve /d "%TerminalPath%"
```
### 3. Starting Directory
Add the following line to your `defaults` in `preferences.json` to always start Windows Terminal in the working directory.

`"startingDirectory": "."`
### 4. Removal
```
REG DELETE HKEY_CLASSES_ROOT\Directory\shell\WindowsTerminal /f
REG DELETE HKEY_CLASSES_ROOT\Directory\Background\shell\WindowsTerminal /f
```
