---
weight: 5
---
# NAME

fluxbox-apps - per-window attribute configuration for fluxbox(1)

# SYNOPSIS

~/.fluxbox/apps

# SYNTAX

Variable parameters are shown in emphasis: *argument*

All other characters shown are required verbatim. Whitespace is only
required to delimit words, but it is fine to add more whitespace.

# DESCRIPTION

It is possible to force an application to always have the same
dimensions, position, and other settings when it is first launched.
These settings are saved in the “apps” file.

Most simple settings can be saved using the “Remember…​” submenu of the
window menu, which can usually be opened with a right-click on the
titlebar. More advanced features require manually editing the “apps”
file. This may include using **GROUP SECTIONS** to set up automatic
window tab groups.

You do not need to “reload” fluxbox after editing the apps file, the
changes should be rescanned when the next window is opened.

The file is made up of two main types of sections, apps and groups,
detailed below.

# APP SECTIONS

**\[app\]** sections provide settings for individual application
windows.

These sections begin with a line of the format
**\[app\]** **(***pattern***)** **{***count***}**

The *pattern* can be one or more patterns which match windows. For more
details, see **CLIENT PATTERNS**. If you specify more than one
*pattern*, they must ALL match for the settings to be applied.

The **{***count***}** is optional. If specified, then the entry will
only match at most that many windows at any time. If omitted, the
default is to apply the settings to all matching windows.

This opening **\[apps\]** line is followed by any number of settings for
the application. See **SETTINGS** for more details.

Each of these sections ends with the single line
**\[end\]**

# TRANSIENT SECTIONS

**\[transient\]** sections provide settings for "dialogs".

This is the same as the **\[app\]** section, but applies to transient
windows. Transient windows have a WM\_TRANSIENT\_FOR property. This will
apply to all modal and several other dialogs which have a "leader" they
remain above. Notably, open/save dialogs fall into this category.

# GROUP SECTIONS

The primary purpose of **\[group\]** sections is to group windows
together. All windows in a group will be tabbed together automatically.

These sections begin with a line of the format
**\[group\]** **(***pattern***)**

Where the *pattern* item is optional. If specified, this pattern must
match for the group to take effect. It is common to use
non-window-specific patterns such as **(workspace)** here. See **CLIENT
PATTERNS** for more details.

This is followed by any number of **\[app\]** lines. These have a
similar format to the **\[app\]** section detailed above in **APP
SECTIONS**, but do not contain any settings and do not have an
associated **\[end\]** line.

Like this
**\[app\]** **(***pattern***)**

This section may also contain settings that are applied to every window
in the group. See the **SETTINGS** section for details.

As with **\[app\]** sections, each of these sections ends with the single line
**\[end\]**

# SETTINGS

These settings may be stored in the “apps” file. A settings line must
appear inside either an **\[app\]** or **\[group\]** section.

The general format is
**\[***setting***\]** **{***value***}**

All allowed values are described below, except for *bool* which can
simply have the value **yes** or **no**, which enables or disables the
associated setting, respectively.

**\[Workspace\]** {*number*}
Forces the application to open on the *number* workspace specified.
Workspaces are set by number, beginning with 0.

**\[Jump\]** {*bool*}
Changes the active workspace to the remembered one when the application
is opened. This is only useful when used in conjunction with
*\[Workspace\]*. See **EXAMPLES**.

**\[Head\]** {*number*}
Forces the application to open on the *number* head specified (Xinerama
only).

**\[Layer\]** {*number*}
Specify the layer to open the window on (by number). Each layer has a
number. The named ones are: 2-AboveDock, 4-Dock, 6-Top, 8-Normal,
10-Bottom, 12-Desktop.

**\[Dimensions\]** {*width\[%\]* *height\[%\]*}
Opens the application with the specified *width* and *height*, in
pixels. If the value is given in percent, then the window size will be
based on the current screen’s size.

**\[IgnoreSizeHints\]** {*bool*}
Some Applications restrict the aspect ratio, minimum or maximum size of
windows. Setting this key "yes" will make fluxbox ignore those
constraints. **NOTICE** that bad client implementations may hard depend
on these constraints (by blindly using their geometry in unsave
calculations, causing div-by-zero segfaults etc.)

