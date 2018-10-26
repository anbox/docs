Install Anbox
=============

To install Anbox your system need to support `snaps <https://snapcraft.io>`_. We
do not officially support any other distribution method of Anbox at the moment
but there are community made packages for various distributions (e.g. Arch Linux).
However please keep in mind that the Anbox project can give not support them
and its solely in the responsibility of the community packager to keep up with
upstream development and update the packaging to any new changes. Please feel
free to report still any bugs you encounter as they may not be related to the
packaging.

If you don't know about snaps yet head over to `snapcraft.io <https://snapcraft.io/>`_
to get an introduction of what snaps are, how to install support for them on your
distribution and how to use them.

The installation of Anbox consists of two steps.

 1. Install necessary kernel modules
 2. Install the Anbox snap

Install kernel modules
^^^^^^^^^^^^^^^^^^^^^^

To install the necessary kernel modules, please read :doc:`install_kernel_modules`.

After correct installation you should have two new nodes in your systems `/dev` directory:

.. code-block:: text

    $ ls -1 /dev/{ashmem,binder}
    /dev/ashmem
    /dev/binder


Install the Anbox snap
^^^^^^^^^^^^^^^^^^^^^^

The second step will install the Anbox snap from the store and will give you
everything you need to run the full Anbox experience.

Installing the Anbox snap is very simple:

.. code-block:: text

    $ snap install --devmode --beta anbox

If you didn't logged into the Ubuntu Store yet, the `snap` command will
ask you to use `sudo snap ...` in order to install the snap:

.. code-block:: text

    $ sudo snap install --devmode --beta anbox

At the moment we require the use of `--devmode` as the Anbox snap is not
yet fully confined. Work has started with the upstream `snapd` project to
get support for full confinement.

As a side effect of using `--devmode` the snap will not automatically update.
In order to update to a newer version you can run:

.. code-block:: text

    $ snap refresh --beta --devmode anbox

Information about the currently available versions of the snap is available
via:

.. code-block:: text

    $ snap info anbox

Available snap channels
^^^^^^^^^^^^^^^^^^^^^^^

Currently we only use the beta and edge channels for the Anbox snap. The edge
channel tracks the latest development is always synced with the state of the
master branch on github. The beta channel is updated less frequently to provide
a more stable and bug free experience.

Once proper confinement for the Anbox snap exists we will also start using the
candidate and stable channels.

Uninstall Anbox
===============

If you want to remove Anbox from your system you first have to remove the snap:

**NOTE:** By removing the snap you remove all data you stored within the snap
from your system. There is no way to bring it back.

.. code-block:: text

    $ snap remove anbox

Once the snap is removed you have to remove the installed kernel modules as well:

.. code-block:: text

    $ sudo apt install ppa-purge
    $ sudo ppa-purge ppa:morphis/anbox-support


Once done Anbox is removed from your system.
