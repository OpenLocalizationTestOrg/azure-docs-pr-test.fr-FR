---
title: "journaux de diagnostic aaaViewing pour Analytique de LAC de données Azure | Documents Microsoft"
description: "Comprendre comment toosetup et diagnostic d’accès des journaux de données Azure analytique de LAC "
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
ms.openlocfilehash: 4cd1eb6f585c1ef96c358340232ef85721a972b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-diagnostic-logs-for-azure-data-lake-analytics"></a><span data-ttu-id="c6868-103">Accès aux journaux de diagnostic d’Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="c6868-103">Accessing diagnostic logs for Azure Data Lake Analytics</span></span>

<span data-ttu-id="c6868-104">Journalisation des diagnostics vous permet de pistes d’audit de toocollect données access.</span><span class="sxs-lookup"><span data-stu-id="c6868-104">Diagnostic logging allows you toocollect data access audit trails.</span></span> <span data-ttu-id="c6868-105">Ces journaux fournissent des informations comme :</span><span class="sxs-lookup"><span data-stu-id="c6868-105">These logs provide information such as:</span></span>

* <span data-ttu-id="c6868-106">Une liste d’utilisateurs qui ont accédé à des données de hello.</span><span class="sxs-lookup"><span data-stu-id="c6868-106">A list of users that accessed hello data.</span></span>
* <span data-ttu-id="c6868-107">La fréquence à laquelle les données de salutation sont accessible.</span><span class="sxs-lookup"><span data-stu-id="c6868-107">How frequently hello data is accessed.</span></span>
* <span data-ttu-id="c6868-108">La quantité de données est stockée dans le compte de hello.</span><span class="sxs-lookup"><span data-stu-id="c6868-108">How much data is stored in hello account.</span></span>

## <a name="enable-logging"></a><span data-ttu-id="c6868-109">Activation de la journalisation</span><span class="sxs-lookup"><span data-stu-id="c6868-109">Enable logging</span></span>

1. <span data-ttu-id="c6868-110">Ouverture de session toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c6868-110">Sign on toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="c6868-111">Ouvrez votre compte Analytique lac de données et sélectionnez **journaux de Diagnostic** de hello __moniteur__ section.</span><span class="sxs-lookup"><span data-stu-id="c6868-111">Open your Data Lake Analytics account and select **Diagnostic logs** from hello __Monitor__ section.</span></span> <span data-ttu-id="c6868-112">Ensuite, sélectionnez __Activer les diagnostics__.</span><span class="sxs-lookup"><span data-stu-id="c6868-112">Next, select __Turn on diagnostics__.</span></span>

    ![Activer les diagnostics toocollect audit et les journaux de demandes](./media/data-lake-analytics-diagnostic-logs/turn-on-logging.png)

