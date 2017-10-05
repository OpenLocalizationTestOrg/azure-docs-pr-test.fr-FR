---
title: "Capturer des données Event Hubs dans Azure Data Lake Store | Microsoft Docs"
description: "Utiliser Azure Data Lake Store pour capturer des données Event Hubs"
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
ms.openlocfilehash: a9e69576958ae96d22a4eb03d0df429f0b307298
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-data-lake-store-to-capture-data-from-event-hubs"></a><span data-ttu-id="d6efa-103">Utiliser Azure Data Lake Store pour capturer des données Event Hubs</span><span class="sxs-lookup"><span data-stu-id="d6efa-103">Use Azure Data Lake Store to capture data from Event Hubs</span></span>

<span data-ttu-id="d6efa-104">Découvrez comment utiliser Azure Data Lake Store pour capturer les données reçues par Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="d6efa-104">Learn how to use Azure Data Lake Store to capture data received by Azure Event Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d6efa-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="d6efa-105">Prerequisites</span></span>

* <span data-ttu-id="d6efa-106">**Un abonnement Azure**.</span><span class="sxs-lookup"><span data-stu-id="d6efa-106">**An Azure subscription**.</span></span> <span data-ttu-id="d6efa-107">Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d6efa-107">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="d6efa-108">**Un compte Azure Data Lake Store**.</span><span class="sxs-lookup"><span data-stu-id="d6efa-108">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="d6efa-109">Pour savoir comment en créer un, consultez [Prise en main d’Azure Data Lake Store](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d6efa-109">For instructions on how to create one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md).</span></span>

