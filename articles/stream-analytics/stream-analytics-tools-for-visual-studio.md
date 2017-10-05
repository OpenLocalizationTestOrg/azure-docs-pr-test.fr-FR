---
title: Utilisation d'outils Azure Stream Analytics pour Visual Studio | Microsoft Docs
description: "Didacticiel pour bien démarrer avec les outils Azure Stream Analytics pour Visual Studio"
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
ms.openlocfilehash: 618c1055795a75e0ed71dacddba3e076f81f4946
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-stream-analytics-tools-for-visual-studio"></a><span data-ttu-id="8e6c9-104">Utilisation d’outils Azure Stream Analytics pour Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8e6c9-104">Use Azure Stream Analytics Tools for Visual Studio</span></span>
## <a name="introduction"></a><span data-ttu-id="8e6c9-105">Introduction</span><span class="sxs-lookup"><span data-stu-id="8e6c9-105">Introduction</span></span>
<span data-ttu-id="8e6c9-106">Dans ce didacticiel, vous apprenez à utiliser les outils Azure Stream Analytics pour Visual Studio afin de créer, fournir du contenu, tester localement, gérer et déboguer vos tâches Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-106">In this tutorial, you learn how to use Azure Stream Analytics Tools for Visual Studio to create, author, test locally, manage, and debug your Stream Analytics jobs.</span></span> 

