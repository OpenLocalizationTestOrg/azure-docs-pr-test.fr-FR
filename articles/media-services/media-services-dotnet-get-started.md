---
title: "aaaGet en main de diffusion de contenu sur demande à l’aide de .NET | Documents Microsoft"
description: "Ce didacticiel vous guide tout au long des étapes hello d’implémentation d’une application de diffusion de contenu sur la demande avec Azure Media Services à l’aide de .NET."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 388b8928-9aa9-46b1-b60a-a918da75bd7b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: 4ca9394bd581e1d9062e5a008a410b2c058e017e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-delivering-content-on-demand-using-net-sdk"></a>Prendre en main la diffusion de contenus à la demande à l’aide du Kit de développement logiciel (SDK) .NET
[!INCLUDE [media-services-selector-get-started](../../includes/media-services-selector-get-started.md)]

Ce didacticiel vous guide tout au long des étapes hello d’implémentation d’un service de diffusion de contenu vidéo à la demande (VoD) base avec l’application Azure Media Services (AMS) à l’aide de hello Azure Media Services .NET SDK.

## <a name="prerequisites"></a>Composants requis

Hello Voici didacticiel de hello toocomplete requis :

* Un compte Azure. Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/).
* Un compte Media Services. toocreate un compte Media Services, consultez [comment tooCreate un compte Media Services](media-services-portal-create-account.md).
* .NET Framework 4.0 ou version ultérieure.
* Visual Studio.

Ce didacticiel inclut hello tâches suivantes :

1. Début de la diffusion en continu de point de terminaison (à l’aide de hello portail Azure).
2. Créer et configurer un projet Visual Studio
3. Connectez le compte de service de média toohello.
2. Télécharger un fichier vidéo.
3. Encoder le fichier de source de hello en un ensemble de fichiers MP4 à débit adaptatif.
4. Publier les actifs hello et get de diffusion en continu et URL de téléchargement progressif.  
5. Lire votre contenu.

## <a name="overview"></a>Vue d'ensemble
Ce didacticiel vous guide tout au long des étapes hello d’implémentation d’une application de diffusion de contenu vidéo à la demande (VoD) à l’aide d’Azure Media Services (AMS) SDK pour .NET.

didacticiel de Hello présente des flux de travail Media Services hello et objets de programmation courants hello et tâches requises pour le développement de Media Services. À l’achèvement de hello du didacticiel de hello, vous être en mesure de toostream ou télécharger progressivement un exemple de fichier de média que vous avez téléchargé, encodé, téléchargé.

### <a name="ams-model"></a>Modèle d’AMS

Hello image suivante montre certains des objets de hello couramment utilisé lors du développement d’applications VoD sur le modèle de Media Services OData hello.

Cliquez sur tooview d’image hello il plein écran.  

<a href="./media/media-services-dotnet-get-started/media-services-overview-object-model.png" target="_blank"><img src="./media/media-services-dotnet-get-started/media-services-overview-object-model-small.png"></a> 

