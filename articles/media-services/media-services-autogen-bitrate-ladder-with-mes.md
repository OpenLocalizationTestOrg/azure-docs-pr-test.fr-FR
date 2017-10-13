---
title: "Utilisation d’Azure Media Encoder Standard pour générer automatiquement une échelle des vitesses de transmission | Microsoft Docs"
description: "Cette rubrique explique comment utiliser Media Encoder Standard (MES) pour générer automatiquement une échelle des vitesses de transmission basée sur la résolution d’entrée et la vitesse de transmission. La résolution d’entrée et la vitesse de transmission ne seront jamais dépassées. Par exemple, si l’entrée est 720p à 3 Mbits/s, la sortie restera à 720p maximum démarrera à des vitesses inférieures à 3 Mbits/s."
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
ms.openlocfilehash: b5616aa9f8b15ab576d914fbae89a56f64c27f4a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
#  <a name="use-azure-media-encoder-standard-to-auto-generate-a-bitrate-ladder"></a>Utilisation d’Azure Media Encoder Standard pour générer automatiquement une échelle des vitesses de transmission

## <a name="overview"></a>Vue d'ensemble

Cette rubrique explique comment utiliser Media Encoder Standard (MES) pour générer automatiquement une échelle des vitesses de transmission (paires vitesse-résolution) basée sur la résolution d’entrée et la vitesse de transmission. La présélection générée automatiquement ne dépassera jamais la résolution d’entrée et la vitesse de transmission. Par exemple, si l’entrée est 720p à 3 Mbits/s, la sortie restera à 720p maximum démarrera à des vitesses inférieures à 3 Mbits/s.

### <a name="encoding-for-streaming-only"></a>Encodage pour la diffusion en continu uniquement

Si votre objectif est d’encoder votre vidéo source uniquement pour la diffusion en continu, il vous faut alors utiliser la présélection « Diffusion adaptative en continu » lors de la création d’une tâche d’encodage. Lorsque vous utilisez la présélection **Diffusion adaptative**, l’encodeur MES limitera intelligemment l’échelle de vitesse de transmission. Mais vous ne pourrez pas contrôler les frais d’encodage car le service détermine le nombre de couches à utiliser et à quelle résolution. Vous pouvez consulter des exemples de couches de sortie produites par MES suite à un encodage avec la présélection **Diffusion adaptative** à la fin de cette rubrique. L’élément multimédia de sortie contiendra des fichiers MP4 où les flux audio et vidéo ne sont pas entrelacés.

### <a name="encoding-for-streaming-and-progressive-download"></a>Encodage pour le téléchargement progressif et la diffusion en continu

Si votre objectif est d’encoder votre vidéo source pour la diffusion en continu ainsi que pour produire des fichiers MP4 pour le téléchargement progressif, il vous faut utiliser la présélection « Contenu adaptatif MP4 à plusieurs débits » lors de la création d’une tâche d’encodage. Lorsque vous utilisez la présélection **Contenu adaptative MP4 à plusieurs débits**, l’encodeur MES s’applique la même logique de codage que celle indiquée ci-dessus, mais maintenant la ressource en sortie contient des fichiers MP4 avec les flux audio et vidéo entrelacés. Vous pouvez utiliser un de ces fichiers MP4 (par exemple, la version la plus élevée à débit binaire) en tant que fichier de téléchargement progressif.

## <a id="encoding_with_dotnet"></a>Encodage à l’aide du Kit de développement logiciel (SDK) .NET de Media Services

Le code suivant utilise le Kit de développement logiciel (SDK) .NET de Media Services pour effectuer les tâches suivantes :

- Création d’une tâche d’encodage.
- Obtention d’une référence à l’encodeur Media Encoder Standard.
- Ajout d’une tâche d’encodage au travail et spécification de l’option pour utiliser la présélection **Diffusion adaptative**. 
- Création d’un élément multimédia de sortie qui contiendra l’élément multimédia encodé.
- Ajout d’un gestionnaire d’événements pour vérifier la progression de la tâche.
- Envoyez le travail.

#### <a name="create-and-configure-a-visual-studio-project"></a>Créer et configurer un projet Visual Studio

Configurez votre environnement de développement et ajoutez des informations de connexion au fichier app.config selon la procédure décrite dans l’article [Développement Media Services avec .NET](media-services-dotnet-how-to-use.md). 

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
        // Read values from the App.config file.
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

            // Encode and generate the output using the "Adaptive Streaming" preset.
            EncodeToAdaptiveBitrateMP4Set(asset);

            Console.ReadLine();
        }

        static public IAsset EncodeToAdaptiveBitrateMP4Set(IAsset asset)
        {
            // Declare a new job.
            IJob job = _context.Jobs.Create("Media Encoder Standard Job");

            // Get a media processor reference, and pass to it the name of the 
            // processor to use for the specific task.
            IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

            // Create a task
            ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
            processor,
            "Adaptive Streaming",
            TaskOptions.None);

            // Specify the input asset to be encoded.
            task.InputAssets.Add(asset);
            // Add an output asset to contain the results of the job. 
            // This output is specified as AssetCreationOptions.None, which 
            // means the output asset is not encrypted. 
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

Cette section présente trois exemples de couches de sortie produits par MES suite à un encodage avec la présélection **Diffusion adaptative**. 

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

