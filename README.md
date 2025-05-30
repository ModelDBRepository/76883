# Downloads

Topographica is currently under very active development, with many changes made daily. Developers, users who plan to modify any of the source files, and users who wish to receive frequent updates, should obtain Topographica using [CVS](http://www.nongnu.org/cvs/) (the version control system used for managing Topographica development), as detailed below.

Alternatively, installation packages are available for Linux, Windows, and Macintosh at our Sourceforge [downloads](http://sourceforge.net/project/showfiles.php?group_id=53602) page. These packages simplify the process of installation (at the cost of making it slightly more difficult to upgrade to new versions). Linux and Mac users should download the desired archive package and then follow the 'Building Topographica' instructions below; Windows users can download and run an .exe file, which will perform all the necessary steps.

## Installing using CVS

Topographica is hosted by [SourceForge.net](http://sourceforge.net/projects/topographica), which maintains the CVS repository. The essentials for using CVS at SourceForge are described below; see the [SourceForge documentation](http://sourceforge.net/docman/display_doc.php?docid=29894&group_id=1) for more details or if you have any difficulties.

To get started, first change to a directory to which you have write access with sufficient space available, i.e., about 400 megabytes as of 2/2006. There are two ways to get your own local copy of the CVS files, depending on whether or not you are an official Topographica developer. Non-developers can check out a read-only version of the repository, while developers have read/write access so that they can make changes that become a permanent part of the project repository. Please follow the appropriate set of instructions below.

### Read-only access

For read-only access from UNIX, Mac, or [Cygwin](http://www.cygwin.com/) (Windows with Unix commands installed), log in to the CVS server using the command:

```
cvs -d :pserver:anonymous@topographica.cvs.sf.net:/cvsroot/topographica login
```

When a password is requested, just press return. Then change to wherever you want the files to be stored, and use the command:

```
cvs -d :pserver:anonymous@topographica.cvs.sf.net:/cvsroot/topographica checkout -P -r LATEST_STABLE topographica
```

(where the entire command should be on a single line, even though it is broken into two lines above). This process will likely take several minutes (probably appearing to hang at certain points), as there are some extremely large files involved. The `-r LATEST_STABLE` option selects the version that has most recently been declared to pass all tests. That option can be omitted if you want the absolutely most up-to-date version, which may not always be usable due to work in progress.

In Windows without Cygwin, you can retrieve the files using [TortoiseCVS](http://www.tortoisecvs.org/) (tested 2/2006 using TortoiseCVS 1.8.25). After installing TortoiseCVS, open the Windows directory where you want the files to be located on your machine, right click, select "CVS Checkout", fill in CVSROOT as `:pserver:anonymous@topographica.cvs.sf.net:/cvsroot/topographica`, and type in `topographica` for the module name. Before clicking OK, select the "Revision" tab and select "Choose branch or tag", filling in "LATEST_STABLE" as the tag name (unless you want the latest bleeding-edge development version). When you click OK, the files should be downloaded for you (though it may take some time).

### Read/write access

For developers wanting read/write access, no login step is needed. However, you may need to tell CVS to use `ssh`, because most systems default to rsh, yet rsh is almost never supported in practice. Just type `export CVS_RSH=ssh` for `sh/bash` or `setenv CVS_RSH ssh` for csh/tcsh; you may wish to put this in your shell startup file. The checkout command is then:

```
cvs -d ':ext:uname@topographica.cvs.sf.net:/cvsroot/topographica' checkout topographica
```

where *uname* should be replaced with your SourceForge.net username. You will be asked for your SourceForge.net password. If instead you get a message about rsh timing out, you have probably forgotten to do the CVS_RSH command. The LATEST_STABLE option can also be provided as above, but developers will more likely want the most up-to-date version for editing.

Windows users can use the read-only procedure described for TortoiseCVS above, replacing CVSROOT with `:ext:uname@topographica.cvs.sf.net:/cvsroot/topographica`. You will typically need to have an SSH client installed for this to work, such as [PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/).

Note that anyone interested in Topographica is welcome to join as a Topographica developer to get read/write access, so that your changes can become part of the main distribution. Just email [Jim](mailto:jbednar@inf.ed.ac.uk?subject=Request%20to%20be%20a%20Topographica%20developer) and describe what you want to do, and he'll tell you what to do from there.

### Problems with CVS?

Sometimes the SourceForge.net cvs service experiences problems. If you receive messages such as "connection closed by remote host", or the cvs connection times out, you may wish to check the SourceForge.net [status page](https://sourceforge.net/docman/display_doc.php?docid=2352&group_id=1). Be aware that this page is not always updated as fast as problems appear.

### Building Topographica

The `topographica` directory you have now checked out includes the files necessary to build Topographica on most platforms. To make the build process simpler for developers using multiple platforms, source code versions of the libraries needed are included, and are created as part of the build process. This approach makes the initial compilation time longer and the simulator directory larger, but it minimizes the changes necessary for specific platforms and operating system versions.

**Linux:**
To build Topographica under Linux, just type `make` from within the `topographica/` directory. The build process will take a while to complete (e.g. about 5-10 minutes on a 1.5GHz Pentium IV machine with a local disk). If you have PHP installed, you can also make local copies of the HTML documentation from the web site; to do so, type "make all" instead of (or after) "make". "make all" will also run the regression tests and example files, to ensure that everything is functioning properly on your system. (Note that if you do the tests on a machine without a functioning DISPLAY, such as a remote text-only session, there will be some warnings about GUI tests being skipped.)

If all goes well, a script named `topographica` will be created in the `topographica/` directory; you can use this to start Topographica as described in the [Tutorials](file:///home/morse/archive/topographica-0.9.1/doc/Tutorials/index.html). If you have problems, try adding `-k` to the `make` command, which will allow the make process to skip any components that do not build properly on your machine. Topographica is highly modular, and most functionality should be accessible even without some of those components.

**UNIX:**
Topographica is developed under Linux, but should work on other versions of UNIX as well, as long as they have standard GNU tools like make and GCC installed. Just follow the Linux instructions, replacing `make` with `gmake` if that's the name of GNU make on your system.

**Mac:**
Topographica builds only under Mac OS X or later. These instructions assume that you have an X server installed. It is also possible to build Topographica using a native (Aqua) version of Python, which looks a bit nicer, but we have not yet documented how to do that.

To install under Mac OS X 10.4 (Tiger):

1. From the Apple developer web site, download [XCode_Tool2.2](http://developer.apple.com/tools/xcode/index.html) (among other development utilities, it provides the gcc C/C++ compiler for Topographica to use).
2. Specify gcc 3.3 using: `sudo gcc_select 3.3`. The default 4.0 compiler is fine for most of the included packages, but some people have reported that SciPy (weave) does not work with gcc 4.0.
3. Download and install the [Fink](http://fink.sourceforge.net/download/) package. Also install the FinkCommander GUI, which makes finding and installing Unix software more convenient.
4. With Fink, find and install the following packages: `libpng` and `freetype219` (they provide, respectively, the PNG format handling and the matplotlib library installation required to run Topographica).
5. If you want to compile the local copy of the documentation (e.g. for online help), use Fink to get imagemagick, transfig, and m4, plus php if it's not already installed.
6. If CVS is not already installed on your Mac, find and install `cvsup` (and the associated library and client) with Fink.
7. Get, unpack, and make Topographica using CVS as described above.

Other OS X versions may require small changes to this procedure, to make sure that compatible libraries are available.

**Windows:**
Double click on setup.bat in the Topographica directory. After installation, '.ty' files are associated with Topographica. Follow the instructions below for running Topographica (from a command prompt), or double click on one of the .ty scripts in the examples directory.

Instead of using the Windows versions of the various support tools for Topographica, it should be possible to build Topographica on [Cygwin](http://www.cygwin.com/), but it may be necessary to modify some of the makefiles.

### Running Topographica

Once you have the code installed and built, go to your topographica/ directory and type e.g.:

```
./topographica -g examples/cfsom_or.ty
```

or

```
./topographica -g examples/hierarchical.ty
```

or

```
./topographica -g examples/som_retinotopy.ty
```

or

```
./topographica -g examples/lissom_oo_or.ty
```

*(Windows users should omit the initial `./`, and replace the second `/` with a backslash `\`)*
For the latter two examples, a good way to get started is to work through the [SOM](file:///home/morse/archive/topographica-0.9.1/doc/Tutorials/som_retinotopy.html) or [LISSOM](file:///home/morse/archive/topographica-0.9.1/doc/Tutorials/lissom_oo_or.html) tutorials.

### Updating Topographica

CVS users who have Topographica checked out can update to the latest stable version at any time by doing:

```
cd topographica
cvs update -d -P -r LATEST_STABLE
make all
```

If you want the very most recent version, stable or not, replace `-r LATEST_STABLE` with `-A` to force a complete update. Under TortoiseCVS in Windows, you can right click in the topographica directory and select CVS Update to get the new files.

Note that updating the external/ subdirectory sometimes takes a long time, if some of the external packages have been upgraded, and in that case "make all" can also take some time to build.

Users of Topographica who don't use CVS (having downloaded one of the archive or binary packages) can subscribe to the [topographica-announce](https://lists.sourceforge.net/lists/listinfo/topographica-announce) mailing list to hear about updates.

---

2025-05-30: Standardized to Markdown, and converted original HTML formatting to Markdown syntax.