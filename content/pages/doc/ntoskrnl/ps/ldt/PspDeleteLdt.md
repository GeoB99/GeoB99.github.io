+++
title = "PspDeleteLdt (Local Descriptor Table)"
slug = "PspDeleteLdt"
+++

### Description

Deletes the Local Descriptor Table (LDT) resources previously created by `PspCreateLdt`.

### Internals & Parameters

```
VOID
NTAPI
PspDeleteLdt(
   IN PEPROCESS Process)
```   

**Process** is a pointer to a Executive process (EPROCESS). The function gathers the non-paged pool quota of the process and deallocates the memory pool block within the memory space. The aforementioned memory pool is created by `PspCreateLdt` during the call of `ExAllocatePoolWithTag` function. The tag named for such pool memory is `dLsP`. The function doesn't return anything.

### Called Functions

- PsReturnProcessNonPagedPoolQuota
- ExFreePoolWithTag (called 2 times)