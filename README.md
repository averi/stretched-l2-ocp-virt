# Bridged networking in OCP Virt with Hosted Control Planes and BGP/EVPN

This repository contains the resources required to run OCP Virtualization on top of Hosted Control Planes for Red Hat Openshift in AWS while being able to utilize a routable private IP address space for virtual machines.

This approach is necessary as by design AWS doesn’t allow unauthenticated ARP packets or spoofed MAC addresses, every MAC address that is generated within AWS is authenticated against a list of well known MAC addresses. Generally, these MAC addresses are EC2 instances which have been created via AWS API and/or web UI. This limitation (or security measure, that is) generally prevents any OCP CNV virtual machine to have a routable - to the customer internal network - IP address and forces the use of pod networking. While the above architecture isn’t necessary for container ready workloads which will use OCP ingress to access the cluster, it’d still be relevant for workloads who haven’t yet been modernized.

Provided resources:

1. hub/ - Hub cluster resources (OCP Installer for the hub, HostedCluster, NodePools, MachineConfigs)
1. networking/ - Spoke and data center router(s) (FRR, NAD, NMState)
