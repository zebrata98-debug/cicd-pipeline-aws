cicd-pipeline-aws

A production-grade CI/CD pipeline that automatically lints, tests, builds, 
and deploys a containerised Flask API to AWS ECS Fargate on every push to 
main. The entire pipeline runs in under 3 minutes with zero manual steps.

 Project Structure
```
cicd-pipeline-aws/
├── app/
│   ├── backend/
│   │   ├── app.py              
│   │   ├── requirements.txt
│   │   └── Dockerfile          
│   └── frontend/
│       └── index.html
├── tests/
│   └── test_app.py            
├── terraform/
│   ├── main.tf                
│   ├── variables.tf
│   ├── outputs.tf
│   └── modules/
│       ├── networking/         
│       ├── ecr/                
│       ├── alb/               
│       └── ecs/                
└── .github/
    └── workflows/
        ├── ci.yml              
        └── cd.yml              
```

Deploy

cd terraform

terraform init

terraform apply -var="github_repo=YOUR_USERNAME/cicd-pipeline-aws"

terraform output next_steps

git push origin main

GitHub Secrets Required

| Secret | Description |
|---|---|
| `AWS_ROLE_ARN` | IAM role ARN for GitHub OIDC auth |
| `AWS_REGION` | AWS region |
| `ECR_REPOSITORY` | ECR repository name |
| `ECS_CLUSTER` | ECS cluster name |
| `ECS_SERVICE` | ECS service name |
| `ECS_TASK_DEFINITION` | ECS task definition family |
| `ECS_CONTAINER_NAME` | Container name (flask-api) |
| `ALB_DNS_NAME` | Load balancer DNS name |

