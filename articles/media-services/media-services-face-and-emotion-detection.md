---
title: "aaaDetect émotion avec Azure Media Analytique et Face | Documents Microsoft"
description: "Cette rubrique montre comment toodetect fait face et émotions avec Azure Media Analytique."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 5ca4692c-23f1-451d-9d82-cbc8bf0fd707
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/18/2017
ms.author: milanga;juliako;
ms.openlocfilehash: f58d81d82dde08a694cdb4d92c6bab6a40a9c157
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="detect-face-and-emotion-with-azure-media-analytics"></a>Détection des visages et des émotions avec Azure Media Analytics
## <a name="overview"></a>Vue d'ensemble
Hello **Azure Media Face détecteur** le processeur multimédia (MP) vous permet de toocount, les mouvements de suivi et même la participation jauge audience et réaction via des expressions visages. Ce service présente deux fonctionnalités : 

* **Détection faciale**
  
    La détection faciale détecte et suit les visages humains au sein d’une vidéo. Plusieurs polices peuvent être détectées et par la suite être suivis comme ils sont en déplacement, avec hello heure et l’emplacement des métadonnées retournées dans un fichier JSON. Lors du suivi, il va tenter de toogive un toohello ID cohérent même sont confrontés lors de la personne de hello tourne autour de l’écran, même s’ils sont coupés ou laisser brièvement les frames de hello.
  
  > [!NOTE]
  > Ce service n’effectue pas la reconnaissance faciale. Une personne qui laisse le frame de hello ou devienne coupée pour trop longtemps recevra un nouvel ID lorsqu’elles retournent.
  > 
  > 
* **Détection d’émotions**
  
    Détection d’émotion est un composant facultatif de hello processeur multimédia de détection Face qui renvoie analysis sur plusieurs attributs émotionnels à partir de face hello détecté, y compris bonheur, leur, peur, colère et bien plus encore. 

Hello **Azure Media Face détecteur** Pack d’administration est actuellement en version préliminaire.

Cette rubrique fournit des détails sur **Azure Media Face détecteur** et montre comment toouse avec Media Services SDK pour .NET.

## <a name="face-detector-input-files"></a>Fichiers d’entrée du détecteur facial
Fichiers vidéo. Actuellement, hello suivant les formats est pris en charge : MP4 et WMV MOV.

## <a name="face-detector-output-files"></a>Fichiers de sortie du détecteur facial
API de détection et le suivi de la face Hello fournit la détection de l’emplacement de haute précision face et de suivi permettant de détecter les visages de humaine too64 dans une vidéo. Hello meilleurs résultats, lors de la face et de petites faces fournissent des visages de face (inférieur ou égal à too24x24 pixels) ne peut pas être aussi précises.

Hello faces détectés et de suivi sont retournées par les coordonnées (gauche, haut, largeur et hauteur) indiquant l’emplacement hello des faces dans l’image de hello en pixels, ainsi que pour un ID face numéro indiquant hello suivi de cette personne. Les numéros d’identification face sont tooreset susceptible d’engendrer des circonstances quand un visage de face hello est perdu ou superposée dans le cadre de hello, aboutissant à certaines personnes plusieurs ID lors de l’attribution.

## <a id="output_elements"></a>Éléments hello JSON du fichier de sortie

[!INCLUDE [media-services-analytics-output-json](../../includes/media-services-analytics-output-json.md)]

Détecteur de face utilise des techniques de fragmentation (où hello métadonnées peuvent être divisées en plusieurs segments de temps, vous pouvez télécharger ce que vous devez uniquement) et la segmentation (où les événements hello sont classifiées dans le cas où ils obtenir trop grandes). Des calculs simples, vous peuvent transformer les données de salutation. Par exemple, si un événement a démarré à 6 300 (cycles), avec une échelle de temps de 2 997 (cycles par seconde) et si la fréquence d’images est de 29,97 (images par seconde), alors :

* Démarrage/Échelle de temps = 2,1 secondes
* Secondes x fréquence d'images = 63 images

