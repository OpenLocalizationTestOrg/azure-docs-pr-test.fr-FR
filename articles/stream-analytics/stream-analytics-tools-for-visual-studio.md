---
title: aaaUse Azure flux Analytique Tools pour Visual Studio | Documents Microsoft
description: Didacticiel de mise en route pour hello Azure flux Analytique Tools pour Visual Studio
keywords: visual studio
documentationcenter: 
services: stream-analytics
author: 
manager: 
editor: 
ms.assetid: a473ea0a-3eaa-4e5b-aaa1-fec7e9069f20
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 
ms.author: 
ms.openlocfilehash: bda8e548040509a6f29f1b713268bc38f73228fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-stream-analytics-tools-for-visual-studio"></a><span data-ttu-id="ead3a-104">Utilisation d’outils Azure Stream Analytics pour Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ead3a-104">Use Azure Stream Analytics Tools for Visual Studio</span></span>
## <a name="introduction"></a><span data-ttu-id="ead3a-105">Introduction</span><span class="sxs-lookup"><span data-stu-id="ead3a-105">Introduction</span></span>
<span data-ttu-id="ead3a-106">Dans ce didacticiel, vous découvrez comment l’Analytique du flux toouse Azure Tools pour Visual Studio toocreate, créer, tester localement, gérer et déboguer vos tâches de flux de données Analytique.</span><span class="sxs-lookup"><span data-stu-id="ead3a-106">In this tutorial, you learn how toouse Azure Stream Analytics Tools for Visual Studio toocreate, author, test locally, manage, and debug your Stream Analytics jobs.</span></span> 

