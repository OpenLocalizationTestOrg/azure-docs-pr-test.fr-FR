---
title: "aaaManage gestion des API Azure à l’aide d’Azure Automation"
description: "Découvrez comment hello service Azure Automation peut être utilisé toomanage gestion des API Azure."
services: api-management, automation
documentationcenter: 
author: csand-msft
manager: eamono
editor: 
ms.assetid: 2e53c9af-f738-47f8-b1b6-593050a7c51b
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 05b8e3cad786fa701feb88f7b6d9629f16686d15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-api-management-using-azure-automation"></a><span data-ttu-id="997a7-103">Gestion des API Azure avec Azure Automation</span><span class="sxs-lookup"><span data-stu-id="997a7-103">Managing Azure API Management using Azure Automation</span></span>
<span data-ttu-id="997a7-104">Ce guide vous oblige à service d’Azure Automation toohello et comment il peut être gestion toosimplify utilisés de la gestion des API Azure.</span><span class="sxs-lookup"><span data-stu-id="997a7-104">This guide will introduce you toohello Azure Automation service, and how it can be used toosimplify management of Azure API Management.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="997a7-105">Qu'est-ce qu'Azure Automation ?</span><span class="sxs-lookup"><span data-stu-id="997a7-105">What is Azure Automation?</span></span>
<span data-ttu-id="997a7-106">[Azure Automation](https://azure.microsoft.com/services/automation/) est un service Azure destiné à simplifier la gestion du cloud via l'automatisation des processus.</span><span class="sxs-lookup"><span data-stu-id="997a7-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="997a7-107">Les tâches manuelles, répétées, longue et sujettes aux erreurs à l’aide d’Azure Automation, peuvent être automatisée tooincrease fiabilité, l’efficacité et toovalue de temps pour votre organisation.</span><span class="sxs-lookup"><span data-stu-id="997a7-107">Using Azure Automation, manual, repeated, long-running, and error-prone tasks can be automated tooincrease reliability, efficiency, and time toovalue for your organization.</span></span>

<span data-ttu-id="997a7-108">Azure Automation fournit un moteur d’exécution de flux de travail hautement fiable et à haute disponibilité qui s’adapte toomeet à vos besoins.</span><span class="sxs-lookup"><span data-stu-id="997a7-108">Azure Automation provides a highly-reliable, highly-available workflow execution engine that scales toomeet your needs.</span></span> <span data-ttu-id="997a7-109">Dans Azure Automation, les processus peuvent être lancés manuellement, par des systèmes tiers ou à des intervalles planifiés, afin que les tâches interviennent exactement au moment opportun.</span><span class="sxs-lookup"><span data-stu-id="997a7-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="997a7-110">Réduire la surcharge opérationnelle et de libérer de l’informatique et toofocus du personnel DevOps sur le travail qui ajoute la valeur de l’entreprise en déplaçant votre toobe de tâches de gestion de cloud exécuté automatiquement par Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="997a7-110">Reduce operational overhead and free up IT and DevOps staff toofocus on work that adds business value by moving your cloud management tasks toobe run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-api-management"></a><span data-ttu-id="997a7-111">Comment Azure Automation peut-il aider à gérer les API Azure ?</span><span class="sxs-lookup"><span data-stu-id="997a7-111">How can Azure Automation help manage Azure API Management?</span></span>
<span data-ttu-id="997a7-112">Gestion des API peuvent être gérée dans Azure Automation à l’aide de hello [applets de commande Windows PowerShell pour l’API de gestion des API Azure](https://azure.microsoft.com/updates/full-set-of-windows-powershell-cmdlets-for-azure-api-management-api/).</span><span class="sxs-lookup"><span data-stu-id="997a7-112">API Management can be managed in Azure Automation by using hello [Windows PowerShell cmdlets for Azure API Management API](https://azure.microsoft.com/updates/full-set-of-windows-powershell-cmdlets-for-azure-api-management-api/).</span></span> <span data-ttu-id="997a7-113">Dans Azure Automation vous pouvez écrire tooperform de scripts PowerShell workflow beaucoup de vos tâches de gestion des API à l’aide des applets de commande hello.</span><span class="sxs-lookup"><span data-stu-id="997a7-113">Within Azure Automation you can write PowerShell workflow scripts tooperform many of your API Management tasks using hello cmdlets.</span></span> <span data-ttu-id="997a7-114">Vous pouvez également de paires de ces applets de commande dans Azure Automation avec les applets de commande hello pour les autres services Azure, les tooautomate des tâches complexes entre des services Azure et les systèmes tiers 3e.</span><span class="sxs-lookup"><span data-stu-id="997a7-114">You can also pair these cmdlets in Azure Automation with hello cmdlets for other Azure services, tooautomate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="997a7-115">Voici quelques exemples de gestion d’API avec Automation :</span><span class="sxs-lookup"><span data-stu-id="997a7-115">Here are some examples of using API Management with Automation:</span></span>

* [<span data-ttu-id="997a7-116">Gestion des API Azure : utilisation de PowerShell pour la sauvegarde et la restauration</span><span class="sxs-lookup"><span data-stu-id="997a7-116">Azure API Management – Using PowerShell for backup and restore</span></span>](https://blogs.msdn.microsoft.com/katriend/2015/10/02/azure-api-management-using-powershell-for-backup-and-restore/)

## <a name="next-steps"></a><span data-ttu-id="997a7-117">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="997a7-117">Next Steps</span></span>
<span data-ttu-id="997a7-118">Maintenant que vous avez appris les notions de base de hello d’Azure Automation et comment il peut être utilisé toomanage gestion des API Azure, suivez ces liens de toolearn plus.</span><span class="sxs-lookup"><span data-stu-id="997a7-118">Now that you've learned hello basics of Azure Automation and how it can be used toomanage Azure API Management, follow these links toolearn more.</span></span>

* <span data-ttu-id="997a7-119">Consultez hello Azure Automation [didacticiel de mise en route](../automation/automation-first-runbook-graphical.md).</span><span class="sxs-lookup"><span data-stu-id="997a7-119">See hello Azure Automation [getting started tutorial](../automation/automation-first-runbook-graphical.md).</span></span>

