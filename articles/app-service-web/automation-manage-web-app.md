---
title: "aaaManage Azure Web App à l’aide d’Azure Automation | Documents Microsoft"
description: "Découvrez comment hello service Azure Automation peut être utilisé toomanage application Web Azure."
services: app-service\web, automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
ms.assetid: c960a44f-f941-401d-afba-a4bc0f0394eb
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2016
ms.author: magoedte
ms.openlocfilehash: 6d80351a2927f26753cfbaead6e1c0c3c94e86e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-web-app-using-azure-automation"></a><span data-ttu-id="0329d-103">Gestion d’une application web Azure à l’aide d’Azure Automation</span><span class="sxs-lookup"><span data-stu-id="0329d-103">Managing Azure Web App using Azure Automation</span></span>
<span data-ttu-id="0329d-104">Ce guide vous oblige à service d’Azure Automation toohello et comment il peut être gestion toosimplify utilisés de l’application Web Azure.</span><span class="sxs-lookup"><span data-stu-id="0329d-104">This guide will introduce you toohello Azure Automation service, and how it can be used toosimplify management of Azure Web App.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="0329d-105">Qu'est-ce qu'Azure Automation ?</span><span class="sxs-lookup"><span data-stu-id="0329d-105">What is Azure Automation?</span></span>
<span data-ttu-id="0329d-106">[Azure Automation](../automation/automation-intro.md) est un service Azure destiné à simplifier la gestion du cloud via l'automatisation des processus.</span><span class="sxs-lookup"><span data-stu-id="0329d-106">[Azure Automation](../automation/automation-intro.md) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="0329d-107">Les tâches manuelles, répétées, longue et sujettes aux erreurs à l’aide d’Azure Automation, peuvent être automatisée tooincrease fiabilité, l’efficacité et toovalue de temps pour votre organisation.</span><span class="sxs-lookup"><span data-stu-id="0329d-107">Using Azure Automation, manual, repeated, long-running, and error-prone tasks can be automated tooincrease reliability, efficiency, and time toovalue for your organization.</span></span>

<span data-ttu-id="0329d-108">Azure Automation fournit un moteur d’exécution de flux de travail hautement fiable et à haute disponibilité qui s’adapte toomeet à vos besoins.</span><span class="sxs-lookup"><span data-stu-id="0329d-108">Azure Automation provides a highly-reliable, highly-available workflow execution engine that scales toomeet your needs.</span></span> <span data-ttu-id="0329d-109">Dans Azure Automation, les processus peuvent être lancés manuellement, par des systèmes tiers ou à des intervalles planifiés, afin que les tâches interviennent exactement au moment opportun.</span><span class="sxs-lookup"><span data-stu-id="0329d-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="0329d-110">Réduire la surcharge opérationnelle et de libérer de l’informatique et toofocus du personnel DevOps sur le travail qui ajoute la valeur de l’entreprise en déplaçant votre toobe de tâches de gestion de cloud exécuté automatiquement par Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="0329d-110">Reduce operational overhead and free up IT and DevOps staff toofocus on work that adds business value by moving your cloud management tasks toobe run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-web-app"></a><span data-ttu-id="0329d-111">Comment Azure Automation peut-il vous aider à gérer une application web Azure ?</span><span class="sxs-lookup"><span data-stu-id="0329d-111">How can Azure Automation help manage Azure Web App?</span></span>
<span data-ttu-id="0329d-112">Application Web peut être gérée dans Azure Automation à l’aide d’applets de commande hello PowerShell qui sont disponibles dans hello [modules Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="0329d-112">Web App can be managed in Azure Automation by using hello PowerShell cmdlets that are available in hello [Azure PowerShell modules](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="0329d-113">Vous pouvez [installer ces applets de commande PowerShell d’application Web dans Azure Automation](https://azure.microsoft.com/blog/announcing-azure-resource-manager-support-azure-automation-runbooks/), de sorte que vous pouvez effectuer toutes vos tâches de gestion de l’application Web au sein du service de hello.</span><span class="sxs-lookup"><span data-stu-id="0329d-113">You can [install these Web App PowerShell cmdlets in Azure Automation](https://azure.microsoft.com/blog/announcing-azure-resource-manager-support-azure-automation-runbooks/), so that you can perform all of your Web App management tasks within hello service.</span></span> <span data-ttu-id="0329d-114">Vous pouvez également de paires de ces applets de commande dans Azure Automation avec les applets de commande hello pour d’autres tâches complexes de services Azure tooautomate entre des services Azure et les systèmes tiers 3e.</span><span class="sxs-lookup"><span data-stu-id="0329d-114">You can also pair these cmdlets in Azure Automation with hello cmdlets for other Azure services tooautomate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="0329d-115">Voici quelques exemples de gestion d’App Services avec Automation :</span><span class="sxs-lookup"><span data-stu-id="0329d-115">Here are some examples of managing App Services with Automation:</span></span>

* [<span data-ttu-id="0329d-116">Scripts de gestion d’applications Web</span><span class="sxs-lookup"><span data-stu-id="0329d-116">Scripts for managing Web Apps</span></span>](https://azure.microsoft.com/documentation/scripts/)

## <a name="next-steps"></a><span data-ttu-id="0329d-117">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0329d-117">Next steps</span></span>
<span data-ttu-id="0329d-118">Maintenant que vous avez appris les notions de base de hello d’Azure Automation et comment il peut être utilisé toomanage application Web Azure, suivez ces liens de toolearn plus sur Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="0329d-118">Now that you've learned hello basics of Azure Automation and how it can be used toomanage Azure Web App, follow these links toolearn more about Azure Automation.</span></span>

* <span data-ttu-id="0329d-119">Consultez hello Azure Automation [didacticiel de mise en route](../automation/automation-first-runbook-graphical.md)</span><span class="sxs-lookup"><span data-stu-id="0329d-119">See hello Azure Automation [Getting Started Tutorial](../automation/automation-first-runbook-graphical.md)</span></span>

