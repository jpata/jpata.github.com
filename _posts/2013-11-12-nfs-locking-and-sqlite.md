---
layout: post
title: "NFS locking and SQLite"
description: ""
category: ""
tags: [theta, ipython, sqlite, nfs, computing]
---

Buggy NFS locking can cause problems in several applications using SQLite:

IPython
=======

Will run into an infinite loop on startup. Workaround is to run IPython as

>ipython --HistoryManager.hist_file=/tmp/ipython_hist.sqlite

theta
=====
Will compile, but throw SIGABRT exceptions, recognizable by the concise "Aborted" message. Running

> strace theta/bin/theta theta/examples/gaussoverflat.cfg

will show errors related to theta::DatabaseException

    write(2, "terminate called after throwing "..., 48) = 48
    write(2, "theta::DatabaseException", 24) = 24
    write(2, "'\n", 2)                      = 2
    write(2, "  what():  ", 11)             = 11
    write(2, "theta::DatabaseException: sqlite"..., 202) = 202
    write(2, "\n", 1)                       = 1
    rt_sigprocmask(SIG_UNBLOCK, [ABRT], NULL, 8) = 0
    tgkill(15093, 15093, SIGABRT)           = 0
    --- SIGABRT (Aborted) @ 0 (0) ---
    +++ killed by SIGABRT +++
