---
title: "aaaHow toocreate un travail de traitement de données analytique pour les flux de données Analytique | Documents Microsoft"
description: "Créer une tâche de traitement d’analyse de données pour Stream Analytics | segment du parcours d’apprentissage."
keywords: "traitement d’analyse de données"
documentationcenter: 
services: stream-analytics
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: e825fbcf-69e9-443f-b402-3b7a4568f415
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: d4a3c89d8862d59688d06a1719b063efa2ab1c93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-data-analytics-processing-job-for-stream-analytics"></a><span data-ttu-id="6dec9-104">Comment toocreate un traitement analytique des données de la tâche de flux de données Analytique</span><span class="sxs-lookup"><span data-stu-id="6dec9-104">How toocreate a data analytics processing job for Stream Analytics</span></span>
<span data-ttu-id="6dec9-105">ressources de niveau supérieur Hello dans Analytique de flux de données Azure est une tâche Analytique de flux de données.</span><span class="sxs-lookup"><span data-stu-id="6dec9-105">hello top-level resource in Azure Stream Analytics is a Stream Analytics Job.</span></span>  <span data-ttu-id="6dec9-106">Il se compose d’une ou plusieurs d’entrée à des sources de données, une requête exprimant la transformation de données hello et une ou plusieurs cibles de sortie qui sont écrits dans.</span><span class="sxs-lookup"><span data-stu-id="6dec9-106">It consists of one or more input data sources, a query expressing hello data transformation, and one or more output targets that results are written to.</span></span> <span data-ttu-id="6dec9-107">Ensemble, ces activer analytique de données hello utilisateur tooperform scénarios de traitement des données de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="6dec9-107">Together these enable hello user tooperform data analytics processing for streaming data scenarios.</span></span>

<span data-ttu-id="6dec9-108">toostart à l’aide de flux de données Analytique, commencez par créer une nouvelle tâche de flux de données Analytique.</span><span class="sxs-lookup"><span data-stu-id="6dec9-108">toostart using Stream Analytics, begin by creating a new Stream Analytics job.</span></span>  <span data-ttu-id="6dec9-109">Notez que cette action n’a aucune incidence facturation jusqu'à ce que la tâche hello est démarrée.</span><span class="sxs-lookup"><span data-stu-id="6dec9-109">Note this action has no billing implications until hello job is started.</span></span>

