---
title: "Bien démarrer avec Azure Active Directory Domain Services | Microsoft Docs"
description: "Activer Azure Active Directory Domain Services à l’aide du portail Azure (préversion)"
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
ms.openlocfilehash: f87bcf33d3b1eb21c7d84814e4c4086f664e293d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="enable-azure-active-directory-domain-services-using-the-azure-portal-preview"></a><span data-ttu-id="a6fba-103">Activer Azure Active Directory Domain Services à l’aide du portail Azure (préversion)</span><span class="sxs-lookup"><span data-stu-id="a6fba-103">Enable Azure Active Directory Domain Services using the Azure portal (Preview)</span></span>


## <a name="task-3-configure-administrative-group"></a><span data-ttu-id="a6fba-104">Tâche 3 : configurer le groupe d’administration</span><span class="sxs-lookup"><span data-stu-id="a6fba-104">Task 3: configure administrative group</span></span>
<span data-ttu-id="a6fba-105">Dans cette tâche de configuration, vous allez créer un groupe d’administration dans votre répertoire Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a6fba-105">In this configuration task, you create an administrative group in your Azure AD directory.</span></span> <span data-ttu-id="a6fba-106">Ce groupe d’administration spécial est appelé *AAD DC Administrators*.</span><span class="sxs-lookup"><span data-stu-id="a6fba-106">This special administrative group is called *AAD DC Administrators*.</span></span> <span data-ttu-id="a6fba-107">Les membres de ce groupe bénéficient d’autorisations d’administration sur les machines jointes au domaine managé.</span><span class="sxs-lookup"><span data-stu-id="a6fba-107">Members of this group are granted administrative permissions on machines that are domain-joined to the managed domain.</span></span> <span data-ttu-id="a6fba-108">Sur les ordinateurs joints au domaine, ce groupe est ajouté au groupe « Administrateurs ».</span><span class="sxs-lookup"><span data-stu-id="a6fba-108">On domain-joined machines, this group is added to the administrators group.</span></span> <span data-ttu-id="a6fba-109">En outre, les membres de ce groupe sont également autorisés à utiliser le Bureau à distance pour se connecter à distance aux ordinateurs joints au domaine.</span><span class="sxs-lookup"><span data-stu-id="a6fba-109">Additionally, members of this group can use Remote Desktop to connect remotely to domain-joined machines.</span></span>

> [!NOTE]
> <span data-ttu-id="a6fba-110">Vous ne bénéficiez pas des autorisations d’administrateur de domaine ou d’administrateur d’entreprise sur le domaine géré que vous avez créé à l’aide des services de domaine Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a6fba-110">You do not have Domain Administrator or Enterprise Administrator permissions on the managed domain that you created by using Azure Active Directory Domain Services.</span></span> <span data-ttu-id="a6fba-111">Dans un domaine géré, ces autorisations sont réservées par le service et ne sont pas accessibles aux utilisateurs au sein du client.</span><span class="sxs-lookup"><span data-stu-id="a6fba-111">On managed domains, these permissions are reserved by the service and are not made available to users within the tenant.</span></span> <span data-ttu-id="a6fba-112">Toutefois, vous pouvez utiliser le groupe d’administrateurs spécial créé dans cette tâche de configuration, afin d’exécuter des opérations privilégiées.</span><span class="sxs-lookup"><span data-stu-id="a6fba-112">However, you can use the special administrative group created in this configuration task to perform some privileged operations.</span></span> <span data-ttu-id="a6fba-113">Ces opérations comprennent l’ajout d’ordinateurs au domaine, l’appartenance au groupe Administrateurs sur les ordinateurs joints au domaine, la configuration de stratégie de groupe.</span><span class="sxs-lookup"><span data-stu-id="a6fba-113">These operations include joining computers to the domain, belonging to the administration group on domain-joined machines, and configuring Group Policy.</span></span>
>

