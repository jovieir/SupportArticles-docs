---
title: Troubleshoot user access issues for different environments
description: Discover how to execute diagnostic checks for user permissions in various environments, along with the requirements needed for access.
author: sericks007
ms.author: sericks
ms.reviewer: paulliew, sericks
ms.custom: sap:Microsoft Dataverse\Environment and app access issues
ms.component: pa-admin
ms.date: 02/20/2025
search.audienceType: 
  - admin
---
# Troubleshoot user access issues for different environments

Multiple factors affect user access to environments. Administrators can use the **Run diagnostics** command to assess user access to an environment, and get details and mitigation suggestions as to why a user can or can't access the environment.

To access an environment, a user must meet the following criteria:

1. Be enabled for sign-in in Microsoft Entra ID.
2. Have a valid license that has a Dynamics 365 or Microsoft Power Platform recognized service plan, or the environment must have active per-app plans.
3. Be a member of the environment's Microsoft Entra group (if one has been associated with the environment).
4. Have at least one Dataverse security role assigned directly to them or to a [group team](/power-platform/admin/manage-group-teams) they're a member of.

A user's level of access within the environment and to the resources (apps and data) in the environment is determined by the privileges defined in the security roles assigned to that user. Their access mode being [Administrative](/power-platform/admin/create-users#create-an-administrative-user-account) or [Read-Write](/power-platform/admin/create-users#create-a-read-write-user-account) also determines their level of access within an environment.

## User diagnostics

Use the following steps to run user access diagnostics on a user in an environment.

