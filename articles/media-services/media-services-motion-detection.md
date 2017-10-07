---
title: les mouvements aaaDetect avec Azure Media Analytique | Documents Microsoft
description: "Bonjour permet de processeur (MP) détecteur de mouvement de média Azure media tooefficiently de vous identifient des sections d’intérêt dans une vidéo sinon long et se déroule normalement."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: d144f813-1a55-442f-a895-5c4cb6d0aeae
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/31/2017
ms.author: milanga;juliako;
ms.openlocfilehash: cb431375c92222053ed2239dd4e45767524dab68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="detect-motions-with-azure-media-analytics"></a>Détecter les mouvements avec Azure Media Analytics
## <a name="overview"></a>Vue d'ensemble
Hello **détecteur de mouvement Azure Media** permet de processeur (MP) support tooefficiently de vous identifient des sections d’intérêt dans une vidéo sinon long et se déroule normalement. Détection de mouvement peut être utilisée sur caméra statique enregistrements tooidentify sections de la vidéo de hello où se produit le mouvement. Il génère un fichier JSON contenant des métadonnées avec les horodateurs et hello englobant la région où l’événement de hello s’est produite.

Cible des flux vidéo de sécurité, cette technologie est mouvement en mesure de toocategorize dans les événements pertinents et des faux positifs, tels que des changements d’éclairage et les ombres. Ainsi, vous toogenerate les alertes de sécurité à partir de flux de l’appareil photo sans recevoir des messages indésirables avec les événements non pertinentes sans fin, tout en étant instants tooextract en mesure d’intérêt de vidéos de surveillance très longs.

Hello **détecteur de mouvement Azure Media** Pack d’administration est actuellement en version préliminaire.

Cette rubrique fournit des détails sur **détecteur de mouvement Azure Media** et montre comment toouse avec Media Services SDK pour .NET

## <a name="motion-detector-input-files"></a>Fichiers d’entrée du détecteur de mouvement
Fichiers vidéo. Actuellement, hello suivant les formats est pris en charge : MP4 et WMV MOV.

## <a name="task-configuration-preset"></a>Configuration de la tâche (préconfiguration)
Lors de la création d’une tâche de vidéo **Azure Media Motion Detector**, vous devez spécifier une présélection de configuration. 

### <a name="parameters"></a>Paramètres
Vous pouvez utiliser hello paramètres suivants :

| Nom | Options | Description | Default |
| --- | --- | --- | --- |
| sensitivityLevel |Chaîne : « low », « medium », « high » |Définit la sensibilité de hello niveau sur les mouvements est signalée. Ajustez ce montant tooadjust de faux positifs. |« medium » |
| frameSamplingValue |Entier positif |Définit la fréquence de hello sur lequel s’exécute algorithme. 1 = chaque trame, 2 = toutes les 2 trames, etc. |1 |
| detectLightChange |Booléen : « True », « False » |Définit si des changements d’éclairage sont signalés dans les résultats de hello |« False » |
| mergeTimeThreshold |Xs-time: Hh:mm:ss<br/>Exemple : 00:00:03 |Spécifie la fenêtre de temps hello entre les événements de mouvement où 2 événements seront combinées et signalés comme 1. |00:00:00 |
| detectionZones |Tableau de zones de détection :<br/>- Zone de détection est un tableau de 3 points ou plus<br/>-Point est x et y coordonnées de too1 0. |Décrit la liste hello de détection polygonale zones toobe est utilisé.<br/>Résultats seront signalés en tant qu’ID, avec hello tout d’abord un est 'id' avec des zones de hello : 0 |Zone unique qui traite de cadre hello dans son intégralité. |

### <a name="json-example"></a>Exemple JSON
    {
      "version": "1.0",
      "options": {
        "sensitivityLevel": "medium",
        "frameSamplingValue": 1,
        "detectLightChange": "False",
        "mergeTimeThreshold":
        "00:00:02",
        "detectionZones": [
          [
            {"x": 0, "y": 0},
            {"x": 0.5, "y": 0},
            {"x": 0, "y": 1}
           ],
          [
            {"x": 0.3, "y": 0.3},
            {"x": 0.55, "y": 0.3},
            {"x": 0.8, "y": 0.3},
            {"x": 0.8, "y": 0.55},
            {"x": 0.8, "y": 0.8},
            {"x": 0.55, "y": 0.8},
            {"x": 0.3, "y": 0.8},
            {"x": 0.3, "y": 0.55}
          ]
        ]
      }
    }


