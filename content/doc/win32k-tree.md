+++
title = "Win32K Tree"
slug = "win32k-tree"
+++

## Windows Subsystem Kernel layout tree

The Windows subsystem environment is divided amongst two chunks that make up the entirety of the said subsystem. The user mode, with client libraries used by applications and components that interact within the user mode space (**Kernel32.dll**, **Gdi32.dll**, **User32.dll** et al) and a large portion being the kernel mode. The latter portion is in itself left undocumented, with no major details or explanation provided about the inner implementation of the kernel mode side. And what I am referring about the kernel mode portion is, without a doubt, **Win32k.sys**.

**Win32k.sys**, which is merely a kernel mode system driver, is responsible for graphics management -- what do you see on the screen. The kernel driver is separated into two major subset components: **GDI** (also known as Graphics Device Interface) and USER (known as the window manager of Windows). GDI is implemented internally in a directory named **ntgdi** (as you'd see in the tree layout below) whereas the window manager is named as **ntuser**. Within GDI source tree you'll see directories called **fontdrv**, **gre** and **halftone**. **Gre** (or Graphics rendering engine) is what it makes up the most of GDI source code base for implementation of primitive graphics handling, brushes, palette, colour objects and whatnot. When capturing the function calls in the call stack of Win32k with WinDBG, whilst in the course of debugging something, you may get across kernel routines such as `GreSetDCOwnerEx` with the prefix Gre\* denoting the function belongs to the GDI kernel module.

**ntuser**, or just USER, is the window manager that has the responsibility for the creation and management of USER objects such as windows, menus, cursor and other stuff. In other words, USER is the internal compoment that provides graphical interaction between the system and user. An important remark is worth noting -- whilst GDI is primarily written in C++, USER for its entirety remains written in C. It's not really surprising considering USER is a massive historic source code dating back with the very early versions of Windows (including the 9x editions as well such as Windows 95 and 98). The inception of Win32k started with the development and release of the successive Windows operating system, Windows NT 4.0. With the 4.0 version of Windows NT all the GDI and USER code were moved into a kernel mode system driver for the sake of improving overall performance in terms of handling GDI/USER objects in a timely fashion. Before that, the Windows subsystem core code was in a server/client communication process called CSRSS.


<ul class="tree">
         <li>d:
            <ul>
               <li>nt
                  <ul>
                     <!-- Public -->
                     <li>public
                        <ul>
                           <li>internal
                              <ul>
                                 <li>windows (Windows Subsystem)
                                    <ul>
                                       <li>inc (Header files)
                                          <ul>
                                             <li>muio.w</li>
                                          </ul>
                                       </li>
                                    </ul>
                                 </li>
                              </ul>
                           </li>
                        </ul>
                     </li>
                     <li>windows (Windows Subsystem)
                        <ul>
                           <li>core (Core Windows Kernel Subsystem)
                              <ul>
                                 <!-- Kernel mode -->
                                 <li>kmode (Kernel Mode)
                                    <ul>
                                       <li>w32init.c</li>
                                    </ul>
                                 </li>
                                 <!-- Native Graphics Device Interface (NTGDI) -->
                                 <li>ntgdi (Native Graphics Device Interface)
                                    <ul>
                                       <!-- Font Driver -->
                                       <li>fontdrv (Font Driver)
                                          <ul>
                                             <li>bmfd
                                                <ul>
                                                   <li>fon16.c</li>
                                                </ul>
                                             </li>
                                          </ul>
                                       </li>
                                       <!-- Graphics rendering engine (Gre) -->
                                       <li>gre (Graphics Rendering Engine)
                                          <ul>
                                             <li>aatext.cxx</li>
                                             <li>alphablt.cxx</li>
                                             <li>alphaimg.cxx</li>
                                             <li>bltlnk.cxx</li>
                                             <li>brushddi.cxx</li>
                                             <li>brushobj.hxx</li>
                                             <li>curseng.cxx</li>
                                             <li>dcgdi.cxx</li>
                                             <li>dcobj.hxx</li>
                                             <li>devlock.hxx</li>
                                             <li>dibapi.cxx</li>
                                             <li>drawstream.cxx</li>
                                             <li>drvsup.cxx</li>
                                             <li>engline.cxx</li>
                                             <li>fastfill.cxx</li>
                                             <li>hmgrapi.cxx</li>
                                             <li>htblt.cxx</li>
                                             <li>ntgdi.c</li>
                                             <li>opendc.cxx</li>
                                             <li>os.cxx</li>
                                             <li>palgdi.cxx</li>
                                             <li>patblt.cxx</li>
                                             <li>plgblt.cxx</li>
                                             <li>rgnobj.cxx</li>
                                             <li>solline.cxx</li>
                                             <li>strchblt.cxx</li>
                                             <li>strdir.cxx</li>
                                             <li>surfgdi.cxx</li>
                                             <li>surfobj.cxx</li>
                                             <li>textddi.cxx</li>
                                             <li>tranblt.cxx</li>
                                             <li>trimesh.cxx</li>
                                             <li>trivblt.cxx</li>
                                             <li>umpd.hxx</li>
                                             <li>umpddrv.cxx</li>
                                             <li>umpdeng.cxx</li>
                                             <li>umpdobj.cxx</li>
                                          </ul>
                                       </li>
                                       <!-- Halftone GDI Support -->
                                       <li>halftone (Halftone Tecnique Support)
                                          <ul>
                                             <li>ht
                                                <ul>
                                                   <li>htalias.c</li>
                                                   <li>htapi.c</li>
                                                   <li>htgetbmp.c</li>
                                                   <li>htmapclr.c</li>
                                                   <li>htmath.c</li>
                                                   <li>htmemory.c</li>
                                                   <li>htpat.c</li>
                                                   <li>htrender.c</li>
                                                   <li>htsetbmp.c</li>
                                                   <li>htstret.c</li>
                                                </ul>
                                             </li>
                                          </ul>
                                       </li>
                                    </ul>
                                 </li>
                                 <!-- Native USER module (Window manager -- NTUSER) -->
                                 <li>ntuser (Native USER Window Manager)
                                    <ul>
                                       <li>inc (Header files)
                                          <ul>
                                             <li>ntcb.h</li>
                                             <li>user.h</li>
                                          </ul>
                                       </li>
                                       <!-- NTUSER Run-Time Library -->
                                       <li>rtl (NTUSER Run-Time Library)
                                          <ul>
                                             <li>chartran.c</li>
                                             <li>draw.c</li>
                                             <li>drawtext.c</li>
                                             <li>menu.c</li>
                                             <li>mmrtl.c</li>
                                             <li>rect.c</li>
                                             <li>winevent.c</li>
                                             <li>winmgr.c</li>
                                             <li>winprop.c</li>
                                             <li>wow.c</li>
                                          </ul>
                                       </li>
                                       <!-- Kernel Mode USER -->
                                       <li>kernel (Kernel Mode USER)
                                          <ul>
                                             <li>access.c</li>
                                             <li>acons.c</li>
                                             <li>atom.c</li>
                                             <li>calcclrc.c</li>
                                             <li>caption.c</li>
                                             <li>capture.c</li>
                                             <li>caret.c</li>
                                             <li>class.c</li>
                                             <li>classchg.c</li>
                                             <li>cleanup.c</li>
                                             <li>clipbrd.c</li>
                                             <li>createw.c</li>
                                             <li>cursor.c</li>
                                             <li>dc.c</li>
                                             <li>ddemlsvr.c</li>
                                             <li>ddetrack.c</li>
                                             <li>debug.c</li>
                                             <li>desktop.c</li>
                                             <li>dragdrop.c</li>
                                             <li>dtbitmap.c</li>
                                             <li>dwp.c</li>
                                             <li>enumwin.c</li>
                                             <li>event.c</li>
                                             <li>ex.c</li>
                                             <li>exitwin.c</li>
                                             <li>fekbd.c</li>
                                             <li>focusact.c</li>
                                             <li>fullscr.c</li>
                                             <li>getset.c</li>
                                             <li>ghost.c</li>
                                             <li>handtabl.c</li>
                                             <li>heap.c</li>
                                             <li>help.c</li>
                                             <li>hidevice.c</li>
                                             <li>hooks.c</li>
                                             <li>hotkeys.c</li>
                                             <li>hungapp.c</li>
                                             <li>imehotky.c</li>
                                             <li>inctlpan.c</li>
                                             <li>init.c</li>
                                             <li>input.c</li>
                                             <li>job.c</li>
                                             <li>kbdlyout.c</li>
                                             <li>keyboard.c</li>
                                             <li>libmgmt.c</li>
                                             <li>loadbits.c</li>
                                             <li>logon.c</li>
                                             <li>menu.c</li>
                                             <li>menudd.c</li>
                                             <li>minmax.c</li>
                                             <li>misc.c</li>
                                             <li>miscutil.c</li>
                                             <li>mnaccel.c</li>
                                             <li>mnapi.c</li>
                                             <li>mnchange.c</li>
                                             <li>mncomput.c</li>
                                             <li>mncreate.c</li>
                                             <li>mndraw.c</li>
                                             <li>mndstry.c</li>
                                             <li>mngray.c</li>
                                             <li>mnkey.c</li>
                                             <li>mnloop.c</li>
                                             <li>mnpopup.c</li>
                                             <li>mnsel.c</li>
                                             <li>mnstate.c</li>
                                             <li>mnsys.c</li>
                                             <li>movesize.c</li>
                                             <li>multimon.c</li>
                                             <li>newmouse.c</li>
                                             <li>ntimm.c</li>
                                             <li>ntinput.c</li>
                                             <li>ntstubs.c</li>
                                             <li>paint.c</li>
                                             <li>palette.c</li>
                                             <li>pnp.c</li>
                                             <li>pool.c</li>
                                             <li>power.c</li>
                                             <li>profile.c</li>
                                             <li>queue.c</li>
                                             <li>random.c</li>
                                             <li>rare.c</li>
                                             <li>sbctl.c</li>
                                             <li>scrollw.c</li>
                                             <li>security.c</li>
                                             <li>sendmsg.c</li>
                                             <li>server.c</li>
                                             <li>service.c</li>
                                             <li>shadow.c</li>
                                             <li>showwin.c</li>
                                             <li>snapshot.c</li>
                                             <li>spb.c</li>
                                             <li>sprite.c</li>
                                             <li>srvhook.c</li>
                                             <li>ssend.c</li>
                                             <li>swp.c</li>
                                             <li>syscmd.c</li>
                                             <li>sysmet.c</li>
                                             <li>taskman.c</li>
                                             <li>timers.c</li>
                                             <li>tmswitch.c</li>
                                             <li>tooltips.c</li>
                                             <li>tounicod.c</li>
                                             <li>update.c</li>
                                             <li>usergdi.c</li>
                                             <li>userk.h</li>
                                             <li>validate.c</li>
                                             <li>visrgn.c</li>
                                             <li>winable.c</li>
                                             <li>winable2.c</li>
                                             <li>winmgr.c</li>
                                             <li>winprop.c</li>
                                             <li>winsta.c</li>
                                             <li>winwhere.c</li>
                                             <li>wmicon.c</li>
                                             <li>xlate.c</li>
                                          </ul>
                                       </li>
                                    </ul>
                                 </li>
                                 <!-- Win32k Run-Time Library -->
                                 <li>rtl (Win32k Run-Time Library)
                                    <ul>
                                       <li>debug.c</li>
                                       <li>heap.c</li>
                                       <li>tag.c</li>
                                    </ul>
                                 </li>
                                 <!-- Win32k Header Files -->
                                 <li>w32inc (Win32k Header Files)
                                    <ul>
                                       <li>w32p.h</li>
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