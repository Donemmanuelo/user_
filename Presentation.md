# Topic 3 : User Interface and Desktop 

## I- Install and Configure X11

# Introduction: 
The X Window System is a software stack that is used to display text and graphics on a screen. In other words, it’s  a windowing system that allows user to have many graphical windows interface for differents tasks. It handles display and Input devices. It includes programs that act as servers in the X11 protocol, programs that act as clients in the X11 protocol, code libraries that contain code that makes use of the X11 protocol, associated documentation, resources such as fonts and keyboard layouts that can be used with programs, libraries, etc. Historically, this software distribution was made by MIT; today it is maintained by the X.Org Foundation.

# X Windows System Architecture 
The X Window System is divided into a client and a server, and in most installations where a graphical desktop is needed both of these components are on the same computer. The client component takes the form of an application, such as a terminal emulator, a game or a web browser, etc. Each client application informs the X server about its window location and size on a computer screen. The client also handles what goes into that window, and the X server puts the requested drawing up on the screen. The X Window System also handles input from devices such as mice, keyboards, trackpads and more.

### What is a the X client ?
In simple terms, the X client is the application that runs on the local machine or remotely.

### What is the X server
We can explain the X server as the process that runs on the local machine and handle the display and input devices.


> **Usefull information**: For example, the terminal emulator on your Ubuntu system is likely using the X Window System to display the terminal interface. However, the terminal itself (e.g., GNOME Terminal, Konsole, etc.) is a separate application that runs on top of the X Window System. In other words, the X Window System provides the underlying graphics and windowing functionality, while the terminal emulator provides the user interface for interacting with the command line.

![alt text](image-4.png)


A key feature of the X Window System is that it is modular. This means that its components are not deendant on each other, allowing developers to create and integrate various extensions, windows manager, and desktop. In this context, a windows don't refers to the OS but instead to a autonomous area on the screen taht displays graphical information such as text, image, or video.  For update or modified the framework of the X windows system, we should just add as extensions to the X server, leaving the core X11 protocol intact. Examples of Xorg libraries include: `libXrandr`, `libXcursor`, `libX11`, `libxkbfile` as well as several others, each providing extended functionality to the X server.
## Display manager ##
A **display manager** is a program that manages the login process for a user, typically running on a graphical display. Its primary function is to provide a graphical interface for users to log in to their system, manage their sessions, and interact with the X11 server. In simple words, it provides a graphical login to a system. This system can either be a local computer or a computer across a network. The display manager is launched after the computer boots and will start an X server session for the authenticated user. The display manager is also responsible for keeping the X server up and running. 
For check which display manger is using by an OS we can use this command : 
```sh
$ cat /etc/X11/default-display-manager

/usr/sbin/gdm3

```
Example display managers include :

**GDM (GNOME Display Manager)**: A display manager developed by the GNOME project, which provides a more modern and feature-rich login experience.

**KDM (KDE Display Manager)**: A display manager developed by the KDE project, which provides a similar login experience to GDM.

**XDM (X Display Manager)**: A traditional display manager that has been part of the X11 distribution for many years.

**LightDM**: A lightweight display manager that is designed to be fast and efficient.

**SDDM (Simple Desktop Display Manager)**: A display manager developed by the KDE project, which provides a simple and modern login experience.

**LXDM (Lightweight X11 Display Manager)**: A display manager developed by the LXDE project, which provides a simple and lightweight login experience.

**SLiM (Simple Login Manager)**: A lightweight display manager that provides a simple and customizable login experience.

> **Note** : The display manager is responsible for providing the graphical interface for the login process, but it does not provide the graphical interface for the desktop environment.


Each instance of a running X server has a display name to identify it. The display name contains
the following:

```shell
hostname:displaynumber.screennumber
```
The display name of a running X session is stored in the `DISPLAY` environment variable:

```sh
$ echo $DISPLAY
:0
```

> **Note** :
The X server in use is on the local system, hence there is nothing printed to the left of the colon.

The current X server session is the first as indicated by the 0 immediately following the colon.
	There is only one logical screen in use, so a screen number is not visible.
To further illustrate this concept, we can look at to this following diagram :

![alt text](image-3.png)

