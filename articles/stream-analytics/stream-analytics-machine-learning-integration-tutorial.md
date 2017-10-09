---
title: "intégration de flux de données Analytique et l’apprentissage d’aaaAzure | Documents Microsoft"
description: "Comment toouse un apprentissage automatique dans une tâche de flux de données Analytique et la fonction définie par l’utilisateur"
keywords: 
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: cfced01f-ccaa-4bc6-81e2-c03d1470a7a2
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 07/06/2017
ms.author: jeffstok
ms.openlocfilehash: e1ba7ab51ece80719839793e1320a7666cfc4181
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="performing-sentiment-analysis-by-using-azure-stream-analytics-and-azure-machine-learning"></a><span data-ttu-id="93c64-103">Analyse des sentiments à l’aide d’Azure Stream Analytics et Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="93c64-103">Performing sentiment analysis by using Azure Stream Analytics and Azure Machine Learning</span></span>
<span data-ttu-id="93c64-104">Cet article décrit comment tooquickly configurer une tâche Analytique de flux de données Azure simple qui s’intègre à Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="93c64-104">This article describes how tooquickly set up a simple Azure Stream Analytics job that integrates Azure Machine Learning.</span></span> <span data-ttu-id="93c64-105">Vous utilisez un modèle d’analytique sentiment Machine Learning à partir de hello données texte diffusion en continu de la galerie de Cortana Intelligence tooanalyze et déterminez le score d’opinion hello en temps réel.</span><span class="sxs-lookup"><span data-stu-id="93c64-105">You use a Machine Learning sentiment analytics model from hello Cortana Intelligence Gallery tooanalyze streaming text data and determine hello sentiment score in real time.</span></span> <span data-ttu-id="93c64-106">Hello Cortana Intelligence Suite vous permet de procéder sans vous soucier des complexités hello de la création d’un modèle d’analytique sentiments.</span><span class="sxs-lookup"><span data-stu-id="93c64-106">Using hello Cortana Intelligence Suite lets you accomplish this task without worrying about hello intricacies of building a sentiment analytics model.</span></span>

<span data-ttu-id="93c64-107">Vous pouvez appliquer ce que vous apprenez à partir de cette tooscenarios article telles que celles-ci :</span><span class="sxs-lookup"><span data-stu-id="93c64-107">You can apply what you learn from this article tooscenarios such as these:</span></span>

* <span data-ttu-id="93c64-108">Analyse des sentiments en temps réel sur la diffusion de données Twitter en continu.</span><span class="sxs-lookup"><span data-stu-id="93c64-108">Analyzing real-time sentiment on streaming Twitter data.</span></span>
* <span data-ttu-id="93c64-109">Analyse des enregistrements de conversations de clients avec le personnel de support.</span><span class="sxs-lookup"><span data-stu-id="93c64-109">Analyzing records of customer chats with support staff.</span></span>
* <span data-ttu-id="93c64-110">Évaluation des commentaires sur les forums, blogs et vidéos.</span><span class="sxs-lookup"><span data-stu-id="93c64-110">Evaluating comments on forums, blogs, and videos.</span></span> 
* <span data-ttu-id="93c64-111">Nombreux autres scénarios de notation prédictive en temps réel.</span><span class="sxs-lookup"><span data-stu-id="93c64-111">Many other real-time, predictive scoring scenarios.</span></span>

<span data-ttu-id="93c64-112">Dans un scénario réel, vous pourriez obtenir des données de salutation directement à partir d’un flux de données Twitter.</span><span class="sxs-lookup"><span data-stu-id="93c64-112">In a real-world scenario, you would get hello data directly from a Twitter data stream.</span></span> <span data-ttu-id="93c64-113">toosimplify hello didacticiel, nous avons écrit il afin que hello Analytique de diffusion en continu travail obtient tweet à partir d’un fichier CSV dans le stockage d’objets Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="93c64-113">toosimplify hello tutorial, we've written it so that hello Streaming Analytics job gets tweets from a CSV file in Azure Blob storage.</span></span> <span data-ttu-id="93c64-114">Vous pouvez créer votre propre fichier CSV, ou vous pouvez utiliser un exemple de fichier CSV, comme indiqué dans hello suivant image :</span><span class="sxs-lookup"><span data-stu-id="93c64-114">You can create your own CSV file, or you can use a sample CSV file, as shown in hello following image:</span></span>

![exemples de tweets dans un fichier CSV](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-figure-2.png)  

<span data-ttu-id="93c64-116">travail de diffusion en continu d’Analytique Hello que vous créez s’applique modèle d’analytique hello sentiment comme une fonction définie par l’utilisateur (UDF) sur les données texte hello à partir du magasin d’objets blob hello.</span><span class="sxs-lookup"><span data-stu-id="93c64-116">hello Streaming Analytics job that you create applies hello sentiment analytics model as a user-defined function (UDF) on hello sample text data from hello blob store.</span></span> <span data-ttu-id="93c64-117">sortie de Hello (résultat hello d’analyse des sentiments hello) est écrit toohello même magasin d’objets blob dans un autre fichier CSV.</span><span class="sxs-lookup"><span data-stu-id="93c64-117">hello output (hello result of hello sentiment analysis) is written toohello same blob store in a different CSV file.</span></span> 

