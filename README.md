# Ghidra typeinfo archives

## How to generate winddk_7_32.gdt

`in.h` contents:

```cpp
#include <ntddk.h>
#include <wdm.h>
#include <ntifs.h>
#include <ndis.h>
#include <wmilib.h>
```

Using WDK 7600.16385.0:

```batch
cl.exe -I C:\WinDDK\7600.16385.0\inc\ddk -I C:\WinDDK\7600.16385.0\inc\api -I C:\WinDDK\7600.16385.0\inc\crt -D_X86_ -D_M_IX86 -D_WIN32 -D_WIN32_WINNT=0
x601 -DWINVER=0x0601 -DNTDDI_VERSION=0x06010000 -E in.h > winddk.h
```

## How to generate winddk_7_64.gdt

`in.h` contents:

```cpp
#include <ntddk.h>
#include <wdm.h>
#include <ntifs.h>
#include <ndis.h>
#include <wmilib.h>
```

Using WDK 7600.16385.0:

```batch
cl.exe -I C:\WinDDK\7600.16385.0\inc\ddk -I C:\WinDDK\7600.16385.0\inc\api -I C:\WinDDK\7600.16385.0\inc\crt -D_AMD64_ -D_M_AMD64 -D_WIN32 -D_WIN64 -D_WIN32_WINNT=0
x601 -DWINVER=0x0601 -DNTDDI_VERSION=0x06010000 -E in.h > winddk.h
```

## How to generate winddk_xp_32.gdt

`in.h` contents:

```cpp
#include <ntddk.h>
#include <wdm.h>
#include <ntifs.h>
#include <ndis.h>
#include <wmilib.h>
```

Using WDK 7600.16385.0:

```batch
cl.exe -I C:\WinDDK\7600.16385.0\inc\ddk -I C:\WinDDK\7600.16385.0\inc\api -I C:\WinDDK\7600.16385.0\inc\crt -D_X86_ -D_M_IX86 -D_WIN32 -D_WIN32_WINNT=0
x501 -DWINVER=0x0501 -DNTDDI_VERSION=0x05010000 -E in.h > winddk.h
```

Some manual modifications are required to get Ghidra's
C parser to play nice, but they're mostly straightforward:

- Ensure `-D__unaligned=""` is defined in Ghidra
- Move the full `POOL_TYPE` enum definition so that it is before its first usage
- Remove any `__forceinline` functions that Ghidra complains about
  
