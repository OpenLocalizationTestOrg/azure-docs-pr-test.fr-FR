---
title: "vue d’ensemble de la terminaison de diffusion en continu Media Services aaaAzure | Documents Microsoft"
description: "Cette rubrique fournit une vue d’ensemble des points de terminaison de streaming Azure Media Services."
services: media-services
documentationcenter: 
author: Juliako
writer: juliako
manager: cfowler
editor: 
ms.assetid: 097ab5e5-24e1-4e8e-b112-be74172c2701
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: f27f590175dcc945d1d3299fc0cae5a68cfbf4e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="streaming-endpoints-overview"></a>Vue d’ensemble des points de terminaison de streaming 

##<a name="overview"></a>Vue d'ensemble

Dans Microsoft Azure Media Services (AMS), un **le point de terminaison de diffusion en continu** représente un service de diffusion en continu qui peut fournir du contenu directement de l’application de lecteur tooa client ou tooa réseau de distribution de contenu (CDN) pour une distribution ultérieure. Media Services fournit également une intégration transparente au CDN Azure. flux sortant de Hello à partir d’un service StreamingEndpoint peut être un flux en direct, d’une vidéo à la demande, ou le téléchargement progressif de votre élément multimédia dans votre compte Media Services. Chaque compte Azure Media Services comprend une valeur de point de terminaison de streaming par défaut. Streamingendpoint supplémentaires peut être créés sous le compte de hello. Il existe deux versions du point de terminaison de streaming : 1.0 et 2.0. À compter du 10 janvier 2017, les nouveaux comptes AMS incluront la version 2.0 du point de terminaison de streaming **par défaut**. Supplémentaire que vous ajoutez toothis compte des points de terminaison de diffusion en continu sera également la version 2.0. Cette modification n’affectera pas les comptes existants hello ; Streamingendpoint existant sera la version 1.0 et peut être mis à niveau tooversion 2.0. Avec cette modification il y aura les changements de comportement, la facturation et fonctionnalité (pour plus d’informations, consultez hello **versions et les types de diffusion en continu** section décrite ci-dessous).

En outre, à compter version hello 2.15 (publiée en janvier 2017), Azure Media Services ajoutées hello suivant l’entité de point de terminaison de diffusion en continu de propriétés toohello : **CdnProvider**, **CdnProfile**,  **FreeTrialEndTime**, **StreamingEndpointVersion**. Pour une présentation détaillée de ces propriétés, consultez [ceci](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint). 

Lorsque vous créez un compte Azure Media Services par défaut standard point de terminaison de diffusion en continu est créé pour vous dans hello **arrêté** état. Vous ne pouvez supprimer le point de terminaison de diffusion en continu de la valeur par défaut hello. En fonction de hello disponibilité CDN Azure dans la région de hello ciblé, par défaut de la valeur par défaut qui vient d’être créée point de terminaison de diffusion en continu inclut également « StandardVerizon » CDN intégration du fournisseur. 

>[!NOTE]
>Intégration d’Azure CDN peut être désactivée avant de démarrer le point de terminaison de diffusion en continu de hello.

Cette rubrique donne une vue d’ensemble de fonctionnalités principales hello fournis par les points de terminaison de diffusion en continu.

## <a name="streaming-types-and-versions"></a>Types et versions de streaming

### <a name="standardpremium-types-version-20"></a>Types Standard/Premium (version 2.0)

Vous démarrez avec la version de janvier 2017 hello de Media Services, vous avez deux types de diffusion en continu : **Standard** et **Premium**. Ces types font partie de la version de point de terminaison de diffusion en continu hello « 2.0 ».

Type|Description
---|---
**Standard**|Il s’agit d’option par défaut hello qui doit s’exécuter pour la majorité de hello des scénarios de hello.<br/>Avec cette option, vous obtenez le contrat SLA de fixe/limité, 15 premiers jours après le démarrage de point de terminaison de diffusion en continu de hello est gratuit.<br/>Si vous créez plusieurs points de terminaison de diffusion en continu, seuls hello tout d’abord une est gratuite pour hello 15 premiers jours, hello d’autres sont facturés dès que vous les démarrez. <br/>Notez que version d’évaluation gratuite s’applique uniquement toonewly créé les comptes de services de support et de la valeur par défaut de la diffusion en continu de point de terminaison. Les points de terminaison de diffusion en continu existants et les points de terminaison de diffusion en continu en outre créés n’inclut la version d’évaluation gratuite période de même, ils sont mis à niveau tooversion 2.0 ou qu’ils sont créés en tant que version 2.0.
**Premium**|Cette option convient aux scénarios professionnels qui nécessitent plus de mise à l’échelle ou de contrôle.<br/>Contrat de niveau de service variable basé sur la capacité d’unité de streaming Premium (SU) achetée et les points de terminaison de streaming en service dans un environnement isolé et n’étant pas en concurrence pour les ressources.

Pour plus d’informations, consultez hello **comparer la diffusion en continu des types** suivant la section.

### <a name="classic-type-version-10"></a>Type classique (version 1.0)

