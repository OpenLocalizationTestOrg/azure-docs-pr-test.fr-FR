---
title: "aaaManagement .NET SDK pour l’Analytique des flux de données Azure | Documents Microsoft"
description: "Familiarisez-vous avec le SDK .NET Stream Analytics Management. Découvrez comment tooset configurer et exécuter des travaux de l’analytique. Créez un projet, ainsi que des entrées, des sorties et des transformations."
keywords: "Kit de développement logiciel (SDK) .NET, API d’analyse"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 5e93de87-0c6f-4f4b-be98-08d63f832897
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/06/2017
ms.author: jeffstok
ms.openlocfilehash: 507c11938bc5bf2249a2e41f6bcc076db8ead3f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="management-net-sdk-set-up-and-run-analytics-jobs-using-hello-azure-stream-analytics-api-for-net"></a>Gestion .NET SDK : Configurer et exécuter des travaux analytique à l’aide de hello API Analytique de flux de données Azure pour .NET
Découvrez comment tooset des et les travaux d’exécution analytique à l’aide de hello API Analytique de flux de données pour l’utilisation de .NET hello Management .NET SDK. configurer un projet, créer des sources d’entrée et de sortie, des transformations, et démarrer et arrêter des tâches. Pour vos tâches d’analyse, vous pouvez diffuser des données à partir du stockage d’objets blob ou d’un hub d’événements.

