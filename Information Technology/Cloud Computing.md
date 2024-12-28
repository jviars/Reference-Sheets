# Comprehensive Cloud Computing Reference Sheet

## Cloud Service Models

### IaaS (Infrastructure as a Service)
- Raw compute, storage, and networking
- Examples:
  * AWS EC2, S3
  * Azure Virtual Machines, Blob Storage
  * Google Compute Engine

### PaaS (Platform as a Service)
- Development and deployment platform
- Examples:
  * AWS Elastic Beanstalk
  * Azure App Service
  * Google App Engine

### SaaS (Software as a Service)
- Ready-to-use software applications
- Examples:
  * Microsoft 365
  * Google Workspace
  * Salesforce

## AWS (Amazon Web Services)

### Compute Services
1. **EC2 (Elastic Compute Cloud)**
   ```bash
   # Launch instance
   aws ec2 run-instances --image-id ami-12345678 \
       --instance-type t2.micro \
       --key-name MyKeyPair
   
   # Stop instance
   aws ec2 stop-instances --instance-ids i-1234567890abcdef0
   ```

2. **Lambda**
   ```python
   def lambda_handler(event, context):
       # Event-driven serverless function
       return {
           'statusCode': 200,
           'body': 'Hello from Lambda!'
       }
   ```

3. **ECS (Elastic Container Service)**
   ```yaml
   # Task definition
   {
     "family": "web-app",
     "containerDefinitions": [
       {
         "name": "web",
         "image": "nginx:latest",
         "memory": 256,
         "cpu": 256,
         "essential": true
       }
     ]
   }
   ```

### Storage Services
1. **S3 (Simple Storage Service)**
   ```python
   import boto3

   s3 = boto3.client('s3')
   s3.upload_file('file.txt', 'mybucket', 'file.txt')
   ```

2. **EBS (Elastic Block Store)**
   - Persistent block storage for EC2
   - Types:
     * gp2/gp3 (General Purpose)
     * io1/io2 (Provisioned IOPS)
     * st1 (Throughput Optimized)
     * sc1 (Cold Storage)

3. **EFS (Elastic File System)**
   - Scalable file storage
   - NFS compatible
   - Multi-AZ access

### Database Services
1. **RDS (Relational Database Service)**
   - Supported engines:
     * Amazon Aurora
     * PostgreSQL
     * MySQL
     * MariaDB
     * Oracle
     * SQL Server

2. **DynamoDB**
   ```javascript
   // Put item
   const params = {
     TableName: 'Users',
     Item: {
       userId: '123',
       name: 'John Doe'
     }
   };
   dynamodb.putItem(params).promise();
   ```

3. **ElastiCache**
   - Redis
   - Memcached

### Networking Services
1. **VPC (Virtual Private Cloud)**
   ```plaintext
   ┌─────────────────────────────┐
   │           VPC               │
   │  ┌──────────┐ ┌──────────┐ │
   │  │ Public   │ │ Private  │ │
   │  │ Subnet   │ │ Subnet   │ │
   │  └──────────┘ └──────────┘ │
   └─────────────────────────────┘
   ```

2. **Route 53**
   - DNS service
   - Domain registration
   - Health checking

3. **CloudFront**
   - CDN service
   - Global edge locations
   - HTTPS support

## Microsoft Azure

