---
title: "Microsoft Entra seamless single sign-on for your Microsoft 365 test environment"
f1.keywords:
- NOCSH
ms.author: kvice
author: kelleyvice-msft
manager: scotv
ms.date: 11/21/2019
audience: ITPro
ms.topic: article
ms.service: microsoft-365-enterprise
ms.localizationpriority: medium
ms.collection: 
- scotvorg
- M365-identity-device-management
- Strat_O365_Enterprise
ms.custom: 
- TLGS
- Ent_TLGs
ms.assetid: 
description: "Summary: Configure and test Microsoft Entra seamless single sign-on for your Microsoft 365 test environment."
---

# Microsoft Entra seamless single sign-on for your Microsoft 365 test environment

*This Test Lab Guide can be used for both Microsoft 365 for enterprise and Office 365 Enterprise test environments.*

Microsoft Entra seamless single sign-on (Seamless SSO) automatically signs in users when they are on their PCs or devices that are connected to their organization network. Microsoft Entra seamless SSO provides users with easy access to cloud-based applications without needing any additional on-premises components.

This article describes how to configure your Microsoft 365 test environment for Microsoft Entra seamless SSO.

Setting up Microsoft Entra seamless SSO involves two phases:
- [Phase 1: Configure password hash synchronization for your Microsoft 365 test environment](#phase-1-configure-password-hash-synchronization-for-your-microsoft-365-test-environment)
- [Phase 2: Configure Microsoft Entra Connect on APP1 for Microsoft Entra seamless SSO](#phase-2-configure-azure-ad-connect-on-app1-for-azure-ad-seamless-sso)
   
![Test Lab Guides for the Microsoft cloud.](../media/m365-enterprise-test-lab-guides/cloud-tlg-icon.png) 
    
> [!TIP]
> For a visual map to all the articles in the Microsoft 365 for enterprise Test Lab Guide stack, go to [Microsoft 365 for enterprise Test Lab Guide Stack](https://download.microsoft.com/download/5/e/4/5e43a139-09c5-4700-b846-e468444bc557/Microsoft365EnterpriseTLGStack.pdf).
  
## Phase 1: Configure password hash synchronization for your Microsoft 365 test environment

Follow the instructions in [password hash synchronization for Microsoft 365](password-hash-sync-m365-ent-test-environment.md). 

Your resulting configuration looks like this:
  
![The simulated enterprise with password hash synchronization test environment.](../media/pass-through-auth-m365-ent-test-environment/Phase1.png)
  
This configuration consists of:
  
- A Microsoft 365 E5 trial or paid subscription.
- A simplified organization intranet connected to the internet, consisting of the DC1, APP1, and CLIENT1 virtual machines on a subnet of an Azure virtual network.
- Microsoft Entra Connect runs on APP1 to periodically synchronize the TESTLAB Active Directory Domain Services (AD DS) domain to the Microsoft Entra tenant of your Microsoft 365 subscription.

<a name='phase-2-configure-azure-ad-connect-on-app1-for-azure-ad-seamless-sso'></a>

## Phase 2: Configure Microsoft Entra Connect on APP1 for Microsoft Entra seamless SSO

In this phase, configure Microsoft Entra Connect on APP1 for Microsoft Entra seamless SSO, and then verify that it works.

<a name='configure-azure-ad-connect-on-app1'></a>

### Configure Microsoft Entra Connect on APP1

1. From the [Azure portal](https://portal.azure.com), sign in with your global administrator account, and then connect to APP1 with the TESTLAB\User1 account.

2. From the APP1 desktop, run Microsoft Entra Connect.

3. On the **Welcome page**, select **Configure**.

4. On the **Additional tasks** page, select **Change user sign-in**, and then select **Next**.

5. On the **Connect to Microsoft Entra ID** page, enter your global administrator account credentials, and then select **Next**.

6. On the **User sign-in** page, select **Enable single sign-on**, and then select **Next**.

7. On the **Enable single sign-on** page, select **Enter credentials**.

8. In the **Windows Security** dialog box, enter **user1** and the password of the user1 account, select **OK**, and then select **Next**.

9. On the **Ready to Configure** page, select **Configure**.

10. On the **Configuration complete** page, select **Exit**.

11. From the Azure portal, in the left pane, select **Microsoft Entra ID** > **Microsoft Entra Connect**. Verify that the **Seamless single sign-on** feature appears as **Enabled**.

Next, test the ability to sign in to your subscription with the <strong>user1@testlab.</strong>\<*your public domain*> user name of the User1 account.

1. From Internet Explorer on APP1, select the settings icon, and then select **Internet Options**.
 
2. In **Internet Options**, select the **Security** tab.

3. Select **Local intranet**, and then select **Sites**.

4. In **Local intranet**, select **Advanced**.

5. In **Add this website to the zone**, enter **https<span>://</span>autologon.microsoftazuread-sso.com**, select **Add** > **Close** > **OK** > **OK**.

6. Sign out, and then sign in again, this time specifying a different account.

7. When prompted to sign in, specify <strong>user1@testlab.</strong>\<*your public domain*> name, and then select **Next**. You should successfully sign in as User1 without being prompted for a password. This proves that Microsoft Entra seamless SSO is working.

Notice that although User1 has domain administrator permissions for the TESTLAB AD DS domain, it is not a global administrator for Microsoft Entra ID. Therefore, you will not see the **Admin** icon as an option.

Here is your resulting configuration:

![The simulated enterprise with pass-through authentication test environment.](../media/pass-through-auth-m365-ent-test-environment/Phase1.png)

This configuration consists of:

- A Microsoft 365 E5 trial or paid subscriptions with the DNS domain testlab.\<*your domain name*> registered.
- A simplified organization intranet connected to the internet, consisting of the DC1, APP1, and CLIENT1 virtual machines on a subnet of an Azure virtual network.
- Microsoft Entra Connect runs on APP1 to synchronize the list of accounts and groups from the Microsoft Entra tenant of your Microsoft 365 subscription to the TESTLAB AD DS domain.
- Microsoft Entra seamless SSO is enabled so that computers on the simulated intranet can sign in to Microsoft 365 cloud resources without specifying a user account password.

## Next step

Explore additional [identity](m365-enterprise-test-lab-guides.md#identity) features and capabilities in your test environment.

## See also

[Microsoft 365 for enterprise Test Lab Guides](m365-enterprise-test-lab-guides.md)

[Microsoft 365 for enterprise overview](microsoft-365-overview.md)

[Microsoft 365 for enterprise documentation](/microsoft-365-enterprise/)