*  <span data-ttu-id="d6efa-110">**Un espace de noms Event Hubs**.</span><span class="sxs-lookup"><span data-stu-id="d6efa-110">**An Event Hubs namespace**.</span></span> <span data-ttu-id="d6efa-111">Pour obtenir des instructions, consultez [Créer un espace de noms Event Hubs](../event-hubs/event-hubs-create.md#create-an-event-hubs-namespace).</span><span class="sxs-lookup"><span data-stu-id="d6efa-111">For instructions, see [Create an Event Hubs namespace](../event-hubs/event-hubs-create.md#create-an-event-hubs-namespace).</span></span> <span data-ttu-id="d6efa-112">Vérifiez que le compte Data Lake Store et l’espace de noms Event Hubs appartiennent au même abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="d6efa-112">Make sure the Data Lake Store account and the Event Hubs namespace are in the same Azure subscription.</span></span>


## <a name="assign-permissions-to-event-hubs"></a><span data-ttu-id="d6efa-113">Affecter des autorisations à Event Hubs</span><span class="sxs-lookup"><span data-stu-id="d6efa-113">Assign permissions to Event Hubs</span></span>

<span data-ttu-id="d6efa-114">Dans cette section, vous allez créer un dossier au sein du compte dans lequel vous souhaitez capturer les données Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="d6efa-114">In this section, you create a folder within the account where you want to capture the data from Event Hubs.</span></span> <span data-ttu-id="d6efa-115">Vous allez également affecter des autorisations à Event Hubs pour qu’il puisse écrire des données dans un compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="d6efa-115">You also assign permissions to Event Hubs so that it can write data into a Data Lake Store account.</span></span> 

1. <span data-ttu-id="d6efa-116">Ouvrez le compte Data Lake Store dans lequel vous souhaitez capturer les données Event Hubs, puis cliquez sur **Explorateur de données**.</span><span class="sxs-lookup"><span data-stu-id="d6efa-116">Open the Data Lake Store account where you want to capture data from Event Hubs and then click on **Data Explorer**.</span></span>

    <span data-ttu-id="d6efa-117">![Explorateur de données Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-open-data-explorer.png "Explorateur de données Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="d6efa-117">![Data Lake Store data explorer](./media/data-lake-store-archive-eventhub-capture/data-lake-store-open-data-explorer.png "Data Lake Store data explorer")</span></span>

2.  <span data-ttu-id="d6efa-118">Cliquez sur **Nouveau dossier**, puis entrez un nom pour le dossier dans lequel vous souhaitez capturer les données.</span><span class="sxs-lookup"><span data-stu-id="d6efa-118">Click **New Folder** and then enter a name for folder where you want to capture the data.</span></span>

    <span data-ttu-id="d6efa-119">![Créer un dossier dans Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-new-folder.png "Créer un dossier dans Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="d6efa-119">![Create a new folder in Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-new-folder.png "Create a new folder in Data Lake Store")</span></span>

3. <span data-ttu-id="d6efa-120">Affectez des autorisations à la racine du compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="d6efa-120">Assign permissions at the root of the Data Lake Store.</span></span> 

    <span data-ttu-id="d6efa-121">a.</span><span class="sxs-lookup"><span data-stu-id="d6efa-121">a.</span></span> <span data-ttu-id="d6efa-122">Cliquez sur **Explorateur de données**, sélectionnez la racine du compte Data Lake Store, puis cliquez sur **Accès**.</span><span class="sxs-lookup"><span data-stu-id="d6efa-122">Click **Data Explorer**, select the root of the Data Lake Store account, and then click **Access**.</span></span>

    <span data-ttu-id="d6efa-123">![Affecter des autorisations pour la racine du compte Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-root.png "Affecter des autorisations pour la racine du compte Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="d6efa-123">![Assign permissions for Data Lake Store root](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-root.png "Assign permissions for Data Lake Store root")</span></span>

    <span data-ttu-id="d6efa-124">b.</span><span class="sxs-lookup"><span data-stu-id="d6efa-124">b.</span></span> <span data-ttu-id="d6efa-125">Sous **Accès**, cliquez sur **Ajouter**, cliquez sur **Sélectionner un utilisateur ou un groupe**, puis recherchez `Microsoft.EventHubs`.</span><span class="sxs-lookup"><span data-stu-id="d6efa-125">Under **Access**, click **Add**, click **Select User or Group**, and then search for `Microsoft.EventHubs`.</span></span> 

    <span data-ttu-id="d6efa-126">![Affecter des autorisations pour la racine du compte Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "Affecter des autorisations pour la racine du compte Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="d6efa-126">![Assign permissions for Data Lake Store root](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "Assign permissions for Data Lake Store root")</span></span>
    
    <span data-ttu-id="d6efa-127">Cliquez sur **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="d6efa-127">Click **Select**.</span></span>

    <span data-ttu-id="d6efa-128">c.</span><span class="sxs-lookup"><span data-stu-id="d6efa-128">c.</span></span> <span data-ttu-id="d6efa-129">Sous **Affecter des autorisations**, cliquez sur **Sélectionner des autorisations**.</span><span class="sxs-lookup"><span data-stu-id="d6efa-129">Under **Assign Permissions**, click **Select Permissions**.</span></span> <span data-ttu-id="d6efa-130">Définissez **Autorisations** à **Exécuter**.</span><span class="sxs-lookup"><span data-stu-id="d6efa-130">Set **Permissions** to **Execute**.</span></span> <span data-ttu-id="d6efa-131">Définissez **Ajouter à** sur **Ce dossier et tous ses enfants**.</span><span class="sxs-lookup"><span data-stu-id="d6efa-131">Set **Add to** to **This folder and all children**.</span></span> <span data-ttu-id="d6efa-132">Définissez **Ajouter en tant que** sur **Une entrée d’autorisation d’accès et une entrée d’autorisation par défaut**.</span><span class="sxs-lookup"><span data-stu-id="d6efa-132">Set **Add as** to **An access permission entry and a default permission entry**.</span></span>

    <span data-ttu-id="d6efa-133">![Affecter des autorisations pour la racine du compte Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp1.png "Affecter des autorisations pour la racine du compte Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="d6efa-133">![Assign permissions for Data Lake Store root](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp1.png "Assign permissions for Data Lake Store root")</span></span>

    <span data-ttu-id="d6efa-134">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="d6efa-134">Click **OK**.</span></span>

4. <span data-ttu-id="d6efa-135">Affectez des autorisations pour le dossier situé dans le compte Data Lake Store où vous voulez capturer des données.</span><span class="sxs-lookup"><span data-stu-id="d6efa-135">Assign permissions for the folder under Data Lake Store account where you want to capture data.</span></span>

    <span data-ttu-id="d6efa-136">a.</span><span class="sxs-lookup"><span data-stu-id="d6efa-136">a.</span></span> <span data-ttu-id="d6efa-137">Cliquez sur **Explorateur de données**, sélectionnez le dossier du compte Data Lake Store, puis cliquez sur **Accès**.</span><span class="sxs-lookup"><span data-stu-id="d6efa-137">Click **Data Explorer**, select the folder in the Data Lake Store account, and then click **Access**.</span></span>

    <span data-ttu-id="d6efa-138">![Affecter des autorisations pour le dossier Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-folder.png "Affecter des autorisations pour le dossier Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="d6efa-138">![Assign permissions for Data Lake Store folder](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-folder.png "Assign permissions for Data Lake Store folder")</span></span>

    <span data-ttu-id="d6efa-139">b.</span><span class="sxs-lookup"><span data-stu-id="d6efa-139">b.</span></span> <span data-ttu-id="d6efa-140">Sous **Accès**, cliquez sur **Ajouter**, cliquez sur **Sélectionner un utilisateur ou un groupe**, puis recherchez `Microsoft.EventHubs`.</span><span class="sxs-lookup"><span data-stu-id="d6efa-140">Under **Access**, click **Add**, click **Select User or Group**, and then search for `Microsoft.EventHubs`.</span></span> 

    <span data-ttu-id="d6efa-141">![Affecter des autorisations pour le dossier Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "Affecter des autorisations pour le dossier Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="d6efa-141">![Assign permissions for Data Lake Store folder](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "Assign permissions for Data Lake Store folder")</span></span>
    
    <span data-ttu-id="d6efa-142">Cliquez sur **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="d6efa-142">Click **Select**.</span></span>

    <span data-ttu-id="d6efa-143">c.</span><span class="sxs-lookup"><span data-stu-id="d6efa-143">c.</span></span> <span data-ttu-id="d6efa-144">Sous **Affecter des autorisations**, cliquez sur **Sélectionner des autorisations**.</span><span class="sxs-lookup"><span data-stu-id="d6efa-144">Under **Assign Permissions**, click **Select Permissions**.</span></span> <span data-ttu-id="d6efa-145">Définissez **Autorisations** sur **Lecture, écriture** et **exécution**.</span><span class="sxs-lookup"><span data-stu-id="d6efa-145">Set **Permissions** to **Read, Write,** and **Execute**.</span></span> <span data-ttu-id="d6efa-146">Définissez **Ajouter à** sur **Ce dossier et tous ses enfants**.</span><span class="sxs-lookup"><span data-stu-id="d6efa-146">Set **Add to** to **This folder and all children**.</span></span> <span data-ttu-id="d6efa-147">Enfin, définissez **Ajouter en tant que** sur **Une entrée d’autorisation d’accès et une entrée d’autorisation par défaut**.</span><span class="sxs-lookup"><span data-stu-id="d6efa-147">Finally, set **Add as** to **An access permission entry and a default permission entry**.</span></span>

    <span data-ttu-id="d6efa-148">![Affecter des autorisations pour le dossier Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp-folder.png "Affecter des autorisations pour le dossier Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="d6efa-148">![Assign permissions for Data Lake Store folder](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp-folder.png "Assign permissions for Data Lake Store folder")</span></span>
    
    <span data-ttu-id="d6efa-149">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="d6efa-149">Click **OK**.</span></span> 

## <a name="configure-event-hubs-to-capture-data-to-data-lake-store"></a><span data-ttu-id="d6efa-150">Configurer Event Hubs pour capturer des données et les envoyer vers Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="d6efa-150">Configure Event Hubs to capture data to Data Lake Store</span></span>

<span data-ttu-id="d6efa-151">Dans cette section, vous allez créer un Event Hub dans un espace de noms Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="d6efa-151">In this section, you create an Event Hub within an Event Hubs namespace.</span></span> <span data-ttu-id="d6efa-152">Vous allez également configurer l’Event Hub pour capturer des données et les envoyer vers un compte Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="d6efa-152">You also configure the Event Hub to capture data to an Azure Data Lake Store account.</span></span> <span data-ttu-id="d6efa-153">Cette section part du principe que vous avez déjà créé un espace de noms Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="d6efa-153">This section assumes that you have already created an Event Hubs namespace.</span></span>

2. <span data-ttu-id="d6efa-154">Dans le volet **Vue d’ensemble** de l’espace de noms Event Hubs, cliquez sur **+ Event Hub**.</span><span class="sxs-lookup"><span data-stu-id="d6efa-154">From the **Overview** pane of the Event Hubs namespace, click **+ Event Hub**.</span></span>

    <span data-ttu-id="d6efa-155">![Créer un Event Hub](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-event-hub.png "Créer un Event Hub")</span><span class="sxs-lookup"><span data-stu-id="d6efa-155">![Create Event Hub](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-event-hub.png "Create Event Hub")</span></span>

3. <span data-ttu-id="d6efa-156">Fournissez les valeurs suivantes pour configurer Event Hubs de manière à capturer des données et à les envoyer vers Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="d6efa-156">Provide the following values to configure Event Hubs to capture data to Data Lake Store.</span></span>

    <span data-ttu-id="d6efa-157">![Créer un Event Hub](./media/data-lake-store-archive-eventhub-capture/data-lake-store-configure-eventhub.png "Créer un Event Hub")</span><span class="sxs-lookup"><span data-stu-id="d6efa-157">![Create Event Hub](./media/data-lake-store-archive-eventhub-capture/data-lake-store-configure-eventhub.png "Create Event Hub")</span></span>

    <span data-ttu-id="d6efa-158">a.</span><span class="sxs-lookup"><span data-stu-id="d6efa-158">a.</span></span> <span data-ttu-id="d6efa-159">Donnez un nom à l’Event Hub.</span><span class="sxs-lookup"><span data-stu-id="d6efa-159">Provide a name for the Event Hub.</span></span>
    
    <span data-ttu-id="d6efa-160">b.</span><span class="sxs-lookup"><span data-stu-id="d6efa-160">b.</span></span> <span data-ttu-id="d6efa-161">Pour ce didacticiel, définissez **Nombre de partitions** et **Rétention des messages** sur les valeurs par défaut.</span><span class="sxs-lookup"><span data-stu-id="d6efa-161">For this tutorial, set **Partition Count** and **Message Retention** to the default values.</span></span>
    
    <span data-ttu-id="d6efa-162">c.</span><span class="sxs-lookup"><span data-stu-id="d6efa-162">c.</span></span> <span data-ttu-id="d6efa-163">Définissez **Capture** sur **Activé**.</span><span class="sxs-lookup"><span data-stu-id="d6efa-163">Set **Capture** to **On**.</span></span> <span data-ttu-id="d6efa-164">Définissez la **Fenêtre de temps** (fréquence de capture) et la **Fenêtre de taille** (taille des données à capturer).</span><span class="sxs-lookup"><span data-stu-id="d6efa-164">Set the **Time Window** (how frequently to capture) and **Size Window** (data size to capture).</span></span> 
    
    <span data-ttu-id="d6efa-165">d.</span><span class="sxs-lookup"><span data-stu-id="d6efa-165">d.</span></span> <span data-ttu-id="d6efa-166">Pour **Fournisseur de capture**, sélectionnez **Azure Data Lake Store**, puis sélectionnez le Data Lake Store que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="d6efa-166">For **Capture Provider**, select **Azure Data Lake Store** and the select the Data Lake Store you created earlier.</span></span> <span data-ttu-id="d6efa-167">Pour **Chemin Data Lake**, entrez le nom du dossier que vous avez créé dans le compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="d6efa-167">For **Data Lake Path**, enter the name of the folder you created in the Data Lake Store account.</span></span> <span data-ttu-id="d6efa-168">Vous devez uniquement fournir le chemin relatif du dossier.</span><span class="sxs-lookup"><span data-stu-id="d6efa-168">You only need to provide the relative path to the folder.</span></span>

    <span data-ttu-id="d6efa-169">e.</span><span class="sxs-lookup"><span data-stu-id="d6efa-169">e.</span></span> <span data-ttu-id="d6efa-170">Pour l’option **Exemples de formats de nom de fichier de capture**, conservez la valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="d6efa-170">Leave the **Sample capture file name formats** to the default value.</span></span> <span data-ttu-id="d6efa-171">Cette option détermine la structure de dossiers qui est créée sous le dossier de capture.</span><span class="sxs-lookup"><span data-stu-id="d6efa-171">This option governs the folder structure that is created under the capture folder.</span></span>

    <span data-ttu-id="d6efa-172">f.</span><span class="sxs-lookup"><span data-stu-id="d6efa-172">f.</span></span> <span data-ttu-id="d6efa-173">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="d6efa-173">Click **Create**.</span></span>

## <a name="test-the-setup"></a><span data-ttu-id="d6efa-174">Tester la configuration</span><span class="sxs-lookup"><span data-stu-id="d6efa-174">Test the setup</span></span>

<span data-ttu-id="d6efa-175">Vous pouvez maintenant tester la solution en envoyant des données vers Azure Event Hub.</span><span class="sxs-lookup"><span data-stu-id="d6efa-175">You can now test the solution by sending data to the Azure Event Hub.</span></span> <span data-ttu-id="d6efa-176">Suivez les instructions de la rubrique [Envoyer des événements vers les hubs d’événements Azure avec .NET Framework](../event-hubs/event-hubs-dotnet-framework-getstarted-send.md).</span><span class="sxs-lookup"><span data-stu-id="d6efa-176">Follow the instructions at [Send events to Azure Event Hubs](../event-hubs/event-hubs-dotnet-framework-getstarted-send.md).</span></span> <span data-ttu-id="d6efa-177">Une fois que vous démarrez l’envoi des données, vous pouvez voir les données dans Data Lake Store avec la structure de dossiers que vous avez spécifiée.</span><span class="sxs-lookup"><span data-stu-id="d6efa-177">Once you start sending the data, you see the data reflected in Data Lake Store using the folder structure you specified.</span></span> <span data-ttu-id="d6efa-178">Vous pouvez voir une structure de dossiers, telle que celle de la capture d’écran ci-dessous, dans Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="d6efa-178">For example, you see a folder structure, as shown in the following screenshot, in your Data Lake Store.</span></span>

<span data-ttu-id="d6efa-179">![Exemple de données EventHub dans Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-eventhub-data-sample.png "Exemple de données EventHub dans Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="d6efa-179">![Sample EventHub data in Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-eventhub-data-sample.png "Sample EventHub data in Data Lake Store")</span></span>

> [!NOTE]
> <span data-ttu-id="d6efa-180">Même si aucun message n’entre dans Event Hubs, celui-ci écrit des fichiers vides avec en-tête dans le compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="d6efa-180">Even if you do not have messages coming into Event Hubs, Event Hubs writes empty files with just the headers into the Data Lake Store account.</span></span> <span data-ttu-id="d6efa-181">Les fichiers sont écrits au même intervalle de temps que celui que vous avez configuré lors de la création des Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="d6efa-181">The files are written at the same time interval that you provided while creating the Event Hubs.</span></span>
> 
>

## <a name="analyze-data-in-data-lake-store"></a><span data-ttu-id="d6efa-182">Analyse des données dans Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="d6efa-182">Analyze data in Data Lake Store</span></span>

<span data-ttu-id="d6efa-183">Une fois les données dans Data Lake Store, vous pouvez exécuter des tâches analytiques pour traiter et analyser les données.</span><span class="sxs-lookup"><span data-stu-id="d6efa-183">Once the data is in Data Lake Store, you can run analytical jobs to process and crunch the data.</span></span> <span data-ttu-id="d6efa-184">Pour plus d’informations sur cette procédure à l’aide d’Azure Data Lake Analytics, consultez [Exemple Avro USQL](https://github.com/Azure/usql/tree/master/Examples/AvroExamples).</span><span class="sxs-lookup"><span data-stu-id="d6efa-184">See [USQL Avro Example](https://github.com/Azure/usql/tree/master/Examples/AvroExamples) on how to do this using Azure Data Lake Analytics.</span></span>
  

## <a name="see-also"></a><span data-ttu-id="d6efa-185">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="d6efa-185">See also</span></span>
* [<span data-ttu-id="d6efa-186">Sécuriser les données dans Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="d6efa-186">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="d6efa-187">Copier des données d’objets blob Azure Storage vers Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="d6efa-187">Copy data from Azure Storage Blobs to Data Lake Store</span></span>](data-lake-store-copy-data-azure-storage-blob.md)
