
  X64 位系统下的注入

# 编译说明

  只有x64模式，才能编译成功

# 使用说明

Usage: ./InjectProc.exe <type of injection> <path/to/exe or process_name> <path/to/dll>

Example:

		./InjectProc.exe dll_inj path/to/dll.dll notepad.exe
		
		./InjectProc.exe proc_rpl path/to/target/exe path/to/exe
		
		./InjectProc.exe hook path/to/target/exe path/to//dll
		
		./InjectProc.exe APC target/proc/name path/to/dll


# InjectProc

Process injection is a very popular method to hide malicious behavior of code and are heavily used by malware authors.

There are several techniques, which are commonly used:
DLL injection, process replacement (a.k.a process hollowing), hook injection and APC injection.

Most of them use same Windows API functions: 
OpenProcess, VirtualAllocEx, WriteProcessMemory, for detailed information about those functions, use MSDN.

## DLL injection:
* Open target process.
* Allocate space.
* Write code into the remote process.
* Execute the remote code.

## Process replacement:
* Create target process and suspend it.
* Unmap from memory.
* Allocate space.
* Write headers and sections into the remote process.
* Resume remote thread.

## Hook injection:
* Find/Create process.
* Set hook
## Note: 
`InjectProc` uses [SetWindowsHookEx](https://msdn.microsoft.com/en-us/library/windows/desktop/ms644990(v=vs.85).aspx) function, you can try different ways to installing hooks, for example, [EasyHook](http://easyhook.github.io/tutorials/nativeremotehook.html)

## APC injection:
* Open process.
* Allocate space.
* Write code into remote threads.
* "Execute" threads using QueueUserAPC.

## Download
[Windows x64 binary](https://github.com/secrary/InjectProc/releases) - x64 bit DEMO
## Dependencies: 
[vc_redist.x64](https://support.microsoft.com/en-us/help/2977003/the-latest-supported-visual-c-downloads) - Microsoft Visual C++ Redistributable
## DEMO
[InjectProc DEMO - Process Injection Techniques](https://www.youtube.com/watch?v=hLPDq9nSHMw)

## Contributors
- [nullbites](https://github.com/nullbites)

# Warning
Works on Windows 10 build 1703, 64bit.

I've not enough time to test other systems and make it portable if you have enough time please contribute.

I create this project for me to better understand how process injection works and 
I think it will be helpful for many beginner malware analysts too. 