Consultez hello [documentation de référence de gestion pour hello flux Analytique API pour .NET](https://msdn.microsoft.com/library/azure/dn889315.aspx).

Analytique de flux de données Azure est un service entièrement géré qui fournit le traitement des événements à faible latence, hautement disponibles, évolutives, complexes sur la diffusion en continu des données dans le cloud de hello. Analytique de flux permet tooset clients de diffusion en continu des flux de données tooanalyze travaux et leur permet de toodrive près analytique en temps réel.  

> [!NOTE]
> Nous avons mis à jour hello exemple de code dans cet article Azure flux Analytique Management .NET SDK v2.x version. Pour l’exemple de code à l’aide de hello utilise la version du Kit de développement logiciel lagecy (1.x), consultez [utiliser version 1.x de Management .NET SDK hello pour les flux de données Analytique](https://docs.microsoft.com/en-us/azure/stream-analytics/stream-analytics-dotnet-management-sdk-v1).

## <a name="prerequisites"></a>Composants requis
Avant de commencer cet article, vous devez disposer de hello :

* Installez Visual Studio 2017 ou 2015.
* Téléchargez et installez le [Kit SDK Azure .NET](https://azure.microsoft.com/downloads/).
* Créez un groupe de ressources Azure dans votre abonnement. Hello Voici un exemple de script Azure PowerShell. Pour obtenir des informations sur Azure PowerShell, consultez [Installation et configuration d’Azure PowerShell](/powershell/azure/overview).  

        # Log in tooyour Azure account
        Add-AzureAccount

        # Select hello Azure subscription you want toouse toocreate hello resource group
        Select-AzureSubscription -SubscriptionName <subscription name>

            # If Stream Analytics has not been registered toohello subscription, remove hello remark symbol (#) toorun hello Register-AzureRMProvider cmdlet tooregister hello provider namespace
            #Register-AzureRMProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>


* Configurer une source d’entrée et de sortie cible toouse. Pour obtenir des instructions, consultez [ajouter des entrées](stream-analytics-add-inputs.md) tooset d’un exemple d’entrée et [ajouter les sorties](stream-analytics-add-outputs.md) tooset d’un exemple de sortie.

## <a name="set-up-a-project"></a>Configuration d’un projet
toocreate une tâche analytique utiliser hello flux Analytique API pour .NET, définissez tout d’abord votre projet.

1. Créez une application console Visual Studio .NET C#.
2. Dans la Console du Gestionnaire de Package de hello, suivante d’exécution hello commandes les packages NuGet tooinstall hello. Hello tout d’abord une est hello Azure flux Analytique Management .NET SDK. Hello deuxième est pour l’authentification du client Azure.
   
        Install-Package Microsoft.Azure.Management.StreamAnalytics -Version 2.0.0
        Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Version 2.3.1
3. Ajoutez hello suivant **appSettings** section toohello du fichier App.config :
   
        <appSettings>
          <add key="ClientId" value="1950a258-227b-4e31-a9cf-717495945fc2" />
          <add key="RedirectUri" value="urn:ietf:wg:oauth:2.0:oob" />
          <add key="SubscriptionId" value="YOUR SUBSCRIPTION ID" />
          <add key="ActiveDirectoryTenantId" value="YOUR TENANT ID" />
        </appSettings>

    Remplacez les valeurs de **SubscriptionId** et **ActiveDirectoryTenantId** par votre ID d’abonnement et votre ID de locataire Azure. Vous pouvez obtenir ces valeurs en exécutant hello suivant l’applet de commande PowerShell de Azure :

        Get-AzureAccount

4. Ajoutez hello suivant référence dans votre fichier .csproj :

        <Reference Include="System.Configuration" />

5. Ajoutez hello suivant **à l’aide de** instructions toohello source fichier (Program.cs) hello projet :
   
        using System;
        using System.Collections.Generic;
        using System.Configuration;
        using System.Threading;
        using System.Threading.Tasks;
        
        using Microsoft.Azure.Management.StreamAnalytics;
        using Microsoft.Azure.Management.StreamAnalytics.Models;
        using Microsoft.Rest.Azure.Authentication;
        using Microsoft.Rest;
6. Ajoutez une méthode d’aide pour l’authentification :

   ```
   private static async Task<ServiceClientCredentials> GetCredentials()
   {
       var activeDirectoryClientSettings = ActiveDirectoryClientSettings.UsePromptOnly(ConfigurationManager.AppSettings["ClientId"], new Uri("urn:ietf:wg:oauth:2.0:oob"));
       ServiceClientCredentials credentials = await UserTokenProvider.LoginWithPromptAsync(ConfigurationManager.AppSettings["ActiveDirectoryTenantId"], activeDirectoryClientSettings);
       
       return credentials;
    }
   ```

## <a name="create-a-stream-analytics-management-client"></a>Création d’un client de gestion Stream Analytics
A **StreamAnalyticsManagementClient** objet vous permet de toomanage hello travail hello travail composants et, comme entrée, sortie et la transformation.

Ajouter hello suivant début toohello de code Hello **Main** méthode :

   ```
    string resourceGroupName = "<YOUR AZURE RESOURCE GROUP NAME>";
    string streamingJobName = "<YOUR STREAMING JOB NAME>";
    string inputName = "<YOUR JOB INPUT NAME>";
    string transformationName = "<YOUR JOB TRANSFORMATION NAME>";
    string outputName = "<YOUR JOB OUTPUT NAME>";
    
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());
    
    // Get credentials
    ServiceClientCredentials credentials = GetCredentials().Result;
    
    // Create Stream Analytics management client
    StreamAnalyticsManagementClient streamAnalyticsManagementClient = new StreamAnalyticsManagementClient(credentials)
    {
        SubscriptionId = ConfigurationManager.AppSettings["SubscriptionId"]
    };
   ```

Hello **resourceGroupName** valeur de la variable doit être hello identique nom hello de ressource de hello groupe que vous avez créé ou choisis dans les étapes requises hello.

format de présentation tooautomate hello d’informations d’identification de la création du travail, consultez trop[l’authentification d’un principal de service avec Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md).

Hello autres sections de cet article supposent que ce code est au début de hello de hello **Main** (méthode).

## <a name="create-a-stream-analytics-job"></a>Création d’un travail Stream Analytics
Hello de code suivant crée une tâche de flux Analytique sous le groupe de ressources hello que vous avez définies. Vous allez ajouter un travail d’entrée, sortie et transformation toohello plus tard.

   ```
   // Create a streaming job
   StreamingJob streamingJob = new StreamingJob()
   {
       Tags = new Dictionary<string, string>()
       {
           { "Origin", ".NET SDK" },
           { "ReasonCreated", "Getting started tutorial" }
       },
       Location = "West US",
       EventsOutOfOrderPolicy = EventsOutOfOrderPolicy.Drop,
       EventsOutOfOrderMaxDelayInSeconds = 5,
       EventsLateArrivalMaxDelayInSeconds = 16,
       OutputErrorPolicy = OutputErrorPolicy.Drop,
       DataLocale = "en-US",
       CompatibilityLevel = CompatibilityLevel.OneFullStopZero,
       Sku = new Sku()
       {
           Name = SkuName.Standard
       }
   };
   StreamingJob createStreamingJobResult = streamAnalyticsManagementClient.StreamingJobs.CreateOrReplace(streamingJob, resourceGroupName, streamingJobName);
   ```

## <a name="create-a-stream-analytics-input-source"></a>Création d’une source d’entrée Stream Analytics
Hello de code suivant crée une source d’entrée de flux de données Analytique avec le type de source d’entrée d’objet blob hello et sérialisation des volumes partagés de cluster. toocreate une source d’entrée de concentrateur d’événements, utilisez **EventHubStreamInputDataSource** au lieu de **BlobStreamInputDataSource**. De même, vous pouvez personnaliser le type de sérialisation hello de source d’entrée de hello.

   ```
   // Create an input
   StorageAccount storageAccount = new StorageAccount()
   {
       AccountName = "<YOUR STORAGE ACCOUNT NAME>",
       AccountKey = "<YOUR STORAGE ACCOUNT KEY>"
   };
   Input input = new Input()
   {
       Properties = new StreamInputProperties()
       {
           Serialization = new CsvSerialization()
           {
               FieldDelimiter = ",",
               Encoding = Encoding.UTF8
           },
           Datasource = new BlobStreamInputDataSource()
           {
               StorageAccounts = new[] { storageAccount },
               Container = "<YOUR STORAGE BLOB CONTAINER>",
               PathPattern = "{date}/{time}",
               DateFormat = "yyyy/MM/dd",
               TimeFormat = "HH",
               SourcePartitionCount = 16
           }
       }
   };
   Input createInputResult = streamAnalyticsManagementClient.Inputs.CreateOrReplace(input, resourceGroupName, streamingJobName, inputName);
   ```

Sources d’entrée, à partir d’un concentrateur d’événements, ou de stockage d’objets Blob sont tâche tooa liée. toouse hello même source d’entrée pour différentes tâches, vous devez rappeler la méthode hello et spécifiez un nom de travail différent.

## <a name="test-a-stream-analytics-input-source"></a>Test d’une source d’entrée Stream Analytics
Hello **TestConnection** si tâche de flux de données Analytique hello est en mesure de tooconnect toohello d’entrée source ainsi que d’autres toohello spécifique aspects des tests méthode d’entrée de type de source. Par exemple, dans hello blob source d’entrée que vous avez créé dans une étape antérieure, méthode hello Vérifiez que nom de compte de stockage hello et la paire de clés permettre être utilisés tooconnect toohello compte de stockage ainsi vérifier le qu'existence du conteneur spécifié hello.

   ```
   // Test hello connection toohello input
   ResourceTestStatus testInputResult = streamAnalyticsManagementClient.Inputs.Test(resourceGroupName, streamingJobName, inputName);
   ```

## <a name="create-a-stream-analytics-output-target"></a>Création d’une cible de sortie Stream Analytics
Création d’une cible de sortie est très similaire toocreating une source d’entrée de flux de données Analytique. Comme sources d’entrée, sortie cibles sont tâche tooa liée. toouse hello même cible de sortie pour les travaux de différentes, vous devez rappeler la méthode hello et spécifiez un nom de travail différent.

Hello suivante de code crée une cible de sortie (base de données SQL Azure). Vous pouvez personnaliser le type de données de la cible de sortie hello et/ou le type de sérialisation.

   ```
   // Create an output
   Output output = new Output()
   {
       Datasource = new AzureSqlDatabaseOutputDataSource()
       {
           Server = "<YOUR DATABASE SERVER NAME>",
           Database = "<YOUR DATABASE NAME>",
           User = "<YOUR DATABASE LOGIN>",
           Password = "<YOUR DATABASE LOGIN PASSWORD>",
           Table = "<YOUR DATABASE TABLE NAME>"
       }
   };
   Output createOutputResult = streamAnalyticsManagementClient.Outputs.CreateOrReplace(output, resourceGroupName, streamingJobName, outputName);
   ```

## <a name="test-a-stream-analytics-output-target"></a>Test d’une cible de sortie Stream Analytics
Une cible de la sortie du flux de données Analytique a également hello **TestConnection** méthode pour tester les connexions.

   ```
   // Test hello connection toohello output
   ResourceTestStatus testOutputResult = streamAnalyticsManagementClient.Outputs.Test(resourceGroupName, streamingJobName, outputName);
   ```

## <a name="create-a-stream-analytics-transformation"></a>Création d’une transformation Stream Analytics
Hello de code suivant crée une transformation de flux de données Analytique avec hello requête « sélectionner * à partir de l’entrée » et spécifie l’unité de diffusion en continu un tooallocate pour la tâche de flux de données Analytique hello. Pour plus d’informations sur le réglage des unités de diffusion en continu, consultez [Mise à l’échelle des travaux Azure Stream Analytics](stream-analytics-scale-jobs.md).

   ```
   // Create a transformation
   Transformation transformation = new Transformation()
   {
       Query = "Select Id, Name from <your input name>", // '<your input name>' should be replaced with hello value you put for hello 'inputName' variable above or in a previous step
       StreamingUnits = 1
   };
   Transformation createTransformationResult = streamAnalyticsManagementClient.Transformations.CreateOrReplace(transformation, resourceGroupName, streamingJobName, transformationName);
   ```

Comme entrée et sortie, une transformation est également qu’il a été créé sous le travail Analytique des flux de données spécifique toohello liée.

## <a name="start-a-stream-analytics-job"></a>Démarrage d’un travail Stream Analytics
Après avoir créé une tâche de flux de données Analytique et son que les entrées, sorties et de transformation, vous pouvez démarrer le travail de hello en appelant hello **Démarrer** (méthode).

Hello suivant l’exemple de code démarre une tâche de flux de données Analytique avec une sortie personnalisée début heure ensemble tooDecember 12, 2012, 12:12:12 UTC :

   ```
   // Start a streaming job
   StartStreamingJobParameters startStreamingJobParameters = new StartStreamingJobParameters()
   {
       OutputStartMode = OutputStartMode.CustomTime,
       OutputStartTime = new DateTime(2012, 12, 12, 12, 12, 12, DateTimeKind.Utc)
   };
   streamAnalyticsManagementClient.StreamingJobs.Start(resourceGroupName, streamingJobName, startStreamingJobParameters);
   ```

## <a name="stop-a-stream-analytics-job"></a>Arrêt d’un travail Stream Analytics
Vous pouvez arrêter une tâche de flux de données Analytique en cours d’exécution en appelant hello **arrêter** (méthode).

   ```
   // Stop a streaming job
   streamAnalyticsManagementClient.StreamingJobs.Stop(resourceGroupName, streamingJobName);
   ```

## <a name="delete-a-stream-analytics-job"></a>Suppression d’un travail Stream Analytics
Hello **supprimer** méthode supprimera hello ainsi que les hello sous-jacent sous-ressources, notamment que les entrées, sorties et la transformation de la tâche de hello.

   ```
   // Delete a streaming job
   streamAnalyticsManagementClient.StreamingJobs.Delete(resourceGroupName, streamingJobName);
   ```

## <a name="get-support"></a>Obtenir de l'aide
Pour obtenir une assistance, consultez le [forum Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Étapes suivantes
Vous avez appris hello notions de base de l’utilisation d’un toocreate du Kit de développement .NET et exécuter des travaux de l’analytique. toolearn plus, voir hello :

* [Introduction tooAzure Analytique de flux de données](stream-analytics-introduction.md)
* [Prise en main d’Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Mise à l’échelle des travaux Azure Stream Analytics](stream-analytics-scale-jobs.md)
* [Kit de développement logiciel (SDK) .NET Azure Stream Analytics Management](https://msdn.microsoft.com/library/azure/dn889315.aspx)
* [Références sur le langage des requêtes d’Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Références sur l’API REST de gestion d’Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

<!--Image references-->
[5]: ./media/markdown-template-for-new-articles/octocats.png
[6]: ./media/markdown-template-for-new-articles/pretty49.png
[7]: ./media/markdown-template-for-new-articles/channel-9.png


<!--Link references-->
[azure.blob.storage]: http://azure.microsoft.com/documentation/services/storage/
[azure.blob.storage.use]: http://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-blobs/

[azure.event.hubs]: http://azure.microsoft.com/services/event-hubs/
[azure.event.hubs.developer.guide]: http://msdn.microsoft.com/library/azure/dn789972.aspx

[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.forum]: http://go.microsoft.com/fwlink/?LinkId=512151

[stream.analytics.introduction]: stream-analytics-introduction.md
[stream.analytics.get.started]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.developer.guide]: stream-analytics-developer-guide.md
[stream.analytics.scale.jobs]: stream-analytics-scale-jobs.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301
