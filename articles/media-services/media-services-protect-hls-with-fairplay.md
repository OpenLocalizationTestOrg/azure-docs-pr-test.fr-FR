---
title: aaaProtect de contenu HLS avec Microsoft PlayReady ou Apple FairPlay - Azure | Documents Microsoft
description: "Cette rubrique donne une vue d’ensemble et montre comment toouse Azure Media Services toodynamically chiffrer votre contenu HTTP Live Streaming (HLS) avec Apple FairPlay. Il montre également comment la remise service toodeliver tooclients de licences FairPlay de licence toouse hello Media Services."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 7c3b35d9-1269-4c83-8c91-490ae65b0817
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: 91ca451e3e7bf0da1d74dac4c99180f08f39e4ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="protect-your-hls-content-with-apple-fairplay-or-microsoft-playready"></a>Protéger votre contenu HLS avec Apple FairPlay ou Microsoft PlayReady
Azure permet de Media Services vous toodynamically chiffrer votre contenu HTTP Live Streaming (HLS) à l’aide de hello suivant formats :  

* **Clé en clair de l’enveloppe AES-128**

    Hello segment entier est chiffré à l’aide de hello **AES-128 CBC** mode. déchiffrement Hello du flux de hello est pris en charge par iOS et le lecteur du système d’exploitation X en mode natif. Pour plus d’informations, consultez la page [Utilisation du chiffrement dynamique AES-128 et du service de distribution des clés](media-services-protect-with-aes128.md).
* **Apple FairPlay**

    Hello individuel vidéo et audio échantillons sont chiffrées à l’aide de hello **AES-128 CBC** mode. **Diffusion en continu de FairPlay** (i/s) est intégré dans les systèmes d’exploitation pour appareils hello, avec prise en charge native sur iOS et Apple TV. Safari sur OS X permet i/s à l’aide de prise en charge d’interface hello chiffrés Media Extensions (EME).
* **Microsoft PlayReady**

Hello image suivante montre hello **HLS + FairPlay ou PlayReady chiffrement dynamique** flux de travail.

![Diagramme de flux de travail de chiffrement dynamique](./media/media-services-content-protection-overview/media-services-content-protection-with-fairplay.png)

Cette rubrique montre comment toouse Media Services toodynamically chiffrer votre contenu HLS avec FairPlay d’Apple. Il montre également comment la remise service toodeliver tooclients de licences FairPlay de licence toouse hello Media Services.

> [!NOTE]
> Si vous voulez également tooencrypt votre contenu HLS avec PlayReady, vous devez toocreate une clé de contenu commune et l’associez à votre élément multimédia. Vous devez également stratégie d’autorisation de tooconfigure hello de clé du contenu, comme décrit dans [du chiffrement commun dynamique à l’aide de PlayReady](media-services-protect-with-drm.md).
>
>

## <a name="requirements-and-considerations"></a>Conditions requises et éléments à prendre en compte

