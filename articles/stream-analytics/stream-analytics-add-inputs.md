---
title: "aaaAdd données d’entrée des tâches de flux de données Analytique tooyour | Documents Microsoft"
description: "Découvrez comment toohook d’un tooyour de source de données Analytique de flux de travail en diffusion en continu de données d’entrée à partir des données de concentrateurs d’événements ou une référence à partir du stockage d’objets BLOB."
keywords: "entrée de données, données de diffusion en continu"
documentationcenter: 
services: stream-analytics
author: samacha
manager: jhubbard
editor: 
ms.assetid: 9e59bd24-2a80-4ecb-b6b2-309a07c70bcd
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: 674000268fcdf9bc000af3e2f166cb66f1366922
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-streaming-data-input-or-reference-data-tooa-stream-analytics-job"></a><span data-ttu-id="7fc33-104">Ajout d’une diffusion en continu données d’entrée ou de référence données tooa flux Analytique tâche</span><span class="sxs-lookup"><span data-stu-id="7fc33-104">Add a streaming data input or reference data tooa Stream Analytics job</span></span>
<span data-ttu-id="7fc33-105">Découvrez comment toohook d’un tooyour de source de données Analytique de flux de travail en diffusion en continu de données d’entrée à partir des données de concentrateurs d’événements ou une référence à partir du stockage d’objets Blob.</span><span class="sxs-lookup"><span data-stu-id="7fc33-105">Learn how toohook up a data source tooyour Stream Analytics job as streaming data input from Event Hubs or reference data from Blob storage.</span></span>

<span data-ttu-id="7fc33-106">Les tâches de flux de données Analytique Azure peuvent être connecté tooone données d’entrée ou plus d’informations, dont chacune définit une source de données existante du tooan de connexion.</span><span class="sxs-lookup"><span data-stu-id="7fc33-106">Azure Stream Analytics jobs can be connected tooone data input or more, each of which define a connection tooan existing data source.</span></span> <span data-ttu-id="7fc33-107">Comme les données sont envoyées de source de données toothat, il est consommé par la tâche de flux de données Analytique hello et traité en temps réel en tant que la diffusion en continu de données.</span><span class="sxs-lookup"><span data-stu-id="7fc33-107">As data is sent toothat data source, it is consumed by hello Stream Analytics job and processed in real time as streaming data.</span></span> <span data-ttu-id="7fc33-108">Flux de données Analytique a integration de première classe avec [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/) et [le stockage Blob Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md) au sein et en dehors de l’abonnement de la tâche hello.</span><span class="sxs-lookup"><span data-stu-id="7fc33-108">Stream Analytics has first class integration with [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/) and [Azure Blob storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md) both within and outside of hello job's subscription.</span></span>

<span data-ttu-id="7fc33-109">Cet article est une étape Bonjour [Analytique de flux de données d’apprentissage](/documentation/learning-paths/stream-analytics/).</span><span class="sxs-lookup"><span data-stu-id="7fc33-109">This article is a step in hello [Stream Analytics learning path](/documentation/learning-paths/stream-analytics/).</span></span>

## <a name="data-input-streaming-data-and-reference-data"></a><span data-ttu-id="7fc33-110">Entrée de données : données de référence et données de diffusion en continu</span><span class="sxs-lookup"><span data-stu-id="7fc33-110">Data input: Streaming data and reference data</span></span>
<span data-ttu-id="7fc33-111">Il existe deux types d’entrées dans Stream Analytics : les flux de données et les données de référence.</span><span class="sxs-lookup"><span data-stu-id="7fc33-111">There are two distinct types of inputs in Stream Analytics: data streams and reference data.</span></span>

