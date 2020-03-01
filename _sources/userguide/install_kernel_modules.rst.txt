Install Kernel Modules
======================

Install with DKMS
^^^^^^^^^^^^^^^^^

In order to support the mandatory kernel subsystems ashmem and binder for the
Android container you have to install two
`DKMS <https://en.wikipedia.org/wiki/Dynamic_Kernel_Module_Support>`_
based kernel modules. The source for the kernel modules is maintained by the
Anbox project `here <https://github.com/anbox/anbox-modules>`_.

At the moment we only have packages prepared for Ubuntu in a PPA on Launchpad.
If you want to help to get the packages in your favorite distribution please
come and :doc:`talk to us <../community/channels>` or submit a PR with the distribution
specific packaging.

Install DKMS package from PPA
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. note::
    Starting with Ubuntu 19.04 binder and ashmem are now build with the standard
    Ubuntu kernel (>= 5.0) and you don't have to install the modules from the PPA
    anymore.

In order to add the PPA to your Ubuntu system please run the following commands:

.. code-block:: text

    $ sudo add-apt-repository ppa:morphis/anbox-support
    $ sudo apt update
    $ sudo apt install linux-headers-generic anbox-modules-dkms

.. note::
    In case `add-apt-repository` is missing, install it via:

.. code-block:: text
    
    $ sudo apt install software-properties-common

These will add the PPA to your system and install the `anbox-modules-dkms`
package which contains the ashmem and binder kernel modules. They will be
automatically rebuild every time the kernel packages on your system update.

.. note::
    Please install the corresponding header package for your running kernel, if
    you're not using the default one.

After you installed the `anbox-modules-dkms` package you have to manually
load the kernel modules. The next time your system starts they will be
automatically loaded.

.. code-block:: text

    $ sudo modprobe ashmem_linux
    $ sudo modprobe binder_linux

Now you should have two new nodes in your systems `/dev` directory:

.. code-block:: text

    $ ls -1 /dev/{ashmem,binder}
    /dev/ashmem
    /dev/binder


Install with in-tree modules
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Android ashmem and binder modules are in linux kernel tree. So it's possible to
build them as in-tree modules.

You can enable them, by looking at the following configuration,

* https://github.com/torvalds/linux/blob/master/drivers/android/Kconfig
* https://github.com/torvalds/linux/blob/master/drivers/staging/android/Kconfig

However if you don't want these modules to be built-in for your kernel, you can apply
the following patches, to build them as modules.

* https://salsa.debian.org/kernel-team/linux/blob/master/debian/patches/debian/android-enable-building-ashmem-and-binder-as-modules.patch
* https://salsa.debian.org/kernel-team/linux/blob/master/debian/patches/debian/export-symbols-needed-by-android-drivers.patch

Debian has enabled these modules since kernel 4.17.3. So you don't need to bother
how to install. Currently kernel 4.17.3 and above are only available in
Debian `Unstable <https://packages.debian.org/sid/linux-image-4.17.0-1-amd64>`_.

Other distributions are welcome to take these patches and enable them by default.