3. <span data-ttu-id="c6868-114">À partir de __paramètres de diagnostic__, définir hello état too__On__ et sélectionnez les options de journalisation.</span><span class="sxs-lookup"><span data-stu-id="c6868-114">From __Diagnostics settings__, set hello status too__On__ and select logging options.</span></span>

    <span data-ttu-id="c6868-115">![Activer les diagnostics toocollect audit et les journaux de demandes](./media/data-lake-analytics-diagnostic-logs/enable-diagnostic-logs.png "activer les journaux de diagnostic")</span><span class="sxs-lookup"><span data-stu-id="c6868-115">![Turn on diagnostics toocollect audit and request logs](./media/data-lake-analytics-diagnostic-logs/enable-diagnostic-logs.png "Enable diagnostic logs")</span></span>

   * <span data-ttu-id="c6868-116">Définissez **état** trop**sur** tooenable journalisation des Diagnostics.</span><span class="sxs-lookup"><span data-stu-id="c6868-116">Set **Status** too**On** tooenable diagnostic logging.</span></span>

   * <span data-ttu-id="c6868-117">Vous pouvez choisir les données toostore/processus hello de trois façons différentes.</span><span class="sxs-lookup"><span data-stu-id="c6868-117">You can choose toostore/process hello data in three different ways.</span></span>

     * <span data-ttu-id="c6868-118">Sélectionnez __archiver le compte de stockage tooa__ toostore enregistre dans un compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="c6868-118">Select __Archive tooa storage account__ toostore logs in an Azure storage account.</span></span> <span data-ttu-id="c6868-119">Utilisez cette option si vous souhaitez que les données de salutation tooarchive.</span><span class="sxs-lookup"><span data-stu-id="c6868-119">Use this option if you want tooarchive hello data.</span></span> <span data-ttu-id="c6868-120">Si vous sélectionnez cette option, vous devez fournir un stockage Azure compte toosave hello se connecte à.</span><span class="sxs-lookup"><span data-stu-id="c6868-120">If you select this option, you must provide an Azure storage account toosave hello logs to.</span></span>

     * <span data-ttu-id="c6868-121">Sélectionnez **tooan concentrateur d’événements de flux** tooan de données de journal toostream concentrateur d’événements Azure.</span><span class="sxs-lookup"><span data-stu-id="c6868-121">Select **Stream tooan Event Hub** toostream log data tooan Azure Event Hub.</span></span> <span data-ttu-id="c6868-122">Utilisez cette option si vous disposez d’un pipeline de traitement en aval qui analyse les journaux entrants en temps réel.</span><span class="sxs-lookup"><span data-stu-id="c6868-122">Use this option if you have a downstream processing pipeline that is analyzing incoming logs in real time.</span></span> <span data-ttu-id="c6868-123">Si vous sélectionnez cette option, vous devez fournir les détails de hello pour hello concentrateur d’événements Azure vous souhaitez toouse.</span><span class="sxs-lookup"><span data-stu-id="c6868-123">If you select this option, you must provide hello details for hello Azure Event Hub you want toouse.</span></span>

     * <span data-ttu-id="c6868-124">Sélectionnez __envoyer tooLog Analytique__ toosend hello données toohello service d’Analytique de journal.</span><span class="sxs-lookup"><span data-stu-id="c6868-124">Select __Send tooLog Analytics__ toosend hello data toohello Log Analytics service.</span></span> <span data-ttu-id="c6868-125">Utilisez cette option si vous souhaitez toouse Analytique de journal toogather et analysez les journaux.</span><span class="sxs-lookup"><span data-stu-id="c6868-125">Use this option if you want toouse Log Analytics toogather and analyze logs.</span></span>
   * <span data-ttu-id="c6868-126">Spécifiez si vous souhaitez que les journaux d’audit de tooget ou les journaux des requêtes ou les deux.</span><span class="sxs-lookup"><span data-stu-id="c6868-126">Specify whether you want tooget audit logs or request logs or both.</span></span>  <span data-ttu-id="c6868-127">Un journal des requêtes capture chaque demande d’API.</span><span class="sxs-lookup"><span data-stu-id="c6868-127">A request log captures every API request.</span></span> <span data-ttu-id="c6868-128">Un journal d’audit enregistre toutes les opérations qui sont déclenchées par cette demande d’API.</span><span class="sxs-lookup"><span data-stu-id="c6868-128">An audit log records all operations that are triggered by that API request.</span></span>

   * <span data-ttu-id="c6868-129">Pour __archiver le compte de stockage tooa__, spécifiez nombre hello de données de hello tooretain jours.</span><span class="sxs-lookup"><span data-stu-id="c6868-129">For __Archive tooa storage account__, specify hello number of days tooretain hello data.</span></span>

   * <span data-ttu-id="c6868-130">Cliquez sur __Enregistrer__.</span><span class="sxs-lookup"><span data-stu-id="c6868-130">Click __Save__.</span></span>

        > [!NOTE]
        > <span data-ttu-id="c6868-131">Vous devez sélectionner __archiver le compte de stockage tooa__, __tooan concentrateur d’événements de flux__ ou __envoyer tooLog Analytique__ avant de cliquer sur hello __enregistrer__bouton.</span><span class="sxs-lookup"><span data-stu-id="c6868-131">You must select either __Archive tooa storage account__, __Stream tooan Event Hub__ or __Send tooLog Analytics__ before clicking hello __Save__ button.</span></span>

<span data-ttu-id="c6868-132">Une fois que vous avez activé les paramètres de diagnostic, vous pouvez retourner toohello __les journaux de diagnostic__ panneau tooview hello journaux.</span><span class="sxs-lookup"><span data-stu-id="c6868-132">Once you have enabled diagnostic settings, you can return toohello __Diagnostics logs__ blade tooview hello logs.</span></span>

## <a name="view-logs"></a><span data-ttu-id="c6868-133">Consulter les journaux</span><span class="sxs-lookup"><span data-stu-id="c6868-133">View logs</span></span>

### <a name="use-hello-data-lake-analytics-view"></a><span data-ttu-id="c6868-134">Utiliser le mode de données Lake Analytique hello</span><span class="sxs-lookup"><span data-stu-id="c6868-134">Use hello Data Lake Analytics view</span></span>

1. <span data-ttu-id="c6868-135">À partir de votre Analytique lac de données compte un panneau, sous **analyse**, sélectionnez **journaux de Diagnostic** et puis sélectionnez une entrée toodisplay ouvre une session.</span><span class="sxs-lookup"><span data-stu-id="c6868-135">From your Data Lake Analytics account blade, under **Monitoring**, select **Diagnostic Logs** and then select an entry toodisplay logs for.</span></span>

    <span data-ttu-id="c6868-136">![Afficher la journalisation des diagnostics](./media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs.png "Afficher les journaux de diagnostic")</span><span class="sxs-lookup"><span data-stu-id="c6868-136">![View diagnostic logging](./media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs.png "View diagnostic logs")</span></span>

