---
title: "Affichage des journaux de diagnostic d’Azure Data Lake Store | Microsoft Docs"
description: "Comprendre comment configurer les journaux de diagnostic et y accéder pour Azure Data Lake Store  "
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: f6e75eb1-d0ae-47cf-bdb8-06684b7c0a94
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: b7a38ec445ef0ce13f3f1931e8ee246dce6412a5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="accessing-diagnostic-logs-for-azure-data-lake-store"></a><span data-ttu-id="b90ca-103">Accès aux journaux de diagnostic d’Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="b90ca-103">Accessing diagnostic logs for Azure Data Lake Store</span></span>
<span data-ttu-id="b90ca-104">Découvrez comment activer la journalisation de diagnostic pour votre compte Data Lake Store et comment afficher les journaux collectés pour votre compte.</span><span class="sxs-lookup"><span data-stu-id="b90ca-104">Learn about how to enable diagnostic logging for your Data Lake Store account and how to view the logs collected for your account.</span></span>

<span data-ttu-id="b90ca-105">Les organisations peuvent activer la journalisation de diagnostic pour leur compte Azure Data Lake Store afin de collecter des pistes d’audit d’accès aux données qui fournissent des informations telles que la liste des utilisateurs qui accèdent aux données, la fréquence à laquelle les données sont consultées, la quantité de données stockée sur le compte, etc.</span><span class="sxs-lookup"><span data-stu-id="b90ca-105">Organizations can enable diagnostic logging for their Azure Data Lake Store account to collect data access audit trails that provides information such as list of users accessing the data, how frequently the data is accessed, how much data is stored in the account, etc.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b90ca-106">Composants requis</span><span class="sxs-lookup"><span data-stu-id="b90ca-106">Prerequisites</span></span>
* <span data-ttu-id="b90ca-107">**Un abonnement Azure**.</span><span class="sxs-lookup"><span data-stu-id="b90ca-107">**An Azure subscription**.</span></span> <span data-ttu-id="b90ca-108">Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b90ca-108">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="b90ca-109">**Compte Azure Data Lake Store**.</span><span class="sxs-lookup"><span data-stu-id="b90ca-109">**Azure Data Lake Store account**.</span></span> <span data-ttu-id="b90ca-110">Suivez les instructions de [Prise en main d'Azure Data Lake Store avec le portail Azure](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b90ca-110">Follow the instructions at [Get started with Azure Data Lake Store using the Azure Portal](data-lake-store-get-started-portal.md).</span></span>

