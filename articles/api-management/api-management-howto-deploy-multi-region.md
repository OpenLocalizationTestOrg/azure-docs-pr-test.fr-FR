---
title: "aaaDeploy gestion des API Azure services toomultiple Azure régions | Documents Microsoft"
description: "Découvrez comment toodeploy une gestion des API Azure service instance toomultiple Azure régions."
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
ms.openlocfilehash: 04a3e762261237d73a769320a21363f99f1d20cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-an-azure-api-management-service-instance-toomultiple-azure-regions"></a><span data-ttu-id="0cc2c-103">Comment toodeploy une gestion des API Azure service instance toomultiple Azure régions</span><span class="sxs-lookup"><span data-stu-id="0cc2c-103">How toodeploy an Azure API Management service instance toomultiple Azure regions</span></span>
<span data-ttu-id="0cc2c-104">Gestion des API prend en charge le déploiement de plusieurs régions, ce qui permet des API éditeurs toodistribute un seul service de gestion des API sur n’importe quel nombre de régions Azure souhaités.</span><span class="sxs-lookup"><span data-stu-id="0cc2c-104">API Management supports multi-region deployment which enables API publishers toodistribute a single API management service across any number of desired Azure regions.</span></span> <span data-ttu-id="0cc2c-105">Ceci permet de réduire la latence de la demande telle qu’elle est perçue par les utilisateurs distribués de l’API. La disponibilité du service est également améliorée si une région est mise hors connexion.</span><span class="sxs-lookup"><span data-stu-id="0cc2c-105">This helps reduce request latency perceived by geographically distributed API consumers and also improves service availability if one region goes offline.</span></span> 

<span data-ttu-id="0cc2c-106">Création d’un service de gestion des API au départ, il contient un seul [unité] [ unit] et se trouve dans une seule région Azure, qui est désignée comme hello région principale.</span><span class="sxs-lookup"><span data-stu-id="0cc2c-106">When an API Management service is created initially, it contains only one [unit][unit] and resides in a single Azure region, which is designated as hello Primary Region.</span></span> <span data-ttu-id="0cc2c-107">Zones supplémentaires peuvent être ajoutées facilement via hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="0cc2c-107">Additional regions can be easily added through hello Azure Portal.</span></span> <span data-ttu-id="0cc2c-108">Un serveur de passerelle de gestion des API est déployé tooeach région et le trafic d’appel est routé toohello les passerelle le plus proche.</span><span class="sxs-lookup"><span data-stu-id="0cc2c-108">An API Management gateway server is deployed tooeach region and call traffic will be routed toohello closest gateway.</span></span> <span data-ttu-id="0cc2c-109">Si une région est mis hors connexion, le trafic de hello est automatiquement redirigée toohello passerelle le plus proche suivant.</span><span class="sxs-lookup"><span data-stu-id="0cc2c-109">If a region goes offline, hello traffic is automatically re-directed toohello next closest gateway.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="0cc2c-110">Déploiement de plusieurs régions est uniquement disponible dans hello  **[Premium] [ Premium]**  couche.</span><span class="sxs-lookup"><span data-stu-id="0cc2c-110">Multi-region deployment is only available in hello **[Premium][Premium]** tier.</span></span>
> 
> 

## <span data-ttu-id="0cc2c-111"><a name="add-region"></a>Déployer une région tooa nouvelle instance du service Gestion des API</span><span class="sxs-lookup"><span data-stu-id="0cc2c-111"><a name="add-region"> </a>Deploy an API Management service instance tooa new region</span></span>
> [!NOTE]
> <span data-ttu-id="0cc2c-112">Si vous n’avez pas encore créé une instance de service de gestion des API, consultez [de créer une instance de service de gestion des API] [ Create an API Management service instance] Bonjour [prise en main Azure API Management] [ Get started with Azure API Management] didacticiel.</span><span class="sxs-lookup"><span data-stu-id="0cc2c-112">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="0cc2c-113">Bonjour portail Azure, accédez toohello **mise à l’échelle et la tarification** page de votre instance de service de gestion des API.</span><span class="sxs-lookup"><span data-stu-id="0cc2c-113">In hello Azure Portal navigate toohello **Scale and pricing** page for your API Management service instance.</span></span> 

