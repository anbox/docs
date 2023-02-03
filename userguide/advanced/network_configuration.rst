Network Configuration
=====================

Anbox provides configuration options to change the network configuration of the
Android container and the network bridge used to let the container talk to networks
the host is connected to.

Network bridge
--------------

By default anbox creates a network bridge called `anbox0`
which will forward traffic from the Android container to the network the machine
Anbox is running on is connected to.

The default configuration of the bridge looks like this:

.. code-block:: text

    anbox0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.250.1  netmask 255.255.255.0  broadcast 0.0.0.0
        inet6 fe80::743a:9ff:fefd:96ac  prefixlen 64  scopeid 0x20<link>
        ether 76:3a:09:fd:96:ac  txqueuelen 1000  (Ethernet)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 113  bytes 17698 (17.6 KB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

To change the configuration of the bridge the following configuration options exists
on the snap:

* `bridge.address`: Address of the bridge (default: `192.168.250.1`)
* `bridge.netmask`: Netmask of the bridge (default: `255.255.255.0`)
* `bridge.network`: Network used by bridge (default: `192.168.250.1/24`)
* `bridge.nat.enable`: Enable or disable NAT support on the bridge (default: `true`)

The values of the configuration items are not validated. If incorrect values are
supplied the bridge may get incorrectly configured and the container wont be able
to access any outside network or will fail to start.

All configuration items can be changed with the `snap` command. For example:

.. code-block:: text

    $ snap set anbox bridge.address=192.168.250.2

Container network configuration
-------------------------------

When the bridge configuration is altered the configuration of the container needs to
be adjusted as well. The following configuration options exist for this:

* `container.network.address`: Address of the container (default: `192.168.250.2`)
* `container.network.gateway`: Gateway the container should use (default: `192.168.250.1`)
* `container.network.dns`: DNS server the container should use (default: `8.8.8.8`)

All configuration items can be changed with the `snap` command:

.. code-block:: text

    $ snap set anbox container.network.address=192.168.250.10
