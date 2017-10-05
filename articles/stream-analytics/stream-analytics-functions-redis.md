---
title: "Traitement en temps réel Stream Analytics pour Azure Functions | Microsoft Docs"
description: "Découvrez comment utiliser une fonction Azure connectée à une file d’attente Service Bus pour remplir un cache Redis Azure à partir de la sortie d’une tâche Stream Analytics."
keywords: "flux de données, cache redis, file d’attente Service Bus"
services: stream-analytics
author: ryancrawcour
manager: jhubbard
documentationcenter: 
ms.assetid: d428bb33-4244-4001-b93d-c77bed816527
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/28/2017
ms.author: ryancraw
ms.openlocfilehash: ad14cc858ff513573e2718a26a9ab5c524e1adc6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-store-data-from-azure-stream-analytics-in-an-azure-redis-cache-using-azure-functions"></a><span data-ttu-id="7a1a6-104">Comment stocker des données Azure Stream Analytics dans un Cache Redis Azure à l’aide d’Azure Functions</span><span class="sxs-lookup"><span data-stu-id="7a1a6-104">How to store data from Azure Stream Analytics in an Azure Redis Cache using Azure Functions</span></span>
<span data-ttu-id="7a1a6-105">Azure Stream Analytics permet de développer et de déployer rapidement des solutions à faible coût pour obtenir des informations en temps réel à partir d’appareils, de capteurs, d’infrastructures et d’applications, ou de tout flux de données.</span><span class="sxs-lookup"><span data-stu-id="7a1a6-105">Azure Stream Analytics lets you rapidly develop and deploy low-cost solutions to gain real-time insights from devices, sensors, infrastructure, and applications, or any stream of data.</span></span> <span data-ttu-id="7a1a6-106">Il permet de déployer différents cas d’utilisation, notamment la gestion en temps réel, la commande et le contrôle, la détection des fraudes, les voitures connectées et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="7a1a6-106">It enables various use cases such as real-time management and monitoring, command and control, fraud detection, connected cars and many more.</span></span> <span data-ttu-id="7a1a6-107">Dans de nombreux scénarios de ce type, vous souhaiterez peut-être stocker des données de sorties d’Azure Stream Analytics dans un magasin de données distribué tel que le cache Redis Azure.</span><span class="sxs-lookup"><span data-stu-id="7a1a6-107">In many such scenarios, you may want to store data outputted by Azure Stream Analytics into a distributed data store such as an Azure Redis cache.</span></span>

<span data-ttu-id="7a1a6-108">Supposons que vous faites partie d’une société de télécommunications.</span><span class="sxs-lookup"><span data-stu-id="7a1a6-108">Suppose you are part of a telecommunications company.</span></span> <span data-ttu-id="7a1a6-109">Vous essayez de détecter une fraude sur une carte SIM qui reçoit plusieurs appels provenant de la même identité, au même moment, mais depuis des emplacements géographiques différents.</span><span class="sxs-lookup"><span data-stu-id="7a1a6-109">You are trying to detect SIM fraud where multiple calls coming from the same identity, at the same time, but in different geographically locations.</span></span> <span data-ttu-id="7a1a6-110">Vous êtes chargé de stocker tous les appels téléphoniques potentiellement frauduleux dans un cache Redis Azure.</span><span class="sxs-lookup"><span data-stu-id="7a1a6-110">You are tasked with storing all the potential fraudulent phone calls in an Azure Redis cache.</span></span> <span data-ttu-id="7a1a6-111">Dans ce blog, nous donnons des conseils sur la manière dont vous pouvez facilement réaliser cette tâche.</span><span class="sxs-lookup"><span data-stu-id="7a1a6-111">In this blog, we provide guidance on how you can easily complete your task.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="7a1a6-112">Composants requis</span><span class="sxs-lookup"><span data-stu-id="7a1a6-112">Prerequisites</span></span>
<span data-ttu-id="7a1a6-113">Exécutez la procédure pas à pas de [détection des fraudes en temps réel][fraud-detection] pour ASA</span><span class="sxs-lookup"><span data-stu-id="7a1a6-113">Complete the [Real-time Fraud Detection][fraud-detection] walk-through for ASA</span></span>

