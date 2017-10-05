---
title: "Débogage à l’aide des journaux des opérations et de service dans Stream Analytics | Microsoft Docs"
description: "Comment utiliser les journaux des opérations Stream Analytics"
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
ms.openlocfilehash: c95d240ebef6a84228eb98db70002792fcfbdea6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="debug-stream-analytics-jobs-using-service-and-operation-logs"></a><span data-ttu-id="0f025-104">Débogage des travaux Stream Analytics à l’aide des journaux des opérations et de service</span><span class="sxs-lookup"><span data-stu-id="0f025-104">Debug Stream Analytics jobs using service and operation logs</span></span>
<span data-ttu-id="0f025-105">Tous les services Azure fournissent des messages de journalisation opérationnelle aux utilisateurs pour enregistrer les détails relatifs aux opérations de gestion.</span><span class="sxs-lookup"><span data-stu-id="0f025-105">All Azure services supply operational logging messages to users to record details related to management operations.</span></span> <span data-ttu-id="0f025-106">Dans Azure Stream Analytics, ces informations peuvent être utilisées à des fins de débogage, comme les messages sur l'affichage de l'état d'une tâche, la progression de la tâche et l'échec pour suivre la progression d'une tâche au fil du temps, depuis son démarrage, jusqu'à son traitement et sa sortie.</span><span class="sxs-lookup"><span data-stu-id="0f025-106">In Azure Stream Analytics, this information can be used for debugging purposes such as viewing job status, job progress, and failure messages to track the progress of a job over time, from start to processing to output.</span></span>

## <a name="find-operation-logs-in-the-azure-management-portal"></a><span data-ttu-id="0f025-107">Rechercher des journaux d’opérations dans le portail de gestion Azure</span><span class="sxs-lookup"><span data-stu-id="0f025-107">Find operation logs in the Azure Management portal</span></span>
<span data-ttu-id="0f025-108">Les journaux des opérations sont accessibles de deux manières :</span><span class="sxs-lookup"><span data-stu-id="0f025-108">Operation Logs can be accessed in two ways:</span></span>  

* <span data-ttu-id="0f025-109">Tableau de bord de la tâche Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="0f025-109">Dashboard of the Stream Analytics job</span></span>  
* <span data-ttu-id="0f025-110">Services de gestion dans le portail Azure Classic</span><span class="sxs-lookup"><span data-stu-id="0f025-110">Management Services in the Azure Classic portal</span></span>  

## <a name="dashboard-of-the-stream-analytics-job"></a><span data-ttu-id="0f025-111">Tableau de bord de la tâche Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="0f025-111">Dashboard of the Stream Analytics job</span></span>
<span data-ttu-id="0f025-112">Un lien vers les journaux correspondants d'une tâche Stream Analytics s'affiche dans l'onglet du Tableau de bord de la tâche. Si vous cliquez sur ce lien, il définit les filtres de manière à afficher les derniers journaux pour cette tâche.</span><span class="sxs-lookup"><span data-stu-id="0f025-112">A link to the corresponding logs of a Stream Analytics job is displayed on the job’s Dashboard tab. If you click on that link, it will set the filters in a way that it shows latest logs for that specific job.</span></span>

  ![Sélection des journaux des services de gestion](./media/stream-analytics-operation-logs/01-stream-analytics-operation-logs.png)  

## <a name="management-services"></a><span data-ttu-id="0f025-114">Services de gestion</span><span class="sxs-lookup"><span data-stu-id="0f025-114">Management Services</span></span>
<span data-ttu-id="0f025-115">Pour accéder manuellement aux journaux des opérations pour Stream Analytics et d’autres services dans le portail Azure Classic :</span><span class="sxs-lookup"><span data-stu-id="0f025-115">To manually navigate to the Operation Logs for Stream Analytics and other services in the Azure Classic portal:</span></span>

