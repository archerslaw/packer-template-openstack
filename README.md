# Huaweicloud packer template example for OpenStack Platform 
Building the private image from OpenStack instance with Packer tool.
Currently it supports packer version ≥ v1.2.3.

# Install
Download the correct packer from you platform from https://www.packer.io/downloads.html
Install packer according to the guide from https://www.packer.io/docs/installation.html
OpenStack Builder helps from https://www.packer.io/docs/builders/openstack.html

# How to excute Packer
$ sudo packer build packer-template-example/huaweicloud.json
e.g: $ sudo packer build packer-template-centos-updating/packer-template-centos-updating.json
