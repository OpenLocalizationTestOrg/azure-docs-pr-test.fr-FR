---
title: "référentiels de Registre de conteneur aaaAzure | Documents Microsoft"
description: "Comment toouse les référentiels de Registre de conteneur Azure pour les images de Docker"
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
ms.openlocfilehash: 06172a63465838a78a607f268da116d8158789ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-registry-repositories"></a><span data-ttu-id="af475-103">Référentiels Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="af475-103">Azure container registry repositories</span></span>

<span data-ttu-id="af475-104">Les référentiels Azure Container Registry sont compatibles avec une multitude de services et d’orchestrators.</span><span class="sxs-lookup"><span data-stu-id="af475-104">Azure Container Registries are compatible with a multitude of services and orchestrators.</span></span> <span data-ttu-id="af475-105">toomake il services de source de hello tootrack plus faciles et les agents à partir de laquelle l’ACR est utilisé, nous avons démarré à l’aide du champ d’en-tête hello Docker dans le fichier de Docker.config hello.</span><span class="sxs-lookup"><span data-stu-id="af475-105">toomake it easier tootrack hello source services and agents from which ACR is used, we have started using hello Docker header field in hello Docker.config file.</span></span>



## <a name="viewing-repositories-in-hello-portal"></a><span data-ttu-id="af475-106">Affichage des référentiels dans hello portail</span><span class="sxs-lookup"><span data-stu-id="af475-106">Viewing repositories in hello Portal</span></span>

<span data-ttu-id="af475-107">en-têtes d’ACR Hello suivent le format de hello :</span><span class="sxs-lookup"><span data-stu-id="af475-107">hello ACR headers follow hello format:</span></span>
```
X-Meta-Source-Client: <cloud>/<service>/<optionalservicename>
```

* <span data-ttu-id="af475-108">Cloud : Azure, Azure Stack ou tout autre cloud Azure propre au secteur public ou à un pays.</span><span class="sxs-lookup"><span data-stu-id="af475-108">Cloud: Azure, Azure Stack, or other government or country-specific Azure clouds.</span></span> <span data-ttu-id="af475-109">Même si Azure Stack et les clouds pour le secteur public ne sont actuellement pas pris en charge, ce paramètre permet d’envisager une prise en charge future.</span><span class="sxs-lookup"><span data-stu-id="af475-109">Although Azure Stack and government clouds are not currently supported, this parameter enables future support.</span></span>
* <span data-ttu-id="af475-110">Service : le nom du service de hello.</span><span class="sxs-lookup"><span data-stu-id="af475-110">Service: name of hello service.</span></span>
* <span data-ttu-id="af475-111">Optionalservicename : le paramètre facultatif pour les services avec sous-Services ou toospecify une référence SKU (ex : les applications web correspondent à Azure /-applications app service/web).</span><span class="sxs-lookup"><span data-stu-id="af475-111">Optionalservicename: optional parameter for services with subservices, or toospecify a SKU (ex: web apps correspond with Azure/app-service/web-apps).</span></span>

<span data-ttu-id="af475-112">Orchestrators et services des partenaires sont encouragés toouse en-tête spécifique valeurs toohelp avec nos données de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="af475-112">Partner services and orchestrators are encouraged toouse specific header values toohelp with our telemetry.</span></span> <span data-ttu-id="af475-113">Les utilisateurs peuvent également modifier valeur hello transmis toohello en-tête s’ils le souhaitent.</span><span class="sxs-lookup"><span data-stu-id="af475-113">Users can also modify hello value passed toohello header if they so desire.</span></span>

<span data-ttu-id="af475-114">les valeurs Hello vous souhaitez ACR partenaires toouse toopopulate hello « X-Meta-Source-Client » champ sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="af475-114">hello values we want ACR partners toouse toopopulate hello "X-Meta-Source-Client" field are below:</span></span>

