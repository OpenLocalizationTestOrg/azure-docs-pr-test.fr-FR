---
title: "surveiller les travaux aaaProgrammatically dans le flux de données Analytique | Documents Microsoft"
description: "Découvrez comment tooprogrammatically surveiller les travaux de flux de données Analytique créés via l’API REST, Windows Azure SDK ou PowerShell."
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
ms.openlocfilehash: 44a9c29c2161ee81ea76ece4646a8691bf5d5b48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="programmatically-create-a-stream-analytics-job-monitor"></a><span data-ttu-id="cf977-104">Créer la surveillance des tâches Stream Analytics par programmation</span><span class="sxs-lookup"><span data-stu-id="cf977-104">Programmatically create a Stream Analytics job monitor</span></span>

<span data-ttu-id="cf977-105">Cet article explique comment tooenable analyse d’une tâche de flux de données Analytique.</span><span class="sxs-lookup"><span data-stu-id="cf977-105">This article demonstrates how tooenable monitoring for a Stream Analytics job.</span></span> <span data-ttu-id="cf977-106">Par défaut, la surveillance n'est pas activée pour les travaux Stream Analytics créés par le biais des API REST, du kit de développement logiciel (SDK) Azure ou de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cf977-106">Stream Analytics jobs that are created via REST APIs, Azure SDK, or PowerShell do not have monitoring enabled by default.</span></span> <span data-ttu-id="cf977-107">Vous pouvez l’activer manuellement Bonjour portail Azure en accédant page de surveillance de la tâche toohello et activer le bouton en cliquant sur hello ou vous pouvez automatiser ce processus en suivant les étapes de hello dans cet article.</span><span class="sxs-lookup"><span data-stu-id="cf977-107">You can manually enable it in hello Azure portal by going toohello job’s Monitor page and clicking hello Enable button or you can automate this process by following hello steps in this article.</span></span> <span data-ttu-id="cf977-108">Hello analyse les données s’afficheront dans zone de mesures hello Hello portail Azure pour votre tâche de flux de données Analytique.</span><span class="sxs-lookup"><span data-stu-id="cf977-108">hello monitoring data will show up in hello Metrics area of hello Azure portal for your Stream Analytics job.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cf977-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="cf977-109">Prerequisites</span></span>

<span data-ttu-id="cf977-110">Avant de commencer ce processus, vous devez disposer de hello :</span><span class="sxs-lookup"><span data-stu-id="cf977-110">Before you begin this process, you must have hello following:</span></span>

