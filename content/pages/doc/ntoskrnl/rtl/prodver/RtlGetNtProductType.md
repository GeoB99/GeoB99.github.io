+++
title = "RtlGetNtProductType (Run-Time Library -- Kernel)"
slug = "RtlGetNtProductType"
+++

### Description

Retrieves the NT type product of the operating system.

### Internals & Parameters

```
BOOLEAN
NTAPI
RtlGetNtProductType(
   OUT PNT\_PRODUCT\_TYPE ProductType)
```      

**ProductType** is a pointer to a NT\_PRODUCT\_TYPE enumeration. The product type can be either Workstation (WinNT), Server (ServerNT) and Advanced Server (LanmanNT). The product type defines the usage of the operating system (Workstation in this case, is regarded for daily-life low-end user usage). This kernel mode function relies on the Registry to query the type of the operating system product. The function returns **TRUE** on success, **FALSE** otherwise. In the latter case, WinNT is returned to the output argument parameter of the function to the caller as the default product type on failure.

### Called Functions

- RtlInitUnicodeString (called 5 times)
- ZwOpenKey
- ExAllocatePoolWithTag
- ZwQueryValueKey
- RtlEqualUnicodeString (called 3 times)
- ExFreePoolWithTag
- ZwClose


### Remarks

As told in the section of the function above, RtlGetNtProductType queries thorough the Registry to grab the product type of the operating system. In comparison to the user mode variant of the function in NTDLL layer, the user mode variant caches the product type data from a particular kernel data structure, `_KUSER_SHARED_DATA`. This structure is managed internally and initialized by the NT kernel during boot initialization phase.