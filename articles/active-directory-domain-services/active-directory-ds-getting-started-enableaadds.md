---
title: "Azure Active Directory Domain Services : activation | Microsoft Docs"
description: "Activer Azure Active Directory Domain Services à l’aide de hello portail Azure classic"
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
ms.openlocfilehash: 6263eb1849808a7c85e572e1046bc9039362dd9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-classic-portal"></a><span data-ttu-id="78392-103">Activer Azure Active Directory Domain Services à l’aide de hello portail Azure classic</span><span class="sxs-lookup"><span data-stu-id="78392-103">Enable Azure Active Directory Domain Services using hello Azure classic portal</span></span>

## <a name="task-3-enable-azure-active-directory-domain-services"></a><span data-ttu-id="78392-104">Tâche 3 : Activer Azure Active Directory Domain Services</span><span class="sxs-lookup"><span data-stu-id="78392-104">Task 3: enable Azure Active Directory Domain Services</span></span>
<span data-ttu-id="78392-105">Dans cette tâche, vous activez les Services de domaine d’Active Directory Azure (Azure AD DS) pour votre annuaire en procédant comme hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="78392-105">In this task, you enable Azure Active Directory Domain Services (Azure AD DS) for your directory by doing hello following steps:</span></span>

1. <span data-ttu-id="78392-106">Accédez toohello [portail Azure classic](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="78392-106">Go toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="78392-107">Dans le volet gauche de hello, sélectionnez hello **Active Directory** bouton.</span><span class="sxs-lookup"><span data-stu-id="78392-107">In hello left pane, select hello **Active Directory** button.</span></span>
3. <span data-ttu-id="78392-108">Sélectionnez le locataire d’Azure Active Directory (Azure AD) hello (répertoire) pour lequel vous souhaitez tooenable Azure AD DS.</span><span class="sxs-lookup"><span data-stu-id="78392-108">Select hello Azure Active Directory (Azure AD) tenant (directory) for which you want tooenable Azure AD DS.</span></span>

    ![Sélectionner un annuaire Azure AD](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. <span data-ttu-id="78392-110">Sur hello **active de la version préliminaire** , cliquez sur hello **configurer** onglet.</span><span class="sxs-lookup"><span data-stu-id="78392-110">On hello **preview directory** page, click hello **Configure** tab.</span></span>

    ![Configurer l’onglet de l’annuaire](./media/active-directory-domain-services-getting-started/configure-tab.png)
5. <span data-ttu-id="78392-112">Sous **services de domaine**, modifiez hello **activer les services de domaine pour ce répertoire** option trop**Oui**.</span><span class="sxs-lookup"><span data-stu-id="78392-112">Under **domain services**, change hello **Enable domain services for this directory** option too**Yes**.</span></span>  
    <span data-ttu-id="78392-113">Les options de configuration Azure des Services de domaine Active Directory supplémentaires s’affichent sur la page de hello.</span><span class="sxs-lookup"><span data-stu-id="78392-113">Additional Azure Active Directory Domain Services configuration options appear on hello page.</span></span>

    ![Activer les services de domaine](./media/active-directory-domain-services-getting-started/enable-domain-services.png)

   > [!NOTE]
   > <span data-ttu-id="78392-115">Lorsque vous activez Azure Active Directory Domain Services pour votre client, Azure AD génère et stocke hello Kerberos et NTLM d’informations d’identification hachages qui sont requis pour l’authentification des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="78392-115">When you enable Azure Active Directory Domain Services for your tenant, Azure AD generates and stores hello Kerberos and NTLM credential hashes that are required for authenticating users.</span></span>
   >
   >
6. <span data-ttu-id="78392-116">Spécifiez hello **le nom de domaine DNS des services de domaine**.</span><span class="sxs-lookup"><span data-stu-id="78392-116">Specify hello **DNS domain name of domain services**.</span></span>

   * <span data-ttu-id="78392-117">nom de domaine par défaut Hello du répertoire de hello (avec un **. onmicrosoft.com** suffixe) est sélectionnée par défaut.</span><span class="sxs-lookup"><span data-stu-id="78392-117">hello default domain name of hello directory (with a **.onmicrosoft.com** suffix) is selected by default.</span></span>

   * <span data-ttu-id="78392-118">Hello liste contient tous les domaines qui ont été configurés pour votre annuaire Azure AD, y compris les deux vérifiés et non vérifiées, les domaines que vous configurez sur hello **domaines** onglet.</span><span class="sxs-lookup"><span data-stu-id="78392-118">hello list contains all domains that have been configured for your Azure AD directory, including both verified and unverified domains that you configure on hello **Domains** tab.</span></span>

   * <span data-ttu-id="78392-119">Vous pouvez également saisir un nom de domaine personnalisé.</span><span class="sxs-lookup"><span data-stu-id="78392-119">You can also enter a custom domain name.</span></span> <span data-ttu-id="78392-120">Dans cet exemple, le nom de domaine personnalisé hello est *contoso100.com*.</span><span class="sxs-lookup"><span data-stu-id="78392-120">In this example, hello custom domain name is *contoso100.com*.</span></span>

     > [!WARNING]
     > <span data-ttu-id="78392-121">préfixe Hello de votre nom de domaine spécifié (par exemple, *contoso100* Bonjour *contoso100.com* nom de domaine) doit contenir au maximum 15 caractères.</span><span class="sxs-lookup"><span data-stu-id="78392-121">hello prefix of your specified domain name (for example, *contoso100* in hello *contoso100.com* domain name) must contain 15 or fewer characters.</span></span> <span data-ttu-id="78392-122">Vous ne pouvez pas créer un domaine Azure AD DS dont le préfixe contient plus de 15 caractères.</span><span class="sxs-lookup"><span data-stu-id="78392-122">You cannot create an Azure Active Directory Domain Services domain with a prefix containing more than 15 characters.</span></span>
     >
     >
7. <span data-ttu-id="78392-123">Vérifiez que nom de domaine DNS hello choisie pour hello géré domaine n’existe pas déjà dans le réseau virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="78392-123">Ensure that hello DNS domain name you have chosen for hello managed domain does not already exist in hello virtual network.</span></span> <span data-ttu-id="78392-124">Plus précisément, vérifiez toosee si :</span><span class="sxs-lookup"><span data-stu-id="78392-124">Specifically, check toosee whether:</span></span>

   * <span data-ttu-id="78392-125">Vous disposez déjà d’un domaine avec hello même nom de domaine DNS sur le réseau virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="78392-125">You already have a domain with hello same DNS domain name on hello virtual network.</span></span>

   * <span data-ttu-id="78392-126">Hello réseau virtuel que vous avez sélectionné possède une connexion VPN à votre réseau local, et que vous avez un domaine avec hello même nom de domaine DNS de votre réseau local.</span><span class="sxs-lookup"><span data-stu-id="78392-126">hello virtual network you've selected has a VPN connection with your on-premises network, and you have a domain with hello same DNS domain name on your on-premises network.</span></span>

   * <span data-ttu-id="78392-127">Vous avez un service cloud existant portant le même nom sur le réseau virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="78392-127">You have an existing cloud service with that name on hello virtual network.</span></span>
8. <span data-ttu-id="78392-128">Sélectionnez un réseau virtuel sur lequel vous souhaitez toobe Azure Active Directory Domain Services disponible.</span><span class="sxs-lookup"><span data-stu-id="78392-128">Select a virtual network on which you want Azure Active Directory Domain Services toobe available.</span></span> <span data-ttu-id="78392-129">Sélectionnez le réseau virtuel de hello et sous-réseau dédié, vous avez créé dans hello **toothis des réseaux virtuels des services de domaine de se connecter** liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="78392-129">Select hello virtual network and dedicated subnet you created in hello **Connect domain services toothis virtual network** drop-down list.</span></span> <span data-ttu-id="78392-130">Également envisager les suivant hello :</span><span class="sxs-lookup"><span data-stu-id="78392-130">Also consider hello following:</span></span>

   * <span data-ttu-id="78392-131">Assurez-vous que ce réseau virtuel hello que vous avez spécifié appartient tooan région Azure qui est pris en charge par les Services de domaine Active Directory de Azure.</span><span class="sxs-lookup"><span data-stu-id="78392-131">Ensure that hello virtual network that you have specified belongs tooan Azure region that's supported by Azure Active Directory Domain Services.</span></span> <span data-ttu-id="78392-132">tooascertain hello régions Azure où Azure des Services de domaine Active Directory est disponible, consultez [des services Azure par région](https://azure.microsoft.com/regions/#services/).</span><span class="sxs-lookup"><span data-stu-id="78392-132">tooascertain hello Azure regions where Azure Active Directory Domain Services is available, see [Azure services by region](https://azure.microsoft.com/regions/#services/).</span></span>

   * <span data-ttu-id="78392-133">Les réseaux virtuels qui appartiennent région tooa où Azure des Services de domaine Active Directory n’est pas prise en charge ne s’affichent pas dans la liste déroulante de hello.</span><span class="sxs-lookup"><span data-stu-id="78392-133">Virtual networks that belong tooa region where Azure Active Directory Domain Services is not supported do not show up in hello drop-down list.</span></span>

   * <span data-ttu-id="78392-134">Utilisez un sous-réseau dédié au sein du réseau virtuel de hello pour Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="78392-134">Use a dedicated subnet within hello virtual network for Azure Active Directory Domain Services.</span></span> <span data-ttu-id="78392-135">Faire *pas* sélectionnez hello sous-réseau de passerelle.</span><span class="sxs-lookup"><span data-stu-id="78392-135">Do *not* select hello gateway subnet.</span></span> <span data-ttu-id="78392-136">Consultez [Mise en réseau - Éléments à prendre en compte](active-directory-ds-networking.md).</span><span class="sxs-lookup"><span data-stu-id="78392-136">See [networking considerations](active-directory-ds-networking.md).</span></span>

   * <span data-ttu-id="78392-137">De même, les réseaux virtuels qui ont été créés à l’aide du Gestionnaire de ressources Azure n’apparaissent pas dans la liste déroulante de hello.</span><span class="sxs-lookup"><span data-stu-id="78392-137">Similarly, virtual networks that were created by using Azure Resource Manager do not appear in hello drop-down list.</span></span> <span data-ttu-id="78392-138">Les réseaux virtuels basés sur Resource Manager ne sont pas pris en charge par Azure AD DS pour le moment.</span><span class="sxs-lookup"><span data-stu-id="78392-138">Resource Manager-based virtual networks are not currently supported by Azure Active Directory Domain Services.</span></span>
9. <span data-ttu-id="78392-139">tooenable Services de domaine Active Directory Azure, dans le volet de tâches hello bas hello de page de hello, cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="78392-139">tooenable Azure Active Directory Domain Services, in hello task pane at hello bottom of hello page, click **Save**.</span></span>
    * <span data-ttu-id="78392-140">Alors que les Services de domaine Active Directory de Azure est activé pour votre annuaire, page de hello affiche l’état *en attente*.</span><span class="sxs-lookup"><span data-stu-id="78392-140">While Azure Active Directory Domain Services is being enabled for your directory, hello page displays a status of *Pending*.</span></span>

        ![Fenêtre Activer les services de domaine](./media/active-directory-domain-services-getting-started/enable-domain-services-pendingstate.png)

        > [!NOTE]
        > <span data-ttu-id="78392-142">Azure AD DS offre une haute disponibilité pour votre domaine managé.</span><span class="sxs-lookup"><span data-stu-id="78392-142">Azure Active Directory Domain Services provides high availability for your managed domain.</span></span> <span data-ttu-id="78392-143">Après avoir activé Azure des Services de domaine Active Directory, les adresses IP hello au domaine dans lequel les services sont disponibles sur le réseau virtuel de hello sont affichent l’un à la fois.</span><span class="sxs-lookup"><span data-stu-id="78392-143">After you enable Azure Active Directory Domain Services, hello IP addresses at which domain services are available on hello virtual network are displayed one at a time.</span></span> <span data-ttu-id="78392-144">adresse IP de la deuxième Hello s’affiche tout d’abord, peu de temps après hello comme bientôt service de hello permet une haute disponibilité pour votre domaine.</span><span class="sxs-lookup"><span data-stu-id="78392-144">hello second IP address is displayed shortly after hello first, as soon hello service enables high availability for your domain.</span></span> <span data-ttu-id="78392-145">Lorsque la haute disponibilité est configurée et actif pour votre domaine, vous devez voir deux adresses IP Bonjour **services de domaine** section Hello **configurer** onglet.</span><span class="sxs-lookup"><span data-stu-id="78392-145">When high availability is configured and active for your domain, you should see two IP addresses in hello **domain services** section of hello **Configure** tab.</span></span>
        >
        >
    * <span data-ttu-id="78392-146">Après environ 20 minutes too30, première adresse IP hello, au domaine dans lequel les services sont disponibles sur votre réseau virtuel Bonjour **adresse IP** champ hello **configurer** page.</span><span class="sxs-lookup"><span data-stu-id="78392-146">After about 20 too30 minutes, hello first IP address at which domain services are available on your virtual network in hello **IP address** field on hello **Configure** page.</span></span>

        ![Fenêtre Azure AD DS affichant la première adresse IP configurée](./media/active-directory-domain-services-getting-started/domain-services-enabled-firstdc-available.png)
    * <span data-ttu-id="78392-148">Lors de la haute disponibilité est opérationnelle pour votre domaine, les deux adresses IP sont affichées sur la page de hello.</span><span class="sxs-lookup"><span data-stu-id="78392-148">When high availability is operational for your domain, two IP addresses are displayed on hello page.</span></span> <span data-ttu-id="78392-149">Votre domaine géré est disponible sur votre réseau virtuel sélectionné à ces deux adresses IP.</span><span class="sxs-lookup"><span data-stu-id="78392-149">Your managed domain is available on your selected virtual network at these two IP addresses.</span></span>

10. <span data-ttu-id="78392-150">Notez les deux adresses IP de hello afin que vous pouvez mettre à jour les paramètres DNS hello pour votre réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="78392-150">Note hello two IP addresses so that you can update hello DNS settings for your virtual network.</span></span> <span data-ttu-id="78392-151">Ainsi, les ordinateurs virtuels sur le domaine de toohello tooconnect hello réseau virtuel pour les opérations telles que la jonction de domaine.</span><span class="sxs-lookup"><span data-stu-id="78392-151">Doing so enables virtual machines on hello virtual network tooconnect toohello domain for operations such as domain join.</span></span>

    ![Fenêtre Azure AD DS affichant les deux adresses IP configurées](./media/active-directory-domain-services-getting-started/domain-services-enabled-bothdcs-available.png)

> [!NOTE]
> <span data-ttu-id="78392-153">Selon la taille de hello de votre client Azure AD (par exemple, le nombre d’hello des utilisateurs ou groupes), domaine de synchronisation tooyour géré prend un certain temps.</span><span class="sxs-lookup"><span data-stu-id="78392-153">Depending on hello size of your Azure AD tenant (for example, hello number of users or groups), synchronization tooyour managed domain takes a while.</span></span> <span data-ttu-id="78392-154">Ce processus de synchronisation se produit en arrière-plan de hello.</span><span class="sxs-lookup"><span data-stu-id="78392-154">This synchronization process happens in hello background.</span></span> <span data-ttu-id="78392-155">Pour les clients avec des dizaines de milliers d’objets volumineux, il peut prendre une ou deux jours pour tous les utilisateurs, les appartenances aux groupes et les toobe des informations d’identification synchronisé.</span><span class="sxs-lookup"><span data-stu-id="78392-155">For large tenants with tens of thousands of objects, it might take a day or two for all users, group memberships, and credentials toobe synchronized.</span></span>
>
>

## <a name="next-step"></a><span data-ttu-id="78392-156">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="78392-156">Next step</span></span>
[<span data-ttu-id="78392-157">Tâche 4 : mettre à jour les paramètres DNS hello hello réseau virtuel Azure</span><span class="sxs-lookup"><span data-stu-id="78392-157">Task 4: update hello DNS settings for hello Azure virtual network</span></span>](active-directory-ds-getting-started-update-dns.md)
