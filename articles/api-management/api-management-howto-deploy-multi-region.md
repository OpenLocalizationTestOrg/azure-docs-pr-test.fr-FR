---
title: "Déployer des services Gestion des API Azure sur plusieurs régions Azure | Microsoft Docs"
description: "Découvrez comment déployer une instance de service Gestion des API Azure dans plusieurs régions Azure."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 47389ad6-f865-4706-833f-846115e22e4d
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 1c39fee739c2f5fd4b928e1e76e1ea57f072b5f8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-deploy-an-azure-api-management-service-instance-to-multiple-azure-regions"></a><span data-ttu-id="91a94-103">Comment déployer une instance de service Gestion des API Azure dans plusieurs régions Azure</span><span class="sxs-lookup"><span data-stu-id="91a94-103">How to deploy an Azure API Management service instance to multiple Azure regions</span></span>
<span data-ttu-id="91a94-104">Gestion des API prend en charge le déploiement sur plusieurs régions, ce qui permet aux éditeurs d’API de ne distribuer qu’un seul service Gestion des API sur le nombre de régions Azure.</span><span class="sxs-lookup"><span data-stu-id="91a94-104">API Management supports multi-region deployment which enables API publishers to distribute a single API management service across any number of desired Azure regions.</span></span> <span data-ttu-id="91a94-105">Ceci permet de réduire la latence de la demande telle qu’elle est perçue par les utilisateurs distribués de l’API. La disponibilité du service est également améliorée si une région est mise hors connexion.</span><span class="sxs-lookup"><span data-stu-id="91a94-105">This helps reduce request latency perceived by geographically distributed API consumers and also improves service availability if one region goes offline.</span></span> 

<span data-ttu-id="91a94-106">Lors de la création initiale du service Gestion des API, il ne contient qu’une seule [unité][unit] et se trouve dans une seule région Azure, désignée comme région primaire.</span><span class="sxs-lookup"><span data-stu-id="91a94-106">When an API Management service is created initially, it contains only one [unit][unit] and resides in a single Azure region, which is designated as the Primary Region.</span></span> <span data-ttu-id="91a94-107">D’autres régions peuvent être facilement ajoutées via le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="91a94-107">Additional regions can be easily added through the Azure Portal.</span></span> <span data-ttu-id="91a94-108">Un serveur de passerelle Gestion des API est déployé dans chaque région et le trafic d’appel est acheminé vers la passerelle la plus proche.</span><span class="sxs-lookup"><span data-stu-id="91a94-108">An API Management gateway server is deployed to each region and call traffic will be routed to the closest gateway.</span></span> <span data-ttu-id="91a94-109">Si une région est déconnectée, le trafic est automatiquement redirigé vers la passerelle suivante la plus proche.</span><span class="sxs-lookup"><span data-stu-id="91a94-109">If a region goes offline, the traffic is automatically re-directed to the next closest gateway.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="91a94-110">Le déploiement multi-régions est disponible uniquement dans le niveau **[Premium][Premium]**.</span><span class="sxs-lookup"><span data-stu-id="91a94-110">Multi-region deployment is only available in the **[Premium][Premium]** tier.</span></span>
> 
> 

