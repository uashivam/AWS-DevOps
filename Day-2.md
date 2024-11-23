# Day-2 | AWS IAM (Identity and Access Management)

AWS **Identity and Access Management (IAM)** is a web service that helps you securely control access to AWS resources. With IAM, you can manage users, groups, roles, and policies to ensure that the right permissions are assigned to the right entities.

This document will walk through the core concepts of **IAM**, including **IAM Users**, **Groups**, **Roles**, **Policies**, and how they work together to provide secure access management for your AWS resources.

### **1. IAM Users**

An **IAM User** is an identity within AWS that represents a person or an application that needs to interact with AWS resources.

#### **Key Features:**
- **Credentials:**
  - **Access Keys**: Used for programmatic access via AWS CLI, SDKs, or APIs.
  - **Password**: Used for accessing the AWS Management Console.
  
- **Permissions:**
  - IAM Users do not have any permissions by default. Permissions must be explicitly assigned via **policies**.

#### **Use Cases:**
- **Personal Access**: Assign to individuals who need access to AWS Management Console or programmatic access.
- **API Access**: Create users for applications that need to make API calls to AWS.

#### **Example:**
Create a user named `JohnDoe` for a team member, and assign read-only access to an S3 bucket.

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "s3:ListBucket",
      "Resource": "arn:aws:s3:::example-bucket"
    }
  ]
}
```

### **2. IAM User Groups**

An **IAM User Group** is a collection of IAM users. The permissions assigned to the group are inherited by all users within that group.

#### **Key Features:**
- **Simplified Permission Management**: Instead of managing individual user permissions, you can manage group-level permissions.
- **Cumulative Permissions**: Users can belong to multiple groups, and the permissions are cumulative (i.e., the user gets permissions from all groups they belong to).

#### **Use Cases:**
- **Team-Based Permissions**: Assign common permissions to users within the same team or role (e.g., Developers, Admins, Finance).
- **Role-Based Permissions**: Manage permissions based on job roles, such as granting all developers EC2 management permissions.

#### **Example:**
Create a **Developers** group and assign the `AmazonEC2FullAccess` policy to allow developers full access to EC2 management.

### **3. IAM Roles**

An **IAM Role** is an identity that defines a set of permissions. Unlike IAM Users, roles do not have permanent credentials; they rely on **temporary security credentials** that can be assumed by an entity (user, AWS service, or another account).

#### **Key Features:**
- **No Permanent Credentials**: Roles use **temporary credentials** provided via **AWS STS (Security Token Service)**.
- **Assumable**: Roles can be assumed by AWS services, users, or applications.
- **Trust Policies**: Trust policies define which entities are allowed to assume the role.

#### **Use Cases:**
- **EC2 Access**: Grant an EC2 instance permissions to access other AWS resources (e.g., S3 buckets) without storing access keys in the application code.
- **Cross-Account Access**: Allow users from another AWS account to assume the role and access resources in your account.

#### **Example:**
Create a role that allows read access to an S3 bucket.

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::example-bucket/*"
    }
  ]
}
```

Attach this role to an EC2 instance to grant it access to the S3 bucket without hardcoding access keys.

### **4. IAM Policies**

An **IAM Policy** is a JSON document that defines the permissions granted to an IAM user, group, or role. Policies specify what actions are allowed or denied for specific resources.

#### **Key Features:**
- **Managed Policies**: Predefined policies provided by AWS (e.g., `AdministratorAccess`, `AmazonS3ReadOnlyAccess`).
- **Inline Policies**: Policies that are directly attached to a single IAM user, group, or role.
- **Custom Policies**: JSON-based policies created to define specific access requirements.

#### **Policy Structure**:
- **Effect**: Defines whether the action is allowed (`Allow`) or denied (`Deny`).
- **Action**: Specifies what actions are allowed (e.g., `s3:ListBucket`, `ec2:StartInstances`).
- **Resource**: Defines the AWS resource(s) the policy applies to (e.g., specific S3 buckets, EC2 instances).
- **Conditions** (optional): Adds extra restrictions (e.g., limiting access to a certain IP address or time range).

