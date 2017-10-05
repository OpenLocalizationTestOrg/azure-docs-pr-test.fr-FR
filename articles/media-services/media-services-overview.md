---
title: "Vue d’ensemble d’Azure Media Services | Microsoft Docs"
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
ms.openlocfilehash: 2a175aed40b9775d9a4de6877eb3467b43819568
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-media-services-overview"></a><span data-ttu-id="d5f07-103">Vue d’ensemble d’Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="d5f07-103">Azure Media Services overview</span></span> 

<span data-ttu-id="d5f07-104">Microsoft Azure Media Services est une plateforme extensible basée sur le cloud qui permet aux développeurs de créer des applications évolutives de gestion et de diffusion de médias.</span><span class="sxs-lookup"><span data-stu-id="d5f07-104">Microsoft Azure Media Services is an extensible cloud-based platform that enables developers to build scalable media management and delivery applications.</span></span> <span data-ttu-id="d5f07-105">Media Services est basé sur les API REST qui permettent de télécharger, stocker, encoder et empaqueter en toute sécurité du contenu vidéo ou audio destiné à être diffusé à la demande ou en direct sur différents clients (par exemple, téléviseurs, PC et appareils mobiles).</span><span class="sxs-lookup"><span data-stu-id="d5f07-105">Media Services is based on REST APIs that enable you to securely upload, store, encode, and package video or audio content for both on-demand and live streaming delivery to various clients (for example, TV, PC, and mobile devices).</span></span>

<span data-ttu-id="d5f07-106">Vous pouvez créer des flux de travail de bout en bout en utilisant uniquement Media Services.</span><span class="sxs-lookup"><span data-stu-id="d5f07-106">You can build end-to-end workflows using entirely Media Services.</span></span> <span data-ttu-id="d5f07-107">Vous pouvez aussi choisir d'utiliser des composants tiers pour certaines parties de votre flux de travail</span><span class="sxs-lookup"><span data-stu-id="d5f07-107">You can also choose to use third-party components for some parts of your workflow.</span></span> <span data-ttu-id="d5f07-108">(par exemple, en encodant avec un encodeur tiers).</span><span class="sxs-lookup"><span data-stu-id="d5f07-108">For example, encode using a third-party encoder.</span></span> <span data-ttu-id="d5f07-109">Le contenu est ensuite téléchargé, protégé, empaqueté et remis à l'aide de Media Services.</span><span class="sxs-lookup"><span data-stu-id="d5f07-109">Then, upload, protect, package, deliver using Media Services.</span></span>

<span data-ttu-id="d5f07-110">Vous pouvez choisir de diffuser votre contenu en direct ou de le distribuer à la demande.</span><span class="sxs-lookup"><span data-stu-id="d5f07-110">You can choose to stream your content live or deliver content on-demand.</span></span> <span data-ttu-id="d5f07-111">La rubrique contient également des liens vers d’autres rubriques pertinentes.</span><span class="sxs-lookup"><span data-stu-id="d5f07-111">The topic also links to other relevant topics.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="d5f07-112">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="d5f07-112">Media Services learning paths</span></span>
<span data-ttu-id="d5f07-113">Vous pouvez afficher les parcours d’apprentissage d’AMS ici :</span><span class="sxs-lookup"><span data-stu-id="d5f07-113">You can view AMS learning paths here:</span></span>

