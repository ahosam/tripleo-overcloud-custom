# Networking Role
Set of templates to deploy a separate network role on a host.

>NOTE: update network-environment.yaml to reference the absolute path of the configuration files in nic-configs

## Prerequisites
A flavor for the new role needs to be created and associated with node.

Create the flavor:
```bash
openstack flavor create --id auto --ram 4096 --disk 40 --vcpus 1 networker
openstack flavor set  --property "capabilities:boot_option"="local" --property "capabilities:profile"="networker" networker
```

Associate the flavor with the node:
```bash
ironic node-update networker add properties/capabilities='profile:networker,boot_option:local'
openstack overcloud profiles list
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
    -e /home/stack/overcloud/networker-flavor.yaml
```