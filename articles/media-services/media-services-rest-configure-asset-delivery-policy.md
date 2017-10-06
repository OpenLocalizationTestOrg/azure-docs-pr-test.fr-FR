---
title: "stratégies de remise aaaConfiguring actif à l’aide des API REST Media Services | Documents Microsoft"
description: "Cette rubrique montre comment tooconfigure des stratégies de remise différents actif à l’aide des API REST Media Services."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 5cb9d32a-e68b-4585-aa82-58dded0691d0
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: 8203230d570935e17382c598820dbfe42f83f8d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-asset-delivery-policies"></a>Configuration des stratégies de remise de ressources
[!INCLUDE [media-services-selector-asset-delivery-policy](../../includes/media-services-selector-asset-delivery-policy.md)]

Si vous envisagez toodeliver dynamiquement chiffré actifs, une des hello étapes Bonjour Media Services de contenu de flux de travail de remise consiste à configurer des stratégies de remise pour les ressources. stratégie de livraison des actifs Hello indique comment vous souhaitez pour votre toobe asset remis à Media Services : dans le protocole de diffusion en continu doit votre élément multimédia dynamiquement packagé (par exemple, MPEG DASH, HLS, Smooth Streaming ou tous), vous souhaitez toodynamically ou non chiffrer votre élément multimédia et comment (enveloppe ou chiffrement commun).

Cette rubrique explique pourquoi et comment toocreate et configurer des stratégies de remise d’élément multimédia.

>[!NOTE]
>Création de votre compte AMS un **par défaut** point de terminaison de diffusion en continu est ajoutée tooyour compte Bonjour **arrêté** état. toostart de diffusion en continu de votre contenu et profitez de l’empaquetage dynamique et chiffrement dynamique, hello de point de terminaison de diffusion en continu à partir de laquelle vous souhaitez que le contenu toostream a toobe Bonjour **en cours d’exécution** état. 
>
>En outre, toobe toouse en mesure de mise en package dynamique et le chiffrement dynamique votre élément multimédia doit contenir un ensemble de fichiers à débit adaptatif MP4s ou des fichiers de diffusion en continu lisse à débit adaptatif.

Vous pouvez appliquer différentes stratégies toohello même actif. Par exemple, vous pouvez appliquer PlayReady chiffrement tooSmooth diffusion en continu et l’enveloppe AES chiffrement tooMPEG DASH et HLS. Tous les protocoles qui ne sont pas définis dans une stratégie de remise (par exemple, vous ajoutez une stratégie unique qui spécifie seulement le HLS en tant que protocole de hello) sera bloquée à partir de la diffusion en continu. Hello exception toothis est si vous ne disposez d’aucune stratégie de remise actif du tout défini. Ensuite, tous les protocoles seront autorisés en hello clair.

Si vous voulez toodeliver un élément multimédia chiffré de stockage, vous devez configurer la stratégie de remise de l’élément multimédia hello. Avant que votre élément multimédia peut être transmis en continu, hello de diffusion en continu flux et chiffrement de stockage de serveur supprime hello votre contenu à l’aide de hello spécifié de stratégie de remise. Par exemple, toodeliver votre élément multimédia chiffré avec la clé de chiffrement d’enveloppe Standard (AES), définissez le type de stratégie hello trop**DynamicEnvelopeEncryption**. tooremove le chiffrement de stockage et les actifs de hello flux Bonjour claires, le type de stratégie hello défini trop**NoDynamicEncryption**. Exemples qui montrent comment tooconfigure suivent ces types de stratégie.

Selon la façon dont vous configurez la stratégie de livraison des actifs hello vous serait sera en mesure de toodynamically package, dynamiquement chiffrer et diffuser en continu hello suite de protocoles de diffusion en continu : Smooth Streaming, HLS, les flux MPEG DASH.

Hello suivant liste affiche hello met en forme que vous utilisez toostream Smooth, HLS, tiret.

Smooth Streaming :

