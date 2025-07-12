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
⦁	Providers are specified within a `terraform` block in your configuration files, often under `required_providers`.
⦁	You must configure the provider, including specifying its source and version. For example, `azurerm` has the source `HashiCorp/azurerm`. that means it is not a partner provider, it is build and maintained by Hashicorp itself. It resides in the terraform Haschicorp registry.


## Why version matters

<img width="554" alt="image" src="https://github.com/user-attachments/assets/2980dbf7-0556-4618-acab-f85ad10db2ec" />
Importance of Locking Provider Versions**:
    *   It is a **best practice to specify provider versions** in your configuration files.
    *   If you don't specify a version, Terraform will default to using the latest available version.
    *   **Your configuration might not be compatible with the latest version**, which can cause your code to break if fields or functionalities you are using are changed or deleted in newer versions.
    *   **Locking the version** means ensuring Terraform uses a specific, tested version of the provider.
    *   The **rule of thumb** is to use the version for which you have developed and thoroughly tested your code.
    *   When upgrading a provider version, you should always do so in your local/test environment first to ensure no breaking changes before promoting it to higher environments.

## Version constraints and operators

![image](https://github.com/user-attachments/assets/9bccafe8-78a9-4def-9b7b-e745b207792d)

*   **Provider Version Operators**:
    *   You can use different operators to control which provider versions Terraform can use:
        *   `=` (Equal to): Uses an **exact version** (e.g., `3.0.2`), even if newer versions are available.
        *   `!=` (Not equal to): **Excludes a specific version**; uses any other latest version.
        *   `>=` (Greater than or equal to): Uses the specified version or any newer version (e.g., `>= 1.1.0` will use 1.1.0 or any newer version available like 1.2.0, 2.0.0, etc.).
        *   `<` (Less than): Uses any version older than the specified one.
        *   `<=` (Less than or equal to): Uses the specified version or any older version.
        *   **`~>` (Tilde and greater than): The most important operator for version constraints**.
            *   This operator allows only the **rightmost non-zero segment** of the version to increment.
            *   Example 1: `~> 3.0.2` allows `3.0.5` or `3.0.10` but **not** `3.1.0` or `4.0.0`. Only the patch version (`.2`, `.5`, `.10`) can change.
            *   Example 2: `~> 1.1` allows `1.2`, `1.3`, etc., but **not** `2.0`. Only the minor version (`.1`, `.2`, `.3`) can change.




