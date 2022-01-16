+++
title = "NTDLL Tree"
slug = "ntdll-tree"
+++

## Native API user-mode layer (NTDLL) layout source tree

The Native API, serving the purpose as a system call interface for subsystem environments, provides the Rtl section known as the Run-Time library as well as Loader and SxS (Side-by-Side Assembly) module source codes. The base library service of the Windows subsystem, **Kernel32.dll**, makes a call into NTDLL which in turn invokes a specific kernel mode service in the NT kernel to accomplish a request. **User32.dll** and **Gdi32.dll** libraries are exceptions as these make calls which are then trapped into kernel mode in Win32k.sys, not NTDLL!

With that said, whenever an application makes a function call to `IsProcessInJob` in **Kernel32.dll** library the call flow operation goes through NTDLL and then into the kernel with the path leading to `NtIsProcessInJob` call. Windows ensures that whatever service call happening in user mode must be uniform, that is, the proper number of kernel mode services in the NT kernel have to be requested for a specific work.

<ul class = "tree">
         <li>d:
            <ul>
               <li>nt
                  <ul>
                     <li>base (Base Operating System)
                        <ul>
                           <!-- NTDLL layer -->
                           <li>ntdll (Native API layer)
                              <ul>
                                 <li>curdir.c</li>
                                 <li>dlluistb.c</li>
                                 <li>importtablehash.cpp</li>
                                 <li>ldrapi.c</li>
                                 <li>ldrinit.c</li>
                                 <li>ldrsnap.c</li>
                                 <li>ldrutil.c</li>
                                 <li>memstm.c</li>
                                 <li>query.c</li>
                                 <li>resource.c</li>
                                 <li>seurtl.c</li>
                                 <li>sxsactctx.c</li>
                                 <li>sxsctxact.c</li>
                                 <li>sxsctxsrch.c</li>
                                 <li>sxsisol.cpp</li>
                                 <li>sxsquery.c</li>
                                 <li>sxsstorage.c</li>
                                 <li>sxsstoragemap.c</li>
                                 <li>verifier.c</li>
                              </ul>
                           </li>
                           <!-- NT kernel -->
                           <li>ntos (NT kernel)
                              <ul>
                                 <!-- NT kernel Run-Time library -->
                                 <li>rtl (NT kernel Run-Time Library)
                                    <ul>
                                       <li>avltable.c</li>
                                       <li>bitmap.c</li>
                                       <li>bootstatus.c</li>
                                       <li>cnvint.c</li>
                                       <li>environ.c</li>
                                       <li>gentable.c</li>
                                       <li>heap.c</li>
                                       <li>heapdll.c</li>
                                       <li>heappage.c</li>
                                       <li>ldrrsrc.c</li>
                                       <li>lookasid.c</li>
                                       <li>lznt1.c</li>
                                       <li>nls.c</li>
                                       <li>nlsxlat.c</li>
                                       <li>rtlexec.c</li>
                                       <li>rtlimagentheader.c</li>
                                       <li>rtlvalidateunicodestring.c</li>
                                       <li>rxact.c</li>
                                       <li>sertl.c</li>
                                       <li>string.c</li>
                                       <li>threads.c</li>
                                       <li>timer.c</li>
                                       <li>tracedb.c</li>
                                       <li>version.c</li>
                                       <li>wait.c</li>
                                       <li>worker.c</li>
                                    </ul>
                                 </li>
                              </ul>
                           </li>
                           <!-- Windows Management Instrumentation -->
                           <li>wmi (Windows Management Instrumentation)
                              <ul>
                                 <li>inc (Header Files)
                                    <ul>
                                       <li>common.h</li>
                                       <li>request.h</li>
                                       <li>wmiump.h</li>
                                    </ul>
                                 </li>
                                 <li>ntdll (Native API layer)
                                    <ul>
                                       <li>guidapi.c</li>
                                       <li>logapi.c</li>
                                       <li>mofapi.c</li>
                                       <li>notify.c</li>
                                       <li>ntdlltrc.c</li>
                                       <li>request.c</li>
                                       <li>trcapi.c</li>
                                       <li>umlog.c</li>
                                    </ul>
                                 </li>
                              </ul>
                           </li>
                        </ul>
                     </li>
                  </ul>
               </li>
            </ul>
         </li>
      </ul>