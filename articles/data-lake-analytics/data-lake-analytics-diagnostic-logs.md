---
title: "Affichage des journaux de diagnostic d’Azure Data Lake Analytics | Microsoft Docs"
description: "Comprendre comment configurer les journaux de diagnostic et y accéder pour Azure Data Lake Analytics  "
services: data-lake-analytics
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: cf5633d4-bc43-444e-90fc-f90fbd0b7935
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 6c74db1659742aa41306388273bec46800ba7609
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="accessing-diagnostic-logs-for-azure-data-lake-analytics"></a><span data-ttu-id="f2953-103">Accès aux journaux de diagnostic d’Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="f2953-103">Accessing diagnostic logs for Azure Data Lake Analytics</span></span>

<span data-ttu-id="f2953-104">La journalisation de diagnostic vous permet de collecter les pistes d’audit d’accès aux données.</span><span class="sxs-lookup"><span data-stu-id="f2953-104">Diagnostic logging allows you to collect data access audit trails.</span></span> <span data-ttu-id="f2953-105">Ces journaux fournissent des informations comme :</span><span class="sxs-lookup"><span data-stu-id="f2953-105">These logs provide information such as:</span></span>

* <span data-ttu-id="f2953-106">Une liste des utilisateurs qui ont accédé aux données.</span><span class="sxs-lookup"><span data-stu-id="f2953-106">A list of users that accessed the data.</span></span>
* <span data-ttu-id="f2953-107">La fréquence à laquelle les données sont consultées.</span><span class="sxs-lookup"><span data-stu-id="f2953-107">How frequently the data is accessed.</span></span>
* <span data-ttu-id="f2953-108">La quantité de données stockées dans le compte.</span><span class="sxs-lookup"><span data-stu-id="f2953-108">How much data is stored in the account.</span></span>

## <a name="enable-logging"></a><span data-ttu-id="f2953-109">Activation de la journalisation</span><span class="sxs-lookup"><span data-stu-id="f2953-109">Enable logging</span></span>

1. <span data-ttu-id="f2953-110">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f2953-110">Sign on to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="f2953-111">Ouvrez votre compte Data Lake Analytics et sélectionnez **Journaux de diagnostic** dans la section __Surveiller__.</span><span class="sxs-lookup"><span data-stu-id="f2953-111">Open your Data Lake Analytics account and select **Diagnostic logs** from the __Monitor__ section.</span></span> <span data-ttu-id="f2953-112">Ensuite, sélectionnez __Activer les diagnostics__.</span><span class="sxs-lookup"><span data-stu-id="f2953-112">Next, select __Turn on diagnostics__.</span></span>

    ![Activer les diagnostics pour collecter des journaux d’audit et de requêtes](./media/data-lake-analytics-diagnostic-logs/turn-on-logging.png)

