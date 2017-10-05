---
title: "Connexion à un compte Media Services à l’aide de l’API REST | Microsoft Docs"
description: "Cette rubrique montre comment se connecter à Media Services avec l’API REST."
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
ms.openlocfilehash: 4feb0eb81823835e8e0b701463d85b27f5598019
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="connecting-to-media-services-account-using-media-services-rest-api"></a><span data-ttu-id="a5428-103">Connexion à un compte Media Services à l’aide de l’API REST</span><span class="sxs-lookup"><span data-stu-id="a5428-103">Connecting to Media Services Account using Media Services REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a5428-104">.NET</span><span class="sxs-lookup"><span data-stu-id="a5428-104">.NET</span></span>](media-services-dotnet-connect-programmatically.md)
> * [<span data-ttu-id="a5428-105">REST</span><span class="sxs-lookup"><span data-stu-id="a5428-105">REST</span></span>](media-services-rest-connect-programmatically.md)
> 
> 

<span data-ttu-id="a5428-106">Cette rubrique décrit comment obtenir une connexion à Microsoft Azure Media Services par programme lorsque vous programmez avec l’API REST Media Services.</span><span class="sxs-lookup"><span data-stu-id="a5428-106">This topic describes how to obtain a programmatic connection to Microsoft Azure Media Services when you are programming with the Media Services REST API.</span></span>

<span data-ttu-id="a5428-107">Vous avez besoin de deux choses pour accéder à Microsoft Azure Media Services : un jeton d’accès fourni par Azure Access Control Service (ACS) et l’URI de Media Services.</span><span class="sxs-lookup"><span data-stu-id="a5428-107">Two things are required when accessing Microsoft Azure Media Services: An access token provided by Azure Access Control Services (ACS), and the URI of Media Services itself.</span></span> <span data-ttu-id="a5428-108">Vous pouvez utiliser la méthode de votre choix lors de la création de ces demandes, tant que vous spécifiez les valeurs d’en-têtes appropriées et transmettez le jeton d’accès correctement lors de l’appel dans Media Services.</span><span class="sxs-lookup"><span data-stu-id="a5428-108">You can use any means you want when creating these requests as long as you specify the correct header values and pass in the access token correctly when calling into Media Services.</span></span>

<span data-ttu-id="a5428-109">Les étapes suivantes décrivent le flux de travail habituel lors de l’utilisation de l’API REST Media Services pour se connecter à Media Services :</span><span class="sxs-lookup"><span data-stu-id="a5428-109">The following steps describe the most common workflow when using the Media Services REST API to connect to Media Services:</span></span>

1. <span data-ttu-id="a5428-110">Obtention d’un jeton d’accès</span><span class="sxs-lookup"><span data-stu-id="a5428-110">Getting an access token</span></span> 
2. <span data-ttu-id="a5428-111">Connexion à l’URI Media Services</span><span class="sxs-lookup"><span data-stu-id="a5428-111">Connecting to the Media Services URI</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="a5428-112">Après vous être connecté à https://media.windows.net, vous recevrez une redirection 301 spécifiant un autre URI Media Services.</span><span class="sxs-lookup"><span data-stu-id="a5428-112">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="a5428-113">Vous devez faire d’autres appels au nouvel URI.</span><span class="sxs-lookup"><span data-stu-id="a5428-113">You must make subsequent calls to the new URI.</span></span>
   > <span data-ttu-id="a5428-114">Vous pouvez également recevoir une réponse HTTP/1.1 200 qui contient la description des métadonnées de l’API ODATA.</span><span class="sxs-lookup"><span data-stu-id="a5428-114">You may also receive a HTTP/1.1 200 response that contains the ODATA API metadata description.</span></span>
   > 
   > 
