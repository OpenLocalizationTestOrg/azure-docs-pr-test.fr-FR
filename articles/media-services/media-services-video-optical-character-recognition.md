---
title: texte aaaDigitize avec Azure Media Analytique OCR | Documents Microsoft
description: "Azure Media d’Analytique OCR (reconnaissance optique des caractères) vous permet de tooconvert le contenu de texte dans des fichiers vidéo en texte numérique interrogeable modifiable.  Cela vous permet d’extraction de hello tooautomate de métadonnées significatives à partir de signal vidéo de hello de votre support."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 307c196e-3a50-4f4b-b982-51585448ffc6
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: 0476c3ba3942b2c5182a34a429909adbf5c75ac9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-media-analytics-tooconvert-text-content-in-video-files-into-digital-text"></a>Utiliser le contenu de texte tooconvert Azure Media Analytique dans les fichiers vidéos en texte numérique
## <a name="overview"></a>Vue d'ensemble
Si vous devez tooextract texte contenu à partir de vos fichiers vidéo et générez un texte numérique modifiable, la recherche, vous devez utiliser Azure Media Analytique OCR (reconnaissance optique des caractères). Ce processeur multimédia Azure détecte le contenu texte de vos fichiers vidéo et génère les fichiers texte à utiliser. OCR permet de vous tooautomate hello d’extraction de métadonnées significatives à partir de signal vidéo de hello de votre support.

Lorsqu’il est utilisé conjointement avec un moteur de recherche, vous pouvez facilement votre support d’index en texte et améliorer la détectabilité hello de votre contenu. Cela est particulièrement utile dans une vidéo contenant beaucoup de texte, comme un enregistrement vidéo ou une capture d’écran de diaporama. Hello processeur OCR Azure est optimisé pour le texte numérique.

Hello **Azure Media OCR** processeur multimédia est actuellement en version préliminaire.

