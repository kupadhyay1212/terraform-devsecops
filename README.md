# terraform-devsecops
A demo implementing DevSecOps and GitOps for IAC- Terraform with Checkcov

![image](https://github.com/kupadhyay1212/terraform-devsecops/assets/60917359/207fdb4b-04a5-41b4-af83-7977970b7500)


we will go through how we can perform automated static analysis for Terraform code using Checkcov and GitHub Actions.
# Analyze Terraform Directory
To scan, you can run:

## checkov -d "terraform root directory" - compact
 
 When you run checkcov with default settings, it will exit with error code 1 on failure. This will stop your workflow/pipeline. To avoid this you can use the -soft-fail switch. This will enable checkcov to list any misconfiguration, but will not stop your workflow
 
 # Analyse Terraform plan
 Checkcov can also analyze a Terraform plan. The plan must be saved as json. I prefer this as a point of proof for any misconfiguration that maybe was not captured before the plan step.
 
## terraform plan -out tfplan
## terraform show -json tfplan > tfplan.json
## checkov -f tfplan.json

# Run in a Container
You can run checkcov from a container. It’s the best and most probably the recommended way one would run this in a production setting. The best part of it is you get the environment each time, and you don't need to bother installing all the dependencies in your workflow/pipeline.

docker run --tty --volume \
/path_to_your_awesome_project/:/tf \
--workdir /tf bridgecrew/checkov --directory /tf

# Run in Pre-Commit Stage
Checkcov is a plugin you can use with pre-commit hooks. You can use it in your pre-commit config file like https://www.checkov.io/4.Integrations/pre-commit.html

![image](https://github.com/kupadhyay1212/terraform-devsecops/assets/60917359/c292e305-2ee4-4d91-89fe-3724b204c821)

# Run in CI/CD workflow

One good thing with pre-commit hooks is to enforce adherence on the developer's computer, but pre-commit hooks can be silenced locally by a simple flag hence it’s good to run this in your workflow/pipeline to force adherence to company policy. You can’t turn this off in the repository where security measures are configured.

In addition to running checkcov in containers and via command as we did above, we can have a GitHub Workflow and soft fail for the pre-commit hook.

![image](https://github.com/kupadhyay1212/terraform-devsecops/assets/60917359/890b914f-c672-4271-8f3f-27a51a388f86)

You can check the whole file https://github.com/kupadhyay1212/terraform-devsecops


