# Tripleo Overcloud Custom
A collection of heat templates to deploy different OpenStack overcloud scenarios using TripleO

## Scenarios:

### Networking role
Set of templates to deploy a separate network role on a host.

[Networking Role](custom-roles/networking)

### Services based role
Set of templates to deploy all the non-pacemaker controlled services on a host.

[Services Role](custom-roles/services)

### Complex Deployment with Services based role
Set of templates to deploy all the non-pacemaker controlled services on a host.

[Complex](custom-roles/complex)

## Troubleshooting:

* Reseting Nodes in Ironic
* Deleting Failed Deployments
* Tracking down failures in Minstral
* [VM Boot Failures](troubleshooting/VM_boot_failures.md)