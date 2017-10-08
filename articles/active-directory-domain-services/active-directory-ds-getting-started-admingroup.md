---
title: "Bien démarrer avec Azure Active Directory Domain Services | Microsoft Docs"
description: "Activer Azure Active Directory Domain Services à l’aide de hello portail Azure (aperçu)"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: ace1ed4a-bf7f-43c1-a64a-6b51a2202473
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/15/2017
ms.author: maheshu
ms.openlocfilehash: 8bde872a13bc9960d1e62c74017ff78a8953a0a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-portal-preview"></a><span data-ttu-id="ea975-103">Activer Azure Active Directory Domain Services à l’aide de hello portail Azure (aperçu)</span><span class="sxs-lookup"><span data-stu-id="ea975-103">Enable Azure Active Directory Domain Services using hello Azure portal (Preview)</span></span>


## <a name="task-3-configure-administrative-group"></a><span data-ttu-id="ea975-104">Tâche 3 : configurer le groupe d’administration</span><span class="sxs-lookup"><span data-stu-id="ea975-104">Task 3: configure administrative group</span></span>
<span data-ttu-id="ea975-105">Dans cette tâche de configuration, vous allez créer un groupe d’administration dans votre répertoire Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ea975-105">In this configuration task, you create an administrative group in your Azure AD directory.</span></span> <span data-ttu-id="ea975-106">Ce groupe d’administration spécial est appelé *AAD DC Administrators*.</span><span class="sxs-lookup"><span data-stu-id="ea975-106">This special administrative group is called *AAD DC Administrators*.</span></span> <span data-ttu-id="ea975-107">Membres de ce groupe ont des autorisations d’administration sur les ordinateurs qui appartiennent à un domaine géré de toohello de domaine.</span><span class="sxs-lookup"><span data-stu-id="ea975-107">Members of this group are granted administrative permissions on machines that are domain-joined toohello managed domain.</span></span> <span data-ttu-id="ea975-108">Sur les ordinateurs joints à un domaine, ce groupe est ajouté toohello groupe d’administrateurs.</span><span class="sxs-lookup"><span data-stu-id="ea975-108">On domain-joined machines, this group is added toohello administrators group.</span></span> <span data-ttu-id="ea975-109">En outre, les membres de ce groupe peuvent utiliser Bureau à distance tooconnect à distance toodomain-ordinateurs joints à un.</span><span class="sxs-lookup"><span data-stu-id="ea975-109">Additionally, members of this group can use Remote Desktop tooconnect remotely toodomain-joined machines.</span></span>

> [!NOTE]
> <span data-ttu-id="ea975-110">Il est inutile des autorisations administrateur de domaine ou administrateur d’entreprise sur un domaine géré hello que vous avez créé à l’aide d’Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="ea975-110">You do not have Domain Administrator or Enterprise Administrator permissions on hello managed domain that you created by using Azure Active Directory Domain Services.</span></span> <span data-ttu-id="ea975-111">Dans des domaines gérés, ces autorisations sont réservées par le service de hello et ne sont pas apportées toousers disponibles au sein de client de hello.</span><span class="sxs-lookup"><span data-stu-id="ea975-111">On managed domains, these permissions are reserved by hello service and are not made available toousers within hello tenant.</span></span> <span data-ttu-id="ea975-112">Toutefois, vous pouvez utiliser hello spéciaux groupe d’administration créés dans cette tooperform de tâche de configuration certaines opérations privilégiées.</span><span class="sxs-lookup"><span data-stu-id="ea975-112">However, you can use hello special administrative group created in this configuration task tooperform some privileged operations.</span></span> <span data-ttu-id="ea975-113">Ces opérations comprennent la jonction de domaine toohello des ordinateurs, appartenant toohello groupe d’administration sur les ordinateurs joints au domaine et stratégie de groupe.</span><span class="sxs-lookup"><span data-stu-id="ea975-113">These operations include joining computers toohello domain, belonging toohello administration group on domain-joined machines, and configuring Group Policy.</span></span>
>

