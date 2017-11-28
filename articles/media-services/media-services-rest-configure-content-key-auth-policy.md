---
title: "stratégie d’autorisation de clé contenu aaaConfigure REST - Azure | Documents Microsoft"
description: "Découvrez comment tooconfigure une stratégie d’autorisation pour une clé de contenu à l’aide des API REST Media Services."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 7af5f9e2-8ed8-43f2-843b-580ce8759fd4
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: c058b7682bcbfb736faba18ec7fce33f2f2acb49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="dynamic-encryption-configure-content-key-authorization-policy"></a><span data-ttu-id="36e60-103">Chiffrement dynamique : configurer la stratégie d’autorisation de clé de contenu</span><span class="sxs-lookup"><span data-stu-id="36e60-103">Dynamic encryption: Configure Content Key Authorization Policy</span></span>
[!INCLUDE [media-services-selector-content-key-auth-policy](../../includes/media-services-selector-content-key-auth-policy.md)]

## <a name="overview"></a><span data-ttu-id="36e60-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="36e60-104">Overview</span></span>
<span data-ttu-id="36e60-105">Microsoft Azure Media Services permet de vous toodeliver votre contenu chiffré (dynamique) avec la norme AES (Advanced Encryption) (à l’aide de clés de chiffrement 128 bits) et PlayReady ou Widevine DRM.</span><span class="sxs-lookup"><span data-stu-id="36e60-105">Microsoft Azure Media Services enables you toodeliver your content encrypted (dynamically) with Advanced Encryption Standard (AES) (using 128-bit encryption keys) and PlayReady or Widevine DRM.</span></span> <span data-ttu-id="36e60-106">Media Services fournit également un service de distribution de clés et les licences PlayReady/Widevine tooauthorized clients.</span><span class="sxs-lookup"><span data-stu-id="36e60-106">Media Services also provides a service for delivering keys and PlayReady/Widevine licenses tooauthorized clients.</span></span>

<span data-ttu-id="36e60-107">Si vous souhaitez un élément multimédia pour tooencrypt de Media Services, vous devez tooassociate une clé de chiffrement (**CommonEncryption** ou **EnvelopeEncryption**) avec l’élément multimédia de hello (comme décrit [ici](media-services-rest-create-contentkey.md)) et également configurer des stratégies d’autorisation pour la clé hello (comme décrit dans cet article).</span><span class="sxs-lookup"><span data-stu-id="36e60-107">If you want for Media Services tooencrypt an asset, you need tooassociate an encryption key (**CommonEncryption** or **EnvelopeEncryption**) with hello asset (as described [here](media-services-rest-create-contentkey.md)) and also configure authorization policies for hello key (as described in this article).</span></span>

<span data-ttu-id="36e60-108">Lorsqu’un flux de données est demandée par un lecteur, Media Services utilise hello spécifié toodynamically clé chiffrer votre contenu à l’aide du chiffrement AES ou PlayReady.</span><span class="sxs-lookup"><span data-stu-id="36e60-108">When a stream is requested by a player, Media Services uses hello specified key toodynamically encrypt your content using AES or PlayReady encryption.</span></span> <span data-ttu-id="36e60-109">flux de données toodecrypt hello, le lecteur hello demande clé de hello de service de distribution de clés hello.</span><span class="sxs-lookup"><span data-stu-id="36e60-109">toodecrypt hello stream, hello player will request hello key from hello key delivery service.</span></span> <span data-ttu-id="36e60-110">toodecide soit ou non d’utilisateur de hello autorisé clé de hello tooget, hello évalue les stratégies d’autorisation hello que vous avez spécifié pour la clé de hello.</span><span class="sxs-lookup"><span data-stu-id="36e60-110">toodecide whether or not hello user is authorized tooget hello key, hello service evaluates hello authorization policies that you specified for hello key.</span></span>

<span data-ttu-id="36e60-111">Media Services prend en charge plusieurs méthodes d’authentification des utilisateurs effectuant des demandes de clé.</span><span class="sxs-lookup"><span data-stu-id="36e60-111">Media Services supports multiple ways of authenticating users who make key requests.</span></span> <span data-ttu-id="36e60-112">Hello contenu clé peut avoir une ou plusieurs restrictions d’autorisation : **ouvrir** ou **jeton** restriction.</span><span class="sxs-lookup"><span data-stu-id="36e60-112">hello content key authorization policy could have one or more authorization restrictions: **open** or **token** restriction.</span></span> <span data-ttu-id="36e60-113">stratégie de restriction token Hello doit être accompagné d’un jeton émis par un Service (jeton de sécurité).</span><span class="sxs-lookup"><span data-stu-id="36e60-113">hello token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="36e60-114">Media Services prend en charge les jetons Bonjour **des jetons Web simples** ([SWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2)) format et ** format de jeton Web JSON **(JWT).</span><span class="sxs-lookup"><span data-stu-id="36e60-114">Media Services supports tokens in hello **Simple Web Tokens** ([SWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2)) format and **JSON Web Token **(JWT) format.</span></span>

<span data-ttu-id="36e60-115">Media Services ne fournit pas de services de jeton sécurisé.</span><span class="sxs-lookup"><span data-stu-id="36e60-115">Media Services does not provide Secure Token Services.</span></span> <span data-ttu-id="36e60-116">Vous pouvez créer un STS personnalisé ou tirer parti des jetons de tooissue Microsoft Azure ACS.</span><span class="sxs-lookup"><span data-stu-id="36e60-116">You can create a custom STS or leverage Microsoft Azure ACS tooissue tokens.</span></span> <span data-ttu-id="36e60-117">Hello STS doit être configuré toocreate un jeton signé avec la clé spécifiée de hello et les revendications de problème que vous avez spécifié dans la configuration de restriction token hello (comme décrit dans cet article).</span><span class="sxs-lookup"><span data-stu-id="36e60-117">hello STS must be configured toocreate a token signed with hello specified key and issue claims that you specified in hello token restriction configuration (as described in this article).</span></span> <span data-ttu-id="36e60-118">Hello service de distribution de clés de Media Services renvoie client de toohello clé de chiffrement hello si hello du jeton est valide et hello revendications de jeton de hello correspondent à ceux configurés pour la clé de contenu hello.</span><span class="sxs-lookup"><span data-stu-id="36e60-118">hello Media Services key delivery service will return hello encryption key toohello client if hello token is valid and hello claims in hello token match those configured for hello content key.</span></span>