<span data-ttu-id="a6fba-114">L’Assistant crée automatiquement le groupe d’administration dans votre répertoire Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a6fba-114">The wizard automatically creates the administrative group in your Azure AD directory.</span></span> <span data-ttu-id="a6fba-115">Ce groupe est appelé « Administrateurs AAD DC ».</span><span class="sxs-lookup"><span data-stu-id="a6fba-115">This group is called 'AAD DC Administrators'.</span></span> <span data-ttu-id="a6fba-116">Si vous disposez d’un groupe du même nom dans votre répertoire Azure AD, l’Assistant sélectionne ce groupe.</span><span class="sxs-lookup"><span data-stu-id="a6fba-116">If you have an existing group with this name in your Azure AD directory, the wizard selects this group.</span></span> <span data-ttu-id="a6fba-117">Vous pouvez configurer l’appartenance au groupe au moyen de la page **Groupe des administrateurs** de l’Assistant.</span><span class="sxs-lookup"><span data-stu-id="a6fba-117">You can configure group membership using the **Administrator group** wizard page.</span></span>

1. <span data-ttu-id="a6fba-118">Pour configurer l’appartenance au groupe, cliquez sur **Administrateurs AAD DC**.</span><span class="sxs-lookup"><span data-stu-id="a6fba-118">To configure group membership, click **AAD DC Administrators**.</span></span>

    ![Configurer l’appartenance au groupe](./media/getting-started/domain-services-blade-admingroup.png)

2. <span data-ttu-id="a6fba-120">Cliquez sur le bouton **Ajouter des membres** pour ajouter des utilisateurs au groupe Administrateurs à partir de votre répertoire Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a6fba-120">Click the **Add members** button to add users from your Azure AD directory to the administrator group.</span></span>

3. <span data-ttu-id="a6fba-121">Lorsque vous avez terminé, cliquez sur **OK** pour accéder à la page **Résumé** de l’Assistant.</span><span class="sxs-lookup"><span data-stu-id="a6fba-121">When you are done, click **OK** to move on to the **Summary** page of the wizard.</span></span>

4. <span data-ttu-id="a6fba-122">Dans la page **Résumé** de l’Assistant, examinez les paramètres de configuration du domaine managé.</span><span class="sxs-lookup"><span data-stu-id="a6fba-122">On the **Summary** page of the wizard, review the configuration settings for the managed domain.</span></span> <span data-ttu-id="a6fba-123">Si nécessaire, vous pouvez revenir à une étape quelconque de l’Assistant pour y apporter des modifications.</span><span class="sxs-lookup"><span data-stu-id="a6fba-123">You can go back to any step of the wizard to make changes, if necessary.</span></span> <span data-ttu-id="a6fba-124">Lorsque vous avez terminé, cliquez sur **OK** pour créer le domaine managé.</span><span class="sxs-lookup"><span data-stu-id="a6fba-124">When you are done, click **OK** to create the new managed domain.</span></span>

    ![Résumé](./media/getting-started/domain-services-blade-summary.png)

5. <span data-ttu-id="a6fba-126">Vous voyez une notification indiquant la progression de votre déploiement Azure AD Domain Services.</span><span class="sxs-lookup"><span data-stu-id="a6fba-126">You see a notification that shows the progress of your Azure AD Domain Services deployment.</span></span> <span data-ttu-id="a6fba-127">Cliquez sur la notification pour afficher la progression détaillée du déploiement.</span><span class="sxs-lookup"><span data-stu-id="a6fba-127">Click the notification to see detailed progress for the deployment.</span></span>

    ![Notification - Déploiement en cours](./media/getting-started/domain-services-blade-deployment-in-progress.png)


## <a name="provision-your-managed-domain"></a><span data-ttu-id="a6fba-129">Approvisionner votre domaine managé</span><span class="sxs-lookup"><span data-stu-id="a6fba-129">Provision your managed domain</span></span>
<span data-ttu-id="a6fba-130">Le processus d’approvisionnement de votre domaine managé peut prendre jusqu’à une heure.</span><span class="sxs-lookup"><span data-stu-id="a6fba-130">The process of provisioning your managed domain can take up to an hour.</span></span>

