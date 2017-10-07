---
title: "aaaConnecting tooMedia compte de Services à l’aide des API REST | Documents Microsoft"
description: Cette rubrique montre comment utiliser de Services tooconnect tooMedia REST API.
services: media-services
documentationcenter: 
author: Juliako
manager: erikre
editor: 
ms.assetid: 79dc64f1-15d8-4a81-b9d9-3d3c44d2e1e8
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 09/26/2016
ms.author: juliako
ms.openlocfilehash: 1d5064a3612dc96f5c5ad910d183d84fb70a3b6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-toomedia-services-account-using-media-services-rest-api"></a>Connexion tooMedia compte de Services à l’aide des API REST Media Services
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-connect-programmatically.md)
> * [REST](media-services-rest-connect-programmatically.md)
> 
> 

Cette rubrique décrit comment tooobtain un tooMicrosoft de connexion par programmation Azure Media Services lorsque vous programmez avec hello API REST Media Services.

Deux éléments sont requis pour accéder à Microsoft Azure Media Services : un jeton d’accès fourni par Azure Access Control Services (ACS) et hello URI de Media Services lui-même. Vous pouvez utiliser la méthode de que votre choix lors de la création de ces demandes tant que vous spécifiez des valeurs d’en-tête correctes hello et transmettez correctement dans le jeton d’accès hello lors de l’appel dans Media Services.

Hello comme suit décrire les flux de travail courants hello lorsque des Services à l’aide de hello API REST Media Services tooconnect tooMedia :

1. Obtention d’un jeton d’accès 
2. Connexion toohello URI Media Services 
   
   > [!NOTE]
   > Après vous être connecté toohttps://media.windows.net, vous recevrez une redirection 301 spécifiant un autre URI de Media Services. Vous devez effectuer les appels suivants toohello nouvel URI.
   > Vous pouvez également recevoir une réponse HTTP/1.1 200 contenant hello description de métadonnées des API ODATA.
   > 
   > 