3. <span data-ttu-id="f2953-114">Dans les __Paramètres de diagnostic__, définissez le statut sur __Activé__ et sélectionnez les options de journalisation.</span><span class="sxs-lookup"><span data-stu-id="f2953-114">From __Diagnostics settings__, set the status to __On__ and select logging options.</span></span>

    <span data-ttu-id="f2953-115">![Activer les diagnostics pour collecter des journaux d’audit et de requêtes](./media/data-lake-analytics-diagnostic-logs/enable-diagnostic-logs.png "Activer les journaux de diagnostic")</span><span class="sxs-lookup"><span data-stu-id="f2953-115">![Turn on diagnostics to collect audit and request logs](./media/data-lake-analytics-diagnostic-logs/enable-diagnostic-logs.png "Enable diagnostic logs")</span></span>

   * <span data-ttu-id="f2953-116">Définissez **État** sur **Activé** pour activer la journalisation de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="f2953-116">Set **Status** to **On** to enable diagnostic logging.</span></span>

   * <span data-ttu-id="f2953-117">Vous pouvez choisir de stocker/traiter les données de trois manières différentes.</span><span class="sxs-lookup"><span data-stu-id="f2953-117">You can choose to store/process the data in three different ways.</span></span>

     * <span data-ttu-id="f2953-118">Sélectionnez __Archive to a storage account (Archiver dans un compte de stockage)__ pour stocker les journaux dans un compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="f2953-118">Select __Archive to a storage account__ to store logs in an Azure storage account.</span></span> <span data-ttu-id="f2953-119">Utilisez cette option si vous souhaitez archiver les données.</span><span class="sxs-lookup"><span data-stu-id="f2953-119">Use this option if you want to archive the data.</span></span> <span data-ttu-id="f2953-120">Si vous sélectionnez cette option, vous devez fournir un compte de stockage Azure dans lequel enregistrer les journaux.</span><span class="sxs-lookup"><span data-stu-id="f2953-120">If you select this option, you must provide an Azure storage account to save the logs to.</span></span>

     * <span data-ttu-id="f2953-121">Sélectionnez **Stream to an Event hub (Transmettre à un Event Hub)** pour transmettre les données journalisées à un Event Hub Azure.</span><span class="sxs-lookup"><span data-stu-id="f2953-121">Select **Stream to an Event Hub** to stream log data to an Azure Event Hub.</span></span> <span data-ttu-id="f2953-122">Utilisez cette option si vous disposez d’un pipeline de traitement en aval qui analyse les journaux entrants en temps réel.</span><span class="sxs-lookup"><span data-stu-id="f2953-122">Use this option if you have a downstream processing pipeline that is analyzing incoming logs in real time.</span></span> <span data-ttu-id="f2953-123">Si vous sélectionnez cette option, vous devez fournir les informations relatives au Event Hub Azure que vous souhaitez utiliser.</span><span class="sxs-lookup"><span data-stu-id="f2953-123">If you select this option, you must provide the details for the Azure Event Hub you want to use.</span></span>

     * <span data-ttu-id="f2953-124">Sélectionnez __Send to Log Analytics (Envoyer à Log Analytics)__ pour envoyer les données au service Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="f2953-124">Select __Send to Log Analytics__ to send the data to the Log Analytics service.</span></span> <span data-ttu-id="f2953-125">Utilisez cette option si vous souhaitez utiliser Log Analytics pour collecter et analyser les journaux.</span><span class="sxs-lookup"><span data-stu-id="f2953-125">Use this option if you want to use Log Analytics to gather and analyze logs.</span></span>
   * <span data-ttu-id="f2953-126">Spécifiez si vous souhaitez obtenir des journaux d’audit ou des journaux de demande ou les deux.</span><span class="sxs-lookup"><span data-stu-id="f2953-126">Specify whether you want to get audit logs or request logs or both.</span></span>  <span data-ttu-id="f2953-127">Un journal des requêtes capture chaque demande d’API.</span><span class="sxs-lookup"><span data-stu-id="f2953-127">A request log captures every API request.</span></span> <span data-ttu-id="f2953-128">Un journal d’audit enregistre toutes les opérations qui sont déclenchées par cette demande d’API.</span><span class="sxs-lookup"><span data-stu-id="f2953-128">An audit log records all operations that are triggered by that API request.</span></span>

   * <span data-ttu-id="f2953-129">Pour __Archiver dans un compte de stockage__, spécifiez le nombre de jours pendant lesquels conserver les données.</span><span class="sxs-lookup"><span data-stu-id="f2953-129">For __Archive to a storage account__, specify the number of days to retain the data.</span></span>

   * <span data-ttu-id="f2953-130">Cliquez sur __Enregistrer__.</span><span class="sxs-lookup"><span data-stu-id="f2953-130">Click __Save__.</span></span>

        > [!NOTE]
        > <span data-ttu-id="f2953-131">Vous devez sélectionner __Archiver dans un compte de stockage__, __Diffuser vers Event Hub__ ou __Envoyer à Log Analytics__ avant de cliquer sur le bouton __Enregistrer__.</span><span class="sxs-lookup"><span data-stu-id="f2953-131">You must select either __Archive to a storage account__, __Stream to an Event Hub__ or __Send to Log Analytics__ before clicking the __Save__ button.</span></span>

<span data-ttu-id="f2953-132">Une fois que vous avez activé les paramètres de diagnostic, vous pouvez retourner dans le panneau __Journaux de diagnostic__ pour consulter les journaux.</span><span class="sxs-lookup"><span data-stu-id="f2953-132">Once you have enabled diagnostic settings, you can return to the __Diagnostics logs__ blade to view the logs.</span></span>

## <a name="view-logs"></a><span data-ttu-id="f2953-133">Consulter les journaux</span><span class="sxs-lookup"><span data-stu-id="f2953-133">View logs</span></span>

### <a name="use-the-data-lake-analytics-view"></a><span data-ttu-id="f2953-134">Utiliser la vue Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="f2953-134">Use the Data Lake Analytics view</span></span>

1. <span data-ttu-id="f2953-135">Dans le panneau de votre compte Data Lake Analytics, sous **Surveillance**, sélectionnez **Journaux de diagnostic**, puis sélectionnez l’entrée pour laquelle afficher les journaux.</span><span class="sxs-lookup"><span data-stu-id="f2953-135">From your Data Lake Analytics account blade, under **Monitoring**, select **Diagnostic Logs** and then select an entry to display logs for.</span></span>

    <span data-ttu-id="f2953-136">![Afficher la journalisation des diagnostics](./media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs.png "Afficher les journaux de diagnostic")</span><span class="sxs-lookup"><span data-stu-id="f2953-136">![View diagnostic logging](./media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs.png "View diagnostic logs")</span></span>

