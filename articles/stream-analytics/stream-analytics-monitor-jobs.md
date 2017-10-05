---
title: "Surveiller par programmation les travaux dans Stream Analytics | Microsoft Docs"
description: "Découvrez comment surveiller par programme les tâches Stream Analytics créées via des API REST, le kit de développement logiciel Microsoft Azure SDK ou PowerShell."
keywords: "surveillance .net, surveillance de tâches, surveillance d’applications"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 2ec02cc9-4ca5-4a25-ae60-c44be9ad4835
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 0d39e77316a03a705586af3ba970a7be1208ec85
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="programmatically-create-a-stream-analytics-job-monitor"></a><span data-ttu-id="3fdcc-104">Créer la surveillance des tâches Stream Analytics par programmation</span><span class="sxs-lookup"><span data-stu-id="3fdcc-104">Programmatically create a Stream Analytics job monitor</span></span>

<span data-ttu-id="3fdcc-105">Cet article explique comment activer la surveillance d'une tâche Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="3fdcc-105">This article demonstrates how to enable monitoring for a Stream Analytics job.</span></span> <span data-ttu-id="3fdcc-106">Par défaut, la surveillance n'est pas activée pour les travaux Stream Analytics créés par le biais des API REST, du kit de développement logiciel (SDK) Azure ou de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3fdcc-106">Stream Analytics jobs that are created via REST APIs, Azure SDK, or PowerShell do not have monitoring enabled by default.</span></span> <span data-ttu-id="3fdcc-107">Vous pouvez l’activer manuellement sur le portail Azure. Pour cela, accédez à la page Surveiller du travail et cliquez sur le bouton Activer. Vous pouvez également automatiser ce processus en suivant les étapes décrites dans cet article.</span><span class="sxs-lookup"><span data-stu-id="3fdcc-107">You can manually enable it in the Azure portal by going to the job’s Monitor page and clicking the Enable button or you can automate this process by following the steps in this article.</span></span> <span data-ttu-id="3fdcc-108">Les données de surveillance sont affichées dans la zone Métriques du portail Azure pour le travail Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="3fdcc-108">The monitoring data will show up in the Metrics area of the Azure portal for your Stream Analytics job.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3fdcc-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="3fdcc-109">Prerequisites</span></span>

<span data-ttu-id="3fdcc-110">Avant de commencer ce processus, vous devez disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="3fdcc-110">Before you begin this process, you must have the following:</span></span>

