---
title: "Restaurer un groupe Office 365 supprimé dans Azure Active Directory | Microsoft Docs"
description: "Comment restaurer un groupe supprimé, afficher les groupes pouvant être restaurés et supprimer de façon permanente un groupe dans Azure Active Directory"
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
ms.openlocfilehash: 32d36ae96797a59bb47bf782ab038f21f231f046
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="restore-a-deleted-office-365-group-in-azure-active-directory"></a><span data-ttu-id="d35f1-103">Restaurer un groupe Office 365 supprimé dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d35f1-103">Restore a deleted Office 365 group in Azure Active Directory</span></span>

<span data-ttu-id="d35f1-104">Lorsque vous supprimez un groupe Office 365 dans Azure Active Directory (Azure AD), celui-ci est conservé, mais il n’est pas visible pendant 30 jours à partir de la date de suppression.</span><span class="sxs-lookup"><span data-stu-id="d35f1-104">When you delete an Office 365 group in the Azure Active Directory (Azure AD), the deleted group is retained but not visible for 30 days from the deletion date.</span></span> <span data-ttu-id="d35f1-105">De cette façon, le groupe et son contenu peuvent être restaurés au besoin.</span><span class="sxs-lookup"><span data-stu-id="d35f1-105">This is so that the group and its contents can be restored if needed.</span></span> <span data-ttu-id="d35f1-106">Cette fonctionnalité est limitée exclusivement aux groupes Office 365 dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d35f1-106">This functionality is restricted exclusively to Office 365 groups in Azure AD.</span></span> <span data-ttu-id="d35f1-107">Elle n’est pas disponible pour les groupes de sécurité et les groupes de distribution.</span><span class="sxs-lookup"><span data-stu-id="d35f1-107">It is not available for security groups and distribution groups.</span></span>

> [!NOTE] 
> <span data-ttu-id="d35f1-108">N’utilisez pas `Remove-MsolGroup`, car il vide le groupe définitivement.</span><span class="sxs-lookup"><span data-stu-id="d35f1-108">Don't use `Remove-MsolGroup` because it purges the group permanently.</span></span> <span data-ttu-id="d35f1-109">Utilisez toujours `Remove-AzureADMSGroup` pour supprimer un groupe O365.</span><span class="sxs-lookup"><span data-stu-id="d35f1-109">Always use `Remove-AzureADMSGroup` to delete an O365 group.</span></span> 

<span data-ttu-id="d35f1-110">Les autorisations requises pour restaurer un groupe peuvent être les suivantes :</span><span class="sxs-lookup"><span data-stu-id="d35f1-110">The permissions required to restore a group can be any of the following:</span></span>

<span data-ttu-id="d35f1-111">Rôle</span><span class="sxs-lookup"><span data-stu-id="d35f1-111">Role</span></span>  | <span data-ttu-id="d35f1-112">Autorisations</span><span class="sxs-lookup"><span data-stu-id="d35f1-112">Permissions</span></span> 
--------- | ---------
<span data-ttu-id="d35f1-113">Administrateur de la société, Prise en charge du partenaire de niveau 2 et Administrateurs de services InTune</span><span class="sxs-lookup"><span data-stu-id="d35f1-113">Company Administrator, Partner Tier2 support, and InTune Service Admins</span></span> | <span data-ttu-id="d35f1-114">Peut restaurer n’importe quel groupe Office 365 supprimé</span><span class="sxs-lookup"><span data-stu-id="d35f1-114">Can restore any deleted Office 365 group</span></span> 
<span data-ttu-id="d35f1-115">Administrateur de compte d’utilisateur et Prise en charge du partenaire de niveau 2</span><span class="sxs-lookup"><span data-stu-id="d35f1-115">User Account Administrator and Partner Tier1 support</span></span> | <span data-ttu-id="d35f1-116">Peut restaurer n’importe quel groupe Office 365 supprimé, à l’exception de ceux affectés au rôle Administrateur de la société</span><span class="sxs-lookup"><span data-stu-id="d35f1-116">Can restore any deleted Office 365 group except those assigned to the Company Administrator role</span></span> 
<span data-ttu-id="d35f1-117">Utilisateur</span><span class="sxs-lookup"><span data-stu-id="d35f1-117">User</span></span> | <span data-ttu-id="d35f1-118">Peut restaurer n’importe quel groupe Office 365 supprimé dont il est propriétaire</span><span class="sxs-lookup"><span data-stu-id="d35f1-118">Can restore any deleted Office 365 group that they owned</span></span> 