{nom du point de terminaison de diffusion en continu-nom du compte media services}.streaming.mediaservices.windows.net/{ID_de_localisateur}/{nom_de_fichier}.ISM/Manifest

HLS :

{nom du point de terminaison de diffusion en continu-nom du compte media services}.streaming.mediaservices.windows.net/{ID_de_localisateur}/{nom_de_fichier}.ISM/Manifest(format=m3u8-aapl)

MPEG DASH

{nom du point de terminaison de diffusion en continu-nom du compte media services}.streaming.mediaservices.windows.net/{ID_de_localisateur}/{nom_de_fichier}.ISM/Manifest(format=mpd-time-csf)


Pour plus d’informations sur comment toopublish un élément multimédia et créer une URL de diffusion en continu, consultez [générer une URL de diffusion en continu](media-services-deliver-streaming-content.md).

## <a name="considerations"></a>Considérations
* Vous ne pouvez pas supprimer une stratégie AssetDeliveryPolicy associée à un élément multimédia alors qu’un localisateur (de diffusion en continuer) OnDemand existe pour cet élément. stratégie de hello tooremove à partir de l’élément multimédia de hello il est recommandé de Hello avant de supprimer la stratégie de hello.
* Il est impossible de créer un localisateur de diffusion en continu sur un élément multimédia chiffré de stockage quand aucune stratégie de distribution d’éléments multimédias n’est définie.  Si hello actif n’est pas chiffré de stockage, système de hello sera vous permettent de créer un élément multimédia hello de recherche et de flux Bonjour effacer sans une stratégie de livraison des actifs.
* Vous pouvez avoir plusieurs stratégies de remise actif associés à un seul élément multimédia, mais vous ne pouvez spécifier qu’une façon toohandle un AssetDeliveryProtocol donné.  Ce qui signifie que si vous essayez de toolink deux stratégies de remise qui spécifient le protocole AssetDeliveryProtocol.SmoothStreaming hello qui entraîne une erreur car le système de hello ne sait pas celui que vous souhaitez tooapply lorsqu’un client effectue une demande de diffusion en continu lisse.
* Si vous avez un élément multimédia avec un localisateur de diffusion en continu, Impossible de lier un élément multimédia de nouvelle stratégie toohello, dissocier une stratégie existante à partir de l’élément multimédia de hello ou mettre à jour une stratégie de remise associée hello actif.  Vous tout d’abord avez localisateur de diffusion en continu tooremove hello, ajustez les stratégies de hello, puis recréez hello localisateur de diffusion en continu.  Vous pouvez utiliser hello locatorId même lorsque vous recréez hello de diffusion en continu de la recherche, mais vous devez vous assurer que causer des problèmes pour les clients, car le contenu peut être mis en cache à l’origine de hello ou un CDN en aval.

>[!NOTE]

>Lors de l’accès aux entités dans Media Services, vous devez définir les valeurs et les champs d’en-tête spécifiques dans vos requêtes HTTP. Pour plus d'informations, consultez [Installation pour le développement REST API de Media Services](media-services-rest-how-to-use.md).

## <a name="connect-toomedia-services"></a>Connecter les Services de tooMedia

Pour plus d’informations sur la façon dont tooconnect toohello AMS API, consultez [hello accès API Azure Media Services avec l’authentification Azure AD](media-services-use-aad-auth-to-access-ams-api.md). 

>[!NOTE]
>Après vous être connecté toohttps://media.windows.net, vous recevrez une redirection 301 spécifiant un autre URI de Media Services. Vous devez effectuer les appels suivants toohello nouvel URI.

## <a name="clear-asset-delivery-policy"></a>Stratégie de remise de ressources
### <a id="create_asset_delivery_policy"></a>Création d’une stratégie de remise d’éléments multimédias
Hello requête HTTP suivante crée une stratégie de remise actif qui spécifie toonot appliquer le chiffrement dynamique et de protocoles de flux de données toodeliver hello dans un des hello suivant : protocoles MPEG DASH, HLS et Smooth Streaming. 