2. <span data-ttu-id="f2953-137">Les journaux sont classés par **journaux d’audit** et **journaux de requêtes**.</span><span class="sxs-lookup"><span data-stu-id="f2953-137">The logs are categorized by **Audit Logs** and **Request Logs**.</span></span>

    ![entrées de journal](./media/data-lake-analytics-diagnostic-logs/diagnostic-log-entries.png)

   * <span data-ttu-id="f2953-139">Les journaux de demande capturent chaque demande d’API effectuée sur le compte Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="f2953-139">Request logs capture every API request made on the Data Lake Analytics account.</span></span>
   * <span data-ttu-id="f2953-140">Les journaux d’audit sont similaires aux journaux de requête, mais ils offrent une répartition beaucoup plus détaillée des opérations.</span><span class="sxs-lookup"><span data-stu-id="f2953-140">Audit Logs are similar to request Logs but provide a much more detailed breakdown of the operations.</span></span> <span data-ttu-id="f2953-141">Par exemple, un simple appel d’API de chargement dans un journal de demande peut entraîner plusieurs opérations « Ajouter » dans son journal d’audit.</span><span class="sxs-lookup"><span data-stu-id="f2953-141">For example, a single upload API call in a request log can result in multiple "Append" operations in its audit log.</span></span>

3. <span data-ttu-id="f2953-142">Cliquez sur le lien **Télécharger** d’une entrée de journal pour le télécharger.</span><span class="sxs-lookup"><span data-stu-id="f2953-142">Click the **Download** link for a log entry to download that log.</span></span>

### <a name="use-the-azure-storage-account-that-contains-log-data"></a><span data-ttu-id="f2953-143">Utiliser le compte de Stockage Azure qui contient les données du journal</span><span class="sxs-lookup"><span data-stu-id="f2953-143">Use the Azure Storage account that contains log data</span></span>

1. <span data-ttu-id="f2953-144">Ouvrez le panneau du compte de Stockage Azure associé à Data Lake Analytics pour la journalisation, puis cliquez sur __Objets blob__.</span><span class="sxs-lookup"><span data-stu-id="f2953-144">Open the Azure Storage account blade associated with Data Lake Analytics for logging, and then click __Blobs__.</span></span> <span data-ttu-id="f2953-145">Le panneau **Service Blob** répertorie deux conteneurs.</span><span class="sxs-lookup"><span data-stu-id="f2953-145">The **Blob service** blade lists two containers.</span></span>

    <span data-ttu-id="f2953-146">![Afficher la journalisation des diagnostics](./media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs-storage-account.png "Afficher les journaux de diagnostic")</span><span class="sxs-lookup"><span data-stu-id="f2953-146">![View diagnostic logging](./media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs-storage-account.png "View diagnostic logs")</span></span>

   * <span data-ttu-id="f2953-147">Le conteneur **insights-logs-audit** contient les journaux d’audit.</span><span class="sxs-lookup"><span data-stu-id="f2953-147">The container **insights-logs-audit** contains the audit logs.</span></span>
   * <span data-ttu-id="f2953-148">Le conteneur **insights-logs-requests** contient les journaux de demande.</span><span class="sxs-lookup"><span data-stu-id="f2953-148">The container **insights-logs-requests** contains the request logs.</span></span>
2. <span data-ttu-id="f2953-149">Les journaux sont stockés dans ces conteneurs selon la structure suivante :</span><span class="sxs-lookup"><span data-stu-id="f2953-149">Within these containers, the logs are stored under the following structure:</span></span>

        resourceId=/
          SUBSCRIPTIONS/
            <<SUBSCRIPTION_ID>>/
              RESOURCEGROUPS/
                <<RESOURCE_GRP_NAME>>/
                  PROVIDERS/
                    MICROSOFT.DATALAKEANALYTICS/
                      ACCOUNTS/
                        <DATA_LAKE_ANALYTICS_NAME>>/
                          y=####/
                            m=##/
                              d=##/
                                h=##/
                                  m=00/
                                    PT1H.json

   > [!NOTE]
   > <span data-ttu-id="f2953-150">Le panneau `##` dans le chemin d’accès contiennent l’année, le mois, le jour et l’heure auxquels le journal a été créé.</span><span class="sxs-lookup"><span data-stu-id="f2953-150">The `##` entries in the path contain the year, month, day, and hour in which the log was created.</span></span> <span data-ttu-id="f2953-151">Data Lake Analytics crée un fichier toutes les heures, par conséquent, `m=` contient toujours une valeur de `00`.</span><span class="sxs-lookup"><span data-stu-id="f2953-151">Data Lake Analytics creates one file every hour, so `m=` always contains a value of `00`.</span></span>

    <span data-ttu-id="f2953-152">Par exemple, le chemin d’accès complet à un journal d’audit peut être :</span><span class="sxs-lookup"><span data-stu-id="f2953-152">As an example, the complete path to an audit log could be:</span></span>

        https://adllogs.blob.core.windows.net/insights-logs-audit/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/mydatalakeanalytics/y=2016/m=07/d=18/h=04/m=00/PT1H.json

    <span data-ttu-id="f2953-153">De même, le chemin d’accès complet à un journal de demande peut être :</span><span class="sxs-lookup"><span data-stu-id="f2953-153">Similarly, the complete path to a request log could be:</span></span>

        https://adllogs.blob.core.windows.net/insights-logs-requests/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/mydatalakeanalytics/y=2016/m=07/d=18/h=14/m=00/PT1H.json

