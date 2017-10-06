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
# <a name="how-tooscale-encoding-with-net-sdk"></a>Comment tooscale encodage avec le Kit de développement .NET
> [!div class="op_single_selector"]
> * [Portail](media-services-portal-scale-media-processing.md)
> * [.NET](media-services-dotnet-encoding-units.md)
> * [REST](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype)
> * [Java](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [PHP](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="overview"></a>Vue d'ensemble
> [!IMPORTANT]
> Assurez-vous que tooreview hello [vue d’ensemble](media-services-scale-media-processing-overview.md) rubrique tooget plus d’informations sur la mise à l’échelle de media du traitement de rubrique.
> 
> 

toochange hello réservé hello et type de numéro d’unité d’encodage des unités réservées à l’aide du Kit de développement .NET, hello suivant :

    IEncodingReservedUnit encodingS1ReservedUnit = _context.EncodingReservedUnits.FirstOrDefault();
    encodingS1ReservedUnit.ReservedUnitType = ReservedUnitType.Basic; // Corresponds tooS1
    encodingS1ReservedUnit.Update();
    Console.WriteLine("Reserved Unit Type: {0}", encodingS1ReservedUnit.ReservedUnitType);

    encodingS1ReservedUnit.CurrentReservedUnits = 2;
    encodingS1ReservedUnit.Update();

    Console.WriteLine("Number of reserved units: {0}", encodingS1ReservedUnit.CurrentReservedUnits);

## <a name="opening-a-support-ticket"></a>Ouverture d'un ticket de support
Par défaut, chaque compte Media Services peut évoluer tooup too25 encodage et 5 à la demande de diffusion en continu unités réservées. Vous pouvez demander une limite supérieure en ouvrant un ticket de support.

### <a name="open-a-support-ticket"></a>Ouverture d’un ticket de support
tooopen un ticket de support hello suivant :

1. Cliquez sur [Obtenir un support](https://manage.windowsazure.com/?getsupport=true). Si vous n’êtes pas connecté, vous allez être invité à tooenter vos informations d’identification.
2. Sélectionnez votre abonnement.
3. Sous le type de support, sélectionnez « Technique ».
4. Cliquez sur « Créer un ticket ».
5. Sélectionnez « Azure Media Services » dans la liste des produits hello présentées sur la page suivante de hello.
6. Sélectionnez un « type de problème » approprié pour votre problème.
7. Cliquez sur Continuer.
8. Suivez les instructions de la page suivante, puis entrez les détails relatifs à votre problème.
9. Cliquez sur Envoyer un ticket de hello tooopen.

## <a name="media-services-learning-paths"></a>Parcours d’apprentissage de Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

