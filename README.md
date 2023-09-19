# AzurePowerBoard

# Ongoing Project

is an OnOff Boarding tool built with Blazor and Azure AD.
![Alt text](https://github.com/fardinbarashi/AzurePowerBoard/raw/main/Movie/1.gif)


# Logic
[![Azure Power Board](https://github.com/fardinbarashi/AzurePowerBoard/raw/main/Images/Azure%20Power%20Board.png)](https://github.com/fardinbarashi/AzurePowerBoard/blob/main/Images/Azure%20Power%20Board.png)

# Setup

## 1. Managers   
### - 1.1 Assign the Managers to the User Administrator role 
In the Azure Active Directory, click on "Roles and administrators". Search After "User Administrator" role. Add the manager that shall create users.

### - 1.2 Create Azure-Group AzurePowerBoard-Manager: 
This AD-group is needed for sending employees to other managers.
Create the group and then add all the manangers.
Look after the GroupID and post it EditUser in Line 94
``` 
managers = await FetchGroupMembers("POST-OBJECT-GROUP-ID-HERE"); /// Task,  Add the Object-id from the ad-group AzurePowerBoard-Manager, Fetch Manager  Details from MS-Graph, Table Content for the manager dropbox menu 
```



## 2. Azure Application 
### - 2.1 Create an Azure app by following the steps in this [quickstart guide](https://learn.microsoft.com/en-us/azure/active-directory/develop/quickstart-register-app):
   - Go to the Azure portal (https://portal.azure.com) and sign in with your Azure account.
   - Create a client secret in "Certificates & secrets".
   - In "API Permissions", add the following permissions:
``` 
     - Directory.Read.All
     - User.Read
     - User.Read.All
     - User.ReadWrite
     - User.ReadWrite.All
     - GroupMember.Read.All 
``` 

Click on "Integrations assistant":
   - Select "Single Page App (SPA)".
   - When asked if the application is calling APIs, select "Yes".
   - Click on "Evaluate my app registration".
   - Click on "Configure a redirect URI for a SPA using authorization code flow by adding a single-page application platform".
   - In the "Add a platform" section, select "Single Page Application". Add the correct Redirect URI (e.g., https://localhost:5001/signin-oid) for your development environment.
   - Continue the wizard.

## Optional : Deny login to Azure Portal
Deny all user except pure admin roles to log in to the Azure Portal, by using Azure Active Directory's Conditional Access policies.


## 2. Create new User - Azure AD attribute mapping  
[![Azure AD attribute mapping](https://github.com/fardinbarashi/AzurePowerBoard/blob/main/Images/AzurePowerBoard%20-%20Create%20User.png)

- Identity information
``` 
identityfirstname - givenName -
Description: User's first name.

identitymiddlename - extensionAttributeX
Description: User's middle name. There isn't a standard attribute in Azure AD for middle names. Consider adding it to extensionAttributeX (where "X" could be a number from 1 to 15).

identitylastname - surname
Description: User's last name.

identityssn - extensionAttributeX
Description: User's national identification number. There isn't a standard attribute in Azure AD for middle names. Consider adding it to extensionAttributeX (where "X" can be a number from 1 to 15).

``` 
     
- Job information
``` 
jobinformationjobtitle - jobTitle
Description: User's job title, e.g., "Project Manager" or "Systems Architect".

jobinformationcompanyname - companyName
Description: Company name.

jobinformationdepartment - department
Description: The department where the user works, e.g., "Sales" or "Tech".

jobinformationofficelocation - physicalDeliveryOfficeName
Description: Name or location of the user's office, e.g., "Office 2B" or "Stockholm Main Office".

jobinformationmanager - Automatically taken from the app, Azure AD relation.
``` 

- Contact information
``` 
contactstreetaddress - streetAddress
Description: Street or road of the user's office address.

contactcity - city
Description: City or town of the user's office address.

contactstate - state 
Description: State, province, or region of the user's office address.

contactzip - postalCode
Description: Postal code of the user's office address.

contactcountry - country
Description: Country of the user's office address.

contactbusinessPhone - telephoneNumber
Description: User's primary phone number.

contactmobilePhone - mobile
Description: User's mobile phone number.

contactemail - mail
Description: User's primary email address.
``` 


- Password Options
``` 
passwordfunctionspecialchar -
Description: Function to generate passwords, include special char.

passwordfunctionsimilarchar -
Description: Function to generate passwords. exclude similar char

passwordLength -
Description: Function to generate passwords. password length
``` 

- Username Options
``` 
firstnameUsernameLength -
Description: Function to generate account, include special char.

lastnameUsernameLength -
Description: Function to generate passwords. exclude similar char

usernameoptionsfunctionusenumbers -
Description: Function to generate passwords. User numbers on the username

potusername - Function
``` 


- Account Options
``` 
accountdate -
Description: Function to account, Enable account at specfic date accountdate, deafult is always today.

``` 
