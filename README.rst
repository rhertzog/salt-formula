====
salt
====

Yes, Salt can Salt itself!

.. note::

    See the full `Salt Formulas installation and usage instructions
    <http://docs.saltstack.com/en/latest/topics/development/conventions/formulas.html>`_.

Available states
================

.. contents::
    :local:

``salt.minion``
---------------

Install a minion

``salt.master``
---------------

Install a master.

``salt.syndic``
---------------

Install a syndic.

``salt.cloud``
---------------

Install salt cloud.

``salt.ssh``
------------

Install salt-ssh with roster file.
Configure pillar data under salt:ssh_roster to feed the template.

``salt.standalone``
------------

Install a minion and configure it in `standalone mode
<docs.saltstack.com/en/latest/topics/tutorials/standalone_minion.html>`_.

``salt.pkgrepo``
----------------

Enable the official saltstack package repository in order to always
benefit from the latest version. This state currently only works on Debian
and Ubuntu, and aims to implement the `installation recommendations of the
official documentation
<http://docs.saltstack.com/en/latest/topics/installation/index.html#platform-specific-installation-instructions>`_.

``salt.pkgrepo.absent``
-----------------------

Undo the effects of ``salt.pkgrepo``.

``Configuration``
=================
Every option available in the templates can be set in pillar. Settings under 'salt' will be overridden by more specific settings under ``salt['master']``, ``salt['minion']`` or ``salt['cloud']``

::

    salt:
      ret_port: 4506
      master:
        user: saltuser
        ...
      minion:
        user: saltuser
        ...
      cloud:
        providers: ec2
        ...

``Extending``
=============
Additional templates can be added by the user under salt/files/minion.d and master.d. This might be useful if, for example, a recently-added configuration option is not yet provided by the default template.

``Vagrant``
===========

Executing the provided `Vagrantfile <http://www.vagrantup.com/>`_  will create a Ubuntu 14.04 VM, add the default Saltstack Repository and install the current stable version.

The folders inside the VM will be set up in a way that enables you to simply execute 'sudo salt "*" state.highstate' to apply the salt formula to the VM, using the pillar.example config. You can check /etc/salt/ for results.

Remember, you will have to run ``state.highstate`` or ``state.sls salt.(master|minion|cloud)`` manually.