Hello Voici requis lors de l’utilisation de toodeliver Media Services que HLS chiffré avec FairPlay et toodeliver FairPlay licences :

  * Un compte Azure. Pour plus d’informations, consultez la page [Version d’évaluation gratuite d’Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).
  * Un compte Media Services. toocreate, consultez [créer un compte Azure Media Services à l’aide de hello Azure portal](media-services-portal-create-account.md).
  * S’inscrire au programme [Apple Developer Program](https://developer.apple.com/).
  * Apple requiert hello de hello propriétaire du contenu tooobtain [package de déploiement](https://developer.apple.com/contact/fps/). L’état que vous déjà implémenté de Module de sécurité de clé (KSM) avec Media Services et que vous demandez le package d’images par seconde final hello. Des instructions Bonjour i/s final toogenerate certification du package et obtenir hello clé de Secret d’Application (demandez). Vous utilisez ASK tooconfigure FairPlay.
  * Kit de développement logiciel (SDK) .NET Azure Media Services version **3.6.0** ou ultérieure.

Hello suivant d’éléments doit être définie sur le côté de distribution de clés de Media Services :

  * **Application Cert (AC)**: il s’agit d’un fichier .pfx qui contient la clé privée de hello. Vous devez créer ce fichier et le chiffrer avec un mot de passe.

       Lorsque vous configurez une stratégie de distribution de clés, vous devez fournir ce fichier .pfx hello et le mot de passe au format Base64.

      Hello suit décrire comment toogenerate un certificat .pfx du fichier pour FairPlay :

    1. Installez OpenSSL à partir de https://slproweb.com/products/Win32OpenSSL.html.

        Accédez toohello dossier certificat FairPlay de hello et d’autres fichiers fournies par Apple.
    2. Exécutez hello de commande suivante à partir de la ligne de commande hello. Cela convertit le fichier .pem tooa hello .cer fichier.

        "C:\OpenSSL-Win32\bin\openssl.exe" x509 -inform der -in fairplay.cer -out fairplay-out.pem
    3. Exécutez hello de commande suivante à partir de la ligne de commande hello. Cela convertit le fichier .pfx tooa hello .pem fichier avec une clé privée de hello. mot de passe Hello pour le fichier .pfx de hello est alors invité par OpenSSL.

        "C:\OpenSSL-Win32\bin\openssl.exe" pkcs12 -export -out fairplay-out.pfx -inkey privatekey.pem -in fairplay-out.pem -passin file:privatekey-pem-pass.txt
  * **Mot de passe de certificat de l’application**: mot de passe hello pour la création du fichier .pfx de hello.
  * **ID de mot de passe d’application Cert**: vous devez télécharger le mot de passe hello, toohow similaires, ils téléchargent d’autres clés de Media Services. Hello d’utilisation **ContentKeyType.FairPlayPfxPassword** hello de tooget de valeur enum ID de Media Services C’est ce qu’ils doivent toouse au sein de l’option de stratégie de distribution de clés hello.
  * **iv** : valeur aléatoire de 16 octets. Il doit correspondre au hello du vecteur d’initialisation dans la stratégie de remise hello actif. Vous générez hello iv et le placer dans deux emplacements : stratégie de livraison des actifs hello et option de stratégie de distribution de clés hello.
  * **Demandez à**: cette clé est reçue lors de la génération de la certification de hello à l’aide du portail des développeurs Apple hello. Chaque équipe de développement recevra une ASK unique. Enregistrer une copie de hello ASK et stockez-le dans un endroit sûr. Vous aurez besoin ultérieurement tooconfigure ASK en tant que FairPlayAsk tooMedia Services.
  * **ASK ID (ID de clé ASK)** : cet ID est obtenu lorsque vous chargez la clé ASK dans Media Services. Vous devez télécharger poser à l’aide de hello **ContentKeyType.FairPlayAsk** valeur enum. En tant que résultat de hello, hello Media Services ID est retournée, et c’est celui qui doit être utilisé lors de la définition d’option de stratégie de distribution de clés hello.

Hello ce qui suit doit être défini par hello côté client de fréquence d’images :

  * **Application Cert (AC)**: il s’agit d’un fichier.cer/.der contenant la clé publique hello, système d’exploitation hello utilise tooencrypt certains charge. Media Services doit tooknow concernant car il est requis par le lecteur hello. service de distribution de clés Hello déchiffre à l’aide de la clé privée correspondante de hello.

tooplay un flux chiffré FairPlay, obtenez un véritable demander d’abord, puis générer un certificat réel. Ce processus crée les trois composants suivants :

  * Fichier .der
  * Fichier .pfx
  * mot de passe pour hello .pfx

Hello clients suivants prennent en charge HLS avec **AES-128 CBC** chiffrement : Safari sur OS X, Apple TV, iOS.

## <a name="configure-fairplay-dynamic-encryption-and-license-delivery-services"></a>Configurer le chiffrement dynamique FairPlay et des services de remise de licences
Hello Voici les étapes générales pour la protection de vos éléments multimédias avec FairPlay à l’aide du service de remise de licences de Media Services hello et également à l’aide du chiffrement dynamique.

1. Créer un élément multimédia et télécharger des fichiers dans l’élément multimédia de hello.
2. Encoder asset hello contenant hello fichier toohello adaptive bitrate que MP4 set.
3. Créer une clé de contenu et l’associer à asset de hello encodé.  
4. Configurez la stratégie d’autorisation de la clé de contenu hello. Spécifiez hello qui suit :

   * méthode de remise Hello (dans ce cas, FairPlay).
   * la configuration des options de stratégie FairPlay. Pour plus d’informations sur la façon de tooconfigure FairPlay, consultez hello **ConfigureFairPlayPolicyOptions()** méthode dans l’exemple hello ci-dessous.

     > [!NOTE]
     > En règle générale, vous souhaiteriez tooconfigure FairPlay stratégie n'options qu’une seule fois, car vous aurez qu’un ensemble de certification et un demandez.
     >
     >
   * Les restrictions (d’ouverture ou jeton).
   * Informations spécifiques toohello clé type de remise qui définit comment la clé de hello est remis toohello client.
5. Configurer la stratégie de remise hello actif. configuration de stratégie de livraison Hello inclut :

   * protocole de livraison Hello (TLS).
   * type Hello du chiffrement dynamique (chiffrement CBC commun).
   * URL d’acquisition de licence Hello.

     > [!NOTE]
     > Si vous voulez toodeliver un flux qui est chiffré avec FairPlay et un autre système de gestion des droits numériques (DRM), vous disposez des stratégies de remise distinct tooconfigure :
     >
     > * Un IAssetDeliveryPolicy tooconfigure dynamique diffusion adaptative en continu via HTTP (tiret) avec courantes chiffrement (CENC) (PlayReady + Widevine) et Smooth Streaming avec PlayReady
     > * Un autre IAssetDeliveryPolicy tooconfigure FairPlay pour TLS
     >
     >
6. Créer un tooget de localisateur OnDemand une URL de diffusion en continu.

## <a name="use-fairplay-key-delivery-by-player-apps"></a>Utiliser la remise de clé FairPlay des applications de lecteur
Vous pouvez développer des applications de lecteur à l’aide de hello, iOS SDK. tooplay en mesure de toobe FairPlay contenu, vous disposez de protocole d’échange de licence tooimplement hello. Ce protocole n’est pas spécifié par Apple. Il est de l’application tooeach la distribution de clés toosend demande. Hello service de distribution de clés de Media Services FairPlay attend hello SPC toocome comme un message encodé post www-form-url, Bonjour suivant du formulaire :

    spc=<Base64 encoded SPC>

> [!NOTE]
> Azure Media Player ne prend pas en charge la lecture de FairPlay prédéfinies hello. lecture de FairPlay tooget sur MAC OS X, obtenir le lecteur exemple hello de hello compte de développeur Apple.
>
>

## <a name="streaming-urls"></a>URL de diffusion
Si votre élément multimédia a été chiffré avec plusieurs DRM, vous devez utiliser une balise de chiffrement dans les URL de diffusion en continu de hello : (format = 'm3u8-aapl', chiffrement = 'xxx').

Hello suivant considérations s’appliquent :

* Seul zéro ou un type de chiffrement peut être spécifié.
* type de chiffrement Hello ne toobe spécifié dans les URL de hello si seul un chiffrement a été appliqué toohello actif.
* type de chiffrement Hello respecte la casse.
* Hello, les types de chiffrement suivants peut être spécifié :  
  * **cenc** : chiffrement commun (Playready ou Widevine)
  * **cbcs-aapl** : Fairplay
  * **cbc** : chiffrement de l’enveloppe AES

## <a name="create-and-configure-a-visual-studio-project"></a>Créer et configurer un projet Visual Studio

1. Configurer votre environnement de développement et de remplir le fichier app.config de hello avec les informations de connexion, comme décrit dans [développement Media Services avec .NET](media-services-dotnet-how-to-use.md). 
2. Ajouter hello suivant éléments trop**appSettings** défini dans votre fichier app.config :

        <add key="Issuer" value="http://testacs.com"/>
        <add key="Audience" value="urn:test"/>

## <a name="example"></a>Exemple

Hello suivant l’exemple montre hello capacité toouse Media Services toodeliver votre contenu chiffré avec FairPlay. Cette fonctionnalité a été introduite dans hello Azure Media Services SDK pour .NET version 3.6.0. 

Remplacer le code hello dans votre fichier Program.cs avec le code hello présenté dans cette section.

>[!NOTE]
>Un nombre limite de 1 000 000 a été défini pour les différentes stratégies AMS (par exemple, pour la stratégie de localisateur ou pour ContentKeyAuthorizationPolicy). Vous devez utiliser hello ID de stratégie même si vous utilisez toujours hello même jours / autorisations d’accès, par exemple, les stratégies pour les localisateurs sont tooremain prévue en place pendant une longue période (non-téléchargement stratégies). Pour plus d’informations, consultez [cette rubrique](media-services-dotnet-manage-entities.md#limit-access-policies) .

Assurez-vous que tooupdate variables toopoint toofolders où se trouvent vos fichiers d’entrée.

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using System.Threading;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using Microsoft.WindowsAzure.MediaServices.Client.ContentKeyAuthorization;
    using Microsoft.WindowsAzure.MediaServices.Client.DynamicEncryption;
    using Microsoft.WindowsAzure.MediaServices.Client.FairPlay;
    using Newtonsoft.Json;
    using System.Security.Cryptography.X509Certificates;

    namespace DynamicEncryptionWithFairPlay
    {
        class Program
        {
        // Read values from hello App.config file.
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

        private static readonly string _mediaFiles =
            Path.GetFullPath(@"../..\Media");

        private static readonly string _singleMP4File =
            Path.Combine(_mediaFiles, @"BigBuckBunny.mp4");

        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            bool tokenRestriction = false;
            string tokenTemplateString = null;

            IAsset asset = UploadFileAndCreateAsset(_singleMP4File);
            Console.WriteLine("Uploaded asset: {0}", asset.Id);

            IAsset encodedAsset = EncodeToAdaptiveBitrateMP4Set(asset);
            Console.WriteLine("Encoded asset: {0}", encodedAsset.Id);

            IContentKey key = CreateCommonCBCTypeContentKey(encodedAsset);
            Console.WriteLine("Created key {0} for hello asset {1} ", key.Id, encodedAsset.Id);
            Console.WriteLine("FairPlay License Key delivery URL: {0}", key.GetKeyDeliveryUrl(ContentKeyDeliveryType.FairPlay));
            Console.WriteLine();

            if (tokenRestriction)
            tokenTemplateString = AddTokenRestrictedAuthorizationPolicy(key);
            else
            AddOpenAuthorizationPolicy(key);

            Console.WriteLine("Added authorization policy: {0}", key.AuthorizationPolicyId);
            Console.WriteLine();

            CreateAssetDeliveryPolicy(encodedAsset, key);
            Console.WriteLine("Created asset delivery policy. \n");
            Console.WriteLine();

            if (tokenRestriction && !String.IsNullOrEmpty(tokenTemplateString))
            {
            // Deserializes a string containing an Xml representation of a TokenRestrictionTemplate
            // back into a TokenRestrictionTemplate class instance.
            TokenRestrictionTemplate tokenTemplate =
                TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

            // Generate a test token based on hello hello data in hello given TokenRestrictionTemplate.
            // Note, you need toopass hello key id Guid because we specified
            // TokenClaim.ContentKeyIdentifierClaim in during hello creation of TokenRestrictionTemplate.
            Guid rawkey = EncryptionUtils.GetKeyIdAsGuid(key.Id);
            string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate, null, rawkey,
                                        DateTime.UtcNow.AddDays(365));
            Console.WriteLine("hello authorization token is:\nBearer {0}", testToken);
            Console.WriteLine();
            }

            string url = GetStreamingOriginLocator(encodedAsset);
            Console.WriteLine("Encrypted HLS URL: {0}/manifest(format=m3u8-aapl)", url);

            Console.ReadLine();
        }

        static public IAsset UploadFileAndCreateAsset(string singleFilePath)
        {
            if (!File.Exists(singleFilePath))
            {
            Console.WriteLine("File does not exist.");
            return null;
            }

            var assetName = Path.GetFileNameWithoutExtension(singleFilePath);
            IAsset inputAsset = _context.Assets.Create(assetName, AssetCreationOptions.None);

            var assetFile = inputAsset.AssetFiles.Create(Path.GetFileName(singleFilePath));

            Console.WriteLine("Created assetFile {0}", assetFile.Name);

            Console.WriteLine("Upload {0}", assetFile.Name);

            assetFile.Upload(singleFilePath);
            Console.WriteLine("Done uploading {0}", assetFile.Name);

            return inputAsset;
        }

        static public IAsset EncodeToAdaptiveBitrateMP4Set(IAsset inputAsset)
        {
            var encodingPreset = "Adaptive Streaming";

            IJob job = _context.Jobs.Create(String.Format("Encoding {0}", inputAsset.Name));

            var mediaProcessors =
            _context.MediaProcessors.Where(p => p.Name.Contains("Media Encoder Standard")).ToList();

            var latestMediaProcessor =
            mediaProcessors.OrderBy(mp => new Version(mp.Version)).LastOrDefault();

            ITask encodeTask = job.Tasks.AddNew("Encoding", latestMediaProcessor, encodingPreset, TaskOptions.None);
            encodeTask.InputAssets.Add(inputAsset);
            encodeTask.OutputAssets.AddNew(String.Format("{0} as {1}", inputAsset.Name, encodingPreset), AssetCreationOptions.StorageEncrypted);

            job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
            job.Submit();
            job.GetExecutionProgressTask(CancellationToken.None).Wait();

            return job.OutputMediaAssets[0];
        }

        static public IContentKey CreateCommonCBCTypeContentKey(IAsset asset)
        {
            // Create HLS SAMPLE AES encryption content key
            Guid keyId = Guid.NewGuid();
            byte[] contentKey = GetRandomBuffer(16);

            IContentKey key = _context.ContentKeys.Create(
                        keyId,
                        contentKey,
                        "ContentKey",
                        ContentKeyType.CommonEncryptionCbcs);

            // Associate hello key with hello asset.
            asset.ContentKeys.Add(key);

            return key;
        }


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


            // Configure FairPlay policy option.
            string FairPlayConfiguration = ConfigureFairPlayPolicyOptions();

            IContentKeyAuthorizationPolicyOption FairPlayPolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("",
            ContentKeyDeliveryType.FairPlay,
            restrictions,
            FairPlayConfiguration);


            IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("Deliver Common CBC Content Key with no restrictions").
                Result;

            contentKeyAuthorizationPolicy.Options.Add(FairPlayPolicy);

            // Associate hello content key authorization policy with hello content key.
            contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
            contentKey = contentKey.UpdateAsync().Result;
        }

        public static string AddTokenRestrictedAuthorizationPolicy(IContentKey contentKey)
        {
            string tokenTemplateString = GenerateTokenRequirements();

            List<ContentKeyAuthorizationPolicyRestriction> restrictions = new List<ContentKeyAuthorizationPolicyRestriction>
                    {
                    new ContentKeyAuthorizationPolicyRestriction
                    {
                        Name = "Token Authorization Policy",
                        KeyRestrictionType = (int)ContentKeyRestrictionType.TokenRestricted,
                        Requirements = tokenTemplateString,
                    }
                    };

            // Configure FairPlay policy option.
            string FairPlayConfiguration = ConfigureFairPlayPolicyOptions();


            IContentKeyAuthorizationPolicyOption FairPlayPolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("Token option",
                   ContentKeyDeliveryType.FairPlay,
                   restrictions,
                   FairPlayConfiguration);

            IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("Deliver Common CBC Content Key with token restrictions").
                Result;

            contentKeyAuthorizationPolicy.Options.Add(FairPlayPolicy);

            // Associate hello content key authorization policy with hello content key
            contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
            contentKey = contentKey.UpdateAsync().Result;

            return tokenTemplateString;
        }

        private static string ConfigureFairPlayPolicyOptions()
        {
            // For testing you can provide all zeroes for ASK bytes together with hello cert from Apple FPS SDK.
            // However, for production you must use a real ASK from Apple bound tooa real prod certificate.
            byte[] askBytes = Guid.NewGuid().ToByteArray();
            var askId = Guid.NewGuid();
            // Key delivery retrieves askKey by askId and uses this key toogenerate hello response.
            IContentKey askKey = _context.ContentKeys.Create(
                        askId,
                        askBytes,
                        "askKey",
                        ContentKeyType.FairPlayASk);

            //Customer password for creating hello .pfx file.
            string pfxPassword = "<customer password for creating hello .pfx file>";
            // Key delivery retrieves pfxPasswordKey by pfxPasswordId and uses this key toogenerate hello response.
            var pfxPasswordId = Guid.NewGuid();
            byte[] pfxPasswordBytes = System.Text.Encoding.UTF8.GetBytes(pfxPassword);
            IContentKey pfxPasswordKey = _context.ContentKeys.Create(
                        pfxPasswordId,
                        pfxPasswordBytes,
                        "pfxPasswordKey",
                        ContentKeyType.FairPlayPfxPassword);

            // iv - 16 bytes random value, must match hello iv in hello asset delivery policy.
            byte[] iv = Guid.NewGuid().ToByteArray();

            //Specify hello .pfx file created by hello customer.
            var appCert = new X509Certificate2("path toohello .pfx file created by hello customer", pfxPassword, X509KeyStorageFlags.Exportable);

            string FairPlayConfiguration =
            Microsoft.WindowsAzure.MediaServices.Client.FairPlay.FairPlayConfiguration.CreateSerializedFairPlayOptionConfiguration(
                appCert,
                pfxPassword,
                pfxPasswordId,
                askId,
                iv);

            return FairPlayConfiguration;
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

        static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
        {
            var kdPolicy = _context.ContentKeyAuthorizationPolicies.Where(p => p.Id == key.AuthorizationPolicyId).Single();

            var kdOption = kdPolicy.Options.Single(o => o.KeyDeliveryType == ContentKeyDeliveryType.FairPlay);

            FairPlayConfiguration configFP = JsonConvert.DeserializeObject<FairPlayConfiguration>(kdOption.KeyDeliveryConfiguration);

            // Get hello FairPlay license service URL.
            Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.FairPlay);

            // hello reason hello below code replaces "https://" with "skd://" is because
            // in hello IOS player sample code which you obtained in Apple developer account,
            // hello player only recognizes a Key URL that starts with skd://.
            // However, if you are using a customized player,
            // you can choose whatever protocol you want.
            // For example, "https".

            Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
            new Dictionary<AssetDeliveryPolicyConfigurationKey, string>
            {
                    {AssetDeliveryPolicyConfigurationKey.FairPlayLicenseAcquisitionUrl, acquisitionUrl.ToString().Replace("https://", "skd://")},
                    {AssetDeliveryPolicyConfigurationKey.CommonEncryptionIVForCbcs, configFP.ContentEncryptionIV}
            };

            var assetDeliveryPolicy = _context.AssetDeliveryPolicies.Create(
                "AssetDeliveryPolicy",
            AssetDeliveryPolicyType.DynamicCommonEncryptionCbcs,
            AssetDeliveryProtocol.HLS,
            assetDeliveryPolicyConfiguration);

            // Add AssetDelivery Policy toohello asset
            asset.DeliveryPolicies.Add(assetDeliveryPolicy);

        }


        /// <summary>
        /// Gets hello streaming origin locator.
        /// </summary>
        /// <param name="assets"></param>
        /// <returns></returns>
        static public string GetStreamingOriginLocator(IAsset asset)
        {

            // Get a reference toohello streaming manifest file from hello  
            // collection of files in hello asset.

            var assetFile = asset.AssetFiles.Where(f => f.Name.ToLower().
                         EndsWith(".ism")).
                         FirstOrDefault();

            // Create a 30-day readonly access policy.
            IAccessPolicy policy = _context.AccessPolicies.Create("Streaming policy",
            TimeSpan.FromDays(30),
            AccessPermissions.Read);

            // Create a locator toohello streaming content on an origin.
            ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
            policy,
            DateTime.UtcNow.AddMinutes(-5));

            // Create a URL toohello manifest file.
            return originLocator.Path + assetFile.Name;
        }

        static private void JobStateChanged(object sender, JobStateChangedEventArgs e)
        {
            Console.WriteLine(string.Format("{0}\n  State: {1}\n  Time: {2}\n\n",
            ((IJob)sender).Name,
            e.CurrentState,
            DateTime.UtcNow.ToString(@"yyyy_M_d__hh_mm_ss")));
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


## <a name="next-steps-media-services-learning-paths"></a>Étapes suivantes : Parcours d’apprentissage Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
