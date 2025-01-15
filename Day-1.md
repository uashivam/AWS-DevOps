# Day-1 | AWS DevOps Bootcamp | DevOps Intro & Workflow

#check
## **What is DevOps?**

**DevOps** is a cultural and technical movement that integrates development (Dev) and operations (Ops) teams to enhance collaboration, automate workflows, and deliver high-quality software faster. It emphasizes removing silos, improving communication, and fostering shared accountability throughout the software development lifecycle (SDLC).

## **Core Principles of DevOps**

### **1. Collaboration and Communication**
- DevOps removes barriers between development and operations teams, ensuring shared goals and responsibilities.
- Continuous feedback loops and cross-functional team alignment help identify and resolve bottlenecks early.

**Example**:
- **Before DevOps**: Developers hand off code to operations teams without knowing how it performs in production.
- **With DevOps**: Developers and operations collaborate using shared tools like Slack, Jira, and Azure DevOps, ensuring smooth transitions and fewer misunderstandings.

### **2. Continuous Integration and Continuous Deployment (CI/CD)**
- **CI** ensures that code changes are integrated into a shared repository frequently, followed by automated builds and tests.
- **CD** extends CI by automating the deployment process, making production-ready changes available to end-users.

**Example**:
- **Continuous Integration**:
  - Developers push code to GitHub.
  - Jenkins automatically triggers builds and unit tests.
- **Continuous Deployment**:
  - AWS CodePipeline deploys tested code to production automatically, ensuring frequent updates.

### **3. Automation**
- Automating repetitive tasks, such as builds, tests, deployments, and infrastructure provisioning, saves time, reduces human error, and increases reliability.

**Example**:
- Using **Ansible** or **Terraform** to automate infrastructure setup instead of manually provisioning servers.

### **4. Infrastructure as Code (IaC)**
- IaC treats infrastructure (servers, networks, databases) as code, enabling version control, repeatability, and scalability.

**Example**:
- **Before DevOps**: Operations manually configure servers.
- **With IaC**: Use a CloudFormation template to provision EC2 instances and S3 buckets in AWS.

### **5. Monitoring and Feedback**
- DevOps emphasizes real-time monitoring and proactive alerts to identify issues before they impact users.
- Feedback from monitoring tools guides teams to make informed decisions.

**Example**:
- **Before DevOps**: Relying on user-reported issues for bug detection.
- **With DevOps**: Using tools like **Prometheus** or **Amazon CloudWatch** to monitor CPU usage, latency, and error rates in real-time.

### **6. Shift-Left Testing**
- Testing moves earlier in the development process, ensuring bugs are caught during development rather than in production.

**Example**:
- Automating unit and integration tests using **Selenium** or **JUnit** in CI pipelines.

### **7. Continuous Improvement**
- DevOps encourages iterative improvement, learning from past failures, and refining processes over time.

**Example**:
- Conducting post-mortem reviews after an incident to identify root causes and prevent recurrence.

## **Benefits of DevOps**

### **1. Faster Delivery of Software**
- DevOps enables shorter development cycles and quicker releases.

**Example**:
- With CI/CD pipelines, a company can release daily updates instead of monthly releases.

### **2. Improved Collaboration**
- By breaking down silos, DevOps fosters a culture of ownership and accountability.

**Example**:
- A shared responsibility model ensures that both developers and operations work together during incidents.

### **3. Enhanced Quality**
- Automation and early testing reduce bugs and ensure higher software quality.

**Example**:
- Automated end-to-end testing with **Cypress** prevents regressions and ensures that new features don’t break existing functionality.

### **4. Increased Reliability**
- Continuous monitoring and automated recovery mechanisms ensure system stability and uptime.

**Example**:
- Implementing **auto-healing** in Kubernetes to restart failed pods.

### **5. Scalability**
- IaC and containerization enable businesses to scale applications seamlessly.

**Example**:
- Scaling microservices in **AWS ECS** during traffic surges without downtime.

### **6. Cost Efficiency**
- Automating manual tasks and optimizing resource usage reduce operational costs.

**Example**:
- Using **spot instances** in AWS for cost-effective batch processing.

