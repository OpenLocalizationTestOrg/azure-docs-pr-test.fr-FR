---
title: "vue d’ensemble des Services de support aaaAzure | Documents Microsoft"
description: Cette rubrique offre une vue d'ensemble d'Azure Media Services
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 7a5e9723-c379-446b-b4d6-d0e41bd7d31f
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/04/2017
ms.author: juliako;anilmur
ms.openlocfilehash: 81f9f4d9ff75effea30c10fd09449e9d2025f377
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-media-services-overview"></a><span data-ttu-id="56b64-103">Vue d’ensemble d’Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="56b64-103">Azure Media Services overview</span></span> 

<span data-ttu-id="56b64-104">Microsoft Azure Media Services est une plateforme cloud extensible qui permet aux développeurs toobuild de contenu multimédia évolutives gestion et remise applications.</span><span class="sxs-lookup"><span data-stu-id="56b64-104">Microsoft Azure Media Services is an extensible cloud-based platform that enables developers toobuild scalable media management and delivery applications.</span></span> <span data-ttu-id="56b64-105">Media Services est basé sur les API REST qui vous permettent de téléchargement de toosecurely, stocker, encoder et empaqueter le contenu vidéo ou audio pour la demande et live diffusion en continu remise toovarious les clients (par exemple, TV, PC et appareils mobiles).</span><span class="sxs-lookup"><span data-stu-id="56b64-105">Media Services is based on REST APIs that enable you toosecurely upload, store, encode, and package video or audio content for both on-demand and live streaming delivery toovarious clients (for example, TV, PC, and mobile devices).</span></span>

<span data-ttu-id="56b64-106">Vous pouvez créer des flux de travail de bout en bout en utilisant uniquement Media Services.</span><span class="sxs-lookup"><span data-stu-id="56b64-106">You can build end-to-end workflows using entirely Media Services.</span></span> <span data-ttu-id="56b64-107">Vous pouvez également choisir toouse des composants tiers pour certaines parties de votre flux de travail.</span><span class="sxs-lookup"><span data-stu-id="56b64-107">You can also choose toouse third-party components for some parts of your workflow.</span></span> <span data-ttu-id="56b64-108">(par exemple, en encodant avec un encodeur tiers).</span><span class="sxs-lookup"><span data-stu-id="56b64-108">For example, encode using a third-party encoder.</span></span> <span data-ttu-id="56b64-109">Le contenu est ensuite téléchargé, protégé, empaqueté et remis à l'aide de Media Services.</span><span class="sxs-lookup"><span data-stu-id="56b64-109">Then, upload, protect, package, deliver using Media Services.</span></span>

<span data-ttu-id="56b64-110">Vous pouvez choisir toostream votre contenu en direct ou fournir le contenu à la demande.</span><span class="sxs-lookup"><span data-stu-id="56b64-110">You can choose toostream your content live or deliver content on-demand.</span></span> <span data-ttu-id="56b64-111">rubrique de Hello lie également les rubriques pertinentes de tooother.</span><span class="sxs-lookup"><span data-stu-id="56b64-111">hello topic also links tooother relevant topics.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="56b64-112">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="56b64-112">Media Services learning paths</span></span>
<span data-ttu-id="56b64-113">Vous pouvez afficher les parcours d’apprentissage d’AMS ici :</span><span class="sxs-lookup"><span data-stu-id="56b64-113">You can view AMS learning paths here:</span></span>

