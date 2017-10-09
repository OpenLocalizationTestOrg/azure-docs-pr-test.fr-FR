---
title: "aaaUse hello vue de l’exécution de sommets dans Data Lake Tools pour Visual Studio | Documents Microsoft"
description: "Découvrez comment toouse hello travaux de vue de l’exécution de sommets tooexam Analytique lac de données."
services: data-lake-analytics
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 5366d852-e7d6-44cf-a88c-e9f52f15f7df
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 10/13/2016
ms.author: jgao
ms.openlocfilehash: fb54d2af8a32aa27a54ff50a73c1b4903677a21e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-vertex-execution-view-in-data-lake-tools-for-visual-studio"></a><span data-ttu-id="58b24-103">Utilisez hello vue de l’exécution de sommets dans Data Lake Tools pour Visual Studio</span><span class="sxs-lookup"><span data-stu-id="58b24-103">Use hello Vertex Execution View in Data Lake Tools for Visual Studio</span></span>
<span data-ttu-id="58b24-104">Découvrez comment toouse hello travaux de vue de l’exécution de sommets tooexam Analytique lac de données.</span><span class="sxs-lookup"><span data-stu-id="58b24-104">Learn how toouse hello Vertex Execution View tooexam Data Lake Analytics jobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="58b24-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="58b24-105">Prerequisites</span></span>

