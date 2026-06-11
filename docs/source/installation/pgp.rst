Verifying with PGP
==================

This next part is very important IMO, you should verify the ISO you
aquired is not corrupted, otherwise you will be doing everything right on a broken
system.

I will be the first to admit, Qubes OS `Verify PGP <https://doc.qubes-os.org/en/latest/project-security/verifying-signatures.html>`_
is very well documented and with patience you can follow it and get the result you want.
So I will encourage you to try and follow their documentation for this, not because it will change but because
the way I write will be simplified which the rest of the world's man pages and documentation will won't.


Therefore you should try to follow their documentation, but if it is too overwhelming, don't worry.
I will provide the steps with a simple explanation which you can check with their guide to make
sure you understand (and trust) what I am telling you to do. 

Acquire OpenPGP compliant Program
---------------------------------

If you are on Linux, open a terminal and use the gpg2 command.
If you don't have it installed on your system, use your package manager and install it.

If you are on macOS you will need to install `GPG Suite <https://www.gpgtools.org/>`_.

If you are on Windows, you will need to install `Gpg4win <https://www.gpg4win.org/download.html>`_.

.. note::
   gpg2 should be the command you use, if it doesn't work, use gpg instead, no worries.

Import and Authenticate Qubes Master Signing Key
------------------------------------------------

I notice as I write these headings, just how mission impossible this may sound to some, but the
reality is that the steps are quite easy and the concepts do make sense overtime.
The same way algebra makes sense (or not) after some time studying it.

That being said, the Qubes Master Signing Key is the 'ultimate root of trust for the Qubes OS Project'.
So we want to be certain that we have the correct key because it will verify everything else for us.

If you look at the Qubes OS documentation, there are various ways of obtaining the key.

Fedora has the `distribution-gpg-keys <https://github.com/xsuchy/distribution-gpg-keys>`_ package:

