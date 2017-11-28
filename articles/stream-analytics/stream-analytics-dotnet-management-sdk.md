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
# <a name="management-net-sdk-set-up-and-run-analytics-jobs-using-hello-azure-stream-analytics-api-for-net"></a><span data-ttu-id="6dc36-106">Gestion .NET SDK : Configurer et exécuter des travaux analytique à l’aide de hello API Analytique de flux de données Azure pour .NET</span><span class="sxs-lookup"><span data-stu-id="6dc36-106">Management .NET SDK: Set up and run analytics jobs using hello Azure Stream Analytics API for .NET</span></span>
<span data-ttu-id="6dc36-107">Découvrez comment tooset des et les travaux d’exécution analytique à l’aide de hello API Analytique de flux de données pour l’utilisation de .NET hello Management .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="6dc36-107">Learn how tooset up and run analytics jobs using hello Stream Analytics API for .NET using hello Management .NET SDK.</span></span> <span data-ttu-id="6dc36-108">configurer un projet, créer des sources d’entrée et de sortie, des transformations, et démarrer et arrêter des tâches.</span><span class="sxs-lookup"><span data-stu-id="6dc36-108">Set up a project, create input and output sources, transformations, and start and stop jobs.</span></span> <span data-ttu-id="6dc36-109">Pour vos tâches d’analyse, vous pouvez diffuser des données à partir du stockage d’objets blob ou d’un hub d’événements.</span><span class="sxs-lookup"><span data-stu-id="6dc36-109">For your analytics jobs, you can stream data from Blob storage or from an event hub.</span></span>

