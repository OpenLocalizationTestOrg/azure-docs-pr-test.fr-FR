---
title: "Créer des référentiels Azure Container Registry | Microsoft Docs"
description: "Utiliser des référentiels Azure Container Registry pour gérer des images Docker"
services: container-registry
documentationcenter: 
author: cristy
manager: balans
editor: dlepow
ms.service: container-registry
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/22/2017
ms.author: cristyg
ms.openlocfilehash: dd4feff057269ed7106990bb63eed7fcffa2dbec
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-container-registry-repositories"></a><span data-ttu-id="4d9cb-103">Référentiels Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="4d9cb-103">Azure container registry repositories</span></span>

<span data-ttu-id="4d9cb-104">Les référentiels Azure Container Registry sont compatibles avec une multitude de services et d’orchestrators.</span><span class="sxs-lookup"><span data-stu-id="4d9cb-104">Azure Container Registries are compatible with a multitude of services and orchestrators.</span></span> <span data-ttu-id="4d9cb-105">Pour faciliter le suivi des services et des agents sources à partir desquels l’ACR est utilisé, nous avons commencé par utiliser le champ d’en-tête Docker dans le fichier Docker.config.</span><span class="sxs-lookup"><span data-stu-id="4d9cb-105">To make it easier to track the source services and agents from which ACR is used, we have started using the Docker header field in the Docker.config file.</span></span>



## <a name="viewing-repositories-in-the-portal"></a><span data-ttu-id="4d9cb-106">Affichage de référentiels dans le portail</span><span class="sxs-lookup"><span data-stu-id="4d9cb-106">Viewing repositories in the Portal</span></span>

<span data-ttu-id="4d9cb-107">Les en-têtes ACR présentent le format suivant :</span><span class="sxs-lookup"><span data-stu-id="4d9cb-107">The ACR headers follow the format:</span></span>
```
X-Meta-Source-Client: <cloud>/<service>/<optionalservicename>
```

* <span data-ttu-id="4d9cb-108">Cloud : Azure, Azure Stack ou tout autre cloud Azure propre au secteur public ou à un pays.</span><span class="sxs-lookup"><span data-stu-id="4d9cb-108">Cloud: Azure, Azure Stack, or other government or country-specific Azure clouds.</span></span> <span data-ttu-id="4d9cb-109">Même si Azure Stack et les clouds pour le secteur public ne sont actuellement pas pris en charge, ce paramètre permet d’envisager une prise en charge future.</span><span class="sxs-lookup"><span data-stu-id="4d9cb-109">Although Azure Stack and government clouds are not currently supported, this parameter enables future support.</span></span>
* <span data-ttu-id="4d9cb-110">Service : nom du service.</span><span class="sxs-lookup"><span data-stu-id="4d9cb-110">Service: name of the service.</span></span>
* <span data-ttu-id="4d9cb-111">Optionalservicename : paramètre facultatif pour les services comprenant des sous-services ou pour spécifier une référence SKU (ex : les applications web correspondent à Azure/app-service/web-apps).</span><span class="sxs-lookup"><span data-stu-id="4d9cb-111">Optionalservicename: optional parameter for services with subservices, or to specify a SKU (ex: web apps correspond with Azure/app-service/web-apps).</span></span>

<span data-ttu-id="4d9cb-112">Les services et orchestrators partenaires sont encouragés à utiliser des valeurs d’en-tête spécifiques pour faciliter notre télémétrie.</span><span class="sxs-lookup"><span data-stu-id="4d9cb-112">Partner services and orchestrators are encouraged to use specific header values to help with our telemetry.</span></span> <span data-ttu-id="4d9cb-113">S’ils le souhaitent, les utilisateurs peuvent aussi modifier la valeur passée à l’en-tête.</span><span class="sxs-lookup"><span data-stu-id="4d9cb-113">Users can also modify the value passed to the header if they so desire.</span></span>

<span data-ttu-id="4d9cb-114">Les valeurs que nous souhaitons que les partenaires ACR utilisent pour remplir le champ « X-Meta-Source-Client » sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="4d9cb-114">The values we want ACR partners to use to populate the "X-Meta-Source-Client" field are below:</span></span>

