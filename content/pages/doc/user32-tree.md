+++
title = "User32 Tree"
+++

## User32 user-mode library layout tree

**User32.dll** is a user mode DLL library that provides windowing manager APIs to the client. An example of a call brought by the said library is `CreateWindowExW` which creates a window with extended styles. The documented function calls in the **User32.dll** library rely on undocumented internal functions in Win32k, the kernel mode side of the Windows subsystem.

{{<raw-html>}}
<ul class = "tree">
         <li>d:
            <ul>
               <li>nt
                  <ul>
                     <li>windows (Windows Subsystem)
                        <ul>
                           <li>core (Core Windows Kernel Subsystem)
                              <ul>
                                 <!-- Native USER Window Manager -->
                                 <li>ntuser (Native USER Window Manager)
                                    <ul>
                                       <!-- USER user-mode library -->
                                       <li>client (USER user-mode library)
                                          <ul>
                                             <li>acons.c</li>
                                             <li>btnctl.c</li>
                                             <li>callback.c</li>
                                             <li>classc.c</li>
                                             <li>cldib.c</li>
                                             <li>clenum.c</li>
                                             <li>clhook.c</li>
                                             <li>client.c</li>
                                             <li>clinit.c</li>
                                             <li>clmenu.c</li>
                                             <li>clmsg.c</li>
                                             <li>clrect.c</li>
                                             <li>clres.c</li>
                                             <li>cltxt.h</li>
                                             <li>combodir.c</li>
                                             <li>comboini.c</li>
                                             <li>connect.c</li>
                                             <li>csrstubs.c</li>
                                             <li>ddemlcli.c</li>
                                             <li>ddemlwp.c</li>
                                             <li>ddetrack.c</li>
                                             <li>dlgbegin.c</li>
                                             <li>dlgend.c</li>
                                             <li>dlgmgr.c</li>
                                             <li>dlgmgr2.c</li>
                                             <li>dlgmgrc.c</li>
                                             <li>dmmnem.c</li>
                                             <li>draw.c</li>
                                             <li>drawtext.c</li>
                                             <li>edecrare.c</li>
                                             <li>editec.c</li>
                                             <li>editml.c</li>
                                             <li>editsl.c</li>
                                             <li>edmlrare.c</li>
                                             <li>fareast.c</li>
                                             <li>fntsweep.c</li>
                                             <li>getsetc.c</li>
                                             <li>handles.c</li>
                                             <li>hdata.c</li>
                                             <li>help.c</li>
                                             <li>hsz.c</li>
                                             <li>imectl.c</li>
                                             <li>immhotky.c</li>
                                             <li>instance.c</li>
                                             <li>lb1.c</li>
                                             <li>lboxctl1.c</li>
                                             <li>lboxctl2.c</li>
                                             <li>lboxctl3.c</li>
                                             <li>lboxrare.c</li>
                                             <li>mdimenu.c</li>
                                             <li>mdiwin.c</li>
                                             <li>menuc.c</li>
                                             <li>menuddc.c</li>
                                             <li>mmcl.c</li>
                                             <li>mngrayc.c</li>
                                             <li>monitor.c</li>
                                             <li>msgbox.c</li>
                                             <li>ntcftxt.h</li>
                                             <li>ntstubs.c</li>
                                             <li>oemxlate.c</li>
                                             <li>queuec.c</li>
                                             <li>random.c</li>
                                             <li>reader.c</li>
                                             <li>register.c</li>
                                             <li>rtlinit.c</li>
                                             <li>rtlres.c</li>
                                             <li>sbapi.c</li>
                                             <li>statctl.c</li>
                                             <li>stdptcl.c</li>
                                             <li>strings.c</li>
                                             <li>usercli.h</li>
                                             <li>winable.c</li>
                                             <li>winmgrc.c</li>
                                             <li>wsprintf.c</li>
                                             <li>wstrings.c</li>
                                             <li>xact.c</li>
                                             <li>combo.c</li>
                                             <li>wow.c</li>
                                          </ul>
                                       </li>
                                       <!-- Header files -->
                                       <li>inc (Header Files)
                                          <ul>
                                             <li>ntcb.h</li>
                                          </ul>
                                       </li>
                                       <!-- User32 Run-Time Library -->
                                       <li>rtl (User32 Run-Time library)
                                          <ul>
                                             <li>chartran.c</li>
                                             <li>draw.c</li>
                                             <li>drawtext.c</li>
                                             <li>menu.c</li>
                                             <li>mmrtl.c</li>
                                             <li>winmgr.c</li>
                                             <li>wow.c</li>
                                             <li>winevent.c</li>
                                          </ul>
                                       </li>
                                    </ul>
                                 </li>
                                 <!-- Win32k Run-Time Library -->
                                 <li>rtl (Win32k Run-Time Library)
                                    <ul>
                                       <li>debug.c</li>
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
