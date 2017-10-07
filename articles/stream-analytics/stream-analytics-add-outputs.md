---
title: "génère des données de tooconfigure aaaHow pour les tâches de flux de données Analytique | Documents Microsoft"
description: "Configurer les sorties pour les tâches Stream Analytics | segment du parcours d’apprentissage."
keywords: "sortie de données, déplacement des données"
documentationcenter: 
services: stream-analytics
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: 3bbea3da-bfce-4af1-a15e-d4b23874034f
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/26/2017
ms.author: samacha
ms.openlocfilehash: c5d89e9e9f9211d3e778580c071dd53d56aed9fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-data-outputs-for-stream-analytics-jobs"></a><span data-ttu-id="f1e2c-104">Comment les données tooconfigure génère des tâches de flux de données Analytique</span><span class="sxs-lookup"><span data-stu-id="f1e2c-104">How tooconfigure data outputs for Stream Analytics jobs</span></span>

<span data-ttu-id="f1e2c-105">Les travaux de flux de données Analytique Azure peuvent être tooone connecté ou des sorties de données supplémentaires, qui définissent un récepteur de données connexion tooan existant.</span><span class="sxs-lookup"><span data-stu-id="f1e2c-105">Azure Stream Analytics jobs can be connected tooone or more data outputs, which define a connection tooan existing data sink.</span></span> <span data-ttu-id="f1e2c-106">Lorsque votre tâche de flux de données Analytique traite et transforme les données entrantes, un flux de données d’événements de sortie est écrite la sortie de la tâche tooyour.</span><span class="sxs-lookup"><span data-stu-id="f1e2c-106">As your Stream Analytics job processes and transforms incoming data, a stream of data output events is written tooyour job's output.</span></span>

<span data-ttu-id="f1e2c-107">Sorties de flux de données Analytique peuvent être utilisé toosource de tableaux de bord en temps réel ou alertes, déclencheur les workflows de déplacement des données ou simplement les données d’archive pour la suite de traitement par lot.</span><span class="sxs-lookup"><span data-stu-id="f1e2c-107">Stream Analytics data outputs can be used toosource real-time dashboards or alerts, trigger data movement workflows, or simply archive data for batch processing later on.</span></span> <span data-ttu-id="f1e2c-108">Stream Analytics bénéficie d'une intégration de première classe avec plusieurs services Azure, qui sont expliqués en détail ici.</span><span class="sxs-lookup"><span data-stu-id="f1e2c-108">Stream Analytics has first class integration with several Azure services, which are documented in detail here.</span></span>

<span data-ttu-id="f1e2c-109">tooadd une tâche de flux de données Analytique tooyour sortie :</span><span class="sxs-lookup"><span data-stu-id="f1e2c-109">tooadd an output tooyour Stream Analytics job:</span></span>