<span data-ttu-id="8e6c9-107">Après avoir effectué ce didacticiel, vous pourrez :</span><span class="sxs-lookup"><span data-stu-id="8e6c9-107">After completing this tutorial, you will be able to:</span></span>
* <span data-ttu-id="8e6c9-108">bien connaître les outils Stream Analytics pour Visual Studio ;</span><span class="sxs-lookup"><span data-stu-id="8e6c9-108">Familiarize yourself with Stream Analytics Tools for Visual Studio.</span></span>
* <span data-ttu-id="8e6c9-109">configurer et déployer un travail Stream Analytics ;</span><span class="sxs-lookup"><span data-stu-id="8e6c9-109">Configure and deploy a Stream Analytics job.</span></span>
* <span data-ttu-id="8e6c9-110">tester votre travail en local avec des exemples de données locaux ;</span><span class="sxs-lookup"><span data-stu-id="8e6c9-110">Test your job locally with local sample data.</span></span>
* <span data-ttu-id="8e6c9-111">utiliser la surveillance pour résoudre les problèmes ;</span><span class="sxs-lookup"><span data-stu-id="8e6c9-111">Use monitoring to troubleshoot issues.</span></span>
* <span data-ttu-id="8e6c9-112">exporter des travaux existants dans des projets.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-112">Export existing jobs to projects.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8e6c9-113">Composants requis</span><span class="sxs-lookup"><span data-stu-id="8e6c9-113">Prerequisites</span></span>
<span data-ttu-id="8e6c9-114">Pour effectuer ce didacticiel, vous avez besoin de ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="8e6c9-114">To complete this tutorial, you need the following prerequisites:</span></span>
* <span data-ttu-id="8e6c9-115">Accomplissez les étapes qui précèdent « Créer une tâche Stream Analytics » du [didacticiel Créer une solution IoT à l’aide de Stream Analytics](https://docs.microsoft.com/azure/stream-analytics/stream-analytics-build-an-iot-solution-using-stream-analytics).</span><span class="sxs-lookup"><span data-stu-id="8e6c9-115">Finish the steps that precede "Create a Stream Analytics job" in the [Build an IoT solution by using Stream Analytics tutorial](https://docs.microsoft.com/azure/stream-analytics/stream-analytics-build-an-iot-solution-using-stream-analytics).</span></span> 
* <span data-ttu-id="8e6c9-116">Utilisez Visual Studio 2015, Visual Studio 2013 mise à jour 4 ou Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-116">Use Visual Studio 2015, Visual Studio 2013 update 4, or Visual Studio 2012.</span></span> <span data-ttu-id="8e6c9-117">Les éditions Enterprise (Ultimate/Premium), Professional et Community sont prises en charge.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-117">Enterprise (Ultimate/Premium), Professional, and Community editions are supported.</span></span> <span data-ttu-id="8e6c9-118">L’édition Express n’est pas prise en charge.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-118">Express edition is not supported.</span></span> <span data-ttu-id="8e6c9-119">Visual Studio 2017 n’est pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-119">Visual Studio 2017 is not supported.</span></span> 
* <span data-ttu-id="8e6c9-120">Utilisez le Kit SDK Azure pour .NET version 2.7.1 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-120">Use the Azure SDK for .NET version 2.7.1 or later.</span></span> <span data-ttu-id="8e6c9-121">Installez-le à l’aide de [Web Platform Installer](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="8e6c9-121">Install it by using the [Web platform installer](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
* <span data-ttu-id="8e6c9-122">Installez les [outils Stream Analytics pour Visual Studio](http://aka.ms/asatoolsvs).</span><span class="sxs-lookup"><span data-stu-id="8e6c9-122">Install the [Stream Analytics Tools for Visual Studio](http://aka.ms/asatoolsvs).</span></span>

## <a name="create-a-stream-analytics-project"></a><span data-ttu-id="8e6c9-123">Créer un projet Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="8e6c9-123">Create a Stream Analytics project</span></span>
1. <span data-ttu-id="8e6c9-124">Dans Visual Studio, cliquez sur le menu **Fichier** et sélectionnez **Nouveau projet**.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-124">In Visual Studio, click the **File** menu and select **New Project**.</span></span> 

2. <span data-ttu-id="8e6c9-125">Dans la liste des modèles sur la gauche, sélectionnez **Stream Analytics**, puis cliquez sur **Application Azure Stream Analytics**.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-125">In the templates list on the left, select **Stream Analytics** and then click **Azure Stream Analytics Application**.</span></span>

3. <span data-ttu-id="8e6c9-126">Entrez le **Nom**, l’**Emplacement** et le **Nom de la solution** du projet, comme vous le feriez pour d’autres projets.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-126">Enter the project **Name**, **Location**, and **Solution name** as you do for other projects.</span></span>

    ![Fenêtre Nouveau projet](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-create-project-01.png)

    <span data-ttu-id="8e6c9-128">Un projet **Toll** est généré dans l’**Explorateur de solutions**.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-128">A **Toll** project is generated in **Solution Explorer**.</span></span>

    ![Projet Toll généré dans l’Explorateur de solutions](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-create-project-02.png)

## <a name="choose-the-correct-subscription"></a><span data-ttu-id="8e6c9-130">Choisir le bon abonnement</span><span class="sxs-lookup"><span data-stu-id="8e6c9-130">Choose the correct subscription</span></span>
1. <span data-ttu-id="8e6c9-131">Dans Visual Studio, cliquez sur le menu **Affichage** et ouvrez **Explorateur de serveurs**.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-131">In Visual Studio, click the **View** menu and open **Server Explorer**.</span></span>

2. <span data-ttu-id="8e6c9-132">Connectez-vous à votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-132">Sign in with your Azure Account.</span></span> 

## <a name="define-the-input-sources"></a><span data-ttu-id="8e6c9-133">Définir les sources d’entrée</span><span class="sxs-lookup"><span data-stu-id="8e6c9-133">Define the input sources</span></span>
1.  <span data-ttu-id="8e6c9-134">Dans l’**Explorateur de solutions**, développez le nœud **Entrées** et renommez **Input.json** en **EntryStream.json**.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-134">In **Solution Explorer**, expand the **Inputs** node and rename **Input.json** to **EntryStream.json**.</span></span> <span data-ttu-id="8e6c9-135">Double-cliquez sur **EntryStream.json**.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-135">Double-click **EntryStream.json**.</span></span>
2.  <span data-ttu-id="8e6c9-136">L’**Alias d’entrée** est désormais **EntryStream**.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-136">The **Input Alias** is now **EntryStream**.</span></span> <span data-ttu-id="8e6c9-137">L’alias d’entrée est utilisé dans le script de requête.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-137">The input alias is used in the query script.</span></span> 
3.  <span data-ttu-id="8e6c9-138">Dans **Type de source**, sélectionnez **Data Stream**.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-138">In **Source Type**, select **Data Stream**.</span></span>
4.  <span data-ttu-id="8e6c9-139">Dans **Source**, sélectionnez **Event Hub**.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-139">In **Source**, select **Event Hub**.</span></span>
5.  <span data-ttu-id="8e6c9-140">Dans **Espace de noms Service Bus**, sélectionnez l’option **TollData**.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-140">In **Service Bus Namespace**, select the **TollData** option.</span></span>
6.  <span data-ttu-id="8e6c9-141">Dans **Nom du hub d’événements**, sélectionnez **entry**.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-141">In **Event Hub Name**, select **entry**.</span></span>
7.  <span data-ttu-id="8e6c9-142">Dans **Nom de la stratégie du hub d’événements**, sélectionnez **RootManageSharedAccessKey** (la valeur par défaut).</span><span class="sxs-lookup"><span data-stu-id="8e6c9-142">In **Event Hub Policy Name**, select **RootManageSharedAccessKey** (the default value).</span></span>
8.  <span data-ttu-id="8e6c9-143">Dans **Format de sérialisation de l’événement**, sélectionnez **Json**.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-143">In **Event Serialization Format**, select **Json**.</span></span> 
9.  <span data-ttu-id="8e6c9-144">Dans **Encodage**, sélectionnez **UTF8**.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-144">In **Encoding**, select **UTF8**.</span></span> <span data-ttu-id="8e6c9-145">Vos paramètres doivent ressembler à ceux de la capture d’écran suivante :</span><span class="sxs-lookup"><span data-stu-id="8e6c9-145">Your settings should look like the following screenshot:</span></span>

    ![Fenêtre Entrée](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-01.png)
 
10. <span data-ttu-id="8e6c9-147">Pour terminer l’exécution de l’Assistant, cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-147">To finish the wizard, click **Save**.</span></span> <span data-ttu-id="8e6c9-148">Vous pouvez maintenant ajouter une autre source d’entrée pour créer le flux de sortie.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-148">Now you can add another input source to create the exit stream.</span></span> <span data-ttu-id="8e6c9-149">Cliquez avec le bouton droit sur le nœud **Entrées** et sélectionnez **Nouvel élément**.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-149">Right-click the **Inputs** node, and select **New Item**.</span></span>

    ![Nouvel élément](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-02.png)
 
11. <span data-ttu-id="8e6c9-151">Dans la fenêtre, sélectionnez **Entrée Azure Stream Analytics** et modifiez le **Nom** en **ExitStream.json**.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-151">In the window, select **Azure Stream Analytics Input**, and change the **Name** to **ExitStream.json**.</span></span> <span data-ttu-id="8e6c9-152">Cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-152">Click **Add**.</span></span>

    ![Fenêtre Ajouter un nouvel élément](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-03.png)
 
12. <span data-ttu-id="8e6c9-154">Double-cliquez sur **ExitStream.json** dans le projet et suivez la même procédure que celle que vous avez utilisée pour le flux d’entrée de données.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-154">Double-click **ExitStream.json** in the project, and follow the same steps as you did for the entry stream.</span></span> <span data-ttu-id="8e6c9-155">Veillez à entrer **exit** pour le **Nom du hub d’événements**, comme indiqué sur la capture d’écran suivante :</span><span class="sxs-lookup"><span data-stu-id="8e6c9-155">Be sure to enter **exit** for the **Event Hub Name** as shown in the following screenshot:</span></span>

    ![Fenêtre ExitStream](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-04.png)

    <span data-ttu-id="8e6c9-157">Vous avez maintenant défini deux flux d’entrée de données :</span><span class="sxs-lookup"><span data-stu-id="8e6c9-157">Now you have defined two input streams:</span></span>

    ![Flux d’entrée et de sortie](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-05.png)
 
    <span data-ttu-id="8e6c9-159">À présent, ajoutons une entrée de données de référence pour le fichier blob contenant les données d’inscription des véhicules.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-159">Next, add reference data input for the blob file that contains car registration data.</span></span>

13. <span data-ttu-id="8e6c9-160">Cliquez avec le bouton droit sur le nœud **Entrées** dans le projet, puis suivez la même procédure que celle que vous avez utilisée pour les entrées de flux de données.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-160">Right-click the **Inputs** node in the project, and then follow the same steps as you did for the stream inputs.</span></span> <span data-ttu-id="8e6c9-161">Dans **Alias d’entrée**, entrez **Registration**, et dans **Type de Source**, sélectionnez **Reference data**.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-161">In **Input Alias**, enter **Registration**, and in **Source Type**, select **Reference data**.</span></span>

    ![Fenêtre Inscription](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-06.png)

14. <span data-ttu-id="8e6c9-163">Dans **Compte de stockage**, sélectionnez l’option **tolldata**.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-163">In **Storage Account**, select the **tolldata** option.</span></span> <span data-ttu-id="8e6c9-164">Dans **Conteneur**, sélectionnez **tolldata**, et dans **Modèle de chemin d’accès**, entrez **registration.json**.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-164">In **Container**, select **tolldata**, and in **Path Pattern**, enter **registration.json**.</span></span> <span data-ttu-id="8e6c9-165">Ce nom de fichier respecte la casse et doit être en minuscules.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-165">This file name is case sensitive and should be lowercase.</span></span>
15. <span data-ttu-id="8e6c9-166">Pour terminer l’exécution de l’Assistant, cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-166">To finish the wizard, click **Save**.</span></span>

<span data-ttu-id="8e6c9-167">À présent, toutes les entrées sont définies.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-167">Now all the inputs are defined.</span></span>

## <a name="define-the-output"></a><span data-ttu-id="8e6c9-168">Définir la sortie</span><span class="sxs-lookup"><span data-stu-id="8e6c9-168">Define the output</span></span>
1.  <span data-ttu-id="8e6c9-169">Dans l’**Explorateur de solutions**, développez le nœud **Entrées** et double-cliquez sur **Output.json**.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-169">In **Solution Explorer**, expand the **Inputs** node and double-click **Output.json**.</span></span>

2.  <span data-ttu-id="8e6c9-170">Dans **Alias de sortie**, entrez **output**.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-170">In **Output Alias**, enter **output**.</span></span> 
3.  <span data-ttu-id="8e6c9-171">Dans **Récepteur**, sélectionnez **SQL Database**.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-171">In **Sink**, select **SQL Database**.</span></span>
4.  <span data-ttu-id="8e6c9-172">Dans **Base de données**, sélectionnez **TollDataDB**.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-172">In **Database**, select **TollDataDB**.</span></span>
5.  <span data-ttu-id="8e6c9-173">Dans **Nom d’utilisateur**, entrez **tolladmin**.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-173">In **User Name**, enter **tolladmin**.</span></span> 
6.  <span data-ttu-id="8e6c9-174">Dans **Mot de passe**, entrez **123toll!**.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-174">In **Password**, enter **123toll!**.</span></span>
7.  <span data-ttu-id="8e6c9-175">Dans **Table**, entrez **TollDataRefJoin**.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-175">In **Table**, enter **TollDataRefJoin**.</span></span>
8.  <span data-ttu-id="8e6c9-176">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-176">Click **Save**.</span></span>

    ![Fenêtre Sortie](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-output-01.png)
 
## <a name="create-a-stream-analytics-query"></a><span data-ttu-id="8e6c9-178">Créer une requête Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="8e6c9-178">Create a Stream Analytics query</span></span>
<span data-ttu-id="8e6c9-179">Ce didacticiel tente de répondre à différentes questions liées aux données de péage.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-179">This tutorial attempts to answer several business questions that are related to toll data.</span></span> <span data-ttu-id="8e6c9-180">Il élabore également des requêtes Stream Analytics utilisables dans Stream Analytics pour fournir des réponses pertinentes.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-180">It also constructs Stream Analytics queries that can be used in Stream Analytics to provide relevant answers.</span></span>
<span data-ttu-id="8e6c9-181">Avant de commencer votre première tâche Stream Analytics, examinons un scénario simple et la syntaxe de requête.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-181">Before you start your first Stream Analytics job, let’s explore a simple scenario and the query syntax.</span></span>

### <a name="introduction-to-the-stream-analytics-query-language"></a><span data-ttu-id="8e6c9-182">Présentation du langage de requête de Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="8e6c9-182">Introduction to the Stream Analytics query language</span></span>
<span data-ttu-id="8e6c9-183">Supposons que nous devons compter le nombre de véhicules qui entrent dans un poste de péage.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-183">Let’s say that you need to count the number of vehicles that enter a toll booth.</span></span> <span data-ttu-id="8e6c9-184">Comme cet exemple est un flux continu d’événements, vous devez définir une période.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-184">Because this example is a continuous stream of events, you have to define a period of time.</span></span> <span data-ttu-id="8e6c9-185">Modifiez la question en « Combien de véhicules entrent en poste de péage toutes les trois minutes ? ».</span><span class="sxs-lookup"><span data-stu-id="8e6c9-185">Modify the question to be “How many vehicles enter a toll booth every three minutes?”</span></span> <span data-ttu-id="8e6c9-186">Cette façon de comptabiliser les données s’appelle communément le « nombre bascule ».</span><span class="sxs-lookup"><span data-stu-id="8e6c9-186">This way to count data is commonly referred to as the tumbling count.</span></span>

<span data-ttu-id="8e6c9-187">Examinez la requête Stream Analytics répondant à cette question :</span><span class="sxs-lookup"><span data-stu-id="8e6c9-187">Look at the Stream Analytics query that answers this question:</span></span>

        SELECT TollId, System.Timestamp AS WindowEnd, COUNT(*) AS Count 
        FROM EntryStream TIMESTAMP BY EntryTime 
        GROUP BY TUMBLINGWINDOW(minute, 3), TollId 

<span data-ttu-id="8e6c9-188">Stream Analytics utilise un langage de requête similaire à SQL et ajoute quelques extensions pour spécifier les aspects de la requête liés au temps.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-188">Stream Analytics uses a query language that's like SQL and adds a few extensions to specify time-related aspects of the query.</span></span>

<span data-ttu-id="8e6c9-189">Pour plus d’informations, consultez les constructions [Gestion du temps](https://msdn.microsoft.com/library/azure/mt582045.aspx) et [Fenêtrage](https://msdn.microsoft.com/library/azure/dn835019.aspx) utilisées dans la requête à partir de MSDN.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-189">For more information, see [Time Management](https://msdn.microsoft.com/library/azure/mt582045.aspx) and [Windowing](https://msdn.microsoft.com/library/azure/dn835019.aspx) constructs used in the query from MSDN.</span></span>

<span data-ttu-id="8e6c9-190">Maintenant que vous avez écrit votre première requête Stream Analytics, il est temps de la tester.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-190">Now that you have written your first Stream Analytics query, it's time to test it.</span></span> <span data-ttu-id="8e6c9-191">Utilisez les exemples de fichiers de données situés dans votre dossier TollApp via le chemin suivant :</span><span class="sxs-lookup"><span data-stu-id="8e6c9-191">Use the sample data files located in your TollApp folder in the following path:</span></span>

<span data-ttu-id="8e6c9-192">..\TollApp\TollApp\Data</span><span class="sxs-lookup"><span data-stu-id="8e6c9-192">..\TollApp\TollApp\Data</span></span>

<span data-ttu-id="8e6c9-193">Ce dossier contient les fichiers suivants :</span><span class="sxs-lookup"><span data-stu-id="8e6c9-193">This folder contains the following files:</span></span>
*   <span data-ttu-id="8e6c9-194">Entry.json</span><span class="sxs-lookup"><span data-stu-id="8e6c9-194">Entry.json</span></span>
*   <span data-ttu-id="8e6c9-195">Exit.json</span><span class="sxs-lookup"><span data-stu-id="8e6c9-195">Exit.json</span></span>
*   <span data-ttu-id="8e6c9-196">registration.json</span><span class="sxs-lookup"><span data-stu-id="8e6c9-196">Registration.json</span></span>

## <a name="count-the-number-of-vehicles-entering-a-toll-booth"></a><span data-ttu-id="8e6c9-197">Compter le nombre de véhicules arrivant à un poste de péage</span><span class="sxs-lookup"><span data-stu-id="8e6c9-197">Count the number of vehicles entering a toll booth</span></span>
<span data-ttu-id="8e6c9-198">Dans le projet, double-cliquez sur **Script.asaql** pour ouvrir le script dans le l’**Éditeur de requête**.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-198">In the project, double-click **Script.asaql** to open the script in the **Query Editor**.</span></span> <span data-ttu-id="8e6c9-199">Copiez et collez le script de la section précédente dans l’éditeur.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-199">Copy and paste the script in the previous section into the editor.</span></span> <span data-ttu-id="8e6c9-200">L’Éditeur de requête prend en charge IntelliSense, la coloration syntaxique et le marquage d’erreurs.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-200">The Query Editor supports IntelliSense, syntax coloring, and the error marker.</span></span>

![Éditeur de requête](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-query-01.png)
 
### <a name="test-stream-analytics-queries-locally"></a><span data-ttu-id="8e6c9-202">Tester localement les requêtes Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="8e6c9-202">Test Stream Analytics queries locally</span></span>

1. <span data-ttu-id="8e6c9-203">Pour compiler la requête et voir si elle comporte une erreur de syntaxe, cliquez avec le bouton droit sur le projet et sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-203">To compile the query to see if there is a syntax error, right-click the project and select **Build**.</span></span> 

2. <span data-ttu-id="8e6c9-204">Pour valider cette requête sur des exemples de données, vous pouvez utiliser des exemples de données locaux.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-204">To validate this query against sample data, you can use local sample data.</span></span> <span data-ttu-id="8e6c9-205">Cliquez avec le bouton droit sur l’entrée et sélectionnez **Ajouter une entrée locale**.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-205">Right-click the input, and select **Add local input**.</span></span>

    ![Ajouter une entrée locale](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-01.png)
 
3. <span data-ttu-id="8e6c9-207">Dans la fenêtre indépendante, sélectionnez l’exemple de données à partir de votre chemin local.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-207">In the pop-up window, select the sample data from your local path.</span></span> <span data-ttu-id="8e6c9-208">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-208">Click **Save**.</span></span>

    ![Fenêtre Ajouter une entrée locale](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-02.png)
 
    <span data-ttu-id="8e6c9-210">Un fichier nommé **local_EntryStream.json** est automatiquement ajouté à votre dossier d’entrées.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-210">A file named **local_EntryStream.json** is automatically added to your inputs folder.</span></span>

    ![Fichier ajouté au dossier des entrées](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-03.png)
 
4. <span data-ttu-id="8e6c9-212">Dans l’**Éditeur de requête**, cliquez sur **Exécution locale**.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-212">In the **Query Editor**, click **Run Locally**.</span></span> <span data-ttu-id="8e6c9-213">Ou vous pouvez appuyer sur la touche F5.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-213">Or you can press the F5 key.</span></span>

    ![Exécution locale](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-local-run-01.png)

    ![Sortie de l’exécution locale](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-local-run-02.png)

    <span data-ttu-id="8e6c9-216">Appuyez sur une touche quelconque pour afficher la sortie dans la fenêtre **Résultat de l’exécution locale ASA** de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-216">Press any key to view the output in the **ASA Local Run Result** window in Visual Studio.</span></span> 

    ![Fenêtre Résultats de l’exécution locale ASA](./media/stream-analytics-tools-for-vs/local-testing-output.png)

5. <span data-ttu-id="8e6c9-218">Cliquez sur **Ouvrir le dossier des résultats** pour vérifier les fichiers de sortie aux formats CSV et JSON.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-218">Click **Open Result Folder** to check the output files both in CSV and JSON format.</span></span>

    ![Sortie Ouvrir le dossier des résultats](./media/stream-analytics-tools-for-vs/local-testing-files.png)
 

### <a name="sample-the-input-data"></a><span data-ttu-id="8e6c9-220">Échantillonner les données d’entrée</span><span class="sxs-lookup"><span data-stu-id="8e6c9-220">Sample the input data</span></span>
<span data-ttu-id="8e6c9-221">Vous pouvez également constituer des exemples de données à partir de sources d’entrée dans un fichier local.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-221">You can also sample input data from input sources to a local file.</span></span> 
1. <span data-ttu-id="8e6c9-222">Cliquez avec le bouton droit sur le fichier de configuration d’entrées et sélectionnez **Exemple de données**.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-222">Right-click the input config file, and select **Sample Data**.</span></span> 

   ![Exemple de données](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-01.png)

    <span data-ttu-id="8e6c9-224">Pour l’instant, vous pouvez uniquement échantillonner le hub d’événements ou le hub IoT.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-224">You can sample only event hub or IoT hub for now.</span></span> <span data-ttu-id="8e6c9-225">Les autres sources d’entrée ne sont pas prises en charge.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-225">Other input sources are not supported.</span></span>

2. <span data-ttu-id="8e6c9-226">Dans la fenêtre indépendante, entrez le chemin local utilisé pour enregistrer les exemples de données.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-226">In the pop-up window, enter the local path used to save the sample data.</span></span> <span data-ttu-id="8e6c9-227">Cliquez sur **Exemple**.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-227">Click **Sample**.</span></span>

    ![Fenêtre Exemples de données](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-02.png)
 
    <span data-ttu-id="8e6c9-229">Vous pouvez voir la progression de l’opération dans la fenêtre **Sortie**.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-229">You can see the progress in the **Output** window.</span></span> 

    ![Fenêtre Sortie](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-03.png)
 
### <a name="submit-a-stream-analytics-query-to-azure"></a><span data-ttu-id="8e6c9-231">Envoyer une requête Stream Analytics sur Azure</span><span class="sxs-lookup"><span data-stu-id="8e6c9-231">Submit a Stream Analytics query to Azure</span></span>
1. <span data-ttu-id="8e6c9-232">Dans l’**Éditeur de requête**, cliquez sur **Envoyer sur Azure** dans l’éditeur de script.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-232">In the **Query Editor**, click **Submit To Azure** in the script editor.</span></span>

    ![Envoyer sur Azure](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-submit-job-01.png)
 
2. <span data-ttu-id="8e6c9-234">Sélectionnez **Créer une tâche Azure Stream Analytics**.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-234">Select **Create a New Azure Stream Analytics Job**.</span></span> <span data-ttu-id="8e6c9-235">Entrez le **Nom de la tâche** et sélectionnez l’**Abonnement** approprié.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-235">Enter the **Job Name**, and select the correct **Subscription**.</span></span> <span data-ttu-id="8e6c9-236">Cliquez sur **Envoyer**.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-236">Click **Submit**.</span></span>

    ![Fenêtre Envoyer la tâche](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-submit-job-02.png)

 
### <a name="start-a-job"></a><span data-ttu-id="8e6c9-238">Démarrer une tâche</span><span class="sxs-lookup"><span data-stu-id="8e6c9-238">Start a job</span></span>
<span data-ttu-id="8e6c9-239">Dès lors que votre tâche est créée, sa vue s’ouvre automatiquement.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-239">Now that your job is created, the job view is automatically opened.</span></span> 
1. <span data-ttu-id="8e6c9-240">Pour commencer cette tâche, cliquez sur le bouton à la **flèche verte**.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-240">To start the job, click the **green arrow** button.</span></span>

    ![Démarrer une tâche](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-01.png)
 
2. <span data-ttu-id="8e6c9-242">Sélectionnez le paramètre par défaut et cliquez sur **Démarrer**.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-242">Select the default setting, and click **Start**.</span></span>
 
    ![Fenêtre Démarrer une tâche](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-02.png)

    <span data-ttu-id="8e6c9-244">L’**État** de la tâche passe à **En cours d’exécution**, et les **Événements d’entrée** ainsi que les **Événements de sortie** s’affichent.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-244">The job **Status** changes to **Running**, and **Input Events** and **Output Events** appear.</span></span>

    ![État en cours d’exécution dans Résumé de la tâche](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-03.png)

## <a name="check-the-results-in-visual-studio"></a><span data-ttu-id="8e6c9-246">Vérifier les résultats dans Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8e6c9-246">Check the results in Visual Studio</span></span>
1. <span data-ttu-id="8e6c9-247">Dans Visual Studio, ouvrez l’**Explorateur de serveurs** et cliquez avec le bouton droit sur la table **TollDataRefJoin**.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-247">In Visual Studio, open **Server Explorer** and right-click the **TollDataRefJoin** table.</span></span>
2. <span data-ttu-id="8e6c9-248">Sélectionnez **Afficher les données de la table** pour voir le résultat de votre tâche.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-248">Select **Show Table Data** to see the output of your job.</span></span>
   
    ![Sélection de l’option Afficher les données de la table dans l’Explorateur de serveurs](media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-check-results.jpg)


### <a name="view-the-job-metrics"></a><span data-ttu-id="8e6c9-250">Afficher les métriques de tâche</span><span class="sxs-lookup"><span data-stu-id="8e6c9-250">View the job metrics</span></span>
<span data-ttu-id="8e6c9-251">Certaines statistiques des tâches de base se trouvent dans **Métriques de tâche**.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-251">Some basic job statistics can be found in **Job Metrics**.</span></span> 

![Fenêtre Métriques de tâche](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-job-metrics-01.png)

 
## <a name="list-the-job-in-server-explorer"></a><span data-ttu-id="8e6c9-253">Répertorier la tâche dans l’Explorateur de serveurs</span><span class="sxs-lookup"><span data-stu-id="8e6c9-253">List the job in Server Explorer</span></span>
<span data-ttu-id="8e6c9-254">Dans l’**Explorateur de serveurs**, cliquez sur **Tâches Stream Analytics**, puis sur **Actualiser**.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-254">In **Server Explorer**, click **Stream Analytics Jobs** and then click **Refresh**.</span></span> <span data-ttu-id="8e6c9-255">La tâche s’affiche sous **Tâches Stream Analytics**.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-255">The job appears under **Stream Analytics jobs**.</span></span>

![Tâches Stream Analytics répertoriées dans l’Explorateur de serveurs](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-list-jobs-01.png)


## <a name="open-the-job-view"></a><span data-ttu-id="8e6c9-257">Ouvrir la vue de la tâche</span><span class="sxs-lookup"><span data-stu-id="8e6c9-257">Open the job view</span></span>
<span data-ttu-id="8e6c9-258">Pour ouvrir la vue de la tâche, développez le nœud de votre tâche et double-cliquez sur le nœud **Vue de la tâche**.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-258">To open the job view, expand your job node and double-click the **Job View** node.</span></span>

![Nœud Vue de la tâche](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-job-view-01.png)


## <a name="export-an-existing-job-to-a-project"></a><span data-ttu-id="8e6c9-260">Exporter un travail existant dans un projet</span><span class="sxs-lookup"><span data-stu-id="8e6c9-260">Export an existing job to a project</span></span>
<span data-ttu-id="8e6c9-261">Il existe deux méthodes pour exporter un travail existant vers un projet.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-261">There are two ways you can export an existing job to a project.</span></span>

<span data-ttu-id="8e6c9-262">Dans l’**Explorateur de serveurs**, cliquez avec le bouton droit sur le nœud de la tâche voulue, situé dans le nœud **Tâches Stream Analytics**, et sélectionnez **Exporter vers un nouveau projet Stream Analytics**.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-262">In **Server Explorer**, right-click the job node in the **Stream Analytics Jobs** node and select **Export to New Stream Analytics Project**.</span></span>

![Exporter vers un nouveau projet Stream Analytics](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-01.png)

<span data-ttu-id="8e6c9-264">Le projet est généré dans l’**Explorateur de solutions**.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-264">The project is generated in **Solution Explorer**.</span></span>

![Projet généré dans l’Explorateur de solutions](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-02.png)
 
<span data-ttu-id="8e6c9-266">Vous pouvez aussi utiliser la vue de la tâche et cliquer sur **Générer le projet**.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-266">You also can use the job view, and click **Generate Project**.</span></span>

![Générer le projet](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-03.png)

## <a name="known-issues-and-limitations"></a><span data-ttu-id="8e6c9-268">Problèmes connus et limitations</span><span class="sxs-lookup"><span data-stu-id="8e6c9-268">Known issues and limitations</span></span>
 
- <span data-ttu-id="8e6c9-269">Il n’existe aucune prise en charge pour la sortie Power BI et la sortie d’Azure Date Lake Store.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-269">There is no support for Power BI output and Azure Date Lake Store output.</span></span>
- <span data-ttu-id="8e6c9-270">Il n’existe aucune prise en charge de l’éditeur pour l’ajout ou la modification de fonctions JavaScript définies par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="8e6c9-270">There is no editor support for adding or changing JavaScript user-defined functions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8e6c9-271">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8e6c9-271">Next steps</span></span>
* [<span data-ttu-id="8e6c9-272">Présentation d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="8e6c9-272">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="8e6c9-273">Bien démarrer avec Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="8e6c9-273">Get started by using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="8e6c9-274">Mise à l'échelle des travaux Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="8e6c9-274">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="8e6c9-275">Références sur le langage des requêtes d'Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="8e6c9-275">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="8e6c9-276">Références sur l’API REST de gestion d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="8e6c9-276">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
