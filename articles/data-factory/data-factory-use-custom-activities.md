---
title: "aaaUse des activités personnalisées dans un pipeline Azure Data Factory"
description: "Découvrez comment toocreate des activités personnalisées et les utiliser dans un pipeline Azure Data Factory."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 8dd7ba14-15d2-4fd9-9ada-0b2c684327e9
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: spelluru
ms.openlocfilehash: 23e33727b2160541ab40938ffd911fdd484b3daa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-custom-activities-in-an-azure-data-factory-pipeline"></a>Utilisation des activités personnalisées dans un pipeline Azure Data Factory

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [Activité Hive](data-factory-hive-activity.md) 
> * [Activité pig](data-factory-pig-activity.md)
> * [Activité MapReduce](data-factory-map-reduce.md)
> * [Activité de diffusion en continu Hadoop](data-factory-hadoop-streaming-activity.md)
> * [Activité Spark](data-factory-spark.md)
> * [Activité d’exécution par lot Machine Learning](data-factory-azure-ml-batch-execution-activity.md)
> * [Activité des ressources de mise à jour de Machine Learning](data-factory-azure-ml-update-resource-activity.md)
> * [Activité de procédure stockée](data-factory-stored-proc-activity.md)
> * [Activité U-SQL Data Lake Analytics](data-factory-usql-activity.md)
> * [Activité personnalisée .NET](data-factory-use-custom-activities.md)

Vous pouvez utiliser deux types d’activités dans un pipeline Azure Data Factory.

