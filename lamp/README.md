##LAMP base image##
this is the minimum docker image for drupal deployment.
This image is available from the [drunomics automated build repository](https://registry.hub.docker.com/u/drunomics/lamp/)

This images is built using the following ansible roles (and their dependencies):
* [drunomics.base](https://github.com/drunomics/ansible-role-base)
* [drunomics.ssh](https://github.com/drunomics/ansible-role-ssh)
* [drunomics.lamp](https://github.com/drunomics/ansible-role-lamp)
* [drunomics.nullmailer](https://github.com/drunomics/ansible-role-nullmailer)
* [drunomics.maildev-apache](https://github.com/drunomics/ansible-role-maildev-apache)
* [kosssi.composer](https://github.com/kosssi/ansible-role-composer)
* [drunomics.drush](https://github.com/drunomics/ansible-role-drush)

(c) 2015 drunomics GmbH. /  MIT License 