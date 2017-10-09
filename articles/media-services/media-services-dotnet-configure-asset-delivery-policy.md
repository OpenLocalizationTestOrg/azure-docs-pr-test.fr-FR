---
title: "stratégies de remise aaaConfigure actif avec le Kit de développement .NET | Documents Microsoft"
description: "Cette rubrique montre comment les stratégies tooconfigure asset différents remise avec Azure Media Services .NET SDK."
services: media-services
documentationcenter: 
author: Mingfeiy
manager: cfowler
editor: 
ms.assetid: 3ec46f58-6cbb-4d49-bac6-1fd01a5a456b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/13/2017
ms.author: juliako;mingfeiy
ms.openlocfilehash: a6f2644d639cd36d4cdc269b6f01fd4acdf7160b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-asset-delivery-policies-with-net-sdk"></a>Configuration de stratégies de remise de ressources à l’aide du Kit de développement logiciel (SDK) .NET
[!INCLUDE [media-services-selector-asset-delivery-policy](../../includes/media-services-selector-asset-delivery-policy.md)]

## <a name="overview"></a>Vue d'ensemble
Si vous envisagez toodelivery chiffré actifs, une des hello étapes Bonjour Media Services de contenu de flux de travail de remise consiste à configurer des stratégies de remise pour les ressources. stratégie de livraison des actifs Hello indique comment vous souhaitez pour votre toobe asset remis à Media Services : dans le protocole de diffusion en continu doit votre élément multimédia dynamiquement packagé (par exemple, MPEG DASH, HLS, Smooth Streaming ou tous), vous souhaitez toodynamically ou non chiffrer votre élément multimédia et comment (enveloppe ou chiffrement commun).

Cette rubrique explique pourquoi et comment toocreate et configurer des stratégies de remise d’élément multimédia.

>[!NOTE]
>Création de votre compte AMS un **par défaut** point de terminaison de diffusion en continu est ajoutée tooyour compte Bonjour **arrêté** état. toostart de diffusion en continu de votre contenu et profitez de l’empaquetage dynamique et chiffrement dynamique, hello de point de terminaison de diffusion en continu à partir de laquelle vous souhaitez que le contenu toostream a toobe Bonjour **en cours d’exécution** état. 
>
>En outre, toobe toouse en mesure de mise en package dynamique et le chiffrement dynamique votre élément multimédia doit contenir un ensemble de fichiers à débit adaptatif MP4s ou des fichiers de diffusion en continu lisse à débit adaptatif.


Vous pouvez appliquer différentes stratégies toohello même actif. Par exemple, vous pouvez appliquer PlayReady chiffrement tooSmooth diffusion en continu et l’enveloppe AES chiffrement tooMPEG DASH et HLS. Tous les protocoles qui ne sont pas définis dans une stratégie de remise (par exemple, vous ajoutez une stratégie unique qui spécifie seulement le HLS en tant que protocole de hello) sera bloquée à partir de la diffusion en continu. Hello exception toothis est si vous ne disposez d’aucune stratégie de remise actif du tout défini. Ensuite, tous les protocoles seront autorisés en hello clair.

Si vous voulez toodeliver un élément multimédia chiffré de stockage, vous devez configurer la stratégie de remise de l’élément multimédia hello. Avant que votre élément multimédia peut être transmis en continu, hello de diffusion en continu flux et chiffrement de stockage de serveur supprime hello votre contenu à l’aide de hello spécifié de stratégie de remise. Par exemple, toodeliver votre élément multimédia chiffré avec la clé de chiffrement d’enveloppe Standard (AES), définissez le type de stratégie hello trop**DynamicEnvelopeEncryption**. tooremove le chiffrement de stockage et les actifs de hello flux Bonjour claires, le type de stratégie hello défini trop**NoDynamicEncryption**. Exemples qui montrent comment tooconfigure suivent ces types de stratégie.

