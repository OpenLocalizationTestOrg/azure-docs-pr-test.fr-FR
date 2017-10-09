---
title: aaaUpdate Azure modules dans Azure Automation | Documents Microsoft
description: "Cet article décrit comment vous pouvez désormais mettre à jour les modules Azure PowerShell courants fournis par défaut dans Azure Automation."
services: automation
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: tysonn
ms.assetid: 
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/13/2017
ms.author: magoedte
ms.openlocfilehash: afa404a643349f044e55be2280e435b575049dec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooupdate-azure-powershell-modules-in-azure-automation"></a><span data-ttu-id="725de-103">Comment les modules Azure PowerShell tooupdate dans Azure Automation</span><span class="sxs-lookup"><span data-stu-id="725de-103">How tooupdate Azure PowerShell modules in Azure Automation</span></span>

<span data-ttu-id="725de-104">les modules Azure PowerShell courants Hello sont fournis par défaut dans chaque compte Automation.</span><span class="sxs-lookup"><span data-stu-id="725de-104">hello most common Azure PowerShell modules are provided by default in each Automation account.</span></span>  <span data-ttu-id="725de-105">mises à jour de l’équipe Azure Hello hello régulièrement, les modules Azure afin de hello compte Automation nous fournissent un moyen de vous tooupdate des modules de hello dans le compte de hello lorsque de nouvelles versions sont disponibles à partir du portail de hello.</span><span class="sxs-lookup"><span data-stu-id="725de-105">hello Azure team updates hello Azure modules regularly, so in hello Automation account we provide a way for you tooupdate hello modules in hello account when new versions are available from hello portal.</span></span>  

<span data-ttu-id="725de-106">Étant donné que les modules sont régulièrement mises à jour par groupe de produits hello, les modifications peuvent se produire avec les applets de commande hello inclus, ce qui peut affecter les vos procédures opérationnelles en fonction de type hello de modification, telles que la modification du nom d’un paramètre ou l’obsolescence d’une applet de commande entièrement.</span><span class="sxs-lookup"><span data-stu-id="725de-106">Because modules are updated regularly by hello product group, changes can occur with hello  included cmdlets, which may negatively impact your runbooks depending on hello type of change, such as renaming a parameter or deprecating a cmdlet entirely.</span></span> <span data-ttu-id="725de-107">tooavoid ayant un impact sur les procédures opérationnelles hello automatisent les processus qu’ils, il est fortement recommandé de tester et valider avant de continuer.</span><span class="sxs-lookup"><span data-stu-id="725de-107">tooavoid impacting your runbooks and hello processes they automate, it is strongly recommended that you test and validate before proceeding.</span></span>  <span data-ttu-id="725de-108">Si vous n’avez pas un compte Automation dédié conçu à cet effet, envisagez de créer une afin que vous pouvez tester les nombreux différents scénarios et les permutations pendant le développement hello de vos runbook, des modifications de tooiterative Ajout telles que la mise à jour de hello Modules PowerShell.</span><span class="sxs-lookup"><span data-stu-id="725de-108">If you do not have a dedicated Automation account intended for this purpose, consider creating one so that you can test many different scenarios and permutations during hello development of your runbooks, in addition tooiterative changes such as updating hello PowerShell modules.</span></span>  <span data-ttu-id="725de-109">Une fois les résultats hello sont validées et que vous avez appliqué les modifications nécessaires, poursuivre la coordination de la migration de tous les runbooks qui exigeait que hello et effectuer la mise à jour de l’hello comme décrit dans la production.</span><span class="sxs-lookup"><span data-stu-id="725de-109">After hello results are validated and you have applied any changes required, proceed with coordinating hello migration of any runbooks that required modification and perform hello update as described below in production.</span></span>     

## <a name="updating-azure-modules"></a><span data-ttu-id="725de-110">Mise à jour de modules Azure</span><span class="sxs-lookup"><span data-stu-id="725de-110">Updating Azure Modules</span></span>

1. <span data-ttu-id="725de-111">Dans les Modules hello Panneau de votre compte Automation il existe une option appelée **mise à jour les Modules Azure**.</span><span class="sxs-lookup"><span data-stu-id="725de-111">In hello Modules blade of your Automation account there is an option called **Update Azure Modules**.</span></span>  <span data-ttu-id="725de-112">Elle est toujours activée.</span><span class="sxs-lookup"><span data-stu-id="725de-112">It is always enabled.</span></span><br><br> <span data-ttu-id="725de-113">![Option de mise à jour de modules Azure dans le panneau Modules](media/automation-update-azure-modules/automation-update-azure-modules-option.png)</span><span class="sxs-lookup"><span data-stu-id="725de-113">![Update Azure Modules option in Modules blade](media/automation-update-azure-modules/automation-update-azure-modules-option.png)</span></span>