**\[Position\]** (*anchor*) {*X\[%\]* *Y\[%\]*}
Position the application at a particular spot. By default the upper-left
corner is placed at screen coordinates (*X*,*Y*). If you specify an
*anchor*, say BottomRight, then the lower-right corner of the window is
positioned (*X*,*Y*) pixels from the lower-right corner of the screen.
If the value is given in percent, then the coordinates will be based on
the current screen’s size.

*anchor* may be set to one of:
**TopLeft Left BottomLeft Top Center Bottom TopRight Right BottomRight**

**\[Deco\]** {*value*}
Specify the decoration state. There are several predefined *value* sets:
**NORMAL**
Standard decorations

**NONE**
No decorations

**BORDER**
Like NONE except keep the X window border

**TAB**
Like BORDER except keep external tabs (if enabled)

**TINY**
Titlebar with only an iconify button

**TOOL**
Titlebar only

The *value* may also be a bitmask for finer-grained control. The bits
are, from (1&lt;&lt;0) to (1&lt;&lt;10): Titlebar, Handle/Grips, Border,
Iconify Button, Maximize Button, Close Button, Menu Button, Sticky
Button, Shade Button, External Tabs, Focus Enabled.

**\[Shaded\]** {*bool*}
Whether the window is Shaded (rolled-up) or not.

**\[Tab\]** {*bool*}
Whether the window has tabs enabled.

**\[FocusNewWindow\]** {*bool*}
**DEPRECATED!** Please use FocusProtection "Gain" or "Refuse" instead.
If enabled, a new window will grab X focus as soon as it is opened. If
disabled, a new window will not grab X focus as soon as it is opened.

**\[FocusProtection\]** {*value* \[,*value* \[, …​\]\] }
Comma separated list of focus controlling flags. *value* may be:
**None**
Regular behavior

**Gain**
A new window will grab X focus as soon as it is opened.

**Refuse**
A new window will not grab X focus as soon as it is opened.

**Deny**
The window is not allowed to claim focus while it is opened.

**Lock**
No window is allowed to claim the focus while this window has it.

Please notice that technically, windows may still obtain the focus which
is then however reverted by the WM. In case you’re very unlucky, a key
event may thus still go to the wrong window.

