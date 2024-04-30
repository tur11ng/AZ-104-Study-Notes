# Manage Azure identities and governance in Azure

Configure Microsoft Entra ID

### Describe Microsoft Entra ID benefits and features

<figure><img src="../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

### Describe Microsoft Entra concepts

| Concept                  | Description                                                                                                                                                      |
| ------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Identity                 | An object that can be authenticated, including users, applications, or servers. Microsoft Entra ID provides the identity service.                                |
| Account                  | An identity with associated data. Requires a valid identity.                                                                                                     |
| Microsoft Entra account  | An identity created through Microsoft Entra ID or another Microsoft cloud service, stored in Microsoft Entra ID. Also known as a work or school account.         |
| Azure tenant (directory) | A dedicated instance of Microsoft Entra ID representing a single organization. Created automatically when signing up for a Microsoft cloud service subscription. |
| Azure subscription       | Used to pay for Azure cloud services. Each subscription is linked to a single tenant. Multiple subscriptions can be created.                                     |

### Compare Active Directory Domain Services to Microsoft Entra ID

* **Identity solution**: AD DS is primarily a directory service, while Microsoft Entra ID is a full identity solution. Microsoft Entra ID is designed for internet-based applications that use HTTP and HTTPS communications. The features and capabilities of Microsoft Entra ID support strong identity management.
* **Communication protocols**: Because Microsoft Entra ID is based on HTTP and HTTPS, it doesn't use Kerberos authentication. Microsoft Entra ID implements HTTP and HTTPS protocols, such as SAML, WS-Federation, and OpenID Connect for authentication (and OAuth for authorization).
* **Federation services**: Microsoft Entra ID includes federation services, and many third-party services like Facebook.
* **Flat structure**: Microsoft Entra users and groups are created in a flat structure. There are no organizational units (OUs) or group policy objects (GPOs).
* **Managed service**: Microsoft Entra ID is a managed service. You manage only users, groups, and policies. If you deploy AD DS with virtual machines by using Azure, you manage many other tasks, including deployment, configuration, virtual machines, patching, and other backend processes.

### Select Microsoft Entra editions

| Feature                                               | Free      | Premium P1 | Premium P2 |
| ----------------------------------------------------- | --------- | ---------- | ---------- |
| Directory Objects                                     | 500,000   | Unlimited  | Unlimited  |
| Single Sign-on                                        | Unlimited | Unlimited  | Unlimited  |
| Core Identity and Access Management                   | X         | X          | X          |
| Business-to-business Collaboration                    | X         | X          | X          |
| Identity and Access Management for Microsoft 365 apps |           | X          | X          |
| Premium Features                                      |           | X          | X          |
| Hybrid Identities                                     |           | X          | X          |
| Advanced Group Access Management                      |           | X          | X          |
| Conditional Access                                    |           | X          | X          |
| Identity Protection                                   |           |            | X          |
| Identity Governance                                   |           |            | X          |

### Implement Microsoft Entra self-service password reset

https://learn.microsoft.com/en-us/entra/identity/authentication/tutorial-enable-sspr

***

## Configure user and group accounts

### Create user accounts

| User account                    | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| ------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Cloud identity                  | A user account with a cloud identity is defined only in Microsoft Entra ID. This type of user account includes administrator accounts and users who are managed as part of your organization. A cloud identity can be for user accounts defined in your Microsoft Entra organization, and also for user accounts defined in an external Microsoft Entra instance. When a cloud identity is removed from the primary directory, the user account is deleted. |
| Directory-synchronized identity | User accounts that have a directory-synchronized identity are defined in an on-premises Active Directory. A synchronization activity occurs via Microsoft Entra Connect to bring these user accounts in to Azure. The source for these accounts is Windows Server Active Directory.                                                                                                                                                                         |
| Guest user                      | Guest user accounts are defined outside Azure. Examples include user accounts from other cloud providers, and Microsoft accounts like an Xbox LIVE account. The source for guest user accounts is Invited user. Guest user accounts are useful when external vendors or contractors need access to your Azure resources.                                                                                                                                    |

