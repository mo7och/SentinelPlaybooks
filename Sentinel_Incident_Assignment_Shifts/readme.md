# Sentinel_Incident_Assignment_Shifts


author: Jeremy Tan

This playbook will assign Incident owner based on Shifts schedule in Microsoft Teams.

[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Ftatecksi%2FSentinelPlaybooks%2Fmaster%2FSentinel_Incident_Assignment_Shifts%2FSentinel_Incident_Assignment_Shifts.json)


[![Deploy to Azure Gov](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/1-CONTRIBUTION-GUIDE/images/deploytoazuregov.png)](https://portal.azure.us/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Ftatecksi%2FSentinelPlaybooks%2Fmaster%2FSentinel_Incident_Assignment_Shifts%2FSentinel_Incident_Assignment_Shifts.json)



## Pre-requisites:

### 1. Sentinel Workspace details
Kindly obtain the following information:

- Workspace Name

- Workspace Resource Group Name

### 2. Service Principal
Create or use existing Service Principal with Azure Sentinel Responder role.

**Steps to create a new Service Principal:**

Perform the following steps as instructed in this [link](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal):

- Register an application with Azure AD and create a service principal

- Create a new application secret

- Assign a role to the application (assign **Azure Sentinel Responder** role to it)


### 3. Shifts for Teams
[Shifts](https://support.microsoft.com/en-us/office/get-started-in-shifts-5f3e30d8-1821-4904-be26-c3cd25a497d6) schedule has been setup in Microsoft Teams.



## Post Deployment Configurations:

- Once deployed, edit the Logic App and find the connectors (5 in total) with ![](media/Pic1.png). 
- Fix those connectors by adding new connection and sign in to authenticate.
- For Shifts connector, make sure you have selected the Teams channel with Shifts schedule.
    ![](media/Pic3.png?s=50)
- Save the Logic App once you have done.



## Incident Assignment Logics:

Incidents are assigned based on the following criterias:

- Users who are on shift during the time incident assignment
- Users who still have at least **2** hours left before going off shift. 
   You can change this value by modifying the below variable:
       ![](media/Pic4.png?s=100)
- User who has the least incident assignment over the past 24 hours will get the priority first.