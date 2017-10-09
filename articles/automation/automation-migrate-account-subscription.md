---
title: aaaMigrate compte Automation et ressources | Documents Microsoft
description: "Cet article décrit comment toomove une automatisation de compte dans Azure Automation et les ressources associées à partir d’un seul abonnement tooanother."
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
ms.openlocfilehash: 201c9091cd2d78d7ea407c1e5fb27f366bb4fa8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-automation-account-and-resources"></a><span data-ttu-id="fd3e7-103">Migration d’un compte et de ressources Automation</span><span class="sxs-lookup"><span data-stu-id="fd3e7-103">Migrate Automation Account and resources</span></span>
<span data-ttu-id="fd3e7-104">Pour les comptes Automation et les ressources associées (c'est-à-dire actifs, runbooks, modules, etc.) que vous avez créé dans hello portail Azure et souhaitez toomigrate à partir d’une ressource de groupe tooanother ou à partir d’un seul abonnement tooanother, vous pouvez faire cela facilement avec Hello [déplacer des ressources](../azure-resource-manager/resource-group-move-resources.md) fonctionnalité disponible dans hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="fd3e7-104">For Automation accounts and its associated resources (i.e. assets, runbooks, modules, etc.) that you have created in hello Azure portal and want toomigrate from one resource group tooanother or from one subscription tooanother, you can accomplish this easily with hello [move resources](../azure-resource-manager/resource-group-move-resources.md) feature available in hello Azure portal.</span></span> <span data-ttu-id="fd3e7-105">Toutefois, avant de procéder à cette action, vous devez tout d’abord examiner suivant de hello [liste de vérification avant le déplacement de ressources](../azure-resource-manager/resource-group-move-resources.md#checklist-before-moving-resources) et en outre, hello liste ci-dessous tooAutomation spécifique.</span><span class="sxs-lookup"><span data-stu-id="fd3e7-105">However, before proceeding with this action, you should first review hello following [checklist before moving resources](../azure-resource-manager/resource-group-move-resources.md#checklist-before-moving-resources) and additionally, hello list below specific tooAutomation.</span></span>   

1. <span data-ttu-id="fd3e7-106">groupe de ressource d’abonnement de destination Hello doit être dans la même région que la source de hello.</span><span class="sxs-lookup"><span data-stu-id="fd3e7-106">hello destination subscription/resource group must be in same region as hello source.</span></span>  <span data-ttu-id="fd3e7-107">Cela signifie que les comptes Automation ne peuvent pas être déplacés entre des régions.</span><span class="sxs-lookup"><span data-stu-id="fd3e7-107">Meaning, Automation accounts cannot be moved across regions.</span></span>
2. <span data-ttu-id="fd3e7-108">Lors du déplacement des ressources (par exemple, les procédures opérationnelles, travaux, etc.), les groupes de source de hello et hello cible sont verrouillées pendant l’opération de hello hello.</span><span class="sxs-lookup"><span data-stu-id="fd3e7-108">When moving resources (e.g. runbooks, jobs, etc.), both hello source group and hello target group are locked for hello duration of hello operation.</span></span> <span data-ttu-id="fd3e7-109">Écriture et suppression des opérations sont bloquées sur les groupes de hello jusqu'à ce que le déplacement de hello se termine.</span><span class="sxs-lookup"><span data-stu-id="fd3e7-109">Write and delete operations are blocked on hello groups until hello move completes.</span></span>  
3. <span data-ttu-id="fd3e7-110">Les runbooks et les variables qui font référence à un ID de ressource ou d’un abonnement à partir de l’abonnement existant de hello devez toobe mis à jour après que la migration est terminée.</span><span class="sxs-lookup"><span data-stu-id="fd3e7-110">Any runbooks or variables which reference a resource or subscription ID from hello existing subscription will need toobe updated after migration is completed.</span></span>   

> [!NOTE]
> <span data-ttu-id="fd3e7-111">Cette fonctionnalité ne prend pas en charge les ressources Automation classiques.</span><span class="sxs-lookup"><span data-stu-id="fd3e7-111">This feature does not support moving Classic automation resources.</span></span>
>
>

## <a name="toomove-hello-automation-account-using-hello-portal"></a><span data-ttu-id="fd3e7-112">toomove hello compte Automation à l’aide du portail de hello</span><span class="sxs-lookup"><span data-stu-id="fd3e7-112">toomove hello Automation Account using hello portal</span></span>
1. <span data-ttu-id="fd3e7-113">À partir de votre compte Automation, cliquez sur **déplacer** haut hello du Panneau de hello.</span><span class="sxs-lookup"><span data-stu-id="fd3e7-113">From your Automation account, click **Move** at hello top of hello blade.</span></span><br> <span data-ttu-id="fd3e7-114">![option Déplacer](media/automation-migrate-account-subscription/automation-menu-move.png)</span><span class="sxs-lookup"><span data-stu-id="fd3e7-114">![Move option](media/automation-migrate-account-subscription/automation-menu-move.png)</span></span><br>
2. <span data-ttu-id="fd3e7-115">Sur hello **déplacer des ressources** panneau, notez qu’il présente tooboth connexes des ressources de votre compte Automation et vos groupes de ressources.</span><span class="sxs-lookup"><span data-stu-id="fd3e7-115">On hello **Move resources** blade, note that it presents resources related tooboth your Automation account and your resource group(s).</span></span>  <span data-ttu-id="fd3e7-116">Sélectionnez hello **abonnement** et **groupe de ressources** à partir des listes déroulantes de hello ou sélectionnez hello option **créer un groupe de ressources** et entrez un nouveau nom de groupe de ressources dans champ Hello fourni.</span><span class="sxs-lookup"><span data-stu-id="fd3e7-116">Select hello **subscription** and **resource group** from hello drop-down lists, or select hello option **create a new resource group** and enter a new resource group name in hello field provided.</span></span>  
3. <span data-ttu-id="fd3e7-117">Passez en revue et sélectionnez hello case à cocher tooacknowledge vous *comprendre les outils et scripts sera nécessaire toobe mis à jour toouse nouveaux ID de ressource après le déplacement de ressources* puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="fd3e7-117">Review and select hello checkbox tooacknowledge you *understand tools and scripts will need toobe updated toouse new resource IDs after resources have been moved* and then click **OK**.</span></span><br> <span data-ttu-id="fd3e7-118">![panneau Déplacer des ressources](media/automation-migrate-account-subscription/automation-move-resources-blade.png)</span><span class="sxs-lookup"><span data-stu-id="fd3e7-118">![Move Resources Blade](media/automation-migrate-account-subscription/automation-move-resources-blade.png)</span></span><br>   

<span data-ttu-id="fd3e7-119">Cette action prendra plusieurs minutes toocomplete.</span><span class="sxs-lookup"><span data-stu-id="fd3e7-119">This action will take several minutes toocomplete.</span></span>  <span data-ttu-id="fd3e7-120">Le panneau **Notifications**affiche l’état de chaque action effectuée : validation, migration, puis confirmation que l’opération est terminée.</span><span class="sxs-lookup"><span data-stu-id="fd3e7-120">In **Notifications**, you will be presented with a status of each action that takes place - validation, migration, and then finally when it is completed.</span></span>     

## <a name="toomove-hello-automation-account-using-powershell"></a><span data-ttu-id="fd3e7-121">toomove hello compte Automation à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="fd3e7-121">toomove hello Automation Account using PowerShell</span></span>
<span data-ttu-id="fd3e7-122">toomove existant abonnement, utilisez hello ou groupe de ressources Automation ressources tooanother **Get-AzureRmResource** compte Automation spécifique d’applet de commande tooget hello, puis **Move-AzureRmResource** déplacement de l’applet de commande tooperform hello.</span><span class="sxs-lookup"><span data-stu-id="fd3e7-122">toomove existing Automation resources tooanother resource group or subscription, use hello  **Get-AzureRmResource** cmdlet tooget hello specific Automation account and then **Move-AzureRmResource** cmdlet tooperform hello move.</span></span>

<span data-ttu-id="fd3e7-123">Hello premier exemple montre comment toomove une automatisation compte tooa nouveau groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="fd3e7-123">hello first example shows how toomove an Automation account tooa new resource group.</span></span>

   ```
    $resource = Get-AzureRmResource -ResourceName "TestAutomationAccount" -ResourceGroupName "ResourceGroup01"
    Move-AzureRmResource -ResourceId $resource.ResourceId -DestinationResourceGroupName "NewResourceGroup"
   ```

<span data-ttu-id="fd3e7-124">Après avoir exécuté hello, exemple de code ci-dessus, vous serez invité à tooverify vous voulez que tooperform cette action.</span><span class="sxs-lookup"><span data-stu-id="fd3e7-124">After you execute hello above code example, you will be prompted tooverify you want tooperform this action.</span></span>  <span data-ttu-id="fd3e7-125">Une fois que vous cliquez sur **Oui** et autoriser hello tooproceed de script, vous ne recevrez pas de notifications pendant qu’il effectue la migration hello.</span><span class="sxs-lookup"><span data-stu-id="fd3e7-125">Once you click **Yes** and allow hello script tooproceed, you will not receive any notifications while it's performing hello migration.</span></span>  

<span data-ttu-id="fd3e7-126">toomove tooa nouvel abonnement, incluez une valeur pour hello *DestinationSubscriptionId* paramètre.</span><span class="sxs-lookup"><span data-stu-id="fd3e7-126">toomove tooa new subscription, include a value for hello *DestinationSubscriptionId* parameter.</span></span>

   ```
    $resource = Get-AzureRmResource -ResourceName "TestAutomationAccount" -ResourceGroupName "ResourceGroup01"
    Move-AzureRmResource -ResourceId $resource.ResourceId -DestinationResourceGroupName "NewResourceGroup" -DestinationSubscriptionId "SubscriptionId"
   ```

<span data-ttu-id="fd3e7-127">Comme avec l’exemple précédent de hello, vous serez invité à tooconfirm hello move.</span><span class="sxs-lookup"><span data-stu-id="fd3e7-127">As with hello previous example, you will be prompted tooconfirm hello move.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="fd3e7-128">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="fd3e7-128">Next steps</span></span>
* <span data-ttu-id="fd3e7-129">Pour plus d’informations sur le groupe de ressources toonew ressources mobile ou d’un abonnement, consultez [déplacer le groupe de ressources toonew ressources ou d’un abonnement](../azure-resource-manager/resource-group-move-resources.md)</span><span class="sxs-lookup"><span data-stu-id="fd3e7-129">For more information about moving resources toonew resource group or subscription, see [Move  resources toonew resource group or subscription](../azure-resource-manager/resource-group-move-resources.md)</span></span>
* <span data-ttu-id="fd3e7-130">Pour plus d’informations sur le contrôle d’accès basée sur les rôles dans Azure Automation, consultez trop[contrôle d’accès basé sur un rôle dans Azure Automation](automation-role-based-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="fd3e7-130">For more information about Role-based Access Control in Azure Automation, refer too[Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="fd3e7-131">toolearn sur les applets de commande PowerShell pour gérer votre abonnement, consultez [à l’aide de Azure PowerShell avec le Gestionnaire de ressources](../azure-resource-manager/powershell-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="fd3e7-131">toolearn about PowerShell cmdlets for managing your subscription, see [Using Azure PowerShell with Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md)</span></span>
* <span data-ttu-id="fd3e7-132">toolearn sur les fonctionnalités du portail de gestion de votre abonnement, consultez [à l’aide des ressources de toomanage portail Azure hello](../azure-resource-manager/resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="fd3e7-132">toolearn about portal features for managing your subscription, see [Using hello Azure Portal toomanage resources](../azure-resource-manager/resource-group-portal.md).</span></span>