Selon la façon dont vous configurez la stratégie de livraison des actifs hello vous serait sera en mesure de toodynamically package, dynamiquement chiffrer et diffuser en continu hello suite de protocoles de diffusion en continu : flux de diffusion en continu lisse, HLS et MPEG DASH.

Hello liste suivante présente les formats hello que vous utilisez toostream Smooth, HLS et DASH.

Smooth Streaming :

{nom du point de terminaison de diffusion en continu-nom du compte media services}.streaming.mediaservices.windows.net/{ID_de_localisateur}/{nom_de_fichier}.ISM/Manifest

HLS :

{nom du point de terminaison de diffusion en continu-nom du compte media services}.streaming.mediaservices.windows.net/{ID_de_localisateur}/{nom_de_fichier}.ISM/Manifest(format=m3u8-aapl)

MPEG DASH

{nom du point de terminaison de diffusion en continu-nom du compte media services}.streaming.mediaservices.windows.net/{ID_de_localisateur}/{nom_de_fichier}.ISM/Manifest(format=mpd-time-csf)


## <a name="considerations"></a>Considérations
* Vous ne pouvez pas supprimer une stratégie AssetDeliveryPolicy associée à un élément multimédia alors qu’un localisateur (de diffusion en continuer) OnDemand existe pour cet élément. stratégie de hello tooremove à partir de l’élément multimédia de hello il est recommandé de Hello avant de supprimer la stratégie de hello.
* Il est impossible de créer un localisateur de diffusion en continu sur un élément multimédia chiffré de stockage quand aucune stratégie de distribution d’éléments multimédias n’est définie.  Si hello actif n’est pas chiffré de stockage, système de hello sera vous permettent de créer un élément multimédia hello de recherche et de flux Bonjour effacer sans une stratégie de livraison des actifs.
* Vous pouvez avoir plusieurs stratégies de remise actif associés à un seul élément multimédia, mais vous ne pouvez spécifier qu’une façon toohandle un AssetDeliveryProtocol donné.  Ce qui signifie que si vous essayez de toolink deux stratégies de remise qui spécifient le protocole AssetDeliveryProtocol.SmoothStreaming hello qui entraîne une erreur car le système de hello ne sait pas celui que vous souhaitez tooapply lorsqu’un client effectue une demande de diffusion en continu lisse.
* Si vous avez un élément multimédia avec un localisateur de diffusion en continu, vous ne peut pas lier un nouveau composant toohello de stratégie (vous pouvez supprimer le lien d’une stratégie existante à partir de l’élément multimédia de hello, ou mettre à jour une stratégie de remise associée hello actif).  Vous tout d’abord avez localisateur de diffusion en continu tooremove hello, ajustez les stratégies de hello, puis recréez hello localisateur de diffusion en continu.  Vous pouvez utiliser hello locatorId même lorsque vous recréez hello de diffusion en continu de la recherche, mais vous devez vous assurer que causer des problèmes pour les clients, car le contenu peut être mis en cache à l’origine de hello ou un CDN en aval.

## <a name="clear-asset-delivery-policy"></a>Stratégie de remise de ressources

suivant de Hello **ConfigureClearAssetDeliveryPolicy** méthode spécifie toonot appliquer le chiffrement dynamique et de protocoles de flux de données toodeliver hello dans un des hello suivant : protocoles MPEG DASH, HLS et Smooth Streaming. Vous pourriez tooapply des ressources de stockage chiffrée cette tooyour stratégie.