### Manage user accounts

There are several ways to add cloud identity user accounts in Microsoft Entra ID. A common approach is by using the Azure portal. User accounts can also be added to Microsoft Entra ID through Microsoft 365 Admin Center, Microsoft Intune admin console, and the Azure CLI.

### Create bulk user accounts

Microsoft Entra ID supports several bulk operations, including bulk create and delete for user accounts. The most common approach for these operations is to use the Azure portal. Azure PowerShell can be used for bulk upload of user accounts.

### Create group accounts

Microsoft Entra ID allows your organization to define **two different types of group accounts** :

* **Security groups** : They are used to manage member and computer access to shared resources for a group of users. You can create a security group for a specific security policy and apply the same permissions to all members of a group.
* **Microsoft 365 groups** : They provide collaboration opportunities. Group members have access to a shared mailbox, calendar, files, SharePoint site, and more.

#### Things to consider when adding group members

| Access rights  | Description                                                                                                                                                                                                                                                                                                                                                                                |
| -------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Assigned       | Add specific users as members of a group, where each user can have unique permissions.                                                                                                                                                                                                                                                                                                     |
| Dynamic user   | Use dynamic membership rules to automatically add and remove group members. When member attributes change, Azure reviews the dynamic group rules for the directory. If the member attributes meet the rule requirements, the member is added to the group. If the member attributes no longer meet the rule requirements, the member is removed.                                           |
| Dynamic device | (Security groups only) Apply dynamic group rules to automatically add and remove devices in security groups. When device attributes change, Azure reviews the dynamic group rules for the directory. If the device attributes meet the rule requirements, the device is added to the security group. If the device attributes no longer meet the rule requirements, the device is removed. |

### Create administrative units

### Interactive lab simulation

***

## Configure subscriptions

### Identify Azure regions

![](../res/1-manage-azure-identities-and-governance/images/image-1.png)

<figure><img src="../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

#### Things to know about regional pairs

| Characteristic                | Description                                                                                                                                                                                                                                                                                                                |
| ----------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Physical isolation            | Azure prefers at least 300 miles of separation between datacenters in a regional pair. This principle isn't practical or possible in all geographies. Physical datacenter separation reduces the likelihood of natural disasters, civil unrest, power outages, or physical network outages affecting both regions at once. |
| Platform-provided replication | Some services like Geo-Redundant Storage provide automatic replication to the paired region.                                                                                                                                                                                                                               |
| Region recovery order         | During a broad outage, recovery of one region is prioritized out of every pair. Applications that are deployed across paired regions are guaranteed to have one of the regions recovered with priority.                                                                                                                    |
| Sequential updates            | Planned Azure system updates are rolled out to paired regions sequentially (not at the same time). Rolling updates minimizes downtime, reduces bugs, and logical failures in the rare event of a bad update.                                                                                                               |
| Data residency                | Regions reside within the same geography as their enabled set (except for the Brazil South and Singapore regions).                                                                                                                                                                                                         |

### Implement Azure subscriptions

<figure><img src="../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

### Obtain an Azure subscription

### Identify Azure subscription usage

Subscription types :

* Free
* Pay-As-You-Go
* Enterprise Agreement
* Student

### Implement Microsoft Cost Management

https://learn.microsoft.com/en-us/azure/cost-management-billing/manage/cost-management-budget-scenario

### Apply resource tagging

### Apply cost savings

***

***

## Configure Azure Policy

### Create management groups

#### Things to know about management groups

<figure><img src="../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

### Implement Azure policies

### Create Azure policies

### Create policy definitions

Azure Policy offers built-in policy definitions to help you quickly configure control conditions for your resources. In addition to the built-in policies, you can also create your own definitions, or import definitions from other sources.

