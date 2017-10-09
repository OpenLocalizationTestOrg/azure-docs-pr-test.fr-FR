---
title: tableau de bord BI aaaPower sur Azure flux Analytique | Documents Microsoft
description: "Utiliser une en temps réel en continu Power BI du tableau de bord toogather business intelligence et analyser les données de volume élevé d’une tâche de flux de données Analytique."
keywords: "tableau de bord d’analyse, tableau de bord en temps réel"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: fe8db732-4397-4e58-9313-fec9537aa2ad
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/27/2017
ms.author: jeffstok
ms.openlocfilehash: cb9127576230e9d327b437b674f31cc23869bfff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="stream-analytics-and-power-bi-a-real-time-analytics-dashboard-for-streaming-data"></a><span data-ttu-id="4e022-104">Stream Analytics et Power BI : tableau de bord d’analyse en temps réel pour les données de streaming</span><span class="sxs-lookup"><span data-stu-id="4e022-104">Stream Analytics and Power BI: A real-time analytics dashboard for streaming data</span></span>
<span data-ttu-id="4e022-105">Analytique de flux de données Azure vous permet de parti tootake de hello des outils d’analyse décisionnelle, [Microsoft Power BI](https://powerbi.com/).</span><span class="sxs-lookup"><span data-stu-id="4e022-105">Azure Stream Analytics enables you tootake advantage of one of hello leading business intelligence tools, [Microsoft Power BI](https://powerbi.com/).</span></span> <span data-ttu-id="4e022-106">Dans cet article, vous allez découvrir comment créer des outils d’analyse décisionnelle en utilisant Power BI comme sortie pour vos travaux Azure Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="4e022-106">In this article, you learn how create business intelligence tools by using Power BI as an output for your Azure Stream Analytics jobs.</span></span> <span data-ttu-id="4e022-107">Vous apprendrez également comment toocreate et utiliser un tableau de bord en temps réel.</span><span class="sxs-lookup"><span data-stu-id="4e022-107">You also learn how toocreate and use a real-time dashboard.</span></span>

<span data-ttu-id="4e022-108">Cet article reprend à partir de hello flux Analytique [la détection des fraudes en temps réel](stream-analytics-real-time-fraud-detection.md) didacticiel.</span><span class="sxs-lookup"><span data-stu-id="4e022-108">This article continues from hello Stream Analytics [real-time fraud detection](stream-analytics-real-time-fraud-detection.md) tutorial.</span></span> <span data-ttu-id="4e022-109">Il s’appuie sur les flux de travail hello créé dans ce didacticiel et ajoute une sortie afin que vous pouvez visualiser les appels téléphoniques frauduleux qui sont détectés par une tâche Analytique de diffusion en continu de Power BI.</span><span class="sxs-lookup"><span data-stu-id="4e022-109">It builds on hello workflow created in that tutorial and adds a Power BI output so that you can visualize fraudulent phone calls that are detected by a Streaming Analytics job.</span></span> 

<span data-ttu-id="4e022-110">Vous pouvez visionner [une vidéo](https://www.youtube.com/watch?v=SGUpT-a99MA) illustrant ce scénario.</span><span class="sxs-lookup"><span data-stu-id="4e022-110">You can watch [a video](https://www.youtube.com/watch?v=SGUpT-a99MA)  that illustrates this scenario.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="4e022-111">Composants requis</span><span class="sxs-lookup"><span data-stu-id="4e022-111">Prerequisites</span></span>

<span data-ttu-id="4e022-112">Avant de commencer, assurez-vous que vous avez hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="4e022-112">Before you start, make sure you have hello following:</span></span>

* <span data-ttu-id="4e022-113">Un compte Azure.</span><span class="sxs-lookup"><span data-stu-id="4e022-113">An Azure account.</span></span>
* <span data-ttu-id="4e022-114">Un compte pour Power BI.</span><span class="sxs-lookup"><span data-stu-id="4e022-114">An account for Power BI.</span></span> <span data-ttu-id="4e022-115">Vous pouvez utiliser un compte professionnel ou un compte scolaire.</span><span class="sxs-lookup"><span data-stu-id="4e022-115">You can use a work account or a school account.</span></span>
* <span data-ttu-id="4e022-116">Une version complète de hello [la détection des fraudes en temps réel](stream-analytics-real-time-fraud-detection.md) didacticiel.</span><span class="sxs-lookup"><span data-stu-id="4e022-116">A completed version of hello [real-time fraud detection](stream-analytics-real-time-fraud-detection.md) tutorial.</span></span> <span data-ttu-id="4e022-117">didacticiel de Hello inclut une application qui génère des métadonnées de l’appel de téléphone fictifs.</span><span class="sxs-lookup"><span data-stu-id="4e022-117">hello tutorial includes an app that generates fictitious telephone-call metadata.</span></span> <span data-ttu-id="4e022-118">Didacticiel de hello, vous créez un hub d’événements et d’envoyez hello concentrateur d’événements d’appel téléphonique données toohello de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="4e022-118">In hello tutorial, you create an event hub and send hello streaming phone call data toohello event hub.</span></span> <span data-ttu-id="4e022-119">Vous écrivez une requête qui détecte les appels frauduleux (appels de hello même nombre à hello même moment dans différents emplacements).</span><span class="sxs-lookup"><span data-stu-id="4e022-119">You write a query that detects fraudulent calls (calls from hello same number at hello same time in different locations).</span></span> 


## <a name="add-power-bi-output"></a><span data-ttu-id="4e022-120">Ajouter une sortie Power BI</span><span class="sxs-lookup"><span data-stu-id="4e022-120">Add Power BI output</span></span>
<span data-ttu-id="4e022-121">Dans le didacticiel de détection de fraude en temps réel hello, hello est affiché tooAzure stockage d’objets Blob.</span><span class="sxs-lookup"><span data-stu-id="4e022-121">In hello real-time fraud detection tutorial, hello output is sent tooAzure Blob storage.</span></span> <span data-ttu-id="4e022-122">Dans cette section, vous ajoutez une sortie qui envoie des informations tooPower BI.</span><span class="sxs-lookup"><span data-stu-id="4e022-122">In this section, you add an output that sends information tooPower BI.</span></span>

1. <span data-ttu-id="4e022-123">Bonjour portail Azure, ouvrez tâche Analytique de diffusion en continu hello que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="4e022-123">In hello Azure portal, open hello Streaming Analytics job that you created earlier.</span></span> <span data-ttu-id="4e022-124">Si vous avez utilisé le nom suggéré de hello, hello est nommée `sa_frauddetection_job_demo`.</span><span class="sxs-lookup"><span data-stu-id="4e022-124">If you used hello suggested name, hello job is named `sa_frauddetection_job_demo`.</span></span>

2. <span data-ttu-id="4e022-125">Sélectionnez hello **sorties** zone au milieu de hello de tableau de bord projet hello, puis sélectionner **+ ajouter**.</span><span class="sxs-lookup"><span data-stu-id="4e022-125">Select hello **Outputs** box in hello middle of hello job dashboard and then select **+ Add**.</span></span>

3. <span data-ttu-id="4e022-126">Pour **Alias de sortie**, entrez `CallStream-PowerBI`.</span><span class="sxs-lookup"><span data-stu-id="4e022-126">For **Output Alias**, enter `CallStream-PowerBI`.</span></span> <span data-ttu-id="4e022-127">Vous pouvez utiliser un autre nom.</span><span class="sxs-lookup"><span data-stu-id="4e022-127">You can use a different name.</span></span> <span data-ttu-id="4e022-128">Si vous le faites, prenez note de celui-ci, car vous devez les nom hello plus tard.</span><span class="sxs-lookup"><span data-stu-id="4e022-128">If you do, make a note of it, because you need hello name later.</span></span> 

4. <span data-ttu-id="4e022-129">Dans **Récepteur**, sélectionnez **Power BI**.</span><span class="sxs-lookup"><span data-stu-id="4e022-129">Under **Sink**, select **Power BI**.</span></span>

   ![Créer une sortie pour Power BI](./media/stream-analytics-power-bi-dashboard/create-pbi-ouptut.png)

5. <span data-ttu-id="4e022-131">Cliquez sur **Autoriser**.</span><span class="sxs-lookup"><span data-stu-id="4e022-131">Click **Authorize**.</span></span>

    <span data-ttu-id="4e022-132">Une fenêtre s’ouvre dans laquelle vous pouvez indiquer vos informations d’identification Azure pour un compte professionnel ou scolaire.</span><span class="sxs-lookup"><span data-stu-id="4e022-132">A window opens where you can provide your Azure credentials for a work or school account.</span></span> 

    ![Entrez les informations d’identification pour l’accès tooPower BI](./media/stream-analytics-power-bi-dashboard/authorize-area.png)

6. <span data-ttu-id="4e022-134">Entrez vos informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="4e022-134">Enter your credentials.</span></span> <span data-ttu-id="4e022-135">N’oubliez pas ensuite, lorsque vous entrez vos informations d’identification, vous êtes également en train de tooaccess de travail autorisation toohello Analytique de diffusion en continu votre zone Power BI.</span><span class="sxs-lookup"><span data-stu-id="4e022-135">Be aware then when you enter your credentials, you're also giving permission toohello Streaming Analytics job tooaccess your Power BI area.</span></span>

7. <span data-ttu-id="4e022-136">Lorsque vous êtes renvoyé toohello **nouvelle sortie** panneau, entrez hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="4e022-136">When you're returned toohello **New output** blade, enter hello following information:</span></span>

    * <span data-ttu-id="4e022-137">**Espace de travail de groupe**: sélectionnez un espace de travail dans votre locataire Power BI où vous souhaitez toocreate hello dataset.</span><span class="sxs-lookup"><span data-stu-id="4e022-137">**Group Workspace**: Select a workspace in your Power BI tenant where you want toocreate hello dataset.</span></span>
    * <span data-ttu-id="4e022-138">**Nom du jeu de données** : entrez `sa-dataset`.</span><span class="sxs-lookup"><span data-stu-id="4e022-138">**Dataset Name**:  Enter `sa-dataset`.</span></span> <span data-ttu-id="4e022-139">Vous pouvez utiliser un autre nom.</span><span class="sxs-lookup"><span data-stu-id="4e022-139">You can use a different name.</span></span> <span data-ttu-id="4e022-140">Le cas échéant, prenez-en note pour l’utiliser ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="4e022-140">If you do, make a note of it for later.</span></span>
    * <span data-ttu-id="4e022-141">**Nom de la table** : entrez `fraudulent-calls`.</span><span class="sxs-lookup"><span data-stu-id="4e022-141">**Table Name**: Enter `fraudulent-calls`.</span></span> <span data-ttu-id="4e022-142">Actuellement, une sortie Power BI des travaux Stream Analytics ne peut avoir qu’une table dans un jeu de données.</span><span class="sxs-lookup"><span data-stu-id="4e022-142">Currently, Power BI output from Stream Analytics jobs can have only one table in a dataset.</span></span>

    ![Espace de travail PBI](./media/stream-analytics-power-bi-dashboard/create-pbi-ouptut-with-dataset-table.png)

    > [!WARNING]
    > <span data-ttu-id="4e022-144">Si Power BI dispose d’un jeu de données et la table qui a hello mêmes noms que hello celles que vous spécifiez dans la tâche de flux de données Analytique hello, hello des groupes existants est remplacé.</span><span class="sxs-lookup"><span data-stu-id="4e022-144">If Power BI has a dataset and table that have hello same names as hello ones that you specify in hello Stream Analytics job, hello existing ones are overwritten.</span></span>
    > <span data-ttu-id="4e022-145">Nous vous recommandons de ne pas créer explicitement ce jeu de données et cette table dans votre compte Power BI.</span><span class="sxs-lookup"><span data-stu-id="4e022-145">We recommend that you do not explicitly create this dataset and table in your Power BI account.</span></span> <span data-ttu-id="4e022-146">Ils sont créés automatiquement lorsque vous lancez votre tâche de flux de données Analytique et hello programmée de sortie pompage dans Power BI.</span><span class="sxs-lookup"><span data-stu-id="4e022-146">They are automatically created when you start your Stream Analytics job and hello job starts pumping output into Power BI.</span></span> <span data-ttu-id="4e022-147">Si votre requête de travail ne renvoie aucun résultat, table et hello dataset ne sont pas créés.</span><span class="sxs-lookup"><span data-stu-id="4e022-147">If your job query doesn't return any results, hello dataset and table are not  created.</span></span>
    >

8. <span data-ttu-id="4e022-148">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="4e022-148">Click **Create**.</span></span>

<span data-ttu-id="4e022-149">jeu de données Hello est créée avec hello suivant les paramètres :</span><span class="sxs-lookup"><span data-stu-id="4e022-149">hello dataset is created with hello following settings:</span></span>

* <span data-ttu-id="4e022-150">**defaultRetentionPolicy : BasicFIFO** : données FIFO avec un maximum de 200 000 lignes.</span><span class="sxs-lookup"><span data-stu-id="4e022-150">**defaultRetentionPolicy: BasicFIFO**: Data is FIFO, with a maximum of 200,000 rows.</span></span>
* <span data-ttu-id="4e022-151">**defaultMode : pushStreaming**: hello le jeu de données prend en charge la diffusion en continu des vignettes et traditionnels basée sur l’état des éléments visuels (aussi appelé)</span><span class="sxs-lookup"><span data-stu-id="4e022-151">**defaultMode: pushStreaming**: hello dataset supports both streaming tiles and traditional report-based visuals (a.k.a.</span></span> <span data-ttu-id="4e022-152">push).</span><span class="sxs-lookup"><span data-stu-id="4e022-152">push).</span></span>

<span data-ttu-id="4e022-153">Pour le moment, vous ne pouvez pas créer de jeux de données avec d’autres indicateurs.</span><span class="sxs-lookup"><span data-stu-id="4e022-153">Currently, you can't create datasets with other flags.</span></span>

<span data-ttu-id="4e022-154">Pour plus d’informations sur les jeux de données Power BI, consultez hello [API REST Power BI](https://msdn.microsoft.com/library/mt203562.aspx) référence.</span><span class="sxs-lookup"><span data-stu-id="4e022-154">For more information about Power BI datasets, see hello [Power BI REST API](https://msdn.microsoft.com/library/mt203562.aspx) reference.</span></span>


## <a name="write-hello-query"></a><span data-ttu-id="4e022-155">Écrire des requêtes de hello</span><span class="sxs-lookup"><span data-stu-id="4e022-155">Write hello query</span></span>

1. <span data-ttu-id="4e022-156">Fermer hello **sorties** panneau et le panneau de tâche toohello retour.</span><span class="sxs-lookup"><span data-stu-id="4e022-156">Close hello **Outputs** blade and return toohello job blade.</span></span>

2. <span data-ttu-id="4e022-157">Cliquez sur hello **requête** boîte.</span><span class="sxs-lookup"><span data-stu-id="4e022-157">Click hello **Query** box.</span></span> 

3. <span data-ttu-id="4e022-158">Entrez hello suivant la requête.</span><span class="sxs-lookup"><span data-stu-id="4e022-158">Enter hello following query.</span></span> <span data-ttu-id="4e022-159">Cette requête est toohello jointure réflexive requête similaire que vous avez créé dans le didacticiel de détection des fraudes hello.</span><span class="sxs-lookup"><span data-stu-id="4e022-159">This query is similar toohello self-join query you created in hello fraud-detection tutorial.</span></span> <span data-ttu-id="4e022-160">Bonjour différence est que cette requête envoie toohello des résultats de la nouvelle sortie que vous avez créé (`CallStream-PowerBI`).</span><span class="sxs-lookup"><span data-stu-id="4e022-160">hello difference is that this query sends results toohello new output you created (`CallStream-PowerBI`).</span></span> 

    >[!NOTE]
    ><span data-ttu-id="4e022-161">Si vous n’avez pas nommé hello entrée `CallStream` dans le didacticiel de détection des fraudes hello, remplacez par votre nom de `CallStream` Bonjour **FROM** et **joindre** clauses de requête de hello.</span><span class="sxs-lookup"><span data-stu-id="4e022-161">If you did not name hello input `CallStream` in hello fraud-detection tutorial, substitute your name for `CallStream` in hello **FROM** and **JOIN** clauses in hello query.</span></span>

        /* Our criteria for fraud:
        Calls made from hello same caller tootwo phone switches in different locations (for example, Australia and Europe) within five seconds */

        SELECT System.Timestamp AS WindowEnd, COUNT(*) AS FraudulentCalls
        INTO "CallStream-PowerBI"
        FROM "CallStream" CS1 TIMESTAMP BY CallRecTime
        JOIN "CallStream" CS2 TIMESTAMP BY CallRecTime

        /* Where hello caller is hello same, as indicated by IMSI (International Mobile Subscriber Identity) */
        ON CS1.CallingIMSI = CS2.CallingIMSI

        /* ...and date between CS1 and CS2 is between one and five seconds */
        AND DATEDIFF(ss, CS1, CS2) BETWEEN 1 AND 5

        /* Where hello switch location is different */
        WHERE CS1.SwitchNum != CS2.SwitchNum
        GROUP BY TumblingWindow(Duration(second, 1))

4. <span data-ttu-id="4e022-162">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="4e022-162">Click **Save**.</span></span>


## <a name="test-hello-query"></a><span data-ttu-id="4e022-163">Tester la requête hello</span><span class="sxs-lookup"><span data-stu-id="4e022-163">Test hello query</span></span>
<span data-ttu-id="4e022-164">Cette étape est facultative, mais recommandée.</span><span class="sxs-lookup"><span data-stu-id="4e022-164">This section is optional, but recommended.</span></span> 

1. <span data-ttu-id="4e022-165">Si l’application de TelcoStreaming hello n’est pas en cours d’exécution, démarrez-le en procédant comme suit :</span><span class="sxs-lookup"><span data-stu-id="4e022-165">If hello TelcoStreaming app is not currently running, start it by following these steps:</span></span>

    * <span data-ttu-id="4e022-166">Ouvrez une fenêtre de commandes.</span><span class="sxs-lookup"><span data-stu-id="4e022-166">Open a command window.</span></span>
    * <span data-ttu-id="4e022-167">Atteindre le dossier toohello où hello telcogenerator.exe et les fichiers modifiés telcodatagen.exe.config sont.</span><span class="sxs-lookup"><span data-stu-id="4e022-167">Go toohello folder where hello telcogenerator.exe and modified telcodatagen.exe.config files are.</span></span>
    * <span data-ttu-id="4e022-168">Exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="4e022-168">Run hello following command:</span></span>

            telcodatagen.exe 1000 .2 2

2. <span data-ttu-id="4e022-169">Bonjour **requête** panneau, cliquez sur toohello suivant de points hello `CallStream` d’entrée, puis sélectionnez **les exemples de données à partir de l’entrée**.</span><span class="sxs-lookup"><span data-stu-id="4e022-169">In hello **Query** blade, click hello dots next toohello `CallStream` input and then select **Sample data from input**.</span></span>

3. <span data-ttu-id="4e022-170">Spécifiez que vous souhaitez une valeur de trois minutes de données, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="4e022-170">Specify that you want three minutes' worth of data and click **OK**.</span></span> <span data-ttu-id="4e022-171">Patientez jusqu'à ce que vous êtes averti que les données de salutation ont été échantillonnées.</span><span class="sxs-lookup"><span data-stu-id="4e022-171">Wait until you're notified that hello data has been sampled.</span></span>

4. <span data-ttu-id="4e022-172">Cliquez sur **Test** et vérifiez que vous obtenez des résultats.</span><span class="sxs-lookup"><span data-stu-id="4e022-172">Click **Test** and make sure you're getting results.</span></span>


## <a name="run-hello-job"></a><span data-ttu-id="4e022-173">Exécuter la tâche de hello</span><span class="sxs-lookup"><span data-stu-id="4e022-173">Run hello job</span></span>

1. <span data-ttu-id="4e022-174">Assurez-vous que cette application de TelcoStreaming hello est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="4e022-174">Make sure that hello TelcoStreaming app is running.</span></span>

2. <span data-ttu-id="4e022-175">Fermer hello **requête** panneau.</span><span class="sxs-lookup"><span data-stu-id="4e022-175">Close hello **Query** blade.</span></span>

3. <span data-ttu-id="4e022-176">Dans le panneau de tâche hello, cliquez sur **Démarrer**.</span><span class="sxs-lookup"><span data-stu-id="4e022-176">In hello job blade, click **Start**.</span></span>

    ![Démarrer la tâche de flux de données Analytique hello](./media/stream-analytics-power-bi-dashboard/stream-analytics-sa-job-start-output.png)

<span data-ttu-id="4e022-178">Votre tâche Analytique de diffusion en continu commence la recherche d’appels frauduleuses dans les flux entrants hello.</span><span class="sxs-lookup"><span data-stu-id="4e022-178">Your Streaming Analytics job starts looking for fraudulent calls in hello incoming stream.</span></span> <span data-ttu-id="4e022-179">travail de Hello crée hello le jeu de données et de table dans Power BI et commence à envoyer des données sur toothem d’appels frauduleux hello.</span><span class="sxs-lookup"><span data-stu-id="4e022-179">hello job also creates hello dataset and table in Power BI and starts sending data about hello fraudulent calls toothem.</span></span>


## <a name="create-hello-dashboard-in-power-bi"></a><span data-ttu-id="4e022-180">Créer un tableau de bord hello dans Power BI</span><span class="sxs-lookup"><span data-stu-id="4e022-180">Create hello dashboard in Power BI</span></span>

1. <span data-ttu-id="4e022-181">Accédez trop[Powerbi.com](https://powerbi.com) et connectez-vous avec votre compte professionnel ou scolaire.</span><span class="sxs-lookup"><span data-stu-id="4e022-181">Go too[Powerbi.com](https://powerbi.com) and sign in with your work or school account.</span></span> <span data-ttu-id="4e022-182">Si la requête de traitement de flux de données Analytique hello génère des résultats, vous consultez que votre jeu de données est déjà créée :</span><span class="sxs-lookup"><span data-stu-id="4e022-182">If hello Stream Analytics job query outputs results, you see that your dataset is already created:</span></span>

    ![Jeu de données de diffusion en continu dans Power BI](./media/stream-analytics-power-bi-dashboard/streaming-dataset.png)

2. <span data-ttu-id="4e022-184">Dans votre espace de travail, cliquez sur **+&nbsp;Créer**.</span><span class="sxs-lookup"><span data-stu-id="4e022-184">In your workspace, click **+&nbsp;Create**.</span></span>

    ![bouton créer de Hello dans l’espace de travail Power BI](./media/stream-analytics-power-bi-dashboard/pbi-create-dashboard.png)

3. <span data-ttu-id="4e022-186">Créez un tableau de bord et nommez-le `Fraudulent Calls`.</span><span class="sxs-lookup"><span data-stu-id="4e022-186">Create a new dashboard and name it `Fraudulent Calls`.</span></span>

    ![Créer un tableau de bord et lui donner un nom dans l’espace de travail Power BI](./media/stream-analytics-power-bi-dashboard/pbi-create-dashboard-name.png)

4. <span data-ttu-id="4e022-188">En haut de hello de fenêtre hello, cliquez sur **ajouter une vignette**, sélectionnez **données de STREAMING personnalisées**, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="4e022-188">At hello top of hello window, click **Add tile**, select **CUSTOM STREAMING DATA**, and then click **Next**.</span></span>

    ![Jeu de données de streaming personnalisé](./media/stream-analytics-power-bi-dashboard/custom-streaming-data.png)

5. <span data-ttu-id="4e022-190">Sous **VOS JEUX DE DONNÉES**, sélectionnez votre jeu de données, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="4e022-190">Under **YOUR DATSETS**, select your dataset and then click **Next**.</span></span>

    ![Votre jeu de données de streaming](./media/stream-analytics-power-bi-dashboard/your-streaming-dataset.png)

6. <span data-ttu-id="4e022-192">Sous **Type de visualisation**, sélectionnez **carte**, puis dans hello **champs** liste, sélectionnez **fraudulentcalls**.</span><span class="sxs-lookup"><span data-stu-id="4e022-192">Under **Visualization Type**, select **Card**, and then in hello **Fields** list, select **fraudulentcalls**.</span></span>

    ![Détails de la visualisation de la nouvelle vignette](./media/stream-analytics-power-bi-dashboard/add-fraud.png)

7. <span data-ttu-id="4e022-194">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="4e022-194">Click **Next**.</span></span>

8. <span data-ttu-id="4e022-195">Renseignez les détails de la vignette, par exemple un titre et un sous-titre.</span><span class="sxs-lookup"><span data-stu-id="4e022-195">Fill in tile details like a title and subtitle.</span></span>

    ![Titre et sous-titre de la nouvelle vignette](./media/stream-analytics-power-bi-dashboard/pbi-new-tile-details.png)

9. <span data-ttu-id="4e022-197">Cliquez sur **Apply**.</span><span class="sxs-lookup"><span data-stu-id="4e022-197">Click **Apply**.</span></span>

    <span data-ttu-id="4e022-198">Nous avons à présent un compteur de fraudes.</span><span class="sxs-lookup"><span data-stu-id="4e022-198">Now you have a fraud counter!</span></span>

    ![Compteur de fraudes](./media/stream-analytics-power-bi-dashboard/fraud-counter.png)

8. <span data-ttu-id="4e022-200">Suivez hello étapes tooadd à nouveau une vignette (à partir de l’étape 4).</span><span class="sxs-lookup"><span data-stu-id="4e022-200">Follow hello steps again tooadd a tile (starting with step 4).</span></span> <span data-ttu-id="4e022-201">Cette fois-ci, hello suivant :</span><span class="sxs-lookup"><span data-stu-id="4e022-201">This time, do hello following:</span></span>

    * <span data-ttu-id="4e022-202">Si vous obtenez trop**Type de visualisation**, sélectionnez **graphique en courbes**.</span><span class="sxs-lookup"><span data-stu-id="4e022-202">When you get too**Visualization Type**, select **Line chart**.</span></span> 
    * <span data-ttu-id="4e022-203">Ajoutez un axe, puis sélectionnez **windowend**.</span><span class="sxs-lookup"><span data-stu-id="4e022-203">Add an axis and select **windowend**.</span></span> 
    * <span data-ttu-id="4e022-204">Ajoutez une valeur, puis sélectionnez **fraudulentcalls**.</span><span class="sxs-lookup"><span data-stu-id="4e022-204">Add a value and select **fraudulentcalls**.</span></span>
    * <span data-ttu-id="4e022-205">Pour **toodisplay de fenêtre de temps**, sélectionnez hello les 10 dernières minutes.</span><span class="sxs-lookup"><span data-stu-id="4e022-205">For **Time window toodisplay**, select hello last 10 minutes.</span></span>

    ![Créer une vignette pour le graphique en courbes](./media/stream-analytics-power-bi-dashboard/pbi-create-tile-line-chart.png)

9. <span data-ttu-id="4e022-207">Cliquez sur **Suivant**, ajoutez un titre et un sous-titre, puis cliquez sur **Appliquer**.</span><span class="sxs-lookup"><span data-stu-id="4e022-207">Click **Next**, add a title and subtitle, and click **Apply**.</span></span>

    <span data-ttu-id="4e022-208">tableau de bord Power BI Hello permet à présent deux vues de données sur les appels frauduleux détectée Bonjour de diffusion en continu de données.</span><span class="sxs-lookup"><span data-stu-id="4e022-208">hello Power BI dashboard now gives you two views of data about fraudulent calls as detected in hello streaming data.</span></span>

    ![Tableau de bord Power BI complété affichant deux vignettes pour les appels frauduleux](./media/stream-analytics-power-bi-dashboard/pbi-dashboard-fraudulent-calls-finished.png)


## <a name="learn-more-about-power-bi"></a><span data-ttu-id="4e022-210">En savoir plus sur Power BI</span><span class="sxs-lookup"><span data-stu-id="4e022-210">Learn more about Power BI</span></span>

<span data-ttu-id="4e022-211">Ce didacticiel montre comment toocreate seulement certains types de visualisations pour un jeu de données.</span><span class="sxs-lookup"><span data-stu-id="4e022-211">This tutorial demonstrates how toocreate only a few kinds of visualizations for a dataset.</span></span> <span data-ttu-id="4e022-212">Power BI peut vous aider à créer d’autres outils d’analyse décisionnelle clients pour votre organisation.</span><span class="sxs-lookup"><span data-stu-id="4e022-212">Power BI can help you create other customer business intelligence tools for your organization.</span></span> <span data-ttu-id="4e022-213">Pour plus d’informations, consultez hello suivant des ressources :</span><span class="sxs-lookup"><span data-stu-id="4e022-213">For more ideas, see hello following resources:</span></span>

* <span data-ttu-id="4e022-214">Pour un autre exemple d’un tableau de bord Power BI, regardez hello [prise en main de Power BI](https://youtu.be/L-Z_6P56aas?t=1m58s) vidéo.</span><span class="sxs-lookup"><span data-stu-id="4e022-214">For another example of a Power BI dashboard, watch hello [Getting Started with Power BI](https://youtu.be/L-Z_6P56aas?t=1m58s) video.</span></span>
* <span data-ttu-id="4e022-215">Pour plus d’informations sur la configuration Analytique de diffusion en continu de la tâche tooPower de sortie BI et à l’aide de groupes Power BI, passez en revue les hello [Power BI](stream-analytics-define-outputs.md#power-bi) section Hello [génère des flux de données Analytique](stream-analytics-define-outputs.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="4e022-215">For more information about configuring Streaming Analytics job output tooPower BI and using Power BI groups, review hello [Power BI](stream-analytics-define-outputs.md#power-bi) section of hello [Stream Analytics outputs](stream-analytics-define-outputs.md) article.</span></span> 
* <span data-ttu-id="4e022-216">Pour plus d’informations sur l’utilisation de Power BI en général, consultez [Tableaux de bord dans Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-dashboards/).</span><span class="sxs-lookup"><span data-stu-id="4e022-216">For information about using Power BI generally, see [Dashboards in Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-dashboards/).</span></span>


## <a name="learn-about-limitations-and-best-practices"></a><span data-ttu-id="4e022-217">En savoir plus sur les limites et les meilleures pratiques</span><span class="sxs-lookup"><span data-stu-id="4e022-217">Learn about limitations and best practices</span></span>
<span data-ttu-id="4e022-218">Actuellement, Power BI peut être appelé environ une fois par seconde.</span><span class="sxs-lookup"><span data-stu-id="4e022-218">Currently, Power BI can be called roughly once per second.</span></span> <span data-ttu-id="4e022-219">Les éléments visuels de streaming prennent en charge des paquets de 15 Ko.</span><span class="sxs-lookup"><span data-stu-id="4e022-219">Streaming visuals support packets of 15 KB.</span></span> <span data-ttu-id="4e022-220">En outre, l’échec de diffusion en continu des éléments visuels (mais push continue toowork).</span><span class="sxs-lookup"><span data-stu-id="4e022-220">Beyond that, streaming visuals fail (but push continues toowork).</span></span> <span data-ttu-id="4e022-221">En raison de ces limitations, Power BI se prête plus naturellement toocases où Analytique de flux de données Azure procède à une réduction significative des données de charge.</span><span class="sxs-lookup"><span data-stu-id="4e022-221">Because of these limitations, Power BI lends itself most naturally toocases where Azure Stream Analytics does a significant data load reduction.</span></span> <span data-ttu-id="4e022-222">Nous vous recommandons d’utiliser une fenêtre bascule ou saut fenêtre tooensure que push de données est au plus un push par seconde, et que votre requête arrive au sein des exigences de débit hello.</span><span class="sxs-lookup"><span data-stu-id="4e022-222">We recommend using a Tumbling window or Hopping window tooensure that data push is at most one push per second, and that your query lands within hello throughput requirements.</span></span>

<span data-ttu-id="4e022-223">Vous pouvez utiliser hello suivant équation toocompute hello valeur toogive votre fenêtre en secondes :</span><span class="sxs-lookup"><span data-stu-id="4e022-223">You can use hello following equation toocompute hello value toogive your window in seconds:</span></span>

![Equation1](./media/stream-analytics-power-bi-dashboard/equation1.png)  

<span data-ttu-id="4e022-225">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="4e022-225">For example:</span></span>

* <span data-ttu-id="4e022-226">Vous disposez de 1 000 appareils qui envoient des données à des intervalles d’une seconde.</span><span class="sxs-lookup"><span data-stu-id="4e022-226">You have 1,000 devices sending data at one-second intervals.</span></span>
* <span data-ttu-id="4e022-227">Vous utilisez hello Power BI Pro référence (SKU) qui prend en charge 1 000 000 lignes par heure.</span><span class="sxs-lookup"><span data-stu-id="4e022-227">You are using hello Power BI Pro SKU that supports 1,000,000 rows per hour.</span></span>
* <span data-ttu-id="4e022-228">Vous souhaitez durée hello toopublish moyenne des données par périphérique tooPower BI.</span><span class="sxs-lookup"><span data-stu-id="4e022-228">You want toopublish hello amount of average data per device tooPower BI.</span></span>

<span data-ttu-id="4e022-229">Par conséquent, les équations hello devient :</span><span class="sxs-lookup"><span data-stu-id="4e022-229">As a result, hello equation becomes:</span></span>

![Equation2](./media/stream-analytics-power-bi-dashboard/equation2.png)  

<span data-ttu-id="4e022-231">Avec cette configuration, vous pouvez modifier les éléments suivants toohello de requête d’origine hello :</span><span class="sxs-lookup"><span data-stu-id="4e022-231">Given this configuration, you can change hello original query toohello following:</span></span>

    SELECT
        MAX(hmdt) AS hmdt,
        MAX(temp) AS temp,
        System.TimeStamp AS time,
        dspl
    INTO "CallStream-PowerBI"
    FROM
        Input TIMESTAMP BY time
    GROUP BY
        TUMBLINGWINDOW(ss,4),
        dspl


### <a name="renew-authorization"></a><span data-ttu-id="4e022-232">Renouveler une autorisation</span><span class="sxs-lookup"><span data-stu-id="4e022-232">Renew authorization</span></span>
<span data-ttu-id="4e022-233">Si un mot de passe hello a changé depuis la création ou de dernière authentification de votre travail, vous devez tooreauthenticate votre compte Power BI.</span><span class="sxs-lookup"><span data-stu-id="4e022-233">If hello password has changed since your job was created or last authenticated, you need tooreauthenticate your Power BI account.</span></span> <span data-ttu-id="4e022-234">Si l’authentification multifacteur Azure est configurée sur votre client Azure Active Directory (Azure AD), vous devez également toorenew d’autorisation de Power BI toutes les deux semaines.</span><span class="sxs-lookup"><span data-stu-id="4e022-234">If Azure Multi-Factor Authentication is configured on your Azure Active Directory (Azure AD) tenant, you also need toorenew Power BI authorization every two weeks.</span></span> <span data-ttu-id="4e022-235">Si vous ne renouvelez pas, vous pouvez constater les symptômes, par exemple l’absence de sortie de la tâche ou un `Authenticate user error` dans les journaux des opérations de hello.</span><span class="sxs-lookup"><span data-stu-id="4e022-235">If you don't renew, you could see symptoms such as a lack of job output or an `Authenticate user error` in hello operation logs.</span></span>

<span data-ttu-id="4e022-236">De même, si un travail démarre après que hello jeton a expiré, une erreur se produit et hello travail échoue.</span><span class="sxs-lookup"><span data-stu-id="4e022-236">Similarly, if a job starts after hello token has expired, an error occurs and hello job fails.</span></span> <span data-ttu-id="4e022-237">tooresolve ce problème, arrêtez tâche hello qui s’exécute et accédez tooyour Power BI de sortie.</span><span class="sxs-lookup"><span data-stu-id="4e022-237">tooresolve this issue, stop hello job that's running and go tooyour Power BI output.</span></span> <span data-ttu-id="4e022-238">perte de données tooavoid, sélectionnez hello **renouveler l’autorisation** lier, puis redémarrez votre travail à partir de hello **heure du dernier arrêt**.</span><span class="sxs-lookup"><span data-stu-id="4e022-238">tooavoid data loss, select hello **Renew authorization** link, and then restart your job from hello **Last Stopped Time**.</span></span>

<span data-ttu-id="4e022-239">Après l’actualisation de l’autorisation de hello avec Power BI, une alerte verte s’affiche dans tooreflect de zone d’autorisation hello que hello problème soit résolu.</span><span class="sxs-lookup"><span data-stu-id="4e022-239">After hello authorization has been refreshed with Power BI, a green alert appears in hello authorization area tooreflect that hello issue has been resolved.</span></span>

## <a name="get-help"></a><span data-ttu-id="4e022-240">Obtenir de l’aide</span><span class="sxs-lookup"><span data-stu-id="4e022-240">Get help</span></span>
<span data-ttu-id="4e022-241">Pour obtenir une assistance, consultez le [forum Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="4e022-241">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4e022-242">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4e022-242">Next steps</span></span>
* [<span data-ttu-id="4e022-243">Introduction tooAzure Analytique de flux de données</span><span class="sxs-lookup"><span data-stu-id="4e022-243">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="4e022-244">Prise en main d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="4e022-244">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="4e022-245">Mise à l'échelle des travaux Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="4e022-245">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="4e022-246">Références sur le langage des requêtes Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="4e022-246">Azure Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="4e022-247">Références sur l’API REST de gestion d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="4e022-247">Azure Stream Analytics Management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