## <a name="log-structure"></a><span data-ttu-id="f2953-154">Structure journal</span><span class="sxs-lookup"><span data-stu-id="f2953-154">Log structure</span></span>

<span data-ttu-id="f2953-155">Les journaux d’audit et de demande présentent un format JSON structuré.</span><span class="sxs-lookup"><span data-stu-id="f2953-155">The audit and request logs are in a structured JSON format.</span></span>

### <a name="request-logs"></a><span data-ttu-id="f2953-156">journaux de demande</span><span class="sxs-lookup"><span data-stu-id="f2953-156">Request logs</span></span>

<span data-ttu-id="f2953-157">Voici un exemple d’entrée dans le journal de demande au format JSON.</span><span class="sxs-lookup"><span data-stu-id="f2953-157">Here's a sample entry in the JSON-formatted request log.</span></span> <span data-ttu-id="f2953-158">Chaque objet blob a un objet racine appelé **enregistrements** qui contient un tableau d’objets du journal.</span><span class="sxs-lookup"><span data-stu-id="f2953-158">Each blob has one root object called **records** that contains an array of log objects.</span></span>

    {
    "records":
      [        
        . . . .
        ,
        {
             "time": "2016-07-07T21:02:53.456Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/<data_lake_analytics_account_name>",
             "category": "Requests",
             "operationName": "GetAggregatedJobHistory",
             "resultType": "200",
             "callerIpAddress": "::ffff:1.1.1.1",
             "correlationId": "4a11c709-05f5-417c-a98d-6e81b3e29c58",
             "identity": "1808bd5f-62af-45f4-89d8-03c5e81bac30",
             "properties": {
                 "HttpMethod":"POST",
                 "Path":"/JobAggregatedHistory",
                 "RequestContentLength":122,
                 "ClientRequestId":"3b7adbd9-3519-4f28-a61c-bd89506163b8",
                 "StartTime":"2016-07-07T21:02:52.472Z",
                 "EndTime":"2016-07-07T21:02:53.456Z"
                 }
        }
        ,
        . . . .
      ]
    }

#### <a name="request-log-schema"></a><span data-ttu-id="f2953-159">Schéma du journal de requête</span><span class="sxs-lookup"><span data-stu-id="f2953-159">Request log schema</span></span>