1. <span data-ttu-id="f1e2c-110">Bonjour [portail Azure](https://portal.azure.com), ouvrez votre projet, cliquez sur **sorties** puis cliquez sur **ajouter** dans le panneau de sorties hello qui s’affiche.</span><span class="sxs-lookup"><span data-stu-id="f1e2c-110">In hello [Azure portal](https://portal.azure.com), open your job and click **Outputs** and then click **Add** in hello Outputs blade that appears.</span></span>
   
    ![Ajout de sorties](./media/stream-analytics-add-outputs/1-stream-analytics-add-outputs.png)  
   
2. <span data-ttu-id="f1e2c-112">Fournissez un nom convivial pour cette sortie Bonjour **Alias de sortie** boîte.</span><span class="sxs-lookup"><span data-stu-id="f1e2c-112">Provide a friendly name for this output in hello **Output Alias** box.</span></span> <span data-ttu-id="f1e2c-113">Ce nom peut être utilisé dans la requête de votre travail plus tard sur toorefer toohello sortie.</span><span class="sxs-lookup"><span data-stu-id="f1e2c-113">This name can be used in your job's query later on toorefer toohello output.</span></span>  
   
    <span data-ttu-id="f1e2c-114">Renseignez les autres hello hello requis connexion propriétés tooconnect tooyour sortie.</span><span class="sxs-lookup"><span data-stu-id="f1e2c-114">Fill in hello rest of hello required connection properties tooconnect tooyour output.</span></span>  <span data-ttu-id="f1e2c-115">Ces champs varient selon le type de sortie et sont définis en détail ici.</span><span class="sxs-lookup"><span data-stu-id="f1e2c-115">These fields vary by output type and are defined in detail here.</span></span>  
   
    ![Choisir le type de déplacement des données](./media/stream-analytics-add-outputs/2-stream-analytics-add-outputs.png)  
   
3. <span data-ttu-id="f1e2c-117">Selon le type de sortie hello, vous devrez peut-être toospecify comment les données de salutation sont sérialisées ou mis en forme.</span><span class="sxs-lookup"><span data-stu-id="f1e2c-117">Depending on hello output type, you may need toospecify how hello data is serialized or formatted.</span></span> <span data-ttu-id="f1e2c-118">paramètres de sérialisation spécifique Hello pour chaque type de sortie sont décrits ici.</span><span class="sxs-lookup"><span data-stu-id="f1e2c-118">hello specific serialization settings for each output type are documented here.</span></span>
   
    <span data-ttu-id="f1e2c-119">Renseignez les autres hello hello connexion requise propriétés tooconnect tooyour de source de données.</span><span class="sxs-lookup"><span data-stu-id="f1e2c-119">Fill in hello rest of hello required connection properties tooconnect tooyour data source.</span></span> <span data-ttu-id="f1e2c-120">Ces champs varient selon le type d’entrée et source de type et sont définies en détail dans hello [article de créer une tâche](stream-analytics-create-a-job.md).</span><span class="sxs-lookup"><span data-stu-id="f1e2c-120">These fields vary by type of input and source type and are defined in detail in hello [Create Job article](stream-analytics-create-a-job.md).</span></span>  

> [!Note]
>
> <span data-ttu-id="f1e2c-121">Une tâche d’ajouté toohello élément de sortie, doivent exister avant la tâche hello est démarrée et événements démarrer le flux.</span><span class="sxs-lookup"><span data-stu-id="f1e2c-121">Any output element added toohello job, must exist before hello job is started and events start flowing.</span></span> <span data-ttu-id="f1e2c-122">Par exemple, si vous utilisez le stockage d’objets Blob comme sortie, le travail de hello ne crée pas un compte de stockage automatiquement.</span><span class="sxs-lookup"><span data-stu-id="f1e2c-122">For example, if you use Blob storage as an output, hello job will not create a storage account automatically.</span></span> <span data-ttu-id="f1e2c-123">Il doit toobe créé par l’utilisateur de hello avant le démarrage du travail ASA hello.</span><span class="sxs-lookup"><span data-stu-id="f1e2c-123">It needs toobe created by hello user before hello ASA job is started.</span></span>
> 
 

## <a name="get-help"></a><span data-ttu-id="f1e2c-124">Obtenir de l’aide</span><span class="sxs-lookup"><span data-stu-id="f1e2c-124">Get help</span></span>
<span data-ttu-id="f1e2c-125">Pour obtenir une assistance, essayez notre [forum Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="f1e2c-125">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="f1e2c-126">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f1e2c-126">Next steps</span></span>
* [<span data-ttu-id="f1e2c-127">Introduction tooAzure Analytique de flux de données</span><span class="sxs-lookup"><span data-stu-id="f1e2c-127">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="f1e2c-128">Prise en main d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="f1e2c-128">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="f1e2c-129">Mise à l'échelle des travaux Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="f1e2c-129">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="f1e2c-130">Références sur le langage des requêtes d'Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="f1e2c-130">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="f1e2c-131">Références sur l’API REST de gestion d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="f1e2c-131">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