3. Valider votre API suivants appelle toohello nouvelle URL. 
   
    Par exemple, si, après la tentative de tooconnect, que vous avez obtenu suivant de hello :
   
        HTTP/1.1 301 Moved Permanently
        Location: https://wamsbayclus001rest-hs.cloudapp.net/api/
   
    Vous devez enregistrer votre ultérieures API appels toohttps://wamsbayclus001rest-hs.cloudapp.net/api/.

    >[!NOTE]
    >Un nombre limite de 1 000 000 a été défini pour les différentes stratégies AMS (par exemple, pour la stratégie de localisateur ou pour ContentKeyAuthorizationPolicy). Vous devez utiliser hello ID de stratégie même si vous utilisez toujours hello même jours / autorisations d’accès, par exemple, les stratégies pour les localisateurs sont tooremain prévue en place pendant une longue période (non-téléchargement stratégies). Pour plus d’informations, consultez [cette rubrique](media-services-dotnet-manage-entities.md#limit-access-policies) .

## <a name="access-control-address"></a>Adresse de contrôle d’accès
L’adresse de contrôle d’accès de Media Services est https://wamsprodglobal001acs.accesscontrol.windows.net (à l’exception de la région Chine du Nord, où l’adresse est https://wamsprodglobal001acs.accesscontrol.chinacloudapi.cn).

## <a name="getting-an-access-token"></a>Obtention d’un jeton d’accès
tooaccess Media Services directement via l’API REST de hello, extraire un jeton d’accès d’ACS et utilisez-le lors de chaque demande HTTP adressée en service de hello. Ce jeton est similaire tooother jetons fournis par ACS basée sur les revendications d’accès fournies dans l’en-tête hello d’une requête HTTP et à l’aide du protocole de hello OAuth v2. Il est inutile toute autre condition requise avant la connexion directe tooMedia Services.

Hello suivant montre en-tête de demande HTTP hello et tooretrieve du corps utilisé un jeton.

**En-tête**:

    POST https://wamsprodglobal001acs.accesscontrol.windows.net/v2/OAuth2-13 HTTP/1.1
    Content-Type: application/x-www-form-urlencoded
    Host: wamsprodglobal001acs.accesscontrol.windows.net
    Content-Length: 120
    Expect: 100-continue
    Connection: Keep-Alive
    Accept: application/json


**Corps**:

Vous avez besoin de hello tooprove client_id et client_secret de valeurs dans le corps hello de cette demande ; client_id et client_secret correspondent toohello AccountName et AccountKey valeurs, respectivement. Ces valeurs sont fournies tooyou par Media Services lorsque vous configurez votre compte. 

Notez que AccountKey hello pour votre compte Media Services doit être encodé en URL (consultez [encodage pourcentage](http://tools.ietf.org/html/rfc3986#section-2.1) lors de son utilisation en tant que valeur de client_secret hello dans votre demande de jeton d’accès.

    grant_type=client_credentials&client_id=ams_account_name&client_secret=URL_encoded_ams_account_key&scope=urn%3aWindowsAzureMediaServices


Par exemple : 

    grant_type=client_credentials&client_id=amstestaccount001&client_secret=wUNbKhNj07oqjqU3Ah9R9f4kqTJ9avPpfe6Pk3YZ7ng%3d&scope=urn%3aWindowsAzureMediaServices


Hello suivant montre réponse HTTP hello qui contient les accès hello jeton dans le corps de la réponse hello.

    HTTP/1.1 200 OK
    Cache-Control: no-cache, no-store
    Pragma: no-cache
    Content-Type: application/json; charset=utf-8
    Expires: -1
    request-id: a65150f5-2784-4a01-a4b7-33456187ad83
    X-Content-Type-Options: nosniff
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Thu, 15 Jan 2015 08:07:20 GMT
    Content-Length: 670

    {  
       "token_type":"http://schemas.xmlsoap.org/ws/2009/11/swt-token-profile-1.0",
       "access_token":"http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f19258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421330840&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=uf69n82KlqZmkJDNxhJkOxpyIpA2HDyeGUTtSnq1vlE%3d",
       "expires_in":"21600",
       "scope":"urn:WindowsAzureMediaServices"
    }


> [!NOTE]
> Il est recommandé de toocache hello « access_token » et « expires_in » valeurs tooan stockage externe. données du jeton Hello ultérieurement pourraient être récupérées à partir du stockage de hello et réutilisées dans vos appels d’API REST Media Services. Cela est particulièrement utile pour les scénarios où le jeton de hello peut être partagé en toute sécurité entre plusieurs processus ou ordinateurs.
> 
> 

Assurez-vous que valeur « expires_in » de hello toomonitor d’accès de hello jeton et mettre à jour vos appels d’API REST avec les nouveaux jetons en fonction des besoins.

### <a name="connecting-toohello-media-services-uri"></a>Connexion toohello URI Media Services
Hello URI racine de Media Services est https://media.windows.net/. Vous devez connecter initialement toothis URI, et si vous obtenez une redirection 301 en réponse, vous devez effectuer les appels suivants toohello nouvel URI. En outre, n’utilisez pas de logique de redirection automatique/de suivi dans vos demandes. Verbes HTTP et le corps de requête ne seront pas transférées toohello nouvel URI.

Notez cette racine hello URI pour le téléchargement des fichiers de ressources est https://yourstorageaccount.blob.core.windows.net/ où le nom de compte de stockage hello est hello celui que vous avez utilisé lors de la configuration de votre compte Media Services.

Hello, l’exemple suivant montre comment HTTP demande toohello Media Services URI racine (https://media.windows.net/). demande de Hello Obtient une redirection 301 en réponse. Hello demande suivante est à l’aide de hello nouvel URI (https://wamsbayclus001rest-hs.cloudapp.net/api/).     

**Demande HTTP**:

    GET https://media.windows.net/ HTTP/1.1
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f19258-6753-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421500579&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=ElVWXOnMVggFQl%2ft9vhdcv1qH1n%2fE8l3hRef4zPmrzg%3d
    x-ms-version: 2.11
    Accept: application/json
    Host: media.windows.net


**Réponse HTTP**:

    HTTP/1.1 301 Moved Permanently
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/
    Server: Microsoft-IIS/8.5
    request-id: 987d7652-497a-44e5-b815-f492e02aef97
    x-ms-request-id: 987d7652-497a-44e5-b815-f492e02aef97
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sat, 17 Jan 2015 07:44:53 GMT
    Content-Length: 164

    <html><head><title>Object moved</title></head><body>
    <h2>Object moved too<a href="https://wamsbayclus001rest-hs.cloudapp.net/api/">here</a>.</h2>
    </body></html>


**Requête HTTP** (à l’aide de hello nouvel URI) :

    GET https://wamsbayclus001rest-hs.cloudapp.net/api/ HTTP/1.1
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f19258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421500579&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=ElVWXOnMVggFQl%2ft9vhdcv1qH1n%2fE8l3hRef4zPmrzg%3d
    x-ms-version: 2.11
    Accept: application/json
    Host: wamsbayclus001rest-hs.cloudapp.net


**Réponse HTTP**:

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 1250
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    request-id: 5f52ea9d-177e-48fe-9709-24953d19f84a
    x-ms-request-id: 5f52ea9d-177e-48fe-9709-24953d19f84a
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sat, 17 Jan 2015 07:44:52 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata","value":[{"name":"AccessPolicies","url":"AccessPolicies"},{"name":"Locators","url":"Locators"},{"name":"ContentKeys","url":"ContentKeys"},{"name":"ContentKeyAuthorizationPolicyOptions","url":"ContentKeyAuthorizationPolicyOptions"},{"name":"ContentKeyAuthorizationPolicies","url":"ContentKeyAuthorizationPolicies"},{"name":"Files","url":"Files"},{"name":"Assets","url":"Assets"},{"name":"AssetDeliveryPolicies","url":"AssetDeliveryPolicies"},{"name":"IngestManifestFiles","url":"IngestManifestFiles"},{"name":"IngestManifestAssets","url":"IngestManifestAssets"},{"name":"IngestManifests","url":"IngestManifests"},{"name":"StorageAccounts","url":"StorageAccounts"},{"name":"Tasks","url":"Tasks"},{"name":"NotificationEndPoints","url":"NotificationEndPoints"},{"name":"Jobs","url":"Jobs"},{"name":"TaskTemplates","url":"TaskTemplates"},{"name":"JobTemplates","url":"JobTemplates"},{"name":"MediaProcessors","url":"MediaProcessors"},{"name":"EncodingReservedUnitTypes","url":"EncodingReservedUnitTypes"},{"name":"Operations","url":"Operations"},{"name":"StreamingEndpoints","url":"StreamingEndpoints"},{"name":"Channels","url":"Channels"},{"name":"Programs","url":"Programs"}]}



> [!NOTE]
> Une fois que vous obtenez hello nouvel URI, qui est hello URI qui doit être utilisé toocommunicate avec Media Services. 
> 
> 

## <a name="media-services-learning-paths"></a>Parcours d’apprentissage de Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

