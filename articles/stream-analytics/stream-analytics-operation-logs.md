---
title: "aaaDebug à l’aide des journaux d’opération et de service dans le flux de données Analytique | Documents Microsoft"
description: "Flux de façon-toouse journaux Analytique"
keywords: journaux de service
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: a2ed9676-f0bd-4398-87c8-a592779ac728
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: d3dd27706ccc879a724e1894b33d47021d972f31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="debug-stream-analytics-jobs-using-service-and-operation-logs"></a><span data-ttu-id="ae3eb-104">Débogage des travaux Stream Analytics à l’aide des journaux des opérations et de service</span><span class="sxs-lookup"><span data-stu-id="ae3eb-104">Debug Stream Analytics jobs using service and operation logs</span></span>
<span data-ttu-id="ae3eb-105">Tous les détails de toorecord toousers messages journalisation opérationnel de fourniture des services Azure liées toomanagement operations.</span><span class="sxs-lookup"><span data-stu-id="ae3eb-105">All Azure services supply operational logging messages toousers toorecord details related toomanagement operations.</span></span> <span data-ttu-id="ae3eb-106">Dans Azure Analytique de flux de données, ces informations peuvent être utilisées pour le débogage, telles que l’affichage État du travail, progression du travail et la défaillance messages tootrack hello progression d’une tâche au fil du temps, à partir du début tooprocessing toooutput.</span><span class="sxs-lookup"><span data-stu-id="ae3eb-106">In Azure Stream Analytics, this information can be used for debugging purposes such as viewing job status, job progress, and failure messages tootrack hello progress of a job over time, from start tooprocessing toooutput.</span></span>

## <a name="find-operation-logs-in-hello-azure-management-portal"></a><span data-ttu-id="ae3eb-107">Rechercher les journaux des opérations dans le portail de gestion Azure hello</span><span class="sxs-lookup"><span data-stu-id="ae3eb-107">Find operation logs in hello Azure Management portal</span></span>
<span data-ttu-id="ae3eb-108">Les journaux des opérations sont accessibles de deux manières :</span><span class="sxs-lookup"><span data-stu-id="ae3eb-108">Operation Logs can be accessed in two ways:</span></span>  

* <span data-ttu-id="ae3eb-109">Tableau de bord de la tâche de flux de données Analytique hello</span><span class="sxs-lookup"><span data-stu-id="ae3eb-109">Dashboard of hello Stream Analytics job</span></span>  
* <span data-ttu-id="ae3eb-110">Services de gestion dans le portail Azure Classic de hello</span><span class="sxs-lookup"><span data-stu-id="ae3eb-110">Management Services in hello Azure Classic portal</span></span>  

## <a name="dashboard-of-hello-stream-analytics-job"></a><span data-ttu-id="ae3eb-111">Tableau de bord de la tâche de flux de données Analytique hello</span><span class="sxs-lookup"><span data-stu-id="ae3eb-111">Dashboard of hello Stream Analytics job</span></span>
<span data-ttu-id="ae3eb-112">Un toohello lien correspondant des journaux d’une tâche de flux de données Analytique est affiché sur l’onglet tableau de bord de la tâche hello. Si vous cliquez sur ce lien, elle définit les filtres hello de manière qu’elle affiche les derniers journaux pour cette tâche.</span><span class="sxs-lookup"><span data-stu-id="ae3eb-112">A link toohello corresponding logs of a Stream Analytics job is displayed on hello job’s Dashboard tab. If you click on that link, it will set hello filters in a way that it shows latest logs for that specific job.</span></span>

  ![Sélection des journaux des services de gestion](./media/stream-analytics-operation-logs/01-stream-analytics-operation-logs.png)  

## <a name="management-services"></a><span data-ttu-id="ae3eb-114">Services de gestion</span><span class="sxs-lookup"><span data-stu-id="ae3eb-114">Management Services</span></span>
<span data-ttu-id="ae3eb-115">toomanually accédez toohello journaux d’opérations de flux de données Analytique et d’autres services dans le portail Azure Classic de hello :</span><span class="sxs-lookup"><span data-stu-id="ae3eb-115">toomanually navigate toohello Operation Logs for Stream Analytics and other services in hello Azure Classic portal:</span></span>

