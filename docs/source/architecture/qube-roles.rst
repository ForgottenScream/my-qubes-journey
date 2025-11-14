Qube Roles
==========

You probably read the last page and thought, "system qubes? what?" which is fair, if you haven't read anything else or had a good look at the diagram from the threat-model page it is confusing.
Essentially different components of your computer are also isolated in various qubes.

System Qubes
============

The default system qubes are:

- sys-net - This is where the internet comes in since it is the only qube that is actually connected to the network device in your computer.
- sys-usb - Same thing as sys-net but for the USB controller device in your computer
- sys-firewall - This qube functions as the firewall for your whole system.
- sys-whonix - This is based off the whonix-gateway template and is where your disposable qubes's traffic goes through.

You will have these qubes running all the time.

Main Qubes
==========

These qubes will be where you will live majority of the time, because ideally we don't want to spend all of our time maintaining, although at the beginning it will be the case.
There is no fixed recipe here, grab your threat model and think. What do I need? A personal qube for things I would do at home. A work qube for work so if anything happened to the personal qube, the work qube wouldn't be affected.
Maybe a vault qube for storing important documents in its own space without any access to the internet? Now you're thinking like a Qubes user.

Disposable Qubes
================

These qubes can be created off of normal templates which can be useful for specific use cases, as I progress I will mention some but this is even more personalised to you and your use cases so you can leave it for now.