Pour plus d’informations sur les valeurs que vous pouvez spécifier lors de la création d’un AssetDeliveryPolicy, consultez hello [Types utilisés lors de la définition AssetDeliveryPolicy](#types) section.   

Demande :

    POST https://media.windows.net/api/AssetDeliveryPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amsaccount1&urn%3aSubscriptionId=zbbef702-e769-2233-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423397827&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=Szo6lbJAvL3dyecAeVmyAnzv3mGzfUNClR5shk9Ivbk%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 4651882c-d7ad-4d5e-86ab-f07f47dcb41e
    Host: media.windows.net

    {"Name":"Clear Policy",
    "AssetDeliveryProtocol":7,
    "AssetDeliveryPolicyType":2,
    "AssetDeliveryConfiguration":null}

Réponse :

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 363
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://media.windows.net/api/AssetDeliveryPolicies('nb%3Aadpid%3AUUID%3A92b0f6ba-3c9f-49b6-a5fa-2a8703b04ecd')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: 4651882c-d7ad-4d5e-86ab-f07f47dcb41e
    request-id: 6aedbf93-4bc2-4586-8845-fd45590136af
    x-ms-request-id: 6aedbf93-4bc2-4586-8845-fd45590136af
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 08 Feb 2015 06:21:27 GMT

    {"odata.metadata":"https://media.windows.net/api/$metadata#AssetDeliveryPolicies/@Element",
    "Id":"nb:adpid:UUID:92b0f6ba-3c9f-49b6-a5fa-2a8703b04ecd",
    "Name":"Clear Policy",
    "AssetDeliveryProtocol":7,
    "AssetDeliveryPolicyType":2,
    "AssetDeliveryConfiguration":null,
    "Created":"2015-02-08T06:21:27.6908329Z",
    "LastModified":"2015-02-08T06:21:27.6908329Z"}

### <a id="link_asset_with_asset_delivery_policy"></a>Liaison d’un élément multimédia à la stratégie de remise d’élément multimédia
Hello suivant hello de liens de demande HTTP spécifié asset toohello asset remise stratégie.

Demande :

    POST https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3A86933344-9539-4d0c-be7d-f842458693e0')/$links/DeliveryPolicies HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Content-Type: application/json
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amsaccount1&urn%3aSubscriptionId=zbbef702-e769-3344-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423397827&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=Szo6lbJAvL3dyecAeVmyAnzv3mGzfUNClR5shk9Ivbk%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 56d2763f-6e72-419d-ba3c-685f6db97e81
    Host: media.windows.net

    {"uri":"https://media.windows.net/api/AssetDeliveryPolicies('nb%3Aadpid%3AUUID%3A92b0f6ba-3c9f-49b6-a5fa-2a8703b04ecd')"}

Réponse :

    HTTP/1.1 204 No Content


## <a name="dynamicenvelopeencryption-asset-delivery-policy"></a>Stratégie de remise de ressources DynamicEnvelopeEncryption
### <a name="create-content-key-of-hello-envelopeencryption-type-and-link-it-toohello-asset"></a>Créer la clé de contenu de type de EnvelopeEncryption hello et le lier toohello actif
Lorsque vous spécifiez la stratégie de livraison DynamicEnvelopeEncryption, vous devez toomake des toolink que votre clé de contenu tooa asset Hello EnvelopeEncryption type. Pour plus d’informations, consultez la page [Création d’une clé de contenu](media-services-rest-create-contentkey.md)).

### <a id="get_delivery_url"></a>Obtention de l’URL de remise
URL de remise Get hello pour hello spécifié méthode de remise de clé de contenu hello créé à l’étape précédente de hello. Un client utilise hello retourné URL toorequest une clé AES ou une licence PlayReady Bonjour tooplayback de commande du contenu protégé.

