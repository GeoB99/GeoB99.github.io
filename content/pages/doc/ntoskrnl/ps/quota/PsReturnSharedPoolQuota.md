+++
title = "PsReturnSharedPoolQuota"
slug = "PsReturnSharedPoolQuota"
+++

### Description

Returns the shared pool quota of a process (paged & non-paged).

### Internals & Parameters

```
VOID
NTAPI
PsReturnSharedPoolQuota(
   IN PEPROCESS Process,
   IN ULONG PagedPoolToReturn,
   IN ULONG NonPagedPoolToReturn)
```      

**Process** is a pointer to a Executive process (EPROCESS). **PagedPoolToReturn** and **NonPagedPoolToReturn** are the argument parameters the caller has to fill the specific amount of quota to be returned. What does this function do is typically giving back the quota both to the non-paged and paged memory pools at the same time. Finally, the function dereferences the quota block pointed by the executive process. The function doesn't return anything. The called functions for this routine are:

- PspGivebackQuota (called 2 times)
- PspDereferenceQuotaBlock