+++
title = "Understanding Blue Screens of Death (Part 1)"
slug = "blue-screen"
+++

## Introduction

Ahh, those blue screens. Everybody hates them and so do you. Especially when you're in the middle of something, like doing important work and out of a sudden a BSoD pops up leaving all of your unsaved work lost forever. It's so frustrating, isn't it? Despite this, Windows (and ReactOS as well) have multitude of reasons why the system has to be brought to a crash and in this article I'll cover the general tenets and aspects of the blue screen. In the Part II of the article I'll be covering how to actually troubleshoot a BSoD using WinDBG and understanding crash dumps.

## Why does ReactOS/Windows have to crash?

Before diving into the realm of blue screens, we must first understand the basic concept of what exactly a blue screen is. The Blue Screen of Death (or BSoD by its acronym) is typically the ominous error screen displayed by Windows indicating a serious condition in which Windows couldn't proceed further. Such condition can be, for example, an illegal execution or phenomenas that, if left un-guarded, could potentially corrupt the system further to the point of no recovery. In the NT programming realm we name BSoDs as bugchecks (and I'll name BSoDs with that term for the rest of the article).

What do I mean by that, exactly? For instance when the NT kernel, an important component of the Windows subsystem (e.g. Win32k) in the kernel space or kernel mode drivers were given a bogus pointer which points to a certain area of memory that couldn't be accessed for a plethora of reasons, like, if the said pointer has an address that is not currently mapped into the memory or it doesn't even exist in the first place the system has to immediately bring its own state to a sudden crash before making the situation way worse, like, writing corrupt data to the I/O storage.

Another instance of a fatal system crash is when some conditions have not been met in order for Windows to continue its normal operation. Let's take MULTIPROCESSOR_CONFIGURATION_NOT_SUPPORTED bugcheck code for example. This bugcheck occurs when Windows has caught that the hardware's multiple logical processors although none of them are symmetrical, that is, each of those have different types and level. It has no correlation with memory or I/O paging corruption whatsoever as the physical/virtual memory areas weren't even touched at all. The NT kernel is baffled because of such differences and doesn't know how to tackle the aforementioned situation, going through a system crash is the only option.

All in all, when it concerns the scenario of bugchecks, we all must ponder this thought that the situation is not black & white. A bugcheck can occur for various of reasons under a plethora of instances depending on the conditions which Windows went through for the bugcheck to happen. Here's a screenshot with a few summarised points of why a bugcheck happens.

![Various reasons of crashing](/images/blue-screen/bsod-reasons.png)

## The anatomy of a BSoD

The basic structure of a bugcheck screen is as follows, taking the previous variant of the blue screen (used from Windows 2000 to 7, the latter like 8 and 10 have a different layout).

![](/images/blue-screen/bsod.png)

In this blue screen, I have numbered the sections as each of those have a specific meaning. Let's get started:

1. Intro -- The generic introduction description. Nothing special here.
1. Bugcheck description -- This is the actual description that differs for each bugcheck code that was used to indicate the crash. On some bugchecks the bugcheck code is directly pointed whilst others may rather display a short summary description that's related to the specific bugcheck.
1. Steps -- As usual, generic description. It mostly tells you what to do in case of a bugcheck being invoked. This portion of the text can change depending on the bugcheck code that was invoked.
1. Technical data -- This is by far the most important piece in a blue screen. When a bugcheck occurs a STOP code is given alongside with 4 parameters. The STOP code indicates the type of bugcheck with the 4 parameters indicating specific and particular information that is tied to the bugcheck. The last 4 parameters are unique on their own as every bugcheck issues those parameters accordingly, some even do not issue any kind of information (the value is 0). In the latter case, if all the said 4 parameters are 0 (0x00000000) then the given bugcheck doesn't log out any extra information.
1. Additional data -- Provides the faulty process, the address and datestamp of the process in question.