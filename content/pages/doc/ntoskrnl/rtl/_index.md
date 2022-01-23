+++
title = "Run-Time (Kernel)"
list_name = "Functions & data structures list"
+++

The Run-Time library (RTL) is a kernel executive module that provides the Run-Time interface and routines for the NT kernel itself and kernel mode drivers. The library comprises a set of functions for string operations, arithemtic operations, data type conversions and a whole lot more. Functions that belong in the RTL executive module of the Executive realm of the kernel denote with a prefix as **Rtl** whereas private Run-Time library functions that aren't exported nor used outside of the said module start with **Rtlp**.

Albeit the RTL kernel service module brings the kernel mode RTL interface in the kernel realm, there's another Run-Time library specifically used for the user mode realm, which it can be found in the NTDLL layer (or simply the Native API layer infrastructure). Interestingly enough, some RTL functions can be found in either operating system space, whether it's in kernel mode or user mode -- an example of such a function being `RtlGetVersion`. A possible theory and explanation for this is that Microsoft took a decision to have certain functions of the same nature in terms of synopsis but with slightly (or complete) different implementation to satisfy both parties -- the kernel mode and user mode. With that said, taking `RtlGetVersion` again as an example, it is implemented in the kernel executive module, RTL, in such a way in order to cover the needs and reflect the design in kernel mode. Hence for this matter, Windows ensures that the caller executes the right call of the right ring level (a user mode software cannot call the kernel mode variant of the function or vice versa).

Besides that, some functions in the RTL library can even have same implementation both in user mode and kernel mode or certain functions that exist in user mode but aren't implemented in kernel mode and vice versa.