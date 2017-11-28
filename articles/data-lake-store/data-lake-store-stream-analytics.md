---
title: "aaaStream des données à partir de l’Analytique des flux de données dans Data Lake Store | Documents Microsoft"
description: "Utiliser des données de toostream Analytique de flux de données Azure dans Azure Data Lake Store"
services: data-lake-store,stream-analytics
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: edb58e0b-311f-44b0-a499-04d7e6c07a90
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 68c727d4807db0abe6efa90145d68c78902eb789
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="stream-data-from-azure-storage-blob-into-data-lake-store-using-azure-stream-analytics"></a><span data-ttu-id="f9cc7-103">Diffuser des données à partir d’un objet blob Azure Storage dans Data Lake Store à l’aide d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="f9cc7-103">Stream data from Azure Storage Blob into Data Lake Store using Azure Stream Analytics</span></span>
<span data-ttu-id="f9cc7-104">Dans cet article, vous allez apprendre comment toouse Azure Data Lake stocker comme sortie pour un travail d’Analytique de flux de données Azure.</span><span class="sxs-lookup"><span data-stu-id="f9cc7-104">In this article you will learn how toouse Azure Data Lake Store as an output for an Azure Stream Analytics job.</span></span> <span data-ttu-id="f9cc7-105">Cet article décrit un scénario simple qui lit les données d’un objet blob de stockage Azure (entrée) et les écritures hello tooData de data Lake Store (sortie).</span><span class="sxs-lookup"><span data-stu-id="f9cc7-105">This article demonstrates a simple scenario that reads data from an Azure Storage blob (input) and writes hello data tooData Lake Store (output).</span></span>

