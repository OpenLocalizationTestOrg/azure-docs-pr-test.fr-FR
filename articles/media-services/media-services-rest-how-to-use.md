---
title: "vue d’ensemble des API REST opérations Services aaaMedia | Documents Microsoft"
description: "Vue d’ensemble de l’API REST Media Services"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: a5f1c5e7-ec52-4e26-9a44-d9ea699f68d9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: b54f4d9123486d6cae832c9817688b0f3da5b401
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="media-services-operations-rest-api-overview"></a>Vue d’ensemble de l’API REST Media Services Operations
[!INCLUDE [media-services-selector-setup](../../includes/media-services-selector-setup.md)]

Hello **opérations REST de Media Services** API est utilisée pour la création de travaux, ressources, les stratégies d’accès et autres opérations sur des objets dans un compte de Service de support. Pour plus d’informations, consultez [Référence de l’API REST Media Services Operations](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference).

Microsoft Azure Media Services est un service qui accepte les demandes HTTP OData et peut répondre dans les formats JSON ou atom+pub détaillés. Étant donné que Media Services sont conformes aux règles de conception tooAzure, il existe un ensemble d’en-têtes HTTP obligatoires que chaque client doit utiliser lors de la connexion des Services de tooMedia, ainsi que d’un ensemble d’en-têtes facultatifs qui peut être utilisé. Hello sections suivantes décrivent les en-têtes hello et verbes HTTP que vous pouvez utiliser lorsque la création de demandes et recevoir des réponses à partir des Services de support.

Cette rubrique donne une vue d’ensemble de la façon v2 REST toouse avec Media Services.

## <a name="considerations"></a>Considérations

Hello suivant considérations s’appliquent lors de l’utilisation de REST.

