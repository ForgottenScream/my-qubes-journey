Installing Qubes OS
===================

So you managed to survive verifying your ISO isn't corrupted. I will assume its because it was so 
easy to follow along with the documentation.

Once again, the `Qubes OS documentation <https://doc.qubes-os.org/en/latest/user/downloading-
installing-upgrading/installation-guide.html>`_ is great for this bit. It includes images which may
help with further understanding. I won't include it as I have stated that you should use both guides
in tandem with each other to fill any missing bits.

Jokes aside you now need to flash that ISO to the USB in your hand. First plug it in, shouldn't be
in your hand at this point, in fact you should make sure it is empty and has no valuable cat pictures!

Then you use either Rufus, balenaEtcher, or dd if you are on linux to flash the ISO image.

.. note::
   macOS users can also use dd, which is recommended since you need more exposure to the dark and scary terminal.

I won't include instructions for the GUI options, should be straightforward.
For linux users, open up that terminal and navigate to your ISO image.


First check where your USB drive is mounted:

.. code-block:: bash

   lsblk

This will show all the drives in your system, typically sda sdb and so on.
The usb drive will have smaller storage so should be easy to identify the name.

Once you know *for sure* which drive is the USB drive, type in the following:

.. code-block:: bash

   sudo dd if=/path/to/iso/file of=/dev/sdX bs=1m status=progress

sdX in this command should be changed to the drive. And do not do sdb1, needs to be the whole drive not just a partition.

.. warning::

   STOP! This command is deadly, like it can ruin your whole system if you don't do it right, so triple check :)

If the flashing was successful, you should be able to unplug the drive and plug in again to see the
contents of the ISO inside the drive.
Don't touch anything inside, just verify its not empty.

Actually Installing on your PC
------------------------------
This is the moment you have been waiting for.
Finally you will boot up your laptop (which shouldn't have anything valuable
i.e. you backed everything up)

BUT WAIT! You haven't disabled secure boot! Which is weird to say since we are installing a
'reasonably secure operating system', but its simply because Qubes OS
is not digitally signed with approved certificates so Secure Boot won't recognise and therefore
won't allow it to boot.

Go over to your BIOS first and disable Secure Boot, then save and restart the machine.

Go over to your BIOS first and disable Secure Boot, then save and restart the machine.
Then press the relevant F key (F11, F10, F9 - depends on manufacturer).

At that point a menu will show up with (hopefully) the USB option with Qubes OS, click it and test
the installation media then install. (If not there are ways to access the media drive and run the
installation script but it is a bit hacky so I will include in another page)

If a window shows up with "Unsupported Hardware Detected", don't stress, relax.
Go over to `Hardware Requirements <https://doc.qubes-os.org/en/latest/user/downloading-installing-
upgrading/installation-guide.html#hardware-requirements>`_ section and learn how to activate
IOMMU-virtualization.

The setup process is quite straightforward and there are many other guides that have covered this
so set up the user, agree to erase your drive, locale, password and so on.

.. note::
   If you use multiple keyboard layouts, note that the disk encryption password will be entered with
   the layout you chose in the installation, not QWERTY. Also encrypt your disk kids.

Let it install, it will take a while and it will be in two parts.
After the restart you will boot in, unlock the drive with your decryption password then finish the
installation. 

.. image:: /_static/initial-setup-menu-configuration.webp
   :alt: Qubes Configuration Menu
   :width: 600px
   :height: 400px
   :align: center

If you are sticking with my recommendations, select only Fedora and Whonix, with Fedora as the Default.
Then select to create default system qubes, making firewall and sys-usb disposable.

.. note::

   I will update this to be able to make sys-net disposable in the future, currently not recommending
   as you would have to put your Wifi password every time you log in. But there is a fix I have seen already.

Now do not select create default application qubes. We will use what we have decided in previous chapters.
Select the 'Use a qube to hold all USB controllers'.

.. note::
   I wouldn't recommend having both net and usb in one qube for security reasons (think malicious usb with internet access).
   But if you think because of your RAM this is something you can live with, fine.

If you are on a PC, you may want to select to automatically accept mice and keyboard, which is discouraged but what can you do.

Finally select to create whonix gateway and workstation and optionally enable updates to go over Tor.
I would recommend this.

.. warning::

   Leave everything else below as is unless you know how it works, which I do not :)

Click on Done at the very top and log in to your new system.
