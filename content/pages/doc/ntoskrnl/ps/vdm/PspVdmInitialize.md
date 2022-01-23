+++
title = "PspVdmInitialize"
slug = "PspVdmInitialize"
+++

### Description

Initializes the Virtual DOS Machine (DOS) in boot phase.

### Internals & Parameters

```
NTSTATUS
NTAPI
PspVdmInitialize(VOID)
```      

The function takes no parameters, it merely initializes the VDM during boot phase specifically during process manager initialization procedure -- first phase (PspInitPhase0). PspInitPhase0 is invoked by PsInitSystem, the completion of the 1st phase leads with the preparation for the 2nd phase initialization. PspVdmInitialize returns a NTSTATUS value, STATUS\_SUCCESS respectively. The function invokes the Executive to add the VDM resource in the system resources list which in turn the kernel is responsible for managing such resource for whatever purpose in the context of VDM.

### Called Functions

- ExInitializeResourceLite