* <span data-ttu-id="3fdcc-111">Visual Studio 2017 ou 2015</span><span class="sxs-lookup"><span data-stu-id="3fdcc-111">Visual Studio 2017 or 2015</span></span>
* <span data-ttu-id="3fdcc-112">[kit de développement logiciel (SDK) Azure .NET](https://azure.microsoft.com/downloads/) téléchargé et installé</span><span class="sxs-lookup"><span data-stu-id="3fdcc-112">[Azure .NET SDK](https://azure.microsoft.com/downloads/) downloaded and installed</span></span>
* <span data-ttu-id="3fdcc-113">Un travail Stream Analytics existant pour lequel la surveillance doit être activée</span><span class="sxs-lookup"><span data-stu-id="3fdcc-113">An existing Stream Analytics job that needs to have monitoring enabled</span></span>

## <a name="create-a-project"></a><span data-ttu-id="3fdcc-114">Création d’un projet</span><span class="sxs-lookup"><span data-stu-id="3fdcc-114">Create a project</span></span>

1. <span data-ttu-id="3fdcc-115">Créez une application console Visual Studio .NET C#.</span><span class="sxs-lookup"><span data-stu-id="3fdcc-115">Create a Visual Studio C# .NET console application.</span></span>
2. <span data-ttu-id="3fdcc-116">Dans la console du Gestionnaire de package, exécutez les commandes suivantes pour installer les packages NuGet.</span><span class="sxs-lookup"><span data-stu-id="3fdcc-116">In the Package Manager Console, run the following commands to install the NuGet packages.</span></span> <span data-ttu-id="3fdcc-117">Le premier est le Kit de développement logiciel (SDK) .NET de gestion Azure Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="3fdcc-117">The first one is the Azure Stream Analytics Management .NET SDK.</span></span> <span data-ttu-id="3fdcc-118">Le second est le SDK Azure Monitor qui sera utilisé pour activer la surveillance.</span><span class="sxs-lookup"><span data-stu-id="3fdcc-118">The second one is the Azure Monitor SDK that will be used to enable monitoring.</span></span> <span data-ttu-id="3fdcc-119">Le dernier est le client Azure Active Directory utilisé pour l'authentification.</span><span class="sxs-lookup"><span data-stu-id="3fdcc-119">The last one is the Azure Active Directory client that will be used for authentication.</span></span>
   
   ```
   Install-Package Microsoft.Azure.Management.StreamAnalytics
   Install-Package Microsoft.Azure.Insights -Pre
   Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
   ```
3. <span data-ttu-id="3fdcc-120">Ajoutez la section appSettings suivante au fichier App.config.</span><span class="sxs-lookup"><span data-stu-id="3fdcc-120">Add the following appSettings section to the App.config file.</span></span>
   
   ```
   <appSettings>
     <!--CSM Prod related values-->
     <add key="ResourceGroupName" value="RESOURCE GROUP NAME" />
     <add key="JobName" value="YOUR JOB NAME" />
     <add key="StorageAccountName" value="YOUR STORAGE ACCOUNT"/>
     <add key="ActiveDirectoryEndpoint" value="https://login.microsoftonline.com/" />
     <add key="ResourceManagerEndpoint" value="https://management.azure.com/" />
     <add key="WindowsManagementUri" value="https://management.core.windows.net/" />
     <add key="AsaClientId" value="1950a258-227b-4e31-a9cf-717495945fc2" />
     <add key="RedirectUri" value="urn:ietf:wg:oauth:2.0:oob" />
     <add key="SubscriptionId" value="YOUR AZURE SUBSCRIPTION ID" />
     <add key="ActiveDirectoryTenantId" value="YOUR TENANT ID" />
   </appSettings>
   ```
   <span data-ttu-id="3fdcc-121">Remplacez les valeurs de *SubscriptionId* et *ActiveDirectoryTenantId* par votre ID d’abonnement et votre ID de locataire Azure.</span><span class="sxs-lookup"><span data-stu-id="3fdcc-121">Replace values for *SubscriptionId* and *ActiveDirectoryTenantId* with your Azure subscription and tenant IDs.</span></span> <span data-ttu-id="3fdcc-122">Vous pouvez obtenir ces valeurs en exécutant l'applet de commande PowerShell suivante :</span><span class="sxs-lookup"><span data-stu-id="3fdcc-122">You can get these values by running the following PowerShell cmdlet:</span></span>
   
   ```
   Get-AzureAccount
   ```
4. <span data-ttu-id="3fdcc-123">Ajoutez les instructions using suivantes au fichier source (Program.cs) dans le projet.</span><span class="sxs-lookup"><span data-stu-id="3fdcc-123">Add the following using statements to the source file (Program.cs) in the project.</span></span>
   
   ```
     using System;
     using System.Configuration;
     using System.Threading;
     using Microsoft.Azure;
     using Microsoft.Azure.Management.Insights;
     using Microsoft.Azure.Management.Insights.Models;
     using Microsoft.Azure.Management.StreamAnalytics;
     using Microsoft.Azure.Management.StreamAnalytics.Models;
     using Microsoft.IdentityModel.Clients.ActiveDirectory;
   ```
5. <span data-ttu-id="3fdcc-124">Ajoutez une méthode d'aide pour l'authentification.</span><span class="sxs-lookup"><span data-stu-id="3fdcc-124">Add an authentication helper method.</span></span>
   
     <span data-ttu-id="3fdcc-125">public static string GetAuthorizationHeader()</span><span class="sxs-lookup"><span data-stu-id="3fdcc-125">public static string GetAuthorizationHeader()</span></span>
   
         {
             AuthenticationResult result = null;
             var thread = new Thread(() =>
             {
                 try
                 {
                     var context = new AuthenticationContext(
                         ConfigurationManager.AppSettings["ActiveDirectoryEndpoint"] +
                         ConfigurationManager.AppSettings["ActiveDirectoryTenantId"]);
   
                     result = context.AcquireToken(
                         resource: ConfigurationManager.AppSettings["WindowsManagementUri"],
                         clientId: ConfigurationManager.AppSettings["AsaClientId"],
                         redirectUri: new Uri(ConfigurationManager.AppSettings["RedirectUri"]),
                         promptBehavior: PromptBehavior.Always);
                 }
                 catch (Exception threadEx)
                 {
                     Console.WriteLine(threadEx.Message);
                 }
             });
   
             thread.SetApartmentState(ApartmentState.STA);
             thread.Name = "AcquireTokenThread";
             thread.Start();
             thread.Join();
   
             if (result != null)
             {
                 return result.AccessToken;
             }
   
             throw new InvalidOperationException("Failed to acquire token");
     <span data-ttu-id="3fdcc-126">}</span><span class="sxs-lookup"><span data-stu-id="3fdcc-126">}</span></span>

