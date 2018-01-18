## Repository for setting up elixir federation via ansible

This role was succesfully used on **Red Hat OpenStack Plattform 10 and 
RHEL/CentOS**, be careful if using with other distros

* Make sure to locate your **sp-cert.pem** and **sp-key.pem** as shibboleth_prod
.tgz in the /files directory
* Make sure to use your **entity-id** in files/etc/shibboleth/shibboleth2_prod.xml
* You might want change the files/etc/yum.repos.d/shibboleth.repo for your distro
* Adjust the vars/main.yml according to your **controller-names/ips**
* Add your controller-hosts ips to the hosts file

## Configure OpenStack federated resources

After the initial deployment of the playbooks, OpenStack has to be configured
to use Elixir AAI.

Create an OpenStack domain:

    openstack domain create elixir

Create an identity provider endpoint for Elixir with the correct entity ID:

    openstack identity provider create --remote-id https://login.elixir-czech.org/idp/ elixir

* Check that the trailing slash is present! It **will not work** with out it.

The mapping between the SAML attributes and Keystone is done by rules defined
in a mapping rule file. Create a rule with following content:

    [{
      "local": [
        { "user": { "name": "{0}", "type": "local", "domain": {"name": "elixir"} } }
      ],
      "remote": [{ "type": "REMOTE_USER" }]
    }]

All users are mapped to the elixir domain. The user name is the EPPN (aka "persistent ID")
provided by ELIXIR.

Create a mapping from the rule file:

    openstack mapping create --rules elixir_mapping_rules.json elixir_mapping
    
Create a object protocol:

    openstack federation protocol create mapped --mapping elixir_mapping --identity-provider elixir
    
Keep in mind that mapped is the name of the authentication method referenced
in keystone.conf and also the name of the driver. It must not be changed.

If you now create a user inside keystone using the elixir-id as username and 
assign the user to a project, you now should be able to login using Elixir AAI.