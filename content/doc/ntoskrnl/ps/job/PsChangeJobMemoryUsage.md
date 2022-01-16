+++
title = "PsChangeJobMemoryUsage"
slug = "PsChangeJobMemoryUsage"
+++

## PsChangeJobMemoryUsage

### Description

This function changes the memory usage of a specific process Executive job.

### Internals & Parameters

```
BOOLEAN
NTAPI
PsChangeJobMemoryUsage(
   IN ULONG Constant,
   IN SSIZE\_T UsageAmount)
```

**Constant** is a parameter that must be set with a constant value of 10 (0x00000010) with the behaviour of this constant being discovered in Windows Server 2003. Currently it's yet to be understood what is the purpose of this parameter and what is it needed for. **UsageAmount** indicates the size difference, the necessary amount for the new memory usage to be changed for the job. The last parameter takes a signed integer value to describe the size. It's worth noting the parameter can take a negative integer which is also left to be understood the reasoning behind this.

This function is called from various places of the NT kernel, notably from `MiRemoveVadCharges` and `NtAllocateVirtualMemory`. It returns **TRUE** when the function completed successfully at changing the memory usage of a job, **FALSE** otherwise.

### Called Functions

* KiAcquireGuardedMutex
* IoSetIoCompletion
* KeSignalGateBoostPriority
* KiCheckForKernelApcDelivery