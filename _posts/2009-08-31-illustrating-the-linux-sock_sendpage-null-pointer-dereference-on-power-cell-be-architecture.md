---
author: Ramon de C Valle
categories:
- security
comments: true
excerpt_separator: <!-- more -->
layout: post
published: true
tags:
- exploit development
- vulnerability research
title: Illustrating the Linux sock_sendpage() NULL Pointer Dereference on Power/Cell BE Architecture
updated: 2009-09-10
---

!!! note "Sep 10, 2009"

    We released [a third and final version][7] of the exploit. The third
    version has complete support for i386, x86_64, ppc, and ppc64; uses the
    [personality trick][4] published by Tavis Ormandy and Julien Tinnes; uses
    the TOC pointer workaround for data items addressing on ppc64 (i.e.,
    functions in exploit code and libc can be referenced); and for
    SELinux-enforced systems, has improved search for domains configured to
    allow mmap_zero it can transition to.


!!! note "Sep 7, 2009"

    We released [a second version][6] of the exploit. The second version also
    works with Linux kernel versions that have copy-on-write (COW) credentials
    (e.g., Fedora 11), and for SELinux-enforced systems, it automatically
    searches the SELinux policy rules for domains configured to allow mmap_zero
    it can transition to, and tries to exploit the vulnerability using these
    domains.


We wrote [an exploit][1] for the [Linux kernel sock_sendpage NULL pointer
dereference vulnerability][2], discovered by Tavis Ormandy and Julien Tinnes,
to illustrate the exploitability of this vulnerability on Linux running on
Power/Cell BE architecture -based processors.

The exploit uses the SELinux policy and the mmap_min_addr protection issue
(CVE-2009-2695) to exploit this vulnerability on Red Hat Enterprise Linux 5.3
and CentOS 5.3. The problem, first noticed by Brad Spengler, was described by
Red Hat in the Red Hat Knowledgebase article: [Security-Enhanced Linux
(SELinux) policy and the mmap_min_addr protection (CVE-2009-2695)][3]

<!-- more -->

We added support for i386 and x86_64 for completeness. For a more complete
implementation, see [Brad Spengler's exploit][4], which also uses the
[personality trick][5] published by Tavis Ormandy and Julien Tinnes.

Linux kernel versions from 2.4.4 to 2.4.37.4, and from 2.6.0 to 2.6.30.4 are
vulnerable.

The exploit was tested on:

* CentOS 5.3 (2.6.18-128.7.1.el5) is not vulnerable
* CentOS 5.3 (2.6.18-128.4.1.el5)
* CentOS 5.3 (2.6.18-128.2.1.el5)
* CentOS 5.3 (2.6.18-128.1.16.el5)
* CentOS 5.3 (2.6.18-128.1.14.el5)
* CentOS 5.3 (2.6.18-128.1.10.el5)
* CentOS 5.3 (2.6.18-128.1.6.el5)
* CentOS 5.3 (2.6.18-128.1.1.el5)
* CentOS 5.3 (2.6.18-128.el5)
* CentOS 4.8 (2.6.9-89.0.9.EL) is not vulnerable
* CentOS 4.8 (2.6.9-89.0.7.EL)
* CentOS 4.8 (2.6.9-89.0.3.EL)
* CentOS 4.8 (2.6.9-89.EL)
* Fedora 11 (2.6.29.4-167.fc11)
* Fedora 10 (2.6.27.5-117.fc10)
* Red Hat Enterprise Linux 5.3 (2.6.18-128.7.1.el5) is not vulnerable
* Red Hat Enterprise Linux 5.3 (2.6.18-128.4.1.el5)
* Red Hat Enterprise Linux 5.3 (2.6.18-128.2.1.el5)
* Red Hat Enterprise Linux 5.3 (2.6.18-128.1.16.el5)
* Red Hat Enterprise Linux 5.3 (2.6.18-128.1.14.el5)
* Red Hat Enterprise Linux 5.3 (2.6.18-128.1.10.el5)
* Red Hat Enterprise Linux 5.3 (2.6.18-128.1.6.el5)
* Red Hat Enterprise Linux 5.3 (2.6.18-128.1.1.el5)
* Red Hat Enterprise Linux 5.3 (2.6.18-128.el5)
* Red Hat Enterprise Linux 4.8 (2.6.9-89.0.9.EL) is not vulnerable
* Red Hat Enterprise Linux 4.8 (2.6.9-89.0.7.EL)
* Red Hat Enterprise Linux 4.8 (2.6.9-89.0.3.EL)
* Red Hat Enterprise Linux 4.8 (2.6.9-89.EL)
* SUSE Linux Enterprise Server 11 (2.6.27.29-0.1) is not vulnerable
* SUSE Linux Enterprise Server 11 (2.6.27.25-0.1)
* SUSE Linux Enterprise Server 11 (2.6.27.23-0.1)
* SUSE Linux Enterprise Server 11 (2.6.27.21-0.1)
* SUSE Linux Enterprise Server 11 (2.6.27.19-5)
* SUSE Linux Enterprise Server 10 SP2 (2.6.16.60-0.42.4) is not vulnerable
* SUSE Linux Enterprise Server 10 SP2 (2.6.16.60-0.39.3)
* SUSE Linux Enterprise Server 10 SP2 (2.6.16.60-0.37_f594963d)
* SUSE Linux Enterprise Server 10 SP2 (2.6.16.60-0.34)
* SUSE Linux Enterprise Server 10 SP2 (2.6.16.60-0.33)
* SUSE Linux Enterprise Server 10 SP2 (2.6.16.60-0.31)
* SUSE Linux Enterprise Server 10 SP2 (2.6.16.60-0.29)
* SUSE Linux Enterprise Server 10 SP2 (2.6.16.60-0.27)
* SUSE Linux Enterprise Server 10 SP2 (2.6.16.60-0.23)
* SUSE Linux Enterprise Server 10 SP2 (2.6.16.60-0.21)
* Ubuntu 8.10 (2.6.27-14) is not vulnerable
* Ubuntu 8.10 (2.6.27-11)
* Ubuntu 8.10 (2.6.27-9)
* Ubuntu 8.10 (2.6.27-7)
* openSUSE 11.1 (2.6.27.29-0.1) is not vulnerable
* openSUSE 11.1 (2.6.27.25-0.1)
* openSUSE 11.1 (2.6.27.23-0.1)
* openSUSE 11.1 (2.6.27.21-0.1)
* openSUSE 11.1 (2.6.27.19-3.2)
* openSUSE 11.1 (2.6.27.7-9)

It may also work on earlier versions of these and other distributions.

[1]: https://github.com/rcvalle/exploits/raw/HEAD/linux-sendpage.c
[2]: https://blog.cr0.org/2009/08/linux-null-pointer-dereference-due-to.html
[3]: https://access.redhat.com/articles/17995
[4]: https://grsecurity.net/~spender/exploits/wunderbar_emporium2.tgz
[5]: https://blog.cr0.org/2009/06/bypassing-linux-null-pointer.html
[6]: https://github.com/rcvalle/exploits/raw/HEAD/linux-sendpage2.tar.gz
[7]: https://github.com/rcvalle/exploits/raw/HEAD/linux-sendpage3.tar.gz
