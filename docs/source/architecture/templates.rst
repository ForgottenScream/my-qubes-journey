Templates
=========

Now that we have somewhat of an idea of our threat model, we can start looking at Templates.
Template qubes are where your software will be installed and maintained.
When you set up Qubes OS you will be given the option to install Whonix templates as well as Fedora and Debian.
Optionally (which we will do later on) you can get minimal templates which have the absolute bare minimum.
This has many use cases but remember to install the necessary software to make the template functional (think like Arch in a way).

.. note::

    I will be updating this as I go through the journey of Qubes OS myself, currently I am only using the full template for system qubes (firewall, net, usb).
    Everything else I use minimal templates because frankly I prefer it not working the first couple of times while I go and find what package I forgot to install than having loads of packages that I never touch.
    Be nice to your HDD.

List of Templates (Suggestion)
==============================
This is in tune with what I use, so if your philosophy around software or distros (linux distributions) differ, then change it accordingly for your use case.

- Fedora Template - For now we will use for system qubes such as (sys-net, sys-usb and sys-firewall)
- Fedora Minimal Template - We will use this for our main qubes, (personal, work, vault)
- Debian Minimal Template - We will use this for our main qubes.
- Whonix Template - We will use this for disposable qubes running through whonix.

.. admonition:: Personal Opinion Time! (POT?)

   I personally only use Debian Minimal Templates for specific software like Signal because the official instructions are only for debian, otherwise I wouldn't touch it. But that's just me.
