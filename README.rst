Accelerated Antimalignant Sandboxed Execution Environment
=========================================================
      A massaged Fork of the F-Secure SEE Project
      Experimental Dirtpit for malware analysis in
        Isolated Spaces
=========================================================

:Source: https://github.com/dverbeeck/aasee
:ORIGINAL Documentation via F-Secure SEE Project: https://see.readthedocs.io
:Download F-Secure SEE: https://pypi.python.org/pypi/python-see

\
Introduction
------------

AASEE is a framework for building test automation in secured Environments.

The Sandboxes, provided via libvirt, are customizable allowing high degree of flexibility. Different type of Hypervisors (Qemu, VirtualBox, LXC) can be employed to run the Test Environments.

Plugins can be added to a Test Environment which provides an Event mechanism synchronisation for their interaction. Users can enable and configure the plugins through a JSON configuration file.


Audience
--------

AASEE is for automating tests against unknown, dangerous or unstable software tracking its activity during the execution.

AASEE is well suited for building modular test platforms or managing executable code with a good degree of isolation.

AASEE allows to write sandboxed tests both for quick prototyping and for running on production environment.

Installation
------------

AASEE is available as Python package on the Python Package Index (PyPI).

It's user's responsibility to install and setup the hypervisors intended to be controlled with AASEE and the possible dependencies and subsystems used by the selected image providers.

Please refer to the documentation to see how to setup and configure each hypervisor.

Supported hypervisors
---------------------

AASEE is build on top of libvirt's APIs, therefore all hypervisors supported by libvirt can be controlled through AASEE.

AASEE comes with a basic support for QEMU, VirtualBox and LXC, to add more hypervisor or customize the basic ones see the code contained in see/context.

Image providers
---------------

AASEE uses a system of pluggable providers to retrieve disk images from arbitrary sources and make them available to AASEE.

AASEE bundles providers for `LibVirt storage pools <https://libvirt.org/storage.html>`_ and `OpenStack Glance <https://docs.openstack.org/developer/glance/>`_ as well as a dummy provider implementation, to add more providers see the code contained in see/image_providers.

Principles
----------

AASEE is an event-driven, plugin-based sandbox provider for synchronous and asynchronous test flow control.

::


                                                                      +----------+
                                                                      |          |
                                                              +-------| SEE Hook |
                                                              |       |          |
                                                              |       +----------+
                  +---------+-------+       +---------+       |       +----------+
                  |                 |       |         |       |       |          |
    User -------> | AASEE  |-------| Sandbox |-------+-------| AASEE Hook |
                  |                 |       |         |       |       |          |
                  +-----------------+       +---------+       |       +----------+
                                                              |       +----------+
                                                              |       |          |
                                                              +-------| SEE Hook |
                                                                      |          |
                                                                      +----------+

A SEE Environment encapsulates all the required resources acting as a handler for the User. The Sandbox is controlled by the Hooks which act as plugins, Hooks communicate and co-ordinate themselves through Events.

Each Hook has direct access to the Sandbox which exposes a simple API for it's control and libvirt's APIs for more fine grained control.

Links
-----

Libvirt project page.

https://libvirt.org

Presentation on PyCon Finland 2015.

https://www.youtube.com/watch?v=k185OMivqbQ
