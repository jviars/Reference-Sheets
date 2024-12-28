# DevOps Reference Sheet

## Continuous Integration (CI)

### Git Version Control
```bash
# Basic Git Commands
git init                    # Initialize repository
git clone <url>            # Clone repository
git add .                  # Stage changes
git commit -m "message"    # Commit changes
git push origin main      # Push to remote
git pull origin main      # Pull from remote

# Branching
git checkout -b feature   # Create and switch to branch
git merge feature        # Merge branch
git rebase main         # Rebase branch

# Git Flow
git flow init          # Initialize git flow
git flow feature start # Start feature branch
git flow feature finish # Finish feature branch
```

### Jenkins Pipeline
```groovy
// Jenkinsfile
pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        
        stage('Deploy') {
            steps {
                sh './deploy.sh'
            }
        }
    }
    
    post {
        always {
            junit '**/target/surefire-reports/TEST-*.xml'
        }
    }
}
```

### GitHub Actions
```yaml
name: CI Pipeline

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  build:
    runs-on: ubuntu-latest
    
    steps:
    - uses: actions/checkout@v2
    
    - name: Set up Node.js
      uses: actions/setup-node@v2
      with:
        node-version: '14'
        
    - name: Install dependencies
      run: npm install
      
    - name: Run tests
      run: npm test
      
    - name: Build
      run: npm run build
```

## Continuous Deployment (CD)

### Docker Containerization
```dockerfile
# Dockerfile
FROM node:14-alpine

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .

EXPOSE 3000
CMD ["npm", "start"]
```

```yaml
# docker-compose.yml
version: '3'
services:
  web:
    build: .
    ports:
      - "3000:3000"
    environment:
      - NODE_ENV=production
    depends_on:
      - db
  
  db:
    image: postgres:13
    environment:
      - POSTGRES_PASSWORD=secret
```

### Kubernetes Deployment
```yaml
# deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp
spec:
  replicas: 3
  selector:
    matchLabels:
      app: myapp
  template:
    metadata:
      labels:
        app: myapp
    spec:
      containers:
      - name: myapp
        image: myapp:1.0
        ports:
        - containerPort: 80

---
# service.yaml
apiVersion: v1
kind: Service
metadata:
  name: myapp-service
spec:
  selector:
    app: myapp
  ports:
  - port: 80
    targetPort: 80
  type: LoadBalancer
```

### Helm Charts
```yaml
# Chart.yaml
apiVersion: v2
name: myapp
version: 1.0.0

# values.yaml
replicaCount: 3
image:
  repository: myapp
  tag: 1.0.0
service:
  type: LoadBalancer
  port: 80
```

## Infrastructure as Code (IaC)

### Terraform
```hcl
# main.tf
provider "aws" {
  region = "us-west-2"
}

resource "aws_instance" "web" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"
  
  tags = {
    Name = "web-server"
  }
}

resource "aws_s3_bucket" "storage" {
  bucket = "my-app-storage"
  acl    = "private"
}
```

### Ansible
```yaml
# playbook.yml
---
- hosts: webservers
  become: yes
  tasks:
    - name: Install nginx
      apt:
        name: nginx
        state: present
    
    - name: Start nginx
      service:
        name: nginx
        state: started
        enabled: yes
    
    - name: Deploy application
      copy:
        src: files/app/
        dest: /var/www/html/
```

## Monitoring and Logging

### Prometheus
```yaml
# prometheus.yml
global:
  scrape_interval: 15s

scrape_configs:
  - job_name: 'node'
    static_configs:
      - targets: ['localhost:9100']
```

### Grafana Dashboard
```json
{
  "dashboard": {
    "panels": [
      {
        "title": "CPU Usage",
        "type": "graph",
        "datasource": "Prometheus",
        "targets": [
          {
            "expr": "node_cpu_seconds_total"
          }
        ]
      }
    ]
  }
}
```