## <a name="architecture-overview"></a><span data-ttu-id="7a1a6-114">Présentation de l'architecture</span><span class="sxs-lookup"><span data-stu-id="7a1a6-114">Architecture Overview</span></span>
![Capture d’écran de l’architecture](./media/stream-analytics-functions-redis/architecture-overview.png)

<span data-ttu-id="7a1a6-116">Comme indiqué dans la figure précédente, Stream Analytics permet d’interroger des flux de données d’entrée et de les envoyer vers une sortie.</span><span class="sxs-lookup"><span data-stu-id="7a1a6-116">As shown in the preceding figure, Stream Analytics allows streaming input data to be queried and sent to an output.</span></span> <span data-ttu-id="7a1a6-117">En fonction de la sortie, Azure Functions peut ensuite déclencher certains types d’événement.</span><span class="sxs-lookup"><span data-stu-id="7a1a6-117">Based on the output, Azure Functions can then trigger some type of event.</span></span> 

<span data-ttu-id="7a1a6-118">Dans ce blog, nous nous concentrons sur la partie Azure Functions de ce pipeline, ou plus précisément sur le déclenchement d’un événement qui stocke les données frauduleuses dans le cache.</span><span class="sxs-lookup"><span data-stu-id="7a1a6-118">In this blog, we focus on the Azure Functions part of this pipeline, or more specifically the triggering of an event that stores fraudulent data into the cache.</span></span>
<span data-ttu-id="7a1a6-119">Une fois le didacticiel [Détection des fraudes en temps réel][fraud-detection] exécuté, vous disposez d’une entrée (un event hub), d’une requête et d’une sortie (stockage d’objets blob) déjà configurées et exécutées.</span><span class="sxs-lookup"><span data-stu-id="7a1a6-119">After completing the [Real-time Fraud Detection][fraud-detection] tutorial, you have an input (an event hub), a query, and an output (blob storage) already configured and running.</span></span> <span data-ttu-id="7a1a6-120">Dans ce blog, nous modifions la sortie pour utiliser une file d’attente Service Bus à la place.</span><span class="sxs-lookup"><span data-stu-id="7a1a6-120">In this blog, we change the output to use a Service Bus Queue instead.</span></span> <span data-ttu-id="7a1a6-121">Après cela, nous connectons une fonction Azure à cette file d’attente.</span><span class="sxs-lookup"><span data-stu-id="7a1a6-121">After that, we connect an Azure Function to this queue.</span></span> 

## <a name="create-and-connect-a-service-bus-queue-output"></a><span data-ttu-id="7a1a6-122">Création et connexion d’une sortie de la file d’attente Service Bus</span><span class="sxs-lookup"><span data-stu-id="7a1a6-122">Create and connect a Service Bus Queue output</span></span>
<span data-ttu-id="7a1a6-123">Pour créer une file d’attente Service Bus, suivez les étapes 1 et 2 de la section .NET de la rubrique [Prise en main des files d’attente Service Bus][servicebus-getstarted].</span><span class="sxs-lookup"><span data-stu-id="7a1a6-123">To create a Service Bus Queue, follow steps 1 and 2 of the .NET section in [Get Started with Service Bus Queues][servicebus-getstarted].</span></span>
<span data-ttu-id="7a1a6-124">Nous allons maintenant connecter la file d’attente à la tâche Stream Analytics qui a été créée dans la procédure de détection de fraude exécutée précédemment.</span><span class="sxs-lookup"><span data-stu-id="7a1a6-124">Now let's connect the queue to the Stream Analytics job that was created in the earlier fraud detection walk-through.</span></span>

1. <span data-ttu-id="7a1a6-125">Dans le portail Azure, accédez au panneau **Sorties** de votre tâche, puis sélectionnez **Ajouter** en haut de la page.</span><span class="sxs-lookup"><span data-stu-id="7a1a6-125">In the Azure portal, go to the **Outputs** blade of your job and select **Add** at the top of the page.</span></span>
   
    ![Ajout de sorties](./media/stream-analytics-functions-redis/adding-outputs.png)