2. <span data-ttu-id="c6868-137">journaux Hello sont classés par **les journaux d’Audit** et **les journaux de demandes**.</span><span class="sxs-lookup"><span data-stu-id="c6868-137">hello logs are categorized by **Audit Logs** and **Request Logs**.</span></span>

    ![entrées de journal](./media/data-lake-analytics-diagnostic-logs/diagnostic-log-entries.png)

   * <span data-ttu-id="c6868-139">Les journaux de demandes de capture chaque demande d’API sur hello compte d’Analytique lac de données.</span><span class="sxs-lookup"><span data-stu-id="c6868-139">Request logs capture every API request made on hello Data Lake Analytics account.</span></span>
   * <span data-ttu-id="c6868-140">Journaux d’audit sont les journaux toorequest similaire, mais fournissent une analyse beaucoup plus détaillée des opérations de hello.</span><span class="sxs-lookup"><span data-stu-id="c6868-140">Audit Logs are similar toorequest Logs but provide a much more detailed breakdown of hello operations.</span></span> <span data-ttu-id="c6868-141">Par exemple, un simple appel d’API de chargement dans un journal de demande peut entraîner plusieurs opérations « Ajouter » dans son journal d’audit.</span><span class="sxs-lookup"><span data-stu-id="c6868-141">For example, a single upload API call in a request log can result in multiple "Append" operations in its audit log.</span></span>

3. <span data-ttu-id="c6868-142">Cliquez sur hello **télécharger** lien pour une toodownload d’entrée de journal du journal.</span><span class="sxs-lookup"><span data-stu-id="c6868-142">Click hello **Download** link for a log entry toodownload that log.</span></span>

### <a name="use-hello-azure-storage-account-that-contains-log-data"></a><span data-ttu-id="c6868-143">Utiliser le compte de stockage Azure hello qui contient les données du journal</span><span class="sxs-lookup"><span data-stu-id="c6868-143">Use hello Azure Storage account that contains log data</span></span>

1. <span data-ttu-id="c6868-144">Ouvrir le panneau de compte de stockage Azure hello associé Analytique lac de données pour la journalisation, puis cliquez sur __BLOB__.</span><span class="sxs-lookup"><span data-stu-id="c6868-144">Open hello Azure Storage account blade associated with Data Lake Analytics for logging, and then click __Blobs__.</span></span> <span data-ttu-id="c6868-145">Hello **service Blob** panneau répertorie deux conteneurs.</span><span class="sxs-lookup"><span data-stu-id="c6868-145">hello **Blob service** blade lists two containers.</span></span>

    <span data-ttu-id="c6868-146">![Afficher la journalisation des diagnostics](./media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs-storage-account.png "Afficher les journaux de diagnostic")</span><span class="sxs-lookup"><span data-stu-id="c6868-146">![View diagnostic logging](./media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs-storage-account.png "View diagnostic logs")</span></span>

   * <span data-ttu-id="c6868-147">conteneur de Hello **insights-journaux-audit** contient les journaux d’audit de hello.</span><span class="sxs-lookup"><span data-stu-id="c6868-147">hello container **insights-logs-audit** contains hello audit logs.</span></span>
   * <span data-ttu-id="c6868-148">conteneur de Hello **demandes de journaux insights** contient les journaux de demandes hello.</span><span class="sxs-lookup"><span data-stu-id="c6868-148">hello container **insights-logs-requests** contains hello request logs.</span></span>
2. <span data-ttu-id="c6868-149">Ces conteneurs, hello journaux sont stockés sous hello suivant structure :</span><span class="sxs-lookup"><span data-stu-id="c6868-149">Within these containers, hello logs are stored under hello following structure:</span></span>

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
   > <span data-ttu-id="c6868-150">Hello `##` contiennent des entrées dans le chemin d’accès hello hello year, month, day et les heures dans le hello journal a été créé.</span><span class="sxs-lookup"><span data-stu-id="c6868-150">hello `##` entries in hello path contain hello year, month, day, and hour in which hello log was created.</span></span> <span data-ttu-id="c6868-151">Data Lake Analytics crée un fichier toutes les heures, par conséquent, `m=` contient toujours une valeur de `00`.</span><span class="sxs-lookup"><span data-stu-id="c6868-151">Data Lake Analytics creates one file every hour, so `m=` always contains a value of `00`.</span></span>

    <span data-ttu-id="c6868-152">Par exemple, le chemin d’accès complet de hello tooan log peut être :</span><span class="sxs-lookup"><span data-stu-id="c6868-152">As an example, hello complete path tooan audit log could be:</span></span>

        https://adllogs.blob.core.windows.net/insights-logs-audit/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/mydatalakeanalytics/y=2016/m=07/d=18/h=04/m=00/PT1H.json

    <span data-ttu-id="c6868-153">De même, le journal des demandes tooa hello chemin d’accès complet peut être :</span><span class="sxs-lookup"><span data-stu-id="c6868-153">Similarly, hello complete path tooa request log could be:</span></span>

        https://adllogs.blob.core.windows.net/insights-logs-requests/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/mydatalakeanalytics/y=2016/m=07/d=18/h=14/m=00/PT1H.json