| <span data-ttu-id="f2953-160">Name</span><span class="sxs-lookup"><span data-stu-id="f2953-160">Name</span></span> | <span data-ttu-id="f2953-161">Type</span><span class="sxs-lookup"><span data-stu-id="f2953-161">Type</span></span> | <span data-ttu-id="f2953-162">Description</span><span class="sxs-lookup"><span data-stu-id="f2953-162">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f2953-163">time</span><span class="sxs-lookup"><span data-stu-id="f2953-163">time</span></span> |<span data-ttu-id="f2953-164">Chaîne</span><span class="sxs-lookup"><span data-stu-id="f2953-164">String</span></span> |<span data-ttu-id="f2953-165">L’horodatage (heure UTC) du journal.</span><span class="sxs-lookup"><span data-stu-id="f2953-165">The timestamp (in UTC) of the log</span></span> |
| <span data-ttu-id="f2953-166">resourceId</span><span class="sxs-lookup"><span data-stu-id="f2953-166">resourceId</span></span> |<span data-ttu-id="f2953-167">String</span><span class="sxs-lookup"><span data-stu-id="f2953-167">String</span></span> |<span data-ttu-id="f2953-168">L’identificateur de la ressource sur laquelle l’opération a eu lieu.</span><span class="sxs-lookup"><span data-stu-id="f2953-168">The identifier of the resource that operation took place on</span></span> |
| <span data-ttu-id="f2953-169">category</span><span class="sxs-lookup"><span data-stu-id="f2953-169">category</span></span> |<span data-ttu-id="f2953-170">Chaîne</span><span class="sxs-lookup"><span data-stu-id="f2953-170">String</span></span> |<span data-ttu-id="f2953-171">La catégorie du journal.</span><span class="sxs-lookup"><span data-stu-id="f2953-171">The log category.</span></span> <span data-ttu-id="f2953-172">Par exemple, **Demandes**.</span><span class="sxs-lookup"><span data-stu-id="f2953-172">For example, **Requests**.</span></span> |
| <span data-ttu-id="f2953-173">operationName</span><span class="sxs-lookup"><span data-stu-id="f2953-173">operationName</span></span> |<span data-ttu-id="f2953-174">Chaîne</span><span class="sxs-lookup"><span data-stu-id="f2953-174">String</span></span> |<span data-ttu-id="f2953-175">Le nom de l’opération qui est journalisée.</span><span class="sxs-lookup"><span data-stu-id="f2953-175">Name of the operation that is logged.</span></span> <span data-ttu-id="f2953-176">Par exemple, GetAggregatedJobHistory.</span><span class="sxs-lookup"><span data-stu-id="f2953-176">For example, GetAggregatedJobHistory.</span></span> |
| <span data-ttu-id="f2953-177">resultType</span><span class="sxs-lookup"><span data-stu-id="f2953-177">resultType</span></span> |<span data-ttu-id="f2953-178">Chaîne</span><span class="sxs-lookup"><span data-stu-id="f2953-178">String</span></span> |<span data-ttu-id="f2953-179">L’état de l’opération. Par exemple, 200.</span><span class="sxs-lookup"><span data-stu-id="f2953-179">The status of the operation, For example, 200.</span></span> |
| <span data-ttu-id="f2953-180">callerIpAddress</span><span class="sxs-lookup"><span data-stu-id="f2953-180">callerIpAddress</span></span> |<span data-ttu-id="f2953-181">Chaîne</span><span class="sxs-lookup"><span data-stu-id="f2953-181">String</span></span> |<span data-ttu-id="f2953-182">L’adresse IP du client qui a effectué la demande.</span><span class="sxs-lookup"><span data-stu-id="f2953-182">The IP address of the client making the request</span></span> |
| <span data-ttu-id="f2953-183">correlationId</span><span class="sxs-lookup"><span data-stu-id="f2953-183">correlationId</span></span> |<span data-ttu-id="f2953-184">String</span><span class="sxs-lookup"><span data-stu-id="f2953-184">String</span></span> |<span data-ttu-id="f2953-185">L’identificateur du journal.</span><span class="sxs-lookup"><span data-stu-id="f2953-185">The identifier of the log.</span></span> <span data-ttu-id="f2953-186">Cette valeur peut être utilisée pour regrouper un ensemble d’entrées de journal associées.</span><span class="sxs-lookup"><span data-stu-id="f2953-186">This value can be used to group a set of related log entries.</span></span> |
| <span data-ttu-id="f2953-187">identité</span><span class="sxs-lookup"><span data-stu-id="f2953-187">identity</span></span> |<span data-ttu-id="f2953-188">Object</span><span class="sxs-lookup"><span data-stu-id="f2953-188">Object</span></span> |<span data-ttu-id="f2953-189">L’identité qui a généré le journal.</span><span class="sxs-lookup"><span data-stu-id="f2953-189">The identity that generated the log</span></span> |
| <span data-ttu-id="f2953-190">properties</span><span class="sxs-lookup"><span data-stu-id="f2953-190">properties</span></span> |<span data-ttu-id="f2953-191">JSON</span><span class="sxs-lookup"><span data-stu-id="f2953-191">JSON</span></span> |<span data-ttu-id="f2953-192">Consultez la section suivante (Schéma des propriétés de journal de demande) pour plus d’informations</span><span class="sxs-lookup"><span data-stu-id="f2953-192">See the next section (Request log properties schema) for details</span></span> |

#### <a name="request-log-properties-schema"></a><span data-ttu-id="f2953-193">Schéma des propriétés de journal de demande</span><span class="sxs-lookup"><span data-stu-id="f2953-193">Request log properties schema</span></span>

| <span data-ttu-id="f2953-194">Name</span><span class="sxs-lookup"><span data-stu-id="f2953-194">Name</span></span> | <span data-ttu-id="f2953-195">Type</span><span class="sxs-lookup"><span data-stu-id="f2953-195">Type</span></span> | <span data-ttu-id="f2953-196">Description</span><span class="sxs-lookup"><span data-stu-id="f2953-196">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f2953-197">HttpMethod</span><span class="sxs-lookup"><span data-stu-id="f2953-197">HttpMethod</span></span> |<span data-ttu-id="f2953-198">Chaîne</span><span class="sxs-lookup"><span data-stu-id="f2953-198">String</span></span> |<span data-ttu-id="f2953-199">La méthode HTTP utilisée pour l’opération.</span><span class="sxs-lookup"><span data-stu-id="f2953-199">The HTTP Method used for the operation.</span></span> <span data-ttu-id="f2953-200">Par exemple, GET.</span><span class="sxs-lookup"><span data-stu-id="f2953-200">For example, GET.</span></span> |
| <span data-ttu-id="f2953-201">Chemin</span><span class="sxs-lookup"><span data-stu-id="f2953-201">Path</span></span> |<span data-ttu-id="f2953-202">Chaîne</span><span class="sxs-lookup"><span data-stu-id="f2953-202">String</span></span> |<span data-ttu-id="f2953-203">Le chemin d’accès vers l’emplacement où l’opération a eu lieu.</span><span class="sxs-lookup"><span data-stu-id="f2953-203">The path the operation was performed on</span></span> |
| <span data-ttu-id="f2953-204">RequestContentLength</span><span class="sxs-lookup"><span data-stu-id="f2953-204">RequestContentLength</span></span> |<span data-ttu-id="f2953-205">int</span><span class="sxs-lookup"><span data-stu-id="f2953-205">int</span></span> |<span data-ttu-id="f2953-206">La longueur du contenu de la demande HTTP.</span><span class="sxs-lookup"><span data-stu-id="f2953-206">The content length of the HTTP request</span></span> |
| <span data-ttu-id="f2953-207">ClientRequestId</span><span class="sxs-lookup"><span data-stu-id="f2953-207">ClientRequestId</span></span> |<span data-ttu-id="f2953-208">String</span><span class="sxs-lookup"><span data-stu-id="f2953-208">String</span></span> |<span data-ttu-id="f2953-209">L’identificateur qui identifie de façon unique cette demande.</span><span class="sxs-lookup"><span data-stu-id="f2953-209">The identifier that uniquely identifies this request</span></span> |
| <span data-ttu-id="f2953-210">StartTime</span><span class="sxs-lookup"><span data-stu-id="f2953-210">StartTime</span></span> |<span data-ttu-id="f2953-211">Chaîne</span><span class="sxs-lookup"><span data-stu-id="f2953-211">String</span></span> |<span data-ttu-id="f2953-212">L’heure à laquelle le serveur a reçu la demande.</span><span class="sxs-lookup"><span data-stu-id="f2953-212">The time at which the server received the request</span></span> |
| <span data-ttu-id="f2953-213">EndTime</span><span class="sxs-lookup"><span data-stu-id="f2953-213">EndTime</span></span> |<span data-ttu-id="f2953-214">Chaîne</span><span class="sxs-lookup"><span data-stu-id="f2953-214">String</span></span> |<span data-ttu-id="f2953-215">L’heure à laquelle le serveur a envoyé une réponse.</span><span class="sxs-lookup"><span data-stu-id="f2953-215">The time at which the server sent a response</span></span> |