### **7. Improved Security**
- DevOps integrates security practices into the development process, creating DevSecOps.

**Example**:
- Running security scans with **SonarQube** or **Aqua Security** in CI pipelines to identify vulnerabilities early.

### **8. Better User Experience**
- Faster updates, fewer outages, and improved quality result in happier users.

**Example**:
- Netflix uses DevOps to deploy hundreds of changes daily without impacting users.

## **Examples of DevOps in Action**

### **Case Study 1: Amazon**
- **Challenge**: Frequent manual deployments caused delays and errors.
- **Solution**: Implemented CI/CD pipelines, automated infrastructure with IaC, and real-time monitoring.
- **Result**: Over 1,000 deployments per day with reduced errors and improved scalability.

### **Case Study 2: Netflix**
- **Challenge**: Deliver uninterrupted streaming services while deploying frequent updates.
- **Solution**: Adopted DevOps principles, including CI/CD, container orchestration, and proactive monitoring.
- **Result**: 99.99% uptime, seamless user experience, and faster feature rollouts.

### **Common Tools in DevOps**

| **Category**         | **Tools**                                                                                  |
|-----------------------|-------------------------------------------------------------------------------------------|
| Version Control       | Git, GitHub, GitLab, Bitbucket                                                           |
| CI/CD                 | Jenkins, CircleCI, GitHub Actions, Azure DevOps, AWS CodePipeline                        |
| IaC                  | Terraform, AWS CloudFormation, Ansible, Chef, Puppet                                     |
| Containers            | Docker, Kubernetes, ECS, EKS                                                             |
| Monitoring            | Prometheus, Grafana, Datadog, Amazon CloudWatch, Splunk                                  |
| Collaboration         | Slack, Microsoft Teams, Jira                                                             |
| Testing               | Selenium, JUnit, Cypress, SonarQube                                                      |


## **DevOps Lifecycle**

1. **Plan**: Define requirements and track progress using tools like Jira or Azure Boards.
2. **Develop**: Write and manage code collaboratively using Git and version control.
3. **Build**: Automate builds using Jenkins or AWS CodeBuild.
4. **Test**: Conduct automated testing with Selenium or JUnit.
5. **Release**: Automate deployment pipelines using Azure Pipelines or CircleCI.
6. **Operate**: Monitor and manage applications using CloudWatch or Datadog.
7. **Monitor**: Analyze performance metrics and logs to improve the system.


---

### **End-to-End DevOps Workflow**

This workflow describes a complete DevOps pipeline, from raising a feature request to deployment and monitoring, integrating security and quality checks at every stage.

## **Workflow Overview**
1. **Client Raises a Ticket**
2. **Development and Testing on Local**
3. **Push Code to GitHub**
4. **CI/CD Pipeline Execution**
   - Compile and Unit Test
   - Trivy FS Security Scan
   - SonarQube Analysis and Quality Gate Check
   - Build Code and Push Artifact
   - Docker Build and Image Scan
   - Push Docker Image to Registry
5. **Deployment to EKS**
6. **Post-Deployment Verification**
7. **Notifications and Monitoring**


### **Step-by-Step Workflow**

#### **Step 1: Client Raises a Ticket**
- The client submits a feature request through a ticketing system (e.g., Jira, ServiceNow).
- The ticket includes:
  - Feature description
  - Acceptance criteria
  - Priority and deadline
- **Example Tool**: Jira for managing tickets and tracking progress.

#### **Step 2: Development and Local Testing**
1. **Developer Writes Code**:
   - A developer pulls the latest codebase from GitHub.
   - Creates a new feature branch.
   - Implements the requested feature in the branch.

   **Example Command**:
   ```bash
   git checkout -b feature/new-feature
   ```

2. **Local Testing**:
   - Run unit tests locally using tools like JUnit, Pytest, or Mocha.
   - Ensure the code passes all tests before committing.

   **Example**:
   ```bash
   npm test       # For JavaScript
   pytest tests/  # For Python
   ```

