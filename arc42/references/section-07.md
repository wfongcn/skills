# Section 7: Deployment View

## Purpose

Describe the infrastructure and deployment of the system. Show how software building blocks map to hardware/infrastructure elements.

## When to Document

- System is deployed to multiple environments
- Infrastructure is complex or distributed
- Deployment affects quality goals (scalability, availability)
- Operations team needs documentation
- Cloud/hybrid infrastructure

## Subsections

### 7.1 Infrastructure

**Content:**
- Hardware/infrastructure overview
- Network topology
- Environment tiers (dev, staging, prod)
- Geographic distribution

**Diagram Elements:**
- Compute resources (servers, containers, functions)
- Data storage (databases, caches, object storage)
- Network elements (load balancers, CDNs, VPCs)
- External services

### 7.2 Deployment Mapping

**Content:**
- How software components map to infrastructure
- Deployment units (containers, VMs, packages)
- Scaling policies
- Resource allocation

## Format

```markdown
## 7. Deployment View

### 7.1 Infrastructure

```
[Infrastructure diagram]
```

| Element | Description | Specs/Configuration |
|---------|-------------|---------------------|
| [Name] | [What it is] | [Size, type, config] |

**Network:**
- VPC/Network configuration
- Load balancer setup
- CDN configuration

### 7.2 Deployment Mapping

| Software Component | Deployment Unit | Infrastructure | Scaling |
|-------------------|-----------------|----------------|---------|
| [Component] | [Docker image/VM] | [Where it runs] | [Policy] |

**Environments:**
| Environment | Purpose | Configuration Differences |
|-------------|---------|--------------------------|
| Development | Local development | Single instance, debug enabled |
| Staging | Pre-production | Production-like, scaled down |
| Production | Live system | Full HA, monitoring, backups |
```

## Input Questions

- What infrastructure is used? (cloud provider, on-premise)
- What are the environment tiers?
- How do software components map to hardware?
- What are the scaling policies?
- What is the network topology?
- Are there geographic considerations?
- What are the backup/disaster recovery procedures?

## Quality Checklist

- [ ] Infrastructure overview is provided
- [ ] All environments are documented
- [ ] Software-to-hardware mapping is clear
- [ ] Scaling policies are documented
- [ ] Network topology is shown
- [ ] Security boundaries are indicated
- [ ] Resource specifications are included

## Common Mistakes

❌ **Outdated information** (infrastructure changes frequently)  
❌ **Missing environment differences**  
❌ **No scaling information**  
❌ **Security gaps** (missing network boundaries)  
❌ **Too much detail** (IP addresses that change)  
❌ **Not considering multi-environment setups**

## Example

```markdown
## 7. Deployment View

### 7.1 Infrastructure

```
                                +------------+
                                |    CDN     |
                                |  CloudFront|
                                +-----+------+
                                      |
                                      v
+----------------+          +------------------+
|   Route 53     |--------->|  ALB (HTTPS)     |
|   (DNS)        |          |  Load Balancer   |
+----------------+          +--------+---------+
                                     |
            +------------------------+------------------------+
            |                        |                        |
   +--------v---------+    +---------v--------+    +---------v--------+
   |   EKS Cluster    |    |   EKS Cluster    |    |   RDS Primary    |
   |   (eu-west-1a)   |    |   (eu-west-1b)   |    |   PostgreSQL     |
   +--------+---------+    +---------+--------+    +---------+--------+
            |                        |                        |
   +--------v---------+    +---------v--------+    +---------v--------+
   |   Order Service  |    |   Order Service  |    |   RDS Replica    |
   |   (3 replicas)   |    |   (3 replicas)   |    |   (eu-west-1b)   |
   +------------------+    +------------------+    +------------------+
            |                        |
   +--------v---------+    +---------v--------+
   |   Redis Cluster  |    |   RabbitMQ       |
   |   (ElastiCache)  |    |   (MQ Broker)    |
   +------------------+    +------------------+
```

| Element | Description | Configuration |
|---------|-------------|---------------|
| EKS Cluster | Kubernetes cluster on AWS | v1.28, 3 nodes t3.large per AZ |
| ALB | Application Load Balancer | HTTPS termination, health checks |
| RDS PostgreSQL | Managed database | db.r5.large, Multi-AZ, automated backups |
| ElastiCache Redis | Managed cache | cache.r5.large, cluster mode enabled |
| RabbitMQ MQ | Managed message broker | mq.m5.large, multi-AZ deployment |
| CloudFront | CDN | Edge caching, DDoS protection |

**Network:**
- VPC: 10.0.0.0/16 across 3 AZs
- Public subnets: ALB, NAT Gateways
- Private subnets: EKS nodes, RDS, ElastiCache
- Security groups restrict traffic between tiers

### 7.2 Deployment Mapping

| Software Component | Deployment Unit | Infrastructure | Scaling |
|-------------------|-----------------|----------------|---------|
| Order Service | Docker container (EKS) | 2-10 pods per AZ | HPA: CPU > 70% |
| Payment Service | Docker container (EKS) | 2-6 pods per AZ | HPA: CPU > 70% |
| Inventory Service | Docker container (EKS) | 2-8 pods per AZ | HPA: CPU > 70% |
| PostgreSQL | RDS managed | Primary + Replica | Storage auto-scaling |
| Redis | ElastiCache | 3 shards, 2 replicas | Auto-scaling enabled |

**Environments:**
| Environment | Purpose | Differences from Production |
|-------------|---------|----------------------------|
| Development | Local/minikube | Single node, no HA, debug logging |
| Staging | Pre-production | 1 AZ, smaller instances, anonymized data |
| Production | Live traffic | Full 3-AZ HA, monitoring, PagerDuty alerts |

**Backup & DR:**
- RDS: Automated daily backups, 35-day retention
- Cross-region backup: Snapshots copied to eu-central-1 weekly
- RTO: 4 hours, RPO: 1 hour
```