* [<span data-ttu-id="56b64-114">Workflow en flux continu AMS</span><span class="sxs-lookup"><span data-stu-id="56b64-114">AMS Live Streaming Workflow</span></span>](https://azure.microsoft.com/documentation/learning-paths/media-services-streaming-live/)
* [<span data-ttu-id="56b64-115">Workflow de streaming à la demande AMS</span><span class="sxs-lookup"><span data-stu-id="56b64-115">AMS on-Demand Streaming Workflow</span></span>](https://azure.microsoft.com/documentation/learning-paths/media-services-streaming-on-demand/)

## <a name="prerequisites"></a><span data-ttu-id="56b64-116">Composants requis</span><span class="sxs-lookup"><span data-stu-id="56b64-116">Prerequisites</span></span>

<span data-ttu-id="56b64-117">toostart à l’aide d’Azure Media Services, vous devez disposer de hello :</span><span class="sxs-lookup"><span data-stu-id="56b64-117">toostart using Azure Media Services, you should have hello following:</span></span>

* <span data-ttu-id="56b64-118">Un compte Azure.</span><span class="sxs-lookup"><span data-stu-id="56b64-118">An Azure account.</span></span> <span data-ttu-id="56b64-119">Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="56b64-119">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="56b64-120">Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="56b64-120">For details, see [Azure Free Trial](https://azure.microsoft.com).</span></span>
* <span data-ttu-id="56b64-121">Un compte Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="56b64-121">An Azure Media Services account.</span></span> <span data-ttu-id="56b64-122">Pour plus d’informations, consultez [Créer un compte](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="56b64-122">For more information, see [Create Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="56b64-123">(Facultatif) Un environnement de développement configuré.</span><span class="sxs-lookup"><span data-stu-id="56b64-123">(Optional) Set up development environment.</span></span> <span data-ttu-id="56b64-124">Choisissez .NET ou API REST comme environnement de développement.</span><span class="sxs-lookup"><span data-stu-id="56b64-124">Choose .NET or REST API for your development environment.</span></span> <span data-ttu-id="56b64-125">Pour plus d’informations, consultez [Configuration d'environnement](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="56b64-125">For more information, see [Set up environment](media-services-dotnet-how-to-use.md).</span></span>

    <span data-ttu-id="56b64-126">En outre, apprenez comment trop[connecter par programmation tooAMS API](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="56b64-126">Also, learn how too[connect  programmatically tooAMS API](media-services-use-aad-auth-to-access-ams-api.md).</span></span>
* <span data-ttu-id="56b64-127">Un point de terminaison de streaming standard ou premium à l’état Démarré.</span><span class="sxs-lookup"><span data-stu-id="56b64-127">A standard or premium streaming endpoint in started state.</span></span>  <span data-ttu-id="56b64-128">Pour plus d’informations, consultez [Gestion des points de terminaison de streaming](media-services-portal-manage-streaming-endpoints.md).</span><span class="sxs-lookup"><span data-stu-id="56b64-128">For more information, see [Managing streaming endpoints](media-services-portal-manage-streaming-endpoints.md)</span></span>

## <a name="sdks-and-tools"></a><span data-ttu-id="56b64-129">Kits de développement logiciel (SDK) et outils</span><span class="sxs-lookup"><span data-stu-id="56b64-129">SDKs and tools</span></span>

<span data-ttu-id="56b64-130">solutions de Media Services toobuild, vous pouvez utiliser :</span><span class="sxs-lookup"><span data-stu-id="56b64-130">toobuild Media Services solutions, you can use:</span></span>

* [<span data-ttu-id="56b64-131">API REST Media Services</span><span class="sxs-lookup"><span data-stu-id="56b64-131">Media Services REST API</span></span>](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference)
* <span data-ttu-id="56b64-132">L’un des kits de développement logiciel de client disponibles hello :</span><span class="sxs-lookup"><span data-stu-id="56b64-132">One of hello available client SDKs:</span></span>
    * <span data-ttu-id="56b64-133">[Kit de développement logiciel (SDK) Azure Media Services pour .NET](https://github.com/Azure/azure-sdk-for-media-services),</span><span class="sxs-lookup"><span data-stu-id="56b64-133">[Azure Media Services SDK for .NET](https://github.com/Azure/azure-sdk-for-media-services),</span></span>
    * <span data-ttu-id="56b64-134">[Kit de développement logiciel (SDK) Azure pour Java](https://github.com/Azure/azure-sdk-for-java),</span><span class="sxs-lookup"><span data-stu-id="56b64-134">[Azure SDK for Java](https://github.com/Azure/azure-sdk-for-java),</span></span>
    * <span data-ttu-id="56b64-135">[Kit de développement logiciel (SDK) Azure pour PHP](https://github.com/Azure/azure-sdk-for-php),</span><span class="sxs-lookup"><span data-stu-id="56b64-135">[Azure PHP SDK](https://github.com/Azure/azure-sdk-for-php),</span></span>
    * <span data-ttu-id="56b64-136">[Azure Media Services pour Node.js](https://github.com/michelle-becker/node-ams-sdk/blob/master/lib/request.js) (il s’agit d’une version non Microsoft du Kit de développement logiciel (SDK) Node.js.</span><span class="sxs-lookup"><span data-stu-id="56b64-136">[Azure Media Services for Node.js](https://github.com/michelle-becker/node-ams-sdk/blob/master/lib/request.js) (This is a non-Microsoft version of a Node.js SDK.</span></span> <span data-ttu-id="56b64-137">Il est géré par une Communauté et n’a pas une couverture de 100 % de hello AMS APIs).</span><span class="sxs-lookup"><span data-stu-id="56b64-137">It is maintained by a community and currently does not have a 100% coverage of hello AMS APIs).</span></span>
* <span data-ttu-id="56b64-138">Outils existants :</span><span class="sxs-lookup"><span data-stu-id="56b64-138">Existing tools:</span></span>
    * [<span data-ttu-id="56b64-139">portail Azure</span><span class="sxs-lookup"><span data-stu-id="56b64-139">Azure portal</span></span>](https://portal.azure.com/)
    * <span data-ttu-id="56b64-140">[Azure-Media-Services-Explorer](https://github.com/Azure/Azure-Media-Services-Explorer) (Azure Media Services Explorer (AMSE) est une application Winforms/C# pour Windows)</span><span class="sxs-lookup"><span data-stu-id="56b64-140">[Azure-Media-Services-Explorer](https://github.com/Azure/Azure-Media-Services-Explorer) (Azure Media Services Explorer (AMSE) is a Winforms/C# application for Windows)</span></span>

## <a name="concepts-and-overview"></a><span data-ttu-id="56b64-141">Concepts et vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="56b64-141">Concepts and overview</span></span>
<span data-ttu-id="56b64-142">Pour les concepts Azure Media Services, consultez [Concepts](media-services-concepts.md).</span><span class="sxs-lookup"><span data-stu-id="56b64-142">For Azure Media Services concepts, see [Concepts](media-services-concepts.md).</span></span>

<span data-ttu-id="56b64-143">Pour une procédure-tooseries qui vous présente tooall hello principaux composants d’Azure Media Services, consultez [didacticiels pas à pas de Azure Media Services](https://docs.com/fukushima-shigeyuki/3439/english-azure-media-services-step-by-step-series).</span><span class="sxs-lookup"><span data-stu-id="56b64-143">For a how-tooseries that introduces you tooall hello main components of Azure Media Services, see [Azure Media Services Step-by-Step tutorials](https://docs.com/fukushima-shigeyuki/3439/english-azure-media-services-step-by-step-series).</span></span> <span data-ttu-id="56b64-144">Cette série a une excellente présentation des concepts et il utilise des tâches de hello AMSE outil toodemonstrate AMS.</span><span class="sxs-lookup"><span data-stu-id="56b64-144">This series has a great overview of concepts and it uses hello AMSE tool toodemonstrate AMS tasks.</span></span> <span data-ttu-id="56b64-145">L’outil AMSE est un outil Windows.</span><span class="sxs-lookup"><span data-stu-id="56b64-145">AMSE tool is a Windows tool.</span></span> <span data-ttu-id="56b64-146">Cet outil prend en charge la plupart des tâches hello vous pouvez obtenir par programme avec [AMS Kit de développement logiciel pour .NET](https://github.com/Azure/azure-sdk-for-media-services), [SDK Azure pour Java](https://github.com/Azure/azure-sdk-for-java), ou [Azure PHP SDK](https://github.com/Azure/azure-sdk-for-php).</span><span class="sxs-lookup"><span data-stu-id="56b64-146">This tool supports most of hello tasks you can achieve programmatically with [AMS SDK for .NET](https://github.com/Azure/azure-sdk-for-media-services), [Azure SDK for Java](https://github.com/Azure/azure-sdk-for-java), or  [Azure PHP SDK](https://github.com/Azure/azure-sdk-for-php).</span></span>

## <a name="supported-scenarios-and-availability-of-media-services-across-data-centers"></a><span data-ttu-id="56b64-147">Scénarios pris en charge et disponibilité de Media Services dans les centres de données</span><span class="sxs-lookup"><span data-stu-id="56b64-147">Supported scenarios and availability of Media Services across data centers</span></span>

<span data-ttu-id="56b64-148">Pour plus d’informations, consultez [Scénarios AMS et disponibilité des fonctionnalités et services dans les centres de données](scenarios-and-availability.md).</span><span class="sxs-lookup"><span data-stu-id="56b64-148">For detailed information, see [AMS scenarios and availability of features and services across data centers](scenarios-and-availability.md).</span></span>

## <a name="service-level-agreement-sla"></a><span data-ttu-id="56b64-149">Contrat de Niveau de Service (SLA)</span><span class="sxs-lookup"><span data-stu-id="56b64-149">Service Level Agreement (SLA)</span></span>

* <span data-ttu-id="56b64-150">Pour Media Services, nous garantissons une disponibilité de 99,9 % des transactions d'API REST.</span><span class="sxs-lookup"><span data-stu-id="56b64-150">For Media Services Encoding, we guarantee 99.9% availability of REST API transactions.</span></span>
* <span data-ttu-id="56b64-151">Pour la diffusion en continu, nous traiterons avec succès les demandes de service avec une garantie de disponibilité de 99,9 % pour le contenu multimédia existant si un point de terminaison de streaming standard ou premium est acheté.</span><span class="sxs-lookup"><span data-stu-id="56b64-151">For Streaming, we will successfully service requests with a 99.9% availability guarantee for existing media content when a standard or premium streaming endpoint is purchased.</span></span>
* <span data-ttu-id="56b64-152">Pour les canaux de Live, nous garantissons que les canaux en cours d’exécution aura une connectivité externe au moins 99,9 % du temps de hello.</span><span class="sxs-lookup"><span data-stu-id="56b64-152">For Live Channels, we guarantee that running Channels will have external connectivity at least 99.9% of hello time.</span></span>
* <span data-ttu-id="56b64-153">Pour la Protection du contenu, nous garantissons que nous avons correctement effectuera principales demandes au moins 99,9 % du temps de hello.</span><span class="sxs-lookup"><span data-stu-id="56b64-153">For Content Protection, we guarantee that we will successfully fulfill key requests at least 99.9% of hello time.</span></span>
* <span data-ttu-id="56b64-154">Pour l’indexeur, nous sera correctement demandes de service indexeur tâche traitées avec un encodage de réservé unité 99,9 % du temps de hello.</span><span class="sxs-lookup"><span data-stu-id="56b64-154">For Indexer, we will successfully service Indexer Task requests processed with an Encoding Reserved Unit 99.9% of hello time.</span></span>

<span data-ttu-id="56b64-155">Pour plus d’informations, consultez le [contrat SLA Microsoft Azure](https://azure.microsoft.com/support/legal/sla/).</span><span class="sxs-lookup"><span data-stu-id="56b64-155">For more information, see [Microsoft Azure SLA](https://azure.microsoft.com/support/legal/sla/).</span></span>

<span data-ttu-id="56b64-156">Pour plus d’informations sur la disponibilité des centres de données, consultez hello [Avaiability](scenarios-and-availability.md#availability) section.</span><span class="sxs-lookup"><span data-stu-id="56b64-156">For information about availability in datacenters, see hello [Avaiability](scenarios-and-availability.md#availability) section.</span></span>

## <a name="support"></a><span data-ttu-id="56b64-157">Support</span><span class="sxs-lookup"><span data-stu-id="56b64-157">Support</span></span>

<span data-ttu-id="56b64-158">[support Azure](https://azure.microsoft.com/support/options/) propose des options de support pour Azure, y compris Media Services.</span><span class="sxs-lookup"><span data-stu-id="56b64-158">[Azure Support](https://azure.microsoft.com/support/options/) provides support options for Azure, including Media Services.</span></span>

## <a name="provide-feedback"></a><span data-ttu-id="56b64-159">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="56b64-159">Provide feedback</span></span>

[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