* <span data-ttu-id="7fc33-112">**Flux de données**: tâches de flux de données Analytique doivent inclure au moins un données flux d’entrée toobe consommé et transformés par la tâche de hello.</span><span class="sxs-lookup"><span data-stu-id="7fc33-112">**Data Streams**: Stream Analytics jobs must include at least one data stream input toobe consumed and transformed by hello job.</span></span> <span data-ttu-id="7fc33-113">Le stockage d’objets blob Azure et Azure Event Hubs sont pris en charge en tant que sources d’entrée de flux de données.</span><span class="sxs-lookup"><span data-stu-id="7fc33-113">Azure Blob storage and Azure Event Hubs are supported as data stream input sources.</span></span> <span data-ttu-id="7fc33-114">Les concentrateurs d’événements Azure sont toocollect utilisés les flux d’événements de périphériques connectés, les services et applications.</span><span class="sxs-lookup"><span data-stu-id="7fc33-114">Azure Event Hubs are used toocollect event streams from connected devices, services and applications.</span></span> <span data-ttu-id="7fc33-115">Le stockage d'objets blob Azure peut être utilisé comme source d'entrée pour la réception de données en bloc en tant que flux.</span><span class="sxs-lookup"><span data-stu-id="7fc33-115">Azure Blob storage can be used as an input source for ingesting bulk data as a stream.</span></span>  
* <span data-ttu-id="7fc33-116">**Données de référence**: Stream Analytics prend en charge un deuxième type d'entrée auxiliaire appelé données de référence.</span><span class="sxs-lookup"><span data-stu-id="7fc33-116">**Reference data**: Stream Analytics supports a second type of auxiliary input called reference data.</span></span>  <span data-ttu-id="7fc33-117">En tant que toodata exécutée en mouvement, ces données sont statiques ou de ralentissement de la modification.</span><span class="sxs-lookup"><span data-stu-id="7fc33-117">As opposed toodata in motion, this data is static or slowing changing.</span></span>  <span data-ttu-id="7fc33-118">Il est généralement utilisé pour effectuer des recherches et les corrélations avec des flux de données toocreate un jeu de données plus riche.</span><span class="sxs-lookup"><span data-stu-id="7fc33-118">It is typically used for performing look-ups and correlations with data streams toocreate a richer data set.</span></span>  <span data-ttu-id="7fc33-119">Stockage d’objets Blob Azure est actuellement hello pris en charge uniquement la source d’entrée pour les données de référence.</span><span class="sxs-lookup"><span data-stu-id="7fc33-119">Azure Blob storage is currently hello only supported input source for reference data.</span></span>  

<span data-ttu-id="7fc33-120">tooadd une tâche de flux de données Analytique tooyour d’entrée :</span><span class="sxs-lookup"><span data-stu-id="7fc33-120">tooadd an input tooyour Stream Analytics job:</span></span>

1. <span data-ttu-id="7fc33-121">Bonjour portail Azure, cliquez sur **entrées** puis cliquez sur **ajouter une entrée** dans votre tâche de flux de données Analytique.</span><span class="sxs-lookup"><span data-stu-id="7fc33-121">In hello Azure portal click **Inputs** and then click **Add an Input** in your Stream Analytics job.</span></span>
   
    ![Portail Azure Classic - ajouter une entrée.](./media/stream-analytics-add-inputs/1-stream-analytics-add-inputs.png)  
   
    <span data-ttu-id="7fc33-123">Bonjour portail Azure, cliquez sur hello **entrées** vignette dans votre tâche de flux de données Analytique.</span><span class="sxs-lookup"><span data-stu-id="7fc33-123">In hello Azure portal click hello **Inputs** tile in your Stream Analytics job.</span></span>  
   
    ![Portail Azure - ajouter une entrée de données.](./media/stream-analytics-add-inputs/7-stream-analytics-add-inputs.png)  
2. <span data-ttu-id="7fc33-125">Spécifiez le type hello d’entrée de hello : soit **flux de données** ou **données de référence**.</span><span class="sxs-lookup"><span data-stu-id="7fc33-125">Specify hello type of hello input: either **Data stream** or **Reference data**.</span></span>
   
    ![Ajouter les données correctes hello d’entrée, en continu ou référence](./media/stream-analytics-add-inputs/2-stream-analytics-add-inputs.png)  
   
    ![Ajouter les données correctes hello d’entrée, en continu ou référence](./media/stream-analytics-add-inputs/8-stream-analytics-add-inputs.png)  
3. <span data-ttu-id="7fc33-128">Si vous créez une entrée de flux de données, spécifiez le type de source de hello pour l’entrée de hello.</span><span class="sxs-lookup"><span data-stu-id="7fc33-128">If creating a Data Stream input, specify hello source type for hello input.</span></span>  <span data-ttu-id="7fc33-129">Cet étape peut être ignorée lors de la création de Données de référence car seul le stockage d'objets Blob est pris en charge à ce stade.</span><span class="sxs-lookup"><span data-stu-id="7fc33-129">This step can be skipped during Reference Data creation as only Blob storage is supported at this time.</span></span>
   
    ![Ajouter une entrée de données de diffusion en continu](./media/stream-analytics-add-inputs/3-stream-analytics-add-inputs.png)  
   
    ![Ajouter une entrée de données de diffusion en continu](./media/stream-analytics-add-inputs/9-stream-analytics-add-inputs.png)  