* [<span data-ttu-id="d5f07-114">Workflow en flux continu AMS</span><span class="sxs-lookup"><span data-stu-id="d5f07-114">AMS Live Streaming Workflow</span></span>](https://azure.microsoft.com/documentation/learning-paths/media-services-streaming-live/)
* [<span data-ttu-id="d5f07-115">Workflow de streaming à la demande AMS</span><span class="sxs-lookup"><span data-stu-id="d5f07-115">AMS on-Demand Streaming Workflow</span></span>](https://azure.microsoft.com/documentation/learning-paths/media-services-streaming-on-demand/)

## <a name="prerequisites"></a><span data-ttu-id="d5f07-116">Composants requis</span><span class="sxs-lookup"><span data-stu-id="d5f07-116">Prerequisites</span></span>

<span data-ttu-id="d5f07-117">Pour commencer à utiliser Azure Media Services, vous devez disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="d5f07-117">To start using Azure Media Services, you should have the following:</span></span>

* <span data-ttu-id="d5f07-118">Un compte Azure.</span><span class="sxs-lookup"><span data-stu-id="d5f07-118">An Azure account.</span></span> <span data-ttu-id="d5f07-119">Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="d5f07-119">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="d5f07-120">Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="d5f07-120">For details, see [Azure Free Trial](https://azure.microsoft.com).</span></span>
* <span data-ttu-id="d5f07-121">Un compte Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="d5f07-121">An Azure Media Services account.</span></span> <span data-ttu-id="d5f07-122">Pour plus d’informations, consultez [Créer un compte](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="d5f07-122">For more information, see [Create Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="d5f07-123">(Facultatif) Un environnement de développement configuré.</span><span class="sxs-lookup"><span data-stu-id="d5f07-123">(Optional) Set up development environment.</span></span> <span data-ttu-id="d5f07-124">Choisissez .NET ou API REST comme environnement de développement.</span><span class="sxs-lookup"><span data-stu-id="d5f07-124">Choose .NET or REST API for your development environment.</span></span> <span data-ttu-id="d5f07-125">Pour plus d’informations, consultez [Configuration d'environnement](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="d5f07-125">For more information, see [Set up environment](media-services-dotnet-how-to-use.md).</span></span>

    <span data-ttu-id="d5f07-126">De plus, découvrez comment [vous connecter par programmation à l’API AMS](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="d5f07-126">Also, learn how to [connect  programmatically to AMS API](media-services-use-aad-auth-to-access-ams-api.md).</span></span>
* <span data-ttu-id="d5f07-127">Un point de terminaison de streaming standard ou premium à l’état Démarré.</span><span class="sxs-lookup"><span data-stu-id="d5f07-127">A standard or premium streaming endpoint in started state.</span></span>  <span data-ttu-id="d5f07-128">Pour plus d’informations, consultez [Gestion des points de terminaison de streaming](media-services-portal-manage-streaming-endpoints.md).</span><span class="sxs-lookup"><span data-stu-id="d5f07-128">For more information, see [Managing streaming endpoints](media-services-portal-manage-streaming-endpoints.md)</span></span>

## <a name="sdks-and-tools"></a><span data-ttu-id="d5f07-129">Kits de développement logiciel (SDK) et outils</span><span class="sxs-lookup"><span data-stu-id="d5f07-129">SDKs and tools</span></span>

<span data-ttu-id="d5f07-130">Pour créer des solutions Media Services, vous pouvez utiliser les composants suivants :</span><span class="sxs-lookup"><span data-stu-id="d5f07-130">To build Media Services solutions, you can use:</span></span>

* [<span data-ttu-id="d5f07-131">API REST Media Services</span><span class="sxs-lookup"><span data-stu-id="d5f07-131">Media Services REST API</span></span>](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference)
* <span data-ttu-id="d5f07-132">Un des Kits de développement logiciel (SDK) de client disponibles :</span><span class="sxs-lookup"><span data-stu-id="d5f07-132">One of the available client SDKs:</span></span>
    * <span data-ttu-id="d5f07-133">[Kit de développement logiciel (SDK) Azure Media Services pour .NET](https://github.com/Azure/azure-sdk-for-media-services),</span><span class="sxs-lookup"><span data-stu-id="d5f07-133">[Azure Media Services SDK for .NET](https://github.com/Azure/azure-sdk-for-media-services),</span></span>
    * <span data-ttu-id="d5f07-134">[Kit de développement logiciel (SDK) Azure pour Java](https://github.com/Azure/azure-sdk-for-java),</span><span class="sxs-lookup"><span data-stu-id="d5f07-134">[Azure SDK for Java](https://github.com/Azure/azure-sdk-for-java),</span></span>
    * <span data-ttu-id="d5f07-135">[Kit de développement logiciel (SDK) Azure pour PHP](https://github.com/Azure/azure-sdk-for-php),</span><span class="sxs-lookup"><span data-stu-id="d5f07-135">[Azure PHP SDK](https://github.com/Azure/azure-sdk-for-php),</span></span>
    * <span data-ttu-id="d5f07-136">[Azure Media Services pour Node.js](https://github.com/michelle-becker/node-ams-sdk/blob/master/lib/request.js) (il s’agit d’une version non Microsoft du Kit de développement logiciel (SDK) Node.js.</span><span class="sxs-lookup"><span data-stu-id="d5f07-136">[Azure Media Services for Node.js](https://github.com/michelle-becker/node-ams-sdk/blob/master/lib/request.js) (This is a non-Microsoft version of a Node.js SDK.</span></span> <span data-ttu-id="d5f07-137">Il est géré par une communauté et ne fournit pas une couverture à 100 % des API AMS).</span><span class="sxs-lookup"><span data-stu-id="d5f07-137">It is maintained by a community and currently does not have a 100% coverage of the AMS APIs).</span></span>
* <span data-ttu-id="d5f07-138">Outils existants :</span><span class="sxs-lookup"><span data-stu-id="d5f07-138">Existing tools:</span></span>
    * [<span data-ttu-id="d5f07-139">portail Azure</span><span class="sxs-lookup"><span data-stu-id="d5f07-139">Azure portal</span></span>](https://portal.azure.com/)
    * <span data-ttu-id="d5f07-140">[Azure-Media-Services-Explorer](https://github.com/Azure/Azure-Media-Services-Explorer) (Azure Media Services Explorer (AMSE) est une application Winforms/C# pour Windows)</span><span class="sxs-lookup"><span data-stu-id="d5f07-140">[Azure-Media-Services-Explorer](https://github.com/Azure/Azure-Media-Services-Explorer) (Azure Media Services Explorer (AMSE) is a Winforms/C# application for Windows)</span></span>

## <a name="concepts-and-overview"></a><span data-ttu-id="d5f07-141">Concepts et vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="d5f07-141">Concepts and overview</span></span>
<span data-ttu-id="d5f07-142">Pour les concepts Azure Media Services, consultez [Concepts](media-services-concepts.md).</span><span class="sxs-lookup"><span data-stu-id="d5f07-142">For Azure Media Services concepts, see [Concepts](media-services-concepts.md).</span></span>

<span data-ttu-id="d5f07-143">Pour découvrir une série de procédures qui présente tous les principaux composants d’Azure Media Services, consultez les [didacticiels pas à pas Azure Media Services](https://docs.com/fukushima-shigeyuki/3439/english-azure-media-services-step-by-step-series).</span><span class="sxs-lookup"><span data-stu-id="d5f07-143">For a how-to series that introduces you to all the main components of Azure Media Services, see [Azure Media Services Step-by-Step tutorials](https://docs.com/fukushima-shigeyuki/3439/english-azure-media-services-step-by-step-series).</span></span> <span data-ttu-id="d5f07-144">Cette série constitue une excellente présentation des concepts, et utilise l’outil AMSE pour effectuer les tâches AMS.</span><span class="sxs-lookup"><span data-stu-id="d5f07-144">This series has a great overview of concepts and it uses the AMSE tool to demonstrate AMS tasks.</span></span> <span data-ttu-id="d5f07-145">L’outil AMSE est un outil Windows.</span><span class="sxs-lookup"><span data-stu-id="d5f07-145">AMSE tool is a Windows tool.</span></span> <span data-ttu-id="d5f07-146">Cet outil prend en charge la plupart des tâches que vous pouvez obtenir par programmation avec le [Kit de développement logiciel (SDK) AMS pour .NET](https://github.com/Azure/azure-sdk-for-media-services), le [Kit de développement logiciel (SDK) Azure pour Java](https://github.com/Azure/azure-sdk-for-java) ou le [Kit de développement logiciel (SDK) Azure pour PHP](https://github.com/Azure/azure-sdk-for-php).</span><span class="sxs-lookup"><span data-stu-id="d5f07-146">This tool supports most of the tasks you can achieve programmatically with [AMS SDK for .NET](https://github.com/Azure/azure-sdk-for-media-services), [Azure SDK for Java](https://github.com/Azure/azure-sdk-for-java), or  [Azure PHP SDK](https://github.com/Azure/azure-sdk-for-php).</span></span>

## <a name="supported-scenarios-and-availability-of-media-services-across-data-centers"></a><span data-ttu-id="d5f07-147">Scénarios pris en charge et disponibilité de Media Services dans les centres de données</span><span class="sxs-lookup"><span data-stu-id="d5f07-147">Supported scenarios and availability of Media Services across data centers</span></span>

<span data-ttu-id="d5f07-148">Pour plus d’informations, consultez [Scénarios AMS et disponibilité des fonctionnalités et services dans les centres de données](scenarios-and-availability.md).</span><span class="sxs-lookup"><span data-stu-id="d5f07-148">For detailed information, see [AMS scenarios and availability of features and services across data centers](scenarios-and-availability.md).</span></span>

## <a name="service-level-agreement-sla"></a><span data-ttu-id="d5f07-149">Contrat de Niveau de Service (SLA)</span><span class="sxs-lookup"><span data-stu-id="d5f07-149">Service Level Agreement (SLA)</span></span>

* <span data-ttu-id="d5f07-150">Pour Media Services, nous garantissons une disponibilité de 99,9 % des transactions d'API REST.</span><span class="sxs-lookup"><span data-stu-id="d5f07-150">For Media Services Encoding, we guarantee 99.9% availability of REST API transactions.</span></span>
* <span data-ttu-id="d5f07-151">Pour la diffusion en continu, nous traiterons avec succès les demandes de service avec une garantie de disponibilité de 99,9 % pour le contenu multimédia existant si un point de terminaison de streaming standard ou premium est acheté.</span><span class="sxs-lookup"><span data-stu-id="d5f07-151">For Streaming, we will successfully service requests with a 99.9% availability guarantee for existing media content when a standard or premium streaming endpoint is purchased.</span></span>
* <span data-ttu-id="d5f07-152">Pour les Canaux en Direct, nous garantissons que les canaux en cours d’exécution auront une connectivité externe au moins 99,9 % du temps.</span><span class="sxs-lookup"><span data-stu-id="d5f07-152">For Live Channels, we guarantee that running Channels will have external connectivity at least 99.9% of the time.</span></span>
* <span data-ttu-id="d5f07-153">Pour la Protection de Contenu, nous garantissons que nous serons en mesure de traiter les demandes de clé au moins 99,9 % du temps.</span><span class="sxs-lookup"><span data-stu-id="d5f07-153">For Content Protection, we guarantee that we will successfully fulfill key requests at least 99.9% of the time.</span></span>
* <span data-ttu-id="d5f07-154">Pour l’Indexeur, nous serons en mesure d’assurer les demandes de tâche d’indexation traitées avec une unité réservée d’encodage 99,9 % du temps.</span><span class="sxs-lookup"><span data-stu-id="d5f07-154">For Indexer, we will successfully service Indexer Task requests processed with an Encoding Reserved Unit 99.9% of the time.</span></span>

<span data-ttu-id="d5f07-155">Pour plus d’informations, consultez le [contrat SLA Microsoft Azure](https://azure.microsoft.com/support/legal/sla/).</span><span class="sxs-lookup"><span data-stu-id="d5f07-155">For more information, see [Microsoft Azure SLA](https://azure.microsoft.com/support/legal/sla/).</span></span>

<span data-ttu-id="d5f07-156">Pour plus d’informations sur la disponibilité dans les centres de données, consultez la section [Disponibilité](scenarios-and-availability.md#availability).</span><span class="sxs-lookup"><span data-stu-id="d5f07-156">For information about availability in datacenters, see the [Avaiability](scenarios-and-availability.md#availability) section.</span></span>

## <a name="support"></a><span data-ttu-id="d5f07-157">Support</span><span class="sxs-lookup"><span data-stu-id="d5f07-157">Support</span></span>

<span data-ttu-id="d5f07-158">[support Azure](https://azure.microsoft.com/support/options/) propose des options de support pour Azure, y compris Media Services.</span><span class="sxs-lookup"><span data-stu-id="d5f07-158">[Azure Support](https://azure.microsoft.com/support/options/) provides support options for Azure, including Media Services.</span></span>

## <a name="provide-feedback"></a><span data-ttu-id="d5f07-159">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="d5f07-159">Provide feedback</span></span>

[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
