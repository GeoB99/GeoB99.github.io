+++
title = "PspDeleteVdmObjects"
slug = "PspDeleteVdmObjects"
+++

### Description

Deletes Virtual DOS Machine (DOS) objects. The function is called in a process deletion scenario (called by **PspDeleteProcess**).

### Internals & Parameters

```
VOID
NTAPI
PspDeleteVdmObjects(
   IN PEPROCESS Process)
```      

**Process** is a pointer to a Executive process (EPROCESS). The function internally frees the **VdmObjects** member of the EPROCESS structure and deletes the Executive resource from the system's resources list. Besides that, the function also deallocates the memory pool block within the memory space of the Virtual DOS Machine (VDM) objects. A peculiarity to take into consideration regard this function is that this function returns the process pool quota (PsReturnProcessPagedPoolQuota and PsReturnProcessNonPagedPoolQuota being called respectively). A possible theory is that the returned paged pool quota is from the allocated Executive process pointed by EPROCESS.

In a non-paged pool scenario however, the actual pool quota returned comes from the VDM objects which are about to be deallocated from the memory, that is guaranteed to stay in the physical memory area. The VDM objects are allocated in a non paged pool on a per process basis in `Ke386CallBios`. This function doesn't return anything.

### Called Functions

- ExFreePoolWithTag (called 5 times)
- ExDeleteResourceLite
- PsReturnProcessPagedPoolQuota
- PsReturnProcessNonPagedPoolQuota (called 2 times)