1. <span data-ttu-id="ae3eb-116">Cliquez sur **des Services de gestion** Bonjour [portail Azure Classic](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="ae3eb-116">Click on **Management Services** in hello [Azure Classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="ae3eb-117">Sélectionnez **flux Analytique** pour **Type** et le nom hello hello du travail de pour **nom du Service**.</span><span class="sxs-lookup"><span data-stu-id="ae3eb-117">Select **Stream Analytics** for **Type** and hello name of hello job for **Service Name**.</span></span>  
   
   ![Sélection de Stream Analytics](./media/stream-analytics-operation-logs/02-stream-analytics-operation-logs.png)  

## <a name="find-audit-logs-in-hello-azure-portal"></a><span data-ttu-id="ae3eb-119">Rechercher des journaux d’audit dans hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="ae3eb-119">Find audit logs in hello Azure portal</span></span>
<span data-ttu-id="ae3eb-120">journaux des opérations toofind pour votre tâche de flux de données Analytique Bonjour portail Azure, cliquez sur **Parcourir** , puis sélectionnez **journaux d’Audit**.</span><span class="sxs-lookup"><span data-stu-id="ae3eb-120">toofind operational logs for your Stream Analytics job in hello Azure portal, Click **Browse** and then select **Audit logs**.</span></span>

  ![Sélection de Stream Analytics dans le portail Azure](./media/stream-analytics-operation-logs/06-stream-analytics-operation-logs.png)  

<span data-ttu-id="ae3eb-122">Un panneau d’affichage des 7 derniers jours pour toutes les ressources d’événements à partir de hello dans votre abonnement s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="ae3eb-122">This will open a blade showing events from hello last 7 days for all resources in your subscription.</span></span>  <span data-ttu-id="ae3eb-123">Vous pouvez filtrer les événements de toosee de spécifier le type ou de l’intervalle de temps en cliquant sur hello **filtre** commande.</span><span class="sxs-lookup"><span data-stu-id="ae3eb-123">You can filter toosee events of a specify type or time frame by clicking hello **Filter** command.</span></span>

  ![Sélection de Stream Analytics dans le portail Azure](./media/stream-analytics-operation-logs/07-stream-analytics-operation-logs.png)  

## <a name="get-log-details"></a><span data-ttu-id="ae3eb-125">Obtenir les détails d’un journal</span><span class="sxs-lookup"><span data-stu-id="ae3eb-125">Get log details</span></span>
<span data-ttu-id="ae3eb-126">Vous pouvez filtrer par plage de temps et les journaux de statut tooview hello pour votre travail.</span><span class="sxs-lookup"><span data-stu-id="ae3eb-126">You can filter by Time Range and Status tooview hello logs for your job.</span></span>

<span data-ttu-id="ae3eb-127">Dans le portail de gestion Azure hello, cliquez sur hello **détails** bouton bas hello hello fenêtre tooview plus de détails sur un événement sélectionné.</span><span class="sxs-lookup"><span data-stu-id="ae3eb-127">In hello Azure Management portal, click on hello **Details** button at hello bottom of hello window tooview more details about a selected event.</span></span> 

  ![Sélection des détails](./media/stream-analytics-operation-logs/03-stream-analytics-operation-logs.png)  

<span data-ttu-id="ae3eb-129">Bonjour portail Azure, cliquez sur un toosee d’entrée de journal hello événements détaillés qu’il contient.</span><span class="sxs-lookup"><span data-stu-id="ae3eb-129">In hello Azure portal, click on a log entry toosee hello detailed events inside it.</span></span>

  ![Sélection des détails dans le portail Azure](./media/stream-analytics-operation-logs/08-stream-analytics-operation-logs.png)  

<span data-ttu-id="ae3eb-131">À partir de là, vous pouvez ouvrir hello **détail** panneau en cliquant sur les événements hello.</span><span class="sxs-lookup"><span data-stu-id="ae3eb-131">From there, you can open hello **Detail** blade by clicking on hello event.</span></span>

  ![Sélection des détails dans le portail Azure](./media/stream-analytics-operation-logs/09-stream-analytics-operation-logs.png)  

## <a name="debug-a-failed-job"></a><span data-ttu-id="ae3eb-133">Débogage d’une tâche ayant échoué</span><span class="sxs-lookup"><span data-stu-id="ae3eb-133">Debug a failed job</span></span>
<span data-ttu-id="ae3eb-134">Dans le portail de gestion Azure hello, cliquez sur l’icône de recherche hello et tapez « échec ».</span><span class="sxs-lookup"><span data-stu-id="ae3eb-134">In hello Azure Management portal, click on hello Search icon and type ‘failed’.</span></span> <span data-ttu-id="ae3eb-135">Vous obtenez comme résultat tous les journaux avec des erreurs.</span><span class="sxs-lookup"><span data-stu-id="ae3eb-135">This gives a result of all logs with failures.</span></span> 

  ![Débogage d'une tâche ayant échoué](./media/stream-analytics-operation-logs/04-stream-analytics-operation-logs.png)  

<span data-ttu-id="ae3eb-137">Bonjour portail Azure, vous pouvez filtrer par niveau de message tooview **critique** événements.</span><span class="sxs-lookup"><span data-stu-id="ae3eb-137">In hello Azure portal, you can filter by level of message tooview **Critical** events.</span></span>

  ![Débogage du portail Azure](./media/stream-analytics-operation-logs/10-stream-analytics-operation-logs.png)  

<span data-ttu-id="ae3eb-139">Vous pouvez sélectionner l’un des échecs de hello et cliquez sur hello **détails** pour plus d’informations sur l’erreur de hello.</span><span class="sxs-lookup"><span data-stu-id="ae3eb-139">You can select any one of hello failures, and click on hello **Details** for more information on hello error.</span></span>  <span data-ttu-id="ae3eb-140">Certains messages d’erreur fournissent des informations sur la façon dont toomitigate hello problème.</span><span class="sxs-lookup"><span data-stu-id="ae3eb-140">Some error messages also provide information about how toomitigate hello issue.</span></span> 

  ![Détails de l'opération](./media/stream-analytics-operation-logs/05-stream-analytics-operation-logs.png)  

<span data-ttu-id="ae3eb-142">En cas de besoin toocontact [prise en charge](https://azure.microsoft.com/support/options/) ou fournissez l’équipe de toohello informations via hello [forum MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics), notez les détails de l’opération hello, spécifiquement hello **ID de corrélation**.</span><span class="sxs-lookup"><span data-stu-id="ae3eb-142">In case you need toocontact [Support](https://azure.microsoft.com/support/options/) or provide information toohello team via hello [MSDN forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics), please note hello Operation Details, specifically hello **Correlation ID**.</span></span> 

## <a name="get-help"></a><span data-ttu-id="ae3eb-143">Obtenir de l’aide</span><span class="sxs-lookup"><span data-stu-id="ae3eb-143">Get help</span></span>
<span data-ttu-id="ae3eb-144">Pour obtenir une assistance, essayez notre [forum Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="ae3eb-144">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="ae3eb-145">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ae3eb-145">Next steps</span></span>
* [<span data-ttu-id="ae3eb-146">Introduction tooAzure Analytique de flux de données</span><span class="sxs-lookup"><span data-stu-id="ae3eb-146">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="ae3eb-147">Prise en main d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="ae3eb-147">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="ae3eb-148">Mise à l'échelle des travaux Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="ae3eb-148">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="ae3eb-149">Références sur le langage des requêtes d'Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="ae3eb-149">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="ae3eb-150">Références sur l’API REST de gestion d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="ae3eb-150">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

