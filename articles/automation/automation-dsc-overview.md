---
title: "Vue d’ensemble d’Azure Automation DSC | Microsoft Docs"
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
ms.openlocfilehash: 468321fa6863d78bc0d179fbe5c2ed6195040d50
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-automation-dsc-overview"></a><span data-ttu-id="4d412-104">Vue d'ensemble d'Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="4d412-104">Azure Automation DSC Overview</span></span>

<span data-ttu-id="4d412-105">Azure Automation DSC est un service Azure qui vous permet d’écrire, de gérer et de compiler les [configurations](https://msdn.microsoft.com/powershell/dsc/configurations) PowerShell DSC, d’importer des [ressources DSC](https://msdn.microsoft.com/powershell/dsc/resources) et d’assigner des configurations aux nœuds cibles, le tout dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="4d412-105">Azure Automation DSC is an Azure service that allows you to write, manage, and compile PowerShell Desired State Configuration (DSC) [configurations](https://msdn.microsoft.com/powershell/dsc/configurations), import [DSC Resources](https://msdn.microsoft.com/powershell/dsc/resources), and assign configurations to target nodes, all in the cloud.</span></span>

## <a name="why-use-azure-automation-dsc"></a><span data-ttu-id="4d412-106">Pourquoi utiliser Azure Automation DSC ?</span><span class="sxs-lookup"><span data-stu-id="4d412-106">Why use Azure Automation DSC</span></span>

<span data-ttu-id="4d412-107">Azure Automation DSC offre plusieurs avantages par rapport à l’utilisation de DSC en dehors d’Azure.</span><span class="sxs-lookup"><span data-stu-id="4d412-107">Azure Automation DSC provides several advantages over using DSC outside of Azure.</span></span>

### <a name="built-in-pull-server"></a><span data-ttu-id="4d412-108">Serveur collecteur intégré</span><span class="sxs-lookup"><span data-stu-id="4d412-108">Built-in pull server</span></span>

<span data-ttu-id="4d412-109">Azure Automation fournit un [serveur collecteur DSC](https://msdn.microsoft.com/en-us/powershell/dsc/pullserver) afin que les nœuds cibles reçoivent automatiquement les configurations, soient conformes à l’état souhaité et renvoient un rapport attestant de leur conformité.</span><span class="sxs-lookup"><span data-stu-id="4d412-109">Azure Automation provides a [DSC pull server](https://msdn.microsoft.com/en-us/powershell/dsc/pullserver) so that target nodes automatically receive configurations, conform to the desired state, and report back on their compliance.</span></span>
<span data-ttu-id="4d412-110">Le serveur collecteur intégré dans Azure Automation vous permet d’éviter d’avoir à configurer et à gérer votre propre serveur collecteur.</span><span class="sxs-lookup"><span data-stu-id="4d412-110">The built-in pull server in Azure Automation eliminates the need to set up and maintain your own pull server.</span></span>
<span data-ttu-id="4d412-111">Azure Automation peut cibler des machines physiques ou virtuelles Windows ou Linux, dans le cloud ou en local.</span><span class="sxs-lookup"><span data-stu-id="4d412-111">Azure Automation can target virtual or physical Windows or Linux machines, in the cloud or on-premises.</span></span>

### <a name="management-of-all-your-dsc-artifacts"></a><span data-ttu-id="4d412-112">Gestion de tous vos artefacts DSC</span><span class="sxs-lookup"><span data-stu-id="4d412-112">Management of all your DSC artifacts</span></span>

<span data-ttu-id="4d412-113">Azure Automation DSC apporte la même couche de gestion à la [configuration d’état souhaité PowerShell](https://msdn.microsoft.com/powershell/dsc/overview) que celle proposée par Azure Automation pour l’écriture de scripts PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4d412-113">Azure Automation DSC brings the same management layer to [PowerShell Desired State Configuration](https://msdn.microsoft.com/powershell/dsc/overview) as Azure Automation offers for PowerShell scripting.</span></span>

<span data-ttu-id="4d412-114">À partir du portail Azure, ou de PowerShell, vous pouvez gérer toutes vos configurations DSC, vos ressources et vos nœuds cibles.</span><span class="sxs-lookup"><span data-stu-id="4d412-114">From the Azure portal, or from PowerShell, you can manage all your DSC configurations, resources, and target nodes.</span></span>

![Capture d’écran du panneau Azure Automation](./media/automation-dsc-overview/azure-automation-blade.png)

### <a name="import-reporting-data-into-log-analytics"></a><span data-ttu-id="4d412-116">Importer des données de création de rapports dans Log Analytics</span><span class="sxs-lookup"><span data-stu-id="4d412-116">Import reporting data into Log Analytics</span></span>

<span data-ttu-id="4d412-117">Les nœuds gérés dans Azure Automation DSC envoient des données détaillées sur l’état de création de rapports au serveur collecteur intégré.</span><span class="sxs-lookup"><span data-stu-id="4d412-117">Nodes that are managed with Azure Automation DSC send detailed reporting status data to the built-in pull server.</span></span>
<span data-ttu-id="4d412-118">Vous pouvez configurer Azure Automation DSC pour envoyer ces données à votre espace de travail Microsoft Operations Management Suite (OMS) Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="4d412-118">You can configure Azure Automation DSC to send this data to your Microsoft Operations Management Suite (OMS) Log Analytics workspace.</span></span>
<span data-ttu-id="4d412-119">Pour savoir comment envoyer des données d’état DSC à votre espace de travail Log Analytics, consultez [Forward Azure Automation DSC reporting data to OMS Log Analytics](automation-dsc-diagnostics.md) (Transférer des données de création de rapports Azure Automation DSC à OMS Log Analytics).</span><span class="sxs-lookup"><span data-stu-id="4d412-119">To learn how to send DSC status data to your Log Analytics workspace, see [Forward Azure Automation DSC reporting data to OMS Log Analytics](automation-dsc-diagnostics.md).</span></span>

## <a name="introduction-video"></a><span data-ttu-id="4d412-120">Vidéo de présentation</span><span class="sxs-lookup"><span data-stu-id="4d412-120">Introduction video</span></span>

<span data-ttu-id="4d412-121">Lire de la documentation vous enchante moyennement ?</span><span class="sxs-lookup"><span data-stu-id="4d412-121">Prefer watching to reading?</span></span> <span data-ttu-id="4d412-122">Jetez un œil à la vidéo ci-dessous, publiée en mai 2015 à l’occasion de l’annonce d’Azure Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="4d412-122">Have a look at the following video from May 2015, when Azure Automation DSC was first announced.</span></span>

>[!NOTE]
><span data-ttu-id="4d412-123">Bien que les concepts et le cycle de vie abordés dans cette vidéo soient corrects, Azure Automation DSC a beaucoup progressé depuis l’enregistrement de cette vidéo.</span><span class="sxs-lookup"><span data-stu-id="4d412-123">While the concepts and life cycle discussed in this video are correct, Azure Automation DSC has progressed a lot since this video was recorded.</span></span>
><span data-ttu-id="4d412-124">Désormais disponible au public, il dispose d’une interface utilisateur plus étendue dans le portail Azure et prend en charge des fonctionnalités supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="4d412-124">It is now generally available, has a much more extensive UI in the Azure portal, and supports many additional capabilities.</span></span>

> [!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3467/player]

## <a name="next-steps"></a><span data-ttu-id="4d412-125">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4d412-125">Next steps</span></span>

* <span data-ttu-id="4d412-126">Pour savoir comment intégrer des nœuds devant être gérés avec Azure Automation DSC, consultez [Gestion de machines avec Azure Automation DSC](automation-dsc-onboarding.md).</span><span class="sxs-lookup"><span data-stu-id="4d412-126">To learn how to onboard nodes to be managed with Azure Automation DSC, see [Onboarding machines for management by Azure Automation DSC](automation-dsc-onboarding.md)</span></span>
* <span data-ttu-id="4d412-127">Pour prendre en main Azure Automation DSC, consultez [Prise en main d’Azure Automation DSC](automation-dsc-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="4d412-127">To get started using Azure Automation DSC, see [Getting started with Azure Automation DSC](automation-dsc-getting-started.md)</span></span>
* <span data-ttu-id="4d412-128">Pour en savoir plus sur la compilation des configurations DSC pour les assigner à des nœuds cibles, consultez [Compilation de configurations dans Azure Automation DSC](automation-dsc-compile.md).</span><span class="sxs-lookup"><span data-stu-id="4d412-128">To learn about compiling DSC configurations so that you can assign them to target nodes, see [Compiling configurations in Azure Automation DSC](automation-dsc-compile.md)</span></span>
* <span data-ttu-id="4d412-129">Pour la référence de cmdlet PowerShell pour Azure Automation DSC, consultez [AzureRM.Automation](/powershell/module/azurerm.automation/#automation).</span><span class="sxs-lookup"><span data-stu-id="4d412-129">For PowerShell cmdlet reference for Azure Automation DSC, see [Azure Automation DSC cmdlets](/powershell/module/azurerm.automation/#automation)</span></span>
* <span data-ttu-id="4d412-130">Pour plus d’informations sur la tarification, consultez [Tarification de Automation](https://azure.microsoft.com/pricing/details/automation/).</span><span class="sxs-lookup"><span data-stu-id="4d412-130">For pricing information, see [Azure Automation DSC pricing](https://azure.microsoft.com/pricing/details/automation/)</span></span>
* <span data-ttu-id="4d412-131">Pour voir un exemple d’utilisation d’Azure Automation DSC dans un pipeline de déploiement continu, consultez [déploiement continu pour IaaS machines virtuelles à l’aide de Azure Automation DSC et Chocolatey](automation-dsc-cd-chocolatey.md)</span><span class="sxs-lookup"><span data-stu-id="4d412-131">To see an example of using Azure Automation DSC in a continuous deployment pipeline, see  [Continuous Deployment to IaaS VMs Using Azure Automation DSC and Chocolatey](automation-dsc-cd-chocolatey.md)</span></span>