1. In the [Power Platform admin center](https://admin.powerplatform.microsoft.com), select an environment.

2. Select **Settings** > **Users + permissions** > **Users**.  

3. Select a user.

4. Select **Run diagnostics**.

5. Review the details for the user, and take any needed corrective actions.

> [!NOTE]
> The action of running or rerunning diagnostics will force the user information in Microsoft Entra ID to synchronize to the environment's Dataverse database to provide up-to-date status on the user's properties. If the diagnostic run doesn't eliminate the root cause of a user access issue, please provide the results of the diagnostic run in the support ticket you create; this will greatly help Microsoft Support engineers to resolve your issue faster.

## Access issues

The following issues are documented below. If you don't see your issue:

- See if you can get your question answered here: <https://powerusers.microsoft.com/t5/Power-Apps-Community/ct-p/PowerApps1>.
- Create a [support request](https://powerapps.microsoft.com/support/).

### Diagnostic tool for user permissions in the Power Platform admin center

Several factors influence user access in an environment. To help administrators with diagnosing user access to an environment and reasons for access or no access, the new "Run diagnostics" feature in the Power Platform admin center provides basic access diagnostics for individual users in the environment. The feature helps to detect potential causes to user sign-in and other issues and suggests potential mitigations. See [User diagnostics](#user-diagnostics).

### Dataverse security roles to users

When an error screen stating the user has no roles is encountered, a system administrator needs to assign roles to the user. Roles can be assigned directly to the user, or to a group team that the user is a part of. For information on how to assign Dataverse security roles to a user, see:
[Assign a security role to a user](/power-platform/admin/assign-security-roles).

### Troubleshoot record visibility issues

See [How access to a record is determined](/power-platform/admin/how-record-access-determined).

### Troubleshoot license and membership issues

1. Verify if a license has been assigned to the user and assign one if not already. See: [Add a license to a user account](/power-platform/admin/assign-licenses).
2. Once a license is assigned, it may take some time for the license change to sync to the environment. To trigger a sync for this user, the system administrator for the environment can read the user to the environment. See: [Add users to an environment that has a Dataverse database](/power-platform/admin/add-users-to-environment#add-users-to-an-environment-that-has-a-dataverse-database).

### Troubleshoot access issues

1. As a system administrator of the environment, verify that the environment is associated with any Microsoft Entra group. See: [Associate a security group with an environment](/power-platform/admin/control-user-access#associate-a-security-group-with-an-environment).
2. Ensure the user with the access issue is a member of the group associated with the environment. See: [Create a security group and add members to the security group](/power-platform/admin/control-user-access#create-a-security-group-and-add-members-to-the-security-group).
3. Once user membership in the environment's group is updated, it may take some time for the change to sync to the environment. To trigger a sync for this user, the system administrator for the environment can read the user to the environment. See: [Add users to an environment that has a Dataverse database](/power-platform/admin/add-users-to-environment#add-users-to-an-environment-that-has-a-dataverse-database).

### Troubleshoot permission issues

You don't have sufficient permissions to access customer engagement apps (Dynamics 365 Sales, Dynamics 365 Customer Service, Dynamics 365 Field Service, Dynamics 365 Marketing, and Dynamics 365 Project Service Automation). A system administrator needs to complete the following steps.  
  
1. In the Power Platform admin center, select an environment.

2. Select **Settings** > **Users + permissions** > **Users**.  
  
3. Open the user record.  
  
4. Select **More Commands** (![More commands button.](../admin/media/not-available.png "More commands button")) > **Manage Roles**.  
  
5. Make note of the role assigned to the user. If appropriate, select a different security role. Close the Manage User Roles dialog box.  
  
6. Select **Security** > **Security Roles**.  
  
7. Select the security role from step 4.  
  
8. Select **Core Records**.  
  
9. Confirm that the **Read** permission for **User Entity UI Settings** is set to the User level (a yellow circle with a wedge-shaped segment).  
  
     If the security role is missing this permission, the system administrator will need to change this setting by clicking or tapping on it.  
  
   ![User Entity UI settings.](../admin/media/user-entity.png "User Entity UI settings")  

### Troubleshoot unaccounted user issues

In some cases, users aren't automatically provisioned into environments.

If a user meets all access requirements but is still missing from an environment, the user may fall into one of the following cases:

1. Users with only Office licenses (with Dataverse plan enabled) won't be pre-provisioned into environments.

2. Owners of Microsoft Entra groups that are associated with environments won't be pre-provisioned.

3. Members of Microsoft Entra groups that are part of a Group Team created for the Microsoft Entra group won't be pre-provisioned.

4. Users won't be pre-provisioned into Microsoft Dataverse for Teams environments.

Although these users aren't pre-provisioned, they can be added to environments through on-demand sync. See the section below for ways to add or refresh users on demand.

### Troubleshoot on demand user management

As mentioned above, there are cases where users aren't provisioned automatically. Additionally, there may be delays in reflecting the users' latest status in environments. In such cases, adding or refreshing specific users on demand can be helpful.

There are multiple ways to do this:

1. **Just-in-time (JIT) user provisioning**: When users access an environment URL, access requirements are checked at the time of sign-in and qualified users are added to the environment.

2. **User impersonation call**: Impersonation call triggers a JIT sync for the user. See [How to impersonate a user](/powerapps/developer/common-data-service/webapi/impersonate-another-user-web-api#how-to-impersonate-a-user).

3. **Add users** in the Power Platform admin center: Admins can add or refresh users. See [Add users to an environment](/power-platform/admin/add-users-to-environment).

4. **PowerShell cmdlets**: See [PowerShell support for Power Apps](/power-platform/admin/powerapps-powershell#power-apps-cmdlets-for-administrators).

5. **Connectors**: See [Power Platform for Admins](/connectors/powerplatformforadmins/#force-sync-user).

6. **Power Automate template**: See [Force Sync Microsoft Entra Group members to specified CDS instance](https://us.flow.microsoft.com/galleries/public/templates/6e4162ca7afc48479e3ad1caadc6c1e6/force-sync-azure-active-directory-group-members-to-specified-cds-instance/).

### Known issue

The check for the presence of security roles assigned to a user only checks for roles directly assigned to the user and can't currently check for roles inherited through group team memberships.

[!INCLUDE[footer-include](../../includes/footer-banner.md)]