<span data-ttu-id="36e60-119">Pour plus d'informations, consultez la rubrique</span><span class="sxs-lookup"><span data-stu-id="36e60-119">For more information, see</span></span>

[<span data-ttu-id="36e60-120">Authentification par jeton JWT</span><span class="sxs-lookup"><span data-stu-id="36e60-120">JWT token authentication</span></span>](http://www.gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/)

<span data-ttu-id="36e60-121">[Intégration d'une application Azure Media Services basée sur OWIN MVC avec Azure Active Directory et une remise de clé de contenu basée sur les revendications JWT](http://www.gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/)</span><span class="sxs-lookup"><span data-stu-id="36e60-121">[Integrate Azure Media Services OWIN MVC based app with Azure Active Directory and restrict content key delivery based on JWT claims](http://www.gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/).</span></span>

<span data-ttu-id="36e60-122">[Utilisez les jetons ACS Azure tooissue](http://mingfeiy.com/acs-with-key-services).</span><span class="sxs-lookup"><span data-stu-id="36e60-122">[Use Azure ACS tooissue tokens](http://mingfeiy.com/acs-with-key-services).</span></span>

### <a name="some-considerations-apply"></a><span data-ttu-id="36e60-123">Certaines considérations s’appliquent :</span><span class="sxs-lookup"><span data-stu-id="36e60-123">Some considerations apply:</span></span>
* <span data-ttu-id="36e60-124">toobe toouse en mesure de mise en package dynamique et chiffrement dynamique, assurez-vous que hello de diffusion en continu de point de terminaison à partir de laquelle vous souhaitez toostream votre contenu est Bonjour **en cours d’exécution** état.</span><span class="sxs-lookup"><span data-stu-id="36e60-124">toobe able toouse dynamic packaging and dynamic encryption, make sure hello streaming endpoint from which you want toostream  your content is in hello **Running** state.</span></span>
* <span data-ttu-id="36e60-125">Votre ressource doit contenir un ensemble de MP4 à débit adaptatif ou des fichiers Smooth Streaming à débit adaptatif.</span><span class="sxs-lookup"><span data-stu-id="36e60-125">Your asset must contain a set of adaptive bitrate MP4s or  adaptive bitrate Smooth Streaming files.</span></span> <span data-ttu-id="36e60-126">Pour plus d'informations, consultez [Encoder une ressource](media-services-encode-asset.md).</span><span class="sxs-lookup"><span data-stu-id="36e60-126">For more information, see [Encode an asset](media-services-encode-asset.md).</span></span>
* <span data-ttu-id="36e60-127">Téléchargez et codez vos ressources à l'aide de l'option **AssetCreationOptions.StorageEncrypted** .</span><span class="sxs-lookup"><span data-stu-id="36e60-127">Upload and encode your assets using **AssetCreationOptions.StorageEncrypted** option.</span></span>
* <span data-ttu-id="36e60-128">Si vous envisagez de toohave plusieurs clés de contenu qui nécessitent hello même configuration de la stratégie, il est fortement recommandé de toocreate une seule stratégie d’autorisation et la réutiliser avec plusieurs clés de contenu.</span><span class="sxs-lookup"><span data-stu-id="36e60-128">If you plan toohave multiple content keys that require hello same policy configuration, it is strongly recommended toocreate a single authorization policy and reuse it with multiple content keys.</span></span>
* <span data-ttu-id="36e60-129">Hello service de fourniture de clé met en cache ContentKeyAuthorizationPolicy et les objets associés (options de stratégie et les restrictions) pendant 15 minutes.</span><span class="sxs-lookup"><span data-stu-id="36e60-129">hello Key Delivery service caches ContentKeyAuthorizationPolicy and its related objects (policy options and restrictions) for 15 minutes.</span></span>  <span data-ttu-id="36e60-130">Si vous créez une stratégie ContentKeyAuthorizationPolicy et spécifiez toouse une restriction « Token », puis testez, puis mettre à jour de stratégie de hello trop « ouvrir » restriction, il prendra environ 15 minutes avant hello commutateurs toohello « Ouvert » version de stratégie de la stratégie de hello.</span><span class="sxs-lookup"><span data-stu-id="36e60-130">If you create a ContentKeyAuthorizationPolicy and specify toouse a “Token” restriction, then test it, and then update hello policy too“Open” restriction, it will take roughly 15 minutes before hello policy switches toohello “Open” version of hello policy.</span></span>
* <span data-ttu-id="36e60-131">Si vous ajoutez ou mettez à jour la stratégie de remise de votre ressource, vous devez supprimer le localisateur existant (le cas échéant) et en créer un nouveau.</span><span class="sxs-lookup"><span data-stu-id="36e60-131">If you add or update your asset’s delivery policy, you must delete an existing locator (if any) and create a new locator.</span></span>
* <span data-ttu-id="36e60-132">Actuellement, vous ne pouvez pas chiffrer les téléchargements progressifs.</span><span class="sxs-lookup"><span data-stu-id="36e60-132">Currently, you cannot encrypt progressive downloads.</span></span>

## <a name="aes-128-dynamic-encryption"></a><span data-ttu-id="36e60-133">Chiffrement dynamique AES-128.</span><span class="sxs-lookup"><span data-stu-id="36e60-133">AES-128 Dynamic Encryption</span></span>
> [!NOTE]
> <span data-ttu-id="36e60-134">Lors de l’utilisation des API REST de Media Services, de hello hello considérations suivantes s’appliquent :</span><span class="sxs-lookup"><span data-stu-id="36e60-134">When working with hello Media Services REST API, hello following considerations apply:</span></span>
> 
> <span data-ttu-id="36e60-135">Lors de l’accès aux entités dans Media Services, vous devez définir les valeurs et les champs d’en-tête spécifiques dans vos requêtes HTTP.</span><span class="sxs-lookup"><span data-stu-id="36e60-135">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="36e60-136">Pour plus d'informations, consultez [Installation pour le développement REST API de Media Services](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="36e60-136">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>
> 
> <span data-ttu-id="36e60-137">Après vous être connecté toohttps://media.windows.net, vous recevrez une redirection 301 spécifiant un autre URI de Media Services.</span><span class="sxs-lookup"><span data-stu-id="36e60-137">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="36e60-138">Vous devez effectuer les appels suivants toohello nouvel URI.</span><span class="sxs-lookup"><span data-stu-id="36e60-138">You must make subsequent calls toohello new URI.</span></span> <span data-ttu-id="36e60-139">Pour plus d’informations sur la façon dont tooconnect toohello AMS API, consultez [hello accès API Azure Media Services avec l’authentification Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="36e60-139">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span>
> 
> 

### <a name="open-restriction"></a><span data-ttu-id="36e60-140">Restriction ouverte</span><span class="sxs-lookup"><span data-stu-id="36e60-140">Open Restriction</span></span>
<span data-ttu-id="36e60-141">Restriction Open signifie hello système fournit des tooanyone clé hello qui fait la demande.</span><span class="sxs-lookup"><span data-stu-id="36e60-141">Open restriction means hello system will deliver hello key tooanyone who makes a key request.</span></span> <span data-ttu-id="36e60-142">Cette restriction peut être utile à des fins de test.</span><span class="sxs-lookup"><span data-stu-id="36e60-142">This restriction might be useful for testing purposes.</span></span>

<span data-ttu-id="36e60-143">Hello, l’exemple suivant crée une stratégie d’autorisation ouverte et il ajoute la clé de contenu toohello.</span><span class="sxs-lookup"><span data-stu-id="36e60-143">hello following example creates an open authorization policy and adds it toohello content key.</span></span>

#### <span data-ttu-id="36e60-144"><a id="ContentKeyAuthorizationPolicies"></a>Création de ContentKeyAuthorizationPolicies</span><span class="sxs-lookup"><span data-stu-id="36e60-144"><a id="ContentKeyAuthorizationPolicies"></a>Create ContentKeyAuthorizationPolicies</span></span>
<span data-ttu-id="36e60-145">Demande :</span><span class="sxs-lookup"><span data-stu-id="36e60-145">Request:</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=bbbef702-e769-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423578086&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=lZlyQ2%2bvH73qtJsb42%2fH3xF7r7EvQFR3UXyezuDENFU%3d
    x-ms-version: 2.11
    x-ms-client-request-id: d732dbfa-54fc-474c-99d6-9b46a006f389
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 36

    {"Name":"Open Authorization Policy"}

<span data-ttu-id="36e60-146">Réponse :</span><span class="sxs-lookup"><span data-stu-id="36e60-146">Response:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 211
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicies('nb%3Ackpid%3AUUID%3Adb4593da-f4d1-4cc5-a92a-d20eacbabee4')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: d732dbfa-54fc-474c-99d6-9b46a006f389
    request-id: aabfa731-e884-4bf3-8314-492b04747ac4
    x-ms-request-id: aabfa731-e884-4bf3-8314-492b04747ac4
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Tue, 10 Feb 2015 08:25:56 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#ContentKeyAuthorizationPolicies/@Element","Id":"nb:ckpid:UUID:db4593da-f4d1-4cc5-a92a-d20eacbabee4","Name":"Open Authorization Policy"}

#### <span data-ttu-id="36e60-147"><a id="ContentKeyAuthorizationPolicyOptions"></a>Création de ContentKeyAuthorizationPolicyOptions</span><span class="sxs-lookup"><span data-stu-id="36e60-147"><a id="ContentKeyAuthorizationPolicyOptions"></a>Create ContentKeyAuthorizationPolicyOptions</span></span>
<span data-ttu-id="36e60-148">Demande :</span><span class="sxs-lookup"><span data-stu-id="36e60-148">Request:</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicyOptions HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 3.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=bbbef702-e769-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423580006&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=Ref3EsonGF7fUKCwGwGgiMnZitzIzsDOvvMTeVrVVPg%3d
    x-ms-version: 2.11
    x-ms-client-request-id: d225e357-e60e-4f42-add8-9d93aba1409a
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 168

    {"Name":"policy","KeyDeliveryType":2,"KeyDeliveryConfiguration":"","Restrictions":[{"Name":"HLS Open Authorization Policy","KeyRestrictionType":0,"Requirements":null}]}

<span data-ttu-id="36e60-149">Réponse :</span><span class="sxs-lookup"><span data-stu-id="36e60-149">Response:</span></span>    

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 349
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicyOptions('nb%3Ackpoid%3AUUID%3A57829b17-1101-4797-919b-f816f4a007b7')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: d225e357-e60e-4f42-add8-9d93aba1409a
    request-id: 81bcad37-295b-431f-972f-b23f2e4172c9
    x-ms-request-id: 81bcad37-295b-431f-972f-b23f2e4172c9
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Tue, 10 Feb 2015 08:56:40 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#ContentKeyAuthorizationPolicyOptions/@Element","Id":"nb:ckpoid:UUID:57829b17-1101-4797-919b-f816f4a007b7","Name":"policy","KeyDeliveryType":2,"KeyDeliveryConfiguration":"","Restrictions":[{"Name":"HLS Open Authorization Policy","KeyRestrictionType":0,"Requirements":null}]}

#### <span data-ttu-id="36e60-150"><a id="LinkContentKeyAuthorizationPoliciesWithOptions"></a>Lien de ContentKeyAuthorizationPolicies avec les options</span><span class="sxs-lookup"><span data-stu-id="36e60-150"><a id="LinkContentKeyAuthorizationPoliciesWithOptions"></a>Link ContentKeyAuthorizationPolicies with Options</span></span>
<span data-ttu-id="36e60-151">Demande :</span><span class="sxs-lookup"><span data-stu-id="36e60-151">Request:</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicies('nb%3Ackpid%3AUUID%3A0baa438b-8ac2-4c40-a53c-4d4722b78715')/$links/Options HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Content-Type: application/json
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423580006&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=Ref3EsonGF7fUKCwGwGgiMnZitzIzsDOvvMTeVrVVPg%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 9847f705-f2ca-4e95-a478-8f823dbbaa29
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 154

    {"uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicyOptions('nb%3Ackpoid%3AUUID%3A57829b17-1101-4797-919b-f816f4a007b7')"}

<span data-ttu-id="36e60-152">Réponse :</span><span class="sxs-lookup"><span data-stu-id="36e60-152">Response:</span></span>

    HTTP/1.1 204 No Content

#### <span data-ttu-id="36e60-153"><a id="AddAuthorizationPolicyToKey"></a>Ajouter la clé de contenu toohello stratégie d’autorisation</span><span class="sxs-lookup"><span data-stu-id="36e60-153"><a id="AddAuthorizationPolicyToKey"></a>Add authorization policy toohello content key</span></span>
<span data-ttu-id="36e60-154">Demande :</span><span class="sxs-lookup"><span data-stu-id="36e60-154">Request:</span></span>

    PUT https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeys('nb%3Akid%3AUUID%3A2e6d36a7-a17c-4e9a-830d-eca23ad1a6f9') HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423581565&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=JiNSG3w6r2C0nIyfKvTZj1uPJGjuitD%2b0sbfZ%2b2JDZI%3d
    x-ms-version: 2.11
    x-ms-client-request-id: e613efff-cb6a-41b4-984a-f4f8fb6e76a4
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 78

    {"AuthorizationPolicyId":"nb:ckpid:UUID:c06cebb8-c4f0-4d1a-ba00-3273fb2bc3ad"}

<span data-ttu-id="36e60-155">Réponse :</span><span class="sxs-lookup"><span data-stu-id="36e60-155">Response:</span></span>

    HTTP/1.1 204 No Content

### <a name="token-restriction"></a><span data-ttu-id="36e60-156">Restriction par jeton</span><span class="sxs-lookup"><span data-stu-id="36e60-156">Token Restriction</span></span>
<span data-ttu-id="36e60-157">Cette section décrit comment toocreate un contenu de stratégie d’autorisation de clé et l’associer à la clé de contenu hello.</span><span class="sxs-lookup"><span data-stu-id="36e60-157">This section describes how toocreate a content key authorization policy and associate it with hello content key.</span></span> <span data-ttu-id="36e60-158">stratégie d’autorisation de Hello décrit les spécifications d’autorisation doivent être rempli toodetermine si utilisateur de hello est clé de hello tooreceive autorisés (par exemple, liste de « clé de vérification » hello contenir la clé de hello ce jeton hello a été signé avec).</span><span class="sxs-lookup"><span data-stu-id="36e60-158">hello authorization policy describes what authorization requirements must be met toodetermine if hello user is authorized tooreceive hello key (for example, does hello “verification key” list contain hello key that hello token was signed with).</span></span>

<span data-ttu-id="36e60-159">option de restriction token tooconfigure hello, vous devez toouse XML exigences d’autorisation du jeton toodescribe hello.</span><span class="sxs-lookup"><span data-stu-id="36e60-159">tooconfigure hello token restriction option, you need toouse an XML toodescribe hello token’s authorization requirements.</span></span> <span data-ttu-id="36e60-160">configuration de restriction token Hello XML doit être conforme à toohello suivant le schéma XML.</span><span class="sxs-lookup"><span data-stu-id="36e60-160">hello token restriction configuration XML must conform toohello following XML schema.</span></span>

#### <span data-ttu-id="36e60-161"><a id="schema"></a>Schéma de restriction par jeton</span><span class="sxs-lookup"><span data-stu-id="36e60-161"><a id="schema"></a>Token restriction schema</span></span>
    <?xml version="1.0" encoding="utf-8"?>
    <xs:schema xmlns:tns="http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/TokenRestrictionTemplate/v1" elementFormDefault="qualified" targetNamespace="http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/TokenRestrictionTemplate/v1" xmlns:xs="http://www.w3.org/2001/XMLSchema">
      <xs:complexType name="TokenClaim">
        <xs:sequence>
          <xs:element name="ClaimType" nillable="true" type="xs:string" />
          <xs:element minOccurs="0" name="ClaimValue" nillable="true" type="xs:string" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="TokenClaim" nillable="true" type="tns:TokenClaim" />
      <xs:complexType name="TokenRestrictionTemplate">
        <xs:sequence>
          <xs:element minOccurs="0" name="AlternateVerificationKeys" nillable="true" type="tns:ArrayOfTokenVerificationKey" />
          <xs:element name="Audience" nillable="true" type="xs:anyURI" />
          <xs:element name="Issuer" nillable="true" type="xs:anyURI" />
          <xs:element name="PrimaryVerificationKey" nillable="true" type="tns:TokenVerificationKey" />
          <xs:element minOccurs="0" name="RequiredClaims" nillable="true" type="tns:ArrayOfTokenClaim" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="TokenRestrictionTemplate" nillable="true" type="tns:TokenRestrictionTemplate" />
      <xs:complexType name="ArrayOfTokenVerificationKey">
        <xs:sequence>
          <xs:element minOccurs="0" maxOccurs="unbounded" name="TokenVerificationKey" nillable="true" type="tns:TokenVerificationKey" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="ArrayOfTokenVerificationKey" nillable="true" type="tns:ArrayOfTokenVerificationKey" />
      <xs:complexType name="TokenVerificationKey">
        <xs:sequence />
      </xs:complexType>
      <xs:element name="TokenVerificationKey" nillable="true" type="tns:TokenVerificationKey" />
      <xs:complexType name="ArrayOfTokenClaim">
        <xs:sequence>
          <xs:element minOccurs="0" maxOccurs="unbounded" name="TokenClaim" nillable="true" type="tns:TokenClaim" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="ArrayOfTokenClaim" nillable="true" type="tns:ArrayOfTokenClaim" />
      <xs:complexType name="SymmetricVerificationKey">
        <xs:complexContent mixed="false">
          <xs:extension base="tns:TokenVerificationKey">
            <xs:sequence>
              <xs:element name="KeyValue" nillable="true" type="xs:base64Binary" />
            </xs:sequence>
          </xs:extension>
        </xs:complexContent>
      </xs:complexType>
      <xs:element name="SymmetricVerificationKey" nillable="true" type="tns:SymmetricVerificationKey" />
    </xs:schema>

<span data-ttu-id="36e60-162">Lors de la configuration hello **jeton** stratégie, vous devez spécifier hello principal ** vérification clé **, **émetteur** et **public** paramètres.</span><span class="sxs-lookup"><span data-stu-id="36e60-162">When configuring hello **token** restricted policy, you must specify hello primary** verification key**, **issuer** and **audience** parameters.</span></span> <span data-ttu-id="36e60-163">Hello ** clé de vérification principale ** contient clé hello hello jeton a été signé avec, **émetteur** est service de jeton sécurisé hello ce jeton hello de problèmes.</span><span class="sxs-lookup"><span data-stu-id="36e60-163">hello **primary verification key **contains hello key that hello token was signed with, **issuer** is hello secure token service that issues hello token.</span></span> <span data-ttu-id="36e60-164">Hello **public** (parfois appelé **étendue**) décrit l’intention de hello de jeton de hello ou ressource de hello jeton de hello autorise l’accès à.</span><span class="sxs-lookup"><span data-stu-id="36e60-164">hello **audience** (sometimes called **scope**) describes hello intent of hello token or hello resource hello token authorizes access to.</span></span> <span data-ttu-id="36e60-165">Hello service de distribution de clés de Media Services valide que ces valeurs dans le jeton de hello correspondent aux valeurs hello modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="36e60-165">hello Media Services key delivery service validates that these values in hello token match hello values in hello template.</span></span> 

<span data-ttu-id="36e60-166">Bonjour à l’exemple suivant crée une stratégie d’autorisation avec une restriction token.</span><span class="sxs-lookup"><span data-stu-id="36e60-166">hello following example creates an authorization policy with a token restriction.</span></span> <span data-ttu-id="36e60-167">Dans cet exemple, les clients hello aurait toopresent un jeton qui contient : clé de signature (VerificationKey), un émetteur de jeton et les revendications nécessaires.</span><span class="sxs-lookup"><span data-stu-id="36e60-167">In this example, hello client would have toopresent a token that contains: signing key (VerificationKey), a token issuer, and required claims.</span></span>

### <a name="create-contentkeyauthorizationpolicies"></a><span data-ttu-id="36e60-168">Création de ContentKeyAuthorizationPolicies</span><span class="sxs-lookup"><span data-stu-id="36e60-168">Create ContentKeyAuthorizationPolicies</span></span>
<span data-ttu-id="36e60-169">Créer un hello « Stratégie de Restriction Token » comme [ici](#ContentKeyAuthorizationPolicies).</span><span class="sxs-lookup"><span data-stu-id="36e60-169">Create hello "Token Restriction Policy" as shown [here](#ContentKeyAuthorizationPolicies).</span></span>

### <a name="create-contentkeyauthorizationpolicyoptions"></a><span data-ttu-id="36e60-170">Création de ContentKeyAuthorizationPolicyOptions</span><span class="sxs-lookup"><span data-stu-id="36e60-170">Create ContentKeyAuthorizationPolicyOptions</span></span>
<span data-ttu-id="36e60-171">Demande :</span><span class="sxs-lookup"><span data-stu-id="36e60-171">Request:</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicyOptions HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 3.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=bbbef702-e769-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423580720&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=5LsNu%2b0D4eD3UOP3BviTLDkUjaErdUx0ekJ8402xidQ%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 2643d836-bfe7-438e-9ba2-bc6ff28e4a53
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 1079

    {"Name":"Token option for HLS","KeyDeliveryType":2,"KeyDeliveryConfiguration":null,"Restrictions":[{"Name":"Token Authorization Policy","KeyRestrictionType":1,"Requirements":"<TokenRestrictionTemplate xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/TokenRestrictionTemplate/v1\"><AlternateVerificationKeys><TokenVerificationKey i:type=\"SymmetricVerificationKey\"><KeyValue>BklyAFiPTQsuJNKriQJBZHYaKM2CkCTDQX2bw9sMYuvEC9sjW0W7GUIBygQL/+POEeUqCYPnmEU2g0o1GW2Oqg==</KeyValue></TokenVerificationKey></AlternateVerificationKeys><Audience>urn:test</Audience><Issuer>http://testacs.com/</Issuer><PrimaryVerificationKey i:type=\"SymmetricVerificationKey\"><KeyValue>E5BUHiN4vBdzUzdP0IWaHFMMU3D1uRZgF16TOhSfwwHGSw+Kbf0XqsHzEIYk11M372viB9vbiacsdcQksA0ftw==</KeyValue></PrimaryVerificationKey><RequiredClaims><TokenClaim><ClaimType>urn:microsoft:azure:mediaservices:contentkeyidentifier</ClaimType><ClaimValue i:nil=\"true\" /></TokenClaim></RequiredClaims><TokenType>SWT</TokenType></TokenRestrictionTemplate>"}]}

<span data-ttu-id="36e60-172">Réponse :</span><span class="sxs-lookup"><span data-stu-id="36e60-172">Response:</span></span>    

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 1260
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicyOptions('nb%3Ackpoid%3AUUID%3Ae1ef6145-46e8-4ee6-9756-b1cf96328c23')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: 2643d836-bfe7-438e-9ba2-bc6ff28e4a53
    request-id: 2310b716-aeaa-421e-913e-3ce2f6f685ca
    x-ms-request-id: 2310b716-aeaa-421e-913e-3ce2f6f685ca
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Tue, 10 Feb 2015 09:10:37 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#ContentKeyAuthorizationPolicyOptions/@Element","Id":"nb:ckpoid:UUID:e1ef6145-46e8-4ee6-9756-b1cf96328c23","Name":"Token option for HLS","KeyDeliveryType":2,"KeyDeliveryConfiguration":null,"Restrictions":[{"Name":"Token Authorization Policy","KeyRestrictionType":1,"Requirements":"<TokenRestrictionTemplate xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/TokenRestrictionTemplate/v1\"><AlternateVerificationKeys><TokenVerificationKey i:type=\"SymmetricVerificationKey\"><KeyValue>BklyAFiPTQsuJNKriQJBZHYaKM2CkCTDQX2bw9sMYuvEC9sjW0W7GUIBygQL/+POEeUqCYPnmEU2g0o1GW2Oqg==</KeyValue></TokenVerificationKey></AlternateVerificationKeys><Audience>urn:test</Audience><Issuer>http://testacs.com/</Issuer><PrimaryVerificationKey i:type=\"SymmetricVerificationKey\"><KeyValue>E5BUHiN4vBdzUzdP0IWaHFMMU3D1uRZgF16TOhSfwwHGSw+Kbf0XqsHzEIYk11M372viB9vbiacsdcQksA0ftw==</KeyValue></PrimaryVerificationKey><RequiredClaims><TokenClaim><ClaimType>urn:microsoft:azure:mediaservices:contentkeyidentifier</ClaimType><ClaimValue i:nil=\"true\" /></TokenClaim></RequiredClaims><TokenType>SWT</TokenType></TokenRestrictionTemplate>"}]}

#### <a name="link-contentkeyauthorizationpolicies-with-options"></a><span data-ttu-id="36e60-173">Lien de ContentKeyAuthorizationPolicies avec les options</span><span class="sxs-lookup"><span data-stu-id="36e60-173">Link ContentKeyAuthorizationPolicies with Options</span></span>
<span data-ttu-id="36e60-174">Liez ContentKeyAuthorizationPolicies avec les options comme illustré [ici](#ContentKeyAuthorizationPolicies).</span><span class="sxs-lookup"><span data-stu-id="36e60-174">Link ContentKeyAuthorizationPolicies with Options as shown [here](#ContentKeyAuthorizationPolicies).</span></span>

#### <a name="add-authorization-policy-toohello-content-key"></a><span data-ttu-id="36e60-175">Ajouter la clé de contenu toohello stratégie d’autorisation</span><span class="sxs-lookup"><span data-stu-id="36e60-175">Add authorization policy toohello content key</span></span>
<span data-ttu-id="36e60-176">Ajoutez AuthorizationPolicy toohello ContentKey, comme indiqué [ici](#AddAuthorizationPolicyToKey).</span><span class="sxs-lookup"><span data-stu-id="36e60-176">Add AuthorizationPolicy toohello ContentKey as shown [here](#AddAuthorizationPolicyToKey).</span></span>

## <a name="playready-dynamic-encryption"></a><span data-ttu-id="36e60-177">Chiffrement dynamique PlayReady</span><span class="sxs-lookup"><span data-stu-id="36e60-177">PlayReady Dynamic Encryption</span></span>
<span data-ttu-id="36e60-178">Media Services vous permet de droits de hello tooconfigure et les restrictions que vous souhaitez pour hello PlayReady DRM runtime tooenforce lorsqu’un utilisateur essaye tooplay précédent du contenu protégé.</span><span class="sxs-lookup"><span data-stu-id="36e60-178">Media Services enables you tooconfigure hello rights and restrictions that you want for hello PlayReady DRM runtime tooenforce when a user is trying tooplay back protected content.</span></span> 

<span data-ttu-id="36e60-179">Lorsque vous protégez votre contenu avec PlayReady, un des éléments de hello vous devez toospecify dans votre stratégie d’autorisation est une chaîne XML qui définit hello [modèle de licence PlayReady](media-services-playready-license-template-overview.md).</span><span class="sxs-lookup"><span data-stu-id="36e60-179">When protecting your content with PlayReady, one of hello things you need toospecify in your authorization policy is an XML string that defines hello [PlayReady license template](media-services-playready-license-template-overview.md).</span></span> 

### <a name="open-restriction"></a><span data-ttu-id="36e60-180">Restriction ouverte</span><span class="sxs-lookup"><span data-stu-id="36e60-180">Open Restriction</span></span>
<span data-ttu-id="36e60-181">Restriction Open signifie hello système fournit des tooanyone clé hello qui fait la demande.</span><span class="sxs-lookup"><span data-stu-id="36e60-181">Open restriction means hello system will deliver hello key tooanyone who makes a key request.</span></span> <span data-ttu-id="36e60-182">Cette restriction peut être utile à des fins de test.</span><span class="sxs-lookup"><span data-stu-id="36e60-182">This restriction might be useful for testing purposes.</span></span>

<span data-ttu-id="36e60-183">Hello, l’exemple suivant crée une stratégie d’autorisation ouverte et il ajoute la clé de contenu toohello.</span><span class="sxs-lookup"><span data-stu-id="36e60-183">hello following example creates an open authorization policy and adds it toohello content key.</span></span>

#### <span data-ttu-id="36e60-184"><a id="ContentKeyAuthorizationPolicies2"></a>Création de ContentKeyAuthorizationPolicies</span><span class="sxs-lookup"><span data-stu-id="36e60-184"><a id="ContentKeyAuthorizationPolicies2"></a>Create ContentKeyAuthorizationPolicies</span></span>
<span data-ttu-id="36e60-185">Demande :</span><span class="sxs-lookup"><span data-stu-id="36e60-185">Request:</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=bbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423581565&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=JiNSG3w6r2C0nIyfKvTZj1uPJGjuitD%2b0sbfZ%2b2JDZI%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 9e7fa407-f84e-43aa-8f05-9790b46e279b
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 58

    {"Name":"Deliver Common Content Key"}

<span data-ttu-id="36e60-186">Réponse :</span><span class="sxs-lookup"><span data-stu-id="36e60-186">Response:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 233
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicies('nb%3Ackpid%3AUUID%3Acc3c64a8-e2fc-4e09-bf60-ac954251a387')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: 9e7fa407-f84e-43aa-8f05-9790b46e279b
    request-id: b3d33c1b-a9cb-4120-ac0c-18f64846c147
    x-ms-request-id: b3d33c1b-a9cb-4120-ac0c-18f64846c147
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Tue, 10 Feb 2015 09:26:00 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#ContentKeyAuthorizationPolicies/@Element","Id":"nb:ckpid:UUID:cc3c64a8-e2fc-4e09-bf60-ac954251a387","Name":"Deliver Common Content Key"}


#### <a name="create-contentkeyauthorizationpolicyoptions"></a><span data-ttu-id="36e60-187">Création de ContentKeyAuthorizationPolicyOptions</span><span class="sxs-lookup"><span data-stu-id="36e60-187">Create ContentKeyAuthorizationPolicyOptions</span></span>
<span data-ttu-id="36e60-188">Demande :</span><span class="sxs-lookup"><span data-stu-id="36e60-188">Request:</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicyOptions HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 3.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423581565&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=JiNSG3w6r2C0nIyfKvTZj1uPJGjuitD%2b0sbfZ%2b2JDZI%3d
    x-ms-version: 2.11
    x-ms-client-request-id: f160ad25-b457-4bc6-8197-315604c5e585
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 593

    {"Name":"","KeyDeliveryType":1,"KeyDeliveryConfiguration":"<PlayReadyLicenseResponseTemplate xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1\"><LicenseTemplates><PlayReadyLicenseTemplate><AllowTestDevices>false</AllowTestDevices><ContentKey i:type=\"ContentEncryptionKeyFromHeader\" /><LicenseType>Nonpersistent</LicenseType><PlayRight /></PlayReadyLicenseTemplate></LicenseTemplates></PlayReadyLicenseResponseTemplate>","Restrictions":[{"Name":"Open","KeyRestrictionType":0,"Requirements":null}]}

<span data-ttu-id="36e60-189">Réponse :</span><span class="sxs-lookup"><span data-stu-id="36e60-189">Response:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 774
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicyOptions('nb%3Ackpoid%3AUUID%3A1052308c-4df7-4fdb-8d21-4d2141fc2be0')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: f160ad25-b457-4bc6-8197-315604c5e585
    request-id: 563f5a42-50a4-4c4a-add8-a833f8364231
    x-ms-request-id: 563f5a42-50a4-4c4a-add8-a833f8364231
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Tue, 10 Feb 2015 09:23:24 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#ContentKeyAuthorizationPolicyOptions/@Element","Id":"nb:ckpoid:UUID:1052308c-4df7-4fdb-8d21-4d2141fc2be0","Name":"","KeyDeliveryType":1,"KeyDeliveryConfiguration":"<PlayReadyLicenseResponseTemplate xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1\"><LicenseTemplates><PlayReadyLicenseTemplate><AllowTestDevices>false</AllowTestDevices><ContentKey i:type=\"ContentEncryptionKeyFromHeader\" /><LicenseType>Nonpersistent</LicenseType><PlayRight /></PlayReadyLicenseTemplate></LicenseTemplates></PlayReadyLicenseResponseTemplate>","Restrictions":[{"Name":"Open","KeyRestrictionType":0,"Requirements":null}]}

#### <a name="link-contentkeyauthorizationpolicies-with-options"></a><span data-ttu-id="36e60-190">Lien de ContentKeyAuthorizationPolicies avec les options</span><span class="sxs-lookup"><span data-stu-id="36e60-190">Link ContentKeyAuthorizationPolicies with Options</span></span>
<span data-ttu-id="36e60-191">Liez ContentKeyAuthorizationPolicies avec les options comme illustré [ici](#ContentKeyAuthorizationPolicies).</span><span class="sxs-lookup"><span data-stu-id="36e60-191">Link ContentKeyAuthorizationPolicies with Options as shown [here](#ContentKeyAuthorizationPolicies).</span></span>

#### <a name="add-authorization-policy-toohello-content-key"></a><span data-ttu-id="36e60-192">Ajouter la clé de contenu toohello stratégie d’autorisation</span><span class="sxs-lookup"><span data-stu-id="36e60-192">Add authorization policy toohello content key</span></span>
<span data-ttu-id="36e60-193">Ajoutez AuthorizationPolicy toohello ContentKey, comme indiqué [ici](#AddAuthorizationPolicyToKey).</span><span class="sxs-lookup"><span data-stu-id="36e60-193">Add AuthorizationPolicy toohello ContentKey as shown [here](#AddAuthorizationPolicyToKey).</span></span>

### <a name="token-restriction"></a><span data-ttu-id="36e60-194">Restriction par jeton</span><span class="sxs-lookup"><span data-stu-id="36e60-194">Token Restriction</span></span>
<span data-ttu-id="36e60-195">option de restriction token tooconfigure hello, vous devez toouse XML exigences d’autorisation du jeton toodescribe hello.</span><span class="sxs-lookup"><span data-stu-id="36e60-195">tooconfigure hello token restriction option, you need toouse an XML toodescribe hello token’s authorization requirements.</span></span> <span data-ttu-id="36e60-196">configuration de restriction token Hello XML doit être conforme à XSD toohello illustré [cela](#schema) section.</span><span class="sxs-lookup"><span data-stu-id="36e60-196">hello token restriction configuration XML must conform toohello XML schema shown in [this](#schema) section.</span></span>

#### <a name="create-contentkeyauthorizationpolicies"></a><span data-ttu-id="36e60-197">Création de ContentKeyAuthorizationPolicies</span><span class="sxs-lookup"><span data-stu-id="36e60-197">Create ContentKeyAuthorizationPolicies</span></span>
<span data-ttu-id="36e60-198">Créez ContentKeyAuthorizationPolicies comme indiqué [ici](#ContentKeyAuthorizationPolicies2).</span><span class="sxs-lookup"><span data-stu-id="36e60-198">Create ContentKeyAuthorizationPolicies as shown [here](#ContentKeyAuthorizationPolicies2).</span></span>

#### <a name="create-contentkeyauthorizationpolicyoptions"></a><span data-ttu-id="36e60-199">Création de ContentKeyAuthorizationPolicyOptions</span><span class="sxs-lookup"><span data-stu-id="36e60-199">Create ContentKeyAuthorizationPolicyOptions</span></span>
<span data-ttu-id="36e60-200">Demande :</span><span class="sxs-lookup"><span data-stu-id="36e60-200">Request:</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicyOptions HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 3.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423583561&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=5eZnkOsSv%2fLLEKmS%2bWObBlsNYyee8BQlp%2bUYbjugcJg%3d
    x-ms-version: 2.11
    x-ms-client-request-id: ab079b0e-2ba9-4cf1-b549-a97bfa6cd2d3
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 1525

    {"Name":"Token option","KeyDeliveryType":1,"KeyDeliveryConfiguration":"<PlayReadyLicenseResponseTemplate xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1\"><LicenseTemplates><PlayReadyLicenseTemplate><AllowTestDevices>false</AllowTestDevices><ContentKey i:type=\"ContentEncryptionKeyFromHeader\" /><LicenseType>Nonpersistent</LicenseType><PlayRight /></PlayReadyLicenseTemplate></LicenseTemplates></PlayReadyLicenseResponseTemplate>","Restrictions":[{"Name":"Token Authorization Policy","KeyRestrictionType":1,"Requirements":"<TokenRestrictionTemplate xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/TokenRestrictionTemplate/v1\"><AlternateVerificationKeys><TokenVerificationKey i:type=\"SymmetricVerificationKey\"><KeyValue>w52OyHVqXT8aaupGxuJ3NGt8M6opHDOtx132p4r6q4hLI6ffnLusgEGie1kedUewVoIe1tqDkVE6xsIV7O91KA==</KeyValue></TokenVerificationKey></AlternateVerificationKeys><Audience>urn:test</Audience><Issuer>http://testacs.com/</Issuer><PrimaryVerificationKey i:type=\"SymmetricVerificationKey\"><KeyValue>dYwLKIEMBljLeY9VM7vWdlhps31Fbt0XXhqP5VyjQa33bJXleBtkzQ6dF5AtwI9gDcdM2dV2TvYNhCilBKjMCg==</KeyValue></PrimaryVerificationKey><RequiredClaims><TokenClaim><ClaimType>urn:microsoft:azure:mediaservices:contentkeyidentifier</ClaimType><ClaimValue i:nil=\"true\" /></TokenClaim></RequiredClaims><TokenType>SWT</TokenType></TokenRestrictionTemplate>"}]}

<span data-ttu-id="36e60-201">Réponse :</span><span class="sxs-lookup"><span data-stu-id="36e60-201">Response:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 1706
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicyOptions('nb%3Ackpoid%3AUUID%3Ae42bbeae-de42-4077-90e9-a844f297ef70')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: ab079b0e-2ba9-4cf1-b549-a97bfa6cd2d3
    request-id: ccf8a4ba-731e-4124-8192-079592c251cc
    x-ms-request-id: ccf8a4ba-731e-4124-8192-079592c251cc
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Tue, 10 Feb 2015 09:58:47 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#ContentKeyAuthorizationPolicyOptions/@Element","Id":"nb:ckpoid:UUID:e42bbeae-de42-4077-90e9-a844f297ef70","Name":"Token option","KeyDeliveryType":1,"KeyDeliveryConfiguration":"<PlayReadyLicenseResponseTemplate xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1\"><LicenseTemplates><PlayReadyLicenseTemplate><AllowTestDevices>false</AllowTestDevices><ContentKey i:type=\"ContentEncryptionKeyFromHeader\" /><LicenseType>Nonpersistent</LicenseType><PlayRight /></PlayReadyLicenseTemplate></LicenseTemplates></PlayReadyLicenseResponseTemplate>","Restrictions":[{"Name":"Token Authorization Policy","KeyRestrictionType":1,"Requirements":"<TokenRestrictionTemplate xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/TokenRestrictionTemplate/v1\"><AlternateVerificationKeys><TokenVerificationKey i:type=\"SymmetricVerificationKey\"><KeyValue>w52OyHVqXT8aaupGxuJ3NGt8M6opHDOtx132p4r6q4hLI6ffnLusgEGie1kedUewVoIe1tqDkVE6xsIV7O91KA==</KeyValue></TokenVerificationKey></AlternateVerificationKeys><Audience>urn:test</Audience><Issuer>http://testacs.com/</Issuer><PrimaryVerificationKey i:type=\"SymmetricVerificationKey\"><KeyValue>dYwLKIEMBljLeY9VM7vWdlhps31Fbt0XXhqP5VyjQa33bJXleBtkzQ6dF5AtwI9gDcdM2dV2TvYNhCilBKjMCg==</KeyValue></PrimaryVerificationKey><RequiredClaims><TokenClaim><ClaimType>urn:microsoft:azure:mediaservices:contentkeyidentifier</ClaimType><ClaimValue i:nil=\"true\" /></TokenClaim></RequiredClaims><TokenType>SWT</TokenType></TokenRestrictionTemplate>"}]}

#### <a name="link-contentkeyauthorizationpolicies-with-options"></a><span data-ttu-id="36e60-202">Lien de ContentKeyAuthorizationPolicies avec les options</span><span class="sxs-lookup"><span data-stu-id="36e60-202">Link ContentKeyAuthorizationPolicies with Options</span></span>
<span data-ttu-id="36e60-203">Liez ContentKeyAuthorizationPolicies avec les options comme illustré [ici](#ContentKeyAuthorizationPolicies).</span><span class="sxs-lookup"><span data-stu-id="36e60-203">Link ContentKeyAuthorizationPolicies with Options as shown [here](#ContentKeyAuthorizationPolicies).</span></span>

#### <a name="add-authorization-policy-toohello-content-key"></a><span data-ttu-id="36e60-204">Ajouter la clé de contenu toohello stratégie d’autorisation</span><span class="sxs-lookup"><span data-stu-id="36e60-204">Add authorization policy toohello content key</span></span>
<span data-ttu-id="36e60-205">Ajoutez AuthorizationPolicy toohello ContentKey, comme indiqué [ici](#AddAuthorizationPolicyToKey).</span><span class="sxs-lookup"><span data-stu-id="36e60-205">Add AuthorizationPolicy toohello ContentKey as shown [here](#AddAuthorizationPolicyToKey).</span></span>

## <span data-ttu-id="36e60-206"><a id="types"></a>Types utilisés durant la définition de ContentKeyAuthorizationPolicy</span><span class="sxs-lookup"><span data-stu-id="36e60-206"><a id="types"></a>Types used when defining ContentKeyAuthorizationPolicy</span></span>
### <span data-ttu-id="36e60-207"><a id="ContentKeyRestrictionType"></a>ContentKeyRestrictionType</span><span class="sxs-lookup"><span data-stu-id="36e60-207"><a id="ContentKeyRestrictionType"></a>ContentKeyRestrictionType</span></span>
    public enum ContentKeyRestrictionType
    {
        Open = 0,
        TokenRestricted = 1,
        IPRestricted = 2,
    }

### <span data-ttu-id="36e60-208"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span><span class="sxs-lookup"><span data-stu-id="36e60-208"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span></span>
    public enum ContentKeyDeliveryType
    {
        None = 0,
        PlayReadyLicense = 1,
        BaselineHttp = 2,
        Widevine = 3
    }


## <a name="media-services-learning-paths"></a><span data-ttu-id="36e60-209">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="36e60-209">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="36e60-210">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="36e60-210">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="36e60-211">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="36e60-211">Next Steps</span></span>
<span data-ttu-id="36e60-212">Maintenant que vous avez configuré la stratégie d’autorisation de clé de contenu, accédez à toohello [la stratégie de livraison des actifs tooconfigure](media-services-rest-configure-asset-delivery-policy.md) rubrique.</span><span class="sxs-lookup"><span data-stu-id="36e60-212">Now that you have configured content key's authorization policy, go toohello [How tooconfigure asset delivery policy](media-services-rest-configure-asset-delivery-policy.md) topic.</span></span>

