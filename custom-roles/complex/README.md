# Complex Deployment
Set of templates to deploy a separate network role on a host.

>NOTE: update network-environment.yaml to reference the absolute path of the configuration files in nic-configs

## Architecture


## Features

* Fernet Tokens for KeyStone
* HIPE Compile for RabbitMQ
* Distributed Virtual Router - DVR


## Assumptions

This deployment assumes that the services exist on the ospservices role. This matters because we specify ExtraConfig as OSPServicesExtraConfig




## Prerequisites

### Custom Role Flavor
A flavor for the new role needs to be created and associated with node.

Create the flavor:
```bash
openstack flavor create --id auto --ram 4096 --disk 40 --vcpus 1 ospservices
openstack flavor set  --property "capabilities:boot_option"="local" --property "capabilities:profile"="ospservices" ospservices
openstack flavor list
```

Associate the flavor with the node:
```bash
ironic node-update ospservices-node-01 add properties/capabilities='profile:ospservices,boot_option:local'
openstack overcloud profiles list
```

### Fernet Tokens

```bash
cd ~/
source stackrc

sudo keystone-manage fernet_setup --keystone-user keystone --keystone-group keystone
sudo tar -zcf keystone-fernet-keys.tar.gz /etc/keystone/fernet-keys

upload-swift-artifacts -f keystone-fernet-keys.tar.gz
```


## Deploy

```bash
openstack overcloud deploy --templates /usr/share/openstack-tripleo-heat-templates \
    -r /home/stack/overcloud/custom_roles.yaml \
    --ntp-server 216.239.35.4 \
    --control-scale 1 --compute-scale 1 \
    --neutron-tunnel-types vxlan --neutron-network-type vxlan \
    --control-flavor control \
    --compute-flavor compute \
    -e /home/stack/overcloud/network-isolation.yaml \
    -e /home/stack/overcloud/network-environment.yaml \
    -e /home/stack/overcloud/low-memory-usage.yaml \
    -e /home/stack/overcloud/ospservices-flavor.yaml
    -e /home/stack/overcloud/fernet.yaml
```