3. <span data-ttu-id="a5428-115">Envoyez vos appels d’API suivants vers la nouvelle URL.</span><span class="sxs-lookup"><span data-stu-id="a5428-115">Post your subsequent API calls to the new URL.</span></span> 
   
    <span data-ttu-id="a5428-116">Par exemple, si après avoir essayé de vous connecter, vous avez les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="a5428-116">For example, if after trying to connect, you got the following:</span></span>
   
        HTTP/1.1 301 Moved Permanently
        Location: https://wamsbayclus001rest-hs.cloudapp.net/api/
   
    <span data-ttu-id="a5428-117">Vous devez enregistrer vos appels d’API suivants à https://wamsbayclus001rest-hs.cloudapp.net/api/.</span><span class="sxs-lookup"><span data-stu-id="a5428-117">You should post your subsequent API calls to https://wamsbayclus001rest-hs.cloudapp.net/api/.</span></span>

    >[!NOTE]
    ><span data-ttu-id="a5428-118">Un nombre limite de 1 000 000 a été défini pour les différentes stratégies AMS (par exemple, pour la stratégie de localisateur ou pour ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="a5428-118">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="a5428-119">Vous devez utiliser le même ID de stratégie si vous utilisez toujours les mêmes jours / autorisations d’accès, par exemple, les stratégies pour les localisateurs destinées à demeurer en place pendant une longue période (stratégies sans chargement).</span><span class="sxs-lookup"><span data-stu-id="a5428-119">You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="a5428-120">Pour plus d’informations, consultez [cette rubrique](media-services-dotnet-manage-entities.md#limit-access-policies) .</span><span class="sxs-lookup"><span data-stu-id="a5428-120">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

## <a name="access-control-address"></a><span data-ttu-id="a5428-121">Adresse de contrôle d’accès</span><span class="sxs-lookup"><span data-stu-id="a5428-121">Access control address</span></span>
<span data-ttu-id="a5428-122">L’adresse de contrôle d’accès de Media Services est https://wamsprodglobal001acs.accesscontrol.windows.net (à l’exception de la région Chine du Nord, où l’adresse est https://wamsprodglobal001acs.accesscontrol.chinacloudapi.cn).</span><span class="sxs-lookup"><span data-stu-id="a5428-122">Media Services access control address is https://wamsprodglobal001acs.accesscontrol.windows.net, except for North China region, where it is https://wamsprodglobal001acs.accesscontrol.chinacloudapi.cn.</span></span>

## <a name="getting-an-access-token"></a><span data-ttu-id="a5428-123">Obtention d’un jeton d’accès</span><span class="sxs-lookup"><span data-stu-id="a5428-123">Getting an access token</span></span>
<span data-ttu-id="a5428-124">Pour accéder à Media Services directement par le biais de l’API REST, obtenez un jeton d’accès ACS et utilisez-le lors de chaque demande HTTP adressée au service.</span><span class="sxs-lookup"><span data-stu-id="a5428-124">To access Media Services directly through the REST API, retrieve an access token from ACS and use it during every HTTP request you make into the service.</span></span> <span data-ttu-id="a5428-125">Ce jeton est semblable aux autres jetons fournis par ACS basés sur les revendications d’accès fournies dans l’en-tête d’une demande HTTP et à l’aide du protocole OAuth v2.</span><span class="sxs-lookup"><span data-stu-id="a5428-125">This token is similar to other tokens provided by ACS based on access claims provided in the header of an HTTP request and using the OAuth v2 protocol.</span></span> <span data-ttu-id="a5428-126">Il n’existe pas d’autre condition préalable pour vous connecter directement à Media Services.</span><span class="sxs-lookup"><span data-stu-id="a5428-126">You do not need any other prerequisites before directly connecting to Media Services.</span></span>

<span data-ttu-id="a5428-127">L’exemple suivant montre l’en-tête et le corps de demande HTTP qui permet de récupérer un jeton.</span><span class="sxs-lookup"><span data-stu-id="a5428-127">The following example shows the HTTP request header and body used to retrieve a token.</span></span>

<span data-ttu-id="a5428-128">**En-tête**:</span><span class="sxs-lookup"><span data-stu-id="a5428-128">**Header**:</span></span>

    POST https://wamsprodglobal001acs.accesscontrol.windows.net/v2/OAuth2-13 HTTP/1.1
    Content-Type: application/x-www-form-urlencoded
    Host: wamsprodglobal001acs.accesscontrol.windows.net
    Content-Length: 120
    Expect: 100-continue
    Connection: Keep-Alive
    Accept: application/json


<span data-ttu-id="a5428-129">**Corps**:</span><span class="sxs-lookup"><span data-stu-id="a5428-129">**Body**:</span></span>

<span data-ttu-id="a5428-130">Il convient de vérifier les valeurs client_id et client_secret dans le corps de cette demande ; client_id et client_secret correspondent aux valeurs AccountName et AccountKey, respectivement.</span><span class="sxs-lookup"><span data-stu-id="a5428-130">You need to prove the client_id and client_secret values in the body of this request; client_id and client_secret correspond to the AccountName and AccountKey values, respectively.</span></span> <span data-ttu-id="a5428-131">Ces valeurs sont fournies par Media Services pour vous lorsque vous configurez votre compte.</span><span class="sxs-lookup"><span data-stu-id="a5428-131">These values are provided to you by Media Services when you set up your account.</span></span> 

<span data-ttu-id="a5428-132">Notez que la valeur AccountKey de votre compte Media Services doit être encodée dans l’URL (consultez [Encodage par pourcentage](http://tools.ietf.org/html/rfc3986#section-2.1) quand vous l’utilisez comme valeur client_secret dans votre demande de jeton d’accès).</span><span class="sxs-lookup"><span data-stu-id="a5428-132">Note that the AccountKey for your Media Services account must be URL-encoded (see [Percent-Encoding](http://tools.ietf.org/html/rfc3986#section-2.1) when using it as the client_secret value in your access token request.</span></span>

    grant_type=client_credentials&client_id=ams_account_name&client_secret=URL_encoded_ams_account_key&scope=urn%3aWindowsAzureMediaServices


<span data-ttu-id="a5428-133">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="a5428-133">For example:</span></span> 

    grant_type=client_credentials&client_id=amstestaccount001&client_secret=wUNbKhNj07oqjqU3Ah9R9f4kqTJ9avPpfe6Pk3YZ7ng%3d&scope=urn%3aWindowsAzureMediaServices


<span data-ttu-id="a5428-134">L’exemple suivant montre la réponse HTTP qui contient le jeton d’accès dans le corps de réponse.</span><span class="sxs-lookup"><span data-stu-id="a5428-134">The following example shows the HTTP response that contains the access token in the response body.</span></span>

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
> <span data-ttu-id="a5428-135">Il est recommandé de mettre en cache les valeurs « access_token » et « expires_in » sur un stockage externe.</span><span class="sxs-lookup"><span data-stu-id="a5428-135">It is recommended to cache the "access_token " and "expires_in " values to an external storage.</span></span> <span data-ttu-id="a5428-136">Les données du jeton peuvent être récupérées ultérieurement à partir du stockage et réutilisées dans vos appels d’API REST Media Services.</span><span class="sxs-lookup"><span data-stu-id="a5428-136">The token data could later be retrieved from the storage and re-used in your Media Services REST API calls.</span></span> <span data-ttu-id="a5428-137">Ceci est particulièrement utile pour les scénarios où le jeton peut être partagé en toute sécurité entre plusieurs processus ou ordinateurs.</span><span class="sxs-lookup"><span data-stu-id="a5428-137">This is especially useful for scenarios where the token can be securely shared among multiple processes or computers.</span></span>
> 
> 

<span data-ttu-id="a5428-138">Veillez à analyser la valeur « expires_in » du jeton d’accès et à mettre à jour vos appels d’API REST avec de nouveaux jetons le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="a5428-138">Make sure to monitor the "expires_in" value of the access token and update your REST API calls with new tokens as needed.</span></span>

### <a name="connecting-to-the-media-services-uri"></a><span data-ttu-id="a5428-139">Connexion à l’URI Media Services</span><span class="sxs-lookup"><span data-stu-id="a5428-139">Connecting to the Media Services URI</span></span>
<span data-ttu-id="a5428-140">L’URI racine pour Media Services est https://media.windows.net/.</span><span class="sxs-lookup"><span data-stu-id="a5428-140">The root URI for Media Services is https://media.windows.net/.</span></span> <span data-ttu-id="a5428-141">Pour commencer, connectez-vous à cet URI. Si vous obtenez une redirection 301 en réponse, adressez les appels suivants au nouvel URI.</span><span class="sxs-lookup"><span data-stu-id="a5428-141">You should initially connect to this URI, and if you get a 301 redirect back in response, you should make subsequent calls to the new URI.</span></span> <span data-ttu-id="a5428-142">En outre, n’utilisez pas de logique de redirection automatique/de suivi dans vos demandes.</span><span class="sxs-lookup"><span data-stu-id="a5428-142">In addition, do not use any auto-redirect/follow logic in your requests.</span></span> <span data-ttu-id="a5428-143">Les verbes HTTP et les corps de demande ne seront pas transférés au nouvel URI.</span><span class="sxs-lookup"><span data-stu-id="a5428-143">HTTP verbs and request bodies will not be forwarded to the new URI.</span></span>

<span data-ttu-id="a5428-144">Notez que l’URI racine pour le téléchargement des fichiers de ressource est https://votrecomptedestockage.blob.core.windows.net/, où le nom du compte de stockage est le même que celui utilisé lors de la configuration de votre compte Media Services.</span><span class="sxs-lookup"><span data-stu-id="a5428-144">Note that the root URI for uploading and downloading Asset files is https://yourstorageaccount.blob.core.windows.net/ where the storage account name is the same one you used during your Media Services account setup.</span></span>

<span data-ttu-id="a5428-145">L’exemple suivant montre la demande HTTP vers l’URI racine de Media Services (https://media.windows.net/).</span><span class="sxs-lookup"><span data-stu-id="a5428-145">The following example demonstrates HTTP request to the Media Services root URI (https://media.windows.net/).</span></span> <span data-ttu-id="a5428-146">La demande obtient une redirection 301 en réponse.</span><span class="sxs-lookup"><span data-stu-id="a5428-146">The request gets a 301 redirect back in response.</span></span> <span data-ttu-id="a5428-147">La requête suivante utilise le nouvel URI (https://wamsbayclus001rest-hs.cloudapp.net/api/).</span><span class="sxs-lookup"><span data-stu-id="a5428-147">The subsequent request is using the new URI (https://wamsbayclus001rest-hs.cloudapp.net/api/).</span></span>     

<span data-ttu-id="a5428-148">**Demande HTTP**:</span><span class="sxs-lookup"><span data-stu-id="a5428-148">**HTTP Request**:</span></span>

    GET https://media.windows.net/ HTTP/1.1
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f19258-6753-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421500579&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=ElVWXOnMVggFQl%2ft9vhdcv1qH1n%2fE8l3hRef4zPmrzg%3d
    x-ms-version: 2.11
    Accept: application/json
    Host: media.windows.net


<span data-ttu-id="a5428-149">**Réponse HTTP**:</span><span class="sxs-lookup"><span data-stu-id="a5428-149">**HTTP Response**:</span></span>

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
    <h2>Object moved to <a href="https://wamsbayclus001rest-hs.cloudapp.net/api/">here</a>.</h2>
    </body></html>


<span data-ttu-id="a5428-150">**Demande HTTP** (à l’aide du nouvel URI) :</span><span class="sxs-lookup"><span data-stu-id="a5428-150">**HTTP Request** (using the new URI):</span></span>

    GET https://wamsbayclus001rest-hs.cloudapp.net/api/ HTTP/1.1
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f19258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421500579&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=ElVWXOnMVggFQl%2ft9vhdcv1qH1n%2fE8l3hRef4zPmrzg%3d
    x-ms-version: 2.11
    Accept: application/json
    Host: wamsbayclus001rest-hs.cloudapp.net


<span data-ttu-id="a5428-151">**Réponse HTTP**:</span><span class="sxs-lookup"><span data-stu-id="a5428-151">**HTTP Response**:</span></span>

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
> <span data-ttu-id="a5428-152">Après l’obtention du nouvel URI, il convient de l’utiliser pour communiquer avec Media Services.</span><span class="sxs-lookup"><span data-stu-id="a5428-152">Once you get the new URI, that is the URI that should be used to communicate with Media Services.</span></span> 
> 
> 

## <a name="media-services-learning-paths"></a><span data-ttu-id="a5428-153">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="a5428-153">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a5428-154">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="a5428-154">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

