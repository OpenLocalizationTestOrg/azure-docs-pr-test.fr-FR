---
title: "Gestion d’une application web Azure à l’aide d’Azure Automation | Microsoft Docs"
description: "Découvrez comment utiliser le service Azure Automation pour gérer une application web Azure."
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
ms.openlocfilehash: a96332346747114620ee6ebd2a2d0c4417d4a213
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="managing-azure-web-app-using-azure-automation"></a><span data-ttu-id="c18ef-103">Gestion d’une application web Azure à l’aide d’Azure Automation</span><span class="sxs-lookup"><span data-stu-id="c18ef-103">Managing Azure Web App using Azure Automation</span></span>
<span data-ttu-id="c18ef-104">Ce guide vous présente le service Azure Automation et décrit comment l’utiliser pour simplifier la gestion d’une application web Azure.</span><span class="sxs-lookup"><span data-stu-id="c18ef-104">This guide will introduce you to the Azure Automation service, and how it can be used to simplify management of Azure Web App.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="c18ef-105">Qu'est-ce qu'Azure Automation ?</span><span class="sxs-lookup"><span data-stu-id="c18ef-105">What is Azure Automation?</span></span>
<span data-ttu-id="c18ef-106">[Azure Automation](../automation/automation-intro.md) est un service Azure destiné à simplifier la gestion du cloud via l'automatisation des processus.</span><span class="sxs-lookup"><span data-stu-id="c18ef-106">[Azure Automation](../automation/automation-intro.md) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="c18ef-107">Il automatise les tâches manuelles, répétitives, fastidieuses et sources d’erreurs pour accroître la fiabilité, l’efficacité et le retour sur investissement de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="c18ef-107">Using Azure Automation, manual, repeated, long-running, and error-prone tasks can be automated to increase reliability, efficiency, and time to value for your organization.</span></span>

<span data-ttu-id="c18ef-108">Azure Automation fournit un moteur d’exécution de workflow à haute fiabilité et à haute disponibilité, qui s’adapte à vos besoins.</span><span class="sxs-lookup"><span data-stu-id="c18ef-108">Azure Automation provides a highly-reliable, highly-available workflow execution engine that scales to meet your needs.</span></span> <span data-ttu-id="c18ef-109">Dans Azure Automation, les processus peuvent être lancés manuellement, par des systèmes tiers ou à des intervalles planifiés, afin que les tâches interviennent exactement au moment opportun.</span><span class="sxs-lookup"><span data-stu-id="c18ef-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="c18ef-110">Réduisez les coûts opérationnels et libérez du temps pour que votre équipe d’informaticiens et de développeurs puisse se concentrer sur des tâches qui génèrent une valeur ajoutée pour l’entreprise, en déléguant l’exécution automatique de vos tâches de gestion de Cloud à Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="c18ef-110">Reduce operational overhead and free up IT and DevOps staff to focus on work that adds business value by moving your cloud management tasks to be run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-web-app"></a><span data-ttu-id="c18ef-111">Comment Azure Automation peut-il vous aider à gérer une application web Azure ?</span><span class="sxs-lookup"><span data-stu-id="c18ef-111">How can Azure Automation help manage Azure Web App?</span></span>
<span data-ttu-id="c18ef-112">Dans Azure Automation, une application web est gérée à l’aide d’applets de commande PowerShell qui sont disponibles dans les [modules Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="c18ef-112">Web App can be managed in Azure Automation by using the PowerShell cmdlets that are available in the [Azure PowerShell modules](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="c18ef-113">Vous pouvez [installer ces applets de commande PowerShell dans Azure Automation](https://azure.microsoft.com/blog/announcing-azure-resource-manager-support-azure-automation-runbooks/)afin d’exécuter toutes vos tâches de gestion d’application Web dans ce service.</span><span class="sxs-lookup"><span data-stu-id="c18ef-113">You can [install these Web App PowerShell cmdlets in Azure Automation](https://azure.microsoft.com/blog/announcing-azure-resource-manager-support-azure-automation-runbooks/), so that you can perform all of your Web App management tasks within the service.</span></span> <span data-ttu-id="c18ef-114">Dans Azure Automation, vous pouvez également associer ces applets de commande à des applets de commande d'autres services Azure, afin d'automatiser des tâches complexes entre des services Azure et des systèmes tiers.</span><span class="sxs-lookup"><span data-stu-id="c18ef-114">You can also pair these cmdlets in Azure Automation with the cmdlets for other Azure services to automate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="c18ef-115">Voici quelques exemples de gestion d’App Services avec Automation :</span><span class="sxs-lookup"><span data-stu-id="c18ef-115">Here are some examples of managing App Services with Automation:</span></span>

* [<span data-ttu-id="c18ef-116">Scripts de gestion d’applications Web</span><span class="sxs-lookup"><span data-stu-id="c18ef-116">Scripts for managing Web Apps</span></span>](https://azure.microsoft.com/documentation/scripts/)

## <a name="next-steps"></a><span data-ttu-id="c18ef-117">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c18ef-117">Next steps</span></span>
<span data-ttu-id="c18ef-118">Maintenant que vous connaissez les bases d’Azure Automation et que vous savez l’utiliser pour gérer une application web Azure, cliquez sur les liens ci-dessous pour en savoir plus.</span><span class="sxs-lookup"><span data-stu-id="c18ef-118">Now that you've learned the basics of Azure Automation and how it can be used to manage Azure Web App, follow these links to learn more about Azure Automation.</span></span>

* <span data-ttu-id="c18ef-119">Consultez le [Didacticiel de prise en main](../automation/automation-first-runbook-graphical.md)</span><span class="sxs-lookup"><span data-stu-id="c18ef-119">See the Azure Automation [Getting Started Tutorial](../automation/automation-first-runbook-graphical.md)</span></span>