## <a name="log-structure"></a><span data-ttu-id="c6868-154">Structure journal</span><span class="sxs-lookup"><span data-stu-id="c6868-154">Log structure</span></span>

<span data-ttu-id="c6868-155">Hello journaux d’audit et de la demande sont dans un format JSON structuré.</span><span class="sxs-lookup"><span data-stu-id="c6868-155">hello audit and request logs are in a structured JSON format.</span></span>

### <a name="request-logs"></a><span data-ttu-id="c6868-156">journaux de demande</span><span class="sxs-lookup"><span data-stu-id="c6868-156">Request logs</span></span>

<span data-ttu-id="c6868-157">Voici un exemple d’entrée dans le journal au format JSON de demande de hello.</span><span class="sxs-lookup"><span data-stu-id="c6868-157">Here's a sample entry in hello JSON-formatted request log.</span></span> <span data-ttu-id="c6868-158">Chaque objet blob a un objet racine appelé **enregistrements** qui contient un tableau d’objets du journal.</span><span class="sxs-lookup"><span data-stu-id="c6868-158">Each blob has one root object called **records** that contains an array of log objects.</span></span>

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

#### <a name="request-log-schema"></a><span data-ttu-id="c6868-159">Schéma du journal de requête</span><span class="sxs-lookup"><span data-stu-id="c6868-159">Request log schema</span></span>

| <span data-ttu-id="c6868-160">Name</span><span class="sxs-lookup"><span data-stu-id="c6868-160">Name</span></span> | <span data-ttu-id="c6868-161">Type</span><span class="sxs-lookup"><span data-stu-id="c6868-161">Type</span></span> | <span data-ttu-id="c6868-162">Description</span><span class="sxs-lookup"><span data-stu-id="c6868-162">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c6868-163">time</span><span class="sxs-lookup"><span data-stu-id="c6868-163">time</span></span> |<span data-ttu-id="c6868-164">String</span><span class="sxs-lookup"><span data-stu-id="c6868-164">String</span></span> |<span data-ttu-id="c6868-165">Hello horodateur (UTC) du journal de hello</span><span class="sxs-lookup"><span data-stu-id="c6868-165">hello timestamp (in UTC) of hello log</span></span> |
| <span data-ttu-id="c6868-166">resourceId</span><span class="sxs-lookup"><span data-stu-id="c6868-166">resourceId</span></span> |<span data-ttu-id="c6868-167">String</span><span class="sxs-lookup"><span data-stu-id="c6868-167">String</span></span> |<span data-ttu-id="c6868-168">Identificateur Hello de ressource de hello opération placer sur</span><span class="sxs-lookup"><span data-stu-id="c6868-168">hello identifier of hello resource that operation took place on</span></span> |
| <span data-ttu-id="c6868-169">category</span><span class="sxs-lookup"><span data-stu-id="c6868-169">category</span></span> |<span data-ttu-id="c6868-170">String</span><span class="sxs-lookup"><span data-stu-id="c6868-170">String</span></span> |<span data-ttu-id="c6868-171">catégorie de journal Hello.</span><span class="sxs-lookup"><span data-stu-id="c6868-171">hello log category.</span></span> <span data-ttu-id="c6868-172">Par exemple, **Demandes**.</span><span class="sxs-lookup"><span data-stu-id="c6868-172">For example, **Requests**.</span></span> |
| <span data-ttu-id="c6868-173">operationName</span><span class="sxs-lookup"><span data-stu-id="c6868-173">operationName</span></span> |<span data-ttu-id="c6868-174">String</span><span class="sxs-lookup"><span data-stu-id="c6868-174">String</span></span> |<span data-ttu-id="c6868-175">Nom de l’opération hello est connectée.</span><span class="sxs-lookup"><span data-stu-id="c6868-175">Name of hello operation that is logged.</span></span> <span data-ttu-id="c6868-176">Par exemple, GetAggregatedJobHistory.</span><span class="sxs-lookup"><span data-stu-id="c6868-176">For example, GetAggregatedJobHistory.</span></span> |
| <span data-ttu-id="c6868-177">resultType</span><span class="sxs-lookup"><span data-stu-id="c6868-177">resultType</span></span> |<span data-ttu-id="c6868-178">String</span><span class="sxs-lookup"><span data-stu-id="c6868-178">String</span></span> |<span data-ttu-id="c6868-179">état Hello d’opération hello, par exemple, 200.</span><span class="sxs-lookup"><span data-stu-id="c6868-179">hello status of hello operation, For example, 200.</span></span> |
| <span data-ttu-id="c6868-180">callerIpAddress</span><span class="sxs-lookup"><span data-stu-id="c6868-180">callerIpAddress</span></span> |<span data-ttu-id="c6868-181">String</span><span class="sxs-lookup"><span data-stu-id="c6868-181">String</span></span> |<span data-ttu-id="c6868-182">adresse IP de Hello du client hello hello demande</span><span class="sxs-lookup"><span data-stu-id="c6868-182">hello IP address of hello client making hello request</span></span> |
| <span data-ttu-id="c6868-183">correlationId</span><span class="sxs-lookup"><span data-stu-id="c6868-183">correlationId</span></span> |<span data-ttu-id="c6868-184">String</span><span class="sxs-lookup"><span data-stu-id="c6868-184">String</span></span> |<span data-ttu-id="c6868-185">Identificateur Hello du journal de hello.</span><span class="sxs-lookup"><span data-stu-id="c6868-185">hello identifier of hello log.</span></span> <span data-ttu-id="c6868-186">Cette valeur peut être utilisé toogroup un ensemble d’entrées de journal connexes.</span><span class="sxs-lookup"><span data-stu-id="c6868-186">This value can be used toogroup a set of related log entries.</span></span> |
| <span data-ttu-id="c6868-187">identité</span><span class="sxs-lookup"><span data-stu-id="c6868-187">identity</span></span> |<span data-ttu-id="c6868-188">Object</span><span class="sxs-lookup"><span data-stu-id="c6868-188">Object</span></span> |<span data-ttu-id="c6868-189">identité Hello qui a généré hello journal</span><span class="sxs-lookup"><span data-stu-id="c6868-189">hello identity that generated hello log</span></span> |
| <span data-ttu-id="c6868-190">properties</span><span class="sxs-lookup"><span data-stu-id="c6868-190">properties</span></span> |<span data-ttu-id="c6868-191">JSON</span><span class="sxs-lookup"><span data-stu-id="c6868-191">JSON</span></span> |<span data-ttu-id="c6868-192">Voir section suivante hello (schéma de propriétés d’un journal de demande) pour plus d’informations</span><span class="sxs-lookup"><span data-stu-id="c6868-192">See hello next section (Request log properties schema) for details</span></span> |