**(A)**
A single monitor, with a single display configuration and only one screen.

**(B)**
Configured as a single display, with two physical monitors configured as one screen.
Application windows can be moved freely between the two monitors.

**(C)**
A single display configuration (as indicated by the `:0`) however each monitor is an independent
screen. Both screens will still share the same input devices such as a keyboard and mouse,
however an application opened on screen `:0.0`can not be moved to screen `:0.1` and vice
versa.

To start an application on a specific screen, assign the screen number to the `DISPLAY`
environment variable prior to launching the application:
 
```sh
$ DISPLAY=:0.1 firefox &
```

# X Server Configuration
Traditionally, the primary configuration file that is used to configure an X server is the `/etc/X11/xorg.conf`  file. On modern Linux distributions, the X server will configure itself at runtime when the X server is started and so no xorg.conf file may exist.
The xorg.conf file is divided up into separate stanzas called sections. Each section begins with the term Section and following this term is the section name which refers to a component’s configuration. Each Section is terminated by a corresponding EndSection. 
The typical `xorg.conf` file contains the following sections:

```sh 
Section "InputClass"
Identifier "system-keyboard"
MatchIsKeyboard "on"
Option "XkbLayout" "us"
Option "XkbModel" "pc105"
EndSection
```

`XkbLayout` determines the layout of the keys on a keyboard, such as Dvorak, left
or right handed, QWERTY and language
`XkbModel` is used to define the type of
keyboard in use.

The files associated with keyboard layouts can be found within `/usr/share/X11/xkb`.

A keyboard’s layout can be modified during a running X session with the `setxkbmap` command. Here is an example of this command setting up the *Greek Polytonic* layout on a Chromebook computer:
```sh
$ setxkbmap -model chromebook -layout "gr(polytonic)"
```
To make such changes permanent,
modify the `/etc/X11/xorg.conf.d/00-keyboard.conf` file to include the settings required.
> **Note** :
The `setxkbmap` command makes use of the X Keyboard Extension (XKB). 

This is an example of the additive functionality of the X Window System through its use of extensions.
For the modern linux distributions, we can use `locatectl` for the same purpose, and it directly create the `/etc/X11/xorg.conf.d/00-keyboard.conf` configuration file.
```sh
$ localectl --no-convert set-x11-keymap "gr(polytonic)" chromebook
```
The `--no-convert` option is used here to prevent `localectl` from modifying the host’s
console keymap (*keyboard layout settings on the system*)
### Monitor
The `Monitor` section describes the physical monitor that is used and where it is connected
```sh
Section "Monitor"
      Identifier     "DP2"
      Option         "Primary" "true"
EndSection
```

### Device
The Device section describes the physical video card that is used. The section will also contain the kernel module used as the driver for the video card, along with its physical location on the motherboard.

```sh
Section "Device"
      Identifier   "Device0"
      Driver       "i915"
      BusID        "PCI:0:2:0"
EndSection
```

### Screen
The Screen section ties the Monitor and Device sections together. An example Screen section
could look like the following;
 ```sh
Section "Screen"
      Identifier "Screen0"
      Device"Device0"
      Monitor"DP2"
EndSection
```

### ServerLayout
The ServerLayout section groups all of the sections such as mouse, keyboard and screens into
one X Window System interface.
```sh
Section "ServerLayout"
    Identifier          "Layout-1"
    Screen              "Screen0" 0 0
    InputDevice         "mouse1"    "CorePointer"
    InputDevice         "system-keyboard"  "CoreKeyboard"
EndSection
```
> **Note** : 
Not all sections may be found within a configuration file. In instances where a section is missing, default values are provided by the running X server instance
instead.

User-specified configuration files also reside in `/etc/X11/xorg.conf.d/`. Configuration files provided by the distribution are located in `/usr/share/X11/xorg.conf.d/`. The configuration files located within `/etc/X11/xorg.conf.d/` are parsed prior to the `/etc/X11/xorg.conf` file if it exists on the system.
The `xdpyinfo` command is used on a computer to display information about a running X server instance. Below is sample output from the command:

