---
title: "aaaAzure vue d’ensemble de Automation DSC | Documents Microsoft"
description: "Vue d'ensemble de la configuration d'état souhaité (DSC) Azure Automation, les termes s'y rapportant et les problèmes connus"
services: automation
documentationcenter: dev-center-name
author: eslesar
manager: carmonm
keywords: "PowerShell DSC, Desired State Configuration, configuration d'état souhaité PowerShell DSC Azure"
ms.assetid: fd40cb68-c1a6-48c3-bba2-710b607d1555
ms.service: automation
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: TBD
ms.date: 06/15/2017
ms.author: eslesar
ms.openlocfilehash: 5b8e5104c7b5bed848c015ac26a8b7d1f5b24de9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-dsc-overview"></a><span data-ttu-id="d73ab-104">Vue d'ensemble d'Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="d73ab-104">Azure Automation DSC Overview</span></span>

<span data-ttu-id="d73ab-105">Azure Automation DSC est un service Azure qui vous permet de toowrite, de gérer et de compiler la Configuration d’état souhaité (DSC) PowerShell [configurations](https://msdn.microsoft.com/powershell/dsc/configurations), importer [des ressources DSC](https://msdn.microsoft.com/powershell/dsc/resources)et attribuer nœuds tootarget configurations, toutes dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="d73ab-105">Azure Automation DSC is an Azure service that allows you toowrite, manage, and compile PowerShell Desired State Configuration (DSC) [configurations](https://msdn.microsoft.com/powershell/dsc/configurations), import [DSC Resources](https://msdn.microsoft.com/powershell/dsc/resources), and assign configurations tootarget nodes, all in hello cloud.</span></span>

## <a name="why-use-azure-automation-dsc"></a><span data-ttu-id="d73ab-106">Pourquoi utiliser Azure Automation DSC ?</span><span class="sxs-lookup"><span data-stu-id="d73ab-106">Why use Azure Automation DSC</span></span>

<span data-ttu-id="d73ab-107">Azure Automation DSC offre plusieurs avantages par rapport à l’utilisation de DSC en dehors d’Azure.</span><span class="sxs-lookup"><span data-stu-id="d73ab-107">Azure Automation DSC provides several advantages over using DSC outside of Azure.</span></span>

### <a name="built-in-pull-server"></a><span data-ttu-id="d73ab-108">Serveur collecteur intégré</span><span class="sxs-lookup"><span data-stu-id="d73ab-108">Built-in pull server</span></span>

<span data-ttu-id="d73ab-109">Azure Automation fournit un [serveur collecteur DSC](https://msdn.microsoft.com/en-us/powershell/dsc/pullserver) afin que les nœuds cibles reçoivent automatiquement les configurations, conformes toohello souhaité état et rapport sur leur conformité.</span><span class="sxs-lookup"><span data-stu-id="d73ab-109">Azure Automation provides a [DSC pull server](https://msdn.microsoft.com/en-us/powershell/dsc/pullserver) so that target nodes automatically receive configurations, conform toohello desired state, and report back on their compliance.</span></span>
<span data-ttu-id="d73ab-110">serveur d’extraction intégrée Hello dans Azure Automation élimine hello besoin tooset des et gérer votre propre serveur collecteur.</span><span class="sxs-lookup"><span data-stu-id="d73ab-110">hello built-in pull server in Azure Automation eliminates hello need tooset up and maintain your own pull server.</span></span>
<span data-ttu-id="d73ab-111">Azure Automation peut cibler des ordinateurs physiques ou virtuels Windows ou Linux, dans le cloud de hello ou localement.</span><span class="sxs-lookup"><span data-stu-id="d73ab-111">Azure Automation can target virtual or physical Windows or Linux machines, in hello cloud or on-premises.</span></span>

### <a name="management-of-all-your-dsc-artifacts"></a><span data-ttu-id="d73ab-112">Gestion de tous vos artefacts DSC</span><span class="sxs-lookup"><span data-stu-id="d73ab-112">Management of all your DSC artifacts</span></span>

<span data-ttu-id="d73ab-113">Azure Automation DSC met hello même couche de gestion trop[Configuration d’état souhaité PowerShell](https://msdn.microsoft.com/powershell/dsc/overview) Azure Automation offre pour l’écriture de scripts PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d73ab-113">Azure Automation DSC brings hello same management layer too[PowerShell Desired State Configuration](https://msdn.microsoft.com/powershell/dsc/overview) as Azure Automation offers for PowerShell scripting.</span></span>

<span data-ttu-id="d73ab-114">À partir de hello portail Azure, ou à partir de PowerShell, vous pouvez gérer tous vos configurations DSC, les ressources et les nœuds cibles.</span><span class="sxs-lookup"><span data-stu-id="d73ab-114">From hello Azure portal, or from PowerShell, you can manage all your DSC configurations, resources, and target nodes.</span></span>

![Capture d’écran du panneau d’Azure Automation hello](./media/automation-dsc-overview/azure-automation-blade.png)

### <a name="import-reporting-data-into-log-analytics"></a><span data-ttu-id="d73ab-116">Importer des données de création de rapports dans Log Analytics</span><span class="sxs-lookup"><span data-stu-id="d73ab-116">Import reporting data into Log Analytics</span></span>

<span data-ttu-id="d73ab-117">Nœuds qui sont gérées avec Azure Automation DSC envoi détaillées état données toohello intégrées par extraction de données serveur de rapports.</span><span class="sxs-lookup"><span data-stu-id="d73ab-117">Nodes that are managed with Azure Automation DSC send detailed reporting status data toohello built-in pull server.</span></span>
<span data-ttu-id="d73ab-118">Vous pouvez configurer Azure Automation DSC toosend cet espace de travail de données tooyour Analytique de journal de Microsoft Operations Management Suite (OMS).</span><span class="sxs-lookup"><span data-stu-id="d73ab-118">You can configure Azure Automation DSC toosend this data tooyour Microsoft Operations Management Suite (OMS) Log Analytics workspace.</span></span>
<span data-ttu-id="d73ab-119">toolearn tooyour de données d’état toosend DSC espace de travail Analytique des journaux, voir [par progression Azure Automation DSC tooOMS de données Analytique de journal de création de rapports](automation-dsc-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="d73ab-119">toolearn how toosend DSC status data tooyour Log Analytics workspace, see [Forward Azure Automation DSC reporting data tooOMS Log Analytics](automation-dsc-diagnostics.md).</span></span>

## <a name="introduction-video"></a><span data-ttu-id="d73ab-120">Vidéo de présentation</span><span class="sxs-lookup"><span data-stu-id="d73ab-120">Introduction video</span></span>

<span data-ttu-id="d73ab-121">Préférez la surveillance tooreading ?</span><span class="sxs-lookup"><span data-stu-id="d73ab-121">Prefer watching tooreading?</span></span> <span data-ttu-id="d73ab-122">Jetez un œil sur hello suivant vidéo à partir de mai 2015, quand Azure Automation DSC a été annoncée.</span><span class="sxs-lookup"><span data-stu-id="d73ab-122">Have a look at hello following video from May 2015, when Azure Automation DSC was first announced.</span></span>

>[!NOTE]
><span data-ttu-id="d73ab-123">Alors que les concepts de hello et cycle de vie présentés dans cette vidéo sont corrects, Azure Automation DSC a beaucoup progressé depuis cette vidéo a été enregistrée.</span><span class="sxs-lookup"><span data-stu-id="d73ab-123">While hello concepts and life cycle discussed in this video are correct, Azure Automation DSC has progressed a lot since this video was recorded.</span></span>
><span data-ttu-id="d73ab-124">Il est désormais généralement disponible, a une interface utilisateur beaucoup plus étendue Bonjour portail Azure et prend en charge de nombreuses fonctions supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="d73ab-124">It is now generally available, has a much more extensive UI in hello Azure portal, and supports many additional capabilities.</span></span>

> [!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3467/player]

## <a name="next-steps"></a><span data-ttu-id="d73ab-125">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d73ab-125">Next steps</span></span>

* <span data-ttu-id="d73ab-126">toolearn tooonboard nœuds toobe gérés dans Azure Automation DSC, voir [d’intégration des ordinateurs pour la gestion par Azure Automation DSC](automation-dsc-onboarding.md)</span><span class="sxs-lookup"><span data-stu-id="d73ab-126">toolearn how tooonboard nodes toobe managed with Azure Automation DSC, see [Onboarding machines for management by Azure Automation DSC](automation-dsc-onboarding.md)</span></span>
* <span data-ttu-id="d73ab-127">tooget démarré à l’aide d’Azure Automation DSC, consultez [prise en main d’Azure Automation DSC](automation-dsc-getting-started.md)</span><span class="sxs-lookup"><span data-stu-id="d73ab-127">tooget started using Azure Automation DSC, see [Getting started with Azure Automation DSC](automation-dsc-getting-started.md)</span></span>
* <span data-ttu-id="d73ab-128">toolearn sur la compilation des configurations DSC afin que vous pouvez les affecter tootarget nœuds, consultez [la compilation des configurations dans Azure Automation DSC](automation-dsc-compile.md)</span><span class="sxs-lookup"><span data-stu-id="d73ab-128">toolearn about compiling DSC configurations so that you can assign them tootarget nodes, see [Compiling configurations in Azure Automation DSC](automation-dsc-compile.md)</span></span>
* <span data-ttu-id="d73ab-129">Pour la référence de cmdlet PowerShell pour Azure Automation DSC, consultez [AzureRM.Automation](/powershell/module/azurerm.automation/#automation).</span><span class="sxs-lookup"><span data-stu-id="d73ab-129">For PowerShell cmdlet reference for Azure Automation DSC, see [Azure Automation DSC cmdlets](/powershell/module/azurerm.automation/#automation)</span></span>
* <span data-ttu-id="d73ab-130">Pour plus d’informations sur la tarification, consultez [Tarification de Automation](https://azure.microsoft.com/pricing/details/automation/).</span><span class="sxs-lookup"><span data-stu-id="d73ab-130">For pricing information, see [Azure Automation DSC pricing](https://azure.microsoft.com/pricing/details/automation/)</span></span>
* <span data-ttu-id="d73ab-131">toosee un exemple d’utilisation d’Azure Automation DSC dans un pipeline de déploiement continu, consultez [tooIaaS déploiement continu Chocolatey et les machines virtuelles à l’aide de Azure Automation DSC](automation-dsc-cd-chocolatey.md)</span><span class="sxs-lookup"><span data-stu-id="d73ab-131">toosee an example of using Azure Automation DSC in a continuous deployment pipeline, see  [Continuous Deployment tooIaaS VMs Using Azure Automation DSC and Chocolatey](automation-dsc-cd-chocolatey.md)</span></span>
