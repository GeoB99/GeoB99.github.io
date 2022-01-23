+++
title = "PspSetLdtInformation"
slug = "PspSetLdtInformation"
+++

### Description

Sets the LDT information to a specific process given the process executive.

### Internals & Parameters

```
NTSTATUS
NTAPI
PspSetLdtInformation(
   IN PEPROCESS Process,
   IN PROCESS\_LDT\_INFORMATION LdtInformation,
   IN ULONG InformationLength)
```      

**Process** is a pointer to a EPROCESS structure, the executive process. **LdtInformation** contains information about Local Descriptor Table (LDT) entries. **InformationLength** is the size length, in bytes, of the second parameter which is LdtInformation. The function returns a NTSTATUS value, that is, STATUS\_SUCCESS if the operation completed successfully or STATUS\_ACCESS\_VIOLATION if a specific address is invalid or not allowable for read/write that the caller tried to access it.

### Called Functions

- \_SEH\_prolog
- ExAllocatePoolWithQuotaTag
- PspIsDescriptorValid
- KeWaitForSingleObject
- ExFreePoolWithTag (called 4 times)
- ExAllocatePoolWithTag
- Ke386SetLdtProcess (called 4 times)
- PsReturnProcessNonPagedPoolQuota (called 2 times)
- PspCreateLdt (called 2 times)
- PsChargeProcessNonPagedPoolQuota (called 2 times)
- KeReleaseMutex
- Ke386SetDescriptorProcess (called 2 times)
- \_SEH\_epilog