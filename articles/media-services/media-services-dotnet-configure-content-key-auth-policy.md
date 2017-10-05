---
title: "Configurer la stratégie d’autorisation de clé de contenu à l’aide du Kit de développement logiciel (SDK).NET Media Services | Microsoft Docs"
description: "Apprenez à configurer une stratégie d’autorisation pour une clé de contenu avec le Kit de développement logiciel (SDK) .NET Media Services."
services: media-services
documentationcenter: 
author: Mingfeiy
manager: cfowler
editor: 
ms.assetid: 1a0aedda-5b87-4436-8193-09fc2f14310c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako;mingfeiy
ms.openlocfilehash: 75dd9107dca215a0b31db3d44bada69210fe9ac6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="dynamic-encryption-configure-content-key-authorization-policy"></a><span data-ttu-id="c72ce-103">Chiffrement dynamique : configurer la stratégie d’autorisation de clé de contenu</span><span class="sxs-lookup"><span data-stu-id="c72ce-103">Dynamic encryption: configure content key authorization policy</span></span>
[!INCLUDE [media-services-selector-content-key-auth-policy](../../includes/media-services-selector-content-key-auth-policy.md)]

## <a name="overview"></a><span data-ttu-id="c72ce-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="c72ce-104">Overview</span></span>
<span data-ttu-id="c72ce-105">Microsoft Azure Media Services vous permet de fournir des flux MPEG-DASH, Smooth Streaming et HLS (HTTP-Live-Streaming) protégés par AES (Advanced Encryption Standard) à l’aide de clés de chiffrement 128 bits ou [Microsoft PlayReady DRM](https://www.microsoft.com/playready/overview/).</span><span class="sxs-lookup"><span data-stu-id="c72ce-105">Microsoft Azure Media Services enables you to deliver MPEG-DASH, Smooth Streaming, and HTTP-Live-Streaming (HLS) streams protected with Advanced Encryption Standard (AES) (using 128-bit encryption keys) or [Microsoft PlayReady DRM](https://www.microsoft.com/playready/overview/).</span></span> <span data-ttu-id="c72ce-106">AMS vous permet également de diffuser des flux DASH chiffrés avec Widevine DRM.</span><span class="sxs-lookup"><span data-stu-id="c72ce-106">AMS also enables you to deliver DASH streams encrypted with Widevine DRM.</span></span> <span data-ttu-id="c72ce-107">PlayReady et Widewine sont chiffrés conformément à la spécification de chiffrement commun (ISO/IEC 23001-7 CENC).</span><span class="sxs-lookup"><span data-stu-id="c72ce-107">Both PlayReady and Widevine are encrypted per the Common Encryption (ISO/IEC 23001-7 CENC) specification.</span></span>

<span data-ttu-id="c72ce-108">Media Services fournit également un **service de remise de clés/de licences** à partir duquel les clients peuvent obtenir des clés AES ou des licences PlayReady/Widevine pour lire le contenu chiffré.</span><span class="sxs-lookup"><span data-stu-id="c72ce-108">Media Services also provides a **Key/License Delivery Service** from which clients can obtain AES keys or PlayReady/Widevine licenses to play the encrypted content.</span></span>

<span data-ttu-id="c72ce-109">Si vous souhaitez que Media Services chiffre une ressource, vous devez associer une clé de chiffrement (**CommonEncryption** ou **EnvelopeEncryption**) à la ressource (comme décrit [ici](media-services-dotnet-create-contentkey.md)) et configurer les stratégies d'autorisation pour la clé (comme décrit dans cet article).</span><span class="sxs-lookup"><span data-stu-id="c72ce-109">If you want for Media Services to encrypt an asset, you need to associate an encryption key (**CommonEncryption** or **EnvelopeEncryption**) with the asset (as described [here](media-services-dotnet-create-contentkey.md)) and also configure authorization policies for the key (as described in this article).</span></span>

<span data-ttu-id="c72ce-110">Lorsqu’un lecteur demande un flux de données, Media Services utilise la clé spécifiée pour chiffrer dynamiquement votre contenu à l’aide du chiffrement AES ou DRM.</span><span class="sxs-lookup"><span data-stu-id="c72ce-110">When a stream is requested by a player, Media Services uses the specified key to dynamically encrypt your content using AES or DRM encryption.</span></span> <span data-ttu-id="c72ce-111">Pour déchiffrer le flux de données, le lecteur demande la clé au service de remise de clé.</span><span class="sxs-lookup"><span data-stu-id="c72ce-111">To decrypt the stream, the player will request the key from the key delivery service.</span></span> <span data-ttu-id="c72ce-112">Pour déterminer si l’utilisateur est autorisé à obtenir la clé, le service évalue les stratégies d’autorisation que vous avez spécifiées pour la clé.</span><span class="sxs-lookup"><span data-stu-id="c72ce-112">To decide whether or not the user is authorized to get the key, the service evaluates the authorization policies that you specified for the key.</span></span>

<span data-ttu-id="c72ce-113">Media Services prend en charge plusieurs méthodes d’authentification des utilisateurs effectuant des demandes de clé.</span><span class="sxs-lookup"><span data-stu-id="c72ce-113">Media Services supports multiple ways of authenticating users who make key requests.</span></span> <span data-ttu-id="c72ce-114">La stratégie d’autorisation des clés de contenu peut comporter une ou plusieurs restrictions d’autorisation : **ouverte** ou **à jeton**.</span><span class="sxs-lookup"><span data-stu-id="c72ce-114">The content key authorization policy could have one or more authorization restrictions: **open** or **token** restriction.</span></span> <span data-ttu-id="c72ce-115">La stratégie de restriction à jeton doit être accompagnée d’un jeton émis par un service de jeton sécurisé (STS).</span><span class="sxs-lookup"><span data-stu-id="c72ce-115">The token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="c72ce-116">Media Services prend en charge les jetons aux formats [SWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2) (**Simple Web Tokens**) et [JWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3) (**JSON Web Token**).</span><span class="sxs-lookup"><span data-stu-id="c72ce-116">Media Services supports tokens in the **Simple Web Tokens** ([SWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2)) format and **JSON Web Token** ([JWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3)) format.</span></span>

<span data-ttu-id="c72ce-117">Media Services ne fournit pas de services de jeton sécurisé.</span><span class="sxs-lookup"><span data-stu-id="c72ce-117">Media Services does not provide Secure Token Services.</span></span> <span data-ttu-id="c72ce-118">Vous pouvez créer un STS personnalisé ou utiliser l’ACS Microsoft Azure pour émettre des jetons.</span><span class="sxs-lookup"><span data-stu-id="c72ce-118">You can create a custom STS or leverage Microsoft Azure ACS to issue tokens.</span></span> <span data-ttu-id="c72ce-119">Le STS doit être configuré pour créer un jeton signé avec la clé spécifiée et émettre les revendications spécifiées dans la configuration de restriction de jeton (comme le décrit cet article).</span><span class="sxs-lookup"><span data-stu-id="c72ce-119">The STS must be configured to create a token signed with the specified key and issue claims that you specified in the token restriction configuration (as described in this article).</span></span> <span data-ttu-id="c72ce-120">Le service de remise de clé Media Services retourne la clé de chiffrement pour le client si le jeton est valide et que les revendications du jeton correspondent à celles configurées pour la clé de contenu.</span><span class="sxs-lookup"><span data-stu-id="c72ce-120">The Media Services key delivery service will return the encryption key to the client if the token is valid and the claims in the token match those configured for the content key.</span></span>

<span data-ttu-id="c72ce-121">Pour plus d'informations, consultez la rubrique</span><span class="sxs-lookup"><span data-stu-id="c72ce-121">For more information, see</span></span>

[<span data-ttu-id="c72ce-122">Authentification par jeton JWT</span><span class="sxs-lookup"><span data-stu-id="c72ce-122">JWT token authentication</span></span>](http://www.gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/)

<span data-ttu-id="c72ce-123">[Intégration d'une application Azure Media Services basée sur OWIN MVC avec Azure Active Directory et une remise de clé de contenu basée sur les revendications JWT](http://www.gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/)</span><span class="sxs-lookup"><span data-stu-id="c72ce-123">[Integrate Azure Media Services OWIN MVC based app with Azure Active Directory and restrict content key delivery based on JWT claims](http://www.gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/).</span></span>

<span data-ttu-id="c72ce-124">[Utilisation d'ACS Azure pour émettre des jetons](http://mingfeiy.com/acs-with-key-services)</span><span class="sxs-lookup"><span data-stu-id="c72ce-124">[Use Azure ACS to issue tokens](http://mingfeiy.com/acs-with-key-services).</span></span>

### <a name="some-considerations-apply"></a><span data-ttu-id="c72ce-125">Certaines considérations s’appliquent :</span><span class="sxs-lookup"><span data-stu-id="c72ce-125">Some considerations apply:</span></span>
* <span data-ttu-id="c72ce-126">Une fois votre compte AMS créé, un point de terminaison de streaming **par défaut** est ajouté à votre compte à l’état **Arrêté**.</span><span class="sxs-lookup"><span data-stu-id="c72ce-126">When your AMS account is created a **default** streaming endpoint is added  to your account in the **Stopped** state.</span></span> <span data-ttu-id="c72ce-127">Pour démarrer la diffusion en continu de votre contenu et tirer parti de l’empaquetage et du chiffrement dynamiques, votre point de terminaison de streaming doit se trouver à l’état **En cours d’exécution**.</span><span class="sxs-lookup"><span data-stu-id="c72ce-127">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, your streaming endpoint has to be in the **Running** state.</span></span> 
* <span data-ttu-id="c72ce-128">Votre ressource doit contenir un ensemble de MP4 à débit adaptatif ou des fichiers de diffusion en continu lisse à débit adaptatif.</span><span class="sxs-lookup"><span data-stu-id="c72ce-128">Your asset must contain a set of adaptive bitrate MP4s or  adaptive bitrate Smooth Streaming files.</span></span> <span data-ttu-id="c72ce-129">Pour plus d'informations, consultez [Encoder une ressource](media-services-encode-asset.md).</span><span class="sxs-lookup"><span data-stu-id="c72ce-129">For more information, see [Encode an asset](media-services-encode-asset.md).</span></span>
* <span data-ttu-id="c72ce-130">Téléchargez et codez vos ressources à l'aide de l'option **AssetCreationOptions.StorageEncrypted** .</span><span class="sxs-lookup"><span data-stu-id="c72ce-130">Upload and encode your assets using **AssetCreationOptions.StorageEncrypted** option.</span></span>
* <span data-ttu-id="c72ce-131">Si vous prévoyez d’avoir plusieurs clés de contenu qui nécessitent la même configuration de stratégie, il est fortement recommandé de créer une stratégie d’autorisation unique et de la réutiliser avec plusieurs clés de contenu.</span><span class="sxs-lookup"><span data-stu-id="c72ce-131">If you plan to have multiple content keys that require the same policy configuration, it is strongly recommended to create a single authorization policy and reuse it with multiple content keys.</span></span>
* <span data-ttu-id="c72ce-132">Le service de remise de clé met en cache ContentKeyAuthorizationPolicy et ses objets connexes (options de stratégie et restrictions) pendant 15 minutes.</span><span class="sxs-lookup"><span data-stu-id="c72ce-132">The Key Delivery service caches ContentKeyAuthorizationPolicy and its related objects (policy options and restrictions) for 15 minutes.</span></span>  <span data-ttu-id="c72ce-133">Si vous créez une ContentKeyAuthorizationPolicy et que vous spécifiez l’utilisation d’une restriction « Jeton », puis la testez avant de mettre à jour la stratégie de restriction vers « Ouverte », vous devrez attendre environ 15 minutes avant que la stratégie bascule vers la version « Ouverte ».</span><span class="sxs-lookup"><span data-stu-id="c72ce-133">If you create a ContentKeyAuthorizationPolicy and specify to use a “Token” restriction, then test it, and then update the policy to “Open” restriction, it will take roughly 15 minutes before the policy switches to the “Open” version of the policy.</span></span>
* <span data-ttu-id="c72ce-134">Si vous ajoutez ou mettez à jour la stratégie de remise de votre ressource, vous devez supprimer le localisateur existant (le cas échéant) et en créer un nouveau.</span><span class="sxs-lookup"><span data-stu-id="c72ce-134">If you add or update your asset’s delivery policy, you must delete an existing locator (if any) and create a new locator.</span></span>
* <span data-ttu-id="c72ce-135">Actuellement, vous ne pouvez pas chiffrer les téléchargements progressifs.</span><span class="sxs-lookup"><span data-stu-id="c72ce-135">Currently, you cannot encrypt progressive downloads.</span></span>

## <a name="aes-128-dynamic-encryption"></a><span data-ttu-id="c72ce-136">Chiffrement dynamique AES-128.</span><span class="sxs-lookup"><span data-stu-id="c72ce-136">AES-128 Dynamic Encryption</span></span>
### <a name="open-restriction"></a><span data-ttu-id="c72ce-137">Restriction ouverte</span><span class="sxs-lookup"><span data-stu-id="c72ce-137">Open Restriction</span></span>
<span data-ttu-id="c72ce-138">La restriction ouverte signifie que le système fournira la clé à toute personne effectuant une demande de clé.</span><span class="sxs-lookup"><span data-stu-id="c72ce-138">Open restriction means the system will deliver the key to anyone who makes a key request.</span></span> <span data-ttu-id="c72ce-139">Cette restriction peut être utile à des fins de test.</span><span class="sxs-lookup"><span data-stu-id="c72ce-139">This restriction might be useful for testing purposes.</span></span>

<span data-ttu-id="c72ce-140">L’exemple suivant crée une stratégie d’autorisation ouverte et l’ajoute à la clé de contenu.</span><span class="sxs-lookup"><span data-stu-id="c72ce-140">The following example creates an open authorization policy and adds it to the content key.</span></span>

    static public void AddOpenAuthorizationPolicy(IContentKey contentKey)
    {
        // Create ContentKeyAuthorizationPolicy with Open restrictions
        // and create authorization policy
        IContentKeyAuthorizationPolicy policy = _context.
        ContentKeyAuthorizationPolicies.
        CreateAsync("Open Authorization Policy").Result;
        
        List<ContentKeyAuthorizationPolicyRestriction> restrictions =
            new List<ContentKeyAuthorizationPolicyRestriction>();

        ContentKeyAuthorizationPolicyRestriction restriction =
            new ContentKeyAuthorizationPolicyRestriction
            {
                Name = "HLS Open Authorization Policy",
                KeyRestrictionType = (int)ContentKeyRestrictionType.Open,
                Requirements = null // no requirements needed for HLS
            };

        restrictions.Add(restriction);

        IContentKeyAuthorizationPolicyOption policyOption =
            _context.ContentKeyAuthorizationPolicyOptions.Create(
            "policy", 
            ContentKeyDeliveryType.BaselineHttp, 
            restrictions, 
            "");

        policy.Options.Add(policyOption);

        // Add ContentKeyAutorizationPolicy to ContentKey
        contentKey.AuthorizationPolicyId = policy.Id;
        IContentKey updatedKey = contentKey.UpdateAsync().Result;
        Console.WriteLine("Adding Key to Asset: Key ID is " + updatedKey.Id);
    }


### <a name="token-restriction"></a><span data-ttu-id="c72ce-141">Restriction par jeton</span><span class="sxs-lookup"><span data-stu-id="c72ce-141">Token Restriction</span></span>
<span data-ttu-id="c72ce-142">Cette section décrit comment créer une stratégie d’autorisation de clé de contenu et l’associer à la clé de contenu.</span><span class="sxs-lookup"><span data-stu-id="c72ce-142">This section describes how to create a content key authorization policy and associate it with the content key.</span></span> <span data-ttu-id="c72ce-143">La stratégie d’autorisation décrit les conditions d’autorisation devant être remplies pour déterminer si l’utilisateur est autorisé à recevoir la clé (par exemple, la liste « clé de vérification » contient-elle la clé qui a servi à signer le jeton).</span><span class="sxs-lookup"><span data-stu-id="c72ce-143">The authorization policy describes what authorization requirements must be met to determine if the user is authorized to receive the key (for example, does the “verification key” list contain the key that the token was signed with).</span></span>

<span data-ttu-id="c72ce-144">Pour configurer l’option de restriction par jeton, vous devez utiliser un document XML pour décrire les exigences du jeton d’autorisation.</span><span class="sxs-lookup"><span data-stu-id="c72ce-144">To configure the token restriction option, you need to use an XML to describe the token’s authorization requirements.</span></span> <span data-ttu-id="c72ce-145">Le XML de configuration de la restriction par jeton doit être conforme au schéma XML suivant.</span><span class="sxs-lookup"><span data-stu-id="c72ce-145">The token restriction configuration XML must conform to the following XML schema.</span></span>

#### <span data-ttu-id="c72ce-146"><a id="schema"></a>Schéma de restriction par jeton</span><span class="sxs-lookup"><span data-stu-id="c72ce-146"><a id="schema"></a>Token restriction schema</span></span>
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

<span data-ttu-id="c72ce-147">Lorsque vous configurez la stratégie de restriction par **jeton**, vous devez définir les paramètres de la **clé de vérification** principale, **d’émetteur** et **d’audience**.</span><span class="sxs-lookup"><span data-stu-id="c72ce-147">When configuring the **token** restricted policy, you must specify the primary** verification key**, **issuer** and **audience** parameters.</span></span> <span data-ttu-id="c72ce-148">La **clé de vérification principale** contient la clé utilisée pour signer le jeton, **l’émetteur** est le service de jeton sécurisé qui émet le jeton.</span><span class="sxs-lookup"><span data-stu-id="c72ce-148">The **primary verification key **contains the key that the token was signed with, **issuer** is the secure token service that issues the token.</span></span> <span data-ttu-id="c72ce-149">Le **public** (parfois appelé **l’étendue**) décrit l’objectif du jeton ou la ressource à laquelle le jeton autorise l’accès.</span><span class="sxs-lookup"><span data-stu-id="c72ce-149">The **audience** (sometimes called **scope**) describes the intent of the token or the resource the token authorizes access to.</span></span> <span data-ttu-id="c72ce-150">Le service de remise de clé Media Services valide le fait que les valeurs du jeton correspondent aux valeurs du modèle.</span><span class="sxs-lookup"><span data-stu-id="c72ce-150">The Media Services key delivery service validates that these values in the token match the values in the template.</span></span> 

<span data-ttu-id="c72ce-151">Quand vous utilisez le **Kit de développement logiciel (SDK) Media Services pour .NET**, vous pouvez utiliser la classe **TokenRestrictionTemplate** pour générer le jeton de restriction.</span><span class="sxs-lookup"><span data-stu-id="c72ce-151">When using **Media Services SDK for .NET**, you can use the **TokenRestrictionTemplate** class to generate the restriction token.</span></span>
<span data-ttu-id="c72ce-152">L’exemple suivant crée une stratégie d’autorisation avec une restriction par jeton.</span><span class="sxs-lookup"><span data-stu-id="c72ce-152">The following example creates an authorization policy with a token restriction.</span></span> <span data-ttu-id="c72ce-153">Dans cet exemple, le client devra présenter un jeton contenant : une clé de signature (VerificationKey), un émetteur de jeton et les revendications requises.</span><span class="sxs-lookup"><span data-stu-id="c72ce-153">In this example, the client would have to present a token that contains: signing key (VerificationKey), a token issuer, and required claims.</span></span>

    public static string AddTokenRestrictedAuthorizationPolicy(IContentKey contentKey)
    {
        string tokenTemplateString = GenerateTokenRequirements();

        IContentKeyAuthorizationPolicy policy = _context.
                                ContentKeyAuthorizationPolicies.
                                CreateAsync("HLS token restricted authorization policy").Result;

        List<ContentKeyAuthorizationPolicyRestriction> restrictions =
                new List<ContentKeyAuthorizationPolicyRestriction>();

        ContentKeyAuthorizationPolicyRestriction restriction =
                new ContentKeyAuthorizationPolicyRestriction
                {
                    Name = "Token Authorization Policy",
                    KeyRestrictionType = (int)ContentKeyRestrictionType.TokenRestricted,
                    Requirements = tokenTemplateString
                };

        restrictions.Add(restriction);

        //You could have multiple options 
        IContentKeyAuthorizationPolicyOption policyOption =
            _context.ContentKeyAuthorizationPolicyOptions.Create(
                "Token option for HLS",
                ContentKeyDeliveryType.BaselineHttp,
                restrictions,
                null  // no key delivery data is needed for HLS
                );

        policy.Options.Add(policyOption);

        // Add ContentKeyAutorizationPolicy to ContentKey
        contentKey.AuthorizationPolicyId = policy.Id;
        IContentKey updatedKey = contentKey.UpdateAsync().Result;
        Console.WriteLine("Adding Key to Asset: Key ID is " + updatedKey.Id);

        return tokenTemplateString;
    }

    static private string GenerateTokenRequirements()
    {
        TokenRestrictionTemplate template = new TokenRestrictionTemplate(TokenType.SWT);

        template.PrimaryVerificationKey = new SymmetricVerificationKey();
        template.AlternateVerificationKeys.Add(new SymmetricVerificationKey());
            template.Audience = _sampleAudience.ToString();
            template.Issuer = _sampleIssuer.ToString();

        template.RequiredClaims.Add(TokenClaim.ContentKeyIdentifierClaim);

        return TokenRestrictionTemplateSerializer.Serialize(template);
    }

#### <span data-ttu-id="c72ce-154"><a id="test"></a>Jeton de test</span><span class="sxs-lookup"><span data-stu-id="c72ce-154"><a id="test"></a>Test token</span></span>
<span data-ttu-id="c72ce-155">Pour obtenir un jeton de test basé sur la restriction par jeton utilisée pour la stratégie d’autorisation de clé, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="c72ce-155">To get a test token based on the token restriction that was used for the key authorization policy, do the following.</span></span>

    // Deserializes a string containing an Xml representation of a TokenRestrictionTemplate
    // back into a TokenRestrictionTemplate class instance.
    TokenRestrictionTemplate tokenTemplate =
        TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

    // Generate a test token based on the the data in the given TokenRestrictionTemplate.
    // Note, you need to pass the key id Guid because we specified 
    // TokenClaim.ContentKeyIdentifierClaim in during the creation of TokenRestrictionTemplate.
    Guid rawkey = EncryptionUtils.GetKeyIdAsGuid(key.Id);

    //The GenerateTestToken method returns the token without the word “Bearer” in front
    //so you have to add it in front of the token string. 
    string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate, null, rawkey);
    Console.WriteLine("The authorization token is:\nBearer {0}", testToken);
    Console.WriteLine();


## <a name="playready-dynamic-encryption"></a><span data-ttu-id="c72ce-156">Chiffrement dynamique PlayReady</span><span class="sxs-lookup"><span data-stu-id="c72ce-156">PlayReady Dynamic Encryption</span></span>
<span data-ttu-id="c72ce-157">Media Services vous permet de configurer les droits et les restrictions que vous souhaitez pour le runtime DRM PlayReady, qui s’appliquent lorsqu’un utilisateur tente de lire un contenu protégé.</span><span class="sxs-lookup"><span data-stu-id="c72ce-157">Media Services enables you to configure the rights and restrictions that you want for the PlayReady DRM runtime to enforce when a user is trying to play back protected content.</span></span> 

<span data-ttu-id="c72ce-158">Quand vous protégez votre contenu avec PlayReady, vous devez spécifier dans votre stratégie d'autorisation une chaîne XML qui définisse le [modèle de licence PlayReady](media-services-playready-license-template-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c72ce-158">When protecting your content with PlayReady, one of the things you need to specify in your authorization policy is an XML string that defines the [PlayReady license template](media-services-playready-license-template-overview.md).</span></span> <span data-ttu-id="c72ce-159">Dans le Kit de développement logiciel (SDK) Media Services pour .NET, les classes **PlayReadyLicenseResponseTemplate** et **PlayReadyLicenseTemplate** vous aideront à définir le modèle de licence PlayReady.</span><span class="sxs-lookup"><span data-stu-id="c72ce-159">In Media Services SDK for .NET, the **PlayReadyLicenseResponseTemplate** and **PlayReadyLicenseTemplate** classes will help you define the PlayReady License Template.</span></span>

<span data-ttu-id="c72ce-160">[Cette rubrique](media-services-protect-with-drm.md) montre comment chiffrer votre contenu avec **PlayReady** et **Widevine**.</span><span class="sxs-lookup"><span data-stu-id="c72ce-160">[This topic](media-services-protect-with-drm.md) shows how to encrypt your content with **PlayReady** and **Widevine**.</span></span>

### <a name="open-restriction"></a><span data-ttu-id="c72ce-161">Restriction ouverte</span><span class="sxs-lookup"><span data-stu-id="c72ce-161">Open Restriction</span></span>
<span data-ttu-id="c72ce-162">La restriction ouverte signifie que le système fournira la clé à toute personne effectuant une demande de clé.</span><span class="sxs-lookup"><span data-stu-id="c72ce-162">Open restriction means the system will deliver the key to anyone who makes a key request.</span></span> <span data-ttu-id="c72ce-163">Cette restriction peut être utile à des fins de test.</span><span class="sxs-lookup"><span data-stu-id="c72ce-163">This restriction might be useful for testing purposes.</span></span>

<span data-ttu-id="c72ce-164">L’exemple suivant crée une stratégie d’autorisation ouverte et l’ajoute à la clé de contenu.</span><span class="sxs-lookup"><span data-stu-id="c72ce-164">The following example creates an open authorization policy and adds it to the content key.</span></span>

    static public void AddOpenAuthorizationPolicy(IContentKey contentKey)
    {

        // Create ContentKeyAuthorizationPolicy with Open restrictions 
        // and create authorization policy          

        List<ContentKeyAuthorizationPolicyRestriction> restrictions = new List<ContentKeyAuthorizationPolicyRestriction>
        {
            new ContentKeyAuthorizationPolicyRestriction 
            { 
                Name = "Open", 
                KeyRestrictionType = (int)ContentKeyRestrictionType.Open, 
                Requirements = null
            }
        };

        // Configure PlayReady license template.
        string newLicenseTemplate = ConfigurePlayReadyLicenseTemplate();

        IContentKeyAuthorizationPolicyOption policyOption =
            _context.ContentKeyAuthorizationPolicyOptions.Create("",
                ContentKeyDeliveryType.PlayReadyLicense,
                    restrictions, newLicenseTemplate);

        IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                    ContentKeyAuthorizationPolicies.
                    CreateAsync("Deliver Common Content Key with no restrictions").
                    Result;


        contentKeyAuthorizationPolicy.Options.Add(policyOption);

        // Associate the content key authorization policy with the content key.
        contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
        contentKey = contentKey.UpdateAsync().Result;
    }

### <a name="token-restriction"></a><span data-ttu-id="c72ce-165">Restriction par jeton</span><span class="sxs-lookup"><span data-stu-id="c72ce-165">Token Restriction</span></span>
<span data-ttu-id="c72ce-166">Pour configurer l’option de restriction par jeton, vous devez utiliser un document XML pour décrire les exigences du jeton d’autorisation.</span><span class="sxs-lookup"><span data-stu-id="c72ce-166">To configure the token restriction option, you need to use an XML to describe the token’s authorization requirements.</span></span> <span data-ttu-id="c72ce-167">Le XML de configuration de la restriction par jeton doit être conforme au schéma XML présenté dans [cette](#schema) section.</span><span class="sxs-lookup"><span data-stu-id="c72ce-167">The token restriction configuration XML must conform to the XML schema shown in [this](#schema) section.</span></span>

    public static string AddTokenRestrictedAuthorizationPolicy(IContentKey contentKey)
    {
        string tokenTemplateString = GenerateTokenRequirements();

        IContentKeyAuthorizationPolicy policy = _context.
                                ContentKeyAuthorizationPolicies.
                                CreateAsync("HLS token restricted authorization policy").Result;

        List<ContentKeyAuthorizationPolicyRestriction> restrictions = new List<ContentKeyAuthorizationPolicyRestriction>
        {
            new ContentKeyAuthorizationPolicyRestriction 
            { 
                Name = "Token Authorization Policy", 
                KeyRestrictionType = (int)ContentKeyRestrictionType.TokenRestricted,
                Requirements = tokenTemplateString, 
            }
        };

        // Configure PlayReady license template.
        string newLicenseTemplate = ConfigurePlayReadyLicenseTemplate();

        IContentKeyAuthorizationPolicyOption policyOption =
            _context.ContentKeyAuthorizationPolicyOptions.Create("Token option",
                ContentKeyDeliveryType.PlayReadyLicense,
                    restrictions, newLicenseTemplate);

        IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                    ContentKeyAuthorizationPolicies.
                    CreateAsync("Deliver Common Content Key with no restrictions").
                    Result;

        policy.Options.Add(policyOption);

        // Add ContentKeyAutorizationPolicy to ContentKey
        contentKeyAuthorizationPolicy.Options.Add(policyOption);

        // Associate the content key authorization policy with the content key
        contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
        contentKey = contentKey.UpdateAsync().Result;

        return tokenTemplateString;
    }

    static private string GenerateTokenRequirements()
    {

        TokenRestrictionTemplate template = new TokenRestrictionTemplate(TokenType.SWT);

        template.PrimaryVerificationKey = new SymmetricVerificationKey();
        template.AlternateVerificationKeys.Add(new SymmetricVerificationKey());
            template.Audience = _sampleAudience.ToString();
            template.Issuer = _sampleIssuer.ToString();


        template.RequiredClaims.Add(TokenClaim.ContentKeyIdentifierClaim);

        return TokenRestrictionTemplateSerializer.Serialize(template);
    } 

    static private string ConfigurePlayReadyLicenseTemplate()
    {
        // The following code configures PlayReady License Template using .NET classes
        // and returns the XML string.

        //The PlayReadyLicenseResponseTemplate class represents the template for the response sent back to the end user. 
        //It contains a field for a custom data string between the license server and the application 
        //(may be useful for custom app logic) as well as a list of one or more license templates.
        PlayReadyLicenseResponseTemplate responseTemplate = new PlayReadyLicenseResponseTemplate();

        // The PlayReadyLicenseTemplate class represents a license template for creating PlayReady licenses
        // to be returned to the end users. 
        //It contains the data on the content key in the license and any rights or restrictions to be 
        //enforced by the PlayReady DRM runtime when using the content key.
        PlayReadyLicenseTemplate licenseTemplate = new PlayReadyLicenseTemplate();
        //Configure whether the license is persistent (saved in persistent storage on the client) 
        //or non-persistent (only held in memory while the player is using the license).  
        licenseTemplate.LicenseType = PlayReadyLicenseType.Nonpersistent;

        // AllowTestDevices controls whether test devices can use the license or not.  
        // If true, the MinimumSecurityLevel property of the license
        // is set to 150.  If false (the default), the MinimumSecurityLevel property of the license is set to 2000.
        licenseTemplate.AllowTestDevices = true;


        // You can also configure the Play Right in the PlayReady license by using the PlayReadyPlayRight class. 
        // It grants the user the ability to playback the content subject to the zero or more restrictions 
        // configured in the license and on the PlayRight itself (for playback specific policy). 
        // Much of the policy on the PlayRight has to do with output restrictions 
        // which control the types of outputs that the content can be played over and 
        // any restrictions that must be put in place when using a given output.
        // For example, if the DigitalVideoOnlyContentRestriction is enabled, 
        //then the DRM runtime will only allow the video to be displayed over digital outputs 
        //(analog video outputs won’t be allowed to pass the content).

        //IMPORTANT: These types of restrictions can be very powerful but can also affect the consumer experience. 
        // If the output protections are configured too restrictive, 
        // the content might be unplayable on some clients. For more information, see the PlayReady Compliance Rules document.

        // For example:
        //licenseTemplate.PlayRight.AgcAndColorStripeRestriction = new AgcAndColorStripeRestriction(1);

        responseTemplate.LicenseTemplates.Add(licenseTemplate);

        return MediaServicesLicenseTemplateSerializer.Serialize(responseTemplate);
    }


<span data-ttu-id="c72ce-168">Pour obtenir un jeton de test basé sur la restriction par jeton utilisée pour la stratégie d'autorisation de clé, consultez [cette](#test) section.</span><span class="sxs-lookup"><span data-stu-id="c72ce-168">To get a test token based on the token restriction that was used for the key authorization policy see [this](#test) section.</span></span> 

## <span data-ttu-id="c72ce-169"><a id="types"></a>Types utilisés durant la définition de ContentKeyAuthorizationPolicy</span><span class="sxs-lookup"><span data-stu-id="c72ce-169"><a id="types"></a>Types used when defining ContentKeyAuthorizationPolicy</span></span>
### <span data-ttu-id="c72ce-170"><a id="ContentKeyRestrictionType"></a>ContentKeyRestrictionType</span><span class="sxs-lookup"><span data-stu-id="c72ce-170"><a id="ContentKeyRestrictionType"></a>ContentKeyRestrictionType</span></span>
    public enum ContentKeyRestrictionType
    {
        Open = 0,
        TokenRestricted = 1,
        IPRestricted = 2,
    }

### <span data-ttu-id="c72ce-171"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span><span class="sxs-lookup"><span data-stu-id="c72ce-171"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span></span>
    public enum ContentKeyDeliveryType
    {
      None = 0,
      PlayReadyLicense = 1,
      BaselineHttp = 2,
      Widevine = 3
    }

### <span data-ttu-id="c72ce-172"><a id="TokenType"></a>TokenType</span><span class="sxs-lookup"><span data-stu-id="c72ce-172"><a id="TokenType"></a>TokenType</span></span>
    public enum TokenType
    {
        Undefined = 0,
        SWT = 1,
        JWT = 2,
    }



## <a name="media-services-learning-paths"></a><span data-ttu-id="c72ce-173">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="c72ce-173">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="c72ce-174">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="c72ce-174">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-step"></a><span data-ttu-id="c72ce-175">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="c72ce-175">Next step</span></span>
<span data-ttu-id="c72ce-176">La stratégie d'autorisation de la clé de contenu étant configurée, consultez la rubrique [Comment configurer une stratégie de remise de ressources](media-services-dotnet-configure-asset-delivery-policy.md) .</span><span class="sxs-lookup"><span data-stu-id="c72ce-176">Now that you have configured content key's authorization policy, go to the [How to configure asset delivery policy](media-services-dotnet-configure-asset-delivery-policy.md) topic.</span></span>

