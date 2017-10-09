---
title: "jeux de données à grande échelle aaaProcess à l’aide de la fabrique de données et de traitement par lots | Documents Microsoft"
description: "Décrit comment tooprocess de grandes quantités de données dans une fabrique de données Azure de pipeline à l’aide des capacités de traitement parallèle de traitement par lots Azure."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 688b964b-51d0-4faa-91a7-26c7e3150868
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: spelluru
ms.openlocfilehash: 6788f02de555d2e9d6588cc990a39043866d7e97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="process-large-scale-datasets-using-data-factory-and-batch"></a>Traiter des jeux de données volumineux à l’aide de Data Factory et Batch
Cet article décrit une architecture d’un exemple de solution qui déplace et traite des jeux de données volumineux de manière automatique et planifiée. Il fournit également une solution de hello tooimplement procédure pas à pas de bout en bout à l’aide d’Azure Data Factory et Azure Batch.

Cet article est plus long que nos articles habituels car il contient une procédure pas à pas d’un exemple de solution complète. Si vous êtes tooBatch nouvelle fabrique de données, vous pouvez en savoir plus sur ces services et comment ils fonctionnent ensemble. Si vous connaissez vos services de hello et sont conception/élaboration d’une solution, vous pouvez concentrer uniquement sur hello [section architecture](#architecture-of-sample-solution) de hello article et si vous développez un prototype ou une solution, vous pouvez également tootry out instructions détaillées dans hello [procédure pas à pas](#implementation-of-sample-solution). N’hésitez pas à nous faire part de vos commentaires sur ce contenu et son utilisation.

Tout d’abord, nous allons voir comment les services de fabrique de données et de traitement par lots peuvent aider à avec le traitement de grands volumes de données dans le cloud de hello.     

## <a name="why-azure-batch"></a>Pourquoi Azure Batch ?
Traitement par lots Azure vous permet de toorun (HPC) informatique à grande échelle en parallèle et haute performance des applications efficacement dans le cloud de hello. Il s’agit d’un service de plateforme qui planifie toorun de travail de calcul intensif sur une collection gérée de machines virtuelles, et peut automatiquement montée en puissance de calcul ressources toomeet hello aux besoins de vos tâches.

Avec hello service Batch, vous définissez tooexecute des ressources de calcul Azure vos applications en parallèle et à grande échelle. Vous pouvez exécuter à la demande ou planifiées travaux et que vous n’avez pas besoin toomanually créer, configurer et gérer un cluster HPC, les machines virtuelles, les réseaux virtuels ou une tâche complexe et infrastructure de planification de tâches.

Consultez hello suivant articles si vous n’êtes pas familiarisé avec Azure Batch car cela permet de comprendre l’architecture de hello/implémentation de solution hello décrite dans cet article.   

* [Notions de base d’Azure Batch](../batch/batch-technical-overview.md)
* [Aperçu des fonctionnalités d’Azure Batch](../batch/batch-api-basics.md)

(facultatif) toolearn en savoir plus sur le traitement par lots Azure, consultez hello [cursus pour Azure Batch](https://azure.microsoft.com/documentation/learning-paths/batch/).

## <a name="why-azure-data-factory"></a>Pourquoi Azure Data Factory ?
Fabrique de données est un service d’intégration de données basés sur le cloud qui orchestre et automatise le déplacement de hello et la transformation de données. À l’aide du service de fabrique de données hello, vous pouvez créer des pipelines de données managées déplacement les données du site et de magasin de données centralisé de données magasins tooa le cloud (par exemple : stockage d’objets Blob Azure) et le processus/transformer les données à l’aide des services tels que Azure HDInsight Azure Apprentissage automatique. Vous pouvez également planifier toorun des pipelines de données dans une manière planifiée (horaire, quotidienne, hebdomadaire, etc.) et un moniteur et les gérer un problèmes de tooidentify coup de œil et prenez les mesures.

Consultez hello suivant articles si vous n’êtes pas familiarisé avec Azure Data Factory car cela permet de comprendre l’architecture de hello/implémentation de solution hello décrite dans cet article.  

* [Présentation d’Azure Data Factory](data-factory-introduction.md)
* [Générer votre premier pipeline de données](data-factory-build-your-first-pipeline.md)   

(facultatif) toolearn en savoir plus sur Azure Data Factory, consultez hello [cursus pour Azure Data Factory](https://azure.microsoft.com/documentation/learning-paths/data-factory/).

## <a name="data-factory-and-batch-together"></a>Intégration de Data Factory et Batch
Fabrique de données inclut des activités intégrées, telles que le magasin de données de toocopy/déplacement de l’activité de copie à partir de la source données tooa banque de données de destination et activité de la ruche tooprocess à l’aide (HDInsight) les clusters Hadoop sur Azure. Consultez l’article [Activités de transformation des données](data-factory-data-transformation-activities.md) pour obtenir la liste des activités de transformation prises en charge.

Aussi, il permet de vous toocreate .NET des activités personnalisées toomove ou traitent des données avec votre propre logique et exécuter ces activités sur un cluster Azure HDInsight ou sur un pool de traitement par lots Azure des machines virtuelles. Lorsque vous utilisez le traitement par lots Azure, vous pouvez configurer hello pool tooauto à l’échelle (ajouter ou supprimer des ordinateurs virtuels en fonction de la charge de travail hello) basé sur une formule que vous fournissez.     

## <a name="architecture-of-sample-solution"></a>Architecture de l’exemple de solution
Bien que l’architecture de hello décrite dans cet article est une solution simple, il est toocomplex pertinentes des scénarios tels que le risque de modélisation par les services financiers, le traitement d’image et rendu et analyse génomique.

Hello illustre 1) la fabrique de données orchestre le déplacement des données et le traitement et 2) de quelle façon Azure Batch traite hello des données de manière parallèle. Téléchargement et diagramme d’impression hello pour faciliter la référence (11 x 17 pouces. ou format A3) : [Calcul haute performance et orchestration de données à l’aide des services Azure Batch et Data Factory](http://go.microsoft.com/fwlink/?LinkId=717686).

[![Diagramme de traitement des données à grande échelle](./media/data-factory-data-processing-using-batch/image1.png)](http://go.microsoft.com/fwlink/?LinkId=717686)

Hello liste suivante fournit les étapes de base hello du processus de hello. solution de Hello inclut le code et des explications pour les solutions de bout en bout toobuild hello.

1. **Configurez Azure Batch avec un pool de nœuds de calcul (machines virtuelles)**. Vous pouvez spécifier le nombre de hello de nœuds et la taille de chaque nœud.
2. **Créez une instance Azure Data Factory** configurée avec des entités qui représentent respectivement le stockage d’objets blob Azure, le service de calcul Azure Batch, les données en entrée et sortie, ainsi qu’un flux de travail, ou pipeline, d’activités qui déplacent et transforment des données.
3. **Créer une activité .NET personnalisée dans le pipeline de Data Factory hello**. activité Hello est votre code utilisateur qui s’exécute sur hello pool Azure Batch.
4. **Stockez de grandes quantités de données d’entrée en tant qu’objets blob dans Azure Storage**. Les données sont divisées en tranches logiques (généralement basées sur l’heure).
5. **Fabrique de données copie les données traitées en parallèle** toohello les emplacement secondaire.
6. **Fabrique de données s’exécute l’activité personnalisée hello est à l’aide de pool hello allouée par lot**. Data Factory peut exécuter plusieurs activités simultanément. Chaque activité traite une tranche de données. résultats de Hello sont stockés dans le stockage Azure.
7. **Fabrique de données déplace le troisième emplacement hello résultats finaux tooa**, soit pour la distribution via une application, ou pour un traitement ultérieur par d’autres outils.

## <a name="implementation-of-sample-solution"></a>Implémentation de l’exemple de solution
exemple de solution Hello est volontairement simple et est tooshow vous comment toouse Data Factory et traitement par lots ensemble tooprocess jeux de données. solution de Hello simplement nombre hello d’occurrences d’un terme à rechercher (« Microsoft ») dans les fichiers d’entrée organisés dans une série chronologique. Il génère des fichiers de toooutput hello count.

**Heure**: Si vous êtes familiarisé avec les concepts de base d’Azure Data Factory et traitement par lots, et ont des conditions préalables de hello terminé répertoriées ci-dessous, nous estimons cette solution prend toocomplete de 1 à 2 heures.

### <a name="prerequisites"></a>Composants requis
#### <a name="azure-subscription"></a>Abonnement Azure
Si vous n’êtes pas abonné, vous pouvez créer un compte d’essai gratuit en quelques minutes. Voir [essai gratuit](https://azure.microsoft.com/pricing/free-trial/).

#### <a name="azure-storage-account"></a>Compte Azure Storage
Vous utilisez un compte de stockage Azure pour stocker les données de hello dans ce didacticiel. Si vous ne possédez pas de compte de stockage Azure, voir [Création d’un compte de stockage](../storage/common/storage-create-storage-account.md#create-a-storage-account). exemple de solution Hello utilise le stockage d’objets blob.

#### <a name="azure-batch-account"></a>Compte Azure Batch
Créer un compte Azure Batch hello [portail Azure](http://manage.windowsazure.com/). Voir [Créer et gérer un compte Azure Batch](../batch/batch-account-create-portal.md). Notez hello Azure Batch compte et le nom de clé du compte. Vous pouvez également utiliser [New-AzureRmBatchAccount](https://msdn.microsoft.com/library/mt603749.aspx) toocreate de l’applet de commande un compte Azure Batch. Pour obtenir des instructions détaillées sur l’utilisation de cette applet de commande, voir [Prise en main des applets de commande Azure Batch PowerShell](../batch/batch-powershell-cmdlets-get-started.md) .

exemple de solution Hello utilise des données de tooprocess d’Azure Batch (indirectement via un pipeline Azure Data Factory) de manière parallèle sur un pool de nœuds de calcul (une collection managée d’ordinateurs virtuels).

#### <a name="azure-batch-pool-of-virtual-machines-vms"></a>Pool de machines virtuelles Azure Batch
Créez un **pool Azure Batch** comprenant au moins 2 nœuds de calcul.

1. Bonjour [portail Azure](https://portal.azure.com), cliquez sur **Parcourir** dans hello du menu de gauche, puis cliquez sur **comptes Batch**.
2. Sélectionnez votre hello tooopen du compte Azure Batch **compte Batch** panneau.
3. Cliquez sur la vignette **Pools** .
4. Bonjour **Pools** panneau, cliquez sur le bouton Ajouter dans la barre d’outils de hello tooadd un pool.
   1. Entrez un ID de pool de hello (**ID du Pool**). Hello de note **ID de pool de hello**; vous en avez besoin lors de la création de solutions de Data Factory hello.
   2. Spécifiez **Windows Server 2012 R2** pour le paramètre de famille du système d’exploitation hello.
   3. Sélectionnez le **niveau tarifaire du nœud**.
   4. Entrez **2** en tant que valeur pour hello **cible dédié** paramètre.
   5. Entrez **2** en tant que valeur pour hello **nombre maximal de tâches par nœud** paramètre.
   6. Cliquez sur **OK** pool de hello toocreate.

#### <a name="azure-storage-explorer"></a>Explorateur de stockage Azure
[Azure Storage Explorer 6 (outil)](https://azurestorageexplorer.codeplex.com/) ou [CloudXplorer](http://clumsyleaf.com/products/cloudxplorer) (à partir du logiciel ClumsyLeaf). Vous utilisez ces outils pour examiner et modifier les données de salutation dans vos projets de stockage Azure, notamment les journaux de hello de vos applications hébergés dans le cloud.

1. Créez un conteneur nommé **mycontainer** avec un accès privé (par d’accès anonyme).
2. Si vous utilisez **CloudXplorer**, créer des dossiers et sous-dossiers avec hello suivant structure :

   ![](./media/data-factory-data-processing-using-batch/image3.png)

   `Inputfolder` et `outputfolder` sont des dossiers de niveau supérieur de `mycontainer`. Hello `inputfolder` a des sous-dossiers contenant les cachets de date et d’heure (AAAA-MM-JJ-HH).

   Si vous utilisez **Azure Storage Explorer**, à l’étape suivante de hello, vous avez besoin des fichiers de tooupload avec des noms : `inputfolder/2015-11-16-00/file.txt`, `inputfolder/2015-11-16-01/file.txt` et ainsi de suite. Cette étape crée automatiquement des dossiers de hello.
3. Créez un fichier texte **fichier.txt** sur votre ordinateur avec un contenu qui a le mot clé de hello **Microsoft**. Par exemple, « activité de test personnalisé Microsoft ».
4. Téléchargez toohello de fichier hello suivant des dossiers d’entrée dans le stockage blob Azure.

   ![](./media/data-factory-data-processing-using-batch/image4.png)

   Si vous utilisez **Azure Storage Explorer**, téléchargez le fichier de hello **fichier.txt** trop**mycontainer**. Cliquez sur **copie** sur la barre d’outils de hello toocreate une copie de l’objet blob de hello. Bonjour **Copy Blob** boîte de dialogue, modification hello **nom d’objet blob de destination** trop`inputfolder/2015-11-16-00/file.txt`. Répétez cette étape toocreate `inputfolder/2015-11-16-01/file.txt`, `inputfolder/2015-11-16-02/file.txt`, `inputfolder/2015-11-16-03/file.txt`, `inputfolder/2015-11-16-04/file.txt` et ainsi de suite. Cette action crée automatiquement des dossiers de hello.
5. Créez un autre conteneur nommé : `customactivitycontainer`. Vous téléchargez des conteneurs de toothis de fichiers zip activité personnalisée hello.

#### <a name="visual-studio"></a>Visual Studio
Installer Microsoft Visual Studio 2012 ou version ultérieure toocreate hello personnalisé lot activité toobe utilisé Bonjour solution de fabrique de données.

### <a name="high-level-steps-toocreate-hello-solution"></a>Solution de hello toocreate étapes principales
1. Créer une activité personnalisée qui contient la logique de traitement des données hello.
2. Créez une fabrique de données Azure qui utilise l’activité personnalisée hello :

### <a name="create-hello-custom-activity"></a>Créer l’activité personnalisée hello
Hello activité personnalisée de fabrique de données est le cœur de hello de cet exemple de solution. exemple de solution Hello utilise l’activité personnalisée de traitement par lots Azure toorun hello. Consultez [utiliser des activités personnalisées dans un pipeline Azure Data Factory](data-factory-use-custom-activities.md) pour des activités personnalisées hello des informations de base toodevelop et l’utilisation dans Azure Data Factory pipelines.

toocreate une activité personnalisée .NET que vous pouvez utiliser dans un pipeline Azure Data Factory, vous devez toocreate une **bibliothèque de classes .NET** projet avec une classe qui implémente cette **IDotNetActivity** interface. Cette interface possède une seule méthode : **Execute**. Voici la signature hello de méthode hello :

```csharp
public IDictionary<string, string> Execute(
            IEnumerable<LinkedService> linkedServices,
            IEnumerable<Dataset> datasets,
            Activity activity,
            IActivityLogger logger)
```

méthode Hello a quelques composants clés que vous avez besoin de toounderstand.

* méthode Hello accepte quatre paramètres :

  1. **linkedServices**. Une liste énumérable de services liés qui relient les sources de données d’entrée/sortie (par exemple : stockage d’objets Blob Azure) fabrique de données toohello. Dans cet exemple, il s’agit du seul service lié de type Azure Storage utilisé à la fois pour les données d’entrée et de sortie.
  2. **jeux de données**. liste énumérable de jeux de données. Vous pouvez utiliser ce emplacements de paramètre tooget hello et les schémas définis par les jeux de données d’entrée et de sortie.
  3. **activity**. Ce paramètre représente hello calcul entité actuelle - dans ce cas, un service Azure Batch.
  4. **logger**. vous permet d’enregistreur d’événements Hello que écrire des commentaires de débogage cette surface comme hello « Utilisateur » pour ouvrir une session hello pipeline.
* méthode Hello retourne un dictionnaire qui peut être des activités personnalisées toochain utilisées ensemble dans un avenir hello. Cette fonctionnalité n’est pas encore implémentée, par conséquent, renvoyer un dictionnaire vide à partir de la méthode hello.

#### <a name="procedure-create-hello-custom-activity"></a>Procédure : Créer l’activité personnalisée hello
1. Créez un projet de bibliothèque de classes .NET dans Visual Studio 2013.

   1. Lancez **Visual Studio 2012**/**2013/2015**.
   2. Cliquez sur **fichier**, pointez trop**nouveau**, puis cliquez sur **projet**.
   3. Développez **Modèles**, puis sélectionnez **Visual C\#**. Dans cette procédure pas à pas, vous utilisez C\#, mais vous pouvez utiliser n’importe quel langage .NET toodevelop hello personnalisée activité.
   4. Sélectionnez **bibliothèque de classes** à partir de la liste hello des types de projets sur hello droite.
   5. Entrez **MyDotNetActivity** pour hello **nom**.
   6. Sélectionnez **C:\\ADF** pour hello **emplacement**. Créer le dossier de hello **ADF** s’il n’existe pas.
   7. Cliquez sur **OK** projet hello de toocreate.
2. Cliquez sur **outils**, pointez trop**Gestionnaire de Package NuGet**, puis cliquez sur **Package Manager Console**.
3. Bonjour **Package Manager Console**, exécutez hello suivant commande tooimport **Microsoft.Azure.Management.DataFactories**.

    ```powershell
    Install-Package Microsoft.Azure.Management.DataFactories
    ```
4. Hello d’importation **Azure Storage** package NuGet dans le projet de toohello. Vous avez besoin de ce package, car vous utilisez des API de stockage d’objets Blob hello dans cet exemple.

    ```powershell
    Install-Package Azure.Storage
    ```
5. Ajoutez hello suivant **à l’aide de** directives toohello source fichier hello projet.

    ```csharp
    using System.IO;
    using System.Globalization;
    using System.Diagnostics;
    using System.Linq;
    
    using Microsoft.Azure.Management.DataFactories.Models;
    using Microsoft.Azure.Management.DataFactories.Runtime;
    
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```
6. Modifier le nom de hello hello **espace de noms** trop**MyDotNetActivityNS**.

    ```csharp
    namespace MyDotNetActivityNS
    ```
7. Modifier le nom hello de classe hello trop**MyDotNetActivity** et la dériver de hello **IDotNetActivity** interface comme indiqué ci-dessous.

    ```csharp
    public class MyDotNetActivity : IDotNetActivity
    ```
8. Hello d’implémenter (Ajouter) **Execute** méthode Hello **IDotNetActivity** interface toohello **MyDotNetActivity** classe et copie hello suivant l’exemple de méthode toohello de code. Consultez hello [exécuter une méthode](#execute-method) section pour une explication pour la logique de hello utilisée dans cette méthode.

    ```csharp
    /// <summary>
    /// Execute method is hello only method of IDotNetActivity interface you must implement.
    /// In this sample, hello method invokes hello Calculate method tooperform hello core logic.  
    /// </summary>
    public IDictionary<string, string> Execute(
       IEnumerable<LinkedService> linkedServices,
       IEnumerable<Dataset> datasets,
       Activity activity,
       IActivityLogger logger)
    {
    
       // declare types for input and output data stores
       AzureStorageLinkedService inputLinkedService;
    
       Dataset inputDataset = datasets.Single(dataset => dataset.Name == activity.Inputs.Single().Name);
    
       foreach (LinkedService ls in linkedServices)
           logger.Write("linkedService.Name {0}", ls.Name);
    
       // using First method instead of Single since we are using hello same
       // Azure Storage linked service for input and output.
       inputLinkedService = linkedServices.First(
           linkedService =>
           linkedService.Name ==
           inputDataset.Properties.LinkedServiceName).Properties.TypeProperties
           as AzureStorageLinkedService;
    
       string connectionString = inputLinkedService.ConnectionString; // toocreate an input storage client.
       string folderPath = GetFolderPath(inputDataset);
       string output = string.Empty; // for use later.
    
       // create storage client for input. Pass hello connection string.
       CloudStorageAccount inputStorageAccount = CloudStorageAccount.Parse(connectionString);
       CloudBlobClient inputClient = inputStorageAccount.CreateCloudBlobClient();
    
       // initialize hello continuation token before using it in hello do-while loop.
       BlobContinuationToken continuationToken = null;
       do
       {   // get hello list of input blobs from hello input storage client object.
           BlobResultSegment blobList = inputClient.ListBlobsSegmented(folderPath,
                                    true,
                                    BlobListingDetails.Metadata,
                                    null,
                                    continuationToken,
                                    null,
                                    null);
    
           // Calculate method returns hello number of occurrences of
           // hello search term (“Microsoft”) in each blob associated
           // with hello data slice.
           //
           // definition of hello method is shown in hello next step.
           output = Calculate(blobList, logger, folderPath, ref continuationToken, "Microsoft");
    
       } while (continuationToken != null);
    
       // get hello output dataset using hello name of hello dataset matched tooa name in hello Activity output collection.
       Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);
    
       folderPath = GetFolderPath(outputDataset);
    
       logger.Write("Writing blob toohello folder: {0}", folderPath);
    
       // create a storage object for hello output blob.
       CloudStorageAccount outputStorageAccount = CloudStorageAccount.Parse(connectionString);
       // write hello name of hello file.
       Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    
       logger.Write("output blob URI: {0}", outputBlobUri.ToString());
       // create a blob and upload hello output text.
       CloudBlockBlob outputBlob = new CloudBlockBlob(outputBlobUri, outputStorageAccount.Credentials);
       logger.Write("Writing {0} toohello output blob", output);
       outputBlob.UploadText(output);
    
       // hello dictionary can be used toochain custom activities together in hello future.
       // This feature is not implemented yet, so just return an empty dictionary.
       return new Dictionary<string, string>();
    }
    ```
9. Ajoutez hello suivant classe toohello de méthodes d’assistance. Ces méthodes sont appelées par hello **Execute** (méthode). Plus important encore, hello **Calculate** méthode isole code hello qui effectue une itération dans chaque objet blob.

    ```csharp
    /// <summary>
    /// Gets hello folderPath value from hello input/output dataset.
    /// </summary>
    private static string GetFolderPath(Dataset dataArtifact)
    {
       if (dataArtifact == null || dataArtifact.Properties == null)
       {
           return null;
       }
    
       AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
       if (blobDataset == null)
       {
           return null;
       }
    
       return blobDataset.FolderPath;
    }
    
    /// <summary>
    /// Gets hello fileName value from hello input/output dataset.
    /// </summary>
    
    private static string GetFileName(Dataset dataArtifact)
    {
       if (dataArtifact == null || dataArtifact.Properties == null)
       {
           return null;
       }
    
       AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
       if (blobDataset == null)
       {
           return null;
       }
    
       return blobDataset.FileName;
    }
    
    /// <summary>
    /// Iterates through each blob (file) in hello folder, counts hello number of instances of search term in hello file,
    /// and prepares hello output text that is written toohello output blob.
    /// </summary>
    
    public static string Calculate(BlobResultSegment Bresult, IActivityLogger logger, string folderPath, ref BlobContinuationToken token, string searchTerm)
    {
       string output = string.Empty;
       logger.Write("number of blobs found: {0}", Bresult.Results.Count<IListBlobItem>());
       foreach (IListBlobItem listBlobItem in Bresult.Results)
       {
           CloudBlockBlob inputBlob = listBlobItem as CloudBlockBlob;
           if ((inputBlob != null) && (inputBlob.Name.IndexOf("$$$.$$$") == -1))
           {
               string blobText = inputBlob.DownloadText(Encoding.ASCII, null, null, null);
               logger.Write("input blob text: {0}", blobText);
               string[] source = blobText.Split(new char[] { '.', '?', '!', ' ', ';', ':', ',' }, StringSplitOptions.RemoveEmptyEntries);
               var matchQuery = from word in source
                                where word.ToLowerInvariant() == searchTerm.ToLowerInvariant()
                                select word;
               int wordCount = matchQuery.Count();
               output += string.Format("{0} occurrences(s) of hello search term \"{1}\" were found in hello file {2}.\r\n", wordCount, searchTerm, inputBlob.Name);
           }
       }
       return output;
    }
    ```
    Hello **GetFolderPath** méthode renvoie hello chemin toohello dossier ce Bonjour dataset points tooand Bonjour **GetFileName** méthode retourne les nom hello de hello/fichier blob qui hello pour les points de jeu de données.

    ```csharp

    "name": "InputDataset",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "fileName": "file.txt",
            "folderPath": "mycontainer/inputfolder/{Year}-{Month}-{Day}-{Hour}",
    ```

    Hello **Calculate** (méthode) calcule le nombre de hello d’instances du mot clé **Microsoft** dans les fichiers d’entrée de hello (objets BLOB dans le dossier de hello). terme de recherche Hello (« Microsoft ») est codé en dur dans le code hello.

1. Compilez le projet de hello. Cliquez sur **générer** de hello menu et cliquez sur **générer la Solution**.
2. Lancez **l’Explorateur Windows**et accédez trop**bin\\déboguer** ou **bin\\release** dossier en fonction de type hello de build.
3. Créer un fichier zip **MyDotNetActivity.zip** qui contient tous les fichiers binaires de hello Bonjour  **\\bin\\déboguer** dossier. Vous souhaiterez peut-être tooinclude hello MyDotNetActivity. **pdb** de fichiers afin que vous obtenez des informations supplémentaires telles que le numéro de ligne dans le code source hello qui a provoqué le problème de hello lorsqu’une défaillance se produit.

   ![](./media/data-factory-data-processing-using-batch/image5.png)
4. Télécharger **MyDotNetActivity.zip** comme un conteneur d’objets blob blob toohello : `customactivitycontainer` Bonjour Azure stockage d’objets blob que hello **StorageLinkedService** service Bonjour lié  **ADFTutorialDataFactory** utilise. Créer le conteneur d’objets blob hello `customactivitycontainer` si elle n’existe pas déjà.

#### <a name="execute-method"></a>Méthode Execute
Cette section fournit plus de détails et remarques sur le code hello Bonjour méthode Execute.

1. membres Hello pour itérer la collection d’entrée de hello sont trouvent dans hello [Microsoft.WindowsAzure.Storage.Blob](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.aspx) espace de noms. Itération dans la collection d’objets blob hello requiert l’utilisation de hello **BlobContinuationToken** classe. Fondamentalement, vous devez utiliser un-boucle avec jeton hello en tant que mécanisme de hello pour quitter hello boucle while. Pour plus d’informations, consultez [comment toouse stockage d’objets Blob à partir de .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md). Une boucle de base est illustrée ici :

    ```csharp
    // Initialize hello continuation token.
    BlobContinuationToken continuationToken = null;
    do
    {
    // Get hello list of input blobs from hello input storage client object.
    BlobResultSegment blobList = inputClient.ListBlobsSegmented(folderPath,
    
                         true,
                                   BlobListingDetails.Metadata,
                                   null,
                                   continuationToken,
                                   null,
                                   null);
    // Return a string derived from parsing each blob.
    
     output = Calculate(blobList, logger, folderPath, ref continuationToken, "Microsoft");
    
    } while (continuationToken != null);

    ```
   Consultez la documentation de hello pour hello [ListBlobsSegmented](https://msdn.microsoft.com/library/jj717596.aspx) méthode pour plus d’informations.
2. Hello code de travail dans le jeu d’objets BLOB hello logiquement dans hello faire-une boucle while. Bonjour **Execute** (méthode), hello-lors de la boucle transmet liste hello d’objets BLOB méthode tooa nommée **Calculate**. méthode Hello retourne une variable chaîne nommée **sortie** qui est le résultat de hello d’avoir parcouru de tous les objets BLOB de hello dans le segment de hello.

   Elle retourne le nombre de hello d’occurrences du terme de recherche hello (**Microsoft**) dans l’objet blob de hello passé toohello **Calculate** (méthode).

    ```csharp
    output += string.Format("{0} occurrences of hello search term \"{1}\" were found in hello file {2}.\r\n", wordCount, searchTerm, inputBlob.Name);
    ```
3. Une fois hello **Calculate** méthode a procédé hello, elle doit être écrite tooa nouvel objet blob. Par conséquent, pour chaque jeu d’objets BLOB traité, un nouvel objet blob peut être écrites avec les résultats hello. un nouvel objet blob toowrite tooa, le premier jeu de données de la sortie de hello rechercher.

    ```csharp
    // Get hello output dataset using hello name of hello dataset matched tooa name in hello Activity output collection.
    Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);
    ```
4. code de Hello appelle également une méthode d’assistance : **GetFolderPath** chemin du dossier hello tooretrieve (nom de conteneur de stockage hello).

    ```csharp
    folderPath = GetFolderPath(outputDataset);
    ```
   Hello **GetFolderPath** casts hello DataSet objet tooan AzureBlobDataSet, qui a une propriété nommée FolderPath.

    ```csharp
    AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
    
    return blobDataset.FolderPath;
    ```
5. appels de code Bonjour Bonjour **GetFileName** méthode tooretrieve hello fichier nom (blob). code de Hello est similaire toohello au-dessus de chemin d’accès du dossier code tooget hello.

    ```csharp
    AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
    
    return blobDataset.FileName;
    ```
6. nom de Hello du fichier de hello est écrit en créant un objet URI. constructeur d’URI Hello utilise hello **BlobEndpoint** nom du conteneur de propriété tooreturn hello. nom de fichier et le chemin du dossier Hello sont ajoutés tooconstruct hello sortie URI d’objet blob.  

    ```csharp
    // Write hello name of hello file.
    Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    ```
7. Hello nom de fichier de hello a été écrit et vous pouvez maintenant écrire la chaîne de sortie hello de hello **Calculate** un nouvel objet blob méthode tooa :

    ```csharp
    // Create a blob and upload hello output text.
    CloudBlockBlob outputBlob = new CloudBlockBlob(outputBlobUri, outputStorageAccount.Credentials);
    logger.Write("Writing {0} toohello output blob", output);
    outputBlob.UploadText(output);
    ```

### <a name="create-hello-data-factory"></a>Créer la fabrique de données hello
Bonjour [créer l’activité personnalisée hello](#create-the-custom-activity) section, vous avez créé une activité personnalisée et téléchargé hello zip avec des fichiers binaires et hello PDB fichier tooan conteneur d’objets blob Azure. Dans cette section, vous créez un Azure **fabrique de données** avec un **pipeline** qui utilise hello **activité personnalisée**.

Hello dataset d’entrée d’activité personnalisée hello représente des objets BLOB de hello (fichiers) dans le dossier d’entrée de hello (`mycontainer\\inputfolder`) dans le stockage blob. jeu de données de sortie Hello d’activité hello représente des objets BLOB de sortie hello dans le dossier de sortie hello (`mycontainer\\outputfolder`) dans le stockage blob.

Supprimer un ou plusieurs fichiers dans les dossiers d’entrée hello :

```
mycontainer -\> inputfolder
    2015-11-16-00
    2015-11-16-01
    2015-11-16-02
    2015-11-16-03
    2015-11-16-04
```

Par exemple, faites glisser un fichier (fichier.txt) avec hello suivant contenu dans chacun des dossiers de hello.

```
test custom activity Microsoft test custom activity Microsoft
```

Chaque dossier d’entrée correspond tranche tooa dans Azure Data Factory, même si le dossier de hello a 2 ou plusieurs fichiers. Lorsque chaque tranche est traitée par le pipeline de hello, activité personnalisée hello itère tous les objets BLOB de hello dans le dossier d’entrée de hello pour cette tranche.

Vous voyez cinq fichiers de sortie avec hello même contenu. Par exemple, le fichier de sortie hello de traiter le fichier hello dans le dossier de hello 2015-11-16-00 a hello suivant le contenu :

```
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file.txt.
```

Si vous supprimez plusieurs fichiers (fichier.txt, file2.txt, file3.txt) avec hello même contenu toohello des dossiers d’entrée, vous voyez hello suivant contenu dans le fichier de sortie hello. Chaque dossier (2015-11-16-00, etc.) correspondant tranche tooa dans cet exemple, même si le dossier de hello a plusieurs fichiers d’entrée.

```csharp
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file.txt.
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file2.txt.
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file3.txt.
```

fichier de sortie Hello a trois lignes à présent, un pour chaque fichier d’entrée (blob) dans le dossier hello associé à la tranche de hello (2015-11-16-00).

Une tâche est créée pour chaque exécution d’activité. Dans cet exemple, il n'est qu’une seule activité dans le pipeline de hello. Lorsqu’une tranche est traitée par le pipeline de hello, activité personnalisée hello s’exécute sur un secteur de traitement par lots Azure tooprocess hello. Étant donné qu’il y a cinq tranches (chacune pouvant comporter plusieurs objets blob ou fichiers), cinq tâches sont créées dans Azure Batch. Lorsqu’une tâche s’exécute sur le lot, il est réellement hello activité personnalisée qui est en cours d’exécution.

Hello, procédure pas à pas fournit des détails supplémentaires.

#### <a name="step-1-create-hello-data-factory"></a>Étape 1 : Créer la fabrique de données hello
1. Une fois connecté toohello [portail Azure](https://portal.azure.com/), hello comme suit :

   1. Cliquez sur **nouveau** sur le menu de gauche hello.
   2. Cliquez sur **données + Analytique** Bonjour **nouveau** panneau.
   3. Cliquez sur **Data Factory** sur hello **analytique des données** panneau.
2. Bonjour **nouvelle fabrique de données** panneau, entrez **CustomActivityFactory** pour hello nom. nom de Hello de fabrique de données Azure hello doit être globalement unique. Si vous recevez une erreur de hello : **nom de fabrique de données « CustomActivityFactory » n’est pas disponible**, modifiez le nom hello hello fabrique de données (par exemple, **yournameCustomActivityFactory**) et essayez de créer à nouveau.
3. Cliquez sur **NOM DU GROUPE DE RESSOURCES**pour sélectionner un groupe de ressources existant, ou créez un groupe de ressources.
4. Vérifiez que vous utilisez le bon abonnement de hello et région où vous souhaitez toobe de fabrique de données hello créé.
5. Cliquez sur **créer** sur hello **nouvelle fabrique de données** panneau.
6. Vous voyez la fabrique de données hello en cours de création dans hello **tableau de bord** de hello portail Azure.
7. Une fois que la fabrique de données hello a été créé avec succès, vous voyez page de fabrique de données hello, qui vous indique hello contenu hello fabrique de données.

   ![](./media/data-factory-data-processing-using-batch/image6.png)

#### <a name="step-2-create-linked-services"></a>Étape 2 : Créer des services liés
Services liés lier des magasins de données ou la fabrique de données Azure tooan de services de calcul. Dans cette étape, vous liez votre **Azure Storage** compte et **Azure Batch** fabrique de données tooyour de compte.

#### <a name="create-azure-storage-linked-service"></a>Créer le service lié Stockage Azure
1. Cliquez sur hello **auteur et déployer** vignette sur hello **DATA FACTORY** panneau pour **CustomActivityFactory**. Vous consultez hello éditeur Data Factory.
2. Cliquez sur **nouveau magasin de données** hello de barre de commandes et choisissez **le stockage Azure.** Vous devez voir hello script JSON pour la création d’un stockage Azure lié à service dans l’éditeur de hello.

   ![](./media/data-factory-data-processing-using-batch/image7.png)

3. Remplacez **nom de compte** avec le nom de hello de votre compte de stockage Azure et **clé de compte** avec la clé d’accès hello Hello compte de stockage Azure. toolearn comment tooget votre stockage accéder aux clés, voir [clés d’accès afficher, copier et régénérer stockage](../storage/common/storage-create-storage-account.md#manage-your-storage-account).

4. Cliquez sur **déployer** sur toodeploy hello lié service de la barre de commandes hello.

   ![](./media/data-factory-data-processing-using-batch/image8.png)

#### <a name="create-azure-batch-linked-service"></a>Créer un service lié Azure Batch
Dans cette étape, vous créez un service lié pour votre **Azure Batch** compte d’activité personnalisée de la fabrique de données utilisé toorun hello.

1. Cliquez sur **nouveau calcul** hello de barre de commandes et choisissez **Azure Batch.** Vous devez voir hello script JSON pour la création d’un traitement par lots Azure lié à service dans l’éditeur de hello.
2. Bonjour script JSON :

   1. Remplacez **nom de compte** avec nom hello de votre compte Azure Batch.
   2. Remplacez **clé d’accès** avec la clé d’accès hello Hello compte Azure Batch.
   3. Entrez les ID de hello du pool de hello pour hello **poolName** propriété**.** Pour cette propriété, vous pouvez spécifier le nom de pool ou l’ID de pool.
   4. Entrez le lot hello URI pour hello **batchUri** propriété JSON.

      > [!IMPORTANT]
      > Hello **URL** de hello **Panneau de compte Azure Batch** est Bonjour suivant le format : \<accountname\>.\< région\>. batch.azure.com. Pourquoi **batchUri** propriété Bonjour JSON, vous devez trop**supprimer « accountname ».** à partir de l’URL de hello. Exemple : `"batchUri": "https://eastus.batch.azure.com"`.
      >
      >

      ![](./media/data-factory-data-processing-using-batch/image9.png)

      Pourquoi **poolName** propriété, vous pouvez également spécifier d’ID hello du pool hello au lieu du nom de hello du pool de hello.

      > [!NOTE]
      > Hello service Data Factory ne prend en charge une option à la demande de traitement par lots Azure comme il le fait pour HDInsight. Vous pouvez uniquement utiliser votre propre pool Azure Batch dans une fabrique de données Azure.
      >
      >
   5. Spécifiez **StorageLinkedService** pour hello **linkedServiceName** propriété. Vous avez créé ce service lié à l’étape précédente de hello. Ce stockage est utilisé en tant que zone de transit pour les fichiers et les journaux.
3. Cliquez sur **déployer** sur toodeploy hello lié service de la barre de commandes hello.

#### <a name="step-3-create-datasets"></a>Étape 3 : Créer les jeux de données
Dans cette étape, vous créez une entrée de toorepresent de jeux de données et les données de sortie.

#### <a name="create-input-dataset"></a>Créer le jeu de données d’entrée
1. Bonjour **éditeur** pour hello fabrique de données, cliquez sur **nouveau dataset** bouton de barre d’outils hello et cliquez sur **le stockage Blob Azure** à partir du menu déroulant de hello.
2. Remplacez hello JSON dans le volet de droite hello hello suivant extrait de code JSON :

    ```json
    {
       "name": "InputDataset",
       "properties": {
           "type": "AzureBlob",
           "linkedServiceName": "AzureStorageLinkedService",
           "typeProperties": {
               "folderPath": "mycontainer/inputfolder/{Year}-{Month}-{Day}-{Hour}",
               "format": {
                   "type": "TextFormat"
               },
               "partitionedBy": [
                   {
                       "name": "Year",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "yyyy"
                       }
                   },
                   {
                       "name": "Month",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "MM"
                       }
                   },
                   {
                       "name": "Day",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "dd"
                       }
                   },
                   {
                       "name": "Hour",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "HH"
                       }
                   }
               ]
           },
           "availability": {
               "frequency": "Hour",
               "interval": 1
           },
           "external": true,
           "policy": {}
       }
    }
    ```

    Plus loin dans cette procédure pas à pas, vous allez créer un pipeline associé à l’heure de début 2015-11-16T00:00:00Z et à l’heure de fin 2015-11-16T05:00:00Z. Elle est planifiée tooproduce données **toutes les heures**, il y a 5 tranches d’entrée/sortie (entre **00**: 00:00 -\> **05**: 00:00).

    Hello **fréquence** et **intervalle** de jeu de données d’entrée hello est défini trop**heure** et **1**, ce qui signifie que hello entrée tranche est disponible toutes les heures.

    Voici les heures de début hello pour chaque secteur, qui sont représentées par **SliceStart** variable système Bonjour ci-dessus extrait de code JSON.

    | **Tranche** | **Heure de début**          |
    |-----------|-------------------------|
    | 1         | 2015-11-16T**00**:00:00 |
    | 2         | 2015-11-16T**01**:00:00 |
    | 3         | 2015-11-16T**02**:00:00 |
    | 4         | 2015-11-16T**03**:00:00 |
    | 5         | 2015-11-16T**04**:00:00 |

    Hello **folderPath** est calculée à l’aide de partie de hello année, mois, jour et heure de l’heure de début de tranche hello (**SliceStart**). Par conséquent, voici comment un dossier d’entrée est mappé tooa tranche.

    | **Tranche** | **Heure de début**          | **Dossier d’entrée**  |
    |-----------|-------------------------|-------------------|
    | 1         | 2015-11-16T**00**:00:00 | 2015-11-16-**00** |
    | 2         | 2015-11-16T**01**:00:00 | 2015-11-16-**01** |
    | 3         | 2015-11-16T**02**:00:00 | 2015-11-16-**02** |
    | 4         | 2015-11-16T**03**:00:00 | 2015-11-16-**03** |
    | 5         | 2015-11-16T**04**:00:00 | 2015-11-16-**04** |

1. Cliquez sur **déployer** hello toocreate de barre d’outils et déployer hello **InputDataset** table.

#### <a name="create-output-dataset"></a>Créer un jeu de données de sortie
Dans cette étape, vous créez un autre jeu de données de type de données de sortie AzureBlob toorepresent hello.

1. Bonjour **éditeur** pour hello fabrique de données, cliquez sur **nouveau dataset** bouton de barre d’outils hello et cliquez sur **le stockage Blob Azure** à partir du menu déroulant de hello.
2. Remplacez hello JSON dans le volet de droite hello hello suivant extrait de code JSON :

    ```json
    {
       "name": "OutputDataset",
       "properties": {
           "type": "AzureBlob",
           "linkedServiceName": "AzureStorageLinkedService",
           "typeProperties": {
               "fileName": "{slice}.txt",
               "folderPath": "mycontainer/outputfolder",
               "partitionedBy": [
                   {
                       "name": "slice",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "yyyy-MM-dd-HH"
                       }
                   }
               ]
           },
           "availability": {
               "frequency": "Hour",
               "interval": 1
           }
       }
    }
    ```

    Un objet blob/fichier de sortie est généré pour chaque tranche d’entrée. Voici la procédure de nommage des fichiers de sortie pour chaque tranche. Tous les fichiers de sortie hello sont générés dans un dossier de sortie : `mycontainer\\outputfolder`.

    | **Tranche** | **Heure de début**          | **Fichier de sortie**       |
    |-----------|-------------------------|-----------------------|
    | 1         | 2015-11-16T**00**:00:00 | 2015-11-16-**00.txt** |
    | 2         | 2015-11-16T**01**:00:00 | 2015-11-16-**01.txt** |
    | 3         | 2015-11-16T**02**:00:00 | 2015-11-16-**02.txt** |
    | 4         | 2015-11-16T**03**:00:00 | 2015-11-16-**03.txt** |
    | 5         | 2015-11-16T**04**:00:00 | 2015-11-16-**04.txt** |

    Souvenez-vous que tous les hello des fichiers dans un dossier d’entrée (par exemple : 2015-11-16-00) font partie d’une tranche avec l’heure de début hello : 2015-11-16-00. Lorsque cette tranche est traitée, activité personnalisée hello parcourt chaque fichier et produit une ligne dans le fichier de sortie hello avec numéro hello d’occurrences du terme de recherche (« Microsoft »). S’il existe trois fichiers dans le dossier hello 2015-11-16-00, il existe trois lignes dans le fichier de sortie hello : 2015-11-16-00.txt.

1. Cliquez sur **déployer** hello toocreate de barre d’outils et déployer hello **OutputDataset**.

#### <a name="step-4-create-and-run-hello-pipeline-with-custom-activity"></a>Étape 4 : Créer et exécuter le pipeline de hello avec une activité personnalisée
Dans cette étape, vous créez un pipeline avec une activité, activité personnalisée hello est créé précédemment.

> [!IMPORTANT]
> Si vous n’avez pas téléchargé hello **fichier.txt** tooinput des dossiers dans le conteneur d’objets blob hello, le faire avant de créer le pipeline de hello. Hello **isPaused** propriété a la valeur toofalse dans le pipeline hello JSON, pour que le pipeline de hello s’exécute immédiatement comme hello **Démarrer** la date est hello passée.
>
>

1. Bonjour éditeur Data Factory, cliquez sur **nouveau pipeline** sur la barre de commandes hello. Si vous ne voyez pas la commande hello, cliquez sur **... (Points de suspension)**  toosee il.
2. Remplacez hello JSON dans le volet de droite hello hello JSON script suivant :

    ```json
    {
       "name": "PipelineCustom",
       "properties": {
           "description": "Use custom activity",
           "activities": [
               {
                   "type": "DotNetActivity",
                   "typeProperties": {
                       "assemblyName": "MyDotNetActivity.dll",
                       "entryPoint": "MyDotNetActivityNS.MyDotNetActivity",
                       "packageLinkedService": "AzureStorageLinkedService",
                       "packageFile": "customactivitycontainer/MyDotNetActivity.zip"
                   },
                   "inputs": [
                       {
                           "name": "InputDataset"
                       }
                   ],
                   "outputs": [
                       {
                           "name": "OutputDataset"
                       }
                   ],
                   "policy": {
                       "timeout": "00:30:00",
                       "concurrency": 5,
                       "retry": 3
                   },
                   "scheduler": {
                       "frequency": "Hour",
                       "interval": 1
                   },
                   "name": "MyDotNetActivity",
                   "linkedServiceName": "AzureBatchLinkedService"
               }
           ],
           "start": "2015-11-16T00:00:00Z",
           "end": "2015-11-16T05:00:00Z",
           "isPaused": false
      }
    }
    ```
   Hello Notez les points suivants :

   * Il n'est qu’une seule activité dans le pipeline de hello et qui est de type : **DotNetActivity**.
   * **AssemblyName** a la valeur nom toohello Hello DLL : **MyDotNetActivity.dll**.
   * **Point d’entrée** est défini trop**MyDotNetActivityNS.MyDotNetActivity**. Il s’agit essentiellement de \<namespace\>.\<classname\> dans votre code.
   * **PackageLinkedService** est défini trop**StorageLinkedService** qui pointe le stockage d’objets blob toohello qui contient le fichier zip d’activité personnalisée hello. Si vous utilisez des comptes de stockage Azure différents pour les fichiers d’entrée/sortie et le fichier zip d’activité personnalisée hello, vous avez toocreate un autre Azure Storage service lié. Cet article suppose que vous utilisez hello même compte de stockage Azure.
   * **PackageFile** est défini trop**customactivitycontainer/MyDotNetActivity.zip**. Il est au format de hello : \<containerforthezip\>/\<nameofthezip.zip\>.
   * activité personnalisée Hello prend **InputDataset** en tant qu’entrée et **OutputDataset** en tant que sortie.
   * Hello **linkedServiceName** toohello la propriété d’activité personnalisée hello pointe **AzureBatchLinkedService**, ce qui indique à Azure Data Factory pour cette activité personnalisée hello doit toorun sur Azure Batch.
   * Hello **concurrency** paramètre est important. Si vous utilisez la valeur par défaut de hello, qui est 1, même si vous disposez de 2 ou de plusieurs nœuds dans le pool de traitement par lots Azure hello, tranches de hello sont traitées une après l’autre. Par conséquent, vous prenez pas parti des capacités de traitement parallèle de hello de traitement par lots Azure. Si vous définissez **concurrency** tooa plus élevée, par exemple 2, cela signifie que deux tranches (correspond tootwo des tâches de traitement par lots Azure) peuvent être traités en hello même moment, dans ce cas, les deux ordinateurs virtuels de hello Bonjour Azure Batch pool sont utilisées. Par conséquent, définir concurrency, propriété hello en conséquence.
   * Par défaut, une seule tâche (tranche) est exécutée sur une machine virtuelle à un moment donné. Hello raison est que, par défaut, hello **Maximum de tâches par ordinateur virtuel** a la valeur too1 pour un pool de traitement par lots Azure. Dans le cadre des conditions préalables, vous avez créé un pool avec cette too2 set de propriété, donc deux tranches de fabrique de données peuvent s’exécuter sur un ordinateur virtuel à hello même temps.

    -   **isPaused** propriété a la valeur toofalse par défaut. pipeline de Hello s’exécute immédiatement dans cet exemple, car le début des tranches de hello Bonjour passées. Vous pouvez définir ce pipeline de propriété tootrue toopause hello et affectez-lui arrière toofalse toorestart.

    -   Hello **Démarrer** temps et **fin** fois éloignés de cinq heures et tranches de produits toutes les heures, afin de cinq tranches sont produits par le pipeline de hello.

1. Cliquez sur **déployer** sur le pipeline de hello toodeploy de barre de commandes hello.

#### <a name="step-5-test-hello-pipeline"></a>Étape 5 : Tester le pipeline de hello
Dans cette étape, vous tester le pipeline de hello en supprimant les fichiers dans des dossiers d’entrée de hello. Commençons par le pipeline de hello test avec un fichier par un seul dossier d’entrée.

1. Dans le panneau de la fabrique de données hello Bonjour portail Azure, cliquez sur **diagramme**.

   ![](./media/data-factory-data-processing-using-batch/image10.png)
2. Dans la vue de diagramme hello, double-cliquez sur le jeu de données d’entrée : **InputDataset**.

   ![](./media/data-factory-data-processing-using-batch/image11.png)
3. Vous devez voir hello **InputDataset** panneau avec toutes les cinq tranches prêt. Hello d’avis **l’heure de début de la tranche** et **heure de fin de la tranche** pour chaque secteur.

   ![](./media/data-factory-data-processing-using-batch/image12.png)
4. Bonjour **vue de diagramme**, cliquez maintenant sur **OutputDataset**.
5. Vous devez voir que les cinq tranches de sortie hello sont dans l’état prêt hello si elles ont déjà été générés.

   ![](./media/data-factory-data-processing-using-batch/image13.png)
6. Hello de tooview portail Azure utilisation **tâches** associé hello **tranches** et voir les ordinateurs virtuels chaque tranche s’exécutait sur. Consultez la section [Intégration de Data Factory et Batch](#data-factory-and-batch-integration) pour plus d’informations.
7. Vous devez voir les fichiers de sortie hello Bonjour `outputfolder` de `mycontainer` dans votre Azure stockage d’objets blob.

   ![](./media/data-factory-data-processing-using-batch/image15.png)

   Vous devriez voir cinq fichiers de sortie, un par tranche d’entrée. Chaque Hello sortie de fichier doit avoir le contenu toohello similaire suivant de sortie :

    ```
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file.txt.
    ```
   Hello diagramme suivant illustre comment les tranches de Data Factory hello mappent tootasks dans Azure Batch. Dans cet exemple, une tranche n’est exécutée qu’une seule fois.

   ![](./media/data-factory-data-processing-using-batch/image16.png)
8. À présent, essayons avec plusieurs fichiers dans un dossier. Créer des fichiers : **file2.txt**, **file3.txt**, **file4.txt**, et **file5.txt** avec hello même contenu que dans fichier.txt dans le dossier de hello : **2015-11-06-01**.
9. Dans le dossier de sortie hello **supprimer** fichier de sortie hello : **2015-11-16-01.txt**.
10. Maintenant, dans hello **OutputDataset** panneau, la tranche de hello avec le bouton avec **l’heure de début de la tranche** défini trop**16/11/2015 01:00:00 AM**, puis cliquez sur **exécuter**tranche de hello toorerun/ré-process. À présent, la tranche de hello contient cinq fichiers au lieu d’un seul fichier.

    ![](./media/data-factory-data-processing-using-batch/image17.png)
11. Une fois que la tranche de hello s’exécute et son état est **prêt**, vérifiez le contenu dans le fichier de sortie hello pour cette tranche hello (**2015-11-16-01.txt**) Bonjour `outputfolder` de `mycontainer` dans votre stockage d’objets blob. Il doit être une ligne pour chaque fichier de tranche de hello.

    ```
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file2.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file3.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file4.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file5.txt.
    ```

> [!NOTE]
> Si vous n’avez pas supprimé 2015 dans le fichier de sortie hello-11-16-01.txt avant d’essayer de cinq fichiers d’entrée, vous voyez une seule ligne à partir de la tranche de hello précédente exécution et les cinq lignes à partir de la tranche hello exécuter. Par défaut, le contenu de hello est ajouté toooutput fichier s’il existe déjà.
>
>

#### <a name="data-factory-and-batch-integration"></a>Intégration de Data Factory et Batch
Hello service Data Factory crée un travail en traitement par lots Azure avec le nom de hello : `adf-poolname:job-xxx`.

![Azure Data Factory - Travaux Batch](media/data-factory-data-processing-using-batch/data-factory-batch-jobs.png)

Une tâche dans la tâche de hello est créée pour chaque exécution de l’activité d’un secteur. S’il y a 10 toobe prêt tranches traitées, 10 tâches sont créés dans la tâche de hello. Vous pouvez avoir plusieurs tranches en cours d’exécution en parallèle si vous avez plusieurs nœuds de calcul dans le pool de hello. Si le nombre maximum de tâches hello par calcul nœud est défini trop > 1, il peut y avoir plusieurs une découper en cours d’exécution sur hello même calcul.

Dans cet exemple, il y a cinq tranches, donc cinq tâches dans Azure Batch. Avec hello **concurrency** défini trop**5** Bonjour pipeline JSON dans Azure Data Factory et **Maximum de tâches par ordinateur virtuel** défini trop**2** dans Azure Batch pool **2** machines virtuelles, hello l’exécution des tâches rapide (Vérifiez les heures de début et de fin pour les tâches).

Utilisez hello tooview portail hello par lots et ses tâches associées hello **tranches** et voir les ordinateurs virtuels chaque tranche s’exécutait sur.

![Azure Data Factory - Tâches de travaux Batch](media/data-factory-data-processing-using-batch/data-factory-batch-job-tasks.png)

### <a name="debug-hello-pipeline"></a>Déboguer hello pipeline
Le débogage consiste à utiliser quelques techniques de base :

1. Si la tranche de hello d’entrée n’est pas défini trop**prêt**, vérifiez que la structure de dossiers d’entrée de hello est correct et fichier.txt existe dans les dossiers d’entrée hello.

   ![](./media/data-factory-data-processing-using-batch/image3.png)
2. Bonjour **Execute** méthode de votre activité personnalisée, utilisez hello **IActivityLogger** informations toolog objet qui vous permet de résoudre les problèmes. messages Hello connecté apparaissent dans les utilisateur hello\_fichier journal de 0.

   Bonjour **OutputDataset** panneau, cliquez sur Bonjour tranche toosee Bonjour **tranche de données** panneau pour ce secteur. Les **activités exécutées** pour cette tranche s’affichent. Vous devez voir une activité à exécuter pour la tranche de hello. Si vous cliquez sur **exécuter** dans la barre de commandes hello, vous pouvez démarrer une autre activité exécutée pour hello même secteur.

   Lorsque vous cliquez sur exécution de l’activité hello, vous voyez hello **détails de l’activité exécuter** panneau avec une liste des fichiers journaux. Vous consultez les messages enregistrés dans hello **utilisateur\_0 journal** fichier. Lorsqu’une erreur se produit, vous voyez trois exécutions d’activité, car de nouvelles tentatives hello est définie too3 dans pipeline/activité hello JSON. Lorsque vous cliquez sur exécution de l’activité hello, vous voyez que vous pouvez consulter les erreurs de hello tootroubleshoot des fichiers journaux hello.

   ![](./media/data-factory-data-processing-using-batch/image18.png)

   Dans la liste hello des fichiers journaux, cliquez sur hello **0.log de l’utilisateur**. Dans le panneau droit hello sont des résultats de l’utilisation de hello hello **IActivityLogger.Write** (méthode).

   ![](./media/data-factory-data-processing-using-batch/image19.png)

   Consultez le fichier system-0.log pour vérifier les exceptions et messages d’erreur système éventuels.

    ```
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Loading assembly file MyDotNetActivity...
    
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Creating an instance of MyDotNetActivityNS.MyDotNetActivity from assembly file MyDotNetActivity...
    
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Executing Module
    
    Trace\_T\_D\_12/6/2015 1:43:38 AM\_T\_D\_\_T\_D\_Information\_T\_D\_0\_T\_D\_Activity e3817da0-d843-4c5c-85c6-40ba7424dce2 finished successfully
    ```
3. Inclure hello **PDB** fichiers dans le fichier zip de hello afin que les détails de l’erreur hello ont des informations telles que **pile des appels** lorsqu’une erreur se produit.
4. Tous les hello des fichiers dans le fichier zip de hello pour l’activité personnalisée hello doit se trouver au hello **niveau supérieur** avec aucun des sous-dossiers.

   ![](./media/data-factory-data-processing-using-batch/image20.png)
5. Vérifiez que hello **assemblyName** (MyDotNetActivity.dll), **entryPoint** (MyDotNetActivityNS.MyDotNetActivity), **packageFile** (customactivitycontainer / MyDotNetActivity.zip), et **packageLinkedService** (doit point toohello Azure stockage d’objets blob qui contient le fichier zip de hello) sont définies les valeurs toocorrect.
6. Si vous avez corrigé une tranche hello tooreprocess erreur et que vous souhaitez, cliquez sur tranche hello Bonjour **OutputDataset** panneau, cliquez sur **exécuter**.

   ![](./media/data-factory-data-processing-using-batch/image21.png)

   > [!NOTE]
   > Vous voyez un **conteneur** dans votre Stockage Blob Azure nommé `adfjobs`. Ce conteneur n’est pas supprimé automatiquement, mais vous pouvez le supprimer en toute sécurité après avoir effectué la solution hello test. De même, hello solution de fabrique de données crée un lot d’Azure **travail** nommé : `adf-\<pool ID/name\>:job-0000000001`. Vous pouvez supprimer cette tâche après avoir testé les solutions hello si vous le souhaitez.
   >
   >
7. activité personnalisée Hello n’utilise pas hello **app.config** fichier à partir de votre package. Par conséquent, si votre code lit les chaînes de connexion à partir du fichier de configuration hello, il ne fonctionne pas lors de l’exécution. Hello meilleures pratiques lors de l’utilisation d’Azure Batch est toohold les clés secrètes dans un **Azure KeyVault**, utilisez un keyvault de hello basée sur certificat de service principal tooprotect et distribuer le pool de traitement par lots hello certificat tooAzure. Hello les activités personnalisées .NET puis peuvent accéder aux clés secrètes hello KeyVault lors de l’exécution. Cette solution est générique et peut évoluer type tooany du secret, pas seulement les chaînes de connexion.

    Il existe une solution plus facile (mais pas une meilleure pratique) : vous pouvez créer un **service lié Azure SQL** avec les paramètres de chaîne de connexion, créez un dataset qu’utilise hello service lié et le jeu de données chaîne hello comme un jeu de données d’entrée factice activité de .NET personnalisée toohello. Vous pouvez ensuite hello d’accès liées la chaîne de connexion du service dans le code d’activité personnalisée hello et il doit fonctionner correctement lors de l’exécution.  

#### <a name="extend-hello-sample"></a>Étendre l’exemple hello
Vous pouvez étendre cet exemple toolearn plus d’informations sur les fonctionnalités d’Azure Data Factory et Azure Batch. Par exemple, les tranches tooprocess dans une plage de temps différente, hello comme suit :

1. Ajouter hello suivant sous-dossiers Bonjour `inputfolder`: 2015-11-16-05, 2015-11-16-06 201-11-16-07, 2011-11-16-08, 2015-11-16-09 et place les fichiers d’entrée dans ces dossiers. Modifier l’heure de fin hello pour le pipeline hello à partir de `2015-11-16T05:00:00Z` trop`2015-11-16T10:00:00Z`. Bonjour **vue de diagramme**, double-cliquez sur hello **InputDataset**et vérifiez que les tranches d’entrée hello sont prêtes. Double-cliquez sur **OuptutDataset** état de hello toosee de tranches de sortie. S’ils sont dans l’état prêt, vérifiez le dossier de sortie hello pour les fichiers de sortie hello.
2. Augmenter ou diminuer hello **concurrency** paramètre toounderstand comment il affecte les performances de hello de votre solution, en particulier hello du traitement qui se produit sur Azure Batch. (Consultez l’étape 4 : créer et exécuter le pipeline de hello pour plus d’informations sur hello **concurrency** paramètre.)
3. Créez un pool avec une valeur **Maximum tasks per VM**(Nombre maximal de tâches par machine virtuelle) supérieure/inférieure. toouse hello nouveau pool est créé, hello de mise à jour de service lié Azure Batch dans la solution de Data Factory hello. (Consultez l’étape 4 : créer et exécuter le pipeline de hello pour plus d’informations sur hello **Maximum de tâches par ordinateur virtuel** paramètre.)
4. Créez un pool Azure Batch avec la fonctionnalité **autoscale** . Automatiquement mise à l’échelle des nœuds de calcul dans un pool Azure Batch est ajustement dynamique de hello de puissance utilisée par votre application de traitement. 

    Hello exemple de formule ici atteint hello suivant comportement : lorsque hello pool est initialement créé, il commence par 1 machine virtuelle. $PendingTasks mesure définit le nombre hello de tâches en cours d’exécution + active (en file d’attente) état.  formule de Hello recherche hello moyenne d’attente de tâches Bonjour 180 dernières secondes et définit les élément TargetDedicated en conséquence. Elle garantit que TargetDedicated ne va jamais au-delà de 25 machines virtuelles. Par conséquent, comme les nouvelles tâches sont envoyés, pool croît automatiquement en tant que tâches se terminent, machines virtuelles deviennent libre un par un et hello échelle réduit ces machines virtuelles. startingNumberOfVMs et maxNumberofVMs peut être ajustée tooyour besoins.
 
    Formule de mise à l’échelle automatique :

    ``` 
    startingNumberOfVMs = 1;
    maxNumberofVMs = 25;
    pendingTaskSamplePercent = $PendingTasks.GetSamplePercent(180 * TimeInterval_Second);
    pendingTaskSamples = pendingTaskSamplePercent < 70 ? startingNumberOfVMs : avg($PendingTasks.GetSample(180 * TimeInterval_Second));
    $TargetDedicated=min(maxNumberofVMs,pendingTaskSamples);
    ```

   Pour plus d’informations, consultez [Mettre automatiquement à l’échelle les nœuds de calcul dans un pool Azure Batch](../batch/batch-automatic-scaling.md) .

   Si le pool de hello utilise par défaut de hello [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx), hello service Batch peut prendre 15 à 30 minutes tooprepare hello machine virtuelle avant d’exécuter l’activité personnalisée hello.  Si le pool de hello utilise un autre autoScaleEvaluationInterval, hello service Batch peut prendre autoScaleEvaluationInterval + 10 minutes.
5. Dans la solution de l’exemple hello hello **Execute** méthode appelle hello **Calculate** méthode qui traite une tooproduce de tranche de données d’entrée une tranche de données de sortie. Vous pouvez écrire votre propre méthode tooprocess les données d’entrée et remplacez l’appel de méthode Calculate hello dans la méthode d’exécution hello avec une méthode d’appel tooyour.

### <a name="next-steps-consume-hello-data"></a>Étapes suivantes : consommer des données de hello
Après avoir traité des données, vous pouvez les employer avec des outils en ligne tels que **Microsoft Power BI**. Voici toohelp liens comprendre de Power BI et comment toouse dans Azure :

* [Explorer un jeu de données dans Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-get-data/)
* [Prise en main de hello Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/)
* [Actualisation des données dans Power BI](https://powerbi.microsoft.com/documentation/powerbi-refresh-data/)
* [Azure et Power BI](https://powerbi.microsoft.com/documentation/powerbi-azure-and-power-bi/)

## <a name="references"></a>Références
* [Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/)

  * [Introduction tooAzure service Data Factory](data-factory-introduction.md)
  * [Prise en main d’Azure Data Factory](data-factory-build-your-first-pipeline.md)
  * [Utilisation des activités personnalisées dans un pipeline Azure Data Factory](data-factory-use-custom-activities.md)
* [Azure Batch](https://azure.microsoft.com/documentation/services/batch/)

  * [Notions de base d’Azure Batch](../batch/batch-technical-overview.md)
  * [Vue d’ensemble des fonctionnalités d’Azure Batch](../batch/batch-api-basics.md)
  * [Créer et gérer le compte Azure Batch Bonjour portail Azure](../batch/batch-account-create-portal.md)
  * [Get started with the .NET Azure Batch Library .NET](../batch/batch-dotnet-get-started.md)

[batch-explorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[batch-explorer-walkthrough]: http://blogs.technet.com/b/windowshpc/archive/2015/01/20/azure-batch-explorer-sample-walkthrough.aspx