## <a name="face-detection-input-and-output-example"></a>Exemple d’entrée et de sortie de détection faciale
### <a name="input-video"></a>Vidéo d’entrée
[Vidéo d’entrée](http://ampdemo.azureedge.net/azuremediaplayer.html?url=https%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fc8834d9f-0b49-4b38-bcaf-ece2746f1972%2FMicrosoft%20Convergence%202015%20%20Keynote%20Highlights.ism%2Fmanifest&amp;autoplay=false)

### <a name="task-configuration-preset"></a>Configuration de la tâche (préconfiguration)
Lors de la création d’une tâche de vidéo **Azure Media Face Detector**, vous devez spécifier une présélection de configuration. Hello suivant présélection de configuration est uniquement pour la détection de visage.

    {
      "version":"1.0",
      "options":{
          "TrackingMode": "Fast"
      }
    }

#### <a name="attribute-descriptions"></a>Descriptions des attributs
| Nom de l’attribut | Description |
| --- | --- |
| Mode |Fast : traitement rapide, mais moins précis (par défaut).|

### <a name="json-output"></a>Sortie JSON
Hello, exemple de sortie JSON suivant a été tronquée.

    {
    "version": 1,
    "timescale": 30000,
    "offset": 0,
    "framerate": 29.97,
    "width": 1280,
    "height": 720,
    "fragments": [
        {
        "start": 0,
        "duration": 60060
        },
        {
        "start": 60060,
        "duration": 60060,
        "interval": 1001,
        "events": [
            [
            {
                "id": 0,
                "x": 0.519531,
                "y": 0.180556,
                "width": 0.0867188,
                "height": 0.154167
            }
            ],
            [
            {
                "id": 0,
                "x": 0.517969,
                "y": 0.181944,
                "width": 0.0867188,
                "height": 0.154167
            }
            ],
            [
            {
                "id": 0,
                "x": 0.517187,
                "y": 0.183333,
                "width": 0.0851562,
                "height": 0.151389
            }
            ],

        . . . 

## <a name="emotion-detection-input-and-output-example"></a>Exemple d’entrée et de sortie de détection d’émotion
### <a name="input-video"></a>Vidéo d’entrée
[Vidéo d’entrée](http://ampdemo.azureedge.net/azuremediaplayer.html?url=https%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fc8834d9f-0b49-4b38-bcaf-ece2746f1972%2FMicrosoft%20Convergence%202015%20%20Keynote%20Highlights.ism%2Fmanifest&amp;autoplay=false)

### <a name="task-configuration-preset"></a>Configuration de la tâche (préconfiguration)
Lors de la création d’une tâche de vidéo **Azure Media Face Detector**, vous devez spécifier une présélection de configuration. Hello suivant présélection de configuration spécifie toocreate que JSON en fonction de détection d’émotion hello.

    {
      "version": "1.0",
      "options": {
        "aggregateEmotionWindowMs": "987",
        "mode": "aggregateEmotion",
        "aggregateEmotionIntervalMs": "342"
      }
    }


#### <a name="attribute-descriptions"></a>Descriptions des attributs
| Nom de l’attribut | Description |
| --- | --- |
| Mode |Faces : détection faciale uniquement.<br/>PerFaceEmotion : retourne les valeurs d’émotion indépendamment pour chaque détection faciale.<br/>AggregateEmotion : retourne les valeurs d’émotion moyennes pour tous les visages dans l’image. |
| AggregateEmotionWindowMs |Utilisez cet attribut si le mode AggregateEmotion est sélectionné. Spécifie hello vidéo tooproduce utilisé chaque résultat d’agrégation, en millisecondes. |
| AggregateEmotionIntervalMs |Utilisez cet attribut si le mode AggregateEmotion est sélectionné. Spécifie quel agrégat tooproduce de fréquence des résultats. |

#### <a name="aggregate-defaults"></a>Valeurs d'agrégation par défaut
Ci-dessous sont valeurs recommandées pour l’agrégation hello et les paramètres d’intervalle. La valeur AggregateEmotionWindowMs doit être supérieure à AggregateEmotionIntervalMs.

|| Valeur(s) par défaut | Valeur(s) min | Valeur(s) max |
|--- | --- | --- | --- |
| AggregateEmotionWindowMs |0.5 |2 |0,25|
| AggregateEmotionIntervalMs |0.5 |1 |0,25|

### <a name="json-output"></a>Sortie JSON
Sortie JSON pour l’émotion agrégée (tronquée) :

    {
     "version": 1,
     "timescale": 30000,
     "offset": 0,
     "framerate": 29.97,
     "width": 1280,
     "height": 720,
     "fragments": [
       {
         "start": 0,
         "duration": 60060,
         "interval": 15015,
         "events": [
           [
             {
               "windowFaceDistribution": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               }
             }
           ],
           [
             {
               "windowFaceDistribution": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               }
             }
           ],
           [
             {
               "windowFaceDistribution": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               }
             }
           ],
           [
             {
               "windowFaceDistribution": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               }
             }
           ]
         ]
       },
       {
         "start": 60060,
         "duration": 60060,
         "interval": 15015,
         "events": [
           [
             {
               "windowFaceDistribution": {
                 "neutral": 1,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0.688541,
                 "happiness": 0.0586323,
                 "surprise": 0.227184,
                 "sadness": 0.00945675,
                 "anger": 0.00592107,
                 "disgust": 0.00154993,
                 "fear": 0.00450447,
                 "contempt": 0.0042109
               }
             }
           ],
           [
             {
               "windowFaceDistribution": {
                 "neutral": 1,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,

## <a name="limitations"></a>Limites
* Hello pris en charge les formats vidéo d’entrée incluent MP4 et WMV MOV.
* plage de tailles de police détectables Hello est 24 x 24 too2048x2048 pixels. faces Hello en dehors de cette plage ne sont pas détectées.
* Pour chaque vidéo, le nombre maximal de hello des faces retourné est 64.
* Certaines faces peut ne pas être détectés en raison de problèmes de tootechnical ; par exemple, très grandes face angles (head-pose) et occlusion volumineuse. Faces frontales et près frontal ont des résultats optimaux hello.

## <a name="net-sample-code"></a>Exemple de code .NET

suivant de Hello programme montre comment :

1. Créer un élément multimédia et téléchargez un fichier multimédia en ressource de hello.
2. Créer une tâche avec une tâche de détection de visage basée sur un fichier de configuration qui contient hello suivant présélection de json. 
   
        {
            "version": "1.0"
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

    namespace FaceDetection
    {
        class Program
        {
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

                // Run hello FaceDetection job.
                var asset = RunFaceDetectionJob(@"C:\supportFiles\FaceDetection\BigBuckBunny.mp4",
                                            @"C:\supportFiles\FaceDetection\config.json");

                // Download hello job output asset.
                DownloadAsset(asset, @"C:\supportFiles\FaceDetection\Output");
            }

            static IAsset RunFaceDetectionJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload hello input media file toostorage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My Face Detection Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My Face Detection Job");

                // Get a reference tooAzure Media Face Detector.
                string MediaProcessorName = "Azure Media Face Detector";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from hello specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with hello encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My Face Detection Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify hello input asset.
                task.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job.
                task.OutputAssets.AddNew("My Face Detectoion Output Asset", AssetCreationOptions.None);

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

[Démonstrations Azure Media Analytics](http://amslabs.azurewebsites.net/demos/Analytics.html)

