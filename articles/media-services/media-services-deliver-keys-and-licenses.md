---
title: "Utilisation d’Azure Media Services pour fournir des licences DRM ou des clés AES"
description: "Cet article décrit comment vous pouvez utiliser Azure Media Services (AMS) pour fournir des licences PlayReady et/ou Widevine et des clés AES, et comment exécuter les autres opérations (encodage, chiffrement, diffusion en continu) à l’aide de vos serveurs locaux."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 8546c2c1-430b-4254-a88d-4436a83f9192
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: 263a381dc72105eea60ad9b39434599ff04a4531
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-media-services-to-deliver-drm-licenses-or-aes-keys"></a><span data-ttu-id="deaed-103">Utilisation d’Azure Media Services pour fournir des licences DRM ou des clés AES</span><span class="sxs-lookup"><span data-stu-id="deaed-103">Use Azure Media Services to deliver DRM licenses or AES keys</span></span>
<span data-ttu-id="deaed-104">Azure Media Services (AMS) vous permet de recevoir, d’encoder, d’ajouter une protection de contenu et de diffuser votre contenu (voir [cet](media-services-protect-with-drm.md) pour plus de détails).</span><span class="sxs-lookup"><span data-stu-id="deaed-104">Azure Media Services (AMS) enables you to ingest, encode, add content protection, and stream your content (see [this](media-services-protect-with-drm.md) article for details).</span></span> <span data-ttu-id="deaed-105">Toutefois, il existe des clients qui souhaitent seulement utiliser AMS pour fournir des licences et/ou des clés et faire de l’encodage, du chiffrement et de la diffusion en continu à l’aide de leurs serveurs locaux.</span><span class="sxs-lookup"><span data-stu-id="deaed-105">However, there are customers who only want to use AMS to deliver licenses and/or keys and do encoding, encrypting and streaming using their on-premises servers.</span></span> <span data-ttu-id="deaed-106">Cet article décrit comment vous pouvez utiliser AMS pour fournir des licences PlayReady et/ou Widevine et exécuter les autres opérations avec vos serveurs locaux.</span><span class="sxs-lookup"><span data-stu-id="deaed-106">This article describes how you can use AMS to deliver PlayReady and/or Widevine licenses but do the rest with your on-premises servers.</span></span> 

## <a name="overview"></a><span data-ttu-id="deaed-107">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="deaed-107">Overview</span></span>
<span data-ttu-id="deaed-108">Media Services fournit un service de remise de licences DRM PlayReady et Widevine, et de clés AES-128.</span><span class="sxs-lookup"><span data-stu-id="deaed-108">Media Services provides a service for delivering PlayReady and Widevine DRM licenses and AES-128 keys.</span></span> <span data-ttu-id="deaed-109">Media Services fournit également des API qui vous permettent de configurer les droits et les restrictions que vous souhaitez pour le runtime DRM, qui s’appliquent lorsqu’un utilisateur lit un contenu DRM protégé.</span><span class="sxs-lookup"><span data-stu-id="deaed-109">Media Services also provides APIs that let you configure the rights and restrictions that you want for the DRM runtime to enforce when a user plays back the DRM protected content.</span></span> <span data-ttu-id="deaed-110">Lorsqu’un utilisateur demande le contenu protégé, l’application de lecteur demande une licence du service de licence AMS.</span><span class="sxs-lookup"><span data-stu-id="deaed-110">When a user requests the protected content, the player application will request a license from the AMS license service.</span></span> <span data-ttu-id="deaed-111">Le service de licence AMS émet la licence pour le lecteur (s’il est autorisé).</span><span class="sxs-lookup"><span data-stu-id="deaed-111">The AMS license service will issue the license to the player (if it is authorized).</span></span> <span data-ttu-id="deaed-112">Les licences PlayReady et Widevine contiennent la clé de déchiffrement qui peut être utilisée par le lecteur client pour déchiffrer et diffuser le contenu.</span><span class="sxs-lookup"><span data-stu-id="deaed-112">The PlayReady and Widevine licenses contain the decryption key that can be used by the client player to decrypt and stream the content.</span></span>

