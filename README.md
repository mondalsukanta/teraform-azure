# teraform-azure
Azure cloud infrastructure automation using Terraform

<h1>Azure Provider</h1>
https://www.terraform.io/docs/providers/azurerm/index.html

<h2>1) Terraform Variables set in Terraform cloud -</h2>
location = "eastus", admin_username = "vm01_admin", admin_password  = "******"

<h2>2) Login to Azure account</h2>
az login

<h2>3) Create a Service Principal</h2>
https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal<br>
https://www.terraform.io/docs/providers/azurerm/guides/service_principal_client_secret.html<br>
Get subscription ID<br>
az account list --query [*].[name,id]<br>
Replace with Subscription ID above -<br>
az ad sp create-for-rbac --role="Contributor" --scopes="/subscriptions/{SubID}" -n TerraformTesting | ConvertFrom-Json<br>
<p> 
  This command will output 5 values: <br>
  {<br>
    "appId": "00000000-0000-0000-0000-000000000000",<br>
     displayName : TerraformTesting<br>
     name        : http://TerraformTesting<br>
     "password": "0000-0000-0000-0000-000000000000",<br>
     "tenant": "00000000-0000-0000-0000-000000000000"<br>
  }<br>
  </p>
<p>
These values map to the Terraform variables like so:
 appId is the client_id defined above.
 password is the client_secret defined above.
 tenant is the tenant_id defined above.
</p>
<h2>4) Terraform CLI commands -</h2>
<ul>
<li>### Intialise the Terraform ####</li>
terraform init

<li>##### Validate the plan ######</li>
terraform plan

<li>##### Apply plan #####</li>
terraform apply
terraform apply -auto-approve 

<li>#### Inspect terraform state ####</li>
terraform show

<li>##### To list specific resource details ###</li>
terraform state show 'azurerm_resource_group.rg'

<li>##### To delete the resource #####</li>
terraform plan -destory
terraform destory

</ul>

<h2>5) Environment Variables set in Terraform cloud -</h2>
ARM_SUBSCRIPTION_ID,ARM_CLIENT_ID,ARM_TENANT_ID,ARM_CLIENT_SECRET<br>
Properties defined in Azure login - Azure Active Directory -> App registrations<br>
