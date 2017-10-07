---
title: "Didacticiel : Créer un pipeline avec l’activité de copie à l’aide de l’API .NET | Microsoft Docs"
description: "Dans ce didacticiel, vous allez créer un pipeline Azure Data Factory avec une activité de copie à l’aide de l’API .NET."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 58fc4007-b46d-4c8e-a279-cb9e479b3e2b
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 52f72da54cdd80691e09d7453bf6730454c4089e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-net-api"></a>Didacticiel : Créer un pipeline avec l’activité de copie à l’aide de l’API .NET
> [!div class="op_single_selector"]
> * [Vue d’ensemble et étapes préalables requises](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [Assistant de copie](data-factory-copy-data-wizard-tutorial.md)
> * [Portail Azure](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)
> * [Modèle Azure Resource Manager](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [API REST](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [API .NET](data-factory-copy-activity-tutorial-using-dotnet-api.md)

Dans cet article, vous apprendrez comment toouse [API .NET](https://portal.azure.com) toocreate une fabrique de données avec un pipeline qui copie les données à partir d’une base de données SQL Azure de tooan stockage blob Azure. Si vous êtes tooAzure nouvelle fabrique de données, lisez hello [Introduction tooAzure Data Factory](data-factory-introduction.md) article avant d’entamer ce didacticiel.   

Dans ce didacticiel, vous créez un pipeline avec une activité : activité de copie. activité de copie Hello copie des données à partir d’un magasin de données de données pris en charge magasin tooa récepteur pris en charge. Pour obtenir la liste des magasins de données pris en charge en tant que sources et récepteurs, consultez [Magasins de données pris en charge](data-factory-data-movement-activities.md#supported-data-stores-and-formats). activité Hello est rendue possible par un service globalement disponible qui permettre copier des données entre différentes banques de données de manière sécurisée, fiable et évolutive. Pour plus d’informations sur l’activité de copie de hello, consultez [les activités de déplacement des données](data-factory-data-movement-activities.md).

Un pipeline peut contenir plusieurs activités. De plus, vous pouvez concaténer les deux activités (exécutée une activité après l’autre) en définissant le dataset de sortie hello d’une activité hello d’entrée dataset Hello autre activité. Pour plus d’informations, consultez [Plusieurs activités dans un pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline). 

> [!NOTE] 
> Pour la documentation complète sur l’API .NET pour Data Factory, consultez [Informations de référence sur l’API .NET Data Factory](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1).
> 
> le pipeline de données Hello dans ce didacticiel copie des données à partir d’un magasin de données de destination source données magasin tooa. Pour obtenir un didacticiel sur la façon de tootransform les données à l’aide d’Azure Data Factory, consultez [didacticiel : créer un pipeline de données tootransform à l’aide de cluster Hadoop](data-factory-build-your-first-pipeline.md).

## <a name="prerequisites"></a>Composants requis
* Passez en revue [vue d’ensemble et conditions préalables](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) tooget une vue d’ensemble du didacticiel de hello et hello complète **condition préalable** étapes.
* Visual Studio 2012, 2013 ou 2015
* Téléchargez et installez le [Kit de développement logiciel (SDK) Azure .NET](http://azure.microsoft.com/downloads/)
* Azure PowerShell. Suivez les instructions de [comment tooinstall et configurer Azure PowerShell](../powershell-install-configure.md) article tooinstall Azure PowerShell sur votre ordinateur. Vous utilisez Azure PowerShell toocreate une application Azure Active Directory.

### <a name="create-an-application-in-azure-active-directory"></a>Créer une application dans Azure Active Directory
Créer une application Azure Active Directory, créez un principal de service pour l’application hello et affectez-le toohello **collaborateur de fabrique de données** rôle.

1. Lancez **PowerShell**.
2. Exécutez hello suivant de commande et entrez le nom d’utilisateur hello et le mot de passe que vous utilisez toosign dans toohello portail Azure.

    ```PowerShell
    Login-AzureRmAccount
    ```
3. Exécutez hello suivant commande tooview tous les abonnements hello pour ce compte.

    ```PowerShell
    Get-AzureRmSubscription
    ```
4. Tooselect hello abonnement toowork avec la commande suivante d’exécution hello. Remplacez  **&lt;NameOfAzureSubscription** &gt; avec le nom de hello de votre abonnement Azure.

    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```

   > [!IMPORTANT]
   > Notez **SubscriptionId** et **TenantId** à partir de la sortie de hello de cette commande.

5. Créer un groupe de ressources Azure nommé **ADFTutorialResourceGroup** en exécutant hello commande Bonjour PowerShell suivante.

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```

    Si groupe de ressources hello existe déjà, vous spécifiez si tooupdate il (Y) ou conserver en tant que (N).

    Si vous utilisez un autre groupe de ressources, vous devez le nom de hello toouse de votre groupe de ressources à la place de ADFTutorialResourceGroup dans ce didacticiel.
6. Créez une application Azure Active Directory.

    ```PowerShell
    $azureAdApplication = New-AzureRmADApplication -DisplayName "ADFCopyTutotiralApp" -HomePage "https://www.contoso.org" -IdentifierUris "https://www.adfcopytutorialapp.org/example" -Password "Pass@word1"
    ```

    Si vous obtenez hello l’erreur suivante, spécifiez une autre URL et réexécutez la commande hello.
    
    ```PowerShell
    Another object with hello same value for property identifierUris already exists.
    ```
7. Créer hello principal du service Active Directory.

    ```PowerShell
    New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId
    ```
8. Ajouter toohello principal de service **collaborateur de fabrique de données** rôle.

    ```PowerShell
    New-AzureRmRoleAssignment -RoleDefinitionName "Data Factory Contributor" -ServicePrincipalName $azureAdApplication.ApplicationId.Guid
    ```
9. Obtenir l’ID d’application hello.

    ```PowerShell
    $azureAdApplication 
    ```
    Notez l’ID d’application hello (applicationID) à partir de la sortie de hello.

Vous devez avoir les quatre valeurs suivantes après ces étapes :

* ID client
* Identifiant d’abonnement
* ID de l'application
* Mot de passe (spécifié dans la première commande de hello)

## <a name="walkthrough"></a>Procédure pas à pas
1. À l’aide de Visual Studio 2012/2013/2015, créez une application console C# .NET.
   1. Lancez **Visual Studio** 2012/2013/2015.
   2. Cliquez sur **fichier**, pointez trop**nouveau**, puis cliquez sur **projet**.
   3. Développez **Modèles**, puis sélectionnez **Visual C#**. Dans cette procédure pas à pas, vous utilisez C#, mais vous pouvez utiliser un autre langage .NET.
   4. Sélectionnez **Application Console** à partir de la liste hello des types de projets sur hello droite.
   5. Entrez **DataFactoryAPITestApp** pour hello nom.
   6. Sélectionnez **C:\ADFGetStarted** pour hello emplacement.
   7. Cliquez sur **OK** projet hello de toocreate.
2. Cliquez sur **outils**, pointez trop**Gestionnaire de Package NuGet**, puis cliquez sur **Package Manager Console**.
3. Bonjour **Package Manager Console**, hello comme suit :
   1. Exécutez hello suivant du package de fabrique de données tooinstall de commande :`Install-Package Microsoft.Azure.Management.DataFactories`
   2. Exécutez hello suivant du package d’Azure Active Directory tooinstall commandes (vous utilisez les API d’Active Directory dans le code hello) :`Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`
4. Ajoutez hello suivant **appSetttings** section toohello **App.config** fichier. Ces paramètres sont utilisés par la méthode d’assistance de hello : **GetAuthorizationHeader**.

    Remplacez les valeurs de **&lt;ID d’Application&gt;**, **&lt;Mot de passe&gt;**, **&lt;ID d’abonnement&gt;**, et **&lt;ID client&gt;** par vos propres valeurs.

    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
        <appSettings>
            <add key="ActiveDirectoryEndpoint" value="https://login.microsoftonline.com/" />
            <add key="ResourceManagerEndpoint" value="https://management.azure.com/" />
            <add key="WindowsManagementUri" value="https://management.core.windows.net/" />

            <add key="ApplicationId" value="your application ID" />
            <add key="Password" value="Password you used while creating hello AAD application" />
            <add key="SubscriptionId" value= "Subscription ID" />
            <add key="ActiveDirectoryTenantId" value="Tenant ID" />
        </appSettings>
    </configuration>
    ```

5. Ajoutez hello suivant **à l’aide de** instructions toohello source fichier (Program.cs) hello projet.

    ```csharp
    using System.Configuration;
    using System.Collections.ObjectModel;
    using System.Threading;
    using System.Threading.Tasks;

    using Microsoft.Azure;
    using Microsoft.Azure.Management.DataFactories;
    using Microsoft.Azure.Management.DataFactories.Models;
    using Microsoft.Azure.Management.DataFactories.Common.Models;

    using Microsoft.IdentityModel.Clients.ActiveDirectory;

    ```

6. Ajouter hello suivant le code qui crée une instance de **DataPipelineManagementClient** classe toohello **Main** (méthode). Vous utilisez cette toocreate objet une fabrique de données, un service lié, les jeux de données d’entrée et de sortie et un pipeline. Vous montre également comment utiliser cet objet toomonitor de plusieurs secteurs un jeu de données lors de l’exécution.

    ```csharp
    // create data factory management client
    string resourceGroupName = "ADFTutorialResourceGroup";
    string dataFactoryName = "APITutorialFactory";

    TokenCloudCredentials aadTokenCredentials = new TokenCloudCredentials(
            ConfigurationManager.AppSettings["SubscriptionId"],
            GetAuthorizationHeader().Result);

    Uri resourceManagerUri = new Uri(ConfigurationManager.AppSettings["ResourceManagerEndpoint"]);

    DataFactoryManagementClient client = new DataFactoryManagementClient(aadTokenCredentials, resourceManagerUri);
    ```

   > [!IMPORTANT]
   > Remplacez la valeur hello **resourceGroupName** avec nom hello de votre groupe de ressources Azure.
   >
   > Nom de la mise à jour de hello données fabrique (dataFactoryName) toobe unique. Nom de la fabrique de données hello doit être globalement unique. Consultez la rubrique [Data Factory - Règles d'affectation des noms](data-factory-naming-rules.md) pour savoir comment nommer les artefacts Data Factory.

7. Ajouter hello suivant le code qui crée un **fabrique de données** toohello **Main** (méthode).

    ```csharp
    // create a data factory
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
    ```

    Une fabrique de données peut avoir un ou plusieurs pipelines. Un pipeline peut contenir une ou plusieurs activités. Par exemple, un activité de copie toocopy des données d’un magasin de données de destination tooa source et un toorun d’activité HDInsight Hive un tootransform de script Hive données tooproduct sortie les données d’entrée. Commençons par créer la fabrique de données hello dans cette étape.
8. Ajouter hello suivant le code qui crée un **service lié Azure Storage** toohello **Main** (méthode).

   > [!IMPORTANT]
   > Remplacez **storageaccountname** et **accountkey** par le nom et la clé de votre compte Azure Storage.

    ```csharp
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
                    new AzureStorageLinkedService("DefaultEndpointsProtocol=https;AccountName=<storageaccountname>;AccountKey=<accountkey>")
                )
            }
        }
    );
    ```

    Vous créez des services liés dans un toolink de fabrique de données stocke de vos données et fabrique de données toohello de services de calcul. Dans ce didacticiel, vous n’allez pas utiliser n’importe quel service de calcul comme Azure HDInsight ou Azure Data Lake Analytics. Vous utilisez deux magasins de données de type Stockage Azure (source) et Base de données SQL Azure (destination). 

    Vous créez ainsi deux services liés nommés AzureStorageLinkedService et AzureSqlLinkedService de types : AzureStorage et AzureSqlDatabase.  

    Hello AzureStorageLinkedService lie votre fabrique de données toohello compte stockage Azure. Ce compte de stockage est hello une dans laquelle vous créé un conteneur et à télécharger des données de hello dans le cadre de [conditions préalables](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
9. Ajouter hello suivant le code qui crée un **service lié Azure SQL** toohello **Main** (méthode).

   > [!IMPORTANT]
   > Remplacez **servername**, **databasename**, **username** et **password** par le nom de votre serveur SQL Azure, le nom de la base de données, le nom de l’utilisateur et le mot de passe.

    ```csharp
    // create a linked service for output data store: Azure SQL Database
    Console.WriteLine("Creating Azure SQL Database linked service");
    client.LinkedServices.CreateOrUpdate(resourceGroupName, dataFactoryName,
        new LinkedServiceCreateOrUpdateParameters()
        {
            LinkedService = new LinkedService()
            {
                Name = "AzureSqlLinkedService",
                Properties = new LinkedServiceProperties
                (
                    new AzureSqlDatabaseLinkedService("Data Source=tcp:<servername>.database.windows.net,1433;Initial Catalog=<databasename>;User ID=<username>;Password=<password>;Integrated Security=False;Encrypt=True;Connect Timeout=30")
                )
            }
        }
    );
    ```

    AzureSqlLinkedService lie votre fabrique de données de toohello de base de données SQL Azure. données Hello sont copiées à partir du stockage d’objets blob hello sont stockées dans cette base de données. Vous avez créé la table emp de hello dans cette base de données dans le cadre de [conditions préalables](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
10. Ajouter hello suivant le code qui crée **jeux de données d’entrée et de sortie** toohello **Main** (méthode).

    ```csharp
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
                Structure = new List<DataElement>()
                {
                    new DataElement() { Name = "FirstName", Type = "String" },
                    new DataElement() { Name = "LastName", Type = "String" }
                },
                LinkedServiceName = "AzureStorageLinkedService",
                TypeProperties = new AzureBlobDataset()
                {
                    FolderPath = "adftutorial/",
                    FileName = "emp.txt"
                },
                External = true,
                Availability = new Availability()
                {
                    Frequency = SchedulePeriod.Hour,
                    Interval = 1,
                },

                Policy = new Policy()
                {
                    Validation = new ValidationPolicy()
                    {
                        MinimumRows = 1
                    }
                }
            }
        }
    });

    Console.WriteLine("Creating output dataset of type: Azure SQL");
    client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,
        new DatasetCreateOrUpdateParameters()
        {
            Dataset = new Dataset()
            {
                Name = Dataset_Destination,
                Properties = new DatasetProperties()
                {
                    Structure = new List<DataElement>()
                    {
                        new DataElement() { Name = "FirstName", Type = "String" },
                        new DataElement() { Name = "LastName", Type = "String" }
                    },
                    LinkedServiceName = "AzureSqlLinkedService",
                    TypeProperties = new AzureSqlTableDataset()
                    {
                        TableName = "emp"
                    },
                    Availability = new Availability()
                    {
                        Frequency = SchedulePeriod.Hour,
                        Interval = 1,
                    },
                }
            }
        });
    ```
    
    Dans l’étape précédente de hello, vous avez créé toolink de services liés de votre compte de stockage Azure et de la fabrique de données de tooyour de base de données SQL Azure. Dans cette étape, vous définissez deux jeux de données nommées InputDataset et OutputDataset qui représentent une entrée et les données de sortie qui sont stockées dans des magasins de données hello visés par AzureStorageLinkedService et AzureSqlLinkedService, respectivement.

    service lié Azure storage de Hello spécifie la chaîne de connexion hello service Data Factory utilise au moment de l’exécution tooconnect tooyour compte de stockage Azure. Et, le jeu de données objet blob d’entrée hello (InputDataset) spécifie le conteneur de hello et dossier hello qui contient les données d’entrée hello.  

    De même, hello service de base de données SQL Azure lié spécifie la chaîne de connexion hello service Data Factory utilise au moment de l’exécution tooconnect tooyour Azure base de données SQL. Et, hello sortie de jeu de données de table SQL (OututDataset) spécifie la table de hello Bonjour de toowhich hello de base de données à partir du stockage d’objets blob hello, les données sont copiées.

    Dans cette étape, vous créez un dataset nommé InputDataset qui pointe le fichier d’objet blob tooa (emp.txt) dans le dossier racine de hello d’un conteneur d’objets blob (adftutorial) Bonjour Azure Storage est représenté par hello AzureStorageLinkedService lié service. Si vous ne spécifiez une valeur pour le nom de fichier hello (ignorer), les données à partir de tous les objets BLOB dans le dossier d’entrée de hello sont copiés toohello destination. Dans ce didacticiel, vous spécifiez une valeur pour le nom de fichier hello.    

    Dans cette étape, vous créez un jeu de données de sortie nommé **OutputDataset**. Ce jeu de données pointe tooa SQL table dans la base de données SQL Azure hello représenté par **AzureSqlLinkedService**.
11. Ajoutez le code suivant de hello **crée et Active un pipeline** toohello **Main** (méthode). Dans cette étape, vous créez un pipeline avec une **activité de copie** qui utilise **InputDataset** en entrée et **OutputDataset** en sortie.

    ```csharp
    // create a pipeline
    Console.WriteLine("Creating a pipeline");
    DateTime PipelineActivePeriodStartTime = new DateTime(2017, 5, 11, 0, 0, 0, 0, DateTimeKind.Utc);
    DateTime PipelineActivePeriodEndTime = new DateTime(2017, 5, 12, 0, 0, 0, 0, DateTimeKind.Utc);
    string PipelineName = "ADFTutorialPipeline";

    client.Pipelines.CreateOrUpdate(resourceGroupName, dataFactoryName,
        new PipelineCreateOrUpdateParameters()
        {
            Pipeline = new Pipeline()
            {
                Name = PipelineName,
                Properties = new PipelineProperties()
                {
                    Description = "Demo Pipeline for data transfer between blobs",

                    // Initial value for pipeline's active period. With this, you won't need tooset slice status
                    Start = PipelineActivePeriodStartTime,
                    End = PipelineActivePeriodEndTime,

                    Activities = new List<Activity>()
                    {
                        new Activity()
                        {
                            Name = "BlobToAzureSql",
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
                            TypeProperties = new CopyActivity()
                            {
                                Source = new BlobSource(),
                                Sink = new BlobSink()
                                {
                                    WriteBatchSize = 10000,
                                    WriteBatchTimeout = TimeSpan.FromMinutes(10)
                                }
                            }
                        }
                    }
                }
            }
        });
    ```

    Hello Notez les points suivants :
   
    - Dans la section d’activités hello, il n'existe qu’une seule activité dont **type** est défini trop**copie**. Pour plus d’informations sur l’activité de copie hello, consultez [les activités de déplacement des données](data-factory-data-movement-activities.md). Dans les solutions Data Factory, vous pouvez également utiliser [Activités de transformation des données](data-factory-data-transformation-activities.md).
    - Entrée d’activité hello est définie trop**InputDataset** et de sortie d’activité hello est définie trop**OutputDataset**. 
    - Bonjour **typeProperties** section, **BlobSource** est spécifié comme type de source de hello et **SqlSink** est spécifié comme type de récepteur hello. Pour obtenir une liste complète des magasins de données pris en charge par l’activité de copie hello en tant que sources et récepteurs, consultez [prise en charge des magasins de données](data-factory-data-movement-activities.md#supported-data-stores-and-formats). toolearn comment toouse données pris en charge spécifiques stocker en tant que source/récepteur, cliquez sur lien hello dans la table de hello.  
   
    Actuellement, le dataset de sortie est les lecteurs hello planification. Dans ce didacticiel, le dataset de sortie est tooproduce configuré une tranche une fois par heure. pipeline de Hello a une heure de début et l’heure de fin sont un jour séparé, ce qui est de 24 heures. Par conséquent, 24 tranches du jeu de données de sortie produits par le pipeline de hello.
12. Ajouter hello suivant code toohello **Main** jeu de données de sortie de statut de hello tooget de méthode d’une tranche de données de hello. Une seule tranche est attendue dans cet exemple.

    ```csharp
    // Pulling status within a timeout threshold
    DateTime start = DateTime.Now;
    bool done = false;

    while (DateTime.Now - start < TimeSpan.FromMinutes(5) && !done)
    {
        Console.WriteLine("Pulling hello slice status");        
        // wait before hello next status check
        Thread.Sleep(1000 * 12);

        var datalistResponse = client.DataSlices.List(resourceGroupName, dataFactoryName, Dataset_Destination,
            new DataSliceListParameters()
            {
                DataSliceRangeStartTime = PipelineActivePeriodStartTime.ConvertToISO8601DateTimeString(),
                DataSliceRangeEndTime = PipelineActivePeriodEndTime.ConvertToISO8601DateTimeString()
            });

        foreach (DataSlice slice in datalistResponse.DataSlices)
        {
            if (slice.State == DataSliceState.Failed || slice.State == DataSliceState.Ready)
            {
                Console.WriteLine("Slice execution is done with status: {0}", slice.State);
                done = true;
                break;
            }
            else
            {
                Console.WriteLine("Slice status is: {0}", slice.State);
            }
        }
    }
    ```

13. Ajouter hello suivant détails tooget exécuter du code pour un toohello de tranche de données **Main** (méthode).

    ```csharp
    Console.WriteLine("Getting run details of a data slice");

    // give it a few minutes for hello output slice toobe ready
    Console.WriteLine("\nGive it a few minutes for hello output slice toobe ready and press any key.");
    Console.ReadKey();

    var datasliceRunListResponse = client.DataSliceRuns.List(
            resourceGroupName,
            dataFactoryName,
            Dataset_Destination,
            new DataSliceRunListParameters()
            {
                DataSliceStartTime = PipelineActivePeriodStartTime.ConvertToISO8601DateTimeString()
            }
        );

    foreach (DataSliceRun run in datasliceRunListResponse.DataSliceRuns)
    {
        Console.WriteLine("Status: \t\t{0}", run.Status);
        Console.WriteLine("DataSliceStart: \t{0}", run.DataSliceStart);
        Console.WriteLine("DataSliceEnd: \t\t{0}", run.DataSliceEnd);
        Console.WriteLine("ActivityId: \t\t{0}", run.ActivityName);
        Console.WriteLine("ProcessingStartTime: \t{0}", run.ProcessingStartTime);
        Console.WriteLine("ProcessingEndTime: \t{0}", run.ProcessingEndTime);
        Console.WriteLine("ErrorMessage: \t{0}", run.ErrorMessage);
    }

    Console.WriteLine("\nPress any key tooexit.");
    Console.ReadKey();
    ```

14. Ajouter hello suivant la méthode d’assistance utilisée par hello **principal** méthode toohello **programme** classe.

    > [!NOTE] 
    > Lorsque vous copiez et collez hello suivant de code, assurez-vous que hello code copié est à hello hello méthode Main de même niveau.

    ```csharp
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
    ```

15. Hello l’Explorateur de solutions, développez le projet hello (DataFactoryAPITestApp), avec le bouton droit dans **références**, puis cliquez sur **ajouter une référence**. Cochez la case de l’assemblage **System.Configuration**. et cliquez sur **OK**.
16. Créer une application de console hello. Cliquez sur **générer** sur hello menu et cliquez sur **générer la Solution**.
17. Confirmer qu’il existe au moins un fichier Bonjour **adftutorial** conteneur dans votre stockage d’objets blob Azure. Dans le cas contraire, créez **Emp.txt** fichier hello suivant contenu dans le bloc-notes, puis téléchargez-le toohello adftutorial conteneur.

    ```
    John, Doe
    Jane, Doe
    ```
18. Exécuter l’exemple hello en cliquant sur **déboguer** -> **démarrer le débogage** menu hello. Lorsque vous consultez hello **détails d’une tranche de données mise en route de l’exécution**, attendez quelques minutes, puis appuyez sur **entrée**.
19. Utilisez hello tooverify portail Azure cette fabrique de données hello **APITutorialFactory** est créée avec hello suivant artefacts :
   * Service lié : **LinkedService_AzureStorage**
   * Jeu de données : **InputDataset** et **OutputDataset**.
   * Pipeline : **PipelineBlobSample**
20. Vérifiez que les enregistrements d’employés hello deux sont créés dans hello **emp** table Bonjour spécifiée de la base de données SQL Azure.

## <a name="next-steps"></a>Étapes suivantes
Pour la documentation complète sur l’API .NET pour Data Factory, consultez [Informations de référence sur l’API .NET Data Factory](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1).

Dans ce didacticiel, vous avez utilisé le stockage Blob Azure comme magasin de données source et une base de données SQL Azure comme banque de données de destination dans une opération de copie. Hello tableau suivant fournit une liste de banques de données pris en charge en tant que sources et destinations par l’activité de copie hello : 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

toolearn sur la banque de données de toocopy vers/à partir de données, cliquez sur lien hello hello magasin de données dans la table de hello.

