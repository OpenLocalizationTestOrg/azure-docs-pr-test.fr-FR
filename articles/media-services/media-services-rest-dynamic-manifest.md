---
title: "Filtres d’aaaCreating avec l’API REST Azure Media Services | Documents Microsoft"
description: "Cette rubrique décrit comment toocreate filtre votre client peut utiliser les toostream des sections spécifiques d’un flux. Media Services crée les manifestes dynamique tooachieve cette diffusion sélective."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: f7d23daf-7cd2-49c7-a195-ab902912ab3c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako;cenkdin
ms.openlocfilehash: d0b5af3b193b35f22ac70887963c2f0a06b60bde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-filters-with-azure-media-services-rest-api"></a>Création de filtres avec l’API REST Media Services Azure
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-dynamic-manifest.md)
> * [REST](media-services-rest-dynamic-manifest.md)
> 
> 

À compter de version 2.11, Media Services vous permet toodefine des filtres pour vos ressources. Ces filtres sont des règles côté serveur qui permettent à vos clients toochoose toodo opérations : lecture uniquement une section d’une vidéo (au lieu de hello vidéo complètes), ou spécifiez uniquement un sous-ensemble de formats audio et vidéo que les appareils de votre client peuvent traiter () au lieu de tous les formats de hello qui sont associés les actifs hello). Ce filtrage de vos ressources est archivé via **manifeste dynamique**s qui sont créées lors de toostream de demande de votre client une vidéo en fonction de filtres spécifiées.

Pour plus d’informations connexes toofilters et dynamique de manifeste, consultez [dynamique manifestes de vue d’ensemble](media-services-dynamic-manifest-overview.md).

Cette rubrique montre comment toouse API REST toocreate, mettre à jour et supprimer des filtres. 

## <a name="types-used-toocreate-filters"></a>Les types utilisés toocreate filtres
les types suivants Hello sont utilisées lors de la création de filtres :  