<span data-ttu-id="6dc36-110">Consultez hello [documentation de référence de gestion pour hello flux Analytique API pour .NET](https://msdn.microsoft.com/library/azure/dn889315.aspx).</span><span class="sxs-lookup"><span data-stu-id="6dc36-110">See hello [management reference documentation for hello Stream Analytics API for .NET](https://msdn.microsoft.com/library/azure/dn889315.aspx).</span></span>

<span data-ttu-id="6dc36-111">Analytique de flux de données Azure est un service entièrement géré qui fournit le traitement des événements à faible latence, hautement disponibles, évolutives, complexes sur la diffusion en continu des données dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="6dc36-111">Azure Stream Analytics is a fully managed service providing low-latency, highly available, scalable, complex event processing over streaming data in hello cloud.</span></span> <span data-ttu-id="6dc36-112">Analytique de flux permet tooset clients de diffusion en continu des flux de données tooanalyze travaux et leur permet de toodrive près analytique en temps réel.</span><span class="sxs-lookup"><span data-stu-id="6dc36-112">Stream Analytics enables customers tooset up streaming jobs tooanalyze data streams, and allows them toodrive near real-time analytics.</span></span>  

> [!NOTE]
> <span data-ttu-id="6dc36-113">Nous avons mis à jour hello exemple de code dans cet article Azure flux Analytique Management .NET SDK v2.x version.</span><span class="sxs-lookup"><span data-stu-id="6dc36-113">We have updated hello sample code in this article with Azure Stream Analytics Management .NET SDK v2.x version.</span></span> <span data-ttu-id="6dc36-114">Pour l’exemple de code à l’aide de hello utilise la version du Kit de développement logiciel lagecy (1.x), consultez [utiliser version 1.x de Management .NET SDK hello pour les flux de données Analytique](https://docs.microsoft.com/en-us/azure/stream-analytics/stream-analytics-dotnet-management-sdk-v1).</span><span class="sxs-lookup"><span data-stu-id="6dc36-114">For sample code using hello uses lagecy (1.x) SDK version, please see [Use hello Management .NET SDK v1.x for Stream Analytics](https://docs.microsoft.com/en-us/azure/stream-analytics/stream-analytics-dotnet-management-sdk-v1).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6dc36-115">Composants requis</span><span class="sxs-lookup"><span data-stu-id="6dc36-115">Prerequisites</span></span>
<span data-ttu-id="6dc36-116">Avant de commencer cet article, vous devez disposer de hello :</span><span class="sxs-lookup"><span data-stu-id="6dc36-116">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="6dc36-117">Installez Visual Studio 2017 ou 2015.</span><span class="sxs-lookup"><span data-stu-id="6dc36-117">Install Visual Studio 2017 or 2015.</span></span>
* <span data-ttu-id="6dc36-118">Téléchargez et installez le [Kit SDK Azure .NET](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="6dc36-118">Download and install [Azure .NET SDK](https://azure.microsoft.com/downloads/).</span></span>
* <span data-ttu-id="6dc36-119">Créez un groupe de ressources Azure dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="6dc36-119">Create an Azure Resource Group in your subscription.</span></span> <span data-ttu-id="6dc36-120">Hello Voici un exemple de script Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6dc36-120">hello following is a sample Azure PowerShell script.</span></span> <span data-ttu-id="6dc36-121">Pour obtenir des informations sur Azure PowerShell, consultez [Installation et configuration d’Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6dc36-121">For Azure PowerShell information, see [Install and configure Azure PowerShell](/powershell/azure/overview);</span></span>  

        # Log in tooyour Azure account
        Add-AzureAccount

        # Select hello Azure subscription you want toouse toocreate hello resource group
        Select-AzureSubscription -SubscriptionName <subscription name>

            # If Stream Analytics has not been registered toohello subscription, remove hello remark symbol (#) toorun hello Register-AzureRMProvider cmdlet tooregister hello provider namespace
            #Register-AzureRMProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>


* <span data-ttu-id="6dc36-122">Configurer une source d’entrée et de sortie cible toouse.</span><span class="sxs-lookup"><span data-stu-id="6dc36-122">Set up an input source and output target toouse.</span></span> <span data-ttu-id="6dc36-123">Pour obtenir des instructions, consultez [ajouter des entrées](stream-analytics-add-inputs.md) tooset d’un exemple d’entrée et [ajouter les sorties](stream-analytics-add-outputs.md) tooset d’un exemple de sortie.</span><span class="sxs-lookup"><span data-stu-id="6dc36-123">For further instructions see [Add Inputs](stream-analytics-add-inputs.md) tooset up a sample input and [Add Outputs](stream-analytics-add-outputs.md) tooset up a sample output.</span></span>

## <a name="set-up-a-project"></a><span data-ttu-id="6dc36-124">Configuration d’un projet</span><span class="sxs-lookup"><span data-stu-id="6dc36-124">Set up a project</span></span>
<span data-ttu-id="6dc36-125">toocreate une tâche analytique utiliser hello flux Analytique API pour .NET, définissez tout d’abord votre projet.</span><span class="sxs-lookup"><span data-stu-id="6dc36-125">toocreate an analytics job use hello Stream Analytics API for .NET, first set up your project.</span></span>

1. <span data-ttu-id="6dc36-126">Créez une application console Visual Studio .NET C#.</span><span class="sxs-lookup"><span data-stu-id="6dc36-126">Create a Visual Studio C# .NET console application.</span></span>
2. <span data-ttu-id="6dc36-127">Dans la Console du Gestionnaire de Package de hello, suivante d’exécution hello commandes les packages NuGet tooinstall hello.</span><span class="sxs-lookup"><span data-stu-id="6dc36-127">In hello Package Manager Console, run hello following commands tooinstall hello NuGet packages.</span></span> <span data-ttu-id="6dc36-128">Hello tout d’abord une est hello Azure flux Analytique Management .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="6dc36-128">hello first one is hello Azure Stream Analytics Management .NET SDK.</span></span> <span data-ttu-id="6dc36-129">Hello deuxième est pour l’authentification du client Azure.</span><span class="sxs-lookup"><span data-stu-id="6dc36-129">hello second one is for Azure client authentication.</span></span>
   
        Install-Package Microsoft.Azure.Management.StreamAnalytics -Version 2.0.0
        Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Version 2.3.1
3. <span data-ttu-id="6dc36-130">Ajoutez hello suivant **appSettings** section toohello du fichier App.config :</span><span class="sxs-lookup"><span data-stu-id="6dc36-130">Add hello following **appSettings** section toohello App.config file:</span></span>
   
        <appSettings>
          <add key="ClientId" value="1950a258-227b-4e31-a9cf-717495945fc2" />
          <add key="RedirectUri" value="urn:ietf:wg:oauth:2.0:oob" />
          <add key="SubscriptionId" value="YOUR SUBSCRIPTION ID" />
          <add key="ActiveDirectoryTenantId" value="YOUR TENANT ID" />
        </appSettings>

    <span data-ttu-id="6dc36-131">Remplacez les valeurs de **SubscriptionId** et **ActiveDirectoryTenantId** par votre ID d’abonnement et votre ID de locataire Azure.</span><span class="sxs-lookup"><span data-stu-id="6dc36-131">Replace values for **SubscriptionId** and **ActiveDirectoryTenantId** with your Azure subscription and tenant IDs.</span></span> <span data-ttu-id="6dc36-132">Vous pouvez obtenir ces valeurs en exécutant hello suivant l’applet de commande PowerShell de Azure :</span><span class="sxs-lookup"><span data-stu-id="6dc36-132">You can get these values by running hello following Azure PowerShell cmdlet:</span></span>

        Get-AzureAccount

4. <span data-ttu-id="6dc36-133">Ajoutez hello suivant référence dans votre fichier .csproj :</span><span class="sxs-lookup"><span data-stu-id="6dc36-133">Add hello following reference in your .csproj file:</span></span>

        <Reference Include="System.Configuration" />

5. <span data-ttu-id="6dc36-134">Ajoutez hello suivant **à l’aide de** instructions toohello source fichier (Program.cs) hello projet :</span><span class="sxs-lookup"><span data-stu-id="6dc36-134">Add hello following **using** statements toohello source file (Program.cs) in hello project:</span></span>
   
        using System;
        using System.Collections.Generic;
        using System.Configuration;
        using System.Threading;
        using System.Threading.Tasks;
        
        using Microsoft.Azure.Management.StreamAnalytics;
        using Microsoft.Azure.Management.StreamAnalytics.Models;
        using Microsoft.Rest.Azure.Authentication;
        using Microsoft.Rest;
6. <span data-ttu-id="6dc36-135">Ajoutez une méthode d’aide pour l’authentification :</span><span class="sxs-lookup"><span data-stu-id="6dc36-135">Add an authentication helper method:</span></span>

   ```
   private static async Task<ServiceClientCredentials> GetCredentials()
   {
       var activeDirectoryClientSettings = ActiveDirectoryClientSettings.UsePromptOnly(ConfigurationManager.AppSettings["ClientId"], new Uri("urn:ietf:wg:oauth:2.0:oob"));
       ServiceClientCredentials credentials = await UserTokenProvider.LoginWithPromptAsync(ConfigurationManager.AppSettings["ActiveDirectoryTenantId"], activeDirectoryClientSettings);
       
       return credentials;
    }
   ```

## <a name="create-a-stream-analytics-management-client"></a><span data-ttu-id="6dc36-136">Création d’un client de gestion Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="6dc36-136">Create a Stream Analytics management client</span></span>
<span data-ttu-id="6dc36-137">A **StreamAnalyticsManagementClient** objet vous permet de toomanage hello travail hello travail composants et, comme entrée, sortie et la transformation.</span><span class="sxs-lookup"><span data-stu-id="6dc36-137">A **StreamAnalyticsManagementClient** object allows you toomanage hello job and hello job components, such as input, output, and transformation.</span></span>

<span data-ttu-id="6dc36-138">Ajouter hello suivant début toohello de code Hello **Main** méthode :</span><span class="sxs-lookup"><span data-stu-id="6dc36-138">Add hello following code toohello beginning of hello **Main** method:</span></span>

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

<span data-ttu-id="6dc36-139">Hello **resourceGroupName** valeur de la variable doit être hello identique nom hello de ressource de hello groupe que vous avez créé ou choisis dans les étapes requises hello.</span><span class="sxs-lookup"><span data-stu-id="6dc36-139">hello **resourceGroupName** variable's value should be hello same as hello name of hello resource group you created or picked in hello prerequisite steps.</span></span>

<span data-ttu-id="6dc36-140">format de présentation tooautomate hello d’informations d’identification de la création du travail, consultez trop[l’authentification d’un principal de service avec Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="6dc36-140">tooautomate hello credential presentation aspect of job creation, refer too[Authenticating a service principal with Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

<span data-ttu-id="6dc36-141">Hello autres sections de cet article supposent que ce code est au début de hello de hello **Main** (méthode).</span><span class="sxs-lookup"><span data-stu-id="6dc36-141">hello remaining sections of this article assume that this code is at hello beginning of hello **Main** method.</span></span>

## <a name="create-a-stream-analytics-job"></a><span data-ttu-id="6dc36-142">Création d’un travail Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="6dc36-142">Create a Stream Analytics job</span></span>
<span data-ttu-id="6dc36-143">Hello de code suivant crée une tâche de flux Analytique sous le groupe de ressources hello que vous avez définies.</span><span class="sxs-lookup"><span data-stu-id="6dc36-143">hello following code creates a Stream Analytics job under hello resource group that you have defined.</span></span> <span data-ttu-id="6dc36-144">Vous allez ajouter un travail d’entrée, sortie et transformation toohello plus tard.</span><span class="sxs-lookup"><span data-stu-id="6dc36-144">You will add an input, output, and transformation toohello job later.</span></span>

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

## <a name="create-a-stream-analytics-input-source"></a><span data-ttu-id="6dc36-145">Création d’une source d’entrée Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="6dc36-145">Create a Stream Analytics input source</span></span>
<span data-ttu-id="6dc36-146">Hello de code suivant crée une source d’entrée de flux de données Analytique avec le type de source d’entrée d’objet blob hello et sérialisation des volumes partagés de cluster.</span><span class="sxs-lookup"><span data-stu-id="6dc36-146">hello following code creates a Stream Analytics input source with hello blob input source type and CSV serialization.</span></span> <span data-ttu-id="6dc36-147">toocreate une source d’entrée de concentrateur d’événements, utilisez **EventHubStreamInputDataSource** au lieu de **BlobStreamInputDataSource**.</span><span class="sxs-lookup"><span data-stu-id="6dc36-147">toocreate an event hub input source, use **EventHubStreamInputDataSource** instead of **BlobStreamInputDataSource**.</span></span> <span data-ttu-id="6dc36-148">De même, vous pouvez personnaliser le type de sérialisation hello de source d’entrée de hello.</span><span class="sxs-lookup"><span data-stu-id="6dc36-148">Similarly, you can customize hello serialization type of hello input source.</span></span>

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

<span data-ttu-id="6dc36-149">Sources d’entrée, à partir d’un concentrateur d’événements, ou de stockage d’objets Blob sont tâche tooa liée.</span><span class="sxs-lookup"><span data-stu-id="6dc36-149">Input sources, whether from Blob storage or an event hub, are tied tooa specific job.</span></span> <span data-ttu-id="6dc36-150">toouse hello même source d’entrée pour différentes tâches, vous devez rappeler la méthode hello et spécifiez un nom de travail différent.</span><span class="sxs-lookup"><span data-stu-id="6dc36-150">toouse hello same input source for different jobs, you must call hello method again and specify a different job name.</span></span>

## <a name="test-a-stream-analytics-input-source"></a><span data-ttu-id="6dc36-151">Test d’une source d’entrée Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="6dc36-151">Test a Stream Analytics input source</span></span>
<span data-ttu-id="6dc36-152">Hello **TestConnection** si tâche de flux de données Analytique hello est en mesure de tooconnect toohello d’entrée source ainsi que d’autres toohello spécifique aspects des tests méthode d’entrée de type de source.</span><span class="sxs-lookup"><span data-stu-id="6dc36-152">hello **TestConnection** method tests whether hello Stream Analytics job is able tooconnect toohello input source as well as other aspects specific toohello input source type.</span></span> <span data-ttu-id="6dc36-153">Par exemple, dans hello blob source d’entrée que vous avez créé dans une étape antérieure, méthode hello Vérifiez que nom de compte de stockage hello et la paire de clés permettre être utilisés tooconnect toohello compte de stockage ainsi vérifier le qu'existence du conteneur spécifié hello.</span><span class="sxs-lookup"><span data-stu-id="6dc36-153">For example, in hello blob input source you created in an earlier step, hello method will check that hello Storage account name and key pair can be used tooconnect toohello Storage account as well as check that hello specified container exists.</span></span>

   ```
   // Test hello connection toohello input
   ResourceTestStatus testInputResult = streamAnalyticsManagementClient.Inputs.Test(resourceGroupName, streamingJobName, inputName);
   ```

## <a name="create-a-stream-analytics-output-target"></a><span data-ttu-id="6dc36-154">Création d’une cible de sortie Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="6dc36-154">Create a Stream Analytics output target</span></span>
<span data-ttu-id="6dc36-155">Création d’une cible de sortie est très similaire toocreating une source d’entrée de flux de données Analytique.</span><span class="sxs-lookup"><span data-stu-id="6dc36-155">Creating an output target is very similar toocreating a Stream Analytics input source.</span></span> <span data-ttu-id="6dc36-156">Comme sources d’entrée, sortie cibles sont tâche tooa liée.</span><span class="sxs-lookup"><span data-stu-id="6dc36-156">Like input sources, output targets are tied tooa specific job.</span></span> <span data-ttu-id="6dc36-157">toouse hello même cible de sortie pour les travaux de différentes, vous devez rappeler la méthode hello et spécifiez un nom de travail différent.</span><span class="sxs-lookup"><span data-stu-id="6dc36-157">toouse hello same output target for different jobs, you must call hello method again and specify a different job name.</span></span>

<span data-ttu-id="6dc36-158">Hello suivante de code crée une cible de sortie (base de données SQL Azure).</span><span class="sxs-lookup"><span data-stu-id="6dc36-158">hello following code creates an output target (Azure SQL database).</span></span> <span data-ttu-id="6dc36-159">Vous pouvez personnaliser le type de données de la cible de sortie hello et/ou le type de sérialisation.</span><span class="sxs-lookup"><span data-stu-id="6dc36-159">You can customize hello output target's data type and/or serialization type.</span></span>

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

## <a name="test-a-stream-analytics-output-target"></a><span data-ttu-id="6dc36-160">Test d’une cible de sortie Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="6dc36-160">Test a Stream Analytics output target</span></span>
<span data-ttu-id="6dc36-161">Une cible de la sortie du flux de données Analytique a également hello **TestConnection** méthode pour tester les connexions.</span><span class="sxs-lookup"><span data-stu-id="6dc36-161">A Stream Analytics output target also has hello **TestConnection** method for testing connections.</span></span>

   ```
   // Test hello connection toohello output
   ResourceTestStatus testOutputResult = streamAnalyticsManagementClient.Outputs.Test(resourceGroupName, streamingJobName, outputName);
   ```

## <a name="create-a-stream-analytics-transformation"></a><span data-ttu-id="6dc36-162">Création d’une transformation Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="6dc36-162">Create a Stream Analytics transformation</span></span>
<span data-ttu-id="6dc36-163">Hello de code suivant crée une transformation de flux de données Analytique avec hello requête « sélectionner * à partir de l’entrée » et spécifie l’unité de diffusion en continu un tooallocate pour la tâche de flux de données Analytique hello.</span><span class="sxs-lookup"><span data-stu-id="6dc36-163">hello following code creates a Stream Analytics transformation with hello query "select * from Input" and specifies tooallocate one streaming unit for hello Stream Analytics job.</span></span> <span data-ttu-id="6dc36-164">Pour plus d’informations sur le réglage des unités de diffusion en continu, consultez [Mise à l’échelle des travaux Azure Stream Analytics](stream-analytics-scale-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="6dc36-164">For more information on adjusting streaming units, see [Scale Azure Stream Analytics jobs](stream-analytics-scale-jobs.md).</span></span>

   ```
   // Create a transformation
   Transformation transformation = new Transformation()
   {
       Query = "Select Id, Name from <your input name>", // '<your input name>' should be replaced with hello value you put for hello 'inputName' variable above or in a previous step
       StreamingUnits = 1
   };
   Transformation createTransformationResult = streamAnalyticsManagementClient.Transformations.CreateOrReplace(transformation, resourceGroupName, streamingJobName, transformationName);
   ```

<span data-ttu-id="6dc36-165">Comme entrée et sortie, une transformation est également qu’il a été créé sous le travail Analytique des flux de données spécifique toohello liée.</span><span class="sxs-lookup"><span data-stu-id="6dc36-165">Like input and output, a transformation is also tied toohello specific Stream Analytics job it was created under.</span></span>

## <a name="start-a-stream-analytics-job"></a><span data-ttu-id="6dc36-166">Démarrage d’un travail Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="6dc36-166">Start a Stream Analytics job</span></span>
<span data-ttu-id="6dc36-167">Après avoir créé une tâche de flux de données Analytique et son que les entrées, sorties et de transformation, vous pouvez démarrer le travail de hello en appelant hello **Démarrer** (méthode).</span><span class="sxs-lookup"><span data-stu-id="6dc36-167">After creating a Stream Analytics job and its input(s), output(s), and transformation, you can start hello job by calling hello **Start** method.</span></span>

<span data-ttu-id="6dc36-168">Hello suivant l’exemple de code démarre une tâche de flux de données Analytique avec une sortie personnalisée début heure ensemble tooDecember 12, 2012, 12:12:12 UTC :</span><span class="sxs-lookup"><span data-stu-id="6dc36-168">hello following sample code starts a Stream Analytics job with a custom output start time set tooDecember 12, 2012, 12:12:12 UTC:</span></span>

   ```
   // Start a streaming job
   StartStreamingJobParameters startStreamingJobParameters = new StartStreamingJobParameters()
   {
       OutputStartMode = OutputStartMode.CustomTime,
       OutputStartTime = new DateTime(2012, 12, 12, 12, 12, 12, DateTimeKind.Utc)
   };
   streamAnalyticsManagementClient.StreamingJobs.Start(resourceGroupName, streamingJobName, startStreamingJobParameters);
   ```

## <a name="stop-a-stream-analytics-job"></a><span data-ttu-id="6dc36-169">Arrêt d’un travail Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="6dc36-169">Stop a Stream Analytics job</span></span>
<span data-ttu-id="6dc36-170">Vous pouvez arrêter une tâche de flux de données Analytique en cours d’exécution en appelant hello **arrêter** (méthode).</span><span class="sxs-lookup"><span data-stu-id="6dc36-170">You can stop a running Stream Analytics job by calling hello **Stop** method.</span></span>

   ```
   // Stop a streaming job
   streamAnalyticsManagementClient.StreamingJobs.Stop(resourceGroupName, streamingJobName);
   ```

## <a name="delete-a-stream-analytics-job"></a><span data-ttu-id="6dc36-171">Suppression d’un travail Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="6dc36-171">Delete a Stream Analytics job</span></span>
<span data-ttu-id="6dc36-172">Hello **supprimer** méthode supprimera hello ainsi que les hello sous-jacent sous-ressources, notamment que les entrées, sorties et la transformation de la tâche de hello.</span><span class="sxs-lookup"><span data-stu-id="6dc36-172">hello **Delete** method will delete hello job as well as hello underlying sub-resources, including input(s), output(s), and transformation of hello job.</span></span>

   ```
   // Delete a streaming job
   streamAnalyticsManagementClient.StreamingJobs.Delete(resourceGroupName, streamingJobName);
   ```

## <a name="get-support"></a><span data-ttu-id="6dc36-173">Obtenir de l'aide</span><span class="sxs-lookup"><span data-stu-id="6dc36-173">Get support</span></span>
<span data-ttu-id="6dc36-174">Pour obtenir une assistance, consultez le [forum Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="6dc36-174">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6dc36-175">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6dc36-175">Next steps</span></span>
<span data-ttu-id="6dc36-176">Vous avez appris hello notions de base de l’utilisation d’un toocreate du Kit de développement .NET et exécuter des travaux de l’analytique.</span><span class="sxs-lookup"><span data-stu-id="6dc36-176">You've learned hello basics of using a .NET SDK toocreate and run analytics jobs.</span></span> <span data-ttu-id="6dc36-177">toolearn plus, voir hello :</span><span class="sxs-lookup"><span data-stu-id="6dc36-177">toolearn more, see hello following:</span></span>

* [<span data-ttu-id="6dc36-178">Introduction tooAzure Analytique de flux de données</span><span class="sxs-lookup"><span data-stu-id="6dc36-178">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="6dc36-179">Prise en main d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="6dc36-179">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="6dc36-180">Mise à l’échelle des travaux Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="6dc36-180">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* <span data-ttu-id="6dc36-181">[Kit de développement logiciel (SDK) .NET Azure Stream Analytics Management](https://msdn.microsoft.com/library/azure/dn889315.aspx)</span><span class="sxs-lookup"><span data-stu-id="6dc36-181">[Azure Stream Analytics Management .NET SDK](https://msdn.microsoft.com/library/azure/dn889315.aspx).</span></span>
* [<span data-ttu-id="6dc36-182">Références sur le langage des requêtes d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="6dc36-182">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="6dc36-183">Références sur l’API REST de gestion d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="6dc36-183">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

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