## <a name="view-the-deleted-office-365-groups-that-are-available-to-restore"></a><span data-ttu-id="d35f1-119">Afficher des groupes Office 365 supprimés disponibles pour la restauration</span><span class="sxs-lookup"><span data-stu-id="d35f1-119">View the deleted Office 365 groups that are available to restore</span></span>
<span data-ttu-id="d35f1-120">Les applets de commande suivantes peuvent servir à afficher les groupes supprimés pour vérifier que ceux qui vous intéressent n’ont pas encore été supprimés de façon définitive.</span><span class="sxs-lookup"><span data-stu-id="d35f1-120">The following cmdlets can be used to view the deleted groups to verify that the one or ones you're interested in have not yet been permanently purged.</span></span> <span data-ttu-id="d35f1-121">Ces cmdlets font partie du module [Azure AD PowerShell](https://www.powershellgallery.com/packages/AzureAD/).</span><span class="sxs-lookup"><span data-stu-id="d35f1-121">These cmdlets are part of the [Azure AD PowerShell module](https://www.powershellgallery.com/packages/AzureAD/).</span></span> <span data-ttu-id="d35f1-122">Pour plus d’informations sur ce module, consultez l’article [Azure Active Directory PowerShell Version 2](/powershell/azure/install-adv2?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="d35f1-122">More information about this module can be found in the [Azure Active Directory PowerShell Version 2](/powershell/azure/install-adv2?view=azureadps-2.0) article.</span></span>

1.  <span data-ttu-id="d35f1-123">Exécutez l’applet de commande suivante pour afficher tous les groupes Office 365 supprimés dans votre locataire et dont la restauration est toujours possible.</span><span class="sxs-lookup"><span data-stu-id="d35f1-123">Run the following cmdlet to display all deleted Office 365 groups in your tenant that are still available to restore.</span></span>
  ```
  Get-AzureADMSDeletedGroup
  ```

2.  <span data-ttu-id="d35f1-124">Ou, si vous connaissez l’ID d’objet d’un groupe spécifique (que vous pouvez obtenir à partir de l’applet de commande indiquée à l’étape 1), exécutez l’applet de commande suivante pour vérifier que le groupe supprimé spécifique n’a pas encore été supprimé de façon définitive.</span><span class="sxs-lookup"><span data-stu-id="d35f1-124">Alternately, if you know the objectID of a specific group (and you can get it from the cmdlet in step 1), run the following cmdlet to verify that the specific deleted group has not yet been permanently purged.</span></span>
  ```
  Get-AzureADMSDeletedGroup –Id <objectId>
  ```



## <a name="how-to-restore-your-deleted-office-365-group"></a><span data-ttu-id="d35f1-125">Comment restaurer votre groupe Office 365 supprimé</span><span class="sxs-lookup"><span data-stu-id="d35f1-125">How to restore your deleted Office 365 group</span></span>
<span data-ttu-id="d35f1-126">Une fois que vous avez vérifié que le groupe est toujours disponible pour la restauration, restaurez-le en effectuant l’une des étapes suivantes.</span><span class="sxs-lookup"><span data-stu-id="d35f1-126">Once you have verified that the group is still available to restore, restore the deleted group with one of the following steps.</span></span> <span data-ttu-id="d35f1-127">Si le groupe contient des documents, des sites SP ou d’autres objets persistants, la restauration du groupe et de son contenu peut nécessiter jusqu’à 24 heures.</span><span class="sxs-lookup"><span data-stu-id="d35f1-127">If the group contains documents, SP sites, or other persistent objects, it might take up to 24 hours to fully restore a group and its contents.</span></span>

