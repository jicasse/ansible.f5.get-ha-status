ansible.f5.get-ha-status
=========

This role is accessing f5 bigip appliances and doing the following : 
- gatering some facts regarding devices and devices groups
- setting up facts which include appliance ha status

At the end three additional facts should have been set :
> f5_ha_status

At the end this fact will contain 'standalone' or 'cluster' as value.

> f5_failover_state

At the end this fact will contain 'active' or 'passive' as value.

> f5_device_groups

This variable is the list of device groups defined on the bigip.

This is useful on f5 as a lot of changes should not be done on both appliances. 
The idea is to use the fact as condition to run a task in others roles. 

As an example, imagine you have have a role changing some datagroups content.
To do this change in a correct f5 way, you do the change on active member for example and then synchronizing the configuration from active device to the passive one.
The objective of the facts defined by this role is to use them as conditions in others roles to do these kind of changes.


Requirements
------------

- Ansible 2.7
- BIGIP minimum version : 12.X
- f5-sdk python library

Role Variables
--------------

Here are the variables needed to have this role working correctly : 

> f5_delegate_to

This variable shouls always defined to 'localhost'
The variable is already defined in the default variables. 

> f5_validate_certs

This variable is used to validate certificate used on f5 bigip system when accessing bigip api.
By default this variable is set to 'no' in the default variables as when using this role in lab environnment it's not necessary to validate the certs.
In production environnement override this variable to 'yes'

> f5_user

This variable contains the username used to access the api and gathers facts.

> f5_passwd

This variable contains the password of the user.
Use ansible vault to encrypt this password.

> f5_host

This variable contains the hostname or ip address of the bigip you need to access.


Dependencies
------------

N/A

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: f5_grp
      gather_facts: no
      roles:
         - ansible.f5.get-ha-status

License
-------

BSD

Author Information
------------------

Jimmy Casse
