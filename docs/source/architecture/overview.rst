Overview
========

Before we start looking into threat models and explaining some of the critical components of Qubes OS, I wanted to give an overview of the project, stigma around it and some clarifications.

Why use Qubes OS
----------------
If I had a {insert coin of choice} for every time I read reasons for and against using Qubes OS or Linux I would be set for life.
And it's funny because you have the same type of people on both sides of the conversation for Windows/Mac -> Linux and Linux -> Qubes OS.

.. note::
   Qubes OS is not Linux. In some corners of the privacy/security world you will find that Linux may not be so `secure <https://madaidans-insecurities.github.io/linux.html>`_ as you thought/were told.

So to put this matter to bed and not have to discuss any further, here is a (clearly not biased) list of reasons **to** use Qubes OS and to **not** use Qubes OS.

Why You Should Use Qubes OS
~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Qubes uses Xen-based virtualization to create isolated qubes. In other words - secure when talking about computer architecture.
- It gives you the opportunity to organize your digital life since right now you probably use one or two devices for everything, in contrast to your physical life where you are able to isolate various aspects of your life.
- Multiple Clipboards - That's right each qube has its own clipboard and Qubes gives you a global clipboard so you can copy stuff over from one qube to another.
- Disposable Qubes - Best security feature I have seen personally. Opening a link from a suspicious email? DispVM. Opening a PDF you don't trust? DispVM. Attaching a USB you found on the street? (don't ever do that btw) DispVM. Honestly the use cases are endless.
- Privacy. Actually Qubes focuses on security, they 'delegate' the whole privacy issue to `Whonix <https://www.whonix.org/>`_ which is a whole other topic but good to know it is there.

Why You Shouldn't Use Qubes OS
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Time is a fickle thing, and only when it is paired with will, passion and determination can you truly do something amazing. If your life is busy and you cannot find the time, Qubes OS may be a heavy undertaking. That being said you can (and should) take it slow, use a spare machine and learn the ropes. With this documentation you will learn automating things which will fix this time issue anyway.
- Software. This is more of a Linux thing and even then Qubes gives you a secret weapon which I will mention later. But if you are dependent on software that is exclusive to Windows or MacOS, then of course you may be discouraged or simply unable to use Qubes OS. And that makes sense to a degree, but try to find alternatives to the software, you may be surprised to find software like it that does work on Linux.
- Skill Requirement - Knowing Linux and the terminal can be very useful to a degree, I say this because you may find that going from Windows/MacOS to Qubes can have a more straightforward learning curve than if you are already on Linux, simply because things on Qubes are done slightly differently. Even so I would argue its a level playing field.


I am not going to make the list too long because the reality is, it doesn't matter what I put on there, you most likely already have your mind made up one way or another.
Looks too difficult to take on or overkill for what you need? I respect that although I would still encourage to try it out and see it through.
If privacy is something you value (and you really should) then having a reasonably secure operating system is a great way to start out (because privacy doesn't exist without security).
