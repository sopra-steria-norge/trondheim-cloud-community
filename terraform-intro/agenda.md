# Terraform Introduction

## Agenda:

1. Introduction to Infrastructure as Code and Terraform (1 hour)
2. Understanding HashiCorp Configuration Language (HCL) (1 hour)
3. Getting Started with Terraform (1 hour)
4. Terraform providers (1 hour)
5. Authenting to Azure with Terraform (1 hour)
6. Advanced Terraform Topics (1 hour)
7. Terraform Backends and State Management (1 hour)
8. Q&A and Recap (30 minutes)

## Session 1: Introduction to Infrastructure as Code and Terraform (1 hour)

- What is Infrastructure as Code (IaC)?
- Other IaC tools and their benefits
- Benefits of using Terraform for IaC
- Key concepts in Terraform
- Interactive: Discuss real-world use cases and benefits of IaC and Terraform

## Session 2: Understanding HashiCorp Configuration Language (HCL) (1 hour)

- Understanding Terraform's declarative configuration language
- Defining resources, variables, and outputs in Terraform
- Managing state with Terraform
- Variables and interpolation in HCL
- Modules and reusability in Terraform
- Interactive: Hands-on exercises to practice writing HCL configurations

### Hands-on exercises

1. Write an HCL block that defines an Azure resource group named "myResourceGroup" with the location set to "norwayeast".
2. Create an HCL variable named "vm_count" and set its value to 3. Use interpolation to define a resource block that creates an Azure virtual machine with a count equal to the value of "vm_count". Each virtual machine should have a unique name and use the same image and size.
3. Define an HCL module named "network" that takes input variables "subnet_name" and "vnet_name". Within the module, create an Azure virtual network with the provided name and a subnet with the provided name.

4. Create an HCL locals block that calculates the sum of two variables, "num1" and "num2", and stores the result in a local variable named "sum". Use interpolation to display the value of "sum" in a resource block.

5. Write an HCL block that creates an Azure storage account with the following properties:

   - Name: "mystorageaccount"
   - Resource group: "myResourceGroup"
   - Location: "norwayeast"
   - Account kind: "StorageV2"
   - Access tier: "Hot"
   - Replication type: "LRS"
   - Note that the storage account name needs to be globally unique. Bonus points if you find a different method than adding your own initials. Hint: look at the `random_string` resource.

## Break (15 minutes)

## Session 3: Getting Started with Terraform (1 hour)

- Setting up Terraform on your machine
- Initializing a Terraform project
- Defining and managing resources with Terraform
- Understanding Terraform state management
- Interactive: Demonstration and hands-on practice of initializing and running a Terraform project

## Session 4: Terraform Providers (1 hour)

- Overview of Terraform providers and their role
- Understanding Terraform providers and their role in infrastructure provisioning
- Installing and configuring providers
- Exploring common providers (e.g., Azure, AWS, GCP)
- Managing provider versions and updates
- Interactive: Guided exercises to install and configure Spotify provider for playlist management

## Lunch (30 minutes)

## Session 5: Authenticating to Azure with Terraform (1 hour)

- Introduction to Azure Resource Manager (ARM)
- Authenticating to Azure using Service Principal and Managed Identity
- Provisioning Azure resources with Terraform
- Managing access control and permissions in Azure
- Interactive: Step-by-step walkthrough of authenticating to Azure using Terraform and deploying Azure resources

## Session 6: Advanced Terraform Topics (1 hour)

- Automating Terraform workflows with GitHub Actions or other CI/CD tools
- Integrating Terraform with Azure DevOps pipelines
- Best practices for Terraform project organization
- Using Terraform modules from the Terraform Registry
- Terraform best practices and common pitfalls
- Debugging Terraform deployments and understanding error messages
- Interactive: Discussion and hands-on exercises to implement GitHub Actions and Azure DevOps pipelines for Terraform automation

## Break (15 minutes)

## Session 7: Terraform Backends and State Management (1 hour)

- Understanding different backend types (local, remote, etc.)
- Configuring and utilizing remote backends (e.g., Azure Storage, AWS S3)
- Managing Terraform state in a collaborative environment
- State locking and concurrent operations
- Managing large-scale state files and state file optimization
- State migration and manipulation techniques (tf import, tf state mv, etc.)

## Session 8: Q&A and Recap (30 minutes)

- Answering participant questions
- Recap of key concepts and best practices
- Additional resources and next steps for further learning
- Interactive: Open forum for participants to ask questions and share their learnings
