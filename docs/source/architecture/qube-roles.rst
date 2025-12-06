Qube Roles
==========

This page will explain the different types of qubes that will come in your system as well as their roles.

Dom0
----
Let's start with the main qube you will encounter when you install Qubes OS.
Dom0 is your administrative domain, meaning you will interact with the rest of your system via this
qube. In other words, while you may be opening different qubes for personal activities, work or
gaming (yes, it is possible), you are using dom0 to access and use these qubes.
If you look at the image from :doc:`Threat Model <architecture/threat-model>` you will see the
'AdminVM' which connects to some other qubes. That is dom0, which has a few rules and best practices
that I will mention as we go along.

.. warning::
   Dom0 never connects to the internet, there are ways around this for updating and installing
   software, but the general rule of thumb is to not install any software on Dom0.

System Qubes
------------

System qubes are focused on running your system (obviously). But how?
Essentially different components of your computer are also isolated in various qubes.
The default system qubes are:

- sys-net - This is where the internet comes in since it is the only qube that is actually connected
  to the network device in your computer.
- sys-usb - Same thing as sys-net but for the USB controller device in your computer
- sys-firewall - This qube functions as the firewall for your whole system.
- sys-whonix - This is based off the whonix-gateway template and is where your disposable qubes's
  traffic goes through.

You will have these qubes running all the time.

Main Qubes / AppVMs
----------

These qubes will be where you will live majority of the time, because ideally we don't want to spend
all of our time maintaining this system, we want to use it!
There is no fixed recipe here, grab your threat model and think.
What do I need? A personal qube for things I would do at home.
A work qube for work so if anything happened to the personal qube, the work qube wouldn't be affected.
Maybe a vault qube for storing important documents in its own space without any access to the internet?
Now you're thinking like a Qubes user.

Template Qubes
--------------
I will delegate a whole page for this but for now all you need to know is that App Qubes have to be
based on something as they will not have their own complete VM with their own filesystem.
That would take up a lot of space if you think about it. (Still posisble, it's called StandaloneVMs)
What we instead do is have a template qube where we install the software we want and base an AppVM
on that template. An example that we won't do is the following: Basing your personal qube and work
qube on the same template because they both share a browser, image software and so on.

StandaloneVMs
-------------
Although for majority of use cases template and app qubes are enough, you may need to have a full
VM with its filesystem and own storage to itself, maybe for Windows? wink wink.
Well that's what StandaloneVMs are for, they won't be based off any template and you bring your own
ISO image.

Disposable Qubes
----------------

These qubes can be created off of normal templates which can be useful for specific use cases, as I
progress I will mention some but this is even more personalised to you and your use cases so you can
leave it for now.