Spécifiez type hello de hello URL tooget dans le corps hello de requête HTTP de hello. Si vous protégez votre contenu avec PlayReady, demandez une URL d’acquisition de licence PlayReady de Media Services, à l’aide de 1 pour hello keyDeliveryType : {« keyDeliveryType » : 1}. Si vous protégez votre contenu avec chiffrement d’enveloppe hello, demandez une URL d’acquisition de clé en spécifiant 2 pour keyDeliveryType : {« keyDeliveryType » : 2}.

Demande :

    POST https://media.windows.net/api/ContentKeys('nb:kid:UUID:dc88f996-2859-4cf7-a279-c52a9d6b2f04')/GetKeyDeliveryUrl HTTP/1.1
    Content-Type: application/json
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amsaccount1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423452029&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=IEXV06e3drSIN5naFRBdhJZCbfEqQbFZsGSIGmawhEo%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 569d4b7c-a446-4edc-b77c-9fb686083dd8
    Host: media.windows.net
    Content-Length: 21

    {"keyDeliveryType":2}

Réponse :

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 198
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: 569d4b7c-a446-4edc-b77c-9fb686083dd8
    request-id: d26f65d2-fe65-4136-8fcf-31545be68377
    x-ms-request-id: d26f65d2-fe65-4136-8fcf-31545be68377
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 08 Feb 2015 21:42:30 GMT

    {"odata.metadata":"media.windows.net/api/$metadata#Edm.String","value":"https://amsaccount1.keydelivery.mediaservices.windows.net/?KID=dc88f996-2859-4cf7-a279-c52a9d6b2f04"}


### <a name="create-asset-delivery-policy"></a>Création d’une stratégie de remise d’éléments multimédias
requête HTTP suivante Hello crée hello **AssetDeliveryPolicy** tooapply configuré qui est le chiffrement dynamique enveloppe (**DynamicEnvelopeEncryption**) toohello **HLS**protocole (dans cet exemple, d’autres protocoles seront bloqués de diffusion en continu). 

