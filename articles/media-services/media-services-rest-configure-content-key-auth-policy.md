---
title: "Configurer la stratégie d’autorisation de clé de contenu avec REST - Azure | Microsoft Docs"
description: "Apprenez à configurer une stratégie d’autorisation pour une clé de contenu avec l’API REST Media Services."
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
ms.openlocfilehash: ed20fca35070c190bb63925d0a57cf919bcdd96c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="dynamic-encryption-configure-content-key-authorization-policy"></a><span data-ttu-id="be887-103">Chiffrement dynamique : configurer la stratégie d’autorisation de clé de contenu</span><span class="sxs-lookup"><span data-stu-id="be887-103">Dynamic encryption: Configure Content Key Authorization Policy</span></span>
[!INCLUDE [media-services-selector-content-key-auth-policy](../../includes/media-services-selector-content-key-auth-policy.md)]

## <a name="overview"></a><span data-ttu-id="be887-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="be887-104">Overview</span></span>
<span data-ttu-id="be887-105">Microsoft Azure Media Services vous permet de transmettre du contenu chiffré de manière dynamique avec la norme AES (Advanced Encryption Standard) à l’aide de clés de chiffrement 128 bits et la gestion des droits numériques (DRM) PlayReady ou Widevine.</span><span class="sxs-lookup"><span data-stu-id="be887-105">Microsoft Azure Media Services enables you to deliver your content encrypted (dynamically) with Advanced Encryption Standard (AES) (using 128-bit encryption keys) and PlayReady or Widevine DRM.</span></span> <span data-ttu-id="be887-106">Media Services fournit également un service de distribution de clés et licences PlayReady/Widevine aux clients autorisés.</span><span class="sxs-lookup"><span data-stu-id="be887-106">Media Services also provides a service for delivering keys and PlayReady/Widevine licenses to authorized clients.</span></span>

<span data-ttu-id="be887-107">Si vous souhaitez que Media Services chiffre une ressource, vous devez associer une clé de chiffrement (**CommonEncryption** ou **EnvelopeEncryption**) à la ressource (comme décrit [ici](media-services-rest-create-contentkey.md)) et configurer les stratégies d'autorisation pour la clé (comme décrit dans cet article).</span><span class="sxs-lookup"><span data-stu-id="be887-107">If you want for Media Services to encrypt an asset, you need to associate an encryption key (**CommonEncryption** or **EnvelopeEncryption**) with the asset (as described [here](media-services-rest-create-contentkey.md)) and also configure authorization policies for the key (as described in this article).</span></span>

<span data-ttu-id="be887-108">Lorsqu’un lecteur demande un flux de données, Media Services utilise la clé spécifiée pour chiffrer dynamiquement votre contenu à l’aide du chiffrement AES ou PlayReady.</span><span class="sxs-lookup"><span data-stu-id="be887-108">When a stream is requested by a player, Media Services uses the specified key to dynamically encrypt your content using AES or PlayReady encryption.</span></span> <span data-ttu-id="be887-109">Pour déchiffrer le flux de données, le lecteur demande la clé au service de remise de clé.</span><span class="sxs-lookup"><span data-stu-id="be887-109">To decrypt the stream, the player will request the key from the key delivery service.</span></span> <span data-ttu-id="be887-110">Pour déterminer si l’utilisateur est autorisé à obtenir la clé, le service évalue les stratégies d’autorisation que vous avez spécifiées pour la clé.</span><span class="sxs-lookup"><span data-stu-id="be887-110">To decide whether or not the user is authorized to get the key, the service evaluates the authorization policies that you specified for the key.</span></span>

