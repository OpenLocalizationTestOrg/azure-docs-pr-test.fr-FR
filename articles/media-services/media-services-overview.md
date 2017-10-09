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
# <a name="azure-media-services-overview"></a>Vue d’ensemble d’Azure Media Services 

Microsoft Azure Media Services est une plateforme cloud extensible qui permet aux développeurs toobuild de contenu multimédia évolutives gestion et remise applications. Media Services est basé sur les API REST qui vous permettent de téléchargement de toosecurely, stocker, encoder et empaqueter le contenu vidéo ou audio pour la demande et live diffusion en continu remise toovarious les clients (par exemple, TV, PC et appareils mobiles).

Vous pouvez créer des flux de travail de bout en bout en utilisant uniquement Media Services. Vous pouvez également choisir toouse des composants tiers pour certaines parties de votre flux de travail. (par exemple, en encodant avec un encodeur tiers). Le contenu est ensuite téléchargé, protégé, empaqueté et remis à l'aide de Media Services.

Vous pouvez choisir toostream votre contenu en direct ou fournir le contenu à la demande. rubrique de Hello lie également les rubriques pertinentes de tooother.

## <a name="media-services-learning-paths"></a>Parcours d’apprentissage de Media Services
Vous pouvez afficher les parcours d’apprentissage d’AMS ici :

* [Workflow en flux continu AMS](https://azure.microsoft.com/documentation/learning-paths/media-services-streaming-live/)
* [Workflow de streaming à la demande AMS](https://azure.microsoft.com/documentation/learning-paths/media-services-streaming-on-demand/)

## <a name="prerequisites"></a>Composants requis

toostart à l’aide d’Azure Media Services, vous devez disposer de hello :

* Un compte Azure. Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes. Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com).
* Un compte Azure Media Services. Pour plus d’informations, consultez [Créer un compte](media-services-portal-create-account.md).
* (Facultatif) Un environnement de développement configuré. Choisissez .NET ou API REST comme environnement de développement. Pour plus d’informations, consultez [Configuration d'environnement](media-services-dotnet-how-to-use.md).

    En outre, apprenez comment trop[connecter par programmation tooAMS API](media-services-use-aad-auth-to-access-ams-api.md).
* Un point de terminaison de streaming standard ou premium à l’état Démarré.  Pour plus d’informations, consultez [Gestion des points de terminaison de streaming](media-services-portal-manage-streaming-endpoints.md).

## <a name="sdks-and-tools"></a>Kits de développement logiciel (SDK) et outils

solutions de Media Services toobuild, vous pouvez utiliser :

* [API REST Media Services](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference)
* L’un des kits de développement logiciel de client disponibles hello :
    * [Kit de développement logiciel (SDK) Azure Media Services pour .NET](https://github.com/Azure/azure-sdk-for-media-services),
    * [Kit de développement logiciel (SDK) Azure pour Java](https://github.com/Azure/azure-sdk-for-java),
    * [Kit de développement logiciel (SDK) Azure pour PHP](https://github.com/Azure/azure-sdk-for-php),
    * [Azure Media Services pour Node.js](https://github.com/michelle-becker/node-ams-sdk/blob/master/lib/request.js) (il s’agit d’une version non Microsoft du Kit de développement logiciel (SDK) Node.js. Il est géré par une Communauté et n’a pas une couverture de 100 % de hello AMS APIs).
* Outils existants :
    * [portail Azure](https://portal.azure.com/)
    * [Azure-Media-Services-Explorer](https://github.com/Azure/Azure-Media-Services-Explorer) (Azure Media Services Explorer (AMSE) est une application Winforms/C# pour Windows)

## <a name="concepts-and-overview"></a>Concepts et vue d’ensemble
Pour les concepts Azure Media Services, consultez [Concepts](media-services-concepts.md).

Pour une procédure-tooseries qui vous présente tooall hello principaux composants d’Azure Media Services, consultez [didacticiels pas à pas de Azure Media Services](https://docs.com/fukushima-shigeyuki/3439/english-azure-media-services-step-by-step-series). Cette série a une excellente présentation des concepts et il utilise des tâches de hello AMSE outil toodemonstrate AMS. L’outil AMSE est un outil Windows. Cet outil prend en charge la plupart des tâches hello vous pouvez obtenir par programme avec [AMS Kit de développement logiciel pour .NET](https://github.com/Azure/azure-sdk-for-media-services), [SDK Azure pour Java](https://github.com/Azure/azure-sdk-for-java), ou [Azure PHP SDK](https://github.com/Azure/azure-sdk-for-php).

## <a name="supported-scenarios-and-availability-of-media-services-across-data-centers"></a>Scénarios pris en charge et disponibilité de Media Services dans les centres de données

Pour plus d’informations, consultez [Scénarios AMS et disponibilité des fonctionnalités et services dans les centres de données](scenarios-and-availability.md).

## <a name="service-level-agreement-sla"></a>Contrat de Niveau de Service (SLA)

* Pour Media Services, nous garantissons une disponibilité de 99,9 % des transactions d'API REST.
* Pour la diffusion en continu, nous traiterons avec succès les demandes de service avec une garantie de disponibilité de 99,9 % pour le contenu multimédia existant si un point de terminaison de streaming standard ou premium est acheté.
* Pour les canaux de Live, nous garantissons que les canaux en cours d’exécution aura une connectivité externe au moins 99,9 % du temps de hello.
* Pour la Protection du contenu, nous garantissons que nous avons correctement effectuera principales demandes au moins 99,9 % du temps de hello.
* Pour l’indexeur, nous sera correctement demandes de service indexeur tâche traitées avec un encodage de réservé unité 99,9 % du temps de hello.

Pour plus d’informations, consultez le [contrat SLA Microsoft Azure](https://azure.microsoft.com/support/legal/sla/).

Pour plus d’informations sur la disponibilité des centres de données, consultez hello [Avaiability](scenarios-and-availability.md#availability) section.

## <a name="support"></a>Support

[support Azure](https://azure.microsoft.com/support/options/) propose des options de support pour Azure, y compris Media Services.

## <a name="provide-feedback"></a>Fournir des commentaires

[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
