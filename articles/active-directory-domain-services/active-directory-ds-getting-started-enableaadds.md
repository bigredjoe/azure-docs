---
title: 'Azure AD Domain Services: Enable Azure AD Domain Services | Microsoft Docs'
description: Getting started with Azure Active Directory Domain Services
services: active-directory-ds
documentationcenter: ''
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand

ms.assetid: c659da59-f4b5-4edd-b702-1727a8ccb36f
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 10/19/2016
ms.author: maheshu

---
# Enable Azure AD Domain Services
## Task 3: Enable Azure AD Domain Services
In this task, you enable Azure AD Domain Services for your directory. Perform the following configuration steps to enable Azure AD Domain Services for your directory.

1. Navigate to the **Azure classic portal** ([https://manage.windowsazure.com](https://manage.windowsazure.com)).
2. Select the **Active Directory** node on the left pane.
3. Select the Azure AD tenant (directory) for which you would like to enable Azure AD Domain Services.
   
    ![Select Azure AD Directory](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. Click the **Configure** tab.
   
    ![Configure tab of directory](./media/active-directory-domain-services-getting-started/configure-tab.png)
5. Scroll down to a section titled **domain services**.
   
    ![Domain Services configuration section](./media/active-directory-domain-services-getting-started/domain-services-configuration.png)
6. Toggle the option titled **Enable domain services for this directory** to **YES**. You notice a few more configuration options for Azure AD Domain services appear on the page.
   
    ![Enable Domain Services](./media/active-directory-domain-services-getting-started/enable-domain-services.png)
   
   > [!NOTE]
   > When you enable Azure AD Domain Services for your tenant, Azure AD generates and stores the Kerberos and NTLM credential hashes that are required for authenticating users.
   > 
   > 
7. Specify the **DNS domain name of domain services**.
   
   * The default domain name of the directory (that is, ending with the **.onmicrosoft.com** domain suffix) is selected by default.
   * The list contains all domains that have been configured for your Azure AD directory – including verified as well as unverified domains that you configure in the ‘Domains’ tab.
   * Additionally, you can also type a custom domain name. In this example, we have typed in a custom domain name 'contoso100.com'.
     
     > [!WARNING]
     > Ensure that the domain prefix of the domain name you specify (for example, 'contoso100' in the 'contoso100.com' domain name) is fewer than 15 characters. You cannot create an Azure AD Domain Services domain with a domain prefix longer than 15 characters.
     > 
     > 
8. Ensure that the DNS domain name you have chosen for the managed domain does not already exist in the virtual network. Specifically, check if:
   
   * you already have a domain with the same DNS domain name on the virtual network.
   * the virtual network you've selected has a VPN connection with your on-premises network and you have a domain with the same DNS domain name on your on-premises network.
   * you have an existing cloud service with that name on the virtual network.
9. The next step is to select a virtual network in which you'd like Azure AD Domain Services to be available. Select the virtual network and dedicated subnet you created in the drop-down titled **Connect domain services to this virtual network**.
   
   * Ensure that the virtual network you have specified belongs to an Azure region supported by Azure AD Domain Services. Refer to the [Azure services by region](https://azure.microsoft.com/regions/#services/) page to know the Azure regions in which Azure AD Domain Services is available.
   * Virtual networks belonging to a region where Azure AD Domain Services is not supported do not show up in the drop-down list.
   * Use a dedicated subnet within the virtual network for Azure AD Domain Services. Ensure you do not select the gateway subnet. See [networking considerations](active-directory-ds-networking.md). 
   * Similarly, virtual networks that were created using Azure Resource Manager do not appear in the drop-down list. Resource Manager-based virtual networks are not currently supported by Azure AD Domain Services.
10. To enable Azure AD Domain Services, click **Save** from the task pane at the bottom of the page.
11. The page displays a ‘Pending …’ state, while Azure AD Domain Services is being enabled for your directory.
    
    ![Enable Domain Services - pending state](./media/active-directory-domain-services-getting-started/enable-domain-services-pendingstate.png)
    
    > [!NOTE]
    > Azure AD Domain Services provides high availability for your managed domain. After you enable Azure AD Domain Services, notice the IP addresses at which Domain Services are available on the virtual network show up one by one. The second IP address is displayed shortly, as soon the service enables high availability for your domain. When high availability is configured and active for your domain, you should see two IP addresses in the **domain services** section of the **Configure** tab.
    > 
    > 
12. After about 20-30 minutes, you see the first IP address at which Domain Services is available on your virtual network in the **IP address** field on the **Configure** page.
    
    ![Domain Services enabled - first IP provisioned](./media/active-directory-domain-services-getting-started/domain-services-enabled-firstdc-available.png)
13. When high availability is operational for your domain, you see two IP addresses displayed on the page. Your managed domain is available on your selected virtual network at these two IP addresses. Note down the IP addresses so you can update the DNS settings for your virtual network. This step enables virtual machines on the virtual network to connect to the domain for operations such as domain join.
    
    ![Domain Services enabled - both IPs provisioned](./media/active-directory-domain-services-getting-started/domain-services-enabled-bothdcs-available.png)

> [!NOTE]
> Depending on the size of your Azure AD tenant (number of users, groups etc.), synchronization to your managed domain takes a while. This synchronization process happens in the background. For large tenants with tens of thousands of objects, it may take a day or two for all users, group memberships, and credentials to be synchronized.
> 
> 

<br>

## Task 4 - Update DNS settings for the Azure virtual network
The next configuration task is to [update the DNS settings for the Azure virtual network](active-directory-ds-getting-started-dns.md).