```sh
$ xdpyinfo

name of display:     :0
version number:     11.0
vendor string:      The X.Org Foundation
vendor release number:      12004000
X.Org version: 1.20.4
maximum request size: 16777212 bytes
motion buffer size: 256
bitmap unit, bit order, padding:  32, LSBFirst, 32
image byte order: LSBFirst
number of supported pixmap formats:     7
supported pixmap formats:
      depth 1, bits_per_pixel 1, scanline_pad 32
      depth 4, bits_per_pixel 8, scanline_pad 32
      depth 8, bits_per_pixel 8, scanline_pad 32
      depth 15, bits_per_pixel 16, scanline_pad 32
      depth 16, bits_per_pixel 16, scanline_pad 32
      depth 24, bits_per_pixel 32, scanline_pad 32
      depth 32, bits_per_pixel 32, scanline_pad 32
keycode range: minimum 8, maximum 255
focus:   None
number of extensions:     25
      BIG-REQUESTS
      Composite
      DAMAGE
      DOUBLE-BUFFER
      DRI3
      GLX
      Generic Event Extension
      MIT-SCREEN-SAVER
      MIT-SHM
      Present
      RANDR
      RECORD
      RENDER
      SECURITY
      SHAPE
      SYNC
      X-Resource
      XC-MISC
      XFIXES
      XFree86-VidModeExtension
      XINERAMA
      XInputExtension
      XKEYBOARD
      XTEST
      XVideo
default screen number:      0
number of screens:      1


screen #0:
  dimensions:     3840x1080 pixels (1016x286 millimeters)
  resolution:   96x96 dots per inch
  depths (7):     24, 1, 4, 8, 15, 16, 32
  root window id:   0x39e
  depth of root window:     24 planes
  number of colormaps:    minimum 1, maximum 1
  default colormap:   0x25
  default number of colormap cells:     256
  preallocated pixels:      black 0, white 16777215
  options:    backing-store WHEN MAPPED,save-unders NO
  largest cursor:  3840x1080
  current input event mask:     0xda0033
  
KeyPressMask                     KeyReleaseMask           EnterWindowMask
LeaveWindowMask                  StructureNotifyMask      SubstructureNotifyMask
SubstructureRedirectMask         PropertyChangeMask       ColormapChangeMask
number of visuals:      270
```


The more relevant portions of the output are, the name of the display (which is the same as the contents of the `DISPLAY`environment variable), the versioning information of the X server in use, the number and listing of Xorg extensions in use, and further information about the screen itself.
Creating a Basic Xorg Configuration File
Even though X will create its configuration after system startup on modern Linux installations, an `xorg.conf` file can still be used. To generate a permanent `/etc/X11/xorg.conf` file, run the following command:

```sh
$ sudo Xorg -configure
```
> **NOTE** :
If there is already an X session running, you will need to specify a different
`DISPLAY` in your command, for example:

``` sh 
$ sudo Xorg :1 -configure
```

In some linux distribution we can use `X` instead of `Xorg`, as `X` is a symbolic link to `Xorg`.
An `xorg.conf.new` file will be created in your current working directory. The contents of this file
are derived from what the X server has found to be available in hardware and drivers on the local
system. To use this file, it will need to be moved to the `/etc/X11/` directory and renamed to
`xorg.conf`:

```sh
$ sudo mv xorg.conf.new /etc/X11/xorg.conf``
```

# Wayland
Wayland is the newer display protocol designed to replace the X Window System. Many modern Linux distributions are using it as their default display server. It is meant to be lighter on system resources and have a smaller installation footprint than X. The project began in 2010 and is still undergoing active development, including work from active and former X.org developers.
Most modern toolkits such Gtk+ 3 and Qt 5 have been updated to allow for rendering to either an X Window System or a computer running Wayland. Not all standalone applications have been written to support rendering in Wayland as of yet. For applications and frameworks that are still targeting the X Window System to run, the application can run within XWayland. The Xwayland system is a separate X server that runs within a Wayland client and thus renders a client window’s contents within a standalone X server instance.
Just as the X Window System uses a `DISPLAY` environment variable to keep track of screens in use, the Wayland protocol uses a `WAYLAND_DISPLAY` environment variable. Below is sample output from a system running a Wayland display:

```sh
$ echo $WAYLAND_DISPLAY

wayland-0
```
This environment variable is not available on systems running X.