Pour les utilisateurs qui a créé les comptes AMS toohello préalable 2017 de 10 janvier, vous avez un **classique** type d’un point de terminaison de diffusion en continu. Ce type fait partie de hello de diffusion en continu de la version de point de terminaison « 1.0 ».

Si votre **version « 1.0 »** point de terminaison de diffusion en continu a > = 1 premium diffusion en continu des unités (SU), il sera le point de terminaison de diffusion en continu premium et fournit toutes les fonctionnalités AMS (comme hello **Standard/Premium** type) sans les étapes de configuration supplémentaires.

>[!NOTE]
>Les points de terminaison de streaming de type **Classique** continu (version « 1.0 » et 0 SU), fournissent des fonctionnalités limitées et n’incluent pas de contrat de niveau de service. Il est recommandé de trop toomigrate**Standard** type tooget un meilleures fonctionnalités de l’expérience et toouse comme empaquetage dynamique ou de chiffrement et d’autres fonctionnalités qui accompagnent hello **Standard** type. toomigrate toohello **Standard** type, accédez toohello [portail Azure](https://portal.azure.com/) et sélectionnez **tooStandard Opt-in**. Pour plus d’informations sur la migration, consultez hello [migration](#migration-between-types) section.
>
>Faites attention, car cette opération ne peut pas être restaurée et a un impact sur la tarification.
>
 
## <a name="comparing-streaming-types"></a>Comparaison des types de streaming

### <a name="versions"></a>Versions

|Type|StreamingEndpointVersion|ScaleUnits|CDN|Facturation|Contrat SLA| 
|--------------|----------|-----------------|-----------------|-----------------|-----------------|    
|Classique|1.0|0|N/D|Gratuit|N/D|
|Point de terminaison de streaming Standard|2.0|0|Oui|Payant|Oui|
|Unités de streaming Premium|1.0|>0|Oui|Payant|Oui|
|Unités de streaming Premium|2.0|>0|Oui|Payant|Oui|

### <a name="features"></a>Caractéristiques

Fonctionnalité|Standard|Premium
---|---|---
Gratuit les 15 premiers jours| Oui |Non
Throughput |Des too600 Mbits/s lorsque Azure CDN n’est pas utilisé. Mis à l’échelle avec CDN.|200 Mbits/s par unité de streaming (SU). Mis à l’échelle avec CDN.
Contrat SLA | 99.9|99,9 (200 Mbits/s par SU).
CDN|Azure CDN, CDN tiers ou sans CDN.|Azure CDN, CDN tiers ou sans CDN.
La facturation est calculée sur la base d'un taux| Quotidien|Quotidien
Chiffrement dynamique|Oui|Oui
l’empaquetage dynamique|Oui|Oui
Mettre à l'échelle|Met à l’échelle automatique haut débit de toohello ciblé.|Unités de diffusion en continu supplémentaires
Hôte de filtrage d’IP/G20/personnalisé|Oui|Oui
Téléchargement progressif|Oui|Oui
Utilisation recommandée |Recommandé pour hello grande majorité des scénarios de diffusion en continu.|Utilisation professionnelle.<br/>Si vous pensez que vos besoins dépassent ce qu’offre l’abonnement Standard. Contactez-nous (amsstreaming arobase microsoft.com) si vous prévoyez un public dépassant les 50 000 utilisateurs.


## <a name="migration-between-types"></a>Migration entre les types

À partir | trop| Action
---|---|---
Classique|Standard|Nécessité de tooopt
Classique|Premium| Échelle (unités de diffusion en continu supplémentaires)
Standard/Premium|Classique|Non disponible (si la version du point de terminaison de streaming est 1.0. Il n’est autorisé tooclassic toochange avec les unités d’échelle de paramètre trop « 0 »)
Standard (avec/sans CDN)|Premium avec hello mêmes configurations|Autorisé Bonjour **démarré** état. (via le portail Azure)
Premium (avec/sans CDN)|Standard avec hello mêmes configurations|Autorisé Bonjour **démarré** état (via le portail Azure)
Standard (avec/sans CDN)|Premium avec une configuration différente|Autorisé Bonjour **arrêté** état (via le portail Azure). Pas autorisé dans l’état d’exécution de hello.
Premium (avec/sans CDN)|Standard avec une configuration différente|Autorisé Bonjour **arrêté** état (via le portail Azure). Pas autorisé dans l’état d’exécution de hello.
Version 1.0 avec SU > = 1 avec CDN|Standard/Premium avec aucun CDN|Autorisé Bonjour **arrêté** état. Interdit dans hello **démarré** état.
Version 1.0 avec SU > = 1 avec CDN|Standard, avec/sans CDN|Autorisé Bonjour **arrêté** état. Interdit dans hello **démarré** état. Le CDN version 1.0 sera supprimé et le nouveau créé et démarré.
Version 1.0 avec SU > = 1 avec CDN|Premium avec/sans CDN|Autorisé Bonjour **arrêté** état. Interdit dans hello **démarré** état. Le CDN classique sera supprimé et le nouveau créé et démarré.

## <a name="next-steps"></a>Étapes suivantes
Consultez les parcours d’apprentissage de Media Services.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

