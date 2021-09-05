# GitHub Actions workflows (CI/CD)

## Setup instructions

These are onetime configuration steps required to set up the GitHub Actions workflows (pipelines). After the steps the [TRE deployment workflow](../.github/workflows/deploy_tre.yml) is ready to run.

1. Create service principal and set their [repository secrets](https://docs.github.com/en/actions/reference/encrypted-secrets) as explained in [Bootstrapping](./bootstrapping.md#create-service-principals)
1. Create app registrations for auth based on the [Authentication & authorization](./auth.md) guide
1. Set other repository secrets as explained in the table below

*Required repository secrets for the CI/CD.*
| Secret name | Description |
| ----------- | ----------- |
| `AZURE_CREDENTIALS` | Explained in [Bootstrapping - Create service principals](./bootstrapping.md#create-service-principals). Main service principal credentials output. |
| `TF_STATE_CONTAINER` | The name of the blob container to hold the Terraform state. By convention the value is `tfstate`. |
| `MGMT_RESOURCE_GROUP` | The name of the shared resource group for all Azure TRE core resources. |
| `STATE_STORAGE_ACCOUNT_NAME` | The name of the storage account to hold the Terraform state and other deployment artifacts. E.g. `mystorageaccount`. |
| `LOCATION` | The Azure location (region) for all resources. E.g. `westeurope` |
| `ACR_NAME` | A globally unique name for the Azure Container Registry (ACR) that will be created to store deployment images. |
| `PORTER_OUTPUT_CONTAINER_NAME` | The name of the storage container where to store the workspace/workspace service deployment output. Workspaces and workspace templates are implemented using [Porter](https://porter.sh) bundles - hence the name of the secret. The storage account used is the same as defined by `STATE_STORAGE_ACCOUNT_NAME`. |
| `TRE_ID` | A globally unique identifier. `TRE_ID` can be found in the resource names of the Azure TRE instance; for example, a `TRE_ID` of `tre-dev-42` will result in a resource group name for Azure TRE instance of `rg-tre-dev-42`. This must be less than 12 characters. Allowed characters: Alphanumeric, underscores, and hyphens. |
| `ADDRESS_SPACE` |  The address space for the Azure TRE core virtual network. E.g. `10.1.0.0/22`. Recommended `/22` or larger.  |
| `TRE_ADDRESS_SPACE` | The address space for the whole TRE environment virtual network where workspaces networks will be created (can include the core network as well). E.g. `10.0.0.0/12`|
| `SWAGGER_UI_CLIENT_ID` | The application (client) ID of the [TRE Swagger UI](./auth.md#tre-swagger-ui) service principal. |
| `AAD_TENANT_ID` | The tenant ID of the Azure AD. |
| `API_CLIENT_ID` | The application (client) ID of the [TRE API](./auth.md#tre-api) service principal. |
| `API_CLIENT_SECRET` | The application password (client secret) of the [TRE API](./auth.md#tre-api) service principal. |
| `DEPLOY_GITEA` | If set to `false` disables deployment of the Gitea shared service. |
| `DEPLOY_NEXUS` | If set to `false` disables deployment of the Nexus shared service. |
| `TEST_APP_ID` | The application (client) ID of the [E2E Test app](./auth.md#tre-e2e-test) service principal. |
| `TEST_USER_NAME` | The username of the [E2E Test User](./auth.md#end-to-end-test-user). |
| `TEST_USER_PASSWORD` | The password of the [E2E Test User](./auth.md#end-to-end-test-user). |
| `TEST_WORKSPACE_APP_ID` | The application (client) ID of the [Workspaces app](./auth.md#workspaces) service principal. |
