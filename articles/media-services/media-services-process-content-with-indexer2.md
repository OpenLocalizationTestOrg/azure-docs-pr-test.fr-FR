---
title: "aaaIndexing des fichiers multimédias avec Azure Media Indexer 2 Aperçu | Documents Microsoft"
description: "Azure Media Indexer vous permet de toomake le contenu de votre recherche de fichiers multimédias et toogenerate une transcription en texte intégral de sous-titrage et les mots clés. Cette rubrique montre comment afficher un aperçu des toouse Media Indexer 2."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 85d25525-a498-44eb-ae3a-2ca5ceb8e53d
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/31/2017
ms.author: adsolank;juliako;
ms.openlocfilehash: f83fa0db58b828ffa29933d68ce108b4906dcd78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="indexing-media-files-with-azure-media-indexer-2-preview"></a>Indexation de fichiers multimédias avec Azure Media Indexer 2 Preview
## <a name="overview"></a>Vue d'ensemble
Hello **Azure Media Indexer 2 aperçu** le processeur multimédia (MP) vous permet de toomake des fichiers multimédias et contenu de recherche, ainsi que pour générer des pistes de sous-titres. Comparés toohello la version précédente de [Azure Media Indexer](media-services-index-content.md), **Azure Media Indexer 2 aperçu** effectue une indexation plus rapide et offre la prise en charge plus large. Les langues prises en charge incluent l’anglais, l’espagnol, le français, l’allemand, l’italien, le chinois (mandarin, simplifié), le portugais, l’arabe et le japonais.

Hello **Azure Media Indexer 2 aperçu** Pack d’administration est actuellement en version préliminaire.

Cette rubrique montre comment des travaux de l’indexation de toocreate avec **Azure Media Indexer 2 aperçu**.

> [!NOTE]
> Hello suivant considérations s’appliquent :
> 
> Indexer 2 n’est pas pris en charge dans Azure China et Azure Government.
> 
> Lors de l’indexation de contenu, assurez-vous que toouse des fichiers multimédias qui sont très clair (sans musique de fond, bruit, effets ou souffle de microphone). Voici quelques exemples de contenu approprié : des réunions, des conférences ou des présentations enregistrées. Hello contenu suivant peut ne pas convenir pour l’indexation : films, émissions de télévision n’est pas défini avec audio mixte et effets sonores, contenu mal enregistrement avec bruit de fond (souffle).
> 
> 

Cette rubrique fournit des détails sur **Azure Media Indexer 2 aperçu** et montre comment toouse avec Media Services SDK pour .NET

## <a name="input-and-output-files"></a>Fichiers d’entrée et de sortie
### <a name="input-files"></a>Fichiers d'entrée
Fichiers audio ou vidéo

### <a name="output-files"></a>Fichiers de sortie
Un travail d’indexation peut générer des fichiers de sous-titres Bonjour suivant formats :  

* **SAMI**
* **TTML**
* **WebVTT**

Les fichiers de sous-titres fermés dans ces formats peuvent être utilisés toomake audio et vidéo fichiers accessible toopeople malentendantes.

## <a name="task-configuration-preset"></a>Configuration de la tâche (préconfiguration)
Lors de la création d’une tâche d’indexation avec **Azure Media Indexer 2 Preview**, vous devez spécifier une présélection de configuration.

Hello JSON suivant définit les paramètres disponibles.

    {
      "version":"1.0",
      "Features":
        [
           {
           "Options": {
                "Formats":["WebVtt","ttml"],
                "Language":"enUs",
                "Type":"RecoOptions"
           },
           "Type":"SpReco"
        }]
    }

## <a name="supported-languages"></a>Langues prises en charge
Azure Media Indexer 2 en version préliminaire prend en charge vocale-texte hello suivant langues (lors de la spécification de nom de la langue hello dans la configuration de la tâche hello, utiliser le code de 4 caractères entre crochets comme indiqué ci-dessous) :

* Anglais [EnUs]
* Espagnol [EsEs]
* Chinois (mandarin, simplifié) [ZhCn]
* Français [FrFr]
* Allemand [DeDe]
* Italien [ItIt]
* Portugais [PtBr]
* Arabe (égyptien) [ArEg]
* Japonais [JaJp]
* Russe [RuRu]
* Anglais britannique [EnGb]
* Espagnol (Mexique) [EsMx] 

## <a name="supported-file-types"></a>Types de fichiers pris en charge

