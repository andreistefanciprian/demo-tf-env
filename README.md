# Description

This repo is meant to store terraform parameters for building GCP infrastructure:

* .envrc file stores environment variables.
* tfvars.json file stores terraform variables.

Note: This repo doesn't have any infrastructure terraform code.

The terraform repository is used for building the infrastructure is loaded from a module that sits in a git repository:
```bash
# specify terraform code repository tag in the .envrc file
export TF_CLI_ARGS_init="-from-module=git::git@github.com:andreistefanciprian/demo-tf-code.git//firewall_rules?ref=tags/0.0.2"
```

## How to run terraform manually

```bash
cd firewall_rules

# load env vars
source .envrc
# or
direnv allow .

# store gcp service account credentials path as env var
export GOOGLE_APPLICATION_CREDENTIALS="$HOME/${GCP_PROJECT}-sa.json"

# check plan infra
make plan

# build infra
make apply

# destroy infra make destroy
make destroy
```