Toggle Mic in A Particular Qube
===============================

Wanted to drop this gem for when you want to connect your microphone with a keybind:

Create the following file in dom0, call it whatever you want, toggle_mic.sh was my first choice.

.. code-block:: bash

    #!/usr/bin/env bash

    VM="$1"
    DEVICE="dom0:mic"

        if qvm-device mic ls | awk '{print $1}' | grep -i "$DEVICE" >/dev/null; then
    
        INUSE=$(qvm-device mic ls | awk -v m="$DEVICE" '$1==m {print $3')

        if [ "$INUSE != "" ]; then
            qvm-device mic d "$INUSE" "$DEVICE"
        else
            qvm-device mic a "$VM" "$DEVICE"
        fi
    fi


Make the file executable with chmod.

``chmod +x toggle_mic.sh``

Then add to your i3 config this line:

``bindsym (choose your keybind here) exec --no-startup-id bash -c '~/.config/i3/toggle_mic.sh (qube of choice)'``

This will help you with not taking your hands off the keyboard in your day to day life which is always a plus!