## <a name="enable-diagnostic-logging-for-your-data-lake-store-account"></a><span data-ttu-id="b90ca-111">Activer la journalisation de diagnostic pour votre compte Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="b90ca-111">Enable diagnostic logging for your Data Lake Store account</span></span>
1. <span data-ttu-id="b90ca-112">Inscrivez-vous au nouveau [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b90ca-112">Sign on to the new [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b90ca-113">Ouvrez votre compte Data Lake Store et, dans le panneau de votre compte Data Lake Store, cliquez sur **Paramètres** puis sur **Paramètres de diagnostic**.</span><span class="sxs-lookup"><span data-stu-id="b90ca-113">Open your Data Lake Store account, and from your Data Lake Store account blade, click **Settings**, and then click **Diagnostic logs**.</span></span>
3. <span data-ttu-id="b90ca-114">Dans le panneau **Journaux de diagnostic**, cliquez sur **Activer les diagnostics**.</span><span class="sxs-lookup"><span data-stu-id="b90ca-114">In the **Diagnostics logs** blade, click **Turn on diagnostics**.</span></span>

    <span data-ttu-id="b90ca-115">![Activer la journalisation des diagnostics](./media/data-lake-store-diagnostic-logs/turn-on-diagnostics.png "Activer les journaux de diagnostic")</span><span class="sxs-lookup"><span data-stu-id="b90ca-115">![Enable diagnostic logging](./media/data-lake-store-diagnostic-logs/turn-on-diagnostics.png "Enable diagnostic logs")</span></span>

3. <span data-ttu-id="b90ca-116">Dans le panneau **Diagnostic** , apportez les modifications suivantes pour configurer la journalisation de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="b90ca-116">In the **Diagnostic** blade, make the following changes to configure diagnostic logging.</span></span>
   
    <span data-ttu-id="b90ca-117">![Activer la journalisation des diagnostics](./media/data-lake-store-diagnostic-logs/enable-diagnostic-logs.png "Activer les journaux de diagnostic")</span><span class="sxs-lookup"><span data-stu-id="b90ca-117">![Enable diagnostic logging](./media/data-lake-store-diagnostic-logs/enable-diagnostic-logs.png "Enable diagnostic logs")</span></span>
   
   * <span data-ttu-id="b90ca-118">Définissez **État** sur **Activé** pour activer la journalisation de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="b90ca-118">Set **Status** to **On** to enable diagnostic logging.</span></span>
   * <span data-ttu-id="b90ca-119">Vous pouvez choisir de stocker/traiter les données de manières différentes.</span><span class="sxs-lookup"><span data-stu-id="b90ca-119">You can choose to store/process the data in different ways.</span></span>
     
        * <span data-ttu-id="b90ca-120">Sélectionnez l’option **Archive to a storage account (Archiver dans un compte de stockage)** pour stocker les journaux dans un compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="b90ca-120">Select the option to **Archive to a storage account** to store logs to an Azure Storage account.</span></span> <span data-ttu-id="b90ca-121">Utilisez cette option si vous souhaitez archiver les données qui seront traitées par lots à une date ultérieure.</span><span class="sxs-lookup"><span data-stu-id="b90ca-121">You use this option if you want to archive the data that will be batch-processed at a later date.</span></span> <span data-ttu-id="b90ca-122">Si vous sélectionnez cette option, vous devez fournir un compte de stockage Azure sur lequel enregistrer les journaux.</span><span class="sxs-lookup"><span data-stu-id="b90ca-122">If you select this option you must provide an Azure Storage account to save the logs to.</span></span>
        
        * <span data-ttu-id="b90ca-123">Sélectionnez l’option **Stream to an event hub (Transmettre à un Event Hub)** pour transmettre les données journalisées à un Event Hub Azure.</span><span class="sxs-lookup"><span data-stu-id="b90ca-123">Select the option to **Stream to an event hub** to stream log data to an Azure Event Hub.</span></span> <span data-ttu-id="b90ca-124">Vous allez probablement utiliser cette option si vous disposez d’un pipeline de traitement en aval pour analyser les journaux entrants en temps réel.</span><span class="sxs-lookup"><span data-stu-id="b90ca-124">Most likely you will use this option if you have a downstream processing pipeline to analyze incoming logs at real time.</span></span> <span data-ttu-id="b90ca-125">Si vous sélectionnez cette option, vous devez fournir les informations relatives au Event Hub Azure que vous souhaitez utiliser.</span><span class="sxs-lookup"><span data-stu-id="b90ca-125">If you select this option, you must provide the details for the Azure Event Hub you want to use.</span></span>

        * <span data-ttu-id="b90ca-126">Sélectionnez l’option **Send to Log Analytics (Envoyer à Log Analytics)** pour analyser les données de journal générées, à l’aide du service Azure Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="b90ca-126">Select the option to **Send to Log Analytics** to use the Azure Log Analytics service to analyze the generated log data.</span></span> <span data-ttu-id="b90ca-127">Si vous sélectionnez cette option, vous devez fournir les détails concernant l’espace de travail Operations Management Suite que vous allez utiliser pour analyser le journal.</span><span class="sxs-lookup"><span data-stu-id="b90ca-127">If you select this option, you must provide the details for the Operations Management Suite workspace that you would use the perform log analysis.</span></span>
     
   * <span data-ttu-id="b90ca-128">Spécifiez si vous souhaitez obtenir des journaux d’audit ou des journaux de demande ou les deux.</span><span class="sxs-lookup"><span data-stu-id="b90ca-128">Specify whether you want to get audit logs or request logs or both.</span></span>
   * <span data-ttu-id="b90ca-129">Spécifiez le nombre de jours pendant lesquels les données doivent être conservées.</span><span class="sxs-lookup"><span data-stu-id="b90ca-129">Specify the number of days for which the data must be retained.</span></span> <span data-ttu-id="b90ca-130">La rétention ne s’applique que si vous utilisez un compte de stockage Azure pour archiver les données du journal.</span><span class="sxs-lookup"><span data-stu-id="b90ca-130">Retention is only applicable if you are using Azure storage account to archive log data.</span></span>
   * <span data-ttu-id="b90ca-131">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="b90ca-131">Click **Save**.</span></span>

<span data-ttu-id="b90ca-132">Une fois que vous avez activé les paramètres de diagnostic, vous pouvez consulter les journaux dans l’onglet **Journaux de diagnostic** .</span><span class="sxs-lookup"><span data-stu-id="b90ca-132">Once you have enabled diagnostic settings, you can watch the logs in the **Diagnostic Logs** tab.</span></span>

## <a name="view-diagnostic-logs-for-your-data-lake-store-account"></a><span data-ttu-id="b90ca-133">Afficher les journaux de diagnostic de votre compte Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="b90ca-133">View diagnostic logs for your Data Lake Store account</span></span>
<span data-ttu-id="b90ca-134">Il existe deux manières d’afficher les données de journal de votre compte Data Lake Store :</span><span class="sxs-lookup"><span data-stu-id="b90ca-134">There are two ways to view the log data for your Data Lake Store account.</span></span>

* <span data-ttu-id="b90ca-135">À partir de la vue des paramètres Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="b90ca-135">From the Data Lake Store account settings view</span></span>
* <span data-ttu-id="b90ca-136">À partir du compte de Stockage Azure dans lequel les données sont stockées</span><span class="sxs-lookup"><span data-stu-id="b90ca-136">From the Azure Storage account where the data is stored</span></span>

### <a name="using-the-data-lake-store-settings-view"></a><span data-ttu-id="b90ca-137">Utilisation de la vue des paramètres Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="b90ca-137">Using the Data Lake Store Settings view</span></span>
1. <span data-ttu-id="b90ca-138">Dans le panneau **Paramètres** de votre compte Data Lake Store, cliquez sur **Journaux de diagnostic**.</span><span class="sxs-lookup"><span data-stu-id="b90ca-138">From your Data Lake Store account **Settings** blade, click **Diagnostic Logs**.</span></span>
   
    <span data-ttu-id="b90ca-139">![Afficher la journalisation des diagnostics](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs.png "Afficher les journaux de diagnostic")</span><span class="sxs-lookup"><span data-stu-id="b90ca-139">![View diagnostic logging](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs.png "View diagnostic logs")</span></span> 
2. <span data-ttu-id="b90ca-140">Dans le panneau **Journaux de diagnostic**, vous devez voir les journaux classés par **journaux d’audit** et **journaux de demande**.</span><span class="sxs-lookup"><span data-stu-id="b90ca-140">In the **Diagnostic Logs** blade, you should see the logs categorized by **Audit Logs** and **Request Logs**.</span></span>
   
   * <span data-ttu-id="b90ca-141">Les journaux de demande capturent chaque demande d’API effectuée sur le compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="b90ca-141">Request logs capture every API request made on the Data Lake Store account.</span></span>
   * <span data-ttu-id="b90ca-142">Les journaux d’audit sont similaires aux journaux de demande, mais ils fournissent une analyse beaucoup plus détaillée des opérations effectuées sur le compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="b90ca-142">Audit Logs are similar to request Logs but provide a much more detailed breakdown of the operations being performed on the Data Lake Store account.</span></span> <span data-ttu-id="b90ca-143">Par exemple, un simple appel d’API de chargement dans les journaux de demande peut entraîner plusieurs opérations « Ajouter » dans les journaux d’audit.</span><span class="sxs-lookup"><span data-stu-id="b90ca-143">For example, a single upload API call in request logs might result in multiple "Append" operations in the audit logs.</span></span>
3. <span data-ttu-id="b90ca-144">Cliquez sur le lien **Télécharger** en regard de chaque entrée de journal pour le télécharger.</span><span class="sxs-lookup"><span data-stu-id="b90ca-144">Click the **Download** link against each log entry to download the logs.</span></span>

### <a name="from-the-azure-storage-account-that-contains-log-data"></a><span data-ttu-id="b90ca-145">À partir du compte de Stockage Azure qui contient des données de journal</span><span class="sxs-lookup"><span data-stu-id="b90ca-145">From the Azure Storage account that contains log data</span></span>
1. <span data-ttu-id="b90ca-146">Ouvrez le panneau du compte de Stockage Azure associé au Data Lake Store pour la journalisation, puis cliquez sur Objets blob.</span><span class="sxs-lookup"><span data-stu-id="b90ca-146">Open the Azure Storage account blade associated with Data Lake Store for logging, and then click Blobs.</span></span> <span data-ttu-id="b90ca-147">Le panneau **Service Blob** répertorie deux conteneurs.</span><span class="sxs-lookup"><span data-stu-id="b90ca-147">The **Blob service** blade lists two containers.</span></span>
   
    <span data-ttu-id="b90ca-148">![Afficher la journalisation des diagnostics](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs-storage-account.png "Afficher les journaux de diagnostic")</span><span class="sxs-lookup"><span data-stu-id="b90ca-148">![View diagnostic logging](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs-storage-account.png "View diagnostic logs")</span></span>
   
   * <span data-ttu-id="b90ca-149">Le conteneur **insights-logs-audit** contient les journaux d’audit.</span><span class="sxs-lookup"><span data-stu-id="b90ca-149">The container **insights-logs-audit** contains the audit logs.</span></span>
   * <span data-ttu-id="b90ca-150">Le conteneur **insights-logs-requests** contient les journaux de demande.</span><span class="sxs-lookup"><span data-stu-id="b90ca-150">The container **insights-logs-requests** contains the request logs.</span></span>
2. <span data-ttu-id="b90ca-151">Les journaux sont stockés dans ces conteneurs selon la structure suivante.</span><span class="sxs-lookup"><span data-stu-id="b90ca-151">Within these containers, the logs are stored under the following structure.</span></span>
   
    <span data-ttu-id="b90ca-152">![Afficher la journalisation des diagnostics](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs-storage-account-structure.png "Afficher les journaux de diagnostic")</span><span class="sxs-lookup"><span data-stu-id="b90ca-152">![View diagnostic logging](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs-storage-account-structure.png "View diagnostic logs")</span></span>
   
    <span data-ttu-id="b90ca-153">Par exemple, le chemin d’accès complet à un journal d’audit peut être `https://adllogs.blob.core.windows.net/insights-logs-audit/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/mydatalakestore/y=2016/m=07/d=18/h=04/m=00/PT1H.json`</span><span class="sxs-lookup"><span data-stu-id="b90ca-153">As an example, the complete path to an audit log could be `https://adllogs.blob.core.windows.net/insights-logs-audit/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/mydatalakestore/y=2016/m=07/d=18/h=04/m=00/PT1H.json`</span></span>
   
    <span data-ttu-id="b90ca-154">De même, le chemin d’accès complet à un journal de demande peut être `https://adllogs.blob.core.windows.net/insights-logs-requests/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/mydatalakestore/y=2016/m=07/d=18/h=14/m=00/PT1H.json`</span><span class="sxs-lookup"><span data-stu-id="b90ca-154">Similary, the complete path to a request log could be `https://adllogs.blob.core.windows.net/insights-logs-requests/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/mydatalakestore/y=2016/m=07/d=18/h=14/m=00/PT1H.json`</span></span>

## <a name="understand-the-structure-of-the-log-data"></a><span data-ttu-id="b90ca-155">Comprendre la structure des données de journal</span><span class="sxs-lookup"><span data-stu-id="b90ca-155">Understand the structure of the log data</span></span>
<span data-ttu-id="b90ca-156">Les journaux d’audit et de demande sont au format JSON.</span><span class="sxs-lookup"><span data-stu-id="b90ca-156">The audit and request logs are in a JSON format.</span></span> <span data-ttu-id="b90ca-157">Dans cette section, nous examinons la structure JSON des journaux de demande et d’audit.</span><span class="sxs-lookup"><span data-stu-id="b90ca-157">In this section, we look at the structure of JSON for request and audit logs.</span></span>

### <a name="request-logs"></a><span data-ttu-id="b90ca-158">journaux de demande</span><span class="sxs-lookup"><span data-stu-id="b90ca-158">Request logs</span></span>
<span data-ttu-id="b90ca-159">Voici un exemple d’entrée dans le journal de demande au format JSON.</span><span class="sxs-lookup"><span data-stu-id="b90ca-159">Here's a sample entry in the JSON-formatted request log.</span></span> <span data-ttu-id="b90ca-160">Chaque objet blob a un objet racine appelé **enregistrements** qui contient un tableau d’objets du journal.</span><span class="sxs-lookup"><span data-stu-id="b90ca-160">Each blob has one root object called **records** that contains an array of log objects.</span></span>

    {
    "records": 
      [        
        . . . .
        ,
        {
             "time": "2016-07-07T21:02:53.456Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/<data_lake_store_account_name>",
             "category": "Requests",
             "operationName": "GETCustomerIngressEgress",
             "resultType": "200",
             "callerIpAddress": "::ffff:1.1.1.1",
             "correlationId": "4a11c709-05f5-417c-a98d-6e81b3e29c58",
             "identity": "1808bd5f-62af-45f4-89d8-03c5e81bac30",
             "properties": {"HttpMethod":"GET","Path":"/webhdfs/v1/Samples/Outputs/Drivers.csv","RequestContentLength":0,"ClientRequestId":"3b7adbd9-3519-4f28-a61c-bd89506163b8","StartTime":"2016-07-07T21:02:52.472Z","EndTime":"2016-07-07T21:02:53.456Z"}
        }
        ,
        . . . .
      ]
    }

#### <a name="request-log-schema"></a><span data-ttu-id="b90ca-161">Schéma du journal de requête</span><span class="sxs-lookup"><span data-stu-id="b90ca-161">Request log schema</span></span>
| <span data-ttu-id="b90ca-162">Name</span><span class="sxs-lookup"><span data-stu-id="b90ca-162">Name</span></span> | <span data-ttu-id="b90ca-163">Type</span><span class="sxs-lookup"><span data-stu-id="b90ca-163">Type</span></span> | <span data-ttu-id="b90ca-164">Description</span><span class="sxs-lookup"><span data-stu-id="b90ca-164">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b90ca-165">time</span><span class="sxs-lookup"><span data-stu-id="b90ca-165">time</span></span> |<span data-ttu-id="b90ca-166">Chaîne</span><span class="sxs-lookup"><span data-stu-id="b90ca-166">String</span></span> |<span data-ttu-id="b90ca-167">L’horodatage (heure UTC) du journal.</span><span class="sxs-lookup"><span data-stu-id="b90ca-167">The timestamp (in UTC) of the log</span></span> |
| <span data-ttu-id="b90ca-168">resourceId</span><span class="sxs-lookup"><span data-stu-id="b90ca-168">resourceId</span></span> |<span data-ttu-id="b90ca-169">Chaîne</span><span class="sxs-lookup"><span data-stu-id="b90ca-169">String</span></span> |<span data-ttu-id="b90ca-170">L’ID de la ressource sur laquelle l’opération a eu lieu.</span><span class="sxs-lookup"><span data-stu-id="b90ca-170">The ID of the resource that operation took place on</span></span> |
| <span data-ttu-id="b90ca-171">category</span><span class="sxs-lookup"><span data-stu-id="b90ca-171">category</span></span> |<span data-ttu-id="b90ca-172">Chaîne</span><span class="sxs-lookup"><span data-stu-id="b90ca-172">String</span></span> |<span data-ttu-id="b90ca-173">La catégorie du journal.</span><span class="sxs-lookup"><span data-stu-id="b90ca-173">The log category.</span></span> <span data-ttu-id="b90ca-174">Par exemple, **Demandes**.</span><span class="sxs-lookup"><span data-stu-id="b90ca-174">For example, **Requests**.</span></span> |
| <span data-ttu-id="b90ca-175">operationName</span><span class="sxs-lookup"><span data-stu-id="b90ca-175">operationName</span></span> |<span data-ttu-id="b90ca-176">Chaîne</span><span class="sxs-lookup"><span data-stu-id="b90ca-176">String</span></span> |<span data-ttu-id="b90ca-177">Le nom de l’opération qui est journalisée.</span><span class="sxs-lookup"><span data-stu-id="b90ca-177">Name of the operation that is logged.</span></span> <span data-ttu-id="b90ca-178">Par exemple, getfilestatus.</span><span class="sxs-lookup"><span data-stu-id="b90ca-178">For example, getfilestatus.</span></span> |
| <span data-ttu-id="b90ca-179">resultType</span><span class="sxs-lookup"><span data-stu-id="b90ca-179">resultType</span></span> |<span data-ttu-id="b90ca-180">Chaîne</span><span class="sxs-lookup"><span data-stu-id="b90ca-180">String</span></span> |<span data-ttu-id="b90ca-181">L’état de l’opération. Par exemple, 200.</span><span class="sxs-lookup"><span data-stu-id="b90ca-181">The status of the operation, For example, 200.</span></span> |
| <span data-ttu-id="b90ca-182">callerIpAddress</span><span class="sxs-lookup"><span data-stu-id="b90ca-182">callerIpAddress</span></span> |<span data-ttu-id="b90ca-183">Chaîne</span><span class="sxs-lookup"><span data-stu-id="b90ca-183">String</span></span> |<span data-ttu-id="b90ca-184">L’adresse IP du client qui a effectué la demande.</span><span class="sxs-lookup"><span data-stu-id="b90ca-184">The IP address of the client making the request</span></span> |
| <span data-ttu-id="b90ca-185">correlationId</span><span class="sxs-lookup"><span data-stu-id="b90ca-185">correlationId</span></span> |<span data-ttu-id="b90ca-186">Chaîne</span><span class="sxs-lookup"><span data-stu-id="b90ca-186">String</span></span> |<span data-ttu-id="b90ca-187">L’ID du journal qui peut être utilisé pour regrouper un ensemble d’entrées de journal associées.</span><span class="sxs-lookup"><span data-stu-id="b90ca-187">The id of the log that can used to group together a set of related log entries</span></span> |
| <span data-ttu-id="b90ca-188">identité</span><span class="sxs-lookup"><span data-stu-id="b90ca-188">identity</span></span> |<span data-ttu-id="b90ca-189">Object</span><span class="sxs-lookup"><span data-stu-id="b90ca-189">Object</span></span> |<span data-ttu-id="b90ca-190">L’identité qui a généré le journal.</span><span class="sxs-lookup"><span data-stu-id="b90ca-190">The identity that generated the log</span></span> |
| <span data-ttu-id="b90ca-191">properties</span><span class="sxs-lookup"><span data-stu-id="b90ca-191">properties</span></span> |<span data-ttu-id="b90ca-192">JSON</span><span class="sxs-lookup"><span data-stu-id="b90ca-192">JSON</span></span> |<span data-ttu-id="b90ca-193">Voir les détails ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="b90ca-193">See below for details</span></span> |

#### <a name="request-log-properties-schema"></a><span data-ttu-id="b90ca-194">Schéma des propriétés de journal de demande</span><span class="sxs-lookup"><span data-stu-id="b90ca-194">Request log properties schema</span></span>
| <span data-ttu-id="b90ca-195">Name</span><span class="sxs-lookup"><span data-stu-id="b90ca-195">Name</span></span> | <span data-ttu-id="b90ca-196">Type</span><span class="sxs-lookup"><span data-stu-id="b90ca-196">Type</span></span> | <span data-ttu-id="b90ca-197">Description</span><span class="sxs-lookup"><span data-stu-id="b90ca-197">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b90ca-198">HttpMethod</span><span class="sxs-lookup"><span data-stu-id="b90ca-198">HttpMethod</span></span> |<span data-ttu-id="b90ca-199">Chaîne</span><span class="sxs-lookup"><span data-stu-id="b90ca-199">String</span></span> |<span data-ttu-id="b90ca-200">La méthode HTTP utilisée pour l’opération.</span><span class="sxs-lookup"><span data-stu-id="b90ca-200">The HTTP Method used for the operation.</span></span> <span data-ttu-id="b90ca-201">Par exemple, GET.</span><span class="sxs-lookup"><span data-stu-id="b90ca-201">For example, GET.</span></span> |
| <span data-ttu-id="b90ca-202">Chemin</span><span class="sxs-lookup"><span data-stu-id="b90ca-202">Path</span></span> |<span data-ttu-id="b90ca-203">Chaîne</span><span class="sxs-lookup"><span data-stu-id="b90ca-203">String</span></span> |<span data-ttu-id="b90ca-204">Le chemin d’accès vers l’emplacement où l’opération a eu lieu.</span><span class="sxs-lookup"><span data-stu-id="b90ca-204">The path the operation was performed on</span></span> |
| <span data-ttu-id="b90ca-205">RequestContentLength</span><span class="sxs-lookup"><span data-stu-id="b90ca-205">RequestContentLength</span></span> |<span data-ttu-id="b90ca-206">int</span><span class="sxs-lookup"><span data-stu-id="b90ca-206">int</span></span> |<span data-ttu-id="b90ca-207">La longueur du contenu de la demande HTTP.</span><span class="sxs-lookup"><span data-stu-id="b90ca-207">The content length of the HTTP request</span></span> |
| <span data-ttu-id="b90ca-208">ClientRequestId</span><span class="sxs-lookup"><span data-stu-id="b90ca-208">ClientRequestId</span></span> |<span data-ttu-id="b90ca-209">Chaîne</span><span class="sxs-lookup"><span data-stu-id="b90ca-209">String</span></span> |<span data-ttu-id="b90ca-210">L’ID qui identifie de façon unique la demande.</span><span class="sxs-lookup"><span data-stu-id="b90ca-210">The Id that uniquely identifies this request</span></span> |
| <span data-ttu-id="b90ca-211">StartTime</span><span class="sxs-lookup"><span data-stu-id="b90ca-211">StartTime</span></span> |<span data-ttu-id="b90ca-212">Chaîne</span><span class="sxs-lookup"><span data-stu-id="b90ca-212">String</span></span> |<span data-ttu-id="b90ca-213">L’heure à laquelle le serveur a reçu la demande.</span><span class="sxs-lookup"><span data-stu-id="b90ca-213">The time at which the server received the request</span></span> |
| <span data-ttu-id="b90ca-214">EndTime</span><span class="sxs-lookup"><span data-stu-id="b90ca-214">EndTime</span></span> |<span data-ttu-id="b90ca-215">Chaîne</span><span class="sxs-lookup"><span data-stu-id="b90ca-215">String</span></span> |<span data-ttu-id="b90ca-216">L’heure à laquelle le serveur a envoyé une réponse.</span><span class="sxs-lookup"><span data-stu-id="b90ca-216">The time at which the server sent a response</span></span> |

### <a name="audit-logs"></a><span data-ttu-id="b90ca-217">Journaux d’audit</span><span class="sxs-lookup"><span data-stu-id="b90ca-217">Audit logs</span></span>
<span data-ttu-id="b90ca-218">Voici un exemple d’entrée dans le journal d’audit au format JSON.</span><span class="sxs-lookup"><span data-stu-id="b90ca-218">Here's a sample entry in the JSON-formatted audit log.</span></span> <span data-ttu-id="b90ca-219">Chaque objet blob a un objet racine appelé **records** qui contient un tableau d’objets du journal</span><span class="sxs-lookup"><span data-stu-id="b90ca-219">Each blob has one root object called **records** that contains an array of log objects</span></span>

    {
    "records": 
      [        
        . . . .
        ,
        {
             "time": "2016-07-08T19:08:59.359Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/<data_lake_store_account_name>",
             "category": "Audit",
             "operationName": "SeOpenStream",
             "resultType": "0",
             "correlationId": "381110fc03534e1cb99ec52376ceebdf;Append_BrEKAmg;25.66.9.145",
             "identity": "A9DAFFAF-FFEE-4BB5-A4A0-1B6CBBF24355",
             "properties": {"StreamName":"adl://<data_lake_store_account_name>.azuredatalakestore.net/logs.csv"}
        }
        ,
        . . . .
      ]
    }

#### <a name="audit-log-schema"></a><span data-ttu-id="b90ca-220">Schéma du journal d’audit</span><span class="sxs-lookup"><span data-stu-id="b90ca-220">Audit log schema</span></span>
| <span data-ttu-id="b90ca-221">Name</span><span class="sxs-lookup"><span data-stu-id="b90ca-221">Name</span></span> | <span data-ttu-id="b90ca-222">Type</span><span class="sxs-lookup"><span data-stu-id="b90ca-222">Type</span></span> | <span data-ttu-id="b90ca-223">Description</span><span class="sxs-lookup"><span data-stu-id="b90ca-223">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b90ca-224">time</span><span class="sxs-lookup"><span data-stu-id="b90ca-224">time</span></span> |<span data-ttu-id="b90ca-225">Chaîne</span><span class="sxs-lookup"><span data-stu-id="b90ca-225">String</span></span> |<span data-ttu-id="b90ca-226">L’horodatage (heure UTC) du journal.</span><span class="sxs-lookup"><span data-stu-id="b90ca-226">The timestamp (in UTC) of the log</span></span> |
| <span data-ttu-id="b90ca-227">resourceId</span><span class="sxs-lookup"><span data-stu-id="b90ca-227">resourceId</span></span> |<span data-ttu-id="b90ca-228">Chaîne</span><span class="sxs-lookup"><span data-stu-id="b90ca-228">String</span></span> |<span data-ttu-id="b90ca-229">L’ID de la ressource sur laquelle l’opération a eu lieu.</span><span class="sxs-lookup"><span data-stu-id="b90ca-229">The ID of the resource that operation took place on</span></span> |
| <span data-ttu-id="b90ca-230">category</span><span class="sxs-lookup"><span data-stu-id="b90ca-230">category</span></span> |<span data-ttu-id="b90ca-231">Chaîne</span><span class="sxs-lookup"><span data-stu-id="b90ca-231">String</span></span> |<span data-ttu-id="b90ca-232">La catégorie du journal.</span><span class="sxs-lookup"><span data-stu-id="b90ca-232">The log category.</span></span> <span data-ttu-id="b90ca-233">Par exemple, **Audit**.</span><span class="sxs-lookup"><span data-stu-id="b90ca-233">For example, **Audit**.</span></span> |
| <span data-ttu-id="b90ca-234">operationName</span><span class="sxs-lookup"><span data-stu-id="b90ca-234">operationName</span></span> |<span data-ttu-id="b90ca-235">Chaîne</span><span class="sxs-lookup"><span data-stu-id="b90ca-235">String</span></span> |<span data-ttu-id="b90ca-236">Le nom de l’opération qui est journalisée.</span><span class="sxs-lookup"><span data-stu-id="b90ca-236">Name of the operation that is logged.</span></span> <span data-ttu-id="b90ca-237">Par exemple, getfilestatus.</span><span class="sxs-lookup"><span data-stu-id="b90ca-237">For example, getfilestatus.</span></span> |
| <span data-ttu-id="b90ca-238">resultType</span><span class="sxs-lookup"><span data-stu-id="b90ca-238">resultType</span></span> |<span data-ttu-id="b90ca-239">Chaîne</span><span class="sxs-lookup"><span data-stu-id="b90ca-239">String</span></span> |<span data-ttu-id="b90ca-240">L’état de l’opération. Par exemple, 200.</span><span class="sxs-lookup"><span data-stu-id="b90ca-240">The status of the operation, For example, 200.</span></span> |
| <span data-ttu-id="b90ca-241">correlationId</span><span class="sxs-lookup"><span data-stu-id="b90ca-241">correlationId</span></span> |<span data-ttu-id="b90ca-242">Chaîne</span><span class="sxs-lookup"><span data-stu-id="b90ca-242">String</span></span> |<span data-ttu-id="b90ca-243">L’ID du journal qui peut être utilisé pour regrouper un ensemble d’entrées de journal associées.</span><span class="sxs-lookup"><span data-stu-id="b90ca-243">The id of the log that can used to group together a set of related log entries</span></span> |
| <span data-ttu-id="b90ca-244">identité</span><span class="sxs-lookup"><span data-stu-id="b90ca-244">identity</span></span> |<span data-ttu-id="b90ca-245">Object</span><span class="sxs-lookup"><span data-stu-id="b90ca-245">Object</span></span> |<span data-ttu-id="b90ca-246">L’identité qui a généré le journal.</span><span class="sxs-lookup"><span data-stu-id="b90ca-246">The identity that generated the log</span></span> |
| <span data-ttu-id="b90ca-247">properties</span><span class="sxs-lookup"><span data-stu-id="b90ca-247">properties</span></span> |<span data-ttu-id="b90ca-248">JSON</span><span class="sxs-lookup"><span data-stu-id="b90ca-248">JSON</span></span> |<span data-ttu-id="b90ca-249">Voir les détails ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="b90ca-249">See below for details</span></span> |

#### <a name="audit-log-properties-schema"></a><span data-ttu-id="b90ca-250">Schéma des propriétés de journal d’audit</span><span class="sxs-lookup"><span data-stu-id="b90ca-250">Audit log properties schema</span></span>
| <span data-ttu-id="b90ca-251">Name</span><span class="sxs-lookup"><span data-stu-id="b90ca-251">Name</span></span> | <span data-ttu-id="b90ca-252">Type</span><span class="sxs-lookup"><span data-stu-id="b90ca-252">Type</span></span> | <span data-ttu-id="b90ca-253">Description</span><span class="sxs-lookup"><span data-stu-id="b90ca-253">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b90ca-254">StreamName</span><span class="sxs-lookup"><span data-stu-id="b90ca-254">StreamName</span></span> |<span data-ttu-id="b90ca-255">Chaîne</span><span class="sxs-lookup"><span data-stu-id="b90ca-255">String</span></span> |<span data-ttu-id="b90ca-256">Le chemin d’accès vers l’emplacement où l’opération a eu lieu.</span><span class="sxs-lookup"><span data-stu-id="b90ca-256">The path the operation was performed on</span></span> |

## <a name="samples-to-process-the-log-data"></a><span data-ttu-id="b90ca-257">Exemples de traitement des données de journal</span><span class="sxs-lookup"><span data-stu-id="b90ca-257">Samples to process the log data</span></span>
<span data-ttu-id="b90ca-258">Azure Data Lake Store fournit un exemple de traitement et d’analyse des données de journal.</span><span class="sxs-lookup"><span data-stu-id="b90ca-258">Azure Data Lake Store provides a sample on how to process and analyze the log data.</span></span> <span data-ttu-id="b90ca-259">Vous trouverez l’exemple à l’adresse [https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample](https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample).</span><span class="sxs-lookup"><span data-stu-id="b90ca-259">You can find the sample at [https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample](https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample).</span></span> 

## <a name="see-also"></a><span data-ttu-id="b90ca-260">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="b90ca-260">See also</span></span>
* [<span data-ttu-id="b90ca-261">Présentation d'Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="b90ca-261">Overview of Azure Data Lake Store</span></span>](data-lake-store-overview.md)
* [<span data-ttu-id="b90ca-262">Sécuriser les données dans Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="b90ca-262">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)