1. <span data-ttu-id="6dec9-110">Connectez-vous à hello en ligne [portail Azure classic](http://manage.windowsazure.com) ou hello [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="6dec9-110">Sign in on hello online [Azure classic portal](http://manage.windowsazure.com) or hello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="6dec9-111">Dans le portail de hello : **cliquez sur Nouveau**, puis cliquez sur **Data Services** ou **données Analytique** en fonction de votre portail et le puis cliquez sur **Analytique de flux de données Azure** ou **flux Analytique** , puis **création rapide**.</span><span class="sxs-lookup"><span data-stu-id="6dec9-111">In hello portal: **Click New**, then click **Data Services** or **Data Analytics** depending on your portal and then click **Azure Stream Analytics** or **Stream Analytics** and then **Quick Create**.</span></span>
   
   ![Assistant Tâche de traitement d’analyse de données](./media/stream-analytics-create-a-job/1-stream-analytics-create-a-job.png)  
   
   ![Créer une tâche de traitement d’analyse de données](./media/stream-analytics-create-a-job/4-stream-analytics-create-a-job.png)  
3. <span data-ttu-id="6dec9-114">Spécifiez la configuration souhaitée de hello de la tâche de flux de données Analytique de hello.</span><span class="sxs-lookup"><span data-stu-id="6dec9-114">Specify hello desired configuration for hello Stream Analytics job.</span></span>
   
   * <span data-ttu-id="6dec9-115">Bonjour **nom de la tâche** , entrez un nom tooidentify hello Analytique de flux du travail.</span><span class="sxs-lookup"><span data-stu-id="6dec9-115">In hello **Job Name** box, enter a name tooidentify hello Stream Analytics job.</span></span> <span data-ttu-id="6dec9-116">Hello lorsque **nom de la tâche** est validé, une coche verte s’affiche dans la zone de nom de la tâche hello.</span><span class="sxs-lookup"><span data-stu-id="6dec9-116">When hello **Job Name** is validated, a green check mark appears in hello Job Name box.</span></span> <span data-ttu-id="6dec9-117">Hello **nom de la tâche** peuvent uniquement contenir des caractères alphanumériques et hello '-' caractère et doit être comprise entre 3 et 63 caractères.</span><span class="sxs-lookup"><span data-stu-id="6dec9-117">hello **Job Name** may contain only alphanumeric characters and hello '-' character, and must be between 3 and 63 characters.</span></span>
   * <span data-ttu-id="6dec9-118">Utilisez **région** Bonjour portail Azure ou **emplacement** Bonjour Azure toospecify portail hello emplacement géographique où vous souhaitez que le travail de hello de toorun.</span><span class="sxs-lookup"><span data-stu-id="6dec9-118">Use **Region** in hello Azure portal or **Location** in hello Azure portal toospecify hello geographic location where you want toorun hello job.</span></span>
   * <span data-ttu-id="6dec9-119">Si à l’aide de hello le portail Azure, sélectionnez ou créez un toouse de compte de stockage comme hello **compte de stockage de surveillance régionale**.</span><span class="sxs-lookup"><span data-stu-id="6dec9-119">If using hello Azure portal, select or create a storage account toouse as hello **Regional Monitoring Storage Account**.</span></span> <span data-ttu-id="6dec9-120">Ce compte de stockage est utilisé toostore données d’analyse de toutes les tâches de flux de données Analytique en cours d’exécution dans cette région.</span><span class="sxs-lookup"><span data-stu-id="6dec9-120">This storage account is used toostore monitoring data for all Stream Analytics jobs running in this region.</span></span>
   * <span data-ttu-id="6dec9-121">Si à l’aide de hello le portail Azure, spécifiez un nouveau ou existant **groupe de ressources** toohold liés des ressources pour votre application.</span><span class="sxs-lookup"><span data-stu-id="6dec9-121">If using hello Azure portal, specify a new or existing **Resource Group** toohold related resources for your application.</span></span>
4. <span data-ttu-id="6dec9-122">Une fois les nouvelles options de tâche de flux Analytique hello sont configurées, cliquez sur **créer une tâche de flux de données Analytique**.</span><span class="sxs-lookup"><span data-stu-id="6dec9-122">Once hello new Stream Analytics job options are configured, click **Create Stream Analytics Job**.</span></span> <span data-ttu-id="6dec9-123">Il peut prendre quelques minutes pour hello flux Analytique travail toobe est créé.</span><span class="sxs-lookup"><span data-stu-id="6dec9-123">It can take a few minutes for hello Stream Analytics job toobe created.</span></span> <span data-ttu-id="6dec9-124">état de hello toocheck, vous pouvez surveiller la progression de hello dans hub de Notifications hello.</span><span class="sxs-lookup"><span data-stu-id="6dec9-124">toocheck hello status, you can monitor hello progress in hello Notifications hub.</span></span>
   
   ![Hub de notification des tâches de traitement d’analyse de données](./media/stream-analytics-create-a-job/2-stream-analytics-create-a-job.png)  
   
   ![Créer une tâche de traitement d’analyse de données dans le portail Azure](./media/stream-analytics-create-a-job/5-stream-analytics-create-a-job.png)  
5. <span data-ttu-id="6dec9-127">nouvelle tâche de Hello présentent l’état de **créé**.</span><span class="sxs-lookup"><span data-stu-id="6dec9-127">hello new job will show a status of **Created**.</span></span> <span data-ttu-id="6dec9-128">Notez que hello **Démarrer** bouton est désactivé.</span><span class="sxs-lookup"><span data-stu-id="6dec9-128">Notice that hello **Start** button is disabled.</span></span> <span data-ttu-id="6dec9-129">Configurer hello travail entrée, de requête et de sortie avant de démarrer le travail de hello.</span><span class="sxs-lookup"><span data-stu-id="6dec9-129">Configure hello job input, query, and output before you start hello job.</span></span>
   
   ![Statut de la tâche de traitement d’analyse de données](./media/stream-analytics-create-a-job/3-stream-analytics-create-a-job.png)  
   
   ![Statut de la tâche de traitement d’analyse de données dans le portail Azure](./media/stream-analytics-create-a-job/6-stream-analytics-create-a-job.png)  

## <a name="get-help"></a><span data-ttu-id="6dec9-132">Obtenir de l’aide</span><span class="sxs-lookup"><span data-stu-id="6dec9-132">Get help</span></span>
<span data-ttu-id="6dec9-133">Pour obtenir une assistance, essayez notre [forum Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="6dec9-133">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="6dec9-134">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6dec9-134">Next steps</span></span>
* [<span data-ttu-id="6dec9-135">Introduction tooAzure Analytique de flux de données</span><span class="sxs-lookup"><span data-stu-id="6dec9-135">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="6dec9-136">Prise en main d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="6dec9-136">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="6dec9-137">Mise à l'échelle des travaux Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="6dec9-137">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="6dec9-138">Références sur le langage des requêtes d'Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="6dec9-138">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="6dec9-139">Références sur l’API REST de gestion d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="6dec9-139">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

