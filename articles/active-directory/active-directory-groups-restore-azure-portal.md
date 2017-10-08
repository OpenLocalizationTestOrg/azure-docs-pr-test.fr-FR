---
title: "groupe aaaRestore un supprimé Office 365 dans Azure Active Directory | Documents Microsoft"
description: "Comment toorestore un groupe supprimé, afficher les groupes qui peuvent être restaurés et permamnently supprimer un groupe dans Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: cc5f232a-1e77-45c2-b28b-1fcb4621725c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: curtand
ms.openlocfilehash: 4e6650d64aa19f0c909f1c511f48681de8032f63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="restore-a-deleted-office-365-group-in-azure-active-directory"></a><span data-ttu-id="20146-103">Restaurer un groupe Office 365 supprimé dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="20146-103">Restore a deleted Office 365 group in Azure Active Directory</span></span>

<span data-ttu-id="20146-104">Lorsque vous supprimez un groupe Office 365 Bonjour Azure Active Directory (Azure AD), groupe de hello supprimé est conservée, mais n’est pas visible pendant 30 jours à partir de la date de suppression hello.</span><span class="sxs-lookup"><span data-stu-id="20146-104">When you delete an Office 365 group in hello Azure Active Directory (Azure AD), hello deleted group is retained but not visible for 30 days from hello deletion date.</span></span> <span data-ttu-id="20146-105">Il s’agit afin que le groupe de hello et son contenu peut être restaurées si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="20146-105">This is so that hello group and its contents can be restored if needed.</span></span> <span data-ttu-id="20146-106">Cette fonctionnalité est limitée exclusivement tooOffice 365 groupes dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="20146-106">This functionality is restricted exclusively tooOffice 365 groups in Azure AD.</span></span> <span data-ttu-id="20146-107">Elle n’est pas disponible pour les groupes de sécurité et les groupes de distribution.</span><span class="sxs-lookup"><span data-stu-id="20146-107">It is not available for security groups and distribution groups.</span></span>

> [!NOTE] 
> <span data-ttu-id="20146-108">N’utilisez pas `Remove-MsolGroup` , car il implique l’élimination de groupe de hello définitivement.</span><span class="sxs-lookup"><span data-stu-id="20146-108">Don't use `Remove-MsolGroup` because it purges hello group permanently.</span></span> <span data-ttu-id="20146-109">Toujours utiliser `Remove-AzureADMSGroup` toodelete un O365 groupe.</span><span class="sxs-lookup"><span data-stu-id="20146-109">Always use `Remove-AzureADMSGroup` toodelete an O365 group.</span></span> 

<span data-ttu-id="20146-110">les autorisations de Hello requises toorestore un groupe peut être hello suivants :</span><span class="sxs-lookup"><span data-stu-id="20146-110">hello permissions required toorestore a group can be any of hello following:</span></span>

<span data-ttu-id="20146-111">Rôle</span><span class="sxs-lookup"><span data-stu-id="20146-111">Role</span></span>  | <span data-ttu-id="20146-112">Autorisations</span><span class="sxs-lookup"><span data-stu-id="20146-112">Permissions</span></span> 
--------- | ---------
<span data-ttu-id="20146-113">Administrateur de la société, Prise en charge du partenaire de niveau 2 et Administrateurs de services InTune</span><span class="sxs-lookup"><span data-stu-id="20146-113">Company Administrator, Partner Tier2 support, and InTune Service Admins</span></span> | <span data-ttu-id="20146-114">Peut restaurer n’importe quel groupe Office 365 supprimé</span><span class="sxs-lookup"><span data-stu-id="20146-114">Can restore any deleted Office 365 group</span></span> 
<span data-ttu-id="20146-115">Administrateur de compte d’utilisateur et Prise en charge du partenaire de niveau 2</span><span class="sxs-lookup"><span data-stu-id="20146-115">User Account Administrator and Partner Tier1 support</span></span> | <span data-ttu-id="20146-116">Peut restaurer n’importe quel groupe Office 365 supprimé à l’exception de ces toohello attribué de rôle d’administrateur d’entreprise</span><span class="sxs-lookup"><span data-stu-id="20146-116">Can restore any deleted Office 365 group except those assigned toohello Company Administrator role</span></span> 
<span data-ttu-id="20146-117">Utilisateur</span><span class="sxs-lookup"><span data-stu-id="20146-117">User</span></span> | <span data-ttu-id="20146-118">Peut restaurer n’importe quel groupe Office 365 supprimé dont il est propriétaire</span><span class="sxs-lookup"><span data-stu-id="20146-118">Can restore any deleted Office 365 group that they owned</span></span> 


