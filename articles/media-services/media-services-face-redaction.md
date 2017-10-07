---
title: faces aaaRedact avec Azure Media Analytique | Documents Microsoft
description: "Cette rubrique montre comment tooredact fait face avec analytique d’Azure media."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 5b6d8b8c-5f4d-4fef-b3d6-dc22c6b5a0f5
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako;
ms.openlocfilehash: 1f5688a8c6374151c526a9c702b904d8c3e46164
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="redact-faces-with-azure-media-analytics"></a>Éditer les visages avec Azure Media Analytique
## <a name="overview"></a>Vue d'ensemble
**Azure Media Redactor** est un [Azure Media Analytique](media-services-analytics-overview.md) processeur multimédia (MP) qui offre la rédaction de face évolutives dans le cloud de hello. Rédaction de face permet de vous toomodify votre vidéo dans faces de tooblur d’ordre d’individus sélectionnés. Vous pouvez choisir de service de rédaction face toouse hello dans les scénarios de sécurité et de médias public. Quelques minutes de film qui contient plusieurs polices peuvent prendre des heures tooredact manuellement, mais avec cette face hello de service des processus de rédaction nécessite quelques étapes simples. Pour plus d’informations, consultez [ce blog](https://azure.microsoft.com/blog/azure-media-redactor/).

Cette rubrique fournit des détails sur **Azure Media Redactor** et montre comment toouse avec Media Services SDK pour .NET.

Hello **Azure Media Redactor** Pack d’administration est actuellement en version préliminaire. Il est disponible dans toutes les régions Azure publiques, ainsi que dans les centres de données de Chine et du Gouvernement des États-Unis. Cette version préliminaire est actuellement disponible gratuitement. 

## <a name="face-redaction-modes"></a>Modes de rédaction de face
Rédaction visages utilise en détectant des faces dans chaque image de la vidéo et suivi du cadran de hello objet à la fois vers l’avant et vers l’arrière dans le temps, afin que hello même personne peut être rendue floue à partir des autres angles ainsi. Bonjour les processus automatisés rédaction sont très complexe et ne produisent pas toujours 100 % de la sortie souhaitée, c’est pourquoi que Analytique de support vous offre deux manières la sortie finale toomodify hello.

Mode Ajout tooa entièrement automatique, il est un flux de travail deux passes qui permet de hello sélection/désérialiser-selection des faces trouvées via une liste d’ID. En outre, toomake arbitraire par hello ajustements de frame du Pack d’administration utilise un fichier de métadonnées au format JSON. Ce flux de travail est divisé en modes **Analyser** et **Rédiger**. Vous pouvez combiner les deux modes de hello en un seul passage qui exécute les deux tâches en tâches ; Ce mode est appelé **combinée**.

### <a name="combined-mode"></a>Mode Combiné
Cela génère un mp4 rédigé automatiquement sans entrée manuelle.

| Étape | Nom de fichier | Remarques |
| --- | --- | --- |
| Élément multimédia d’entrée |foo.bar |Vidéo au format WMV, MOV ou MP4 |
| Configuration d’entrée |Job configuration preset |{'version':'1.0', 'options': {'mode':'combined'}} |
| Élément multimédia de sortie |foo_redacted.mp4 |Vidéo avec flou appliqué |

#### <a name="input-example"></a>Exemple d’entrée :
[regarder cette vidéo](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fed99001d-72ee-4f91-9fc0-cd530d0adbbc%2FDancing.mp4)

#### <a name="output-example"></a>Exemple de sortie :
[regarder cette vidéo](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fc6608001-e5da-429b-9ec8-d69d8f3bfc79%2Fdance_redacted.mp4)

### <a name="analyze-mode"></a>Mode Analyser
Hello **analyser** réussissent du flux de travail de deux passes hello accepte une entrée vidéo et génère un fichier JSON des emplacements de face et les images jpg de chaque détecté face.

| Étape | Nom de fichier | Remarques |
| --- | --- | --- |
| Élément multimédia d’entrée |foo.bar |Vidéo au format WMV, MPV ou MP4 |
| Configuration d’entrée |Job configuration preset |{'version':'1.0', 'options': {'mode':'analyze'}} |
| Élément multimédia de sortie |foo_annotations.json |Données d’annotation des emplacements de visage au format JSON. Cela peut être modifié par hello utilisateur toomodify hello flou des cadres. Voir l’exemple ci-dessous. |
| Élément multimédia de sortie |foo_thumb%06d.jpg [foo_thumb000001.jpg, foo_thumb000002.jpg] |Jpg rognée de chaque détecté face, où le nombre de hello indique labelId hello du cadran de hello |

#### <a name="output-example"></a>Exemple de sortie :

    {
      "version": 1,
      "timescale": 24000,
      "offset": 0,
      "framerate": 23.976,
      "width": 1280,
      "height": 720,
      "fragments": [
        {
          "start": 0,
          "duration": 48048,
          "interval": 1001,
          "events": [
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [
              {
                "index": 13,
                "id": 1138,
                "x": 0.29537,
                "y": -0.18987,
                "width": 0.36239,
                "height": 0.80335
              },
              {
                "index": 13,
                "id": 2028,
                "x": 0.60427,
                "y": 0.16098,
                "width": 0.26958,
                "height": 0.57943
              }
            ],

    … truncated

### <a name="redact-mode"></a>Mode Rédiger
deuxième passe de Hello du flux de travail hello prend un plus grand nombre d’entrées qui doivent être combinées en un seul élément multimédia.

Cela inclut une liste des ID tooblur hello d’origine et la vidéo annotations de hello JSON. Ce mode utilise hello annotations tooapply flou sur la vidéo d’entrée de hello.

Hello sortie de test d’analyse hello n’inclut pas les vidéo d’origine hello. Hello vidéo doit toobe chargé dans l’élément multimédia d’entrée de hello pour la tâche en mode de Redact hello et sélectionné comme fichier principal de hello.

| Étape | Nom de fichier | Remarques |
| --- | --- | --- |
| Élément multimédia d’entrée |foo.bar |Vidéo au format WMV, MPV ou MP4. Même vidéo que celle de l’étape 1. |
| Élément multimédia d’entrée |foo_annotations.json |Fichier de métadonnées d’annotations de la première phase, avec des modifications facultatives. |
| Élément multimédia d’entrée |foo_IDList.txt (facultatif) |Ligne facultatif liste séparée par des ID tooredact de face. Si ce champ est laissé vide, tous les visages sont floutés. |
| Configuration d’entrée |Job configuration preset |{'version':'1.0', 'options': {'mode':'redact'}} |
| Élément multimédia de sortie |foo_redacted.mp4 |Vidéo avec flou appliqué en fonction des annotations |

#### <a name="example-output"></a>Exemple de sortie
Il s’agit de sortie hello à partir d’un conjointe avec un code sélectionné.

[regarder cette vidéo](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fad6e24a2-4f9c-46ee-9fa7-bf05e20d19ac%2Fdance_redacted1.mp4)

Exemple : foo_IDList.txt
 
     1
     2
     3

## <a name="blur-types"></a>Types de flou

Bonjour **combinée** ou **Redact** mode, il existe 5 flou différents modes, vous pouvez choisir parmi via la configuration d’entrée de JSON hello : **faible**, **Med**, **Haute**, **déboguer**, et **noir**. Par défaut, **Med** (Moyen) est utilisé.

Vous pouvez trouver les exemples de hello flou types ci-dessous.

### <a name="example-json"></a>Exemple JSON :

    {'version':'1.0', 'options': {'Mode': 'Combined', 'BlurType': 'High'}}

#### <a name="low"></a>Faible

![Faible](./media/media-services-face-redaction/blur1.png)
 
#### <a name="med"></a>Med (Moyen)

![Med (Moyen)](./media/media-services-face-redaction/blur2.png)

#### <a name="high"></a>Élevé

![Élevé](./media/media-services-face-redaction/blur3.png)

#### <a name="debug"></a>Déboguer

![Déboguer](./media/media-services-face-redaction/blur4.png)

#### <a name="black"></a>Noir

![Noir](./media/media-services-face-redaction/blur5.png)

## <a name="elements-of-hello-output-json-file"></a>Éléments hello JSON du fichier de sortie

Hello rédaction du Pack d’administration fournit la détection de l’emplacement de haute précision face et de suivi permettant de détecter les visages de humaine too64 dans une image vidéo. Visages de face fournissent hello meilleurs résultats, lors de la face et de petites faces (inférieur ou égal à too24x24 pixels) est difficile.

[!INCLUDE [media-services-analytics-output-json](../../includes/media-services-analytics-output-json.md)]

## <a name="net-sample-code"></a>Exemple de code .NET

suivant de Hello programme montre comment :

1. Créer un élément multimédia et téléchargez un fichier multimédia en ressource de hello.
2. Créer une tâche avec une tâche de rédaction face basée sur un fichier de configuration qui contient hello suivant présélection de json. 
   
        {'version':'1.0', 'options': {'mode':'combined'}}
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

    namespace FaceRedaction
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

            // Run hello FaceRedaction job.
            var asset = RunFaceRedactionJob(@"C:\supportFiles\FaceRedaction\SomeFootage.mp4",
                        @"C:\supportFiles\FaceRedaction\config.json");

            // Download hello job output asset.
            DownloadAsset(asset, @"C:\supportFiles\FaceRedaction\Output");
        }

        static IAsset RunFaceRedactionJob(string inputMediaFilePath, string configurationFile)
        {
            // Create an asset and upload hello input media file toostorage.
            IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
            "My Face Redaction Input Asset",
            AssetCreationOptions.None);

            // Declare a new job.
            IJob job = _context.Jobs.Create("My Face Redaction Job");

            // Get a reference tooAzure Media Redactor.
            string MediaProcessorName = "Azure Media Redactor";

            var processor = GetLatestMediaProcessorByName(MediaProcessorName);

            // Read configuration from hello specified file.
            string configuration = File.ReadAllText(configurationFile);

            // Create a task with hello encoding details, using a string preset.
            ITask task = job.Tasks.AddNew("My Face Redaction Task",
            processor,
            configuration,
            TaskOptions.None);

            // Specify hello input asset.
            task.InputAssets.Add(asset);

            // Add an output asset toocontain hello results of hello job.
            task.OutputAssets.AddNew("My Face Redaction Output Asset", AssetCreationOptions.None);

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

## <a name="next-steps"></a>Étapes suivantes

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a>Liens connexes
[Vue d’ensemble d’Azure Media Services Analytics](media-services-analytics-overview.md)

[Démonstrations Azure Media Analytics](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

