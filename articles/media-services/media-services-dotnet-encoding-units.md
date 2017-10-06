---
title: "support aaaScale du traitement en ajoutant des unités d’encodage - Azure |  Documents Microsoft"
description: "Découvrez comment unités d’encodage tooadd toohow avec .NET"
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
ms.openlocfilehash: b9f71a6487c5d136319a38a1598d60edfaa81b9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooscale-encoding-with-net-sdk"></a><span data-ttu-id="9ebe7-103">Comment tooscale encodage avec le Kit de développement .NET</span><span class="sxs-lookup"><span data-stu-id="9ebe7-103">How tooscale encoding with .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9ebe7-104">Portail</span><span class="sxs-lookup"><span data-stu-id="9ebe7-104">Portal</span></span>](media-services-portal-scale-media-processing.md)
> * [<span data-ttu-id="9ebe7-105">.NET</span><span class="sxs-lookup"><span data-stu-id="9ebe7-105">.NET</span></span>](media-services-dotnet-encoding-units.md)
> * [<span data-ttu-id="9ebe7-106">REST</span><span class="sxs-lookup"><span data-stu-id="9ebe7-106">REST</span></span>](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype)
> * [<span data-ttu-id="9ebe7-107">Java</span><span class="sxs-lookup"><span data-stu-id="9ebe7-107">Java</span></span>](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [<span data-ttu-id="9ebe7-108">PHP</span><span class="sxs-lookup"><span data-stu-id="9ebe7-108">PHP</span></span>](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="overview"></a><span data-ttu-id="9ebe7-109">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="9ebe7-109">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="9ebe7-110">Assurez-vous que tooreview hello [vue d’ensemble](media-services-scale-media-processing-overview.md) rubrique tooget plus d’informations sur la mise à l’échelle de media du traitement de rubrique.</span><span class="sxs-lookup"><span data-stu-id="9ebe7-110">Make sure tooreview hello [overview](media-services-scale-media-processing-overview.md) topic tooget more information about scaling media processing topic.</span></span>
> 
> 

<span data-ttu-id="9ebe7-111">toochange hello réservé hello et type de numéro d’unité d’encodage des unités réservées à l’aide du Kit de développement .NET, hello suivant :</span><span class="sxs-lookup"><span data-stu-id="9ebe7-111">toochange hello reserved unit type and hello number of encoding reserved units using .NET SDK, do hello following:</span></span>

    IEncodingReservedUnit encodingS1ReservedUnit = _context.EncodingReservedUnits.FirstOrDefault();
    encodingS1ReservedUnit.ReservedUnitType = ReservedUnitType.Basic; // Corresponds tooS1
    encodingS1ReservedUnit.Update();
    Console.WriteLine("Reserved Unit Type: {0}", encodingS1ReservedUnit.ReservedUnitType);

    encodingS1ReservedUnit.CurrentReservedUnits = 2;
    encodingS1ReservedUnit.Update();

    Console.WriteLine("Number of reserved units: {0}", encodingS1ReservedUnit.CurrentReservedUnits);

## <a name="opening-a-support-ticket"></a><span data-ttu-id="9ebe7-112">Ouverture d'un ticket de support</span><span class="sxs-lookup"><span data-stu-id="9ebe7-112">Opening a Support Ticket</span></span>
<span data-ttu-id="9ebe7-113">Par défaut, chaque compte Media Services peut évoluer tooup too25 encodage et 5 à la demande de diffusion en continu unités réservées.</span><span class="sxs-lookup"><span data-stu-id="9ebe7-113">By default every Media Services account can scale tooup too25 Encoding and 5 On-Demand Streaming Reserved Units.</span></span> <span data-ttu-id="9ebe7-114">Vous pouvez demander une limite supérieure en ouvrant un ticket de support.</span><span class="sxs-lookup"><span data-stu-id="9ebe7-114">You can request a higher limit by opening a support ticket.</span></span>

### <a name="open-a-support-ticket"></a><span data-ttu-id="9ebe7-115">Ouverture d’un ticket de support</span><span class="sxs-lookup"><span data-stu-id="9ebe7-115">Open a support ticket</span></span>
<span data-ttu-id="9ebe7-116">tooopen un ticket de support hello suivant :</span><span class="sxs-lookup"><span data-stu-id="9ebe7-116">tooopen a support ticket do hello following:</span></span>

1. <span data-ttu-id="9ebe7-117">Cliquez sur [Obtenir un support](https://manage.windowsazure.com/?getsupport=true).</span><span class="sxs-lookup"><span data-stu-id="9ebe7-117">Click [Get Support](https://manage.windowsazure.com/?getsupport=true).</span></span> <span data-ttu-id="9ebe7-118">Si vous n’êtes pas connecté, vous allez être invité à tooenter vos informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="9ebe7-118">If you are not logged in, you will be prompted tooenter your credentials.</span></span>
2. <span data-ttu-id="9ebe7-119">Sélectionnez votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="9ebe7-119">Select your subscription.</span></span>
3. <span data-ttu-id="9ebe7-120">Sous le type de support, sélectionnez « Technique ».</span><span class="sxs-lookup"><span data-stu-id="9ebe7-120">Under support type, select "Technical".</span></span>
4. <span data-ttu-id="9ebe7-121">Cliquez sur « Créer un ticket ».</span><span class="sxs-lookup"><span data-stu-id="9ebe7-121">Click on "Create Ticket".</span></span>
5. <span data-ttu-id="9ebe7-122">Sélectionnez « Azure Media Services » dans la liste des produits hello présentées sur la page suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="9ebe7-122">Select "Azure Media Services" in hello product list presented on hello next page.</span></span>
6. <span data-ttu-id="9ebe7-123">Sélectionnez un « type de problème » approprié pour votre problème.</span><span class="sxs-lookup"><span data-stu-id="9ebe7-123">Select a "Problem type" that is appropriate for your issue.</span></span>
7. <span data-ttu-id="9ebe7-124">Cliquez sur Continuer.</span><span class="sxs-lookup"><span data-stu-id="9ebe7-124">Click Continue.</span></span>
8. <span data-ttu-id="9ebe7-125">Suivez les instructions de la page suivante, puis entrez les détails relatifs à votre problème.</span><span class="sxs-lookup"><span data-stu-id="9ebe7-125">Follow instructions on next page and then enter details about your issue.</span></span>
9. <span data-ttu-id="9ebe7-126">Cliquez sur Envoyer un ticket de hello tooopen.</span><span class="sxs-lookup"><span data-stu-id="9ebe7-126">Click submit tooopen hello ticket.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="9ebe7-127">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="9ebe7-127">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="9ebe7-128">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="9ebe7-128">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

