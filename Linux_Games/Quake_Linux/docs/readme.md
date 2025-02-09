![Title](https://raw.githubusercontent.com/exohood/exohood-exogames/main/Linux_Games/Quake_Linux/client/quakeworld.bmp) 

# README for Linux QWCL
---------------------

Please refer to

http://www.quakeworld.net/

for documentation on the client that is not operating system specific.

This README covers all versions of QWCL for Linux:

Requirements for SVGALib qwcl:

- SVGALib 1.20 or later (/lib/libvga.so.1.2.10)
- libc 5.2.18 or later (5.0.9 will not work, /lib/libc.so.5.2.18)
- CD-ROM for CDAudio
- Soundcard capable of mmap'd buffers.  USSLite 3.5.4 was used to build squake
  with.  Works fine on SoundBlaster 16.
- SVGALib supported mouse (usually if it works with X, it'll work with
  squake).
- Kernel 2.0.24 or later
  - untested with 2.1 kernels, your mileage may vary

Requirements for glqwcl:

- 3DFX based card for the GLQuake version, VooDoo, VooDoo Rush or VooDoo2
at this writing.  In order to use 3DFX hardware, you must have 3DFX's
GLIDE drivers installed.  RPMs for these drivers are available at:
http://glide.xxedgexx.com/3DfxRPMS.html
- For the glX version, an OpenGL implementation that includes hardware
glX support.
- CD-ROM for CDAudio
- Soundcard capable of mmap'd buffers.  USSLite 3.5.4 was used to build squake
  with.  Works fine on SoundBlaster 16 and Gravis Ultrasound MAX.
- SVGALib compatible mouse for glquake or X11 for glquake.glx
- Kernel 2.0.24 or later
  - untested with 2.1 kernels, your mileage may vary

Requirements for X11 qwcl:

- X11R5 later, only tested with XFree86, should work with most X Servers
- libc 5.2.18 or later (5.0.9 will not work, /lib/libc.so.5.2.18)
  or glibc (libc6) for the glibc version
- CD-ROM for CDAudio
- Soundcard capable of mmap'd buffers.  USSLite 3.5.4 was used to build squake
  with.  Works fine on SoundBlaster 16 and Gravis Ultrasound MAX.
- SVGALib supported mouse (usually if it works with X, it'll work with
  squake).
- Kernel 2.0.24 or later
  - untested with 2.1 kernels, your mileage may vary

Skins Note
----------

After you get the skin files from ftp.idsoftware.com (currently, 
qw_skins.zip, qws_9652.zip and qws_9706.zip) and install them in
qw/skins, you should run the shell script 'fixskins.sh' that you can find in
the qw/skins directly distributed with this archive.

Linux qwcl will always look for lowercase file names first.

Additional notes for SVGALib QWCL
---------------------------------

Linux qwcl supports 320x200x256, the various modeX modes (320x400, 360x400, 
etc) as well as high res modes if your card is supported by SVGALib.  Use 
the Quake console command vid_describemodes to list supported modes and 
the command vid_mode <number> to change modes.

Full sound support is included.  The default sound rate is 16-bit stereo,
11KHz.  You can change this in the options section below.

Mouse works great, but SVGALib may not detect a 3-button mouse properly (it
will only use two buttons).  Check your /etc/libvga.config (or
/etc/vga/libvga.config for SlackWare users).

Additional notes for glqwcl
---------------------------

There are three different ways to execute glqwcl:

1. The binary "glqwcl" requires Mesa 3-D 2.5 or later installed and compiled
with 3DFX support (fxMesa..() function interface).  It also requires
svgalib 1.3.0 or later for keyboard/mouse input.  This binary is a console
application.  Mesa 3-D requires GLIDE to be installed.

2. The shell script "glqwcl.3dfxgl" runs the "glqwcl" binary after
preloading the lib3dfxgl.so library.  This is a port of 3DFX's Win32
OpenGL MCD (Mini Client Driver) to Linux.  It is faster than Mesa 3-D
since it was written specifically with supporting GLQuake in mind.
lib3dfxgl.so requires that GLIDE be installed.

3. The binary "glqwcl.glx" is linked against standard OpenGL libraries.
It should run on many different hardward OpenGL implementations under
Linux and X11.  This binary is an X11 application and must be run under
X11.  It will work with Mesa 3-D as a standard glX based OpenGL 
applications.  If the Mesa 3-D library is compiled with 3DFX support,
you can have Mesa 3-D support 3DFX hardware under X11 by setting the
enviroment variable "MESA_GLX_FX" to "fullscreen" for fullscreen mode
and "window" for windowed mode, eg. "export MESA_GLX_FX=fullscreen" for sh 
or "setenv MESA_GLX_FX fullscreen" for csh.

For glqwcl, you must also have SVGALib or later installed (1.3.0 or later
prefered).  glqwcl uses SVGALib for mouse and keyboard handling.

If you have gpm and/or selection running, you will have to terminate them
before running glqwcl since they will not give up the mouse when glqwcl
attempts to run.  You can kill gpm by typing 'killall gpm' as root.

You must run glqwcl as root or setuid root since it needs to access things 
such as sound, keyboard, mouse and the 3DFX video.  Future versions may not 
require root permissions.

Additional notes for X11 qwcl
-----------------------------

This is a windowed version that is generic for X11.  It runs in a window
and can be resized.  You can specify a starting window size with:
	-width <width>
	-height <height>
	-winsize <width> <height>
Default is 320x200. It works in 16bit modes, but it's slower (twice as many
bytes to copy).