**\[FocusHidden\]** {*bool*}
If enabled, the window will not appear in *NextWindow*/*PrevWindow*
lists.

**\[IconHidden\]** {*bool*}
If enabled, the window will not appear in the icon area of the toolbar.

**\[Hidden\]** {*bool*}
A shortcut for setting both **FocusHidden** and **IconHidden** at the
same time.

**\[Sticky\]** {*bool*}
Specify if an application should be sticky (shown on all workspaces) or
not.

**\[Minimized\]** {*bool*}
Application should start minimized

**\[Maximized\]** {*value*}
Application should start maximized. *value* may be:
**yes**
Fully maximized

**horz**
Horizontally maximized

**vert**
Vertically maximized

**no**
Not maximized

**\[Fullscreen\]** {*bool*}
Application should start in fullscreen mode (fully maximized without any
decorations).

**\[Close\]** {*bool*}
Save settings on close. By default, application settings are not updated
when a window is closed.

**\[Alpha\]** {*value* \[*value*\]}
Set the alpha value for this window. If two values are given, they
correspond to the focused and unfocused transparency, respectively. One
number only will be used for both values. *value* is an integer between
0 and 255.

# CLIENT PATTERNS

A *pattern* looks like this
**(**\[*propertyname*\[!\]=\]*regexp***)** …​

Match definitions are enclosed in parentheses **(**…​**)**, and if no
*propertyname* is given then **Name** is assumed. The *regexp* can
contain any regular expression, or the special value **\[current\]**,
which matches the corresponding value of the currently focused window.
See *regex(7)* for more information on acceptable regular expressions.

*propertyname* is not case sensitive, whereas the *regexp* is.

If you specify multiple **(*pattern***) arguments, this implies an AND
condition - All specified patterns must match.

You can use **=** to test for equality or **!=** to test for inequality.

The following values are accepted for *propertyname*
**Name**
A string, corresponding to the CLASSNAME property (The first field of
WM\_CLASS from the output of the **xprop(1)** utility).

**Class**
A string, corresponding to the CLASSCLASS property (The second field of
WM\_CLASS from the output of the **xprop(1)** utility).

**Title**
A string, corresponding to the window title (WM\_NAME from
**xprop(1)**).

**Role**
A string, corresponding to the ROLE property (WM\_WINDOW\_ROLE from
**xprop(1)**).

**Transient**
Either **yes** or **no**, depending on whether the window is transient
(typically, a popup dialog) or not.

**Maximized**
Either **yes** or **no**, depending on whether the window is maximized
or not.

**MaximizedHorizontal**
Either **yes** or **no**, depending on whether the window is maximized
horizontally or not.

**MaximizedVertical**
Either **yes** or **no**, depending on whether the window is maximized
vertically or not.

**Minimized**
Either **yes** or **no**, depending on whether the window is minimized
(iconified) or not.

**Fullscreen**
Either **yes** or **no**, depending on whether the window is fullscreen
or not.

**Shaded**
Either **yes** or **no**, depending on whether the window is shaded or
not.

**Stuck**
Either **yes** or **no**, depending on whether the window is sticky (on
all workspaces) or not.

**FocusHidden**
Either **yes** or **no**, depending on whether the window has asked to
be left off the focus list (or, the alt-tab list), or not.

**IconHidden**
Either **yes** or **no**, depending on whether the window has asked to
be left off the icon list (or, the taskbar), or not.

**Urgent**
Either **yes** or **no**, depending on whether the window has the urgent
hint set.

**Workspace**
A number corresponding to the workspace number to which the window is
attached. The first workspace here is **0**. You may also use
**\[current\]** to match the currently visible workspace.

**WorkspaceName**
A string corresponding to the name of the workspace to which the window
is attached.

**Head**
The number of the display head to which the window is attached. You may
match this against the special value **\[mouse\]** which refers to the
head where the mouse pointer currently resides.

**Layer**
The string name of the window’s layer, which is one of **AboveDock**,
**Dock**, **Top**, **Normal**, **Bottom**, **Desktop**

**Screen**
The number of the currently used *screen*. If the setup of the running
xserver involves independent screens (*not Xinerama*), the $DISPLAY
environment contains something like *:0.1* or *:1.0*. The part after the
dot (*.*) is the number of the screen.

**@XPROP**
A string, corresponding to any xproperty (Use either the **xprop(1)**
utility or the *SetXProp* command to set a xproperty to a window)

**Matches any windows with the CLASSNAME of "xterm"**

    (xterm)

**Matches any windows with the same CLASSNAME as the currently focused
window**

    (Name=[current])

**Matches any windows on the same head as the mouse but on a different
layer than the currently focused window**

    (Head=[mouse]) (Layer!=[current])

**Matches any windows having a xproperty named FOO with "bar" in it**

    (@FOO=.*bar.*)

# FILES

**~/.fluxbox/apps**
This is the default location for the application settings.

# RESOURCES

**session.appsFile:** *location*
This may be set to override the location of the application settings.

# EXAMPLES

Here are some interesting and/or useful examples you can do with your
apps file.

    # Put the first two windows which end with 'term' on workspace 1
    [app] (name=.*[tT]erm) {2}
      [Workspace]   {1}
    [end]

    # Center kate with a specific size, and update these values when the window is
    # closed.
    [app] (name=kate)
      [Dimensions]  {1022 747}
      [Position]    (CENTER) {0 0}
      [Close]       {yes}
    [end]

    # When starting konqueror, jump to workspace 1 first and start it there.
    [app] (name=konqueror)
      [Workspace]   {1}
      [Jump]        {yes}
    [end]

    # start all aterm without decorations
    [app] (name=aterm)
      [Deco]        {NONE}
    [end]

    # a group with the gimp dock and toolbox
    # appears on layer 4 (bottom)
    [group]
      [app] (name=gimp) (role=gimp-dock)
      [app] (name=gimp) (role=gimp-toolbox)
      [Layer]       {4}
    [end]

# AUTHORS

-   Jim Ramsay &lt;i.am at jimramsay com&gt; (&gt;fluxbox-1.0.0)

-   Curt Micol &lt;asenchi at asenchi com&gt; (&gt;fluxbox-0.9.11)

-   Tobias Klausmann &lt;klausman at users sourceforge net&gt;
    (⇐fluxbox-0.9.11)

-   Grubert &lt;grubert at users sourceforge net&gt; (fluxbox)

-   Matthew Hawkins &lt;matt at mh dropbear id au&gt; (blackbox)

-   Wilbert Berendsen &lt;wbsoft at xs4all nl&gt; (blackbox)

# SEE ALSO

fluxbox(1) xprop(1) regex(7)