3. **Push Code to GitHub**:
   - Push the feature branch to GitHub.
   - This triggers the CI/CD pipeline.

   **Example Command**:
   ```bash
   git add .
   git commit -m "Implemented new feature"
   git push origin feature/new-feature
   ```

#### **Step 3: Continuous Integration Pipeline**

1. **Compile Code**:
   - Build the application using tools like Maven, Gradle, or npm.
   - Detect and fail early if there are compilation errors.

   **Example**:
   ```bash
   mvn clean install
   ```

2. **Run Unit Tests**:
   - Execute automated unit tests and generate reports.
   - Fail the pipeline if any test fails.

   **Example**:
   ```bash
   mvn test
   ```

3. **Trivy FS Security Scan**:
   - Scan the codebase for vulnerabilities using **Trivy**.
   - Generate reports and fail the pipeline if critical vulnerabilities are found.

   **Example**:
   ```bash
   trivy fs . --severity HIGH,CRITICAL --format table
   ```

4. **SonarQube Analysis**:
   - Perform static code analysis to check for code smells, bugs, and vulnerabilities.
   - Enforce a **quality gate** to ensure code meets specified thresholds.

   **Example**:
   ```bash
   sonar-scanner -Dsonar.projectKey=my-project -Dsonar.host.url=http://sonarqube:9000 -Dsonar.login=my-token
   ```

5. **Build and Push Artifact**:
   - Package the application (e.g., `.jar`, `.war`) and push it to an artifact repository like **Nexus** or **Artifactory**.

   **Example**:
   ```bash
   mvn deploy
   ```

#### **Step 4: Continuous Deployment Pipeline**

1. **Docker Build**:
   - Create a Docker image for the application.
   - Tag the image with the version or commit hash.

   **Example**:
   ```bash
   docker build -t myapp:1.0 .
   ```

2. **Scan Docker Image**:
   - Scan the Docker image for vulnerabilities using **Trivy** or **Aqua**.

   **Example**:
   ```bash
   trivy image myapp:1.0
   ```

3. **Push Docker Image to Registry**:
   - Push the scanned image to a container registry like Docker Hub, AWS ECR, or Azure ACR.

   **Example**:
   ```bash
   docker push myrepo/myapp:1.0
   ```

4. **Deploy to EKS**:
   - Deploy the Docker image to an **Elastic Kubernetes Service (EKS)** cluster using `kubectl` or Helm charts.

   **Example**:
   ```bash
   kubectl apply -f deployment.yaml
   ```

#### **Step 5: Post-Deployment Verification**

1. **Verify Deployment**:
   - Check the application’s health and ensure all pods are running.
   - Verify using Kubernetes commands.

   **Example**:
   ```bash
   kubectl get pods
   kubectl describe deployment myapp-deployment
   ```

2. **Functional Testing**:
   - Run automated functional and integration tests using Selenium, Postman, or Karate.

3. **Smoke Testing**:
   - Perform smoke tests to validate the deployment’s basic functionality.

#### **Step 6: Send Notifications**
- Notify stakeholders (e.g., developers, managers, QA) about deployment status.
- Use tools like **Slack**, **Microsoft Teams**, or email for notifications.

**Example Using Email**:
```bash
echo "Deployment successful for version 1.0" | mail -s "Deployment Status" stakeholder@example.com
```

#### **Step 7: Monitor Application**
1. **Real-Time Monitoring**:
   - Use **Prometheus** and **Grafana** to monitor application metrics like CPU usage, memory, response time, and error rates.

2. **Log Aggregation**:
   - Collect and analyze logs using tools like **ELK Stack** (Elasticsearch, Logstash, Kibana).

   **Example Kibana Dashboard**:
   - Monitor error trends and identify anomalies.

3. **Set Alerts**:
   - Configure alerts in **Amazon CloudWatch** or **Datadog** to notify teams of performance degradation or failures.

### **Pipeline Diagram**
Here’s how the process flows in a typical pipeline:

