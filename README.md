## Repository for setting up elixir federation via ansible

This role was succesfully used on Red Hat OpenStack Plattform 10 and RHEL/CentOS, be careful if using with other distros

* Make sure to locate your sp-cert.pem and sp-key.pem as shibboleth.tgz in the /files directory
* Make sure to use your entity-id in files/etc/shibboleth/shibboleth2.xml
* You might want change the files/etc/yum.repos.d/shibboleth.repo for your distro
* Adjust the vars/main.yml according to your controller-names/ips
* Add your controller-hosts ips to the hosts file
* Please also have a look at the manual setup guide for the elixir federation (especially https://github.com/deNBI/cloud-docs/blob/master/aai/src/docs/asciidoc/elixir-aai-keystone.adoc#create-federated-resources). The OpenStack specific part (domain creation, mapping etc.) is not part of the playbooks in the moment.
