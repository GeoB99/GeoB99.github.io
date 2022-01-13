+++
title = "Documentation"
list_name = "Windows Server 2003 layout source tree"
+++

## Documentation home page
In this section of the website I'll provide documentation and details of parts that aren't currently documented over the Internet, with the OS platform of interest being Windows Server 2003 as ReactOS primarily targets this edition of Windows. From here I publish details about undocumented functions (and possibly structures) in WS2003, ranging from the NT kernel itself to other areas and fields of the operating system. The section is divived into two separate fields, kernel and user mode.

### Disclaimer!

Documentation pages are subject to change frequently depending on information and data I gather during my research so whatever that was being written in the past may change in the future.

## Windows Server 2003 layout source tree

The layout source paths tree of Windows components were taken by extracting the path strings embedded in debug checked build files. This helps understanding the structure of a module and determining how a certain component works. The strings were extracted with Strings Sysinternals.

`./strings.exe -nobanner ./filename | grep -e "^[a-zA-Z]:\\\\" | sort -u`

Where filename is the file of interest that you want to extract the embedded path strings of the file. This command has to be ran in a *nix-like shell (Cygwin or Git SCM Bash in Windows). You can also output the data stream pointed by the command into a text file. The strings will be sorted in alphabetical order after the string extraction is complete.