.. code-block:: bash

   dnf install distribution-gpg-keys
   gpg2 --import /usr/share/distribution-gpg-keys/qubes/*

Debian may already have in their keyring so you can fetch it with GPG:

.. code-block:: bash

   gpg2 --fetch-keys https://keys.qubes-os.org/keys/qubes-master-signing-key.asc

You can also get it from a public keyserver:

.. code-block:: bash

    gpg2 --keyserver-options no-self-sigs-only,no-import-clean --keyserver hkp://keyserver.ubuntu.com
    --recv-keys 0x427F11FD0FAA4B080123F01CDDFA1A3E36879494

Or you can download it from various sources as a
`file <https://keys.qubes-os.org/keys/qubes-master-signing-key.asc>`_ and then import the file:

.. code-block:: bash

    gpg2 --import /<PATH_TO_FILE>/qubes-master-signing-key.asc


Whichever way you choose to aquire the key, you will need to verify it, because it can be forged.
The easiest way is to look at the fingerprint which is a string of 40 alphanumeric characters:

.. `427F 11FD 0FAA 4B08 0123  F01C DDFA 1A3E 3687 9494` 

But, how can you be so sure this is the correct fingerprint?
Are you trusting me just because I am on the internet and therefore am trustworthy?
You shouldn't. You should verify things yourself. Compare this fingerprint with at least 1 other source.

This is really important because you are about to set the trust level to "ultimate", that way it
can verify everything other key that is signed by the Master Key.

.. code-block:: bash

    gpg2 --edit-key 0x427F11FD0FAA4B080123F01CDDFA1A3E36879494

    gpg> fpr

    gpg> trust

    5

    y

    gpg> q

Boom done, you will obviously see more text but the commands above will set to trust the key you obtained.
To make sure everything is okay do the following:

.. code-block:: bash

   gpg2 -k "Qubes Master Signing Key"

You should see the "ultimate" trust level applied.
If you don't try the instructions again, maybe with a key from a different source.

You would think that is all you need to do for this section.
It's not. That's probably why people hate this part and want to skip over. I get it.
But don't do that.

Import and Authenticate Qubes Release Signing Key
-------------------------------------------------

We now have the Qubes Master Signing Key, but why?
Well if you noticed below the blue download buttons on the Qubes OS website, there were other 
options, other files that we could download. Those files will be used to verify the authenticity
of the ISO image.

First, let's get the Release Signing Key, or RSK.
Make sure you get the correct RSK for the version you downloaded and the method which you downloaded
the ISO, torrent or otherwise.

Right click the button on the website and 'Save link as..'
Once you downloaded the RSK as a file on your system, import it with GPG:

.. code-block:: bash

   gpg2 --keyserver-options no-self-sigs-only,no-import-clean --import ./qubes-release-X-signing-key.asc

.. warning::

   STOP! What is X? That is the version number, which won't be X so change it to the correct value
   when you enter this command. 

Now you have imported it, verify that it is signed with the Master Key:

.. code-block:: bash

   gpg2 --check-signatures "Qubes OS Release X Signing Key"

Check that the line with the sig! prefix states that the QMSK has signed this key.

Finally we will check that the RSK is in the keyring:

.. code-block:: bash

   gpg2 -k "Qubes OS Release X Signing Key"

The trust level should be "full" or higher. If not, do the steps again.

Verify Qubes ISOs
----------------------------------------------

Are we nearly there yet? Almost!

We just need to verify the ISO.
There are two options, which correspond to the two files left on the downloads page.
Cryptographic has values and Detached GPG signatures.
Which to do? Up to you! I will note which is "quicker" so you can hurry up to more interesting bits.

.. note::

   Both methods are equally secure, so doing both methods is not necessary.

Verify Detached PGP signatures
------------------------------

This method is quicker than the other one so if you don't have any patience, follow along.

Download the Detached PGP Signature file. (Right-click -> 'Save link as')

Ensure both files are in the same directory. Navigate to that directory and type this command:

.. code-block:: bash

   gpg2 -v --verify Qubes-RX-x86_64.iso.asc Qubes-RX-x86_64.iso

Find the line that says: Good signature from "Qubes OS Release X Signing Key"

That is all you need to do! You can move on to the next page and be confident you are downloading an authentic ISO image.

Verify Cryptographic hash values
--------------------------------

Want to check by verifying the cryptographic hash values instead? 
It isn't more secure or anything, slightly longer than the other method, but up to you!


Download the Cryptographic hash values file. (Right-click -> 'Save link as')
The file will end in .DIGESTS and contains the output of several hash functions on the ISO.
Any computer can generate these hashes which makes this quite convenient.

Go ahead and open the file with any text editor.
Looks cryptic doesn't it? Don't worry we won't compare it ourselves, we have software for that.

The file has the following hashes (presumably):
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

- MD5
- SHA-1
- SHA-256
- SHA-512

We will use the \*sum command to verify for each hash:

.. code-block:: bash

   md5sum -c Qubes-RX-x86_64.iso.DIGESTS
   sha1sum -c Qubes-RX-x86_64.iso.DIGESTS
   sha256sum -c Qubes-RX-x86_64.iso.DIGESTS
   sha512sum -c Qubes-RX-x86_64.iso.DIGESTS

The OK response tells us that the hash value for that function matches.
(Ignore the improperly formatted lines, doesn't matter)

You can also use openssl to compute each hash value, then compare to the contents of the digest file:

.. code-block:: bash

   openssl dgst -md5 Qubes-RX-x86_64.iso
   openssl dgst -sha1 Qubes-RX-x86_64.iso
   openssl dgst -sha256 Qubes-RX-x86_64.iso
   openssl dgst -sha512 Qubes-RX-x86_64.iso

(You should be able to see that the outputs match the values from the DIGESTS file)

"Is that it?!" I hear you screaming internally.
One more command and you are done, promise.

See this is all cool except an attacker could also replace these hashed values along with the malicious
ISO, so what then?

Simple, we verify the authenticity with GPG, since the DIGESTS file is a clearsigned PGP file.

.. code-block:: bash

   gpg2 -v --verify Qubes-RX-x86_64.iso.DIGESTS

Find the line that says: Good signature from "Qubes OS Release X Signing Key"

That is it!!! You can move on to the next page and be confident you are downloading an authentic ISO image.
