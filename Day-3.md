# Day-3 | AWS EC2

## **What is Virtualization?**

Virtualization is a technology that allows a single physical computer (referred to as the host) to run multiple virtual computers, known as virtual machines (VMs). Each virtual machine operates independently with its own operating system, storage, and applications, all while utilizing the same physical hardware.

## **Why is Virtualization Useful?**

1. **Improves Resource Efficiency**  
   - Maximizes the usage of hardware by running multiple VMs on a single machine, reducing idle resources.

2. **Reduces Hardware Costs**  
   - Avoids the need for multiple physical machines by creating virtual ones on a single host.

3. **Simplifies Management**  
   - Easier to manage multiple environments on a centralized host rather than several individual computers.


## **The Role of Hypervisors in Virtualization**

A hypervisor is software that sits between the host machine's physical hardware and its virtual machines. It manages resource allocation and ensures each VM operates independently.

1. **Types of Hypervisors**
   - **Type 1 (Bare-Metal)**: Runs directly on physical hardware, highly efficient for data centers (e.g., VMware ESXi, Microsoft Hyper-V).
   - **Type 2 (Hosted)**: Operates on top of an existing operating system, suitable for testing (e.g., VirtualBox, VMware Workstation).

2. **Example of Hypervisor Functionality**  
   Imagine a server with 64 GB RAM and a powerful CPU. A hypervisor can divide this server into multiple VMs, each allocated specific CPU and memory resources, enabling separate environments for different applications.


## **Understanding Virtual Machines (VMs)**

A virtual machine (VM) is a software-based computer that uses the physical resources of the host. Each VM operates independently, with its own OS and applications.

- **Benefits of VMs**:
  - **Isolation**: Each VM operates independently, minimizing the risk of interference.
  - **Scalability**: Resources can be easily adjusted as needed.
  - **Portability**: VMs can be moved across different hardware or environments without issues.


### **Transition to EC2 with Virtualization Context**

#### **How EC2 Uses Virtualization**

Amazon EC2 leverages virtualization to provide scalable virtual machines, referred to as instances, in the cloud. These instances offer:

1. **Elasticity**: On-demand creation, resizing, and termination of instances based on workloads.  
2. **Resource Management**: AWS manages physical servers and hypervisors, ensuring optimal resource allocation.

#### **Benefits of EC2 Over Traditional VMs**

1. **On-Demand Resource Availability**  
   Launch and terminate instances as required, with flexible pricing models.

2. **Simplified Management**  
   AWS takes care of the underlying infrastructure, allowing users to focus on application-level management.

3. **Wide Range of Instance Types**  
   Select from a variety of instance types optimized for specific workloads.


## **Setting Up an Amazon EC2 Instance for DevOps**

### **1. EC2 Instances**

An EC2 instance is essentially a VM running on AWS.  
- **Key Features**:
  - Scalability: Adjust resources as needed.
  - Flexible Pricing: Choose On-Demand, Reserved, or Spot instances.
  - Customizability: Configure OS, storage, network settings, and more.

#### **2. Amazon Machine Images (AMIs)**

An AMI is a template for launching EC2 instances, containing an OS and optional software configurations.  

- **Types of AMIs**:
  - AWS-provided (e.g., Amazon Linux, Ubuntu).
  - Community AMIs (pre-configured by other users).
  - Custom AMIs (user-created for specific needs).


### **3. EC2 Instance Types**

AWS offers a range of EC2 instances for different workloads:
1. **General Purpose**: Balanced resources for most applications (e.g., t3, m5).  
2. **Compute Optimized**: High CPU performance for intensive applications (e.g., c5).  
3. **Memory Optimized**: High memory for databases (e.g., r5).  
4. **Storage Optimized**: High-speed local storage (e.g., i3).  
5. **Accelerated Computing**: GPU-based for ML and HPC tasks (e.g., g4).


### **4. Launching an EC2 Instance**

**Step-by-Step Guide**:
1. **Choose an AMI**: Select an OS template (e.g., Ubuntu, Amazon Linux).  
2. **Select an Instance Type**: Choose based on workload needs (e.g., t2.micro for basic setups).  
3. **Configure Instance Details**:
   - Attach IAM roles for AWS service access.
   - Add user data scripts for automated setup.  
4. **Add Storage**: Define storage needs (default 8 GB root volume).  
5. **Configure Security Groups**: Set inbound rules (e.g., SSH on port 22).  
6. **Review and Launch**: Verify settings and launch the instance.


### **5. Configuring the EC2 Instance**

**Connecting via SSH**:
```bash
ssh -i /path/to/key.pem ec2-user@<instance-public-ip>
```

**Install Development Tools**:
- For **Amazon Linux**:
  ```bash
  sudo yum update -y
  sudo yum install git docker -y
  ```
- For **Ubuntu**:
  ```bash
  sudo apt update -y
  sudo apt install git docker -y
  ```

**Docker Setup**:
- Start Docker:
  ```bash
  sudo systemctl start docker
  ```
- Enable Docker at boot:
  ```bash
  sudo systemctl enable docker
  ```

### **6. Securing the EC2 Instance**

1. **Security Groups**:
   - Restrict inbound traffic to necessary ports (e.g., SSH on port 22).  
   - Limit access by IP ranges for additional security.

2. **IAM Roles**:  
   - Avoid static access keys; use roles for temporary credentials.  

3. **Enable Encryption**:
   - Encrypt EBS volumes for data at rest.  

4. **Regular Updates**:
   - Apply security patches:
     ```bash
     sudo yum update -y
     ```

5. **Disable SSH Post-Setup**:
   - Use bastion hosts or VPNs for secure access.


### **7. Understanding Instance Types and Use Cases**

| Instance Type        | Use Cases                                   | Examples     |
|----------------------|---------------------------------------------|--------------|
| General Purpose      | Web servers, microservices, small databases | t3, m5       |
| Compute Optimized    | Batch processing, gaming, real-time apps    | c5, c6g      |
| Memory Optimized     | Databases, big data analytics               | r5, x1e      |
| Storage Optimized    | Data warehousing, analytics                 | i3, d2       |
| Accelerated Computing| ML training, HPC, graphics rendering        | g4, p4       |


## **Key Takeaways**

- Virtualization enables resource efficiency and cost savings.  
- EC2 leverages virtualization to provide scalable cloud infrastructure.  
- Choosing the right EC2 instance type ensures optimal performance and cost-effectiveness.  
- Security and regular updates are critical for production environments.
