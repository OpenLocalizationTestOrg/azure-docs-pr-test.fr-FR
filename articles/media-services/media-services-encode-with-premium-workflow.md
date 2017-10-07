---
title: "aaaAdvanced encodage avec Workflow d’encodeur multimédia Premium | Documents Microsoft"
description: "Découvrez comment tooencode avec Workflow d’encodeur multimédia Premium. Exemples de code sont écrits en c# et utilisent hello Media Services SDK pour .NET."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 0f4c87ac-810a-4d42-8df8-923dff2016c6
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: 5a1c3d019a5c8fbf9bda2da751a7eff4c4907d97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-encoding-with-media-encoder-premium-workflow"></a>Encodage avancé avec Media Encoder Premium Workflow
> [!NOTE]
> Le processeur multimédia Media Encoder Premium Workflow présenté dans cette rubrique n’est pas disponible en Chine.
>
>

Pour les questions relatives à Encoder Premium, envoyez un e-mail à mepd sur Microsoft.com.

## <a name="overview"></a>Vue d'ensemble
Microsoft Azure Media Services introduit hello **Workflow d’encodeur multimédia Premium** processeur multimédia. Ce processeur offre des fonctionnalités d’encodage avancées pour vos flux de travail à la demande premium.

Hello rubriques suivantes décrivent les détails associés trop**Workflow d’encodeur multimédia Premium**:

* [Formats pris en charge par hello Workflow d’encodeur multimédia Premium](media-services-premium-workflow-encoder-formats.md) – traite des formats de fichier hello et codecs pris en charge par **Workflow d’encodeur multimédia Premium**.
* [Vue d’ensemble et la comparaison d’Azure sur les encodeurs de média à la demande](media-services-encode-asset.md) compare hello capacités de codage de **Workflow d’encodeur multimédia Premium** et **Media Encoder Standard**.

Cette rubrique montre comment tooencode avec **Workflow d’encodeur multimédia Premium** à l’aide de .NET.

Encodage des tâches pour hello **Workflow d’encodeur multimédia Premium** nécessitent un fichier de configuration distinct, appelé fichier de flux de travail. Ces fichiers ont une extension de lettres et sont créés à l’aide de hello [le Concepteur de flux de travail](media-services-workflow-designer.md) outil.

Vous pouvez également obtenir par défaut de hello les fichiers de flux de travail [ici](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows). dossier de Hello contient également la description hello de ces fichiers.

fichiers de flux de travail de Hello doivent toobe téléchargé tooyour Media Services compte comme un élément multimédia, et cette ressource doit être passée toohello tâche de codage.

## <a name="create-and-configure-a-visual-studio-project"></a>Créer et configurer un projet Visual Studio

Configurer votre environnement de développement et de remplir le fichier app.config de hello avec les informations de connexion, comme décrit dans [développement Media Services avec .NET](media-services-dotnet-how-to-use.md). 

## <a name="encoding-example"></a>Exemple d’encodage

Hello exemple suivant montre comment tooencode avec **Workflow d’encodeur multimédia Premium**.

Hello suivant les étapes est effectuée :

1. Créez une ressource et téléchargez un fichier de flux de travail.
2. Créez une ressource et téléchargez un fichier multimédia source.
3. Obtenir un processeur multimédia de « Workflow Premium d’encodeur multimédia » hello.
4. Créez un travail et une tâche.

    Dans la plupart des cas, la chaîne de configuration hello pour la tâche hello est vide (comme dans hello exemple suivant). Il existe certains scénarios avancés (nécessitant les propriétés d’exécution tootooset dynamiquement) auquel cas vous souhaitez fournir une tâche de codage toohello de chaîne XML. La création d'une superposition, l'assemblage parallèle ou séquentiel multimédia, le sous-titrage sont des exemples de ces scénarios.