2. <span data-ttu-id="7a1a6-127">Choisissez **File d’attente Service Bus** comme **Récepteur** et suivez les instructions à l’écran.</span><span class="sxs-lookup"><span data-stu-id="7a1a6-127">Choose **Service Bus Queue** as the **Sink** and follow the instructions on the screen.</span></span> <span data-ttu-id="7a1a6-128">Veillez à choisir l’espace de noms de la file d’attente Service Bus que vous avez créé dans le cadre de la [Prise en main des files d’attente Service Bus][servicebus-getstarted].</span><span class="sxs-lookup"><span data-stu-id="7a1a6-128">Be sure to choose the namespace of the Service Bus Queue you created in [Get Started with Service Bus Queues][servicebus-getstarted].</span></span> <span data-ttu-id="7a1a6-129">Cliquez sur le bouton « Droite » lorsque vous avez terminé.</span><span class="sxs-lookup"><span data-stu-id="7a1a6-129">Click the "right" button when you are finished.</span></span>
3. <span data-ttu-id="7a1a6-130">Spécifiez les valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="7a1a6-130">Specify the following values:</span></span>
   
   * <span data-ttu-id="7a1a6-131">**Format du sérialiseur d'événement**: JSON</span><span class="sxs-lookup"><span data-stu-id="7a1a6-131">**Event Serializer Format**: JSON</span></span>
   * <span data-ttu-id="7a1a6-132">**Encodage**: UTF8</span><span class="sxs-lookup"><span data-stu-id="7a1a6-132">**Encoding**: UTF8</span></span>
   * <span data-ttu-id="7a1a6-133">**FORMAT**: séparé par une ligne</span><span class="sxs-lookup"><span data-stu-id="7a1a6-133">**FORMAT**: Line separated</span></span>
4. <span data-ttu-id="7a1a6-134">Cliquez sur le bouton **Créer** pour ajouter cette source et vérifier que Stream Analytics peut se connecter au compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="7a1a6-134">Click the **Create** button to add this source and to verify that Stream Analytics can successfully connect to the storage account.</span></span>
5. <span data-ttu-id="7a1a6-135">Dans l’onglet **Requête** , remplacez la requête en cours par l’élément suivant.</span><span class="sxs-lookup"><span data-stu-id="7a1a6-135">In the **Query** tab, replace the current query with the following.</span></span> <span data-ttu-id="7a1a6-136">Remplacez *[VOTRE NOM DE SERVICE BUS] * par le nom de sortie que vous avez créé à l’étape 3.</span><span class="sxs-lookup"><span data-stu-id="7a1a6-136">Replace *[YOUR SERVICE BUS NAME] * with the output name you created in step 3.</span></span> 
   
    ```    
   
        SELECT 
            System.Timestamp as Time, CS1.CallingIMSI, CS1.CallingNum as CallingNum1, 
            CS2.CallingNum as CallingNum2, CS1.SwitchNum as Switch1, CS2.SwitchNum as Switch2
   
        INTO [YOUR SERVICE BUS NAME]
   
        FROM CallStream CS1 TIMESTAMP BY CallRecTime
        JOIN CallStream CS2 TIMESTAMP BY CallRecTime
            ON CS1.CallingIMSI = CS2.CallingIMSI AND DATEDIFF(ss, CS1, CS2) BETWEEN 1 AND 5
   
        WHERE CS1.SwitchNum != CS2.SwitchNum
   
    ```

## <a name="create-an-azure-redis-cache"></a><span data-ttu-id="7a1a6-137">Création d'un cache Redis Azure</span><span class="sxs-lookup"><span data-stu-id="7a1a6-137">Create an Azure Redis Cache</span></span>
<span data-ttu-id="7a1a6-138">Créez un cache Redis Azure en suivant la section .NET de la rubrique [Utilisation du cache Redis Azure][use-rediscache] jusqu’à la section ***Configuration des clients du cache***.</span><span class="sxs-lookup"><span data-stu-id="7a1a6-138">Create an Azure Redis cache by following the .NET section in [How to Use Azure Redis Cache][use-rediscache] until the section called ***Configure the cache clients***.</span></span>
<span data-ttu-id="7a1a6-139">Une fois que vous avez terminé, vous disposez d’un nouveau cache Redis.</span><span class="sxs-lookup"><span data-stu-id="7a1a6-139">Once complete, you have a new Redis Cache.</span></span> <span data-ttu-id="7a1a6-140">Sous **Tous les paramètres**, sélectionnez **Clés d’accès** et notez la ***Chaîne de connexion principale***.</span><span class="sxs-lookup"><span data-stu-id="7a1a6-140">Under **All settings**, select **Access keys** and note down the ***Primary connection string***.</span></span>