> [!NOTE]
> <span data-ttu-id="f9cc7-106">À ce stade, la création et la configuration de Data Lake Store génère pour les flux de données Analytique est pris en charge uniquement dans hello [portail classique Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="f9cc7-106">At this time, creation and configuration of Data Lake Store outputs for Stream Analytics is supported only in hello [Azure Classic Portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="f9cc7-107">Par conséquent, certaines parties de ce didacticiel utilise hello portail classique Azure.</span><span class="sxs-lookup"><span data-stu-id="f9cc7-107">Hence, some parts of this tutorial will use hello Azure Classic Portal.</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="f9cc7-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="f9cc7-108">Prerequisites</span></span>
<span data-ttu-id="f9cc7-109">Avant de commencer ce didacticiel, vous devez disposer de hello :</span><span class="sxs-lookup"><span data-stu-id="f9cc7-109">Before you begin this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="f9cc7-110">**Un abonnement Azure**.</span><span class="sxs-lookup"><span data-stu-id="f9cc7-110">**An Azure subscription**.</span></span> <span data-ttu-id="f9cc7-111">Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f9cc7-111">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="f9cc7-112">**Compte Stockage Azure**.</span><span class="sxs-lookup"><span data-stu-id="f9cc7-112">**Azure Storage account**.</span></span> <span data-ttu-id="f9cc7-113">Vous allez utiliser un conteneur d’objets blob à partir de ces données tooinput de compte pour une tâche de flux de données Analytique.</span><span class="sxs-lookup"><span data-stu-id="f9cc7-113">You will use a blob container from this account tooinput data for a Stream Analytics job.</span></span> <span data-ttu-id="f9cc7-114">Pour ce didacticiel, vous possédez un compte de stockage nommé **storageforasa** et un conteneur dans le compte de hello appelé **storageforasacontainer**.</span><span class="sxs-lookup"><span data-stu-id="f9cc7-114">For this tutorial, assume you have a storage account called **storageforasa** and a container within hello account called **storageforasacontainer**.</span></span> <span data-ttu-id="f9cc7-115">Une fois que vous avez créé le conteneur de hello, téléchargez un tooit de fichier de données exemple.</span><span class="sxs-lookup"><span data-stu-id="f9cc7-115">Once you have created hello container, upload a sample data file tooit.</span></span> 
  
* <span data-ttu-id="f9cc7-116">**Compte Azure Data Lake Store**.</span><span class="sxs-lookup"><span data-stu-id="f9cc7-116">**Azure Data Lake Store account**.</span></span> <span data-ttu-id="f9cc7-117">Suivez les instructions de hello à [prise en main Azure Data Lake Store à l’aide de hello Azure Portal](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f9cc7-117">Follow hello instructions at [Get started with Azure Data Lake Store using hello Azure Portal](data-lake-store-get-started-portal.md).</span></span> <span data-ttu-id="f9cc7-118">Imaginons que vous ayez un compte Data Lake Store nommé **asadatalakestore**.</span><span class="sxs-lookup"><span data-stu-id="f9cc7-118">Let's assume you have a Data Lake Store account called **asadatalakestore**.</span></span> 

## <a name="create-a-stream-analytics-job"></a><span data-ttu-id="f9cc7-119">Créer un objet blob Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="f9cc7-119">Create a Stream Analytics Job</span></span>
<span data-ttu-id="f9cc7-120">Pour commencer, vous allez créez une tâche Stream Analytics qui inclut une source d’entrée et une destination de sortie.</span><span class="sxs-lookup"><span data-stu-id="f9cc7-120">You start by creating a Stream Analytics job that includes an input source and an output destination.</span></span> <span data-ttu-id="f9cc7-121">Pour ce didacticiel, source de hello est un conteneur d’objets blob Azure et destination de hello Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="f9cc7-121">For this tutorial, hello source is an Azure blob container and hello destination is Data Lake Store.</span></span>

1. <span data-ttu-id="f9cc7-122">Ouverture de session toohello [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f9cc7-122">Sign on toohello [Azure Portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="f9cc7-123">Dans le volet gauche de hello, cliquez sur **des tâches de flux de données Analytique**, puis cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="f9cc7-123">From hello left pane, click **Stream Analytics jobs**, and then click **Add**.</span></span>

    <span data-ttu-id="f9cc7-124">![Création d’un travail Stream Analytics](./media/data-lake-store-stream-analytics/create.job.png "Création d’un travail Stream Analytics")</span><span class="sxs-lookup"><span data-stu-id="f9cc7-124">![Create a Stream Analytics Job](./media/data-lake-store-stream-analytics/create.job.png "Create a Stream Analytics job")</span></span>

    > [!NOTE]
    > <span data-ttu-id="f9cc7-125">Vérifiez que vous créez un travail Bonjour même région que le compte de stockage hello ou occasionnent des frais supplémentaires de déplacement des données entre les régions.</span><span class="sxs-lookup"><span data-stu-id="f9cc7-125">Make sure you create job in hello same region as hello storage account or you will incur additional cost of moving data between regions.</span></span>
    >

## <a name="create-a-blob-input-for-hello-job"></a><span data-ttu-id="f9cc7-126">Créer une entrée d’objet Blob pour le travail de hello</span><span class="sxs-lookup"><span data-stu-id="f9cc7-126">Create a Blob input for hello job</span></span>

1. <span data-ttu-id="f9cc7-127">Page de hello ouvert pour la tâche de flux de données Analytique hello, hello volet de gauche, cliquez sur hello **entrées** onglet, puis cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="f9cc7-127">Open hello page for hello Stream Analytics job, from hello left pane click hello **Inputs** tab, and then click **Add**.</span></span>

    <span data-ttu-id="f9cc7-128">![Ajouter un travail d’entrée tooyour](./media/data-lake-store-stream-analytics/create.input.1.png "d’ajouter un travail d’entrée tooyour")</span><span class="sxs-lookup"><span data-stu-id="f9cc7-128">![Add an input tooyour job](./media/data-lake-store-stream-analytics/create.input.1.png "Add an input tooyour job")</span></span>

2. <span data-ttu-id="f9cc7-129">Sur hello **nouvelle entrée** panneau, fournir hello valeurs suivantes.</span><span class="sxs-lookup"><span data-stu-id="f9cc7-129">On hello **New input** blade, provide hello following values.</span></span>

    <span data-ttu-id="f9cc7-130">![Ajouter un travail d’entrée tooyour](./media/data-lake-store-stream-analytics/create.input.2.png "d’ajouter un travail d’entrée tooyour")</span><span class="sxs-lookup"><span data-stu-id="f9cc7-130">![Add an input tooyour job](./media/data-lake-store-stream-analytics/create.input.2.png "Add an input tooyour job")</span></span>

    * <span data-ttu-id="f9cc7-131">Pour **alias d’entrée**, entrez un nom unique pour l’entrée de tâche hello.</span><span class="sxs-lookup"><span data-stu-id="f9cc7-131">For **Input alias**, enter a unique name for hello job input.</span></span>
    * <span data-ttu-id="f9cc7-132">Pour **Type de source**, sélectionnez **Flux de données**.</span><span class="sxs-lookup"><span data-stu-id="f9cc7-132">For **Source type**, select **Data stream**.</span></span>
    * <span data-ttu-id="f9cc7-133">Pour **Source**, sélectionnez **Stockage d’objets blob**.</span><span class="sxs-lookup"><span data-stu-id="f9cc7-133">For **Source**, select **Blob storage**.</span></span>
    * <span data-ttu-id="f9cc7-134">Pour **Abonnement**, sélectionnez **Utiliser l'objet blob de stockage de l'abonnement actuel**.</span><span class="sxs-lookup"><span data-stu-id="f9cc7-134">For **Subscription**, select **Use blob storage from current subscription**.</span></span>
    * <span data-ttu-id="f9cc7-135">Pour **compte de stockage**, sélectionnez le compte de stockage hello que vous avez créé dans le cadre des conditions préalables de hello.</span><span class="sxs-lookup"><span data-stu-id="f9cc7-135">For **Storage account**, select hello storage account that you created as part of hello prerequisites.</span></span> 
    * <span data-ttu-id="f9cc7-136">Pour **conteneur**, sélectionnez conteneur hello que vous avez créé dans hello sélectionné compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="f9cc7-136">For **Container**, select hello container that you created in hello selected storage account.</span></span>
    * <span data-ttu-id="f9cc7-137">Pour **Format de sérialisation de l’événement**, sélectionnez **CSV**.</span><span class="sxs-lookup"><span data-stu-id="f9cc7-137">For **Event serialization format**, select **CSV**.</span></span>
    * <span data-ttu-id="f9cc7-138">Pour **Délimiteur**, sélectionnez **tabulation**.</span><span class="sxs-lookup"><span data-stu-id="f9cc7-138">For **Delimiter**, select **tab**.</span></span>
    * <span data-ttu-id="f9cc7-139">Pour **Encodage**, sélectionnez **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="f9cc7-139">For **Encoding**, select **UTF-8**.</span></span>

    <span data-ttu-id="f9cc7-140">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="f9cc7-140">Click **Create**.</span></span> <span data-ttu-id="f9cc7-141">portail de Hello maintenant ajoute l’entrée de hello et teste hello connexion tooit.</span><span class="sxs-lookup"><span data-stu-id="f9cc7-141">hello portal now adds hello input and tests hello connection tooit.</span></span>


## <a name="create-a-data-lake-store-output-for-hello-job"></a><span data-ttu-id="f9cc7-142">Créez une sortie Data Lake Store pour le travail de hello</span><span class="sxs-lookup"><span data-stu-id="f9cc7-142">Create a Data Lake Store output for hello job</span></span>

1. <span data-ttu-id="f9cc7-143">Page hello pour la tâche de flux de données Analytique hello, cliquez sur hello **sorties** onglet, puis cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="f9cc7-143">Open hello page for hello Stream Analytics job, click hello **Outputs** tab, and then click **Add**.</span></span>

    <span data-ttu-id="f9cc7-144">![Ajouter un travail de tooyour sortie](./media/data-lake-store-stream-analytics/create.output.1.png "d’ajouter un travail tooyour de sortie")</span><span class="sxs-lookup"><span data-stu-id="f9cc7-144">![Add an output tooyour job](./media/data-lake-store-stream-analytics/create.output.1.png "Add an output tooyour job")</span></span>

2. <span data-ttu-id="f9cc7-145">Sur hello **nouvelle sortie** panneau, fournir hello valeurs suivantes.</span><span class="sxs-lookup"><span data-stu-id="f9cc7-145">On hello **New output** blade, provide hello following values.</span></span>

    <span data-ttu-id="f9cc7-146">![Ajouter un travail de tooyour sortie](./media/data-lake-store-stream-analytics/create.output.2.png "d’ajouter un travail tooyour de sortie")</span><span class="sxs-lookup"><span data-stu-id="f9cc7-146">![Add an output tooyour job](./media/data-lake-store-stream-analytics/create.output.2.png "Add an output tooyour job")</span></span>

    * <span data-ttu-id="f9cc7-147">Pour **alias de sortie**, saisissez un un nom unique pour la sortie de tâche hello.</span><span class="sxs-lookup"><span data-stu-id="f9cc7-147">For **Output alias**, enter a a unique name for hello job output.</span></span> <span data-ttu-id="f9cc7-148">Il s’agit d’un nom convivial utilisé dans les requêtes toodirect hello requête sortie toothis Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="f9cc7-148">This is a friendly name used in queries toodirect hello query output toothis Data Lake Store.</span></span>
    * <span data-ttu-id="f9cc7-149">Pour **Récepteur**, sélectionnez **Data Lake Store**.</span><span class="sxs-lookup"><span data-stu-id="f9cc7-149">For **Sink**, select **Data Lake Store**.</span></span>
    * <span data-ttu-id="f9cc7-150">Vous serez invité à tooauthorize accéder au compte tooData Lake Store.</span><span class="sxs-lookup"><span data-stu-id="f9cc7-150">You will be prompted tooauthorize access tooData Lake Store account.</span></span> <span data-ttu-id="f9cc7-151">Cliquez sur **Autoriser**.</span><span class="sxs-lookup"><span data-stu-id="f9cc7-151">Click **Authorize**.</span></span>

3. <span data-ttu-id="f9cc7-152">Sur hello **nouvelle sortie** lames, continuer hello tooprovide valeurs suivantes.</span><span class="sxs-lookup"><span data-stu-id="f9cc7-152">On hello **New output** blade, continue tooprovide hello following values.</span></span>

    <span data-ttu-id="f9cc7-153">![Ajouter un travail de tooyour sortie](./media/data-lake-store-stream-analytics/create.output.3.png "d’ajouter un travail tooyour de sortie")</span><span class="sxs-lookup"><span data-stu-id="f9cc7-153">![Add an output tooyour job](./media/data-lake-store-stream-analytics/create.output.3.png "Add an output tooyour job")</span></span>

    * <span data-ttu-id="f9cc7-154">Pour **nom de compte**, sélectionnez compte de Data Lake Store hello créé déjà où vous souhaitez toobe de sortie de tâche hello envoyé à.</span><span class="sxs-lookup"><span data-stu-id="f9cc7-154">For **Account name**, select hello Data Lake Store account you already created where you want hello job output toobe sent to.</span></span>
    * <span data-ttu-id="f9cc7-155">Pour **motif de préfixe de chemin d’accès**, entrez un toowrite de chemin d’accès du fichier vos fichiers au sein de hello spécifié compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="f9cc7-155">For **Path prefix pattern**, enter a file path used toowrite your files within hello specified Data Lake Store account.</span></span>
    * <span data-ttu-id="f9cc7-156">Pour **format de Date**, si vous avez utilisé un jeton de date dans le chemin d’accès de hello préfixe, vous pouvez sélectionner le format de date hello dans lequel vos fichiers sont organisés.</span><span class="sxs-lookup"><span data-stu-id="f9cc7-156">For **Date format**, if you used a date token in hello prefix path, you can select hello date format in which your files are organized.</span></span>
    * <span data-ttu-id="f9cc7-157">Pour **format d’heure**, si vous avez utilisé un jeton de temps dans le chemin d’accès du préfixe hello, spécifiez le format d’heure hello dans lequel vos fichiers sont organisés.</span><span class="sxs-lookup"><span data-stu-id="f9cc7-157">For **Time format**, if you used a time token in hello prefix path, specify hello time format in which your files are organized.</span></span>
    * <span data-ttu-id="f9cc7-158">Pour **Format de sérialisation de l’événement**, sélectionnez **CSV**.</span><span class="sxs-lookup"><span data-stu-id="f9cc7-158">For **Event serialization format**, select **CSV**.</span></span>
    * <span data-ttu-id="f9cc7-159">Pour **Délimiteur**, sélectionnez **tabulation**.</span><span class="sxs-lookup"><span data-stu-id="f9cc7-159">For **Delimiter**, select **tab**.</span></span>
    * <span data-ttu-id="f9cc7-160">Pour **Encodage**, sélectionnez **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="f9cc7-160">For **Encoding**, select **UTF-8**.</span></span>
    
    <span data-ttu-id="f9cc7-161">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="f9cc7-161">Click **Create**.</span></span> <span data-ttu-id="f9cc7-162">portail de Hello maintenant ajoute la sortie de hello et teste hello connexion tooit.</span><span class="sxs-lookup"><span data-stu-id="f9cc7-162">hello portal now adds hello output and tests hello connection tooit.</span></span>
    
## <a name="run-hello-stream-analytics-job"></a><span data-ttu-id="f9cc7-163">Exécuter la tâche de flux de données Analytique hello</span><span class="sxs-lookup"><span data-stu-id="f9cc7-163">Run hello Stream Analytics job</span></span>

1. <span data-ttu-id="f9cc7-164">toorun une tâche de flux de données Analytique, vous devez exécuter une requête à partir de hello **requête** onglet. Pour ce didacticiel, vous pouvez exécuter l’exemple de requête hello en remplaçant des espaces réservés de hello avec hello travail alias d’entrée et de sortie, comme indiqué dans la capture d’écran hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="f9cc7-164">toorun a Stream Analytics job, you must run a query from hello **Query** tab. For this tutorial, you can run hello sample query by replacing hello placeholders with hello job input and output aliases, as shown in hello screen capture below.</span></span>

    <span data-ttu-id="f9cc7-165">![Exécutez une requête](./media/data-lake-store-stream-analytics/run.query.png "Exécuter une requête")</span><span class="sxs-lookup"><span data-stu-id="f9cc7-165">![Run query](./media/data-lake-store-stream-analytics/run.query.png "Run query")</span></span>

2. <span data-ttu-id="f9cc7-166">Cliquez sur **enregistrer** de haut hello d’écran hello, puis de hello **vue d’ensemble** , cliquez sur **Démarrer**.</span><span class="sxs-lookup"><span data-stu-id="f9cc7-166">Click **Save** from hello top of hello screen, and then from hello **Overview** tab, click **Start**.</span></span> <span data-ttu-id="f9cc7-167">Dans la boîte de dialogue hello, sélectionnez **heure personnalisé**, puis définissez hello date et heure actuelles.</span><span class="sxs-lookup"><span data-stu-id="f9cc7-167">From hello dialog box, select **Custom Time**, and then set hello current date and time.</span></span>

    <span data-ttu-id="f9cc7-168">![Définir l’heure du travail](./media/data-lake-store-stream-analytics/run.query.2.png "Définir l’heure du travail")</span><span class="sxs-lookup"><span data-stu-id="f9cc7-168">![Set job time](./media/data-lake-store-stream-analytics/run.query.2.png "Set job time")</span></span>

    <span data-ttu-id="f9cc7-169">Cliquez sur **Démarrer** tâche hello de toostart.</span><span class="sxs-lookup"><span data-stu-id="f9cc7-169">Click **Start** toostart hello job.</span></span> <span data-ttu-id="f9cc7-170">Il peut prendre le travail hello toostart tooa deux minutes.</span><span class="sxs-lookup"><span data-stu-id="f9cc7-170">It can take up tooa couple minutes toostart hello job.</span></span>

3. <span data-ttu-id="f9cc7-171">données de salutation tootrigger hello travail toopick à partir de l’objet blob de hello, copiez un conteneur d’objets blob toohello fichier exemple données.</span><span class="sxs-lookup"><span data-stu-id="f9cc7-171">tootrigger hello job toopick hello data from hello blob, copy a sample data file toohello blob container.</span></span> <span data-ttu-id="f9cc7-172">Vous pouvez obtenir un exemple de fichier de données à partir de hello [référentiel Git de LAC de données Azure](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/Drivers.txt).</span><span class="sxs-lookup"><span data-stu-id="f9cc7-172">You can get a sample data file from hello [Azure Data Lake Git Repository](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/Drivers.txt).</span></span> <span data-ttu-id="f9cc7-173">Pour ce didacticiel, nous allons copier hello fichier **vehicle1_09142014.csv**.</span><span class="sxs-lookup"><span data-stu-id="f9cc7-173">For this tutorial, let's copy hello file **vehicle1_09142014.csv**.</span></span> <span data-ttu-id="f9cc7-174">Vous pouvez utiliser différents clients, tels que [Azure Storage Explorer](http://storageexplorer.com/), conteneur d’objets blob tooa tooupload données.</span><span class="sxs-lookup"><span data-stu-id="f9cc7-174">You can use various clients, such as [Azure Storage Explorer](http://storageexplorer.com/), tooupload data tooa blob container.</span></span>

4. <span data-ttu-id="f9cc7-175">À partir de hello **vue d’ensemble** sous l’onglet sous **analyse**, voir la façon dont les données de hello ont été traitées.</span><span class="sxs-lookup"><span data-stu-id="f9cc7-175">From hello **Overview** tab, under **Monitoring**, see how hello data was processed.</span></span>

    <span data-ttu-id="f9cc7-176">![Surveiller la tâche](./media/data-lake-store-stream-analytics/run.query.3.png "Surveiller la tâche")</span><span class="sxs-lookup"><span data-stu-id="f9cc7-176">![Monitor job](./media/data-lake-store-stream-analytics/run.query.3.png "Monitor job")</span></span>

5. <span data-ttu-id="f9cc7-177">Enfin, vous pouvez vérifier que les données de sortie de tâche hello soient disponibles dans le compte Data Lake Store de hello.</span><span class="sxs-lookup"><span data-stu-id="f9cc7-177">Finally, you can verify that hello job output data is available in hello Data Lake Store account.</span></span> 

    <span data-ttu-id="f9cc7-178">![Vérifier la sortie](./media/data-lake-store-stream-analytics/run.query.4.png "Vérifier la sortie")</span><span class="sxs-lookup"><span data-stu-id="f9cc7-178">![Verify output](./media/data-lake-store-stream-analytics/run.query.4.png "Verify output")</span></span>

    <span data-ttu-id="f9cc7-179">Dans le volet de l’Explorateur de données hello, notez que hello sortie le chemin d’accès du dossier tooa écrit comme spécifié dans hello Data Lake Store les paramètres de sortie (`streamanalytics/job/output/{date}/{time}`).</span><span class="sxs-lookup"><span data-stu-id="f9cc7-179">In hello Data Explorer pane, notice that hello output is written tooa folder path as specified in hello Data Lake Store output settings (`streamanalytics/job/output/{date}/{time}`).</span></span>  

## <a name="see-also"></a><span data-ttu-id="f9cc7-180">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="f9cc7-180">See also</span></span>
* [<span data-ttu-id="f9cc7-181">Créer un toouse du cluster HDInsight Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="f9cc7-181">Create an HDInsight cluster toouse Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
