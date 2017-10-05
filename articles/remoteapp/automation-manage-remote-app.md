---
title: "Gérer Azure RemoteApp avec Azure Automation | Microsoft Docs"
description: "Découvrez comment le service Azure Automation peut être utilisé pour gérer Azure RemoteApp."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
ms.assetid: 589f01ef-f9c1-4e7b-a040-1b46862d3544
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: magoedte;csand
ms.openlocfilehash: 59ac11f153c0bd74a1106400dbbf5790968b657c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="managing-azure-remoteapp-using-azure-automation"></a><span data-ttu-id="56471-103">Gestion d'Azure RemoteApp à l'aide d'Azure Automation</span><span class="sxs-lookup"><span data-stu-id="56471-103">Managing Azure RemoteApp using Azure Automation</span></span>
> [!IMPORTANT]
> <span data-ttu-id="56471-104">Azure RemoteApp ne sera plus disponible à partir du 31 août 2017.</span><span class="sxs-lookup"><span data-stu-id="56471-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="56471-105">Pour plus d’informations, lisez [l’annonce](https://go.microsoft.com/fwlink/?linkid=821148) .</span><span class="sxs-lookup"><span data-stu-id="56471-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="56471-106">Ce guide vous présente le service Azure Automation et la manière de l'utiliser pour gérer plus simplement Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="56471-106">This guide will introduce you to the Azure Automation service, and how it can be used to simplify management of Azure RemoteApp.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="56471-107">Qu'est-ce qu'Azure Automation ?</span><span class="sxs-lookup"><span data-stu-id="56471-107">What is Azure Automation?</span></span>
<span data-ttu-id="56471-108">[Azure Automation](../automation/automation-intro.md) est un service Azure destiné à simplifier la gestion du cloud via l'automatisation des processus.</span><span class="sxs-lookup"><span data-stu-id="56471-108">[Azure Automation](../automation/automation-intro.md) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="56471-109">Il automatise les tâches manuelles, répétitives, fastidieuses et sources d’erreurs pour accroître la fiabilité, l’efficacité et le retour sur investissement de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="56471-109">Using Azure Automation, manual, frequently-repeated, long-running, and error-prone tasks can be automated to increase reliability, efficiency, and time to value for your organization.</span></span>

<span data-ttu-id="56471-110">Azure Automation fournit un moteur d’exécution de workflow à haute fiabilité et à haute disponibilité, qui s’adapte à vos besoins.</span><span class="sxs-lookup"><span data-stu-id="56471-110">Azure Automation provides a highly-reliable, highly-available workflow execution engine that scales to meet your needs.</span></span> <span data-ttu-id="56471-111">Dans Azure Automation, les processus peuvent être lancés manuellement, par des systèmes tiers ou à des intervalles planifiés, afin que les tâches interviennent exactement au moment opportun.</span><span class="sxs-lookup"><span data-stu-id="56471-111">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="56471-112">Réduisez les coûts opérationnels et libérez du temps pour que votre équipe d’informaticiens et de développeurs puisse se concentrer sur des tâches qui génèrent une valeur ajoutée pour l’entreprise, en déléguant l’exécution automatique de vos tâches de gestion de Cloud à Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="56471-112">Reduce operational overhead and free up IT and DevOps staff to focus on work that adds business value by moving your cloud management tasks to be run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-remoteapp"></a><span data-ttu-id="56471-113">Comment Azure Automation peut-il aider à gérer Azure RemoteApp ?</span><span class="sxs-lookup"><span data-stu-id="56471-113">How can Azure Automation help manage Azure RemoteApp?</span></span>
<span data-ttu-id="56471-114">RemoteApp peut être géré dans Azure Automation à l'aide des applets de commande PowerShell qui sont disponibles dans les [outils Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span><span class="sxs-lookup"><span data-stu-id="56471-114">RemoteApp can be managed in Azure Automation by using the PowerShell cmdlets that are available in the [Azure PowerShell tools](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span></span> <span data-ttu-id="56471-115">Azure Automation dispose dès le départ de ces applets de commande PowerShell pour RemoteApp, de sorte que vous pouvez effectuer toutes vos tâches de gestion de RemoteApp au sein du service.</span><span class="sxs-lookup"><span data-stu-id="56471-115">Azure Automation has these RemoteApp PowerShell cmdlets available out of the box, so that you can perform all of your RemoteApp management tasks within the service.</span></span> <span data-ttu-id="56471-116">Dans Azure Automation, vous pouvez également associer ces applets de commande à des applets de commande d'autres services Azure, afin d'automatiser des tâches complexes entre des services Azure et des systèmes tiers.</span><span class="sxs-lookup"><span data-stu-id="56471-116">You can also pair these cmdlets in Azure Automation with the cmdlets for other Azure services, to automate complex tasks across Azure services and 3rd party systems.</span></span>

## <a name="next-steps"></a><span data-ttu-id="56471-117">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="56471-117">Next steps</span></span>
<span data-ttu-id="56471-118">Maintenant que vous avez appris les bases d'Azure Automation et la manière de l'utiliser pour gérer Azure RemoteApp, cliquez sur ces liens pour en savoir plus sur Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="56471-118">Now that you've learned the basics of Azure Automation and how it can be used to manage Azure RemoteApp, follow these links to learn more about Azure Automation.</span></span>

* <span data-ttu-id="56471-119">Consultez le [Didacticiel de prise en main](../automation/automation-first-runbook-graphical.md)</span><span class="sxs-lookup"><span data-stu-id="56471-119">See the Azure Automation [Getting Started Tutorial](../automation/automation-first-runbook-graphical.md)</span></span>

