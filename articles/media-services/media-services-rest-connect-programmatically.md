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
# <a name="connecting-toomedia-services-account-using-media-services-rest-api"></a><span data-ttu-id="9fcca-103">Connexion tooMedia compte de Services à l’aide des API REST Media Services</span><span class="sxs-lookup"><span data-stu-id="9fcca-103">Connecting tooMedia Services Account using Media Services REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9fcca-104">.NET</span><span class="sxs-lookup"><span data-stu-id="9fcca-104">.NET</span></span>](media-services-dotnet-connect-programmatically.md)
> * [<span data-ttu-id="9fcca-105">REST</span><span class="sxs-lookup"><span data-stu-id="9fcca-105">REST</span></span>](media-services-rest-connect-programmatically.md)
> 
> 

<span data-ttu-id="9fcca-106">Cette rubrique décrit comment tooobtain un tooMicrosoft de connexion par programmation Azure Media Services lorsque vous programmez avec hello API REST Media Services.</span><span class="sxs-lookup"><span data-stu-id="9fcca-106">This topic describes how tooobtain a programmatic connection tooMicrosoft Azure Media Services when you are programming with hello Media Services REST API.</span></span>

<span data-ttu-id="9fcca-107">Deux éléments sont requis pour accéder à Microsoft Azure Media Services : un jeton d’accès fourni par Azure Access Control Services (ACS) et hello URI de Media Services lui-même.</span><span class="sxs-lookup"><span data-stu-id="9fcca-107">Two things are required when accessing Microsoft Azure Media Services: An access token provided by Azure Access Control Services (ACS), and hello URI of Media Services itself.</span></span> <span data-ttu-id="9fcca-108">Vous pouvez utiliser la méthode de que votre choix lors de la création de ces demandes tant que vous spécifiez des valeurs d’en-tête correctes hello et transmettez correctement dans le jeton d’accès hello lors de l’appel dans Media Services.</span><span class="sxs-lookup"><span data-stu-id="9fcca-108">You can use any means you want when creating these requests as long as you specify hello correct header values and pass in hello access token correctly when calling into Media Services.</span></span>

<span data-ttu-id="9fcca-109">Hello comme suit décrire les flux de travail courants hello lorsque des Services à l’aide de hello API REST Media Services tooconnect tooMedia :</span><span class="sxs-lookup"><span data-stu-id="9fcca-109">hello following steps describe hello most common workflow when using hello Media Services REST API tooconnect tooMedia Services:</span></span>

1. <span data-ttu-id="9fcca-110">Obtention d’un jeton d’accès</span><span class="sxs-lookup"><span data-stu-id="9fcca-110">Getting an access token</span></span> 
2. <span data-ttu-id="9fcca-111">Connexion toohello URI Media Services</span><span class="sxs-lookup"><span data-stu-id="9fcca-111">Connecting toohello Media Services URI</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="9fcca-112">Après vous être connecté toohttps://media.windows.net, vous recevrez une redirection 301 spécifiant un autre URI de Media Services.</span><span class="sxs-lookup"><span data-stu-id="9fcca-112">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="9fcca-113">Vous devez effectuer les appels suivants toohello nouvel URI.</span><span class="sxs-lookup"><span data-stu-id="9fcca-113">You must make subsequent calls toohello new URI.</span></span>
   > <span data-ttu-id="9fcca-114">Vous pouvez également recevoir une réponse HTTP/1.1 200 contenant hello description de métadonnées des API ODATA.</span><span class="sxs-lookup"><span data-stu-id="9fcca-114">You may also receive a HTTP/1.1 200 response that contains hello ODATA API metadata description.</span></span>
   > 
   > 
