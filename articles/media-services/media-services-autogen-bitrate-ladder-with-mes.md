---
title: "tooauto d’Azure Media Encoder Standard aaaUse-générer une échelle de la vitesse de transmission | Documents Microsoft"
description: "Cette rubrique montre comment toouse Media Encoder Standard (MES) tooauto-générer une échelle de la vitesse de transmission en fonction de la résolution d’entrée hello et la vitesse de transmission. vitesse de transmission et la résolution d’entrée hello ne seront jamais dépassées. Par exemple, si l’entrée de hello est 720p à 3 Mbits/s, sortie sera restent 720p au mieux et commence à un taux inférieurs à 3 Mbits/s."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 63ed95da-1b82-44b0-b8ff-eebd535bc5c7
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: 5437f54ac28c42ddd4f9d1986549d6da6261c5da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
#  <a name="use-azure-media-encoder-standard-tooauto-generate-a-bitrate-ladder"></a>Utiliser Azure Media Encoder Standard tooauto-générer une échelle de la vitesse de transmission

## <a name="overview"></a>Vue d'ensemble

Cette rubrique montre comment toouse Media Encoder Standard (MES) tooauto-générer une échelle de la vitesse de transmission (paires de résolution de la vitesse de transmission) en fonction de la résolution d’entrée hello et la vitesse de transmission. Hello générée automatiquement la présélection ne dépasse jamais vitesse de transmission et de résolution de hello d’entrée. Par exemple, si l’entrée de hello est 720p à 3 Mbits/s, sortie sera restent 720p au mieux et commence à un taux inférieurs à 3 Mbits/s.

### <a name="encoding-for-streaming-only"></a>Encodage pour la diffusion en continu uniquement

Si votre objectif est de tooencode votre source vidéo uniquement pour la diffusion en continu, puis vous faut-il utiliser hello « Diffusion adaptative en continu » prédéfini lors de la création d’une tâche d’encodage. Lorsque vous utilisez hello **diffusion adaptative en continu** prédéfinis, encodeur MES hello sera intelligemment imposer une échelle de la vitesse de transmission. Toutefois, vous ne serez pas hello toocontrol en mesure de codage des coûts, car le service de hello détermine combien couches toouse et à quelle résolution. Vous pouvez voir des exemples de couches de sortie produits par MES suite à l’encodage avec hello **diffusion adaptative en continu** prédéfinie à la fin de hello de cette rubrique. Hello de sortie actif contiennent des fichiers MP4 où audio et vidéo ne sont pas entrelacées.

### <a name="encoding-for-streaming-and-progressive-download"></a>Encodage pour le téléchargement progressif et la diffusion en continu

Si votre objectif est de tooencode votre vidéo source pour la diffusion en continu, ainsi que des fichiers MP4 à tooproduce pour le téléchargement progressif, puis vous faut-il utiliser hello « Contenu adaptative MP4 à plusieurs débits » prédéfini lors de la création d’une tâche d’encodage. Lorsque vous utilisez hello **contenu adaptative MP4 à plusieurs débits** prédéfinis, encodeur MES hello applique hello même encodage logique comme indiqué ci-dessus, mais la ressource en sortie hello contiendra alors MP4 de fichiers audio et vidéo sont entrelacées. Vous pouvez utiliser un de ces fichiers MP4 (par exemple, hello version la plus récente à débit binaire) en tant qu’un fichier de téléchargement progressif.

## <a id="encoding_with_dotnet"></a>Encodage à l’aide du Kit de développement logiciel (SDK) .NET de Media Services

Hello, exemple de code suivant utilise hello tooperform de Media Services .NET SDK tâches suivantes :

- Création d’une tâche d’encodage.
- Obtient un encodeur Media Encoder Standard toohello de référence.
- Ajouter une tâche de toohello tâche codage et spécifiez toouse hello **diffusion adaptative en continu** prédéfini. 
- Créer un élément multimédia de sortie qui contiendra les actifs de hello encodé.
- Ajouter une événement Gestionnaire toocheck hello progression de la tâche.
- Envoi de la tâche de hello.

#### <a name="create-and-configure-a-visual-studio-project"></a>Créer et configurer un projet Visual Studio