4. <span data-ttu-id="7fc33-132">Fournissez un nom convivial pour cette entrée dans hello zone Alias d’entrée.</span><span class="sxs-lookup"><span data-stu-id="7fc33-132">Provide a friendly name for this input in hello Input Alias box.</span></span>  <span data-ttu-id="7fc33-133">Ce nom sera utilisé dans la requête de votre travail plus tard dans l’entrée de toohello toorefer.</span><span class="sxs-lookup"><span data-stu-id="7fc33-133">This name will be used in your job's query later on toorefer toohello input.</span></span>
   
    <span data-ttu-id="7fc33-134">Renseignez les autres hello hello connexion requise propriétés tooconnect tooyour de source de données.</span><span class="sxs-lookup"><span data-stu-id="7fc33-134">Fill in hello rest of hello required connection properties tooconnect tooyour data source.</span></span> <span data-ttu-id="7fc33-135">Ces champs varient selon le type d'entrée et le type de source, et sont définis en détail [ici](stream-analytics-create-a-job.md).</span><span class="sxs-lookup"><span data-stu-id="7fc33-135">These fields vary by type of input and source type and are defined in detail [here](stream-analytics-create-a-job.md).</span></span>  
   
    ![Ajouter une entrée de données de hub d’événements](./media/stream-analytics-add-inputs/4-stream-analytics-add-inputs.png)  
5. <span data-ttu-id="7fc33-137">Spécifiez les paramètres de sérialisation hello pour les données d’entrée hello :</span><span class="sxs-lookup"><span data-stu-id="7fc33-137">Specify hello serialization settings for hello input data:</span></span>
   
   * <span data-ttu-id="7fc33-138">toomake que vos requêtes fonctionnent comme de hello vous le souhaitez, spécifier hello **Format de sérialisation d’événements** des données entrantes.</span><span class="sxs-lookup"><span data-stu-id="7fc33-138">toomake sure your queries work hello way you expect, specify hello **Event Serialization Format** of incoming data.</span></span>  <span data-ttu-id="7fc33-139">Les formats de sérialisation pris en charge sont JSON, CSV et Avro.</span><span class="sxs-lookup"><span data-stu-id="7fc33-139">Supported serialization formats are JSON, CSV, and Avro.</span></span>
   * <span data-ttu-id="7fc33-140">Vérifiez que hello **codage** pour les données de salutation.</span><span class="sxs-lookup"><span data-stu-id="7fc33-140">Verify hello **Encoding** for hello data.</span></span>  <span data-ttu-id="7fc33-141">UTF-8 est hello uniquement une prise en charge de format d’encodage pour l’instant.</span><span class="sxs-lookup"><span data-stu-id="7fc33-141">UTF-8 is hello only supported encoding format at this time.</span></span>
     
     ![Paramètres de sérialisation des données pour l’entrée de données hello](./media/stream-analytics-add-inputs/5-stream-analytics-add-inputs.png)  
     
     ![Paramètres de sérialisation des données pour l’entrée de données hello](./media/stream-analytics-add-inputs/10-stream-analytics-add-inputs.png)  
6. <span data-ttu-id="7fc33-144">À l’issue de la création d’entrée de hello, flux de données Analytique vérifiera qu’il peut se connecter source d’entrée de toohello.</span><span class="sxs-lookup"><span data-stu-id="7fc33-144">After completing hello input creation, Stream Analytics will verify that it can connect toohello input source.</span></span>  <span data-ttu-id="7fc33-145">Vous pouvez afficher l’état hello Hello opération de tester la connexion dans le hub de Notification hello.</span><span class="sxs-lookup"><span data-stu-id="7fc33-145">You can view hello status of hello Test Connection operation in hello Notification hub.</span></span>
   
    ![Tester la connexion de hello de diffusion en continu des données d’entrée](./media/stream-analytics-add-inputs/6-stream-analytics-add-inputs.png)  
   
    ![Tester la connexion de hello de diffusion en continu des données d’entrée](./media/stream-analytics-add-inputs/11-stream-analytics-add-inputs.png)  

## <a name="get-help-with-streaming-data-inputs"></a><span data-ttu-id="7fc33-148">Obtenir de l'aide sur les entrées de données de diffusion en continu</span><span class="sxs-lookup"><span data-stu-id="7fc33-148">Get help with streaming data inputs</span></span>
<span data-ttu-id="7fc33-149">Pour obtenir une assistance, essayez notre [forum Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="7fc33-149">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="7fc33-150">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7fc33-150">Next steps</span></span>
* [<span data-ttu-id="7fc33-151">Introduction tooAzure Analytique de flux de données</span><span class="sxs-lookup"><span data-stu-id="7fc33-151">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="7fc33-152">Prise en main d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="7fc33-152">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="7fc33-153">Mise à l'échelle des travaux Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="7fc33-153">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="7fc33-154">Références sur le langage des requêtes d'Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="7fc33-154">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="7fc33-155">Références sur l’API REST de gestion d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="7fc33-155">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