### <a name="audit-logs"></a><span data-ttu-id="f2953-216">Journaux d’audit</span><span class="sxs-lookup"><span data-stu-id="f2953-216">Audit logs</span></span>

<span data-ttu-id="f2953-217">Voici un exemple d’entrée dans le journal d’audit au format JSON.</span><span class="sxs-lookup"><span data-stu-id="f2953-217">Here's a sample entry in the JSON-formatted audit log.</span></span> <span data-ttu-id="f2953-218">Chaque objet blob a un objet racine appelé **enregistrements** qui contient un tableau d’objets du journal.</span><span class="sxs-lookup"><span data-stu-id="f2953-218">Each blob has one root object called **records** that contains an array of log objects.</span></span>

    {
    "records":
      [        
        . . . .
        ,
        {
             "time": "2016-07-28T19:15:16.245Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/<data_lake_ANALYTICS_account_name>",
             "category": "Audit",
             "operationName": "JobSubmitted",
             "identity": "user@somewhere.com",
             "properties": {
                 "JobId":"D74B928F-5194-4E6C-971F-C27026C290E6",
                 "JobName": "New Job",
                 "JobRuntimeName": "default",
                 "SubmitTime": "7/28/2016 7:14:57 PM"
                 }
        }
        ,
        . . . .
      ]
    }

#### <a name="audit-log-schema"></a><span data-ttu-id="f2953-219">Schéma du journal d’audit</span><span class="sxs-lookup"><span data-stu-id="f2953-219">Audit log schema</span></span>

