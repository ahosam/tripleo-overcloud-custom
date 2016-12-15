# Tripleo Overcloud Custom
A collection of heat templates to deploy different OpenStack overcloud scenarios using TripleO

## Scenarios:

### Networking role
Set of templates to deploy a separate network role on a host.

[Networking Role](custom-roles/networking)

These templates assume you are on a virtual environment with the following network layout

```
                                             gateway
                                                +
                                                |
                                                |
                       +-----------+            |
    +----------+       |    ctl    |            |
    | Storage  |       +-----------+            |
    +------------------+eth0 | eth1+------------+
    | Internal |       +-----------+            |
    +----------+                                |
                       +-----------+            |
    +----------+       |    com    |         +----------+
    | Storage  |       +-----------+         | External |
    +------------------+eth0 | eth1|         +----------+
    | Internal |       +-----------+            |
    +----------+                                |
    | Tenant   |                                |
    +----------+                                |
                                                |
                       +-----------+            |
    +----------+       |    net    |            |
    | Tenant   |       +-----------+            |
    +------------------+eth0 | eth1+------------+
    | Internal |       +-----------+
    +----------+
```

### services based role
Set of templates to deploy all the non-pacemaker controlled services on a host.

[Services Role](custom-roles/services)


## Troubleshooting:

* Reseting Nodes in Ironic
* Deleting Failed Deployments
* Tracking down failures in Minstral
* [VM Boot Failures](troubleshooting/VM_boot_failures.md)