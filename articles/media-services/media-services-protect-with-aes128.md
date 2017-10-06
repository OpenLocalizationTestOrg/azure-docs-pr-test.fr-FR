---
title: "aaaUsing AES-128 dynamique chiffrement et la clé de service de remise | Documents Microsoft"
description: "Microsoft Azure Media Services permet de vous toodeliver votre contenu chiffré avec les clés de chiffrement AES 128 bits. Media Services fournit également un service de fourniture de clé hello qui remet les utilisateurs tooauthorized de clés de chiffrement. Cette rubrique montre comment toodynamically chiffrer avec AES-128 et utiliser le service de distribution de clés hello."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 4d2c10af-9ee0-408f-899b-33fa4c1d89b9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: juliako
ms.openlocfilehash: cb1b413ec2ba79f7437464099cf72236ab93f312
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-aes-128-dynamic-encryption-and-key-delivery-service"></a>Utilisation du chiffrement dynamique AES-128 et du service de distribution des clés
> [!div class="op_single_selector"]
> * [.NET](media-services-protect-with-aes128.md)
> * [Java](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [PHP](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="overview"></a>Vue d'ensemble
> [!NOTE]
> Consultez [cela](https://channel9.msdn.com/Shows/Azure-Friday/Azure-Media-Services-Protecting-your-Media-Content-with-AES-Encryption) vidéo pour un aperçu de comment tooprotect votre du contenu multimédia avec chiffrement AES.
> 
> 

Microsoft Azure Media Services vous permet de toodeliver Http Live Streaming (HLS) et Smooth Streaming chiffré avec Advanced Encryption Standard (AES) (à l’aide de clés de chiffrement 128 bits). Media Services fournit également un service de fourniture de clé hello qui remet les utilisateurs tooauthorized de clés de chiffrement. Si vous souhaitez un élément multimédia pour tooencrypt de Media Services, vous devez tooassociate une clé de chiffrement avec asset de hello et également configurez des stratégies d’autorisation pour la clé de hello. Lorsqu’un flux de données est demandée par un lecteur, Media Services utilise hello spécifié toodynamically clé chiffrer votre contenu à l’aide du chiffrement AES. flux de données toodecrypt hello, le lecteur hello demande clé de hello de service de distribution de clés hello. toodecide soit ou non d’utilisateur de hello autorisé clé de hello tooget, hello évalue les stratégies d’autorisation hello que vous avez spécifié pour la clé de hello.

Media Services prend en charge plusieurs méthodes d’authentification des utilisateurs effectuant des demandes de clé. Hello contenu clé peut avoir une ou plusieurs restrictions d’autorisation : ouvrir ou de restriction de jeton. stratégie de restriction token Hello doit être accompagné d’un jeton émis par un Service (jeton de sécurité). Media Services prend en charge les jetons Bonjour [des jetons Web simples](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2) format de (SWT) et [jeton Web JSON](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3) format (JWT). Pour plus d’informations, consultez [configurer la stratégie d’autorisation de clé de contenu hello](media-services-protect-with-aes128.md#configure_key_auth_policy).

tootake parti du chiffrement dynamique, vous devez toohave une ressource qui contient un ensemble de fichiers MP4 à plusieurs débits ou des fichiers sources de diffusion en continu lisse débits. Vous devez également stratégie de livraison tooconfigure hello pour un composant hello (décrite plus loin dans cette rubrique). Ensuite, selon le format de hello spécifié dans l’URL de diffusion en continu de hello, serveur de diffusion en continu à la demande de hello s’assure que ce flux de données hello est remis dans le protocole hello que vous avez choisi. Par conséquent, vous devez uniquement toostore et payer pour les fichiers hello dans un seul format de stockage et le service Media Services pour la génération et fournit hello de réponse appropriée en fonction des demandes d’un client.

Cette rubrique serait utile toodevelopers qui fonctionnent sur les applications qui fournissent du contenu multimédia protégé. rubrique de Hello vous montre comment tooconfigure hello service de distribution de clés avec les stratégies d’autorisation afin que seuls les clients autorisés puissent recevoir des clés de chiffrement hello. Il montre également comment le chiffrement dynamique toouse.


## <a name="aes-128-dynamic-encryption-and-key-delivery-service-workflow"></a>Flux de travail du chiffrement dynamique AES-128 et du service de distribution des clés

Hello Voici les étapes générales que vous devez tooperform lors du chiffrement de vos éléments multimédias avec AES, à l’aide du service de distribution de clés de Media Services hello et utiliser le chiffrement dynamique.

1. [Créer un élément multimédia et télécharger des fichiers dans l’élément multimédia de hello](media-services-protect-with-aes128.md#create_asset).
2. [Encoder asset hello contenant hello fichier toohello adaptive bitrate MP4 set](media-services-protect-with-aes128.md#encode_asset).
3. [Créer une clé de contenu et l’associer à asset de hello codé](media-services-protect-with-aes128.md#create_contentkey). Dans Media Services, clé de contenu hello contient la clé de chiffrement de l’élément multimédia hello.
4. [Configurer la stratégie d’autorisation de clé de contenu hello](media-services-protect-with-aes128.md#configure_key_auth_policy). stratégie d’autorisation de clé contenu de Hello doit être configurée par vous et remplie par client hello pour hello toobe clé contenu livré toohello client.
5. [Configurer la stratégie de remise hello d’un composant](media-services-protect-with-aes128.md#configure_asset_delivery_policy). configuration de la stratégie Hello livraison inclut : URL d’acquisition et le vecteur d’initialisation (IV) de clé (AES 128 exige hello même vecteur d’initialisation toobe fourni lors du chiffrement et déchiffrement), protocole de remise (par exemple, MPEG DASH, HLS, Smooth Streaming ou tous), hello type de chiffrement dynamique (par exemple, enveloppe ou aucun chiffrement dynamique).

    Vous pouvez appliquer le protocole de tooeach stratégie différente sur hello même actif. Par exemple, vous pouvez appliquer tooSmooth de chiffrement PlayReady/DASH et tooHLS d’enveloppe AES. Tous les protocoles qui ne sont pas définis dans une stratégie de remise (par exemple, vous ajoutez une stratégie unique qui spécifie seulement le HLS en tant que protocole de hello) sera bloquée à partir de la diffusion en continu. Hello exception toothis est si vous ne disposez d’aucune stratégie de remise actif du tout défini. Ensuite, tous les protocoles seront autorisés en hello clair.

6. [Créer un localisateur OnDemand](media-services-protect-with-aes128.md#create_locator) commander tooget une URL de diffusion en continu.

Hello montre également [comment une application cliente peut demander une clé à partir du service de distribution de clés hello](media-services-protect-with-aes128.md#client_request).

Vous trouverez un .NET complète [exemple](media-services-protect-with-aes128.md#example) à fin hello de rubrique de hello.

Hello suivant image montre workflow hello décrit ci-dessus. Ici, le jeton de hello est utilisé pour l’authentification.

![Protéger avec AES-128](./media/media-services-content-protection-overview/media-services-content-protection-with-aes.png)

reste Hello de cette rubrique fournit des explications détaillées, des exemples de code et tootopics des liens qui vous montrent comment tooachieve hello les tâches décrites ci-dessus.

## <a name="current-limitations"></a>Limitations actuelles
Si vous ajoutez ou mettez à jour la stratégie de remise de votre ressource, vous devez supprimer le localisateur existant (le cas échéant) et en créer un nouveau.

## <a id="create_asset"></a>Créer un élément multimédia et télécharger des fichiers dans l’élément multimédia de hello
Dans l’ordre toomanage, encoder et diffuser en continu vos vidéos, vous devez d’abord télécharger votre contenu dans Microsoft Azure Media Services. Une fois téléchargé, votre contenu est stocké en toute sécurité dans le cloud hello pour poursuivre le traitement et la diffusion en continu. 

Pour plus d’informations, consultez [Charger des fichiers vers un compte Media Services](media-services-dotnet-upload-files.md).

## <a id="encode_asset"></a>Encoder hello asset contenant hello fichier toohello ensemble à débit adaptatif MP4
Avec le chiffrement dynamique, il vous suffit de toocreate un élément multimédia contenant un ensemble de fichiers MP4 à plusieurs débits ou des fichiers sources de diffusion en continu lisse débits. Ensuite, en fonction hello le format spécifié dans le manifeste de hello ou demande de fragment, hello à la demande de diffusion en continu serveur garantit que vous recevez des flux de hello protocole hello que vous avez choisi. Par conséquent, vous devez uniquement toostore et payer pour les fichiers hello dans un seul format de stockage et le service Media Services pour la génération et fournit hello de réponse appropriée en fonction des demandes d’un client. Pour plus d’informations, consultez hello [présentation de la mise en package dynamique](media-services-dynamic-packaging-overview.md) rubrique.

>[!NOTE]
>Création de votre compte AMS un **par défaut** point de terminaison de diffusion en continu est ajoutée tooyour compte Bonjour **arrêté** état. toostart de diffusion en continu de votre contenu et profitez de l’empaquetage dynamique et chiffrement dynamique, hello de point de terminaison de diffusion en continu à partir de laquelle vous souhaitez que le contenu toostream a toobe Bonjour **en cours d’exécution** état. 
>
>En outre, toobe toouse en mesure de mise en package dynamique et le chiffrement dynamique votre élément multimédia doit contenir un ensemble de fichiers à débit adaptatif MP4s ou des fichiers de diffusion en continu lisse à débit adaptatif.

Pour obtenir des instructions sur la façon de tooencode, consultez [comment tooencode un élément multimédia à l’aide de Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md).

## <a id="create_contentkey"></a>Créer une clé de contenu et l’associer à asset de hello codée
Dans Media Services, clé de contenu hello contient la clé hello que vous souhaitez tooencrypt un élément multimédia avec.

Pour plus d’informations, consultez [Créer une clé de contenu](media-services-dotnet-create-contentkey.md).

## <a id="configure_key_auth_policy"></a>Configurer la stratégie d’autorisation de clé de contenu hello
Media Services prend en charge plusieurs méthodes d’authentification des utilisateurs effectuant des demandes de clé. stratégie d’autorisation de clé contenu de Hello doit être configurée par vous et remplie par le client hello (lecteur) afin que les toobe clé hello remis toohello client. Hello contenu clé peut avoir une ou plusieurs restrictions d’autorisation : ouverte, restriction de jeton ou restrictions d’adresse IP.

Pour plus d’informations, consultez [Configurer la stratégie d’autorisation de clé de contenu](media-services-dotnet-configure-content-key-auth-policy.md).

## <a id="configure_asset_delivery_policy"></a>Configurer la stratégie de distribution d’éléments multimédia
Configurer la stratégie de livraison de hello pour votre élément multimédia. Les éléments qui hello configuration actif de la stratégie de livraison inclut :

* URL d’acquisition de clé Hello. 
* Bonjour toouse du vecteur d’initialisation (IV) pour le chiffrement d’enveloppe hello. AES 128 exige hello même vecteur d’initialisation toobe fourni lors du chiffrement et déchiffrement. 
* protocole de la livraison d’asset Hello (par exemple, MPEG DASH, HLS, Smooth Streaming ou tous).
* type de Hello de chiffrement dynamique (par exemple, d’enveloppe AES) ou aucun chiffrement dynamique. 

Pour plus d’informations, consultez [Configurer la stratégie de distribution d’éléments multimédia ](media-services-rest-configure-asset-delivery-policy.md).

## <a id="create_locator"></a>Créer une recherche dans l’ordre tooget une URL de diffusion en continu de diffusion en continu à la demande
Vous devez tooprovide votre utilisateur avec hello URL pour Smooth, DASH ou HLS de diffusion en continu.

> [!NOTE]
> Si vous ajoutez ou mettez à jour la stratégie de remise de votre ressource, vous devez supprimer le localisateur existant (le cas échéant) et en créer un nouveau.
> 
> 

Pour plus d’informations sur comment toopublish un élément multimédia et créer une URL de diffusion en continu, consultez [générer une URL de diffusion en continu](media-services-deliver-streaming-content.md).

## <a name="get-a-test-token"></a>Obtenir un test de jeton
Obtenez un test de jeton basé sur la restriction de type hello token qui a été utilisée pour la stratégie d’autorisation de clé de hello.

    // Deserializes a string containing an Xml representation of a TokenRestrictionTemplate
    // back into a TokenRestrictionTemplate class instance.
    TokenRestrictionTemplate tokenTemplate = 
        TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

    // Generate a test token based on hello data in hello given TokenRestrictionTemplate.
    //hello GenerateTestToken method returns hello token without hello word “Bearer” in front
    //so you have tooadd it in front of hello token string. 
    string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate);
    Console.WriteLine("hello authorization token is:\nBearer {0}", testToken);

Vous pouvez utiliser hello [AMS lecteur](http://amsplayer.azurewebsites.net/azuremediaplayer.html) tootest votre flux de données.

## <a id="client_request"></a>Comment votre client peut demander une clé à partir du service de distribution de clés hello ?
Dans l’étape précédente de hello, vous avez construit hello URL qui pointe le fichier de manifeste tooa. Votre client doit tooextract hello d’informations nécessaires hello fichiers manifeste dans l’ordre toomake un service de remise de clés toohello demande de diffusion en continu.

### <a name="manifest-files"></a>Fichiers manifeste
client de Hello nécessite des URL de hello tooextract (qui contient également la clé de contenu Id (enfant)) la valeur à partir du fichier de manifeste hello. Hello client essaiera alors clé de chiffrement hello tooget à partir du service de distribution de clés hello. Hello client doit également valeur hello IV de tooextract et utiliser pour déchiffrer stream.hello hello suivant extrait de code montre hello <Protection> élément du manifeste de diffusion en continu lisse hello.

    <Protection>
      <ProtectionHeader SystemID="B47B251A-2409-4B42-958E-08DBAE7B4EE9">
        <ContentProtection xmlns:sea="urn:mpeg:dash:schema:sea:2012" schemeIdUri="urn:mpeg:dash:sea:2012">
          <sea:SegmentEncryption schemeIdUri="urn:mpeg:dash:sea:aes128-cbc:2013"/>
          <sea:KeySystem keySystemUri="urn:mpeg:dash:sea:keysys:http:2013"/>
          <sea:CryptoPeriod IV="0xD7D7D7D7D7D7D7D7D7D7D7D7D7D7D7D7" 
                            keyUriTemplate="https://wamsbayclus001kd-hs.cloudapp.net/HlsHandler.ashx?
                                            kid=da3813af-55e6-48e7-aa9f-a4d6031f7b4d"/>
        </ContentProtection>
      </ProtectionHeader>
    </Protection>

Dans les cas de hello de TLS, manifeste de racine hello est divisé en fichiers de segment. 

Par exemple, le manifeste de racine hello est : http://test001.origin.mediaservices.windows.net/8bfe7d6f-34e3-4d1a-b289-3e48a8762490/BigBuckBunny.ism/manifest(format=m3u8-aapl) et qu’elle contient une liste de noms de fichiers de segment.

    . . . 
    #EXT-X-STREAM-INF:PROGRAM-ID=1,BANDWIDTH=630133,RESOLUTION=424x240,CODECS="avc1.4d4015,mp4a.40.2",AUDIO="audio"
    QualityLevels(514369)/Manifest(video,format=m3u8-aapl)
    #EXT-X-STREAM-INF:PROGRAM-ID=1,BANDWIDTH=965441,RESOLUTION=636x356,CODECS="avc1.4d401e,mp4a.40.2",AUDIO="audio"
    QualityLevels(842459)/Manifest(video,format=m3u8-aapl)
    …

Si vous ouvrez un des fichiers de segment hello dans l’éditeur de texte (par exemple, http://test001.origin.mediaservices.windows.net/8bfe7d6f-34e3-4d1a-b289-3e48a8762490/BigBuckBunny.ism/QualityLevels(514369)/Manifest(video,format=m3u8-aapl), it should contient la #EXT-X-clé indique ce fichier hello est chiffré.

    #EXTM3U
    #EXT-X-VERSION:4
    #EXT-X-ALLOW-CACHE:NO
    #EXT-X-MEDIA-SEQUENCE:0
    #EXT-X-TARGETDURATION:9
    #EXT-X-KEY:METHOD=AES-128,
    URI="https://wamsbayclus001kd-hs.cloudapp.net/HlsHandler.ashx?
         kid=da3813af-55e6-48e7-aa9f-a4d6031f7b4d",
            IV=0XD7D7D7D7D7D7D7D7D7D7D7D7D7D7D7D7
    #EXT-X-PROGRAM-DATE-TIME:1970-01-01T00:00:00.000+00:00
    #EXTINF:8.425708,no-desc
    Fragments(video=0,format=m3u8-aapl)
    #EXT-X-ENDLIST

>[!NOTE] 
>Si vous envisagez de tooplay une AES chiffrée TLS dans Safari, consultez [ce billet de blog](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/).

### <a name="request-hello-key-from-hello-key-delivery-service"></a>Demander une clé de hello du service de distribution de clés hello

Hello de code suivant montre comment toosend un toohello demande Media Services clé de service de remise à l’aide d’une Uri (qui a été extrait à partir du manifeste de hello) de la remise de clé et un jeton (cette rubrique n’aborde pas comment tooget Web Simple des jetons auprès d’un Service de jeton sécurisé).

    private byte[] GetDeliveryKey(Uri keyDeliveryUri, string token)
    {
        HttpWebRequest request = (HttpWebRequest)WebRequest.Create(keyDeliveryUri);

        request.Method = "POST";
        request.ContentType = "text/xml";
        if (!string.IsNullOrEmpty(token))
        {
            request.Headers[AuthorizationHeader] = token;
        }
        request.ContentLength = 0;

        var response = request.GetResponse();

        var stream = response.GetResponseStream();
        if (stream == null)
        {
            throw new NullReferenceException("Response stream is null");
        }

        var buffer = new byte[256];
        var length = 0;
        while (stream.CanRead && length <= buffer.Length)
        {
            var nexByte = stream.ReadByte();
            if (nexByte == -1)
            {
                break;
            }
            buffer[length] = (byte)nexByte;
            length++;
        }
        response.Close();

        // AES keys must be exactly 16 bytes (128 bits).
        var key = new byte[length];
        Array.Copy(buffer, key, length);
        return key;
    }

## <a name="protect-your-content-with-aes-128-using-net"></a>Protéger votre contenu avec AES-128 en utilisant .NET

### <a name="create-and-configure-a-visual-studio-project"></a>Créer et configurer un projet Visual Studio

1. Configurer votre environnement de développement et de remplir le fichier app.config de hello avec les informations de connexion, comme décrit dans [développement Media Services avec .NET](media-services-dotnet-how-to-use.md). 
2. Ajouter hello suivant éléments trop**appSettings** défini dans votre fichier app.config :

        <add key="Issuer" value="http://testacs.com"/>
        <add key="Audience" value="urn:test"/>

### <a id="example"></a>Exemple

Remplacer le code hello dans votre fichier Program.cs avec le code hello présenté dans cette section.
 
>[!NOTE]
>Un nombre limite de 1 000 000 a été défini pour les différentes stratégies AMS (par exemple, pour la stratégie de localisateur ou pour ContentKeyAuthorizationPolicy). Vous devez utiliser hello ID de stratégie même si vous utilisez toujours hello même jours / autorisations d’accès, par exemple, les stratégies pour les localisateurs sont tooremain prévue en place pendant une longue période (non-téléchargement stratégies). Pour plus d’informations, consultez [cette rubrique](media-services-dotnet-manage-entities.md#limit-access-policies) .

Assurez-vous que tooupdate variables toopoint toofolders où se trouvent vos fichiers d’entrée.

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using System.Security.Cryptography;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;
    using Microsoft.WindowsAzure.MediaServices.Client.ContentKeyAuthorization;
    using Microsoft.WindowsAzure.MediaServices.Client.DynamicEncryption;

    namespace AESDynamicEncryptionAndKeyDeliverySvc
    {
        class Program
        {
        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
        ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
        ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        // A Uri describing hello issuer of hello token.  
        // Must match hello value in hello token for hello token toobe considered valid.
        private static readonly Uri _sampleIssuer =
            new Uri(ConfigurationManager.AppSettings["Issuer"]);
        // hello Audience or Scope of hello token.  
        // Must match hello value in hello token for hello token toobe considered valid.
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

            IContentKey key = CreateEnvelopeTypeContentKey(encodedAsset);
            Console.WriteLine("Created key {0} for hello asset {1} ", key.Id, encodedAsset.Id);
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

            // Generate a test token based on hello data in hello given TokenRestrictionTemplate.
            // Note, you need toopass hello key id Guid because we specified 
            // TokenClaim.ContentKeyIdentifierClaim in during hello creation of TokenRestrictionTemplate.
            Guid rawkey = EncryptionUtils.GetKeyIdAsGuid(key.Id);

            //hello GenerateTestToken method returns hello token without hello word “Bearer” in front
            //so you have tooadd it in front of hello token string. 
            string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate, null, rawkey);
            Console.WriteLine("hello authorization token is:\nBearer {0}", testToken);
            Console.WriteLine();
            }

            // You can use hello bit.ly/aesplayer Flash player tootest hello URL 
            // (with open authorization policy). 
            // Paste hello URL and click hello Update button tooplay hello video. 
            //
            string URL = GetStreamingOriginLocator(encodedAsset);
            Console.WriteLine("Smooth Streaming Url: {0}/manifest", URL);
            Console.WriteLine();
            Console.WriteLine("HLS Url: {0}/manifest(format=m3u8-aapl)", URL);
            Console.WriteLine();

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
            IAsset inputAsset = _context.Assets.Create(assetName, AssetCreationOptions.StorageEncrypted);

            var assetFile = inputAsset.AssetFiles.Create(Path.GetFileName(singleFilePath));

            Console.WriteLine("Created assetFile {0}", assetFile.Name);


            Console.WriteLine("Upload {0}", assetFile.Name);

            assetFile.Upload(singleFilePath);
            Console.WriteLine("Done uploading {0}", assetFile.Name);

            return inputAsset;
        }

        static public IAsset EncodeToAdaptiveBitrateMP4Set(IAsset asset)
        {
            // Declare a new job.
            IJob job = _context.Jobs.Create("Media Encoder Standard Job");
            // Get a media processor reference, and pass tooit hello name of hello 
            // processor toouse for hello specific task.
            IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

            // Create a task with hello encoding details, using a string preset.
            // In this case "Adaptive Streaming" preset is used.
            ITask task = job.Tasks.AddNew("My encoding task",
            processor,
            "Adaptive Streaming",
            TaskOptions.None);

            // Specify hello input asset toobe encoded.
            task.InputAssets.Add(asset);
            // Add an output asset toocontain hello results of hello job. 
            // This output is specified as AssetCreationOptions.None, which 
            // means hello output asset is not encrypted. 
            task.OutputAssets.AddNew("Output asset",
            AssetCreationOptions.StorageEncrypted);

            job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
            job.Submit();
            job.GetExecutionProgressTask(CancellationToken.None).Wait();

            return job.OutputMediaAssets[0];
        }

        private static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
        {
            var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
            ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

            if (processor == null)
            throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

            return processor;
        }

        static public IContentKey CreateEnvelopeTypeContentKey(IAsset asset)
        {
            // Create envelope encryption content key
            Guid keyId = Guid.NewGuid();
            byte[] contentKey = GetRandomBuffer(16);

            IContentKey key = _context.ContentKeys.Create(
                keyId,
                contentKey,
                "ContentKey",
                ContentKeyType.EnvelopeEncryption);

            // Associate hello key with hello asset.
            asset.ContentKeys.Add(key);

            return key;
        }

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

        static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
        {
            Uri keyAcquisitionUri = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.BaselineHttp);

            string envelopeEncryptionIV = Convert.ToBase64String(GetRandomBuffer(16));

            // When configuring delivery policy, you can choose tooassociate it
            // with a key acquisition URL that has a KID appended or
            // or a key acquisition URL that does not have a KID appended  
            // in which case a content key can be reused. 

            // EnvelopeKeyAcquisitionUrl:  contains a key ID in hello key URL.
            // EnvelopeBaseKeyAcquisitionUrl:  hello URL does not contains a key ID

            // hello following policy configuration specifies: 
            // key url that will have KID=<Guid> appended toohello envelope and
            // hello Initialization Vector (IV) toouse for hello envelope encryption.

            Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
            new Dictionary<AssetDeliveryPolicyConfigurationKey, string>
            {
            {AssetDeliveryPolicyConfigurationKey.EnvelopeKeyAcquisitionUrl, keyAcquisitionUri.ToString()}
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
            Console.WriteLine("Adding Asset Delivery Policy: " +
            assetDeliveryPolicy.AssetDeliveryPolicyType);
        }

        static public string GetStreamingOriginLocator(IAsset asset)
        {

            // Get a reference toohello streaming manifest file from hello  
            // collection of files in hello asset. 

            var assetFile = asset.AssetFiles.Where(f => f.Name.ToLower().
                EndsWith(".ism")).
                FirstOrDefault();

            // Create a 30-day readonly access policy. 
            // You cannot create a streaming locator using an AccessPolicy that includes write or delete permissions.            
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

        static private void JobStateChanged(object sender, JobStateChangedEventArgs e)
        {
            Console.WriteLine(string.Format("{0}\n  State: {1}\n  Time: {2}\n\n",
            ((IJob)sender).Name,
            e.CurrentState,
            DateTime.UtcNow.ToString(@"yyyy_M_d__hh_mm_ss")));
        }

        static private byte[] GetRandomBuffer(int size)
        {
            byte[] randomBytes = new byte[size];
            using (RNGCryptoServiceProvider rng = new RNGCryptoServiceProvider())
            {
            rng.GetBytes(randomBytes);
            }

            return randomBytes;
        }
        }
    }


## <a name="media-services-learning-paths"></a>Parcours d’apprentissage de Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