1. <span data-ttu-id="0f025-116">Cliquez sur **Services de gestion** dans le [portail Azure Classic](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="0f025-116">Click on **Management Services** in the [Azure Classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="0f025-117">Sélectionnez **Stream Analytics** pour **Type** et le nom du travail pour **Nom du service**.</span><span class="sxs-lookup"><span data-stu-id="0f025-117">Select **Stream Analytics** for **Type** and the name of the job for **Service Name**.</span></span>  
   
   ![Sélection de Stream Analytics](./media/stream-analytics-operation-logs/02-stream-analytics-operation-logs.png)  

## <a name="find-audit-logs-in-the-azure-portal"></a><span data-ttu-id="0f025-119">Rechercher des journaux d’audit dans le portail Azure</span><span class="sxs-lookup"><span data-stu-id="0f025-119">Find audit logs in the Azure portal</span></span>
<span data-ttu-id="0f025-120">Pour rechercher des journaux d’opérations pour votre travail Stream Analytics dans le portail Azure, cliquez sur **Parcourir**, puis sélectionnez **Journaux d’audit**.</span><span class="sxs-lookup"><span data-stu-id="0f025-120">To find operational logs for your Stream Analytics job in the Azure portal, Click **Browse** and then select **Audit logs**.</span></span>

  ![Sélection de Stream Analytics dans le portail Azure](./media/stream-analytics-operation-logs/06-stream-analytics-operation-logs.png)  

<span data-ttu-id="0f025-122">Cette action ouvre un panneau répertoriant les événements survenus au cours des sept derniers jours pour toutes les ressources de votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="0f025-122">This will open a blade showing events from the last 7 days for all resources in your subscription.</span></span>  <span data-ttu-id="0f025-123">Vous pouvez filtrer ces informations pour afficher les événements d’un type ou d’un intervalle de temps spécifique en cliquant sur la commande **Filtrer** .</span><span class="sxs-lookup"><span data-stu-id="0f025-123">You can filter to see events of a specify type or time frame by clicking the **Filter** command.</span></span>

  ![Sélection de Stream Analytics dans le portail Azure](./media/stream-analytics-operation-logs/07-stream-analytics-operation-logs.png)  

## <a name="get-log-details"></a><span data-ttu-id="0f025-125">Obtenir les détails d’un journal</span><span class="sxs-lookup"><span data-stu-id="0f025-125">Get log details</span></span>
<span data-ttu-id="0f025-126">Vous pouvez filtrer par Période et État pour afficher les journaux pour votre tâche.</span><span class="sxs-lookup"><span data-stu-id="0f025-126">You can filter by Time Range and Status to view the logs for your job.</span></span>

<span data-ttu-id="0f025-127">Dans le portail de gestion Azure, cliquez sur le bouton **Détails** au bas de la fenêtre pour afficher plus de détails sur un événement sélectionné.</span><span class="sxs-lookup"><span data-stu-id="0f025-127">In the Azure Management portal, click on the **Details** button at the bottom of the window to view more details about a selected event.</span></span> 

  ![Sélection des détails](./media/stream-analytics-operation-logs/03-stream-analytics-operation-logs.png)  

<span data-ttu-id="0f025-129">Dans le portail Azure, cliquez sur une entrée de journal pour afficher le détail des événements.</span><span class="sxs-lookup"><span data-stu-id="0f025-129">In the Azure portal, click on a log entry to see the detailed events inside it.</span></span>

  ![Sélection des détails dans le portail Azure](./media/stream-analytics-operation-logs/08-stream-analytics-operation-logs.png)  

<span data-ttu-id="0f025-131">À partir de là, vous pouvez ouvrir le panneau **Détail** en cliquant sur l’événement.</span><span class="sxs-lookup"><span data-stu-id="0f025-131">From there, you can open the **Detail** blade by clicking on the event.</span></span>

  ![Sélection des détails dans le portail Azure](./media/stream-analytics-operation-logs/09-stream-analytics-operation-logs.png)  

## <a name="debug-a-failed-job"></a><span data-ttu-id="0f025-133">Débogage d’une tâche ayant échoué</span><span class="sxs-lookup"><span data-stu-id="0f025-133">Debug a failed job</span></span>
<span data-ttu-id="0f025-134">Dans le portail de gestion Azure, cliquez sur l’icône Rechercher et tapez « échoué ».</span><span class="sxs-lookup"><span data-stu-id="0f025-134">In the Azure Management portal, click on the Search icon and type ‘failed’.</span></span> <span data-ttu-id="0f025-135">Vous obtenez comme résultat tous les journaux avec des erreurs.</span><span class="sxs-lookup"><span data-stu-id="0f025-135">This gives a result of all logs with failures.</span></span> 

  ![Débogage d'une tâche ayant échoué](./media/stream-analytics-operation-logs/04-stream-analytics-operation-logs.png)  

<span data-ttu-id="0f025-137">Dans le portail Azure, vous pouvez filtrer par niveau de message pour afficher les événements **Critiques** .</span><span class="sxs-lookup"><span data-stu-id="0f025-137">In the Azure portal, you can filter by level of message to view **Critical** events.</span></span>

  ![Débogage du portail Azure](./media/stream-analytics-operation-logs/10-stream-analytics-operation-logs.png)  

<span data-ttu-id="0f025-139">Vous pouvez sélectionner l’une des erreurs et cliquer sur **Détails** pour obtenir plus d’informations sur l’erreur.</span><span class="sxs-lookup"><span data-stu-id="0f025-139">You can select any one of the failures, and click on the **Details** for more information on the error.</span></span>  <span data-ttu-id="0f025-140">Certains messages d’erreur fournissent également des informations sur la façon d’atténuer le problème.</span><span class="sxs-lookup"><span data-stu-id="0f025-140">Some error messages also provide information about how to mitigate the issue.</span></span> 

  ![Détails de l'opération](./media/stream-analytics-operation-logs/05-stream-analytics-operation-logs.png)  

<span data-ttu-id="0f025-142">Si vous devez contacter le [support technique](https://azure.microsoft.com/support/options/) ou fournir des informations à l’équipe par le biais du [forum MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics), notez les détails de l’opération, en particulier l’**ID de corrélation**.</span><span class="sxs-lookup"><span data-stu-id="0f025-142">In case you need to contact [Support](https://azure.microsoft.com/support/options/) or provide information to the team via the [MSDN forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics), please note the Operation Details, specifically the **Correlation ID**.</span></span> 

## <a name="get-help"></a><span data-ttu-id="0f025-143">Obtenir de l'aide</span><span class="sxs-lookup"><span data-stu-id="0f025-143">Get help</span></span>
<span data-ttu-id="0f025-144">Pour obtenir une assistance, essayez notre [forum Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="0f025-144">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="0f025-145">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0f025-145">Next steps</span></span>
* [<span data-ttu-id="0f025-146">Présentation d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="0f025-146">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="0f025-147">Prise en main d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="0f025-147">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="0f025-148">Mise à l'échelle des travaux Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="0f025-148">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="0f025-149">Références sur le langage des requêtes d'Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="0f025-149">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="0f025-150">Références sur l’API REST de gestion d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="0f025-150">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