No other video modes are supported (just runs windowed).  Mouse is read, but
not "grabbed" by default.  Go to the Options menu and turn on Use Mouse to grab
the mouse and use it in the game (or type "_windowed_mouse 1" at the console).

New Command Line Options for Linux Quake
----------------------------------------

-mem <mb>
Specify memory in megabytes to allocate (default is 8MB, which should be fine
for most needs).

-nostdout
Don't do any output to stdout

-mdev <device>
Mouse device, default is /dev/mouse

-mrate <speed>
Mouse baud rate, default is 1200

-cddev <device>
CD device, default is /dev/cdrom

-mode <modenum>
Use indicated video mode

-nokdb
Don't initialize keyboard

-sndbits <8 or 16>
Set sound bit sample size.  Default is 16 if supported.

-sndspeed <speed>
Set sound speed.  Usual values are 8000, 11025, 22051 and 44100.
Default is 11025.

-sndmono
Set mono sound

-sndstereo
Set stereo sound (default if supported)

Installation
------------

Boot DOS (I know, but you need it to run the Quake install program) and
install Quake from your Quake CD to a DOS parition.

Boot Linux and make a directory for Quake.  Copy everything from the DOS Quake
directory into it.  i.e.:
	(cd /dos/quake; tar cf - .) | (cd ~/quake; tar xf -)

Place qwcl into your Quake directory.  You must make it setuid root (since
Quake access stuff like direct video writes, the raw keyboard mode, CD, etc).
Quake will setuid back to the normal user as soon as it opens these files.
Make Quake suid root as follows:
	chown root qwcl
	chmod 4755 qwcl

Run qwcl.  I don't recommend running it as root, since all the saved
config.cfg files will be then owned as root.  Use your normal account, unless
you do everything as root, then your mileage will vary.

qwcl may segfault if it tries to initialize your sound card and their isn't
one.  Same with the CDROM.  If it dies, try it with -nosound and/or
-nocdaudio.  If you have a sound card it died on and you know it is
supported by USSLite (the driver that comes with the Linux kernel), let me
know and I'll take a look at it.

It should work with SCSI CDROMs, but is untested.

End Notes
---------

Linux QuakeWorld is *NOT* an officially supported product.  Mail about it
will be deleted.  Do not email id about this product.  If you are having
technical difficultly, you can email me, but make sure you have the correct
kernel, libc, svgalib and other software versions before you email me.

/// Dave 'Zoid' Kirsch
zoid@idsoftware.com
Official Quake Unix Port Administrator

Acks
----

Greg Alexander <galexand@sietch.bloomington.in.us> for initial work in SVGALib
support.
Dave Taylor <ddt@crack.com> for basic Linux support.
id Software for Quake and making me port it. :)

Lots of people on #linux, #quake for testing.

