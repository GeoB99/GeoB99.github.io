+++
title = "Winsrv layout tree"
slug = "winsrv-tree"
+++

## Windows USER + Console server library layout tree

Nothing much has to be said about this library. **Winsrv.dll** is all but a provider for server intercommunication support for console and window manager environment. That is, the server being the kernel mode realm of the Windows subsystem environment (as usual **Winsrv.dll** relies on Win32k). Speaking of the window manager environment, some fundamental aspects of **Winsrv.dll** are the hard-error implementation, shutdown/logout notification mechanism and windowing message communication.

{{<raw-html>}}
<ul class="tree">
         <li>d:
            <ul>
               <li>nt
                  <ul>
                     <li>windows (Windows Subsystem)
                        <ul>
                           <li>core (Core Windows Kernel Subsystem)
                              <ul>
                                 <li>ntcon (Native Console)
                                    <ul>
                                       <li>server
                                          <ul>
                                             <li>_output.h</li>
                                             <li>_stream.h</li>
                                             <li>bitmap.c</li>
                                             <li>clipbrd.c</li>
                                             <li>cmdline.c</li>
                                             <li>convarea.c</li>
                                             <li>cursor.c</li>
                                             <li>dbcs.c</li>
                                             <li>directio.c</li>
                                             <li>find.c</li>
                                             <li>foncache.c</li>
                                             <li>hard.c</li>
                                             <li>input.c</li>
                                             <li>link.c</li>
                                             <li>menu.c</li>
                                             <li>misc.c</li>
                                             <li>output.c</li>
                                             <li>private.c</li>
                                             <li>resize.c</li>
                                             <li>share.c</li>
                                             <li>srvinit.c</li>
                                             <li>srvvdm.c</li>
                                             <li>stream.c</li>
                                          </ul>
                                       </li>
                                    </ul>
                                 </li>

                                 <!-- Native USER Window Manager -->
                                 <li>ntuser (Native USER Window Manager)
                                    <ul>
                                       <li>server
                                          <ul>
                                             <li>api.c</li>
                                             <li>command.c</li>
                                             <li>debug.c</li>
                                             <li>exitwin.c</li>
                                             <li>harderr.c</li>
                                             <li>icamsg.c</li>
                                             <li>instdev.c</li>
                                             <li>reclient.c</li>
                                             <li>sendmsg.c</li>
                                             <li>server.c</li>
                                          </ul>
                                       </li>
                                    </ul>
                                 </li>

                                 <!-- Win32k Run-Time Library -->
                                 <li>rtl (Win32k Run-Time Library)
                                    <ul>
                                       <li>heap.c</li>
                                    </ul>
                                 </li>

                                 <!-- Terminal Spool -->
                                 <li>termspl (Terminal Spool)
                                    <ul>
                                       <li>kmspool.c</li>
                                       <li>splkernl.c</li>
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
{{</raw-html>}}
