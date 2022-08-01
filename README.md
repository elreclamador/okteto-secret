# GitHub Actions for Okteto Cloud

## Automate your development workflows using Github Actions and Okteto Cloud
GitHub Actions gives you the flexibility to build an automated software development workflows. With GitHub Actions for Okteto Cloud you can create workflows to build, deploy and update your applications in [Okteto Cloud](https://cloud.okteto.com).

Get started today with a [free Okteto Cloud account](https://cloud.okteto.com)!

## Github Action for Applying Resources in Okteto Cloud

You can use this action to create secrets in your Okteto Cloud namespace. This is equivalent to running `kubectl create secret generic <name> --from-file=<path>` or `kubectl create secret generic <name> --from-literal=<literal>`.

## Inputs

### `name`

Secret name.

### `path`

Path to files that will be included as secrets. Can be a file or a directory. If not specified, it will seek for literal.

### `literal`

Literal that will be included as secret. If not specified, it will seek for path.

### `namespace`

The Okteto namespace to use. If not specified it will use the namespace specified by the `namespace` action.

## Example usage

This example runs the login action, activates a namespace and creates a secret.

```yaml
# File: .github/workflows/workflow.yml
on: [push]

name: example

jobs:

  devflow:
    runs-on: ubuntu-latest
    steps:
    - name: checkout
      uses: actions/checkout@master
      
    - uses: okteto/login@master
      with:
        token: ${{ secrets.OKTETO_TOKEN }}
    
    - name: "Activate personal namespace"
      uses: okteto/namespace@master
      with:
        name: cindylopez

    - name: "Create my-secret"
      uses: elreclamador/okteto-secret@master
      with:
        name: my-secret
        path: secret.txt
```

