+++
title = "Kernel"
+++

## Kernel design summary

The NT kernel is the fundamental core at the deepest level in Windows that interacts with the bare metal (the hardware). The kernel compromises two distinct parts that makes up the whole NT kernel. The **Executive** and the **microkernel** (although the latter is more a microkernel-ish monolithic kernel than a very real microkernel per se, in rigorous definition of what a microkernel is). The **Executive** of the kernel bases on various kernel-mode modules of NTOSKRNL, the base kernel OS services such as memory manager, I/O manager, local procedure call (LPC) and a whole lot more. For a list of the module prefix meanings, consult [this](/pages/reactos-source-tree/#ntoskrnl-tree) page.
    
## Kernel Executive service modules list

    <ul>
         <li>
            <a href = "/ps/">Ps</a>
         </li>
         <li>
            <a href = "/rtl/">Rtl</a>
         </li>
      </ul>