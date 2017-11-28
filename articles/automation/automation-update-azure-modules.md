---
title: "Mise à jour de modules Azure dans Azure Automation | Microsoft Docs"
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
ms.openlocfilehash: ed8c97b642d406a05817ec6c67f31a1b4bce93b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-update-azure-powershell-modules-in-azure-automation"></a><span data-ttu-id="c680b-103">Guide de mise à jour des modules Azure PowerShell dans Azure Automation</span><span class="sxs-lookup"><span data-stu-id="c680b-103">How to update Azure PowerShell modules in Azure Automation</span></span>

<span data-ttu-id="c680b-104">Les modules Azure PowerShell courants sont fournis par défaut dans chaque compte Automation.</span><span class="sxs-lookup"><span data-stu-id="c680b-104">The most common Azure PowerShell modules are provided by default in each Automation account.</span></span>  <span data-ttu-id="c680b-105">L’équipe Azure met à jour régulièrement les modules Azure. Nous fournissons donc dans le compte Automation une méthode permettant de mettre à jour les modules dans le compte lorsque de nouvelles versions sont disponibles dans le portail.</span><span class="sxs-lookup"><span data-stu-id="c680b-105">The Azure team updates the Azure modules regularly, so in the Automation account we provide a way for you to update the modules in the account when new versions are available from the portal.</span></span>  

<span data-ttu-id="c680b-106">Étant donné que les modules sont régulièrement mis à jour par le groupe de produits, les modifications peuvent se produire avec les cmdlets inclus. Cela peut avoir un impact négatif sur vos runbooks suivant le type de modification, comme renommer un paramètre ou désapprouver entièrement un cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c680b-106">Because modules are updated regularly by the product group, changes can occur with the  included cmdlets, which may negatively impact your runbooks depending on the type of change, such as renaming a parameter or deprecating a cmdlet entirely.</span></span> <span data-ttu-id="c680b-107">Pour éviter toute incidence sur vos runbooks ainsi que les processus qu’ils automatisent, il est fortement conseillé de tester et valider les mises à jour avant de les appliquer.</span><span class="sxs-lookup"><span data-stu-id="c680b-107">To avoid impacting your runbooks and the processes they automate, it is strongly recommended that you test and validate before proceeding.</span></span>  <span data-ttu-id="c680b-108">Si vous ne possédez pas de compte Automation dédié destiné à cet usage, pensez à en créer un. Vous pourrez tester de nombreux scénarios et différentes permutations lors du développement de vos runbooks, en plus des modifications répétitives comme la mise à jour des modules PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c680b-108">If you do not have a dedicated Automation account intended for this purpose, consider creating one so that you can test many different scenarios and permutations during the development of your runbooks, in addition to iterative changes such as updating the PowerShell modules.</span></span>  <span data-ttu-id="c680b-109">Dès que les résultats sont validés et une fois que vous avez appliqué les modifications requises, passez à la coordination de la migration de tout runbook nécessitant une modification, puis réalisez la mise à jour comme décrit ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="c680b-109">After the results are validated and you have applied any changes required, proceed with coordinating the migration of any runbooks that required modification and perform the update as described below in production.</span></span>     

## <a name="updating-azure-modules"></a><span data-ttu-id="c680b-110">Mise à jour de modules Azure</span><span class="sxs-lookup"><span data-stu-id="c680b-110">Updating Azure Modules</span></span>

1. <span data-ttu-id="c680b-111">Le panneau Modules de votre compte Automation comprend une option de **mise à jour des modules Azure**.</span><span class="sxs-lookup"><span data-stu-id="c680b-111">In the Modules blade of your Automation account there is an option called **Update Azure Modules**.</span></span>  <span data-ttu-id="c680b-112">Elle est toujours activée.</span><span class="sxs-lookup"><span data-stu-id="c680b-112">It is always enabled.</span></span><br><br> <span data-ttu-id="c680b-113">![Option de mise à jour de modules Azure dans le panneau Modules](media/automation-update-azure-modules/automation-update-azure-modules-option.png)</span><span class="sxs-lookup"><span data-stu-id="c680b-113">![Update Azure Modules option in Modules blade](media/automation-update-azure-modules/automation-update-azure-modules-option.png)</span></span>

2. <span data-ttu-id="c680b-114">Cliquez sur **Mettre à jour les modules Azure** et un message de confirmation s’affichera vous demandant si vous souhaitez continuer.</span><span class="sxs-lookup"><span data-stu-id="c680b-114">Click **Update Azure Modules** and you will be presented with a confirmation notification that asks you if you want to continue.</span></span><br><br> <span data-ttu-id="c680b-115">![Notification de mise à jour des modules Azure](media/automation-update-azure-modules/automation-update-azure-modules-popup.png)</span><span class="sxs-lookup"><span data-stu-id="c680b-115">![Update Azure Modules notification](media/automation-update-azure-modules/automation-update-azure-modules-popup.png)</span></span>

