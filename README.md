# AzurePowerBoard
is an OnOff Boarding tool built with Blazor and Azure AD. You can find more information about Blazor and Azure AD in this tutorial.

## Setup

1. Managers   
- 1.1 Assign the Managers to the User Administrator role 
In the Azure Active Directory blade, click on Roles and administrators.On the Roles and administrators blade, click on the User Administrator role.
On the User Administrator blade, click Add assignments.

- 1.2 Create Azure-Group AzurePowerBoard-Manager: 
This AD-group is needed for sending employees to other managers.
Create the group and then add all the manangers.
Look after the GroupID and post it EditUser line 94
´´´ managers = await FetchGroupMembers("POST-OBJECT-GROUP-ID-HERE"); /// Task,  Add the Object-id from the ad-group AzurePowerBoard-Manager, Fetch Manager Details from MS-Graph, Table Content for the manager dropbox menu ´´´

2. Azure Application 
- 2.1 Create an Azure app by following the steps in this [quickstart guide](https://learn.microsoft.com/en-us/azure/active-directory/develop/quickstart-register-app):
   - Go to the Azure portal (https://portal.azure.com) and sign in with your Azure account.
   - Create a client secret in "Certificates & secrets".
   - In "API Permissions", add the following permissions:
     - Directory.Read.All
     - User.Read
     - User.Read.All
     - User.ReadWrite
     - User.ReadWrite.All
     - GroupMember.Read.All 

Click on "Integrations assistant":
   - Select "Single Page App (SPA)".
   - When asked if the application is calling APIs, select "Yes".
   - Click on "Evaluate my app registration".
   - Click on "Configure a redirect URI for a SPA using authorization code flow by adding a single-page application platform".
   - In the "Add a platform" section, select "Single Page Application". Add the correct Redirect URI (e.g., https://localhost:5001/signin-oid) for your development environment.
   - Continue the wizard.

Optional : Deny all user except pure admin roles to log in to the Azure Portal, by using Azure Active Directory's Conditional Access policies. 
