---
weight: 6
---
# NAME

fluxbox-style - A comprehensive look at styles/themes for fluxbox(1).

# SYNOPSIS

This document describes various options available for fluxbox styles.

# DESCRIPTION

What is a Style?

Styles, sometimes referred to as Themes, are a graphical overlay for the
fluxbox(1) window manager. If you wanted to get to know fluxbox, the
styles would be the *look* of the *look and feel*.

Styles are simple ASCII text files that tell fluxbox(1) how to generate
the appearance of different components of the window manager. The
default installation of fluxbox(1) is shipped with many classic examples
that show a great deal of what one could do. To use one of the standard
styles navigate to the *System Styles* menu under your main fluxbox(1)
menu.

fluxbox(1) uses its own graphics class to render its images on the fly.
By using styles you can determine, at a great level of configurability,
what your desktop will look like. Since fluxbox(1) was derived from
blackbox many often wonder if old themes will work on the latest
releases of fluxbox(1). Well they basically do, but you will have to
tune them since the fluxbox(1) code has changed quite a bit since the
initial grab.

# STRUCTURE

A style is made up of a few major components which then have their own
sub-directives. The major components are as follows:

The *window.\** directives control the appearance of the window frames,
*window.tab.\\* controls the appearance of the window tabs, *menu.\**
controls the appearance of the popup menu that you see when you right
click on the desktop. *toolbar.\\* is the bar you will see at the top or
bottom of your screen. Finally the *slit.\** has options you can use to
customize the appearance of the slit. However if you don’t set the slit
directives specifically, the slit’s appearance is controlled by the
toolbar directives instead.

To understand how the style mechanism works, it is nice to know a little
about how X11 resources work. X11 resources consist of a key and a
value. The key is constructed of several smaller keys (sometimes
referred to as children), delimited by a period (.). Keys may also
contain an asterisk (\*) to serve as a wildcard, which means that one
line of text will match several keys. This is useful for styles that are
based on one or two colors.

A more complete reference to this can be found in X(7), section
*RESOURCES*.

# LOCATION

There are many places to store your styles, the most common is in your
*~/.fluxbox/styles* directory. The initial installation will place the
default styles in *@pkgdatadir@/styles* providing a basic usable
configuration.

