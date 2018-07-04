Software Rendering
==================

In some use cases (e.g. VirtualBox) it can be helpful to run Anbox with
software rendering rather than with the EGL/GL driver provided by the host
operating system. Anbox includes `Swiftshader <https://swiftshader.googlesource.com/SwiftShader/>`_
for this which provides a high-performance CPU based implementation of
OpenGL ES and EGL.

**NOTE:** You need at least revision *114* of the Anbox snap for this.

To enable software rendering in Anbox the only thing you have to do is

.. code-block:: text

    $ snap set anbox software-rendering.enable=true
    $ snap restart anbox.container-manager

**BUT** this will stop any running Anbox process. You have to start Anbox
again afterwards.

Afterwards Anbox will use software rendering. If you want to disable software
rendering it's as simple as

.. code-block:: text

    $ snap set anbox software-rendering.enable=false
    $ snap restart anbox.container-manager
