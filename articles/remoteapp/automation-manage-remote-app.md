---
title: "aaaManage Azure RemoteApp à l’aide d’Azure Automation | Documents Microsoft"
description: "Découvrez comment hello service Azure Automation peut être utilisé toomanage Azure RemoteApp."
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
ms.openlocfilehash: a4cb23e292c797256e971acb3b363b025f140f16
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-remoteapp-using-azure-automation"></a><span data-ttu-id="24f20-103">Gestion d'Azure RemoteApp à l'aide d'Azure Automation</span><span class="sxs-lookup"><span data-stu-id="24f20-103">Managing Azure RemoteApp using Azure Automation</span></span>
> [!IMPORTANT]
> <span data-ttu-id="24f20-104">Azure RemoteApp ne sera plus disponible à partir du 31 août 2017.</span><span class="sxs-lookup"><span data-stu-id="24f20-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="24f20-105">Hello de lecture [annonce](https://go.microsoft.com/fwlink/?linkid=821148) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="24f20-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="24f20-106">Ce guide vous oblige à service d’Azure Automation toohello et comment il peut être gestion toosimplify utilisé d’Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="24f20-106">This guide will introduce you toohello Azure Automation service, and how it can be used toosimplify management of Azure RemoteApp.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="24f20-107">Qu'est-ce qu'Azure Automation ?</span><span class="sxs-lookup"><span data-stu-id="24f20-107">What is Azure Automation?</span></span>
<span data-ttu-id="24f20-108">[Azure Automation](../automation/automation-intro.md) est un service Azure destiné à simplifier la gestion du cloud via l'automatisation des processus.</span><span class="sxs-lookup"><span data-stu-id="24f20-108">[Azure Automation](../automation/automation-intro.md) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="24f20-109">Les tâches manuelles, fréquence de répétition, longue et sujettes aux erreurs à l’aide d’Azure Automation, peuvent être automatisée tooincrease fiabilité, l’efficacité et toovalue de temps pour votre organisation.</span><span class="sxs-lookup"><span data-stu-id="24f20-109">Using Azure Automation, manual, frequently-repeated, long-running, and error-prone tasks can be automated tooincrease reliability, efficiency, and time toovalue for your organization.</span></span>

<span data-ttu-id="24f20-110">Azure Automation fournit un moteur d’exécution de flux de travail hautement fiable et à haute disponibilité qui s’adapte toomeet à vos besoins.</span><span class="sxs-lookup"><span data-stu-id="24f20-110">Azure Automation provides a highly-reliable, highly-available workflow execution engine that scales toomeet your needs.</span></span> <span data-ttu-id="24f20-111">Dans Azure Automation, les processus peuvent être lancés manuellement, par des systèmes tiers ou à des intervalles planifiés, afin que les tâches interviennent exactement au moment opportun.</span><span class="sxs-lookup"><span data-stu-id="24f20-111">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="24f20-112">Réduire la surcharge opérationnelle et de libérer de l’informatique et toofocus du personnel DevOps sur le travail qui ajoute la valeur de l’entreprise en déplaçant votre toobe de tâches de gestion de cloud exécuté automatiquement par Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="24f20-112">Reduce operational overhead and free up IT and DevOps staff toofocus on work that adds business value by moving your cloud management tasks toobe run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-remoteapp"></a><span data-ttu-id="24f20-113">Comment Azure Automation peut-il aider à gérer Azure RemoteApp ?</span><span class="sxs-lookup"><span data-stu-id="24f20-113">How can Azure Automation help manage Azure RemoteApp?</span></span>
<span data-ttu-id="24f20-114">RemoteApp peut être géré dans Azure Automation à l’aide d’applets de commande hello PowerShell qui sont disponibles dans hello [outils Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span><span class="sxs-lookup"><span data-stu-id="24f20-114">RemoteApp can be managed in Azure Automation by using hello PowerShell cmdlets that are available in hello [Azure PowerShell tools](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span></span> <span data-ttu-id="24f20-115">Azure Automation dispose de ces applets de commande RemoteApp PowerShell disponibles en dehors de la zone de hello, afin que vous puissiez effectuer toutes les tâches de gestion de RemoteApp dans le service de hello.</span><span class="sxs-lookup"><span data-stu-id="24f20-115">Azure Automation has these RemoteApp PowerShell cmdlets available out of hello box, so that you can perform all of your RemoteApp management tasks within hello service.</span></span> <span data-ttu-id="24f20-116">Vous pouvez également de paires de ces applets de commande dans Azure Automation avec les applets de commande hello pour les autres services Azure, les tooautomate des tâches complexes entre des services Azure et les systèmes tiers 3e.</span><span class="sxs-lookup"><span data-stu-id="24f20-116">You can also pair these cmdlets in Azure Automation with hello cmdlets for other Azure services, tooautomate complex tasks across Azure services and 3rd party systems.</span></span>

## <a name="next-steps"></a><span data-ttu-id="24f20-117">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="24f20-117">Next steps</span></span>
<span data-ttu-id="24f20-118">Maintenant que vous avez appris les notions de base de hello d’Azure Automation et comment il peut être utilisé toomanage Azure RemoteApp, suivez ces liens de toolearn plus sur Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="24f20-118">Now that you've learned hello basics of Azure Automation and how it can be used toomanage Azure RemoteApp, follow these links toolearn more about Azure Automation.</span></span>

* <span data-ttu-id="24f20-119">Consultez hello Azure Automation [didacticiel de mise en route](../automation/automation-first-runbook-graphical.md)</span><span class="sxs-lookup"><span data-stu-id="24f20-119">See hello Azure Automation [Getting Started Tutorial](../automation/automation-first-runbook-graphical.md)</span></span>