#### **Example:**
A policy that allows starting and stopping EC2 instances.

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "ec2:StartInstances",
        "ec2:StopInstances"
      ],
      "Resource": "arn:aws:ec2:region:account-id:instance/instance-id"
    }
  ]
}
```

### **How IAM Components Work Together**

#### **1. Users**:
- Users represent individuals or applications that need access.
- Example: JohnDoe is created with no permissions by default.

#### **2. Groups**:
- Groups help manage permissions for multiple users.
- Example: JohnDoe is added to the **Developers** group, which grants EC2 permissions.

#### **3. Roles**:
- Roles are assumed by AWS services or cross-account users for temporary access.
- Example: An EC2 instance assumes a role to access an S3 bucket without embedding credentials.

#### **4. Policies**:
- Policies define the actual permissions for users, groups, and roles.
- Example: A policy attached to the **Developers** group allows full EC2 management.

### **Summary: IAM and Its Core Components**

- **IAM Users**: Represent individual identities that require access to AWS resources.
- **IAM Groups**: Simplify the management of permissions for multiple users.
- **IAM Roles**: Used by AWS services or cross-account users for temporary access.
- **IAM Policies**: Define the permissions (actions) allowed on specific resources.

Each IAM component works together to grant controlled access to AWS resources, whether to users, applications, or services. By combining IAM users, groups, roles, and policies, AWS enables you to set up a secure, scalable, and flexible access management system for your AWS infrastructure.

### **Detailed Documentation: IAM Users, Groups, Policies, and Roles Demo Using AWS Management Console**

This document provides a step-by-step guide to creating and managing **IAM Users, Groups, Policies, and Roles** and demonstrates how they interact with **EC2 instances**. All tasks are performed using the **AWS Management Console** to visually showcase access management.

### **POC Objective**
1. **Create and use IAM Users, Groups, and Policies.**
2. **Demonstrate IAM Roles with EC2 instances.**
3. **Perform all operations via AWS Management Console.**

### **Step-by-Step Demo**

#### **1. Create an IAM Group with Limited EC2 Permissions**

##### **1.1 Navigate to IAM Dashboard**
- In the AWS Management Console, go to **IAM**.
- Select **Groups** > **Create Group**.

##### **1.2 Create the Group**
- **Group Name**: `LimitedEC2AccessGroup`.
- Skip attaching policies during creation.

##### **1.3 Create a Custom Policy**
- Go to **Policies** > **Create Policy**.
- Select the **JSON Tab** and paste the following policy:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "ec2:Describe*",
      "Resource": "*"
    },
    {
      "Effect": "Deny",
      "Action": [
        "ec2:StartInstances",
        "ec2:StopInstances",
        "ec2:TerminateInstances"
      ],
      "Resource": "*"
    }
  ]
}
```

- **Name the policy**: `LimitedEC2PermissionsPolicy`.

##### **1.4 Attach the Policy to the Group**
- Go to the **Groups** tab and select `LimitedEC2AccessGroup`.
- Navigate to **Permissions** > **Attach Policies**.
- Search for `LimitedEC2PermissionsPolicy` and attach it.

#### **2. Create IAM Users**

##### **2.1 Create Two Users**
- Navigate to **IAM** > **Users** > **Add Users**.
- **User 1**: `AdminUser`
  - Assign the **AdministratorAccess** managed policy.
- **User 2**: `LimitedUser`
  - Add this user to the `LimitedEC2AccessGroup`.

##### **2.2 Set Passwords**
- During user creation, enable **password login** for AWS Management Console access for both users.
- Assign temporary or custom passwords.

#### **3. Create an IAM Role for EC2**

##### **3.1 Navigate to IAM Roles**
- Go to **IAM** > **Roles** > **Create Role**.

##### **3.2 Choose Trusted Entity**
- Choose **AWS Service**.
- Select **EC2** as the trusted service.