#### <a name="request-log-properties-schema"></a><span data-ttu-id="c6868-193">Schéma des propriétés de journal de demande</span><span class="sxs-lookup"><span data-stu-id="c6868-193">Request log properties schema</span></span>

| <span data-ttu-id="c6868-194">Name</span><span class="sxs-lookup"><span data-stu-id="c6868-194">Name</span></span> | <span data-ttu-id="c6868-195">Type</span><span class="sxs-lookup"><span data-stu-id="c6868-195">Type</span></span> | <span data-ttu-id="c6868-196">Description</span><span class="sxs-lookup"><span data-stu-id="c6868-196">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c6868-197">HttpMethod</span><span class="sxs-lookup"><span data-stu-id="c6868-197">HttpMethod</span></span> |<span data-ttu-id="c6868-198">String</span><span class="sxs-lookup"><span data-stu-id="c6868-198">String</span></span> |<span data-ttu-id="c6868-199">Hello méthode HTTP utilisée pour l’opération de hello.</span><span class="sxs-lookup"><span data-stu-id="c6868-199">hello HTTP Method used for hello operation.</span></span> <span data-ttu-id="c6868-200">Par exemple, GET.</span><span class="sxs-lookup"><span data-stu-id="c6868-200">For example, GET.</span></span> |
| <span data-ttu-id="c6868-201">Chemin</span><span class="sxs-lookup"><span data-stu-id="c6868-201">Path</span></span> |<span data-ttu-id="c6868-202">String</span><span class="sxs-lookup"><span data-stu-id="c6868-202">String</span></span> |<span data-ttu-id="c6868-203">opération hello Hello a été effectuée sur</span><span class="sxs-lookup"><span data-stu-id="c6868-203">hello path hello operation was performed on</span></span> |
| <span data-ttu-id="c6868-204">RequestContentLength</span><span class="sxs-lookup"><span data-stu-id="c6868-204">RequestContentLength</span></span> |<span data-ttu-id="c6868-205">int</span><span class="sxs-lookup"><span data-stu-id="c6868-205">int</span></span> |<span data-ttu-id="c6868-206">longueur du contenu de la demande de hello HTTP Hello</span><span class="sxs-lookup"><span data-stu-id="c6868-206">hello content length of hello HTTP request</span></span> |
| <span data-ttu-id="c6868-207">ClientRequestId</span><span class="sxs-lookup"><span data-stu-id="c6868-207">ClientRequestId</span></span> |<span data-ttu-id="c6868-208">String</span><span class="sxs-lookup"><span data-stu-id="c6868-208">String</span></span> |<span data-ttu-id="c6868-209">Identificateur Hello qui identifie de façon unique cette demande</span><span class="sxs-lookup"><span data-stu-id="c6868-209">hello identifier that uniquely identifies this request</span></span> |
| <span data-ttu-id="c6868-210">StartTime</span><span class="sxs-lookup"><span data-stu-id="c6868-210">StartTime</span></span> |<span data-ttu-id="c6868-211">String</span><span class="sxs-lookup"><span data-stu-id="c6868-211">String</span></span> |<span data-ttu-id="c6868-212">heure Hello qui demande hello du serveur reçues hello</span><span class="sxs-lookup"><span data-stu-id="c6868-212">hello time at which hello server received hello request</span></span> |
| <span data-ttu-id="c6868-213">EndTime</span><span class="sxs-lookup"><span data-stu-id="c6868-213">EndTime</span></span> |<span data-ttu-id="c6868-214">String</span><span class="sxs-lookup"><span data-stu-id="c6868-214">String</span></span> |<span data-ttu-id="c6868-215">temps de Hello à quels hello serveur a envoyé une réponse</span><span class="sxs-lookup"><span data-stu-id="c6868-215">hello time at which hello server sent a response</span></span> |

