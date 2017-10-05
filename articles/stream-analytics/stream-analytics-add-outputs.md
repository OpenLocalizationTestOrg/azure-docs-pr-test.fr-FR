---
title: "Guide pratique pour configurer les sorties de données pour les travaux Stream Analytics | Microsoft Docs"
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
ms.openlocfilehash: 1ffa517469da1a8d79917b9747abc97ca3bef463
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-configure-data-outputs-for-stream-analytics-jobs"></a><span data-ttu-id="29154-104">Comment configurer les sorties de données pour les tâches Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="29154-104">How to configure data outputs for Stream Analytics jobs</span></span>

<span data-ttu-id="29154-105">Les tâches Azure Stream Analytics peuvent être connectées à une ou plusieurs sorties de données qui définissent une connexion à un récepteur de données existant.</span><span class="sxs-lookup"><span data-stu-id="29154-105">Azure Stream Analytics jobs can be connected to one or more data outputs, which define a connection to an existing data sink.</span></span> <span data-ttu-id="29154-106">Quand votre travail Stream Analytics traite et transforme les données entrantes, un flux d’événements de sortie de données est écrit dans la sortie de votre travail.</span><span class="sxs-lookup"><span data-stu-id="29154-106">As your Stream Analytics job processes and transforms incoming data, a stream of data output events is written to your job's output.</span></span>

<span data-ttu-id="29154-107">Les sorties de données Stream Analytics peuvent servir de source aux tableaux de bord ou aux alertes en temps réel, déclencher des workflows de déplacement ou simplement archiver les données pour le traitement par lot ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="29154-107">Stream Analytics data outputs can be used to source real-time dashboards or alerts, trigger data movement workflows, or simply archive data for batch processing later on.</span></span> <span data-ttu-id="29154-108">Stream Analytics bénéficie d'une intégration de première classe avec plusieurs services Azure, qui sont expliqués en détail ici.</span><span class="sxs-lookup"><span data-stu-id="29154-108">Stream Analytics has first class integration with several Azure services, which are documented in detail here.</span></span>

<span data-ttu-id="29154-109">Pour ajouter une sortie à votre tâche Stream Analytics :</span><span class="sxs-lookup"><span data-stu-id="29154-109">To add an output to your Stream Analytics job:</span></span>

1. <span data-ttu-id="29154-110">Dans le [portail Azure](https://portal.azure.com), ouvrez votre tâche et cliquez successivement sur **Sorties**, puis sur **Ajouter** dans le panneau Sorties qui s’affiche.</span><span class="sxs-lookup"><span data-stu-id="29154-110">In the [Azure portal](https://portal.azure.com), open your job and click **Outputs** and then click **Add** in the Outputs blade that appears.</span></span>
   
    ![Ajout de sorties](./media/stream-analytics-add-outputs/1-stream-analytics-add-outputs.png)  
   
2. <span data-ttu-id="29154-112">Attribuez un nom convivial à cette sortie dans la zone **Alias de sortie** .</span><span class="sxs-lookup"><span data-stu-id="29154-112">Provide a friendly name for this output in the **Output Alias** box.</span></span> <span data-ttu-id="29154-113">Ce nom pourra être utilisé dans la requête de votre tâche plus tard pour faire référence à la sortie.</span><span class="sxs-lookup"><span data-stu-id="29154-113">This name can be used in your job's query later on to refer to the output.</span></span>  
   
    <span data-ttu-id="29154-114">Renseignez le reste des propriétés de connexion requises pour vous connecter à votre sortie.</span><span class="sxs-lookup"><span data-stu-id="29154-114">Fill in the rest of the required connection properties to connect to your output.</span></span>  <span data-ttu-id="29154-115">Ces champs varient selon le type de sortie et sont définis en détail ici.</span><span class="sxs-lookup"><span data-stu-id="29154-115">These fields vary by output type and are defined in detail here.</span></span>  
   
    ![Choisir le type de déplacement des données](./media/stream-analytics-add-outputs/2-stream-analytics-add-outputs.png)  
   
3. <span data-ttu-id="29154-117">Selon le type de sortie, vous devrez peut-être spécifier comment les données sont sérialisées ou mises en forme.</span><span class="sxs-lookup"><span data-stu-id="29154-117">Depending on the output type, you may need to specify how the data is serialized or formatted.</span></span> <span data-ttu-id="29154-118">Les paramètres de sérialisation spécifiques pour chaque type de sortie sont décrits ici.</span><span class="sxs-lookup"><span data-stu-id="29154-118">The specific serialization settings for each output type are documented here.</span></span>
   
    <span data-ttu-id="29154-119">Renseignez le reste des propriétés de connexion requises pour vous connecter à votre source de données.</span><span class="sxs-lookup"><span data-stu-id="29154-119">Fill in the rest of the required connection properties to connect to your data source.</span></span> <span data-ttu-id="29154-120">Ces champs varient selon le type d’entrée et le type de source et sont définis en détail dans l’[article Créer une tâche](stream-analytics-create-a-job.md).</span><span class="sxs-lookup"><span data-stu-id="29154-120">These fields vary by type of input and source type and are defined in detail in the [Create Job article](stream-analytics-create-a-job.md).</span></span>  

> [!Note]
>
> <span data-ttu-id="29154-121">Tout élément de sortie ajouté à la tâche doit exister avant que la tâche soit démarrée et que les événements commencent à transiter.</span><span class="sxs-lookup"><span data-stu-id="29154-121">Any output element added to the job, must exist before the job is started and events start flowing.</span></span> <span data-ttu-id="29154-122">Par exemple, si vous utilisez le stockage d'objets Blob en tant que sortie, la tâche ne créera pas de compte de stockage automatiquement.</span><span class="sxs-lookup"><span data-stu-id="29154-122">For example, if you use Blob storage as an output, the job will not create a storage account automatically.</span></span> <span data-ttu-id="29154-123">Celui-ci doit être créé par l'utilisateur avant que la tâche ASA soit démarrée.</span><span class="sxs-lookup"><span data-stu-id="29154-123">It needs to be created by the user before the ASA job is started.</span></span>
> 
 

## <a name="get-help"></a><span data-ttu-id="29154-124">Obtenir de l'aide</span><span class="sxs-lookup"><span data-stu-id="29154-124">Get help</span></span>
<span data-ttu-id="29154-125">Pour obtenir une assistance, essayez notre [forum Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="29154-125">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="29154-126">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="29154-126">Next steps</span></span>
* [<span data-ttu-id="29154-127">Présentation d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="29154-127">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="29154-128">Prise en main d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="29154-128">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="29154-129">Mise à l'échelle des travaux Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="29154-129">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="29154-130">Références sur le langage des requêtes d'Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="29154-130">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="29154-131">Références sur l’API REST de gestion d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="29154-131">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