3. <span data-ttu-id="9fcca-115">Valider votre API suivants appelle toohello nouvelle URL.</span><span class="sxs-lookup"><span data-stu-id="9fcca-115">Post your subsequent API calls toohello new URL.</span></span> 
   
    <span data-ttu-id="9fcca-116">Par exemple, si, après la tentative de tooconnect, que vous avez obtenu suivant de hello :</span><span class="sxs-lookup"><span data-stu-id="9fcca-116">For example, if after trying tooconnect, you got hello following:</span></span>
   
        HTTP/1.1 301 Moved Permanently
        Location: https://wamsbayclus001rest-hs.cloudapp.net/api/
   
    <span data-ttu-id="9fcca-117">Vous devez enregistrer votre ultérieures API appels toohttps://wamsbayclus001rest-hs.cloudapp.net/api/.</span><span class="sxs-lookup"><span data-stu-id="9fcca-117">You should post your subsequent API calls toohttps://wamsbayclus001rest-hs.cloudapp.net/api/.</span></span>

    >[!NOTE]
    ><span data-ttu-id="9fcca-118">Un nombre limite de 1 000 000 a été défini pour les différentes stratégies AMS (par exemple, pour la stratégie de localisateur ou pour ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="9fcca-118">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="9fcca-119">Vous devez utiliser hello ID de stratégie même si vous utilisez toujours hello même jours / autorisations d’accès, par exemple, les stratégies pour les localisateurs sont tooremain prévue en place pendant une longue période (non-téléchargement stratégies).</span><span class="sxs-lookup"><span data-stu-id="9fcca-119">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="9fcca-120">Pour plus d’informations, consultez [cette rubrique](media-services-dotnet-manage-entities.md#limit-access-policies) .</span><span class="sxs-lookup"><span data-stu-id="9fcca-120">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

## <a name="access-control-address"></a><span data-ttu-id="9fcca-121">Adresse de contrôle d’accès</span><span class="sxs-lookup"><span data-stu-id="9fcca-121">Access control address</span></span>
<span data-ttu-id="9fcca-122">L’adresse de contrôle d’accès de Media Services est https://wamsprodglobal001acs.accesscontrol.windows.net (à l’exception de la région Chine du Nord, où l’adresse est https://wamsprodglobal001acs.accesscontrol.chinacloudapi.cn).</span><span class="sxs-lookup"><span data-stu-id="9fcca-122">Media Services access control address is https://wamsprodglobal001acs.accesscontrol.windows.net, except for North China region, where it is https://wamsprodglobal001acs.accesscontrol.chinacloudapi.cn.</span></span>

## <a name="getting-an-access-token"></a><span data-ttu-id="9fcca-123">Obtention d’un jeton d’accès</span><span class="sxs-lookup"><span data-stu-id="9fcca-123">Getting an access token</span></span>
<span data-ttu-id="9fcca-124">tooaccess Media Services directement via l’API REST de hello, extraire un jeton d’accès d’ACS et utilisez-le lors de chaque demande HTTP adressée en service de hello.</span><span class="sxs-lookup"><span data-stu-id="9fcca-124">tooaccess Media Services directly through hello REST API, retrieve an access token from ACS and use it during every HTTP request you make into hello service.</span></span> <span data-ttu-id="9fcca-125">Ce jeton est similaire tooother jetons fournis par ACS basée sur les revendications d’accès fournies dans l’en-tête hello d’une requête HTTP et à l’aide du protocole de hello OAuth v2.</span><span class="sxs-lookup"><span data-stu-id="9fcca-125">This token is similar tooother tokens provided by ACS based on access claims provided in hello header of an HTTP request and using hello OAuth v2 protocol.</span></span> <span data-ttu-id="9fcca-126">Il est inutile toute autre condition requise avant la connexion directe tooMedia Services.</span><span class="sxs-lookup"><span data-stu-id="9fcca-126">You do not need any other prerequisites before directly connecting tooMedia Services.</span></span>

<span data-ttu-id="9fcca-127">Hello suivant montre en-tête de demande HTTP hello et tooretrieve du corps utilisé un jeton.</span><span class="sxs-lookup"><span data-stu-id="9fcca-127">hello following example shows hello HTTP request header and body used tooretrieve a token.</span></span>

<span data-ttu-id="9fcca-128">**En-tête**:</span><span class="sxs-lookup"><span data-stu-id="9fcca-128">**Header**:</span></span>

    POST https://wamsprodglobal001acs.accesscontrol.windows.net/v2/OAuth2-13 HTTP/1.1
    Content-Type: application/x-www-form-urlencoded
    Host: wamsprodglobal001acs.accesscontrol.windows.net
    Content-Length: 120
    Expect: 100-continue
    Connection: Keep-Alive
    Accept: application/json


<span data-ttu-id="9fcca-129">**Corps**:</span><span class="sxs-lookup"><span data-stu-id="9fcca-129">**Body**:</span></span>

<span data-ttu-id="9fcca-130">Vous avez besoin de hello tooprove client_id et client_secret de valeurs dans le corps hello de cette demande ; client_id et client_secret correspondent toohello AccountName et AccountKey valeurs, respectivement.</span><span class="sxs-lookup"><span data-stu-id="9fcca-130">You need tooprove hello client_id and client_secret values in hello body of this request; client_id and client_secret correspond toohello AccountName and AccountKey values, respectively.</span></span> <span data-ttu-id="9fcca-131">Ces valeurs sont fournies tooyou par Media Services lorsque vous configurez votre compte.</span><span class="sxs-lookup"><span data-stu-id="9fcca-131">These values are provided tooyou by Media Services when you set up your account.</span></span> 

<span data-ttu-id="9fcca-132">Notez que AccountKey hello pour votre compte Media Services doit être encodé en URL (consultez [encodage pourcentage](http://tools.ietf.org/html/rfc3986#section-2.1) lors de son utilisation en tant que valeur de client_secret hello dans votre demande de jeton d’accès.</span><span class="sxs-lookup"><span data-stu-id="9fcca-132">Note that hello AccountKey for your Media Services account must be URL-encoded (see [Percent-Encoding](http://tools.ietf.org/html/rfc3986#section-2.1) when using it as hello client_secret value in your access token request.</span></span>

    grant_type=client_credentials&client_id=ams_account_name&client_secret=URL_encoded_ams_account_key&scope=urn%3aWindowsAzureMediaServices


<span data-ttu-id="9fcca-133">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="9fcca-133">For example:</span></span> 

    grant_type=client_credentials&client_id=amstestaccount001&client_secret=wUNbKhNj07oqjqU3Ah9R9f4kqTJ9avPpfe6Pk3YZ7ng%3d&scope=urn%3aWindowsAzureMediaServices


<span data-ttu-id="9fcca-134">Hello suivant montre réponse HTTP hello qui contient les accès hello jeton dans le corps de la réponse hello.</span><span class="sxs-lookup"><span data-stu-id="9fcca-134">hello following example shows hello HTTP response that contains hello access token in hello response body.</span></span>

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
> <span data-ttu-id="9fcca-135">Il est recommandé de toocache hello « access_token » et « expires_in » valeurs tooan stockage externe.</span><span class="sxs-lookup"><span data-stu-id="9fcca-135">It is recommended toocache hello "access_token " and "expires_in " values tooan external storage.</span></span> <span data-ttu-id="9fcca-136">données du jeton Hello ultérieurement pourraient être récupérées à partir du stockage de hello et réutilisées dans vos appels d’API REST Media Services.</span><span class="sxs-lookup"><span data-stu-id="9fcca-136">hello token data could later be retrieved from hello storage and re-used in your Media Services REST API calls.</span></span> <span data-ttu-id="9fcca-137">Cela est particulièrement utile pour les scénarios où le jeton de hello peut être partagé en toute sécurité entre plusieurs processus ou ordinateurs.</span><span class="sxs-lookup"><span data-stu-id="9fcca-137">This is especially useful for scenarios where hello token can be securely shared among multiple processes or computers.</span></span>
> 
> 

<span data-ttu-id="9fcca-138">Assurez-vous que valeur « expires_in » de hello toomonitor d’accès de hello jeton et mettre à jour vos appels d’API REST avec les nouveaux jetons en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="9fcca-138">Make sure toomonitor hello "expires_in" value of hello access token and update your REST API calls with new tokens as needed.</span></span>

### <a name="connecting-toohello-media-services-uri"></a><span data-ttu-id="9fcca-139">Connexion toohello URI Media Services</span><span class="sxs-lookup"><span data-stu-id="9fcca-139">Connecting toohello Media Services URI</span></span>
<span data-ttu-id="9fcca-140">Hello URI racine de Media Services est https://media.windows.net/.</span><span class="sxs-lookup"><span data-stu-id="9fcca-140">hello root URI for Media Services is https://media.windows.net/.</span></span> <span data-ttu-id="9fcca-141">Vous devez connecter initialement toothis URI, et si vous obtenez une redirection 301 en réponse, vous devez effectuer les appels suivants toohello nouvel URI.</span><span class="sxs-lookup"><span data-stu-id="9fcca-141">You should initially connect toothis URI, and if you get a 301 redirect back in response, you should make subsequent calls toohello new URI.</span></span> <span data-ttu-id="9fcca-142">En outre, n’utilisez pas de logique de redirection automatique/de suivi dans vos demandes.</span><span class="sxs-lookup"><span data-stu-id="9fcca-142">In addition, do not use any auto-redirect/follow logic in your requests.</span></span> <span data-ttu-id="9fcca-143">Verbes HTTP et le corps de requête ne seront pas transférées toohello nouvel URI.</span><span class="sxs-lookup"><span data-stu-id="9fcca-143">HTTP verbs and request bodies will not be forwarded toohello new URI.</span></span>

<span data-ttu-id="9fcca-144">Notez cette racine hello URI pour le téléchargement des fichiers de ressources est https://yourstorageaccount.blob.core.windows.net/ où le nom de compte de stockage hello est hello celui que vous avez utilisé lors de la configuration de votre compte Media Services.</span><span class="sxs-lookup"><span data-stu-id="9fcca-144">Note that hello root URI for uploading and downloading Asset files is https://yourstorageaccount.blob.core.windows.net/ where hello storage account name is hello same one you used during your Media Services account setup.</span></span>

<span data-ttu-id="9fcca-145">Hello, l’exemple suivant montre comment HTTP demande toohello Media Services URI racine (https://media.windows.net/).</span><span class="sxs-lookup"><span data-stu-id="9fcca-145">hello following example demonstrates HTTP request toohello Media Services root URI (https://media.windows.net/).</span></span> <span data-ttu-id="9fcca-146">demande de Hello Obtient une redirection 301 en réponse.</span><span class="sxs-lookup"><span data-stu-id="9fcca-146">hello request gets a 301 redirect back in response.</span></span> <span data-ttu-id="9fcca-147">Hello demande suivante est à l’aide de hello nouvel URI (https://wamsbayclus001rest-hs.cloudapp.net/api/).</span><span class="sxs-lookup"><span data-stu-id="9fcca-147">hello subsequent request is using hello new URI (https://wamsbayclus001rest-hs.cloudapp.net/api/).</span></span>     

<span data-ttu-id="9fcca-148">**Demande HTTP**:</span><span class="sxs-lookup"><span data-stu-id="9fcca-148">**HTTP Request**:</span></span>

    GET https://media.windows.net/ HTTP/1.1
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f19258-6753-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421500579&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=ElVWXOnMVggFQl%2ft9vhdcv1qH1n%2fE8l3hRef4zPmrzg%3d
    x-ms-version: 2.11
    Accept: application/json
    Host: media.windows.net


<span data-ttu-id="9fcca-149">**Réponse HTTP**:</span><span class="sxs-lookup"><span data-stu-id="9fcca-149">**HTTP Response**:</span></span>

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


<span data-ttu-id="9fcca-150">**Requête HTTP** (à l’aide de hello nouvel URI) :</span><span class="sxs-lookup"><span data-stu-id="9fcca-150">**HTTP Request** (using hello new URI):</span></span>

    GET https://wamsbayclus001rest-hs.cloudapp.net/api/ HTTP/1.1
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f19258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421500579&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=ElVWXOnMVggFQl%2ft9vhdcv1qH1n%2fE8l3hRef4zPmrzg%3d
    x-ms-version: 2.11
    Accept: application/json
    Host: wamsbayclus001rest-hs.cloudapp.net


<span data-ttu-id="9fcca-151">**Réponse HTTP**:</span><span class="sxs-lookup"><span data-stu-id="9fcca-151">**HTTP Response**:</span></span>

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
> <span data-ttu-id="9fcca-152">Une fois que vous obtenez hello nouvel URI, qui est hello URI qui doit être utilisé toocommunicate avec Media Services.</span><span class="sxs-lookup"><span data-stu-id="9fcca-152">Once you get hello new URI, that is hello URI that should be used toocommunicate with Media Services.</span></span> 
> 
> 

## <a name="media-services-learning-paths"></a><span data-ttu-id="9fcca-153">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="9fcca-153">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="9fcca-154">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="9fcca-154">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

