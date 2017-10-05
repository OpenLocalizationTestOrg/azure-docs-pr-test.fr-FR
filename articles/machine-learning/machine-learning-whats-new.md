---
title: "Nouveautés dans Azure Machine Learning | Microsoft Docs"
description: "De nouvelles fonctionnalités sont disponibles dans Microsoft Azure Learning."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: ddc716ed-2615-4806-bf27-6c9a5662a7f2
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/28/2017
ms.author: v-donglo
ms.openlocfilehash: 551b977b90612ddbfa1514a9c2358ebf8179c385
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="whats-new-in-azure-machine-learning"></a><span data-ttu-id="45c17-103">Nouveautés dans Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="45c17-103">What's New in Azure Machine Learning</span></span>

### <a name="the-march-2017-release-of-microsoft-azure-machine-learning-updates-provides-the-following-feature"></a><span data-ttu-id="45c17-104">La mise à jour de mars 2017 de Microsoft Azure Machine Learning inclut la fonctionnalité suivante :</span><span class="sxs-lookup"><span data-stu-id="45c17-104">The March 2017 release of Microsoft Azure Machine Learning updates provides the following feature:</span></span>



* <span data-ttu-id="45c17-105">Capacité dédiée pour les travaux du service d’exécution de lot d’Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="45c17-105">Dedicated Capacity for Azure Machine Learning BES Jobs</span></span>

    <span data-ttu-id="45c17-106">Le traitement par pool Batch de Machine Learning utilise le [service Azure Batch](../batch/batch-technical-overview.md) pour fournir une échelle gérée par le client pour le service d’exécution de lot d’Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="45c17-106">Machine Learning Batch Pool processing uses the [Azure Batch](../batch/batch-technical-overview.md) service to provide customer-managed scale for the Azure Machine Learning Batch Execution Service.</span></span> <span data-ttu-id="45c17-107">Le traitement par pool Batch vous permet de créer des pools Azure Batch, dans lesquels vous pouvez soumettre des travaux par lots, en vous assurant qu’ils s’exécutent de manière prévisible.</span><span class="sxs-lookup"><span data-stu-id="45c17-107">Batch Pool processing allows you to create Azure Batch pools on which you can submit batch jobs and have them execute in a predictable manner.</span></span>

    <span data-ttu-id="45c17-108">Pour en savoir plus, voir [Service Azure Batch pour les travaux Machine Learning](machine-learning-dedicated-capacity-for-bes-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="45c17-108">For more information, see [Azure Batch service for Machine Learning jobs](machine-learning-dedicated-capacity-for-bes-jobs.md).</span></span>


### <a name="the-august-2016-release-of-microsoft-azure-machine-learning-updates-provide-the-following-features"></a><span data-ttu-id="45c17-109">La mise à jour d’août 2016 de Microsoft Azure Machine Learning inclut les fonctionnalités suivantes :</span><span class="sxs-lookup"><span data-stu-id="45c17-109">The August 2016 release of Microsoft Azure Machine Learning updates provide the following features:</span></span>
* <span data-ttu-id="45c17-110">Vous pouvez désormais gérer Les services web Machine via le nouveau portail [Services web Microsoft Azure Machine Learning](https://services.azureml.net/) qui fournit un emplacement pour gérer tous les aspects de votre service web.</span><span class="sxs-lookup"><span data-stu-id="45c17-110">Classic Web services can now be managed in the new [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/) portal that provides one place to manage all aspects of your Web service.</span></span>    
  * <span data-ttu-id="45c17-111">Fournit des [statistiques d’utilisation](machine-learning-manage-new-webservice.md) du service web.</span><span class="sxs-lookup"><span data-stu-id="45c17-111">Which provides web service [usage statistics](machine-learning-manage-new-webservice.md).</span></span>
  * <span data-ttu-id="45c17-112">Simplifie le test des appels de demande distante d’Azure Machine Learning à l’aide d’exemples de données.</span><span class="sxs-lookup"><span data-stu-id="45c17-112">Simplifies testing of Azure Machine Learning Remote-Request calls using sample data.</span></span>
  * <span data-ttu-id="45c17-113">Fournit une nouvelle page de test de service d’exécution de lot avec des exemples de données et un historique des travaux soumis.</span><span class="sxs-lookup"><span data-stu-id="45c17-113">Provides a new Batch Execution Service test page with sample data and job submission history.</span></span>
  * <span data-ttu-id="45c17-114">Fournit une gestion de point de terminaison simplifiée.</span><span class="sxs-lookup"><span data-stu-id="45c17-114">Provides easier endpoint management.</span></span>

### <a name="the-july-2016-release-of-microsoft-azure-machine-learning-updates-provide-the-following-features"></a><span data-ttu-id="45c17-115">La mise à jour de juillet 2016 de Microsoft Azure Machine Learning inclut les fonctionnalités suivantes :</span><span class="sxs-lookup"><span data-stu-id="45c17-115">The July 2016 release of Microsoft Azure Machine Learning updates provide the following features:</span></span>
* <span data-ttu-id="45c17-116">Les services web sont désormais gérés en tant que ressources Azure via les interfaces [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) , ce qui permet les améliorations suivantes :</span><span class="sxs-lookup"><span data-stu-id="45c17-116">Web services are now managed as Azure resources managed through [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) interfaces, allowing for the following enhancements:</span></span>
  * <span data-ttu-id="45c17-117">De nouvelles [API REST](https://msdn.microsoft.com/library/azure/Dn950030.aspx) pour déployer et gérer vos services web basés sur Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="45c17-117">There are new [REST APIs](https://msdn.microsoft.com/library/azure/Dn950030.aspx) to deploy and manage your Resource Manager based Web services.</span></span>
  * <span data-ttu-id="45c17-118">Un nouveau portail [Services web Microsoft Azure Machine Learning](https://services.azureml.net/) qui fournit un emplacement pour gérer tous les aspects de votre service web.</span><span class="sxs-lookup"><span data-stu-id="45c17-118">There is a new [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/) portal that provides one place to manage all aspects of your Web service.</span></span>
* <span data-ttu-id="45c17-119">Intègre un nouveau modèle de déploiement de service web multi-régions et basé sur un abonnement, qui utilise des API basées sur Resource Manager afin d’exploiter le fournisseur de ressources Resource Manager pour les services web.</span><span class="sxs-lookup"><span data-stu-id="45c17-119">Incorporates a new subscription-based, multi-region web service deployment model using Resource Manager based APIs leveraging the Resource Manager Resource Provider for Web Services.</span></span>
* <span data-ttu-id="45c17-120">Présente de nouveaux [plans de tarification](https://azure.microsoft.com/pricing/details/machine-learning/) et des capacités de gestion en utilisant le nouveau fournisseur de ressources Resource Manager pour la facturation.</span><span class="sxs-lookup"><span data-stu-id="45c17-120">Introduces new [pricing plans](https://azure.microsoft.com/pricing/details/machine-learning/) and plan management capabilities using the new Resource Manager RP for Billing.</span></span>
  * <span data-ttu-id="45c17-121">Vous pouvez à présent [déployer votre service web dans plusieurs régions](machine-learning-how-to-deploy-to-multiple-regions.md) sans avoir à créer un abonnement dans chaque région.</span><span class="sxs-lookup"><span data-stu-id="45c17-121">You can now [deploy your web service to multiple regions](machine-learning-how-to-deploy-to-multiple-regions.md) without needing to create a subscription in each region.</span></span>
* <span data-ttu-id="45c17-122">Fournit des [statistiques d’utilisation](machine-learning-manage-new-webservice.md)du service web.</span><span class="sxs-lookup"><span data-stu-id="45c17-122">Provides web service [usage statistics](machine-learning-manage-new-webservice.md).</span></span>
* <span data-ttu-id="45c17-123">Simplifie le test des appels de demande distante d’Azure Machine Learning à l’aide d’exemples de données.</span><span class="sxs-lookup"><span data-stu-id="45c17-123">Simplifies testing of Azure Machine Learning Remote-Request calls using sample data.</span></span>
* <span data-ttu-id="45c17-124">Fournit une nouvelle page de test de service d’exécution de lot avec des exemples de données et un historique des travaux soumis.</span><span class="sxs-lookup"><span data-stu-id="45c17-124">Provides a new Batch Execution Service test page with sample data and job submission history.</span></span>

<span data-ttu-id="45c17-125">En outre, Machine Learning Studio a été mis à jour afin que vous puissiez déployer vers le nouveau modèle de service web ou continuer à déployer vers le modèle de service web classique.</span><span class="sxs-lookup"><span data-stu-id="45c17-125">In addition, the Machine Learning Studio has been updated to allow you to deploy to the new Web service model or continue to deploy to the classic Web service model.</span></span> 