<span data-ttu-id="ea975-114">Assistant de Hello crée automatiquement le groupe d’administration hello dans votre annuaire Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ea975-114">hello wizard automatically creates hello administrative group in your Azure AD directory.</span></span> <span data-ttu-id="ea975-115">Ce groupe est appelé « Administrateurs AAD DC ».</span><span class="sxs-lookup"><span data-stu-id="ea975-115">This group is called 'AAD DC Administrators'.</span></span> <span data-ttu-id="ea975-116">Si vous disposez d’un groupe portant ce nom dans votre annuaire Azure AD, Assistant de hello sélectionne ce groupe.</span><span class="sxs-lookup"><span data-stu-id="ea975-116">If you have an existing group with this name in your Azure AD directory, hello wizard selects this group.</span></span> <span data-ttu-id="ea975-117">Vous pouvez configurer l’appartenance au groupe à l’aide de hello **groupe administrateur** page de l’Assistant.</span><span class="sxs-lookup"><span data-stu-id="ea975-117">You can configure group membership using hello **Administrator group** wizard page.</span></span>

1. <span data-ttu-id="ea975-118">appartenance au groupe de tooconfigure, cliquez sur **administrateurs du contrôleur de domaine AAD**.</span><span class="sxs-lookup"><span data-stu-id="ea975-118">tooconfigure group membership, click **AAD DC Administrators**.</span></span>

    ![Configurer l’appartenance au groupe](./media/getting-started/domain-services-blade-admingroup.png)

2. <span data-ttu-id="ea975-120">Cliquez sur hello **ajouter des membres** bouton tooadd les utilisateurs de votre groupe d’administrateur Azure AD directory toohello.</span><span class="sxs-lookup"><span data-stu-id="ea975-120">Click hello **Add members** button tooadd users from your Azure AD directory toohello administrator group.</span></span>

3. <span data-ttu-id="ea975-121">Lorsque vous avez terminé, cliquez sur **OK** toomove sur toohello **Résumé** page d’Assistant de hello.</span><span class="sxs-lookup"><span data-stu-id="ea975-121">When you are done, click **OK** toomove on toohello **Summary** page of hello wizard.</span></span>

4. <span data-ttu-id="ea975-122">Sur hello **Résumé** page d’Assistant hello, vérifier les paramètres de configuration hello pour le domaine géré de hello.</span><span class="sxs-lookup"><span data-stu-id="ea975-122">On hello **Summary** page of hello wizard, review hello configuration settings for hello managed domain.</span></span> <span data-ttu-id="ea975-123">Vous pouvez revenir en arrière étape tooany des modifications de toomake Assistant hello, si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="ea975-123">You can go back tooany step of hello wizard toomake changes, if necessary.</span></span> <span data-ttu-id="ea975-124">Lorsque vous avez terminé, cliquez sur **OK** toocreate hello gérés nouveau domaine.</span><span class="sxs-lookup"><span data-stu-id="ea975-124">When you are done, click **OK** toocreate hello new managed domain.</span></span>

    ![Résumé](./media/getting-started/domain-services-blade-summary.png)

5. <span data-ttu-id="ea975-126">Vous voyez une notification qui affiche la progression de hello de votre déploiement de Services de domaine Active Directory de Azure.</span><span class="sxs-lookup"><span data-stu-id="ea975-126">You see a notification that shows hello progress of your Azure AD Domain Services deployment.</span></span> <span data-ttu-id="ea975-127">Cliquez sur la notification de hello toosee détaillées de progression pour le déploiement de hello.</span><span class="sxs-lookup"><span data-stu-id="ea975-127">Click hello notification toosee detailed progress for hello deployment.</span></span>

    ![Notification - Déploiement en cours](./media/getting-started/domain-services-blade-deployment-in-progress.png)


## <a name="provision-your-managed-domain"></a><span data-ttu-id="ea975-129">Approvisionner votre domaine managé</span><span class="sxs-lookup"><span data-stu-id="ea975-129">Provision your managed domain</span></span>
<span data-ttu-id="ea975-130">processus de Hello de configuration de votre domaine géré peut prendre tooan heure.</span><span class="sxs-lookup"><span data-stu-id="ea975-130">hello process of provisioning your managed domain can take up tooan hour.</span></span>

