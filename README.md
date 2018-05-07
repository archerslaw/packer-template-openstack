# Huaweicloud packer template example for OpenStack Platform 
Building the private image from OpenStack instance with Packer tool.
Currently it supports packer version ≥ v1.2.3.

## Install
- Download the correct packer from you platform from https://www.packer.io/downloads.html
- Install packer according to the guide from https://www.packer.io/docs/installation.html
- OpenStack Builder helps from https://www.packer.io/docs/builders/openstack.html

## How to excute Packer
$ sudo packer build packer-template-example/huaweicloud.json
e.g: $ sudo packer build packer-template-centos-updating/packer-template-centos-updating.json

If output similar as following, configurations, you can now start the journey of huaweicloud with packer support
```
   openstack output will be in this color.
   
   ==> openstack: Loading flavor: s2.small.1
       openstack: Verified flacvor. ID: s2.small.1
   ==> openstack: Creating temporary keypair: packer_512fc394-e00d-658f-6620-8f1ae664273a ...
   ==> openstack: Creating temporary keypair: packer_512fc394-e00d-658f-6620-8f1ae664273a
   ==> openstack: Launching server ...
   ==> openstack: Waiting for server to become ready ...
   ==> openstack: Associating floating IP with server ...
   ==> openstack: Waiting for SSH to become available ...
   ==> openstack: Connected to SSH!
   ==> openstack: Provisioning with shell script: /tmp/packer-shell17057963
 ```  
## How to debug
$ sudo exprot OS_DEBUG=1
$ sudo exprot PACKER_LOG_PATH=/var/log/packer.log
   
## Example
### Create a simple image with OS updating.
```
{
  "builders": [{
    "type": "openstack",
    "identity_endpoint": "https://iam.cn-north-1.myhuaweicloud.com/v3",
    "tenant_name": "cn-north-1",
    "domain_name": "xxxxxxx", 
    "username": "yyyyyy",
    "password": "zzzzzz",
    "ssh_username": "root",
    "region": "cn-north-1",
    "image_name": "CentOS-image-updating-powered-by-Packer",
    "instance_name": "CentOS-image-updating-powered-by-Packer".
    "source_image": "dec6b36c-b122-4a20-b4eb-e9c32344b13e",
    "availibility_zone": "cn-north-1b"
    "flavor": "s2.small.1",
    "networks": ["036de9cf-3330-4b14-ba71-62a8ba75c60a"],
    "floating_ip": "**.**.**.**"
  }],
  "provisioners": [{
    "execute_command": "chmod +x {{ .Path }}; {{ .Vars }} sudo -S -E sh '{{ .Path }}'",
    "inline": [
      "yum update -y"
    ],
    "inline_shebang": "/bin/sh -x",
    "type": "shell",
    "skip_clean": true
  }],
  "post-processors": [{
    "strip_path": true,
    "output": "packer-template-centos-updating-result.log",
    "type": "manifest"
  }]
}
```