1. <span data-ttu-id="a6fba-131">Pendant que votre déploiement est en cours, vous pouvez rechercher « Domain Services » dans la zone de recherche **Rechercher des ressources**.</span><span class="sxs-lookup"><span data-stu-id="a6fba-131">While your deployment is in progress, you can search for 'domain services' in the **Search resources** search box.</span></span> <span data-ttu-id="a6fba-132">Sélectionnez **Azure AD Domain Services** dans les résultats de la recherche.</span><span class="sxs-lookup"><span data-stu-id="a6fba-132">Select **Azure AD Domain Services** from the search result.</span></span> <span data-ttu-id="a6fba-133">Le panneau **Azure AD Domain Services** affiche le domaine managé en cours d’approvisionnement.</span><span class="sxs-lookup"><span data-stu-id="a6fba-133">The **Azure AD Domain Services** blade lists the managed domain that is being provisioned.</span></span>

    ![Rechercher le domaine managé en cours d’approvisionnement](./media/getting-started/domain-services-provisioning-state-find-resource.png)

2. <span data-ttu-id="a6fba-135">Pour plus d’informations sur le domaine, cliquez sur le nom du domaine managé (par exemple, « contoso100.com »).</span><span class="sxs-lookup"><span data-stu-id="a6fba-135">Click the name of the managed domain (for example, 'contoso100.com') to see more details about the domain.</span></span>

    ![Domain Services - État d’approvisionnement](./media/getting-started/domain-services-provisioning-state.png)

3. <span data-ttu-id="a6fba-137">L’onglet **Vue d’ensemble** montre que le domaine est actuellement en cours d’approvisionnement.</span><span class="sxs-lookup"><span data-stu-id="a6fba-137">The **Overview** tab shows that the domain is currently being provisioned.</span></span> <span data-ttu-id="a6fba-138">Vous ne pouvez pas configurer le domaine managé tant qu’il n’est pas entièrement approvisionné.</span><span class="sxs-lookup"><span data-stu-id="a6fba-138">You cannot configure the managed domain until it is fully provisioned.</span></span> <span data-ttu-id="a6fba-139">L’approvisionnement complet de votre domaine managé peut prendre jusqu’à une heure.</span><span class="sxs-lookup"><span data-stu-id="a6fba-139">It may take up to an hour for your managed domain to be fully provisioned.</span></span>

    ![<span data-ttu-id="a6fba-140">Domain Services - Onglet Vue d’ensemble durant l’approvisionnement</span><span class="sxs-lookup"><span data-stu-id="a6fba-140">Domain Services - Overview tab during the provisioning state</span></span> ](./media/getting-started/domain-services-provisioning-state-details.png)

4. <span data-ttu-id="a6fba-141">Lorsque le domaine managé est entièrement approvisionné, l’onglet **Vue d’ensemble** affiche l’état du domaine comme **En cours d’exécution**.</span><span class="sxs-lookup"><span data-stu-id="a6fba-141">When the managed domain is fully provisioned, the **Overview** tab shows the domain status as **Running**.</span></span>

    ![Domain Services - Onglet Vue d’ensemble une fois la configuration terminée](./media/getting-started/domain-services-provisioned.png)

5. <span data-ttu-id="a6fba-143">Sous l’onglet **Propriétés**, vous voyez deux adresses IP auxquelles des contrôleurs de domaine sont disponibles pour le réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="a6fba-143">On the **Properties** tab, you see two IP addresses at which domain controllers are available for the virtual network.</span></span>

    ![Domain Services - Onglet Propriétés après un approvisionnement complet](./media/getting-started/domain-services-provisioned-properties.png)


## <a name="next-step"></a><span data-ttu-id="a6fba-145">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="a6fba-145">Next step</span></span>
[<span data-ttu-id="a6fba-146">Tâche 4 : Mettre à jour les paramètres DNS pour le réseau virtuel Azure</span><span class="sxs-lookup"><span data-stu-id="a6fba-146">Task 4: update the DNS settings for the Azure virtual network</span></span>](active-directory-ds-getting-started-dns.md)