```json
{
  "mode": "All",
  "parameters": {
    "effect": {
      "type": "String",
      "metadata": {
        "displayName": "Effect",
        "description": "Enable or disable the execution of the policy"
      },
      "allowedValues": [
        "Deny",
        "AuditIfNotExists",
        "Disabled"
      ],
      "defaultValue": "Deny"
    }
  },
  "policyRule": {
    "if": {
      "field": "type",
      "equals": "Microsoft.Storage/storageAccounts"
    },
    "then": {
      "effect": "[parameters('effect')]",
      "details": {
        "type": "Microsoft.Storage/storageAccounts/blobServices/containers",
        "name": "default",
        "existenceCondition": {
          "allOf": [
            {
              "field": "Microsoft.Storage/storageAccounts/enableHttpsTrafficOnly",
              "equals": "true"
            },
            {
              "field": "Microsoft.Storage/storageAccounts/supportsHttpsTrafficOnly",
              "equals": "true"
            }
          ]
        },
        "deploymentScope": "Subscription"
      }
    }
  }
}
```

https://portal.azure.com/#view/Microsoft\_Azure\_Policy/PolicyMenuBlade/\~/Definitions

https://github.com/Azure/azure-policy

### Create an initiative definition

After you determine your policy definitions, the next step is to create an initiative definition for your policies. An initiative definition has one or more policy definitions. One example for using initiative definitions is to ensure your resources are compliant with security regulations.

### Scope the initiative definition

After you create your initiative definition, the next step is to assign the initiative to establish the scope for the policies. The scope determines what resources or grouping of resources are affected by the conditions of the policies.

### Determine compliance

You have your policies defined, your initiative definition created, and your policies assigned to affected resources. The last step is to evaluate the state of compliance for your scoped resources.

***

## Configure role-based access control

### Implement role-based access control

### Create a role definition

<figure><img src="../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

The Actions permissions show the Contributor role has all action privileges. The asterisk "\*" wildcard means "all." The NotActions permissions narrow the privileges provided by the Actions set, and deny three actions:

* Authorization/\*/Delete: Not authorized to delete or remove for "all."
* Authorization/\*/Write: Not authorized to write or change for "all."
* Authorization/elevateAccess/Action: Not authorized to increase the level or scope of access privileges.

The Contributor role also has two permissions to specify how data can be affected:

* "NotDataActions": \[]: No specific actions are listed. Therefore, all actions can affect the data.
* "AssignableScopes": \["/"]: The role can be assigned for all scopes that affect data.

#### Things to know about role definitions

Review the following characteristics of role definitions:

Azure RBAC provides built-in roles and permissions sets. You can also create custom roles and permissions.

The Owner built-in role has the highest level of access privilege in Azure.

The system subtracts NotActions permissions from Actions permissions to determine the effective permissions for a role.

The AssignableScopes permissions for a role can be management groups, subscriptions, resource groups, or resources.

#### Azure RBAC concepts

| Concept            | Description                                                                             | Examples                                                                                                                                                                                         |
| ------------------ | --------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Security principal | An object that represents something that requests access to resources.                  | User, group, service principal, managed identity                                                                                                                                                 |
| Role definition    | A set of permissions that lists the allowed operations.                                 | Azure RBAC comes with built-in role definitions, but you can also create your own custom role definitions. Some built-in role definitions: Reader, Contributor, Owner, User Access Administrator |
| Scope              | The boundary for the requested level of access, or "how much" access is granted.        | Management group, subscription, resource group, resource                                                                                                                                         |
| Role assignment    | An assignment attaches a role definition to a security principal at a particular scope. | - Assign the User Access Administrator role to an admin group scoped to a management group - Assign the Contributor role to a user scoped to a subscription                                      |

#### Things to consider when creating roles

* **Consider using built-in roles**. Review the list of built-in role definitions in Azure RBAC. There are over 100 predefined role definitions to choose from, such as Owner, Backup Operator, Website Contributor, and SQL Security Manager. Built-in roles are defined for several categories of services, tasks, and users, including General, Networking, Storage, Databases, and more.
* **Consider creating custom definitions**. Define your own custom roles to meet specific business scenarios for your organization. You can modify the permissions for a built-in role to meet the specific requirements for your organization. You can also create custom role definitions from scratch.

### Create a role assignment

### Compare Azure roles to Microsoft Entra roles

### Apply role-based access control

### Review fundamental Azure RBAC roles

