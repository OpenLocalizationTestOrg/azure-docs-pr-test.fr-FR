---
title: "stratégie de contenu d’autorisation de clé aaaConfigure à l’aide de Media Services .NET SDK | Documents Microsoft"
description: "Découvrez comment tooconfigure une stratégie d’autorisation pour une clé de contenu à l’aide de Media Services .NET SDK."
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
ms.openlocfilehash: cfcbc5da9819bcec8b163fef183988a8beff9ed2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="dynamic-encryption-configure-content-key-authorization-policy"></a><span data-ttu-id="6bb87-103">Chiffrement dynamique : configurer la stratégie d’autorisation de clé de contenu</span><span class="sxs-lookup"><span data-stu-id="6bb87-103">Dynamic encryption: configure content key authorization policy</span></span>
[!INCLUDE [media-services-selector-content-key-auth-policy](../../includes/media-services-selector-content-key-auth-policy.md)]

## <a name="overview"></a><span data-ttu-id="6bb87-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="6bb87-104">Overview</span></span>
<span data-ttu-id="6bb87-105">Microsoft Azure Media Services vous permet de toodeliver MPEG-DASH, Smooth Streaming et les flux HTTP Live Streaming (HLS) protégés avec Advanced Encryption Standard (AES) (à l’aide de clés de chiffrement 128 bits) ou [Microsoft PlayReady DRM](https://www.microsoft.com/playready/overview/).</span><span class="sxs-lookup"><span data-stu-id="6bb87-105">Microsoft Azure Media Services enables you toodeliver MPEG-DASH, Smooth Streaming, and HTTP-Live-Streaming (HLS) streams protected with Advanced Encryption Standard (AES) (using 128-bit encryption keys) or [Microsoft PlayReady DRM](https://www.microsoft.com/playready/overview/).</span></span> <span data-ttu-id="6bb87-106">AMS permet également de vous toodeliver tiret flux chiffrés avec Widevine DRM.</span><span class="sxs-lookup"><span data-stu-id="6bb87-106">AMS also enables you toodeliver DASH streams encrypted with Widevine DRM.</span></span> <span data-ttu-id="6bb87-107">PlayReady et Widevine sont chiffrées par hello spécification de chiffrement commun (CENC 23001-7 de norme ISO/IEC).</span><span class="sxs-lookup"><span data-stu-id="6bb87-107">Both PlayReady and Widevine are encrypted per hello Common Encryption (ISO/IEC 23001-7 CENC) specification.</span></span>

<span data-ttu-id="6bb87-108">Media Services fournit également un **Service de remise de clé/licence** à partir desquels les clients peuvent obtenir des clés AES ou PlayReady/Widevine licences tooplay hello contenu chiffré.</span><span class="sxs-lookup"><span data-stu-id="6bb87-108">Media Services also provides a **Key/License Delivery Service** from which clients can obtain AES keys or PlayReady/Widevine licenses tooplay hello encrypted content.</span></span>

<span data-ttu-id="6bb87-109">Si vous souhaitez un élément multimédia pour tooencrypt de Media Services, vous devez tooassociate une clé de chiffrement (**CommonEncryption** ou **EnvelopeEncryption**) avec l’élément multimédia de hello (comme décrit [ici](media-services-dotnet-create-contentkey.md)) et également configurer des stratégies d’autorisation pour la clé hello (comme décrit dans cet article).</span><span class="sxs-lookup"><span data-stu-id="6bb87-109">If you want for Media Services tooencrypt an asset, you need tooassociate an encryption key (**CommonEncryption** or **EnvelopeEncryption**) with hello asset (as described [here](media-services-dotnet-create-contentkey.md)) and also configure authorization policies for hello key (as described in this article).</span></span>

<span data-ttu-id="6bb87-110">Lorsqu’un flux de données est demandée par un lecteur, Media Services utilise hello spécifié toodynamically clé chiffrer votre contenu à l’aide du chiffrement AES ou la gestion des droits numériques.</span><span class="sxs-lookup"><span data-stu-id="6bb87-110">When a stream is requested by a player, Media Services uses hello specified key toodynamically encrypt your content using AES or DRM encryption.</span></span> <span data-ttu-id="6bb87-111">flux de données toodecrypt hello, le lecteur hello demande clé de hello de service de distribution de clés hello.</span><span class="sxs-lookup"><span data-stu-id="6bb87-111">toodecrypt hello stream, hello player will request hello key from hello key delivery service.</span></span> <span data-ttu-id="6bb87-112">toodecide soit ou non d’utilisateur de hello autorisé clé de hello tooget, hello évalue les stratégies d’autorisation hello que vous avez spécifié pour la clé de hello.</span><span class="sxs-lookup"><span data-stu-id="6bb87-112">toodecide whether or not hello user is authorized tooget hello key, hello service evaluates hello authorization policies that you specified for hello key.</span></span>

<span data-ttu-id="6bb87-113">Media Services prend en charge plusieurs méthodes d’authentification des utilisateurs effectuant des demandes de clé.</span><span class="sxs-lookup"><span data-stu-id="6bb87-113">Media Services supports multiple ways of authenticating users who make key requests.</span></span> <span data-ttu-id="6bb87-114">Hello contenu clé peut avoir une ou plusieurs restrictions d’autorisation : **ouvrir** ou **jeton** restriction.</span><span class="sxs-lookup"><span data-stu-id="6bb87-114">hello content key authorization policy could have one or more authorization restrictions: **open** or **token** restriction.</span></span> <span data-ttu-id="6bb87-115">stratégie de restriction token Hello doit être accompagné d’un jeton émis par un Service (jeton de sécurité).</span><span class="sxs-lookup"><span data-stu-id="6bb87-115">hello token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="6bb87-116">Media Services prend en charge les jetons Bonjour **des jetons Web simples** ([SWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2)) format et **jeton Web JSON** ([JWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3)) format.</span><span class="sxs-lookup"><span data-stu-id="6bb87-116">Media Services supports tokens in hello **Simple Web Tokens** ([SWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2)) format and **JSON Web Token** ([JWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3)) format.</span></span>

<span data-ttu-id="6bb87-117">Media Services ne fournit pas de services de jeton sécurisé.</span><span class="sxs-lookup"><span data-stu-id="6bb87-117">Media Services does not provide Secure Token Services.</span></span> <span data-ttu-id="6bb87-118">Vous pouvez créer un STS personnalisé ou tirer parti des jetons de tooissue Microsoft Azure ACS.</span><span class="sxs-lookup"><span data-stu-id="6bb87-118">You can create a custom STS or leverage Microsoft Azure ACS tooissue tokens.</span></span> <span data-ttu-id="6bb87-119">Hello STS doit être configuré toocreate un jeton signé avec la clé spécifiée de hello et les revendications de problème que vous avez spécifié dans la configuration de restriction token hello (comme décrit dans cet article).</span><span class="sxs-lookup"><span data-stu-id="6bb87-119">hello STS must be configured toocreate a token signed with hello specified key and issue claims that you specified in hello token restriction configuration (as described in this article).</span></span> <span data-ttu-id="6bb87-120">Hello service de distribution de clés de Media Services renvoie client de toohello clé de chiffrement hello si hello du jeton est valide et hello revendications de jeton de hello correspondent à ceux configurés pour la clé de contenu hello.</span><span class="sxs-lookup"><span data-stu-id="6bb87-120">hello Media Services key delivery service will return hello encryption key toohello client if hello token is valid and hello claims in hello token match those configured for hello content key.</span></span>

<span data-ttu-id="6bb87-121">Pour plus d'informations, consultez la rubrique</span><span class="sxs-lookup"><span data-stu-id="6bb87-121">For more information, see</span></span>

[<span data-ttu-id="6bb87-122">Authentification par jeton JWT</span><span class="sxs-lookup"><span data-stu-id="6bb87-122">JWT token authentication</span></span>](http://www.gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/)

<span data-ttu-id="6bb87-123">[Intégration d'une application Azure Media Services basée sur OWIN MVC avec Azure Active Directory et une remise de clé de contenu basée sur les revendications JWT](http://www.gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/)</span><span class="sxs-lookup"><span data-stu-id="6bb87-123">[Integrate Azure Media Services OWIN MVC based app with Azure Active Directory and restrict content key delivery based on JWT claims](http://www.gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/).</span></span>

<span data-ttu-id="6bb87-124">[Utilisez les jetons ACS Azure tooissue](http://mingfeiy.com/acs-with-key-services).</span><span class="sxs-lookup"><span data-stu-id="6bb87-124">[Use Azure ACS tooissue tokens](http://mingfeiy.com/acs-with-key-services).</span></span>

### <a name="some-considerations-apply"></a><span data-ttu-id="6bb87-125">Certaines considérations s’appliquent :</span><span class="sxs-lookup"><span data-stu-id="6bb87-125">Some considerations apply:</span></span>
* <span data-ttu-id="6bb87-126">Création de votre compte AMS un **par défaut** point de terminaison de diffusion en continu est ajoutée tooyour compte Bonjour **arrêté** état.</span><span class="sxs-lookup"><span data-stu-id="6bb87-126">When your AMS account is created a **default** streaming endpoint is added  tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="6bb87-127">toostart votre contenu et profitez de l’empaquetage dynamique et chiffrement dynamique, votre point de terminaison de diffusion en continu de diffusion en continu a toobe Bonjour **en cours d’exécution** état.</span><span class="sxs-lookup"><span data-stu-id="6bb87-127">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, your streaming endpoint has toobe in hello **Running** state.</span></span> 
* <span data-ttu-id="6bb87-128">Votre ressource doit contenir un ensemble de MP4 à débit adaptatif ou des fichiers Smooth Streaming à débit adaptatif.</span><span class="sxs-lookup"><span data-stu-id="6bb87-128">Your asset must contain a set of adaptive bitrate MP4s or  adaptive bitrate Smooth Streaming files.</span></span> <span data-ttu-id="6bb87-129">Pour plus d'informations, consultez [Encoder une ressource](media-services-encode-asset.md).</span><span class="sxs-lookup"><span data-stu-id="6bb87-129">For more information, see [Encode an asset](media-services-encode-asset.md).</span></span>
* <span data-ttu-id="6bb87-130">Téléchargez et codez vos ressources à l'aide de l'option **AssetCreationOptions.StorageEncrypted** .</span><span class="sxs-lookup"><span data-stu-id="6bb87-130">Upload and encode your assets using **AssetCreationOptions.StorageEncrypted** option.</span></span>
* <span data-ttu-id="6bb87-131">Si vous envisagez de toohave plusieurs clés de contenu qui nécessitent hello même configuration de la stratégie, il est fortement recommandé de toocreate une seule stratégie d’autorisation et la réutiliser avec plusieurs clés de contenu.</span><span class="sxs-lookup"><span data-stu-id="6bb87-131">If you plan toohave multiple content keys that require hello same policy configuration, it is strongly recommended toocreate a single authorization policy and reuse it with multiple content keys.</span></span>
* <span data-ttu-id="6bb87-132">Hello service de fourniture de clé met en cache ContentKeyAuthorizationPolicy et les objets associés (options de stratégie et les restrictions) pendant 15 minutes.</span><span class="sxs-lookup"><span data-stu-id="6bb87-132">hello Key Delivery service caches ContentKeyAuthorizationPolicy and its related objects (policy options and restrictions) for 15 minutes.</span></span>  <span data-ttu-id="6bb87-133">Si vous créez une stratégie ContentKeyAuthorizationPolicy et spécifiez toouse une restriction « Token », puis testez, puis mettre à jour de stratégie de hello trop « ouvrir » restriction, il prendra environ 15 minutes avant hello commutateurs toohello « Ouvert » version de stratégie de la stratégie de hello.</span><span class="sxs-lookup"><span data-stu-id="6bb87-133">If you create a ContentKeyAuthorizationPolicy and specify toouse a “Token” restriction, then test it, and then update hello policy too“Open” restriction, it will take roughly 15 minutes before hello policy switches toohello “Open” version of hello policy.</span></span>
* <span data-ttu-id="6bb87-134">Si vous ajoutez ou mettez à jour la stratégie de remise de votre ressource, vous devez supprimer le localisateur existant (le cas échéant) et en créer un nouveau.</span><span class="sxs-lookup"><span data-stu-id="6bb87-134">If you add or update your asset’s delivery policy, you must delete an existing locator (if any) and create a new locator.</span></span>
* <span data-ttu-id="6bb87-135">Actuellement, vous ne pouvez pas chiffrer les téléchargements progressifs.</span><span class="sxs-lookup"><span data-stu-id="6bb87-135">Currently, you cannot encrypt progressive downloads.</span></span>

## <a name="aes-128-dynamic-encryption"></a><span data-ttu-id="6bb87-136">Chiffrement dynamique AES-128.</span><span class="sxs-lookup"><span data-stu-id="6bb87-136">AES-128 Dynamic Encryption</span></span>
### <a name="open-restriction"></a><span data-ttu-id="6bb87-137">Restriction ouverte</span><span class="sxs-lookup"><span data-stu-id="6bb87-137">Open Restriction</span></span>
<span data-ttu-id="6bb87-138">Restriction Open signifie hello système fournit des tooanyone clé hello qui fait la demande.</span><span class="sxs-lookup"><span data-stu-id="6bb87-138">Open restriction means hello system will deliver hello key tooanyone who makes a key request.</span></span> <span data-ttu-id="6bb87-139">Cette restriction peut être utile à des fins de test.</span><span class="sxs-lookup"><span data-stu-id="6bb87-139">This restriction might be useful for testing purposes.</span></span>

<span data-ttu-id="6bb87-140">Hello, l’exemple suivant crée une stratégie d’autorisation ouverte et il ajoute la clé de contenu toohello.</span><span class="sxs-lookup"><span data-stu-id="6bb87-140">hello following example creates an open authorization policy and adds it toohello content key.</span></span>

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

        // Add ContentKeyAutorizationPolicy tooContentKey
        contentKey.AuthorizationPolicyId = policy.Id;
        IContentKey updatedKey = contentKey.UpdateAsync().Result;
        Console.WriteLine("Adding Key tooAsset: Key ID is " + updatedKey.Id);
    }


### <a name="token-restriction"></a><span data-ttu-id="6bb87-141">Restriction par jeton</span><span class="sxs-lookup"><span data-stu-id="6bb87-141">Token Restriction</span></span>
<span data-ttu-id="6bb87-142">Cette section décrit comment toocreate un contenu de stratégie d’autorisation de clé et l’associer à la clé de contenu hello.</span><span class="sxs-lookup"><span data-stu-id="6bb87-142">This section describes how toocreate a content key authorization policy and associate it with hello content key.</span></span> <span data-ttu-id="6bb87-143">stratégie d’autorisation de Hello décrit les spécifications d’autorisation doivent être rempli toodetermine si utilisateur de hello est clé de hello tooreceive autorisés (par exemple, liste de « clé de vérification » hello contenir la clé de hello ce jeton hello a été signé avec).</span><span class="sxs-lookup"><span data-stu-id="6bb87-143">hello authorization policy describes what authorization requirements must be met toodetermine if hello user is authorized tooreceive hello key (for example, does hello “verification key” list contain hello key that hello token was signed with).</span></span>

<span data-ttu-id="6bb87-144">option de restriction token tooconfigure hello, vous devez toouse XML exigences d’autorisation du jeton toodescribe hello.</span><span class="sxs-lookup"><span data-stu-id="6bb87-144">tooconfigure hello token restriction option, you need toouse an XML toodescribe hello token’s authorization requirements.</span></span> <span data-ttu-id="6bb87-145">configuration de restriction token Hello XML doit être conforme à toohello suivant le schéma XML.</span><span class="sxs-lookup"><span data-stu-id="6bb87-145">hello token restriction configuration XML must conform toohello following XML schema.</span></span>

#### <span data-ttu-id="6bb87-146"><a id="schema"></a>Schéma de restriction par jeton</span><span class="sxs-lookup"><span data-stu-id="6bb87-146"><a id="schema"></a>Token restriction schema</span></span>
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

<span data-ttu-id="6bb87-147">Lors de la configuration hello **jeton** stratégie, vous devez spécifier hello principal ** vérification clé **, **émetteur** et **public** paramètres.</span><span class="sxs-lookup"><span data-stu-id="6bb87-147">When configuring hello **token** restricted policy, you must specify hello primary** verification key**, **issuer** and **audience** parameters.</span></span> <span data-ttu-id="6bb87-148">Hello ** clé de vérification principale ** contient clé hello hello jeton a été signé avec, **émetteur** est service de jeton sécurisé hello ce jeton hello de problèmes.</span><span class="sxs-lookup"><span data-stu-id="6bb87-148">hello **primary verification key **contains hello key that hello token was signed with, **issuer** is hello secure token service that issues hello token.</span></span> <span data-ttu-id="6bb87-149">Hello **public** (parfois appelé **étendue**) décrit l’intention de hello de jeton de hello ou ressource de hello jeton de hello autorise l’accès à.</span><span class="sxs-lookup"><span data-stu-id="6bb87-149">hello **audience** (sometimes called **scope**) describes hello intent of hello token or hello resource hello token authorizes access to.</span></span> <span data-ttu-id="6bb87-150">Hello service de distribution de clés de Media Services valide que ces valeurs dans le jeton de hello correspondent aux valeurs hello modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="6bb87-150">hello Media Services key delivery service validates that these values in hello token match hello values in hello template.</span></span> 

<span data-ttu-id="6bb87-151">Lorsque vous utilisez **Media Services SDK pour .NET**, vous pouvez utiliser hello **TokenRestrictionTemplate** jeton de restriction de classe toogenerate hello.</span><span class="sxs-lookup"><span data-stu-id="6bb87-151">When using **Media Services SDK for .NET**, you can use hello **TokenRestrictionTemplate** class toogenerate hello restriction token.</span></span>
<span data-ttu-id="6bb87-152">Bonjour à l’exemple suivant crée une stratégie d’autorisation avec une restriction token.</span><span class="sxs-lookup"><span data-stu-id="6bb87-152">hello following example creates an authorization policy with a token restriction.</span></span> <span data-ttu-id="6bb87-153">Dans cet exemple, les clients hello aurait toopresent un jeton qui contient : clé de signature (VerificationKey), un émetteur de jeton et les revendications nécessaires.</span><span class="sxs-lookup"><span data-stu-id="6bb87-153">In this example, hello client would have toopresent a token that contains: signing key (VerificationKey), a token issuer, and required claims.</span></span>

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

        // Add ContentKeyAutorizationPolicy tooContentKey
        contentKey.AuthorizationPolicyId = policy.Id;
        IContentKey updatedKey = contentKey.UpdateAsync().Result;
        Console.WriteLine("Adding Key tooAsset: Key ID is " + updatedKey.Id);

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

#### <span data-ttu-id="6bb87-154"><a id="test"></a>Jeton de test</span><span class="sxs-lookup"><span data-stu-id="6bb87-154"><a id="test"></a>Test token</span></span>
<span data-ttu-id="6bb87-155">tooget un jeton de test basé sur la restriction de type hello token qui a été utilisée pour la stratégie d’autorisation de clé de hello, hello suivant.</span><span class="sxs-lookup"><span data-stu-id="6bb87-155">tooget a test token based on hello token restriction that was used for hello key authorization policy, do hello following.</span></span>

    // Deserializes a string containing an Xml representation of a TokenRestrictionTemplate
    // back into a TokenRestrictionTemplate class instance.
    TokenRestrictionTemplate tokenTemplate =
        TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

    // Generate a test token based on hello hello data in hello given TokenRestrictionTemplate.
    // Note, you need toopass hello key id Guid because we specified 
    // TokenClaim.ContentKeyIdentifierClaim in during hello creation of TokenRestrictionTemplate.
    Guid rawkey = EncryptionUtils.GetKeyIdAsGuid(key.Id);

    //hello GenerateTestToken method returns hello token without hello word “Bearer” in front
    //so you have tooadd it in front of hello token string. 
    string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate, null, rawkey);
    Console.WriteLine("hello authorization token is:\nBearer {0}", testToken);
    Console.WriteLine();


## <a name="playready-dynamic-encryption"></a><span data-ttu-id="6bb87-156">Chiffrement dynamique PlayReady</span><span class="sxs-lookup"><span data-stu-id="6bb87-156">PlayReady Dynamic Encryption</span></span>
<span data-ttu-id="6bb87-157">Media Services vous permet de droits de hello tooconfigure et les restrictions que vous souhaitez pour hello PlayReady DRM runtime tooenforce lorsqu’un utilisateur essaye tooplay précédent du contenu protégé.</span><span class="sxs-lookup"><span data-stu-id="6bb87-157">Media Services enables you tooconfigure hello rights and restrictions that you want for hello PlayReady DRM runtime tooenforce when a user is trying tooplay back protected content.</span></span> 

<span data-ttu-id="6bb87-158">Lorsque vous protégez votre contenu avec PlayReady, un des éléments de hello vous devez toospecify dans votre stratégie d’autorisation est une chaîne XML qui définit hello [modèle de licence PlayReady](media-services-playready-license-template-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6bb87-158">When protecting your content with PlayReady, one of hello things you need toospecify in your authorization policy is an XML string that defines hello [PlayReady license template](media-services-playready-license-template-overview.md).</span></span> <span data-ttu-id="6bb87-159">Dans Media Services SDK pour .NET, hello **PlayReadyLicenseResponseTemplate** et **PlayReadyLicenseTemplate** classes vous permettent de définir le modèle de licence PlayReady de hello.</span><span class="sxs-lookup"><span data-stu-id="6bb87-159">In Media Services SDK for .NET, hello **PlayReadyLicenseResponseTemplate** and **PlayReadyLicenseTemplate** classes will help you define hello PlayReady License Template.</span></span>

<span data-ttu-id="6bb87-160">[Cette rubrique](media-services-protect-with-drm.md) montre comment tooencrypt votre contenu avec **PlayReady** et **Widevine**.</span><span class="sxs-lookup"><span data-stu-id="6bb87-160">[This topic](media-services-protect-with-drm.md) shows how tooencrypt your content with **PlayReady** and **Widevine**.</span></span>

### <a name="open-restriction"></a><span data-ttu-id="6bb87-161">Restriction ouverte</span><span class="sxs-lookup"><span data-stu-id="6bb87-161">Open Restriction</span></span>
<span data-ttu-id="6bb87-162">Restriction Open signifie hello système fournit des tooanyone clé hello qui fait la demande.</span><span class="sxs-lookup"><span data-stu-id="6bb87-162">Open restriction means hello system will deliver hello key tooanyone who makes a key request.</span></span> <span data-ttu-id="6bb87-163">Cette restriction peut être utile à des fins de test.</span><span class="sxs-lookup"><span data-stu-id="6bb87-163">This restriction might be useful for testing purposes.</span></span>

<span data-ttu-id="6bb87-164">Hello, l’exemple suivant crée une stratégie d’autorisation ouverte et il ajoute la clé de contenu toohello.</span><span class="sxs-lookup"><span data-stu-id="6bb87-164">hello following example creates an open authorization policy and adds it toohello content key.</span></span>

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

        // Associate hello content key authorization policy with hello content key.
        contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
        contentKey = contentKey.UpdateAsync().Result;
    }

### <a name="token-restriction"></a><span data-ttu-id="6bb87-165">Restriction par jeton</span><span class="sxs-lookup"><span data-stu-id="6bb87-165">Token Restriction</span></span>
<span data-ttu-id="6bb87-166">option de restriction token tooconfigure hello, vous devez toouse XML exigences d’autorisation du jeton toodescribe hello.</span><span class="sxs-lookup"><span data-stu-id="6bb87-166">tooconfigure hello token restriction option, you need toouse an XML toodescribe hello token’s authorization requirements.</span></span> <span data-ttu-id="6bb87-167">configuration de restriction token Hello XML doit être conforme à XSD toohello illustré [cela](#schema) section.</span><span class="sxs-lookup"><span data-stu-id="6bb87-167">hello token restriction configuration XML must conform toohello XML schema shown in [this](#schema) section.</span></span>

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

        // Add ContentKeyAutorizationPolicy tooContentKey
        contentKeyAuthorizationPolicy.Options.Add(policyOption);

        // Associate hello content key authorization policy with hello content key
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
        // hello following code configures PlayReady License Template using .NET classes
        // and returns hello XML string.

        //hello PlayReadyLicenseResponseTemplate class represents hello template for hello response sent back toohello end user. 
        //It contains a field for a custom data string between hello license server and hello application 
        //(may be useful for custom app logic) as well as a list of one or more license templates.
        PlayReadyLicenseResponseTemplate responseTemplate = new PlayReadyLicenseResponseTemplate();

        // hello PlayReadyLicenseTemplate class represents a license template for creating PlayReady licenses
        // toobe returned toohello end users. 
        //It contains hello data on hello content key in hello license and any rights or restrictions toobe 
        //enforced by hello PlayReady DRM runtime when using hello content key.
        PlayReadyLicenseTemplate licenseTemplate = new PlayReadyLicenseTemplate();
        //Configure whether hello license is persistent (saved in persistent storage on hello client) 
        //or non-persistent (only held in memory while hello player is using hello license).  
        licenseTemplate.LicenseType = PlayReadyLicenseType.Nonpersistent;

        // AllowTestDevices controls whether test devices can use hello license or not.  
        // If true, hello MinimumSecurityLevel property of hello license
        // is set too150.  If false (hello default), hello MinimumSecurityLevel property of hello license is set too2000.
        licenseTemplate.AllowTestDevices = true;


        // You can also configure hello Play Right in hello PlayReady license by using hello PlayReadyPlayRight class. 
        // It grants hello user hello ability tooplayback hello content subject toohello zero or more restrictions 
        // configured in hello license and on hello PlayRight itself (for playback specific policy). 
        // Much of hello policy on hello PlayRight has toodo with output restrictions 
        // which control hello types of outputs that hello content can be played over and 
        // any restrictions that must be put in place when using a given output.
        // For example, if hello DigitalVideoOnlyContentRestriction is enabled, 
        //then hello DRM runtime will only allow hello video toobe displayed over digital outputs 
        //(analog video outputs won’t be allowed toopass hello content).

        //IMPORTANT: These types of restrictions can be very powerful but can also affect hello consumer experience. 
        // If hello output protections are configured too restrictive, 
        // hello content might be unplayable on some clients. For more information, see hello PlayReady Compliance Rules document.

        // For example:
        //licenseTemplate.PlayRight.AgcAndColorStripeRestriction = new AgcAndColorStripeRestriction(1);

        responseTemplate.LicenseTemplates.Add(licenseTemplate);

        return MediaServicesLicenseTemplateSerializer.Serialize(responseTemplate);
    }


<span data-ttu-id="6bb87-168">tooget un jeton de test basé sur la restriction de type hello token qui a été utilisée pour voir de stratégie d’autorisation de clé hello [cela](#test) section.</span><span class="sxs-lookup"><span data-stu-id="6bb87-168">tooget a test token based on hello token restriction that was used for hello key authorization policy see [this](#test) section.</span></span> 

## <span data-ttu-id="6bb87-169"><a id="types"></a>Types utilisés durant la définition de ContentKeyAuthorizationPolicy</span><span class="sxs-lookup"><span data-stu-id="6bb87-169"><a id="types"></a>Types used when defining ContentKeyAuthorizationPolicy</span></span>
### <span data-ttu-id="6bb87-170"><a id="ContentKeyRestrictionType"></a>ContentKeyRestrictionType</span><span class="sxs-lookup"><span data-stu-id="6bb87-170"><a id="ContentKeyRestrictionType"></a>ContentKeyRestrictionType</span></span>
    public enum ContentKeyRestrictionType
    {
        Open = 0,
        TokenRestricted = 1,
        IPRestricted = 2,
    }

### <span data-ttu-id="6bb87-171"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span><span class="sxs-lookup"><span data-stu-id="6bb87-171"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span></span>
    public enum ContentKeyDeliveryType
    {
      None = 0,
      PlayReadyLicense = 1,
      BaselineHttp = 2,
      Widevine = 3
    }

### <span data-ttu-id="6bb87-172"><a id="TokenType"></a>TokenType</span><span class="sxs-lookup"><span data-stu-id="6bb87-172"><a id="TokenType"></a>TokenType</span></span>
    public enum TokenType
    {
        Undefined = 0,
        SWT = 1,
        JWT = 2,
    }



## <a name="media-services-learning-paths"></a><span data-ttu-id="6bb87-173">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="6bb87-173">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="6bb87-174">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="6bb87-174">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-step"></a><span data-ttu-id="6bb87-175">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="6bb87-175">Next step</span></span>
<span data-ttu-id="6bb87-176">Maintenant que vous avez configuré la stratégie d’autorisation de clé de contenu, accédez à toohello [la stratégie de livraison des actifs tooconfigure](media-services-dotnet-configure-asset-delivery-policy.md) rubrique.</span><span class="sxs-lookup"><span data-stu-id="6bb87-176">Now that you have configured content key's authorization policy, go toohello [How tooconfigure asset delivery policy](media-services-dotnet-configure-asset-delivery-policy.md) topic.</span></span>