### <a name="audit-logs"></a><span data-ttu-id="c6868-216">Journaux d’audit</span><span class="sxs-lookup"><span data-stu-id="c6868-216">Audit logs</span></span>

<span data-ttu-id="c6868-217">Voici un exemple d’entrée dans le journal d’audit d’au format JSON hello.</span><span class="sxs-lookup"><span data-stu-id="c6868-217">Here's a sample entry in hello JSON-formatted audit log.</span></span> <span data-ttu-id="c6868-218">Chaque objet blob a un objet racine appelé **enregistrements** qui contient un tableau d’objets du journal.</span><span class="sxs-lookup"><span data-stu-id="c6868-218">Each blob has one root object called **records** that contains an array of log objects.</span></span>

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

#### <a name="audit-log-schema"></a><span data-ttu-id="c6868-219">Schéma du journal d’audit</span><span class="sxs-lookup"><span data-stu-id="c6868-219">Audit log schema</span></span>

| <span data-ttu-id="c6868-220">Name</span><span class="sxs-lookup"><span data-stu-id="c6868-220">Name</span></span> | <span data-ttu-id="c6868-221">Type</span><span class="sxs-lookup"><span data-stu-id="c6868-221">Type</span></span> | <span data-ttu-id="c6868-222">Description</span><span class="sxs-lookup"><span data-stu-id="c6868-222">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c6868-223">time</span><span class="sxs-lookup"><span data-stu-id="c6868-223">time</span></span> |<span data-ttu-id="c6868-224">String</span><span class="sxs-lookup"><span data-stu-id="c6868-224">String</span></span> |<span data-ttu-id="c6868-225">Hello horodateur (UTC) du journal de hello</span><span class="sxs-lookup"><span data-stu-id="c6868-225">hello timestamp (in UTC) of hello log</span></span> |
| <span data-ttu-id="c6868-226">resourceId</span><span class="sxs-lookup"><span data-stu-id="c6868-226">resourceId</span></span> |<span data-ttu-id="c6868-227">String</span><span class="sxs-lookup"><span data-stu-id="c6868-227">String</span></span> |<span data-ttu-id="c6868-228">Identificateur Hello de ressource de hello opération placer sur</span><span class="sxs-lookup"><span data-stu-id="c6868-228">hello identifier of hello resource that operation took place on</span></span> |
| <span data-ttu-id="c6868-229">category</span><span class="sxs-lookup"><span data-stu-id="c6868-229">category</span></span> |<span data-ttu-id="c6868-230">String</span><span class="sxs-lookup"><span data-stu-id="c6868-230">String</span></span> |<span data-ttu-id="c6868-231">catégorie de journal Hello.</span><span class="sxs-lookup"><span data-stu-id="c6868-231">hello log category.</span></span> <span data-ttu-id="c6868-232">Par exemple, **Audit**.</span><span class="sxs-lookup"><span data-stu-id="c6868-232">For example, **Audit**.</span></span> |
| <span data-ttu-id="c6868-233">operationName</span><span class="sxs-lookup"><span data-stu-id="c6868-233">operationName</span></span> |<span data-ttu-id="c6868-234">String</span><span class="sxs-lookup"><span data-stu-id="c6868-234">String</span></span> |<span data-ttu-id="c6868-235">Nom de l’opération hello est connectée.</span><span class="sxs-lookup"><span data-stu-id="c6868-235">Name of hello operation that is logged.</span></span> <span data-ttu-id="c6868-236">Par exemple, JobSubmitted.</span><span class="sxs-lookup"><span data-stu-id="c6868-236">For example, JobSubmitted.</span></span> |
| <span data-ttu-id="c6868-237">resultType</span><span class="sxs-lookup"><span data-stu-id="c6868-237">resultType</span></span> |<span data-ttu-id="c6868-238">String</span><span class="sxs-lookup"><span data-stu-id="c6868-238">String</span></span> |<span data-ttu-id="c6868-239">Un sous-état pour l’état de la tâche hello (NomOpération).</span><span class="sxs-lookup"><span data-stu-id="c6868-239">A substatus for hello job status (operationName).</span></span> |
| <span data-ttu-id="c6868-240">resultSignature</span><span class="sxs-lookup"><span data-stu-id="c6868-240">resultSignature</span></span> |<span data-ttu-id="c6868-241">String</span><span class="sxs-lookup"><span data-stu-id="c6868-241">String</span></span> |<span data-ttu-id="c6868-242">Plus d’informations sur l’état du travail hello (NomOpération).</span><span class="sxs-lookup"><span data-stu-id="c6868-242">Additional details on hello job status (operationName).</span></span> |
| <span data-ttu-id="c6868-243">identité</span><span class="sxs-lookup"><span data-stu-id="c6868-243">identity</span></span> |<span data-ttu-id="c6868-244">String</span><span class="sxs-lookup"><span data-stu-id="c6868-244">String</span></span> |<span data-ttu-id="c6868-245">utilisateur Hello hello l’opération demandée.</span><span class="sxs-lookup"><span data-stu-id="c6868-245">hello user that requested hello operation.</span></span> <span data-ttu-id="c6868-246">Par exemple, susan@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="c6868-246">For example, susan@contoso.com.</span></span> |
| <span data-ttu-id="c6868-247">properties</span><span class="sxs-lookup"><span data-stu-id="c6868-247">properties</span></span> |<span data-ttu-id="c6868-248">JSON</span><span class="sxs-lookup"><span data-stu-id="c6868-248">JSON</span></span> |<span data-ttu-id="c6868-249">Voir section suivante hello (schéma des propriétés du journal d’Audit) pour plus d’informations</span><span class="sxs-lookup"><span data-stu-id="c6868-249">See hello next section (Audit log properties schema) for details</span></span> |