- [Activités de déplacement des données](data-factory-data-movement-activities.md) toomove des données entre [prise en charge des magasins de données source et récepteur](data-factory-data-movement-activities.md#supported-data-stores-and-formats).
- [Activités de Transformation des données](data-factory-data-transformation-activities.md) tootransform les données à l’aide des services tels que Azure HDInsight, Azure Batch et Azure Machine Learning de calcul. 

les données toomove vers/depuis un magasin de données qui fabrique de données ne prend pas en charge, créez un **activité personnalisée** avec vos propres données mouvement logique et l’utilisation hello activité dans un pipeline. De même, tootransform/traitement des données d’une manière qui n’est pas pris en charge par la fabrique de données, créer une activité personnalisée avec votre propre logique de transformation de données et utiliser l’activité hello dans un pipeline. 

Vous pouvez configurer un toorun d’activité personnalisée sur une **Azure Batch** pool d’ordinateurs virtuels ou basé sur un Windows **Azure HDInsight** cluster. Lorsque vous utilisez Azure Batch, vous pouvez utiliser uniquement un pool Azure Batch. À l’inverse, lorsque vous utilisez HDInsight, vous pouvez utiliser un cluster HDInsight existant ou un cluster qui est créé automatiquement pour vous à la demande lors de l’exécution.  

Hello suivant de procédure pas à pas fournit des instructions détaillées pour la création d’une activité .NET personnalisée et à l’aide d’activité personnalisée hello dans un pipeline. procédure pas à pas Hello utilise un **Azure Batch** service lié. toouse un HDInsight Azure lié à service au lieu de cela, vous créez un service lié de type **HDInsight** (votre propre cluster HDInsight) ou **HDInsightOnDemand** (fabrique de données crée un cluster HDInsight à la demande). Ensuite, configurez hello de toouse d’activité personnalisée service lié HDInsight. Consultez [utilisez Azure HDInsight les services liés](#use-hdinsight-compute-service) pour plus d’informations sur l’utilisation d’activités personnalisées de Azure HDInsight toorun hello.

> [!IMPORTANT]
> - activités de .NET personnalisées Hello s’exécutent uniquement sur des clusters HDInsight de basés sur Windows. Une solution de contournement pour cette limitation est toouse hello carte réduire toorun personnalisé Java code d’activité sur un cluster HDInsight de basés sur Linux. Une autre option consiste à toouse un pool de traitement par lots Azure d’activités personnalisées de machines virtuelles toorun au lieu d’utiliser un cluster HDInsight.
> - Il n’est pas possible de toouse une passerelle de gestion des données à partir de sources de données sur site tooaccess activité personnalisée. Actuellement, [passerelle de gestion des données](data-factory-data-management-gateway.md) prend en charge uniquement l’activité de copie hello et l’activité de procédure stockée dans la fabrique de données.   

## <a name="walkthrough-create-a-custom-activity"></a>Procédure pas à pas : création d’une activité personnalisée
### <a name="prerequisites"></a>Conditions préalables
* Visual Studio 2012/2013/2015
* Téléchargez et installez le [Kit de développement logiciel (SDK) Azure .NET](https://azure.microsoft.com/downloads/)

### <a name="azure-batch-prerequisites"></a>Configuration requise pour Azure Batch
Hello procédure pas à pas, vous exécutez vos activités .NET personnalisées à l’aide du traitement par lots Azure en tant qu’une ressource de calcul. **Traitement par lots Azure** est une plateforme de service pour l’exécution parallèle à grande échelle et hautes performances (HPC) des applications efficacement dans le cloud de hello informatiques. Traitement par lots Azure planifie toorun de travail de calcul intensif sur managé **collection de machines virtuelles**, et peut automatiquement montée en puissance de calcul ressources toomeet hello aux besoins de vos tâches. Consultez [principes de base Azure Batch] [ batch-technical-overview] l’article pour une présentation détaillée de hello service Azure Batch.

Didacticiel de hello, créez un compte Azure Batch avec un pool d’ordinateurs virtuels. Voici les étapes hello :

1. Créer un **compte Azure Batch** à l’aide de hello [portail Azure](http://portal.azure.com). Consultez l’article [Créer et gérer un compte Azure Batch][batch-create-account] pour obtenir des instructions.
2. Notez le nom du compte Azure Batch hello, clé de compte, URI et nom du pool. Vous avez besoin toocreate un service lié Azure Batch.
    1. Sur la page d’accueil hello pour le compte Azure Batch, vous voyez un **URL** Bonjour suivant le format : `https://myaccount.westus.batch.azure.com`. Dans cet exemple, **myaccount** hello désigne hello compte Azure Batch. URI que vous utilisez dans la définition de service hello lié est URL hello sans nom hello du compte de hello. Par exemple : `https://<region>.batch.azure.com`.
    2. Cliquez sur **clés** sur le menu de gauche hello et hello de copie **clé d’accès primaire**.
    3. toouse un pool existant, cliquez sur **Pools** sur le menu de hello et notez les hello **ID** du pool de hello. Si vous n’avez pas un pool existant, déplacer l’étape suivante de toohello.     
2. Créez un **pool Azure Batch**.

   1. Bonjour [portail Azure](https://portal.azure.com), cliquez sur **Parcourir** dans hello du menu de gauche, puis cliquez sur **comptes Batch**.
   2. Sélectionnez votre hello tooopen du compte Azure Batch **compte Batch** panneau.
   3. Cliquez sur la vignette **Pools** .
   4. Bonjour **Pools** panneau, cliquez sur le bouton Ajouter dans la barre d’outils de hello tooadd un pool.
      1. Entrez un ID de pool de hello (ID du Pool). Hello de note **ID de pool de hello**; vous en avez besoin lors de la création de solutions de Data Factory hello.
      2. Spécifiez **Windows Server 2012 R2** pour le paramètre de famille du système d’exploitation hello.
      3. Sélectionnez le **niveau tarifaire du nœud**.
      4. Entrez **2** en tant que valeur pour hello **cible dédié** paramètre.
      5. Entrez **2** en tant que valeur pour hello **nombre maximal de tâches par nœud** paramètre.
   5. Cliquez sur **OK** pool de hello toocreate.
   6. Notez les hello **ID** du pool de hello. 



### <a name="high-level-steps"></a>Procédure générale
Voici hello deux étapes que vous effectuez dans le cadre de cette procédure pas à pas : 

1. Créer une activité personnalisée qui contient une logique simple de transformation/traitement des données.
2. Créez une fabrique de données Azure avec un pipeline qui utilise l’activité personnalisée hello.

### <a name="create-a-custom-activity"></a>création d'une activité personnalisée
toocreate une activité personnalisée .NET, créez un **bibliothèque de classes .NET** projet avec une classe qui implémente cette **IDotNetActivity** interface. Cette interface possède une seule méthode, [Execute](https://msdn.microsoft.com/library/azure/mt603945.aspx) , avec la signature suivante :

```csharp
public IDictionary<string, string> Execute(
        IEnumerable<LinkedService> linkedServices,
        IEnumerable<Dataset> datasets,
        Activity activity,
        IActivityLogger logger)
```


méthode Hello accepte quatre paramètres :

- **linkedServices**. Cette propriété est une liste énumérable de services liés de magasin de données référencées par les jeux de données d’entrée/sortie pour l’activité de hello.   
- **jeux de données**. Cette propriété est une liste énumérable de jeux de données d’entrée/sortie pour l’activité de hello. Vous pouvez utiliser ce emplacements de paramètre tooget hello et les schémas définis par les jeux de données d’entrée et de sortie.
- **activity**. Cette propriété représente l’activité en cours hello. Il peut être utilisé tooaccess les propriétés étendues associées d’activité personnalisée hello. Consultez la section [Accéder aux propriétés étendues](#access-extended-properties) pour plus d’informations.
- **logger**. Cet objet vous permet d’écrire des commentaires de débogage survenant dans le journal d’utilisateur hello pour le pipeline de hello.

méthode Hello retourne un dictionnaire qui peut être des activités personnalisées toochain utilisées ensemble dans un avenir hello. Cette fonctionnalité n’est pas encore implémentée, par conséquent, renvoyer un dictionnaire vide à partir de la méthode hello.  

### <a name="procedure"></a>Procédure
1. Créez un projet de **bibliothèque de classes .NET** .
   <ol type="a">
     <li>Lancez <b>Visual Studio 2017</b> ou <b>Visual Studio 2015</b> ou <b>Visual Studio 2013</b> ou <b>Visual Studio 2012</b>.</li>
     <li>Cliquez sur <b>fichier</b>, pointez trop<b>nouveau</b>, puis cliquez sur <b>projet</b>.</li>
     <li>Développez <b>Modèles</b>, puis sélectionnez <b>Visual C#</b>. Dans cette procédure pas à pas, vous utilisez c#, mais vous pouvez utiliser n’importe quel langage .NET toodevelop hello personnalisée activité.</li>
     <li>Sélectionnez <b>bibliothèque de classes</b> à partir de la liste hello des types de projets sur hello droite. Dans VS 2017, choisissez <b>Bibliothèque de classes (.NET Framework)</b> .</li>
     <li>Entrez <b>MyDotNetActivity</b> pour hello <b>nom</b>.</li>
     <li>Sélectionnez <b>C:\ADFGetStarted</b> pour hello <b>emplacement</b>.</li>
     <li>Cliquez sur <b>OK</b> projet hello de toocreate.</li>
   </ol>
2.Cliquez sur **outils**, pointez trop**Gestionnaire de Package NuGet**, puis cliquez sur **Package Manager Console**.
3. Dans la Console du Gestionnaire de Package de hello, exécutez hello suivant commande tooimport **Microsoft.Azure.Management.DataFactories**.

    ```PowerShell
    Install-Package Microsoft.Azure.Management.DataFactories
    ```
4. Hello d’importation **Azure Storage** package NuGet dans le projet de toohello.

    ```PowerShell
    Install-Package WindowsAzure.Storage -Version 4.3.0
    ```

    > [!IMPORTANT]
    > Lanceur de service de fabrique de données nécessite la version de hello 4.3 de WindowsAzure.Storage. Si vous ajoutez une référence tooa une version ultérieure de l’assembly de stockage Azure dans votre projet d’activité personnalisée, vous voyez une erreur lors de l’exécution de l’activité hello. Erreur de hello tooresolve, consultez [isolement de Appdomain](#appdomain-isolation) section. 
5. Ajoutez hello suivant **à l’aide de** instructions toohello source fichier hello projet.

    ```csharp

    // Comment these lines if using VS 2017
    using System.IO;
    using System.Globalization;
    using System.Diagnostics;
    using System.Linq;
    // --------------------

    // Comment these lines if using <= VS 2015
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    // ---------------------

    using Microsoft.Azure.Management.DataFactories.Models;
    using Microsoft.Azure.Management.DataFactories.Runtime;

    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```
6. Modifier le nom de hello hello **espace de noms** trop**MyDotNetActivityNS**.

    ```csharp
    namespace MyDotNetActivityNS
    ```
7. Modifier le nom hello de classe hello trop**MyDotNetActivity** et la dériver de hello **IDotNetActivity** comme indiqué dans hello suivant extrait de code de l’interface :

    ```csharp
    public class MyDotNetActivity : IDotNetActivity
    ```
8. Hello d’implémenter (Ajouter) **Execute** méthode Hello **IDotNetActivity** interface toohello **MyDotNetActivity** classe et copie hello suivant l’exemple de méthode toohello de code.

    Hello exemple suivant compte hello nombre d’occurrences du terme de recherche hello (« Microsoft ») dans chaque objet blob associé à une tranche de données.

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
        // get extended properties defined in activity JSON definition
        // (for example: SliceStart)
        DotNetActivity dotNetActivity = (DotNetActivity)activity.TypeProperties;
        string sliceStartString = dotNetActivity.ExtendedProperties["SliceStart"];
    
        // toolog information, use hello logger object
        // log all extended properties            
        IDictionary<string, string> extendedProperties = dotNetActivity.ExtendedProperties;
        logger.Write("Logging extended properties if any...");
        foreach (KeyValuePair<string, string> entry in extendedProperties)
        {
            logger.Write("<key:{0}> <value:{1}>", entry.Key, entry.Value);
        }
    
        // linked service for input and output data stores
        // in this example, same storage is used for both input/output
        AzureStorageLinkedService inputLinkedService;

        // get hello input dataset
        Dataset inputDataset = datasets.Single(dataset => dataset.Name == activity.Inputs.Single().Name);
    
        // declare variables toohold type properties of input/output datasets
        AzureBlobDataset inputTypeProperties, outputTypeProperties;
        
        // get type properties from hello dataset object
        inputTypeProperties = inputDataset.Properties.TypeProperties as AzureBlobDataset;
    
        // log linked services passed in linkedServices parameter
        // you will see two linked services of type: AzureStorage
        // one for input dataset and hello other for output dataset 
        foreach (LinkedService ls in linkedServices)
            logger.Write("linkedService.Name {0}", ls.Name);
    
        // get hello first Azure Storate linked service from linkedServices object
        // using First method instead of Single since we are using hello same
        // Azure Storage linked service for input and output.
        inputLinkedService = linkedServices.First(
            linkedService =>
            linkedService.Name ==
            inputDataset.Properties.LinkedServiceName).Properties.TypeProperties
            as AzureStorageLinkedService;
    
        // get hello connection string in hello linked service
        string connectionString = inputLinkedService.ConnectionString;
    
        // get hello folder path from hello input dataset definition
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
               // with hello data slice. definition of hello method is shown in hello next step.
    
            output = Calculate(blobList, logger, folderPath, ref continuationToken, "Microsoft");
    
        } while (continuationToken != null);
    
        // get hello output dataset using hello name of hello dataset matched tooa name in hello Activity output collection.
        Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);

        // get type properties for hello output dataset
        outputTypeProperties = outputDataset.Properties.TypeProperties as AzureBlobDataset;
    
        // get hello folder path from hello output dataset definition
        folderPath = GetFolderPath(outputDataset);

        // log hello output folder path 
        logger.Write("Writing blob toohello folder: {0}", folderPath);
    
        // create a storage object for hello output blob.
        CloudStorageAccount outputStorageAccount = CloudStorageAccount.Parse(connectionString);
        // write hello name of hello file.
        Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    
        // log hello output file name
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
9. Ajoutez hello les méthodes d’assistance suivantes : 

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

        // get type properties of hello dataset 
        AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
        if (blobDataset == null)
        {
            return null;
        }
    
        // return hello folder path found in hello type properties
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
    
        // get type properties of hello dataset
        AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
        if (blobDataset == null)
        {
            return null;
        }
    
        // return hello blob/file name in hello type properties
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

    Hello GetFolderPath méthode renvoie hello chemin d’accès toohello qui hello dataset pointe dossier tooand hello GetFileName retourne hello nom de méthode hello/fichier blob qui hello pour les points de jeu de données. Si vous havefolderPath définit à l’aide de variables telles que {Year}, {mois}, retourne des {Day}, etc., méthode hello hello chaîne car il est sans les remplacer par les valeurs d’exécution. Consultez la section [Accéder aux propriétés étendues](#access-extended-properties) pour plus d’informations sur l’accès à SliceStart, SliceEnd, etc.    

    ```JSON
    "name": "InputDataset",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "fileName": "file.txt",
            "folderPath": "adftutorial/inputfolder/",
    ```

    Hello méthode Calculate calcule le nombre hello d’instances du mot clé Microsoft dans les fichiers d’entrée de hello (objets BLOB dans le dossier de hello). terme de recherche Hello (« Microsoft ») est codé en dur dans le code hello.
10. Compilez le projet de hello. Cliquez sur **générer** de hello menu et cliquez sur **générer la Solution**.

    > [!IMPORTANT]
    > 4.5.2 de définir la version du .NET Framework comme infrastructure cible de hello pour votre projet : droit hello projet, puis cliquez sur **propriétés** tooset hello cible de .NET framework. Data Factory ne prend pas en charge les activités personnalisées compilées avec les versions de .NET Framework ultérieures à la version 4.5.2.

11. Lancez **l’Explorateur Windows**, puis accédez trop**bin\debug** ou **bin\release** dossier en fonction de type hello de build.
12. Créer un fichier zip **MyDotNetActivity.zip** qui contient tous les fichiers binaires de hello Bonjour <project folder>dossier \bin\Debug. Inclure hello **MyDotNetActivity.pdb** de fichiers afin que vous obtenez les détails supplémentaires tels que numéro de ligne dans le code source hello qui a provoqué le problème de hello s’il existe un échec. 

    > [!IMPORTANT]
    > Tous les hello des fichiers dans le fichier zip de hello pour l’activité personnalisée hello doit se trouver au hello **niveau supérieur** avec aucune sous-dossiers.

    ![Fichiers de sortie binaires](./media/data-factory-use-custom-activities/Binaries.png)
14. Si nécessaire, créez un conteneur de blobs nommé **customactivitycontainer**. 
15. Télécharger MyDotNetActivity.zip comme un customactivitycontainer de toohello d’objets blob dans un **à usage général** stockage d’objets blob Azure (stockage d’objets Blob à chaud pas/utile) qui est référencé par AzureStorageLinkedService.  

> [!IMPORTANT]
> Si vous ajoutez cette solution de tooa .NET activité projet dans Visual Studio qui contient un projet de la fabrique de données et ajoutez un projet d’activité too.NET référence de projet d’application hello fabrique de données, vous n’avez pas besoin de tooperform hello deux dernières étapes de création manuelle fichier zip de Hello et téléchargement de stockage d’objets blob Azure à usage général toohello. Lorsque vous publiez des entités de fabrique de données à l’aide de Visual Studio, ces étapes sont effectuées automatiquement par le processus de publication hello. Pour plus d’informations, consultez la section [Projet Data Factory dans Visual Studio](#data-factory-project-in-visual-studio).

## <a name="create-a-pipeline-with-custom-activity"></a>Créer un pipeline avec une activité personnalisée
Vous avez créé une activité personnalisée et téléchargé le fichier zip de hello avec le conteneur d’objets blob binaires tooa dans un **à usage général** compte de stockage Azure. Dans cette section, vous créez une fabrique de données Azure avec un pipeline qui utilise l’activité personnalisée hello.

Hello un jeu de données d’entrée pour l’activité personnalisée hello représente les objets BLOB (fichiers) dans dossier de customactivityinput hello du conteneur adftutorial dans le stockage blob hello. le dataset de sortie Hello pour l’activité de hello représente des objets BLOB de sortie dans le dossier de customactivityoutput hello du conteneur adftutorial dans le stockage blob hello.

Créer **fichier.txt** fichier avec hello suivante de contenu et le télécharger trop**customactivityinput** dossier Hello **adftutorial** conteneur. Créer le conteneur d’adftutorial hello s’il n’existe pas déjà. 

```
test custom activity Microsoft test custom activity Microsoft
```

dossier d’entrée de Hello correspond tranche tooa dans Azure Data Factory, même si le dossier de hello a deux ou plusieurs fichiers. Lorsque chaque tranche est traitée par le pipeline de hello, activité personnalisée hello itère tous les objets BLOB de hello dans le dossier d’entrée de hello pour cette tranche.

Vous consultez un fichier avec hello adftutorial\customactivityoutput dossier de sortie avec une ou plusieurs lignes (identique au nombre d’objets BLOB dans le dossier d’entrée de hello) :

```
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2016-11-16-00/file.txt.
```


Voici les étapes hello que vous effectuez dans cette section :

1. Création d'une **fabrique de données**.
2. Créer **services liés** pour le pool de traitement par lots Azure hello de machines virtuelles sur le hello activité personnalisée s’exécute et hello le stockage Azure qui contient des objets BLOB d’entrée/sortie hello.
3. Créer des entrées et sorties **datasets** qui représentent l’entrée et sortie de l’activité personnalisée hello.
4. Créer un **pipeline** qui utilise l’activité personnalisée hello.

> [!NOTE]
> Créer hello **fichier.txt** et télécharger le conteneur d’objets blob tooa si vous n’avez pas déjà fait. Consultez les instructions dans la précédente section de hello.   

### <a name="step-1-create-hello-data-factory"></a>Étape 1 : Créer la fabrique de données hello
1. Après l’ouverture dans toohello le portail Azure, procédez comme hello comme suit :
   1. Cliquez sur **nouveau** sur le menu de gauche hello.
   2. Cliquez sur **données + Analytique** Bonjour **nouveau** panneau.
   3. Cliquez sur **Data Factory** sur hello **analytique des données** panneau.
   
    ![Nouveau menu Azure Data Factory](media/data-factory-use-custom-activities/new-azure-data-factory-menu.png)
2. Bonjour **nouvelle fabrique de données** panneau, entrez **CustomActivityFactory** pour hello nom. nom de Hello de fabrique de données Azure hello doit être globalement unique. Si vous recevez une erreur de hello : **nom de fabrique de données « CustomActivityFactory » n’est pas disponible**, modifiez le nom hello hello fabrique de données (par exemple, **yournameCustomActivityFactory**) et essayez de créer à nouveau.

    ![Nouveau panneau Azure Data Factory](media/data-factory-use-custom-activities/new-azure-data-factory-blade.png)
3. Cliquez sur **NOM DU GROUPE DE RESSOURCES**pour sélectionner un groupe de ressources existant, ou créez un groupe de ressources.
4. Vérifiez que vous utilisez hello correct **abonnement** et **région** où vous souhaitez toobe de fabrique de données hello créé.
5. Cliquez sur **créer** sur hello **nouvelle fabrique de données** panneau.
6. Vous voyez la fabrique de données hello en cours de création dans hello **tableau de bord** de hello portail Azure.
7. Une fois que la fabrique de données hello a été créé avec succès, vous voyez panneau hello fabrique de données, qui vous indique hello contenu hello fabrique de données.
    
    ![Panneau Data Factory](media/data-factory-use-custom-activities/data-factory-blade.png)

### <a name="step-2-create-linked-services"></a>Étape 2 : Créer des services liés
Services liés lier des magasins de données ou la fabrique de données Azure tooan de services de calcul. Dans cette étape, vous liez votre compte de stockage Azure et d’un traitement par lots Azure compte tooyour data factory.

#### <a name="create-azure-storage-linked-service"></a>Créer le service lié Stockage Azure
1. Cliquez sur hello **auteur et déployer** vignette sur hello **DATA FACTORY** panneau pour **CustomActivityFactory**. Vous consultez hello éditeur Data Factory.
2. Cliquez sur **nouveau magasin de données** hello de barre de commandes et choisissez **le stockage Azure**. Vous devez voir hello script JSON pour la création d’un stockage Azure lié à service dans l’éditeur de hello.
    
    ![Nouveau magasin de données - Stockage Azure](media/data-factory-use-custom-activities/new-data-store-menu.png)
3. Remplacez `<accountname>` avec le nom de votre compte de stockage Azure et `<accountkey>` avec la clé d’accès de hello compte de stockage Azure. toolearn comment tooget votre stockage accéder aux clés, voir [clés d’accès afficher, copier et régénérer stockage](../storage/common/storage-create-storage-account.md#manage-your-storage-account).

    ![Service lié Stockage Azure](media/data-factory-use-custom-activities/azure-storage-linked-service.png)
4. Cliquez sur **déployer** sur toodeploy hello lié service de la barre de commandes hello.

#### <a name="create-azure-batch-linked-service"></a>Créer un service lié Azure Batch
1. Bonjour éditeur Data Factory, cliquez sur **... Plus** dans la barre de commandes hello, cliquez sur **nouveau calcul**, puis sélectionnez **Azure Batch** à partir du menu de hello.

    ![Nouveau calcul - Azure Batch](media/data-factory-use-custom-activities/new-azure-compute-batch.png)
2. Rendre hello modifications toohello JSON script suivant :

   1. Spécifiez le nom du compte Azure Batch pour hello **accountName** propriété. Hello **URL** de hello **Panneau de compte Azure Batch** est Bonjour suivant le format : `http://accountname.region.batch.azure.com`. Pourquoi **batchUri** propriété hello JSON, vous devez tooremove `accountname.` de hello URL et l’utilisation de hello `accountname` pour hello `accountName` propriété JSON.
   2. Spécifiez la clé de compte Azure Batch hello pour hello **accessKey** propriété.
   3. Spécifiez nom hello de pool hello vous avez créé dans le cadre de la configuration requise pour hello **poolName** propriété. Vous pouvez également spécifier les ID hello du pool hello au lieu du nom de hello du pool de hello.
   4. Spécifiez l’URI du lot Azure pour hello **batchUri** propriété. Exemple : `https://westus.batch.azure.com`.  
   5. Spécifiez hello **AzureStorageLinkedService** pour hello **linkedServiceName** propriété.

        ```json
        {
         "name": "AzureBatchLinkedService",
         "properties": {
           "type": "AzureBatch",
           "typeProperties": {
             "accountName": "myazurebatchaccount",
             "batchUri": "https://westus.batch.azure.com",
             "accessKey": "<yourbatchaccountkey>",
             "poolName": "myazurebatchpool",
             "linkedServiceName": "AzureStorageLinkedService"
           }
         }
        }
        ```

       Pourquoi **poolName** propriété, vous pouvez également spécifier d’ID hello du pool hello au lieu du nom de hello du pool de hello.

      > [!IMPORTANT]
      > Hello service Data Factory ne prend en charge une option à la demande de traitement par lots Azure comme il le fait pour HDInsight. Vous pouvez uniquement utiliser votre propre pool Azure Batch dans une fabrique de données Azure.   
    

### <a name="step-3-create-datasets"></a>Étape 3 : Créer les jeux de données
Dans cette étape, vous créez une entrée de toorepresent de jeux de données et les données de sortie.

#### <a name="create-input-dataset"></a>Créer le jeu de données d’entrée
1. Bonjour **éditeur** pour hello fabrique de données, cliquez sur **... Plus** dans la barre de commandes hello, cliquez sur **nouveau dataset**, puis sélectionnez **le stockage Blob Azure** à partir du menu déroulant de hello.
2. Remplacez hello JSON dans le volet de droite hello hello suivant extrait de code JSON :

    ```json
    {
     "name": "InputDataset",
     "properties": {
         "type": "AzureBlob",
         "linkedServiceName": "AzureStorageLinkedService",
         "typeProperties": {
             "folderPath": "adftutorial/customactivityinput/",
             "format": {
                 "type": "TextFormat"
             }
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

   Plus loin dans cette procédure pas à pas, vous allez créer un pipeline associé à l’heure de début 2016-11-16T00:00:00Z et à l’heure de fin 2016-11-16T05:00:00Z. Ce sont des données de tooproduce planifiée toutes les heures, il y a cinq tranches d’entrée/sortie (entre **00**: 00:00 -> **05**: 00:00).

   Hello **fréquence** et **intervalle** de jeu de données d’entrée hello est défini trop**heure** et **1**, ce qui signifie que hello entrée tranche est disponible toutes les heures. Dans cet exemple, il est même hello hello intputfolder fichier (fichier.txt).

   Voici les heures de début hello pour chaque secteur, qui est représentée par la variable de système SliceStart Bonjour ci-dessus extrait de code JSON.
3. Cliquez sur **déployer** hello toocreate de barre d’outils et déployer hello **InputDataset**. Vérifiez que vous voyez hello **TABLE créée avec succès** message sur la barre de titre hello Hello éditeur.

#### <a name="create-an-output-dataset"></a>Créer un jeu de données de sortie
1. Bonjour **l’éditeur Data Factory**, cliquez sur **... Plus** dans la barre de commandes hello, cliquez sur **nouveau dataset**, puis sélectionnez **le stockage Blob Azure**.
2. Remplacez script JSON de hello dans le volet de droite hello hello JSON script suivant :

    ```JSON
    {
        "name": "OutputDataset",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "fileName": "{slice}.txt",
                "folderPath": "adftutorial/customactivityoutput/",
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

     Emplacement de sortie est **adftutorial/customactivityoutput/** et le nom de fichier de sortie est AAAA-MM-JJ-HH.txt où AAAA-MM-JJ-HH est hello year, month, date et l’heure de tranche hello fabriqué. Pour en savoir plus, consultez la page [Référence du développeur][adf-developer-reference].

    Un objet blob/fichier de sortie est généré pour chaque tranche d’entrée. Voici la procédure de nommage des fichiers de sortie pour chaque tranche. Tous les fichiers de sortie hello sont générés dans un dossier de sortie : **adftutorial\customactivityoutput**.

   | Tranche | Heure de début | Fichier de sortie |
   |:--- |:--- |:--- |
   | 1 |2016-11-16T00:00:00 |2016-11-16-00.txt |
   | 2 |2016-11-16T01:00:00 |2016-11-16-01.txt |
   | 3 |2016-11-16T02:00:00 |2016-11-16-02.txt |
   | 4 |2016-11-16T03:00:00 |2016-11-16-03.txt |
   | 5 |2016-11-16T04:00:00 |2016-11-16-04.txt |

    N’oubliez pas que tous les fichiers hello dans un dossier d’entrée font partie d’une section avec des heures de début hello mentionnés ci-dessus. Lorsque cette tranche est traitée, activité personnalisée hello parcourt chaque fichier et produit une ligne dans le fichier de sortie hello avec numéro hello d’occurrences du terme de recherche (« Microsoft »). S’il existe trois fichiers dans hello inputfolder, il existe trois lignes dans le fichier de sortie hello pour chaque tranche horaire : 2016-11-16-00.txt 2016-11-16:01:00:00.txt, etc..
3. toodeploy hello **OutputDataset**, cliquez sur **déployer** sur la barre de commandes hello.

### <a name="create-and-run-a-pipeline-that-uses-hello-custom-activity"></a>Créer et exécuter un pipeline qui utilise l’activité personnalisée hello
1. Bonjour éditeur Data Factory, cliquez sur **... Plus**, puis sélectionnez **nouveau pipeline** sur la barre de commandes hello. 
2. Remplacez hello JSON dans le volet de droite hello hello JSON script suivant :

    ```JSON
    {
      "name": "ADFTutorialPipelineCustom",
      "properties": {
        "description": "Use custom activity",
        "activities": [
          {
            "Name": "MyDotNetActivity",
            "Type": "DotNetActivity",
            "Inputs": [
              {
                "Name": "InputDataset"
              }
            ],
            "Outputs": [
              {
                "Name": "OutputDataset"
              }
            ],
            "LinkedServiceName": "AzureBatchLinkedService",
            "typeProperties": {
              "AssemblyName": "MyDotNetActivity.dll",
              "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
              "PackageLinkedService": "AzureStorageLinkedService",
              "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
              "extendedProperties": {
                "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"
              }
            },
            "Policy": {
              "Concurrency": 2,
              "ExecutionPriorityOrder": "OldestFirst",
              "Retry": 3,
              "Timeout": "00:30:00",
              "Delay": "00:00:00"
            }
          }
        ],
        "start": "2016-11-16T00:00:00Z",
        "end": "2016-11-16T05:00:00Z",
        "isPaused": false
      }
    }
    ```

    Hello Notez les points suivants :

   * **Accès concurrentiel** est défini trop**2** afin que les deux sections sont traitées en parallèle par 2 machines virtuelles dans le pool de traitement par lots Azure hello.
   * Il existe une activité dans la section des activités hello et elle est de type : **DotNetActivity**.
   * **AssemblyName** a la valeur nom toohello Hello DLL : **MyDotnetActivity.dll**.
   * **Point d’entrée** est défini trop**MyDotNetActivityNS.MyDotNetActivity**.
   * **PackageLinkedService** est défini trop**AzureStorageLinkedService** qui pointe le stockage d’objets blob toohello qui contient le fichier zip d’activité personnalisée hello. Si vous n’utilisez pas d’entrée/sortient de différents comptes de stockage Azure pour les fichiers et hello fichier zip d’activité personnalisée, vous créez un autre service lié Azure Storage. Cet article suppose que vous utilisez hello même compte de stockage Azure.
   * **PackageFile** est défini trop**customactivitycontainer/MyDotNetActivity.zip**. Il est au format de hello : containerforthezip/nameofthezip.zip.
   * activité personnalisée Hello prend **InputDataset** en tant qu’entrée et **OutputDataset** en tant que sortie.
   * propriété de linkedServiceName Hello d’activité personnalisée hello pointe toohello **AzureBatchLinkedService**, ce qui indique à Azure Data Factory pour cette activité personnalisée hello doit toorun sur des machines virtuelles de traitement par lots Azure.
   * **isPaused** propriété a la valeur trop**false** par défaut. pipeline de Hello s’exécute immédiatement dans cet exemple, car le début des tranches de hello Bonjour passées. Vous pouvez définir ce pipeline de propriété tootrue toopause hello et affectez-lui arrière toofalse toorestart.
   * Hello **Démarrer** temps et **fin** heures sont **cinq** heures éloignés et tranches produites toutes les heures, afin de cinq tranches sont produits par le pipeline de hello.
3. pipeline de hello toodeploy, cliquez sur **déployer** sur la barre de commandes hello.

### <a name="monitor-hello-pipeline"></a>Pipeline d’analyse hello
1. Dans le panneau de la fabrique de données hello Bonjour portail Azure, cliquez sur **diagramme**.

    ![Vignette schématique](./media/data-factory-use-custom-activities/DataFactoryBlade.png)
2. Bonjour vue de diagramme, cliquez maintenant sur hello OutputDataset.

    ![Vue schématique](./media/data-factory-use-custom-activities/diagram.png)
3. Vous devez voir que les cinq tranches de sortie hello sont dans l’état prêt hello. S’ils ne sont pas dans l’état prêt hello, ils n’ont pas encore été générés. 

   ![Tranches de sortie](./media/data-factory-use-custom-activities/OutputSlices.png)
4. Vérifiez que les fichiers de sortie hello sont générées dans le stockage blob hello hello **adftutorial** conteneur.

   ![Sortie de l’activité personnalisée][image-data-factory-ouput-from-custom-activity]
5. Si vous ouvrez le fichier de sortie hello, vous devez voir hello toohello similaire après la sortie de sortie :

    ```
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2016-11-16-00/file.txt.
    ```
6. Hello d’utilisation [portail Azure] [ azure-preview-portal] ou toomonitor d’applets de commande Azure PowerShell votre fabrique de données, les pipelines et les jeux de données. Vous pouvez voir des messages à partir de hello **ActivityLogger** dans le code hello pour une activité personnalisée hello dans les journaux de hello (spécifiquement 0.log utilisateur) que vous pouvez télécharger à partir de portail de hello ou à l’aide des applets de commande.

   ![Téléchargement des journaux d’activités personnalisées][image-data-factory-download-logs-from-custom-activity]

Pour découvrir la procédure détaillée de surveillance des jeux de données et des pipelines, consultez l’article [Surveiller et gérer les pipelines](data-factory-monitor-manage-pipelines.md) .      

## <a name="data-factory-project-in-visual-studio"></a>Projet Data Factory dans Visual Studio  
Vous pouvez créer et publier des entités Data Factory à l’aide de Visual Studio au lieu d’utiliser le portail Azure. Pour plus d’informations sur la création et les entités de fabrique de données de publication à l’aide de Visual Studio, consultez [générer votre première pipeline à l’aide de Visual Studio](data-factory-build-your-first-pipeline-using-vs.md) et [copier les données d’objets Blob Azure tooAzure SQL](data-factory-copy-activity-tutorial-using-visual-studio.md) articles.

Hello suivant les étapes supplémentaires si vous créez un projet de la fabrique de données dans Visual Studio :
 
1. Ajoutez hello Data Factory projet toohello solution Visual Studio qui contient le projet d’activité personnalisée hello. 
2. Ajouter un projet d’activité de référence toohello .NET à partir du projet de Data Factory hello. Cliquez sur le projet de la fabrique de données, pointez trop**ajouter**, puis cliquez sur **référence**. 
3. Bonjour **ajouter une référence** boîte de dialogue, sélectionnez hello **MyDotNetActivity** le projet, puis cliquez sur **OK**.
4. Générer et publier des solutions de hello.

    > [!IMPORTANT]
    > Lorsque vous publiez des entités de fabrique de données, un fichier zip est créé automatiquement pour vous et est le conteneur d’objets blob téléchargés toohello : customactivitycontainer. Si le conteneur d’objets blob hello n’existe pas, il est automatiquement créé trop.  


## <a name="data-factory-and-batch-integration"></a>Intégration de Data Factory et Batch
Hello service Data Factory crée un travail en traitement par lots Azure avec le nom de hello : **adf-poolname : xxx-travail**. Cliquez sur **travaux** à partir du menu de gauche hello. 

![Azure Data Factory - Travaux Batch](media/data-factory-use-custom-activities/data-factory-batch-jobs.png)

Une tâche est créée pour chaque exécution d’activité d’une tranche. S’il existe cinq toobe prêt tranches traitées, cinq tâches sont créés dans cette tâche. S’il existe plusieurs nœuds de calcul dans le pool de traitement par lots de hello, deux ou plusieurs secteurs peuvent s’exécuter en parallèle. Si le nombre maximum de tâches hello par jeu de nœud de calcul trop > 1, vous pouvez également avoir plusieurs tranches en cours d’exécution sur hello même calcul.

![Azure Data Factory - Tâches de travaux Batch](media/data-factory-use-custom-activities/data-factory-batch-job-tasks.png)

Hello suivant schéma illustre les relations de hello entre les tâches Azure Data Factory et de traitement par lots.

![Data Factory et Batch](./media/data-factory-use-custom-activities/DataFactoryAndBatch.png)

## <a name="troubleshoot-failures"></a>Résoudre les défaillances
Quelques techniques de base peuvent être utilisées pour résoudre les défaillances :

1. Si vous voyez hello l’erreur suivante, vous utilisez peut-être un stockage d’objets blob à chaud/utile au lieu d’utiliser un stockage d’objets blob Azure à usage général. Télécharger hello zip fichier tooa **compte de stockage Azure à usage général**. 
 
    ```
    Error in Activity: Job encountered scheduling error. Code: BlobDownloadMiscError Category: ServerError Message: Miscellaneous error encountered while downloading one of hello specified Azure Blob(s).
    ``` 
2. Si vous voyez hello l’erreur suivante, confirmez ce nom hello de classe hello hello CS nom de fichier correspond à hello vous avez spécifié pour hello **EntryPoint** propriété dans le code JSON de pipeline hello. Procédure pas à pas de hello, nom de classe hello est : MyDotNetActivity et hello EntryPoint Bonjour JSON est : MyDotNetActivityNS. **MyDotNetActivity**.

    ```
    MyDotNetActivity assembly does not exist or doesn't implement hello type Microsoft.DataFactories.Runtime.IDotNetActivity properly
    ```

   Si les noms de hello ne correspondent pas, vérifiez que tous les fichiers binaires de hello sont Bonjour **dossier racine** du fichier zip de hello. Autrement dit, lorsque vous ouvrez le fichier zip de hello, vous devez voir tous les fichiers hello dans le dossier racine de hello, et non dans les sous-dossiers.   
3. Si la tranche de hello d’entrée n’est pas défini trop**prêt**, vérifiez que la structure de dossiers d’entrée de hello est correcte et **fichier.txt** existe dans les dossiers d’entrée hello.
3. Bonjour **Execute** méthode de votre activité personnalisée, utilisez hello **IActivityLogger** informations toolog objet qui vous permet de résoudre les problèmes. messages Hello connecté apparaissent dans les fichiers journaux utilisateur hello (un ou plusieurs fichiers nommés : 0.log de l’utilisateur, utilisateur-1.log, 2.log de l’utilisateur, etc..).

   Bonjour **OutputDataset** panneau, cliquez sur Bonjour tranche toosee Bonjour **tranche de données** panneau pour ce secteur. Les **activités exécutées** pour cette tranche s’affichent. Vous devez voir une activité à exécuter pour la tranche de hello. Si vous cliquez sur Exécuter dans la barre de commandes hello, vous pouvez démarrer une autre activité exécutée pour hello même secteur.

   Lorsque vous cliquez sur exécution de l’activité hello, vous voyez hello **détails de l’activité exécuter** panneau avec une liste des fichiers journaux. Vous consultez les messages enregistrés dans le fichier de user_0.log hello. Lorsqu’une erreur se produit, vous voyez trois exécutions d’activité, car de nouvelles tentatives hello est définie too3 dans pipeline/activité hello JSON. Lorsque vous cliquez sur exécution de l’activité hello, vous voyez que vous pouvez consulter les erreurs de hello tootroubleshoot des fichiers journaux hello.

   Dans la liste hello des fichiers journaux, cliquez sur hello **0.log de l’utilisateur**. Dans le panneau droit hello sont des résultats de l’utilisation de hello hello **IActivityLogger.Write** (méthode). Si vous ne voyez pas tous les messages, vérifiez si vous avez plusieurs fichiers journaux nommés user_1.log, user_2.log, etc. Sinon, code de hello a peut-être échoué après que hello du dernier message connecté.

   En outre, consultez **system-0.log** pour vérifier les exceptions et messages d’erreur système éventuels.
4. Inclure hello **PDB** fichiers dans le fichier zip de hello afin que les détails de l’erreur hello ont des informations telles que **pile des appels** lorsqu’une erreur se produit.
5. Tous les hello des fichiers dans le fichier zip de hello pour l’activité personnalisée hello doit se trouver au hello **niveau supérieur** avec aucune sous-dossiers.
6. Vérifiez que hello **assemblyName** (MyDotNetActivity.dll), **entryPoint**(MyDotNetActivityNS.MyDotNetActivity), **packageFile** (customactivitycontainer / MyDotNetActivity.zip), et **packageLinkedService** (doit pointer toohello **à usage général**stockage d’objets blob Azure qui contient le fichier zip de hello) sont définies les valeurs toocorrect.
7. Si vous avez corrigé une tranche hello tooreprocess erreur et que vous souhaitez, cliquez sur tranche hello Bonjour **OutputDataset** panneau, cliquez sur **exécuter**.
8. Si vous voyez hello l’erreur suivante, vous utilisez le package de stockage Azure hello de version > 4.3.0. Lanceur de service de fabrique de données nécessite la version de hello 4.3 de WindowsAzure.Storage. Consultez [isolement de Appdomain](#appdomain-isolation) section pour résoudre ce problème, si vous devez utiliser hello une version ultérieure de l’assembly de stockage Azure. 

    ```
    Error in Activity: Unknown error in module: System.Reflection.TargetInvocationException: Exception has been thrown by hello target of an invocation. ---> System.TypeLoadException: Could not load type 'Microsoft.WindowsAzure.Storage.Blob.CloudBlob' from assembly 'Microsoft.WindowsAzure.Storage, Version=4.3.0.0, Culture=neutral, 
    ```

    Si vous pouvez utiliser la version de hello 4.3.0 de package Azure Storage, supprimez hello référence tooAzure stockage package existant de version > 4.3.0. Ensuite, exécutez hello de commande suivante à partir de la Console du Gestionnaire de Package NuGet. 

    ```PowerShell
    Install-Package WindowsAzure.Storage -Version 4.3.0
    ```

    Générez le projet de hello. Supprimez l’assembly Azure.Storage de version > 4.3.0 à partir du dossier bin\Debug hello. Créer un fichier zip avec des fichiers binaires et le fichier PDB hello. Remplacer l’ancien fichier zip de hello par celui-ci dans le conteneur d’objets blob hello (customactivitycontainer). Hello de réexécuter tranches ayant échoué (tranche d’avec le bouton droit et cliquez sur Exécuter).   
8. activité personnalisée Hello n’utilise pas hello **app.config** fichier à partir de votre package. Par conséquent, si votre code lit les chaînes de connexion à partir du fichier de configuration hello, il ne fonctionne pas lors de l’exécution. Hello meilleures pratiques lors de l’utilisation d’Azure Batch est toohold les clés secrètes dans un **Azure KeyVault**, utilisez un Bonjour tooprotect principal de service basé sur le certificat **keyvault**et distribuer des certificats de hello tooAzure pool de traitement par lots. Hello les activités personnalisées .NET puis peuvent accéder aux clés secrètes hello KeyVault lors de l’exécution. Cette solution est une solution générique et peut évoluer type tooany du secret, pas seulement les chaînes de connexion.

   Il existe une solution plus facile (mais pas une meilleure pratique) : vous pouvez créer un **service lié Azure SQL** avec les paramètres de chaîne de connexion, créez un dataset qu’utilise hello service lié et le jeu de données chaîne hello comme un jeu de données d’entrée factice activité de .NET personnalisée toohello. Vous pouvez ensuite hello d’accès liées la chaîne de connexion du service dans le code d’activité personnalisée hello.  

## <a name="update-custom-activity"></a>Mettre à jour l’activité personnalisée
Si vous mettez à jour le code hello pour une activité personnalisée hello, générer et télécharger le fichier compressé hello qui contient le nouveau stockage d’objets blob binaires toohello.

## <a name="appdomain-isolation"></a>Isolation du domaine d’application
Consultez [exemple de AppDomain Cross](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/CrossAppDomainDotNetActivitySample) qui vous montre comment toocreate une activité personnalisée qui n’est pas contraint versions tooassembly utilisées hello Data Factory (exemple : WindowsAzure.Storage v4.3.0, Newtonsoft.Json v6.0.x, etc..).

## <a name="access-extended-properties"></a>Accéder aux propriétés étendues
Vous pouvez déclarer des propriétés étendues dans l’activité hello JSON comme indiqué dans hello suivant l’exemple :

```JSON
"typeProperties": {
  "AssemblyName": "MyDotNetActivity.dll",
  "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
  "PackageLinkedService": "AzureStorageLinkedService",
  "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
  "extendedProperties": {
    "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))",
    "DataFactoryName": "CustomActivityFactory"
  }
},
```


Dans l’exemple de hello, il existe deux propriétés étendues : **SliceStart** et **DataFactoryName**. valeur de Hello pour SliceStart est basée sur la variable de système SliceStart hello. Consultez [Variables système](data-factory-functions-variables.md) pour obtenir la liste des variables système prises en charge. valeur Hello DataFactoryName est codé en dur les tooCustomActivityFactory.

tooaccess ces les propriétés étendues à hello **Execute** méthode toohello similaires du code utilisation suivante du code :

```csharp
// tooget extended properties (for example: SliceStart)
DotNetActivity dotNetActivity = (DotNetActivity)activity.TypeProperties;
string sliceStartString = dotNetActivity.ExtendedProperties["SliceStart"];

// toolog all extended properties                               
IDictionary<string, string> extendedProperties = dotNetActivity.ExtendedProperties;
logger.Write("Logging extended properties if any...");
foreach (KeyValuePair<string, string> entry in extendedProperties)
{
    logger.Write("<key:{0}> <value:{1}>", entry.Key, entry.Value);
}
```

## <a name="auto-scaling-of-azure-batch"></a>Mise à l’échelle automatique d’Azure Batch
Vous pouvez aussi créer un pool Azure Batch avec la fonctionnalité **autoscale** . Par exemple, vous pouvez créer un pool de traitement par lots azure avec des machines virtuelles de dédié 0 et une formule de mise à l’échelle en fonction du nombre de hello de tâches en attente. 

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

## <a name="use-hdinsight-compute-service"></a>Utiliser le service de calcul HDInsight
Hello procédure pas à pas, vous avez utilisé des activités personnalisées de traitement par lots Azure compute toorun hello. Vous pouvez également utiliser votre propre cluster HDInsight de basés sur Windows ou avez Data Factory créer une cluster HDInsight de basés sur Windows sur demande et activité personnalisée hello s’exécutent sur le cluster HDInsight de hello. Voici les étapes principales hello à l’aide d’un cluster HDInsight.

> [!IMPORTANT]
> activités de .NET personnalisées Hello s’exécutent uniquement sur des clusters HDInsight de basés sur Windows. Une solution de contournement pour cette limitation est toouse hello carte réduire toorun personnalisé Java code d’activité sur un cluster HDInsight de basés sur Linux. Une autre option consiste à toouse un pool de traitement par lots Azure d’activités personnalisées de machines virtuelles toorun au lieu d’utiliser un cluster HDInsight.
 

1. Créez un service lié Azure HDInsight.   
2. Utilisez HDInsight lié service à la place de **AzureBatchLinkedService** Bonjour JSON de pipeline.

Si vous souhaitez tootest avec hello procédure pas à pas, modification **Démarrer** et **fin** fois pour le pipeline de hello afin que vous pouvez tester le scénario hello avec hello service Azure HDInsight.

#### <a name="create-azure-hdinsight-linked-service"></a>Créer le service lié Azure HDInsight
Hello service Azure Data Factory prend en charge la création d’un cluster à la demande et données de sortie d’entrée tooproduce tooprocess l’utiliser. Vous pouvez également utiliser votre propre cluster tooperform hello identiques. Lorsque vous utilisez un cluster HDInsight à la demande, un cluster est créé pour chaque tranche. Alors que, si vous utilisez votre propre cluster HDInsight, cluster de hello est prêt tooprocess hello immédiatement la tranche. Par conséquent, lorsque vous utilisez le cluster de la demande, vous ne pouvez pas voir les données de sortie hello aussi rapidement que lorsque vous utilisez votre propre cluster.

> [!NOTE]
> Lors de l’exécution, une instance d’une activité .NET s’exécute uniquement sur un nœud de travail dans le cluster HDInsight de hello ; Il ne peut pas être mis à l’échelle toorun sur plusieurs nœuds. Plusieurs instances d’activité .NET peuvent s’exécuter en parallèle sur différents nœuds du cluster HDInsight de hello.
>
>

##### <a name="toouse-an-on-demand-hdinsight-cluster"></a>toouse un cluster de HDInsight à la demande
1. Bonjour **portail Azure**, cliquez sur **auteur et à déployer** dans la page d’accueil de Data Factory hello.
2. Bonjour éditeur Data Factory, cliquez sur **nouveau calcul** à partir de la commande hello barre et sélectionnez **cluster à la demande HDInsight** à partir du menu de hello.
3. Rendre hello modifications toohello JSON script suivant :

   1. Pourquoi **la taille du cluster** propriété, spécifiez la taille hello du cluster HDInsight de hello.
   2. Pourquoi **timeToLive** propriété, spécifiez la durée pendant laquelle les clients hello peuvent être inactif avant d’être supprimé.
   3. Pourquoi **version** propriété, spécifiez la version de HDInsight hello souhaité toouse. Si vous excluez cette propriété, la version la plus récente hello est utilisée.  
   4. Pourquoi **linkedServiceName**, spécifiez **AzureStorageLinkedService**.

        ```JSON
        {
           "name": "HDInsightOnDemandLinkedService",
           "properties": {
               "type": "HDInsightOnDemand",
               "typeProperties": {
                   "clusterSize": 4,
                   "timeToLive": "00:05:00",
                   "osType": "Windows",
                   "linkedServiceName": "AzureStorageLinkedService",
               }
           }
        }
        ```

    > [!IMPORTANT]
    > activités de .NET personnalisées Hello s’exécutent uniquement sur des clusters HDInsight de basés sur Windows. Une solution de contournement pour cette limitation est toouse hello carte réduire toorun personnalisé Java code d’activité sur un cluster HDInsight de basés sur Linux. Une autre option consiste à toouse un pool de traitement par lots Azure d’activités personnalisées de machines virtuelles toorun au lieu d’utiliser un cluster HDInsight.

4. Cliquez sur **déployer** sur toodeploy hello lié service de la barre de commandes hello.

##### <a name="toouse-your-own-hdinsight-cluster"></a>toouse votre propre cluster HDInsight :
1. Bonjour **portail Azure**, cliquez sur **auteur et à déployer** dans la page d’accueil de Data Factory hello.
2. Bonjour **éditeur Data Factory**, cliquez sur **nouveau calcul** à partir de la commande hello barre et sélectionnez **cluster HDInsight** à partir du menu de hello.
3. Rendre hello modifications toohello JSON script suivant :

   1. Pourquoi **clusterUri** propriété, entrez les URL hello pour votre HDInsight. Par exemple : https://<clustername>.azurehdinsight.net/.     
   2. Pourquoi **nom d’utilisateur** propriété, entrez les nom d’utilisateur hello qui possède le cluster d’accès toohello HDInsight.
   3. Pourquoi **mot de passe** propriété, entrez le mot de passe de hello pour l’utilisateur de hello.
   4. Pourquoi **LinkedServiceName** propriété, entrez **AzureStorageLinkedService**.
4. Cliquez sur **déployer** sur toodeploy hello lié service de la barre de commandes hello.

Pour plus d’informations, consultez [Services de calcul liés](data-factory-compute-linked-services.md) .

Bonjour **JSON de pipeline**, utilisez HDInsight (à la demande ou votre propre) service lié :

```JSON
{
  "name": "ADFTutorialPipelineCustom",
  "properties": {
    "description": "Use custom activity",
    "activities": [
      {
        "Name": "MyDotNetActivity",
        "Type": "DotNetActivity",
        "Inputs": [
          {
            "Name": "InputDataset"
          }
        ],
        "Outputs": [
          {
            "Name": "OutputDataset"
          }
        ],
        "LinkedServiceName": "HDInsightOnDemandLinkedService",
        "typeProperties": {
          "AssemblyName": "MyDotNetActivity.dll",
          "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
          "PackageLinkedService": "AzureStorageLinkedService",
          "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
          "extendedProperties": {
            "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"
          }
        },
        "Policy": {
          "Concurrency": 2,
          "ExecutionPriorityOrder": "OldestFirst",
          "Retry": 3,
          "Timeout": "00:30:00",
          "Delay": "00:00:00"
        }
      }
    ],
    "start": "2016-11-16T00:00:00Z",
    "end": "2016-11-16T05:00:00Z",
    "isPaused": false
  }
}
```

## <a name="create-a-custom-activity-by-using-net-sdk"></a>Créer une activité personnalisée à l’aide du kit .NET SDK
Dans la procédure pas à pas hello dans cet article, vous créez une fabrique de données avec un pipeline qui utilise l’activité personnalisée hello à l’aide de hello portail Azure. Hello suivant de code montre comment toocreate hello fabrique de données à l’aide du SDK .NET à la place. Vous trouverez plus d’informations sur l’utilisation du Kit de développement logiciel tooprogrammatically créer des pipelines dans hello [créer un pipeline avec l’activité de copie à l’aide des API .NET](data-factory-copy-activity-tutorial-using-dotnet-api.md) l’article. 

```csharp
using System;
using System.Configuration;
using System.Collections.ObjectModel;
using System.Threading;
using System.Threading.Tasks;

using Microsoft.Azure;
using Microsoft.Azure.Management.DataFactories;
using Microsoft.Azure.Management.DataFactories.Models;
using Microsoft.Azure.Management.DataFactories.Common.Models;

using Microsoft.IdentityModel.Clients.ActiveDirectory;
using System.Collections.Generic;

namespace DataFactoryAPITestApp
{
    class Program
    {
        static void Main(string[] args)
        {
            // create data factory management client

            // TODO: replace ADFTutorialResourceGroup with hello name of your resource group.
            string resourceGroupName = "ADFTutorialResourceGroup";

            // TODO: replace APITutorialFactory with a name that is globally unique. For example: APITutorialFactory04212017
            string dataFactoryName = "APITutorialFactory";

            TokenCloudCredentials aadTokenCredentials = new TokenCloudCredentials(
                ConfigurationManager.AppSettings["SubscriptionId"],
                GetAuthorizationHeader().Result);

            Uri resourceManagerUri = new Uri(ConfigurationManager.AppSettings["ResourceManagerEndpoint"]);

            DataFactoryManagementClient client = new DataFactoryManagementClient(aadTokenCredentials, resourceManagerUri);

            Console.WriteLine("Creating a data factory");
            client.DataFactories.CreateOrUpdate(resourceGroupName,
                new DataFactoryCreateOrUpdateParameters()
                {
                    DataFactory = new DataFactory()
                    {
                        Name = dataFactoryName,
                        Location = "westus",
                        Properties = new DataFactoryProperties()
                    }
                }
            );

            // create a linked service for input data store: Azure Storage
            Console.WriteLine("Creating Azure Storage linked service");
            client.LinkedServices.CreateOrUpdate(resourceGroupName, dataFactoryName,
                new LinkedServiceCreateOrUpdateParameters()
                {
                    LinkedService = new LinkedService()
                    {
                        Name = "AzureStorageLinkedService",
                        Properties = new LinkedServiceProperties
                        (
                            // TODO: Replace <accountname> and <accountkey> with name and key of your Azure Storage account.
                            new AzureStorageLinkedService("DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>")
                        )
                    }
                }
            );

            // create a linked service for output data store: Azure SQL Database
            Console.WriteLine("Creating Azure Batch linked service");
            client.LinkedServices.CreateOrUpdate(resourceGroupName, dataFactoryName,
                new LinkedServiceCreateOrUpdateParameters()
                {
                    LinkedService = new LinkedService()
                    {
                        Name = "AzureBatchLinkedService",
                        Properties = new LinkedServiceProperties
                        (
                            // TODO: replace <batchaccountname> and <yourbatchaccountkey> with name and key of your Azure Batch account
                            new AzureBatchLinkedService("<batchaccountname>", "https://westus.batch.azure.com", "<yourbatchaccountkey>", "myazurebatchpool", "AzureStorageLinkedService")
                        )
                    }
                }
            );

            // create input and output datasets
            Console.WriteLine("Creating input and output datasets");
            string Dataset_Source = "InputDataset";
            string Dataset_Destination = "OutputDataset";

            Console.WriteLine("Creating input dataset of type: Azure Blob");
            client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,

                new DatasetCreateOrUpdateParameters()
                {
                    Dataset = new Dataset()
                    {
                        Name = Dataset_Source,
                        Properties = new DatasetProperties()
                        {
                            LinkedServiceName = "AzureStorageLinkedService",
                            TypeProperties = new AzureBlobDataset()
                            {
                                FolderPath = "adftutorial/customactivityinput/",
                                Format = new TextFormat()
                            },
                            External = true,
                            Availability = new Availability()
                            {
                                Frequency = SchedulePeriod.Hour,
                                Interval = 1,
                            },

                            Policy = new Policy() { }
                        }
                    }
                });

            Console.WriteLine("Creating output dataset of type: Azure Blob");
            client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,
                new DatasetCreateOrUpdateParameters()
                {
                    Dataset = new Dataset()
                    {
                        Name = Dataset_Destination,
                        Properties = new DatasetProperties()
                        {
                            LinkedServiceName = "AzureStorageLinkedService",
                            TypeProperties = new AzureBlobDataset()
                            {
                                FileName = "{slice}.txt",
                                FolderPath = "adftutorial/customactivityoutput/",
                                PartitionedBy = new List<Partition>()
                                {
                                    new Partition()
                                    {
                                        Name = "slice",
                                        Value = new DateTimePartitionValue()
                                        {
                                            Date = "SliceStart",
                                            Format = "yyyy-MM-dd-HH"
                                        }
                                    }
                                }
                            },
                            Availability = new Availability()
                            {
                                Frequency = SchedulePeriod.Hour,
                                Interval = 1,
                            },
                        }
                    }
                });

            Console.WriteLine("Creating a custom activity pipeline");
            DateTime PipelineActivePeriodStartTime = new DateTime(2017, 3, 9, 0, 0, 0, 0, DateTimeKind.Utc);
            DateTime PipelineActivePeriodEndTime = PipelineActivePeriodStartTime.AddMinutes(60);
            string PipelineName = "ADFTutorialPipelineCustom";

            client.Pipelines.CreateOrUpdate(resourceGroupName, dataFactoryName,
                new PipelineCreateOrUpdateParameters()
                {
                    Pipeline = new Pipeline()
                    {
                        Name = PipelineName,
                        Properties = new PipelineProperties()
                        {
                            Description = "Use custom activity",

                            // Initial value for pipeline's active period. With this, you won't need tooset slice status
                            Start = PipelineActivePeriodStartTime,
                            End = PipelineActivePeriodEndTime,
                            IsPaused = false,

                            Activities = new List<Activity>()
                            {
                                new Activity()
                                {
                                    Name = "MyDotNetActivity",
                                    Inputs = new List<ActivityInput>()
                                    {
                                        new ActivityInput() {
                                            Name = Dataset_Source
                                        }
                                    },
                                    Outputs = new List<ActivityOutput>()
                                    {
                                        new ActivityOutput()
                                        {
                                            Name = Dataset_Destination
                                        }
                                    },
                                    LinkedServiceName = "AzureBatchLinkedService",
                                    TypeProperties = new DotNetActivity()
                                    {
                                        AssemblyName = "MyDotNetActivity.dll",
                                        EntryPoint = "MyDotNetActivityNS.MyDotNetActivity",
                                        PackageLinkedService = "AzureStorageLinkedService",
                                        PackageFile = "customactivitycontainer/MyDotNetActivity.zip",
                                        ExtendedProperties = new Dictionary<string, string>()
                                        {
                                            { "SliceStart", "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"}
                                        }
                                    },
                                    Policy = new ActivityPolicy()
                                    {
                                        Concurrency = 2,
                                        ExecutionPriorityOrder = "OldestFirst",
                                        Retry = 3,
                                        Timeout = new TimeSpan(0,0,30,0),
                                        Delay = new TimeSpan()
                                    }
                                }
                            }
                        }
                    }
                });
        }

        public static async Task<string> GetAuthorizationHeader()
        {
            AuthenticationContext context = new AuthenticationContext(ConfigurationManager.AppSettings["ActiveDirectoryEndpoint"] + ConfigurationManager.AppSettings["ActiveDirectoryTenantId"]);
            ClientCredential credential = new ClientCredential(
                ConfigurationManager.AppSettings["ApplicationId"],
                ConfigurationManager.AppSettings["Password"]);
            AuthenticationResult result = await context.AcquireTokenAsync(
                resource: ConfigurationManager.AppSettings["WindowsManagementUri"],
                clientCredential: credential);

            if (result != null)
                return result.AccessToken;

            throw new InvalidOperationException("Failed tooacquire token");
        }
    }
}
```

## <a name="debug-custom-activity-in-visual-studio"></a>Déboguer une activité personnalisée dans Visual Studio
Hello [Azure Data Factory - environnement local](https://github.com/gbrueckl/Azure.DataFactory.LocalEnvironment) exemple sur GitHub inclut un outil qui vous permet de toodebug des activités .NET personnalisées dans Visual Studio.  


## <a name="sample-custom-activities-on-github"></a>Exemples d’activités personnalisées sur GitHub
| Exemple | Rôle des activités personnalisées |
| --- | --- |
| [Téléchargeur de données HTTP](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/HttpDataDownloaderSample). |Télécharge des données à partir d’un point de terminaison HTTP de tooAzure stockage d’objets Blob à l’aide de c# activité personnalisée dans la fabrique de données. |
| [Exemple d’analyse d’opinions Twitter](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TwitterAnalysisSample-CustomC%23Activity) |Appelle un modèle Azure ML et effectue l’analyse, la notation, la prédiction, etc. des opinions. |
| [Exécuter un script R](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample). |Appelle un script R en exécutant RScript.exe sur votre cluster HDInsight, sur lequel R est installé. |
| [Activité .NET entre AppDomains](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/CrossAppDomainDotNetActivitySample) |Utilise des versions d’assembly différentes de celles utilisées par le service de lancement de Data Factory hello |
| [Retraiter un modèle dans Azure Analysis Services](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/AzureAnalysisServicesProcessSample) |  Retraite un modèle dans Azure Analysis Services. |

[batch-net-library]: ../batch/batch-dotnet-get-started.md
[batch-create-account]: ../batch/batch-account-create-portal.md
[batch-technical-overview]: ../batch/batch-technical-overview.md
[batch-get-started]: ../batch/batch-dotnet-get-started.md
[use-custom-activities]: data-factory-use-custom-activities.md
[troubleshoot]: data-factory-troubleshoot.md
[data-factory-introduction]: data-factory-introduction.md
[azure-powershell-install]: https://github.com/Azure/azure-sdk-tools/releases


[developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[cmdlet-reference]: http://go.microsoft.com/fwlink/?LinkId=517456

[new-azure-batch-account]: https://msdn.microsoft.com/library/mt125880.aspx
[new-azure-batch-pool]: https://msdn.microsoft.com/library/mt125936.aspx
[azure-batch-blog]: http://blogs.technet.com/b/windowshpc/archive/2014/10/28/using-azure-powershell-to-manage-azure-batch-account.aspx

[nuget-package]: http://go.microsoft.com/fwlink/?LinkId=517478
[adf-developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[azure-preview-portal]: https://portal.azure.com/

[adfgetstarted]: data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[hivewalkthrough]: data-factory-data-transformation-activities.md

[image-data-factory-ouput-from-custom-activity]: ./media/data-factory-use-custom-activities/OutputFilesFromCustomActivity.png

[image-data-factory-download-logs-from-custom-activity]: ./media/data-factory-use-custom-activities/DownloadLogsFromCustomActivity.png
