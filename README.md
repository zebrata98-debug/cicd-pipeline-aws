cicd-pipeline-aws

A production-grade CI/CD pipeline that automatically lints, tests, builds, 
and deploys a containerised Flask API to AWS ECS Fargate on every push to 
main. The entire pipeline runs in under 3 minutes with zero manual steps.

 Project Structure
```
cicd-pipeline-aws/
├── app/
│   ├── backend/
│   │   ├── app.py              # Flask REST API
│   │   ├── requirements.txt
│   │   └── Dockerfile          # Multi-stage, non-root user
│   └── frontend/
│       └── index.html
├── tests/
│   └── test_app.py             # 10 unit tests (pytest)
├── terraform/
│   ├── main.tf                 # Root module + GitHub OIDC IAM role
│   ├── variables.tf
│   ├── outputs.tf
│   └── modules/
│       ├── networking/         # VPC, subnets, route tables
│       ├── ecr/                # ECR repo + lifecycle policy
│       ├── alb/                # ALB, target group, listener
│       └── ecs/                # Cluster, task def, service, IAM
└── .github/
    └── workflows/
        ├── ci.yml              # Lint → Test → Docker check
        └── cd.yml              # Build → ECR → ECS deploy
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
