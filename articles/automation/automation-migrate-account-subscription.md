---
title: "Migration d’un compte et de ressources Automation | Microsoft Docs"
description: "Cet article décrit comment déplacer un compte Automation dans Azure Automation et les ressources associées d’un abonnement vers un autre."
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: tysonn
ms.assetid: 9c2db4a2-f324-48dc-8ce7-3343bf7230d5
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/21/2016
ms.author: magoedte
ms.openlocfilehash: 687da15bdaf854254321b59350f47549781676f5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="migrate-automation-account-and-resources"></a><span data-ttu-id="48c8c-103">Migration d’un compte et de ressources Automation</span><span class="sxs-lookup"><span data-stu-id="48c8c-103">Migrate Automation Account and resources</span></span>
<span data-ttu-id="48c8c-104">Pour les comptes Automation et les ressources associées (composants, Runbooks, modules, etc.) que vous avez créées dans le Portail Azure et que vous souhaitez migrer d’un groupe de ressources à un autre ou d’un abonnement à un autre, vous pouvez utiliser en toute simplicité la fonctionnalité [déplacer des ressources](../azure-resource-manager/resource-group-move-resources.md) disponible dans le Portail Azure.</span><span class="sxs-lookup"><span data-stu-id="48c8c-104">For Automation accounts and its associated resources (i.e. assets, runbooks, modules, etc.) that you have created in the Azure portal and want to migrate from one resource group to another or from one subscription to another, you can accomplish this easily with the [move resources](../azure-resource-manager/resource-group-move-resources.md) feature available in the Azure portal.</span></span> <span data-ttu-id="48c8c-105">Toutefois, avant d’exécuter cette action, vous devez tout d’abord examiner cette [liste de vérification avant de déplacer des ressources](../azure-resource-manager/resource-group-move-resources.md#checklist-before-moving-resources) ainsi que la liste ci-dessous, propre à Automation.</span><span class="sxs-lookup"><span data-stu-id="48c8c-105">However, before proceeding with this action, you should first review the following [checklist before moving resources](../azure-resource-manager/resource-group-move-resources.md#checklist-before-moving-resources) and additionally, the list below specific to Automation.</span></span>   

1. <span data-ttu-id="48c8c-106">Le groupe de ressources/abonnement de destination doit figurer dans la même région que la source.</span><span class="sxs-lookup"><span data-stu-id="48c8c-106">The destination subscription/resource group must be in same region as the source.</span></span>  <span data-ttu-id="48c8c-107">Cela signifie que les comptes Automation ne peuvent pas être déplacés entre des régions.</span><span class="sxs-lookup"><span data-stu-id="48c8c-107">Meaning, Automation accounts cannot be moved across regions.</span></span>
2. <span data-ttu-id="48c8c-108">Lorsque vous déplacez des ressources (Runbooks, journaux, etc.), le groupe source et le groupe cible sont verrouillés pendant la durée de l'opération.</span><span class="sxs-lookup"><span data-stu-id="48c8c-108">When moving resources (e.g. runbooks, jobs, etc.), both the source group and the target group are locked for the duration of the operation.</span></span> <span data-ttu-id="48c8c-109">Les opérations d’écriture et de suppression sont bloquées sur les groupes tant que le déplacement n’est pas terminé.</span><span class="sxs-lookup"><span data-stu-id="48c8c-109">Write and delete operations are blocked on the groups until the move completes.</span></span>  
3. <span data-ttu-id="48c8c-110">La totalité des Runbooks ou variables faisant référence à une ressource à un ID d’abonnement de l’abonnement existant devra être mise à jour une fois la migration terminée.</span><span class="sxs-lookup"><span data-stu-id="48c8c-110">Any runbooks or variables which reference a resource or subscription ID from the existing subscription will need to be updated after migration is completed.</span></span>   

> [!NOTE]
> <span data-ttu-id="48c8c-111">Cette fonctionnalité ne prend pas en charge les ressources Automation classiques.</span><span class="sxs-lookup"><span data-stu-id="48c8c-111">This feature does not support moving Classic automation resources.</span></span>
>
>

## <a name="to-move-the-automation-account-using-the-portal"></a><span data-ttu-id="48c8c-112">Pour déplacer le compte Automation à l’aide du portail</span><span class="sxs-lookup"><span data-stu-id="48c8c-112">To move the Automation Account using the portal</span></span>
1. <span data-ttu-id="48c8c-113">À partir de votre compte Automation, cliquez sur **Déplacer** en haut du panneau.</span><span class="sxs-lookup"><span data-stu-id="48c8c-113">From your Automation account, click **Move** at the top of the blade.</span></span><br> <span data-ttu-id="48c8c-114">![option Déplacer](media/automation-migrate-account-subscription/automation-menu-move.png)</span><span class="sxs-lookup"><span data-stu-id="48c8c-114">![Move option](media/automation-migrate-account-subscription/automation-menu-move.png)</span></span><br>
2. <span data-ttu-id="48c8c-115">Notez que le panneau **Déplacer des ressources** présente les ressources liées à la fois à votre compte Automation et à vos groupes de ressources.</span><span class="sxs-lookup"><span data-stu-id="48c8c-115">On the **Move resources** blade, note that it presents resources related to both your Automation account and your resource group(s).</span></span>  <span data-ttu-id="48c8c-116">Sélectionnez **l’abonnement** et le **groupe de ressources** dans les listes déroulantes, ou sélectionnez l’option **créer un groupe de ressources** et entrez un nouveau nom de groupe de ressources dans le champ fourni.</span><span class="sxs-lookup"><span data-stu-id="48c8c-116">Select the **subscription** and **resource group** from the drop-down lists, or select the option **create a new resource group** and enter a new resource group name in the field provided.</span></span>  
3. <span data-ttu-id="48c8c-117">Vérifiez les informations et cochez la case pour confirmer que vous *comprenez que les outils et scripts devront être mis à jour afin d’utiliser les nouveaux ID de ressources une fois les ressources déplacées*, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="48c8c-117">Review and select the checkbox to acknowledge you *understand tools and scripts will need to be updated to use new resource IDs after resources have been moved* and then click **OK**.</span></span><br> <span data-ttu-id="48c8c-118">![panneau Déplacer des ressources](media/automation-migrate-account-subscription/automation-move-resources-blade.png)</span><span class="sxs-lookup"><span data-stu-id="48c8c-118">![Move Resources Blade](media/automation-migrate-account-subscription/automation-move-resources-blade.png)</span></span><br>   

<span data-ttu-id="48c8c-119">Cette opération peut prendre plusieurs minutes.</span><span class="sxs-lookup"><span data-stu-id="48c8c-119">This action will take several minutes to complete.</span></span>  <span data-ttu-id="48c8c-120">Le panneau **Notifications**affiche l’état de chaque action effectuée : validation, migration, puis confirmation que l’opération est terminée.</span><span class="sxs-lookup"><span data-stu-id="48c8c-120">In **Notifications**, you will be presented with a status of each action that takes place - validation, migration, and then finally when it is completed.</span></span>     

## <a name="to-move-the-automation-account-using-powershell"></a><span data-ttu-id="48c8c-121">Pour déplacer le compte Automation à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="48c8c-121">To move the Automation Account using PowerShell</span></span>
<span data-ttu-id="48c8c-122">Pour déplacer des ressources Automation existantes vers un autre groupe de ressources ou abonnement, utilisez l’applet de commande **Get-AzureRmResource** afin de récupérer le compte Automation en question, puis l’applet de commande**AzureRmResource de déplacement** afin d’effectuer le déplacement.</span><span class="sxs-lookup"><span data-stu-id="48c8c-122">To move existing Automation resources to another resource group or subscription, use the  **Get-AzureRmResource** cmdlet to get the specific Automation account and then **Move-AzureRmResource** cmdlet to perform the move.</span></span>

<span data-ttu-id="48c8c-123">Le premier exemple indique comment déplacer un compte Automation vers un nouveau groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="48c8c-123">The first example shows how to move an Automation account to a new resource group.</span></span>

   ```
    $resource = Get-AzureRmResource -ResourceName "TestAutomationAccount" -ResourceGroupName "ResourceGroup01"
    Move-AzureRmResource -ResourceId $resource.ResourceId -DestinationResourceGroupName "NewResourceGroup"
   ```

<span data-ttu-id="48c8c-124">Une fois que vous exécutez l’exemple de code ci-dessus, vous devrez confirmer que vous souhaitez effectuer cette action.</span><span class="sxs-lookup"><span data-stu-id="48c8c-124">After you execute the above code example, you will be prompted to verify you want to perform this action.</span></span>  <span data-ttu-id="48c8c-125">Une fois que vous cliquez sur **Oui** et autoriser l’exécution du script, vous ne recevrez plus d’autres notifications pendant la migration.</span><span class="sxs-lookup"><span data-stu-id="48c8c-125">Once you click **Yes** and allow the script to proceed, you will not receive any notifications while it's performing the migration.</span></span>  

<span data-ttu-id="48c8c-126">Pour déplacer des ressources vers un nouvel abonnement, renseignez une valeur pour le paramètre *DestinationSubscriptionId* .</span><span class="sxs-lookup"><span data-stu-id="48c8c-126">To move to a new subscription, include a value for the *DestinationSubscriptionId* parameter.</span></span>

   ```
    $resource = Get-AzureRmResource -ResourceName "TestAutomationAccount" -ResourceGroupName "ResourceGroup01"
    Move-AzureRmResource -ResourceId $resource.ResourceId -DestinationResourceGroupName "NewResourceGroup" -DestinationSubscriptionId "SubscriptionId"
   ```

<span data-ttu-id="48c8c-127">Comme dans l’exemple précédent, vous devrez confirmer le déplacement.</span><span class="sxs-lookup"><span data-stu-id="48c8c-127">As with the previous example, you will be prompted to confirm the move.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="48c8c-128">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="48c8c-128">Next steps</span></span>
* <span data-ttu-id="48c8c-129">Pour plus d’informations sur le déplacement de ressources vers un nouveau groupe de ressources ou un nouvel abonnement, consultez [Déplacer des ressources vers un nouveau groupe de ressource ou un nouvel abonnement](../azure-resource-manager/resource-group-move-resources.md)</span><span class="sxs-lookup"><span data-stu-id="48c8c-129">For more information about moving resources to new resource group or subscription, see [Move  resources to new resource group or subscription](../azure-resource-manager/resource-group-move-resources.md)</span></span>
* <span data-ttu-id="48c8c-130">Pour plus d’informations sur le contrôle d’accès en fonction du rôle dans Azure Automation, reportez-vous à l’article [Contrôle d’accès en fonction du rôle dans Azure Automation](automation-role-based-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="48c8c-130">For more information about Role-based Access Control in Azure Automation, refer to [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="48c8c-131">Pour plus d’informations sur les applets de commande PowerShell permettant de gérer votre abonnement, consultez [Utilisation d’Azure PowerShell avec Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="48c8c-131">To learn about PowerShell cmdlets for managing your subscription, see [Using Azure PowerShell with Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md)</span></span>
* <span data-ttu-id="48c8c-132">Pour plus d’informations sur les fonctionnalités du portail permettant de gérer votre abonnement, consultez [Utilisation du Portail Azure pour gérer les ressources](../azure-resource-manager/resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="48c8c-132">To learn about portal features for managing your subscription, see [Using the Azure Portal to manage resources](../azure-resource-manager/resource-group-portal.md).</span></span>