> [!NOTE]
> <span data-ttu-id="c6868-250">**resultType** et **resultSignature** fournissent des informations sur le résultat de hello d’une opération et contenir uniquement une valeur si une opération est terminée.</span><span class="sxs-lookup"><span data-stu-id="c6868-250">**resultType** and **resultSignature** provide information on hello result of an operation, and only contain a value if an operation has completed.</span></span> <span data-ttu-id="c6868-251">Par exemple, ils contiennent uniquement une valeur quand **operationName** contient la valeur **JobStarted** ou **JobEnded**.</span><span class="sxs-lookup"><span data-stu-id="c6868-251">For example, they only contain a value when **operationName** contains a value of **JobStarted** or **JobEnded**.</span></span>
>
>

#### <a name="audit-log-properties-schema"></a><span data-ttu-id="c6868-252">Schéma des propriétés de journal d’audit</span><span class="sxs-lookup"><span data-stu-id="c6868-252">Audit log properties schema</span></span>

| <span data-ttu-id="c6868-253">Name</span><span class="sxs-lookup"><span data-stu-id="c6868-253">Name</span></span> | <span data-ttu-id="c6868-254">Type</span><span class="sxs-lookup"><span data-stu-id="c6868-254">Type</span></span> | <span data-ttu-id="c6868-255">Description</span><span class="sxs-lookup"><span data-stu-id="c6868-255">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c6868-256">JobId</span><span class="sxs-lookup"><span data-stu-id="c6868-256">JobId</span></span> |<span data-ttu-id="c6868-257">String</span><span class="sxs-lookup"><span data-stu-id="c6868-257">String</span></span> |<span data-ttu-id="c6868-258">travail de Hello ID toohello attribué</span><span class="sxs-lookup"><span data-stu-id="c6868-258">hello ID assigned toohello job</span></span> |
| <span data-ttu-id="c6868-259">JobName</span><span class="sxs-lookup"><span data-stu-id="c6868-259">JobName</span></span> |<span data-ttu-id="c6868-260">String</span><span class="sxs-lookup"><span data-stu-id="c6868-260">String</span></span> |<span data-ttu-id="c6868-261">nom Hello qui a été fournie pour le travail de hello</span><span class="sxs-lookup"><span data-stu-id="c6868-261">hello name that was provided for hello job</span></span> |
| <span data-ttu-id="c6868-262">JobRunTime</span><span class="sxs-lookup"><span data-stu-id="c6868-262">JobRunTime</span></span> |<span data-ttu-id="c6868-263">String</span><span class="sxs-lookup"><span data-stu-id="c6868-263">String</span></span> |<span data-ttu-id="c6868-264">Hello runtime utilisé la tâche de hello tooprocess</span><span class="sxs-lookup"><span data-stu-id="c6868-264">hello runtime used tooprocess hello job</span></span> |
| <span data-ttu-id="c6868-265">SubmitTime</span><span class="sxs-lookup"><span data-stu-id="c6868-265">SubmitTime</span></span> |<span data-ttu-id="c6868-266">String</span><span class="sxs-lookup"><span data-stu-id="c6868-266">String</span></span> |<span data-ttu-id="c6868-267">temps de Hello (au format UTC) que le travail hello a été soumis</span><span class="sxs-lookup"><span data-stu-id="c6868-267">hello time (in UTC) that hello job was submitted</span></span> |
| <span data-ttu-id="c6868-268">StartTime</span><span class="sxs-lookup"><span data-stu-id="c6868-268">StartTime</span></span> |<span data-ttu-id="c6868-269">String</span><span class="sxs-lookup"><span data-stu-id="c6868-269">String</span></span> |<span data-ttu-id="c6868-270">Hello temps hello tâche de démarrage en cours d’exécution après l’envoi (au format UTC)</span><span class="sxs-lookup"><span data-stu-id="c6868-270">hello time hello job started running after submission (in UTC)</span></span> |
| <span data-ttu-id="c6868-271">EndTime</span><span class="sxs-lookup"><span data-stu-id="c6868-271">EndTime</span></span> |<span data-ttu-id="c6868-272">String</span><span class="sxs-lookup"><span data-stu-id="c6868-272">String</span></span> |<span data-ttu-id="c6868-273">Hello temps hello tâche s’est terminée</span><span class="sxs-lookup"><span data-stu-id="c6868-273">hello time hello job ended</span></span> |
| <span data-ttu-id="c6868-274">Parallélisme</span><span class="sxs-lookup"><span data-stu-id="c6868-274">Parallelism</span></span> |<span data-ttu-id="c6868-275">String</span><span class="sxs-lookup"><span data-stu-id="c6868-275">String</span></span> |<span data-ttu-id="c6868-276">nombre de Hello d’unités Analytique lac de données demandé pour ce travail lors de l’envoi</span><span class="sxs-lookup"><span data-stu-id="c6868-276">hello number of Data Lake Analytics units requested for this job during submission</span></span> |

