# GitHub Action: Terragrunt


This action runs terragrunt `run-all` against the directory you point it to.


## Quick Start (No modules)

```yaml
name: "Terragrunt: name"
on: [push]

jobs:
  terraform:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v3
      - name: Terragrunt
        uses: userbradley/action-terragrunt@v1.0.0
        with:
          directory: "terragrunt"
          serviceAccount: "email@userbradley-cicd.iam.gserviceaccount.com"
```

## Quick Start (With Modules)

By adding in the `sshPrivateKey: ${{ secrets.SSH_KEY }}` it will run Terragrunt with the 

```yaml
name: "Terragrunt: name"
on: [push]

jobs:
  terraform:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v3
      - name: Terragrunt
        uses: userbradley/action-terragrunt@v1.0.0
        with:
          directory: "terragrunt"
          serviceAccount: "email@userbradley-cicd.iam.gserviceaccount.com"
          sshPrivateKey: ${{ secrets.SSH_KEY }}
```

## Dry Run

Dry run is a feature that allows you to test the terragrunt and terraform without applying any changes

```yaml
name: "Terragrunt: name"
on: [push]

jobs:
  terraform:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v3
      - name: Terragrunt
        uses: userbradley/action-terragrunt@v1.0.0
        with:
          directory: "terragrunt"
          serviceAccount: "email@userbradley-cicd.iam.gserviceaccount.com"
          sshPrivateKey: ${{ secrets.SSH_KEY }}
          dryRun: true
```


## Different location for the Provider file

```yaml
name: "Terragrunt: name"
on: [push]

jobs:
  terraform:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v3
      - name: Terragrunt
        uses: userbradley/action-terragrunt@v1.0.0
        with:
          directory: "terragrunt"
          serviceAccount: "email@userbradley-cicd.iam.gserviceaccount.com"
          sshPrivateKey: ${{ secrets.SSH_KEY }}
          dryRun: true
          providerFileLocation: "terraform/location/to/directory" #Do NOT prepend `provider.tf` - it works this out automagically
```

## Inputs

| Input Name             | Required | Default Value         | Example                                            |
|------------------------|----------|-----------------------|----------------------------------------------------|
| `directory`            | `yes`    | `null`                | `terraform/deployments/puppy-ui`                   |
| `providerFileLocation` | `no`     | `terraform/templates` | `terraform/deployments/puppy-ui`                   |
| `sshPrivateKey`        | `no`     | `null`                | `${{ secrets.SSH_KEY }}`                           |
| `dryRun`               | `no`     | `false`               | `true`                                             |

---

Built by Bradley