* <span data-ttu-id="cf977-111">Visual Studio 2017 ou 2015</span><span class="sxs-lookup"><span data-stu-id="cf977-111">Visual Studio 2017 or 2015</span></span>
* <span data-ttu-id="cf977-112">[kit de développement logiciel (SDK) Azure .NET](https://azure.microsoft.com/downloads/) téléchargé et installé</span><span class="sxs-lookup"><span data-stu-id="cf977-112">[Azure .NET SDK](https://azure.microsoft.com/downloads/) downloaded and installed</span></span>
* <span data-ttu-id="cf977-113">Une tâche Analytique de flux de données existante qui doit toohave analyse activée</span><span class="sxs-lookup"><span data-stu-id="cf977-113">An existing Stream Analytics job that needs toohave monitoring enabled</span></span>

## <a name="create-a-project"></a><span data-ttu-id="cf977-114">Création d’un projet</span><span class="sxs-lookup"><span data-stu-id="cf977-114">Create a project</span></span>

1. <span data-ttu-id="cf977-115">Créez une application console Visual Studio .NET C#.</span><span class="sxs-lookup"><span data-stu-id="cf977-115">Create a Visual Studio C# .NET console application.</span></span>
2. <span data-ttu-id="cf977-116">Dans la Console du Gestionnaire de Package de hello, suivante d’exécution hello commandes les packages NuGet tooinstall hello.</span><span class="sxs-lookup"><span data-stu-id="cf977-116">In hello Package Manager Console, run hello following commands tooinstall hello NuGet packages.</span></span> <span data-ttu-id="cf977-117">Hello tout d’abord une est hello Azure flux Analytique Management .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="cf977-117">hello first one is hello Azure Stream Analytics Management .NET SDK.</span></span> <span data-ttu-id="cf977-118">Hello second est hello SDK analyse Azure qui sera utilisé tooenable d’analyse.</span><span class="sxs-lookup"><span data-stu-id="cf977-118">hello second one is hello Azure Monitor SDK that will be used tooenable monitoring.</span></span> <span data-ttu-id="cf977-119">Hello dernière une est client Azure Active Directory hello qui sera utilisé pour l’authentification.</span><span class="sxs-lookup"><span data-stu-id="cf977-119">hello last one is hello Azure Active Directory client that will be used for authentication.</span></span>
   
   ```
   Install-Package Microsoft.Azure.Management.StreamAnalytics
   Install-Package Microsoft.Azure.Insights -Pre
   Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
   ```
3. <span data-ttu-id="cf977-120">Ajoutez hello suivant appSettings section toohello du fichier App.config.</span><span class="sxs-lookup"><span data-stu-id="cf977-120">Add hello following appSettings section toohello App.config file.</span></span>
   
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
   <span data-ttu-id="cf977-121">Remplacez les valeurs de *SubscriptionId* et *ActiveDirectoryTenantId* par votre ID d’abonnement et votre ID de locataire Azure.</span><span class="sxs-lookup"><span data-stu-id="cf977-121">Replace values for *SubscriptionId* and *ActiveDirectoryTenantId* with your Azure subscription and tenant IDs.</span></span> <span data-ttu-id="cf977-122">Vous pouvez obtenir ces valeurs en exécutant hello suivant l’applet de commande PowerShell :</span><span class="sxs-lookup"><span data-stu-id="cf977-122">You can get these values by running hello following PowerShell cmdlet:</span></span>
   
   ```
   Get-AzureAccount
   ```
4. <span data-ttu-id="cf977-123">Ajoutez hello qui suit à l’aide d’instructions toohello source fichier (Program.cs) hello projet.</span><span class="sxs-lookup"><span data-stu-id="cf977-123">Add hello following using statements toohello source file (Program.cs) in hello project.</span></span>
   
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
5. <span data-ttu-id="cf977-124">Ajoutez une méthode d'aide pour l'authentification.</span><span class="sxs-lookup"><span data-stu-id="cf977-124">Add an authentication helper method.</span></span>
   
     <span data-ttu-id="cf977-125">public static string GetAuthorizationHeader()</span><span class="sxs-lookup"><span data-stu-id="cf977-125">public static string GetAuthorizationHeader()</span></span>
   
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
   
             throw new InvalidOperationException("Failed tooacquire token");
     <span data-ttu-id="cf977-126">}</span><span class="sxs-lookup"><span data-stu-id="cf977-126">}</span></span>

## <a name="create-management-clients"></a><span data-ttu-id="cf977-127">Création de clients de gestion</span><span class="sxs-lookup"><span data-stu-id="cf977-127">Create management clients</span></span>

<span data-ttu-id="cf977-128">Hello de code suivant définit les variables nécessaires de hello et les clients de gestion.</span><span class="sxs-lookup"><span data-stu-id="cf977-128">hello following code will set up hello necessary variables and management clients.</span></span>

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

## <a name="enable-monitoring-for-an-existing-stream-analytics-job"></a><span data-ttu-id="cf977-129">Activation de la surveillance pour un travail Stream Analytics existant</span><span class="sxs-lookup"><span data-stu-id="cf977-129">Enable monitoring for an existing Stream Analytics job</span></span>

