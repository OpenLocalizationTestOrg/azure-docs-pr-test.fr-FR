---
title: "Azure Active Directory Domain Services : activation | Microsoft Docs"
description: "Activer Azure Active Directory Domain Services à l’aide du portail Azure Classic"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: c659da59-f4b5-4edd-b702-1727a8ccb36f
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/28/2017
ms.author: maheshu
ms.openlocfilehash: ed72325ca9db99405c6173eb882a92f80cd77f47
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="enable-azure-active-directory-domain-services-using-the-azure-classic-portal"></a><span data-ttu-id="b68f9-103">Activer Azure Active Directory Domain Services à l’aide du portail Azure Classic</span><span class="sxs-lookup"><span data-stu-id="b68f9-103">Enable Azure Active Directory Domain Services using the Azure classic portal</span></span>

## <a name="task-3-enable-azure-active-directory-domain-services"></a><span data-ttu-id="b68f9-104">Tâche 3 : Activer Azure Active Directory Domain Services</span><span class="sxs-lookup"><span data-stu-id="b68f9-104">Task 3: enable Azure Active Directory Domain Services</span></span>
<span data-ttu-id="b68f9-105">Pour activer Azure Active Directory Domain Services (Azure AD DS) afin de gérer votre répertoire, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="b68f9-105">In this task, you enable Azure Active Directory Domain Services (Azure AD DS) for your directory by doing the following steps:</span></span>