| <span data-ttu-id="f2953-220">Name</span><span class="sxs-lookup"><span data-stu-id="f2953-220">Name</span></span> | <span data-ttu-id="f2953-221">Type</span><span class="sxs-lookup"><span data-stu-id="f2953-221">Type</span></span> | <span data-ttu-id="f2953-222">Description</span><span class="sxs-lookup"><span data-stu-id="f2953-222">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f2953-223">time</span><span class="sxs-lookup"><span data-stu-id="f2953-223">time</span></span> |<span data-ttu-id="f2953-224">Chaîne</span><span class="sxs-lookup"><span data-stu-id="f2953-224">String</span></span> |<span data-ttu-id="f2953-225">L’horodatage (heure UTC) du journal.</span><span class="sxs-lookup"><span data-stu-id="f2953-225">The timestamp (in UTC) of the log</span></span> |
| <span data-ttu-id="f2953-226">resourceId</span><span class="sxs-lookup"><span data-stu-id="f2953-226">resourceId</span></span> |<span data-ttu-id="f2953-227">String</span><span class="sxs-lookup"><span data-stu-id="f2953-227">String</span></span> |<span data-ttu-id="f2953-228">L’identificateur de la ressource sur laquelle l’opération a eu lieu.</span><span class="sxs-lookup"><span data-stu-id="f2953-228">The identifier of the resource that operation took place on</span></span> |
| <span data-ttu-id="f2953-229">category</span><span class="sxs-lookup"><span data-stu-id="f2953-229">category</span></span> |<span data-ttu-id="f2953-230">Chaîne</span><span class="sxs-lookup"><span data-stu-id="f2953-230">String</span></span> |<span data-ttu-id="f2953-231">La catégorie du journal.</span><span class="sxs-lookup"><span data-stu-id="f2953-231">The log category.</span></span> <span data-ttu-id="f2953-232">Par exemple, **Audit**.</span><span class="sxs-lookup"><span data-stu-id="f2953-232">For example, **Audit**.</span></span> |
| <span data-ttu-id="f2953-233">operationName</span><span class="sxs-lookup"><span data-stu-id="f2953-233">operationName</span></span> |<span data-ttu-id="f2953-234">Chaîne</span><span class="sxs-lookup"><span data-stu-id="f2953-234">String</span></span> |<span data-ttu-id="f2953-235">Le nom de l’opération qui est journalisée.</span><span class="sxs-lookup"><span data-stu-id="f2953-235">Name of the operation that is logged.</span></span> <span data-ttu-id="f2953-236">Par exemple, JobSubmitted.</span><span class="sxs-lookup"><span data-stu-id="f2953-236">For example, JobSubmitted.</span></span> |
| <span data-ttu-id="f2953-237">resultType</span><span class="sxs-lookup"><span data-stu-id="f2953-237">resultType</span></span> |<span data-ttu-id="f2953-238">Chaîne</span><span class="sxs-lookup"><span data-stu-id="f2953-238">String</span></span> |<span data-ttu-id="f2953-239">Un sous-état de l’état de la tâche (operationName).</span><span class="sxs-lookup"><span data-stu-id="f2953-239">A substatus for the job status (operationName).</span></span> |
| <span data-ttu-id="f2953-240">resultSignature</span><span class="sxs-lookup"><span data-stu-id="f2953-240">resultSignature</span></span> |<span data-ttu-id="f2953-241">Chaîne</span><span class="sxs-lookup"><span data-stu-id="f2953-241">String</span></span> |<span data-ttu-id="f2953-242">Informations supplémentaires sur l’état de la tâche (operationName).</span><span class="sxs-lookup"><span data-stu-id="f2953-242">Additional details on the job status (operationName).</span></span> |
| <span data-ttu-id="f2953-243">identité</span><span class="sxs-lookup"><span data-stu-id="f2953-243">identity</span></span> |<span data-ttu-id="f2953-244">Chaîne</span><span class="sxs-lookup"><span data-stu-id="f2953-244">String</span></span> |<span data-ttu-id="f2953-245">L’utilisateur qui a demandé l’opération.</span><span class="sxs-lookup"><span data-stu-id="f2953-245">The user that requested the operation.</span></span> <span data-ttu-id="f2953-246">Par exemple, susan@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="f2953-246">For example, susan@contoso.com.</span></span> |
| <span data-ttu-id="f2953-247">properties</span><span class="sxs-lookup"><span data-stu-id="f2953-247">properties</span></span> |<span data-ttu-id="f2953-248">JSON</span><span class="sxs-lookup"><span data-stu-id="f2953-248">JSON</span></span> |<span data-ttu-id="f2953-249">Consultez la section suivante (Schéma des propriétés de journal d’audit) pour plus d’informations</span><span class="sxs-lookup"><span data-stu-id="f2953-249">See the next section (Audit log properties schema) for details</span></span> |

> [!NOTE]
> <span data-ttu-id="f2953-250">**resultType** et **resultSignature** fournissent des informations sur le résultat d’une opération et contiennent uniquement une valeur si une opération est terminée.</span><span class="sxs-lookup"><span data-stu-id="f2953-250">**resultType** and **resultSignature** provide information on the result of an operation, and only contain a value if an operation has completed.</span></span> <span data-ttu-id="f2953-251">Par exemple, ils contiennent uniquement une valeur quand **operationName** contient la valeur **JobStarted** ou **JobEnded**.</span><span class="sxs-lookup"><span data-stu-id="f2953-251">For example, they only contain a value when **operationName** contains a value of **JobStarted** or **JobEnded**.</span></span>
>
>

#### <a name="audit-log-properties-schema"></a><span data-ttu-id="f2953-252">Schéma des propriétés de journal d’audit</span><span class="sxs-lookup"><span data-stu-id="f2953-252">Audit log properties schema</span></span>

