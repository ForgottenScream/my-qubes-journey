Setup Wifi Connection
=====================

What's cool: Having a qube solely for handling the network components (excluding
usb of course)

What's amazing: Having said qube be disposable so the only things that persist
are the configuration files for the network connections, nothing else.

Of course we will be going with the second option, but if it is your first time
doing this I undertand you will want a smoother ride so feel free to have the
default sys-net qube that is not disposable.

.. code-block:: bash

    #!/usr/bin/env bash
    set -e
    SSID='Put your wifi name here.'
    CONN_NAME="${SSID}.nmconnection"
    CFG_DIR="/rw/config/NM-system-connections"
    CFG_PATH="$CFG_DIR/$CONN_NAME"

    sudo mkdir -p "$CFG_DIR"
    sudo chown root:root "$CFG_DIR"
    sudo chmod 700 "$CFG_DIR"

    # generate uuid once

    UUID=$(uuidgen)

    read -s -p "Enter passphrase for Wi-Fi '$SSID': " WIFI_PSK
    echo
    if [ -z "$WIFI_PSK" ]; then
    echo "No password entered; aborting."
    exit 1
    fi

    sudo tee "$CFG_PATH" > /dev/null <<EOF
    [connection]
    id=$SSID
    uuid=$UUID
    type=802-11-wireless
    autoconnect=true

    [wifi]
    ssid=$SSID
    mode=infrastructure

    [wifi-security]
    auth-alg=open
    key-mgmt=wpa-psk
    psk=$WIFI_PSK

    [ipv4]
    method=auto

    [ipv6]
    method=ignore
    EOF

    sudo chown root:root "$CFG_PATH"
    sudo chmod 600 "$CFG_PATH"

    echo "Created $CFG_PATH with fixed UUID. Shutdown the template and start sys-net disposable to test."

Grab this, create a file, make it executable with chmod +x {filename} and place
the file in the template of sys-net (you should clone the template and dedicate
it to just sys-net to avoid issues as sys-usb also uses said template - good to
have isolation)

Then execute the file in the template, this will create the NetworkManager
connection file necessary to connect to your wifi network. Assuming you are
connecting to a standard network, this should work. You can always connect to
the wifi and go to /etc/NetworkManager/system-connections to check out how the
file should be.