<span data-ttu-id="93c64-118">Hello figure suivante illustre cette configuration.</span><span class="sxs-lookup"><span data-stu-id="93c64-118">hello following figure demonstrates this configuration.</span></span> <span data-ttu-id="93c64-119">Comme nous l’avons indiqué, pour un scénario plus réaliste, vous pouvez remplacer le stockage d’objets blob par la diffusion de données Twitter en continu à partir d’une entrée Event Hub Azure.</span><span class="sxs-lookup"><span data-stu-id="93c64-119">As noted, for a more realistic scenario, you can replace blob storage with streaming Twitter data from an Azure Event Hubs input.</span></span> <span data-ttu-id="93c64-120">En outre, vous pouvez générer un [Microsoft Power BI](https://powerbi.microsoft.com/) visualisation en temps réel de sentiment d’agrégation de hello.</span><span class="sxs-lookup"><span data-stu-id="93c64-120">Additionally, you could build a [Microsoft Power BI](https://powerbi.microsoft.com/) real-time visualization of hello aggregate sentiment.</span></span>    

![Vue d’ensemble de l’intégration de Machine Learning dans Stream Analytics](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-figure-1.png)  

## <a name="prerequisites"></a><span data-ttu-id="93c64-122">Composants requis</span><span class="sxs-lookup"><span data-stu-id="93c64-122">Prerequisites</span></span>
<span data-ttu-id="93c64-123">Avant de commencer, assurez-vous que vous avez hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="93c64-123">Before you start, make sure you have hello following:</span></span>

* <span data-ttu-id="93c64-124">Un abonnement Azure actif.</span><span class="sxs-lookup"><span data-stu-id="93c64-124">An active Azure subscription.</span></span>
* <span data-ttu-id="93c64-125">Un fichier CSV contenant des données.</span><span class="sxs-lookup"><span data-stu-id="93c64-125">A CSV file with some data in it.</span></span> <span data-ttu-id="93c64-126">Vous pouvez télécharger le fichier hello présentée précédemment à partir de [GitHub](https://github.com/Azure/azure-stream-analytics/blob/master/Sample%20Data/sampleinput.csv), ou vous pouvez créer votre propre fichier.</span><span class="sxs-lookup"><span data-stu-id="93c64-126">You can download hello file shown earlier from [GitHub](https://github.com/Azure/azure-stream-analytics/blob/master/Sample%20Data/sampleinput.csv), or you can create your own file.</span></span> <span data-ttu-id="93c64-127">Pour cet article, nous supposons que vous utilisez le fichier hello à partir de GitHub.</span><span class="sxs-lookup"><span data-stu-id="93c64-127">For this article, we assume that you're using hello file from GitHub.</span></span>

<span data-ttu-id="93c64-128">À un niveau élevé, les tâches hello toocomplete présentés dans cet article, vous hello suivant :</span><span class="sxs-lookup"><span data-stu-id="93c64-128">At a high level, toocomplete hello tasks demonstrated in this article, you do hello following:</span></span>

1. <span data-ttu-id="93c64-129">Créer un compte de stockage Azure et un conteneur de stockage d’objets blob et télécharger un conteneur de toohello du fichier d’entrée au format CSV.</span><span class="sxs-lookup"><span data-stu-id="93c64-129">Create an Azure storage account and a blob storage container, and upload a CSV-formatted input file toohello container.</span></span>
3. <span data-ttu-id="93c64-130">Ajouter un modèle d’analytique sentiment à partir de l’espace de travail Azure Machine Learning hello Cortana Intelligence galerie tooyour et déployer ce modèle en tant qu’un service web dans l’espace de travail Machine Learning hello.</span><span class="sxs-lookup"><span data-stu-id="93c64-130">Add a sentiment analytics model from hello Cortana Intelligence Gallery tooyour Azure Machine Learning workspace and deploy this model as a web service in hello Machine Learning workspace.</span></span>
5. <span data-ttu-id="93c64-131">Créer une tâche de flux de données Analytique qui appelle ce service web en fonction de l’opinion de toodetermine de commande pour l’entrée de texte hello.</span><span class="sxs-lookup"><span data-stu-id="93c64-131">Create a Stream Analytics job that calls this web service as a function in order toodetermine sentiment for hello text input.</span></span>
6. <span data-ttu-id="93c64-132">Démarrer la tâche de flux de données Analytique hello et vérifier la sortie de hello.</span><span class="sxs-lookup"><span data-stu-id="93c64-132">Start hello Stream Analytics job and check hello output.</span></span>

## <a name="create-a-storage-container-and-upload-hello-csv-input-file"></a><span data-ttu-id="93c64-133">Créer un conteneur de stockage et de télécharger un fichier d’entrée CSV hello</span><span class="sxs-lookup"><span data-stu-id="93c64-133">Create a storage container and upload hello CSV input file</span></span>
<span data-ttu-id="93c64-134">Pour cette étape, vous pouvez utiliser n’importe quel fichier CSV, par exemple hello disponible à partir de GitHub.</span><span class="sxs-lookup"><span data-stu-id="93c64-134">For this step, you can use any CSV file, such as hello one available from GitHub.</span></span>

1. <span data-ttu-id="93c64-135">Bonjour portail Azure, cliquez sur **nouveau** &gt; **stockage** &gt; **compte de stockage**.</span><span class="sxs-lookup"><span data-stu-id="93c64-135">In hello Azure portal, click **New** &gt; **Storage** &gt; **Storage account**.</span></span>

   ![créer un compte de stockage](./media/stream-analytics-machine-learning-integration-tutorial/azure-portal-create-storage-account.png)

2. <span data-ttu-id="93c64-137">Fournissez un nom (`samldemo` dans l’exemple de hello).</span><span class="sxs-lookup"><span data-stu-id="93c64-137">Provide a name (`samldemo` in hello example).</span></span> <span data-ttu-id="93c64-138">nom de Hello peut utiliser que des lettres minuscules et des chiffres, et il doit être unique dans Azure.</span><span class="sxs-lookup"><span data-stu-id="93c64-138">hello name can use only lowercase letters and numbers, and it must be unique across Azure.</span></span> 

3. <span data-ttu-id="93c64-139">Spécifiez un groupe de ressources existant et un emplacement.</span><span class="sxs-lookup"><span data-stu-id="93c64-139">Specify an existing resource group and specify a location.</span></span> <span data-ttu-id="93c64-140">Pour l’emplacement, nous recommandons que toutes les ressources hello créés dans ce didacticiel, utilisez hello même emplacement.</span><span class="sxs-lookup"><span data-stu-id="93c64-140">For location, we recommend that all hello resources created in this tutorial use hello same location.</span></span>

    ![indiquer les détails du compte de stockage](./media/stream-analytics-machine-learning-integration-tutorial/create-sa1.png)

4. <span data-ttu-id="93c64-142">Bonjour portail Azure, sélectionnez le compte de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="93c64-142">In hello Azure portal, select hello storage account.</span></span> <span data-ttu-id="93c64-143">Dans le panneau de compte de stockage hello, cliquez sur **conteneurs** puis cliquez sur  **+ &nbsp;conteneur** toocreate stockage d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="93c64-143">In hello storage account blade, click **Containers** and then click **+&nbsp;Container** toocreate blob storage.</span></span>

    ![créer un conteneur d’objets blob](./media/stream-analytics-machine-learning-integration-tutorial/create-sa2.png)

5. <span data-ttu-id="93c64-145">Fournissez un nom pour le conteneur de hello (`azuresamldemoblob` dans l’exemple de hello) et vérifiez que **type d’accès** est défini trop**Blob**.</span><span class="sxs-lookup"><span data-stu-id="93c64-145">Provide a name for hello container (`azuresamldemoblob` in hello example) and verify that **Access type** is set too**Blob**.</span></span> <span data-ttu-id="93c64-146">Quand vous avez terminé, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="93c64-146">When you're done, click **OK**.</span></span>

    ![spécifier les détails du conteneur d’objets blob](./media/stream-analytics-machine-learning-integration-tutorial/create-sa3.png)

6. <span data-ttu-id="93c64-148">Bonjour **conteneurs** panneau, sélectionnez hello nouveau conteneur, qui ouvre le panneau hello pour ce conteneur.</span><span class="sxs-lookup"><span data-stu-id="93c64-148">In hello **Containers** blade, select hello new container, which opens hello blade for that container.</span></span>

7. <span data-ttu-id="93c64-149">Cliquez sur **Télécharger**.</span><span class="sxs-lookup"><span data-stu-id="93c64-149">Click **Upload**.</span></span>

    ![Bouton ’Télécharger’ d’un conteneur](./media/stream-analytics-machine-learning-integration-tutorial/create-sa-upload-button.png)

8. <span data-ttu-id="93c64-151">Bonjour **téléchargement blob** panneau, spécifiez le fichier CSV de hello que vous souhaitez toouse pour ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="93c64-151">In hello **Upload blob** blade, specify hello CSV file that you want toouse for this tutorial.</span></span> <span data-ttu-id="93c64-152">Pour **type d’objets Blob**, sélectionnez **objet blob de blocs** et ensemble hello bloc taille too4 Mo, ce qui est suffisant pour ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="93c64-152">For **Blob type**, select **Block blob** and set hello block size too4 MB, which is sufficient for this tutorial.</span></span>

    ![charger le fichier blob](./media/stream-analytics-machine-learning-integration-tutorial/create-sa4.png)

9. <span data-ttu-id="93c64-154">Cliquez sur hello **télécharger** bouton bas hello du Panneau de hello.</span><span class="sxs-lookup"><span data-stu-id="93c64-154">Click hello **Upload** button at hello bottom of hello blade.</span></span>

## <a name="add-hello-sentiment-analytics-model-from-hello-cortana-intelligence-gallery"></a><span data-ttu-id="93c64-155">Ajouter un modèle d’analytique de sentiment hello de hello Cortana Intelligence galerie</span><span class="sxs-lookup"><span data-stu-id="93c64-155">Add hello sentiment analytics model from hello Cortana Intelligence Gallery</span></span>

<span data-ttu-id="93c64-156">Maintenant que les données d’exemple hello sont dans un objet blob, vous pouvez activer le modèle d’analyse de sentiments hello dans Cortana Intelligence galerie.</span><span class="sxs-lookup"><span data-stu-id="93c64-156">Now that hello sample data is in a blob, you can enable hello sentiment analysis model in Cortana Intelligence Gallery.</span></span>

1. <span data-ttu-id="93c64-157">Accédez toohello [modèle analytique de sentiment prédictive](https://gallery.cortanaintelligence.com/Experiment/Predictive-Mini-Twitter-sentiment-analysis-Experiment-1) page Bonjour Cortana Intelligence galerie.</span><span class="sxs-lookup"><span data-stu-id="93c64-157">Go toohello [predictive sentiment analytics model](https://gallery.cortanaintelligence.com/Experiment/Predictive-Mini-Twitter-sentiment-analysis-Experiment-1) page in hello Cortana Intelligence Gallery.</span></span>  

2. <span data-ttu-id="93c64-158">Cliquez sur **Ouvrir dans Studio**.</span><span class="sxs-lookup"><span data-stu-id="93c64-158">Click **Open in Studio**.</span></span>  
   
   ![Stream Analytics Machine Learning, ouvrir Machine Learning Studio](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-open-ml-studio.png)  

3. <span data-ttu-id="93c64-160">Espace de travail toogo toohello vous connecter.</span><span class="sxs-lookup"><span data-stu-id="93c64-160">Sign in toogo toohello workspace.</span></span> <span data-ttu-id="93c64-161">Sélectionnez un emplacement.</span><span class="sxs-lookup"><span data-stu-id="93c64-161">Select a location.</span></span>

4. <span data-ttu-id="93c64-162">Cliquez sur **exécuter** bas hello de page de hello.</span><span class="sxs-lookup"><span data-stu-id="93c64-162">Click **Run** at hello bottom of hello page.</span></span> <span data-ttu-id="93c64-163">processus de Hello s’exécute, ce qui dure environ une minute.</span><span class="sxs-lookup"><span data-stu-id="93c64-163">hello process runs, which takes about a minute.</span></span>

   ![exécuter une expérience dans Machine Learning Studio](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-run-experiment.png)  

5. <span data-ttu-id="93c64-165">Une fois le processus de hello s’est exécutée correctement, sélectionnez **déployer le Service Web** bas hello de page de hello.</span><span class="sxs-lookup"><span data-stu-id="93c64-165">After hello process has run successfully, select **Deploy Web Service** at hello bottom of hello page.</span></span>

   ![déployer l’expérience dans Machine Learning Studio en tant que service web](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-deploy-web-service.png)  

6. <span data-ttu-id="93c64-167">toovalidate qui hello sentiment modèle d’analytique est toouse prêt, cliquez sur hello **Test** bouton.</span><span class="sxs-lookup"><span data-stu-id="93c64-167">toovalidate that hello sentiment analytics model is ready toouse, click hello **Test** button.</span></span> <span data-ttu-id="93c64-168">Entrez du texte, par exemple « I love Microsoft ».</span><span class="sxs-lookup"><span data-stu-id="93c64-168">Provide text input such as "I love Microsoft".</span></span> 

   ![tester une expérience dans Machine Learning Studio](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-test.png)  

    <span data-ttu-id="93c64-170">Si le test de hello fonctionne, vous consultez un toohello comme résultat l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="93c64-170">If hello test works, you see a result similar toohello following example:</span></span>

   ![résultats du test dans Machine Learning Studio](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-test-results.png)  

7. <span data-ttu-id="93c64-172">Bonjour **applications** colonne, cliquez sur hello **Excel 2010 ou classeur antérieur** toodownload de lien un classeur Excel.</span><span class="sxs-lookup"><span data-stu-id="93c64-172">In hello **Apps** column, click hello **Excel 2010 or earlier workbook** link toodownload an Excel workbook.</span></span> <span data-ttu-id="93c64-173">classeur de Hello contient clé de hello une API et l’URL de hello que vous avez besoin tooset ultérieure de la tâche de flux de données Analytique hello.</span><span class="sxs-lookup"><span data-stu-id="93c64-173">hello workbook contains hello an API key and hello URL that you need later tooset up hello Stream Analytics job.</span></span>

    ![Stream Analytics Machine Learning, aperçu rapide](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-quick-glance.png)  


## <a name="create-a-stream-analytics-job-that-uses-hello-machine-learning-model"></a><span data-ttu-id="93c64-175">Créer une tâche de flux de données Analytique qui utilise le modèle d’apprentissage hello</span><span class="sxs-lookup"><span data-stu-id="93c64-175">Create a Stream Analytics job that uses hello Machine Learning model</span></span>

<span data-ttu-id="93c64-176">Vous pouvez maintenant créer une tâche de flux Analytique qui lit hello exemple tweets d’un fichier CSV hello dans le stockage blob.</span><span class="sxs-lookup"><span data-stu-id="93c64-176">You can now create a Stream Analytics job that reads hello sample tweets from hello CSV file in blob storage.</span></span> 

### <a name="create-hello-job"></a><span data-ttu-id="93c64-177">Créer le travail de hello</span><span class="sxs-lookup"><span data-stu-id="93c64-177">Create hello job</span></span>

1. <span data-ttu-id="93c64-178">Accédez toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="93c64-178">Go toohello [Azure portal](https://portal.azure.com).</span></span>  

2. <span data-ttu-id="93c64-179">Dans le portail Azure, cliquez sur **Nouveau** > **Internet des objets** > **Travail Stream Analytics**.</span><span class="sxs-lookup"><span data-stu-id="93c64-179">Click **New** > **Internet of Things** > **Stream Analytics job**.</span></span> 

   ![Chemin d’accès au portail Azure pour obtenir la nouvelle tâche de flux de données Analytique tooa](./media/stream-analytics-machine-learning-integration-tutorial/azure-portal-new-iot-sa-job.png)
   
3. <span data-ttu-id="93c64-181">Nom du travail hello `azure-sa-ml-demo`, spécifiez un abonnement, spécifiez un groupe de ressources existant ou créez-en un et sélectionnez hello emplacement pour le travail de hello.</span><span class="sxs-lookup"><span data-stu-id="93c64-181">Name hello job `azure-sa-ml-demo`, specify a subscription, specify an existing resource group or create a new one, and select hello location for hello job.</span></span>

   ![spécifier les paramètres du nouveau travail Stream Analytics](./media/stream-analytics-machine-learning-integration-tutorial/create-job-1.png)
   

### <a name="configure-hello-job-input"></a><span data-ttu-id="93c64-183">Configurer l’entrée de tâche hello</span><span class="sxs-lookup"><span data-stu-id="93c64-183">Configure hello job input</span></span>
<span data-ttu-id="93c64-184">travail de Hello obtient son entrée d’un fichier CSV hello que vous avez téléchargé antérieures tooblob stockage.</span><span class="sxs-lookup"><span data-stu-id="93c64-184">hello job gets its input from hello CSV file that you uploaded earlier tooblob storage.</span></span>

1. <span data-ttu-id="93c64-185">Une fois le travail de hello a été créé, sous **travail topologie** dans le panneau de tâche hello, cliquez sur hello **entrées** boîte.</span><span class="sxs-lookup"><span data-stu-id="93c64-185">After hello job has been created, under **Job Topology** in hello job blade, click hello **Inputs** box.</span></span>  
   
   ![zone 'Entrées' du panneau du travail dans Stream Analytics](./media/stream-analytics-machine-learning-integration-tutorial/create-job-add-input.png)  

2. <span data-ttu-id="93c64-187">Bonjour **entrées** panneau, cliquez sur **+ ajouter**.</span><span class="sxs-lookup"><span data-stu-id="93c64-187">In hello **Inputs** blade, click **+ Add**.</span></span>

   !['Add' bouton pour ajouter une tâche de flux de données Analytique toohello d’entrée](./media/stream-analytics-machine-learning-integration-tutorial/create-job-add-input-button.png)  

3. <span data-ttu-id="93c64-189">Remplir hello **nouvelle entrée** panneau avec ces valeurs :</span><span class="sxs-lookup"><span data-stu-id="93c64-189">Fill out hello **New input** blade with these values:</span></span>

    * <span data-ttu-id="93c64-190">**Alias d’entrée**: utiliser le nom hello `datainput`.</span><span class="sxs-lookup"><span data-stu-id="93c64-190">**Input alias**: Use hello name `datainput`.</span></span>
    * <span data-ttu-id="93c64-191">**Type de source** : sélectionnez **Flux de données**.</span><span class="sxs-lookup"><span data-stu-id="93c64-191">**Source type**: Select **Data stream**.</span></span>
    * <span data-ttu-id="93c64-192">**Source** : sélectionnez **Stockage d’objets blob**.</span><span class="sxs-lookup"><span data-stu-id="93c64-192">**Source**: Select **Blob storage**.</span></span>
    * <span data-ttu-id="93c64-193">**Option d’importation** : sélectionnez **Utiliser l’objet blob de stockage de l’abonnement actuel**.</span><span class="sxs-lookup"><span data-stu-id="93c64-193">**Import option**: Select **Use blob storage from current subscription**.</span></span> 
    * <span data-ttu-id="93c64-194">**Compte de stockage**.</span><span class="sxs-lookup"><span data-stu-id="93c64-194">**Storage account**.</span></span> <span data-ttu-id="93c64-195">Sélectionnez le compte de stockage hello que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="93c64-195">Select hello storage account you created earlier.</span></span>
    * <span data-ttu-id="93c64-196">**Conteneur** :</span><span class="sxs-lookup"><span data-stu-id="93c64-196">**Container**.</span></span> <span data-ttu-id="93c64-197">Conteneur de sélection hello vous avez créé précédemment (`azuresamldemoblob`).</span><span class="sxs-lookup"><span data-stu-id="93c64-197">Select hello container you created earlier (`azuresamldemoblob`).</span></span>
    * <span data-ttu-id="93c64-198">**Format de sérialisation de l’événement**.</span><span class="sxs-lookup"><span data-stu-id="93c64-198">**Event serialization format**.</span></span> <span data-ttu-id="93c64-199">Sélectionnez **CSV**.</span><span class="sxs-lookup"><span data-stu-id="93c64-199">Select **CSV**.</span></span>

    ![Paramètres de la nouvelle entrée de travail](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-create-sa-input-new-portal.png)

4. <span data-ttu-id="93c64-201">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="93c64-201">Click **Create**.</span></span>

### <a name="configure-hello-job-output"></a><span data-ttu-id="93c64-202">Configurer la sortie de tâche hello</span><span class="sxs-lookup"><span data-stu-id="93c64-202">Configure hello job output</span></span>
<span data-ttu-id="93c64-203">Bonjour toohello de résultats de la tâche envoie même lorsqu’il obtient une entrée de stockage d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="93c64-203">hello job sends results toohello same blob storage where it gets input.</span></span> 

1. <span data-ttu-id="93c64-204">Sous **travail topologie** dans le panneau de tâche hello, cliquez sur hello **sorties** boîte.</span><span class="sxs-lookup"><span data-stu-id="93c64-204">Under **Job Topology** in hello job blade, click hello **Outputs** box.</span></span>  
  
   ![Créer une sortie pour le travail Stream Analytics](./media/stream-analytics-machine-learning-integration-tutorial/create-output.png)  

2. <span data-ttu-id="93c64-206">Bonjour **sorties** panneau, cliquez sur **+ ajouter**, puis ajoutez une sortie avec l’alias de hello `datamloutput`.</span><span class="sxs-lookup"><span data-stu-id="93c64-206">In hello **Outputs** blade, click **+ Add**, and then add an output with hello alias `datamloutput`.</span></span> 

3. <span data-ttu-id="93c64-207">Au niveau du paramètre **Récepteur**, sélectionnez **Stockage d’objets blob**.</span><span class="sxs-lookup"><span data-stu-id="93c64-207">For **Sink**, select **Blob storage**.</span></span> <span data-ttu-id="93c64-208">Puis renseignez reste hello Hello de sortie à l’aide des paramètres hello les mêmes valeurs que vous avez utilisé pour le stockage d’objets blob hello pour l’entrée :</span><span class="sxs-lookup"><span data-stu-id="93c64-208">Then fill in hello rest of hello output settings using hello same values that you used for hello blob storage for input:</span></span>

    * <span data-ttu-id="93c64-209">**Compte de stockage**.</span><span class="sxs-lookup"><span data-stu-id="93c64-209">**Storage account**.</span></span> <span data-ttu-id="93c64-210">Sélectionnez le compte de stockage hello que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="93c64-210">Select hello storage account you created earlier.</span></span>
    * <span data-ttu-id="93c64-211">**Conteneur** :</span><span class="sxs-lookup"><span data-stu-id="93c64-211">**Container**.</span></span> <span data-ttu-id="93c64-212">Conteneur de sélection hello vous avez créé précédemment (`azuresamldemoblob`).</span><span class="sxs-lookup"><span data-stu-id="93c64-212">Select hello container you created earlier (`azuresamldemoblob`).</span></span>
    * <span data-ttu-id="93c64-213">**Format de sérialisation de l’événement**.</span><span class="sxs-lookup"><span data-stu-id="93c64-213">**Event serialization format**.</span></span> <span data-ttu-id="93c64-214">Sélectionnez **CSV**.</span><span class="sxs-lookup"><span data-stu-id="93c64-214">Select **CSV**.</span></span>

   ![Paramètres de la nouvelle sortie de travail](./media/stream-analytics-machine-learning-integration-tutorial/create-output2.png) 

4. <span data-ttu-id="93c64-216">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="93c64-216">Click **Create**.</span></span>   


### <a name="add-hello-machine-learning-function"></a><span data-ttu-id="93c64-217">Ajouter une fonction d’apprentissage hello</span><span class="sxs-lookup"><span data-stu-id="93c64-217">Add hello Machine Learning function</span></span> 
<span data-ttu-id="93c64-218">Précédemment, vous avez publié un service web de Machine Learning modèle tooa.</span><span class="sxs-lookup"><span data-stu-id="93c64-218">Earlier you published a Machine Learning model tooa web service.</span></span> <span data-ttu-id="93c64-219">Dans notre scénario, lorsque la tâche d’analyse de flux de hello s’exécute, il envoie chaque tweet exemple hello toohello d’entrée web service pour l’analyse de sentiments.</span><span class="sxs-lookup"><span data-stu-id="93c64-219">In our scenario, when hello Stream Analysis job runs, it sends each sample tweet from hello input toohello web service for sentiment analysis.</span></span> <span data-ttu-id="93c64-220">Hello service web Machine Learning retourne un sentiments (`positive`, `neutral`, ou `negative`) et une probabilité de tweet hello positif.</span><span class="sxs-lookup"><span data-stu-id="93c64-220">hello Machine Learning web service returns a sentiment (`positive`, `neutral`, or `negative`) and a probability of hello tweet being positive.</span></span> 

<span data-ttu-id="93c64-221">Dans cette section du didacticiel de hello, vous définissez une fonction dans la tâche de flux de données analyse hello.</span><span class="sxs-lookup"><span data-stu-id="93c64-221">In this section of hello tutorial, you define a function in hello Stream Analysis job.</span></span> <span data-ttu-id="93c64-222">fonction Hello peut être appelée toosend un service web de toohello tweet et revenir réponse de hello.</span><span class="sxs-lookup"><span data-stu-id="93c64-222">hello function can be invoked toosend a tweet toohello web service and get hello response back.</span></span> 

1. <span data-ttu-id="93c64-223">Assurez-vous que vous avez hello web service URL et la clé API que vous avez téléchargé précédemment dans le classeur Excel de hello.</span><span class="sxs-lookup"><span data-stu-id="93c64-223">Make sure you have hello web service URL and API key that you downloaded earlier in hello Excel workbook.</span></span>

2. <span data-ttu-id="93c64-224">Panneau de vue d’ensemble du travail toohello retour.</span><span class="sxs-lookup"><span data-stu-id="93c64-224">Return toohello job overview blade.</span></span>

3. <span data-ttu-id="93c64-225">Sous **Paramètres**, sélectionnez **Fonctions**, puis cliquez sur **+ Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="93c64-225">Under **Settings**, select **Functions** and then click **+ Add**.</span></span>

   ![Ajouter une tâche de flux de données Analytique toohello (fonction)](./media/stream-analytics-machine-learning-integration-tutorial/create-function1.png) 

4. <span data-ttu-id="93c64-227">Entrez `sentiment` comme hello fonction alias et remplissez les autres hello du panneau hello à l’aide de ces valeurs :</span><span class="sxs-lookup"><span data-stu-id="93c64-227">Enter `sentiment` as hello function alias and fill out hello rest of hello blade using these values:</span></span>

    * <span data-ttu-id="93c64-228">**Type de fonction** : sélectionnez **Azure ML**.</span><span class="sxs-lookup"><span data-stu-id="93c64-228">**Function type**: Select **Azure ML**.</span></span>
    * <span data-ttu-id="93c64-229">**Option d’importation** : sélectionnez **Importer à partir d’un autre abonnement**.</span><span class="sxs-lookup"><span data-stu-id="93c64-229">**Import option**: Select **Import from a different subscription**.</span></span> <span data-ttu-id="93c64-230">Cela vous donne une occasion tooenter hello URL et une clé.</span><span class="sxs-lookup"><span data-stu-id="93c64-230">This gives you a chance tooenter hello URL and key.</span></span>
    * <span data-ttu-id="93c64-231">**URL**: coller dans l’URL du service web hello.</span><span class="sxs-lookup"><span data-stu-id="93c64-231">**URL**: Paste in hello web service URL.</span></span>
    * <span data-ttu-id="93c64-232">**Clé**: coller dans la clé de l’API de hello.</span><span class="sxs-lookup"><span data-stu-id="93c64-232">**Key**: Paste in hello API key.</span></span>
  
    ![Paramètres pour l’ajout d’une tâche de flux de données Analytique toohello Machine Learning (fonction)](./media/stream-analytics-machine-learning-integration-tutorial/add-function.png)  
    
5. <span data-ttu-id="93c64-234">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="93c64-234">Click **Create**.</span></span>

### <a name="create-a-query-tootransform-hello-data"></a><span data-ttu-id="93c64-235">Créer une requête de données hello tootransform</span><span class="sxs-lookup"><span data-stu-id="93c64-235">Create a query tootransform hello data</span></span>

<span data-ttu-id="93c64-236">Flux de données Analytique utilise une entrée de hello tooexamine requête déclarative basé sur SQL et le traiter.</span><span class="sxs-lookup"><span data-stu-id="93c64-236">Stream Analytics uses a declarative, SQL-based query tooexamine hello input and process it.</span></span> <span data-ttu-id="93c64-237">Dans cette section, vous créez une requête qui lit chaque tweet d’entrée, puis appelle analyse des sentiments tooperform hello Machine Learning (fonction).</span><span class="sxs-lookup"><span data-stu-id="93c64-237">In this section, you create a query that reads each tweet from input and then invokes hello Machine Learning function tooperform sentiment analysis.</span></span> <span data-ttu-id="93c64-238">requête de Hello envoie ensuite hello résultat toohello de sortie que vous avez définies (stockage d’objets blob).</span><span class="sxs-lookup"><span data-stu-id="93c64-238">hello query then sends hello result toohello output that you defined (blob storage).</span></span>

1. <span data-ttu-id="93c64-239">Panneau de vue d’ensemble du travail toohello retour.</span><span class="sxs-lookup"><span data-stu-id="93c64-239">Return toohello job overview blade.</span></span>

2.  <span data-ttu-id="93c64-240">Sous **travail topologie**, cliquez sur hello **requête** boîte.</span><span class="sxs-lookup"><span data-stu-id="93c64-240">Under **Job Topology**, click hello **Query** box.</span></span>

    ![Créer une requête pour le travail Stream Analytics](./media/stream-analytics-machine-learning-integration-tutorial/create-query.png)  

3. <span data-ttu-id="93c64-242">Entrez hello suivant la requête :</span><span class="sxs-lookup"><span data-stu-id="93c64-242">Enter hello following query:</span></span>

    ```
    WITH sentiment AS (  
    SELECT text, sentiment(text) as result from datainput  
    )  

    Select text, result.[Score]  
    Into datamloutput
    From sentiment  
    ```    

    <span data-ttu-id="93c64-243">requête de Hello appelle la fonction hello que vous avez créé précédemment (`sentiment`) dans l’analyse des sentiments tooperform commande sur chaque tweet dans l’entrée de hello.</span><span class="sxs-lookup"><span data-stu-id="93c64-243">hello query invokes hello function you created earlier (`sentiment`) in order tooperform sentiment analysis on each tweet in hello input.</span></span> 

4. <span data-ttu-id="93c64-244">Cliquez sur **enregistrer** requête de hello toosave.</span><span class="sxs-lookup"><span data-stu-id="93c64-244">Click **Save** toosave hello query.</span></span>


## <a name="start-hello-stream-analytics-job-and-check-hello-output"></a><span data-ttu-id="93c64-245">Démarrer la tâche de flux de données Analytique hello et vérifier la sortie de hello</span><span class="sxs-lookup"><span data-stu-id="93c64-245">Start hello Stream Analytics job and check hello output</span></span>

<span data-ttu-id="93c64-246">Vous pouvez maintenant démarrer la tâche de flux de données Analytique hello.</span><span class="sxs-lookup"><span data-stu-id="93c64-246">You can now start hello Stream Analytics job.</span></span>

### <a name="start-hello-job"></a><span data-ttu-id="93c64-247">Démarrer le travail de hello</span><span class="sxs-lookup"><span data-stu-id="93c64-247">Start hello job</span></span>
1. <span data-ttu-id="93c64-248">Panneau de vue d’ensemble du travail toohello retour.</span><span class="sxs-lookup"><span data-stu-id="93c64-248">Return toohello job overview blade.</span></span>

2. <span data-ttu-id="93c64-249">Cliquez sur **Démarrer** haut hello du Panneau de hello.</span><span class="sxs-lookup"><span data-stu-id="93c64-249">Click **Start** at hello top of hello blade.</span></span>

    ![Créer une requête pour le travail Stream Analytics](./media/stream-analytics-machine-learning-integration-tutorial/start-job.png)  

3. <span data-ttu-id="93c64-251">Bonjour **Start job**, sélectionnez **personnalisé**, puis sélectionnez toowhen préalable à un jour vous avez téléchargé un stockage tooblob fichier CSV hello.</span><span class="sxs-lookup"><span data-stu-id="93c64-251">In hello **Start job**, select **Custom**, and then select one day prior toowhen you uploaded hello CSV file tooblob storage.</span></span> <span data-ttu-id="93c64-252">Quand vous avez terminé, cliquez sur **Démarrer**.</span><span class="sxs-lookup"><span data-stu-id="93c64-252">When you're done, click **Start**.</span></span>  


### <a name="check-hello-output"></a><span data-ttu-id="93c64-253">Vérifier la sortie de hello</span><span class="sxs-lookup"><span data-stu-id="93c64-253">Check hello output</span></span>
1. <span data-ttu-id="93c64-254">Tâche hello laisser s’exécutée pendant quelques minutes jusqu'à ce que vous voyiez activité Bonjour **analyse** boîte.</span><span class="sxs-lookup"><span data-stu-id="93c64-254">Let hello job run for a few minutes until you see activity in hello **Monitoring** box.</span></span> 

2. <span data-ttu-id="93c64-255">Si vous disposez d’un outil que vous utilisez normalement contenu de hello tooexamine de stockage d’objets blob, utilisez ce hello de tooexamine outil `azuresamldemoblob` conteneur.</span><span class="sxs-lookup"><span data-stu-id="93c64-255">If you have a tool that you normally use tooexamine hello contents of blob storage, use that tool tooexamine hello `azuresamldemoblob` container.</span></span> <span data-ttu-id="93c64-256">Vous pouvez également le hello Bonjour portail Azure comme suit :</span><span class="sxs-lookup"><span data-stu-id="93c64-256">Alternatively, do hello following steps in hello Azure portal:</span></span>

    1. <span data-ttu-id="93c64-257">Dans le portail de hello, recherchez hello `samldemo` stockage compte et dans le compte de hello, recherche hello `azuresamldemoblob` conteneur.</span><span class="sxs-lookup"><span data-stu-id="93c64-257">In hello portal, find hello `samldemo` storage account, and within hello account, find hello `azuresamldemoblob` container.</span></span> <span data-ttu-id="93c64-258">Vous voyez deux fichiers dans le conteneur de hello : hello du fichier qui contient des tweets d’exemple hello et un fichier CSV généré par la tâche de flux de données Analytique hello.</span><span class="sxs-lookup"><span data-stu-id="93c64-258">You see two files in hello container: hello file that contains hello sample tweets and a CSV file generated by hello Stream Analytics job.</span></span>
    2. <span data-ttu-id="93c64-259">Fichier de hello généré de droit et sélectionnez **télécharger**.</span><span class="sxs-lookup"><span data-stu-id="93c64-259">Right-click hello generated file and then select **Download**.</span></span> 

   ![Télécharger la sortie CSV du travail à partir du stockage d’objets blob](./media/stream-analytics-machine-learning-integration-tutorial/download-output-csv-file.png)  

3. <span data-ttu-id="93c64-261">Ouvrez hello généré un fichier CSV.</span><span class="sxs-lookup"><span data-stu-id="93c64-261">Open hello generated CSV file.</span></span> <span data-ttu-id="93c64-262">Vous voyez quelque chose comme hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="93c64-262">You see something like hello following example:</span></span>  
   
   ![Stream Analytics Machine Learning, vue CSV](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-csv-view.png)  


### <a name="view-metrics"></a><span data-ttu-id="93c64-264">Afficher les mesures</span><span class="sxs-lookup"><span data-stu-id="93c64-264">View metrics</span></span>
<span data-ttu-id="93c64-265">Vous pouvez également afficher les mesures liées à la fonction Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="93c64-265">You also can view Azure Machine Learning function-related metrics.</span></span> <span data-ttu-id="93c64-266">Hello suit les mesures associées à la fonction est affiché dans hello **analyse** zone dans le panneau de tâche hello :</span><span class="sxs-lookup"><span data-stu-id="93c64-266">hello following function-related metrics are displayed in hello **Monitoring** box in hello job blade:</span></span>

* <span data-ttu-id="93c64-267">**Demandes de fonction** indique le nombre de hello de demandes envoyées tooa service web Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="93c64-267">**Function Requests** indicates hello number of requests sent tooa Machine Learning web service.</span></span>  
* <span data-ttu-id="93c64-268">**Événements de la fonction** indique le nombre de hello d’événements dans la demande de hello.</span><span class="sxs-lookup"><span data-stu-id="93c64-268">**Function Events** indicates hello number of events in hello request.</span></span> <span data-ttu-id="93c64-269">Par défaut, chaque demande de tooa service web Machine Learning contient too1, 000 événements.</span><span class="sxs-lookup"><span data-stu-id="93c64-269">By default, each request tooa Machine Learning web service contains up too1,000 events.</span></span>  


## <a name="next-steps"></a><span data-ttu-id="93c64-270">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="93c64-270">Next steps</span></span>

* [<span data-ttu-id="93c64-271">Introduction tooAzure Analytique de flux de données</span><span class="sxs-lookup"><span data-stu-id="93c64-271">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="93c64-272">Références sur le langage des requêtes d'Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="93c64-272">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="93c64-273">Intégrer l’API REST et le service Machine Learning</span><span class="sxs-lookup"><span data-stu-id="93c64-273">Integrate REST API and Machine Learning</span></span>](stream-analytics-how-to-configure-azure-machine-learning-endpoints-in-stream-analytics.md)
* [<span data-ttu-id="93c64-274">Références sur l’API REST de gestion d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="93c64-274">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)