| <span data-ttu-id="af475-115">Nom du service</span><span class="sxs-lookup"><span data-stu-id="af475-115">Service Name</span></span>              | <span data-ttu-id="af475-116">En-tête</span><span class="sxs-lookup"><span data-stu-id="af475-116">Header</span></span>                                |
| ------------------------- | ------------------------------------- |
| <span data-ttu-id="af475-117">Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="af475-117">Azure Container Service</span></span>   | <span data-ttu-id="af475-118">azure/compute/azure-container-service</span><span class="sxs-lookup"><span data-stu-id="af475-118">azure/compute/azure-container-service</span></span> |
| <span data-ttu-id="af475-119">App Service - Web Apps</span><span class="sxs-lookup"><span data-stu-id="af475-119">App Service - Web Apps</span></span>    | <span data-ttu-id="af475-120">azure/app-service/web-apps</span><span class="sxs-lookup"><span data-stu-id="af475-120">azure/app-service/web-apps</span></span>            |
| <span data-ttu-id="af475-121">App Service - Logic Apps</span><span class="sxs-lookup"><span data-stu-id="af475-121">App Service - Logic Apps</span></span>  | <span data-ttu-id="af475-122">azure/app-service/logic-apps</span><span class="sxs-lookup"><span data-stu-id="af475-122">azure/app-service/logic-apps</span></span>          |
| <span data-ttu-id="af475-123">Batch</span><span class="sxs-lookup"><span data-stu-id="af475-123">Batch</span></span>                     | <span data-ttu-id="af475-124">azure/compute/batch</span><span class="sxs-lookup"><span data-stu-id="af475-124">azure/compute/batch</span></span>                   |
| <span data-ttu-id="af475-125">Cloud Console</span><span class="sxs-lookup"><span data-stu-id="af475-125">Cloud Console</span></span>             | <span data-ttu-id="af475-126">azure/cloud-console</span><span class="sxs-lookup"><span data-stu-id="af475-126">azure/cloud-console</span></span>                   |
| <span data-ttu-id="af475-127">Functions</span><span class="sxs-lookup"><span data-stu-id="af475-127">Functions</span></span>                 | <span data-ttu-id="af475-128">azure/compute/functions</span><span class="sxs-lookup"><span data-stu-id="af475-128">azure/compute/functions</span></span>               |
| <span data-ttu-id="af475-129">Internet des objets - Hub</span><span class="sxs-lookup"><span data-stu-id="af475-129">Internet of Things - Hub</span></span>  | <span data-ttu-id="af475-130">azure/iot/hub</span><span class="sxs-lookup"><span data-stu-id="af475-130">azure/iot/hub</span></span>                         |
| <span data-ttu-id="af475-131">HDInsight</span><span class="sxs-lookup"><span data-stu-id="af475-131">HDInsight</span></span>                 | <span data-ttu-id="af475-132">azure/data/hdinsight</span><span class="sxs-lookup"><span data-stu-id="af475-132">azure/data/hdinsight</span></span>                  |
| <span data-ttu-id="af475-133">Jenkins</span><span class="sxs-lookup"><span data-stu-id="af475-133">Jenkins</span></span>                   | <span data-ttu-id="af475-134">azure/jenkins</span><span class="sxs-lookup"><span data-stu-id="af475-134">azure/jenkins</span></span>                         |
| <span data-ttu-id="af475-135">Machine Learning</span><span class="sxs-lookup"><span data-stu-id="af475-135">Machine Learning</span></span>          | <span data-ttu-id="af475-136">azure/data/machile-learning</span><span class="sxs-lookup"><span data-stu-id="af475-136">azure/data/machile-learning</span></span>           |
| <span data-ttu-id="af475-137">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="af475-137">Service Fabric</span></span>            | <span data-ttu-id="af475-138">azure/compute/service-fabric</span><span class="sxs-lookup"><span data-stu-id="af475-138">azure/compute/service-fabric</span></span>          |
| <span data-ttu-id="af475-139">VSTS</span><span class="sxs-lookup"><span data-stu-id="af475-139">VSTS</span></span>                      | <span data-ttu-id="af475-140">azure/vsts</span><span class="sxs-lookup"><span data-stu-id="af475-140">azure/vsts</span></span>                            |


## <a name="next-steps"></a><span data-ttu-id="af475-141">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="af475-141">Next steps</span></span>
[<span data-ttu-id="af475-142">En savoir plus sur les registres et hello pris en charge les services et orchestrators</span><span class="sxs-lookup"><span data-stu-id="af475-142">Learn more about registries and hello supported services and orchestrators</span></span>](container-registry-intro.md)