***

## Configure role-based access control

### Implement role-based access control

#### Things to know about Azure RBAC

* Allow an application to access all resources in a resource group.
* Allow one user to manage VMs in a subscription, and allow another user to manage virtual networks.
* Allow a database administrator (DBA) group to manage SQL databases in a subscription.
* Allow a user to manage all resources in a resource group, such as VMs, websites, and subnets.

#### Azure RBAC concepts

| Concept            | Description                                                                                                                                                                                           | Examples                                                                                                                                                    |
| ------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Security Principal | An object that represents something that requests access to resources.                                                                                                                                | User, group, service principal, managed identity                                                                                                            |
| Role Definition    | A set of permissions that lists the allowed operations. Azure RBAC comes with built-in role definitions, but you can also create your own custom role definitions.                                    | Some built-in role definitions: Reader, Contributor, Owner, User Access Administrator                                                                       |
| Scope              | The boundary for the requested level of access, or "how much" access is granted.                                                                                                                      | Management group, subscription, resource group, resource                                                                                                    |
| Role Assignment    | An assignment attaches a role definition to a security principal at a particular scope. Users can grant the access described in a role definition by creating (attaching) an assignment for the role. | - Assign the User Access Administrator role to an admin group scoped to a management group - Assign the Contributor role to a user scoped to a subscription |

### Things to consider when using Azure RBAC

As you think about how you can implement roles and scope assignments within your organization, consider these points:

* **Consider your requestors**: Plan your strategy to accommodate for all types of access to your resources. Security principals are created for anything that requests access to your resources. Determine who are the requestors in your organization. Requestors can be internal or external users, groups of users, applications and services, resources, and so on.
* **Consider your roles**: Examine the types of job responsibilities and work scenarios in your organization. Roles are commonly built around the requirements to fulfill job tasks or complete work goals. Certain users like administrators, corporate controllers, and engineers can require a level of access beyond what most users need. Some roles can be defined to provide the same access for all members of a team or department for specific resources or applications.
* **Consider scope of permissions**: Think about how you can ensure security by controlling the scope of permissions for role assignments. Outline the types of permissions and levels of scope that you need to support. You can apply different scope levels for a single role to support requestors in different scenarios.
* **Consider built-in or custom definitions**: Review the built-in role definitions in Azure RBAC. Built-in roles can be used as-is, or adjusted to meet the specific requirements for your organization. You can also create custom role definitions from scratch.

### Create a role definition

<figure><img src="../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

#### Things to know about role definitions

* Azure RBAC provides built-in roles and permissions sets. You can also create custom roles and permissions.
* The Owner built-in role has the highest level of access privilege in Azure.
* The system subtracts NotActions permissions from Actions permissions to determine the effective permissions for a role.
* The AssignableScopes permissions for a role can be management groups, subscriptions, resource groups, or resources.

#### Role permissions

| Role name   | Description                                               | Actions permissions | NotActions permissions                                                                                                                           |
| ----------- | --------------------------------------------------------- | ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------ |
| Owner       | Allow all actions                                         | \*                  | n/a                                                                                                                                              |
| Contributor | Allow all actions, except write or delete role assignment | \*                  | <p>- Microsoft.Authorization/<em>/Delete</em><br><em>- Microsoft.Authorization/</em>/Write<br>- Microsoft.Authorization/elevateAccess/Action</p> |
| Reader      | Allow all read actions                                    | /\*/read            | n/a                                                                                                                                              |

***

## Create Azure users and groups in Microsoft Entra ID

### What are user accounts in Microsoft Entra ID?

* **Administrator roles** : Allow users elevated access to control who is allowed to do what. You assign these roles to a limited group of users to manage identity tasks in a Microsoft Entra organization. You can assign administrator roles that allow a user to create or edit users, assign administrative roles to others, reset user passwords, manage user licenses, and more.
* **Member users** : A member user account is a native member of the Microsoft Entra organization that has a set of default permissions like being able to manage their profile information. When someone new joins your organization, they typically have this type of account created for them.
* **Guest users** : Guest users have restricted Microsoft Entra organization permissions. When you invite someone to collaborate with your organization, you add them to your Microsoft Entra organization as a guest user. Then, you can either send an invitation email that contains a redemption link or send a direct link to an app you want to share. Guest users sign in with their own work, school, or social identities. By default, Microsoft Entra member users can invite guest users. Someone with the User Administrator role can disable this default.