Cette rubrique fournit des détails sur **Azure Media OCR** et montre comment toouse avec Media Services SDK pour .NET. Pour plus d’informations et d’exemples, consultez [ce blog](https://azure.microsoft.com/blog/announcing-video-ocr-public-preview-new-config/).

## <a name="ocr-input-files"></a>Fichiers d'entrée OCR
Fichiers vidéo. Actuellement, hello suivant les formats est pris en charge : MP4 et WMV MOV.

## <a name="task-configuration"></a>Configuration de la tâche
Configuration de la tâche (préconfiguration). Lors de la création d’une tâche **Azure Media OCR**, vous devez spécifier une présélection de configuration avec JSON ou XML. 

>[!NOTE]
>moteur de reconnaissance optique des caractères Hello n’accepte qu’une région de l’image avec des pixels toomaximum 32000 40 pixels minimale comme une entrée valide dans les deux hauteur/largeur.
>

### <a name="attribute-descriptions"></a>Descriptions des attributs
| Nom de l’attribut | Description |
| --- | --- |
|AdvancedOutput| Si vous définissez AdvancedOutput tootrue, la sortie JSON hello contiendra les données positionnelles pour chaque mot (dans Ajout toophrases et régions). Si vous ne souhaitez pas toosee ces détails, définissez hello indicateur toofalse. valeur par défaut de Hello est false. Pour plus d’informations, consultez [ce blog](https://azure.microsoft.com/blog/azure-media-ocr-simplified-output/).|
| language |(facultatif) décrit le langage hello du texte pour le toolook. Hello suivantes : détection automatique (par défaut), arabe, ChineseSimplified, sait, tchèque danois, néerlandais, anglais, finnois, Français, allemand, grec, hongrois, italien, japonais, coréen, norvégien, polonais, portugais, roumain, russe, SerbianCyrillic, SerbianLatin, slovaque, espagnol, suédois, turc. |
| TextOrientation |(facultatif) décrit l’orientation de hello du texte pour le toolook.  « Gauche » signifie que hello en haut de toutes les lettres est pointé vers hello gauche.  Par défaut, le texte peut être affiché en mode « Up » (comme dans un livre).  Hello suivantes : détection automatique (par défaut), haut, droite, bas, gauche. |
| TimeInterval |(facultatif) décrit le taux d’échantillonnage de hello.  La valeur par défaut est chaque demie seconde.<br/>Format JSON – HH:mm:ss.SSS (par défaut : 00:00:00.500)<br/>Format XML – durée de la primitive W3C XSD (par défaut PT0.5) |
| DetectRegions |(facultatif) Tableau d’objets DetectRegion spécifiant des zones dans les images vidéo hello dans le texte toodetect.<br/>Un objet DetectRegion est constitué de hello quatre valeurs d’entier suivantes :<br/>Gauche – pixels à partir de la marge de gauche hello<br/>Haut – pixels à partir de la marge supérieure hello<br/>Largeur : la largeur de la région de hello en pixels<br/>Hauteur – la hauteur de la région de hello en pixels |

#### <a name="json-preset-example"></a>Exemple de présélection JSON

    {
        "Version":1.0, 
        "Options": 
        {
            "AdvancedOutput":"true",
            "Language":"English", 
            "TimeInterval":"00:00:01.5",
            "TextOrientation":"Up",
            "DetectRegions": [
                    {
                       "Left": 10,
                       "Top": 10,
                       "Width": 100,
                       "Height": 50
                    }
             ]
        }
    }


#### <a name="xml-preset-example"></a>Exemple de présélection XML
    <?xml version=""1.0"" encoding=""utf-16""?>
    <VideoOcrPreset xmlns:xsi=""http://www.w3.org/2001/XMLSchema-instance"" xmlns:xsd=""http://www.w3.org/2001/XMLSchema"" Version=""1.0"" xmlns=""http://www.windowsazure.com/media/encoding/Preset/2014/03"">
      <Options>
         <AdvancedOutput>true</AdvancedOutput>
         <Language>English</Language>
         <TimeInterval>PT1.5S</TimeInterval>
         <DetectRegions>
             <DetectRegion>
                   <Left>10</Left>
                   <Top>10</Top>
                   <Width>100</Width>
                   <Height>50</Height>
            </DetectRegion>
       </DetectRegions>
       <TextOrientation>Up</TextOrientation>
      </Options>
    </VideoOcrPreset>

## <a name="ocr-output-files"></a>Fichiers de sortie OCR
sortie Hello de processeur multimédia de OCR hello est un fichier JSON.

### <a name="elements-of-hello-output-json-file"></a>Éléments hello JSON du fichier de sortie
Hello OCR vidéo sortie fournit des données de temps segmenté sur les caractères de hello ont été trouvés dans votre vidéo.  Vous pouvez utiliser des attributs tels que la langue ou l’orientation dans toohone exactement les mots hello qui vous intéressent analyse. 

sortie de Hello contient hello suivant d’attributs :

| Élément | Description |
| --- | --- |
| Échelle de temps |« cycles » par seconde de la vidéo de hello |
| Offset |décalage des horodatages. Cette valeur sera toujours 0 dans la version 1.0 des API vidéo. |
| Framerate |Images par seconde de hello vidéo |
| width |largeur de la vidéo en pixels de hello |
| height |hauteur de la vidéo en pixels de hello |
| Fragments |tableau de segments de durée de vidéo dans le hello métadonnées sont mémorisé en bloc |
| start |heure de début d’un fragment en « cycles » |
| duration |durée d’un fragment en « cycles » |
| interval |intervalle de chaque événement dans hello donné fragment |
| événements |tableau contenant des régions |
| region |objet représentant des mots ou expressions détectés |
| Langage |langue du texte hello détecté dans une région |
| orientation |orientation du texte hello détecté dans une région |
| lignes |tableau de lignes de texte détecté dans une région |
| texte |texte Hello |

### <a name="json-output-example"></a>Exemple de sortie JSON
Hello exemple de sortie suivant contient des informations générales vidéo hello et plusieurs fragments vidéo. Dans chaque fragment de vidéo, il contient toutes les régions sont détectée par le Pack d’administration OCR avec le langage de hello et son orientation de texte. région de Hello contient également toutes les lignes dans cette zone de texte, position de ligne hello et chaque mot d’informations (contenu word, position et confiance) dans cette ligne de la ligne hello word. Hello suit est un exemple et placer des commentaires en ligne.

    {
        "version": 1, 
        "timescale": 90000, 
        "offset": 0, 
        "framerate": 30, 
        "width": 640, 
        "height": 480,  // general video information
        "fragments": [
            {
                "start": 0, 
                "duration": 180000, 
                "interval": 90000,  // hello time information about this fragment
                "events": [
                    [
                       { 
                            "region": { // hello detected region array in this fragment 
                                "language": "English",  // region language
                                "orientation": "Up",  // text orientation
                                "lines": [  // line information array in this region, including hello text and hello position
                                    {
                                        "text": "One Two", 
                                        "left": 10, 
                                        "top": 10, 
                                        "right": 210, 
                                        "bottom": 110, 
                                        "word": [  // word information array in this line
                                            {
                                                "text": "One", 
                                                "left": 10, 
                                                "top": 10, 
                                                "right": 110, 
                                                "bottom": 110, 
                                                "confidence": 900
                                            }, 
                                            {
                                                "text": "Two", 
                                                "left": 110, 
                                                "top": 10, 
                                                "right": 210, 
                                                "bottom": 110, 
                                                "confidence": 910
                                            }
                                        ]
                                    }
                                ]
                            }
                        }
                    ]
                ]
            }
        ]
    }

## <a name="net-sample-code"></a>Exemple de code .NET

suivant de Hello programme montre comment :

1. Créer un élément multimédia et téléchargez un fichier multimédia en ressource de hello.
2. Créer un travail avec un fichier de configuration OCR/prédéfini.
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

    namespace OCR
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

                // Run hello OCR job.
                var asset = RunOCRJob(@"C:\supportFiles\OCR\presentation.mp4",
                                            @"C:\supportFiles\OCR\config.json");

                // Download hello job output asset.
                DownloadAsset(asset, @"C:\supportFiles\OCR\Output");
            }

            static IAsset RunOCRJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload hello input media file toostorage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My OCR Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My OCR Job");

                // Get a reference tooAzure Media OCR.
                string MediaProcessorName = "Azure Media OCR";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from hello specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with hello encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My OCR Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify hello input asset.
                task.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job.
                task.OutputAssets.AddNew("My OCR Output Asset", AssetCreationOptions.None);

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

