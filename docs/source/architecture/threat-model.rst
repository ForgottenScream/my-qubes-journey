Threat Model
============

Before building a Qubes OS architecture, you should develop a basic threat model.
This does **not** need to be perfect, and it will evolve over time as you better understand your needs. 
Think of it as an ongoing process rather than a single task you complete once.

Identify Your Assets
--------------------

Start by identifying the things you want to protect. These are your **assets**.

Examples include:

- personal documents  
- credentials and authentication secrets  
- financial information  
- private conversations  
- photos and memorabilia  
- work-related data  
- anything you value and do not want exposed or lost  

Assets can be digital *or* physical, and their value may change depending on context.

Define Potential Adversaries
----------------------------

“Adversary” might sound dramatic, but in security it simply means **anyone or anything that could compromise your assets**, intentionally or unintentionally.

Typical adversary categories include:

**Government or State-Level Actors**  
Although highly unlikely for most people, these actors have significant resources and capabilities.
They matter mainly if you have a very specific risk profile (journalism, research, activism, sensitive industries).

**Tech Companies and Data Harvesters**  
A far more common concern. Large companies collect massive amounts of telemetry, behavioural data, and metadata.
Many users move toward systems like Qubes partly to limit data collection and reduce the attack surface.

**Cybercriminals**  
Phishing, ransomware, account takeover attempts, identity theft, and opportunistic attacks fall into this category.
This is the “practical reality” for most users.

**Other Individuals**  
This covers everything from someone shoulder-surfing your screen, to someone physically accessing your device, to misuse by somebody you share a system with.
Physical security and compartmentalisation matter here.

**Your Future Self**  
Believe it or not, accidental self-harm (deleting files, breaking systems, misconfigurations) is a common adversary.
Compartmentalisation helps reduce the damage when you inevitably make mistakes.

Modeling Risk
-------------

Once you understand **what** you want to protect and **who** you want to protect it from, the next step is to think about **how likely** each threat is and **how much damage** it could cause.

You don't need a complex scoring system. A simple mental model works:

- What is the likelihood? (low / medium / high)  
- What is the impact if it happens? (low / medium / high)  

.. note:: Focus your attention on threats that are **high-impact** even if they are low-probability. This helps avoid over-engineering while still being realistic.

Visualising the System
----------------------

Once you have a sense of your assets and risks, it's helpful to **draw your environment on paper**.
Visualisation makes abstract concepts concrete and helps you understand what Qubes OS actually offers.
You will most likely have to restart the drawing multiple times, but to start you off, think of different aspects of your life that do not mix.
Work, personal life, government related maintenance, fun hobbies or activities.
These kind of isolated factors of your life exist digitally too, so take note and when we start drawing a model similar to the one below, you will know what to fill in and where.

.. figure:: /_static/qubes-trust-level-architecture.png
   :width: 80%
   :align: center

   Example of a trust-based architecture within Qubes OS.