##### **3.3 Attach a Policy**
- Select an existing policy like **AmazonS3ReadOnlyAccess** or create a custom policy to allow EC2 instances to access S3.  
- Example Custom Policy:
  ```json
  {
    "Version": "2012-10-17",
    "Statement": [
      {
        "Effect": "Allow",
        "Action": "s3:GetObject",
        "Resource": "arn:aws:s3:::example-bucket/*"
      }
    ]
  }
  ```

##### **3.4 Complete Role Creation**
- Name the role: `EC2S3AccessRole`.

##### **3.5 Assign the Role to an EC2 Instance**
- Go to the **EC2 Dashboard**.
- Select the instance, click **Actions** > **Security** > **Modify IAM Role**.
- Assign the `EC2S3AccessRole` to the instance.

#### **4. Launch and Configure EC2 Instances**

##### **4.1 Launch Two EC2 Instances**
- Launch two instances using the **Amazon Linux 2 AMI**:
  - **Instance 1**: Assign the `EC2S3AccessRole` to demonstrate role-based access.
  - **Instance 2**: Launch without any role to show the difference.

##### **4.2 Log in to Instances**
- Use **Instance Connect** to log in to both instances:
  - Go to **EC2 Dashboard** > Select an instance > **Actions** > **Connect** > **Instance Connect**.

#### **5. Test IAM Permissions in the AWS Console**

##### **5.1 Log in as `AdminUser`**
1. Log in to the AWS Management Console as `AdminUser`.
2. Navigate to the **EC2 Dashboard**:
   - Start, stop, and terminate instances to demonstrate full control.
   - Verify that `AdminUser` has unrestricted access due to the **AdministratorAccess** policy.

##### **5.2 Log in as `LimitedUser`**
1. Log in to the AWS Management Console as `LimitedUser`.
2. Navigate to the **EC2 Dashboard**:
   - Attempt to start, stop, or terminate instances (these actions should be denied due to the policy attached to the `LimitedEC2AccessGroup`).
   - Use the `DescribeInstances` action to view instance details (this action should succeed).

   **Explanation**: `LimitedEC2PermissionsPolicy` allows only read access (`DescribeInstances`) and denies modification actions (e.g., `StartInstances`, `TerminateInstances`).

##### **5.3 Access EC2 Instance with IAM Role**
1. Log in to the **Instance 1** (with `EC2S3AccessRole`) using **Instance Connect**:
   - Go to **EC2 Dashboard** > Select **Instance 1** > **Actions** > **Connect** > **Instance Connect**.
2. Access S3 resources using the role's permissions:
   - Example: Use a web browser (if GUI-enabled) or a pre-installed application like `curl` to verify access to S3 buckets.

   **Verify Role Functionality**:
   - Open a browser and navigate to `https://s3.amazonaws.com/YOUR-BUCKET-NAME`.
   - The S3 bucket contents should be accessible due to the role.

3. Log in to **Instance 2** (without a role) and attempt the same. It should fail since no role is assigned.

### **Summary**

| Feature                          | `AdminUser`         | `LimitedUser`            | `EC2S3AccessRole`                  |
|----------------------------------|---------------------|--------------------------|-------------------------------------|
| Full EC2 Access                  | ✅                  | ❌                       | N/A                                 |
| Limited EC2 Permissions          | ❌                  | ✅ (DescribeInstances)   | N/A                                 |
| S3 Access (via Role)             | N/A                 | N/A                      | ✅ (Assigned to Instance 1 only)    |

---

### **Key Learnings**
1. IAM **Groups** simplify permission management for teams.
2. IAM **Roles** securely provide temporary credentials to AWS services without hardcoding access keys.
3. IAM **Policies** define granular permissions for users, groups, and roles.
4. Access management can be visually verified using the AWS Management Console.

### **Best Practices for IAM Management**
1. Apply **least privilege** principles to all users and roles.
2. Use **roles** instead of long-term credentials for applications.
3. Regularly audit and clean up unused users, roles, and permissions.
4. Enable **MFA** for all privileged users.


This concludes the step-by-step guide for demonstrating IAM users, groups, policies, and roles with EC2 instances using the AWS Management Console.

