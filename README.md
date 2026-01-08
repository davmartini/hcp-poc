# HCP PoC

## Components used

* OpenShift BareMetal Cluster
* RHACM
* OpenShift Virtualization
* OpenShift Data Foundation

## Servers

During this PoC, 9 servers will be used with this repartition :

| DC  | Cluster Name | Server Name | Server role | LUN Storage |
| --- | --- | --- | --- | --- |
| DC01 | ocp-inf01 | ocp-inf01-master01 | master, ODF monitor, ODF storage, worker | 2x512Go |
| DC02 | ocp-inf01 | ocp-inf01-master02 | master, ODF monitor, ODF storage, worker | 2x512Go |
| Arbiter zone | ocp-inf01 | ocp-inf01-master03 | master, ODF monitor | N/A |
| DC01 | ocp-inf01 | ocp-inf01-worker01 | ODF storage, worker | 2x512Go |
| DC02 | ocp-inf01 | ocp-inf01-worker02 | ODF storage, worker | 2x512Go |
| DC01 | ocp-inf01 | ocp-inf01-worker03 | ODF storage, worker | 2x512Go |
| DC02 | ocp-inf01 | ocp-inf01-worker04 | ODF storage, worker | 2x512Go |
| DC01 | ocp-inf01 | ocp-inf01-worker05 | ODF storage, worker | 2x512Go |
| DC02 | ocp-inf01 | ocp-inf01-worker06 | ODF storage, worker | 2x512Go |

## Storage

### Two storage types :
    - Non replicated Local Storage (Managed Etcd Pods)
    - ODF SDS Storage (all other needs) 

### OpenShift Data Foundation (ODF):
    - 16 LUNs on 8 servers (2 per server)
    - 8 LUNs of 512Go per DC
    - RF4 = 8*512/4 = 1To for workload

## Network

### Three underlay VLANs (CIDR)
| VLAN  | CIDR | Role | Usage | BOND | Physical interfaces | DHCP |
| --- | --- | --- | --- | --- | --- | --- |
| VLAN01 | 192.168.1.0/24 | Infrastructure network | OpenShift nodes, SDN traffic, Storage replication | BOND0 | eth0, eth2 | Optionnal |
| VLAN02 | 192.168.2.0/24 | Application network zone 01 | OpenShift worker VMs traffic | BOND1 | eth1, eth3 | Mandatory |
| VLAN03 | 192.168.3.0/24 | Application network zone 02 | OpenShift worker VMs traffic | BOND1 | eth1, eth3 | Mandatory |

## Architecture