<span data-ttu-id="be887-111">Media Services prend en charge plusieurs méthodes d’authentification des utilisateurs effectuant des demandes de clé.</span><span class="sxs-lookup"><span data-stu-id="be887-111">Media Services supports multiple ways of authenticating users who make key requests.</span></span> <span data-ttu-id="be887-112">La stratégie d’autorisation des clés de contenu peut comporter une ou plusieurs restrictions d’autorisation : **ouverte** ou **à jeton**.</span><span class="sxs-lookup"><span data-stu-id="be887-112">The content key authorization policy could have one or more authorization restrictions: **open** or **token** restriction.</span></span> <span data-ttu-id="be887-113">La stratégie de restriction à jeton doit être accompagnée d’un jeton émis par un service de jeton sécurisé (STS).</span><span class="sxs-lookup"><span data-stu-id="be887-113">The token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="be887-114">Media Services prend en charge les jetons aux formats **SWT** ([Simple Web Tokens](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2)) et **JWT **(JSON Web Token).</span><span class="sxs-lookup"><span data-stu-id="be887-114">Media Services supports tokens in the **Simple Web Tokens** ([SWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2)) format and **JSON Web Token **(JWT) format.</span></span>

<span data-ttu-id="be887-115">Media Services ne fournit pas de services de jeton sécurisé.</span><span class="sxs-lookup"><span data-stu-id="be887-115">Media Services does not provide Secure Token Services.</span></span> <span data-ttu-id="be887-116">Vous pouvez créer un STS personnalisé ou utiliser l’ACS Microsoft Azure pour émettre des jetons.</span><span class="sxs-lookup"><span data-stu-id="be887-116">You can create a custom STS or leverage Microsoft Azure ACS to issue tokens.</span></span> <span data-ttu-id="be887-117">Le STS doit être configuré pour créer un jeton signé avec la clé spécifiée et émettre les revendications spécifiées dans la configuration de restriction de jeton (comme le décrit cet article).</span><span class="sxs-lookup"><span data-stu-id="be887-117">The STS must be configured to create a token signed with the specified key and issue claims that you specified in the token restriction configuration (as described in this article).</span></span> <span data-ttu-id="be887-118">Le service de remise de clé Media Services retourne la clé de chiffrement pour le client si le jeton est valide et que les revendications du jeton correspondent à celles configurées pour la clé de contenu.</span><span class="sxs-lookup"><span data-stu-id="be887-118">The Media Services key delivery service will return the encryption key to the client if the token is valid and the claims in the token match those configured for the content key.</span></span>

<span data-ttu-id="be887-119">Pour plus d'informations, consultez la rubrique</span><span class="sxs-lookup"><span data-stu-id="be887-119">For more information, see</span></span>

