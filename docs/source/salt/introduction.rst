Introduction to Salt on Qubes OS
================================

This will evolve as my understanding of Salt on Qubes OS evolves, but basically
it is the main way for you to automate the setup and maintenance of your Qubes
OS installation.

Currently there is a backup system in Qubes OS that you can
use. I never touched it because I always preferred the idea of having a fixed
state which basically means I boot things up and they are the exact same way
every time. (Unless I change it, of course.)

This is executed in various ways across the landscape, with honorable mentions
such as the Atomic desktop over at Fedora which is very impressive for what it
is, as well as bootable ISOs that have saved files and packages that will boot
up the exact same way (Tails OS is a decent example). 

If you have a look around the Qubes OS forum, any conversation related to Salt
and SaltStack will include colorful comments about their passion towards any
alternative software to SaltStack.
This is mainly due to its complexity (which is no lie, look up their manual..)
and while there are alternatives that could do the job better than Salt currently
does, it is what Qubes OS comes with, and although the philosophy for free
software is that we can just use what we want, we need to be careful.
Do you know how Qubes OS works internally? I sure don't. We could have a look
and see exactly how they use Salt and how we could change it to
<insert_alternative_here> but I enjoy having free time in life. If Qubes OS
(currently) runs with Salt then we should use it for the time being.
