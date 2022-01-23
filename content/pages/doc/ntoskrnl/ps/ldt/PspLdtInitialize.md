+++
title = "PspLdtInitialize"
slug = "PspLdtInitialize"
+++

### Description

Initialises the Local Descriptor Table (LDT) during the early boot phase (Phase 0).

### Internals & Parameters

```
VOID
NTAPI
PspLdtInitialize(VOID)
```

The function takes no arguments. What does it simply do is to initialise a mutant object specifically in the context of the LDT realm. Internally such mutant object (or mutex) is named as **LdtMutex**. The initialisation of such LDT mutex object is done at the early boot phase of Windows, in `PspInitPhase0` function which is responsible for Process Manager kernel subsystem initialisation.

### Called Functions

- KeInitializeMutex