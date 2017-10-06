---
title: "aaaManage Azure Cloud Services à l’aide d’Azure Automation | Documents Microsoft"
description: "Découvrez comment hello service Azure Automation peut être utilisés toomanage services cloud Azure à l’échelle."
services: cloud-services, automation
documentationcenter: 
author: jodoglevy
manager: timlt
editor: 
ms.assetid: 3789810a-2892-4eef-bf29-c781c1b5af48
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2016
ms.author: timlt
ms.openlocfilehash: 8e920fb94955466bfec71cc332444f5f0ee497a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-cloud-services-using-azure-automation"></a><span data-ttu-id="1ed9c-103">Gestion d'Azure Cloud Services à l'aide d'Azure Automation</span><span class="sxs-lookup"><span data-stu-id="1ed9c-103">Managing Azure Cloud Services using Azure Automation</span></span>
<span data-ttu-id="1ed9c-104">Ce guide vous présentent service Azure Automation de toohello, et comment il peut être gestion toosimplify utilisés de vos services cloud Azure.</span><span class="sxs-lookup"><span data-stu-id="1ed9c-104">This guide will introduce you toohello Azure Automation service, and how it can be used toosimplify management of your Azure cloud services.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="1ed9c-105">Qu'est-ce qu'Azure Automation ?</span><span class="sxs-lookup"><span data-stu-id="1ed9c-105">What is Azure Automation?</span></span>
<span data-ttu-id="1ed9c-106">[Azure Automation](https://azure.microsoft.com/services/automation/) est un service Azure destiné à simplifier la gestion du cloud via l'automatisation des processus.</span><span class="sxs-lookup"><span data-stu-id="1ed9c-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="1ed9c-107">Les tâches longues, manuelles, sujette aux erreurs et répétitives à l’aide d’Azure Automation, peuvent être automatisée tooincrease fiabilité, l’efficacité et toovalue de temps pour votre organisation.</span><span class="sxs-lookup"><span data-stu-id="1ed9c-107">Using Azure Automation, long-running, manual, error-prone, and frequently repeated tasks can be automated tooincrease reliability, efficiency, and time toovalue for your organization.</span></span>

<span data-ttu-id="1ed9c-108">Azure Automation fournit un moteur d’exécution de flux de travail hautement fiable et à haute disponibilité qui s’adapte toomeet vos besoins que votre organisation se développe.</span><span class="sxs-lookup"><span data-stu-id="1ed9c-108">Azure Automation provides a highly-reliable and highly-available workflow execution engine that scales toomeet your needs as your organization grows.</span></span> <span data-ttu-id="1ed9c-109">Dans Azure Automation, les processus peuvent être lancés manuellement, par des systèmes tiers ou à des intervalles planifiés, afin que les tâches interviennent exactement au moment opportun.</span><span class="sxs-lookup"><span data-stu-id="1ed9c-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="1ed9c-110">Réduire la surcharge opérationnelle et de libérer de l’informatique / toofocus du personnel DevOps sur le travail qui ajoute la valeur de l’entreprise en déplaçant votre toobe de tâches de gestion de cloud exécutés automatiquement par Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="1ed9c-110">Lower operational overhead and free up IT / DevOps staff toofocus on work that adds business value by moving your cloud management tasks toobe run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-cloud-services"></a><span data-ttu-id="1ed9c-111">Comment Azure Automation peut-il aider à gérer des services de cloud computing Azure ?</span><span class="sxs-lookup"><span data-stu-id="1ed9c-111">How can Azure Automation help manage Azure cloud services?</span></span>
<span data-ttu-id="1ed9c-112">Services de cloud computing Azure peuvent être gérés dans Azure Automation à l’aide d’applets de commande hello PowerShell qui sont disponibles dans hello [outils Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span><span class="sxs-lookup"><span data-stu-id="1ed9c-112">Azure cloud services can be managed in Azure Automation by using hello PowerShell cmdlets that are available in hello [Azure PowerShell tools](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span></span> <span data-ttu-id="1ed9c-113">Azure Automation dispose ces cloud service applets de commande PowerShell disponibles en dehors de la zone de hello, afin que vous pouvez effectuer toutes vos tâches de gestion de service cloud dans le service de hello.</span><span class="sxs-lookup"><span data-stu-id="1ed9c-113">Azure Automation has these cloud service PowerShell cmdlets available out of hello box, so that you can perform all of your cloud service management tasks within hello service.</span></span> <span data-ttu-id="1ed9c-114">Vous pouvez également de paires de ces applets de commande dans Azure Automation avec les applets de commande hello pour les autres services Azure, les tooautomate des tâches complexes entre des services Azure et les systèmes tiers 3e.</span><span class="sxs-lookup"><span data-stu-id="1ed9c-114">You can also pair these cmdlets in Azure Automation with hello cmdlets for other Azure services, tooautomate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="1ed9c-115">Quelques exemples d’utilisations de toomanage Azure Automation qu'incluent des Services de cloud computing Azure :</span><span class="sxs-lookup"><span data-stu-id="1ed9c-115">Some example uses of Azure Automation toomanage Azure Cloud Services include:</span></span>

* [<span data-ttu-id="1ed9c-116">Déploiement continu d’un service cloud si cscfg ou cspkg est mis à jour dans Azure Blob Storage</span><span class="sxs-lookup"><span data-stu-id="1ed9c-116">Continous deployment of a Cloud Service whenever cscfg or cspkg is updated in Azure Blob storage</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Continuous-Deployment-of-A-eeebf3a6)
* [<span data-ttu-id="1ed9c-117">Redémarrage des instances de service cloud en parallèle, un domaine de mise à niveau à la fois</span><span class="sxs-lookup"><span data-stu-id="1ed9c-117">Rebooting Cloud Service instances in parallel, one upgrade domain at a time</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Reboot-Cloud-Service-PaaS-b337a06d)

## <a name="next-steps"></a><span data-ttu-id="1ed9c-118">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1ed9c-118">Next Steps</span></span>
<span data-ttu-id="1ed9c-119">Maintenant que vous avez appris les notions de base de hello d’Azure Automation et comment il peut être utilisé toomanage services cloud Azure, suivez ces liens de toolearn plus sur Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="1ed9c-119">Now that you've learned hello basics of Azure Automation and how it can be used toomanage Azure cloud services, follow these links toolearn more about Azure Automation.</span></span>

* [<span data-ttu-id="1ed9c-120">Vue d’ensemble de Microsoft Azure Automation</span><span class="sxs-lookup"><span data-stu-id="1ed9c-120">Azure Automation Overview</span></span>](../automation/automation-intro.md)
* [<span data-ttu-id="1ed9c-121">Mon premier Runbook</span><span class="sxs-lookup"><span data-stu-id="1ed9c-121">My first runbook</span></span>](../automation/automation-first-runbook-graphical.md)
* [<span data-ttu-id="1ed9c-122">Plan d’apprentissage pour Azure Automation</span><span class="sxs-lookup"><span data-stu-id="1ed9c-122">Azure Automation learning map</span></span>](https://azure.microsoft.com/documentation/learning-paths/automation/)
