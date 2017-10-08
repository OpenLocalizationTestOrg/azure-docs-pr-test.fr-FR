---
title: "aaaCreate des pipelines de données à l’aide du Kit de développement .NET Azure | Documents Microsoft"
description: "Découvrez comment tooprogrammatically créer, surveiller et gérer des fabriques de données Azure à l’aide du SDK de fabrique de données."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: b0a357be-3040-4789-831e-0d0a32a0bda5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 190b5f99edbb3c27e1e8efb8990b9e601b22458f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-monitor-and-manage-azure-data-factories-using-azure-data-factory-net-sdk"></a>Créer, surveiller et gérer des fabriques de données Azure à l’aide du Kit de développement logiciel (SDK) Azure Data Factory .NET
## <a name="overview"></a>Vue d'ensemble
Vous pouvez créer, surveiller et gérer des fabriques de données Azure par programmation à l'aide du Kit SDK Data Factory .NET. Cet article contient une procédure pas à pas que vous pouvez suivre toocreate une exemple .NET d’application console qui crée et analyse d’une fabrique de données. 

> [!NOTE]
> Cet article ne couvre pas hello toutes les API .NET de fabrique de données. Consultez [Informations de référence sur l’API .NET Data Factory](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1) pour la documentation complète sur l’API .NET pour Data Factory. 

