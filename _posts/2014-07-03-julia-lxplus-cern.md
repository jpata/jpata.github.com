---
layout: post
title: "Julia for data analysis on LXPLUS in CERN"
description: ""
category: ""
tags: [julia, computing, ipython, cern]
---

On lxplus6, installing julia is pretty easy.

You can do

{% highlight bash %}
code {
    cd public
    git clone git@github.com:JuliaLang/julia.git
    cd julia
    #disable Haswell optimization currently resulting in errors
    echo OPENBLAS_DYNAMIC_ARCH=0 > Make.user
    make -j10
    ./julia
}
{% endhighlight %}

The build takes about half an hour or so.

If all is fine, you should have a shiny new julia prompt:

    [lxplus0224:julia@master]$ ./julia
                   _
       _       _ _(_)_     |  A fresh approach to technical computing
      (_)     | (_) (_)    |  Documentation: http://docs.julialang.org
       _ _   _| |_  __ _   |  Type "help()" to list help topics
      | | | | | | |/ _` |  |
      | | |_| | | | (_| |  |  Version 0.3.0-prerelease+4029 (2014-07-03 04:30 UTC)
     _/ |\__'_|_|_|\__'_|  |  Commit a8545c0 (0 days old master)
    |__/                   |  x86_64-redhat-linux

What about installing ROOT? On lxplus, ROOT is set up by doing

{% highlight bash %}
code {
    source /afs/cern.ch/sw/lcg/external/gcc/4.7/x86_64-slc6/setup.sh
    source /afs/cern.ch/sw/lcg/app/releases/ROOT/5.34.18/x86_64-slc6-gcc47-opt/root/bin/thisroot.sh
}
{% endhighlight %}

You can install the ROOT bindings for julia by opening the julia prompt

{% highlight bash %}
code {
    ~/public/julia/julia
}
{% endhighlight %}

and entering

{% highlight python %}
code {
    Pkg.clone("https://github.com/jpata/ROOT.jl.git")
    Pkg.clone("https://github.com/jpata/Histograms.jl.git")
    Pkg.build("ROOT")
    using ROOT
}
{% endhighlight %}

Standard ROOT objects can now be created, e.g.

{% highlight python %}
code {
    h = TH1F("h", "h", int32(10), -1.0, 1.0);
    Print(h, "ALL")
}
{% endhighlight %}
