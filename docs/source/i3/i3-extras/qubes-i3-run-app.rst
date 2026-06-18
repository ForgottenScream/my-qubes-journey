Use universal keybind to run an application on any Qube
=======================================================

So you finished configuring i3 and you have all your keybinds (I hope) ready to
open your favourite applications in your domains, but then you realize, they all
have to be unique? That's not efficient. You shouldn't have to have multiple
keybinds to open the same application, only because they are in different Qubes!

How can we fix this? Well, we can actually take inspiration from another package
that we DO open with one keybind that works in any domain! The terminal! If you
notice the "$terminal" variable in the i3 config file, it's definition explains
that qubes-i3-sensible-terminal will open the terminal in the currently active
domain. That's perfect!

But how can we adapt that to any application? Well if you run:

.. code-block:: bash

    which qubes-i3-sensible-terminal

You will find the location of the script, usually in /usr/bin, so use your
favorite editor, open it and look at the code!

It seems that it uses xprop to identify the domain, then qrexec to open the
terminal. We can apply that (with some changes) to accept any package in our
various qubes, with a default to a specific qube.

Create the following file in /usr/bin/, call it whatever you want,
qubes-i3-run-app was my first choice as it follows suit with the other scripts.

.. code-block:: bash

    #!/usr/bin/sh
    set -eu

    # Usage: qubes-i3-run-app <default-vm> <application>
    # Example: qubes-i3-run-app work-vm firefox

    main() {
      default_vm="${1:-}"
      app_name="${2:-}"

      if test -z "$default_vm" || test -z "$app_name"; then
        printf '%s\n' "Usage: $0 <default-vm> <application>" >&2
        exit 1
      fi

      # Detect the active window's VM
      id="$(xprop -root _NET_ACTIVE_WINDOW)"
      id="${id##* }"
      vm="$(xprop -id "$id" | grep '_QUBES_VMNAME(STRING)')" || true

      # Extract VM name
      if test -n "$vm"; then
        vm="${vm#*\"}"
        vm="${vm%\"*}"
      else
        vm="$default_vm"
      fi

      # Run the application using qvm-run
      exec qvm-run "$vm" "$app_name"
    }

    main "$@"


Make the file executable with chmod.

.. code-block:: bash

    chmod +x qubes-i3-run-app

Then amend your i3 config bindings:

.. code-block:: bash

    bindsym (choose your keybind here) exec --no-startup-id qubes-i3-run-app <default-vm-name> <app_name>

This will now open the application you want in the active qube and will fall
back to the defined qube so you can maintain your habit of opening your main
qube and application in one keybind.

.. note::

   Review the code properly, I used qvm-run instead of qrexec due to its
   simplicity, but it is likely that qrexec is more secure so if you get that up
   and running open an issue in the repository! Thanks!
