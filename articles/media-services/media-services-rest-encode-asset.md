---
title: "aaaHow tooencode une ressource Azure à l’aide de Media Encoder Standard | Documents Microsoft"
description: "Découvrez comment du contenu multimédia de tooencode Media Encoder Standard toouse sur Azure Media Services. Les exemples de code utilisent l’API REST."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 2a7273c6-8a22-4f82-9bfe-4509ff32d4a4
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: b766bafded7ee98eda3e6ef149c31d5d8fe406fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooencode-an-asset-by-using-media-encoder-standard"></a>Comment tooencode un élément multimédia à l’aide de Media Encoder Standard
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-encode-with-media-encoder-standard.md)
> * [REST](media-services-rest-encode-asset.md)
> * [Portail](media-services-portal-encode.md)
>
>

## <a name="overview"></a>Vue d'ensemble
toodeliver vidéo numérique sur hello Internet, vous devez compresser le média de hello. Fichiers vidéo numériques sont volumineux et peuvent être trop toodeliver hello Internet, ou, pour toodisplay des appareils de vos clients correctement. Encodage consiste hello compression vidéo et audio afin que vos clients puissent afficher votre contenu multimédia.

Travaux d’encodage est une des opérations les plus courantes traitement hello dans Azure Media Services. Vous créez des fichiers multimédias tooconvert travaux encodage à partir d’un tooanother de codage. Lorsque vous codez, vous pouvez utiliser hello encodeur Media Services intégré (Media Encoder Standard). Vous pouvez également utiliser un encodeur fourni par un partenaire Media Services. Les encodeurs tiers sont disponibles via hello Azure Marketplace. Vous pouvez spécifier les détails de hello des tâches d’encodage à l’aide de chaînes de présélection définies pour votre encodeur ou à l’aide de fichiers de configuration prédéfinis. types de hello toosee des paramètres prédéfinis qui sont disponibles, consultez [Présélections de tâches pour Media Encoder Standard](http://msdn.microsoft.com/library/mt269960).

Chaque tâche peut avoir l’une ou plusieurs tâches en fonction de type hello de traitement que vous souhaitez tooaccomplish. Via l’API REST de hello, vous pouvez créer des tâches et leurs tâches connexes de deux manières :

* Tâches peuvent être définies inline via la propriété de navigation hello tâches sur des entités Job.
* Utilisez le traitement par lots OData.

Nous vous recommandons de toujours encoder vos fichiers sources dans un ensemble de fichiers MP4 de débit adaptatif et de puis convertir le format désiré de hello ensemble toohello à l’aide de [empaquetage dynamique](media-services-dynamic-packaging-overview.md).

Si votre élément multimédia de sortie est chiffré de stockage, vous devez configurer la stratégie de livraison des actifs hello. Pour plus d'informations, consultez [Configuration de la stratégie de remise de ressources](media-services-rest-configure-asset-delivery-policy.md).

## <a name="considerations"></a>Considérations

Lors de l’accès aux entités dans Media Services, vous devez définir les valeurs et les champs d’en-tête spécifiques dans vos requêtes HTTP. Pour plus d'informations, consultez [Installation pour le développement REST API de Media Services](media-services-rest-how-to-use.md).

Avant de commencer, faisant référence à des processeurs multimédias, vérifiez que vous avez hello ID de processeur média approprié. Pour plus d’informations, consultez la rubrique [Obtenir des processeurs multimédias](media-services-rest-get-media-processor.md).

## <a name="connect-toomedia-services"></a>Connecter les Services de tooMedia

Pour plus d’informations sur la façon dont tooconnect toohello AMS API, consultez [hello accès API Azure Media Services avec l’authentification Azure AD](media-services-use-aad-auth-to-access-ams-api.md). 

>[!NOTE]
>Après vous être connecté toohttps://media.windows.net, vous recevrez une redirection 301 spécifiant un autre URI de Media Services. Vous devez effectuer les appels suivants toohello nouvel URI.

## <a name="create-a-job-with-a-single-encoding-task"></a>Création d’un travail avec une seule tâche d’encodage
> [!NOTE]
> Lorsque vous travaillez avec hello API REST Media Services, hello considérations suivantes s’appliquent :
>
> Lors de l’accès aux entités dans Media Services, vous devez définir les valeurs et les champs d’en-tête spécifiques dans vos requêtes HTTP. Pour plus d’informations, consultez [Installation pour le développement REST API de Media Services](media-services-rest-how-to-use.md).
>
> Après vous être connecté toohttps://media.windows.net, vous recevrez une redirection 301 spécifiant un autre URI de Media Services. Vous devez effectuer les appels suivants toohello nouvel URI. Pour plus d’informations sur la façon dont tooconnect toohello AMS API, consultez [hello accès API Azure Media Services avec l’authentification Azure AD](media-services-use-aad-auth-to-access-ams-api.md).
>
> Lors de l’utilisation de JSON et en spécifiant toouse hello **__metadata** mot clé dans la demande de hello (par exemple, tooreferences un objet lié), vous devez définir hello **accepter** en-tête trop[format JSON détaillé ](http://www.odata.org/documentation/odata-version-3-0/json-verbose-format/): Accepter : application/json ; odata = verbose.
>
>

Hello l’exemple suivant vous montre toocreate et valider un travail avec une seule tâche définition tooencode une vidéo à une résolution spécifique et la qualité. Quand vous encodez à l’aide de Media Encoder Standard, vous pouvez utiliser les présélections de configuration de tâche spécifiées [ici](http://msdn.microsoft.com/library/mt269960).

Demande :

    POST https://media.windows.net/API/Jobs HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000
    Host: media.windows.net

    {"Name" : "NewTestJob", "InputMediaAssets" : [{"__metadata" : {"uri" : "https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3Aaab7f15b-3136-4ddf-9962-e9ecb28fb9d2')"}}],  "Tasks" : [{"Configuration" : "Adaptive Streaming", "MediaProcessorId" : "nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",  "TaskBody" : "<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset>JobOutputAsset(0)</outputAsset></taskBody>"}]}

Réponse :

    HTTP/1.1 201 Created

    . . .

### <a name="set-hello-output-assets-name"></a>Définir le nom de l’élément multimédia de sortie de hello
Bonjour à l’exemple suivant montre comment tooset hello attribut assetName :

    { "TaskBody" : "<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset assetName=\"CustomOutputAssetName\">JobOutputAsset(0)</outputAsset></taskBody>"}

## <a name="considerations"></a>Considérations
* Propriétés TaskBody doivent utiliser le nombre de hello de toodefine littéral XML d’entrée, ou d’éléments multimédias de sortie qui sont utilisées par la tâche hello. la rubrique Hello contient hello définition de schéma XML pour hello XML.
* Bonjour définition de TaskBody, chaque interne valeur <inputAsset> et <outputAsset> doit être définie en tant que JobInputAsset(value) ou JobOutputAsset(value).
* Une tâche peut comporter plusieurs ressources de sortie. Un JobOutputAsset(x) ne peut être utilisé qu’une fois en tant que résultat d’une tâche dans un travail.
* Vous pouvez spécifier JobInputAsset ou JobOutputAsset en tant que ressource d’entrée d’une tâche.
* Les tâches ne doivent pas former un cycle.
* paramètre de valeur Hello que vous passez tooJobInputAsset ou JobOutputAsset représente la valeur d’index hello pour un élément multimédia. éléments multimédias réels de Hello sont définies dans hello InputMediaAssets et OutputMediaAssets des propriétés de navigation sur la définition de l’entité tâche hello.
* Comme Media Services repose sur OData v3, hello des éléments multimédias individuels dans hello InputMediaAssets et OutputMediaAssets des ensembles de propriétés de navigation sont référencés par un « __metadata : uri « paire nom-valeur.
* InputMediaAssets mappe tooone ou plus actifs que vous avez créé dans Media Services. Propriétés OutputMediaAssets sont créées par le système de hello. Ils ne font pas référence à une ressource existante.
* OutputMediaAssets peut être nommé en utilisant l’attribut assetName de hello. Si cet attribut n’est pas présent, nom hello Hello OutputMediaAsset est la valeur de texte interne hello Hello <outputAsset> élément est avec un suffixe de valeur de nom de la tâche hello ou valeur d’Id de tâche hello (dans le cas de hello où la propriété de nom hello n’est pas définie). Par exemple, si vous définissez une valeur pour assetName trop « Exemple », puis hello propriété a la valeur Name du OutputMediaAsset trop « Sample. » Toutefois, si vous n’avez pas de définir une valeur pour assetName, mais qui définissez le nom de la tâche hello trop « NewJob », puis hello Name du OutputMediaAsset serait « JobOutputAsset (valeur) _NewJob. »

## <a name="create-a-job-with-chained-tasks"></a>Création d’un travail avec des tâches chaînées
Dans de nombreux scénarios d’application, les développeurs souhaitent toocreate une série de tâches de traitement. Dans Media Services, vous pouvez créer une série de tâches chaînées. Chaque tâche effectue différentes étapes de traitement et peut utiliser différents processeurs multimédias. tâches de Hello chaînée peuvent transmettre une ressource à partir d’une tâche tooanother, exécution d’une séquence linéaire de tâches sur les actifs hello. Toutefois, les tâches de hello effectuées dans un travail ne sont pas requis toobe dans une séquence. Lorsque vous créez une tâche chaînée, hello chaînés **ITask** objets sont créés dans un seul **IJob** objet.

> [!NOTE]
> Il existe actuellement une limite de 30 tâches par travail. Si vous devez toochain plus de 30 tâches, vous pouvez créer plusieurs travaux toocontain des tâches hello.
>
>

    POST https://media.windows.net/api/Jobs HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000

    {  
       "Name":"NewTestJob",
       "InputMediaAssets":[  
          {  
             "__metadata":{  
                "uri":"https://testrest.cloudapp.net/api/Assets('nb%3Acid%3AUUID%3A910ffdc1-2e25-4b17-8a42-61ffd4b8914c')"
             }
          }
       ],
       "Tasks":[  
          {  
             "Configuration":"H264 Adaptive Bitrate MP4 Set 720p",
             "MediaProcessorId":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
             "TaskBody":"<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset>JobOutputAsset(0)</outputAsset></taskBody>"
          },
          {  
             "Configuration":"H264 Smooth Streaming 720p",
             "MediaProcessorId":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
             "TaskBody":"<?xml version=\"1.0\" encoding=\"utf-16\"?><taskBody><inputAsset>JobOutputAsset(0)</inputAsset><outputAsset>JobOutputAsset(1)</outputAsset></taskBody>"
          }
       ]
    }


### <a name="considerations"></a>Considérations
tooenable chaînage des tâches :

* un travail doit comporter au moins deux tâches.
* Il doit exister au moins une tâche dont l’entrée est sortie hello d’une autre tâche dans la tâche de hello.

## <a name="use-odata-batch-processing"></a>Utiliser le traitement par lots OData
Bonjour à l’exemple suivant montre comment toouse OData lot traitement toocreate un projet et les tâches. Pour plus d’informations sur le traitement par lots, consultez [Traitement par lots d’Open Data Protocol (OData)](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).

    POST https://media.windows.net/api/$batch HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Content-Type: multipart/mixed; boundary=batch_a01a5ec4-ba0f-4536-84b5-66c5a5a6d34e
    Accept: multipart/mixed
    Accept-Charset: UTF-8
    Authorization: Bearer <token>
    x-ms-version: 2.11
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000
    Host: media.windows.net


    --batch_a01a5ec4-ba0f-4536-84b5-66c5a5a6d34e
    Content-Type: multipart/mixed; boundary=changeset_122fb0a4-cd80-4958-820f-346309967e4d

    --changeset_122fb0a4-cd80-4958-820f-346309967e4d
    Content-Type: application/http
    Content-Transfer-Encoding: binary

    POST https://media.windows.net/api/Jobs HTTP/1.1
    Content-ID: 1
    Content-Type: application/json
    Accept: application/json
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    Accept-Charset: UTF-8
    Authorization: Bearer <token>
    x-ms-version: 2.11
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000

    {"Name" : "NewTestJob", "InputMediaAssets@odata.bind":["https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3A2a22445d-1500-80c6-4b34-f1e5190d33c6')"]}

    --changeset_122fb0a4-cd80-4958-820f-346309967e4d
    Content-Type: application/http
    Content-Transfer-Encoding: binary

    POST https://media.windows.net/api/$1/Tasks HTTP/1.1
    Content-ID: 2
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    Accept-Charset: UTF-8
    Authorization: Bearer <token>
    x-ms-version: 2.11
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000

    {  
       "Configuration":"H264 Adaptive Bitrate MP4 Set 720p",
       "MediaProcessorId":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
       "TaskBody":"<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset assetName=\"Custom output name\">JobOutputAsset(0)</outputAsset></taskBody>"
    }

    --changeset_122fb0a4-cd80-4958-820f-346309967e4d--
    --batch_a01a5ec4-ba0f-4536-84b5-66c5a5a6d34e--



## <a name="create-a-job-by-using-a-jobtemplate"></a>Création d’un travail à l’aide d’un JobTemplate
Lorsque vous traitez plusieurs éléments multimédias à l’aide d’un jeu commun de tâches, utilisez qu'une tâche par défaut de JobTemplate toospecify hello prédéfinis ou ordre de hello tooset des tâches.

Bonjour à l’exemple suivant montre comment toocreate un JobTemplate avec un TaskTemplate qui est définie en ligne. Hello TaskTemplate utilise hello Media Encoder Standard en tant que fichier d’élément multimédia hello MediaProcessor tooencode hello. Toutefois, d’autres MediaProcessors peuvent être également utilisés.

    POST https://media.windows.net/API/JobTemplates HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    Host: media.windows.net


    {"Name" : "NewJobTemplate25", "JobTemplateBody" : "<?xml version=\"1.0\" encoding=\"utf-8\"?><jobTemplate><taskBody taskTemplateId=\"nb:ttid:UUID:071370A3-E63E-4E81-A099-AD66BCAC3789\"><inputAsset>JobInputAsset(0)</inputAsset><outputAsset>JobOutputAsset(0)</outputAsset></taskBody></jobTemplate>", "TaskTemplates" : [{"Id" : "nb:ttid:UUID:071370A3-E63E-4E81-A099-AD66BCAC3789", "Configuration" : "H264 Smooth Streaming 720p", "MediaProcessorId" : "nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56", "Name" : "SampleTaskTemplate2", "NumberofInputAssets" : 1, "NumberofOutputAssets" : 1}] }


> [!NOTE]
> Contrairement à d’autres entités Media Services, vous devez définir un nouvel identificateur GUID pour chaque TaskTemplate et placez-le dans Propriétés hello taskTemplateId et Id dans le corps de la demande. schéma d’identification du contenu Hello doit suivre hello schéma décrit dans identifier les entités Azure Media Services. En outre, les JobTemplates ne peuvent pas être mis à jour. À la place, vous devez en créer un avec vos modifications mises à jour.
>
>

En cas de réussite, hello suivant la réponse est retournée :

    HTTP/1.1 201 Created

    . . .


Hello suivant montre l’exemple de comment toocreate un travail qui fait référence à un JobTemplate Id :

    POST https://media.windows.net/API/Jobs HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    Host: media.windows.net


    {"Name" : "NewTestJob", "InputMediaAssets" : [{"__metadata" : {"uri" : "https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3A3f1fe4a2-68f5-4190-9557-cd45beccef92')"}}], "TemplateId" : "nb:jtid:UUID:15e6e5e6-ac85-084e-9dc2-db3645fbf0aa"}


En cas de réussite, hello suivant la réponse est retournée :

    HTTP/1.1 201 Created

    . . .



## <a name="media-services-learning-paths"></a>Parcours d’apprentissage de Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous savez comment toocreate un tooencode de travail un élément multimédia, consultez [comment toocheck travail progression avec Media Services](media-services-rest-check-job-progress.md).

## <a name="see-also"></a>Voir aussi
[Obtenir des processeurs multimédias](media-services-rest-get-media-processor.md)
