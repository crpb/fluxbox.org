---
weight: 2
---
# NAME

startfluxbox - start a fluxbox session

# SYNOPSIS

**startfluxbox**

# DESCRIPTION

**startfluxbox** is a script which runs the file **~/.fluxbox/startup**
If it doesn’t exist it will be generated.

**startfluxbox** should be started from your **\\/.xinitrc** if you use
startx, or **~/.xsession** if you run a display manager, like xdm.

# FILES

**~/.fluxbox/startup**
This file contains all commands that should be executed before fluxbox
is started. The initial file contains helpful comments for beginners. It
also starts fluxbox.

# EXAMPLES

The default **~/.fluxbox/startup** is as follows:

    #!/bin/sh
    #
    # fluxbox startup-script:
    #
    # Lines starting with a '#' are ignored.

    # Change your keymap:
    xmodmap "$HOME/.Xmodmap"

    # Applications you want to run with fluxbox.
    # MAKE SURE THAT APPS THAT KEEP RUNNING HAVE AN ''&'' AT THE END.
    #
    # unclutter -idle 2 &
    # wmnd &
    # wmsmixer -w &
    # idesk &

    # And last but not least we start fluxbox.
    # Because it is the last app you have to run it with ''exec'' before it.

    exec fluxbox
    # or if you want to keep a log:
    # exec fluxbox -log "$fluxdir/log"

If you need to start applications after fluxbox, you can change the
**exec fluxbox** line above to something like this:

    exec fluxbox &
    fbpid=$!

    sleep 1
    {
        xsetroot -cursor_name left_ptr -fg white -bg black &
        ipager &
        gkrellm2 &
    } &

    wait $fbpid

So xsetroot, ipager, and gkrellm2 will all be started after fluxbox,
after giving fluxbox 1 second to startup.

For more details on what else you can do in this script, see **sh(1)**,
or the documentation for your shell.

# AUTHORS

The author of **startfluxbox(1)** is Han Boetes &lt;han at
fluxbox.org&gt;

This manpage was converted to asciidoc format by Jim Ramsay &lt;i.am at
jimramsay.com&gt; for fluxbox-1.1.2

# SEE ALSO

fluxbox(1)