<span data-ttu-id="58b24-106">Vous avez besoin d’une connaissance élémentaire à l’aide des outils lac de données pour le script toodevelop U-SQL de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="58b24-106">You need basic knowledge of using Data Lake Tools for Visual Studio toodevelop U-SQL script.</span></span>  <span data-ttu-id="58b24-107">Consultez [Didacticiel : Développer des scripts U-SQL avec Data Lake Tools pour Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="58b24-107">See [Tutorial: develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>

## <a name="open-hello-vertex-execution-view"></a><span data-ttu-id="58b24-108">Ouvrez hello vue de l’exécution de sommets</span><span class="sxs-lookup"><span data-stu-id="58b24-108">Open hello Vertex Execution View</span></span>
<span data-ttu-id="58b24-109">Ouvrez une tâche U-SQL dans Data Lake Tools pour Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="58b24-109">Open a U-SQL job in Data Lake Tools for Visual Studio.</span></span> <span data-ttu-id="58b24-110">Cliquez sur **vue de l’exécution de sommets** dans hello bas à gauche.</span><span class="sxs-lookup"><span data-stu-id="58b24-110">Click **Vertex Execution View** in hello bottom left corner.</span></span> <span data-ttu-id="58b24-111">Vous pouvez être invité à tooload profils tout d’abord, et elle peut prendre un certain temps en fonction de la connectivité réseau.</span><span class="sxs-lookup"><span data-stu-id="58b24-111">You may be prompted tooload profiles first and it can take some time depending on your network connectivity.</span></span>

![Vue d’exécution du vertex Data Lake Analytics Tools](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-open-vertex-execution-view.png)

## <a name="understand-vertex-execution-view"></a><span data-ttu-id="58b24-113">Présentation de la vue d’exécution du vertex</span><span class="sxs-lookup"><span data-stu-id="58b24-113">Understand Vertex Execution View</span></span>
<span data-ttu-id="58b24-114">Hello, vue de l’exécution de sommets comprend trois parties :</span><span class="sxs-lookup"><span data-stu-id="58b24-114">hello Vertex Execution View has three parts:</span></span>

![Vue d’exécution du vertex Data Lake Analytics Tools](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view.png)

<span data-ttu-id="58b24-116">Hello **sélecteur de sommets** sur permet de gauche hello vous sélectionnez les sommets par les fonctionnalités (telles que les premières 10 données lire, ou choisissez par étape).</span><span class="sxs-lookup"><span data-stu-id="58b24-116">hello **Vertex selector** on hello left lets you select vertices by features (such as top 10 data read, or choose by stage).</span></span> <span data-ttu-id="58b24-117">Un des filtres de hello plus couramment utilisées est toosee hello **sommets sur le chemin critique**.</span><span class="sxs-lookup"><span data-stu-id="58b24-117">One of hello most commonly-used filters is toosee hello **vertices on critical path**.</span></span> <span data-ttu-id="58b24-118">Hello **chemin d’accès critique** est hello plus longue séquence de sommets d’un travail U-SQL.</span><span class="sxs-lookup"><span data-stu-id="58b24-118">hello **Critical path** is hello longest chain of vertices of a U-SQL job.</span></span> <span data-ttu-id="58b24-119">Chemin d’accès critique de présentation hello est utile pour optimiser vos travaux en vérifiant les sommets prend plus longtemps hello.</span><span class="sxs-lookup"><span data-stu-id="58b24-119">Understanding hello critical path is useful for optimizing your jobs by checking which vertex takes hello longest time.</span></span>
  
![Vue d’exécution du vertex Data Lake Analytics Tools](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view-pane2.png)

<span data-ttu-id="58b24-121">volet en haut au centre de Hello affiche hello **état de tous les sommets hello en cours d’exécution**.</span><span class="sxs-lookup"><span data-stu-id="58b24-121">hello top center pane shows hello **running status of all hello vertices**.</span></span>
  
![Vue d’exécution du vertex Data Lake Analytics Tools](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view-pane3.png)

<span data-ttu-id="58b24-123">volet central de bas Hello affiche des informations sur chaque sommet :</span><span class="sxs-lookup"><span data-stu-id="58b24-123">hello bottom center pane shows information about each vertex:</span></span>
* <span data-ttu-id="58b24-124">: Processus hello nom d’instance de sommets hello.</span><span class="sxs-lookup"><span data-stu-id="58b24-124">Process Name: hello name of hello vertex instance.</span></span> <span data-ttu-id="58b24-125">Il est composé de différentes parties de StageName|VertexName|VertexRunInstance.</span><span class="sxs-lookup"><span data-stu-id="58b24-125">It is composed of different parts in StageName|VertexName|VertexRunInstance.</span></span> <span data-ttu-id="58b24-126">Par exemple, sommet de .v1 [62] hello SV7_Split signifie hello deuxième instance d’exécution (.v1, index à partir de 0) du nombre de sommets 62 dans étape SV7_Split.</span><span class="sxs-lookup"><span data-stu-id="58b24-126">For example, hello SV7_Split[62].v1 vertex stands for hello second running instance (.v1, index starting from 0) of Vertex number 62 in Stage SV7_Split.</span></span>
* <span data-ttu-id="58b24-127">Lecture de données total/écrit : les données de salutation a été lus/écrits par ce vertex.</span><span class="sxs-lookup"><span data-stu-id="58b24-127">Total Data Read/Written: hello data was read/written by this vertex.</span></span>
* <span data-ttu-id="58b24-128">État de l’état/sortie : hello état final lorsque les sommets hello sont terminée.</span><span class="sxs-lookup"><span data-stu-id="58b24-128">State/Exit Status: hello final status when hello vertex is ended.</span></span>
* <span data-ttu-id="58b24-129">Type/Échec du Code de sortie : hello lors de sommet de hello a échoué.</span><span class="sxs-lookup"><span data-stu-id="58b24-129">Exit Code/Failure Type: hello error when hello vertex failed.</span></span>
* <span data-ttu-id="58b24-130">Raison de la création : Pourquoi les sommets hello a été créé.</span><span class="sxs-lookup"><span data-stu-id="58b24-130">Creation Reason: Why hello vertex was created.</span></span>
* <span data-ttu-id="58b24-131">Temps de latence de file d’attente de ressources latence/processus latence/PN : hello durée de toowait de sommets hello pour les ressources, les données tooprocess et toostay dans la file d’attente hello.</span><span class="sxs-lookup"><span data-stu-id="58b24-131">Resource Latency/Process Latency/PN Queue Latency: hello time taken for hello vertex toowait for resources, tooprocess data, and toostay in hello queue.</span></span>
* <span data-ttu-id="58b24-132">GUID du processus/créateur : GUID vertex en cours d’exécution actuel de hello ou son créateur.</span><span class="sxs-lookup"><span data-stu-id="58b24-132">Process/Creator GUID: GUID for hello current running vertex or its creator.</span></span>
* <span data-ttu-id="58b24-133">Version : instance de hello N-th Hello vertex en cours d’exécution (hello système peut-être planifier des instances d’un sommet pour nombreuses raisons, par exemple le basculement, de calcul redondance, etc..)</span><span class="sxs-lookup"><span data-stu-id="58b24-133">Version: hello N-th instance of hello running vertex (hello system might schedule new instances of a vertex for many reasons, for example failover, compute redundancy, etc.)</span></span>
* <span data-ttu-id="58b24-134">Heure de création de la version.</span><span class="sxs-lookup"><span data-stu-id="58b24-134">Version Created Time.</span></span>
* <span data-ttu-id="58b24-135">Créer début processus d’exécution en file d’attente/processus de l’heure début heure/processus terminé de traiter temps : lorsque le processus de sommets hello démarre la création ; début du processus de sommet de hello tooqueue ; Lorsque hello certains processus de sommets démarre ; Lorsque hello certains sommets est terminée.</span><span class="sxs-lookup"><span data-stu-id="58b24-135">Process Create Start Time/Process Queued Time/Process Start Time/Process Complete Time: when hello vertex process starts creation; when hello vertex process starts tooqueue; when hello certain vertex process starts; when hello certain vertex is completed.</span></span>

## <a name="next-steps"></a><span data-ttu-id="58b24-136">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="58b24-136">Next steps</span></span>
* <span data-ttu-id="58b24-137">toolog des informations de diagnostic, consultez [l’accès aux journaux de diagnostic pour l’Analytique de LAC de données Azure](data-lake-analytics-diagnostic-logs.md)</span><span class="sxs-lookup"><span data-stu-id="58b24-137">toolog diagnostics information, see [Accessing diagnostics logs for Azure Data Lake Analytics](data-lake-analytics-diagnostic-logs.md)</span></span>
* <span data-ttu-id="58b24-138">toosee une requête plus complexe, consultez [site Web d’analyse se connecte à l’aide d’Analytique de LAC de données Azure](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="58b24-138">toosee a more complex query, see [Analyze Website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="58b24-139">Détails de la tâche tooview, consultez [navigateur de travail d’utilisation et de la vue des travaux pour les travaux de l’Analytique de LAC de données Azure](data-lake-analytics-data-lake-tools-view-jobs.md)</span><span class="sxs-lookup"><span data-stu-id="58b24-139">tooview job details, see [Use Job Browser and Job View for Azure Data lake Analytics jobs](data-lake-analytics-data-lake-tools-view-jobs.md)</span></span>
