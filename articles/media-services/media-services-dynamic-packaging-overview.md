---
title: "vue d’ensemble de mise en package dynamique de Media Services aaaAzure | Documents Microsoft"
description: "fournit les rubrique Hello et vue d’ensemble de l’empaquetage dynamique."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 0d9e4f54-5daa-45c1-bfaa-cf09ca89b812
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: 970e24eba800e098774172c87f56629430b227a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="dynamic-packaging"></a>l’empaquetage dynamique
## <a name="overview"></a>Vue d'ensemble
Microsoft Azure Media Services peut être utilisé toodeliver source du média nombreux formats de fichiers et formats de diffusion en continu de contenus multimédias protection du contenu formats tooa diverses technologies clientes (par exemple, iOS, XBOX, Silverlight, Windows 8). Ces clients comprennent différents protocoles. Par exemple, iOS nécessite un format HTTP Live Streaming (HLS) V4, tandis que Silverlight et Xbox nécessitent le format Smooth Streaming. Si vous disposez d’un ensemble de fichiers à débit adaptatif (plusieurs débits binaires) MP4 les fichiers (ISO Base Media 14496-12) ou un ensemble de fichiers de diffusion en continu lisse à débit adaptatif que vous souhaitez tooclients tooserve qui comprennent MPEG DASH, HLS ou Smooth Streaming, vous devez tirer profit de média Services d’empaquetage dynamique.

Avec l’empaquetage dynamique, vous devez est toocreate une ressource qui contient un ensemble de fichiers MP4 ou de fichiers de diffusion en continu lisse à débit adaptatif. Ensuite, en fonction hello le format spécifié dans le manifeste de hello ou demande de fragment, hello à la demande de diffusion en continu serveur garantit que vous recevez des flux de hello protocole hello que vous avez choisi. Par conséquent, vous devez uniquement toostore et payer pour les fichiers hello dans un seul format de stockage et le service Media Services pour la génération et fournit hello de réponse appropriée en fonction des demandes d’un client.

Hello diagramme suivant illustre encodage traditionnel hello et flux de travail empaquetage statique.

![Encodage statique](./media/media-services-dynamic-packaging-overview/media-services-static-packaging.png)

Hello diagramme suivant montre du flux de travail hello empaquetage dynamique.

![Encodage dynamique](./media/media-services-dynamic-packaging-overview/media-services-dynamic-packaging.png)


## <a name="common-scenario"></a>Scénario courant
1. Téléchargez un fichier d'entrée (appelé fichier mezzanine). Par exemple, H.264, MP4 ou WMV (pour la liste des formats pris en charge hello consultez [Formats pris en charge par hello Media Encoder Standard](media-services-media-encoder-standard-formats.md).
2. Encoder vos jeux de mezzanine fichier tooH.264 MP4 à débit adaptatif.
3. Publier asset hello contenant hello ensemble à débit adaptatif MP4 en créant hello recherche de la demande.
4. Générez des hello tooaccess des URL de diffusion en continu et diffuser votre contenu.

## <a name="preparing-assets-for-dynamic-streaming"></a>Préparation des éléments multimédias pour un streaming dynamique
tooprepare votre élément multimédia pour dynamique de diffusion en continu vous avez deux options :

1. [Chargez un fichier maître](media-services-dotnet-upload-files.md).
2. [Utiliser des jeux de hello Media Encoder Standard encodeur tooproduce H.264 MP4 à débit adaptatif](media-services-dotnet-encode-with-media-encoder-standard.md).
3. [Diffusez votre contenu](media-services-deliver-content-overview.md).

## <a id="unsupported_formats"></a>Formats non pris en charge pour l'empaquetage dynamique
Hello des formats de fichier source suivants ne sont pas pris en charge par l’empaquetage dynamique.

* Fichiers MP4 Dolby Digital
* Fichiers Smooth Streaming Dolby Digital

## <a name="media-services-learning-paths"></a>Parcours d’apprentissage de Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

