---
title: "aaaCapture des données à partir de concentrateurs d’événements dans Azure Data Lake Store | Documents Microsoft"
description: "Données de toocapture utilisation Azure Data Lake Store à partir des concentrateurs d’événements"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/28/2017
ms.author: nitinme
ms.openlocfilehash: 09b17bd0b47043bd2c83dba72c01a8064f206a0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-data-lake-store-toocapture-data-from-event-hubs"></a><span data-ttu-id="5350f-103">Données de toocapture utilisation Azure Data Lake Store à partir des concentrateurs d’événements</span><span class="sxs-lookup"><span data-stu-id="5350f-103">Use Azure Data Lake Store toocapture data from Event Hubs</span></span>

<span data-ttu-id="5350f-104">Découvrez comment toouse données toocapture de Azure Data Lake Store reçues par Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="5350f-104">Learn how toouse Azure Data Lake Store toocapture data received by Azure Event Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5350f-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="5350f-105">Prerequisites</span></span>

* <span data-ttu-id="5350f-106">**Un abonnement Azure**.</span><span class="sxs-lookup"><span data-stu-id="5350f-106">**An Azure subscription**.</span></span> <span data-ttu-id="5350f-107">Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5350f-107">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="5350f-108">**Un compte Azure Data Lake Store**.</span><span class="sxs-lookup"><span data-stu-id="5350f-108">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="5350f-109">Pour obtenir des instructions sur la façon de voir d’un seul, toocreate [prise en main Azure Data Lake Store](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5350f-109">For instructions on how toocreate one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md).</span></span>

