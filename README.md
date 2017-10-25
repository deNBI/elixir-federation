## Repository for setting up elixir federation via ansible

This role was succesfully used on Red Hat OpenStack Plattform 10 and RHEL/CentOS, be careful if using with other distros

* Make sure to locate your sp-cert.pem and sp-key.pem as shibboleth.tgz in the /files directory
* Make sure to use your entity-id in files/etc/shibboleth/shibboleth2.xml
* You might want change the files/etc/yum.repos.d/shibboleth.repo for your distro
* Adjust the vars/main.yml according to your controller-names/ips
* Add your controller-hosts ips to the hosts file
