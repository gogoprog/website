---
layout: post
title:  "Belgian card reader on ArchLinux"
date:   2014-08-12 14:55:39
categories: linux app archlinux
---

First install the following packages :

    yaourt -S beid-4.0.6 ccid

Run the pcscd daemon:

    pcscd

Then if you're using chromium you'll need to do that :

    modutil -dbdir sql:.pki/nssdb/ -add "Belgium eID" -libfile /usr/lib/libbeidpkcs11.so.0 

Restart chromium and everything should work fine!

