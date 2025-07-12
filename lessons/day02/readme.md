# Day02 - Terraform Providers

## What is a terraform provider?

- Providers are plugins using which we call the cloud APIs or any third-party APIs for infra provisioning and management.

<img width="634" alt="image" src="https://github.com/user-attachments/assets/e451a76f-75ea-4000-b63f-3aec5b313810" />

Terraform version is different and terraform providers version is different. terraform provider is maintained separately from terraform. It could be maintained by third-party such as
Azure, AWS, GCP and so on. or it could be maintained in joint collaboration between Hashicorp and that provider. 

-> Terraform Version: This is version of the Terraform software. This is the core software you install on your machine. It decides how Terraform itself works—how it reads code, plans, applies, or destroys resources.

Examples: Terraform v1.5.0, Terraform v1.8.3

-> Provider Version = The Version of the Plugin. Each provider knows how to talk or communicate to a specific cloud platform (like Azure, AWS, GCP) or service (like Kubernetes or GitHub).

Example:

azurerm provider v3.76.0 knows how to talk to Azure resources.

aws provider v5.10.0 knows how to manage AWS stuff.

The provider is what actually does the work—creates VMs, sets up networks, etc. The provider version determines what specific resources and features are supported.

🧠 Putting It Together:
When you run Terraform, here’s what happens:

⦁	Terraform core reads your configuration (.tf files).

⦁	It then calls the appropriate provider to carry out the job.

⦁	Each provider version has its own rules and capabilities.

⦁	Terraform itself doesn’t know how to create an Azure VM, it relies on the Azure provider for that.

There different types of Terraform providers:
-> Official - Built and maintained by HashiCorp (the company that created Terraform)
   Examples: Azure, AWS, GCP
   These are 100% trusted, regularly updated, and tested deeply.

-> Partner - Made by Cloud Vendors like Datadog (DNS & edge security), cloudflare (cloud monitoring), newrelic (cloud observability) but verified by HashiCorp. These are officially supported, but not made by HashiCorp. The cloud company itself creates the provider and keeps it updated.

-> Community - Made by individuals or small teams, not officially verified. 

-> What does Terraform providers do?
   When you run Terraform commands, the provider takes the request, hits the target API (just like you would manually call an API to create a virtual machine), provisions the resources, and then displays the response on your screen. These are nothing but plugins.
   Why do we need plugins?
   It is required so that it could support multiple services, they have different variables and authentication mechanism and so on. So, API shold be called or accessed through standardized process, so these plugins provide that process. For example, we have Azurerm, Azurerm will help translating the Terraform configuration files into the language that Azure understands.

⦁	Each provider is designed to work with a specific platform (like Azure).
⦁	Providers support many services (VMs, storage, networks, firewalls, etc.).
⦁	They use Terraform syntax to define resources, which then call the platform’s API in the background.


## Provider version v/s Terraform core version

<img width="412" alt="image" src="https://github.com/user-attachments/assets/18b67936-5744-43dc-a748-552544969591" />

## Why version matters

<img width="554" alt="image" src="https://github.com/user-attachments/assets/2980dbf7-0556-4618-acab-f85ad10db2ec" />

## Version constraints and operators

![image](https://github.com/user-attachments/assets/9bccafe8-78a9-4def-9b7b-e745b207792d)


