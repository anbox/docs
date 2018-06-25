Install applications
====================

Installation applications into the Android container provided by Anbox
we currently use the sideloading functionality Android provides. For
this you need to have the Android Debug Bridge (ADB) installed on your
host system. See the `Android documentation <https://developer.android.com/studio/command-line/adb>`_
for details.

If you're running Ubuntu or Fedora you can install ADB from the package archive:

.. code-block:: text

    # On Ubuntu
    $ sudo apt install android-tools-adb

    # On Fedora
    $ sudo dnf install android-tools

Once ADB is installed you're ready to install Android applications.

Anbox does not provide any functionality to retrieve Android applications.
You need to get them from a source on the internet. Once you have the APK
package for the application you can install it into the Android container
with the following command:

.. code-block:: text

    $ adb install my-app.apk

If the Anbox container is not running yet you can start it with loading
the application manager application:

.. code-block:: text

    $ anbox.appmgr