Configurer votre environnement de développement et de remplir le fichier app.config de hello avec les informations de connexion, comme décrit dans [développement Media Services avec .NET](media-services-dotnet-how-to-use.md). 

#### <a name="example"></a>Exemple

    using System;
    using System.Configuration;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;

    namespace AdaptiveStreamingMESPresest
    {
        class Program
        {
        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
        ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
        ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        // Field for service context.
        private static CloudMediaContext _context = null;

        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            // Get an uploaded asset.
            var asset = _context.Assets.FirstOrDefault();

            // Encode and generate hello output using hello "Adaptive Streaming" preset.
            EncodeToAdaptiveBitrateMP4Set(asset);

            Console.ReadLine();
        }

        static public IAsset EncodeToAdaptiveBitrateMP4Set(IAsset asset)
        {
            // Declare a new job.
            IJob job = _context.Jobs.Create("Media Encoder Standard Job");

            // Get a media processor reference, and pass tooit hello name of hello 
            // processor toouse for hello specific task.
            IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

            // Create a task
            ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
            processor,
            "Adaptive Streaming",
            TaskOptions.None);

            // Specify hello input asset toobe encoded.
            task.InputAssets.Add(asset);
            // Add an output asset toocontain hello results of hello job. 
            // This output is specified as AssetCreationOptions.None, which 
            // means hello output asset is not encrypted. 
            task.OutputAssets.AddNew("Output asset",
            AssetCreationOptions.None);

            job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
            job.Submit();
            job.GetExecutionProgressTask(CancellationToken.None).Wait();

            return job.OutputMediaAssets[0];
        }
        private static void JobStateChanged(object sender, JobStateChangedEventArgs e)
        {
            Console.WriteLine("Job state changed event:");
            Console.WriteLine("  Previous state: " + e.PreviousState);
            Console.WriteLine("  Current state: " + e.CurrentState);
            switch (e.CurrentState)
            {
            case JobState.Finished:
                Console.WriteLine();
                Console.WriteLine("Job is finished. Please wait while local tasks or downloads complete...");
                break;
            case JobState.Canceling:
            case JobState.Queued:
            case JobState.Scheduled:
            case JobState.Processing:
                Console.WriteLine("Please wait...\n");
                break;
            case JobState.Canceled:
            case JobState.Error:

                // Cast sender as a job.
                IJob job = (IJob)sender;

                // Display or log error details as needed.
                break;
            default:
                break;
            }
        }
        private static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
        {
            var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
            ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

            if (processor == null)
            throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

            return processor;
        }
        }
    }

## <a id="output"></a>Sortie

Cette section présente trois exemples de couches de sortie produits par MES suite à l’encodage avec hello **diffusion adaptative en continu** prédéfini. 

### <a name="example-1"></a>Exemple 1
Une source avec une hauteur de « 1080 » et une fréquence d’images de « 29.970 » crée 6 couches vidéo :

|Couche|Hauteur|Largeur|Vitesse de transmission (Kbits/s)|
|---|---|---|---|
|1|1080|1920|6780|
|2|720|1 280|3520|
|3|540|960|2210|
|4|360|640|1150|
|5|270|480|720|
|6|180|320|380|

### <a name="example-2"></a>Exemple 2
Une source avec une hauteur de « 720 » et une fréquence d’images de « 23.970 » crée 5 couches vidéo :

|Couche|Hauteur|Largeur|Vitesse de transmission (Kbits/s)|
|---|---|---|---|
|1|720|1 280|2940|
|2|540|960|1850|
|3|360|640|960|
|4|270|480|600|
|5|180|320|320|

### <a name="example-3"></a>Exemple 3
Une source avec une hauteur de « 360 » et une fréquence d’images de « 29.970 » crée 3 couches vidéo :

|Couche|Hauteur|Largeur|Vitesse de transmission (Kbits/s)|
|---|---|---|---|
|1|360|640|700|
|2|270|480|440|
|3|180|320|230|
## <a name="media-services-learning-paths"></a>Parcours d’apprentissage de Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Voir aussi
[Vue d’ensemble de l’encodage de Media Services](media-services-encode-asset.md)