## <a name="create-management-clients"></a><span data-ttu-id="3fdcc-127">Création de clients de gestion</span><span class="sxs-lookup"><span data-stu-id="3fdcc-127">Create management clients</span></span>

<span data-ttu-id="3fdcc-128">Le code suivant définit les variables nécessaires et les clients de gestion.</span><span class="sxs-lookup"><span data-stu-id="3fdcc-128">The following code will set up the necessary variables and management clients.</span></span>

    string resourceGroupName = "<YOUR AZURE RESOURCE GROUP NAME>";
    string streamAnalyticsJobName = "<YOUR STREAM ANALYTICS JOB NAME>";

    // Get authentication token
    TokenCloudCredentials aadTokenCredentials =
        new TokenCloudCredentials(
            ConfigurationManager.AppSettings["SubscriptionId"],
            GetAuthorizationHeader());

    Uri resourceManagerUri = new
    Uri(ConfigurationManager.AppSettings["ResourceManagerEndpoint"]);

    // Create Stream Analytics and Insights management client
    StreamAnalyticsManagementClient streamAnalyticsClient = new
    StreamAnalyticsManagementClient(aadTokenCredentials, resourceManagerUri);
    InsightsManagementClient insightsClient = new
    InsightsManagementClient(aadTokenCredentials, resourceManagerUri);

## <a name="enable-monitoring-for-an-existing-stream-analytics-job"></a><span data-ttu-id="3fdcc-129">Activation de la surveillance pour un travail Stream Analytics existant</span><span class="sxs-lookup"><span data-stu-id="3fdcc-129">Enable monitoring for an existing Stream Analytics job</span></span>

<span data-ttu-id="3fdcc-130">Le code suivant permet d'activer la surveillance pour un travail Stream Analytics **existant**.</span><span class="sxs-lookup"><span data-stu-id="3fdcc-130">The following code enables monitoring for an **existing** Stream Analytics job.</span></span> <span data-ttu-id="3fdcc-131">La première partie du code exécute une requête GET sur le service Stream Analytics pour récupérer des informations sur le travail Stream Analytics spécifique.</span><span class="sxs-lookup"><span data-stu-id="3fdcc-131">The first part of the code performs a GET request against the Stream Analytics service to retrieve information about the particular Stream Analytics job.</span></span> <span data-ttu-id="3fdcc-132">Elle utilise la propriété *Id* (récupérée à partir de la requête GET) en tant que paramètre pour la méthode Put dans la seconde moitié du code qui envoie une requête PUT au service Insights afin d'activer la surveillance du travail Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="3fdcc-132">It uses the *Id* property (retrieved from the GET request) as a parameter for the Put method in the second half of the code, which sends a PUT request to the Insights service to enable monitoring for the Stream Analytics job.</span></span>

