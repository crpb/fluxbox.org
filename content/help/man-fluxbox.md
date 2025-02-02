---
weight: 1
---

# NAME

fluxbox - A lightweight window manager for the X Windowing System

# SYNOPSIS

**fluxbox** \[-rc *rcfile*\] \[-no-slit\] \[-no-toolbar\] \[-log
*logfile*\] \[-display *display*\] \[-screen all|*scr*,*scr*…​\]
\[-verbose\] \[-sync\]

**fluxbox** \[-v | -version\] | \[-h | -help\] | \[-i | -info\] |
\[-list-commands\]

# DESCRIPTION

**fluxbox(1)** is a window manager. As such it provides configurable
window decorations, a root menu to launch applications and a toolbar
that shows the current workspace name, a set of application names and
the current time. There is also a workspace menu to add or remove
workspaces.

Fluxbox can iconify (or minimize) windows to the toolbar One click and
they reappear. A double-click on the titlebar of the window will *shade*
it; i.e. the window will disappear, and only the titlebar will remain
visible.

There are also two areas commonly used by small applets: the “slit” can
be used to dock small applications; e.g. most of the “bbtools” and
“Window Maker dockapps” can use the slit, and the “systray” which lives
in the toolbar supports standard system tray icons provided by some
applications.

Fluxbox uses its own graphics class to render its images on the fly. By
using style files, you can determine in great detail how your desktop
looks. fluxbox styles are compatible with those of Blackbox 0.65 or
earlier versions, so users migrating can still use their current
favourite themes.

Most of the default keyboard and mouse button actions mentioned in this
manual can be changed and configured in the “keys” file. This powerful
configuration file can also be used to automate almost any action you
may want to perform, from launching applications to moving windows
around the screen. See **fluxbox-keys(5)** for details.

Fluxbox can also remember certain attributes of individual application
windows and restore these settings the next time the window opens. See
the **fluxbox-apps(5)** for details.

Fluxbox supports the majority of the Extended Window Manager Hints
(EWMH) specification, as well as numerous other Window Hinting
standards. This allows all compliant window managers to provide a common
interface to standard features used by applications and desktop
utilities.

# OPTIONS

**-display** *display*
Start fluxbox on the specified display. Programs started by fluxbox will
share the DISPLAY environment variable also.

**-h**, **-help**
Display command line options.

**-i**, **-info**
Display useful information concerning the defaults and compiled-in
options.

**-log** *logfile*
Starting fluxbox with this option will designate a file in which you
want to log events to.

**-no-slit**
Do not use the container for DockApps (aka the Slit)

**-no-toolbar**
Do not use the toolbar

**-rc** *rcfile*
Use a different config file other than the default **~/.fluxbox/init**.

**-v**, **-version**
The version of fluxbox installed.

**-screen** all|*scr*,*scr*…​
Run on specified screens only or all (by default).

**-verbose**
Print more information in process.

**-sync**
Synchronize with the X server for debugging.

**-list-commands**
Lists all available internal commands.

# STARTING FLUXBOX

**fluxbox(1)** comes with a program called **startfluxbox(1)** usually
located wherever you installed fluxbox. This script provides you with
many options and variables that can be set when starting fluxbox. To
actually call fluxbox and begin using it, you should place “exec
startfluxbox” in your **\\/.xinitrc** as the last executed command. This
is assuming that the location of **fluxbox(1)** and **startfluxbox(1)**
are in your shell’s $PATH. Also note that you may need to create the
**\\/.xinitrc** file or your setup may use **~/.xsession** instead,
depending on your X setup. Some X login managers like **gdm(1)** or
**kdm(1)** may simply provide a “Fluxbox” session for you without having
to alter any settings.

By using fluxbox -i you’ll see the defaults used by **fluxbox(1)**.
These are what fluxbox looks for upon startup. In the list of
“Defaults:” you’ll see a menu file location, this is where you can
provide a system-wide menu file for your users.

On exit or restart, fluxbox will save user defaults in the file
**~/.fluxbox/init**. Resources in this file can also be edited by hand,
see the **RESOURCES** section for more details. **fluxbox(1)** also has
many tools to edit these; look through the main menu once fluxbox has
started to find different ways of managing your session.

# USING FLUXBOX

When using fluxbox for the first time, users who are more accustomed to
full desktop environments such as KDE or Gnome may be a little surprised
by the minimal screen content. fluxbox is designed to be fast and
powerful, so it may take a bit of getting used to — however, the rewards
are worthwhile.

In this section, we’ll give a quick summary of the common things.
However, we recommend that you consult the referenced sections of this
manual to further develop your understanding of what you can do with
fluxbox.

## Root Window (Main)

Looking at the fluxbox desktop immediately after startup you’ll
generally see only one thing: the toolbar. If you right-click (mouse
button 3) somewhere on the desktop, you can access the Root Menu. A
middle-click (mouse button 2) on the desktop shows you the Workspace
Menu.

## Root Menu and Workspace Menu

From the RootMenu you can launch applications and configure fluxbox. The
WorkspaceMenu shows all windows and on which workspaces they are. See
section **MENUS** on how to customize these menus.

## Toolbar

The toolbar contains any combination of the following tools, by default
in this order:

-   **Workspace Name**: Name of the current visible workspace

-   **Workspace Arrows**: Previous/Next Workspace

-   **Iconbar**: List of windows managed by fluxbox

-   **Window Arrows**: Previous/Next Application Window

-   **System Tray**: Area for applets

-   **Clock**: Date and Time

-   **Button.&lt;name&gt;**: A generic button with customizable label
    and mouse actions

The contents and behavior of the toolbar can be configured, see the
**TOOLBAR** section for details.

## Slit

Initially you won’t be able to see the slit. It is there, but it isn’t
being used yet, which confuses some people initially. Think of it as a
dock where you can place smaller programs. If you’ve looked at any
screenshots on the official fluxbox web site, you will have noticed some
small programs on the edge of some of the screens. These were more than
likely docked programs in the slit. To learn more about the slit, we
have an entire **SLIT** section below that goes into detail about the
options you have.

