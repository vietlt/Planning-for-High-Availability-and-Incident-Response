# Infrastructure

## AWS Zones
Identify your zones here
Zone 1 : US-EAST-2
Zone 2 : US-WEST-1
## Servers and Clusters

### Table 1.1 Summary
| Asset             | Purpose               | Size        | Qty   | DR                                                      |
|------------       |-------------------    |-------------|-------|---------------------------------------------------------|
| VPC               | Virtual Network       | -           |   2   | 2 zones, 1 VPC each zone for DR purpose                 |
| EC2 instances     | App Servers           | t3.micro    |   6   | 2 zones, 3 instances each zone for DR purpose           |
| EC2 keypair       | SSH key to access EC2 | -           |   2   | 2 zones, 1 keypair each zone for DR purpose             |
| EKS               | Kubernetes Clusters   | t3.medium   |   4   | 2 zones, 2 nodes each zone for DR purpose               |
| Prometheus Grafana| Monitoring System     | -           |   2   | 2 zones, 2 nodes each zone for DR purpose               |
| S3 bucket         | Bucket for terraform  | -           |   2   | 2 zones, 1 bucket each zone for DR purpose              |
| ALB               | App Load balancer     | -           |   2   | For HA/DR purpose                                       |
| RDS               | Backend Database      | db.t3.micro |   2   | 1 cluster 2 node on zone 1                              |
| RDS               | Backend Database      | db.t3.micro |   2   | 1 cluster 2 node replicated from zone 1 to zone 2       |

### Descriptions
- VPC: Networking for infra
- EC2 instances: Virtual Machine to host app
- EC2 keypair:  SSH key for access instances
- EKS: K8s cluster to host prometheus and grafana
- Prometheus Grafana: Monitor application
- S3 bucket: Store tfstate file
- ALB: Load balancing for HA/DR purpose
- RDS: SQL db cluster for storing data

## DR Plan
### Pre-Steps:
- Spin up the infra
- Go through the infra to make sure DR is up and running with proper setting

## Steps:
- DB: Promote replicate cluster RDS on DR site in case of failover
- Traffic: Reroute traffic to DR site in case of failover