Pour plus d’informations sur les types de fichiers pris en charge, consultez hello [prise en charge des formats decodecs/](media-services-media-encoder-standard-formats.md#input-containerfile-formats) section.

## <a name="net-sample-code"></a>Exemple de code .NET

suivant de Hello programme montre comment :

1. Créer un élément multimédia et téléchargez un fichier multimédia en ressource de hello.
2. Créer une tâche avec une tâche d’indexation basée sur un fichier de configuration qui contient hello suivant présélection de json.
   
        {
          "version":"1.0",
          "Features":
            [
               {
               "Options": {
                    "Formats":["WebVtt","ttml"],
                    "Language":"enUs",
                    "Type":"RecoOptions"
               },
               "Type":"SpReco"
            }]
        }
3. Télécharger les fichiers de sortie hello. 
   
#### <a name="create-and-configure-a-visual-studio-project"></a>Créer et configurer un projet Visual Studio

Configurer votre environnement de développement et de remplir le fichier app.config de hello avec les informations de connexion, comme décrit dans [développement Media Services avec .NET](media-services-dotnet-how-to-use.md). 

#### <a name="example"></a>Exemple

    using System;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;
    using System.Threading.Tasks;

    namespace IndexContent
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

                // Run indexing job.
                var asset = RunIndexingJob(@"C:\supportFiles\Indexer\BigBuckBunny.mp4",
                                            @"C:\supportFiles\Indexer\config.json");

                // Download hello job output asset.
                DownloadAsset(asset, @"C:\supportFiles\Indexer\Output");
            }

            static IAsset RunIndexingJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload hello input media file toostorage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My Indexing Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My Indexing Job");

                // Get a reference tooAzure Media Indexer 2 Preview.
                string MediaProcessorName = "Azure Media Indexer 2 Preview";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from hello specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with hello encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My Indexing Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify hello input asset toobe indexed.
                task.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job.
                task.OutputAssets.AddNew("My Indexing Output Asset", AssetCreationOptions.None);

                // Use hello following event handler toocheck job progress.  
                job.StateChanged += new EventHandler<JobStateChangedEventArgs>(StateChanged);

                // Launch hello job.
                job.Submit();

                // Check job execution and wait for job toofinish.
                Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);

                progressJobTask.Wait();

                // If job state is Error, hello event handling
                // method for job progress should log errors.  Here we check
                // for error state and exit if needed.
                if (job.State == JobState.Error)
                {
                    ErrorDetail error = job.Tasks.First().ErrorDetails.First();
                    Console.WriteLine(string.Format("Error: {0}. {1}",
                                                    error.Code,
                                                    error.Message));
                    return null;
                }

                return job.OutputMediaAssets[0];
            }

            static IAsset CreateAssetAndUploadSingleFile(string filePath, string assetName, AssetCreationOptions options)
            {
                IAsset asset = _context.Assets.Create(assetName, options);

                var assetFile = asset.AssetFiles.Create(Path.GetFileName(filePath));
                assetFile.Upload(filePath);

                return asset;
            }

            static void DownloadAsset(IAsset asset, string outputDirectory)
            {
                foreach (IAssetFile file in asset.AssetFiles)
                {
                    file.Download(Path.Combine(outputDirectory, file.Name));
                }
            }

            static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
            {
                var processor = _context.MediaProcessors
                    .Where(p => p.Name == mediaProcessorName)
                    .ToList()
                    .OrderBy(p => new Version(p.Version))
                    .LastOrDefault();

                if (processor == null)
                    throw new ArgumentException(string.Format("Unknown media processor",
                                                               mediaProcessorName));

                return processor;
            }

            static private void StateChanged(object sender, JobStateChangedEventArgs e)
            {
                Console.WriteLine("Job state changed event:");
                Console.WriteLine("  Previous state: " + e.PreviousState);
                Console.WriteLine("  Current state: " + e.CurrentState);

                switch (e.CurrentState)
                {
                    case JobState.Finished:
                        Console.WriteLine();
                        Console.WriteLine("Job is finished.");
                        Console.WriteLine();
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
                        // LogJobStop(job.Id);
                        break;
                    default:
                        break;
                }
            }
        }
    }

## <a name="media-services-learning-paths"></a>Parcours d’apprentissage de Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a>Liens connexes
[Vue d’ensemble d’Azure Media Services Analytics](media-services-analytics-overview.md)

[Démonstrations Azure Media Analytics](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

