+++
title = "Introduction to the NT kernel development (Part 2)"
slug = "nt-internals-part-2"
aliases = [
    "/pages/nt-internals-part2/"
]
+++

In this chapter we'll cover some further topics about the NT kernel, namely the system calls interface in NT, the basic data types used, function conventions and syntax topology of the prefix routines and the startup and shutdown mechanism procedure of the kernel.

## Topology of the routine prefixes in the NT kernel

The more you explore around the kernel you may find a plethora of functions across different components of the kernel that adhere to a set of rules regarding function prefixing. Consider this as an example:

[![Function](../images/nt-internals/part2/func.png)](../images/nt-internals/part2/func.png)

It can be quite alien at first as you may were probably getting used to POSIX call interface syntax like `write()` or `read()`, but in reality it makes things easier to understand. Concerning the kernel's layered nature, Microsoft had to organise a set of syntax conventions for the kernel to meet the design principles of the kernel, which such syntax rules regarding function prefixes got adopted in ReactOS as our aim is to have a compatible and interoperable operating system both at API and ABI levels. This syntax interface that both Windows and ReactOS follow can be explained in this screenshot.

[![Syntax](../images/nt-internals/part2/syntax.png)](../images/nt-internals/part2/syntax.png)

In case it's still confusing to you, I'll further explain detail by detail each case that are seen in the screenshot.  
  
**function\_attribute** -- Not every function in the kernel comes with it, but some do. The function attribute is a compiler specific that instructs the compiler that the function behaves in a certain pattern or way. **DECLSPEC\_NORETURN** in this example means that the function never returns and thus the code calling the said function is unreachable, that is, it has no end. Some examples of attributes can be found in [this header](https://git.reactos.org/?p=reactos.git;a=blob;f=sdk/include/xdk/ntbasedef.h;hb=249f2388bd7ce086578119b50c988ba752169fc1#l164) within ReactOS source code.  
  
**function\_data\_type** -- This is the obvious one, as each function must have a data type that represents the function itself. The NT API (and consequently the Windows API as well) come with a collection of data types.  
  
**function\_call\_convention** -- Similar to the function attribute, the calling convention is a mechanism scheme that judges how a function returns the value, how are the parameters treated and where do they come from and what's the relationship between this function and the others. For instance, **NTAPI** is a Microsoft specific standard declaration calling convention which means the routine in question belongs to the NT API (in the Windows world however, the convention is **WINAPI**).  
  
**Prefix & Action & Suffix** -- The basic rule when writing a name of the function is that every routine must come up with a prefix that is tied to the respective module, the purpose of the function (hence the **action** which is the combination of a verb and subject such as `NtQueryInformationToken` or vice-versa) and a suffix. The suffix usually consists of **Ex** which means that the routine is an extension of the original one that adds more functionality in code. This is for the sake of preserving backwards compatibility with the older API calls, so that early versions of software that use such APIs can still benefit of the older function calls whereas the new software can benefit of using the newer/extended ones.  
  
**p (private)** -- A private routine, as the name implies, is a function that is only used within the module's file itself and cannot be used outside of that file. Think of it like a static defined function for example, where the scope is visible only on that file. Nearly every component of the Executive take use of this naming, an example of such a private routine is `SepCreateTokenLock`.  
  
**i (internal)** -- Same as the private routine, that it cannot be used outside of the respective module's file. Only one module of the Executive adopts such naming and that is the Memory Manager and the separate entity, the Kernel. Examples of routines are `KiPcToFileHeader` and `MiInitializePoolEvents`.  
  
**f (fastcall routine)** -- A fastcall routine is a function whose parameter arguments are passed to registers, whenever possible. This is a mere slight optimisation, if used properly. Notable modules that implement fastcall functions are the Object and I/O managers. This naming syntax can be used alognside with private or internal routine naming. Examples of functions are `IofCallDriver` and `ObfReferenceObject`. It's worth noting however that not all of the functions declared with fastcall convention are prefixed as such.

This prefix naming scheme doesn't apply only to the NT kernel but to the whole infrastructure space in the NT world, including the base kernel services and without a doubt, the NTDLL. Here are some other examples of prefixes notably known in Windows.

[![Prefixes](../images/nt-internals/part2/prefixes.png)](../images/nt-internals/part2/prefixes.png)