Pour plus d’informations sur les valeurs que vous pouvez spécifier lors de la création d’un AssetDeliveryPolicy, consultez hello [Types utilisés lors de la définition AssetDeliveryPolicy](#types) section.

    static public void ConfigureClearAssetDeliveryPolicy(IAsset asset)
    {
        IAssetDeliveryPolicy policy =
        _context.AssetDeliveryPolicies.Create("Clear Policy",
        AssetDeliveryPolicyType.NoDynamicEncryption,
        AssetDeliveryProtocol.HLS | AssetDeliveryProtocol.SmoothStreaming | AssetDeliveryProtocol.Dash, null);
        
        asset.DeliveryPolicies.Add(policy);
    }

## <a name="dynamiccommonencryption-asset-delivery-policy"></a>Stratégie de remise de ressources DynamicCommonEncryption

suivant de Hello **CreateAssetDeliveryPolicy** méthode crée hello **AssetDeliveryPolicy** tooapply configuré qui est le chiffrement commun dynamique (**DynamicCommonEncryption**) tooa (les autres protocoles seront bloqués à partir de la diffusion en continu) de protocole de diffusion en continu lisse. méthode Hello accepte deux paramètres : **Asset** (hello toowhich asset tooapply hello remise stratégie) et **IContentKey** (clé de contenu hello Hello **CommonEncryption**de type, pour plus d’informations, consultez : [création d’une clé de contenu](media-services-dotnet-create-contentkey.md#common_contentkey)).

Pour plus d’informations sur les valeurs que vous pouvez spécifier lors de la création d’un AssetDeliveryPolicy, consultez hello [Types utilisés lors de la définition AssetDeliveryPolicy](#types) section.

    static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
    {
        Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.PlayReadyLicense);
        
        Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
                new Dictionary<AssetDeliveryPolicyConfigurationKey, string>
            {
                {AssetDeliveryPolicyConfigurationKey.PlayReadyLicenseAcquisitionUrl, acquisitionUrl.ToString()},
            };
    
            var assetDeliveryPolicy = _context.AssetDeliveryPolicies.Create(
                    "AssetDeliveryPolicy",
                AssetDeliveryPolicyType.DynamicCommonEncryption,
                AssetDeliveryProtocol.SmoothStreaming,
                assetDeliveryPolicyConfiguration);
    
            // Add AssetDelivery Policy toohello asset
            asset.DeliveryPolicies.Add(assetDeliveryPolicy);
    
            Console.WriteLine();
            Console.WriteLine("Adding Asset Delivery Policy: " +
                assetDeliveryPolicy.AssetDeliveryPolicyType);
     }

Azure Media Services vous permet également le chiffrement Widevine tooadd. Hello exemple suivant illustre PlayReady et Widevine ajouté toohello stratégie de livraison des actifs.

    static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
    {
        // Get hello PlayReady license service URL.
        Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.PlayReadyLicense);


        // GetKeyDeliveryUrl for Widevine attaches hello KID toohello URL.
        // For example: https://amsaccount1.keydelivery.mediaservices.windows.net/Widevine/?KID=268a6dcb-18c8-4648-8c95-f46429e4927c.  
        // hello WidevineBaseLicenseAcquisitionUrl (used below) also tells Dynamaic Encryption 
        // tooappend /? KID =< keyId > toohello end of hello url when creating hello manifest.
        // As a result Widevine license acquisition URL will have KID appended twice, 
        // so we need tooremove hello KID that in hello URL when we call GetKeyDeliveryUrl.

        Uri widevineUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.Widevine);
        UriBuilder uriBuilder = new UriBuilder(widevineUrl);
        uriBuilder.Query = String.Empty;
        widevineUrl = uriBuilder.Uri;

        Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
            new Dictionary<AssetDeliveryPolicyConfigurationKey, string>
        {
            {AssetDeliveryPolicyConfigurationKey.PlayReadyLicenseAcquisitionUrl, acquisitionUrl.ToString()},
            {AssetDeliveryPolicyConfigurationKey.WidevineLicenseAcquisitionUrl, widevineUrl.ToString()}

        };

        var assetDeliveryPolicy = _context.AssetDeliveryPolicies.Create(
                "AssetDeliveryPolicy",
            AssetDeliveryPolicyType.DynamicCommonEncryption,
            AssetDeliveryProtocol.Dash,
            assetDeliveryPolicyConfiguration);


        // Add AssetDelivery Policy toohello asset
        asset.DeliveryPolicies.Add(assetDeliveryPolicy);

    }

> [!NOTE]
> Lors du chiffrement avec Widevine, vous serez uniquement en mesure de toodeliver à l’aide de tiret. Assurez-vous que toospecify tiret dans le protocole de livraison hello actif.
> 
> 

## <a name="dynamicenvelopeencryption-asset-delivery-policy"></a>Stratégie de remise de ressources DynamicEnvelopeEncryption
suivant de Hello **CreateAssetDeliveryPolicy** méthode crée hello **AssetDeliveryPolicy** tooapply configuré qui est le chiffrement dynamique enveloppe (**DynamicEnvelopeEncryption** ) protocoles de diffusion en continu, HLS et DASH tooSmooth (si vous décidez de toonot spécifier certains protocoles, ils seront bloqués à partir de la diffusion en continu). méthode Hello accepte deux paramètres : **Asset** (hello toowhich asset tooapply hello remise stratégie) et **IContentKey** (clé de contenu hello Hello **EnvelopeEncryption**de type, pour plus d’informations, consultez : [création d’une clé de contenu](media-services-dotnet-create-contentkey.md#envelope_contentkey)).

Pour plus d’informations sur les valeurs que vous pouvez spécifier lors de la création d’un AssetDeliveryPolicy, consultez hello [Types utilisés lors de la définition AssetDeliveryPolicy](#types) section.   

    private static void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
    {

        //  Get hello Key Delivery Base Url by removing hello Query parameter.  hello Dynamic Encryption service will
        //  automatically add hello correct key identifier toohello url when it generates hello Envelope encrypted content
        //  manifest.  Omitting hello IV will also cause hello Dynamice Encryption service toogenerate a deterministic
        //  IV for hello content automatically.  By using hello EnvelopeBaseKeyAcquisitionUrl and omitting hello IV, this
        //  allows hello AssetDelivery policy toobe reused by more than one asset.
        //
        Uri keyAcquisitionUri = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.BaselineHttp);
        UriBuilder uriBuilder = new UriBuilder(keyAcquisitionUri);
        uriBuilder.Query = String.Empty;
        keyAcquisitionUri = uriBuilder.Uri;

        // hello following policy configuration specifies: 
        //   key url that will have KID=<Guid> appended toohello envelope and
        //   hello Initialization Vector (IV) toouse for hello envelope encryption.
        Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
            new Dictionary<AssetDeliveryPolicyConfigurationKey, string> 
        {
            {AssetDeliveryPolicyConfigurationKey.EnvelopeBaseKeyAcquisitionUrl, keyAcquisitionUri.ToString()},
        };

        IAssetDeliveryPolicy assetDeliveryPolicy =
            _context.AssetDeliveryPolicies.Create(
                        "AssetDeliveryPolicy",
                        AssetDeliveryPolicyType.DynamicEnvelopeEncryption,
                        AssetDeliveryProtocol.SmoothStreaming | AssetDeliveryProtocol.HLS | AssetDeliveryProtocol.Dash,
                        assetDeliveryPolicyConfiguration);

        // Add AssetDelivery Policy toohello asset
        asset.DeliveryPolicies.Add(assetDeliveryPolicy);

        Console.WriteLine();
        Console.WriteLine("Adding Asset Delivery Policy: " + assetDeliveryPolicy.AssetDeliveryPolicyType);
    }


## <a id="types"></a>Types utilisés durant la définition de AssetDeliveryPolicy

### <a id="AssetDeliveryProtocol"></a>AssetDeliveryProtocol

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

### <a id="AssetDeliveryPolicyType"></a>AssetDeliveryPolicyType

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

### <a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType

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

### <a id="AssetDeliveryPolicyConfigurationKey"></a>AssetDeliveryPolicyConfigurationKey

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