When creating your own style, create a directory (normally the name of
your style) in *~/.fluxbox/styles/* (If the *styles* directory doesn’t
exist, create that also). While there isn’t an official structure, it is
common to create a directory named after your style and place your
pixmaps directory (if required) in there along with a file called
theme.cfg (may also be named style.cfg). This file is where you will
construct your style using the components covered later in this manual
page. An example of steps taken when beginning a style project of your
own may look like:

    $ cd
    $ mkdir -p ~/.fluxbox/styles/YourStyle/pixmaps
    $ cd ~/.fluxbox/styles/YourStyle
    $ nano theme.cfg

Output of a packaged style should look like the following:

    $ cd
    $ tar -tjvf YourStyle.tar.bz2
     .fluxbox/styles/YourStyle/theme.cfg
     .fluxbox/styles/YourStyle/pixmaps
     .fluxbox/styles/YourStyle/pixmaps/stick.xpm
     ...

Of course, all of these are just preferences, fluxbox(1) allows for the
customization of many things, including how you handle your styles. Just
remember, however, that if you plan to distribute your style you may
find some community bickering if you don’t follow practices. :)

# CREATING YOUR STYLE

As discussed above, fluxbox(1) allows you to configure its four main
components: the toolbar, menus, slit and window decorations. Remember
that you can customize the slit with its own directives, otherwise the
slit will take the appearance of the toolbar.

Here are some quick examples to illustrate basic syntax:

    toolbar.clock.color: green

This sets the color resource of the toolbar clock to *green*. Another
example:

    menu*color:     rgb:3/4/5

This sets the color resource of the menu and all of its *children* to
“rgb:3/4/5”. (For a description of color names, see X(1).) So this one
also applies to *menu.title.color* and *menu.frame.color*. And with

    *font:  -b&h-lucida-medium-r-normal-*-*-140-*

you set the font resource for all keys to this font name all at once
(For information about the fonts installed on your system, you can use a
program like xfontsel(1), gtkfontsel, or xlsfonts(1).)

In the last example you will notice the wildcard (\*) before font. In a
Fluxbox style you can set a value with a wildcard. The example means
that every font in the style will be what is specified. You can do this
with any component/value. For example if you wanted all of the text to
be one color you would do:

    *textColor:  rgb:3/4/5

This means that you can setup a very simple style with very few
properties. See the EXAMPLES below for an example of this in practice.
fluxbox(1) also allows you to override wildcards in your style. Lets
take our example above and add an override for the
toolbar.clock.textColor component:

    *textColor: rgb:3/4/5
    toolbar.clock.textColor: rgb:255/0/0

With that all of the text will be *rgb:3/4/5* except the toolbar clock
text which will be *rgb:255/0/0*.

Now what makes fluxbox(1) so spectacular is its ability to render
textures on the fly. A texture is a fillpattern that you see on some
styles. Texture descriptions are specified directly to the key that they
should apply to, e.g.:

    toolbar.clock:  Raised Gradient Diagonal Bevel1
    toolbar.clock.color:    rgb:8/6/4
    toolbar.clock.colorTo:  rgb:4/3/2

Don’t worry, we will explain what these mean. A texture description
consists of up to five fields, which are as follows:

**Flat | Raised | Sunken**

gives the component either a flat, raised or sunken appearance.

**Gradient | Solid**

tells fluxbox(1) to draw either a solid color or a gradient texture.

**Horizontal | Vertical | Diagonal | Crossdiagonal | Pipecross |
Elliptic | Rectangle | Pyramid**

Select one of these texture types. They only work when **Gradient** is
specified.

**Interlaced**

tells fluxbox(1) to interlace the texture (darken every other line).
This option is most commonly used with gradiented textures, but it also
works in solid textures.

**Bevel1 | Bevel2**

tells fluxbox(1) which type of bevel to use. Bevel1 is the default
bevel. The shading is placed on the edge of the image. Bevel2 is an
alternative. The shading is placed one pixel in from the edge of the
image.

Instead of a texture description, also the option **ParentRelative** is
available, which makes the component appear as a part of its parent,
e.g. totally transparent.

Or for even more possibilities Pixmap. If pixmap texture is specified
(it might not be necessary on every occasion) the pixmap file is
specified in a separate pixmap resource.

    toolbar.clock: pixmap
    toolbar.clock.pixmap: clock_background.xpm

This feature might need some investigation, reports say that sometimes
the resources color and colorTo must be set and then they may not be
set.

All gradiented textures are composed of two color values: the *color*
and *colorTo* resources. When **Interlaced** is used in **Solid** mode,
the *colorTo* resource is used to find the interlacing color.

# FONT EFFECTS

In addition to specifying the font-family and the font-weight via the
supported font-rendering-engine (eg, Xft), fluxbox(1) supports some
effects: *halo* and *shadow*. To set the shadow effect:

    menu.title.font: sans-8:bold
    menu.title.effect: shadow
    menu.title.shadow.color: green
    menu.title.shadow.x: 3
    menu.title.shadow.y: 3

To set the halo effect:

    menu.title.font: sans-8:bold
    menu.title.effect: halo
    menu.title.halo.color: green

## FONT PROBLEMS

If you have problems installing fonts or getting them to work, you
should read the docs page at xfree.org. Here is a link to one of these:
<http://xfree.org/4.3.0/fonts2.html#3>

# FULL COMPONENT LIST

Here is the exhaustive component list for fluxbox(1) styles. Each one is
listed with their type of value required. Comments in a style file are
preceded with an exclamation point (!) which we also use here so that
these can be pasted into a new theme.cfg to be customized appropriately.
Please note that in order to keep styles consistent it is often the
practice of stylists to provide all of the theme-items in their style
file even if they are not used. This allows the user the ease of
changing different components.

# WINDOW OPTIONS

Many, many things you can do with window design in fluxbox(1), below are
your options. Have fun.

    -----------------------------------------
    window.bevelWidth:              <integer>
    window.borderColor:             <color>
    window.borderWidth:             <integer>
    window.button.focus:            <texture type>
    window.button.focus.color:      <color>
    window.button.focus.colorTo:    <color>
    window.button.focus.picColor:   <color>
    window.button.focus.pixmap:     <filename>
    window.button.pressed: <texture type>
    window.button.pressed.color:    <color>
    window.button.pressed.colorTo:  <color>
    window.button.pressed.pixmap:   <filename>
    window.button.unfocus:          <texture type>
    window.button.unfocus.color:    <color>
    window.button.unfocus.colorTo:  <color>
    window.button.unfocus.picColor: <color>
    window.button.unfocus.pixmap:   <filename>
    window.close.pixmap:            <filename>
    window.close.pressed.pixmap:    <filename>
    window.close.unfocus.pixmap:    <filename>
    window.frame.focusColor:        <color>
    window.frame.unfocusColor:      <color>
    window.grip.focus:              <texture type>
    window.grip.focus.color:        <color>
    window.grip.focus.colorTo:      <color>
    window.grip.focus.pixmap:       <filename>
    window.grip.unfocus:            <texture type>
    window.grip.unfocus.color:      <color>
    window.grip.unfocus.colorTo:    <color>
    window.grip.unfocus.pixmap:     <filename>
    window.handle.focus:            <texture type>
    window.handle.focus.color:      <color>
    window.handle.focus.colorTo:    <color>
    window.handle.focus.pixmap:     <filename>
    window.handle.unfocus:          <texture type>
    window.handle.unfocus.color:    <color>
    window.handle.unfocus.colorTo:  <color>
    window.handle.unfocus.pixmap:   <filename>
    window.handleWidth:             <integer>
    window.iconify.pixmap:          <filename>
    window.iconify.pressed.pixmap:  <filename>
    window.iconify.unfocus.pixmap:  <filename>
    window.justify:                 <{Left|Right|Center}>
    window.label.active:            <texture type>
    window.label.active.textColor:  <color>
    window.label.focus:             <texture type>
    window.label.focus.color:       <color>
    window.label.focus.colorTo:     <color>
    window.label.focus.font:        <font>
    window.label.focus.pixmap:      <filename>
    window.label.unfocus:           <texture type>
    window.label.unfocus.color:     <color>
    window.label.unfocus.colorTo:   <color>
    window.label.unfocus.font:      <font>
    window.label.unfocus.pixmap:    <filename>
    window.label.focus.textColor:   <color>
    window.label.unfocus.textColor: <color>
    window.maximize.pixmap:         <filename>
    window.maximize.pressed.pixmap: <filename>
    window.maximize.unfocus.pixmap: <filename>
    window.roundCorners:            <{Top|Bottom}{Left|Right}>
    window.shade.pixmap:            <filename>
    window.shade.pressed.pixmap:    <filename>
    window.shade.unfocus.pixmap:    <filename>
    window.stick.pixmap:            <filename>
    window.stick.pressed.pixmap:    <filename>
    window.stick.unfocus.pixmap:    <filename>
    window.stuck.pixmap:            <filename>
    window.stuck.unfocus.pixmap:    <filename>
    window.lhalf.pixmap:            <filename>
    window.lhalf.unfocus.pixmap:    <filename>
    window.rhalf.pixmap:            <filename>
    window.rhalf.unfocus.pixmap:    <filename>
    window.title.focus:             <texture type>
    window.title.focus.color:       <color>
    window.title.focus.colorTo:     <color>
    window.title.focus.pixmap:      <filename>
    window.title.height:            <integer>
    window.title.unfocus:           <texture type>
    window.title.unfocus.color:     <color>
    window.title.unfocus.colorTo:   <color>
    window.title.unfocus.pixmap:    <filename>
    -----------------------------------------

# MENU OPTIONS

Everything you need to make your menu look pretty.

    -----------------------------------------
    menu.bevelWidth:                <integer>
    menu.borderColor:               <color>
    menu.borderWidth:               <integer>
    menu.bullet:                    <{empty|square|triangle|diamond}>
    menu.bullet.position:           <{left|right}>
    menu.frame:                     <texture type>
    menu.frame.color:               <color>
    menu.frame.colorTo:             <color>
    menu.frame.disableColor:        <color>
    menu.frame.font:                <font>
    menu.frame.justify:             <{Left|Right|Center}>
    menu.frame.pixmap:              <filename>
    menu.frame.textColor:           <color>
    menu.hilite:                    <texture type>
    menu.hilite.color:              <color>
    menu.hilite.colorTo:            <color>
    menu.hilite.font:               <font>
    menu.hilite.justify:            <{left|center|right}>
    menu.hilite.pixmap:             <filename>
    menu.hilite.textColor:          <color>
    menu.itemHeight:                <integer>
    menu.title:                     <texture type>
    menu.title.color:               <color>
    menu.title.colorTo:             <color>
    menu.title.font:                <font>
    menu.title.pixmap:              <filename>
    menu.title.textColor:           <color>
    menu.title.justify:             <{Left|Right|Center}>
    menu.titleHeight:               <integer>
    menu.roundCorners:              <{Top|Bottom}{Left|Right}>
    menu.selected.pixmap:           <filename>
    menu.submenu.pixmap:            <filename>
    menu.unselected.pixmap:         <filename>
    -----------------------------------------

BACKGROUND

    Every style must specify the background option. If you don't want your style to
    change the user's background, then use `background: none'. The options
    `centered', `aspect', `tiled', and `fullscreen' require the `background.pixmap'
    resource to contain a valid file name. The `random' option requires
    `background.pixmap' to contain a valid directory name. For these options,
    *fluxbox(1)* will call *fbsetbg(1)* to set the background. The options `gradient',
    `solid', and `mod' all require `background.color' to be set. `gradient' and
    `mod' both require `background.colorTo'. `mod' requires `background.modX' and
    `background.modY' to be set as well. These options will be passed to
    *fbsetroot(1)* to set the background. The special option `unset' is for use in
    user overlay files only. It specifies that fbsetbg should never be run (by
    default, even when `none' is set in the overlay, fluxbox will try to run
    ``fbsetbg -z'' to restore the last wallpaper).

       background: centered|aspect|tiled|fullscreen|random|solid|gradient <texture>|mod|none|unset
       background.pixmap: <file or directory>
       background.color: <color>
       background.colorTo: <color>
       background.modX: <integer>
       background.modY: <integer>

    SLIT
    ----
    Here are all of the options for the slit.

       -----------------------------------------
       slit: <texture type>
       slit.bevelWidth: <integer>
       slit.borderColor: <color>
       slit.borderWidth:               <integer>
       slit.color:                     <color>
       slit.colorTo:                   <color>
       slit.pixmap:                    <filename>
       -----------------------------------------

    TOOLBAR OPTIONS
    ---------------
    Below you will find all of the configuration possibilities for the toolbar.
    The list is pretty extensive and offers you many options to make your toolbar
    look just the way you want it.

       -----------------------------------------
       toolbar: <texture type>
       toolbar.bevelWidth:             <integer (0-255)>
       toolbar.borderColor:            <color>
       toolbar.borderWidth:            <integer>
       toolbar.button.scale:           <integer>
       toolbar.color:                  <color>
       toolbar.colorTo:                <color>
       toolbar.clock:                  <texture type>
       toolbar.clock.borderColor:      <color>
       toolbar.clock.borderWidth:      <integer>
       toolbar.clock.font:             <font>
       toolbar.clock.justify:          <{Left|Right|Center}>
       toolbar.clock.pixmap:           <filename>
       toolbar.clock.color:            <color>
       toolbar.clock.colorTo:          <color>
       toolbar.clock.textColor:        <color>
       toolbar.height:                 <integer>
       toolbar.iconbar.focused:        <texture type>
       toolbar.iconbar.focused.color:  <color>
       toolbar.iconbar.focused.colorTo:<color>
       toolbar.iconbar.focused.pixmap: <filename>
       toolbar.iconbar.unfocused:      <texture type>
       toolbar.iconbar.unfocused.color:  <color>
       toolbar.iconbar.unfocused.colorTo: <color>
       toolbar.iconbar.unfocused.pixmap: <filename>
       toolbar.iconbar.empty:          <texture type>
       toolbar.iconbar.empty.color:    <color>
       toolbar.iconbar.empty.colorTo:  <color>
       toolbar.iconbar.empty.pixmap:   <filename>
       toolbar.iconbar.focused.borderColor: <color>
       toolbar.iconbar.focused.borderWidth:    <integer>
       toolbar.iconbar.unfocused.borderColor: <color>
       toolbar.iconbar.unfocused.borderWidth:  <integer>
       toolbar.iconbar.borderColor:    <color>
       toolbar.iconbar.borderWidth:    <integer>
       toolbar.iconbar.focused.font:   <font>
       toolbar.iconbar.focused.justify:        <{Left|Right|Center}>
       toolbar.iconbar.focused.textColor: <color>
       toolbar.iconbar.unfocused.font: <font>
       toolbar.iconbar.unfocused.justify:      <{Left|Right|Center}>
       toolbar.iconbar.unfocused.textColor: <color>
       toolbar.pixmap:                 <filename>
       toolbar.shaped:                 <boolean>
       toolbar.workspace.font:         <font>
       toolbar.workspace.justify:      <{Left|Right|Center}>
       toolbar.workspace.textColor:    <color>
       toolbar.workspace:              <texture type>
       toolbar.workspace.borderColor:  <color>
       toolbar.workspace.borderWidth:  <integer>
       toolbar.workspace.color:        <color>
       toolbar.workspace.colorTo:      <color>
       toolbar.workspace.pixmap:       <filename>
       -----------------------------------------

    EXAMPLES
    --------
    This list may seem intimidating, but remember, when you create your own style
    you can easily set a majority of these keys with a single component. For an
    example of this:

       -----------------------------------------
       *color: slategrey
       *colorTo:       darkslategrey
       *unfocus.color: darkslategrey
       *unfocus.colorTo:       black
       *textColor:     white
       *unfocus.textColor:     lightgrey
       *font:  lucidasans-10
       -----------------------------------------

    This sets nice defaults for many components.

    COLOR FORMATS
    -------------
    These are the color formats for styles:

       #000000 (Hexadecimal)
       rgb:<0-255>/<0-255>/<0-255>

    See /usr/share/X11/rgb.txt for an explanation.

    AUTHORS
    -------
    Blackbox was written and maintained by Brad Hughes <blackbox at alug.org>
    and Jeff Raven <jraven at psu.edu>.

    fluxbox(1) is written and maintained by Henrik Kinnunen <fluxgen at fluxbox.org>
    with contributions and patches merged from many individuals around the world.

    The Official fluxbox(1) website: http://www.fluxbox.org
    You can find a lot of styles here: http://tenr.de/

    This manpage was composed from various resources including the official
    documentation, fluxbox(1) man page and numerous other resources by Curt
    "Asenchi" Micol. If you notice any errors or problems with this page, please
    contact him here: <asenchi at asenchi.com> and using the great contributions of
    <grubert at users.sourceforge.net>.  Numerous other languages could be available
    if someone jumps in.

    SEE ALSO
    --------
    fluxbox(1) fbsetbg(1) fbsetroot(1)