Vous pouvez afficher hello ensemble modèle [ici](https://media.windows.net/API/$metadata?api-version=2.15).  

## <a name="start-streaming-endpoints-using-hello-azure-portal"></a>Démarrer la diffusion en continu des points de terminaison à l’aide de hello portail Azure

Lorsque vous travaillez avec un des scénarios les plus courants de hello est diffusion vidéo via à débit adaptatif de diffusion en continu Azure Media Services. Media Services propose un empaquetage dynamique, ce qui vous permet de toodeliver votre vitesse de transmission adaptative MP4 encodés le contenu de diffusion en continu des formats pris en charge par Media Services (MPEG DASH, HLS, Smooth Streaming) juste-à-temps, sans que vous ayez toostore préconçue versions de chacune de ces formats de diffusion en continu.

>[!NOTE]
>Création de votre compte AMS un **par défaut** point de terminaison de diffusion en continu est ajoutée tooyour compte Bonjour **arrêté** état. toostart de diffusion en continu de votre contenu et profitez de l’empaquetage dynamique et chiffrement dynamique, hello de point de terminaison de diffusion en continu à partir de laquelle vous souhaitez que le contenu toostream a toobe Bonjour **en cours d’exécution** état.

toostart hello du point de terminaison de diffusion en continu, hello suivant :

1. Connectez-vous à l’adresse hello [portail Azure](https://portal.azure.com/).
2. Dans la fenêtre des paramètres hello, cliquez sur les points de terminaison de diffusion en continu.
3. Cliquez sur le point de terminaison de diffusion en continu de la valeur par défaut hello.

    fenêtre de détails par défaut du point de terminaison de diffusion en continu Hello s’affiche.

4. Cliquez sur l’icône Démarrer hello.
5. Cliquez sur toosave de bouton hello enregistrer vos modifications.

## <a name="create-and-configure-a-visual-studio-project"></a>Créer et configurer un projet Visual Studio

1. Configurer votre environnement de développement et de remplir le fichier app.config de hello avec les informations de connexion, comme décrit dans [développement Media Services avec .NET](media-services-dotnet-how-to-use.md). 
2. Créer un nouveau dossier (dossier peut être n’importe où sur votre disque local) et copiez le fichier .mp4 que vous voulez tooencode et flux de données ou téléchargez progressivement. Dans cet exemple, le chemin d’accès de hello « C:\VideoFiles » est utilisé.

## <a name="connect-toohello-media-services-account"></a>Compte de service de média toohello de connexion

Lorsque vous utilisez Media Services avec .NET, vous devez utiliser hello **CloudMediaContext** classe pour les Services de support la plupart des tâches de programmation : la connexion de compte de Services tooMedia ; la création, mise à jour, l’accès à et suppression suivantes de hello objets : actifs, fichiers d’éléments multimédias, travaux, les stratégies d’accès, les localisateurs, etc..

Remplacer classe de programme par défaut hello hello suivant de code. Hello de code montre comment les valeurs de connexion de hello tooread à partir du fichier App.config de hello et toocreate hello **CloudMediaContext** Services d’objet dans l’ordre tooconnect tooMedia. Pour plus d’informations, consultez [connexion toohello API Media Services](media-services-use-aad-auth-to-access-ams-api.md).

Assurez-vous que tooupdate hello fichier nom et chemin d’accès toowhere que vous avez votre fichier multimédia.

Hello **Main** fonction appelle des méthodes qui seront définies ultérieurement dans cette section.

> [!NOTE]
> Vous allez récupérer les erreurs de compilation jusqu'à ce que vous ajoutez des définitions pour toutes les fonctions hello.

    class Program
    {
        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
        ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
        ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        private static CloudMediaContext _context = null;

        static void Main(string[] args)
        {
        try
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            // Add calls toomethods defined in this section.
            // Make sure tooupdate hello file name and path toowhere you have your media file.
            IAsset inputAsset =
            UploadFile(@"C:\VideoFiles\BigBuckBunny.mp4", AssetCreationOptions.None);

            IAsset encodedAsset =
            EncodeToAdaptiveBitrateMP4s(inputAsset, AssetCreationOptions.None);

            PublishAssetGetURLs(encodedAsset);
        }
        catch (Exception exception)
        {
            // Parse hello XML error message in hello Media Services response and create a new
            // exception with its content.
            exception = MediaServicesExceptionParser.Parse(exception);

            Console.Error.WriteLine(exception.Message);
        }
        finally
        {
            Console.ReadLine();
        }
        }
    }

## <a name="create-a-new-asset-and-upload-a-video-file"></a>Créer un nouvel élément et charger un fichier vidéo

Dans Media Services, vous téléchargez (ou réceptionnez) vos fichiers numériques dans un élément multimédia. Hello **Asset** entité peut contenir vidéo, audio, images, collections de miniatures, texte assure le suivi et sous-titres fichiers (et les métadonnées hello sur ces fichiers.)  Une fois que les fichiers hello sont téléchargés, votre contenu est stocké en toute sécurité dans le cloud hello pour le traitement et la diffusion en continu. fichiers Hello dans asset de hello sont appelés **des fichiers**.

Hello **UploadFile** définie sous les appels de méthode **CreateFromFile** (défini dans les Extensions du Kit de développement logiciel .NET). **CreateFromFile** crée un nouvel élément multimédia dans quel hello fichier source spécifié est chargé.

Hello **CreateFromFile** méthode **AssetCreationOptions** qui vous permet de spécifier l’une des hello asset création options suivantes :

* **None** : aucun chiffrement. Il s’agit de valeur par défaut de hello. À noter que quand vous utilisez cette option, votre contenu n'est pas protégé pendant le transit ou le repos dans le stockage.
  Si vous envisagez de toodeliver un fichier MP4 à l’aide d’un téléchargement progressif, utilisez cette option.
* **StorageEncrypted** -Utilisez cette option tooencrypt votre contenu en clair localement à l’aide de chiffrement Advanced Encryption Standard (AES)-256 bits, qui télécharge tooAzure Storage où il est stocké et chiffré au repos. Les éléments multimédias protégés par chiffrement de stockage sont automatiquement déchiffrés et placés dans un tooencoding préalable de système de fichiers chiffrés et éventuellement RE-chiffrée toouploading préalable comme un nouvel élément multimédia de sortie. Hello est principalement utilisé pour le chiffrement de stockage lorsque vous souhaitez toosecure vos fichiers multimédias d’entrée de haute qualité avec un chiffrement renforcé au repos sur le disque.
* **CommonEncryptionProtected** : utilisez cette option quand vous chargez du contenu qui a déjà été chiffré et protégé avec la DRM Common Encryption ou PlayReady (par exemple Smooth Streaming protégé avec la DRM PlayReady).
* **EnvelopeEncryptionProtected** : utilisez cette option lorsque vous téléchargez un contenu au format TLS chiffré avec AES. Notez que les fichiers hello doivent avoir été codés et chiffrés par Transform Manager.

Hello **CreateFromFile** méthode vous permet également de spécifier un rappel de progression du téléchargement ordre tooreport hello du fichier de hello.

Bonjour l’exemple suivant, nous spécifions **aucun** pour les options d’asset hello.

Ajoutez hello suivant de méthode toohello classe de programme.

    static public IAsset UploadFile(string fileName, AssetCreationOptions options)
    {
        IAsset inputAsset = _context.Assets.CreateFromFile(
            fileName,
            options,
            (af, p) =>
            {
                Console.WriteLine("Uploading '{0}' - Progress: {1:0.##}%", af.Name, p.Progress);
            });

        Console.WriteLine("Asset {0} created.", inputAsset.Id);

        return inputAsset;
    }


## <a name="encode-hello-source-file-into-a-set-of-adaptive-bitrate-mp4-files"></a>Encoder le fichier de source de hello en un ensemble de fichiers MP4 à débit adaptatif
Après réception d’éléments multimédias dans Media Services, support peut être codée, transmuxed, filigrane et ainsi de suite, avant de le livrer tooclients. Ces activités sont planifiées et exécutées sur plusieurs arrière-plan rôle instances tooensure performances et la disponibilité. Ces activités sont appellent des travaux, et chaque tâche se compose de tâches atomiques qui hello travail réel dans le fichier d’élément multimédia hello.

Comme mentionné précédemment, lorsque vous travaillez avec Azure Media Services, un des scénarios les plus courants de hello est remise à débit adaptatif tooyour clients de diffusion en continu. Media Services peut package dynamiquement un ensemble de fichiers MP4 à débit adaptatif dans une des hello suivant formats : HTTP Live Streaming (HLS), la diffusion en continu lisse et MPEG DASH.

tootake parti de l’empaquetage dynamique, vous devez tooencode ou transcoder votre fichier mezzanine (source) dans un ensemble de fichiers MP4 ou de fichiers de diffusion en continu lisse à débit adaptatif.  

Hello suivant de code montre comment toosubmit un encodage de la tâche. tâche Hello contient une tâche qui spécifie un fichier mezzanine de hello tootranscode dans un ensemble de l’utilisation de fichiers à débit adaptatif MP4s **Media Encoder Standard**. code de Hello soumet le travail de hello et attend jusqu'à son terme.

Une fois le travail de hello est terminé, vous est en mesure de toostream votre élément multimédia ou télécharger progressivement les fichiers MP4 qui ont été créés à la suite de transcodage.

Ajoutez hello suivant de méthode toohello classe de programme.

    static public IAsset EncodeToAdaptiveBitrateMP4s(IAsset asset, AssetCreationOptions options)
    {

        // Prepare a job with a single task tootranscode hello specified asset
        // into a multi-bitrate asset.

        IJob job = _context.Jobs.CreateWithSingleTask(
            "Media Encoder Standard",
            "Adaptive Streaming",
            asset,
            "Adaptive Bitrate MP4",
            options);

        Console.WriteLine("Submitting transcoding job...");


        // Submit hello job and wait until it is completed.
        job.Submit();

        job = job.StartExecutionProgressTask(
            j =>
            {
                Console.WriteLine("Job state: {0}", j.State);
                Console.WriteLine("Job progress: {0:0.##}%", j.GetOverallProgress());
            },
            CancellationToken.None).Result;

        Console.WriteLine("Transcoding job finished.");

        IAsset outputAsset = job.OutputMediaAssets[0];

        return outputAsset;
    }

## <a name="publish-hello-asset-and-get-urls-for-streaming-and-progressive-download"></a>Publier l’élément multimédia de hello et obtenir l’URL pour le téléchargement progressif et de diffusion en continu

toostream ou téléchargement d’un élément multimédia, vous tout d’abord besoin trop « publier » en créant un localisateur. Les localisateurs offrent toofiles accès contenues dans l’élément multimédia de hello. Media Services prend en charge deux types de localisateurs : OnDemandOrigin localisateurs, support toostream utilisé (par exemple, MPEG DASH, HLS ou Smooth Streaming) et les localisateurs de Signature d’accès (SAS), les fichiers de support de toodownload (pour plus d’informations sur SAS localisateurs, consultez utilisés[cela](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog).

### <a name="some-details-about-url-formats"></a>Informations sur les formats d’URL

Après avoir créé les localisateurs hello, vous pouvez générer des URL hello qui est utilisé toostream ou téléchargez vos fichiers. exemple Hello dans ce didacticiel ne produira pas les URL que vous pouvez coller dans les navigateurs appropriés. Cette section donne simplement quelques rapides exemples de l’aspect des différents formats.

#### <a name="a-streaming-url-for-mpeg-dash-has-hello-following-format"></a>Une URL de diffusion en continu pour MPEG DASH a hello suivant le format :

{nom du point de terminaison de streaming-nom du compte media services}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest**(format=mpd-time-csf)**

#### <a name="a-streaming-url-for-hls-has-hello-following-format"></a>Une URL de diffusion en continu pour TLS a hello suivant le format :

{nom du point de terminaison de streaming-nom du compte media services}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest**(format=m3u8-aapl)**

#### <a name="a-streaming-url-for-smooth-streaming-has-hello-following-format"></a>Une URL de diffusion pour Smooth Streaming a hello suivant le format :

{nom du point de terminaison de diffusion en continu-nom du compte media services}.streaming.mediaservices.windows.net/{ID_de_localisateur}/{nom_de_fichier}.ISM/Manifest


#### <a name="a-sas-url-used-toodownload-files-has-hello-following-format"></a>Une URL SAS utilisé des fichiers toodownload a hello suivant le format :

{nom du conteneur d’objets blob}/{nom de la ressource}/{nom du fichier}/{signature SAS}

Extensions de Media Services .NET SDK fournissent des méthodes d’assistance pratiques que retour mise en forme des URL pour hello publié actif.

Hello de code suivant utilise les localisateurs toocreate Extensions du Kit de développement .NET et URL de téléchargement progressif et tooget de diffusion en continu. code de Hello montre également comment toodownload fichiers tooa les dossier local.

Ajoutez hello suivant de méthode toohello classe de programme.

    static public void PublishAssetGetURLs(IAsset asset)
    {
        // Publish hello output asset by creating an Origin locator for adaptive streaming,
        // and a SAS locator for progressive download.

        _context.Locators.Create(
            LocatorType.OnDemandOrigin,
            asset,
            AccessPermissions.Read,
            TimeSpan.FromDays(30));

        _context.Locators.Create(
            LocatorType.Sas,
            asset,
            AccessPermissions.Read,
            TimeSpan.FromDays(30));


        IEnumerable<IAssetFile> mp4AssetFiles = asset
                .AssetFiles
                .ToList()
                .Where(af => af.Name.EndsWith(".mp4", StringComparison.OrdinalIgnoreCase));

        // Get hello Smooth Streaming, HLS and MPEG-DASH URLs for adaptive streaming,
        // and hello Progressive Download URL.
        Uri smoothStreamingUri = asset.GetSmoothStreamingUri();
        Uri hlsUri = asset.GetHlsUri();
        Uri mpegDashUri = asset.GetMpegDashUri();

        // Get hello URls for progressive download for each MP4 file that was generated as a result
        // of encoding.
        List<Uri> mp4ProgressiveDownloadUris = mp4AssetFiles.Select(af => af.GetSasUri()).ToList();


        // Display  hello streaming URLs.
        Console.WriteLine("Use hello following URLs for adaptive streaming: ");
        Console.WriteLine(smoothStreamingUri);
        Console.WriteLine(hlsUri);
        Console.WriteLine(mpegDashUri);
        Console.WriteLine();

        // Display hello URLs for progressive download.
        Console.WriteLine("Use hello following URLs for progressive download.");
        mp4ProgressiveDownloadUris.ForEach(uri => Console.WriteLine(uri + "\n"));
        Console.WriteLine();

        // Download hello output asset tooa local folder.
        string outputFolder = "job-output";
        if (!Directory.Exists(outputFolder))
        {
            Directory.CreateDirectory(outputFolder);
        }

        Console.WriteLine();
        Console.WriteLine("Downloading output asset files tooa local folder...");
        asset.DownloadToFolder(
            outputFolder,
            (af, p) =>
            {
                Console.WriteLine("Downloading '{0}' - Progress: {1:0.##}%", af.Name, p.Progress);
            });

        Console.WriteLine("Output asset files available at '{0}'.", Path.GetFullPath(outputFolder));
    }

## <a name="test-by-playing-your-content"></a>Tester en lisant votre contenu

Une fois que vous exécutez le programme hello défini dans la section précédente de hello, hello URL similaire toohello suivant s’affichera dans la fenêtre de console hello.

URL de diffusion adaptative :

Smooth Streaming

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest

HLS

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=m3u8-aapl)

MPEG DASH

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=mpd-time-csf)

URL de téléchargement progressif (audio et vidéo).

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1500kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1000kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_56kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z


toostream votre vidéo, collez l’URL dans la zone de texte URL hello Bonjour [lecteur Azure Media Services](http://amsplayer.azurewebsites.net/azuremediaplayer.html).

tootest progressif de téléchargement, collez une URL dans un navigateur (par exemple, Internet Explorer, Chrome ou Safari).

Pour plus d’informations, consultez hello rubriques suivantes :

- [Lecture de votre contenu à l’aide des lecteurs existants](media-services-playback-content-with-existing-players.md)
- [Développement d'applications de lecteur vidéo](media-services-develop-video-players.md)
- [Incorporation d'une vidéo de diffusion en continu adaptative MPEG-DASH dans une application HTML5 avec DASH.js](media-services-embed-mpeg-dash-in-html5.md)

## <a name="download-sample"></a>Charger l’exemple
exemple de code suivant Hello contient code hello que vous avez créé dans ce didacticiel : [exemple](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/).

## <a name="next-steps"></a>Étapes suivantes

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]



<!-- Anchors. -->


<!-- URLs. -->
[Web Platform Installer]: http://go.microsoft.com/fwlink/?linkid=255386
[Portal]: http://manage.windowsazure.com/
