---
weight: 5
---
A 'pattern' looks like this
**(**\['propertyname'\[!\]=\]'regexp'**)** …​

Match definitions are enclosed in parentheses **(**…​**)**, and if no
'propertyname' is given then **Name** is assumed. The 'regexp' can
contain any regular expression, or the special value **\[current\]**,
which matches the corresponding value of the currently focused window.
See 'regex(7)' for more information on acceptable regular expressions.

'propertyname' is not case sensitive, whereas the 'regexp' is.

If you specify multiple **('pattern'**) arguments, this implies an AND
condition - All specified patterns must match.

You can use **=** to test for equality or **!=** to test for inequality.

The following values are accepted for 'propertyname'
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
The number of the currently used 'screen'. If the setup of the running
xserver involves independent screens ('not Xinerama'), the $DISPLAY
environment contains something like ':0.1' or ':1.0'. The part after the
dot ('.') is the number of the screen.

**@XPROP**
A string, corresponding to any xproperty (Use either the **xprop(1)**
utility or the 'SetXProp' command to set a xproperty to a window)

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