## <span data-ttu-id="91a94-111"><a name="add-region"> </a>Déploiement d’une instance de service Gestion des API sur une nouvelle région</span><span class="sxs-lookup"><span data-stu-id="91a94-111"><a name="add-region"> </a>Deploy an API Management service instance to a new region</span></span>
> [!NOTE]
> <span data-ttu-id="91a94-112">Si vous n’avez pas encore créé une instance de service Gestion des API, consultez la page de [création d’une instance de service Gestion des API][Create an API Management service instance] dans le didacticiel de [prise en main de Gestion des API Azure][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="91a94-112">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="91a94-113">Dans le portail Azure, accédez à la page **Scale and pricing (Échelle et tarification)** de votre instance du service Gestion des API.</span><span class="sxs-lookup"><span data-stu-id="91a94-113">In the Azure Portal navigate to the **Scale and pricing** page for your API Management service instance.</span></span> 

![Onglet Mettre à l’échelle][api-management-scale-service]

<span data-ttu-id="91a94-115">Pour procéder au déploiement vers une nouvelle région, cliquez sur **+ Ajouter une région** dans la barre d’outils.</span><span class="sxs-lookup"><span data-stu-id="91a94-115">To deploy to a new region, click on **+ Add region** from the toolbar.</span></span>

![Ajouter une région][api-management-add-region]

<span data-ttu-id="91a94-117">Sélectionnez l’emplacement dans la liste déroulante et définissez le nombre d’unités à l’aide du curseur.</span><span class="sxs-lookup"><span data-stu-id="91a94-117">Select the location from the drop-down list and set the number of units for with the slider.</span></span>

![Spécifier les unités][api-management-select-location-units]

<span data-ttu-id="91a94-119">Cliquez sur **Ajouter** pour placer votre sélection dans la table des emplacements.</span><span class="sxs-lookup"><span data-stu-id="91a94-119">Click **Add** to place your selection in the Locations table.</span></span> 

<span data-ttu-id="91a94-120">Répétez cette procédure jusqu’à ce que vous ayez configuré tous les emplacements, puis cliquez sur **Enregistrer** dans la barre d’outils pour démarrer le déploiement.</span><span class="sxs-lookup"><span data-stu-id="91a94-120">Repeat this process until you have all locations configured and click **Save** from the toolbar to start the deployment process.</span></span>

## <span data-ttu-id="91a94-121"><a name="remove-region"> </a>Suppression d’une instance de service Gestion des API dans un emplacement</span><span class="sxs-lookup"><span data-stu-id="91a94-121"><a name="remove-region"> </a>Delete an API Management service instance from a location</span></span>
<span data-ttu-id="91a94-122">Dans le portail Azure, accédez à la page **Scale and pricing (Échelle et tarification)** de votre instance du service Gestion des API.</span><span class="sxs-lookup"><span data-stu-id="91a94-122">In the Azure Portal navigate to the **Scale and pricing** page for your API Management service instance.</span></span> 

![Onglet Mettre à l’échelle][api-management-scale-service]

<span data-ttu-id="91a94-124">Pour l’emplacement que vous souhaitez supprimer, ouvrez le menu contextuel à l’aide du bouton **...** situé à l’extrême droite du tableau.</span><span class="sxs-lookup"><span data-stu-id="91a94-124">For the location you would like to remove open the context menu using the **...** button at the right end of the table.</span></span> <span data-ttu-id="91a94-125">Sélectionnez l’option **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="91a94-125">Select the **Delete** option.</span></span>

![Supprimer la région][api-management-remove-region]

<span data-ttu-id="91a94-127">Confirmez la suppression, puis cliquez sur **Enregistrer** pour appliquer les modifications.</span><span class="sxs-lookup"><span data-stu-id="91a94-127">Confirm the deletion and click **Save** to apply the changes.</span></span>

[api-management-management-console]: ./media/api-management-howto-deploy-multi-region/api-management-management-console.png

[api-management-scale-service]: ./media/api-management-howto-deploy-multi-region/api-management-scale-service.png
[api-management-add-region]: ./media/api-management-howto-deploy-multi-region/api-management-add-region.png
[api-management-select-location-units]: ./media/api-management-howto-deploy-multi-region/api-management-select-location-units.png
[api-management-remove-region]: ./media/api-management-howto-deploy-multi-region/api-management-remove-region.png

[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Get started with Azure API Management]: api-management-get-started.md

[Deploy an API Management service instance to a new region]: #add-region
[Delete an API Management service instance from a region]: #remove-region

[unit]: http://azure.microsoft.com/pricing/details/api-management/
[Premium]: http://azure.microsoft.com/pricing/details/api-management/

