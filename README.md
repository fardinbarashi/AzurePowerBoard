# AzurePowerBoard
is an OnOff Boarding tool built with Blazor and Azure AD. You can find more information about Blazor and Azure AD in this tutorial.

## Setup
1. Managers

1.1 Assign the Managers to the User Administrator role 
In the Azure Active Directory blade, click on Roles and administrators.On the Roles and administrators blade, click on the User Administrator role.
On the User Administrator blade, click Add assignments.

1.2 Create Azure-Group AzurePowerBoard-Manager: 
This AD-group is needed for sending employees to other managers.
Create the group and then add all the manangers.

2. Azure Application 
2.1 Create an Azure app by following the steps in this [quickstart guide](https://learn.microsoft.com/en-us/azure/active-directory/develop/quickstart-register-app):
   - Go to the Azure portal (https://portal.azure.com) and sign in with your Azure account.
   - Create a client secret in "Certificates & secrets".
   - In "API Permissions", add the following permissions:
     - Directory.Read.All
     - User.Read
     - User.Read.All
     - User.ReadWrite
     - User.ReadWrite.All

Click on "Integrations assistant":
   - Select "Single Page App (SPA)".
   - When asked if the application is calling APIs, select "Yes".
   - Click on "Evaluate my app registration".
   - Click on "Configure a redirect URI for a SPA using authorization code flow by adding a single-page application platform".
   - In the "Add a platform" section, select "Single Page Application". Add the correct Redirect URI (e.g., https://localhost:5001/signin-oid) for your development environment.
   - Continue the wizard.

3. App Roles
Click on "App Roles" and then "Assign User and groups" to assign roles to users: - [App Roles]([https://learn.microsoft.com/en-us/azure/active-directory/develop/quickstart-register-app](https://learn.microsoft.com/en-us/azure/active-directory/develop/scenario-protected-web-api-verification-scope-app-roles?tabs=aspnetcore):

   - Normal users: Add all the users who should have access to the application.
     - Name: NormalUser
     - Display Name: Normal User
     - Description: This role grants access to view and update the user's own profile.
     - Value: NormalUser

   - Super users: Add all the users who should have administrative access.
     - Name: SuperUser
     - Display Name: Super User
     - Description: This role grants access to manage user profiles and perform administrative actions.
     - Value: SuperUser (or any other identifier you prefer, as long as it matches your application's code)

Make sure to follow these steps carefully to set up AzurePowerBoard with the required configurations and permissions.

Optional : Deny all user except pure admin roles to log in to the Azure Portal, by using Azure Active Directory's Conditional Access policies. 
