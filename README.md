# demo-terraform-devsecops
A demo implementing DevSecOps and GitOps for IAC- Terraform with Checkcov

![image](https://github.com/kupadhyay1212/terraform-devsecops/assets/60917359/207fdb4b-04a5-41b4-af83-7977970b7500)


we will go through how we can perform automated static analysis for Terraform code using Checkcov and GitHub Actions.
# Analyze Terraform Directory
To scan, you can run:

checkov -d "terraform root directory" - compact
 
 When you run checkcov with default settings, it will exit with error code 1 on failure. This will stop your workflow/pipeline. To avoid this you can use the -soft-fail switch. This will enable checkcov to list any misconfiguration, but will not stop your workflow


