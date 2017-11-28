---
title: "aaaIndexing des fichiers multimédias avec Azure Media Indexer"
description: "Azure Media Indexer vous permet de toomake le contenu de votre recherche de fichiers multimédias et toogenerate une transcription en texte intégral de sous-titrage et les mots clés. Cette rubrique montre comment toouse Media Indexer."
services: media-services
documentationcenter: 
author: Asolanki
manager: cfowler
editor: 
ms.assetid: 827a56b2-58a5-4044-8d5c-3e5356488271
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/20/2017
ms.author: adsolank;juliako;johndeu
ms.openlocfilehash: c1bed774e302e61ca3510668645dc2015b434a0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="indexing-media-files-with-azure-media-indexer"></a>Indexation de fichiers multimédias avec Azure Media Indexer
Azure Media Indexer vous permet de toomake le contenu de votre recherche de fichiers multimédias et toogenerate une transcription en texte intégral de sous-titrage et les mots clés. Vous pouvez traiter un fichier multimédia ou plusieurs dans un lot.  

> [!IMPORTANT]
> Lors de l’indexation de contenu, assurez-vous que toouse des fichiers multimédias qui sont très clair (sans musique de fond, bruit, effets ou souffle de microphone). Voici quelques exemples de contenu approprié : des réunions, des conférences ou des présentations enregistrées. Hello contenu suivant peut ne pas convenir pour l’indexation : films, émissions de télévision n’est pas défini avec audio mixte et effets sonores, contenu mal enregistrement avec bruit de fond (souffle).
> 
> 

Un travail d’indexation peut générer hello suivant sorties :

* Fichiers de sous-titres Bonjour suivant formats : **SAMI**, **TTML**, et **WebVTT**.
  
    Fichiers de sous-titres contiennent une balise appelée des raisons de reconnaissance, les scores d’un travail d’indexation en fonction de comment reconnaissable vocale hello dans la vidéo source de hello est.  Vous pouvez utiliser la valeur hello raisons de reconnaissance tooscreen des fichiers de sortie de la facilité d’utilisation. Un faible score signifie mauvais résultats d’indexation en raison de la qualité de tooaudio.
