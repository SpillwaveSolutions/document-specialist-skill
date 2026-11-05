# Pulumi Code-to-Docs Guide

---
TOKEN_BUDGET: 250
TIER: 3
LOAD_TRIGGER: CODE_TO_DOCS + Pulumi detected
DEPENDENCIES: brownfield-workflow.md
---

## Detection

```
Glob: "Pulumi.yaml"
Grep: "import pulumi"
```

## Extraction Commands

### Network Resources
```
Grep: "pulumi.aws.ec2.Vpc" → VPC configuration
Grep: "pulumi.aws.ec2.Subnet" → Subnets
Grep: "pulumi.aws.ec2.NatGateway" → NAT
Grep: "pulumi.aws.ec2.InternetGateway" → IGW
```

### Compute Resources
```
Grep: "pulumi.aws.ecs.Cluster" → ECS clusters
Grep: "pulumi.aws.ecs.Service" → ECS services
Grep: "pulumi.aws.ec2.Instance" → EC2 instances
Grep: "pulumi.aws.lambda.Function" → Lambda
```

### Data Resources
```
Grep: "pulumi.aws.rds.Instance" → RDS databases
Grep: "pulumi.aws.dynamodb.Table" → DynamoDB
Grep: "pulumi.aws.s3.Bucket" → S3 buckets
```

### Security Resources
```
Grep: "pulumi.aws.ec2.SecurityGroup" → Security groups
Grep: "pulumi.aws.iam.Role" → IAM roles
Grep: "pulumi.aws.iam.Policy" → IAM policies
```

### CDN/Edge
```
Grep: "pulumi.aws.cloudfront.Distribution" → CloudFront
Grep: "pulumi.aws.route53" → DNS
```

## Output Files

| Artifact | Location | Content |
|----------|----------|---------|
| Infrastructure Doc | `docs/deployment/{project}-infrastructure.md` | Full architecture |
| C4 Diagram | `docs/diagrams/infrastructure-c4.md` | System overview |
| Deployment Diagram | `docs/diagrams/deployment-topology.puml` | AWS resources |

## Document Structure

1. **Network Architecture**
   - VPC CIDR blocks
   - Public/private subnets
   - NAT Gateway configuration

2. **Compute Layer**
   - ECS clusters and services
   - Task definitions
   - Auto-scaling config

3. **Data Layer**
   - RDS configuration
   - S3 buckets and policies

4. **Security**
   - Security group rules
   - IAM roles and policies

5. **Cost Estimation** (optional)
   - Resource costs by category
