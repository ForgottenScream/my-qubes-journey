Use universal keybind to open a file manager for any Qube
=========================================================

Going up to the menu to open the file manager is annoying, and we are on i3 so
we should be able to do something about it! Right?

Of course we can, we have the blueprints from qubes-i3-sensible-terminal, we
just need to take advantage and adapt to what we need!

Create the following file in /usr/bin/, call it whatever you want,
qubes-i3-file-manager was my first choice as it follows suit with the other scripts.

.. code-block:: bash

    #!/usr/bin/sh
    set -eu

    main() {
    case "${1-}" in
    "") ;;
    *) printf '%s\n' "invalid argument" >&2; exit 1;;
    esac

    guivm_fm="thunar"
    domU_fm="thunar"
    id="$(xprop -root _NET_ACTIVE_WINDOW)"
    id="${id##* }"
    vm="$(xprop -id "$id" | grep '_QUBES_VMNAME(STRING)')" || true
    if test -z "$vm"; then
    exec "$guivm_fm"
    fi
    vm="${vm#*\"}"
    vm="${vm%\"*}"

    if command -v qrexec-client >/dev/null; then
    exec qrexec-client -e -d "$vm" -- \
    "DEFAULT:QUBESRPC qubes.StartApp+$domU_fm $vm"
    fi
    exec qvm-run --no-gui --service -- "$vm" qubes.StartApp+"$domU_fm"
    }

    main "$@"


Make the file executable with chmod.

.. code-block:: bash

    chmod +x qubes-i3-file-manager

Then amend your i3 config. I chose to follow suit with
qubes-i3-sensible-terminal :

.. code-block:: bash

    set $file-manager qubes-i3-file-manager

    # start file manager in domain of currently active window
    bindsym (choose your keybind here) exec $file-manager

This will now open the default file manager in the active qube and will fall
back to opening the default file manager in dom0.