## <a name="view-hello-deleted-office-365-groups-that-are-available-toorestore"></a><span data-ttu-id="20146-119">Hello d’affichage supprimé les groupes Office 365 qui sont disponible toorestore</span><span class="sxs-lookup"><span data-stu-id="20146-119">View hello deleted Office 365 groups that are available toorestore</span></span>
<span data-ttu-id="20146-120">Hello suivant d’applets de commande peut être utilisé tooview hello supprimé groupes tooverify qui hello une ou ceux que vous êtes intéressé n'ont pas encore été définitivement supprimés.</span><span class="sxs-lookup"><span data-stu-id="20146-120">hello following cmdlets can be used tooview hello deleted groups tooverify that hello one or ones you're interested in have not yet been permanently purged.</span></span> <span data-ttu-id="20146-121">Ces applets de commande font partie de hello [module PowerShell Azure AD](https://www.powershellgallery.com/packages/AzureAD/).</span><span class="sxs-lookup"><span data-stu-id="20146-121">These cmdlets are part of hello [Azure AD PowerShell module](https://www.powershellgallery.com/packages/AzureAD/).</span></span> <span data-ttu-id="20146-122">Vous trouverez plus d’informations sur ce module Bonjour [Azure Active Directory PowerShell Version 2](/powershell/azure/install-adv2?view=azureadps-2.0) l’article.</span><span class="sxs-lookup"><span data-stu-id="20146-122">More information about this module can be found in hello [Azure Active Directory PowerShell Version 2](/powershell/azure/install-adv2?view=azureadps-2.0) article.</span></span>

1.  <span data-ttu-id="20146-123">Exécutez hello suivant l’applet de commande toodisplay toutes les supprimer les groupes Office 365 dans votre client qui sont toujours disponible toorestore.</span><span class="sxs-lookup"><span data-stu-id="20146-123">Run hello following cmdlet toodisplay all deleted Office 365 groups in your tenant that are still available toorestore.</span></span>
  ```
  Get-AzureADMSDeletedGroup
  ```

2.  <span data-ttu-id="20146-124">Ou bien, si vous savez objectID hello d’un groupe spécifique (et vous pouvez l’obtenir à partir de l’applet de commande hello à l’étape 1), hello exécution suivant tooverify applet de commande qui hello groupe supprimé spécifique n'a pas encore été définitivement supprimé.</span><span class="sxs-lookup"><span data-stu-id="20146-124">Alternately, if you know hello objectID of a specific group (and you can get it from hello cmdlet in step 1), run hello following cmdlet tooverify that hello specific deleted group has not yet been permanently purged.</span></span>
  ```
  Get-AzureADMSDeletedGroup –Id <objectId>
  ```



## <a name="how-toorestore-your-deleted-office-365-group"></a><span data-ttu-id="20146-125">Comment toorestore votre groupe Office 365 supprimé</span><span class="sxs-lookup"><span data-stu-id="20146-125">How toorestore your deleted Office 365 group</span></span>
<span data-ttu-id="20146-126">Une fois que vous avez vérifié que hello ce groupe est toujours disponible toorestore, restauration hello a supprimé le groupe avec l’un des hello comme suit.</span><span class="sxs-lookup"><span data-stu-id="20146-126">Once you have verified that hello group is still available toorestore, restore hello deleted group with one of hello following steps.</span></span> <span data-ttu-id="20146-127">Si le groupe de hello contient des documents, des sites de Service Pack ou d’autres objets persistants, elle peut prendre too24 heures toofully restaurer un groupe et son contenu.</span><span class="sxs-lookup"><span data-stu-id="20146-127">If hello group contains documents, SP sites, or other persistent objects, it might take up too24 hours toofully restore a group and its contents.</span></span>

1.  <span data-ttu-id="20146-128">Exécution hello après le groupe de hello toorestore applet de commande et son contenu.</span><span class="sxs-lookup"><span data-stu-id="20146-128">Run hello following cmdlet toorestore hello group and its contents.</span></span>
  
  ```
  Restore-AzureADMSDeletedDirectoryObject –Id <objectId>
  ``` 

<span data-ttu-id="20146-129">Vous pouvez également hello applet de commande suivante peut être exécuté toopermanently supprimer le groupe hello supprimé.</span><span class="sxs-lookup"><span data-stu-id="20146-129">Alternatively, hello following cmdlet can be run toopermanently remove hello deleted group.</span></span>
  ```
  Remove-AzureADMSDeletedDirectoryObject –Id <objectId>
  ```

## <a name="how-do-you-know-this-worked"></a><span data-ttu-id="20146-130">Comment savez-vous si l’opération a fonctionné ?</span><span class="sxs-lookup"><span data-stu-id="20146-130">How do you know this worked?</span></span>
<span data-ttu-id="20146-131">tooverify que vous avez restauré un groupe Office 365, exécutez hello `Get-AzureADGroup –ObjectId <objectId>` applet de commande toodisplay plus d’informations sur le groupe de hello.</span><span class="sxs-lookup"><span data-stu-id="20146-131">tooverify that you’ve successfully restored an Office 365 group, run hello `Get-AzureADGroup –ObjectId <objectId>` cmdlet toodisplay information about hello group.</span></span> <span data-ttu-id="20146-132">Après la restauration de hello demande est terminée :</span><span class="sxs-lookup"><span data-stu-id="20146-132">After hello restore request is completed:</span></span>
- <span data-ttu-id="20146-133">groupe de Hello s’affiche dans la barre de navigation gauche de hello sur Exchange</span><span class="sxs-lookup"><span data-stu-id="20146-133">hello group will appear in hello Left nav bar on Exchange</span></span>
- <span data-ttu-id="20146-134">plan Hello pour le groupe de hello s’affiche dans le planificateur</span><span class="sxs-lookup"><span data-stu-id="20146-134">hello plan for hello group will appear in Planner</span></span>
- <span data-ttu-id="20146-135">Les sites Sharepoint et tout leur contenu sont disponibles.</span><span class="sxs-lookup"><span data-stu-id="20146-135">Any Sharepoint sites and all of their contents will be available</span></span>
- <span data-ttu-id="20146-136">groupe de Hello est accessible à partir d’un des points de terminaison Exchange hello et autres charges de travail Office 365 qui prennent en charge les groupes Office 365</span><span class="sxs-lookup"><span data-stu-id="20146-136">hello group can be accessed from any of hello Exchange endpoints and other Office 365 workloads that support Office 365 groups</span></span>


## <a name="next-steps"></a><span data-ttu-id="20146-137">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="20146-137">Next steps</span></span>
<span data-ttu-id="20146-138">Ces articles fournissent des informations supplémentaires sur les groupes Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="20146-138">These articles provide additional information on Azure Active Directory groups.</span></span>

* [<span data-ttu-id="20146-139">Consulter les groupes existants</span><span class="sxs-lookup"><span data-stu-id="20146-139">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="20146-140">Gérer les paramètres d’un groupe</span><span class="sxs-lookup"><span data-stu-id="20146-140">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="20146-141">Gérer les membres d’un groupe</span><span class="sxs-lookup"><span data-stu-id="20146-141">Manage members of a group</span></span>](active-directory-groups-members-azure-portal.md)
* [<span data-ttu-id="20146-142">Gérer l’appartenance à un groupe</span><span class="sxs-lookup"><span data-stu-id="20146-142">Manage memberships of a group</span></span>](active-directory-groups-membership-azure-portal.md)
* [<span data-ttu-id="20146-143">Gérer les règles dynamiques pour les utilisateurs dans un groupe</span><span class="sxs-lookup"><span data-stu-id="20146-143">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