>[!WARNING]
><span data-ttu-id="3fdcc-133">Si vous avez déjà activé la surveillance pour un travail Stream Analytics différente par le passé, via le portail Azure ou par programmation via le code ci-dessous, **nous vous recommandons de fournir le même nom de compte de stockage que celui utilisé lors de l’activation de la surveillance.**</span><span class="sxs-lookup"><span data-stu-id="3fdcc-133">If you have previously enabled monitoring for a different Stream Analytics job, either through the Azure portal or programmatically via the below code, **we recommend that you provide the same storage account name that you used when you previously enabled monitoring.**</span></span>
> 
> <span data-ttu-id="3fdcc-134">Le compte de stockage est lié à la région dans laquelle vous avez créé la tâche Stream Analytics, pas spécifiquement à la tâche en soi.</span><span class="sxs-lookup"><span data-stu-id="3fdcc-134">The storage account is linked to the region that you created your Stream Analytics job in, not specifically to the job itself.</span></span>
> 
> <span data-ttu-id="3fdcc-135">Tous les travaux Stream Analytics (et l’ensemble des autres ressources Microsoft Azure) d’une même région partagent ce compte de stockage afin d’y consigner les données de surveillance.</span><span class="sxs-lookup"><span data-stu-id="3fdcc-135">All Stream Analytics jobs (and all other Azure resources) in that same region share this storage account to store monitoring data.</span></span> <span data-ttu-id="3fdcc-136">Si vous communiquez un compte de stockage différent, cela peut entraîner des effets collatéraux imprévus sur la surveillance de vos autres travaux Stream Analytics ou autres ressources Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="3fdcc-136">If you provide a different storage account, it might cause unintended side effects in the monitoring of your other Stream Analytics jobs or other Azure resources.</span></span>
> 
> <span data-ttu-id="3fdcc-137">Le compte de stockage utilisé pour remplacer `<YOUR STORAGE ACCOUNT NAME>` dans le code ci-dessous doit être un compte de stockage qui se trouve dans l’abonnement du travail Stream Analytics pour lequel vous avez activé la surveillance.</span><span class="sxs-lookup"><span data-stu-id="3fdcc-137">The storage account name that you use to replace `<YOUR STORAGE ACCOUNT NAME>` in the following code should be a storage account that is in the same subscription as the Stream Analytics job that you are enabling monitoring for.</span></span>
> 
> 

    // Get an existing Stream Analytics job
    JobGetParameters jobGetParameters = new JobGetParameters()
    {
        PropertiesToExpand = "inputs,transformation,outputs"
    };
    JobGetResponse jobGetResponse = streamAnalyticsClient.StreamingJobs.Get(resourceGroupName, streamAnalyticsJobName, jobGetParameters);

    // Enable monitoring
    ServiceDiagnosticSettingsPutParameters insightPutParameters = new ServiceDiagnosticSettingsPutParameters()
    {
            Properties = new ServiceDiagnosticSettings()
            {
                StorageAccountName = "<YOUR STORAGE ACCOUNT NAME>"
            }
    };
    insightsClient.ServiceDiagnosticSettingsOperations.Put(jobGetResponse.Job.Id, insightPutParameters);



## <a name="get-support"></a><span data-ttu-id="3fdcc-138">Obtenir de l'aide</span><span class="sxs-lookup"><span data-stu-id="3fdcc-138">Get support</span></span>

<span data-ttu-id="3fdcc-139">Pour obtenir une assistance, consultez le [forum Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="3fdcc-139">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3fdcc-140">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3fdcc-140">Next steps</span></span>

* [<span data-ttu-id="3fdcc-141">Présentation d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="3fdcc-141">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="3fdcc-142">Prise en main d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="3fdcc-142">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="3fdcc-143">Mise à l'échelle des travaux Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="3fdcc-143">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="3fdcc-144">Références sur le langage des requêtes d'Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="3fdcc-144">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="3fdcc-145">Références sur l’API REST de gestion d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="3fdcc-145">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

