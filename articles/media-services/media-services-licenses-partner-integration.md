---
title: aaaUsing partenaires toodeliver Widevine licences tooAzure Media Services | Documents Microsoft
description: "Cet article décrit comment vous pouvez utiliser Azure Media Services (AMS) toodeliver un flux qui est chiffré dynamiquement par AMS avec PlayReady et Widevine DRMs. la licence PlayReady Hello est fourni à partir du serveur de licences PlayReady de Media Services et les licences Widevine sont remis par le serveur de licences castLabs."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 5bcad5a4-c0bb-4871-9cce-808a913c53e6
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: 3c18a8a22ced239931dea5385020194bd6d83f28
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-partners-toodeliver-widevine-licenses-tooazure-media-services"></a>À l’aide de partenaires toodeliver Widevine licences tooAzure Media Services
## <a name="overview"></a>Vue d'ensemble
Microsoft Azure Media Services permet toodeliver QUE MPEG-DASH protégée par DRM Widevine, laquelle est chiffrée par hello spécification de chiffrement commun (CENC).

À compter de hello Media Services .NET SDK version 3.5.2, Media Services permet de vous tooconfigure Widevine modèle de licence et obtenir des licences Widevine. Vous pouvez également utiliser hello suivant toohelp de partenaires AMS vous fournir des licences Widevine : [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).

## <a name="castlabs"></a>castLabs
Vous pouvez utiliser [castLabs](http://castlabs.com/company/partners/azure/) toodeliver Widevine licences. Pour plus d’informations, consultez [à l’aide de castLabs toodeliver DRM licences tooAzure Media Services](media-services-castlabs-integration.md)

## <a name="axinom"></a>Axinom
Vous pouvez utiliser [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/) toodeliver Widevine licences. Pour plus d’informations, consultez [à l’aide de Axinom toodeliver DRM licences tooAzure Media Services](media-services-axinom-integration.md)

## <a name="media-services-learning-paths"></a>Parcours d’apprentissage de Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Voir aussi
[Utilisation du chiffrement commun dynamique PlayReady et/ou Widevine](media-services-protect-with-drm.md)

[Blog de Mingfei](https://azure.microsoft.com/blog/azure-media-services-adds-google-widevine-packaging-for-delivering-multi-drm-stream/)

