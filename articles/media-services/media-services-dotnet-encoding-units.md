---
title: "Mettre à l’échelle le traitement multimédia en ajoutant des unités d’encodage - Azure | Microsoft Docs"
description: "Découvrez comment ajouter des unités d’encodage avec .NET"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 33f7625a-966a-4f06-bc09-bccd6e2a42b5
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako;milangada;
ms.openlocfilehash: 72a8729d22a9e76c8076d7a3347619a2163e4f09
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-scale-encoding-with-net-sdk"></a><span data-ttu-id="a0e0b-103">Mise à l’échelle de l’encodage avec le Kit de développement logiciel (SDK) .NET</span><span class="sxs-lookup"><span data-stu-id="a0e0b-103">How to scale encoding with .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a0e0b-104">Portail</span><span class="sxs-lookup"><span data-stu-id="a0e0b-104">Portal</span></span>](media-services-portal-scale-media-processing.md)
> * [<span data-ttu-id="a0e0b-105">.NET</span><span class="sxs-lookup"><span data-stu-id="a0e0b-105">.NET</span></span>](media-services-dotnet-encoding-units.md)
> * [<span data-ttu-id="a0e0b-106">REST</span><span class="sxs-lookup"><span data-stu-id="a0e0b-106">REST</span></span>](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype)
> * [<span data-ttu-id="a0e0b-107">Java</span><span class="sxs-lookup"><span data-stu-id="a0e0b-107">Java</span></span>](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [<span data-ttu-id="a0e0b-108">PHP</span><span class="sxs-lookup"><span data-stu-id="a0e0b-108">PHP</span></span>](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="overview"></a><span data-ttu-id="a0e0b-109">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="a0e0b-109">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="a0e0b-110">Pour obtenir plus d’informations sur la mise à l’échelle du traitement multimédia, consultez la rubrique de [présentation](media-services-scale-media-processing-overview.md) .</span><span class="sxs-lookup"><span data-stu-id="a0e0b-110">Make sure to review the [overview](media-services-scale-media-processing-overview.md) topic to get more information about scaling media processing topic.</span></span>
> 
> 

<span data-ttu-id="a0e0b-111">Pour modifier le type d’unité réservée et le nombre d’unités réservées d’encodage à l’aide du Kit de développement logiciel (SDK) .NET, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="a0e0b-111">To change the reserved unit type and the number of encoding reserved units using .NET SDK, do the following:</span></span>

    IEncodingReservedUnit encodingS1ReservedUnit = _context.EncodingReservedUnits.FirstOrDefault();
    encodingS1ReservedUnit.ReservedUnitType = ReservedUnitType.Basic; // Corresponds to S1
    encodingS1ReservedUnit.Update();
    Console.WriteLine("Reserved Unit Type: {0}", encodingS1ReservedUnit.ReservedUnitType);

    encodingS1ReservedUnit.CurrentReservedUnits = 2;
    encodingS1ReservedUnit.Update();

    Console.WriteLine("Number of reserved units: {0}", encodingS1ReservedUnit.CurrentReservedUnits);

## <a name="opening-a-support-ticket"></a><span data-ttu-id="a0e0b-112">Ouverture d'un ticket de support</span><span class="sxs-lookup"><span data-stu-id="a0e0b-112">Opening a Support Ticket</span></span>
<span data-ttu-id="a0e0b-113">Par défaut, chaque compte Media Services a une capacité maximale de 25 unités réservées d'encodage et 5 unités réservées de streaming à la demande.</span><span class="sxs-lookup"><span data-stu-id="a0e0b-113">By default every Media Services account can scale to up to 25 Encoding and 5 On-Demand Streaming Reserved Units.</span></span> <span data-ttu-id="a0e0b-114">Vous pouvez demander une limite supérieure en ouvrant un ticket de support.</span><span class="sxs-lookup"><span data-stu-id="a0e0b-114">You can request a higher limit by opening a support ticket.</span></span>

### <a name="open-a-support-ticket"></a><span data-ttu-id="a0e0b-115">Ouverture d’un ticket de support</span><span class="sxs-lookup"><span data-stu-id="a0e0b-115">Open a support ticket</span></span>
<span data-ttu-id="a0e0b-116">Pour ouvrir un ticket de support, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="a0e0b-116">To open a support ticket do the following:</span></span>

1. <span data-ttu-id="a0e0b-117">Cliquez sur [Obtenir un support](https://manage.windowsazure.com/?getsupport=true).</span><span class="sxs-lookup"><span data-stu-id="a0e0b-117">Click [Get Support](https://manage.windowsazure.com/?getsupport=true).</span></span> <span data-ttu-id="a0e0b-118">Si vous n'êtes pas connecté, vous devrez entrer vos informations d'identification.</span><span class="sxs-lookup"><span data-stu-id="a0e0b-118">If you are not logged in, you will be prompted to enter your credentials.</span></span>
2. <span data-ttu-id="a0e0b-119">Sélectionnez votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="a0e0b-119">Select your subscription.</span></span>
3. <span data-ttu-id="a0e0b-120">Sous le type de support, sélectionnez « Technique ».</span><span class="sxs-lookup"><span data-stu-id="a0e0b-120">Under support type, select "Technical".</span></span>
4. <span data-ttu-id="a0e0b-121">Cliquez sur « Créer un ticket ».</span><span class="sxs-lookup"><span data-stu-id="a0e0b-121">Click on "Create Ticket".</span></span>
5. <span data-ttu-id="a0e0b-122">Sélectionnez « Azure Media Services » dans la liste de produits affichée sur la page suivante.</span><span class="sxs-lookup"><span data-stu-id="a0e0b-122">Select "Azure Media Services" in the product list presented on the next page.</span></span>
6. <span data-ttu-id="a0e0b-123">Sélectionnez un « type de problème » approprié pour votre problème.</span><span class="sxs-lookup"><span data-stu-id="a0e0b-123">Select a "Problem type" that is appropriate for your issue.</span></span>
7. <span data-ttu-id="a0e0b-124">Cliquez sur Continuer.</span><span class="sxs-lookup"><span data-stu-id="a0e0b-124">Click Continue.</span></span>
8. <span data-ttu-id="a0e0b-125">Suivez les instructions de la page suivante, puis entrez les détails relatifs à votre problème.</span><span class="sxs-lookup"><span data-stu-id="a0e0b-125">Follow instructions on next page and then enter details about your issue.</span></span>
9. <span data-ttu-id="a0e0b-126">Cliquez sur Envoyer pour ouvrir le ticket.</span><span class="sxs-lookup"><span data-stu-id="a0e0b-126">Click submit to open the ticket.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="a0e0b-127">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="a0e0b-127">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a0e0b-128">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="a0e0b-128">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

