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
# <a name="programmatically-create-a-stream-analytics-job-monitor"></a>Créer la surveillance des tâches Stream Analytics par programmation

Cet article explique comment tooenable analyse d’une tâche de flux de données Analytique. Par défaut, la surveillance n'est pas activée pour les travaux Stream Analytics créés par le biais des API REST, du kit de développement logiciel (SDK) Azure ou de PowerShell. Vous pouvez l’activer manuellement Bonjour portail Azure en accédant page de surveillance de la tâche toohello et activer le bouton en cliquant sur hello ou vous pouvez automatiser ce processus en suivant les étapes de hello dans cet article. Hello analyse les données s’afficheront dans zone de mesures hello Hello portail Azure pour votre tâche de flux de données Analytique.

## <a name="prerequisites"></a>Composants requis

Avant de commencer ce processus, vous devez disposer de hello :

* Visual Studio 2017 ou 2015
* [kit de développement logiciel (SDK) Azure .NET](https://azure.microsoft.com/downloads/) téléchargé et installé
* Une tâche Analytique de flux de données existante qui doit toohave analyse activée

## <a name="create-a-project"></a>Création d’un projet

1. Créez une application console Visual Studio .NET C#.
2. Dans la Console du Gestionnaire de Package de hello, suivante d’exécution hello commandes les packages NuGet tooinstall hello. Hello tout d’abord une est hello Azure flux Analytique Management .NET SDK. Hello second est hello SDK analyse Azure qui sera utilisé tooenable d’analyse. Hello dernière une est client Azure Active Directory hello qui sera utilisé pour l’authentification.
   
   ```
   Install-Package Microsoft.Azure.Management.StreamAnalytics
   Install-Package Microsoft.Azure.Insights -Pre
   Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
   ```
3. Ajoutez hello suivant appSettings section toohello du fichier App.config.
   
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
   Remplacez les valeurs de *SubscriptionId* et *ActiveDirectoryTenantId* par votre ID d’abonnement et votre ID de locataire Azure. Vous pouvez obtenir ces valeurs en exécutant hello suivant l’applet de commande PowerShell :
   
   ```
   Get-AzureAccount
   ```
4. Ajoutez hello qui suit à l’aide d’instructions toohello source fichier (Program.cs) hello projet.
   
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
5. Ajoutez une méthode d'aide pour l'authentification.
   
     public static string GetAuthorizationHeader()
   
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
     }

## <a name="create-management-clients"></a>Création de clients de gestion

Hello de code suivant définit les variables nécessaires de hello et les clients de gestion.

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

## <a name="enable-monitoring-for-an-existing-stream-analytics-job"></a>Activation de la surveillance pour un travail Stream Analytics existant

Active l’analyse de code suivant de Hello un **existant** tâche de flux de données Analytique. Hello première partie du code de hello effectue une demande GET hello flux Analytique service tooretrieve plus d’informations sur la tâche de flux de données Analytique hello particulière. Il utilise hello *Id* propriété (récupéré à partir de la demande d’obtention de hello) en tant que paramètre pour la méthode Put Bonjour de hello deuxième moitié de code hello, qui envoie une demande PUT toohello Insights analyse du service tooenable pour hello Analytique de flux de données tâche.

>[!WARNING]
>Si vous avez déjà activé la surveillance pour un travail de flux de données Analytique, via hello portail Azure ou par programme via hello sous code, **nous vous recommandons de fournir hello même nom de compte de stockage que vous avez utilisé lorsque vous précédemment activé le contrôle.**
> 
> compte de stockage Hello est région toohello lié que vous avez créé votre tâche de flux de données Analytique dans ne sont pas spécifiquement les travaux toohello lui-même.
> 
> Tous les flux de données Analytique travaux (et toutes les autres ressources Windows Azure) dans cette région même partagent cette toostore de compte de stockage données d’analyse. Si vous fournissez un autre compte de stockage, il peut provoquer des effets secondaires involontaires dans hello analyse de vos autres tâches de flux de données Analytique ou d’autres ressources Azure.
> 
> nom de compte de stockage Hello que vous utilisez tooreplace `<YOUR STORAGE ACCOUNT NAME>` Bonjour suivant le code doit être un compte de stockage qui se trouve dans hello même abonnement en tant que tâche de flux de données Analytique hello que vous activez la surveillance pour.
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



## <a name="get-support"></a>Obtenir de l'aide

Pour obtenir une assistance, consultez le [forum Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Étapes suivantes

* [Introduction tooAzure Analytique de flux de données](stream-analytics-introduction.md)
* [Prise en main d’Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Mise à l'échelle des travaux Azure Stream Analytics](stream-analytics-scale-jobs.md)
* [Références sur le langage des requêtes d'Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Références sur l’API REST de gestion d’Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