<span data-ttu-id="deaed-113">Media Services prend en charge plusieurs méthodes d’autorisation des utilisateurs effectuant des demandes de clé ou de licence.</span><span class="sxs-lookup"><span data-stu-id="deaed-113">Media Services supports multiple ways of authorizing users who make license or key requests.</span></span> <span data-ttu-id="deaed-114">Vous configurez la stratégie d’autorisation des clés de contenu et celle-ci peut comporter une ou plusieurs restrictions : ouverte ou restriction à jeton.</span><span class="sxs-lookup"><span data-stu-id="deaed-114">You configure the content key's authorization policy and the policy could have one or more restrictions: open or token restriction.</span></span> <span data-ttu-id="deaed-115">La stratégie de restriction à jeton doit être accompagnée d’un jeton émis par un service de jeton sécurisé (STS).</span><span class="sxs-lookup"><span data-stu-id="deaed-115">The token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="deaed-116">Media Services prend en charge les jetons aux formats SWT (Simple Web Tokens) et JWT (JSON Web Token).</span><span class="sxs-lookup"><span data-stu-id="deaed-116">Media Services supports tokens in the Simple Web Tokens (SWT) format and JSON Web Token (JWT) format.</span></span>

<span data-ttu-id="deaed-117">Le diagramme suivant montre les principales étapes à suivre pour utiliser AMS pour fournir des licences PlayReady et/ou Widevine, et exécuter les autres opérations avec vos serveurs locaux.</span><span class="sxs-lookup"><span data-stu-id="deaed-117">The following diagram shows the main steps you need to take to use AMS to deliver PlayReady and/or Widevine licenses but do the rest with your on-premises servers.</span></span>

![Protéger avec PlayReady](./media/media-services-deliver-keys-and-licenses/media-services-diagram1.png)