2. <span data-ttu-id="725de-114">Cliquez sur **mise à jour Azure Modules** et vous verrez un message de confirmation qui vous demande si vous voulez toocontinue.</span><span class="sxs-lookup"><span data-stu-id="725de-114">Click **Update Azure Modules** and you will be presented with a confirmation notification that asks you if you want toocontinue.</span></span><br><br> <span data-ttu-id="725de-115">![Notification de mise à jour des modules Azure](media/automation-update-azure-modules/automation-update-azure-modules-popup.png)</span><span class="sxs-lookup"><span data-stu-id="725de-115">![Update Azure Modules notification](media/automation-update-azure-modules/automation-update-azure-modules-popup.png)</span></span>

3. <span data-ttu-id="725de-116">Cliquez sur **Oui** et processus de mise à jour de module hello commence.</span><span class="sxs-lookup"><span data-stu-id="725de-116">Click **Yes** and hello module update process will begin.</span></span>  <span data-ttu-id="725de-117">processus de mise à jour Hello prend environ hello tooupdate de 15 à 20 minutes suivant des modules :</span><span class="sxs-lookup"><span data-stu-id="725de-117">hello update process takes about 15-20 minutes tooupdate hello following modules:</span></span>

  * <span data-ttu-id="725de-118">Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="725de-118">Azure</span></span>
  * <span data-ttu-id="725de-119">Azure.Storage</span><span class="sxs-lookup"><span data-stu-id="725de-119">Azure.Storage</span></span>
  * <span data-ttu-id="725de-120">AzureRm.Automation</span><span class="sxs-lookup"><span data-stu-id="725de-120">AzureRm.Automation</span></span>
  * <span data-ttu-id="725de-121">AzureRm.Compute</span><span class="sxs-lookup"><span data-stu-id="725de-121">AzureRm.Compute</span></span>
  * <span data-ttu-id="725de-122">AzureRm.Profile</span><span class="sxs-lookup"><span data-stu-id="725de-122">AzureRm.Profile</span></span>
  * <span data-ttu-id="725de-123">AzureRm.Resources</span><span class="sxs-lookup"><span data-stu-id="725de-123">AzureRm.Resources</span></span>
  * <span data-ttu-id="725de-124">AzureRm.Sql</span><span class="sxs-lookup"><span data-stu-id="725de-124">AzureRm.Sql</span></span>
  * <span data-ttu-id="725de-125">AzureRm.Storage</span><span class="sxs-lookup"><span data-stu-id="725de-125">AzureRm.Storage</span></span>

    <span data-ttu-id="725de-126">Si les modules hello sont déjà toodate, processus de hello s’achève en quelques secondes.</span><span class="sxs-lookup"><span data-stu-id="725de-126">If hello modules are already up toodate, then hello process will complete in a few seconds.</span></span>  <span data-ttu-id="725de-127">Vous serez averti une fois hello mise à jour terminée.</span><span class="sxs-lookup"><span data-stu-id="725de-127">When hello update process completes you will be notified.</span></span><br><br> ![Mise à jour d’état de mise à jour des modules Azure](media/automation-update-azure-modules/automation-update-azure-modules-updatestatus.png)

> [!NOTE]
> <span data-ttu-id="725de-129">Azure Automation utilise les modules dernière hello dans votre compte Automation lors de l’exécution d’une tâche planifiée.</span><span class="sxs-lookup"><span data-stu-id="725de-129">Azure Automation will use hello latest modules in your Automation account when a new scheduled job is run.</span></span>    

<span data-ttu-id="725de-130">Si vous utilisez les applets de commande à partir de ces modules Azure PowerShell dans votre toomanage runbooks Azure ressources, il convient alors tooperform ce processus de mise à jour tous les mois ou donc tooassure que vous avez hello modules plus récente.</span><span class="sxs-lookup"><span data-stu-id="725de-130">If you use cmdlets from these Azure PowerShell modules in your runbooks toomanage Azure resources, then you will want tooperform this update process every month or so tooassure that you have hello latest modules.</span></span>

## <a name="next-steps"></a><span data-ttu-id="725de-131">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="725de-131">Next steps</span></span>

* <span data-ttu-id="725de-132">toolearn en savoir plus sur les Modules d’intégration et comment toofurther de modules personnalisés toocreate intégrer Automation avec d’autres systèmes, les services ou les solutions, consultez [Modules d’intégration](automation-integration-modules.md).</span><span class="sxs-lookup"><span data-stu-id="725de-132">toolearn more about Integration Modules and how toocreate custom modules toofurther integrate Automation with other systems, services, or solutions, see [Integration Modules](automation-integration-modules.md).</span></span>

* <span data-ttu-id="725de-133">Envisagez d’intégration de contrôle de code source à l’aide [GitHub Enterprise](automation-scenario-source-control-integration-with-github-ent.md) ou [Visual Studio Team Services](automation-scenario-source-control-integration-with-vsts.md) toocentrally gérer et contrôler les versions de votre portefeuille de configuration et de runbook Automation.</span><span class="sxs-lookup"><span data-stu-id="725de-133">Consider source control integration using [GitHub Enterprise](automation-scenario-source-control-integration-with-github-ent.md) or [Visual Studio Team Services](automation-scenario-source-control-integration-with-vsts.md) toocentrally manage and control releases of your Automation runbook and configuration portfolio.</span></span>  
