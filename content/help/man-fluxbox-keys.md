---
weight: 3
---
# NAME

fluxbox-keys - keyboard shortcuts configuration for fluxbox(1)

# SYNOPSIS

~/.fluxbox/keys

# SYNTAX

Variable parameters are shown in emphasis: *argument*

Optional parameters are shown in square brackets: \[*argument*\]

All other characters shown are required verbatim. Whitespace is required
where shown, but it is fine to add more whitespace.

# DESCRIPTION

The keys file defines the keyboard shortcuts for *fluxbox(1)*.

You can customize fluxbox’s key handling through the ~/.fluxbox/keys
file. The file consists of lines of the basic format:

**\[*modifiers*\] *key* :'command' \[*arguments* *…​*\]**

The space between the *key* and the **:** before the *command* is
mandatory.

All modifiers and commands are case-insensitive. Some command arguments
(especially those that will be passed to the shell) are case-sensitive.
Some key names are case-sensitive.

Lines beginning with a *\#* or *!* are considered comments and are
unread by fluxbox.

You will need to “reload” fluxbox after editing the keys file so it
picks up your change.

# MODIFIERS

You can get a list of possible modifiers by calling “xmodmap -pm”. This
also shows you to which keys the modifiers are mapped, but the following
modifiers are most commonly used:

**Shift Control Mod1 Mod4**

where **Mod1** is the Alt key on the PC keyboard and **Mod4** is usually
a key branded with a familiar company logo.

There are also some special modifiers that refer to mouse button events
**OnDesktop**
The mouse cursor is over the desktop (root window), and not any window.

**OnToolbar**
The mouse cursor is over the toolbar (which is normally at the bottom of
the screen).

**OnSlit**
The mouse cursor is over the mystic slit (the thing that collects dock
type windows).

**OnWindow**
The mouse cursor is over a window.

**OnTitlebar**
The mouse cursor is over a window’s titlebar.

**OnTab**
The mouse cursor is over a tab.

**Double**
Limits this action to double-clicks only.

## Combining Modifiers

To combine two or more modifiers, just list them (space-delimited) in
any order.

# KEYS

You may specify a key by its key name (for example, **a** or **space**)
or by its numeric keycode (for example, **38** or **0xf3**).

If you don’t know the name of a key, you can run **xev(1)** in a
terminal, push the key, and see the name in the output. If you have some
"special" keys that do not produce a key name in the output of
**xev(1)**, you can just use the keycode (NOT the keysym!) in your keys
file.