```powershell
# create a new user
az ad user create

# create a new user
New-MgUser

$invitations = import-csv c:\bulkinvite\invitations.csv

$messageInfo = [Microsoft.Graph.PowerShell.Models.MicrosoftGraphInvitation]@{ CustomizedMessageBody = "Hello. You are invited to the Contoso organization." }

foreach ($email in $invitations)
   {New-MgInvitation -InviteRedirectUrl https://myapps.microsoft.com -InvitedUserDisplayName $email.Name -InvitedUserEmailAddress $email.InvitedUserEmailAddress -InvitedUserMessageInfo $messageInfo -SendInvitationMessage 
   }

# delete a user
Remove-MgUser

# delete a user
az ad user delete
```

* When you delete a user, the account remains in a suspended state for 30 days. During that 30-day window, the user account can be restored.

### Exercise - Add and delete users in Microsoft Entra ID

### Manage app and resource access by using Microsoft Entra groups

#### Access management in Microsoft Entra ID

* Microsoft Entra roles: Use Microsoft Entra roles to manage Microsoft Entra ID-related resources like users, groups, billing, licensing, application registration, and more.
* Role-based access control (RBAC) for Azure resources: Use RBAC roles to manage access to Azure resources like virtual machines, SQL databases, or storage. For example, you could assign an RBAC role to a user to manage and delete SQL databases in a specific resource group or subscription.

#### Access rights through single user or group assignment

* **Direct assignment**: Assign a user the required access rights by directly assigning a role that has those access rights.
* **Group assignment**: Assign a group the required access rights, and members of the group will inherit those rights.
* **Rule-based assignment**: Use rules to determine a group membership based on user or device properties. For a user account or device's group membership to be valid, the user or device must meet the rules. If the rules aren't met, the user account or device's group membership is no longer valid. The rules can be simple. You can select prewritten rules or write your own advanced rules.

### Exercise - Assign users to Microsoft Entra groups

#### Modify the group to use dynamic assignment

<figure><img src="../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

### Collaborate by using guest accounts and Microsoft Entra B2B

* With Microsoft Entra business to business (B2B), you can add people from other companies to your Microsoft Entra tenant as guest users.
* If your organization has multiple Microsoft Entra tenants, you may also want to use Microsoft Entra B2B to give a user in tenant A access to resources in tenant B. Each Microsoft Entra tenant is distinct and separate from other Microsoft Entra tenants and has its own representation of identities and app registrations.

#### Why use Microsoft Entra B2B instead of federation?

With Microsoft Entra B2B, you don't take on the responsibility of managing and authenticating the credentials and identities of partners. Your partners can collaborate with you even if they don't have an IT department. For example, you can collaborate with a contractor who only has a personal or business email address and no identity management solution managed by an IT department.

Giving access to external users is much easier than in a federation. You don't need an AD administrator to create and manage external user accounts. Any authorized user can invite other users. A line manager could, for example, invite external users to collaborate with their team. When collaboration is no longer needed, you can easily remove these external users.

A federation is more complex. A federation is where you have a trust established with another organization, or a collection of domains, for shared access to a set of resources. You might be using an on-premises identity provider and authorization service like Active Directory Federation Services (AD FS) that has an established trust with Microsoft Entra ID. To get access to resources, all users have to provide their credentials and successfully authenticate against the AD FS server. If you have someone trying to authenticate outside the internal network, you need to set up a web application proxy. The architecture might look something like the following diagram:

<figure><img src="../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

### Exercise - Give guest users access in Microsoft Entra B2B

#### Add guest users to the organization

<figure><img src="../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

#### Add guest users to an application

<figure><img src="../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>

***

## Secure your Azure resources with Azure role-based access control (Azure RBAC)