```
 Client Ticket
   ↓
 Developer (Code + Test Locally)
   ↓
 Push to GitHub → CI/CD Pipeline Triggered
   ↓
   ├── Compile Code
   ├── Unit Tests
   ├── Trivy Scan (FS)
   ├── SonarQube Analysis
   ├── Build Artifact
   ├── Docker Build + Scan
   ├── Push Docker Image
   ↓
 Deploy to EKS
   ↓
 Verify Deployment
   ↓
 Notify Stakeholders
   ↓
 Monitor and Optimize
```

### **Key Benefits of this Workflow**
1. **Automation**:
   - Reduces manual intervention, speeding up deployments.
2. **Quality Assurance**:
   - Enforces checks for security, code quality, and functionality at every stage.
3. **Scalability**:
   - Seamlessly deploys updates to scalable infrastructure (e.g., Kubernetes on AWS).
4. **Proactive Monitoring**:
   - Detects and resolves issues before they affect end users.

---

### **AWS DevOps: A Comprehensive Overview**

AWS (Amazon Web Services) provides a suite of tools and services designed to implement DevOps practices efficiently, helping organizations achieve faster development, delivery, and scalability of applications. 

## **What is AWS DevOps?**

AWS DevOps combines AWS cloud infrastructure with DevOps practices such as Continuous Integration (CI), Continuous Deployment (CD), monitoring, and automation. AWS provides scalable, flexible, and secure services to help teams adopt DevOps principles.

### **Key DevOps Practices in AWS**
1. **Infrastructure as Code (IaC):** Automating infrastructure provisioning using tools like AWS CloudFormation and Terraform.
2. **Continuous Integration and Continuous Deployment (CI/CD):** Using AWS CodePipeline, AWS CodeBuild, and AWS CodeDeploy for automated build, test, and deployment.
3. **Monitoring and Logging:** Employing tools like Amazon CloudWatch and AWS X-Ray for real-time insights.
4. **Automation:** Automating workflows using AWS Lambda, Step Functions, and Elastic Beanstalk.
5. **Security and Compliance:** Integrating AWS Identity and Access Management (IAM), Secrets Manager, and GuardDuty for secure DevOps workflows.

## **Key AWS DevOps Services**

### 1. **Code Services (AWS CodeSuite)**
AWS offers a range of tools for CI/CD under the CodeSuite:

#### **a. AWS CodePipeline**
- Automates CI/CD workflows.
- Integrates with GitHub, Bitbucket, AWS CodeCommit, and Jenkins.
- Orchestrates the build, test, and deployment phases.
  
  **Example Workflow**:
  ```text
  CodePipeline Stages:
  1. Source Stage: Fetch code from GitHub.
  2. Build Stage: Build code using CodeBuild.
  3. Deploy Stage: Deploy artifacts using CodeDeploy.
  ```

  **Command**:
  ```bash
  aws codepipeline create-pipeline --cli-input-json file://pipeline-config.json
  ```

#### **b. AWS CodeBuild**
- Fully managed build service.
- Compiles source code, runs tests, and produces deployable artifacts.

  **Example Use**:
  ```yaml
  version: 0.2
  phases:
    build:
      commands:
        - echo "Building the application..."
        - mvn clean package
  ```

#### **c. AWS CodeDeploy**
- Automates application deployments to EC2 instances, Lambda functions, or on-premises servers.
- Supports blue/green deployments and rolling updates.

  **Example Deployment**:
  ```json
  {
    "applicationName": "MyApplication",
    "deploymentGroupName": "MyDeploymentGroup",
    "revision": {
      "revisionType": "S3",
      "s3Location": {
        "bucket": "my-bucket",
        "key": "my-app.zip",
        "bundleType": "zip"
      }
    }
  }
  ```

#### **d. AWS CodeCommit**
- Secure, scalable, and managed Git repositories.
- Used as a version control service.

  **Command**:
  ```bash
  git remote add origin https://git-codecommit.<region>.amazonaws.com/v1/repos/MyRepository
  ```

### 2. **Infrastructure as Code (IaC)**

#### **a. AWS CloudFormation**
- Provides a declarative way to define and provision AWS infrastructure.
- Allows reusability of templates to manage infrastructure consistently.

  **Example Template**:
  ```yaml
  Resources:
    MyInstance:
      Type: "AWS::EC2::Instance"
      Properties:
        InstanceType: "t2.micro"
        ImageId: "ami-0abcdef1234567890"
  ```