* [Filter](https://docs.microsoft.com/rest/api/media/operations/filter)
* [AssetFilter](https://docs.microsoft.com/rest/api/media/operations/assetfilter)
* [PresentationTimeRange](https://docs.microsoft.com/rest/api/media/operations/presentationtimerange)
* [FilterTrackSelect et FilterTrackPropertyCondition](https://docs.microsoft.com/rest/api/media/operations/filtertrackselect)

>[!NOTE]

>Lors de l’accès aux entités dans Media Services, vous devez définir les valeurs et les champs d’en-tête spécifiques dans vos requêtes HTTP. Pour plus d'informations, consultez [Installation pour le développement REST API de Media Services](media-services-rest-how-to-use.md).

## <a name="connect-toomedia-services"></a>Connecter les Services de tooMedia

Pour plus d’informations sur la façon dont tooconnect toohello AMS API, consultez [hello accès API Azure Media Services avec l’authentification Azure AD](media-services-use-aad-auth-to-access-ams-api.md). 

>[!NOTE]
>Après vous être connecté toohttps://media.windows.net, vous recevrez une redirection 301 spécifiant un autre URI de Media Services. Vous devez effectuer les appels suivants toohello nouvel URI.

## <a name="create-filters"></a>Création de filtres
### <a name="create-global-filters"></a>Création de filtres globaux
toocreate un filtre global, utilisez hello suivant des requêtes HTTP :  

#### <a name="http-request"></a>Demande HTTP
En-têtes de demande

    POST https://media.windows.net/API/Filters HTTP/1.1 
    DataServiceVersion:3.0 
    MaxDataServiceVersion: 3.0 
    Content-Type: application/json 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000 
    Host:media.windows.net 

Corps de la demande 

    {  
       "Name":"GlobalFilter",
       "PresentationTimeRange":{  
          "StartTimestamp":"0",
          "EndTimestamp":"9223372036854775807",
          "PresentationWindowDuration":"12000000000",
          "LiveBackoffDuration":"0",
          "Timescale":"10000000"
       },
       "Tracks":[  
          {  
             "PropertyConditions":
                  [  
                {  
                   "Property":"Type",
                   "Value":"audio",
                   "Operator":"Equal"
                },
                {  
                   "Property":"Bitrate",
                   "Value":"0-2147483647",
                   "Operator":"Equal"
                }
             ]
          }
       ]
    }




#### <a name="http-response"></a>Réponse HTTP
    HTTP/1.1 201 Created 

### <a name="create-local-assetfilters"></a>Création d'AssetFilters locaux
toocreate un AssetFilter local, utilisez hello suivant des requêtes HTTP :  

#### <a name="http-request"></a>Demande HTTP
En-têtes de demande

    POST https://media.windows.net/API/AssetFilters HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Content-Type: application/json 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000 
    Host: media.windows.net  

Corps de la demande 

    {   
       "Name":"AssetFilter", 
       "ParentAssetId":"nb:cid:UUID:536e555d-1500-80c3-92dc-f1e4fdc6c592", 
       "PresentationTimeRange":{   
          "StartTimestamp":"0", 
          "EndTimestamp":"9223372036854775807", 
          "PresentationWindowDuration":"12000000000", 
          "LiveBackoffDuration":"0", 
          "Timescale":"10000000" 
       }, 
       "Tracks":[   
          {   
             "PropertyConditions": 
                  [   
                {   
                   "Property":"Type", 
                   "Value":"audio", 
                   "Operator":"Equal" 
                }, 
                {   
                   "Property":"Bitrate", 
                   "Value":"0-2147483647", 
                   "Operator":"Equal" 
                } 
             ] 
          } 
       ] 
    } 

#### <a name="http-response"></a>Réponse HTTP
    HTTP/1.1 201 Created 
    . . . 

## <a name="list-filters"></a>Liste des filtres
### <a name="get-all-global-filters-in-hello-ams-account"></a>Obtenir tous les global **filtre**s dans le compte de hello AMS
filtres de toolist, utilisez hello suivant des requêtes HTTP : 

#### <a name="http-request"></a>Demande HTTP
    GET https://media.windows.net/API/Filters HTTP/1.1 
    DataServiceVersion:3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    Host: media.windows.net 

### <a name="get-assetfilters-associated-with-an-asset"></a>Obtention des **AssetFilter**s associés à un élément multimédia
#### <a name="http-request"></a>Demande HTTP
    GET https://media.windows.net/API/Assets('nb%3Acid%3AUUID%3A536e555d-1500-80c3-92dc-f1e4fdc6c592')/AssetFilters HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000 
    Host: media.windows.net 

### <a name="get-an-assetfilter-based-on-its-id"></a>Obtention d'un **AssetFilter** en fonction de son ID
#### <a name="http-request"></a>Demande HTTP
    GET https://media.windows.net/API/AssetFilters('nb%3Acid%3AUUID%3A536e555d-1500-80c3-92dc-f1e4fdc6c592__%23%23%23__TestFilter') HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000


## <a name="update-filters"></a>Mise à jour des filtres
Utilisez PATCH, PUT ou fusion tooupdate un filtre avec les nouvelles valeurs de propriété.  Pour plus d'informations sur ces opérations, consultez [PATCH, PUT, MERGE](http://msdn.microsoft.com/library/dd541276.aspx).

Si vous mettez à jour un filtre, peut prendre jusqu'à minutes too2 de règles de hello toorefresh de point de terminaison de diffusion en continu. Si le contenu hello a été traitée à l’aide de ce filtre (et mises en cache proxys et CDN caches), mise à jour de ce filtre peut entraîner des échecs de lecteur. Il est recommandé de cache de hello tooclear après la mise à jour de filtre de hello. Si cette option n'est pas possible, envisagez d'utiliser un filtre différent.  

### <a name="update-global-filters"></a>Mise à jour de filtres globaux
tooupdate un filtre global, utilisez hello suivant des requêtes HTTP : 

#### <a name="http-request"></a>Demande HTTP
En-têtes de requête : 

    MERGE https://media.windows.net/API/Filters('filterName') HTTP/1.1 
    DataServiceVersion:3.0 
    MaxDataServiceVersion: 3.0 
    Content-Type: application/json 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000 
    Host: media.windows.net 
    Content-Length: 384

Corps de la requête : 

    { 
       "Tracks":[   
          {   
             "PropertyConditions": 
             [   
                {   
                   "Property":"Type", 
                   "Value":"audio", 
                   "Operator":"Equal" 
                }, 
                {   
                   "Property":"Bitrate", 
                   "Value":"0-2147483647", 
                   "Operator":"Equal" 
                } 
             ] 
          } 
       ] 
    } 

### <a name="update-local-assetfilters"></a>Mise à jour d’AssetFilters locaux
tooupdate un filtre local, utilisez hello suivant des requêtes HTTP : 

#### <a name="http-request"></a>Demande HTTP
En-têtes de requête : 

    MERGE https://media.windows.net/API/AssetFilters('nb%3Acid%3AUUID%3A536e555d-1500-80c3-92dc-f1e4fdc6c592__%23%23%23__TestFilter')  HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Content-Type: application/json 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000 
    Host: media.windows.net 

Corps de la requête : 

    { 
       "Tracks":[   
          {   
             "PropertyConditions": 
             [   
                {   
                   "Property":"Type", 
                   "Value":"audio", 
                   "Operator":"Equal" 
                }, 
                {   
                   "Property":"Bitrate", 
                   "Value":"0-2147483647", 
                   "Operator":"Equal" 
                } 
             ] 
          } 
       ] 
    } 


## <a name="delete-filters"></a>Suppression de filtres
### <a name="delete-global-filters"></a>Suppression de filtres globaux
toodelete un filtre global, utilisez hello suivant des requêtes HTTP :

#### <a name="http-request"></a>Demande HTTP
    DELETE https://media.windows.net/api/Filters('GlobalFilter') HTTP/1.1 
    DataServiceVersion:3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    Host: media.windows.net 


### <a name="delete-local-assetfilters"></a>Suppression d'AssetFilters locaux
toodelete un AssetFilter local, utilisez hello suivant des requêtes HTTP :

#### <a name="http-request"></a>Demande HTTP
    DELETE https://media.windows.net/API/AssetFilters('nb%3Acid%3AUUID%3A536e555d-1500-80c3-92dc-f1e4fdc6c592__%23%23%23__LocalFilter') HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    Host: media.windows.net 

## <a name="build-streaming-urls-that-use-filters"></a>Création d'URL de diffusion qui utilisent des filtres
Pour plus d’informations sur comment toopublish et proposer vos éléments multimédias, consultez [tooCustomers de fourniture de contenu vue d’ensemble](media-services-deliver-content-overview.md).

Hello exemples suivants montrent comment tooadd filtre tooyour URL de diffusion en continu.

**MPEG DASH** 

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=mpd-time-csf, filter=MyFilter)

**Apple HTTP Live Streaming (HLS) V4**

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl, filter=MyFilter)

**Apple HTTP Live Streaming (HLS) V3**

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl-v3, filter=MyFilter)

**Smooth Streaming**

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(filter=MyFilter)

    
## <a name="media-services-learning-paths"></a>Parcours d’apprentissage de Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Voir aussi
[Vue d'ensemble des manifestes dynamiques](media-services-dynamic-manifest-overview.md)
