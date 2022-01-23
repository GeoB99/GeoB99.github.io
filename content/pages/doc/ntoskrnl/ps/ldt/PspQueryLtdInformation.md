+++
title = "PspQueryLtdInformation"
slug = "PspQueryLtdInformation"
+++

### Description

This function queries the local descriptor table (LDT) information of a specific process.

### Internals & Parameters

This function takes a number of 4 parameters, it is unknown the nature of the said parameters and what are they. However it is noted that this function returns a value of NTSTATUS. An example of NTSTATUS values returned by this function are STATUS\_INFO\_LENGTH\_MISMATCH, STATUS\_INVALID\_LDT\_SIZE and STATUS\_INVALID\_LDT\_OFFSET.

### Called Functions

- \_SEH\_prolog
- KeWaitForSingleObject
- KeReleaseMutex
- \_SEH\_epilog