* Un fichier de mot-clé(XML).
* Un fichier blob d’indexation audio (AIB) à utiliser avec SQL Server.
  
    Pour plus d’informations, consultez [Utilisation de fichiers AIB avec Azure Media Indexer et SQL Server](https://azure.microsoft.com/blog/2014/11/03/using-aib-files-with-azure-media-indexer-and-sql-server/).

Cette rubrique montre comment l’indexation de toocreate travaux trop**indexer un élément multimédia** et **plusieurs fichiers d’Index**.

Bonjour Azure Media Indexer mises à jour récentes, consultez [blogs de Media Services](#preset).

## <a name="using-configuration-and-manifest-files-for-indexing-tasks"></a>Utilisation des fichiers de configuration et manifeste pour l’indexation des tâches
Vous pouvez définir plus de détails pour vos tâches d’indexation en utilisant une configuration de tâche. Par exemple, vous pouvez spécifier quels toouse de métadonnées de votre fichier multimédia. Ces métadonnées sont utilisées par tooexpand de moteur de langage hello son vocabulaire et améliore considérablement la précision de la reconnaissance vocale hello.  Vous est également en mesure de toospecify vos fichiers de sortie souhaité.

Vous pouvez également traiter plusieurs fichiers multimédias à la fois à l’aide d’un fichier manifeste.

Pour plus d’informations, consultez [Présélection de tâches pour Azure Media Indexer](https://msdn.microsoft.com/library/dn783454.aspx).

## <a name="index-an-asset"></a>Indexation d’une ressource
Hello méthode ci-dessous télécharge un fichier multimédia comme un élément multimédia et crée un élément multimédia de travail tooindex hello.

Notez que si aucun fichier de configuration n’est spécifié, fichier de média hello sera annexé avec tous les paramètres par défaut.

    static bool RunIndexingJob(string inputMediaFilePath, string outputFolder, string configurationFile = "")
    {
        // Create an asset and upload hello input media file toostorage.
        IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
            "My Indexing Input Asset",
            AssetCreationOptions.None);

        // Declare a new job.
        IJob job = _context.Jobs.Create("My Indexing Job");

        // Get a reference toohello Azure Media Indexer.
        string MediaProcessorName = "Azure Media Indexer";
        IMediaProcessor processor = GetLatestMediaProcessorByName(MediaProcessorName);

        // Read configuration from file if specified.
        string configuration = string.IsNullOrEmpty(configurationFile) ? "" : File.ReadAllText(configurationFile);

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
            Console.WriteLine("Exiting method due toojob error.");
            return false;
        }

        // Download hello job outputs.
        DownloadAsset(task.OutputAssets.First(), outputFolder);

        return true;
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
<!-- __ -->
### <a id="output_files"></a>Fichiers de sortie
Par défaut, un travail d’indexation génère hello les fichiers de sortie suivants. Hello fichiers seront stockés dans la première ressource en sortie hello.

Lorsqu’il existe plusieurs fichiers multimédias d’entrée, indexeur génère un fichier manifeste pour les sorties de travail hello, nommé « JobResult.txt ». Pour chaque fichier multimédia d’entrée, hello résultant AIB, SAMI, TTML, WebVTT et fichiers de mot clé, sont séquentiellement numérotés et nommées à l’aide de hello « Alias ».

| Nom de fichier | Description |
| --- | --- |
| **InputFileName.aib** |Fichier blob d’indexation audio. <br/><br/> Un fichier blob d’indexation audio (AIB) est un fichier binaire qui peut être recherché dans le serveur Microsoft SQL à l’aide de la recherche de texte intégral.  fichier AIB de Hello est plus performante que les fichiers de légende simple hello, car il contient des alternatives pour chaque mot, ce qui permet une expérience plus riche de la recherche. <br/> <br/>Elle nécessite l’installation de hello du module complémentaire Indexer SQL de hello sur un ordinateur exécutant Microsoft SQL server 2008 ou version ultérieur. Recherche en texte intégral serveur recherche hello AIB à l’aide de Microsoft SQL fournit des résultats plus précis que recherche hello fermé les fichiers de légende générés par WAMI. Il s’agit, car hello AIB contient des alternatives prononciation similaire, tandis que hello fermé les fichiers de légende contient hello plus élevé en toute confiance word pour chaque segment de données audio de hello. Si la recherche des mots revêt une importance parlé, il est recommandé toouse hello fichier AIB conjointement avec Microsoft SQL Server.<br/><br/> toodownload hello module complémentaire, cliquez sur <a href="http://aka.ms/indexersql">module complémentaire de Azure Media Indexer SQL</a>. <br/><br/>Il est également possible de tooutilize autres moteurs de recherche tels que hello d’index Apache Lucene/Solr toosimply vidéo basées sur la légende de hello fermé et le mot clé des fichiers XML, mais cela entraîne des résultats moins précis. |
| **InputFileName.smi**<br/>**InputFileName.ttml**<br/>**InputFileName.vtt** |Fichiers de sous-titres (CC) aux formats SAMI, TTML et WebVTT.<br/><br/>Ils peuvent être utilisés toomake audio et vidéo de fichiers accessible toopeople malentendantes.<br/><br/>Les fichiers de légende fermés contiennent une balise appelée <b>raisons de reconnaissance</b> qui évalue un travail d’indexation en fonction de comment reconnaissable vocale hello dans la vidéo source de hello est.  Vous pouvez utiliser la valeur hello <b>raisons de reconnaissance</b> tooscreen facilité d’utilisation dans les fichiers de sortie. Un faible score signifie mauvais résultats d’indexation en raison de la qualité de tooaudio. |
| **InputFileName.kw.xml<br/>InputFileName.info** |Fichiers de mots clés et d’informations. <br/><br/>Fichier de mot clé est un fichier XML qui contient des mots clés extraits à partir du contenu de reconnaissance vocale hello, avec la fréquence et les informations de décalage. <br/><br/>Un fichier d’informations est un fichier de texte brut qui contient des informations précises sur chaque terme reconnu. première ligne de Hello est spécial et contient le score de raisons de reconnaissance hello. Chaque ligne suivante est une liste de séparés par des tabulations de hello données suivantes : démarrer l’heure, heure de fin, mot/expression, en toute confiance. les durées de Hello sont exprimées en secondes et en toute confiance hello est fourni en tant que nombre de 0-1. <br/><br/>Exemple de ligne : "1.20    1.45    word    0.67" <br/><br/>Ces fichiers peuvent être utilisés pour de nombreuses fins, par exemple, tooperform analytique de reconnaissance vocale, ou toosearch exposé moteurs tels que Bing, Google ou Microsoft SharePoint toomake hello fichiers multimédias plus détectables, ou même utilisé toodeliver annonces plus pertinentes. |
| **JobResult.txt** |Manifeste de sortie présente uniquement lorsque l’indexation de plusieurs fichiers, contenant hello informations suivantes :<br/><br/><table border="1"><tr><th>InputFile</th><th>Alias</th><th>MediaLength</th><th>Erreur</th></tr><tr><td>a.mp4</td><td>Media_1</td><td>300</td><td>0</td></tr><tr><td>b.mp4</td><td>Media_2</td><td>0</td><td>3000</td></tr><tr><td>c.mp4</td><td>Media_3</td><td>600</td><td>0</td></tr></table><br/> |

Si tous les fichiers multimédias d’entrée sont correctement indexées, la tâche d’indexation hello échoue avec le code d’erreur 4000. Pour plus d’informations, consultez les [codes d’erreur](#error_codes).

## <a name="index-multiple-files"></a>indexer plusieurs fichiers
Bonjour méthode télécharge plusieurs fichiers multimédias en tant qu’un élément multimédia et crée un travail tooindex tous ces fichiers dans un lot.

Un fichier manifeste avec l’extension .lst de hello est créé et téléchargé dans l’élément multimédia de hello. fichier de manifeste de Hello contient la liste hello de tous les fichiers de ressources hello. Pour plus d’informations, consultez [Présélection de tâches pour Azure Media Indexer](https://msdn.microsoft.com/library/dn783454.aspx).

    static bool RunBatchIndexingJob(string[] inputMediaFiles, string outputFolder)
    {
        // Create an asset and upload toostorage.
        IAsset asset = CreateAssetAndUploadMultipleFiles(inputMediaFiles,
            "My Indexing Input Asset - Batch Mode",
            AssetCreationOptions.None);

        // Create a manifest file that contains all hello asset file names and upload toostorage.
        string manifestFile = "input.lst";            
        File.WriteAllLines(manifestFile, asset.AssetFiles.Select(f => f.Name).ToArray());
        var assetFile = asset.AssetFiles.Create(Path.GetFileName(manifestFile));
        assetFile.Upload(manifestFile);

        // Declare a new job.
        IJob job = _context.Jobs.Create("My Indexing Job - Batch Mode");

        // Get a reference toohello Azure Media Indexer.
        string MediaProcessorName = "Azure Media Indexer";
        IMediaProcessor processor = GetLatestMediaProcessorByName(MediaProcessorName);

        // Read configuration.
        string configuration = File.ReadAllText("batch.config");

        // Create a task with hello encoding details, using a string preset.
        ITask task = job.Tasks.AddNew("My Indexing Task - Batch Mode",
            processor,
            configuration,
            TaskOptions.None);

        // Specify hello input asset toobe indexed.
        task.InputAssets.Add(asset);

        // Add an output asset toocontain hello results of hello job.
        task.OutputAssets.AddNew("My Indexing Output Asset - Batch Mode", AssetCreationOptions.None);

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
            Console.WriteLine("Exiting method due toojob error.");
            return false;
        }

        // Download hello job outputs.
        DownloadAsset(task.OutputAssets.First(), outputFolder);

        return true;
    }

    private static IAsset CreateAssetAndUploadMultipleFiles(string[] filePaths, string assetName, AssetCreationOptions options)
    {
        IAsset asset = _context.Assets.Create(assetName, options);

        foreach (string filePath in filePaths)
        {
            var assetFile = asset.AssetFiles.Create(Path.GetFileName(filePath));
            assetFile.Upload(filePath);
        }

        return asset;
    }

### <a name="partially-succeeded-job"></a>Tâche partiellement réussie
Si tous les fichiers multimédias d’entrée sont correctement indexées, la tâche d’indexation hello échoue avec le code d’erreur 4000. Pour plus d’informations, consultez les [codes d’erreur](#error_codes).

Hello mêmes sorties (que les travaux réussis) sont générés. Vous pouvez faire référence toohello sortie fichier manifeste toofind les fichiers d’entrée défaillants, en fonction des valeurs de colonne d’erreur toohello. Pour les fichiers d’entrée qui a échoué, hello résultant AIB, SAMI, TTML, WebVTT et les fichiers de mot clé ne seront pas générées.

### <a id="preset"></a> Présélection de tâches pour l’Indexeur multimédia Azure
Bonjour Azure Media Indexer de traitement peut être personnalisé en fournissant une tâche facultative prédéfinie en même temps que la tâche hello.  la section suivante de Hello décrit format hello de ce fichier de configuration xml.

| Nom | Require | Description |
| --- | --- | --- |
| **Entrée** |false |Fichier (s) actif que vous souhaitez tooindex.</p><p>Azure Media Indexer prend en charge hello suivant les formats de fichiers multimédias : MP4, WMV, MP3, M4A, WMA, AAC, WAV.</p><p>Vous pouvez spécifier le nom de fichier hello (s) Bonjour **nom** ou **liste** attribut Hello **d’entrée** élément (comme indiqué ci-dessous). Si vous ne spécifiez pas le tooindex de fichier actif, le fichier primaire de hello est choisi. Si aucun fichier principal n’est définie, le premier fichier de ressource en entrée hello hello est indexé.</p><p>tooexplicitly spécifier le nom du fichier multimédia hello, procédez comme :<br/>`<input name="TestFile.wmv">`<br/><br/>Vous pouvez également indexer plusieurs fichiers d’éléments multimédias à la fois (des fichiers de too10). toodo cela :<br/><br/><ol class="ordered"><li><p>Créez un fichier texte (fichier manifeste) et affectez-lui une extension .lst. </p></li><li><p>Ajouter une liste de tous les noms de fichiers de ressources hello dans votre fichier de manifeste toothis élément multimédia d’entrée. </p></li><li><p>Ajoutez (Téléchargez) thanifest fichier toohello actif.  </p></li><li><p>Spécifier le nom hello du fichier de manifeste hello dans l’attribut de la liste de l’entrée hello.<br/>`<input list="input.lst">`</li></ol><br/><br/>Remarque : Si vous ajoutez le fichier manifeste de plus de 10 fichiers toohello, hello l’indexation de travail échoue avec le code d’erreur 2006 hello. |
| **métadonnées** |false |Métadonnées de hello spécifié utilisés pour l’Adaptation de vocabulaire ou les fichiers actifs.  Tooprepare utile indexeur toorecognize vocabulaire non standard des mots tels que des noms propres.<br/>`<metadata key="..." value="..."/>` <br/><br/>Vous pouvez fournir des **valeurs** pour les **clés** prédéfinies. Hello suivant clés est actuellement prises en charge :<br/><br/>« title » et « description » - utilisés pour vocabulaire adaptation tootweak hello langue de modèle pour votre travail et améliorer la précision de la reconnaissance vocale.  les valeurs Hello amorcer Internet recherche toofind des documents texte approprié en fonction du contexte, à l’aide du dictionnaire interne pour hello contenu tooaugment hello pour la durée de la tâche d’indexation hello.<br/>`<metadata key="title" value="[Title of hello media file]" />`<br/>`<metadata key="description" value="[Description of hello media file] />"` |
| **fonctionnalités** <br/><br/> ajoutées dans la version 1.2. Actuellement, la fonctionnalité de hello uniquement pris en charge est la reconnaissance vocale (« ASR »). |false |fonctionnalité de reconnaissance vocale Hello a hello suivant les clés de paramètres :<table><tr><th><p>Clé</p></th>        <th><p>Description</p></th><th><p>Exemple de valeur</p></th></tr><tr><td><p>language</p></td><td><p>toobe de langage naturel Hello reconnu dans le fichier multimédia de hello.</p></td><td><p>Anglais, espagnol</p></td></tr><tr><td><p>CaptionFormats</p></td><td><p>une liste délimitée par des points-virgules de hello souhaitée des formats de sortie de légende (le cas échéant)</p></td><td><p>ttml;sami;webvtt</p></td></tr><tr><td><p>GenerateAIB</p></td><td><p>Indicateur booléen indiquant si un fichier AIB est requis (pour une utilisation avec SQL Server et hello Indexer IFilter client).  Pour plus d’informations, consultez <a href="http://azure.microsoft.com/blog/2014/11/03/using-aib-files-with-azure-media-indexer-and-sql-server/">Utilisation de fichiers AIB avec Azure Media Indexer et SQL Server</a>.</p></td><td><p>True; False</p></td></tr><tr><td><p>GenerateKeywords</p></td><td><p>Indicateur booléen indiquant si un fichier XML de mot-clé est requis ou non.</p></td><td><p>True; False. </p></td></tr><tr><td><p>ForceFullCaption</p></td><td><p>Indicateur booléen indiquant si tooforce complète légendes (quel que soit le niveau de confiance).  </p><p>Valeur par défaut est false, auquel cas mots et expressions qui ont un niveau de confiance de 50 % inférieurs sont omises de sorties de légende final hello et remplacées par les points de suspension («... »).  points de suspension Hello sont utiles pour l’audit et de contrôle de qualité de légende.</p></td><td><p>True; False. </p></td></tr></table> |

### <a id="error_codes"></a>Codes d’erreur
Dans le cas de hello d’une erreur, signalez Azure Media Indexer un Hello suivant des codes d’erreur en arrière :

| Code | Nom | Causes possibles |
| --- | --- | --- |
| 2000 |Configuration non valide |Configuration non valide |
| 2001 |Ressources d’entrée non valides |Ressources d’entrée manquantes ou vides. |
| 2002 |Manifeste non valide |Le manifeste est vide ou contient des éléments non valides. |
| 2003 |Fichier de média toodownload ayant échoué |L’URL dans le fichier manifeste n’est pas valide. |
| 2004 |Protocole non pris en charge |Le protocole de l'URL du média n’est pas pris en charge. |
| 2005 |Type de fichier non pris en charge |Le type de fichier multimédia d’entrée n’est pas pris en charge. |
| 2006 |Trop de fichiers d’entrée |Il existe plus de 10 fichiers dans le manifeste d’entrée de hello. |
| 3000 |Fichier de média toodecode ayant échoué |Codec de média non pris en charge  <br/>ou<br/> Fichier multimédia endommagé <br/>ou<br/> Il n’y a aucun flux audio dans le fichier d’entrée. |
| 4000 |Indexation en lot partiellement réussie |Certains des médias d’entrée de hello sont des fichiers a échoué toobe indexé. Pour plus d’informations, consultez <a href="#output_files">Fichiers de sortie</a>. |
| autres |Erreurs internes |Veuillez contacter l’équipe du support technique. indexer@microsoft.com |

## <a id="supported_languages"></a>Langues prises en charge
Actuellement, les langues anglaise et espagnole hello sont pris en charge. Pour plus d’informations, consultez [hello billet de blog de mise en production v1.2](https://azure.microsoft.com/blog/2015/04/13/azure-media-indexer-spanish-v1-2/).

## <a name="media-services-learning-paths"></a>Parcours d’apprentissage de Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a>Liens connexes
[Vue d’ensemble d’Azure Media Services Analytics](media-services-analytics-overview.md)

[Utilisation de fichiers AIB avec Azure Media Indexer et SQL Server](https://azure.microsoft.com/blog/2014/11/03/using-aib-files-with-azure-media-indexer-and-sql-server/)

[Indexation de fichiers multimédias avec Azure Media Indexer 2 Preview](media-services-process-content-with-indexer2.md)