## Layers

fluxbox manages the following layers (from highest to lowest):

-   Above Dock

-   Dock

-   Top

-   Normal

-   Bottom

-   Desktop

Windows on a higher layer will always appear above those on a lower one.
These layers can be used on application windows, the slit or the
toolbar. You can assign applications to a certain layer by specifying it
in the “apps” file or through the WindowMenu. We discuss the “apps” file
in **fluxbox-apps(5)**. We discuss the WindowMenu in the **MENUS**
section. We discuss layers in more detail in the **LAYERS** section.

## Focus Model

The window that has the focus is the one that receives key and mouse
events. The focus model is selectable via the Configuration menu located
in the root menu. We’ll discuss the different types of focus below in
the **FOCUS MODEL** section.

## Windows

A left-click (mouse button 1) on any part of the window’s border will
raise it. Dragging then moves the window to another part of the desktop.
A right click and drag on the border resizes the window. Dragging the
resize grips at the left and right bottom corners also will resize the
window. Middle clicking on a border or titlebar will immediately lower
the window. Right clicking on the titlebar opens the Window menu. The
commands unique to this menu are discussed in detail in the **Window
Menu** section.

## Tabs

fluxbox allows windows to be “grouped” by middle clicking and holding on
a window’s tab and dragging it onto another window. This “tabbing”
allows you to put multiple applications in one location on the desktop
and do several operations (for example, moving or resizing) to all
windows in the group. By default, tabs are located just above the
window, but they may be embedded in the titlebar or moved to other
locations on the outside of the window. Configuration is discussed in
TAB OPTIONS section.

You can also set up automatic grouping using the “apps” file. See
**GROUP SECTIONS** in **fluxbox-apps(5)** for details.

## Key Bindings

There are a number of key bindings set up by default, which can be
configured and extended to just about anything you can imagine with the
keyboard. See **fluxbox-keys(5)** for details on how to do this.

The default bindings set up by fluxbox are as follows:

Mouse clicks on the empty desktop:

-   **Left-click** (Button 1): hides all fluxbox menus

-   **Middle-click** (Button 2): shows the Workspace Menu

-   **Right-click** (Button 3): shows the Root Menu

-   **Scroll wheel** (Buttons 4 and 5): jump to the previous/next
    workspace

Mouse gestures on a window:

-   **ALT+Drag Left-click** anywhere on a window moves the window.

-   **ALT+Drag Right-click** anywhere on a window resizes the window.

-   **ALT+Middle-click** anywhere on a window lowers the current window.

Mouse gestures on a window’s titlebar:

-   **CTRL+Drag Left-click** on a window’s titlebar lets you drag to
    attach the window to another’s tab group

-   **Double Left-click** on a window’s titlebar shades the window

-   **Middle-click** on a window’s titlebar lowers the window

-   **Right-click** on a window’s titlebar pops up the **Window Menu**

Mouse gestures on the toolbar:

-   **Scroll wheel** on the toolbar cycles through windows

Keyboard bindings:

-   **ALT+Tab** / **ALT+Shift+Tab**: Cycle through windows

-   **WIN+Tab** / **WIN+Shift+Tab**: Cycle through tabs

-   **WIN+1** - **WIN+9**: Select the 1st → 9th tab in the current
    window

-   **ALT+F1**: Run **xterm(1)** to open a new terminal

-   **ALT+F2**: Run **fbrun(1)** for a small “run program” dialog

-   **ALT+F4**: Close the current window

-   **ALT+F5**: Kill the current window (like **xkill(1)**)

-   **ALT+F9**: Minimize (iconify) the current window

-   **ALT+F10**: Maximize the current window

-   **ALT+F11**: Full-screen the current window

-   **ALT+Space**: Open the **Window Menu**

-   **CTRL+ALT+Del**: Exit fluxbox (log out)

-   **CTRL+ALT+Left** / **CTRL+ALT+Right**: Go to the previous/next
    workspace

-   **WIN+Left** / **WIN+Right**: Send the current window to the
    previous/next workspace, but remain on this workspace

-   **CTRL+WIN+Left** / **CTRL+WIN+Right**: Take the current window to
    the previous/next workspace, and switch to that workspace

-   **CTRL+F1** - **CTRL+F12**: Switch to the 1st → 12th workspace

-   **WIN+F1** - **WIN+F12**: Send the current window to a specific
    workspace

-   **CTRL+WIN+F1** - **CTRL+WIN+F12**: Take the current window to a
    specific workspace

# MENUS

fluxbox provides a popup menu facility that is used by a few different
types of native menus.

When a menu is open, you can click on items with the mouse to activate
them. Some special menu items react slightly differently depending on
the mouse button you use, but normally you will want to use a left-click
(button 1).

You can also use the the keyboard arrow key to navigate, or even type
the first few letters of the item’s label to select it, and “enter” to
activate the item.

Normally activating a menu item should close the menu. You can also
right-click the title are of a menu or press “esc” to close it without
activating an item.

## Root Menu

The root menu is where you can launch commonly-used applications and
change different aspects of fluxbox by simply clicking on a menu item.
By default it is opened by a right-click on the empty area of the
desktop.

The contents of this menu can be configured, see **fluxbox-menu(5)** for
details.

The default menu, which is created by the “fluxbox-generate\_menu”
command, contains menus for installed applications, as well as a special
“Fluxbox menu” item with the items detailed below:

**Configure**
The next level under this menu is where you can set certain resources
and really begin to customize the look and feel of your desktop. See the
**Configure Menu** section below for more details.

