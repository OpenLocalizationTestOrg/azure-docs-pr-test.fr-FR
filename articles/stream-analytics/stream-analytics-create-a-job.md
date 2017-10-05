---
title: "Guide pratique pour créer un travail de traitement d’analyse de données pour Stream Analytics | Microsoft Docs"
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
ms.openlocfilehash: 05fdf1e20efd129cdfc27e1d37bc9e124edf5dcd
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-create-a-data-analytics-processing-job-for-stream-analytics"></a><span data-ttu-id="538a0-104">Comment créer une tâche de traitement d’analyse de données pour Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="538a0-104">How to create a data analytics processing job for Stream Analytics</span></span>
<span data-ttu-id="538a0-105">La ressource de niveau supérieur dans Azure Stream Analytics est une tâche Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="538a0-105">The top-level resource in Azure Stream Analytics is a Stream Analytics Job.</span></span>  <span data-ttu-id="538a0-106">Elle se compose d'une ou plusieurs sources de données d'entrée, une requête exprimant la transformation de données et une ou plusieurs cibles de sortie où les résultats sont écrits.</span><span class="sxs-lookup"><span data-stu-id="538a0-106">It consists of one or more input data sources, a query expressing the data transformation, and one or more output targets that results are written to.</span></span> <span data-ttu-id="538a0-107">Ensemble, ces éléments permettent à l’utilisateur de traiter l’analyse des données dans différents scénarios de données de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="538a0-107">Together these enable the user to perform data analytics processing for streaming data scenarios.</span></span>

<span data-ttu-id="538a0-108">Pour utiliser Stream Analytics, commencez par créer une tâche Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="538a0-108">To start using Stream Analytics, begin by creating a new Stream Analytics job.</span></span>  <span data-ttu-id="538a0-109">Notez que cette action n'a aucune incidence de facturation tant que la tâche n'a pas démarré.</span><span class="sxs-lookup"><span data-stu-id="538a0-109">Note this action has no billing implications until the job is started.</span></span>

