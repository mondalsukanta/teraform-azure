# teraform-azure
Azure cloud infrastructure automation using Terraform

Azure Provider -
https://www.terraform.io/docs/providers/azurerm/index.html

1) Terraform Variables set in Terraform cloud -
location = "eastus"
admin_username = "vm01_admin"
admin_password  = "******"

2) Login to Azure account
az login

3) Create a Service Principal
https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal
https://www.terraform.io/docs/providers/azurerm/guides/service_principal_client_secret.html
Get subscription ID
az account list --query [*].[name,id]
Replace with Subscription ID above -
az ad sp create-for-rbac --role="Contributor" --scopes="/subscriptions/{SubID}" -n TerraformTesting | ConvertFrom-Json

This command will output 5 values:
{
  "appId": "00000000-0000-0000-0000-000000000000",
   displayName : TerraformTesting
   name        : http://TerraformTesting
  "password": "0000-0000-0000-0000-000000000000",
  "tenant": "00000000-0000-0000-0000-000000000000"
}

These values map to the Terraform variables like so:
appId is the client_id defined above.
password is the client_secret defined above.
tenant is the tenant_id defined above.

4) Terraform CLI commands -
### Intialise the Terraform ####
terraform init

##### Validate the plan ######
terraform plan

##### Apply plan #####
terraform apply
terraform apply -auto-approve 

#### Inspect terraform state ####
terraform show

##### To list specific resource details ###
terraform state show 'azurerm_resource_group.rg'

##### To delete the resource #####
terraform plan -destory
terraform destory

5) Environment Variables set in Terraform cloud -
ARM_SUBSCRIPTION_ID,ARM_CLIENT_ID,ARM_TENANT_ID,ARM_CLIENT_SECRET
Properties defined in Azure login - Azure Active Directory -> App registrations
