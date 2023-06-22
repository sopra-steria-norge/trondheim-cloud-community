# Terraform Introduction

## Agenda:

1. General introduction (10 minutes)
2. Introduction to Infrastructure as Code and Terraform (45 mins)
3. Understanding HashiCorp Configuration Language (HCL) (45 mins)
4. Getting Started with Terraform (45 mins)
5. Terraform providers (45 mins)
6. Authenting to Azure with Terraform (45 mins)
7. Advanced Terraform Topics (45 mins)
8. Terraform Backends and State Management (45 mins)
9. Q&A and Recap (30 minutes)

## Session 1: General introduction (10 minutes)

- Introductions
- Participants expectations
- Presenter expectations
- Practical information

## Session 2: Introduction to Infrastructure as Code and Terraform (45 mins)

- What is Infrastructure as Code (IaC)?
- Other IaC tools and their benefits
- Benefits of using Terraform for IaC
- Key concepts in Terraform
- Interactive: Discuss real-world use cases and benefits of IaC and Terraform

## Session 3: Understanding HashiCorp Configuration Language (HCL) (45 mins)

- Understanding Terraform's declarative configuration language
- Defining resources, variables, and outputs in Terraform
- Managing state with Terraform
- Variables and interpolation in HCL
- Understanding the locals block
- Modules and reusability in Terraform
- Interactive: Hands-on exercises to practice writing HCL configurations

### Hands-on exercises

1. Write an HCL block that defines a local output with the value "Hello, world!".
2. Write an HCL block that defines a local output with a value from some input. For example, if the input is "Hello", the output should be "Hello, world!".
3. Write a couple of HCL blocks that combined create a conditional output based in some input. For example, if the input is "true", the output should be "Hello, world!". If the input is "false", the output should be "Goodbye, world!".
4. Write a couple of HCL blocks that create some random outputs based on some input. Hint: Take a look at the `random_pet_name` and `random_string` resources.
5. Create an HCL locals block that calculates the sum of two variables, "num1" and "num2", and stores the result in a local variable named "sum". Use interpolation to display the value of "sum" in an output.

## Break (15 minutes)

## Session 4: Getting Started with Terraform (45 mins)

- Setting up Terraform on your machine
- Initializing a Terraform project
- Defining and managing resources with Terraform
- Understanding Terraform state management
- Interactive: Demonstration and hands-on practice of initializing and running a Terraform project

### Hands-on exercises

1. Install Terraform.
2. Install Azure CLI.
3. Create a directory for your Terraform project.
4. Initialize your Terraform project.
5. Write an HCL block that defines an Azure resource group named "myResourceGroup" with the location set to "norwayeast".
6. Write an HCL block that creates an Azure storage account with the following properties:
   - Name: "mystorageaccount"
   - Resource group: "myResourceGroup"
   - Location: "norwayeast"
   - Account kind: "StorageV2"
   - Access tier: "Hot"
   - Replication type: "LRS"
   - Note that the storage account name needs to be globally unique. Bonus points if you find a different method than adding your own initials. Hint: look at the `random_string` resource.
7. Create an HCL variable named "vm_count" and set its value to 3. Use interpolation to define a resource block that creates an Azure virtual machine with a count equal to the value of "vm_count". Each virtual machine should have a unique name and use the same image and size.
8. Define an HCL module named "network" that takes input variables "subnet_name" and "vnet_name". Within the module, create an Azure virtual network with the provided name and a subnet with the provided name.

## Session 5: Terraform Providers (45 mins)

- Overview of Terraform providers and their role
- Understanding Terraform providers and their role in infrastructure provisioning
- Installing and configuring providers
- Exploring common providers (e.g., Azure, AWS, GCP)
- Managing provider versions and updates
- Interactive: Guided exercises to configure Spotify provider for playlist management.

### Hands-on exercises

Follow the guide [here](https://developer.hashicorp.com/terraform/tutorials/community-providers/spotify-playlist) or just look at the demonstration. **Requires Docker Desktop on your client and a Spotify account.**

## Lunch (30 minutes)

## Session 6: Authenticating to Azure with Terraform (45 mins)

- Introduction to Azure Resource Manager (ARM)
- Authenticating to Azure using Service Principal and Managed Identity
- Provisioning Azure resources with Terraform
- Managing access control and permissions in Azure
- Interactive: Step-by-step walkthrough of authenticating to Azure using Terraform and deploying Azure resources

### Hands-on exercises

#### Azure CLI manual authentication

- Authenticate to Azure with Azure CLI.
- Use the authenticated Azure CLI session to deploy an Azure resource group.

#### Azure Service Principal authentication

- Store service principal credentials in environment variables.
- Use the service principal credentials to authenticate to Azure and deploy an Azure resource group.

#### Azure Managed Identity authentication

- Run Terraform from an Azure virtual machine with a managed identity.
- Create an Azure resource group with Terraform from an Azure virtual machine with a managed identity.

## Session 7: Advanced Terraform Topics (45 mins)

- Automating Terraform workflows with GitHub Actions or other CI/CD tools
- Integrating Terraform with Azure DevOps pipelines
- Best practices for Terraform project organization
- Using Terraform modules from the Terraform Registry
- Terraform best practices and common pitfalls
- Debugging Terraform deployments and understanding error messages
- Demonstration: Deploying Azure Landing Zones framework from Azure Terraform module with GitHub actions workflows.

## Break (15 minutes)

## Session 8: Terraform Backends and State Management (45 mins)

- Understanding different backend types (local, remote, etc.)
- Configuring and utilizing remote backends (e.g., Azure Storage, AWS S3)
- Managing Terraform state in a collaborative environment
- State locking and concurrent operations
- Managing large-scale state files and state file optimization
- State migration and manipulation techniques (tf import, tf state mv, etc.)
- Interactive: Test out different backend types and state management techniques

### Hands-on exercises

#### Local backend

- Initialize a Terraform project with a local backend.
- Deploy an Azure resource group with Terraform.
- Change the name of the resource group in the Terraform configuration.
- Deploy the Terraform configuration again and observe the changes.
- Inspect the state file in the local backend.

#### Remote backend

- Create an Azure Storage account.
- Create a container in the Azure Storage account.
- Initialize a Terraform project with a remote backend.
- Deploy an Azure resource group with Terraform.
- Inspect the state file in the Azure Storage account.

## Session 9: Q&A and Recap (30 minutes)

- Answering participant questions
- Recap of key concepts and best practices
- Additional resources and next steps for further learning
- Interactive: Open forum for participants to ask questions and share their learnings
