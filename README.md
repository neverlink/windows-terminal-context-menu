# WindowsTerminal-Context-Menu
Adding a context menu option to open the current directory in Windows Terminal.

### Removing the default "Open in Windows Terminal"
By default, such an option exists, but only on the left pane in Explorer.

Get rid of it with the following registry entry. [Source](https://github.com/microsoft/terminal/issues/8105#issuecomment-726789079)

```
Windows Registry Editor Version 5.00

[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Shell Extensions\Blocked]
"{9F156763-7844-4DC4-B2B1-901F640F5155}"="Windows Terminal"
```

### Adding the new entries

Edit the path to Windows Terminal where necessary
You can also set Position to either Top or Bottom.
```
Windows Registry Editor Version 5.00

[HKEY_CLASSES_ROOT\Directory\shell\WindowsTerminalMenu]
"Icon"="C:\\Program Files\\WindowsApps\\REPLACE_THIS\\wt.exe"
@="Windows Terminal"
"Position"=""

[HKEY_CLASSES_ROOT\Directory\shell\WindowsTerminalMenu\command]
@="C:\\Program Files\\WindowsApps\\REPLACE_THIS\\wt.exe -d %V"


[HKEY_CLASSES_ROOT\Directory\Background\shell\WindowsTerminalMenu]
"Icon"="C:\\Program Files\\WindowsApps\\REPLACE_THIS\\wt.exe"
@="Windows Terminal"
"Position"=""

[HKEY_CLASSES_ROOT\Directory\Background\shell\WindowsTerminalMenu\command]
@="C:\\Program Files\\WindowsApps\\REPLACE_THIS\\wt.exe -d %V"
```

boom