### Compute Services
1. **Virtual Machines**
   ```powershell
   # Create VM
   New-AzVM -ResourceGroupName "myRG" `
            -Name "myVM" `
            -Location "eastus" `
            -Image "UbuntuLTS"
   ```

2. **Azure Functions**
   ```csharp
   [FunctionName("HttpExample")]
   public static async Task<IActionResult> Run(
       [HttpTrigger(AuthorizationLevel.Function, "get", "post")] HttpRequest req,
       ILogger log)
   {
       return new OkObjectResult("Hello from Azure Functions!");
   }
   ```

3. **Azure Kubernetes Service (AKS)**
   ```bash
   # Create cluster
   az aks create --resource-group myRG \
                 --name myAKSCluster \
                 --node-count 3
   ```

### Storage Services
1. **Blob Storage**
   ```csharp
   // Upload blob
   var blobClient = containerClient.GetBlobClient(fileName);
   await blobClient.UploadAsync(stream, overwrite: true);
   ```

2. **Azure Files**
   - SMB file shares
   - Cloud native

3. **Azure Disk Storage**
   - Managed disks
   - Unmanaged disks

### Database Services
1. **Azure SQL Database**
2. **Cosmos DB**
3. **Azure Database for:
   - PostgreSQL
   - MySQL
   - MariaDB

## Google Cloud Platform (GCP)

### Compute Services
1. **Compute Engine**
   ```bash
   # Create instance
   gcloud compute instances create my-instance \
       --machine-type=n1-standard-1 \
       --zone=us-central1-a
   ```

2. **Cloud Functions**
   ```python
   def hello_world(request):
       return 'Hello from GCP!'
   ```

3. **Google Kubernetes Engine (GKE)**
   ```bash
   # Create cluster
   gcloud container clusters create my-cluster \
       --num-nodes=3 \
       --zone=us-central1-a
   ```

### Storage Services
1. **Cloud Storage**
2. **Persistent Disk**
3. **Filestore**

### Database Services
1. **Cloud SQL**
2. **Cloud Spanner**
3. **Cloud Bigtable**

## Cloud Architecture Patterns

### High Availability
```plaintext
┌─────────────┐    ┌─────────────┐
│  Region A   │    │  Region B   │
│ ┌─────────┐ │    │ ┌─────────┐ │
│ │Instance │ │    │ │Instance │ │
│ └─────────┘ │    │ └─────────┘ │
└─────────────┘    └─────────────┘
```

### Auto Scaling
```yaml
# AWS Auto Scaling Group
{
  "AutoScalingGroupName": "my-asg",
  "MinSize": 1,
  "MaxSize": 5,
  "DesiredCapacity": 2,
  "LaunchTemplate": {
    "LaunchTemplateId": "lt-12345",
    "Version": "1"
  }
}
```

### Load Balancing
1. Application Load Balancer
2. Network Load Balancer
3. Global Load Balancer

## Security Best Practices

### Identity and Access Management (IAM)
1. Principle of Least Privilege
2. Role-Based Access Control
3. Multi-Factor Authentication

### Network Security
1. Security Groups
2. Network ACLs
3. VPC Flow Logs

### Data Protection
1. Encryption at Rest
2. Encryption in Transit
3. Key Management

## Cost Optimization

### Best Practices
1. Right Sizing
2. Reserved Instances
3. Spot Instances
4. Auto Scaling

### Monitoring Tools
1. AWS Cost Explorer
2. Azure Cost Management
3. Google Cloud Billing

## DevOps Integration

### Infrastructure as Code
```yaml
# Terraform Example
resource "aws_instance" "web" {
  ami           = "ami-12345678"
  instance_type = "t2.micro"
  
  tags = {
    Name = "web-server"
  }
}
```

### CI/CD Pipeline
```yaml
# GitHub Actions Example
name: Deploy to Cloud
on: [push]
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Deploy
        run: |
          # deployment commands
```

### Monitoring and Logging
1. CloudWatch (AWS)
2. Azure Monitor
3. Cloud Monitoring (GCP)

## Disaster Recovery

### Strategies
1. Backup and Restore
2. Pilot Light
3. Warm Standby
4. Multi-Site Active/Active

### Recovery Metrics
- RPO (Recovery Point Objective)
- RTO (Recovery Time Objective)

## Serverless Architecture

### Components
1. Functions as a Service (FaaS)
2. Backend as a Service (BaaS)
3. API Gateway

### Event Sources
1. HTTP Triggers
2. Queue Triggers
3. Schedule Triggers

## Containers and Orchestration

### Docker
```dockerfile
FROM node:14
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
EXPOSE 3000
CMD ["npm", "start"]
```

### Kubernetes
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: web-app
spec:
  replicas: 3
  selector:
    matchLabels:
      app: web
  template:
    metadata:
      labels:
        app: web
    spec:
      containers:
      - name: web
        image: nginx:latest
```

## Performance Optimization

### Caching Strategies
1. Content Delivery Networks
2. In-Memory Caching
3. Database Caching

### Application Performance
1. Auto Scaling
2. Load Balancing
3. Resource Optimization

## Compliance and Governance

### Frameworks
1. AWS Well-Architected Framework
2. Azure Well-Architected Framework
3. Google Cloud Architecture Framework

### Compliance Standards
1. HIPAA
2. GDPR
3. SOC 2
4. PCI DSS
