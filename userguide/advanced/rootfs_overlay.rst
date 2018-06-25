Android rootfs overlay
======================

Anbox provides support to allow customizing the used Android root filesystem. This
is useful for development and debugging purposes but also to add additional functionality
to the Android root filesystem Anbox ships by default.

Overlaying the default Android filesystem is a powerful feature but needs to be used
carefully as it may introduce bugs and unwanted behavior if used incorrectly.

The following steps will provide an overview of the basic steps to setup the rootfs
overlay (which is disabled by default) and how to use it.

Enable Android rootfs overlay
-----------------------------

The rootfs overlay support is hidden behind a configuration option of the snap. You
enable it by running the following commands:

.. code-block:: text

    $ snap set anbox rootfs-overlay.enable=true
    $ snap restart anbox.container-manager

Now the container manager is running and the overlayed rootfs exists within the snap
mount namespace at `/var/snap/anbox/common/combined-rootfs`. To verify everything
is setup correctly you can inspect the `combined-rootfs` this way:

.. code-block:: text

    $ sudo snap run --shell anbox.container-manager
    # ls -alh /var/snap/anbox/common/combined-rootfs

Extend Android rootfs with additional files
-------------------------------------------

Now that the overlay is setup you can start using it. For that you can put any files
into the directory `/var/snap/anbox/common/rootfs-overlay` and they will show up in
the Android root filesystem used by Anbox.

Once you placed files inside the overlay directory you have to ensure all files have
the right uid/gid assigned. Anbox uses a user namespace where all uid/gid are shifted
to the unprivileged base UID `100000`. This means that UID `100000` on your host system
will be UID `0` inside the Android container.

The most common case is that all files need to be owned by root inside the Android container.
For that you can simply recursively change the UID/GID of all files in the overlay directory
with the following command:

.. code-block:: text

    $ sudo chown -R 100000:100000 /var/snap/anbox/common/rootfs-overlay