[<span data-ttu-id="be887-120">Authentification par jeton JWT</span><span class="sxs-lookup"><span data-stu-id="be887-120">JWT token authentication</span></span>](http://www.gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/)

<span data-ttu-id="be887-121">[Intégration d'une application Azure Media Services basée sur OWIN MVC avec Azure Active Directory et une remise de clé de contenu basée sur les revendications JWT](http://www.gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/)</span><span class="sxs-lookup"><span data-stu-id="be887-121">[Integrate Azure Media Services OWIN MVC based app with Azure Active Directory and restrict content key delivery based on JWT claims](http://www.gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/).</span></span>

<span data-ttu-id="be887-122">[Utilisation d'ACS Azure pour émettre des jetons](http://mingfeiy.com/acs-with-key-services)</span><span class="sxs-lookup"><span data-stu-id="be887-122">[Use Azure ACS to issue tokens](http://mingfeiy.com/acs-with-key-services).</span></span>

### <a name="some-considerations-apply"></a><span data-ttu-id="be887-123">Certaines considérations s’appliquent :</span><span class="sxs-lookup"><span data-stu-id="be887-123">Some considerations apply:</span></span>
* <span data-ttu-id="be887-124">Pour pouvoir utiliser l’empaquetage et le chiffrement dynamiques, assurez-vous que le point de terminaison de streaming à partir duquel vous souhaitez diffuser votre contenu se trouve à l’état **En cours d’exécution**.</span><span class="sxs-lookup"><span data-stu-id="be887-124">To be able to use dynamic packaging and dynamic encryption, make sure the streaming endpoint from which you want to stream  your content is in the **Running** state.</span></span>
* <span data-ttu-id="be887-125">Votre ressource doit contenir un ensemble de MP4 à débit adaptatif ou des fichiers Smooth Streaming à débit adaptatif.</span><span class="sxs-lookup"><span data-stu-id="be887-125">Your asset must contain a set of adaptive bitrate MP4s or  adaptive bitrate Smooth Streaming files.</span></span> <span data-ttu-id="be887-126">Pour plus d'informations, consultez [Encoder une ressource](media-services-encode-asset.md).</span><span class="sxs-lookup"><span data-stu-id="be887-126">For more information, see [Encode an asset](media-services-encode-asset.md).</span></span>
* <span data-ttu-id="be887-127">Téléchargez et codez vos ressources à l'aide de l'option **AssetCreationOptions.StorageEncrypted** .</span><span class="sxs-lookup"><span data-stu-id="be887-127">Upload and encode your assets using **AssetCreationOptions.StorageEncrypted** option.</span></span>
* <span data-ttu-id="be887-128">Si vous prévoyez d’avoir plusieurs clés de contenu qui nécessitent la même configuration de stratégie, il est fortement recommandé de créer une stratégie d’autorisation unique et de la réutiliser avec plusieurs clés de contenu.</span><span class="sxs-lookup"><span data-stu-id="be887-128">If you plan to have multiple content keys that require the same policy configuration, it is strongly recommended to create a single authorization policy and reuse it with multiple content keys.</span></span>
* <span data-ttu-id="be887-129">Le service de remise de clé met en cache ContentKeyAuthorizationPolicy et ses objets connexes (options de stratégie et restrictions) pendant 15 minutes.</span><span class="sxs-lookup"><span data-stu-id="be887-129">The Key Delivery service caches ContentKeyAuthorizationPolicy and its related objects (policy options and restrictions) for 15 minutes.</span></span>  <span data-ttu-id="be887-130">Si vous créez une ContentKeyAuthorizationPolicy et que vous spécifiez l’utilisation d’une restriction « Jeton », puis la testez avant de mettre à jour la stratégie de restriction vers « Ouverte », vous devrez attendre environ 15 minutes avant que la stratégie bascule vers la version « Ouverte ».</span><span class="sxs-lookup"><span data-stu-id="be887-130">If you create a ContentKeyAuthorizationPolicy and specify to use a “Token” restriction, then test it, and then update the policy to “Open” restriction, it will take roughly 15 minutes before the policy switches to the “Open” version of the policy.</span></span>
* <span data-ttu-id="be887-131">Si vous ajoutez ou mettez à jour la stratégie de remise de votre ressource, vous devez supprimer le localisateur existant (le cas échéant) et en créer un nouveau.</span><span class="sxs-lookup"><span data-stu-id="be887-131">If you add or update your asset’s delivery policy, you must delete an existing locator (if any) and create a new locator.</span></span>
* <span data-ttu-id="be887-132">Actuellement, vous ne pouvez pas chiffrer les téléchargements progressifs.</span><span class="sxs-lookup"><span data-stu-id="be887-132">Currently, you cannot encrypt progressive downloads.</span></span>

## <a name="aes-128-dynamic-encryption"></a><span data-ttu-id="be887-133">Chiffrement dynamique AES-128.</span><span class="sxs-lookup"><span data-stu-id="be887-133">AES-128 Dynamic Encryption</span></span>
> [!NOTE]
> <span data-ttu-id="be887-134">Lorsque vous utilisez l’API REST de Media Services, les considérations suivantes s’appliquent :</span><span class="sxs-lookup"><span data-stu-id="be887-134">When working with the Media Services REST API, the following considerations apply:</span></span>
> 
> <span data-ttu-id="be887-135">Lors de l’accès aux entités dans Media Services, vous devez définir les valeurs et les champs d’en-tête spécifiques dans vos requêtes HTTP.</span><span class="sxs-lookup"><span data-stu-id="be887-135">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="be887-136">Pour plus d'informations, consultez [Installation pour le développement REST API de Media Services](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="be887-136">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>
> 
> <span data-ttu-id="be887-137">Après vous être connecté à https://media.windows.net, vous recevrez une redirection 301 spécifiant un autre URI Media Services.</span><span class="sxs-lookup"><span data-stu-id="be887-137">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="be887-138">Vous devez faire d’autres appels au nouvel URI.</span><span class="sxs-lookup"><span data-stu-id="be887-138">You must make subsequent calls to the new URI.</span></span> <span data-ttu-id="be887-139">Pour savoir comment se connecter à l’API AMS, consultez [Accéder à l’API Azure Media Services avec l’authentification Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="be887-139">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span>
> 
> 

### <a name="open-restriction"></a><span data-ttu-id="be887-140">Restriction ouverte</span><span class="sxs-lookup"><span data-stu-id="be887-140">Open Restriction</span></span>
<span data-ttu-id="be887-141">La restriction ouverte signifie que le système fournira la clé à toute personne effectuant une demande de clé.</span><span class="sxs-lookup"><span data-stu-id="be887-141">Open restriction means the system will deliver the key to anyone who makes a key request.</span></span> <span data-ttu-id="be887-142">Cette restriction peut être utile à des fins de test.</span><span class="sxs-lookup"><span data-stu-id="be887-142">This restriction might be useful for testing purposes.</span></span>

<span data-ttu-id="be887-143">L’exemple suivant crée une stratégie d’autorisation ouverte et l’ajoute à la clé de contenu.</span><span class="sxs-lookup"><span data-stu-id="be887-143">The following example creates an open authorization policy and adds it to the content key.</span></span>

#### <span data-ttu-id="be887-144"><a id="ContentKeyAuthorizationPolicies"></a>Création de ContentKeyAuthorizationPolicies</span><span class="sxs-lookup"><span data-stu-id="be887-144"><a id="ContentKeyAuthorizationPolicies"></a>Create ContentKeyAuthorizationPolicies</span></span>
<span data-ttu-id="be887-145">Demande :</span><span class="sxs-lookup"><span data-stu-id="be887-145">Request:</span></span>

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

<span data-ttu-id="be887-146">Réponse :</span><span class="sxs-lookup"><span data-stu-id="be887-146">Response:</span></span>

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

#### <span data-ttu-id="be887-147"><a id="ContentKeyAuthorizationPolicyOptions"></a>Création de ContentKeyAuthorizationPolicyOptions</span><span class="sxs-lookup"><span data-stu-id="be887-147"><a id="ContentKeyAuthorizationPolicyOptions"></a>Create ContentKeyAuthorizationPolicyOptions</span></span>
<span data-ttu-id="be887-148">Demande :</span><span class="sxs-lookup"><span data-stu-id="be887-148">Request:</span></span>

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

<span data-ttu-id="be887-149">Réponse :</span><span class="sxs-lookup"><span data-stu-id="be887-149">Response:</span></span>    

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

#### <span data-ttu-id="be887-150"><a id="LinkContentKeyAuthorizationPoliciesWithOptions"></a>Lien de ContentKeyAuthorizationPolicies avec les options</span><span class="sxs-lookup"><span data-stu-id="be887-150"><a id="LinkContentKeyAuthorizationPoliciesWithOptions"></a>Link ContentKeyAuthorizationPolicies with Options</span></span>
<span data-ttu-id="be887-151">Demande :</span><span class="sxs-lookup"><span data-stu-id="be887-151">Request:</span></span>

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

<span data-ttu-id="be887-152">Réponse :</span><span class="sxs-lookup"><span data-stu-id="be887-152">Response:</span></span>

    HTTP/1.1 204 No Content

#### <span data-ttu-id="be887-153"><a id="AddAuthorizationPolicyToKey"></a>Ajout de la stratégie d’autorisation à la clé de contenu</span><span class="sxs-lookup"><span data-stu-id="be887-153"><a id="AddAuthorizationPolicyToKey"></a>Add authorization policy to the content key</span></span>
<span data-ttu-id="be887-154">Demande :</span><span class="sxs-lookup"><span data-stu-id="be887-154">Request:</span></span>

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

<span data-ttu-id="be887-155">Réponse :</span><span class="sxs-lookup"><span data-stu-id="be887-155">Response:</span></span>

    HTTP/1.1 204 No Content

### <a name="token-restriction"></a><span data-ttu-id="be887-156">Restriction par jeton</span><span class="sxs-lookup"><span data-stu-id="be887-156">Token Restriction</span></span>
<span data-ttu-id="be887-157">Cette section décrit comment créer une stratégie d’autorisation de clé de contenu et l’associer à la clé de contenu.</span><span class="sxs-lookup"><span data-stu-id="be887-157">This section describes how to create a content key authorization policy and associate it with the content key.</span></span> <span data-ttu-id="be887-158">La stratégie d’autorisation décrit les conditions d’autorisation devant être remplies pour déterminer si l’utilisateur est autorisé à recevoir la clé (par exemple, la liste « clé de vérification » contient-elle la clé qui a servi à signer le jeton).</span><span class="sxs-lookup"><span data-stu-id="be887-158">The authorization policy describes what authorization requirements must be met to determine if the user is authorized to receive the key (for example, does the “verification key” list contain the key that the token was signed with).</span></span>

<span data-ttu-id="be887-159">Pour configurer l’option de restriction par jeton, vous devez utiliser un document XML pour décrire les exigences du jeton d’autorisation.</span><span class="sxs-lookup"><span data-stu-id="be887-159">To configure the token restriction option, you need to use an XML to describe the token’s authorization requirements.</span></span> <span data-ttu-id="be887-160">Le XML de configuration de la restriction par jeton doit être conforme au schéma XML suivant.</span><span class="sxs-lookup"><span data-stu-id="be887-160">The token restriction configuration XML must conform to the following XML schema.</span></span>

#### <span data-ttu-id="be887-161"><a id="schema"></a>Schéma de restriction par jeton</span><span class="sxs-lookup"><span data-stu-id="be887-161"><a id="schema"></a>Token restriction schema</span></span>
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

<span data-ttu-id="be887-162">Lorsque vous configurez la stratégie de restriction par **jeton**, vous devez définir les paramètres de la **clé de vérification** principale, **d’émetteur** et **d’audience**.</span><span class="sxs-lookup"><span data-stu-id="be887-162">When configuring the **token** restricted policy, you must specify the primary** verification key**, **issuer** and **audience** parameters.</span></span> <span data-ttu-id="be887-163">La **clé de vérification principale** contient la clé utilisée pour signer le jeton, **l’émetteur** est le service de jeton sécurisé qui émet le jeton.</span><span class="sxs-lookup"><span data-stu-id="be887-163">The **primary verification key **contains the key that the token was signed with, **issuer** is the secure token service that issues the token.</span></span> <span data-ttu-id="be887-164">Le **public** (parfois appelé **l’étendue**) décrit l’objectif du jeton ou la ressource à laquelle le jeton autorise l’accès.</span><span class="sxs-lookup"><span data-stu-id="be887-164">The **audience** (sometimes called **scope**) describes the intent of the token or the resource the token authorizes access to.</span></span> <span data-ttu-id="be887-165">Le service de remise de clé Media Services valide le fait que les valeurs du jeton correspondent aux valeurs du modèle.</span><span class="sxs-lookup"><span data-stu-id="be887-165">The Media Services key delivery service validates that these values in the token match the values in the template.</span></span> 

<span data-ttu-id="be887-166">L’exemple suivant crée une stratégie d’autorisation avec une restriction par jeton.</span><span class="sxs-lookup"><span data-stu-id="be887-166">The following example creates an authorization policy with a token restriction.</span></span> <span data-ttu-id="be887-167">Dans cet exemple, le client devra présenter un jeton contenant : une clé de signature (VerificationKey), un émetteur de jeton et les revendications requises.</span><span class="sxs-lookup"><span data-stu-id="be887-167">In this example, the client would have to present a token that contains: signing key (VerificationKey), a token issuer, and required claims.</span></span>

### <a name="create-contentkeyauthorizationpolicies"></a><span data-ttu-id="be887-168">Création de ContentKeyAuthorizationPolicies</span><span class="sxs-lookup"><span data-stu-id="be887-168">Create ContentKeyAuthorizationPolicies</span></span>
<span data-ttu-id="be887-169">Créez la « stratégie de restriction par jeton » comme indiqué [ici](#ContentKeyAuthorizationPolicies).</span><span class="sxs-lookup"><span data-stu-id="be887-169">Create the "Token Restriction Policy" as shown [here](#ContentKeyAuthorizationPolicies).</span></span>

### <a name="create-contentkeyauthorizationpolicyoptions"></a><span data-ttu-id="be887-170">Création de ContentKeyAuthorizationPolicyOptions</span><span class="sxs-lookup"><span data-stu-id="be887-170">Create ContentKeyAuthorizationPolicyOptions</span></span>
<span data-ttu-id="be887-171">Demande :</span><span class="sxs-lookup"><span data-stu-id="be887-171">Request:</span></span>

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

<span data-ttu-id="be887-172">Réponse :</span><span class="sxs-lookup"><span data-stu-id="be887-172">Response:</span></span>    

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

#### <a name="link-contentkeyauthorizationpolicies-with-options"></a><span data-ttu-id="be887-173">Lien de ContentKeyAuthorizationPolicies avec les options</span><span class="sxs-lookup"><span data-stu-id="be887-173">Link ContentKeyAuthorizationPolicies with Options</span></span>
<span data-ttu-id="be887-174">Liez ContentKeyAuthorizationPolicies avec les options comme illustré [ici](#ContentKeyAuthorizationPolicies).</span><span class="sxs-lookup"><span data-stu-id="be887-174">Link ContentKeyAuthorizationPolicies with Options as shown [here](#ContentKeyAuthorizationPolicies).</span></span>

#### <a name="add-authorization-policy-to-the-content-key"></a><span data-ttu-id="be887-175">Ajout de la stratégie d’autorisation à la clé de contenu</span><span class="sxs-lookup"><span data-stu-id="be887-175">Add authorization policy to the content key</span></span>
<span data-ttu-id="be887-176">Ajoutez AuthorizationPolicy à la ContentKey comme illustré [ici](#AddAuthorizationPolicyToKey).</span><span class="sxs-lookup"><span data-stu-id="be887-176">Add AuthorizationPolicy to the ContentKey as shown [here](#AddAuthorizationPolicyToKey).</span></span>

## <a name="playready-dynamic-encryption"></a><span data-ttu-id="be887-177">Chiffrement dynamique PlayReady</span><span class="sxs-lookup"><span data-stu-id="be887-177">PlayReady Dynamic Encryption</span></span>
<span data-ttu-id="be887-178">Media Services vous permet de configurer les droits et les restrictions que vous souhaitez pour le runtime DRM PlayReady, qui s’appliquent lorsqu’un utilisateur tente de lire un contenu protégé.</span><span class="sxs-lookup"><span data-stu-id="be887-178">Media Services enables you to configure the rights and restrictions that you want for the PlayReady DRM runtime to enforce when a user is trying to play back protected content.</span></span> 

<span data-ttu-id="be887-179">Quand vous protégez votre contenu avec PlayReady, vous devez spécifier dans votre stratégie d'autorisation une chaîne XML qui définisse le [modèle de licence PlayReady](media-services-playready-license-template-overview.md).</span><span class="sxs-lookup"><span data-stu-id="be887-179">When protecting your content with PlayReady, one of the things you need to specify in your authorization policy is an XML string that defines the [PlayReady license template](media-services-playready-license-template-overview.md).</span></span> 

### <a name="open-restriction"></a><span data-ttu-id="be887-180">Restriction ouverte</span><span class="sxs-lookup"><span data-stu-id="be887-180">Open Restriction</span></span>
<span data-ttu-id="be887-181">La restriction ouverte signifie que le système fournira la clé à toute personne effectuant une demande de clé.</span><span class="sxs-lookup"><span data-stu-id="be887-181">Open restriction means the system will deliver the key to anyone who makes a key request.</span></span> <span data-ttu-id="be887-182">Cette restriction peut être utile à des fins de test.</span><span class="sxs-lookup"><span data-stu-id="be887-182">This restriction might be useful for testing purposes.</span></span>

<span data-ttu-id="be887-183">L’exemple suivant crée une stratégie d’autorisation ouverte et l’ajoute à la clé de contenu.</span><span class="sxs-lookup"><span data-stu-id="be887-183">The following example creates an open authorization policy and adds it to the content key.</span></span>

#### <span data-ttu-id="be887-184"><a id="ContentKeyAuthorizationPolicies2"></a>Création de ContentKeyAuthorizationPolicies</span><span class="sxs-lookup"><span data-stu-id="be887-184"><a id="ContentKeyAuthorizationPolicies2"></a>Create ContentKeyAuthorizationPolicies</span></span>
<span data-ttu-id="be887-185">Demande :</span><span class="sxs-lookup"><span data-stu-id="be887-185">Request:</span></span>

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

<span data-ttu-id="be887-186">Réponse :</span><span class="sxs-lookup"><span data-stu-id="be887-186">Response:</span></span>

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


#### <a name="create-contentkeyauthorizationpolicyoptions"></a><span data-ttu-id="be887-187">Création de ContentKeyAuthorizationPolicyOptions</span><span class="sxs-lookup"><span data-stu-id="be887-187">Create ContentKeyAuthorizationPolicyOptions</span></span>
<span data-ttu-id="be887-188">Demande :</span><span class="sxs-lookup"><span data-stu-id="be887-188">Request:</span></span>

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

<span data-ttu-id="be887-189">Réponse :</span><span class="sxs-lookup"><span data-stu-id="be887-189">Response:</span></span>

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

#### <a name="link-contentkeyauthorizationpolicies-with-options"></a><span data-ttu-id="be887-190">Lien de ContentKeyAuthorizationPolicies avec les options</span><span class="sxs-lookup"><span data-stu-id="be887-190">Link ContentKeyAuthorizationPolicies with Options</span></span>
<span data-ttu-id="be887-191">Liez ContentKeyAuthorizationPolicies avec les options comme illustré [ici](#ContentKeyAuthorizationPolicies).</span><span class="sxs-lookup"><span data-stu-id="be887-191">Link ContentKeyAuthorizationPolicies with Options as shown [here](#ContentKeyAuthorizationPolicies).</span></span>

#### <a name="add-authorization-policy-to-the-content-key"></a><span data-ttu-id="be887-192">Ajout de la stratégie d’autorisation à la clé de contenu</span><span class="sxs-lookup"><span data-stu-id="be887-192">Add authorization policy to the content key</span></span>
<span data-ttu-id="be887-193">Ajoutez AuthorizationPolicy à la ContentKey comme illustré [ici](#AddAuthorizationPolicyToKey).</span><span class="sxs-lookup"><span data-stu-id="be887-193">Add AuthorizationPolicy to the ContentKey as shown [here](#AddAuthorizationPolicyToKey).</span></span>

### <a name="token-restriction"></a><span data-ttu-id="be887-194">Restriction par jeton</span><span class="sxs-lookup"><span data-stu-id="be887-194">Token Restriction</span></span>
<span data-ttu-id="be887-195">Pour configurer l’option de restriction par jeton, vous devez utiliser un document XML pour décrire les exigences du jeton d’autorisation.</span><span class="sxs-lookup"><span data-stu-id="be887-195">To configure the token restriction option, you need to use an XML to describe the token’s authorization requirements.</span></span> <span data-ttu-id="be887-196">Le XML de configuration de la restriction par jeton doit être conforme au schéma XML présenté dans [cette](#schema) section.</span><span class="sxs-lookup"><span data-stu-id="be887-196">The token restriction configuration XML must conform to the XML schema shown in [this](#schema) section.</span></span>

#### <a name="create-contentkeyauthorizationpolicies"></a><span data-ttu-id="be887-197">Création de ContentKeyAuthorizationPolicies</span><span class="sxs-lookup"><span data-stu-id="be887-197">Create ContentKeyAuthorizationPolicies</span></span>
<span data-ttu-id="be887-198">Créez ContentKeyAuthorizationPolicies comme indiqué [ici](#ContentKeyAuthorizationPolicies2).</span><span class="sxs-lookup"><span data-stu-id="be887-198">Create ContentKeyAuthorizationPolicies as shown [here](#ContentKeyAuthorizationPolicies2).</span></span>

#### <a name="create-contentkeyauthorizationpolicyoptions"></a><span data-ttu-id="be887-199">Création de ContentKeyAuthorizationPolicyOptions</span><span class="sxs-lookup"><span data-stu-id="be887-199">Create ContentKeyAuthorizationPolicyOptions</span></span>
<span data-ttu-id="be887-200">Demande :</span><span class="sxs-lookup"><span data-stu-id="be887-200">Request:</span></span>

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

<span data-ttu-id="be887-201">Réponse :</span><span class="sxs-lookup"><span data-stu-id="be887-201">Response:</span></span>

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

#### <a name="link-contentkeyauthorizationpolicies-with-options"></a><span data-ttu-id="be887-202">Lien de ContentKeyAuthorizationPolicies avec les options</span><span class="sxs-lookup"><span data-stu-id="be887-202">Link ContentKeyAuthorizationPolicies with Options</span></span>
<span data-ttu-id="be887-203">Liez ContentKeyAuthorizationPolicies avec les options comme illustré [ici](#ContentKeyAuthorizationPolicies).</span><span class="sxs-lookup"><span data-stu-id="be887-203">Link ContentKeyAuthorizationPolicies with Options as shown [here](#ContentKeyAuthorizationPolicies).</span></span>

#### <a name="add-authorization-policy-to-the-content-key"></a><span data-ttu-id="be887-204">Ajout de la stratégie d’autorisation à la clé de contenu</span><span class="sxs-lookup"><span data-stu-id="be887-204">Add authorization policy to the content key</span></span>
<span data-ttu-id="be887-205">Ajoutez AuthorizationPolicy à la ContentKey comme illustré [ici](#AddAuthorizationPolicyToKey).</span><span class="sxs-lookup"><span data-stu-id="be887-205">Add AuthorizationPolicy to the ContentKey as shown [here](#AddAuthorizationPolicyToKey).</span></span>

## <span data-ttu-id="be887-206"><a id="types"></a>Types utilisés durant la définition de ContentKeyAuthorizationPolicy</span><span class="sxs-lookup"><span data-stu-id="be887-206"><a id="types"></a>Types used when defining ContentKeyAuthorizationPolicy</span></span>
### <span data-ttu-id="be887-207"><a id="ContentKeyRestrictionType"></a>ContentKeyRestrictionType</span><span class="sxs-lookup"><span data-stu-id="be887-207"><a id="ContentKeyRestrictionType"></a>ContentKeyRestrictionType</span></span>
    public enum ContentKeyRestrictionType
    {
        Open = 0,
        TokenRestricted = 1,
        IPRestricted = 2,
    }

### <span data-ttu-id="be887-208"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span><span class="sxs-lookup"><span data-stu-id="be887-208"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span></span>
    public enum ContentKeyDeliveryType
    {
        None = 0,
        PlayReadyLicense = 1,
        BaselineHttp = 2,
        Widevine = 3
    }


## <a name="media-services-learning-paths"></a><span data-ttu-id="be887-209">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="be887-209">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="be887-210">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="be887-210">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="be887-211">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="be887-211">Next Steps</span></span>
<span data-ttu-id="be887-212">La stratégie d'autorisation de la clé de contenu étant configurée, consultez la rubrique [Comment configurer une stratégie de remise de ressources](media-services-rest-configure-asset-delivery-policy.md) .</span><span class="sxs-lookup"><span data-stu-id="be887-212">Now that you have configured content key's authorization policy, go to the [How to configure asset delivery policy](media-services-rest-configure-asset-delivery-policy.md) topic.</span></span>