| <span data-ttu-id="f2953-253">Name</span><span class="sxs-lookup"><span data-stu-id="f2953-253">Name</span></span> | <span data-ttu-id="f2953-254">Type</span><span class="sxs-lookup"><span data-stu-id="f2953-254">Type</span></span> | <span data-ttu-id="f2953-255">Description</span><span class="sxs-lookup"><span data-stu-id="f2953-255">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f2953-256">JobId</span><span class="sxs-lookup"><span data-stu-id="f2953-256">JobId</span></span> |<span data-ttu-id="f2953-257">Chaîne</span><span class="sxs-lookup"><span data-stu-id="f2953-257">String</span></span> |<span data-ttu-id="f2953-258">L’ID affecté à la tâche.</span><span class="sxs-lookup"><span data-stu-id="f2953-258">The ID assigned to the job</span></span> |
| <span data-ttu-id="f2953-259">JobName</span><span class="sxs-lookup"><span data-stu-id="f2953-259">JobName</span></span> |<span data-ttu-id="f2953-260">Chaîne</span><span class="sxs-lookup"><span data-stu-id="f2953-260">String</span></span> |<span data-ttu-id="f2953-261">Le nom fourni pour la tâche.</span><span class="sxs-lookup"><span data-stu-id="f2953-261">The name that was provided for the job</span></span> |
| <span data-ttu-id="f2953-262">JobRunTime</span><span class="sxs-lookup"><span data-stu-id="f2953-262">JobRunTime</span></span> |<span data-ttu-id="f2953-263">Chaîne</span><span class="sxs-lookup"><span data-stu-id="f2953-263">String</span></span> |<span data-ttu-id="f2953-264">Le runtime utilisé pour traiter la tâche.</span><span class="sxs-lookup"><span data-stu-id="f2953-264">The runtime used to process the job</span></span> |
| <span data-ttu-id="f2953-265">SubmitTime</span><span class="sxs-lookup"><span data-stu-id="f2953-265">SubmitTime</span></span> |<span data-ttu-id="f2953-266">Chaîne</span><span class="sxs-lookup"><span data-stu-id="f2953-266">String</span></span> |<span data-ttu-id="f2953-267">L’heure (UTC) à laquelle la tâche a été envoyée.</span><span class="sxs-lookup"><span data-stu-id="f2953-267">The time (in UTC) that the job was submitted</span></span> |
| <span data-ttu-id="f2953-268">StartTime</span><span class="sxs-lookup"><span data-stu-id="f2953-268">StartTime</span></span> |<span data-ttu-id="f2953-269">String</span><span class="sxs-lookup"><span data-stu-id="f2953-269">String</span></span> |<span data-ttu-id="f2953-270">L’heure à laquelle l’exécution de la tâche a commencé après la soumission (UTC).</span><span class="sxs-lookup"><span data-stu-id="f2953-270">The time the job started running after submission (in UTC)</span></span> |
| <span data-ttu-id="f2953-271">EndTime</span><span class="sxs-lookup"><span data-stu-id="f2953-271">EndTime</span></span> |<span data-ttu-id="f2953-272">String</span><span class="sxs-lookup"><span data-stu-id="f2953-272">String</span></span> |<span data-ttu-id="f2953-273">L’heure à laquelle la tâche s’est terminée.</span><span class="sxs-lookup"><span data-stu-id="f2953-273">The time the job ended</span></span> |
| <span data-ttu-id="f2953-274">Parallélisme</span><span class="sxs-lookup"><span data-stu-id="f2953-274">Parallelism</span></span> |<span data-ttu-id="f2953-275">String</span><span class="sxs-lookup"><span data-stu-id="f2953-275">String</span></span> |<span data-ttu-id="f2953-276">Le nombre d’unités Data Lake Analytics demandées pour cette tâche pendant la soumission.</span><span class="sxs-lookup"><span data-stu-id="f2953-276">The number of Data Lake Analytics units requested for this job during submission</span></span> |

> [!NOTE]
> <span data-ttu-id="f2953-277">**SubmitTime**, **StartTime**, **EndTime** et **Parallélisme** fournissent des informations sur une opération.</span><span class="sxs-lookup"><span data-stu-id="f2953-277">**SubmitTime**, **StartTime**, **EndTime**, and **Parallelism** provide information on an operation.</span></span> <span data-ttu-id="f2953-278">Ces entrées ne contiennent une valeur que si cette opération a démarré ou est terminée.</span><span class="sxs-lookup"><span data-stu-id="f2953-278">These entries only contain a value if that operation has started or completed.</span></span> <span data-ttu-id="f2953-279">Par exemple, **SubmitTime** contient uniquement une valeur après que **operationName** a la valeur **JobSubmitted**.</span><span class="sxs-lookup"><span data-stu-id="f2953-279">For example, **SubmitTime** only contains a value after **operationName** has the value **JobSubmitted**.</span></span>

## <a name="process-the-log-data"></a><span data-ttu-id="f2953-280">Traiter les données de journal</span><span class="sxs-lookup"><span data-stu-id="f2953-280">Process the log data</span></span>

<span data-ttu-id="f2953-281">Azure Data Lake Analytics fournit un exemple de traitement et d’analyse des données de journal.</span><span class="sxs-lookup"><span data-stu-id="f2953-281">Azure Data Lake Analytics provides a sample on how to process and analyze the log data.</span></span> <span data-ttu-id="f2953-282">Vous trouverez l’exemple à l’adresse [https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample](https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample).</span><span class="sxs-lookup"><span data-stu-id="f2953-282">You can find the sample at [https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample](https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f2953-283">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f2953-283">Next steps</span></span>
* [<span data-ttu-id="f2953-284">Présentation d’Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="f2953-284">Overview of Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