| <span data-ttu-id="4d9cb-115">Nom du service</span><span class="sxs-lookup"><span data-stu-id="4d9cb-115">Service Name</span></span>              | <span data-ttu-id="4d9cb-116">En-tête</span><span class="sxs-lookup"><span data-stu-id="4d9cb-116">Header</span></span>                                |
| ------------------------- | ------------------------------------- |
| <span data-ttu-id="4d9cb-117">Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="4d9cb-117">Azure Container Service</span></span>   | <span data-ttu-id="4d9cb-118">azure/compute/azure-container-service</span><span class="sxs-lookup"><span data-stu-id="4d9cb-118">azure/compute/azure-container-service</span></span> |
| <span data-ttu-id="4d9cb-119">App Service - Web Apps</span><span class="sxs-lookup"><span data-stu-id="4d9cb-119">App Service - Web Apps</span></span>    | <span data-ttu-id="4d9cb-120">azure/app-service/web-apps</span><span class="sxs-lookup"><span data-stu-id="4d9cb-120">azure/app-service/web-apps</span></span>            |
| <span data-ttu-id="4d9cb-121">App Service - Logic Apps</span><span class="sxs-lookup"><span data-stu-id="4d9cb-121">App Service - Logic Apps</span></span>  | <span data-ttu-id="4d9cb-122">azure/app-service/logic-apps</span><span class="sxs-lookup"><span data-stu-id="4d9cb-122">azure/app-service/logic-apps</span></span>          |
| <span data-ttu-id="4d9cb-123">Batch</span><span class="sxs-lookup"><span data-stu-id="4d9cb-123">Batch</span></span>                     | <span data-ttu-id="4d9cb-124">azure/compute/batch</span><span class="sxs-lookup"><span data-stu-id="4d9cb-124">azure/compute/batch</span></span>                   |
| <span data-ttu-id="4d9cb-125">Cloud Console</span><span class="sxs-lookup"><span data-stu-id="4d9cb-125">Cloud Console</span></span>             | <span data-ttu-id="4d9cb-126">azure/cloud-console</span><span class="sxs-lookup"><span data-stu-id="4d9cb-126">azure/cloud-console</span></span>                   |
| <span data-ttu-id="4d9cb-127">Functions</span><span class="sxs-lookup"><span data-stu-id="4d9cb-127">Functions</span></span>                 | <span data-ttu-id="4d9cb-128">azure/compute/functions</span><span class="sxs-lookup"><span data-stu-id="4d9cb-128">azure/compute/functions</span></span>               |
| <span data-ttu-id="4d9cb-129">Internet des objets - Hub</span><span class="sxs-lookup"><span data-stu-id="4d9cb-129">Internet of Things - Hub</span></span>  | <span data-ttu-id="4d9cb-130">azure/iot/hub</span><span class="sxs-lookup"><span data-stu-id="4d9cb-130">azure/iot/hub</span></span>                         |
| <span data-ttu-id="4d9cb-131">HDInsight</span><span class="sxs-lookup"><span data-stu-id="4d9cb-131">HDInsight</span></span>                 | <span data-ttu-id="4d9cb-132">azure/data/hdinsight</span><span class="sxs-lookup"><span data-stu-id="4d9cb-132">azure/data/hdinsight</span></span>                  |
| <span data-ttu-id="4d9cb-133">Jenkins</span><span class="sxs-lookup"><span data-stu-id="4d9cb-133">Jenkins</span></span>                   | <span data-ttu-id="4d9cb-134">azure/jenkins</span><span class="sxs-lookup"><span data-stu-id="4d9cb-134">azure/jenkins</span></span>                         |
| <span data-ttu-id="4d9cb-135">Machine Learning</span><span class="sxs-lookup"><span data-stu-id="4d9cb-135">Machine Learning</span></span>          | <span data-ttu-id="4d9cb-136">azure/data/machile-learning</span><span class="sxs-lookup"><span data-stu-id="4d9cb-136">azure/data/machile-learning</span></span>           |
| <span data-ttu-id="4d9cb-137">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="4d9cb-137">Service Fabric</span></span>            | <span data-ttu-id="4d9cb-138">azure/compute/service-fabric</span><span class="sxs-lookup"><span data-stu-id="4d9cb-138">azure/compute/service-fabric</span></span>          |
| <span data-ttu-id="4d9cb-139">VSTS</span><span class="sxs-lookup"><span data-stu-id="4d9cb-139">VSTS</span></span>                      | <span data-ttu-id="4d9cb-140">azure/vsts</span><span class="sxs-lookup"><span data-stu-id="4d9cb-140">azure/vsts</span></span>                            |


## <a name="next-steps"></a><span data-ttu-id="4d9cb-141">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4d9cb-141">Next steps</span></span>
[<span data-ttu-id="4d9cb-142">En savoir plus sur les registres et les services et orchestrators pris en charge</span><span class="sxs-lookup"><span data-stu-id="4d9cb-142">Learn more about registries and the supported services and orchestrators</span></span>](container-registry-intro.md)
