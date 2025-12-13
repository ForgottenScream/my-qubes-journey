Installing i3 on our Qubes Installation
=======================================

To install i3 on our system, we will first open our dom0 terminal and use the
``qubes-dom0-update`` command.

.. code-block:: bash

   sudo qubes-dom0-update i3 i3-settings-qubes

This will install everything necessary to run i3 without any issue.

But what did you actually install? Well to avoid installing from source, which
is a bother and not favourable on dom0, you installed the pre-build package of
i3 as well as the Qubes OS settings that make i3 play nice. This includes
``qubes-i3status`` which we will look at soon enough to edit the bar at the 
(for now) bottom of the screen.

After, just log out and select i3 from the login manager and log in again.