*  <span data-ttu-id="5350f-110">**Un espace de noms Event Hubs**.</span><span class="sxs-lookup"><span data-stu-id="5350f-110">**An Event Hubs namespace**.</span></span> <span data-ttu-id="5350f-111">Pour obtenir des instructions, consultez [Créer un espace de noms Event Hubs](../event-hubs/event-hubs-create.md#create-an-event-hubs-namespace).</span><span class="sxs-lookup"><span data-stu-id="5350f-111">For instructions, see [Create an Event Hubs namespace](../event-hubs/event-hubs-create.md#create-an-event-hubs-namespace).</span></span> <span data-ttu-id="5350f-112">Assurez-vous que le compte Data Lake Store de hello et espace de noms de concentrateurs d’événements hello sont Bonjour même abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="5350f-112">Make sure hello Data Lake Store account and hello Event Hubs namespace are in hello same Azure subscription.</span></span>


## <a name="assign-permissions-tooevent-hubs"></a><span data-ttu-id="5350f-113">Affecter des autorisations tooEvent concentrateurs</span><span class="sxs-lookup"><span data-stu-id="5350f-113">Assign permissions tooEvent Hubs</span></span>

<span data-ttu-id="5350f-114">Dans cette section, vous créez un dossier dans le compte de hello où vous souhaitez toocapture les données de hello de concentrateurs d’événements.</span><span class="sxs-lookup"><span data-stu-id="5350f-114">In this section, you create a folder within hello account where you want toocapture hello data from Event Hubs.</span></span> <span data-ttu-id="5350f-115">Vous également affectez des autorisations tooEvent concentrateurs afin qu’il peut écrire des données dans un compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="5350f-115">You also assign permissions tooEvent Hubs so that it can write data into a Data Lake Store account.</span></span> 

1. <span data-ttu-id="5350f-116">Ouvrez hello Data Lake Store compte sur lequel vous souhaitez toocapture les données à partir de concentrateurs d’événements, puis cliquez sur **Explorateur de données**.</span><span class="sxs-lookup"><span data-stu-id="5350f-116">Open hello Data Lake Store account where you want toocapture data from Event Hubs and then click on **Data Explorer**.</span></span>

    <span data-ttu-id="5350f-117">![Explorateur de données Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-open-data-explorer.png "Explorateur de données Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="5350f-117">![Data Lake Store data explorer](./media/data-lake-store-archive-eventhub-capture/data-lake-store-open-data-explorer.png "Data Lake Store data explorer")</span></span>

2.  <span data-ttu-id="5350f-118">Cliquez sur **nouveau dossier** , puis entrez un nom pour le dossier dans lequel les données de salutation toocapture.</span><span class="sxs-lookup"><span data-stu-id="5350f-118">Click **New Folder** and then enter a name for folder where you want toocapture hello data.</span></span>

    <span data-ttu-id="5350f-119">![Créer un dossier dans Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-new-folder.png "Créer un dossier dans Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="5350f-119">![Create a new folder in Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-new-folder.png "Create a new folder in Data Lake Store")</span></span>

3. <span data-ttu-id="5350f-120">Affecter des autorisations au niveau de la racine de hello Hello Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="5350f-120">Assign permissions at hello root of hello Data Lake Store.</span></span> 

    <span data-ttu-id="5350f-121">a.</span><span class="sxs-lookup"><span data-stu-id="5350f-121">a.</span></span> <span data-ttu-id="5350f-122">Cliquez sur **Explorateur de données**, sélectionnez racine hello hello compte Data Lake Store, puis cliquez sur **accès**.</span><span class="sxs-lookup"><span data-stu-id="5350f-122">Click **Data Explorer**, select hello root of hello Data Lake Store account, and then click **Access**.</span></span>

    <span data-ttu-id="5350f-123">![Affecter des autorisations pour la racine du compte Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-root.png "Affecter des autorisations pour la racine du compte Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="5350f-123">![Assign permissions for Data Lake Store root](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-root.png "Assign permissions for Data Lake Store root")</span></span>

    <span data-ttu-id="5350f-124">b.</span><span class="sxs-lookup"><span data-stu-id="5350f-124">b.</span></span> <span data-ttu-id="5350f-125">Sous **Accès**, cliquez sur **Ajouter**, cliquez sur **Sélectionner un utilisateur ou un groupe**, puis recherchez `Microsoft.EventHubs`.</span><span class="sxs-lookup"><span data-stu-id="5350f-125">Under **Access**, click **Add**, click **Select User or Group**, and then search for `Microsoft.EventHubs`.</span></span> 

    <span data-ttu-id="5350f-126">![Affecter des autorisations pour la racine du compte Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "Affecter des autorisations pour la racine du compte Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="5350f-126">![Assign permissions for Data Lake Store root](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "Assign permissions for Data Lake Store root")</span></span>
    
    <span data-ttu-id="5350f-127">Cliquez sur **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="5350f-127">Click **Select**.</span></span>

    <span data-ttu-id="5350f-128">c.</span><span class="sxs-lookup"><span data-stu-id="5350f-128">c.</span></span> <span data-ttu-id="5350f-129">Sous **Affecter des autorisations**, cliquez sur **Sélectionner des autorisations**.</span><span class="sxs-lookup"><span data-stu-id="5350f-129">Under **Assign Permissions**, click **Select Permissions**.</span></span> <span data-ttu-id="5350f-130">Définissez **autorisations** trop**Execute**.</span><span class="sxs-lookup"><span data-stu-id="5350f-130">Set **Permissions** too**Execute**.</span></span> <span data-ttu-id="5350f-131">Définissez **ajouter à** trop**ce dossier et tous les enfants**.</span><span class="sxs-lookup"><span data-stu-id="5350f-131">Set **Add to** too**This folder and all children**.</span></span> <span data-ttu-id="5350f-132">Définissez **ajouter en tant que** trop**une entrée d’autorisation accès et une entrée d’autorisation par défaut**.</span><span class="sxs-lookup"><span data-stu-id="5350f-132">Set **Add as** too**An access permission entry and a default permission entry**.</span></span>

    <span data-ttu-id="5350f-133">![Affecter des autorisations pour la racine du compte Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp1.png "Affecter des autorisations pour la racine du compte Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="5350f-133">![Assign permissions for Data Lake Store root](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp1.png "Assign permissions for Data Lake Store root")</span></span>

    <span data-ttu-id="5350f-134">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="5350f-134">Click **OK**.</span></span>

4. <span data-ttu-id="5350f-135">Affecter des autorisations pour le dossier hello sous le compte Data Lake Store où vous souhaitez que les données de toocapture.</span><span class="sxs-lookup"><span data-stu-id="5350f-135">Assign permissions for hello folder under Data Lake Store account where you want toocapture data.</span></span>

    <span data-ttu-id="5350f-136">a.</span><span class="sxs-lookup"><span data-stu-id="5350f-136">a.</span></span> <span data-ttu-id="5350f-137">Cliquez sur **Explorateur de données**, sélectionnez le dossier de hello Bonjour compte Data Lake Store, puis cliquez sur **accès**.</span><span class="sxs-lookup"><span data-stu-id="5350f-137">Click **Data Explorer**, select hello folder in hello Data Lake Store account, and then click **Access**.</span></span>

    <span data-ttu-id="5350f-138">![Affecter des autorisations pour le dossier Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-folder.png "Affecter des autorisations pour le dossier Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="5350f-138">![Assign permissions for Data Lake Store folder](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-folder.png "Assign permissions for Data Lake Store folder")</span></span>

    <span data-ttu-id="5350f-139">b.</span><span class="sxs-lookup"><span data-stu-id="5350f-139">b.</span></span> <span data-ttu-id="5350f-140">Sous **Accès**, cliquez sur **Ajouter**, cliquez sur **Sélectionner un utilisateur ou un groupe**, puis recherchez `Microsoft.EventHubs`.</span><span class="sxs-lookup"><span data-stu-id="5350f-140">Under **Access**, click **Add**, click **Select User or Group**, and then search for `Microsoft.EventHubs`.</span></span> 

    <span data-ttu-id="5350f-141">![Affecter des autorisations pour le dossier Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "Affecter des autorisations pour le dossier Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="5350f-141">![Assign permissions for Data Lake Store folder](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "Assign permissions for Data Lake Store folder")</span></span>
    
    <span data-ttu-id="5350f-142">Cliquez sur **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="5350f-142">Click **Select**.</span></span>

    <span data-ttu-id="5350f-143">c.</span><span class="sxs-lookup"><span data-stu-id="5350f-143">c.</span></span> <span data-ttu-id="5350f-144">Sous **Affecter des autorisations**, cliquez sur **Sélectionner des autorisations**.</span><span class="sxs-lookup"><span data-stu-id="5350f-144">Under **Assign Permissions**, click **Select Permissions**.</span></span> <span data-ttu-id="5350f-145">Définissez **autorisations** trop**lecture, écriture,** et **Execute**.</span><span class="sxs-lookup"><span data-stu-id="5350f-145">Set **Permissions** too**Read, Write,** and **Execute**.</span></span> <span data-ttu-id="5350f-146">Définissez **ajouter à** trop**ce dossier et tous les enfants**.</span><span class="sxs-lookup"><span data-stu-id="5350f-146">Set **Add to** too**This folder and all children**.</span></span> <span data-ttu-id="5350f-147">Enfin, définissez **ajouter en tant que** trop**une entrée d’autorisation accès et une entrée d’autorisation par défaut**.</span><span class="sxs-lookup"><span data-stu-id="5350f-147">Finally, set **Add as** too**An access permission entry and a default permission entry**.</span></span>

    <span data-ttu-id="5350f-148">![Affecter des autorisations pour le dossier Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp-folder.png "Affecter des autorisations pour le dossier Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="5350f-148">![Assign permissions for Data Lake Store folder](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp-folder.png "Assign permissions for Data Lake Store folder")</span></span>
    
    <span data-ttu-id="5350f-149">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="5350f-149">Click **OK**.</span></span> 

## <a name="configure-event-hubs-toocapture-data-toodata-lake-store"></a><span data-ttu-id="5350f-150">Configurer le service Event Hubs toocapture data tooData Lake Store</span><span class="sxs-lookup"><span data-stu-id="5350f-150">Configure Event Hubs toocapture data tooData Lake Store</span></span>

<span data-ttu-id="5350f-151">Dans cette section, vous allez créer un Event Hub dans un espace de noms Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="5350f-151">In this section, you create an Event Hub within an Event Hubs namespace.</span></span> <span data-ttu-id="5350f-152">Vous configurez également hello concentrateur d’événements toocapture données tooan compte Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="5350f-152">You also configure hello Event Hub toocapture data tooan Azure Data Lake Store account.</span></span> <span data-ttu-id="5350f-153">Cette section part du principe que vous avez déjà créé un espace de noms Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="5350f-153">This section assumes that you have already created an Event Hubs namespace.</span></span>

2. <span data-ttu-id="5350f-154">À partir de hello **vue d’ensemble** volet de l’espace de noms hello concentrateurs d’événements, cliquez sur **+ concentrateur d’événements**.</span><span class="sxs-lookup"><span data-stu-id="5350f-154">From hello **Overview** pane of hello Event Hubs namespace, click **+ Event Hub**.</span></span>

    <span data-ttu-id="5350f-155">![Créer un Event Hub](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-event-hub.png "Créer un Event Hub")</span><span class="sxs-lookup"><span data-stu-id="5350f-155">![Create Event Hub](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-event-hub.png "Create Event Hub")</span></span>

3. <span data-ttu-id="5350f-156">Fournissez suivant de hello valeurs tooconfigure toocapture des concentrateurs d’événements data Lake tooData Store.</span><span class="sxs-lookup"><span data-stu-id="5350f-156">Provide hello following values tooconfigure Event Hubs toocapture data tooData Lake Store.</span></span>

    <span data-ttu-id="5350f-157">![Créer un Event Hub](./media/data-lake-store-archive-eventhub-capture/data-lake-store-configure-eventhub.png "Créer un Event Hub")</span><span class="sxs-lookup"><span data-stu-id="5350f-157">![Create Event Hub](./media/data-lake-store-archive-eventhub-capture/data-lake-store-configure-eventhub.png "Create Event Hub")</span></span>

    <span data-ttu-id="5350f-158">a.</span><span class="sxs-lookup"><span data-stu-id="5350f-158">a.</span></span> <span data-ttu-id="5350f-159">Fournissez un nom pour hello concentrateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="5350f-159">Provide a name for hello Event Hub.</span></span>
    
    <span data-ttu-id="5350f-160">b.</span><span class="sxs-lookup"><span data-stu-id="5350f-160">b.</span></span> <span data-ttu-id="5350f-161">Pour ce didacticiel, définissez **nombre de partitions** et **rétention des messages** toohello les valeurs par défaut.</span><span class="sxs-lookup"><span data-stu-id="5350f-161">For this tutorial, set **Partition Count** and **Message Retention** toohello default values.</span></span>
    
    <span data-ttu-id="5350f-162">c.</span><span class="sxs-lookup"><span data-stu-id="5350f-162">c.</span></span> <span data-ttu-id="5350f-163">Définissez **Capture** trop**sur**.</span><span class="sxs-lookup"><span data-stu-id="5350f-163">Set **Capture** too**On**.</span></span> <span data-ttu-id="5350f-164">Ensemble hello **fenêtre de temps** (fréquence toocapture) et **taille de fenêtre** (toocapture de taille de données).</span><span class="sxs-lookup"><span data-stu-id="5350f-164">Set hello **Time Window** (how frequently toocapture) and **Size Window** (data size toocapture).</span></span> 
    
    <span data-ttu-id="5350f-165">d.</span><span class="sxs-lookup"><span data-stu-id="5350f-165">d.</span></span> <span data-ttu-id="5350f-166">Pour **capturer le fournisseur**, sélectionnez **Azure Data Lake Store** et sélectionnez hello hello Data Lake Store que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="5350f-166">For **Capture Provider**, select **Azure Data Lake Store** and hello select hello Data Lake Store you created earlier.</span></span> <span data-ttu-id="5350f-167">Pour **le chemin d’accès de données Lake**, entrez le nom hello du dossier hello créé Bonjour compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="5350f-167">For **Data Lake Path**, enter hello name of hello folder you created in hello Data Lake Store account.</span></span> <span data-ttu-id="5350f-168">Vous devez uniquement le dossier de toohello tooprovide hello chemin d’accès relatif.</span><span class="sxs-lookup"><span data-stu-id="5350f-168">You only need tooprovide hello relative path toohello folder.</span></span>

    <span data-ttu-id="5350f-169">e.</span><span class="sxs-lookup"><span data-stu-id="5350f-169">e.</span></span> <span data-ttu-id="5350f-170">Laissez hello **formats de nom de fichier de capture exemple** toohello par défaut.</span><span class="sxs-lookup"><span data-stu-id="5350f-170">Leave hello **Sample capture file name formats** toohello default value.</span></span> <span data-ttu-id="5350f-171">Cette option détermine la structure de dossiers de hello est créé sous le dossier de capture hello.</span><span class="sxs-lookup"><span data-stu-id="5350f-171">This option governs hello folder structure that is created under hello capture folder.</span></span>

    <span data-ttu-id="5350f-172">f.</span><span class="sxs-lookup"><span data-stu-id="5350f-172">f.</span></span> <span data-ttu-id="5350f-173">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="5350f-173">Click **Create**.</span></span>

## <a name="test-hello-setup"></a><span data-ttu-id="5350f-174">Programme d’installation de test hello</span><span class="sxs-lookup"><span data-stu-id="5350f-174">Test hello setup</span></span>

<span data-ttu-id="5350f-175">Vous pouvez maintenant tester la solution de hello en envoyant des données toohello concentrateur d’événements Azure.</span><span class="sxs-lookup"><span data-stu-id="5350f-175">You can now test hello solution by sending data toohello Azure Event Hub.</span></span> <span data-ttu-id="5350f-176">Suivez les instructions de hello à [envoyer des événements de concentrateurs d’événements tooAzure](../event-hubs/event-hubs-dotnet-framework-getstarted-send.md).</span><span class="sxs-lookup"><span data-stu-id="5350f-176">Follow hello instructions at [Send events tooAzure Event Hubs](../event-hubs/event-hubs-dotnet-framework-getstarted-send.md).</span></span> <span data-ttu-id="5350f-177">Une fois que vous démarrez l’envoi de données de hello, consultez données hello dans Data Lake Store à l’aide de la structure de dossiers hello spécifié.</span><span class="sxs-lookup"><span data-stu-id="5350f-177">Once you start sending hello data, you see hello data reflected in Data Lake Store using hello folder structure you specified.</span></span> <span data-ttu-id="5350f-178">Par exemple, vous voyez une structure de dossiers, comme indiqué dans hello suivant capture d’écran, dans votre Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="5350f-178">For example, you see a folder structure, as shown in hello following screenshot, in your Data Lake Store.</span></span>

<span data-ttu-id="5350f-179">![Exemple de données EventHub dans Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-eventhub-data-sample.png "Exemple de données EventHub dans Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="5350f-179">![Sample EventHub data in Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-eventhub-data-sample.png "Sample EventHub data in Data Lake Store")</span></span>

> [!NOTE]
> <span data-ttu-id="5350f-180">Même si vous n’avez pas les messages entrants dans les concentrateurs d’événements, les concentrateurs d’événements écrit des fichiers vides avec uniquement les en-têtes hello dans hello compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="5350f-180">Even if you do not have messages coming into Event Hubs, Event Hubs writes empty files with just hello headers into hello Data Lake Store account.</span></span> <span data-ttu-id="5350f-181">Hello fichiers sont écrits à hello même intervalle de temps que vous avez fourni lors de la création de concentrateurs d’événements hello.</span><span class="sxs-lookup"><span data-stu-id="5350f-181">hello files are written at hello same time interval that you provided while creating hello Event Hubs.</span></span>
> 
>

## <a name="analyze-data-in-data-lake-store"></a><span data-ttu-id="5350f-182">Analyse des données dans Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="5350f-182">Analyze data in Data Lake Store</span></span>

<span data-ttu-id="5350f-183">Une fois les données de salutation Data Lake Store, vous pouvez exécuter des tâches analytiques tooprocess et faites vos données de hello.</span><span class="sxs-lookup"><span data-stu-id="5350f-183">Once hello data is in Data Lake Store, you can run analytical jobs tooprocess and crunch hello data.</span></span> <span data-ttu-id="5350f-184">Consultez [USQL Avro exemple](https://github.com/Azure/usql/tree/master/Examples/AvroExamples) sur la façon de toodo ce à l’aide d’Analytique de LAC de données Azure.</span><span class="sxs-lookup"><span data-stu-id="5350f-184">See [USQL Avro Example](https://github.com/Azure/usql/tree/master/Examples/AvroExamples) on how toodo this using Azure Data Lake Analytics.</span></span>
  

## <a name="see-also"></a><span data-ttu-id="5350f-185">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="5350f-185">See also</span></span>
* [<span data-ttu-id="5350f-186">Sécuriser les données dans Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="5350f-186">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="5350f-187">Copier des données d’objets BLOB de stockage Azure tooData Lake Store</span><span class="sxs-lookup"><span data-stu-id="5350f-187">Copy data from Azure Storage Blobs tooData Lake Store</span></span>](data-lake-store-copy-data-azure-storage-blob.md)