#### **b. Terraform**
- Open-source IaC tool that supports AWS.
- Uses HashiCorp Configuration Language (HCL) for defining resources.

  **Example Script**:
  ```hcl
  resource "aws_instance" "example" {
    ami           = "ami-0abcdef1234567890"
    instance_type = "t2.micro"
  }
  ```

### 3. **Monitoring and Logging**

#### **a. Amazon CloudWatch**
- Monitors applications, infrastructure, and services.
- Provides alerts, dashboards, and event-based automation.

  **Use Case**:
  - Set alarms to trigger when CPU usage exceeds 80%.

  **Command**:
  ```bash
  aws cloudwatch put-metric-alarm --alarm-name HighCPUUsage --metric-name CPUUtilization --namespace AWS/EC2 --statistic Average --period 300 --threshold 80 --comparison-operator GreaterThanThreshold --dimensions Name=InstanceId,Value=i-1234567890abcdef0 --evaluation-periods 2 --alarm-actions arn:aws:sns:region:123456789012:MyTopic
  ```

#### **b. AWS X-Ray**
- Debugs and analyzes distributed applications.
- Identifies performance bottlenecks in microservices.

  **Example Use**:
  - Trace requests across Lambda, API Gateway, and DynamoDB.

#### **c. AWS CloudTrail**
- Tracks user activity and API usage for auditing.

  **Command**:
  ```bash
  aws cloudtrail create-trail --name MyTrail --s3-bucket-name my-logs-bucket
  ```

### 4. **Container and Serverless Deployments**

#### **a. Amazon ECS and EKS**
- **ECS (Elastic Container Service):** Orchestrates Docker containers.
- **EKS (Elastic Kubernetes Service):** Runs Kubernetes workloads.

  **Example ECS Task Definition**:
  ```json
  {
    "family": "my-task-family",
    "containerDefinitions": [
      {
        "name": "my-app",
        "image": "my-docker-image",
        "memory": 512,
        "cpu": 256,
        "essential": true
      }
    ]
  }
  ```

#### **b. AWS Lambda**
- Runs serverless applications with auto-scaling and pay-per-use pricing.
- Used for event-driven architecture.

  **Command**:
  ```bash
  aws lambda create-function --function-name MyFunction --runtime python3.8 --role arn:aws:iam::123456789012:role/MyRole --handler lambda_function.lambda_handler --zip-file fileb://my-function.zip
  ```

### 5. **Security and Compliance**

#### **a. AWS IAM**
- Manages access permissions for AWS services and users.

  **Example Policy**:
  ```json
  {
    "Version": "2012-10-17",
    "Statement": [
      {
        "Effect": "Allow",
        "Action": "s3:*",
        "Resource": "arn:aws:s3:::my-bucket/*"
      }
    ]
  }
  ```

#### **b. AWS Secrets Manager**
- Securely stores secrets like API keys and database credentials.

  **Command**:
  ```bash
  aws secretsmanager create-secret --name MySecret --secret-string '{"username":"admin","password":"password123"}'
  ```

#### **c. AWS GuardDuty**
- Detects anomalies and unauthorized access attempts.


## **AWS DevOps Workflow**

1. **Source Code Management:** Use AWS CodeCommit or GitHub.
2. **Build & Test:** Automate with AWS CodeBuild.
3. **Release & Deploy:** Use AWS CodePipeline and AWS CodeDeploy for CI/CD pipelines.
4. **Monitor:** Employ Amazon CloudWatch and AWS X-Ray for logging and tracing.
5. **Scale & Optimize:** Use auto-scaling groups, spot instances, or serverless architectures.


## **Benefits of AWS DevOps**
1. **Scalability:** Auto-scaling for applications and services.
2. **Flexibility:** Integration with third-party tools like Jenkins, Terraform, and GitHub.
3. **Cost-Effectiveness:** Pay-per-use pricing for compute and storage.
4. **Security:** Built-in compliance, encryption, and access control.
5. **Automation:** Reduced manual intervention in deployment and monitoring.

