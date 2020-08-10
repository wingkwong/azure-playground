# Create Application ID

## Goal

Create an Application ID (aka service principal) in your Azure AD Tenant (xxxxx.onmicrosoft.com) to facilitate access from Azure Databricks to ADLS Gen 2.

## Steps

Go to Azure Portal > Azure Active Directory > App registrations > New registration

![image](https://user-images.githubusercontent.com/35857179/89767573-cb0ea500-db2c-11ea-8c09-1472e8c18d9c.png)

Provide a name for the application (e.g. ``your-app-serviceprincipal``) and then Register

![image](https://user-images.githubusercontent.com/35857179/89767616-e7124680-db2c-11ea-9d9a-e158acc44ef8.png)

Note down the Application (client) ID & Directory (tenant) ID, and then go to ``Certificates & secrets``

![image](https://user-images.githubusercontent.com/35857179/89768980-fc887000-db2e-11ea-8a9e-2391fe7a77a9.png)

Create a New client secret, and please let us know the secret value

![image](https://user-images.githubusercontent.com/35857179/89767814-41130c00-db2d-11ea-8a02-00c1d9d48c8c.png)

Grant the ``Storage Blob Data Contributor`` role to the newly created Service Principal on the Storage account ``your-storage-account``

![image](https://user-images.githubusercontent.com/35857179/89767962-820b2080-db2d-11ea-9026-98d0b84d794b.png)


## References:

- [How to: Use the portal to create an Azure AD application and service principal that can access resources](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal)

- [Create an Azure service principal with the Azure CLI](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?view=azure-cli-latest#password-based-authentication)