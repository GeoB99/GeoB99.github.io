+++
title = "PspRemoveProcessFromJob"
slug = "PspRemoveProcessFromJob"
+++

## PspRemoveProcessFromJob

### Description

The function removes a process executive object from a job.

### Internals & Parameters

```
VOID
NTAPI
PspRemoveProcessFromJob(
   IN PEPROCESS Process,
   IN PEJOB Job)
```

**Process** is a pointer to a Executive Process structure (EPROCESS). The first argument parameter is compulsory as it's needed to specify a process to be removed from a job, it mustn't be NULL. **Job** is a pointer to a Executive Job structure (EJOB). As with the second parameter, the caller is expected to pass a valid job object to the callee function service. The function acquires a resource within the calling thread in a waitable state, that is, the NT kernel ensures the said resource can be acquired for the calling thread within exclusive usage when the wait state is finished.

The job object structure's information is modified in the middle of the calling execution when the function successfully acquired the internal job resource. APC (Asynchronous Procedure Call) delivery is checked to ensure if there's kernel APC delivery prior to resource acquire procedure. The function doesn't return anything.

### Called Functions
* ExAcquireResourceExclusiveLite
* PspFoldProcessAccountingIntoJob
* ExReleaseResourceLite
* KiCheckForKernelApcDelivery