Toggle Mic in A Particular Qube
===============================

Wanted to drop this gem for when you want to connect your microphone with a
keybind:

Create the following file in dom0, call it whatever you want, toggle_mic.sh was
my first choice.

.. code-block:: bash

    #!/usr/bin/env bash

    VM="$1"
    DEVICE="dom0:mic"

    INUSE=$(qvm-device mic ls | awk -v m="$DEVICE" '$1==m {print $5}')

    if [ -n "$INUSE" ]; then
        qvm-device mic d "$INUSE" "$DEVICE"
    else
        qvm-device mic a "$VM" "$DEVICE"
    fi


Make the file executable with chmod.

``chmod +x toggle_mic.sh``

Then add to your i3 config this line:

``bindsym (choose your keybind here) exec --no-startup-id bash -c '~/.config/i3/toggle_mic.sh (qube of choice)'``

This will help you with not taking your hands off the keyboard in your day to
day life which is always a plus!

.. note::
    Can be done with camera and other USB block devices as well, but you will
    need to change the commands slightly, I suggest looking at the --help flag
    of the qvm-device command and testing the commands until you get there!
