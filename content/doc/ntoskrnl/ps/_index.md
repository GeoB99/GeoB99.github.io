+++
title = "Process Manager (Kernel)"
list_name = "Functions & data structures list"
+++

## Process Manager summary

The process manager of the Executive deals with maintaining, creation of processes, management of internal process data and thread management. A function that lies down in this module starts with a prefix of **Ps**. Functions that begin with **Psp** are so called -- private functions. A private function is a function that is originally not within export routines list and they're used only in the internal source code files of the said module.

An important distinction to make is that not every function in process manager kernel service begins with **Ps**. In fact, shim application management of the said kernel service has functions that start with **Apphelp**.