## <a name="motion-detector-output-files"></a>Fichiers de sortie du détecteur de mouvement
Une tâche de détection de mouvement renvoie un fichier JSON de la ressource en sortie hello qui décrit les alertes de mouvement hello, ainsi que leurs catégories, au sein de hello vidéo. fichier de Hello contient plus d’informations sur hello et la durée de mouvement détecté dans hello vidéo.

une fois qu’il existe des objets en mouvement dans une vidéo d’arrière-plan fixe (par exemple, une surveillance vidéo) Hello API de détecteur de mouvement fournit des indicateurs. Hello détecteur de mouvement est formé tooreduce fausses alertes, telles que l’éclairage et les modifications de clichés instantanés. Limitations actuelles des algorithmes de hello incluent les vidéos de vision de nuit, les objets semi-transparents et les petits objets.

### <a id="output_elements"></a>Éléments hello JSON du fichier de sortie
> [!NOTE]
> Dans la version la plus récente hello, format de sortie JSON hello a changé et peut représenter une modification avec rupture pour certains clients.
> 
> 

Hello tableau suivant décrit les éléments hello JSON du fichier de sortie.

| Élément | Description |
| --- | --- |
| Version |Cela fait référence version toohello Hello vidéo API. version actuelle de Hello est 2. |
| Échelle de temps |« Cycles » par seconde de la vidéo de hello. |
| Offset |décalage de temps Hello des horodatages dans « cycles ». Cette valeur sera toujours 0 dans la version 1.0 des API vidéo. Cette valeur est susceptible d’être modifiée dans les scénarios pris en charge ultérieurement. |
| Framerate |Images par seconde de hello vidéo. |
| Width, Height |Fait référence toohello largeur et hauteur de hello vidéo en pixels. |
| Démarrer |Hello démarrer timestamp dans « cycles ». |
| Duration |longueur de Hello d’événement hello, dans « cycles ». |
| Intervalle |intervalle de salutation de chaque entrée de l’événement hello, dans « cycles ». |
| Événements |Chaque fragment de l’événement contient un mouvement de hello détecté au sein de cette durée. |
| Type |Dans la version actuelle de hello, il est toujours « 2 » pour le mouvement générique. Cette étiquette donne un mouvement de toocategorize vidéo API hello flexibilité dans les futures versions. |
| RegionID |Comme expliqué ci-dessus, cette valeur sera toujours « 0 » dans la présente version. Cette étiquette donne un mouvement de toofind vidéo API hello flexibilité dans différentes régions dans les futures versions. |
| Régions |Désigne la zone toohello dans la vidéo où vous vous souciez de mouvement. <br/><br/>-« id » représente la zone de la région hello : dans cette version il existe un seul ID 0. <br/>-« type » représente la forme hello de région de hello vous souciez de mouvement. Pour l’instant, seules « rectangle » et « polygone » sont prises en charge.<br/> Si vous avez spécifié « rectangle », région de hello possède dimensions X, Y, largeur et hauteur. Hello X et Y coordonnées représentent les coordonnées XY hello angle supérieur gauche de région de hello dans une échelle normalisée de too1.0 0.0. hauteur et largeur de hello représentent la taille hello de région de hello dans une échelle normalisée de too1.0 0.0. Dans la version actuelle de hello, X, Y, largeur et hauteur sont toujours fixes au niveau 0, 0 et 1, 1. <br/>Si vous avez spécifié « polygone », région de hello possède les dimensions en points. <br/> |
| Fragments |les métadonnées Hello sont mémorisé en bloc dans différents segments appelés fragments. Chaque fragment contient des valeurs de début (start), de durée (duration), un numéro d’intervalle et des événements (event). Un fragment sans aucun événement signifie qu’aucun mouvement n’a été détecté pendant cette heure de début et la durée. |
| Crochets [] |Chaque support représente un intervalle de l’événement de hello. Les crochets vides pour cet intervalle signifient qu’aucun mouvement n’a été détecté. |
| emplacements |Cette nouvelle entrée sous événements répertorie l’emplacement hello où le mouvement de hello s’est produite. Il s’agit plus précis que les zones de détection hello. |