* Lors de l’interrogation des entités, il existe une limite de 1000 entités retournées à la fois, car il est public reste v2 limite les résultats de too1000 de résultats de requête. Vous devez toouse **ignorer** et **prendre** (.NET) / **haut** (REST), comme décrit dans [cet exemple .NET](media-services-dotnet-manage-entities.md#enumerating-through-large-collections-of-entities) et [cette API REST exemple](media-services-rest-manage-entities.md#enumerating-through-large-collections-of-entities). 
* Lors de l’utilisation de JSON et en spécifiant toouse hello **__metadata** mot clé dans la demande de hello (par exemple, un objet lié tooreferences) vous devez définir hello **accepter** en-tête trop[format JSON détaillé ](http://www.odata.org/documentation/odata-version-3-0/json-verbose-format/) (voir hello exemple suivant). OData ne comprend pas hello **__metadata** propriété Bonjour demander, sauf si vous lui affectez tooverbose.  
  
        POST https://media.windows.net/API/Jobs HTTP/1.1
        Content-Type: application/json;odata=verbose
        Accept: application/json;odata=verbose
        DataServiceVersion: 3.0
        MaxDataServiceVersion: 3.0
        x-ms-version: 2.11
        Authorization: Bearer <token> 
        Host: media.windows.net
  
        {
            "Name" : "NewTestJob", 
            "InputMediaAssets" : 
                [{"__metadata" : {"uri" : "https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3Aba5356eb-30ff-4dc6-9e5a-41e4223540e7')"}}]
        . . . 

## <a name="standard-http-request-headers-supported-by-media-services"></a>En-têtes de requête HTTP standard pris en charge par Media Services
Pour chaque appel que vous apportez dans Media Services, il existe un ensemble d’en-têtes obligatoires, vous devez inclure dans votre demande et un ensemble d’en-têtes facultatifs vous pouvez également tooinclude. Hello suivant table listes hello requis en-têtes :

| En-tête | Type | Valeur |
| --- | --- | --- |
| Autorisation |Support |Le support est hello acceptées uniquement le mécanisme d’autorisation. valeur de Hello doit également inclure hello accès jeton fourni par ACS. |
| x-ms-version |Décimal |2.11 |
| DataServiceVersion |Décimal |3.0 |
| MaxDataServiceVersion |Décimal |3.0 |

> [!NOTE]
> Étant donné que Media Services utilise OData tooexpose son référentiel de métadonnées asset sous-jacent via les API REST, hello DataServiceVersion et MaxDataServiceVersion en-têtes doit être inclus dans une demande ; Toutefois, si elles ne sont pas, puis Media Services suppose valeur DataServiceVersion de hello à utiliser est 3.0.
> 
> 

Hello Voici un ensemble d’en-têtes facultatifs :

| En-tête | Type | Valeur |
| --- | --- | --- |
| Date |Date RFC 1123 |Horodatage de la demande de hello |
| Acceptation |Type de contenu |Hello demandé le type de contenu de réponse hello tels que les suivants hello :<p> -application/json;odata=verbose<p> - application/atom+xml<p> Les réponses peuvent avoir un type de contenu différents, comme une extraction d’objets blob, où une réponse correcte contient le flux d’objets blob hello comme charge utile de hello. |
| Accept-Encoding |Gzip, deflate |Codage GZIP et DEFLATE, le cas échéant. Remarque : pour les ressources volumineuses, Media Services peut ignorer cet en-tête et retourner des données non compressées. |
| Accept-Language |« en », « es » et ainsi de suite. |Spécifie la langue de hello préféré pour la réponse de hello. |
| Accept-Charset |Type de jeu de caractères comme « UTF-8 » |La valeur par défaut est UTF-8. |
| X-HTTP-Method |Méthode HTTP |Permet aux clients ou un pare-feu qui ne prennent pas en charge les méthodes HTTP telles que PUT ou DELETE toouse ces méthodes, tunnel établis via un appel GET. |
| Content-Type |Type de contenu |Contenu de type hello du corps de demande dans les demandes PUT ou POST. |
| client-request-id |String |Une valeur défini par l’appelant qui identifie hello donnée de demande. Si spécifié, cette valeur sera incluse dans le message de réponse hello en tant que moyen toomap hello demande. <p><p>**Important**<p>Les valeurs doivent être limitées à 2096 b (2k). |

## <a name="standard-http-response-headers-supported-by-media-services"></a>En-têtes de réponse HTTP standard pris en charge par Media Services
Hello Voici un ensemble d’en-têtes qui peuvent être retournées tooyou en fonction de la ressource hello demandée et hello action que vous vouliez tooperform.

| En-tête | Type | Valeur |
| --- | --- | --- |
| request-id |String |Identificateur unique pour l’opération en cours hello, générés par le service. |
| client-request-id |String |Un identificateur spécifié par l’appelant hello dans la demande d’origine hello, le cas échéant. |
| Date |Date RFC 1123 |date de Hello cette demande hello a été traitée. |
| Content-Type |Varie |type de contenu Hello hello du corps de réponse. |
| Content-Encoding |Varie |Gzip ou deflate, le cas échéant. |

## <a name="standard-http-verbs-supported-by-media-services"></a>Verbes HTTP standard pris en charge par Media Services
Hello Voici une liste complète des verbes HTTP qui peuvent être utilisés lors des demandes HTTP :

| Verbe | Description |
| --- | --- |
| GET |Retourne hello la valeur actuelle d’un objet. |
| POST |Crée un objet basé sur les données hello fournies, ou envoie une commande. |
| PUT |Remplace un objet ou crée un objet nommé (le cas échéant). |
| SUPPRIMER |Supprime un objet. |
| MERGE |Met à jour un objet existant avec des modifications de propriété nommées. |
| HEAD |Retourne les métadonnées d’un objet d’une réponse GET. |

## <a name="discover-media-services-model"></a>Découvrir le modèle Media Services
entités de Media Services toomake plus détectables, opération de hello $metadata peuvent être utilisées. Il vous permet de tooretrieve tous les types d’entité valide, les propriétés d’entité, associations, fonctions, actions et ainsi de suite. Hello suivant montre comment tooconstruct hello URI : https://media.windows.net/API/$ métadonnées.

Vous devez ajouter « ? api-version=2.x « fin toohello Hello URI si vous souhaitez que les métadonnées de hello tooview dans un navigateur, n’incluez pas d’en-tête x-ms-version de hello dans votre demande.

## <a name="connect-toomedia-services"></a>Connecter les Services de tooMedia

Pour plus d’informations sur la façon dont tooconnect toohello AMS API, consultez [hello accès API Azure Media Services avec l’authentification Azure AD](media-services-use-aad-auth-to-access-ams-api.md). Après vous être connecté toohttps://media.windows.net, vous recevrez une redirection 301 spécifiant un autre URI de Media Services. Vous devez effectuer les appels suivants toohello nouvel URI.

## <a name="next-steps"></a>Étapes suivantes

tooaccess AMS APIs avec REST, consultez [utilisent Azure AD authentication tooaccess hello API Azure Media Services avec REST](media-services-rest-connect-with-aad.md).

## <a name="media-services-learning-paths"></a>Parcours d’apprentissage de Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