> [!NOTE]
> <span data-ttu-id="c6868-277">**SubmitTime**, **StartTime**, **EndTime** et **Parallélisme** fournissent des informations sur une opération.</span><span class="sxs-lookup"><span data-stu-id="c6868-277">**SubmitTime**, **StartTime**, **EndTime**, and **Parallelism** provide information on an operation.</span></span> <span data-ttu-id="c6868-278">Ces entrées ne contiennent une valeur que si cette opération a démarré ou est terminée.</span><span class="sxs-lookup"><span data-stu-id="c6868-278">These entries only contain a value if that operation has started or completed.</span></span> <span data-ttu-id="c6868-279">Par exemple, **SubmitTime** contient uniquement une valeur après **NomOpération** a la valeur de hello **JobSubmitted**.</span><span class="sxs-lookup"><span data-stu-id="c6868-279">For example, **SubmitTime** only contains a value after **operationName** has hello value **JobSubmitted**.</span></span>

## <a name="process-hello-log-data"></a><span data-ttu-id="c6868-280">Données de journal hello de processus</span><span class="sxs-lookup"><span data-stu-id="c6868-280">Process hello log data</span></span>

<span data-ttu-id="c6868-281">Analytique de LAC de données Azure fournit un exemple sur la façon de tooprocess et analyser les données de journal hello.</span><span class="sxs-lookup"><span data-stu-id="c6868-281">Azure Data Lake Analytics provides a sample on how tooprocess and analyze hello log data.</span></span> <span data-ttu-id="c6868-282">Vous trouverez un exemple hello à [https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample](https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample).</span><span class="sxs-lookup"><span data-stu-id="c6868-282">You can find hello sample at [https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample](https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c6868-283">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c6868-283">Next steps</span></span>
* [<span data-ttu-id="c6868-284">Présentation d’Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="c6868-284">Overview of Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