Pour plus d’informations sur les valeurs que vous pouvez spécifier lors de la création d’un AssetDeliveryPolicy, consultez hello [Types utilisés lors de la définition AssetDeliveryPolicy](#types) section.   

Demande :

    POST https://media.windows.net/api/AssetDeliveryPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amsaccount1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423480651&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=T2FG3tIV0e2ETzxQ6RDWxWAsAzuy3ez2ruXPhrBe62Y%3d
    x-ms-version: 2.11
    x-ms-client-request-id: fff319f6-71dd-4f6c-af27-b675c0066fa7
    Host: media.windows.net

    {"Name":"AssetDeliveryPolicy","AssetDeliveryProtocol":4,"AssetDeliveryPolicyType":3,"AssetDeliveryConfiguration":"[{\"Key\":2,\"Value\":\"https:\\/\\/amsaccount1.keydelivery.mediaservices.windows.net\\/\"}]"}


Réponse :

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 460
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: media.windows.net/api/AssetDeliveryPolicies('nb%3Aadpid%3AUUID%3Aec9b994e-672c-4a5b-8490-a464eeb7964b')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: fff319f6-71dd-4f6c-af27-b675c0066fa7
    request-id: c2a1ac0e-9644-474f-b38f-b9541c3a7c5f
    x-ms-request-id: c2a1ac0e-9644-474f-b38f-b9541c3a7c5f
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 09 Feb 2015 05:24:38 GMT

    {"odata.metadata":"media.windows.net/api/$metadata#AssetDeliveryPolicies/@Element","Id":"nb:adpid:UUID:ec9b994e-672c-4a5b-8490-a464eeb7964b","Name":"AssetDeliveryPolicy","AssetDeliveryProtocol":4,"AssetDeliveryPolicyType":3,"AssetDeliveryConfiguration":"[{\"Key\":2,\"Value\":\"https:\\/\\/amsaccount1.keydelivery.mediaservices.windows.net\\/\"}]","Created":"2015-02-09T05:24:38.9167436Z","LastModified":"2015-02-09T05:24:38.9167436Z"}


### <a name="link-asset-with-asset-delivery-policy"></a>Liaison d’un élément multimédia à la stratégie de remise d’élément multimédia
Consultez la rubrique [Liaison d’un élément multimédia à la stratégie de remise d’élément multimédia](#link_asset_with_asset_delivery_policy)

## <a name="dynamiccommonencryption-asset-delivery-policy"></a>Stratégie de remise de ressources DynamicCommonEncryption
### <a name="create-content-key-of-hello-commonencryption-type-and-link-it-toohello-asset"></a>Créer la clé de contenu de type de CommonEncryption hello et le lier toohello actif
Lorsque vous spécifiez la stratégie de livraison DynamicCommonEncryption, vous devez toomake des toolink que votre clé de contenu tooa asset Hello CommonEncryption type. Pour plus d’informations, consultez la page [Création d’une clé de contenu](media-services-rest-create-contentkey.md)).

### <a name="get-delivery-url"></a>Obtention de l’URL de remise
Obtenir l’URL de remise hello hello PlayReady mode de livraison de la clé de contenu hello créé à l’étape précédente de hello. Un client utilise hello retourné toorequest URL protégée par une licence PlayReady Bonjour tooplayback de commande contenu. Pour plus d’informations, consultez la rubrique [Obtention de l’URL de remise](#get_delivery_url).

### <a name="create-asset-delivery-policy"></a>Création d’une stratégie de remise d’éléments multimédias
requête HTTP suivante Hello crée hello **AssetDeliveryPolicy** tooapply configuré qui est le chiffrement commun dynamique (**DynamicCommonEncryption**) toohello **Smooth Streaming**  protocole (dans cet exemple, d’autres protocoles seront bloqués de diffusion en continu). 

Pour plus d’informations sur les valeurs que vous pouvez spécifier lors de la création d’un AssetDeliveryPolicy, consultez hello [Types utilisés lors de la définition AssetDeliveryPolicy](#types) section.   

Demande :

    POST https://media.windows.net/api/AssetDeliveryPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amsaccount1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423480651&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=T2FG3tIV0e2ETzxQ6RDWxWAsAzuy3ez2ruXPhrBe62Y%3d
    x-ms-version: 2.11
    x-ms-client-request-id: fff319f6-71dd-4f6c-af27-b675c0066fa7
    Host: media.windows.net

    {"Name":"AssetDeliveryPolicy","AssetDeliveryProtocol":1,"AssetDeliveryPolicyType":4,"AssetDeliveryConfiguration":"[{\"Key\":2,\"Value\":\"https:\\/\\/amsaccount1.keydelivery.mediaservices.windows.net\/PlayReady\/"}]"}


Si vous souhaitez tooprotect votre contenu à l’aide de Widevine DRM, mettre à jour hello AssetDeliveryConfiguration valeurs toouse WidevineLicenseAcquisitionUrl (qui a la valeur hello 7) et spécifiez les URL de hello d’un service de remise de licences. Vous pouvez utiliser hello suivant toohelp de partenaires AMS vous fournir des licences Widevine : [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).

Par exemple : 

    {"Name":"AssetDeliveryPolicy","AssetDeliveryProtocol":2,"AssetDeliveryPolicyType":4,"AssetDeliveryConfiguration":"[{\"Key\":7,\"Value\":\"https:\\/\\/example.net\/WidevineLicenseAcquisition\/"}]"}

> [!NOTE]
> Lors du chiffrement avec Widevine, vous serez uniquement en mesure de toodeliver à l’aide de tiret. Vérifiez le protocole de livraison actif que toospecify tiret hello en (2).
> 
> 

### <a name="link-asset-with-asset-delivery-policy"></a>Liaison d’un élément multimédia à la stratégie de remise d’élément multimédia
Consultez la rubrique [Liaison d’un élément multimédia à la stratégie de remise d’élément multimédia](#link_asset_with_asset_delivery_policy)

## <a id="types"></a>Types utilisés durant la définition de AssetDeliveryPolicy

### <a name="assetdeliveryprotocol"></a>AssetDeliveryProtocol

Hello enum suivant décrit les valeurs que vous pouvez définir pour le protocole de remise hello actif.

    [Flags]
    public enum AssetDeliveryProtocol
    {
        /// <summary>
        /// No protocols.
        /// </summary>
        None = 0x0,

        /// <summary>
        /// Smooth streaming protocol.
        /// </summary>
        SmoothStreaming = 0x1,

        /// <summary>
        /// MPEG Dynamic Adaptive Streaming over HTTP (DASH)
        /// </summary>
        Dash = 0x2,

        /// <summary>
        /// Apple HTTP Live Streaming protocol.
        /// </summary>
        HLS = 0x4,

        ProgressiveDownload = 0x10, 
 
        /// <summary>
        /// Include all protocols.
        /// </summary>
        All = 0xFFFF
    }

### <a name="assetdeliverypolicytype"></a>AssetDeliveryPolicyType

Hello enum suivant décrit les valeurs que vous pouvez définir pour le type de stratégie de remise hello asset.  

    public enum AssetDeliveryPolicyType
    {
        /// <summary>
        /// Delivery Policy Type not set.  An invalid value.
        /// </summary>
        None,

        /// <summary>
        /// hello Asset should not be delivered via this AssetDeliveryProtocol. 
        /// </summary>
        Blocked, 

        /// <summary>
        /// Do not apply dynamic encryption toohello asset.
        /// </summary>
        /// 
        NoDynamicEncryption,  

        /// <summary>
        /// Apply Dynamic Envelope encryption.
        /// </summary>
        DynamicEnvelopeEncryption,

        /// <summary>
        /// Apply Dynamic Common encryption.
        /// </summary>
        DynamicCommonEncryption
        }

### <a name="contentkeydeliverytype"></a>ContentKeyDeliveryType

Hello enum suivant décrit les valeurs que vous pouvez utiliser la méthode de remise tooconfigure hello du client de contenu toohello clé hello.
    
    public enum ContentKeyDeliveryType
    {
        /// <summary>
        /// None.
        ///
        </summary>
        None = 0,

        /// <summary>
        /// Use PlayReady License acquistion protocol
        ///
        </summary>
        PlayReadyLicense = 1,

        /// <summary>
        /// Use MPEG Baseline HTTP key protocol.
        ///
        </summary>
        BaselineHttp = 2,

        /// <summary>
        /// Use Widevine License acquistion protocol
        ///
        </summary>
        Widevine = 3

    }


### <a name="assetdeliverypolicyconfigurationkey"></a>AssetDeliveryPolicyConfigurationKey

Hello suivant enum décrit les valeurs que vous pouvez définir la configuration spécifique du tooget tooconfigure clés utilisées pour une stratégie de livraison des actifs.

    public enum AssetDeliveryPolicyConfigurationKey
    {
        /// <summary>
        /// No policies.
        /// </summary>
        None,

        /// <summary>
        /// Exact Envelope key URL.
        /// </summary>
        EnvelopeKeyAcquisitionUrl,

        /// <summary>
        /// Base key url that will have KID=<Guid> appended for Envelope.
        /// </summary>
        EnvelopeBaseKeyAcquisitionUrl,

        /// <summary>
        /// hello initialization vector toouse for envelope encryption in Base64 format.
        /// </summary>
        EnvelopeEncryptionIVAsBase64,

        /// <summary>
        /// hello PlayReady License Acquisition Url toouse for common encryption.
        /// </summary>
        PlayReadyLicenseAcquisitionUrl,

        /// <summary>
        /// hello PlayReady Custom Attributes tooadd toohello PlayReady Content Header
        /// </summary>
        PlayReadyCustomAttributes,

        /// <summary>
        /// hello initialization vector toouse for envelope encryption.
        /// </summary>
        EnvelopeEncryptionIV,

        /// <summary>
        /// Widevine DRM acquisition url
        /// </summary>
        WidevineLicenseAcquisitionUrl
    }

## <a name="media-services-learning-paths"></a>Parcours d’apprentissage de Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