### What is Azure RBAC?

When it comes to identity and access, most organizations that are considering using the public cloud are concerned about two things:

* **Ensuring that when people leave the organization**, they lose access to resources in the cloud.
* **Striking the right balance between autonomy and central governance**; for example, giving project teams the ability to create and manage virtual machines in the cloud while centrally controlling the networks those VMs use to communicate with other resources.

#### What's Azure RBAC?

<figure><img src="../.gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>

#### How does Azure RBAC work?

To create a role assignment, you need three elements: a security principal, a role definition, and a scope. You can think of these elements as **"who"**, **"what"**, and **"where"**.

1. **Security principal (who)** : A security principal is just a fancy name for a user, group, or application to which you want to grant access.
2. **Role definition** (what you can do) : A role definition is a collection of permissions. It's sometimes just called a role. A role definition lists the permissions the role can perform, such as read, write, and delete. Roles can be high-level, like Owner, or specific, like Virtual Machine Contributor.
3. **Scope (where)** : Scope is the level where the access applies. This is helpful if you want to make someone a Website Contributor, but only for one resource group.

### Exercise - List access using Azure RBAC and the Azure portal

### Exercise - Grant access using Azure RBAC and the Azure portal

### Exercise - View activity logs for Azure RBAC changes

***

## Allow users to reset their password with Microsoft Entra self-service password reset

### Implement Microsoft Entra self-service password reset

#### How SSPR works

The user initiates a password reset either by going directly to the password-reset portal or by selecting the Can't access your account link on a sign-in page. The reset portal takes these steps:

1. **Localization**: The portal checks the browser's locale setting and renders the SSPR page in the appropriate language.
2. **Verification**: The user enters their username and passes a captcha to ensure that it's a user and not a bot.
3. **Authentication**: The user enters the required data to authenticate their identity. They might, for example, enter a code or answer security questions.
4. **Password reset**: If the user passes the authentication tests, they can enter a new password and confirm it.
5. **Notification**: A message is sent to the user to confirm the reset. There are several ways you can customize the SSPR user experience. For example, you can add your company logo to the sign-in page so users know they're in the right place to reset their password.

#### Authenticate a password reset

| Authentication method   | How to register                                                                                                               | How to authenticate for a password reset                                                                                              |
| ----------------------- | ----------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| Mobile app notification | Install the Microsoft Authenticator app on your mobile device, then register it on the multifactor authentication setup page. | Azure sends a notification to the app, which you can either verify or deny.                                                           |
| Mobile app code         | This method also uses the Authenticator app, and you install and register it in the same way.                                 | Enter the code from the app.                                                                                                          |
| Email                   | Provide an email address that's external to Azure and Microsoft 365.                                                          | Azure sends a code to the address, which you enter in the reset wizard.                                                               |
| Mobile phone            | Provide a mobile phone number.                                                                                                | Azure sends a code to the phone in an SMS message, which you enter in the reset wizard. You can also choose to get an automated call. |
| Office phone            | Provide a nonmobile phone number.                                                                                             | You receive an automated call to this number and press #.                                                                             |
| Security questions      | Select questions such as "In what city was your mother born?" and save their responses.                                       | Answer the questions.                                                                                                                 |

#### Require the minimum number of authentication methods

**You can specify the minimum number of methods that the user must set up: one or two.** For example, you might enable the mobile app code, email, office phone, and security questions methods and specify a minimum of two methods. Users can then choose the two methods they prefer, like mobile app code and email.

#### Accounts associated with administrator roles

* A strong, two-method authentication policy is always applied to accounts with an administrator role, regardless of your configuration for other users.
* The security-question method isn't available to accounts associated with an administrator role.

#### License requirements

* In a hybrid situation, where you have Active Directory on-premises and Microsoft Entra ID in the cloud, any password change in the cloud must be written back to the on-premises directory. This writeback support is available in Microsoft Entra ID P1 or P2. It's also available with Microsoft 365 Apps for business.

### What is self-service password reset in Microsoft Entra ID?

### Exercise - Set up self-service password reset

### Exercise - Customize directory branding
