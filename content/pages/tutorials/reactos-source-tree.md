+++
title = "Understanding the ReactOS source tree"
slug = "reactos-source-tree"
+++

## ReactOS source tree structure

Poking through the [ReactOS repository source tree](https://github.com/reactos/reactos) it might intimidate you by the fact that ReactOS repository infrastructure is a behemoth in size with every directory serving own purpose. Fear not as in this tutorial I'll be explaining the structure of ReactOS source tree for an ease navigation through the repository.

### ReactOS source tree directories

**.github** -- Primary GitHub directory of the repository. It contains the workflow file configuration as well as the PR management and funding document.

**.theia** -- Gitpod configuration files directory

**base** -- Base directory that contains the build-in applications of ReactOS (e.g. Calculator), services, setup (USETUP module and other related setup components), parts of the Shell and system modules, for example LSASS (Local Security Authority Subsystem Service).

**boot** -- Contains ARM boot libraries, Boot Configuration Data (BCD), boot data files and FreeLoader source code.

**dll** -- Dynamic link libraries directory. Contains the NTDLL layer library, user mode DLLs, control panel applets (CPL) and much more.

**drivers** -- Kernel mode drivers. Ranging from base drivers to Windows Management Instrumentation (WMI) driver.

**hal** -- Contains the Hardware Abstraction Layer (HAL) modules. An example of these include HALs for Xbox (1st generation) x86 HAL, ACPI HAL and PowerPC (PPC) HAL.

**media** -- Documentations, fonts, themes, VGA fonts and other stuff reside here.

**modules** -- Contains ReactOS Test cases suite, ReactOS applications (not to be confused with the built-in applications in the **base** directory) and wallpapers.

**ntoskrnl** -- Home to NT kernel of ReactOS.

**sdk** -- Software development kit of ReactOS.

**subsystems** -- Contains subsystem environment like Windows 16-bit, Windows 32-bit subsystems and Multiple Virtual DOS Machines (MVDM).

**Win32SS** -- Kernel side of the Windows subsystem (Win32k). Provides windowing (USER) and graphics (GDI) manager and printing support.

## ReactOS NT kernel source tree

In this section I'll cover the structure tree of the NT kernel with explaining briefly each directory and their purpose. Further information regard the NT function prefixes and how to understand them when writing NT code (this both includes the kernel and what you develop in NTDLL or HAL) will be explained in a different tutorial.

### NT kernel source tree

**cache** -- Cache logging code directory.

**cc** -- Cache manager. It contains common caching code used for FSD (Filesystem drivers) and for I/O operations.

**config** -- Contains configuration management code such as hive system registry initialization.

**dbgk** -- Directory for for kernel debugger support internal routines.

**ex** -- This directory contains the "Executive" part of the kernel.

**fsrtl** -- Contains filesystem Run-Time library routines.

**fstub** -- Directory for stub routine entries for I/O and HAL.

**inbv** -- Contains initialization boot video code.

**include** -- Directory for internal NT kernel headers.

**io** -- Contains I/O management routines and structures.

**kd** -- Kernel debugger code.

**kd64** -- Kernel debugger code (64-bit).

**kdbg** -- Directory for kernel debugger command line support.

**ke** -- Contains the _microkernel_ of NT. It compromises the kernel entry routines and internal kernel functions (Ki) not used for export.

**lpc** -- Contains the local procedure call code.

**mm** -- The memory manager. This directory compromises memory manipulation routines as well as internal functions (Mi) not used for export.

**ntkrnlmp** -- Multiprocessor support for the NT kernel. For now this directory remains empty.

**ob** -- Object manager code for the kernel.

**po** -- Directory that contains power manager kernel code.

**ps** -- Contains process and thread management code.

**rtl** -- Directory that contains specific C Run-Time library code for NT.

**se** -- Security manager kernel code.

**vdm** -- Virtual DOS Machine (VDM) code.

**vf** -- Directory that contains driver verifier code.

**wmi** -- Windows management instrumentation support kernel code.