1. <span data-ttu-id="538a0-110">Connectez-vous au [portail Azure Classic](http://manage.windowsazure.com) en ligne ou au [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="538a0-110">Sign in on the online [Azure classic portal](http://manage.windowsazure.com) or the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="538a0-111">Dans le portail : cliquez successivement sur **Nouveau**, sur **Data Services** ou **Data Analytics** (selon votre portail), sur **Azure Stream Analytics** ou **Stream Analytics**, puis sur **Création rapide**.</span><span class="sxs-lookup"><span data-stu-id="538a0-111">In the portal: **Click New**, then click **Data Services** or **Data Analytics** depending on your portal and then click **Azure Stream Analytics** or **Stream Analytics** and then **Quick Create**.</span></span>
   
   ![Assistant Tâche de traitement d’analyse de données](./media/stream-analytics-create-a-job/1-stream-analytics-create-a-job.png)  
   
   ![Créer une tâche de traitement d’analyse de données](./media/stream-analytics-create-a-job/4-stream-analytics-create-a-job.png)  
3. <span data-ttu-id="538a0-114">Spécifiez la configuration souhaitée pour la tâche Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="538a0-114">Specify the desired configuration for the Stream Analytics job.</span></span>
   
   * <span data-ttu-id="538a0-115">Dans la zone **Nom de la tâche** , entrez un nom pour identifier la tâche Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="538a0-115">In the **Job Name** box, enter a name to identify the Stream Analytics job.</span></span> <span data-ttu-id="538a0-116">Une fois le **nom de la tâche** validé, une coche verte s’affiche dans la zone Nom de la tâche.</span><span class="sxs-lookup"><span data-stu-id="538a0-116">When the **Job Name** is validated, a green check mark appears in the Job Name box.</span></span> <span data-ttu-id="538a0-117">Le **Nom de la tâche** ne peut contenir que des caractères alphanumériques et le caractère « - », et doit compter entre 3 et 63 caractères.</span><span class="sxs-lookup"><span data-stu-id="538a0-117">The **Job Name** may contain only alphanumeric characters and the '-' character, and must be between 3 and 63 characters.</span></span>
   * <span data-ttu-id="538a0-118">Utilisez **Région** dans le portail Azure ou **Emplacement** dans le portail Azure pour spécifier l’emplacement géographique où vous souhaitez exécuter le travail.</span><span class="sxs-lookup"><span data-stu-id="538a0-118">Use **Region** in the Azure portal or **Location** in the Azure portal to specify the geographic location where you want to run the job.</span></span>
   * <span data-ttu-id="538a0-119">Si vous utilisez le portail Azure, sélectionnez ou créez un compte de stockage à utiliser comme **Compte de stockage de surveillance régionale**.</span><span class="sxs-lookup"><span data-stu-id="538a0-119">If using the Azure portal, select or create a storage account to use as the **Regional Monitoring Storage Account**.</span></span> <span data-ttu-id="538a0-120">Ce compte de stockage est utilisé pour stocker les données de surveillance de toutes les tâches Stream Analytics en cours d'exécution dans cette région.</span><span class="sxs-lookup"><span data-stu-id="538a0-120">This storage account is used to store monitoring data for all Stream Analytics jobs running in this region.</span></span>
   * <span data-ttu-id="538a0-121">Si vous utilisez le portail Azure, indiquez un **groupe de ressources** nouveau ou existant contenant les ressources associées à votre application.</span><span class="sxs-lookup"><span data-stu-id="538a0-121">If using the Azure portal, specify a new or existing **Resource Group** to hold related resources for your application.</span></span>
4. <span data-ttu-id="538a0-122">Une fois les options de la nouvelle tâche Stream Analytics configurées, cliquez sur **Créer une tâche Stream Analytics**.</span><span class="sxs-lookup"><span data-stu-id="538a0-122">Once the new Stream Analytics job options are configured, click **Create Stream Analytics Job**.</span></span> <span data-ttu-id="538a0-123">La création de la tâche Stream Analytics peut prendre plusieurs minutes.</span><span class="sxs-lookup"><span data-stu-id="538a0-123">It can take a few minutes for the Stream Analytics job to be created.</span></span> <span data-ttu-id="538a0-124">Pour vérifier l'état, vous pouvez suivre l'avancement dans le hub de notifications.</span><span class="sxs-lookup"><span data-stu-id="538a0-124">To check the status, you can monitor the progress in the Notifications hub.</span></span>
   
   ![Hub de notification des tâches de traitement d’analyse de données](./media/stream-analytics-create-a-job/2-stream-analytics-create-a-job.png)  
   
   ![Créer une tâche de traitement d’analyse de données dans le portail Azure](./media/stream-analytics-create-a-job/5-stream-analytics-create-a-job.png)  
5. <span data-ttu-id="538a0-127">Le nouveau travail est affiché avec l’état **Créé**.</span><span class="sxs-lookup"><span data-stu-id="538a0-127">The new job will show a status of **Created**.</span></span> <span data-ttu-id="538a0-128">Notez que le bouton **Démarrer** est désactivé.</span><span class="sxs-lookup"><span data-stu-id="538a0-128">Notice that the **Start** button is disabled.</span></span> <span data-ttu-id="538a0-129">Avant de pouvoir démarrer la tâche, vous devez configurer son entrée, sa requête et sa sortie.</span><span class="sxs-lookup"><span data-stu-id="538a0-129">Configure the job input, query, and output before you start the job.</span></span>
   
   ![Statut de la tâche de traitement d’analyse de données](./media/stream-analytics-create-a-job/3-stream-analytics-create-a-job.png)  
   
   ![Statut de la tâche de traitement d’analyse de données dans le portail Azure](./media/stream-analytics-create-a-job/6-stream-analytics-create-a-job.png)  

## <a name="get-help"></a><span data-ttu-id="538a0-132">Obtenir de l’aide</span><span class="sxs-lookup"><span data-stu-id="538a0-132">Get help</span></span>
<span data-ttu-id="538a0-133">Pour obtenir une assistance, essayez notre [forum Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="538a0-133">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="538a0-134">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="538a0-134">Next steps</span></span>
* [<span data-ttu-id="538a0-135">Présentation d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="538a0-135">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="538a0-136">Prise en main d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="538a0-136">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="538a0-137">Mise à l'échelle des travaux Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="538a0-137">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="538a0-138">Références sur le langage des requêtes d'Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="538a0-138">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="538a0-139">Références sur l’API REST de gestion d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="538a0-139">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