1. <span data-ttu-id="b68f9-106">Connectez-vous au [Portail Azure Classic](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="b68f9-106">Go to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="b68f9-107">Dans le volet de gauche, cliquez sur le bouton **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b68f9-107">In the left pane, select the **Active Directory** button.</span></span>
3. <span data-ttu-id="b68f9-108">Sélectionnez le locataire Azure AD (annuaire) pour lequel vous souhaitez activer Azure AD DS.</span><span class="sxs-lookup"><span data-stu-id="b68f9-108">Select the Azure Active Directory (Azure AD) tenant (directory) for which you want to enable Azure AD DS.</span></span>

    ![Sélectionner un annuaire Azure AD](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. <span data-ttu-id="b68f9-110">Sur la page de la **version préliminaire de l’annuaire**, cliquez sur l’onglet **Configurer**.</span><span class="sxs-lookup"><span data-stu-id="b68f9-110">On the **preview directory** page, click the **Configure** tab.</span></span>

    ![Configurer l’onglet de l’annuaire](./media/active-directory-domain-services-getting-started/configure-tab.png)
5. <span data-ttu-id="b68f9-112">Sous **Services de domaine**, affectez à l’option **Activer les services de domaine pour cet annuaire** la valeur **Oui**.</span><span class="sxs-lookup"><span data-stu-id="b68f9-112">Under **domain services**, change the **Enable domain services for this directory** option to **Yes**.</span></span>  
    <span data-ttu-id="b68f9-113">D’autres options de configuration d’Azure AD DS s’affichent sur la page.</span><span class="sxs-lookup"><span data-stu-id="b68f9-113">Additional Azure Active Directory Domain Services configuration options appear on the page.</span></span>

    ![Activer les services de domaine](./media/active-directory-domain-services-getting-started/enable-domain-services.png)

   > [!NOTE]
   > <span data-ttu-id="b68f9-115">Lorsque vous activez Azure AD DS pour votre locataire, Azure AD génère et stocke les hachages d’informations d’identification Kerberos et NTLM nécessaires pour l’authentification des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="b68f9-115">When you enable Azure Active Directory Domain Services for your tenant, Azure AD generates and stores the Kerberos and NTLM credential hashes that are required for authenticating users.</span></span>
   >
   >
6. <span data-ttu-id="b68f9-116">Spécifiez le **Nom de domaine DNS des services de domaine**.</span><span class="sxs-lookup"><span data-stu-id="b68f9-116">Specify the **DNS domain name of domain services**.</span></span>

   * <span data-ttu-id="b68f9-117">Le nom de domaine par défaut de l’annuaire (qui présente le suffixe **.onmicrosoft.com**) est sélectionné par défaut.</span><span class="sxs-lookup"><span data-stu-id="b68f9-117">The default domain name of the directory (with a **.onmicrosoft.com** suffix) is selected by default.</span></span>

   * <span data-ttu-id="b68f9-118">La liste contient tous les domaines qui ont été configurés pour votre annuaire Azure AD, y compris les domaines vérifiés et non vérifiés que vous configurez sous l’onglet **Domaines**.</span><span class="sxs-lookup"><span data-stu-id="b68f9-118">The list contains all domains that have been configured for your Azure AD directory, including both verified and unverified domains that you configure on the **Domains** tab.</span></span>

   * <span data-ttu-id="b68f9-119">Vous pouvez également saisir un nom de domaine personnalisé.</span><span class="sxs-lookup"><span data-stu-id="b68f9-119">You can also enter a custom domain name.</span></span> <span data-ttu-id="b68f9-120">Dans cet exemple, le nom de domaine personnalisé est *contoso100.com*.</span><span class="sxs-lookup"><span data-stu-id="b68f9-120">In this example, the custom domain name is *contoso100.com*.</span></span>

     > [!WARNING]
     > <span data-ttu-id="b68f9-121">Le préfixe du nom de domaine spécifié (par exemple, *contoso100* dans le nom de domaine *contoso100.com*) doit contenir au maximum 15 caractères.</span><span class="sxs-lookup"><span data-stu-id="b68f9-121">The prefix of your specified domain name (for example, *contoso100* in the *contoso100.com* domain name) must contain 15 or fewer characters.</span></span> <span data-ttu-id="b68f9-122">Vous ne pouvez pas créer un domaine Azure AD DS dont le préfixe contient plus de 15 caractères.</span><span class="sxs-lookup"><span data-stu-id="b68f9-122">You cannot create an Azure Active Directory Domain Services domain with a prefix containing more than 15 characters.</span></span>
     >
     >
7. <span data-ttu-id="b68f9-123">Vérifiez que le nom de domaine DNS choisi pour le domaine géré n’existe pas au sein du réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="b68f9-123">Ensure that the DNS domain name you have chosen for the managed domain does not already exist in the virtual network.</span></span> <span data-ttu-id="b68f9-124">Plus précisément, vérifiez ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="b68f9-124">Specifically, check to see whether:</span></span>

   * <span data-ttu-id="b68f9-125">Vous disposez d’un domaine présentant le nom de domaine DNS au sein du réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="b68f9-125">You already have a domain with the same DNS domain name on the virtual network.</span></span>

   * <span data-ttu-id="b68f9-126">Le réseau virtuel que vous avez sélectionné comprend une connexion VPN avec votre réseau local et vous disposez d’un domaine présentant le même nom de domaine DNS sur votre réseau local.</span><span class="sxs-lookup"><span data-stu-id="b68f9-126">The virtual network you've selected has a VPN connection with your on-premises network, and you have a domain with the same DNS domain name on your on-premises network.</span></span>

   * <span data-ttu-id="b68f9-127">Il existe un service cloud portant ce nom sur le réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="b68f9-127">You have an existing cloud service with that name on the virtual network.</span></span>
8. <span data-ttu-id="b68f9-128">Sélectionnez le réseau virtuel sur lequel vous souhaitez qu’Azure AD DS soit disponible.</span><span class="sxs-lookup"><span data-stu-id="b68f9-128">Select a virtual network on which you want Azure Active Directory Domain Services to be available.</span></span> <span data-ttu-id="b68f9-129">Dans la liste déroulante **Connecter les services de domaine à ce réseau virtuel**, sélectionnez le réseau virtuel et le sous-réseau dédié que vous avez créés.</span><span class="sxs-lookup"><span data-stu-id="b68f9-129">Select the virtual network and dedicated subnet you created in the **Connect domain services to this virtual network** drop-down list.</span></span> <span data-ttu-id="b68f9-130">Tenez également compte des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="b68f9-130">Also consider the following:</span></span>

   * <span data-ttu-id="b68f9-131">Assurez-vous que le réseau virtuel que vous avez spécifié appartient à une région Azure prise en charge par Azure AD DS.</span><span class="sxs-lookup"><span data-stu-id="b68f9-131">Ensure that the virtual network that you have specified belongs to an Azure region that's supported by Azure Active Directory Domain Services.</span></span> <span data-ttu-id="b68f9-132">Pour connaître les régions Azure dans lesquelles Azure AD DS est disponible, consultez la page [Services Azure par région](https://azure.microsoft.com/regions/#services/).</span><span class="sxs-lookup"><span data-stu-id="b68f9-132">To ascertain the Azure regions where Azure Active Directory Domain Services is available, see [Azure services by region](https://azure.microsoft.com/regions/#services/).</span></span>

   * <span data-ttu-id="b68f9-133">Les réseaux virtuels appartenant à une région dans laquelle Azure AD DS n’est pas pris en charge n’apparaissent pas dans la liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="b68f9-133">Virtual networks that belong to a region where Azure Active Directory Domain Services is not supported do not show up in the drop-down list.</span></span>

   * <span data-ttu-id="b68f9-134">Utilisez un sous-réseau dédié au sein du réseau virtuel pour Azure AD DS.</span><span class="sxs-lookup"><span data-stu-id="b68f9-134">Use a dedicated subnet within the virtual network for Azure Active Directory Domain Services.</span></span> <span data-ttu-id="b68f9-135">Veillez à ne *pas* sélectionner le sous-réseau de passerelle.</span><span class="sxs-lookup"><span data-stu-id="b68f9-135">Do *not* select the gateway subnet.</span></span> <span data-ttu-id="b68f9-136">Consultez [Mise en réseau - Éléments à prendre en compte](active-directory-ds-networking.md).</span><span class="sxs-lookup"><span data-stu-id="b68f9-136">See [networking considerations](active-directory-ds-networking.md).</span></span>

   * <span data-ttu-id="b68f9-137">De même, les réseaux virtuels créés à l’aide du logiciel Azure Resource Manager ne sont pas affichés dans la liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="b68f9-137">Similarly, virtual networks that were created by using Azure Resource Manager do not appear in the drop-down list.</span></span> <span data-ttu-id="b68f9-138">Les réseaux virtuels basés sur Resource Manager ne sont pas pris en charge par Azure AD DS pour le moment.</span><span class="sxs-lookup"><span data-stu-id="b68f9-138">Resource Manager-based virtual networks are not currently supported by Azure Active Directory Domain Services.</span></span>
9. <span data-ttu-id="b68f9-139">Pour activer Azure AD DS, cliquez sur **Enregistrer** dans le volet des tâches, en bas de la page.</span><span class="sxs-lookup"><span data-stu-id="b68f9-139">To enable Azure Active Directory Domain Services, in the task pane at the bottom of the page, click **Save**.</span></span>
    * <span data-ttu-id="b68f9-140">La page affiche l’état *En attente* pendant l’activation de cette fonctionnalité pour votre annuaire.</span><span class="sxs-lookup"><span data-stu-id="b68f9-140">While Azure Active Directory Domain Services is being enabled for your directory, the page displays a status of *Pending*.</span></span>

        ![Fenêtre Activer les services de domaine](./media/active-directory-domain-services-getting-started/enable-domain-services-pendingstate.png)

        > [!NOTE]
        > <span data-ttu-id="b68f9-142">Azure AD DS offre une haute disponibilité pour votre domaine managé.</span><span class="sxs-lookup"><span data-stu-id="b68f9-142">Azure Active Directory Domain Services provides high availability for your managed domain.</span></span> <span data-ttu-id="b68f9-143">Une fois Azure Active Directory Domain Services activé, les adresses IP auxquelles les services de domaine sont disponibles sur le réseau virtuel s’affichent l’une après l’autre.</span><span class="sxs-lookup"><span data-stu-id="b68f9-143">After you enable Azure Active Directory Domain Services, the IP addresses at which domain services are available on the virtual network are displayed one at a time.</span></span> <span data-ttu-id="b68f9-144">La deuxième adresse IP s’affiche rapidement après la première, dès que le service active la haute disponibilité pour votre domaine.</span><span class="sxs-lookup"><span data-stu-id="b68f9-144">The second IP address is displayed shortly after the first, as soon the service enables high availability for your domain.</span></span> <span data-ttu-id="b68f9-145">Une fois que la haute disponibilité est configurée et active pour votre domaine, deux adresses IP apparaissent normalement dans la section **services de domaine** de l’onglet **Configurer**.</span><span class="sxs-lookup"><span data-stu-id="b68f9-145">When high availability is configured and active for your domain, you should see two IP addresses in the **domain services** section of the **Configure** tab.</span></span>
        >
        >
    * <span data-ttu-id="b68f9-146">Après 20 à 30 minutes, la première adresse IP à laquelle les services de domaine sont disponibles sur votre réseau virtuel apparaît dans le champ **Adresse IP** de la page **Configurer**.</span><span class="sxs-lookup"><span data-stu-id="b68f9-146">After about 20 to 30 minutes, the first IP address at which domain services are available on your virtual network in the **IP address** field on the **Configure** page.</span></span>

        ![Fenêtre Azure AD DS affichant la première adresse IP configurée](./media/active-directory-domain-services-getting-started/domain-services-enabled-firstdc-available.png)
    * <span data-ttu-id="b68f9-148">Une fois que la haute disponibilité est opérationnelle pour votre domaine, deux adresses IP apparaissent sur la page.</span><span class="sxs-lookup"><span data-stu-id="b68f9-148">When high availability is operational for your domain, two IP addresses are displayed on the page.</span></span> <span data-ttu-id="b68f9-149">Votre domaine géré est disponible sur votre réseau virtuel sélectionné à ces deux adresses IP.</span><span class="sxs-lookup"><span data-stu-id="b68f9-149">Your managed domain is available on your selected virtual network at these two IP addresses.</span></span>

10. <span data-ttu-id="b68f9-150">Notez ces adresses IP afin de pouvoir mettre à jour les paramètres DNS pour votre réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="b68f9-150">Note the two IP addresses so that you can update the DNS settings for your virtual network.</span></span> <span data-ttu-id="b68f9-151">Cette étape permet aux machines virtuelles du réseau virtuel de se connecter au domaine en vue de procéder à diverses opérations, telles que la jonction de domaine.</span><span class="sxs-lookup"><span data-stu-id="b68f9-151">Doing so enables virtual machines on the virtual network to connect to the domain for operations such as domain join.</span></span>

    ![Fenêtre Azure AD DS affichant les deux adresses IP configurées](./media/active-directory-domain-services-getting-started/domain-services-enabled-bothdcs-available.png)

> [!NOTE]
> <span data-ttu-id="b68f9-153">En fonction de la taille de votre locataire Azure AD (par exemple, le nombre d’utilisateurs ou de groupes), la synchronisation avec votre domaine managé peut prendre du temps.</span><span class="sxs-lookup"><span data-stu-id="b68f9-153">Depending on the size of your Azure AD tenant (for example, the number of users or groups), synchronization to your managed domain takes a while.</span></span> <span data-ttu-id="b68f9-154">Ce processus de synchronisation se produit en arrière-plan.</span><span class="sxs-lookup"><span data-stu-id="b68f9-154">This synchronization process happens in the background.</span></span> <span data-ttu-id="b68f9-155">Pour les locataires volumineux comportant des dizaines de milliers d’objets, un ou deux jours peuvent s’écouler avant que la totalité des utilisateurs, des appartenances aux groupes et des informations d’identification soit synchronisée.</span><span class="sxs-lookup"><span data-stu-id="b68f9-155">For large tenants with tens of thousands of objects, it might take a day or two for all users, group memberships, and credentials to be synchronized.</span></span>
>
>

## <a name="next-step"></a><span data-ttu-id="b68f9-156">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="b68f9-156">Next step</span></span>
[<span data-ttu-id="b68f9-157">Tâche 4 : Mettre à jour les paramètres DNS pour le réseau virtuel Azure</span><span class="sxs-lookup"><span data-stu-id="b68f9-157">Task 4: update the DNS settings for the Azure virtual network</span></span>](active-directory-ds-getting-started-update-dns.md)