<span data-ttu-id="ead3a-107">Après avoir effectué ce didacticiel, vous pourrez :</span><span class="sxs-lookup"><span data-stu-id="ead3a-107">After completing this tutorial, you will be able to:</span></span>
* <span data-ttu-id="ead3a-108">bien connaître les outils Stream Analytics pour Visual Studio ;</span><span class="sxs-lookup"><span data-stu-id="ead3a-108">Familiarize yourself with Stream Analytics Tools for Visual Studio.</span></span>
* <span data-ttu-id="ead3a-109">configurer et déployer un travail Stream Analytics ;</span><span class="sxs-lookup"><span data-stu-id="ead3a-109">Configure and deploy a Stream Analytics job.</span></span>
* <span data-ttu-id="ead3a-110">tester votre travail en local avec des exemples de données locaux ;</span><span class="sxs-lookup"><span data-stu-id="ead3a-110">Test your job locally with local sample data.</span></span>
* <span data-ttu-id="ead3a-111">Analyse des problèmes de tootroubleshoot à utiliser.</span><span class="sxs-lookup"><span data-stu-id="ead3a-111">Use monitoring tootroubleshoot issues.</span></span>
* <span data-ttu-id="ead3a-112">Exporter tooprojects de travaux existants.</span><span class="sxs-lookup"><span data-stu-id="ead3a-112">Export existing jobs tooprojects.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ead3a-113">Composants requis</span><span class="sxs-lookup"><span data-stu-id="ead3a-113">Prerequisites</span></span>
<span data-ttu-id="ead3a-114">toocomplete ce didacticiel, vous devez hello suivant des conditions préalables :</span><span class="sxs-lookup"><span data-stu-id="ead3a-114">toocomplete this tutorial, you need hello following prerequisites:</span></span>
* <span data-ttu-id="ead3a-115">Terminer les étapes hello qui précèdent « Créer une tâche de flux de données Analytique » Bonjour [générer une solution IoT à l’aide du didacticiel de flux de données Analytique](https://docs.microsoft.com/azure/stream-analytics/stream-analytics-build-an-iot-solution-using-stream-analytics).</span><span class="sxs-lookup"><span data-stu-id="ead3a-115">Finish hello steps that precede "Create a Stream Analytics job" in hello [Build an IoT solution by using Stream Analytics tutorial](https://docs.microsoft.com/azure/stream-analytics/stream-analytics-build-an-iot-solution-using-stream-analytics).</span></span> 
* <span data-ttu-id="ead3a-116">Utilisez Visual Studio 2015, Visual Studio 2013 mise à jour 4 ou Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="ead3a-116">Use Visual Studio 2015, Visual Studio 2013 update 4, or Visual Studio 2012.</span></span> <span data-ttu-id="ead3a-117">Les éditions Enterprise (Ultimate/Premium), Professional et Community sont prises en charge.</span><span class="sxs-lookup"><span data-stu-id="ead3a-117">Enterprise (Ultimate/Premium), Professional, and Community editions are supported.</span></span> <span data-ttu-id="ead3a-118">L’édition Express n’est pas prise en charge.</span><span class="sxs-lookup"><span data-stu-id="ead3a-118">Express edition is not supported.</span></span> <span data-ttu-id="ead3a-119">Visual Studio 2017 n’est pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="ead3a-119">Visual Studio 2017 is not supported.</span></span> 
* <span data-ttu-id="ead3a-120">Hello d’utiliser Azure SDK pour .NET version 2.7.1 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="ead3a-120">Use hello Azure SDK for .NET version 2.7.1 or later.</span></span> <span data-ttu-id="ead3a-121">Installez-le à l’aide de hello [le programme d’installation de Web platform](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="ead3a-121">Install it by using hello [Web platform installer](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
* <span data-ttu-id="ead3a-122">Installer hello [outils Analytique de flux de données pour Visual Studio](http://aka.ms/asatoolsvs).</span><span class="sxs-lookup"><span data-stu-id="ead3a-122">Install hello [Stream Analytics Tools for Visual Studio](http://aka.ms/asatoolsvs).</span></span>

## <a name="create-a-stream-analytics-project"></a><span data-ttu-id="ead3a-123">Créer un projet Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="ead3a-123">Create a Stream Analytics project</span></span>
1. <span data-ttu-id="ead3a-124">Dans Visual Studio, cliquez sur hello **fichier** menu et sélectionnez **nouveau projet**.</span><span class="sxs-lookup"><span data-stu-id="ead3a-124">In Visual Studio, click hello **File** menu and select **New Project**.</span></span> 

2. <span data-ttu-id="ead3a-125">Dans la liste des modèles hello sur hello gauche, sélectionnez **flux Analytique** puis cliquez sur **Application Analytique de flux de données Azure**.</span><span class="sxs-lookup"><span data-stu-id="ead3a-125">In hello templates list on hello left, select **Stream Analytics** and then click **Azure Stream Analytics Application**.</span></span>

3. <span data-ttu-id="ead3a-126">Entrez le projet de hello **nom**, **emplacement**, et **nom de la Solution** comme vous le feriez pour d’autres projets.</span><span class="sxs-lookup"><span data-stu-id="ead3a-126">Enter hello project **Name**, **Location**, and **Solution name** as you do for other projects.</span></span>

    ![Fenêtre Nouveau projet](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-create-project-01.png)

    <span data-ttu-id="ead3a-128">Un projet **Toll** est généré dans l’**Explorateur de solutions**.</span><span class="sxs-lookup"><span data-stu-id="ead3a-128">A **Toll** project is generated in **Solution Explorer**.</span></span>

    ![Projet Toll généré dans l’Explorateur de solutions](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-create-project-02.png)

## <a name="choose-hello-correct-subscription"></a><span data-ttu-id="ead3a-130">Choisissez l’abonnement approprié de hello</span><span class="sxs-lookup"><span data-stu-id="ead3a-130">Choose hello correct subscription</span></span>
1. <span data-ttu-id="ead3a-131">Dans Visual Studio, cliquez sur hello **vue** menu et ouvrez **l’Explorateur de serveurs**.</span><span class="sxs-lookup"><span data-stu-id="ead3a-131">In Visual Studio, click hello **View** menu and open **Server Explorer**.</span></span>

2. <span data-ttu-id="ead3a-132">Connectez-vous à votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="ead3a-132">Sign in with your Azure Account.</span></span> 

## <a name="define-hello-input-sources"></a><span data-ttu-id="ead3a-133">Définir des sources d’entrée hello</span><span class="sxs-lookup"><span data-stu-id="ead3a-133">Define hello input sources</span></span>
1.  <span data-ttu-id="ead3a-134">Dans **l’Explorateur de solutions**, développez hello **entrées** nœud et renommer **Input.json** trop**EntryStream.json**.</span><span class="sxs-lookup"><span data-stu-id="ead3a-134">In **Solution Explorer**, expand hello **Inputs** node and rename **Input.json** too**EntryStream.json**.</span></span> <span data-ttu-id="ead3a-135">Double-cliquez sur **EntryStream.json**.</span><span class="sxs-lookup"><span data-stu-id="ead3a-135">Double-click **EntryStream.json**.</span></span>
2.  <span data-ttu-id="ead3a-136">Hello **Alias d’entrée** est désormais **EntryStream**.</span><span class="sxs-lookup"><span data-stu-id="ead3a-136">hello **Input Alias** is now **EntryStream**.</span></span> <span data-ttu-id="ead3a-137">alias de Hello d’entrée est utilisé dans le script de requête hello.</span><span class="sxs-lookup"><span data-stu-id="ead3a-137">hello input alias is used in hello query script.</span></span> 
3.  <span data-ttu-id="ead3a-138">Dans **Type de source**, sélectionnez **Data Stream**.</span><span class="sxs-lookup"><span data-stu-id="ead3a-138">In **Source Type**, select **Data Stream**.</span></span>
4.  <span data-ttu-id="ead3a-139">Dans **Source**, sélectionnez **Event Hub**.</span><span class="sxs-lookup"><span data-stu-id="ead3a-139">In **Source**, select **Event Hub**.</span></span>
5.  <span data-ttu-id="ead3a-140">Dans **Service Bus Namespace**, sélectionnez hello **TollData** option.</span><span class="sxs-lookup"><span data-stu-id="ead3a-140">In **Service Bus Namespace**, select hello **TollData** option.</span></span>
6.  <span data-ttu-id="ead3a-141">Dans **Nom du hub d’événements**, sélectionnez **entry**.</span><span class="sxs-lookup"><span data-stu-id="ead3a-141">In **Event Hub Name**, select **entry**.</span></span>
7.  <span data-ttu-id="ead3a-142">Dans **nom de la stratégie concentrateur d’événements**, sélectionnez **RootManageSharedAccessKey** (valeur par défaut de hello).</span><span class="sxs-lookup"><span data-stu-id="ead3a-142">In **Event Hub Policy Name**, select **RootManageSharedAccessKey** (hello default value).</span></span>
8.  <span data-ttu-id="ead3a-143">Dans **Format de sérialisation de l’événement**, sélectionnez **Json**.</span><span class="sxs-lookup"><span data-stu-id="ead3a-143">In **Event Serialization Format**, select **Json**.</span></span> 
9.  <span data-ttu-id="ead3a-144">Dans **Encodage**, sélectionnez **UTF8**.</span><span class="sxs-lookup"><span data-stu-id="ead3a-144">In **Encoding**, select **UTF8**.</span></span> <span data-ttu-id="ead3a-145">Vos paramètres doivent ressembler à hello suivant capture d’écran :</span><span class="sxs-lookup"><span data-stu-id="ead3a-145">Your settings should look like hello following screenshot:</span></span>

    ![Fenêtre Entrée](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-01.png)
 
10. <span data-ttu-id="ead3a-147">Assistant de hello toofinish, cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="ead3a-147">toofinish hello wizard, click **Save**.</span></span> <span data-ttu-id="ead3a-148">Vous pouvez maintenant ajouter un autre flux de sortie hello toocreate source d’entrée.</span><span class="sxs-lookup"><span data-stu-id="ead3a-148">Now you can add another input source toocreate hello exit stream.</span></span> <span data-ttu-id="ead3a-149">Avec le bouton hello **entrées** nœud et sélectionnez **un nouvel élément**.</span><span class="sxs-lookup"><span data-stu-id="ead3a-149">Right-click hello **Inputs** node, and select **New Item**.</span></span>

    ![Nouvel élément](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-02.png)
 
11. <span data-ttu-id="ead3a-151">Dans la fenêtre hello, sélectionnez **Azure flux Analytique Entrée**et modifier hello **nom** trop**ExitStream.json**.</span><span class="sxs-lookup"><span data-stu-id="ead3a-151">In hello window, select **Azure Stream Analytics Input**, and change hello **Name** too**ExitStream.json**.</span></span> <span data-ttu-id="ead3a-152">Cliquez sur **Add**.</span><span class="sxs-lookup"><span data-stu-id="ead3a-152">Click **Add**.</span></span>

    ![Fenêtre Ajouter un nouvel élément](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-03.png)
 
12. <span data-ttu-id="ead3a-154">Double-cliquez sur **ExitStream.json** hello projet et hello suivent même étapes comme vous l’avez fait pour le flux d’entrée hello.</span><span class="sxs-lookup"><span data-stu-id="ead3a-154">Double-click **ExitStream.json** in hello project, and follow hello same steps as you did for hello entry stream.</span></span> <span data-ttu-id="ead3a-155">Être vraiment tooenter **quitter** pour hello **nom de Hub d’événements** comme indiqué dans hello suivant capture d’écran :</span><span class="sxs-lookup"><span data-stu-id="ead3a-155">Be sure tooenter **exit** for hello **Event Hub Name** as shown in hello following screenshot:</span></span>

    ![Fenêtre ExitStream](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-04.png)

    <span data-ttu-id="ead3a-157">Vous avez maintenant défini deux flux d’entrée de données :</span><span class="sxs-lookup"><span data-stu-id="ead3a-157">Now you have defined two input streams:</span></span>

    ![Flux d’entrée et de sortie](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-05.png)
 
    <span data-ttu-id="ead3a-159">Ensuite, ajoutez des entrées de données de référence pour le fichier blob hello qui contient les données d’inscription de voiture.</span><span class="sxs-lookup"><span data-stu-id="ead3a-159">Next, add reference data input for hello blob file that contains car registration data.</span></span>

13. <span data-ttu-id="ead3a-160">Avec le bouton hello **entrées** nœud dans le projet de hello, puis hello suivent même étapes comme vous l’avez fait pour les entrées de flux hello.</span><span class="sxs-lookup"><span data-stu-id="ead3a-160">Right-click hello **Inputs** node in hello project, and then follow hello same steps as you did for hello stream inputs.</span></span> <span data-ttu-id="ead3a-161">Dans **Alias d’entrée**, entrez **Registration**, et dans **Type de Source**, sélectionnez **Reference data**.</span><span class="sxs-lookup"><span data-stu-id="ead3a-161">In **Input Alias**, enter **Registration**, and in **Source Type**, select **Reference data**.</span></span>

    ![Fenêtre Inscription](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-06.png)

14. <span data-ttu-id="ead3a-163">Dans **compte de stockage**, sélectionnez hello **tolldata** option.</span><span class="sxs-lookup"><span data-stu-id="ead3a-163">In **Storage Account**, select hello **tolldata** option.</span></span> <span data-ttu-id="ead3a-164">Dans **Conteneur**, sélectionnez **tolldata**, et dans **Modèle de chemin d’accès**, entrez **registration.json**.</span><span class="sxs-lookup"><span data-stu-id="ead3a-164">In **Container**, select **tolldata**, and in **Path Pattern**, enter **registration.json**.</span></span> <span data-ttu-id="ead3a-165">Ce nom de fichier respecte la casse et doit être en minuscules.</span><span class="sxs-lookup"><span data-stu-id="ead3a-165">This file name is case sensitive and should be lowercase.</span></span>
15. <span data-ttu-id="ead3a-166">Assistant de hello toofinish, cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="ead3a-166">toofinish hello wizard, click **Save**.</span></span>

<span data-ttu-id="ead3a-167">Maintenant, toutes les entrées de hello sont définies.</span><span class="sxs-lookup"><span data-stu-id="ead3a-167">Now all hello inputs are defined.</span></span>

## <a name="define-hello-output"></a><span data-ttu-id="ead3a-168">Définir la sortie de hello</span><span class="sxs-lookup"><span data-stu-id="ead3a-168">Define hello output</span></span>
1.  <span data-ttu-id="ead3a-169">Dans **l’Explorateur de solutions**, développez hello **entrées** nœud et double-cliquez sur **Output.json**.</span><span class="sxs-lookup"><span data-stu-id="ead3a-169">In **Solution Explorer**, expand hello **Inputs** node and double-click **Output.json**.</span></span>

2.  <span data-ttu-id="ead3a-170">Dans **Alias de sortie**, entrez **output**.</span><span class="sxs-lookup"><span data-stu-id="ead3a-170">In **Output Alias**, enter **output**.</span></span> 
3.  <span data-ttu-id="ead3a-171">Dans **Récepteur**, sélectionnez **SQL Database**.</span><span class="sxs-lookup"><span data-stu-id="ead3a-171">In **Sink**, select **SQL Database**.</span></span>
4.  <span data-ttu-id="ead3a-172">Dans **Base de données**, sélectionnez **TollDataDB**.</span><span class="sxs-lookup"><span data-stu-id="ead3a-172">In **Database**, select **TollDataDB**.</span></span>
5.  <span data-ttu-id="ead3a-173">Dans **Nom d’utilisateur**, entrez **tolladmin**.</span><span class="sxs-lookup"><span data-stu-id="ead3a-173">In **User Name**, enter **tolladmin**.</span></span> 
6.  <span data-ttu-id="ead3a-174">Dans **Mot de passe**, entrez **123toll!**.</span><span class="sxs-lookup"><span data-stu-id="ead3a-174">In **Password**, enter **123toll!**.</span></span>
7.  <span data-ttu-id="ead3a-175">Dans **Table**, entrez **TollDataRefJoin**.</span><span class="sxs-lookup"><span data-stu-id="ead3a-175">In **Table**, enter **TollDataRefJoin**.</span></span>
8.  <span data-ttu-id="ead3a-176">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="ead3a-176">Click **Save**.</span></span>

    ![Fenêtre Sortie](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-output-01.png)
 
## <a name="create-a-stream-analytics-query"></a><span data-ttu-id="ead3a-178">Créer une requête Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="ead3a-178">Create a Stream Analytics query</span></span>
<span data-ttu-id="ead3a-179">Ce didacticiel tentatives tooanswer plusieurs questions qui sont des données de tootoll connexes.</span><span class="sxs-lookup"><span data-stu-id="ead3a-179">This tutorial attempts tooanswer several business questions that are related tootoll data.</span></span> <span data-ttu-id="ead3a-180">Il crée également des requêtes de flux de données Analytique qui peuvent être utilisés dans les réponses correspondantes de flux de données Analytique tooprovide.</span><span class="sxs-lookup"><span data-stu-id="ead3a-180">It also constructs Stream Analytics queries that can be used in Stream Analytics tooprovide relevant answers.</span></span>
<span data-ttu-id="ead3a-181">Avant de commencer votre premier travail Analytique des flux de données, examinons une syntaxe de requête simple scénario et hello.</span><span class="sxs-lookup"><span data-stu-id="ead3a-181">Before you start your first Stream Analytics job, let’s explore a simple scenario and hello query syntax.</span></span>

### <a name="introduction-toohello-stream-analytics-query-language"></a><span data-ttu-id="ead3a-182">Introduction toohello langage de requête Analytique de flux de données</span><span class="sxs-lookup"><span data-stu-id="ead3a-182">Introduction toohello Stream Analytics query language</span></span>
<span data-ttu-id="ead3a-183">Supposons que vous devez toocount hello de véhicules qui permet d’entrer une gare de péage.</span><span class="sxs-lookup"><span data-stu-id="ead3a-183">Let’s say that you need toocount hello number of vehicles that enter a toll booth.</span></span> <span data-ttu-id="ead3a-184">Cet exemple est un flux continu d’événements, vous devez toodefine une période de temps.</span><span class="sxs-lookup"><span data-stu-id="ead3a-184">Because this example is a continuous stream of events, you have toodefine a period of time.</span></span> <span data-ttu-id="ead3a-185">Modifier hello toobe de question « Combien de véhicules entrer une gare de péage toutes les trois minutes » ?</span><span class="sxs-lookup"><span data-stu-id="ead3a-185">Modify hello question toobe “How many vehicles enter a toll booth every three minutes?”</span></span> <span data-ttu-id="ead3a-186">Cette toocount de manière les données sont souvent appelée tooas hello bascule count.</span><span class="sxs-lookup"><span data-stu-id="ead3a-186">This way toocount data is commonly referred tooas hello tumbling count.</span></span>

<span data-ttu-id="ead3a-187">Examinez la requête de flux de données Analytique hello qui répond à cette question :</span><span class="sxs-lookup"><span data-stu-id="ead3a-187">Look at hello Stream Analytics query that answers this question:</span></span>

        SELECT TollId, System.Timestamp AS WindowEnd, COUNT(*) AS Count 
        FROM EntryStream TIMESTAMP BY EntryTime 
        GROUP BY TUMBLINGWINDOW(minute, 3), TollId 

<span data-ttu-id="ead3a-188">Flux de données Analytique utilise un langage de requête tel que SQL et ajoute quelques extensions toospecify liées au temps aspects de hello requête.</span><span class="sxs-lookup"><span data-stu-id="ead3a-188">Stream Analytics uses a query language that's like SQL and adds a few extensions toospecify time-related aspects of hello query.</span></span>

<span data-ttu-id="ead3a-189">Pour plus d’informations, consultez [gestion du temps](https://msdn.microsoft.com/library/azure/mt582045.aspx) et [fenêtrage](https://msdn.microsoft.com/library/azure/dn835019.aspx) constructions utilisées dans la requête hello à partir de MSDN.</span><span class="sxs-lookup"><span data-stu-id="ead3a-189">For more information, see [Time Management](https://msdn.microsoft.com/library/azure/mt582045.aspx) and [Windowing](https://msdn.microsoft.com/library/azure/dn835019.aspx) constructs used in hello query from MSDN.</span></span>

<span data-ttu-id="ead3a-190">Maintenant que vous avez écrit votre première requête Analytique de flux de données, il est temps tootest il.</span><span class="sxs-lookup"><span data-stu-id="ead3a-190">Now that you have written your first Stream Analytics query, it's time tootest it.</span></span> <span data-ttu-id="ead3a-191">Utilisez les fichiers de données d’exemple hello situés dans le dossier TollApp hello suivant le chemin d’accès :</span><span class="sxs-lookup"><span data-stu-id="ead3a-191">Use hello sample data files located in your TollApp folder in hello following path:</span></span>

<span data-ttu-id="ead3a-192">..\TollApp\TollApp\Data</span><span class="sxs-lookup"><span data-stu-id="ead3a-192">..\TollApp\TollApp\Data</span></span>

<span data-ttu-id="ead3a-193">Ce dossier contient les fichiers suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="ead3a-193">This folder contains hello following files:</span></span>
*   <span data-ttu-id="ead3a-194">Entry.json</span><span class="sxs-lookup"><span data-stu-id="ead3a-194">Entry.json</span></span>
*   <span data-ttu-id="ead3a-195">Exit.json</span><span class="sxs-lookup"><span data-stu-id="ead3a-195">Exit.json</span></span>
*   <span data-ttu-id="ead3a-196">registration.json</span><span class="sxs-lookup"><span data-stu-id="ead3a-196">Registration.json</span></span>

## <a name="count-hello-number-of-vehicles-entering-a-toll-booth"></a><span data-ttu-id="ead3a-197">Nombre hello véhicules entrant une gare de péage</span><span class="sxs-lookup"><span data-stu-id="ead3a-197">Count hello number of vehicles entering a toll booth</span></span>
<span data-ttu-id="ead3a-198">Dans le projet de hello, double-cliquez sur **Script.asaql** script hello tooopen hello **l’éditeur de requête**.</span><span class="sxs-lookup"><span data-stu-id="ead3a-198">In hello project, double-click **Script.asaql** tooopen hello script in hello **Query Editor**.</span></span> <span data-ttu-id="ead3a-199">Copiez et collez le script de hello dans la section précédente de hello dans l’éditeur de hello.</span><span class="sxs-lookup"><span data-stu-id="ead3a-199">Copy and paste hello script in hello previous section into hello editor.</span></span> <span data-ttu-id="ead3a-200">Hello éditeur de requête prend en charge IntelliSense, la coloration de syntaxe et erroné hello.</span><span class="sxs-lookup"><span data-stu-id="ead3a-200">hello Query Editor supports IntelliSense, syntax coloring, and hello error marker.</span></span>

![Éditeur de requête](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-query-01.png)
 
### <a name="test-stream-analytics-queries-locally"></a><span data-ttu-id="ead3a-202">Tester localement les requêtes Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="ead3a-202">Test Stream Analytics queries locally</span></span>

1. <span data-ttu-id="ead3a-203">toocompile hello requête toosee s’il existe une erreur de syntaxe, droit hello projet, puis sélectionnez **Build**.</span><span class="sxs-lookup"><span data-stu-id="ead3a-203">toocompile hello query toosee if there is a syntax error, right-click hello project and select **Build**.</span></span> 

2. <span data-ttu-id="ead3a-204">toovalidate cette requête par rapport à des exemples de données, vous pouvez utiliser les données local.</span><span class="sxs-lookup"><span data-stu-id="ead3a-204">toovalidate this query against sample data, you can use local sample data.</span></span> <span data-ttu-id="ead3a-205">Entrée de hello d’avec le bouton droit, puis sélectionnez **Ajouter entrée locale**.</span><span class="sxs-lookup"><span data-stu-id="ead3a-205">Right-click hello input, and select **Add local input**.</span></span>

    ![Ajouter une entrée locale](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-01.png)
 
3. <span data-ttu-id="ead3a-207">Dans la fenêtre contextuelle de hello, sélectionnez les données d’exemple hello à partir de votre chemin d’accès local.</span><span class="sxs-lookup"><span data-stu-id="ead3a-207">In hello pop-up window, select hello sample data from your local path.</span></span> <span data-ttu-id="ead3a-208">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="ead3a-208">Click **Save**.</span></span>

    ![Fenêtre Ajouter une entrée locale](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-02.png)
 
    <span data-ttu-id="ead3a-210">Un fichier nommé **local_EntryStream.json** est automatiquement ajouté le dossier d’entrées tooyour.</span><span class="sxs-lookup"><span data-stu-id="ead3a-210">A file named **local_EntryStream.json** is automatically added tooyour inputs folder.</span></span>

    ![Dossier ajouté tooinputs de fichier](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-03.png)
 
4. <span data-ttu-id="ead3a-212">Bonjour **l’éditeur de requête**, cliquez sur **exécuter localement**.</span><span class="sxs-lookup"><span data-stu-id="ead3a-212">In hello **Query Editor**, click **Run Locally**.</span></span> <span data-ttu-id="ead3a-213">Ou vous pouvez appuyer hello F5.</span><span class="sxs-lookup"><span data-stu-id="ead3a-213">Or you can press hello F5 key.</span></span>

    ![Exécution locale](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-local-run-01.png)

    ![Sortie de l’exécution locale](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-local-run-02.png)

    <span data-ttu-id="ead3a-216">Appuyez sur la touche de sortie de hello tooview clé Bonjour **résultat d’exécution Local ASA** fenêtre dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ead3a-216">Press any key tooview hello output in hello **ASA Local Run Result** window in Visual Studio.</span></span> 

    ![Fenêtre Résultats de l’exécution locale ASA](./media/stream-analytics-tools-for-vs/local-testing-output.png)

5. <span data-ttu-id="ead3a-218">Cliquez sur **ouvrir le dossier résultat** des fichiers de sortie de hello toocheck tous deux au format CSV et JSON.</span><span class="sxs-lookup"><span data-stu-id="ead3a-218">Click **Open Result Folder** toocheck hello output files both in CSV and JSON format.</span></span>

    ![Sortie Ouvrir le dossier des résultats](./media/stream-analytics-tools-for-vs/local-testing-files.png)
 

### <a name="sample-hello-input-data"></a><span data-ttu-id="ead3a-220">Exemples de données d’entrée hello</span><span class="sxs-lookup"><span data-stu-id="ead3a-220">Sample hello input data</span></span>
<span data-ttu-id="ead3a-221">Vous pouvez également des exemples de données d’entrée à partir du fichier local tooa de sources d’entrée.</span><span class="sxs-lookup"><span data-stu-id="ead3a-221">You can also sample input data from input sources tooa local file.</span></span> 
1. <span data-ttu-id="ead3a-222">Cliquez sur le fichier de configuration d’entrée hello, puis sélectionnez **Sample Data**.</span><span class="sxs-lookup"><span data-stu-id="ead3a-222">Right-click hello input config file, and select **Sample Data**.</span></span> 

   ![Exemple de données](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-01.png)

    <span data-ttu-id="ead3a-224">Pour l’instant, vous pouvez uniquement échantillonner le hub d’événements ou le hub IoT.</span><span class="sxs-lookup"><span data-stu-id="ead3a-224">You can sample only event hub or IoT hub for now.</span></span> <span data-ttu-id="ead3a-225">Les autres sources d’entrée ne sont pas prises en charge.</span><span class="sxs-lookup"><span data-stu-id="ead3a-225">Other input sources are not supported.</span></span>

2. <span data-ttu-id="ead3a-226">Dans la fenêtre contextuelle de hello, entrez hello chemin d’accès local utilisé toosave hello exemples de données.</span><span class="sxs-lookup"><span data-stu-id="ead3a-226">In hello pop-up window, enter hello local path used toosave hello sample data.</span></span> <span data-ttu-id="ead3a-227">Cliquez sur **Exemple**.</span><span class="sxs-lookup"><span data-stu-id="ead3a-227">Click **Sample**.</span></span>

    ![Fenêtre Exemples de données](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-02.png)
 
    <span data-ttu-id="ead3a-229">Vous pouvez voir la progression hello Bonjour **sortie** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="ead3a-229">You can see hello progress in hello **Output** window.</span></span> 

    ![Fenêtre Sortie](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-03.png)
 
### <a name="submit-a-stream-analytics-query-tooazure"></a><span data-ttu-id="ead3a-231">Envoyer un tooAzure de requête Analytique de flux de données</span><span class="sxs-lookup"><span data-stu-id="ead3a-231">Submit a Stream Analytics query tooAzure</span></span>
1. <span data-ttu-id="ead3a-232">Bonjour **l’éditeur de requête**, cliquez sur **envoyer tooAzure** dans l’éditeur de script hello.</span><span class="sxs-lookup"><span data-stu-id="ead3a-232">In hello **Query Editor**, click **Submit tooAzure** in hello script editor.</span></span>

    ![Envoyer tooAzure](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-submit-job-01.png)
 
2. <span data-ttu-id="ead3a-234">Sélectionnez **Créer une tâche Azure Stream Analytics**.</span><span class="sxs-lookup"><span data-stu-id="ead3a-234">Select **Create a New Azure Stream Analytics Job**.</span></span> <span data-ttu-id="ead3a-235">Entrez hello **nom de la tâche**et sélectionnez hello correct **abonnement**.</span><span class="sxs-lookup"><span data-stu-id="ead3a-235">Enter hello **Job Name**, and select hello correct **Subscription**.</span></span> <span data-ttu-id="ead3a-236">Cliquez sur **Envoyer**.</span><span class="sxs-lookup"><span data-stu-id="ead3a-236">Click **Submit**.</span></span>

    ![Fenêtre Envoyer la tâche](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-submit-job-02.png)

 
### <a name="start-a-job"></a><span data-ttu-id="ead3a-238">Démarrer une tâche</span><span class="sxs-lookup"><span data-stu-id="ead3a-238">Start a job</span></span>
<span data-ttu-id="ead3a-239">Maintenant que votre travail est créé, vue de tâche hello est ouvert automatiquement.</span><span class="sxs-lookup"><span data-stu-id="ead3a-239">Now that your job is created, hello job view is automatically opened.</span></span> 
1. <span data-ttu-id="ead3a-240">toostart hello des tâches, cliquez sur hello **flèche verte** bouton.</span><span class="sxs-lookup"><span data-stu-id="ead3a-240">toostart hello job, click hello **green arrow** button.</span></span>

    ![Démarrer une tâche](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-01.png)
 
2. <span data-ttu-id="ead3a-242">Sélectionnez le paramètre par défaut de hello, puis cliquez sur **Démarrer**.</span><span class="sxs-lookup"><span data-stu-id="ead3a-242">Select hello default setting, and click **Start**.</span></span>
 
    ![Fenêtre Démarrer une tâche](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-02.png)

    <span data-ttu-id="ead3a-244">travail de Hello **état** change également**en cours d’exécution**, et **événements d’entrée** et **événements de sortie** s’affichent.</span><span class="sxs-lookup"><span data-stu-id="ead3a-244">hello job **Status** changes too**Running**, and **Input Events** and **Output Events** appear.</span></span>

    ![État en cours d’exécution dans Résumé de la tâche](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-03.png)

## <a name="check-hello-results-in-visual-studio"></a><span data-ttu-id="ead3a-246">Vérifier les résultats de hello dans Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ead3a-246">Check hello results in Visual Studio</span></span>
1. <span data-ttu-id="ead3a-247">Dans Visual Studio, ouvrez **l’Explorateur de serveurs** et avec le bouton hello **TollDataRefJoin** table.</span><span class="sxs-lookup"><span data-stu-id="ead3a-247">In Visual Studio, open **Server Explorer** and right-click hello **TollDataRefJoin** table.</span></span>
2. <span data-ttu-id="ead3a-248">Sélectionnez **afficher les données de Table** sortie de hello toosee de votre travail.</span><span class="sxs-lookup"><span data-stu-id="ead3a-248">Select **Show Table Data** toosee hello output of your job.</span></span>
   
    ![Sélection de l’option Afficher les données de la table dans l’Explorateur de serveurs](media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-check-results.jpg)


### <a name="view-hello-job-metrics"></a><span data-ttu-id="ead3a-250">Métriques de travail vue hello</span><span class="sxs-lookup"><span data-stu-id="ead3a-250">View hello job metrics</span></span>
<span data-ttu-id="ead3a-251">Certaines statistiques des tâches de base se trouvent dans **Métriques de tâche**.</span><span class="sxs-lookup"><span data-stu-id="ead3a-251">Some basic job statistics can be found in **Job Metrics**.</span></span> 

![Fenêtre Métriques de tâche](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-job-metrics-01.png)

 
## <a name="list-hello-job-in-server-explorer"></a><span data-ttu-id="ead3a-253">Tâche hello de liste dans l’Explorateur de serveurs</span><span class="sxs-lookup"><span data-stu-id="ead3a-253">List hello job in Server Explorer</span></span>
<span data-ttu-id="ead3a-254">Dans l’**Explorateur de serveurs**, cliquez sur **Tâches Stream Analytics**, puis sur **Actualiser**.</span><span class="sxs-lookup"><span data-stu-id="ead3a-254">In **Server Explorer**, click **Stream Analytics Jobs** and then click **Refresh**.</span></span> <span data-ttu-id="ead3a-255">travail de Hello apparaît sous **des tâches de flux de données Analytique**.</span><span class="sxs-lookup"><span data-stu-id="ead3a-255">hello job appears under **Stream Analytics jobs**.</span></span>

![Tâches Stream Analytics répertoriées dans l’Explorateur de serveurs](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-list-jobs-01.png)


## <a name="open-hello-job-view"></a><span data-ttu-id="ead3a-257">Vue du travail hello ouvert</span><span class="sxs-lookup"><span data-stu-id="ead3a-257">Open hello job view</span></span>
<span data-ttu-id="ead3a-258">mode de travail tooopen hello, développez le nœud de votre travail et double-cliquez sur hello **vue des travaux** nœud.</span><span class="sxs-lookup"><span data-stu-id="ead3a-258">tooopen hello job view, expand your job node and double-click hello **Job View** node.</span></span>

![Nœud Vue de la tâche](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-job-view-01.png)


## <a name="export-an-existing-job-tooa-project"></a><span data-ttu-id="ead3a-260">Exporter un projet tooa de travail existant</span><span class="sxs-lookup"><span data-stu-id="ead3a-260">Export an existing job tooa project</span></span>
<span data-ttu-id="ead3a-261">Il existe deux façons, vous pouvez exporter un projet tooa de travail existant.</span><span class="sxs-lookup"><span data-stu-id="ead3a-261">There are two ways you can export an existing job tooa project.</span></span>

<span data-ttu-id="ead3a-262">Dans **l’Explorateur de serveurs**, nœud de travail avec le bouton hello Bonjour **des travaux Stream Analytique** nœud et sélectionnez **exporter tooNew flux Analytique projet**.</span><span class="sxs-lookup"><span data-stu-id="ead3a-262">In **Server Explorer**, right-click hello job node in hello **Stream Analytics Jobs** node and select **Export tooNew Stream Analytics Project**.</span></span>

![Exportation tooNew projet Analytique de flux de données](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-01.png)

<span data-ttu-id="ead3a-264">projet de Hello est généré dans **l’Explorateur de solutions**.</span><span class="sxs-lookup"><span data-stu-id="ead3a-264">hello project is generated in **Solution Explorer**.</span></span>

![Projet généré dans l’Explorateur de solutions](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-02.png)
 
<span data-ttu-id="ead3a-266">Vous également pourrez utiliser le mode de travail hello, puis cliquez sur **générer le projet**.</span><span class="sxs-lookup"><span data-stu-id="ead3a-266">You also can use hello job view, and click **Generate Project**.</span></span>

![Générer le projet](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-03.png)

## <a name="known-issues-and-limitations"></a><span data-ttu-id="ead3a-268">Problèmes connus et limitations</span><span class="sxs-lookup"><span data-stu-id="ead3a-268">Known issues and limitations</span></span>
 
- <span data-ttu-id="ead3a-269">Il n’existe aucune prise en charge pour la sortie Power BI et la sortie d’Azure Date Lake Store.</span><span class="sxs-lookup"><span data-stu-id="ead3a-269">There is no support for Power BI output and Azure Date Lake Store output.</span></span>
- <span data-ttu-id="ead3a-270">Il n’existe aucune prise en charge de l’éditeur pour l’ajout ou la modification de fonctions JavaScript définies par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="ead3a-270">There is no editor support for adding or changing JavaScript user-defined functions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ead3a-271">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ead3a-271">Next steps</span></span>
* [<span data-ttu-id="ead3a-272">Introduction tooAzure Analytique de flux de données</span><span class="sxs-lookup"><span data-stu-id="ead3a-272">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="ead3a-273">Bien démarrer avec Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="ead3a-273">Get started by using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="ead3a-274">Mise à l'échelle des travaux Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="ead3a-274">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="ead3a-275">Références sur le langage des requêtes d'Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="ead3a-275">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="ead3a-276">Références sur l’API REST de gestion d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="ead3a-276">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