## <a name="download-sample"></a><span data-ttu-id="deaed-119">Charger l’exemple</span><span class="sxs-lookup"><span data-stu-id="deaed-119">Download sample</span></span>
<span data-ttu-id="deaed-120">Vous pouvez télécharger l’exemple décrit dans cet article à partir d’ [ici](https://github.com/Azure/media-services-dotnet-deliver-drm-licenses).</span><span class="sxs-lookup"><span data-stu-id="deaed-120">You can download the sample described in this article from [here](https://github.com/Azure/media-services-dotnet-deliver-drm-licenses).</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="deaed-121">Créer et configurer un projet Visual Studio</span><span class="sxs-lookup"><span data-stu-id="deaed-121">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="deaed-122">Configurez votre environnement de développement et ajoutez des informations de connexion au fichier app.config selon la procédure décrite dans l’article [Développement Media Services avec .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="deaed-122">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 
2. <span data-ttu-id="deaed-123">Ajoutez les éléments suivants aux **appSettings** définis dans votre fichier app.config :</span><span class="sxs-lookup"><span data-stu-id="deaed-123">Add the following elements to **appSettings** defined in your app.config file:</span></span>

    <span data-ttu-id="deaed-124"><add key="Issuer" value="http://testacs.com"/> <add key="Audience" value="urn:test"/></span><span class="sxs-lookup"><span data-stu-id="deaed-124"><add key="Issuer" value="http://testacs.com"/> <add key="Audience" value="urn:test"/></span></span>

## <a name="net-code-example"></a><span data-ttu-id="deaed-125">Exemple de code .NET</span><span class="sxs-lookup"><span data-stu-id="deaed-125">.NET code example</span></span>

<span data-ttu-id="deaed-126">L’exemple de code suivant montre comment créer une clé de contenu courante et obtenir les URL d’acquisition de licence PlayReady ou Widevine.</span><span class="sxs-lookup"><span data-stu-id="deaed-126">The following code example shows how to create a common content key and get PlayReady or Widevine license acquisition URLs.</span></span> <span data-ttu-id="deaed-127">Vous devez obtenir les informations suivantes à partir d’AMS et configurer votre serveur local : **clé de contenu**, **ID de clé**, **URL d’acquisition de licence**.</span><span class="sxs-lookup"><span data-stu-id="deaed-127">You need to get the following pieces of information from AMS and configure your on-premises server: **content key**, **key id**, **license acquisition URL**.</span></span> <span data-ttu-id="deaed-128">Une fois votre serveur local configuré, vous pouvez diffuser à partir de votre propre serveur de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="deaed-128">Once you configure your on-premises server, you could stream from your own streaming server.</span></span> <span data-ttu-id="deaed-129">Étant donné que le flux chiffré pointe vers le serveur de licences AMS, votre lecteur demande une licence à AMS.</span><span class="sxs-lookup"><span data-stu-id="deaed-129">Since the encrypted stream points to AMS license server, your player will request a license from AMS.</span></span> <span data-ttu-id="deaed-130">Si vous choisissez l’authentification par jeton, le serveur de licences AMS validera le jeton que vous avez envoyé via HTTPS et (s’il est valide) fournira la licence à votre lecteur.</span><span class="sxs-lookup"><span data-stu-id="deaed-130">If you choose token authentication, the AMS license server will validate the token you sent through HTTPS and (if valid) will deliver the license back to your player.</span></span> <span data-ttu-id="deaed-131">(L’exemple de code montre seulement comment créer une clé de contenu courante et obtenir les URL d’acquisition de licence PlayReady ou Widevine.</span><span class="sxs-lookup"><span data-stu-id="deaed-131">(The code example only shows how to create a common content key and  get PlayReady or Widevine license acquisition URLs.</span></span> <span data-ttu-id="deaed-132">Si vous souhaitez fournir des clés AES-128, vous devez créer une clé de contenu d’enveloppe et obtenir une URL d’acquisition de clé ; [cet](media-services-protect-with-aes128.md) vous explique comment procéder).</span><span class="sxs-lookup"><span data-stu-id="deaed-132">If you want to delivery AES-128 keys, you need to create an envelope content key and get a key acquisition URL and [this](media-services-protect-with-aes128.md) article shows how to do it).</span></span>

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using Microsoft.WindowsAzure.MediaServices.Client.ContentKeyAuthorization;
    using Microsoft.WindowsAzure.MediaServices.Client.Widevine;
    using Newtonsoft.Json;

    namespace DeliverDRMLicenses
    {
        class Program
        {
            // Read values from the App.config file.
            private static readonly string _AADTenantDomain =
                ConfigurationManager.AppSettings["AADTenantDomain"];
            private static readonly string _RESTAPIEndpoint =
                ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

            private static readonly Uri _sampleIssuer =
                new Uri(ConfigurationManager.AppSettings["Issuer"]);
            private static readonly Uri _sampleAudience =
                new Uri(ConfigurationManager.AppSettings["Audience"]);

            // Field for service context.
            private static CloudMediaContext _context = null;

            static void Main(string[] args)
            {
                var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
                var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

                _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

                bool tokenRestriction = true;
                string tokenTemplateString = null;


                IContentKey key = CreateCommonTypeContentKey();

                // Print out the key ID and Key in base64 string format
                Console.WriteLine("Created key {0} with key value {1} ",
                    key.Id, System.Convert.ToBase64String(key.GetClearKeyValue()));

                Console.WriteLine("PlayReady License Key delivery URL: {0}",
                    key.GetKeyDeliveryUrl(ContentKeyDeliveryType.PlayReadyLicense));

                Console.WriteLine("Widevine License Key delivery URL: {0}",
                    key.GetKeyDeliveryUrl(ContentKeyDeliveryType.Widevine));

                if (tokenRestriction)
                    tokenTemplateString = AddTokenRestrictedAuthorizationPolicy(key);
                else
                    AddOpenAuthorizationPolicy(key);

                Console.WriteLine("Added authorization policy: {0}",
                    key.AuthorizationPolicyId);
                Console.WriteLine();
                Console.ReadLine();
            }

            static public void AddOpenAuthorizationPolicy(IContentKey contentKey)
            {

                // Create ContentKeyAuthorizationPolicy with Open restrictions 
                // and create authorization policy          

                List<ContentKeyAuthorizationPolicyRestriction> restrictions =
                    new List<ContentKeyAuthorizationPolicyRestriction>
                {
                        new ContentKeyAuthorizationPolicyRestriction
                        {
                            Name = "Open",
                            KeyRestrictionType = (int)ContentKeyRestrictionType.Open,
                            Requirements = null
                        }
                };

                // Configure PlayReady and Widevine license templates.
                string PlayReadyLicenseTemplate = ConfigurePlayReadyLicenseTemplate();

                string WidevineLicenseTemplate = ConfigureWidevineLicenseTemplate();

                IContentKeyAuthorizationPolicyOption PlayReadyPolicy =
                    _context.ContentKeyAuthorizationPolicyOptions.Create("",
                        ContentKeyDeliveryType.PlayReadyLicense,
                            restrictions, PlayReadyLicenseTemplate);

                IContentKeyAuthorizationPolicyOption WidevinePolicy =
                    _context.ContentKeyAuthorizationPolicyOptions.Create("",
                        ContentKeyDeliveryType.Widevine,
                        restrictions, WidevineLicenseTemplate);

                IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                            ContentKeyAuthorizationPolicies.
                            CreateAsync("Deliver Common Content Key with no restrictions").
                            Result;


                contentKeyAuthorizationPolicy.Options.Add(PlayReadyPolicy);
                contentKeyAuthorizationPolicy.Options.Add(WidevinePolicy);
                // Associate the content key authorization policy with the content key.
                contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
                contentKey = contentKey.UpdateAsync().Result;
            }

            public static string AddTokenRestrictedAuthorizationPolicy(IContentKey contentKey)
            {
                string tokenTemplateString = GenerateTokenRequirements();

                List<ContentKeyAuthorizationPolicyRestriction> restrictions =
                    new List<ContentKeyAuthorizationPolicyRestriction>
                {
                        new ContentKeyAuthorizationPolicyRestriction
                        {
                            Name = "Token Authorization Policy",
                            KeyRestrictionType = (int)ContentKeyRestrictionType.TokenRestricted,
                            Requirements = tokenTemplateString,
                        }
                };

                // Configure PlayReady and Widevine license templates.
                string PlayReadyLicenseTemplate = ConfigurePlayReadyLicenseTemplate();

                string WidevineLicenseTemplate = ConfigureWidevineLicenseTemplate();

                IContentKeyAuthorizationPolicyOption PlayReadyPolicy =
                    _context.ContentKeyAuthorizationPolicyOptions.Create("Token option",
                        ContentKeyDeliveryType.PlayReadyLicense,
                            restrictions, PlayReadyLicenseTemplate);

                IContentKeyAuthorizationPolicyOption WidevinePolicy =
                    _context.ContentKeyAuthorizationPolicyOptions.Create("Token option",
                        ContentKeyDeliveryType.Widevine,
                            restrictions, WidevineLicenseTemplate);

                IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                            ContentKeyAuthorizationPolicies.
                            CreateAsync("Deliver Common Content Key with token restrictions").
                            Result;

                contentKeyAuthorizationPolicy.Options.Add(PlayReadyPolicy);
                contentKeyAuthorizationPolicy.Options.Add(WidevinePolicy);

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

                //The PlayReadyLicenseResponseTemplate class represents the template 
                //for the response sent back to the end user. 
                //It contains a field for a custom data string between the license server 
                //and the application (may be useful for custom app logic) 
                //as well as a list of one or more license templates.

                PlayReadyLicenseResponseTemplate responseTemplate =
                    new PlayReadyLicenseResponseTemplate();

                // The PlayReadyLicenseTemplate class represents a license template 
                // for creating PlayReady licenses
                // to be returned to the end users. 
                // It contains the data on the content key in the license 
                // and any rights or restrictions to be 
                // enforced by the PlayReady DRM runtime when using the content key.
                PlayReadyLicenseTemplate licenseTemplate = new PlayReadyLicenseTemplate();

                // Configure whether the license is persistent 
                // (saved in persistent storage on the client) 
                // or non-persistent (only held in memory while the player is using the license).  
                licenseTemplate.LicenseType = PlayReadyLicenseType.Nonpersistent;

                // AllowTestDevices controls whether test devices can use the license or not.  
                // If true, the MinimumSecurityLevel property of the license
                // is set to 150.  If false (the default), 
                // the MinimumSecurityLevel property of the license is set to 2000.
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

                // IMPORTANT: These types of restrictions can be very powerful 
                // but can also affect the consumer experience. 
                // If the output protections are configured too restrictive, 
                // the content might be unplayable on some clients. 
                // For more information, see the PlayReady Compliance Rules document.

                // For example:
                //licenseTemplate.PlayRight.AgcAndColorStripeRestriction = new AgcAndColorStripeRestriction(1);

                responseTemplate.LicenseTemplates.Add(licenseTemplate);

                return MediaServicesLicenseTemplateSerializer.Serialize(responseTemplate);
            }


            private static string ConfigureWidevineLicenseTemplate()
            {
                var template = new WidevineMessage
                {
                    allowed_track_types = AllowedTrackTypes.SD_HD,
                    content_key_specs = new[]
                    {
                            new ContentKeySpecs
                            {
                                required_output_protection =
                                    new RequiredOutputProtection { hdcp = Hdcp.HDCP_NONE},
                                security_level = 1,
                                track_type = "SD"
                            }
                        },
                    policy_overrides = new
                    {
                        can_play = true,
                        can_persist = true,
                        can_renew = false
                    }
                };

                string configuration = JsonConvert.SerializeObject(template);
                return configuration;
            }


            static public IContentKey CreateCommonTypeContentKey()
            {
                // Create envelope encryption content key
                Guid keyId = Guid.NewGuid();
                byte[] contentKey = GetRandomBuffer(16);

                IContentKey key = _context.ContentKeys.Create(
                                        keyId,
                                        contentKey,
                                        "ContentKey",
                                        ContentKeyType.CommonEncryption);

                return key;
            }

            static private byte[] GetRandomBuffer(int length)
            {
                var returnValue = new byte[length];

                using (var rng =
                    new System.Security.Cryptography.RNGCryptoServiceProvider())
                {
                    rng.GetBytes(returnValue);
                }

                return returnValue;
            }
        }
    }

## <a name="media-services-learning-paths"></a><span data-ttu-id="deaed-133">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="deaed-133">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="deaed-134">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="deaed-134">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="deaed-135">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="deaed-135">See also</span></span>
[<span data-ttu-id="deaed-136">Utilisation du chiffrement commun dynamique PlayReady et/ou Widevine</span><span class="sxs-lookup"><span data-stu-id="deaed-136">Using PlayReady and/or Widevine Dynamic Common Encryption</span></span>](media-services-protect-with-drm.md)

[<span data-ttu-id="deaed-137">Utilisation du chiffrement dynamique AES-128 et du service de distribution des clés</span><span class="sxs-lookup"><span data-stu-id="deaed-137">Using AES-128 Dynamic Encryption and Key Delivery Service</span></span>](media-services-protect-with-aes128.md)

[<span data-ttu-id="deaed-138">Utilisation de partenaires pour fournir des licences Widevine à Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="deaed-138">Using partners to deliver Widevine licenses to Azure Media Services</span></span>](media-services-licenses-partner-integration.md)