Hello Voici un exemple de sortie JSON

    {
      "version": 2,
      "timescale": 23976,
      "offset": 0,
      "framerate": 24,
      "width": 1280,
      "height": 720,
      "regions": [
        {
          "id": 0,
          "type": "polygon",
          "points": [{'x': 0, 'y': 0},
            {'x': 0.5, 'y': 0},
            {'x': 0, 'y': 1}]
        }
      ],
      "fragments": [
        {
          "start": 0,
          "duration": 226765
        },
        {
          "start": 226765,
          "duration": 47952,
          "interval": 999,
          "events": [
            [
              {
                "type": 2,
                "typeName": "motion",
                "locations": [
                  {
                    "x": 0.004184,
                    "y": 0.007463,
                    "width": 0.991667,
                    "height": 0.985185
                  }
                ],
                "regionId": 0
              }
            ],

    …
## <a name="limitations"></a>Limites
* Hello pris en charge les formats vidéo d’entrée incluent MP4 et WMV MOV.
* La détection de mouvement est optimisée pour les vidéos dont l’arrière-plan est fixe. algorithme de Hello se concentre sur la réduction de fausses alertes, telles que des changements d’éclairage et les ombres.
* Certains mouvement peut ne pas être détecté en raison de problèmes de tootechnical ; par exemple, vidéos de vision de nuit, les objets semi-transparents et petits objets.

## <a name="net-sample-code"></a>Exemple de code .NET

suivant de Hello programme montre comment :

1. Créer un élément multimédia et téléchargez un fichier multimédia en ressource de hello.
2. Créer une tâche avec une tâche de détection de mouvement vidéo basée sur un fichier de configuration qui contient hello suivant présélection de json. 
   
        {
          "Version": "1.0",
          "Options": {
            "SensitivityLevel": "medium",
            "FrameSamplingValue": 1,
            "DetectLightChange": "False",
            "MergeTimeThreshold":
            "00:00:02",
            "DetectionZones": [
              [
                {"x": 0, "y": 0},
                {"x": 0.5, "y": 0},
                {"x": 0, "y": 1}
               ],
              [
                {"x": 0.3, "y": 0.3},
                {"x": 0.55, "y": 0.3},
                {"x": 0.8, "y": 0.3},
                {"x": 0.8, "y": 0.55},
                {"x": 0.8, "y": 0.8},
                {"x": 0.55, "y": 0.8},
                {"x": 0.3, "y": 0.8},
                {"x": 0.3, "y": 0.55}
              ]
            ]
          }
        }
3. Télécharger les fichiers JSON de sortie hello. 

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

    namespace VideoMotionDetection
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

                // Run hello VideoMotionDetection job.
                var asset = RunVideoMotionDetectionJob(@"C:\supportFiles\VideoMotionDetection\BigBuckBunny.mp4",
                                            @"C:\supportFiles\VideoMotionDetection\config.json");

                // Download hello job output asset.
                DownloadAsset(asset, @"C:\supportFiles\VideoMotionDetection\Output");
            }

            static IAsset RunVideoMotionDetectionJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload hello input media file toostorage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My Video Motion Detection Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My Video Motion Detection Job");

                // Get a reference tooAzure Media Motion Detector.
                string MediaProcessorName = "Azure Media Motion Detector";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from hello specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with hello encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My Video Motion Detection Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify hello input asset.
                task.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job.
                task.OutputAssets.AddNew("My Video Motion Detectoion Output Asset", AssetCreationOptions.None);

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
[Blog Azure Media Services Motion Detector](https://azure.microsoft.com/blog/motion-detector-update/)

[Vue d’ensemble d’Azure Media Services Analytics](media-services-analytics-overview.md)

[Démonstrations Azure Media Analytics](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

