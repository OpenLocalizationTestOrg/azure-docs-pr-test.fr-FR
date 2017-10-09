---
title: "aaaManage machines virtuelles à l’aide d’Azure Automation | Documents Microsoft"
description: "Découvrez comment hello service Azure Automation peut être utilisé toomanage machines virtuelles à l’échelle."
services: virtual-machines-windows, automation
documentationcenter: 
author: jodoglevy
manager: timlt
editor: 
ms.assetid: ce49f83a-f409-42ee-af74-a8ea2caa9ae8
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2016
ms.author: timlt
ms.openlocfilehash: bfe7b3a51b6e82bd7cd5b0a83df7226476ed4f36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-virtual-machines-using-azure-automation"></a><span data-ttu-id="4e614-103">Gestion d'Azure Virtual Machines à l'aide d'Azure Automation</span><span class="sxs-lookup"><span data-stu-id="4e614-103">Managing Azure Virtual Machines using Azure Automation</span></span>
<span data-ttu-id="4e614-104">Ce guide vous présente un service d’Azure Automation toohello et comment il peut être utilisé toosimplify la gestion de vos machines virtuelles Azure.</span><span class="sxs-lookup"><span data-stu-id="4e614-104">This guide introduces you toohello Azure Automation service and how it can be used toosimplify managing your Azure virtual machines.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="4e614-105">Qu'est-ce qu'Azure Automation ?</span><span class="sxs-lookup"><span data-stu-id="4e614-105">What is Azure Automation?</span></span>
<span data-ttu-id="4e614-106">[Azure Automation](https://azure.microsoft.com/services/automation/) est un service Azure destiné à simplifier la gestion du cloud via l'automatisation des processus.</span><span class="sxs-lookup"><span data-stu-id="4e614-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="4e614-107">À l’aide de Azure Automation, des tâches longues, manuelles, sujette aux erreurs et répétitives peuvent être automatisée tooincrease fiabilité, l’efficacité et time-to-value pour votre organisation.</span><span class="sxs-lookup"><span data-stu-id="4e614-107">By using Azure Automation, long-running, manual, error-prone, and frequently repeated tasks can be automated tooincrease reliability, efficiency, and time-to-value for your organization.</span></span>

<span data-ttu-id="4e614-108">Azure Automation fournit un moteur d’exécution de flux de travail hautement fiable et à haute disponibilité qui s’adapte toomeet vos besoins que votre organisation se développe.</span><span class="sxs-lookup"><span data-stu-id="4e614-108">Azure Automation provides a highly reliable and highly available workflow execution engine that scales toomeet your needs as your organization grows.</span></span> <span data-ttu-id="4e614-109">Dans Azure Automation, les processus peuvent être lancés manuellement, par des systèmes tiers ou à des intervalles planifiés, afin que les tâches interviennent exactement au moment opportun.</span><span class="sxs-lookup"><span data-stu-id="4e614-109">In Azure Automation, processes can be kicked off manually, by third-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="4e614-110">Vous pouvez réduire la surcharge opérationnelle et libérer de l’informatique et DevOps personnel toofocus sur le travail qui ajoute la valeur commerciale en exécutant votre cloud de tâches de gestion automatiquement avec Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="4e614-110">You can lower operational overhead and free up IT and DevOps staff toofocus on work that adds business value by running your cloud management tasks automatically with Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-virtual-machines"></a><span data-ttu-id="4e614-111">Comment Azure Automation peut-il aider à gérer des machines virtuelles Azure ?</span><span class="sxs-lookup"><span data-stu-id="4e614-111">How can Azure Automation help manage Azure virtual machines?</span></span>
<span data-ttu-id="4e614-112">Les machines virtuelles peuvent être gérées dans Azure Automation à l’aide d’ [Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span><span class="sxs-lookup"><span data-stu-id="4e614-112">Virtual machines can be managed in Azure Automation by using [Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span></span> <span data-ttu-id="4e614-113">Azure Automation inclut des applets de commande PowerShell Azure hello, afin de pouvoir effectuer toutes vos tâches de gestion de machine virtuelle au sein du service de hello.</span><span class="sxs-lookup"><span data-stu-id="4e614-113">Azure Automation includes hello Azure PowerShell cmdlets, so you can perform all of your virtual machine management tasks within hello service.</span></span> <span data-ttu-id="4e614-114">Vous pouvez également Couplez applets de commande hello dans Azure Automation avec les applets de commande hello pour les autres services Azure, les tooautomate des tâches complexes entre des services Azure et systèmes tiers.</span><span class="sxs-lookup"><span data-stu-id="4e614-114">You can also pair hello cmdlets in Azure Automation with hello cmdlets for other Azure services, tooautomate complex tasks across Azure services and third-party systems.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4e614-115">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4e614-115">Next steps</span></span>
<span data-ttu-id="4e614-116">Maintenant que vous avez appris les notions de base de hello d’Azure Automation et comment il peut être utilisé toomanage machines virtuelles Azure, en savoir plus :</span><span class="sxs-lookup"><span data-stu-id="4e614-116">Now that you've learned hello basics of Azure Automation and how it can be used toomanage Azure virtual machines, learn more:</span></span>

* [<span data-ttu-id="4e614-117">Vue d’ensemble de Microsoft Azure Automation</span><span class="sxs-lookup"><span data-stu-id="4e614-117">Azure Automation Overview</span></span>](../../automation/automation-intro.md)
* [<span data-ttu-id="4e614-118">Mon premier Runbook</span><span class="sxs-lookup"><span data-stu-id="4e614-118">My first runbook</span></span>](../../automation/automation-first-runbook-graphical.md)
* [<span data-ttu-id="4e614-119">Plan d’apprentissage pour Azure Automation</span><span class="sxs-lookup"><span data-stu-id="4e614-119">Azure Automation learning map</span></span>](https://azure.microsoft.com/documentation/learning-paths/automation/)