**System Styles**
This is where the standard styles are listed. You can select one of
these by clicking on it, and it will be applied immediately. System
styles are located in **@pkgdatadir@/styles/** upon a default install.
Remember that you can confirm this with fluxbox -i.

**User Styles**
This is where your custom styles are listed. It will list any styles
from **~/.fluxbox/styles/**, which may be styles you grab from the
Internet, or your own custom styles, provided you follow the standards
described in **fluxbox-style(5)**.

**Workspace List**
This is the same as the **Workspace Menu** detailed below.

**Tools**
Listed here are different tools that you can use. You can rename your
workspace, run programs from a command line or regenerate your menu.

**Window Managers**
Allows you to switch your window manager. (Only listed if you have other
window managers/desktop environments installed.)

**Lock Screen**
Locks the screen, if a suitable locking program has been detected.

**Fluxbox Command**
A little Commandline will popup where you can enter a fluxbox command.
These commands are the same as those detailed in **fluxbox-keys(5)**.

**Reload config**
Use this to reload the fluxbox configuration files. You must do this
after editing the “keys” file, “init” file, or the current style.

**Restart**
Restart the whole darn thing. This starts a completely new fluxbox
process, rereads files and redraws all graphical elements. Running
applications will remain open, however, and restored to the same
workspaces they were previously in once fluxbox returns.

**Exit**
Exits fluxbox, which in turn either shuts down the X Window server or
returns you to the graphical login screen.

## Configuration Menu

This menu offers the opportunity to set up fluxbox. It contains many
options which can be altered manually in the “init” file, but this is an
easier and faster way to change the most common settings.

All changes take effect immediately.

**Focus Model**
Lets you configure the window focus model. For details, see **FOCUS
MODEL**, below.

**Maximize Options**
Lets you configure what happens when you maximize a window. The four
options are:

**Full Maximization**:
Normally, a maximized window will not overlap the toolbar, slit, or any
docked windows (like panels). Enabling this option allows maximized
windows to be as large as the actual screen resolution.

**Ignore Resize Increment**:
Normally, terminal windows specify a “resize increment” which mean
fluxbox will only resize the window to an even multiple of the character
size. Enabling this option will ignore this specification when
maximizing.

**Disable Moving** / **Disable Resizing**:
Normally, maximized windows can still be moved and resized. Enabling
these options prevents these behaviour.

**Tab Options**
Lets you configure the properties of tabs. Detailed in **TAB OPTIONS**,
below.

**Slit**
This menu can also be found by right-clicking the slit (if visible).
Find more information about this menu’s options in the **Slit Menu**
section, below.

**Toolbar**
This menu can also be found by right-clicking any non-icon part of the
toolbar. Find more information about this menu’s options in the
**Toolbar Menu** section, below.

**Transparency**
This sets the default transparency for a focused windows, unfocused
window and the menu. Use the left mouse button to decrease and the right
mouse button to increase the value. 0 is invisible, 255 is not
transparent at all.

The transparency of individual application windows can be overridden in
the “apps” file (**fluxbox-apps(5)**).

The **Force Pseudo Transparency** option will force fluxbox to ignore
the xcomposite extension and use pseudo-transparency instead of true
transparency. Note: When pseudo-transparency is on, the transparency
values here only affect titlebars, not window contents.

**Opaque Window Moving**
If enabled, you will see the window content while dragging it. Otherwise
only an outline of the window will be shown.

**Opaque Window Resizing**
If enabled, you will see the window content while resizing it. Otherwise
only an outline of the window will be shown.

**Workspace Warping**
If enabled, you can drag windows from one workspace to another. There
are parameters to set independently whether this warping happens
horizontally and/or vertically, and in each direction you can set the
number of workspaces to jump when warping (to allow for a virtual
rectangular grid of workspaces). When warping, lower-numbered workspaces
are above/to the left, and higher-numbered workspaces below/to the
right.

## Window Menu

The Window menu is displayed when you right click on the titlebar of a
window.

To customize this menu, see the **WINDOW MENU** section of
**fluxbox-menu(5)**.

By default, this menu contains:

**Shade**
Shade the window (display the titlebar only).

**Stick**
(Un)Stick window. A “stuck” window will always be displayed on all
workspaces.

**Send To…​**
Send window to another workspace. When you select the workspace with a
middle click, fluxbox will send you along with the application to the
selected workspace.

**Maximize**
(Un)Maximize window. Depending on your toolbar and slit configuration,
maximize may cover them. You can use the different mouse buttons for
different aspects of maximize function.

-   Button 1 (Un)Maximize as normal.

-   Button 2 (Un)Maximize window vertically.

-   Button 3 (Un)Maximize window horizontally.

**Iconify**
Iconify (or minimize) a window. The “icon” can be found in the Icons
submenu of the workspace menu as well as in the toolbar (if a Toolbar
mode showing Icons is selected).

**Raise**
Raise the window above all others in the same layer.

**Lower**
Lower the window below all others in the same layer.

**Layer…​**
Change the layer of this window. See **LAYERS** for more details.

**Transparency**
Change this window’s transparency, overriding the defaults from the
**Configuration Menu**.

**Remember…​**
Specify which window settings should be stored in the “apps” file and
resumed the next time this window is opened.

Specifically the setting you may store are:

**Workpace:**
Open this in the same workspace as where the window currently resides.

**Jump to workspace:**
When **Workspace** is selected, fluxbox will jump to the appropriate
workspace when this window is opened there. If not selected, the window
will open in the background.

**Head**:
For xinerama users only, start this window on the current head (or
screen).

**Dimensions**:
Record the current window height and width.

**Position**:
Record the current X and Y coordinates of the window.

**Sticky**:
Record whether the window is on all desktops, or not.

**Decorations**:
Record the current set of decorations (title bar, grips, tabs, etc) on
the window.

**Shaded**:
Record whether the window is shaded (or rolled-up) or not.

**Minimized**:
Record whether the window is iconified (or minimized) or not.

**Maximized**:
Record whether the window is maximized or not.

**Fullscreen**:
Record whether the window is in fullscreen mode or not.

**Transparency**:
Record the current **Transparency** settings.

**Layer**:
Record the current layer.

**Save on close**:
If selected, any of the above items which are also selected will be
updated with the window’s current values as it is closed.

These are is covered in more detail in **fluxbox-apps(5)**.

**Close**
Close the application softly.

**Kill**
Kill the window’s parent process, like **xkill(1)**.

## Workspace Menu

The workspace menu can be found, by default, by middle-clicking on the
background. This menu contains entries to explore the currently defined
workspaces, windows, and add/remove/rename workspaces.

**Icons**
This menu shows any iconified (or, minimized) windows. Clicking on a
window in this menu will raise it on the current workspace.

*Workspaces*
The next section provides one submenu per workspace. Middle-clicking on
a workspace name will take you to that workspace. The submenu contains a
list of all open windows on that workspace. Clicking on a window name
will take you to that window and raise it, changing the active workspace
if necessary.

**New Workspace**
This entry adds a new workspace to the end of the list of current
workspaces.

**Edit current workspace name**
Pops up a dialog to enter a new name for the current workspace.

**Remove Last**
Remove the last workspace in the list. Any windows currently open there
will be sent to the next-to-last workspace.

# TOOLBAR

The toolbar is a small area to display information like a clock,
workspace name, a system tray or a taskbar (iconbar) that can contain
the running programs. The color, look, font etc. is defined in the
**STYLE**.

The tools in the toolbar can be enabled/disabled in the “init” file with
the **session.screen0.toolbar.tools** resource. See the **RESOURCES**
section for details on how to alter this value.

The possible tools are:

**Clock**
This will show an area to display a clock and the date according to the
format specification listed in "man strtftime"

**Button.&lt;name&gt;**
This displays a clickable label with custom text.

**Iconbar**
This is the area that contains all windows (all running applications,
all minimized windows or maybe no window, all depending on the Toolbar
Settings).

**Systemtray**
The Systemtray can hold applications that are made to use it.

**WorkspaceName**
This displays the name of the current workspace. Also, one is able to
switch to the workspace left of the current one with a left click and to
the workspace right of the current one with a right click.

**PrevWorkspace**
This displays an arrow that allows one to switch to the workspace left
of the current one.

**NextWorkspace**
This displays an arrow that allows one to switch to the workspace right
of the current one.

**PrevWindow**
This displays an arrow that switches focus to the previous visible
window on the current workspace.

**NextWindow**
This displays an arrow that switches focus to the next visible window on
the current workspace.

Other aspects of the toolbar can be configured in two ways: through the
toolbar menu, which is accessible in the Configuration part of the
RootMenu or with a middle click on the edge the toolbar, or by editing
the init file (see the **RESOURCES** section for more information about
that).

## Toolbar Menu

This menu can be opened by right-clicking on the toolbar (though not on
a window’s name in the iconbar), or from the **Configuration Menu**.

All changes take effect immediately. Here are the settings:

**Visible**
Sets the toolbar either to visible or invisible.

**Auto hide**
If this is enabled the toolbar will disappear after a defined time when
the mouse pointer leaves the toolbar. It will slide in when the cursor
hits the remaining edge of the toolbar. See the
**session.autoRaiseDelay** resource for the delay time.

**Auto raise**
If this is enabled the toolbar will elevate after a defined time when
the mouse pointer enters the it. It will fall back when the cursor
leaves the toolbar. See the **session.autoRaiseDelay** resource for the
delay time.

**Toolbar width percentage**
Sets the width of the toolbar in a percentage of your total screen size.
Use the left mouse button to decrease and the right mouse-button to
increase the value. The value can be from 1-100.

**Maximize Over**
Enabling this option will allow windows to maximize over the toolbar.
With this switched on they will only expand to the edge of the bar. This
option may be overridden by the “Full Maximization” from the
**Configuration Menu**. If that option is enabled, this option will have
no effect..

**Layer…​**
This sets the layer on which the toolbar is set. With this you can set
the toolbar to "Always on top".

**Placement**
Sets the toolbar to any edge of the screen, either centered or aligned
with a corner.

**Alpha**
This sets the alpha value for the toolbar. Use the left mouse button to
decrease and the right mouse button to increase the value. 0 is
invisible, 255 is not transparent at all.

**Iconbar Mode**
Specifies various modes of the iconbar’s operation.

The first section outlines what types of windows will be shown in the
iconbar:

**None**:
Will not show any windows

**Icons**:
Shows windows from all workspaces that are iconified (or, minimized)

**NoIcons**:
Shows windows from all workspaces that are not iconified

**WorkspaceIcons**:
Shows windows from the current workspace that are iconified

**WorkspaceNoIcons**:
Shows windows from the current workspace that are not iconified

**Workspace**:
Shows all windows (iconified or not) from the current workspace

**All Windows**:
Shows all windows (iconified or not) from all workspaces

The next section specifies the alignment of the window names shown in
the iconbar. The width is specified via the
**session.screen0.iconbar.iconWidth** resource:

**Left**:
All icons will be left-aligned with the width set in the “init” file

**Relative**:
All icons will be sized evenly to fill the iconbar completely

**RelativeSmart**:
All icons will initially be sized evenly, but icons with long titles
will be larger

**Right**:
All icons will be right-aligned with the width set in the “init” file

The last option in this submenu is:

**Show Pictures**:
If enabled the iconbar will show the application’s icon (if provided by
the application)

**Clock**
Lets you switch between the 00:00am - 11:59pm and 00:00 - 23:59 notation

**Edit Clock Format**
clicking this entry will pop up a dialog window in which the clock
format can be set according to *man strftime* (or *man date*).

# FOCUS MODEL

The Focus Model defines how windows gain focus (i.e. become the active
window, which receives keyboard and mouse events). The focus model can
be changed in the configuration menu (usually located under *fluxbox
menu* in the Root Menu.

There are two main aspects of the focus model: how windows gain focus
and how tabs gain focus. Each of these has two options: focus follows
mouse and click to focus. Focus follows mouse means that windows will
gain focus when the mouse hovers over them. Click to focus means that
windows will gain focus when the mouse clicks on them.

Thus, there are four main options when choosing a focus model. You
should choose one of the first two and one of the last two. They are:

**Click To Focus**
Click to focus windows.

**Mouse Focus**
Window focus follows mouse.

**Mouse Focus (Strict)**
Like Mouse Focus, but no mouse movement is required, ie. the window is
also focused if it moves below the mouse, eg. because it shows up or you
change the virtual desktop.

**ClickTabFocus**
Click to focus tabs.

**MouseTabFocus**
Tab focus follows mouse.

There are three more settings in the “Focus Model” menu:

**Focus New Windows**
If enabled, a new window will grab X focus as soon as it is opened.

**Auto Raise**
If enabled, focusing on a new window will automatically raise that
window above all others within its layer. When disabled, you must
explicitly raise a focused window using the window menu, keybinding, or
**Click Raises**.

**Click Raises**
If enabled, clicking anywhere on a window will raise it above all others
within its layer.

# TAB OPTIONS

This section of fluxbox configuration menu lets you configure many
features of tabs. Inside of it there are three main options:

**Placement**
You can choose where the external tabs will be positioned relative to
the window. For these options to work, *Tabs in Titlebar* must be off.

**Tabs in Titlebar**
When this option is on, tabs are fixed in window titlebar and the width
varies according to the amount of windows grouped.

**Maximize Over**
When this option is on, maximizing a window will disregard the size and
location of external tabs, which means they may be pushed out of the
screen entirely.

**External Tab Width**
This specifies in pixels the width of external tabs.

# STYLES

fluxbox enables you to use specialized files that contain **X(1)**
resources to specify colors, textures, pixmaps and fonts, and thus the
overall look of your window borders, menus and the toolbar.

The default installation of fluxbox provides some of these style files.
See **fluxbox-style(5)** to accommodate the growing number of style
components.

## Style Overlay

In addition to the style file, the overlay file, whose location is
specified by **session.screen0.styleOverlay** (default:
**~/.fluxbox/overlay**) can be used to set style resources that override
all styles. For more information about which parts of fluxbox can be
controlled by the overlay file, see **fluxbox-style(5)**.

# THE SLIT

The slit is a special fluxbox window frame that can contain dockable
applications, such as “bbtools” or “window maker dockapps”.

When applications are run in the slit they have no window borders of
their own; instead they are framed in the slit, and they are always
visible in the current workspace.

Most dockable applications use the -w option to run in the slit. For
example, you could put in your **~/.fluxbox/startup**:

    bbmail -w &
    bbpager -w &
    wmdrawer &
    exec fluxbox

To use the slit you must have it compiled into fluxbox. This is the
default setting.

## Slit Menu

This menu can be opened by right-clicking on the slit (though not on an
application running within the slit), or from the **Configuration
Menu**.

All changes take effect immediately. Here are the settings:

**Placement**
This lets you set the position of the slit.

**Layer**
See **LAYERS** for details on the layer order.

**Auto hide**
If this is enabled the slit will disappear after a defined time when the
mouse pointer leaves the slit. It will slide in when the cursor hits the
remaining edge of the slit. See the **session.autoRaiseDelay** resource
for the delay time.

**Auto raise**
If this is enabled the slit will elevate after a defined time when the
mouse pointer enters the it. It will fall back when the cursor leaves
the slit. See the **session.autoRaiseDelay** resource for the delay
time.

**Maximize Over**
Enabling this option will allow windows to maximizing over the slit.
With this switched off they will only expand to the edge of the slit.
This option may be overridden by the “Full Maximization” from the
**Configuration Menu**. If that option is enabled, this option will have
no effect..

**Alpha**
This sets the alpha value for the slit. Use the left mouse button to
decrease and the right mouse button to increase the value. 0 is
invisible, 255 is not transparent at all.

**Clients**
This submenu lets you reorder the the applications running in the slit.
You are able to hide apps from the slit by unselecting them in the list
showing. This will not kill the app. You can make them re-appear by
selecting them in the list. The "Save SlitList" option saves the new
order to you slitlist located in **~/.fluxbox/slitlist**. See the next
section for details.

## Slitlist File

fluxbox’s slitlist file is available for those that use dockapps in the
slit. This file helps fluxbox keep track of the **order** of the
dockapps when in the slit. The file is generally located at
**~/.fluxbox/slitlist**.

A simple procedure for getting the slit sequences the way you like it
is: 1. Run fluxbox with no pre-loaded dockapps 2. Run dockapps
individually in the order you want them 3. Add dockapps to your
**startfluxbox(1)** script

This sequence will be saved by default to **~/.fluxbox/slitlist** and
will be remembered for future instances of fluxbox.

Users are free to manually edit the slitlist file. It is a simple list
of window names, as given by **xprop(1)**, one per dockapp. Similar to
the init file it should not be edited while fluxbox is running.
Otherwise changes may get overwritten.

The user also has the option of choosing a different path for the
slitlist file, by setting the **session.session0.slitlistFile**
resource.

# LAYERS

Layers affect the way that windows will overlap each other on the
screen. Windows on a higher layer will always appear above those on a
lower one, whether they are focused or not. Fluxbox uses 13 layers,
starting from 1 (highest).

There are two ways to assign a window to a different layer. When the
window is open, you may select the layer in the “Layer …​” submenu of the
window menu. The menu gives six choices for the layer, which fluxbox
manages by name. The names are (from highest to lowest layer):

-   2 - Above Dock

-   4 - Dock

-   6 - Top

-   8 - Normal

-   10 - Bottom

-   12 - Desktop

The other way to set the layer for a window is through the “apps” file.
This method is described in **fluxbox-apps(5)**.

# RESOURCES

Usually the **~/.fluxbox/init** resource file is created and maintained
by fluxbox itself. You can use the **Configure Menu**, mentioned above,
to set most of these options. However, we’ll cover all of the resource
options that are available to the user. If you edit this file while
fluxbox is running, you must “reconfigure” to reload the resource
options.

When running fluxbox in a multiple-screen environment the screen0 key
can also be screen1, screen2, to customize the behavior of fluxbox on
each desktop accordingly. Here are the resources that are currently
available:

**session.screen0.window.{focus|unfocus}.alpha**: *integer*
These resources are available to the user to set different levels of
transparency for different components of fluxbox. Each one accepts a
value between 0-255, 255 being opaque and 0 being completely
transparent.

Default: **255**

**session.screen0.{slit|toolbar}.autoHide**: *boolean*
The autoHide resources allow the user to set the behavior of the toolbar
and slit. This behavior can be that they disappear when they are not
being used actively by the user, or they remain visible at all times.

Default: **False**

**session.screen0.{slit|toolbar}.autoRaise**: *boolean*
If enabled, the respective item will elevate to the AboveDock layer when
entered and fall back to its regular layer when left. Notice that this
does **not** implicitly alter the items regular layer or the workspace
padding, ie. if the item is already set to AboveDock this does nothing
and if a mximized window completely covers the item you won’t be able to
enter, thus elevate it.

Default: **False**

**session.screen0.{slit|toolbar}.layer**: *layer*
With these two resources, you can set the layer you want the toolbar and
the slit to appear on. Please read the LAYER section for more
information.

Default: **Dock**

**session.screen0.{slit|toolbar}.placement**: *placement*
These allow users to place the slit and toolbar where they like.

Possible options are:
**BottomLeft BottomCenter BottomRight LeftBottom LeftCenter LeftTop
RightBottom RightCenter RightTop TopLeft TopCenter TopRight**

Slit default: **RightBottom**

Toolbar default: **BottomCenter**

**session.screen0.{slit|toolbar|tabs}.maxOver**: *boolean*
Setting these to True will allow application windows to maximize over
the complete screen. Setting to False allows the slit, toolbar, and
external tabs to hold their territory and will always be visible when an
application is maximized.

Default: **False**

**session.screen0.toolbar.height**: *integer*
Set the height of the toolbar. If the value is set to 0, the style file
will gain control over the toolbar height. It is possible to set a fixed
height by changing this value to something greater than 0.

Default: **0**

**session.screen0.toolbar.visible**: *boolean*
The user can set whether they want to have a toolbar on screen at all.
Setting to False removes the toolbar from the screen.

Default: **True**

**session.screen0.toolbar.widthPercent**: *integer*
This resource sets the width percentage of the toolbar on the screen.

Default: **100**

**session.screen0.toolbar.tools**: *tools*
This resource specifies the tools plugged into the toolbar. Read the
TOOLBAR section in this manual for a description of each of these. They
may be specified in any order, delimited by the **,** character. They
will appear in the order given.

Possible tools:
**clock iconbar nextwindow prevwindow nextworkspace prevworkspace
systemtray workspacename button.&lt;name&gt;**

Default:
**workspacename, prevworkspace, nextworkspace, iconbar, prevwindow,
nextwindow, systemtray, clock**

**session.screen0.{slit|toolbar}.onhead**: *integer*
For those that use xinerama, users can set this value to the number of
the head where they would like to see the slit and toolbar, starting
from 1. Setting this to 0 will ignore xinerama information.

Default: **0** for slit, **1** for toolbar

**session.screen0.iconbar.mode**: *pattern*
This determines which windows will be displayed in the iconbar. Any
window pattern is acceptable. See the section **CLIENT PATTERNS** in
either **fluxbox-keys(5)** or **fluxbox-apps(5)** for details.

Default: **{static groups} (workspace)**

**session.screen0.iconbar.usePixmap**: *boolean*
This is also set in the Iconbar Mode menu. When set to True, this will
show the native icon of applications.

Default: **True**

**session.screen0.iconbar.iconTextPadding**: *integer*
This specifies the space between the window title and the edge of the
button.

Default: **10**

**session.screen0.iconbar.alignment**: *position*
This value should be changed in the Iconbar Mode menu.

**session.screen0.iconbar.iconifiedPattern**: *string*
Allows to decorate the title of iconified (minimized) windows. The title
is represented by "%t".

Default: **( %t )**

<!-- -->

Available options:
-   **Left**: Fixed width, aligned left

-   **Relative**: Width varies to fill the iconbar

-   **Right**: Fixed width, aligned right

\+ Default: **Relative**

**session.screen0.iconbar.iconWidth**: *integer*
Used to specify the iconbar button width for Left/Right alignment.

Default: **128**

**session.screen0.strftimeFormat**: *date*
This adjusts the way the current time is displayed in the toolbar. The
**strftime(3)** format is used.

Default: **%k:%M**

**session.screen0.tabs.intitlebar**: *boolean*
This specifies whether tabs should be embedded in the titlebar or placed
outside the window.

Default: **True**

**session.screen0.tab.placement**: *placement*
This specifies where external tabs will appear on the window. It has the
same possible values as **sesion.screen0.{slit|toolbar}.placement**.

Default: **TopLeft**

**session.screen0.tab.width**: *integer*
This specifies the width of external tabs in pixels.

Default: **64**

**session.screen0.focusModel**: **ClickToFocus|MouseFocus|StrictMouseFocus**
This controls how windows gain focus via the mouse. With “ClickToFocus”,
the user must click on the window. With “MouseFocus”, windows gain focus
whenever the mouse moves over them, but only when the mouse is moving.
With “StrictMouseFocus”, windows gain focus whenever the mouse enters
any exposed area, even if this is due to layer changes, window movement,
changing desktops, closing windows, etc.

Default: **ClickToFocus**

**session.screen0.autoRaise**: *boolean*
When True, this setting automatically raises any window that gains
focus.

Default: **True**

**session.autoRaiseDelay**: *integer*
Adjusts the delay (in milli-sec) before focused windows will raise when
using the Autoraise option.

Default: **250**

**session.screen0.clickRaises**: *boolean*
This setting allows a user to click anywhere on a window to bring it on
top of other windows. Otherwise, only the titlebar will work.

Default: **True**

**session.screen0.workspacewarping**: *boolean*
This setting enables a user to change workspaces by dragging a window
across the edge of the screen.

Default: **True**

**session.screen0.showwindowposition**: *boolean*
Setting this resource to True shows the user, in a little window, the
exact position of the application window while the user is dragging it.
Allows a precise placement of windows on a screen.

Default: **False**

**session.screen0.defaultDeco**: *string*
This specifies the default window decorations, according to the same
options available to the **\[Deco\]** option in the “apps” file,
described in **fluxbox-apps(5)**.

Default: **NORMAL**

**session.screen0.menuDelay**: *integer*
This sets the delay in milliseconds for submenus to open when you hover
over them or to close when you hover over another item.

Default: **200**

**session.screen0.focusNewWindows**: *boolean*
This sets whether or not new windows will become focused automatically.

Default: **True**

**session.screen0.workspaceNames**: *names*
Here is where the user can name their workspaces, in a comma-delimited
list. However it is recommended to use the tool available in the
Workspace Menu to set these.

Default: **Workspace 1, Workspace 2, Workspace 3, Workspace 4**

**session.screen0.edgeSnapThreshold**: *integer*
When moving a window across your screen, fluxbox is able to have it
“snap” to the edges of the screen and other windows for easy placement.
This variable tells fluxbox the distance (in pixels) at which the window
will jump to the edge.

Default: **10**

**session.screen0.edgeResizeSnapThreshold**: *integer*
When resizing a window by grabbing a corner, fluxbox is able to have it
“snap” to the edges of the screen and other windows for easy placement.
This variable tells fluxbox the distance (in pixels) at which the window
will jump to the edge.

Default: **0**

**session.screen0.windowPlacement**: *strategy*
This resource specifies where to place new windows when not otherwise
specified (by the program or the “apps” file, for example).

Available strategies:
-   RowSmartPlacement: tries to place windows in rows without
    overlapping

-   ColSmartPlacement: tries to place windows in columns without
    overlapping

-   CascadePlacement: places windows below the titlebar of the previous
    one

-   UnderMousePlacement: places new windows underneath the mouse

-   RowMinOverlapPlacement: place windows in rows with minimal
    overlapping

-   ColMinOverlapPlacement: place windows in columns with minimal
    overlapping

-   AutotabPlacement: tabs the window to the currently focused one

Default: **RowSmartPlacement**

**session.screen0.rowPlacementDirection**: **LeftToRight**|**RightToLeft**
These settings control the direction in which windows are tiled using
the RowSmartPlacement and ColSmartPlacement strategies described above.

Default: **LeftToRight**

**session.screen0.colPlacementDirection**: **TopToBottom**|**BottomToTop**
These settings control the direction in which windows are tiled using
the RowSmartPlacement and ColSmartPlacement strategies described above.

Default: **TopToBottom**

**session.screen0.fullMaximization**: *boolean*
If this setting is enabled, windows will maximize over the toolbar,
slit, and any other window that creates a strut, no matter what their
individual settings are.

Default: **False**

**session.screen0.opaqueMove**: *boolean*
When moving a window, setting this to True will draw the window contents
as it moves (this is nasty on slow systems). If False, it will only draw
an outline of the window border.

Default: **True**

**session.screen0.opaqueResize**: *boolean*
When resizing a window, setting this to True will draw the window
contents as it resizes (this is nasty on slow systems). If False, it
will only draw an outline of the window border.

Default: **False**

**session.screen0.opaqueResizeDelay**: *integer*
When resizing a window in opaque mode, this controls the resize clock
pulse in ms. Low values resize "smoother" but slow clients (browser etc.
which are expensive to resize) can put too much stress on the system
(stalling everything) High values will cause notable latency (delay
before the size is aligned to the mouse position)

Default: **40**

**session.screen0.workspaces**: *integer*
Set this to the number of workspaces the users wants.

Default: **4**

**session.screen0.struts**: *integer*, *integer*, *integer*, *integer*
Shrink the workspace by left, right, top, bottom pixels (positive
integers) This allows you to add some padding to the workspace eg. to
keep a fraction of the desktop visible against maximized windows.
session.screen0.struts.&lt;n&gt; allows to control this for individual
heads (&lt;n&gt; starts counting at 1)

Default: **0,0,0,0**

**session.screen0.toolbar.button.&lt;name&gt;.label**: *string*
The label text for the toolbar button tool "button.&lt;name&gt;"

Default: **blank**

**session.screen0.toolbar.button.&lt;name&gt;.commands**: *string*:'string':'string':'string':'string'
A colon delimited list of commands, executed when the respective mouse
button is pressed on the toolbar button tool "button.&lt;name&gt;" The
commands are the same as those detailed in **fluxbox-keys(5)**.

Default: **blank**

**session.cacheLife**: *minutes*
This tells fluxbox how long unused pixmaps may stay in the X server’s
memory.

Default: **5**

**session.cacheMax**: *KbSize*
This tells fluxbox how much memory it may use to store cached pixmaps on
the X server. If your machine runs short of memory, you may lower this
value.

Default: **200**

**session.colorsPerChannel**: *integer*
This tells fluxbox how many colors to take from the X server on
pseudo-color displays. A channel would be red, green, or blue. fluxbox
will allocate this variable ^ 3 and make them always available. Value
must be between 2-6. When you run fluxbox on an 8bpp display, you must
set this resource to 4.

Default: **4**

**session.doubleClickInterval**: *integer*
Adjust the delay in milliseconds between mouse clicks for fluxbox to
consider a double click.

Default: **250**

**session.forcePseudoTransparency**: *boolean*
If you have Xorg’s composite extension enabled, this setting will force
the menu, windows, toolbar, and slit to use pseudo-transparency instead
of true transparency.

Default: **False**

**session.ignoreBorder**: *boolean*
This configures the ability to move windows by dragging the border.

Default: **False**

**session.tabPadding**: *integer*
This specifies the spacing between tabs.

Default: **0**

**session.tabsAttachArea**: **Window|Titlebar**
With this set to “Window”, windows may be grouped by dragging one tab
with the middle mouse button and dropping it anywhere on another window.
With “Titlebar”, the user must drop the tab on the target window’s
titlebar.

Default: **Window**

**session.titlebar.{left|right}**: *buttons*
The buttons or icons to place in the titlebar of decorated windows. You
may specify any number, space-delimited.

The available options are:
**Close Maximize MenuIcon Minimize Shade Stick LHalf RHalf**

Default left: **Stick**

Default right: **Shade Minimize Maximize Close**

*LHalf* and *RHalf* are buttons to quickly place a window into the left
and right half of the current monitor.

**session.screen0.pin{Left|Right}**: *classes*
Sort the system tray icons according to order specified in *classes*,
which is a comma-separated list of CLASSCLASS properties of the X
clients (The second field of WM\_CLASS from the output of the
**xprop(1)** utility).

Consider a system tray "A C B D E F". With pinRight set to "A, B" and
pinLeft set to "E, F" it will look like "E F \[C D\] A B" while the
icons in \[\] are unordered as usual.

All of the *location* resources following require a pathname to their
specific files. This is where you can specify different files. Most of
the defaults will be located in the user’s **~/.fluxbox** directory.

**session.appsFile**: *location*
Location of persistent application settings, or the “apps” file. See the
**Remember…​** item in the **Window Menu** section above or
**fluxbox-apps(5)** for details.

**session.groupFile**: *location*
Deprecated, auto-grouping is now done in the “apps” file, see
**fluxbox-apps(5)** for details.

**session.keyFile**: *location*
Location of the keyboard mapping settings, or the “keys” file. See
**fluxbox-keys(5)** for details.

**session.menuFile**: *location*
Location of the Root Menu file. See **fluxbox-menu(5)** for details.

**session.slitlistFile**: *location*
Location of the file used to remember slit client ordering. See **SLIT**
above for details.

**session.styleFile**: *location*
Location of the currently selected style. See **fluxbox-style(5)** for
details.

**session.styleOverlay**: *location*
Location of the style overlay file. See **fluxbox-style(5)** for
details.

**session.screen0.windowMenu**: *location*
This optionally specifies the location of a user-defined window menu. If
left blank, it will use **~/.fluxbox/windowmenu**.

Default: **blank**

**session.menuSearch**: **nowhere**|**itemstart**|**somewhere**
This setting controls the way the menu search feature works.

<!-- -->

Available options:
-   nowhere: disables the menu search

-   itemstart: typed text matches at the start of a menu items

-   somewhere: typed text matches somewhere in a menu item

\+ Default: **itemstart**

# ENVIRONMENT

**HOME**
fluxbox uses **$HOME** to find the .fluxbox/init file and to resolve
style file and -directory names.

**DISPLAY**
When no other display was given on the command line, fluxbox will start
on the display specified by this variable.

fluxbox can also take advantage of other environment variables if they
are set before fluxbox is started. For example, if $TERM is set, then it
will be available whenever fluxbox uses the shell, such as the “keys”
file **ExecCommand** or the root menu’s **\[exec\]** tag. See
**fluxbox-keys(5)** and **fluxbox-menu(5)** for details.

The “keys” file also provides two commands that can alter the current
environment of fluxbox: **SetEnv** and **Export**. Any changes made by
these commands will also affect the environment as seen by fluxbox and
all child processes started after that point. See **fluxbox-keys(5)**
for details.

For more information about environment variables in general, see your
shell’s manual.

# SIGNALS

fluxbox responds to the following signals:

-   SIGUSR1 restarts fluxbox.

-   SIGUSR2 Forces reloading of configuration.

# AUTHORS

fluxbox is written and maintained by Henrik Kinnunen &lt;fluxgen at
fluxbox org&gt;, Simon Bowden &lt;rathnor at fluxbox org&gt;, Mathias
Gumz &lt;akira at fluxbox org&gt;, and Mark Tiefenbruck &lt;mark at
fluxbox org&gt;, with contributions and patches merged from many
individuals around the world.

Blackbox was written and maintained by Brad Hughes &lt;blackbox at alug
org&gt; and Jeff Raven &lt;jraven at psu edu&gt;.

This manpage is the combined work of:

-   Jim Ramsay &lt;i.am at jimramsay com&gt; (&gt;fluxbox-1.0.0)

-   Curt Micol &lt;asenchi at asenchi com&gt; (&gt;fluxbox-0.9.11)

-   Tobias Klausmann &lt;klausman at users sourceforge net&gt;
    (⇐fluxbox-0.9.11)

-   Grubert &lt;grubert at users sourceforge net&gt; (fluxbox)

-   Matthew Hawkins &lt;matt at mh dropbear id au&gt; (blackbox)

-   Wilbert Berendsen &lt;wbsoft at xs4all nl&gt; (blackbox)

-   Numerous other languages could be available if someone jumps in.

# ONLINE DOCUMENTATION

The Official fluxbox website: <http://www.fluxbox.org>

The Official fluxbox wiki: <http://www.fluxbox-wiki.org>

Many compatible themes: <http://tenr.de>

# BUGS

If you find any bugs, please visit the \#fluxbox irc channel on
irc.freenode.net or submit them to the bug tracker at
<http://sf.net/projects/fluxbox> . Or you may subscribe to one of the
mailinglists. More information can be found on the official website.

# SEE ALSO

fluxbox-apps(5) fluxbox-keys(5) fluxbox-style(5) fluxbox-menu(5)
fluxbox-remote(1) fbsetroot(1) fbsetbg(1) fbrun(1) startfluxbox(1)
