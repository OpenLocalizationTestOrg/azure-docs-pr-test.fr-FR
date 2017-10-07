---
title: "aaaEncode un élément multimédia avec Media Encoder Standard à l’aide de .NET | Documents Microsoft"
description: "Cette rubrique montre comment toouse .NET tooencode un élément multimédia à l’aide de Media Encoder standard."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 03431b64-5518-478a-a1c2-1de345999274
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako;anilmur
ms.openlocfilehash: 25e274c3b67168f4afc8b8ab04af2d654c9dd6e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="encode-an-asset-with-media-encoder-standard-using-net"></a>Encoder un élément multimédia avec Media Encoder Standard à l’aide de .NET
Travaux d’encodage est une des opérations les plus courantes traitement hello dans Media Services. Vous créez des fichiers multimédias tooconvert travaux encodage à partir d’un tooanother de codage. Lorsque vous codez, vous pouvez utiliser hello encodeur multimédia intégré de Media Services. Vous pouvez également utiliser un encodeur fourni par un partenaire de Media Services ; encodeurs tiers sont disponibles via hello Azure Marketplace. 

Cette rubrique montre comment toouse .NET tooencode vos éléments multimédias avec Media Encoder Standard (MES). Encodeur de support Standard est configuré d’à l’aide d’une des présélections d’encodeur hello décrites [ici](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).

Il est recommandé de tooalways Encoder vos fichiers sources dans un ensemble de fichiers MP4 de débit adaptatif, puis la convertir hello ensemble toohello format souhaité à l’aide de hello [empaquetage dynamique](media-services-dynamic-packaging-overview.md). 

Si votre ressource de sortie est stockée sous forme chiffrée, vous devez configurer une stratégie de remise de ressources. Pour plus d'informations, consultez [Configuration de la stratégie de remise de ressources](media-services-dotnet-configure-asset-delivery-policy.md).

> [!NOTE]
> Produit MES avec un nom qui contient un fichier de sortie hello les 32 premiers caractères de hello nom de fichier d’entrée. nom de Hello est basé sur ce qui est spécifié dans le fichier de présélection hello. Par exemple, "FileName": "{NomBase}_{Index}{Extension}". {Basename} est remplacé par hello 32 premiers caractères du nom de fichier d’entrée hello.
> 
> 

### <a name="mes-formats"></a>Formats MES
[Formats et codecs](media-services-media-encoder-standard-formats.md)

### <a name="mes-presets"></a>Présélections MES
Encodeur de support Standard est configuré d’à l’aide d’une des présélections d’encodeur hello décrites [ici](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).

### <a name="input-and-output-metadata"></a>Métadonnées d’entrée et de sortie
Lorsque vous encodez un élément multimédia d’entrée (ou plusieurs éléments multimédias à l’aide de MES), vous obtenez une ressource en sortie à hello achèvement réussi de qui encoder la tâche. ressource en sortie Hello contient vidéo, audio, miniatures, manifeste, etc. selon hello valeur prédéfinie d’encodage que vous utilisez.

la ressource en sortie Hello contient également un fichier contenant des métadonnées sur l’élément multimédia d’entrée de hello. nom du fichier XML de métadonnées hello Hello a hello suivant le format : < id_ressource > _metadata.xml (par exemple, 41114ad3-eb5e - 4c 57-8d92-5354e2b7d4a4_metadata), où < id_ressource > est la valeur AssetId de hello de ressource en entrée hello. Hello schéma de ces métadonnées d’entrée XML décrit [ici](media-services-input-metadata-schema.md).

la ressource en sortie Hello contient également un fichier contenant des métadonnées sur l’élément multimédia de sortie hello. nom du fichier XML de métadonnées hello Hello a hello suivant le format : < nom_fichier_source > _manifest.xml (par exemple, BigBuckBunny_manifest.xml). schéma Hello de ces métadonnées de sortie XML est décrite [ici](media-services-output-metadata-schema.md).

Si vous souhaitez un des fichiers de métadonnées hello deux tooexamine, vous pouvez créer un localisateur SAS et télécharger l’ordinateur local de hello fichier tooyour. Vous trouverez un exemple montrant comment toocreate un localisateur SAS et télécharger un fichier à l’aide hello de Media Services .NET SDK Extensions.

## <a name="download-sample"></a>Charger l’exemple
Vous pouvez obtenir et exécuter un exemple qui montre comment tooencode avec MES de [ici](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/).

## <a name="net-sample-code"></a>Exemple de code .NET

Hello, exemple de code suivant utilise hello tooperform de Media Services .NET SDK tâches suivantes :

* Création d’une tâche d’encodage.
* Obtient un encodeur Media Encoder Standard toohello de référence.
* Spécifiez toouse hello [diffusion adaptative en continu](media-services-autogen-bitrate-ladder-with-mes.md) prédéfini. 
* Ajouter une tâche de toohello tâche encodage unique. 
* Spécifier une entrée de hello toobe asset encodé.
* Créer un élément multimédia de sortie qui contiendra les actifs de hello encodé.
* Ajouter une événement Gestionnaire toocheck hello progression de la tâche.
* Envoi de la tâche de hello.

#### <a name="create-and-configure-a-visual-studio-project"></a>Créer et configurer un projet Visual Studio

Configurer votre environnement de développement et de remplir le fichier app.config de hello avec les informations de connexion, comme décrit dans [développement Media Services avec .NET](media-services-dotnet-how-to-use.md). 

#### <a name="example"></a>Exemple 

        using System;
        using System.Linq;
        using System.Configuration;
        using System.IO;
        using System.Threading;
        using Microsoft.WindowsAzure.MediaServices.Client;

        namespace MediaEncoderStandardSample
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

## <a name="media-services-learning-paths"></a>Parcours d’apprentissage de Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a>Étapes suivantes
[La miniature toogenerate à l’aide de Media Encoder Standard avec .NET](media-services-dotnet-generate-thumbnail-with-mes.md)
[vue d’ensemble de Media Services d’encodage](media-services-encode-asset.md)

