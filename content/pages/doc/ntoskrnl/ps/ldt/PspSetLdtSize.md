+++
title = "PspSetLdtSize"
slug = "PspSetLdtSize"
+++

### Description

Sets the Local Descriptor Table (LDT) size of a Executive process object.

### Internals & Parameters

```
NTSTATUS
NTAPI
PspSetLdtSize(
   IN PEPROCESS Process,
   IN PROCESS\_LDT\_SIZE LdtSize,
   IN ULONG InformationLength)
```      

**Process** is a pointer to a Executive process (EPROCESS). **LdtSize** is the Local Descriptor Table (LDT) size pointed by its particular structure -- **PROCESS\_LDT\_SIZE**. **InformationLength** is the length size, in bytes, pointed by **LdtSize** parameter. The function is internally called by NtSetInformationProess() when `ProcessLdtSize` information class is invoked. The function returns STATUS\_SUCCESS if the size of LDT of a process has been set. Otherwise the function will return **STATUS\_INFO\_LENGTH\_MISMATCH** if the information length size doesn't match with the actual information parameter argument, **LdtSize**, **STATUS\_INVALID\_LDT\_SIZE** or **STATUS\_NO\_LDT** if the given process doesn't have a LDT.

### Called Functions

- \_SEH\_prolog
- KeWaitForSingleObject
- KeReleaseMutex (called 2 times)
- PspCreateLdt
- Ke386SetLdtProcess
- ExFreePoolWithTag
- PsReturnProcessNonPagedPoolQuota
- \_SEH\_epilog