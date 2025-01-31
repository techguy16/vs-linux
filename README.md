# Linux.NET

**Linux.NET** is a full-featured integrated development environment (IDE) for mono using Gtk# forked from MonoDevelop

Directory organization
----------------------

There are two main directories:

 * `main`: The core Linux.NET assemblies and add-ins (all in a single
    tarball/package).
 * `extras`: Additional add-ins (each add-in has its own
    tarball/package).

Compiling
---------

If you are building from Git, make sure that you initialize the submodules
that are part of this repository by executing:
`git submodule update --init --recursive`

If you are running a parallel mono installation, make sure to run all the following steps
while having sourced your mono installation script. (source path/to/my-environment-script)
See: http://www.mono-project.com/Parallel_Mono_Environments

To compile execute:
`./configure ; make`

There are two variables you can set when running `configure`:

* The install prefix: `--prefix=/path/to/prefix`

  * To install with the rest of the assemblies, use:
  `--prefix="pkg-config --variable=prefix mono"`

* The build profile: `--profile=profile-name`

  * `stable`: builds the Linux.NET core and some stable extra add-ins.
  * `core`: builds the Linux.NET core only.
  * `all`: builds everything

**PS:** You can also create your own profile by adding a file to the profiles directory containing a list of the directories to build.

Disclaimer: Please be aware that the 'extras/JavaBinding' and 'extras/ValaBinding' packages do not currently work. When prompted or by manually selecting them during the './configure --select' step, make sure they stay deselected. (deselected by default)

Running
-------

You can run Linux.NET from the build directory by executing:
`make run`

Installing *(Optional)*
----------

You can install Linux.NET by running:
`make install`

Bear in mind that if you are installing under a custom prefix, you may need to modify your `/etc/ld.so.conf` or `LD_LIBRARY_PATH` to ensure that any required native libraries are found correctly.

*(It's possible that you need to install for your locale to be
correctly set.)*


Dependencies
------------

- [Linux](http://www.monodevelop.com/developers/building-monodevelop/#linux)

Special Environment Variables
-----------------------------

**BUILD_REVISION**

	If this environment variable exists we assume we are compiling inside wrench.
	We use this to enable raygun only for 'release' builds and not for normal
	developer builds compiled on a dev machine with 'make && make run'.


Known Problems
-----------------------------
```
"The type `GLib.IIcon' is defined in an assembly that is not referenced"
```

This happens when you accidentally installed gtk-sharp3 instead of the 2.12.x branch version.
Make sure to 'make uninstall' or otherwise remove the gtk-sharp3 version and install the older one.

xbuild may still cache a reference to assemblies that you may have accidentally installed into your mono installation,
like the gtk-sharp3 as described before. You can delete the cache in $HOME/.config/xbuild/pkgconfig-cache-2.xml



References
----------

**[MonoDevelop website](http://www.monodevelop.com)**

**[Gnome Human Interface Guidelines (HIG)](https://developer.gnome.org/hig/stable/)**

**[freedesktop.org standards](http://freedesktop.org/Standards/)**