<span data-ttu-id="cf977-130">Active l’analyse de code suivant de Hello un **existant** tâche de flux de données Analytique.</span><span class="sxs-lookup"><span data-stu-id="cf977-130">hello following code enables monitoring for an **existing** Stream Analytics job.</span></span> <span data-ttu-id="cf977-131">Hello première partie du code de hello effectue une demande GET hello flux Analytique service tooretrieve plus d’informations sur la tâche de flux de données Analytique hello particulière.</span><span class="sxs-lookup"><span data-stu-id="cf977-131">hello first part of hello code performs a GET request against hello Stream Analytics service tooretrieve information about hello particular Stream Analytics job.</span></span> <span data-ttu-id="cf977-132">Il utilise hello *Id* propriété (récupéré à partir de la demande d’obtention de hello) en tant que paramètre pour la méthode Put Bonjour de hello deuxième moitié de code hello, qui envoie une demande PUT toohello Insights analyse du service tooenable pour hello Analytique de flux de données tâche.</span><span class="sxs-lookup"><span data-stu-id="cf977-132">It uses hello *Id* property (retrieved from hello GET request) as a parameter for hello Put method in hello second half of hello code, which sends a PUT request toohello Insights service tooenable monitoring for hello Stream Analytics job.</span></span>

>[!WARNING]
><span data-ttu-id="cf977-133">Si vous avez déjà activé la surveillance pour un travail de flux de données Analytique, via hello portail Azure ou par programme via hello sous code, **nous vous recommandons de fournir hello même nom de compte de stockage que vous avez utilisé lorsque vous précédemment activé le contrôle.**</span><span class="sxs-lookup"><span data-stu-id="cf977-133">If you have previously enabled monitoring for a different Stream Analytics job, either through hello Azure portal or programmatically via hello below code, **we recommend that you provide hello same storage account name that you used when you previously enabled monitoring.**</span></span>
> 
> <span data-ttu-id="cf977-134">compte de stockage Hello est région toohello lié que vous avez créé votre tâche de flux de données Analytique dans ne sont pas spécifiquement les travaux toohello lui-même.</span><span class="sxs-lookup"><span data-stu-id="cf977-134">hello storage account is linked toohello region that you created your Stream Analytics job in, not specifically toohello job itself.</span></span>
> 
> <span data-ttu-id="cf977-135">Tous les flux de données Analytique travaux (et toutes les autres ressources Windows Azure) dans cette région même partagent cette toostore de compte de stockage données d’analyse.</span><span class="sxs-lookup"><span data-stu-id="cf977-135">All Stream Analytics jobs (and all other Azure resources) in that same region share this storage account toostore monitoring data.</span></span> <span data-ttu-id="cf977-136">Si vous fournissez un autre compte de stockage, il peut provoquer des effets secondaires involontaires dans hello analyse de vos autres tâches de flux de données Analytique ou d’autres ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="cf977-136">If you provide a different storage account, it might cause unintended side effects in hello monitoring of your other Stream Analytics jobs or other Azure resources.</span></span>
> 
> <span data-ttu-id="cf977-137">nom de compte de stockage Hello que vous utilisez tooreplace `<YOUR STORAGE ACCOUNT NAME>` Bonjour suivant le code doit être un compte de stockage qui se trouve dans hello même abonnement en tant que tâche de flux de données Analytique hello que vous activez la surveillance pour.</span><span class="sxs-lookup"><span data-stu-id="cf977-137">hello storage account name that you use tooreplace `<YOUR STORAGE ACCOUNT NAME>` in hello following code should be a storage account that is in hello same subscription as hello Stream Analytics job that you are enabling monitoring for.</span></span>
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



## <a name="get-support"></a><span data-ttu-id="cf977-138">Obtenir de l'aide</span><span class="sxs-lookup"><span data-stu-id="cf977-138">Get support</span></span>

<span data-ttu-id="cf977-139">Pour obtenir une assistance, consultez le [forum Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="cf977-139">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="cf977-140">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="cf977-140">Next steps</span></span>

* [<span data-ttu-id="cf977-141">Introduction tooAzure Analytique de flux de données</span><span class="sxs-lookup"><span data-stu-id="cf977-141">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="cf977-142">Prise en main d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="cf977-142">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="cf977-143">Mise à l'échelle des travaux Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="cf977-143">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="cf977-144">Références sur le langage des requêtes d'Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="cf977-144">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="cf977-145">Références sur l’API REST de gestion d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="cf977-145">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