## <a name="prerequisites"></a>Conditions préalables
* Visual Studio 2012, 2013 ou 2015
* Téléchargez et installez le [Kit SDK Azure .NET](http://azure.microsoft.com/downloads/).
* Azure PowerShell. Suivez les instructions de [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview) article tooinstall Azure PowerShell sur votre ordinateur. Vous utilisez Azure PowerShell toocreate une application Azure Active Directory.

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
    $azureAdApplication = New-AzureRmADApplication -DisplayName "ADFDotNetWalkthroughApp" -HomePage "https://www.contoso.org" -IdentifierUris "https://www.adfdotnetwalkthroughapp.org/example" -Password "Pass@word1"
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
Hello procédure pas à pas, vous créez une fabrique de données avec un pipeline qui contient une activité de copie. Hello activité de copie copie les données à partir d’un dossier dans le dossier tooanother stockage blob Azure hello même stockage d’objets blob. 

Activité de copie de Hello effectue le déplacement des données de hello dans Azure Data Factory. activité Hello est rendue possible par un service globalement disponible qui permettre copier des données entre différentes banques de données de manière sécurisée, fiable et évolutive. Consultez [les activités de déplacement des données](data-factory-data-movement-activities.md) article pour plus d’informations sur l’activité de copie de hello.

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
4. Remplacez le contenu hello de **App.config** fichier projet hello avec hello suivant le contenu : 
    
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
5. Dans le fichier App.Config hello, mettre à jour les valeurs de  **&lt;ID d’Application&gt;**,  **&lt;mot de passe&gt;**,  **&lt; ID d’abonnement&gt;**, et  **&lt;ID de locataire&gt;**  avec vos propres valeurs.
6. Ajoutez hello suivant **à l’aide de** instructions toohello **Program.cs** fichier hello projet.

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

    //IMPORTANT: specify hello name of Azure resource group here
    string resourceGroupName = "ADFTutorialResourceGroup";

    //IMPORTANT: hello name of hello data factory must be globally unique.
    // Therefore, update this value. For example:APITutorialFactory05122017
    string dataFactoryName = "APITutorialFactory";

    TokenCloudCredentials aadTokenCredentials = new TokenCloudCredentials(
            ConfigurationManager.AppSettings["SubscriptionId"],
            GetAuthorizationHeader().Result);

    Uri resourceManagerUri = new Uri(ConfigurationManager.AppSettings["ResourceManagerEndpoint"]);

    DataFactoryManagementClient client = new DataFactoryManagementClient(aadTokenCredentials, resourceManagerUri);
    ```

   > [!IMPORTANT]
   > Remplacez la valeur hello **resourceGroupName** avec nom hello de votre groupe de ressources Azure. Vous pouvez créer un groupe de ressources à l’aide de hello [New-AzureResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) applet de commande.
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
9. Ajouter hello suivant le code qui crée **jeux de données d’entrée et de sortie** toohello **Main** (méthode).

    Hello **FolderPath** d’objet blob d’entrée de hello est défini trop**adftutorial /** où **adftutorial** est le nom hello du conteneur de hello dans votre stockage d’objets blob. Si ce conteneur n’existe pas dans votre stockage d’objets blob Azure, créer un conteneur portant ce nom : **adftutorial** et télécharger un conteneur de toohello du fichier texte.

    Hello FolderPath pour hello blob a la valeur de sortie : **adftutorial/apifactoryoutput / {Slice}** où **tranche** est la valeur calculée dynamiquement hello selon **SliceStart**(début de date et heure de chaque secteur).

    ```csharp
    // create input and output datasets
    Console.WriteLine("Creating input and output datasets");
    string Dataset_Source = "DatasetBlobSource";
    string Dataset_Destination = "DatasetBlobDestination";
    
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
                    FolderPath = "adftutorial/apifactoryoutput/{Slice}",
                    PartitionedBy = new Collection<Partition>()
                    {
                        new Partition()
                        {
                            Name = "Slice",
                            Value = new DateTimePartitionValue()
                            {
                                Date = "SliceStart",
                                Format = "yyyyMMdd-HH"
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
    ```
10. Ajoutez le code suivant de hello **crée et Active un pipeline** toohello **Main** (méthode). Ce pipeline dispose d’une fonction **CopyActivity** qui accepte **BlobSource** en tant que source et **BlobSink** en tant que récepteur.

    Activité de copie de Hello effectue le déplacement des données de hello dans Azure Data Factory. activité Hello est rendue possible par un service globalement disponible qui permettre copier des données entre différentes banques de données de manière sécurisée, fiable et évolutive. Consultez [les activités de déplacement des données](data-factory-data-movement-activities.md) article pour plus d’informations sur l’activité de copie de hello.

    ```csharp
    // create a pipeline
    Console.WriteLine("Creating a pipeline");
    DateTime PipelineActivePeriodStartTime = new DateTime(2014, 8, 9, 0, 0, 0, 0, DateTimeKind.Utc);
    DateTime PipelineActivePeriodEndTime = PipelineActivePeriodStartTime.AddMinutes(60);
    string PipelineName = "PipelineBlobSample";
    
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
                        Name = "BlobToBlob",
                        Inputs = new List<ActivityInput>()
                        {
                            new ActivityInput()
                {
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
    
                },
            }
        }
    });
    ```
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
13. **(facultatif)**  Tooget exécuter les détails pour un toohello de tranche de données de code suivant de hello ajouter **Main** (méthode).

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
        });
    
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
14. Ajouter hello suivant la méthode d’assistance utilisée par hello **principal** méthode toohello **programme** classe. Cette méthode affiche une boîte de dialogue qui vous permet de fournir **nom d’utilisateur** et **mot de passe** utiliser toolog dans tooAzure portal.

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

15. Bonjour l’Explorateur de solutions, développez le projet de hello : **DataFactoryAPITestApp**, avec le bouton droit **références**, puis cliquez sur **ajouter une référence**. Cochez la case pour l’assembly `System.Configuration` et cliquez sur **OK**.
15. Créer une application de console hello. Cliquez sur **générer** sur hello menu et cliquez sur **générer la Solution**.
16. Vérifiez qu’est au moins un fichier dans le conteneur d’adftutorial hello dans votre stockage d’objets blob Azure. Si ce n’est pas le cas, créer à Emp.txt fichier dans le bloc-notes avec hello suivant contenu et le télécharger toohello adftutorial conteneur.

    ```
    John, Doe
    Jane, Doe
    ```
17. Exécuter l’exemple hello en cliquant sur **déboguer** -> **démarrer le débogage** menu hello. Lorsque vous consultez hello **détails d’une tranche de données mise en route de l’exécution**, attendez quelques minutes, puis appuyez sur **entrée**.
18. Utilisez hello tooverify portail Azure cette fabrique de données hello **APITutorialFactory** est créée avec hello suivant artefacts :
    * Service lié : **AzureStorageLinkedService**
    * Jeu de données : **DatasetBlobSource** et **DatasetBlobDestination**.
    * Pipeline : **PipelineBlobSample**
19. Vérifiez qu’un fichier de sortie est créé dans hello **apifactoryoutput** dossier Bonjour **adftutorial** conteneur.

## <a name="get-a-list-of-failed-data-slices"></a>Obtenir une liste des tranches de données en échec 

```csharp
// Parse hello resource path
var ResourceGroupName = "ADFTutorialResourceGroup";
var DataFactoryName = "DataFactoryAPITestApp";

var parameters = new ActivityWindowsByDataFactoryListParameters(ResourceGroupName, DataFactoryName);
parameters.WindowState = "Failed";
var response = dataFactoryManagementClient.ActivityWindows.List(parameters);
do
{
    foreach (var activityWindow in response.ActivityWindowListResponseValue.ActivityWindows)
    {
        var row = string.Join(
            "\t",
            activityWindow.WindowStart.ToString(),
            activityWindow.WindowEnd.ToString(),
            activityWindow.RunStart.ToString(),
            activityWindow.RunEnd.ToString(),
            activityWindow.DataFactoryName,
            activityWindow.PipelineName,
            activityWindow.ActivityName,
            string.Join(",", activityWindow.OutputDatasets));
        Console.WriteLine(row);
    }

    if (response.NextLink != null)
    {
        response = dataFactoryManagementClient.ActivityWindows.ListNext(response.NextLink, parameters);
    }
    else
    {
        response = null;
    }
}
while (response != null);
```

## <a name="next-steps"></a>Étapes suivantes
Consultez hello exemple pour la création d’un pipeline à l’aide du Kit de développement logiciel .NET qui copie les données à partir d’une base de données SQL Azure de tooan stockage blob Azure suivant : 

- [Créer un pipeline de données de toocopy de tooSQL de stockage d’objets Blob de base de données](data-factory-copy-activity-tutorial-using-dotnet-api.md)