1. <span data-ttu-id="ea975-131">Pendant que votre déploiement est en cours d’exécution, vous pouvez rechercher des services de domaine Bonjour **recherche les ressources** zone de recherche.</span><span class="sxs-lookup"><span data-stu-id="ea975-131">While your deployment is in progress, you can search for 'domain services' in hello **Search resources** search box.</span></span> <span data-ttu-id="ea975-132">Sélectionnez **les Services de domaine Active Directory de Azure** à partir du résultat de recherche hello.</span><span class="sxs-lookup"><span data-stu-id="ea975-132">Select **Azure AD Domain Services** from hello search result.</span></span> <span data-ttu-id="ea975-133">Hello **les Services de domaine Active Directory de Azure** panneau répertorie hello domaine géré qui est en cours d’approvisionnement.</span><span class="sxs-lookup"><span data-stu-id="ea975-133">hello **Azure AD Domain Services** blade lists hello managed domain that is being provisioned.</span></span>

    ![Rechercher le domaine managé en cours d’approvisionnement](./media/getting-started/domain-services-provisioning-state-find-resource.png)

2. <span data-ttu-id="ea975-135">Cliquez sur nom hello hello géré (par exemple, « contoso100.com ») de domaine toosee plus de détails sur le domaine de hello.</span><span class="sxs-lookup"><span data-stu-id="ea975-135">Click hello name of hello managed domain (for example, 'contoso100.com') toosee more details about hello domain.</span></span>

    ![Domain Services - État d’approvisionnement](./media/getting-started/domain-services-provisioning-state.png)

3. <span data-ttu-id="ea975-137">Hello **vue d’ensemble** onglet affiche ce domaine hello est actuellement en cours d’approvisionnement.</span><span class="sxs-lookup"><span data-stu-id="ea975-137">hello **Overview** tab shows that hello domain is currently being provisioned.</span></span> <span data-ttu-id="ea975-138">Vous ne pouvez pas configurer le domaine géré de hello jusqu'à ce qu’il est entièrement configuré.</span><span class="sxs-lookup"><span data-stu-id="ea975-138">You cannot configure hello managed domain until it is fully provisioned.</span></span> <span data-ttu-id="ea975-139">Cela peut prendre jusqu'à l’heure tooan pour votre toobe domaine géré entièrement configuré.</span><span class="sxs-lookup"><span data-stu-id="ea975-139">It may take up tooan hour for your managed domain toobe fully provisioned.</span></span>

    ![<span data-ttu-id="ea975-140">Services de domaine - onglet vue d’ensemble au cours de l’état d’approvisionnement de hello</span><span class="sxs-lookup"><span data-stu-id="ea975-140">Domain Services - Overview tab during hello provisioning state</span></span> ](./media/getting-started/domain-services-provisioning-state-details.png)

4. <span data-ttu-id="ea975-141">Lorsque le domaine géré de hello est entièrement configuré, hello **vue d’ensemble** onglet affiche l’état domaine hello **en cours d’exécution**.</span><span class="sxs-lookup"><span data-stu-id="ea975-141">When hello managed domain is fully provisioned, hello **Overview** tab shows hello domain status as **Running**.</span></span>

    ![Domain Services - Onglet Vue d’ensemble une fois la configuration terminée](./media/getting-started/domain-services-provisioned.png)

5. <span data-ttu-id="ea975-143">Sur hello **propriétés** onglet, vous voyez deux adresses IP pour le domaine contrôleurs sont disponibles pour les réseaux virtuels hello.</span><span class="sxs-lookup"><span data-stu-id="ea975-143">On hello **Properties** tab, you see two IP addresses at which domain controllers are available for hello virtual network.</span></span>

    ![Domain Services - Onglet Propriétés après un approvisionnement complet](./media/getting-started/domain-services-provisioned-properties.png)


## <a name="next-step"></a><span data-ttu-id="ea975-145">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="ea975-145">Next step</span></span>
[<span data-ttu-id="ea975-146">Tâche 4 : mettre à jour les paramètres DNS hello hello réseau virtuel Azure</span><span class="sxs-lookup"><span data-stu-id="ea975-146">Task 4: update hello DNS settings for hello Azure virtual network</span></span>](active-directory-ds-getting-started-dns.md)