![Capture d’écran de l’architecture](./media/stream-analytics-functions-redis/redis-cache-keys.png)

## <a name="create-an-azure-function"></a><span data-ttu-id="7a1a6-142">Création d’une fonction Azure</span><span class="sxs-lookup"><span data-stu-id="7a1a6-142">Create an Azure Function</span></span>
<span data-ttu-id="7a1a6-143">Suivez le didacticiel [Créer votre première fonction Azure][functions-getstarted] pour vous familiariser avec Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="7a1a6-143">Follow [Create your first Azure Function][functions-getstarted] tutorial to get started with Azure Functions.</span></span> <span data-ttu-id="7a1a6-144">Si vous disposez déjà d’une fonction Azure que vous souhaitez utiliser, passez à [Écriture dans le cache Redis](#Writing-to-Redis-Cache)</span><span class="sxs-lookup"><span data-stu-id="7a1a6-144">If you already have an Azure function you would like to use, then skip ahead to [Writing to Redis Cache](#Writing-to-Redis-Cache)</span></span>

1. <span data-ttu-id="7a1a6-145">Dans le portail, sélectionnez App Services dans le volet de navigation gauche, puis cliquez sur le nom de votre application de fonction Azure pour accéder au site Web de l’application de fonction.</span><span class="sxs-lookup"><span data-stu-id="7a1a6-145">In the portal, select App Services from the left-hand navigation, then click your Azure function app name to get to the Function's app website.</span></span>
    <span data-ttu-id="7a1a6-146">![Capture d’écran de la liste des applications App Services](./media/stream-analytics-functions-redis/app-services-function-list.png)</span><span class="sxs-lookup"><span data-stu-id="7a1a6-146">![Screenshot of app services function list](./media/stream-analytics-functions-redis/app-services-function-list.png)</span></span>
2. <span data-ttu-id="7a1a6-147">Cliquez sur **Nouvelle fonction > ServiceBusQueueTrigger – C#**.</span><span class="sxs-lookup"><span data-stu-id="7a1a6-147">Click **New Function > ServiceBusQueueTrigger – C#**.</span></span> <span data-ttu-id="7a1a6-148">Pour les champs suivants, suivez les instructions ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="7a1a6-148">For the following fields, follow these instructions:</span></span>
   
   * <span data-ttu-id="7a1a6-149">**Nom de la file d’attente** : le même nom que le nom que vous avez entré lorsque vous avez créé la file d’attente dans [Prise en main des files d’attente Service Bus][servicebus-getstarted] (pas le nom du service bus).</span><span class="sxs-lookup"><span data-stu-id="7a1a6-149">**Queue name**: The same name as the name you entered when you created the queue in [Get Started with Service Bus Queues][servicebus-getstarted] (not the name of the service bus).</span></span> <span data-ttu-id="7a1a6-150">Vérifiez que vous utilisez la file d’attente qui est connectée à la sortie Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="7a1a6-150">Make sure you use the queue that is connected to the Stream Analytics output.</span></span>
   * <span data-ttu-id="7a1a6-151">**Connexion Service Bus** : sélectionnez **Ajouter une chaîne de connexion**.</span><span class="sxs-lookup"><span data-stu-id="7a1a6-151">**Service Bus connection**: Select **Add a connection string**.</span></span> <span data-ttu-id="7a1a6-152">Pour rechercher la chaîne de connexion, accédez au portail Classic, sélectionnez **Service Bus**, le bus de service que vous avez créé, et **INFORMATIONS DE CONNEXION** en bas de l’écran.</span><span class="sxs-lookup"><span data-stu-id="7a1a6-152">To find the connection string, go to the classic portal, select **Service Bus**, the service bus you created, and **CONNECTION INFORMATION** at the bottom of the screen.</span></span> <span data-ttu-id="7a1a6-153">Assurez-vous que vous êtes dans l’écran principal de cette page.</span><span class="sxs-lookup"><span data-stu-id="7a1a6-153">Make sure you are on the main screen on this page.</span></span> <span data-ttu-id="7a1a6-154">Copiez et collez la chaîne de connexion.</span><span class="sxs-lookup"><span data-stu-id="7a1a6-154">Copy and paste the connection string.</span></span> <span data-ttu-id="7a1a6-155">N’hésitez pas à entrer un nom de connexion.</span><span class="sxs-lookup"><span data-stu-id="7a1a6-155">Feel free to enter any connection name.</span></span>
     
       ![Capture d’écran de la connexion Service Bus](./media/stream-analytics-functions-redis/servicebus-connection.png)
   * <span data-ttu-id="7a1a6-157">**AccessRights** : choisissez **Gérer**</span><span class="sxs-lookup"><span data-stu-id="7a1a6-157">**AccessRights**: Choose **Manage**</span></span>
3. <span data-ttu-id="7a1a6-158">Cliquez sur **Créer**</span><span class="sxs-lookup"><span data-stu-id="7a1a6-158">Click **Create**</span></span>

## <a name="writing-to-redis-cache"></a><span data-ttu-id="7a1a6-159">Écriture dans le cache Redis</span><span class="sxs-lookup"><span data-stu-id="7a1a6-159">Writing to Redis Cache</span></span>
<span data-ttu-id="7a1a6-160">Nous avons maintenant créé une fonction Azure qui lit à partir d’une file d’attente Service Bus.</span><span class="sxs-lookup"><span data-stu-id="7a1a6-160">We have now created an Azure Function that reads from a Service Bus Queue.</span></span> <span data-ttu-id="7a1a6-161">Tout ce qui reste à faire est d’utiliser notre fonction pour écrire ces données dans le cache Redis.</span><span class="sxs-lookup"><span data-stu-id="7a1a6-161">All that is left to do is use our Function to write this data to the Redis Cache.</span></span> 

1. <span data-ttu-id="7a1a6-162">Sélectionnez votre **ServiceBusQueueTrigger** nouvellement créé, puis cliquez sur **Paramètres Function App** dans le coin supérieur droit.</span><span class="sxs-lookup"><span data-stu-id="7a1a6-162">Select your newly created **ServiceBusQueueTrigger**, and click **Function app settings** on the top right corner.</span></span> <span data-ttu-id="7a1a6-163">Sélectionnez **Accédez aux paramètres App Service > Paramètres > Paramètres de l’application**</span><span class="sxs-lookup"><span data-stu-id="7a1a6-163">Select **Go to App Service Settings > Settings > Application settings**</span></span>
2. <span data-ttu-id="7a1a6-164">Dans la section Chaînes de connexion, spécifiez un nom dans la section **Nom** .</span><span class="sxs-lookup"><span data-stu-id="7a1a6-164">In the Connection strings section, create a name in the **Name** section.</span></span> <span data-ttu-id="7a1a6-165">Collez la chaîne de connexion principale que vous avez trouvée à l’étape **Création d’un cache Redis** dans la section **Valeur**.</span><span class="sxs-lookup"><span data-stu-id="7a1a6-165">Paste the primary connection string you found in the **Create a Redis Cache** step into the **Value** section.</span></span> <span data-ttu-id="7a1a6-166">Sélectionnez **Personnalisé** pour la **Base de données SQL**.</span><span class="sxs-lookup"><span data-stu-id="7a1a6-166">Select **Custom** where it says **SQL Database**.</span></span>
3. <span data-ttu-id="7a1a6-167">Cliquez sur **Enregistrer** en haut.</span><span class="sxs-lookup"><span data-stu-id="7a1a6-167">Click **Save** at the top.</span></span>
   
    ![Capture d’écran de la connexion Service Bus](./media/stream-analytics-functions-redis/function-connection-string.png)
4. <span data-ttu-id="7a1a6-169">Revenez aux paramètres App Service et sélectionnez **Outils > Éditeur App Service (Préversion) > Activé > Accéder**.</span><span class="sxs-lookup"><span data-stu-id="7a1a6-169">Now go back to the App Service Settings and select **Tools > App Service Editor (Preview) > On > Go**.</span></span>
   
    ![Capture d’écran de la connexion Service Bus](./media/stream-analytics-functions-redis/app-service-editor.png)
5. <span data-ttu-id="7a1a6-171">Dans un éditeur de votre choix, créez un fichier JSON nommé **project.json** avec les éléments suivants et enregistrez-le sur votre disque local.</span><span class="sxs-lookup"><span data-stu-id="7a1a6-171">In an editor of your choice, create a JSON file named **project.json** with the following and save it to your local disk.</span></span>
   
        {
            "frameworks": {
                "net46": {
                    "dependencies": {
                        "StackExchange.Redis":"1.1.603",
                        "Newtonsoft.Json": "9.0.1"
                    }
                }
            }
        }
6. <span data-ttu-id="7a1a6-172">Chargez ce fichier dans le répertoire racine de votre fonction (pas WWWROOT).</span><span class="sxs-lookup"><span data-stu-id="7a1a6-172">Upload this file into the root directory of your function (not WWWROOT).</span></span> <span data-ttu-id="7a1a6-173">Vous devriez voir un fichier nommé **project.lock.json** s’afficher automatiquement qui confirme que les packages Nuget « StackExchange.Redis » et « Newtonsoft.Json » ont été importés.</span><span class="sxs-lookup"><span data-stu-id="7a1a6-173">You should see a file named **project.lock.json** automatically appear, confirming that the Nuget packages “StackExchange.Redis” and “Newtonsoft.Json” have been imported.</span></span>
7. <span data-ttu-id="7a1a6-174">Dans le fichier **run.csx** , remplacez le code préalablement généré par le code suivant.</span><span class="sxs-lookup"><span data-stu-id="7a1a6-174">In the **run.csx** file, replace the pre-generated code with the following code.</span></span> <span data-ttu-id="7a1a6-175">Dans la fonction lazyConnection, remplacez « CONN NAME » par le nom que vous avez créé à l’étape 2 de **Stocker des données dans le cache Redis**.</span><span class="sxs-lookup"><span data-stu-id="7a1a6-175">In the lazyConnection function, replace “CONN NAME” with the name you created in step 2 of **Store data into the Redis cache**.</span></span>

````

    using System;
    using System.Threading.Tasks;
    using StackExchange.Redis;
    using Newtonsoft.Json;
    using System.Configuration;

    public static void Run(string myQueueItem, TraceWriter log)
    {
        log.Info($"Function processed message: {myQueueItem}");

        // Connection refers to a property that returns a ConnectionMultiplexer
        IDatabase db = Connection.GetDatabase();
        log.Info($"Created database {db}");

        // Parse JSON and extract the time
        var message = JsonConvert.DeserializeObject<dynamic>(myQueueItem);
        string time = message.time;
        string callingnum1 = message.callingnum1;

        // Perform cache operations using the cache object...
        // Simple put of integral data types into the cache
        string key = time + " - " + callingnum1;
        db.StringSet(key, myQueueItem);
        log.Info($"Object put in database. Key is {key} and value is {myQueueItem}");

        // Simple get of data types from the cache
        string value = db.StringGet(key);
        log.Info($"Database got: {value}"); 
    }

    // Connect to the Service Bus
    private static Lazy<ConnectionMultiplexer> lazyConnection = 
        new Lazy<ConnectionMultiplexer>(() =>
            {
                var cnn = ConfigurationManager.ConnectionStrings["CONN NAME"].ConnectionString
                return ConnectionMultiplexer.Connect();
            });

    public static ConnectionMultiplexer Connection
    {
        get
        {
            return lazyConnection.Value;
        }
    }

````

## <a name="start-the-stream-analytics-job"></a><span data-ttu-id="7a1a6-176">Démarrage de la tâche Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="7a1a6-176">Start the Stream Analytics job</span></span>
1. <span data-ttu-id="7a1a6-177">Démarrez l’application telcodatagen.exe.</span><span class="sxs-lookup"><span data-stu-id="7a1a6-177">Start the telcodatagen.exe application.</span></span> <span data-ttu-id="7a1a6-178">Procédez comme suit : ````telcodatagen.exe [#NumCDRsPerHour] [SIM Card Fraud Probability] [#DurationHours]````</span><span class="sxs-lookup"><span data-stu-id="7a1a6-178">The usage is as follows: ````telcodatagen.exe [#NumCDRsPerHour] [SIM Card Fraud Probability] [#DurationHours]````</span></span>
2. <span data-ttu-id="7a1a6-179">Dans le panneau Tâche Stream Analytics du portail, cliquez sur **Démarrer** en haut de la page.</span><span class="sxs-lookup"><span data-stu-id="7a1a6-179">From the Stream Analytics Job blade in the portal, click **Start** at the top of the page.</span></span>
   
    ![Capture d’écran de la tâche de démarrage](./media/stream-analytics-functions-redis/starting-job.png)
3. <span data-ttu-id="7a1a6-181">Dans le panneau **Démarrer la tâche** qui s’affiche, sélectionnez **Maintenant**, puis cliquez sur le bouton **Démarrer** au bas de l’écran.</span><span class="sxs-lookup"><span data-stu-id="7a1a6-181">In the **Start job** blade that appears, select **Now** and then click the **Start** button at the bottom of the screen.</span></span> <span data-ttu-id="7a1a6-182">L’état de la tâche passe à Démarrage, puis à Exécution après quelques instants.</span><span class="sxs-lookup"><span data-stu-id="7a1a6-182">The job status changes to Starting and after some time changes to Running.</span></span>
   
    ![Capture d’écran de la sélection de l’heure de la tâche de démarrage](./media/stream-analytics-functions-redis/start-job-time.png)

## <a name="run-solution-and-check-results"></a><span data-ttu-id="7a1a6-184">Exécution de la solution et vérification des résultats</span><span class="sxs-lookup"><span data-stu-id="7a1a6-184">Run solution and check results</span></span>
<span data-ttu-id="7a1a6-185">En revenant à votre page **ServiceBusQueueTrigger** , vous devez maintenant voir les instructions de journaux.</span><span class="sxs-lookup"><span data-stu-id="7a1a6-185">Going back to your **ServiceBusQueueTrigger** page, you should now see log statements.</span></span> <span data-ttu-id="7a1a6-186">Ces journaux indiquent que vous avez copié quelque chose de la file d’attente Service Bus dans la base de données et que vous l’avez récupéré sur la base de l’heure !</span><span class="sxs-lookup"><span data-stu-id="7a1a6-186">These logs show that you got something from the Service Bus Queue, put it into the database, and fetched it out using the time as the key!</span></span>

<span data-ttu-id="7a1a6-187">Pour vérifier que vos données se trouvent dans votre cache Redis, accédez à votre page Cache Redis dans le nouveau portail (comme indiqué à l’étape précédente [Création d’un cache Redis Azure](#Create-an-Azure-Redis-Cache) ), puis sélectionnez Console.</span><span class="sxs-lookup"><span data-stu-id="7a1a6-187">To verify that your data is in your Redis cache, go to your Redis cache page in the new portal (as shown in the preceding [Create an Azure Redis Cache](#Create-an-Azure-Redis-Cache) step) and select Console.</span></span>

<span data-ttu-id="7a1a6-188">Vous pouvez maintenant écrire des commandes Redis pour confirmer que les données se trouvent vraiment dans le cache.</span><span class="sxs-lookup"><span data-stu-id="7a1a6-188">Now you can write Redis commands to confirm that data is in fact in the cache.</span></span>

![Capture d’écran de la console Redis](./media/stream-analytics-functions-redis/redis-console.png)

## <a name="next-steps"></a><span data-ttu-id="7a1a6-190">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7a1a6-190">Next steps</span></span>
<span data-ttu-id="7a1a6-191">Nous sommes heureux de ce que la combinaison d’Azure Functions et de Stream Analytics permet de réaliser, et nous espérons que vous pourrez y trouver de nouvelles opportunités.</span><span class="sxs-lookup"><span data-stu-id="7a1a6-191">We’re excited about the new things Azure Functions and Stream analytics can do together, and we hope this unlocks new possibilities for you.</span></span> <span data-ttu-id="7a1a6-192">Si vous avez des commentaires sur la manière dont nous devons faire évoluer nos produits, n’hésitez pas à utiliser le [site Azure UserVoice](https://feedback.azure.com/forums/270577-stream-analytics).</span><span class="sxs-lookup"><span data-stu-id="7a1a6-192">If you have any feedback on what you want next, feel free to use the [Azure UserVoice site](https://feedback.azure.com/forums/270577-stream-analytics).</span></span>

<span data-ttu-id="7a1a6-193">Si vous ne connaissez pas encore Microsoft Azure, nous vous invitons à le découvrir en vous connectant à un [compte d’évaluation Azure gratuit](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7a1a6-193">If you are new Microsoft Azure, we invite you to try it out by signing up for a [free Azure trial account](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="7a1a6-194">Si vous ne connaissez pas encore Stream Analytics, nous vous invitons à [créer votre première tâche Stream Analytics](stream-analytics-create-a-job.md).</span><span class="sxs-lookup"><span data-stu-id="7a1a6-194">If you are new to Stream Analytics, then we invite you to [create your first Stream Analytics job](stream-analytics-create-a-job.md).</span></span>

<span data-ttu-id="7a1a6-195">Si vous avez besoin d’aide ou avez des questions, postez-les sur les forums [MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics) ou [Stackoverflow](http://stackoverflow.com/questions/tagged/azure-stream-analytics).</span><span class="sxs-lookup"><span data-stu-id="7a1a6-195">If you need any help or have questions, post on [MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics) or [Stackoverflow](http://stackoverflow.com/questions/tagged/azure-stream-analytics) forums.</span></span> 

<span data-ttu-id="7a1a6-196">Vous pouvez également vous référer aux ressources suivantes :</span><span class="sxs-lookup"><span data-stu-id="7a1a6-196">You can also see the following resources:</span></span>

* [<span data-ttu-id="7a1a6-197">Informations de référence pour les développeurs sur Azure Functions</span><span class="sxs-lookup"><span data-stu-id="7a1a6-197">Azure Functions developer reference</span></span>](../azure-functions/functions-reference.md)
* [<span data-ttu-id="7a1a6-198">Informations de référence pour les développeurs C# sur Azure Functions</span><span class="sxs-lookup"><span data-stu-id="7a1a6-198">Azure Functions C# developer reference</span></span>](../azure-functions/functions-reference-csharp.md)
* [<span data-ttu-id="7a1a6-199">Informations de référence pour les développeurs F# sur Azure Functions</span><span class="sxs-lookup"><span data-stu-id="7a1a6-199">Azure Functions F# developer reference</span></span>](../azure-functions/functions-reference-fsharp.md)
* [<span data-ttu-id="7a1a6-200">Azure Functions NodeJS developer reference (Référence pour les développeurs NodeJS Azure Functions)</span><span class="sxs-lookup"><span data-stu-id="7a1a6-200">Azure Functions NodeJS developer reference</span></span>](../azure-functions/functions-reference.md)
* [<span data-ttu-id="7a1a6-201">Déclencheurs et liaisons Azure Functions</span><span class="sxs-lookup"><span data-stu-id="7a1a6-201">Azure Functions triggers and bindings</span></span>](../azure-functions/functions-triggers-bindings.md)
* [<span data-ttu-id="7a1a6-202">Surveillance du cache Redis Azure</span><span class="sxs-lookup"><span data-stu-id="7a1a6-202">How to monitor Azure Redis Cache</span></span>](../redis-cache/cache-how-to-monitor.md)

<span data-ttu-id="7a1a6-203">Pour vous tenir informé des dernières nouveautés et fonctionnalités, suivez [@AzureStreaming](https://twitter.com/AzureStreaming) sur Twitter.</span><span class="sxs-lookup"><span data-stu-id="7a1a6-203">To stay up-to-date on all the latest news and features, follow [@AzureStreaming](https://twitter.com/AzureStreaming) on Twitter.</span></span>

[fraud-detection]: stream-analytics-real-time-fraud-detection.md
[servicebus-getstarted]: ../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md
[use-rediscache]: ../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md
[functions-getstarted]: ../azure-functions/functions-create-first-azure-function.md