### ELK Stack
```yaml
# logstash.conf
input {
  beats {
    port => 5044
  }
}

filter {
  grok {
    match => { "message" => "%{COMBINEDAPACHELOG}" }
  }
}

output {
  elasticsearch {
    hosts => ["localhost:9200"]
    index => "app-logs-%{+YYYY.MM.dd}"
  }
}
```

## Security and Compliance

### Security Scanning
```yaml
# OWASP ZAP Scan
- name: OWASP ZAP Scan
  uses: zaproxy/action-baseline@v0.4.0
  with:
    target: 'https://www.example.com'
```

### Vault Secret Management
```hcl
# Vault Configuration
path "secret/*" {
  capabilities = ["create", "read", "update", "delete", "list"]
}

# Vault API Usage
curl \
    --header "X-Vault-Token: $VAULT_TOKEN" \
    --request POST \
    --data @payload.json \
    https://vault.example.com/v1/secret/my-secret
```

## Testing

### Unit Testing
```python
# Python unit test
import unittest

class TestMathFunctions(unittest.TestCase):
    def test_addition(self):
        self.assertEqual(1 + 1, 2)
        
    def test_multiplication(self):
        self.assertEqual(2 * 3, 6)
```

### Integration Testing
```java
// Java integration test
@SpringBootTest
public class UserServiceIntegrationTest {
    @Autowired
    private UserService userService;
    
    @Test
    public void testCreateUser() {
        User user = new User("test", "test@example.com");
        User created = userService.create(user);
        assertNotNull(created.getId());
    }
}
```

## Automation Scripts

### Shell Scripting
```bash
#!/bin/bash

# Deployment script
echo "Starting deployment..."

# Build application
npm run build

# Run tests
npm test

# Deploy to production
if [ $? -eq 0 ]; then
    docker build -t myapp .
    docker push myapp
    kubectl apply -f deployment.yaml
else
    echo "Tests failed, aborting deployment"
    exit 1
fi
```

### Python Automation
```python
# Automated backup script
import boto3
import datetime

def backup_database():
    rds = boto3.client('rds')
    
    # Create snapshot
    timestamp = datetime.datetime.now().strftime('%Y-%m-%d-%H-%M')
    snapshot_id = f'automated-backup-{timestamp}'
    
    response = rds.create_db_snapshot(
        DBSnapshotIdentifier=snapshot_id,
        DBInstanceIdentifier='my-database'
    )
    
    return response
```

## Performance Optimization

### Load Testing
```yaml
# k6 load test
import http from 'k6/http';
import { check } from 'k6';

export default function () {
  const res = http.get('http://test.k6.io');
  check(res, {
    'status is 200': (r) => r.status === 200,
  });
}
```

### Caching Strategies
```nginx
# Nginx caching configuration
proxy_cache_path /path/to/cache levels=1:2 keys_zone=my_cache:10m;

server {
    location / {
        proxy_cache my_cache;
        proxy_cache_use_stale error timeout http_500 http_502 http_503 http_504;
        proxy_cache_valid 200 60m;
    }
}
```

## Best Practices

### Code Quality
1. Linting
```yaml
# ESLint configuration
{
  "extends": "eslint:recommended",
  "rules": {
    "indent": ["error", 2],
    "quotes": ["error", "single"]
  }
}
```

2. Code Review Process
```markdown
## Code Review Checklist
- [ ] Code follows style guide
- [ ] Tests are included
- [ ] Documentation is updated
- [ ] No security vulnerabilities
- [ ] Performance impact considered
```

### Documentation
```markdown
# Project Documentation

## Overview
Brief description of the project

## Architecture
System architecture diagram and explanation

## Deployment
Step-by-step deployment instructions

## Monitoring
Monitoring and alerting setup
```

### Incident Response
```yaml
# Incident Response Plan
stages:
  - identification:
      - detect incident
      - assess severity
  - containment:
      - isolate affected systems
      - prevent further damage
  - eradication:
      - remove threat
      - patch vulnerabilities
  - recovery:
      - restore systems
      - verify functionality
  - lessons_learned:
      - document incident
      - improve processes
```