3. <span data-ttu-id="c680b-116">Cliquez sur **Oui** et le processus de mise à jour du module commence.</span><span class="sxs-lookup"><span data-stu-id="c680b-116">Click **Yes** and the module update process will begin.</span></span>  <span data-ttu-id="c680b-117">Le processus de mise à jour prend environ 15 à 20 minutes pour les modules suivants :</span><span class="sxs-lookup"><span data-stu-id="c680b-117">The update process takes about 15-20 minutes to update the following modules:</span></span>

  * <span data-ttu-id="c680b-118">Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="c680b-118">Azure</span></span>
  * <span data-ttu-id="c680b-119">Azure.Storage</span><span class="sxs-lookup"><span data-stu-id="c680b-119">Azure.Storage</span></span>
  * <span data-ttu-id="c680b-120">AzureRm.Automation</span><span class="sxs-lookup"><span data-stu-id="c680b-120">AzureRm.Automation</span></span>
  * <span data-ttu-id="c680b-121">AzureRm.Compute</span><span class="sxs-lookup"><span data-stu-id="c680b-121">AzureRm.Compute</span></span>
  * <span data-ttu-id="c680b-122">AzureRm.Profile</span><span class="sxs-lookup"><span data-stu-id="c680b-122">AzureRm.Profile</span></span>
  * <span data-ttu-id="c680b-123">AzureRm.Resources</span><span class="sxs-lookup"><span data-stu-id="c680b-123">AzureRm.Resources</span></span>
  * <span data-ttu-id="c680b-124">AzureRm.Sql</span><span class="sxs-lookup"><span data-stu-id="c680b-124">AzureRm.Sql</span></span>
  * <span data-ttu-id="c680b-125">AzureRm.Storage</span><span class="sxs-lookup"><span data-stu-id="c680b-125">AzureRm.Storage</span></span>

    <span data-ttu-id="c680b-126">Si les modules sont déjà à jour, le processus se termine en quelques secondes.</span><span class="sxs-lookup"><span data-stu-id="c680b-126">If the modules are already up to date, then the process will complete in a few seconds.</span></span>  <span data-ttu-id="c680b-127">Vous serez averti lorsque le processus de mise à jour sera terminé.</span><span class="sxs-lookup"><span data-stu-id="c680b-127">When the update process completes you will be notified.</span></span><br><br> ![Mise à jour d’état de mise à jour des modules Azure](media/automation-update-azure-modules/automation-update-azure-modules-updatestatus.png)

> [!NOTE]
> <span data-ttu-id="c680b-129">Azure Automation utilisera les derniers modules de votre compte Automation lors de l’exécution d’un nouveau travail planifié.</span><span class="sxs-lookup"><span data-stu-id="c680b-129">Azure Automation will use the latest modules in your Automation account when a new scheduled job is run.</span></span>    

<span data-ttu-id="c680b-130">Si vous utilisez des applets de commande à partir de ces modules Azure PowerShell dans des runbooks pour gérer des ressources Azure, vous devez effectuer cette mise à jour chaque mois pour vous assurer que vous avez les derniers modules.</span><span class="sxs-lookup"><span data-stu-id="c680b-130">If you use cmdlets from these Azure PowerShell modules in your runbooks to manage Azure resources, then you will want to perform this update process every month or so to assure that you have the latest modules.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c680b-131">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c680b-131">Next steps</span></span>

* <span data-ttu-id="c680b-132">Pour plus d’informations sur les modules d’intégration et la création de modules personnalisés pour intégrer Automation dans d’autres systèmes, services ou solutions, consultez [Modules d’intégration](automation-integration-modules.md).</span><span class="sxs-lookup"><span data-stu-id="c680b-132">To learn more about Integration Modules and how to create custom modules to further integrate Automation with other systems, services, or solutions, see [Integration Modules](automation-integration-modules.md).</span></span>

* <span data-ttu-id="c680b-133">Envisagez d’intégrer un contrôle de code source à l’aide de [GitHub Enterprise](automation-scenario-source-control-integration-with-github-ent.md) ou de [Visual Studio Team Services](automation-scenario-source-control-integration-with-vsts.md). Vous pourrez gérer et contrôler votre runbook Automation et votre portefeuille de configuration de manière centralisée.</span><span class="sxs-lookup"><span data-stu-id="c680b-133">Consider source control integration using [GitHub Enterprise](automation-scenario-source-control-integration-with-github-ent.md) or [Visual Studio Team Services](automation-scenario-source-control-integration-with-vsts.md) to centrally manage and control releases of your Automation runbook and configuration portfolio.</span></span>  