5. Ajoutez deux tâches de toohello d’éléments multimédias en entrée.

    1. 1er – actif du flux de travail hello.
    2. 2 – élément multimédia vidéo de hello.

    >[!NOTE]
    >tâche toohello avant multimédia hello doit être ajouté à actif du flux de travail Hello.
   chaîne de configuration Hello pour cette tâche doit être vide.
   
6. Envoi de la tâche de codage hello.

        using System;
        using System.Linq;
        using System.Configuration;
        using System.IO;
        using System.Threading;
        using System.Threading.Tasks;
        using Microsoft.WindowsAzure.MediaServices.Client;

        namespace MediaEncoderPremiumWorkflowSample
        {
            class Program
            {
                private static readonly string _AADTenantDomain =
                    ConfigurationManager.AppSettings["AADTenantDomain"];
                private static readonly string _RESTAPIEndpoint =
                    ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

                // Field for service context.
                private static CloudMediaContext _context = null;

                private static readonly string _supportFiles =
                    Path.GetFullPath(@"../..\Media");

                private static readonly string _workflowFilePath =
                    Path.GetFullPath(_supportFiles + @"\H264 Progressive Download MP4.workflow");

                private static readonly string _singleMP4InputFilePath =
                    Path.GetFullPath(_supportFiles + @"\BigBuckBunny.mp4");

                static void Main(string[] args)
                {
                    var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
                    var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

                    _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

                    var workflowAsset = CreateAssetAndUploadSingleFile(_workflowFilePath);
                    var videoAsset = CreateAssetAndUploadSingleFile(_singleMP4InputFilePath);
                    IAsset outputAsset = CreateEncodingJob(workflowAsset, videoAsset);

                }

                static public IAsset CreateAssetAndUploadSingleFile(string singleFilePath)
                {
                    var assetName = "UploadSingleFile_" + DateTime.UtcNow.ToString();
                    var asset = _context.Assets.Create(assetName, AssetCreationOptions.None);

                    var fileName = Path.GetFileName(singleFilePath);

                    var assetFile = asset.AssetFiles.Create(fileName);

                    Console.WriteLine("Created assetFile {0}", assetFile.Name);

                    Console.WriteLine("Upload {0}", assetFile.Name);

                    assetFile.Upload(singleFilePath);
                    Console.WriteLine("Done uploading {0}", assetFile.Name);

                    return asset;
                }

                static public IAsset CreateEncodingJob(IAsset workflow, IAsset video)
                {
                    // Declare a new job.
                    IJob job = _context.Jobs.Create("Premium Workflow encoding job");
                    // Get a media processor reference, and pass tooit hello name of the
                    // processor toouse for hello specific task.
                    IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Premium Workflow");

                    // Create a task with hello encoding details, using a string preset.
                    ITask task = job.Tasks.AddNew("Premium Workflow encoding task",
                        processor,
                        "",
                        TaskOptions.None);

                    // Specify hello input asset toobe encoded.
                    task.InputAssets.Add(workflow);
                    task.InputAssets.Add(video); // we add one asset
                                                 // Add an output asset toocontain hello results of hello job.
                                                 // This output is specified as AssetCreationOptions.None, which
                                                 // means hello output asset is not encrypted.
                    task.OutputAssets.AddNew("Output asset",
                        AssetCreationOptions.None);

                    // Use hello following event handler toocheck job progress.  
                    job.StateChanged += new
                            EventHandler<JobStateChangedEventArgs>(StateChanged);

                    // Launch hello job.
                    job.Submit();

                    // Check job execution and wait for job toofinish.
                    Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);
                    progressJobTask.Wait();

                    // If job state is Error hello event handling
                    // method for job progress should log errors.  Here we check
                    // for error state and exit if needed.
                    if (job.State == JobState.Error)
                    {
                        throw new Exception("\nExiting method due toojob error.");
                    }

                    return job.OutputMediaAssets[0];
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

Pour les questions relatives à Encoder Premium, envoyez un e-mail à mepd sur Microsoft.com.

## <a name="media-services-learning-paths"></a>Parcours d’apprentissage de Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
