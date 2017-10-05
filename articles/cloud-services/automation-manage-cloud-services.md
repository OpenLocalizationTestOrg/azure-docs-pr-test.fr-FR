---
title: "Gestion d’Azure Cloud Services à l’aide d’Azure Automation | Microsoft Docs"
description: "Découvrez comment le service Azure Automation peut être utilisé pour gérer les services de cloud computing Azure à grande échelle."
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
ms.openlocfilehash: 6b5acac1b8647c324988c316cd5602b3dba98a1d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="managing-azure-cloud-services-using-azure-automation"></a><span data-ttu-id="e42f2-103">Gestion d'Azure Cloud Services à l'aide d'Azure Automation</span><span class="sxs-lookup"><span data-stu-id="e42f2-103">Managing Azure Cloud Services using Azure Automation</span></span>
<span data-ttu-id="e42f2-104">Ce guide vous présente le service Azure Automation et la manière de l'utiliser pour gérer plus simplement vos services de cloud computing Azure.</span><span class="sxs-lookup"><span data-stu-id="e42f2-104">This guide will introduce you to the Azure Automation service, and how it can be used to simplify management of your Azure cloud services.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="e42f2-105">Qu'est-ce qu'Azure Automation ?</span><span class="sxs-lookup"><span data-stu-id="e42f2-105">What is Azure Automation?</span></span>
<span data-ttu-id="e42f2-106">[Azure Automation](https://azure.microsoft.com/services/automation/) est un service Azure destiné à simplifier la gestion du cloud via l'automatisation des processus.</span><span class="sxs-lookup"><span data-stu-id="e42f2-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="e42f2-107">Azure Automation permet d'automatiser les tâches fastidieuses, manuelles, propices aux erreurs et répétitives, afin d'augmenter la fiabilité, l'efficacité et le retour sur investissement pour votre organisation.</span><span class="sxs-lookup"><span data-stu-id="e42f2-107">Using Azure Automation, long-running, manual, error-prone, and frequently repeated tasks can be automated to increase reliability, efficiency, and time to value for your organization.</span></span>

<span data-ttu-id="e42f2-108">Azure Automation fournit un moteur d'exécution de workflow hautement fiable et hautement disponible, qui s'adapte à vos besoins au fur et à mesure que votre entreprise se développe.</span><span class="sxs-lookup"><span data-stu-id="e42f2-108">Azure Automation provides a highly-reliable and highly-available workflow execution engine that scales to meet your needs as your organization grows.</span></span> <span data-ttu-id="e42f2-109">Dans Azure Automation, les processus peuvent être lancés manuellement, par des systèmes tiers ou à des intervalles planifiés, afin que les tâches interviennent exactement au moment opportun.</span><span class="sxs-lookup"><span data-stu-id="e42f2-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="e42f2-110">Réduisez les coûts opérationnels et dégagez du temps pour votre personnel informatique/DevOps afin de lui permettre de se concentrer sur des tâches générant une valeur ajoutée pour l'entreprise, en configurant Azure Automation pour exécuter automatiquement vos tâches de gestion de cloud.</span><span class="sxs-lookup"><span data-stu-id="e42f2-110">Lower operational overhead and free up IT / DevOps staff to focus on work that adds business value by moving your cloud management tasks to be run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-cloud-services"></a><span data-ttu-id="e42f2-111">Comment Azure Automation peut-il aider à gérer des services de cloud computing Azure ?</span><span class="sxs-lookup"><span data-stu-id="e42f2-111">How can Azure Automation help manage Azure cloud services?</span></span>
<span data-ttu-id="e42f2-112">Les services cloud Azure peuvent être gérés dans Azure Automation à l'aide des applets de commande PowerShell qui sont disponibles dans les [outils Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span><span class="sxs-lookup"><span data-stu-id="e42f2-112">Azure cloud services can be managed in Azure Automation by using the PowerShell cmdlets that are available in the [Azure PowerShell tools](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span></span> <span data-ttu-id="e42f2-113">Azure Automation dispose dès le départ de ces applets de commande PowerShell de services de cloud computing, de sorte que vous pouvez effectuer toutes vos tâches de gestion de services de cloud computing au sein du service.</span><span class="sxs-lookup"><span data-stu-id="e42f2-113">Azure Automation has these cloud service PowerShell cmdlets available out of the box, so that you can perform all of your cloud service management tasks within the service.</span></span> <span data-ttu-id="e42f2-114">Dans Azure Automation, vous pouvez également associer ces applets de commande à des applets de commande d'autres services Azure, afin d'automatiser des tâches complexes entre des services Azure et des systèmes tiers.</span><span class="sxs-lookup"><span data-stu-id="e42f2-114">You can also pair these cmdlets in Azure Automation with the cmdlets for other Azure services, to automate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="e42f2-115">Voici quelques exemples qui utilisent Azure Automation pour gérer Azure Cloud Services :</span><span class="sxs-lookup"><span data-stu-id="e42f2-115">Some example uses of Azure Automation to manage Azure Cloud Services include:</span></span>

* [<span data-ttu-id="e42f2-116">Déploiement continu d’un service cloud si cscfg ou cspkg est mis à jour dans Azure Blob Storage</span><span class="sxs-lookup"><span data-stu-id="e42f2-116">Continous deployment of a Cloud Service whenever cscfg or cspkg is updated in Azure Blob storage</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Continuous-Deployment-of-A-eeebf3a6)
* [<span data-ttu-id="e42f2-117">Redémarrage des instances de service cloud en parallèle, un domaine de mise à niveau à la fois</span><span class="sxs-lookup"><span data-stu-id="e42f2-117">Rebooting Cloud Service instances in parallel, one upgrade domain at a time</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Reboot-Cloud-Service-PaaS-b337a06d)

## <a name="next-steps"></a><span data-ttu-id="e42f2-118">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e42f2-118">Next Steps</span></span>
<span data-ttu-id="e42f2-119">Maintenant que vous avez appris les bases d'Azure Automation et la manière de l'utiliser pour gérer les services de cloud computing Azure, cliquez sur ces liens pour en savoir plus sur Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="e42f2-119">Now that you've learned the basics of Azure Automation and how it can be used to manage Azure cloud services, follow these links to learn more about Azure Automation.</span></span>

* [<span data-ttu-id="e42f2-120">Vue d’ensemble de Microsoft Azure Automation</span><span class="sxs-lookup"><span data-stu-id="e42f2-120">Azure Automation Overview</span></span>](../automation/automation-intro.md)
* [<span data-ttu-id="e42f2-121">Mon premier Runbook</span><span class="sxs-lookup"><span data-stu-id="e42f2-121">My first runbook</span></span>](../automation/automation-first-runbook-graphical.md)
* [<span data-ttu-id="e42f2-122">Plan d’apprentissage pour Azure Automation</span><span class="sxs-lookup"><span data-stu-id="e42f2-122">Azure Automation learning map</span></span>](https://azure.microsoft.com/documentation/learning-paths/automation/)
