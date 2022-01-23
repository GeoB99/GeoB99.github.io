+++
title = "PsChargeSharedPoolQuota"
slug = "PsChargeSharedPoolQuota"
+++

### Description

Charges the shared pool quota of a process (paged & non-paged).

### Internals & Parameters

```
VOID
NTAPI
PsChargeSharedPoolQuota(
   IN PEPROCESS Process,
   IN ULONG PagedPoolToCharge,
   IN ULONG NonPagedPoolToCharge)
```      

**Process** is a pointer to a Executive process (EPROCESS). **PagedPoolToCharge** and **NonPagedPoolToCharge** are the argument parameters the caller has to fill the specific amount of quota to be charged for the process. What does this function do is typically expanding the quota list both to the non-paged and paged memory pools at the same time. The function doesn't return anything. The called functions for this routine are:

- PspExpandQuota (called 2 times)
- PspGivebackQuota