1.  <span data-ttu-id="d35f1-128">Exécutez l’applet de commande suivante pour restaurer le groupe et son contenu.</span><span class="sxs-lookup"><span data-stu-id="d35f1-128">Run the following cmdlet to restore the group and its contents.</span></span>
  
  ```
  Restore-AzureADMSDeletedDirectoryObject –Id <objectId>
  ``` 

<span data-ttu-id="d35f1-129">Vous pouvez également exécuter l’applet de commande suivante pour supprimer définitivement le groupe supprimé.</span><span class="sxs-lookup"><span data-stu-id="d35f1-129">Alternatively, the following cmdlet can be run to permanently remove the deleted group.</span></span>
  ```
  Remove-AzureADMSDeletedDirectoryObject –Id <objectId>
  ```

## <a name="how-do-you-know-this-worked"></a><span data-ttu-id="d35f1-130">Comment savez-vous si l’opération a fonctionné ?</span><span class="sxs-lookup"><span data-stu-id="d35f1-130">How do you know this worked?</span></span>
<span data-ttu-id="d35f1-131">Pour vérifier que vous avez correctement restauré un groupe Office 365, exécutez l’applet de commande `Get-AzureADGroup –ObjectId <objectId>` pour afficher des informations sur le groupe.</span><span class="sxs-lookup"><span data-stu-id="d35f1-131">To verify that you’ve successfully restored an Office 365 group, run the `Get-AzureADGroup –ObjectId <objectId>` cmdlet to display information about the group.</span></span> <span data-ttu-id="d35f1-132">Une fois que vous avez effectué la demande de restauration :</span><span class="sxs-lookup"><span data-stu-id="d35f1-132">After the restore request is completed:</span></span>
- <span data-ttu-id="d35f1-133">Le groupe s’affiche dans la barre de navigation de gauche dans Exchange.</span><span class="sxs-lookup"><span data-stu-id="d35f1-133">The group will appear in the Left nav bar on Exchange</span></span>
- <span data-ttu-id="d35f1-134">Le plan associé au groupe apparaît dans le planificateur.</span><span class="sxs-lookup"><span data-stu-id="d35f1-134">The plan for the group will appear in Planner</span></span>
- <span data-ttu-id="d35f1-135">Les sites Sharepoint et tout leur contenu sont disponibles.</span><span class="sxs-lookup"><span data-stu-id="d35f1-135">Any Sharepoint sites and all of their contents will be available</span></span>
- <span data-ttu-id="d35f1-136">Le groupe est accessible à partir des points de terminaison Exchange et des autres charges de travail Office 365 qui prennent en charge les groupes Office 365.</span><span class="sxs-lookup"><span data-stu-id="d35f1-136">The group can be accessed from any of the Exchange endpoints and other Office 365 workloads that support Office 365 groups</span></span>


## <a name="next-steps"></a><span data-ttu-id="d35f1-137">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d35f1-137">Next steps</span></span>
<span data-ttu-id="d35f1-138">Ces articles fournissent des informations supplémentaires sur les groupes Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d35f1-138">These articles provide additional information on Azure Active Directory groups.</span></span>

* [<span data-ttu-id="d35f1-139">Consulter les groupes existants</span><span class="sxs-lookup"><span data-stu-id="d35f1-139">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="d35f1-140">Gérer les paramètres d’un groupe</span><span class="sxs-lookup"><span data-stu-id="d35f1-140">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="d35f1-141">Gérer les membres d’un groupe</span><span class="sxs-lookup"><span data-stu-id="d35f1-141">Manage members of a group</span></span>](active-directory-groups-members-azure-portal.md)
* [<span data-ttu-id="d35f1-142">Gérer l’appartenance à un groupe</span><span class="sxs-lookup"><span data-stu-id="d35f1-142">Manage memberships of a group</span></span>](active-directory-groups-membership-azure-portal.md)
* [<span data-ttu-id="d35f1-143">Gérer les règles dynamiques pour les utilisateurs dans un groupe</span><span class="sxs-lookup"><span data-stu-id="d35f1-143">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