Commands can also be bound to mouse events (*N* denotes the number of
the button, eg. *1* is the primary button, *4*/*5* are the wheel
buttons):

**MouseN**
The mouse button *N* is pressed down and held.

**ClickN**
The mouse button *N* is clicked (pressed and released with no movement
in between)

**MoveN**
The mouse button *N* is currently held, the bound action is triggered as
often as the mouse moves.

There are some special "keys" that let you bind events to non-keyboard
events:

**ChangeWorkspace**
Fires when the workspace changes. This can be used to change backgrounds
or do anything else you like when you switch to a new workspace. See the
**EXAMPLES** below for one idea.

Use caution with this event! For example, do NOT bind this to any action
that changes your current workspace. If you break your fluxbox with this
feature, you get to keep the pieces.

# CHAINING

Key bindings can be chained in a fashion similar to Emacs key bindings
using the syntax:

*modifiers-1* *key-1* *modifiers-2* *key-2* :'command' \[*arguments
…​*\]\*

To abort a chained command part-way through typing it, press the
&lt;ESC&gt; key.

**To Bind CTRL+C CTRL+X (Which means, press CTRL+C then CTRL+X) to quit
fluxbox**

    Control c Control x :Quit

# KEYMODES

A specific set of key mappings can be activated and de-activated
on-the-fly using what are called keymodes. The syntax to define a
mapping in a keymode is:

***keymode*: *modifiers* *key* :'command' \[*arguments* *…​*\]**

Where *keymode* is any alpha-numeric string name.

When this keymode is activated (see the **KeyMode** command below), all
bindings prefaced by that keymode name become active (and all other
keybindings will be deactivated) until the keymode changes again.

# COMMANDS

Some commands have multiple names which are shown below as
CMD1 | CMD2

Related commands have been grouped below as
CMD1 / CMD2

The commands are broken up into sections as follows
-   Mouse Commands

-   Window Commands

-   Workspace Commands

-   Menu Commands

-   Window Manager Commands

-   Special Commands

## Mouse Commands

These commands may only be bound to mouse buttons (plus modifiers), not
keystrokes. In all cases, the action finishes when the mouse button is
released.

**StartMoving**
Start dragging to move the window.

**StartResizing** \[*corner*\]
Start dragging to resize the window as if you had grabbed the window at
the specified *corner*.

By default *corner* is **BottomRight**, but may be overridden with one of:
**NearestCorner NearestEdge NearestCornerOrEdge Center TopLeft Top
TopRight Left Right BottomLeft Bottom BottomRight**

If **NearestCornerOrEdge** is specified the size of the corner can also
be specified to be the larger of one or two following numbers:
\[*pixel-size* \[*percent-size*\]\] or *percent-size*%, where
*percent-size* is the percentage of half the window width or height. If
no size is given, it defaults to 50 pixels and 30%.

**StartTabbing**
Start dragging to add this window to another’s tabgroup.

**ActivateTab**
Activates the tab underneath the mouse.

## Window Commands

These commands ordinarily affect only the currently focused window. The
**OnWindow** modifier and **ForEach** command may affect the window that
is used.

**Minimize** | **MinimizeWindow** | **Iconify**
Minimize the current window, equivalent to the window button.

**Maximize** | **MaximizeWindow**
Maximize the current window, equivalent to the window button.

**MaximizeHorizontal** / **MaximizeVertical**
Maximize the current window in one direction only, leaving the other
dimension unchanged.

**Fullscreen**
Resize the window’s content to fit the whole screen, without any window
decoration.

**Raise** / **Lower**
Reorder this window to the top or bottom of the window stack, within its
current layer. See *fluxbox(1)* for a discussion of layers.

**RaiseLayer** / **LowerLayer** \[*offset*\]
Raise the window up to the layer above, or lower it to the layer below.
See *fluxbox(1)* for a discussion of layers.

**SetLayer** *layer*
Move the window to the specified layer. *layer* should be one of
**AboveDock**, **Dock**, **Top**, **Normal**, **Bottom**, **Desktop**.
See *fluxbox(1)* for a discussion of layers.

**Close**
Close the current window, equivalent to the window button.

**Kill** | **KillWindow**
Close a window that’s not responding to **Close**, like using
**xkill(1)**.

**Shade** | **ShadeWindow**
Toggle the **shaded** state of the current window, equivalent to the
window button. A **shaded** window appears as only the title bar.

**ShadeOn** / **ShadeOff**
Set the **shaded** state of the window to On / Off.

**Stick** | **StickWindow**
Toggle the **sticky** state of the current window, equivalent to the
window button. A **sticky** window is visible on all workspaces.

**SetDecor** *decor*
Sets which window decorations will be shown. *decor* has the same format
as the “\[Deco\]” parameter in the apps file. See *fluxbox-apps(5)* for
more info.

**ToggleDecor**
Toggles the presence of the window decorations (title bar, window
buttons, and resize bar).

**NextTab** / **PrevTab**
Cycle to the next / previous tab in the current tab group.

**Tab** *number*
Cycle to the given tab in the current tab group, where **1** is the
first tab. A negative *number* counts from the end of the tab group
(**-1** is the last tab, **-2** is the next-to-last, etc.).

**MoveTabRight** / **MoveTabLeft**
Reorder the tabs in the current tab group, swapping the current tab with
the one to the right / left.

**DetachClient**
Remove the current tab from the tab group, placing it in its own window.

**ResizeTo** *width\[%\]* *height\[%\]*
Resizes the window to the given width and height. If the value is given
in percent, then the window size will be based on the current screen’s
size.

**Resize** *delta-width\[%\]* *delta-height\[%\]*
Resizes the window relative to the current width and height. If the
value is given in percent, then the window size will be based on the
current window’s size.

**ResizeHorizontal** *delta-width\[%\]* / **ResizeVertical** *delta-height\[%\]*
Resizes the window in one dimension only. If the value is given in
percent, then the window size will be based on the current window’s
size.

**MoveTo** *x\[%\]* *y\[%\]* \[*anchor*\]
Moves the window to the given coordinates, given in pixels or relatively
to the current screen size if % is specified after the value.

If either *x* or *y* is set to **\\**\*, that coordinate will be
ignored, and the movement will only take place in one dimension.

The default *anchor* is the upper left corner, but this may be overridden with one of:
**TopLeft Left BottomLeft Top Center Bottom TopRight Right BottomRight**

**Move** *delta-x* *delta-y*
Moves the window relative to its current position. Positive numbers
refer to right and down, and negative to left and up, respectively.

**MoveRight** *d* / **MoveLeft** *d* / **MoveUp** *d* / **MoveDown** *d*
Moves the window relative to its current position by the number of
pixels specified in *d*. If the number is negative, it moves in the
opposite direction.

**TakeToWorkspace** *workspace* / **SendToWorkspace** *workspace*
Sends you along with the current window to the selected workspace.
SendToWorkspace just sends the window. The first workspace is number
**1**, not 0.

**TakeToNextWorkspace** \[*offset*\] / **TakeToPrevWorkspace** \[*offset*\]
Sends you along with the current window to the next or previous
workspace. If you set *offset* to a value greater than the default of
**1**, it will move you that number of workspaces ahead or behind. If
you go beyond the end of the currently defined workspaces, it will wrap
around to the other end automatically.

**SendToNextWorkspace** \[*offset*\] / **SendToPrevWorkspace** \[*offset*\]
Identical to the "TakeTo…​" commands, but again this sends only the
window, and does not move you away from your current workspace.

**SetAlpha** \[*alpha* \[*unfocused-alpha*\]\]
Sets the alpha value of a window.

Putting a **+** or **-** in front of the value adds or subtracts from
the current value. A plain integer sets the value explicitly.

no arguments
Resets both focused and unfocused settings to default opacity.

one argument
Changes both focused and unfocused alpha settings.

two arguments
First value becomes the focused alpha, second becomes the unfocused
alpha value.

**SetHead** *number*
Moves the window to the given display head. Only available when fluxbox
has been compiled with Xinerama support.

**SendToNextHead** \[*offset*\] / **SendToPrevHead** \[*offset*\]
Sends the current window to the next/previous display head. If you
specify an *offset* greater than **1**, it will move the window that
many heads. If this takes the window beyond the total number of heads,
it will wrap around to the beginning.

**SetXProp** *PROP=value*
Sets the xproperty *PROP* of the current window to *value*. Delete the
content of *PROP* by using *PROP=*.

## Workspace Commands

These commands affect the entire workspace (or "desktop" as it is
sometimes called).

**AddWorkspace** / **RemoveLastWorkspace**
Adds or removes a workspace from the end of the list of workspaces.

**NextWorkspace** \[*n*\] / **PrevWorkspace** \[*n*\] / **RightWorkspace** \[*n*\] / **LeftWorkspace** \[*n*\]
Switch to the Next / Previous workspace. All versions accept an offset
value *n*, which defaults to **1** and refers to the number of
workspaces to move at one time. {Next,Prev}Workspace wrap around when
going past the last workspace, whereas {Right,Left}Workspace do not. The
special offset "0" will toggle the former workspace for Next- and
PrevWorkspace

**Workspace** *number*
Jumps to the given workspace *number*. The first workspace is **1**.

**NextWindow** \[{*options*}\] \[*pattern*\] / **PrevWindow** \[{*options*}\] \[*pattern*\]
Focuses the next / previous window in the focus list.

*options* is one or more of the following, space delimited:
**static**
Instead of moving in order of most-recent focus, move in order of when
the window was opened (or, the order shown in the iconbar).

**groups**
Only include the current tab in windows with multiple tabs.

If *pattern* arguments are supplied, only windows that match all the
patterns are considered - all others are skipped. See the section
**CLIENT PATTERNS** below for more information.

This pair of commands has a special side-effect when the keybinding used
has a modifier - It will temporarily raise the cycled window to the
front so you can see it, but if you continue holding down the modifier
and press the key again (For example, keep holding "Alt" while you tap
the "Tab" key a few times), fluxbox will lower the window again when you
move on to the next one. This allows you to preview the windows in
order, but does not change the order in doing so.

**NextGroup** \[{*options*}\] \[*pattern*\] / **PrevGroup** \[{*options*}\] \[*pattern*\]
Equivalent to NextWindow / PrevWindow above, but with the **groups**
option forced on.

**GotoWindow** *number* \[{*options*}\] \[*pattern*\]
Focuses and activates the window at position *number* in the focus list.
The *options* and *pattern* arguments have the same meaning as
**NextWindow** above.

**Activate** \[*pattern*\] | **Focus** \[*pattern*\]
With *pattern*, this is an alias for **GoToWindow** 1 *pattern*.
Without, this behaves like a window command, so that OnWindow events can
change the focused window.

**Attach** *pattern*
Combines all windows that match the *pattern* into a single tab group.
See **CLIENT PATTERNS** for more about the *pattern* arguments.

**FocusLeft** / **FocusRight** / **FocusUp** / **FocusDown**
Focus to the next window which is located in the direction specified.

**ArrangeWindows** *pattern* / **ArrangeWindowsVertical** *pattern* / **ArrangeWindowsHorizontal** *pattern*
Tries to arrange all windows on the current workspace so that they
overlap the least amount possible. **ArrangeWindowsVertical** prefers
vertical splits (windows side by side), whereas
**ArrangeWindowsHorizontal** prefers horizontal splits (windows on top
of eachother). See **CLIENT PATTERNS** for more about the *pattern*
arguments.

**ArrangeWindowsStackLeft** *pattern* / **ArrangeWindowsStackRight** *pattern*
Similar to **ArrangeWindows**, these commands arrange windows on the
current workspace. The currently focussed window is used as the *main*
window, and will fill half the screen, while the other windows are tiled
on the other half of the screen as if they were tiled with
ArrangeWindows. **ArrangeWindowsStackLeft** puts the main window on the
RIGHT hand side of the screen, and the tiled windows are on the LEFT
hand side of the screen. **ArrangeWindowsStackRight** puts the main
window on the LEFT hand side of the screen, and the tiled windows are on
the RIGHT hand side of the screen.

**ArrangeWindowsStackTop** *pattern* / **ArrangeWindowsStackBottom** *pattern*
Behaves just like **ArrangeWindowsStackLeft** and
**ArrangeWindowsStackRight**. **ArrangeWindowsStackBottom** places the
main window on the TOP half of the screen, and the tiled windows on the
bottom half of the screen. **ArrangeWindowsStackTop** places the main
window on the BOTTOM half of the screen and the tiled windows on the top
half of the screen.

**Unclutter** *pattern*
Arrange all matching windows to reduce the overall window overlap as
much as possible. Windows are not resized. See **CLIENT PATTERNS** for
more about the *pattern* arguments.

**ShowDesktop**
Minimizes all windows on the current workspace. If they are already all
minimized, then it restores them.

**ToggleSlitAbove**
Toggles the slit between its regular and the AboveDock layer

**ToggleSlitHidden**
Toggles the slit’s autohiding state (autohide doesn’t have to be
enabled)

**ToggleToolbarAbove**
Toggles the toolbar between its regular and the AboveDock layer

**ToggleToolbarHidden**
Toggles the toolbar’s autohiding state (autohide doesn’t have to be
enabled)

**Deiconify** *mode* *destination*
Deiconifies windows (or, restores from a minimized state).

Where *mode* may be one of:
**All**
All icons across all workspaces.

**AllWorkspace**
All icons on the current workspace.

**Last**
The last icon across all workspaces.

**LastWorkspace** (default)
The last icon on the current workspace.

And *destination* may be one of:
**Current** (default)
Deiconify to the current workspace.

**OriginQuiet**
Deiconify to the window’s original workspace, but does so in the
background, without moving you there.

**SetWorkspaceName** *name* / **SetWorkspaceNameDialog**
Sets the name of the current workspace.

**CloseAllWindows**
Closes all windows on all desktops.

## Menu Commands

These commands open or close fluxbox popup menus. For more information
on what these menus contain or how to configure them, see *fluxbox(1)*.

**RootMenu**
Opens the root menu. See **ROOT MENU** in **fluxbox-menu(5)** for
details.

**WorkspaceMenu**
Opens a menu showing all workspaces and windows. See **Workspace Menu**
in **fluxbox(1)** for details.

**WindowMenu**
Opens a menu containing actions for the current window. See **WINDOW
MENU** in **fluxbox-menu(5)** for details.

**ClientMenu** \[*pattern*\]
Opens a menu that contains all windows. If you specify a *pattern*, only
matching windows will be in the menu. Selecting a window will jump to
that workspace and raise the window. See **CLIENT PATTERNS** below for
more details on the *pattern* argument.

**CustomMenu** *path*
Opens a custom menu file. This *path* must be a valid menu file in the
same format as detailed by the **ROOT MENU** section of
**fluxbox-menu(5)**.

**HideMenus**
Hide all fluxbox popup menus.

## Window Manager Commands

These commands affect the Window Manager, or more than one window.

**Restart** \[*path*\]
Restarts fluxbox. This does not close any running applications. If the
optional *path* is a path to an executable window manager, that manager
is started in place of fluxbox.

**Quit** | **Exit**
Exits fluxbox. This will normally cause X to stop as well and terminate
all existing applications, returning you to the login manager or
console.

**Reconfig** | **Reconfigure**
Reloads all fluxbox configuration files including the keys file, apps
file, and init file, if they have changed.

**SetStyle** *path*
Sets the current style to that given in *path*, which must be the full
path to a fluxbox style.

**ReloadStyle**
Reloads only the current style. Useful after editing a style which is
currently in use.

**ExecCommand** *args …​* | **Exec** *args …​* | **Execute** *args …​*
Probably the most-used binding of all. Passes all the arguments to your
**$SHELL** (or /bin/sh if $SHELL is not set). You can use this to launch
applications, run shell scripts, etc. Since all arguments are passed
verbatim to the shell, you can use environment variables, pipes, or
anything else the shell can do. Note that processes only see environment
variables that were set before fluxbox started (such as in
**\\/.fluxbox/startup**), or any that are set via the **Export** or
**SetEnv** commands, below. See **fluxbox(1)** for more details on the
**ENVIRONMENT** and **\\/.fluxbox/startup** file.

**CommandDialog**
Pops up a dialog box that lets you type in any of these commands
manually.

**SetEnv** *name* *value* | **Export** *name*=*value*
Sets an environment variable in Fluxbox. It will be passed to any
applications spawned by any future ExecCommand commands.

**SetResourceValue** *resourcename* *resourcevalue* | **SetResourceValueDialog**
Sets a fluxbox resource value, which are normally stored in the init
file. See *fluxbox(1)* for more details on available resources and
allowed values.

## Special Commands

These commands have special meanings or behaviors.

**MacroCmd** {*command1*} {*command2*} {*command3*} *…​*
Allows you to execute more than one command with one keybinding. The
commands will be executed in series. The **{** **}** brackets are
literally required, as in the following example:

    MacroCmd {MoveTo 0 0} {ResizeTo 1280 800}

**Delay** {*command*} \[*microseconds*\]
Delays running *command* for the given amount of time. If the same key
binding is activated again, the timer will be restarted.

**ToggleCmd** {*command1*} {*command2*} *…​*
Alternates between the commands. On the first press of the bound key,
runs *command1*. On the next press, runs *command2*.

**BindKey** *keybinding*
Adds the given *keybinding* (which must be a valid key binding as
defined in the DESCRIPTION section above) to your keys file.

**KeyMode** *keymode* \[*return-keybinding*\]
Activates the named *keymode* (or, all key binding lines prefaced with
the same *keymode*:) and deactivates all others until the
*return-keybinding* (by default **Escape**) is pressed. The default
keymode is named *default*.

**ForEach** {*command*} \[{*condition*}\] | **Map** {*command*} \[{*condition*}\]
Runs the given *command* (normally one from the **Window Commands**
section above) on each window. If you specify a *condition* (See
**Conditions**, below) the action will be limited to matching windows.

**If** {*condition*} {*then-command*} \[{*else-command*}\] | **Cond** {*condition*} {*then-command*} \[{*else-command*}\]
If the *condition* command returns **true**, then run the
*then-command*, otherwise run the optional *else-command*. See
**Conditions** below for more information on the *condition* argument.

## Conditions

These special commands are used to match windows conditionally. They are
commonly used by the **If** and **ForEach** command.

**Matches** *pattern*
Returns **true** if the current window matches the given *pattern*. See
**CLIENT PATTERNS** below for details on the *pattern* syntax.

If your key binding uses the **OnWindow** modifier, it matches against
the window you clicked, not the currently focused window.

To check other windows besides the currently focused one, see the
**Every** and **Some** conditions below.

**Some** *condition*
Returns **true** if any window on any workspace (not just the currently
focused one) matches the *condition*.

**Every** *condition*
Returns **true** if every window on every workspace (not just the
current one) matches the *condition*.

**Not** *condition*
Returns **true** if *condition* returns **false**, and vice-versa.

**And** {*condition1*} {*condition2*} \[{*condition3*} …​\]
Returns **true** if and only if all given conditions return **true**.

**Or** {*condition1*} {*condition2*} \[{*condition3*} …​\]
Returns **true** if any of the listed conditions return **true**.

**Xor** {*condition1*} {*condition2*} \[{*condition3*} …​\]
Returns the boolean **xor** of the truth values for all conditions
listed.

# CLIENT PATTERNS

Many of the more advanced commands take a *pattern* argument, which
allows you to direct the action at a specific window or set of windows
which match the properties specified in the *pattern*.

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

**~/.fluxbox/keys**
This is the default location for the keybinding definitions.

**/usr/X11R6/include/X11/keysymdef.h**
X key names are in this file.

**/usr/X11R6/lib/X11/XKeysymDB**
X key names are also in this file.

# RESOURCES

**session.keyFile:** *location*
This may be set to override the location of the keybinding definitions.

# ENVIRONMENT

Remember that **ExecCommand** command can take advantage of other
environment variables if they are set before fluxbox is started, or via
the **Export** or **SetEnv** commands. For example, if **$TERM** is set,
it could be use like this:

    Mod1 x :ExecCommand $TERM

For more information about environment variables, see your shell’s
manual.

# EXAMPLES

Here are some interesting and/or useful examples you can do with your
keys file.

    # Mod4+drag moves a window
    OnWindow Mod4 Mouse1 :StartMoving

    # If any xterm windows are open, cycle through them. If none are open, open
    # one:
    Mod4 t :If {Some Matches (xterm)} {NextWindow (xterm)} {Exec xterm}

    # Set a different wallpaper on every workspace:
    ChangeWorkspace :Exec fbsetbg ~/.fluxbox/bg$(xprop -root _NET_CURRENT_DESKTOP | awk '{print $3}').png

    # Focusses the next window with it's xproperty 'PROP' set to 'foo'
    Mod4 p Mod4 Tab :NextWindow (@PROP=foo)

# AUTHORS

-   Jim Ramsay &lt;i.am at jimramsay com&gt; (&gt;fluxbox-1.0.0)

-   Curt Micol &lt;asenchi at asenchi com&gt; (&gt;fluxbox-0.9.11)

-   Tobias Klausmann &lt;klausman at users sourceforge net&gt;
    (⇐fluxbox-0.9.11)

-   Grubert &lt;grubert at users sourceforge net&gt; (fluxbox)

-   Matthew Hawkins &lt;matt at mh dropbear id au&gt; (blackbox)

-   Wilbert Berendsen &lt;wbsoft at xs4all nl&gt; (blackbox)

# SEE ALSO

fluxbox(1) xprop(1) xev(1) xkill(1) regex(7)
