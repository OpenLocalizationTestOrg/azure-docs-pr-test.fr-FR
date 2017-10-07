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
# <a name="dynamic-encryption-configure-content-key-authorization-policy"></a>Chiffrement dynamique : configurer la stratégie d’autorisation de clé de contenu
[!INCLUDE [media-services-selector-content-key-auth-policy](../../includes/media-services-selector-content-key-auth-policy.md)]

## <a name="overview"></a>Vue d'ensemble
Microsoft Azure Media Services vous permet de toodeliver MPEG-DASH, Smooth Streaming et les flux HTTP Live Streaming (HLS) protégés avec Advanced Encryption Standard (AES) (à l’aide de clés de chiffrement 128 bits) ou [Microsoft PlayReady DRM](https://www.microsoft.com/playready/overview/). AMS permet également de vous toodeliver tiret flux chiffrés avec Widevine DRM. PlayReady et Widevine sont chiffrées par hello spécification de chiffrement commun (CENC 23001-7 de norme ISO/IEC).

Media Services fournit également un **Service de remise de clé/licence** à partir desquels les clients peuvent obtenir des clés AES ou PlayReady/Widevine licences tooplay hello contenu chiffré.

Si vous souhaitez un élément multimédia pour tooencrypt de Media Services, vous devez tooassociate une clé de chiffrement (**CommonEncryption** ou **EnvelopeEncryption**) avec l’élément multimédia de hello (comme décrit [ici](media-services-dotnet-create-contentkey.md)) et également configurer des stratégies d’autorisation pour la clé hello (comme décrit dans cet article).

Lorsqu’un flux de données est demandée par un lecteur, Media Services utilise hello spécifié toodynamically clé chiffrer votre contenu à l’aide du chiffrement AES ou la gestion des droits numériques. flux de données toodecrypt hello, le lecteur hello demande clé de hello de service de distribution de clés hello. toodecide soit ou non d’utilisateur de hello autorisé clé de hello tooget, hello évalue les stratégies d’autorisation hello que vous avez spécifié pour la clé de hello.

Media Services prend en charge plusieurs méthodes d’authentification des utilisateurs effectuant des demandes de clé. Hello contenu clé peut avoir une ou plusieurs restrictions d’autorisation : **ouvrir** ou **jeton** restriction. stratégie de restriction token Hello doit être accompagné d’un jeton émis par un Service (jeton de sécurité). Media Services prend en charge les jetons Bonjour **des jetons Web simples** ([SWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2)) format et **jeton Web JSON** ([JWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3)) format.

Media Services ne fournit pas de services de jeton sécurisé. Vous pouvez créer un STS personnalisé ou tirer parti des jetons de tooissue Microsoft Azure ACS. Hello STS doit être configuré toocreate un jeton signé avec la clé spécifiée de hello et les revendications de problème que vous avez spécifié dans la configuration de restriction token hello (comme décrit dans cet article). Hello service de distribution de clés de Media Services renvoie client de toohello clé de chiffrement hello si hello du jeton est valide et hello revendications de jeton de hello correspondent à ceux configurés pour la clé de contenu hello.

Pour plus d'informations, consultez la rubrique

[Authentification par jeton JWT](http://www.gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/)

[Intégration d'une application Azure Media Services basée sur OWIN MVC avec Azure Active Directory et une remise de clé de contenu basée sur les revendications JWT](http://www.gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/)

[Utilisez les jetons ACS Azure tooissue](http://mingfeiy.com/acs-with-key-services).

### <a name="some-considerations-apply"></a>Certaines considérations s’appliquent :
* Création de votre compte AMS un **par défaut** point de terminaison de diffusion en continu est ajoutée tooyour compte Bonjour **arrêté** état. toostart votre contenu et profitez de l’empaquetage dynamique et chiffrement dynamique, votre point de terminaison de diffusion en continu de diffusion en continu a toobe Bonjour **en cours d’exécution** état. 
* Votre ressource doit contenir un ensemble de MP4 à débit adaptatif ou des fichiers Smooth Streaming à débit adaptatif. Pour plus d'informations, consultez [Encoder une ressource](media-services-encode-asset.md).
* Téléchargez et codez vos ressources à l'aide de l'option **AssetCreationOptions.StorageEncrypted** .
* Si vous envisagez de toohave plusieurs clés de contenu qui nécessitent hello même configuration de la stratégie, il est fortement recommandé de toocreate une seule stratégie d’autorisation et la réutiliser avec plusieurs clés de contenu.
* Hello service de fourniture de clé met en cache ContentKeyAuthorizationPolicy et les objets associés (options de stratégie et les restrictions) pendant 15 minutes.  Si vous créez une stratégie ContentKeyAuthorizationPolicy et spécifiez toouse une restriction « Token », puis testez, puis mettre à jour de stratégie de hello trop « ouvrir » restriction, il prendra environ 15 minutes avant hello commutateurs toohello « Ouvert » version de stratégie de la stratégie de hello.
* Si vous ajoutez ou mettez à jour la stratégie de remise de votre ressource, vous devez supprimer le localisateur existant (le cas échéant) et en créer un nouveau.
* Actuellement, vous ne pouvez pas chiffrer les téléchargements progressifs.

## <a name="aes-128-dynamic-encryption"></a>Chiffrement dynamique AES-128.
### <a name="open-restriction"></a>Restriction ouverte
Restriction Open signifie hello système fournit des tooanyone clé hello qui fait la demande. Cette restriction peut être utile à des fins de test.

Hello, l’exemple suivant crée une stratégie d’autorisation ouverte et il ajoute la clé de contenu toohello.

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


### <a name="token-restriction"></a>Restriction par jeton
Cette section décrit comment toocreate un contenu de stratégie d’autorisation de clé et l’associer à la clé de contenu hello. stratégie d’autorisation de Hello décrit les spécifications d’autorisation doivent être rempli toodetermine si utilisateur de hello est clé de hello tooreceive autorisés (par exemple, liste de « clé de vérification » hello contenir la clé de hello ce jeton hello a été signé avec).

option de restriction token tooconfigure hello, vous devez toouse XML exigences d’autorisation du jeton toodescribe hello. configuration de restriction token Hello XML doit être conforme à toohello suivant le schéma XML.

#### <a id="schema"></a>Schéma de restriction par jeton
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

Lors de la configuration hello **jeton** stratégie, vous devez spécifier hello principal ** vérification clé **, **émetteur** et **public** paramètres. Hello ** clé de vérification principale ** contient clé hello hello jeton a été signé avec, **émetteur** est service de jeton sécurisé hello ce jeton hello de problèmes. Hello **public** (parfois appelé **étendue**) décrit l’intention de hello de jeton de hello ou ressource de hello jeton de hello autorise l’accès à. Hello service de distribution de clés de Media Services valide que ces valeurs dans le jeton de hello correspondent aux valeurs hello modèle de hello. 

Lorsque vous utilisez **Media Services SDK pour .NET**, vous pouvez utiliser hello **TokenRestrictionTemplate** jeton de restriction de classe toogenerate hello.
Bonjour à l’exemple suivant crée une stratégie d’autorisation avec une restriction token. Dans cet exemple, les clients hello aurait toopresent un jeton qui contient : clé de signature (VerificationKey), un émetteur de jeton et les revendications nécessaires.

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

#### <a id="test"></a>Jeton de test
tooget un jeton de test basé sur la restriction de type hello token qui a été utilisée pour la stratégie d’autorisation de clé de hello, hello suivant.

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


## <a name="playready-dynamic-encryption"></a>Chiffrement dynamique PlayReady
Media Services vous permet de droits de hello tooconfigure et les restrictions que vous souhaitez pour hello PlayReady DRM runtime tooenforce lorsqu’un utilisateur essaye tooplay précédent du contenu protégé. 

Lorsque vous protégez votre contenu avec PlayReady, un des éléments de hello vous devez toospecify dans votre stratégie d’autorisation est une chaîne XML qui définit hello [modèle de licence PlayReady](media-services-playready-license-template-overview.md). Dans Media Services SDK pour .NET, hello **PlayReadyLicenseResponseTemplate** et **PlayReadyLicenseTemplate** classes vous permettent de définir le modèle de licence PlayReady de hello.

[Cette rubrique](media-services-protect-with-drm.md) montre comment tooencrypt votre contenu avec **PlayReady** et **Widevine**.

### <a name="open-restriction"></a>Restriction ouverte
Restriction Open signifie hello système fournit des tooanyone clé hello qui fait la demande. Cette restriction peut être utile à des fins de test.

Hello, l’exemple suivant crée une stratégie d’autorisation ouverte et il ajoute la clé de contenu toohello.

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

### <a name="token-restriction"></a>Restriction par jeton
option de restriction token tooconfigure hello, vous devez toouse XML exigences d’autorisation du jeton toodescribe hello. configuration de restriction token Hello XML doit être conforme à XSD toohello illustré [cela](#schema) section.

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


tooget un jeton de test basé sur la restriction de type hello token qui a été utilisée pour voir de stratégie d’autorisation de clé hello [cela](#test) section. 

## <a id="types"></a>Types utilisés durant la définition de ContentKeyAuthorizationPolicy
### <a id="ContentKeyRestrictionType"></a>ContentKeyRestrictionType
    public enum ContentKeyRestrictionType
    {
        Open = 0,
        TokenRestricted = 1,
        IPRestricted = 2,
    }

### <a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType
    public enum ContentKeyDeliveryType
    {
      None = 0,
      PlayReadyLicense = 1,
      BaselineHttp = 2,
      Widevine = 3
    }

### <a id="TokenType"></a>TokenType
    public enum TokenType
    {
        Undefined = 0,
        SWT = 1,
        JWT = 2,
    }



## <a name="media-services-learning-paths"></a>Parcours d’apprentissage de Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-step"></a>Étape suivante
Maintenant que vous avez configuré la stratégie d’autorisation de clé de contenu, accédez à toohello [la stratégie de livraison des actifs tooconfigure](media-services-dotnet-configure-asset-delivery-policy.md) rubrique.