![Onglet Mettre à l’échelle][api-management-scale-service]

<span data-ttu-id="0cc2c-115">toodeploy tooa nouvelle zone, cliquez sur **+ ajouter région** à partir de la barre d’outils hello.</span><span class="sxs-lookup"><span data-stu-id="0cc2c-115">toodeploy tooa new region, click on **+ Add region** from hello toolbar.</span></span>

![Ajouter une région][api-management-add-region]

<span data-ttu-id="0cc2c-117">Sélectionnez l’emplacement de hello à partir de la liste déroulante de hello et définir nombre hello d’unités pour avec le curseur de hello.</span><span class="sxs-lookup"><span data-stu-id="0cc2c-117">Select hello location from hello drop-down list and set hello number of units for with hello slider.</span></span>

![Spécifier les unités][api-management-select-location-units]

<span data-ttu-id="0cc2c-119">Cliquez sur **ajouter** tooplace votre sélection dans la table d’emplacements hello.</span><span class="sxs-lookup"><span data-stu-id="0cc2c-119">Click **Add** tooplace your selection in hello Locations table.</span></span> 

<span data-ttu-id="0cc2c-120">Répétez ce processus jusqu'à ce que vous ayez tous les emplacements configurés, puis cliquez sur **enregistrer** hello barre d’outils toostart hello processus de déploiement.</span><span class="sxs-lookup"><span data-stu-id="0cc2c-120">Repeat this process until you have all locations configured and click **Save** from hello toolbar toostart hello deployment process.</span></span>

## <span data-ttu-id="0cc2c-121"><a name="remove-region"></a>Suppression d’une instance de service Gestion des API dans un emplacement</span><span class="sxs-lookup"><span data-stu-id="0cc2c-121"><a name="remove-region"> </a>Delete an API Management service instance from a location</span></span>
<span data-ttu-id="0cc2c-122">Bonjour portail Azure, accédez toohello **mise à l’échelle et la tarification** page de votre instance de service de gestion des API.</span><span class="sxs-lookup"><span data-stu-id="0cc2c-122">In hello Azure Portal navigate toohello **Scale and pricing** page for your API Management service instance.</span></span> 

![Onglet Mettre à l’échelle][api-management-scale-service]

<span data-ttu-id="0cc2c-124">Pour hello emplacement auquel vous tooremove ouvrir le menu contextuel de hello à l’aide de hello **...**  bouton à hello droite de la table de hello.</span><span class="sxs-lookup"><span data-stu-id="0cc2c-124">For hello location you would like tooremove open hello context menu using hello **...** button at hello right end of hello table.</span></span> <span data-ttu-id="0cc2c-125">Sélectionnez hello **supprimer** option.</span><span class="sxs-lookup"><span data-stu-id="0cc2c-125">Select hello **Delete** option.</span></span>

![Supprimer la région][api-management-remove-region]

<span data-ttu-id="0cc2c-127">Confirmer la suppression de hello et cliquez sur **enregistrer** modifications de hello tooapply.</span><span class="sxs-lookup"><span data-stu-id="0cc2c-127">Confirm hello deletion and click **Save** tooapply hello changes.</span></span>

[api-management-management-console]: ./media/api-management-howto-deploy-multi-region/api-management-management-console.png

[api-management-scale-service]: ./media/api-management-howto-deploy-multi-region/api-management-scale-service.png
[api-management-add-region]: ./media/api-management-howto-deploy-multi-region/api-management-add-region.png
[api-management-select-location-units]: ./media/api-management-howto-deploy-multi-region/api-management-select-location-units.png
[api-management-remove-region]: ./media/api-management-howto-deploy-multi-region/api-management-remove-region.png

[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Get started with Azure API Management]: api-management-get-started.md

[Deploy an API Management service instance tooa new region]: #add-region
[Delete an API Management service instance from a region]: #remove-region

[unit]: http://azure.microsoft.com/pricing/details/api-management/
[Premium]: http://azure.microsoft.com/pricing/details/api-management/

