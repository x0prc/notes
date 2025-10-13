---
dg-publish: true
---






## ==API Call Structure==

- Refer Windows API Documentation

```C
BOOL WriteProcessMemory(
	[in] HANDLE hProcess,
	[in] LPVOID lpBaseAddress,
	[in] LPCVOID lpBuffer,
	[in] SIZE_T nSize, 
	[out] SIZE_T *lpNumberOfBytesWritten
```

- WriteProcessMemory API Call code.

```C
BOOL Create(
        PCWSTR lpWindowName,
        DWORD dwStyle,
        DWORD dwExStyle = 0,
        int x = CW_USEDEFAULT,
        int y = CW_USEDEFAULT,
        int nWidth = CW_USEDEFAULT,
        int nHeight = CW_USEDEFAULT,
        HWND hWndParent = 0,
        HMENU hMenu = 0
        )
    {
        WNDCLASS wc = {0};

        wc.lpfnWndProc   = DERIVED_TYPE::WindowProc;
        wc.hInstance     = GetModuleHandle(NULL);
        wc.lpszClassName = ClassName();

        RegisterClass(&wc);

        m_hwnd = CreateWindowEx(
            dwExStyle, ClassName(), lpWindowName, dwStyle, x, y,
            nWidth, nHeight, hWndParent, hMenu, GetModuleHandle(NULL), this
            );

        return (m_hwnd ? TRUE : FALSE);
    }
```

- Basic New Window code displaying output THM.

```C
class Win32 {
  [DllImport("kernel32")]
  public static extern IntPtr GetComputerNameA(StringBuilder lpBuffer, ref uint lpnSize);
}

static void Main(string[] args) {
  bool success;
  StringBuilder name = new StringBuilder(260);
  uint size = 260;
  success = GetComputerNameA(name, ref size);
  Console.WriteLine(name.ToString());
}
```

- Example application that uses the API to get the computer name and other information of the device it is run on.

> [!important] Refer to
> 
> [malapi.io](http://malapi.io) for several vulnerable API calls.

## ==Keylogger & Shellcode==

- Written in C#, must obtain pointers for each call.

```C#
[DllImport("user32.dll", CharSet = CharSet.Auto, SetLastError = true)]
private static extern IntPtr SetWindowsHookEx(int idHook, LowLevelKeyboardProc lpfn, IntPtr hMod, uint dwThreadId);
[DllImport("user32.dll", CharSet = CharSet.Auto, SetLastError = true)]
[return: MarshalAs(UnmanagedType.Bool)]
private static extern bool UnhookWindowsHookEx(IntPtr hhk);
[DllImport("kernel32.dll", CharSet = CharSet.Auto, SetLastError = true)]
private static extern IntPtr GetModuleHandle(string lpModuleName);
private static int WHKEYBOARDLL = 13;
[DllImport("kernel32.dll", CharSet = CharSet.Auto, SetLastError = true)]
private static extern IntPtr GetCurrentProcess();
```