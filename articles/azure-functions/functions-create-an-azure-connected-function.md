---
title: "aaaCreate une fonction qui se connecte à des services de tooAzure | Documents Microsoft"
description: Utilisez les fonctions Azure toocreate une application sans serveur qui se connecte tooother Azure services.
services: functions
documentationcenter: dev-center-name
author: yochay
manager: manager-alias
editor: 
tags: 
keywords: "azure functions, fonctions, traitement des événements, webhooks, calcul dynamique, architecture sans serveur"
ms.assetid: ab86065d-6050-46c9-a336-1bfc1fa4b5a1
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/01/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 9d1f7d3b236f8d2c1a404c76aee410f6d458fb7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-functions-toocreate-a-function-that-connects-tooother-azure-services"></a><span data-ttu-id="39cb4-104">Utilisez les fonctions Azure toocreate une fonction qui se connecte tooother Azure services</span><span class="sxs-lookup"><span data-stu-id="39cb4-104">Use Azure Functions toocreate a function that connects tooother Azure services</span></span>

<span data-ttu-id="39cb4-105">Cette rubrique vous montre comment toocreate une fonction dans les fonctions Azure toomessages sur un hello de file d’attente et les copies de stockage Azure est à l’écoute les messages toorows dans une table de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="39cb4-105">This topic shows you how toocreate a function in Azure Functions that listens toomessages on an Azure Storage queue and copies hello messages toorows in an Azure Storage table.</span></span> <span data-ttu-id="39cb4-106">Une fonction de minuteur déclenché est tooload utilisé des messages en file d’attente hello.</span><span class="sxs-lookup"><span data-stu-id="39cb4-106">A timer triggered function is used tooload messages into hello queue.</span></span> <span data-ttu-id="39cb4-107">Une deuxième fonction lit à partir de la file d’attente hello et écrit les messages toohello table.</span><span class="sxs-lookup"><span data-stu-id="39cb4-107">A second function reads from hello queue and writes messages toohello table.</span></span> <span data-ttu-id="39cb4-108">File d’attente hello et table de hello sont créés pour vous par les fonctions Azure basé sur des définitions de liaison hello.</span><span class="sxs-lookup"><span data-stu-id="39cb4-108">Both hello queue and hello table are created for you by Azure Functions based on hello binding definitions.</span></span> 

<span data-ttu-id="39cb4-109">toomake les choses plus intéressants, une fonction est écrit en JavaScript et hello autres est écrit dans le script c#.</span><span class="sxs-lookup"><span data-stu-id="39cb4-109">toomake things more interesting, one function is written in JavaScript and hello other is written in C# script.</span></span> <span data-ttu-id="39cb4-110">Cela montre qu’une Function App peut avoir des fonctions dans différentes langues.</span><span class="sxs-lookup"><span data-stu-id="39cb4-110">This demonstrates how a function app can have functions in various languages.</span></span> 

<span data-ttu-id="39cb4-111">Vous pouvez voir la démonstration de ce scénario dans une [vidéo sur Channel 9](https://channel9.msdn.com/Series/Windows-Azure-Web-Sites-Tutorials/Create-an-Azure-Function-which-binds-to-an-Azure-service/player).</span><span class="sxs-lookup"><span data-stu-id="39cb4-111">You can see this scenario demonstrated in a [video on Channel 9](https://channel9.msdn.com/Series/Windows-Azure-Web-Sites-Tutorials/Create-an-Azure-Function-which-binds-to-an-Azure-service/player).</span></span>

## <a name="create-a-function-that-writes-toohello-queue"></a><span data-ttu-id="39cb4-112">Créez une fonction qui écrit la file d’attente toohello</span><span class="sxs-lookup"><span data-stu-id="39cb4-112">Create a function that writes toohello queue</span></span>

<span data-ttu-id="39cb4-113">Avant de pouvoir vous connecter de la file d’attente de stockage tooa, vous devez toocreate une fonction qui charge la file d’attente de messages hello.</span><span class="sxs-lookup"><span data-stu-id="39cb4-113">Before you can connect tooa storage queue, you need toocreate a function that loads hello message queue.</span></span> <span data-ttu-id="39cb4-114">Cette fonction JavaScript utilise un déclencheur du minuteur qui écrit une file d’attente de message toohello toutes les 10 secondes.</span><span class="sxs-lookup"><span data-stu-id="39cb4-114">This JavaScript function uses a timer trigger that writes a message toohello queue every 10 seconds.</span></span> <span data-ttu-id="39cb4-115">Si vous n’avez pas encore un compte Azure, consultez hello [essayer les fonctions Azure](https://functions.azure.com/try) expérience, ou [créer gratuitement un compte Azure](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="39cb4-115">If you don't already have an Azure account, check out hello [Try Azure Functions](https://functions.azure.com/try) experience, or [create your free Azure account](https://azure.microsoft.com/free/).</span></span>

1. <span data-ttu-id="39cb4-116">Accédez toohello portail Azure et recherchez votre application de la fonction.</span><span class="sxs-lookup"><span data-stu-id="39cb4-116">Go toohello Azure portal and locate your function app.</span></span>

2. <span data-ttu-id="39cb4-117">Cliquez sur **Nouvelle fonction** > **TimerTrigger-JavaScript**.</span><span class="sxs-lookup"><span data-stu-id="39cb4-117">Click **New Function** > **TimerTrigger-JavaScript**.</span></span> 

3. <span data-ttu-id="39cb4-118">Nom de fonction hello **FunctionsBindingsDemo1**, entrez une valeur d’expression cron `0/10 * * * * *` pour **planification**, puis cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="39cb4-118">Name hello function **FunctionsBindingsDemo1**, enter a cron expression value of `0/10 * * * * *` for **Schedule**, and then click **Create**.</span></span>
   
    ![Ajouter une fonction de minuteur déclencheur](./media/functions-create-an-azure-connected-function/new-trigger-timer-function.png)

    <span data-ttu-id="39cb4-120">Vous venez de créer une fonction de minuteur déclencheur qui s’exécute toutes les 10 secondes.</span><span class="sxs-lookup"><span data-stu-id="39cb4-120">You have now created a timer triggered function that runs every 10 seconds.</span></span>

5. <span data-ttu-id="39cb4-121">Sur hello **développer** , cliquez sur **journaux** et afficher les activités de hello dans le journal de hello.</span><span class="sxs-lookup"><span data-stu-id="39cb4-121">On hello **Develop** tab, click **Logs** and view hello activity in hello log.</span></span> <span data-ttu-id="39cb4-122">Les entrées de journal que vous consultez ont été écrites toutes les 10 secondes.</span><span class="sxs-lookup"><span data-stu-id="39cb4-122">You see a log entry written every 10 seconds.</span></span>
   
    ![Fonctionnement de la fonction vue hello journal tooverify hello](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-view-log.png)

## <a name="add-a-message-queue-output-binding"></a><span data-ttu-id="39cb4-124">Ajouter une liaison de sortie de file d’attente de messages</span><span class="sxs-lookup"><span data-stu-id="39cb4-124">Add a message queue output binding</span></span>

1. <span data-ttu-id="39cb4-125">Sur hello **intégrer** , onglet choisir **nouvelle sortie** > **stockage de file d’attente Azure** > **sélectionnez**.</span><span class="sxs-lookup"><span data-stu-id="39cb4-125">On hello **Integrate** tab, choose **New Output** > **Azure Queue Storage** > **Select**.</span></span>

    ![Ajouter une fonction de minuteur déclencheur](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab.png)

2. <span data-ttu-id="39cb4-127">Entrez `myQueueItem` pour **nom de paramètre de Message** et `functions-bindings` pour **nom de la file d’attente**, sélectionnez un existant **connexion au compte de stockage** ou cliquez sur **nouvelle** toocreate un stockage compte de connexion, puis cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="39cb4-127">Enter `myQueueItem` for **Message parameter name** and `functions-bindings` for **Queue name**, select an existing **Storage account connection** or click **new** toocreate a storage account connection, and then click **Save**.</span></span>  

    ![Créer la file d’attente de liaison toohello stockage hello sortie](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab2.png)

1. <span data-ttu-id="39cb4-129">Dans hello **développer** onglet, ajouter hello suivant code toohello fonction :</span><span class="sxs-lookup"><span data-stu-id="39cb4-129">Back in hello **Develop** tab, append hello following code toohello function:</span></span>
   
    ```javascript
   
    function myQueueItem() 
    {
        return {
            msg: "some message goes here",
            time: "time goes here"
        }
    }
   
    ```
2. <span data-ttu-id="39cb4-130">Recherchez hello *si* instruction environ 9 de la fonction hello et de code suivant de hello d’insertion après cette instruction.</span><span class="sxs-lookup"><span data-stu-id="39cb4-130">Locate hello *if* statement around line 9 of hello function, and insert hello following code after that statement.</span></span>
   
    ```javascript
   
    var toBeQed = myQueueItem();
    toBeQed.time = timeStamp;
    context.bindings.myQueueItem = toBeQed;
   
    ```  
   
    <span data-ttu-id="39cb4-131">Ce code crée un **myQueueItem** et définit ses **temps** horodateur actuel toohello de propriété.</span><span class="sxs-lookup"><span data-stu-id="39cb4-131">This code creates a **myQueueItem** and sets its **time** property toohello current timeStamp.</span></span> <span data-ttu-id="39cb4-132">Il ajoute ensuite hello nouvelle file d’attente élément toohello du contexte **myQueueItem** liaison.</span><span class="sxs-lookup"><span data-stu-id="39cb4-132">It then adds hello new queue item toohello context's **myQueueItem** binding.</span></span>

3. <span data-ttu-id="39cb4-133">Cliquez sur **Enregistrer et exécuter**.</span><span class="sxs-lookup"><span data-stu-id="39cb4-133">Click **Save and Run**.</span></span>

## <a name="view-storage-updates-by-using-storage-explorer"></a><span data-ttu-id="39cb4-134">Afficher les mises à jour du stockage à l’aide de l’Explorateur de stockage</span><span class="sxs-lookup"><span data-stu-id="39cb4-134">View storage updates by using Storage Explorer</span></span>
<span data-ttu-id="39cb4-135">Vous pouvez vérifier que votre fonction fonctionne en consultant les messages dans la file d’attente hello que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="39cb4-135">You can verify that your function is working by viewing messages in hello queue you created.</span></span>  <span data-ttu-id="39cb4-136">Vous pouvez connecter la file d’attente de stockage tooyour à l’aide de l’Explorateur de Cloud dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="39cb4-136">You can connect tooyour storage queue by using Cloud Explorer in Visual Studio.</span></span> <span data-ttu-id="39cb4-137">Toutefois, portail de hello rend compte de stockage tooyour tooconnect facile à l’aide de l’Explorateur de stockage Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="39cb4-137">However, hello portal makes it easy tooconnect tooyour storage account by using Microsoft Azure Storage Explorer.</span></span>

1. <span data-ttu-id="39cb4-138">Bonjour **intégrer** , cliquez sur votre file d’attente de liaison de sortie > **Documentation**, afficher hello chaîne de connexion pour votre compte de stockage, puis copiez la valeur de hello.</span><span class="sxs-lookup"><span data-stu-id="39cb4-138">In hello **Integrate** tab, click your queue output binding > **Documentation**, then unhide hello Connection String for your storage account and copy hello value.</span></span> <span data-ttu-id="39cb4-139">Vous utilisez ce compte de stockage de valeur tooconnect tooyour.</span><span class="sxs-lookup"><span data-stu-id="39cb4-139">You use this value tooconnect tooyour storage account.</span></span>

    ![Télécharger l’Explorateur de stockage Azure](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab3.png)


2. <span data-ttu-id="39cb4-141">Si ce n’est déjà fait, téléchargez et installez [l’Explorateur de stockage Microsoft Azure](http://storageexplorer.com).</span><span class="sxs-lookup"><span data-stu-id="39cb4-141">If you haven't already done so, download and install [Microsoft Azure Storage Explorer](http://storageexplorer.com).</span></span> 
 
3. <span data-ttu-id="39cb4-142">Dans l’Explorateur de stockage, cliquez sur hello tooAzure stockage icône de connexion, collez la chaîne de connexion hello dans le champ de hello et terminer l’Assistant de hello.</span><span class="sxs-lookup"><span data-stu-id="39cb4-142">In Storage Explorer, click hello connect tooAzure Storage icon, paste hello connection string in hello field, and complete hello wizard.</span></span>

    ![Explorateur de stockage - Ajout d’une connexion](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-storage-explorer.png)

4. <span data-ttu-id="39cb4-144">Sous **Local et attachées**, développez **comptes de stockage** > votre compte de stockage > **les files d’attente** > **deliaisonsdefonctions**et vérifiez que les messages sont écrits de file d’attente toohello.</span><span class="sxs-lookup"><span data-stu-id="39cb4-144">Under **Local and attached**, expand **Storage Accounts** > your storage account > **Queues** > **functions-bindings** and verify that messages are written toohello queue.</span></span>

    ![Affichage des messages dans la file d’attente hello](./media/functions-create-an-azure-connected-function/functionsbindings-azure-storage-explorer.png)

    <span data-ttu-id="39cb4-146">Si la file d’attente hello n’existe pas ou est vide, il s’agit probablement d’un problème avec votre code ou de liaison de fonction.</span><span class="sxs-lookup"><span data-stu-id="39cb4-146">If hello queue does not exist or is empty, there is most likely a problem with your function binding or code.</span></span>

## <a name="create-a-function-that-reads-from-hello-queue"></a><span data-ttu-id="39cb4-147">Créez une fonction qui lit à partir de la file d’attente hello</span><span class="sxs-lookup"><span data-stu-id="39cb4-147">Create a function that reads from hello queue</span></span>

<span data-ttu-id="39cb4-148">Maintenant que vous avez ajoutés la file d’attente de toohello de messages, vous pouvez créer une autre fonction qui lit à partir de la file d’attente hello et écritures hello messages définitivement table de stockage Azure tooan.</span><span class="sxs-lookup"><span data-stu-id="39cb4-148">Now that you have messages being added toohello queue, you can create another function that reads from hello queue and writes hello messages permanently tooan Azure Storage table.</span></span>

1. <span data-ttu-id="39cb4-149">Cliquez sur **Nouvelle fonction** > **QueueTrigger-CSharp**.</span><span class="sxs-lookup"><span data-stu-id="39cb4-149">Click **New Function** > **QueueTrigger-CSharp**.</span></span> 
 
2. <span data-ttu-id="39cb4-150">Nom de fonction hello `FunctionsBindingsDemo2`, entrez **liaisons de fonctions** Bonjour **nom de la file d’attente** champ, sélectionnez un compte de stockage existant ou créez-en un, puis cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="39cb4-150">Name hello function `FunctionsBindingsDemo2`, enter **functions-bindings** in hello **Queue name** field, select an existing storage account or create one, and then click **Create**.</span></span>

    ![Ajouter une fonction de minuteur de file d’attente de sortie](./media/functions-create-an-azure-connected-function/function-demo2-new-function.png) 

3. <span data-ttu-id="39cb4-152">(Facultatif) Vous pouvez vérifier que la nouvelle fonction de hello fonctionne en consultant la nouvelle file d’attente de hello dans l’Explorateur de stockage comme avant.</span><span class="sxs-lookup"><span data-stu-id="39cb4-152">(Optional) You can verify that hello new function works by viewing hello new queue in Storage Explorer as before.</span></span> <span data-ttu-id="39cb4-153">Vous pouvez également utiliser Cloud Explorer dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="39cb4-153">You can also use Cloud Explorer in Visual Studio.</span></span>  

4. <span data-ttu-id="39cb4-154">(Facultatif) Actualiser hello **liaisons de fonctions** file d’attente et notez que les éléments ont été supprimés de la file d’attente hello.</span><span class="sxs-lookup"><span data-stu-id="39cb4-154">(Optional) Refresh hello **functions-bindings** queue and notice that items have been removed from hello queue.</span></span> <span data-ttu-id="39cb4-155">Hello suppression se produit, car la fonction hello est lié toohello **liaisons de fonctions** comme une fonction d’entrée de déclencheur et hello lit la file d’attente hello en file d’attente.</span><span class="sxs-lookup"><span data-stu-id="39cb4-155">hello removal occurs because hello function is bound toohello **functions-bindings** queue as an input trigger and hello function reads hello queue.</span></span> 
 
## <a name="add-a-table-output-binding"></a><span data-ttu-id="39cb4-156">Ajouter une liaison de sortie de table</span><span class="sxs-lookup"><span data-stu-id="39cb4-156">Add a table output binding</span></span>

1. <span data-ttu-id="39cb4-157">Dans FunctionsBindingsDemo2, cliquez sur **Intégrer** > **Nouvelle sortie** > **Table de stockage Azure** > **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="39cb4-157">In FunctionsBindingsDemo2, click **Integrate** > **New Output** > **Azure Table Storage** > **Select**.</span></span>

    ![Ajouter une table de stockage Azure tooan liaison](./media/functions-create-an-azure-connected-function/functionsbindingsdemo2-integrate-tab.png) 

2. <span data-ttu-id="39cb4-159">Entrez `functionbindings` pour **Nom de la table** et `myTable` pour **Nom du paramètre de table**, choisissez une **Connexion du compte de stockage** ou créez-en une, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="39cb4-159">Enter `functionbindings` for **Table name** and `myTable` for **Table parameter name**, choose a **Storage account connection** or create a new one, and then click **Save**.</span></span>

    ![Configurer la liaison de table de stockage hello](./media/functions-create-an-azure-connected-function/functionsbindingsdemo2-integrate-tab2.png)
   
3. <span data-ttu-id="39cb4-161">Bonjour **développer** onglet, remplacez le code existant de la fonction hello par qui suit hello :</span><span class="sxs-lookup"><span data-stu-id="39cb4-161">In hello **Develop** tab, replace hello existing function code with hello following:</span></span>
   
    ```cs
    
    using System;
    
    public static void Run(QItem myQueueItem, ICollector<TableItem> myTable, TraceWriter log)
    {    
        TableItem myItem = new TableItem
        {
            PartitionKey = "key",
            RowKey = Guid.NewGuid().ToString(),
            Time = DateTime.Now.ToString("hh.mm.ss.ffffff"),
            Msg = myQueueItem.Msg,
            OriginalTime = myQueueItem.Time    
        };
        
        // Add hello item toohello table binding collection.
        myTable.Add(myItem);
    
        log.Verbose($"C# Queue trigger function processed: {myItem.RowKey} | {myItem.Msg} | {myItem.Time}");
    }
    
    public class TableItem
    {
        public string PartitionKey {get; set;}
        public string RowKey {get; set;}
        public string Time {get; set;}
        public string Msg {get; set;}
        public string OriginalTime {get; set;}
    }
    
    public class QItem
    {
        public string Msg { get; set;}
        public string Time { get; set;}
    }
    ```
    <span data-ttu-id="39cb4-162">Hello **TableItem** classe représente une ligne dans la table de stockage hello, et vous ajoutez hello élément toohello `myTable` collection de **TableItem** objets.</span><span class="sxs-lookup"><span data-stu-id="39cb4-162">hello **TableItem** class represents a row in hello storage table, and you add hello item toohello `myTable` collection of **TableItem** objects.</span></span> <span data-ttu-id="39cb4-163">Vous devez définir hello **PartitionKey** et **RowKey** tooinsert en mesure de propriétés toobe dans la table de hello.</span><span class="sxs-lookup"><span data-stu-id="39cb4-163">You must set hello **PartitionKey** and **RowKey** properties toobe able tooinsert into hello table.</span></span>

4. <span data-ttu-id="39cb4-164">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="39cb4-164">Click **Save**.</span></span>  <span data-ttu-id="39cb4-165">Enfin, vous pouvez vérifier le fonctionnement de la fonction hello en consultant la table de hello dans l’Explorateur de stockage ou de Visual Studio Cloud Explorer.</span><span class="sxs-lookup"><span data-stu-id="39cb4-165">Finally, you can verify hello function works by viewing hello table in Storage explorer or Visual Studio Cloud Explorer.</span></span>

5. <span data-ttu-id="39cb4-166">(Facultatif) Dans votre compte de stockage dans l’Explorateur de stockage, développez **Tables** > **functionsbindings** et vérifiez que les lignes sont ajoutées toohello table.</span><span class="sxs-lookup"><span data-stu-id="39cb4-166">(Optional) In your storage account in Storage Explorer, expand **Tables** > **functionsbindings** and verify that rows are added toohello table.</span></span> <span data-ttu-id="39cb4-167">Vous pouvez effectuer même hello dans Cloud Explorer dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="39cb4-167">You can do hello same in Cloud Explorer in Visual Studio.</span></span>

    ![Affichage des lignes de table de hello](./media/functions-create-an-azure-connected-function/functionsbindings-azure-storage-explorer2.png)

    <span data-ttu-id="39cb4-169">Si la table de hello n’existe pas ou est vide, il s’agit probablement d’un problème avec votre code ou de liaison de fonction.</span><span class="sxs-lookup"><span data-stu-id="39cb4-169">If hello table does not exist or is empty, there is most likely a problem with your function binding or code.</span></span> 
 
[!INCLUDE [More binding information](../../includes/functions-bindings-next-steps.md)]

## <a name="next-steps"></a><span data-ttu-id="39cb4-170">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="39cb4-170">Next steps</span></span>
<span data-ttu-id="39cb4-171">Pour plus d’informations sur les fonctions d’Azure, consultez hello rubriques suivantes :</span><span class="sxs-lookup"><span data-stu-id="39cb4-171">For more information about Azure Functions, see hello following topics:</span></span>

* [<span data-ttu-id="39cb4-172">Référence du développeur Azure Functions</span><span class="sxs-lookup"><span data-stu-id="39cb4-172">Azure Functions developer reference</span></span>](functions-reference.md)  
  <span data-ttu-id="39cb4-173">Référence du programmeur pour le codage de fonctions et la définition de déclencheurs et de liaisons.</span><span class="sxs-lookup"><span data-stu-id="39cb4-173">Programmer reference for coding functions and defining triggers and bindings.</span></span>
* [<span data-ttu-id="39cb4-174">Test d’Azure Functions</span><span class="sxs-lookup"><span data-stu-id="39cb4-174">Testing Azure Functions</span></span>](functions-test-a-function.md)  
  <span data-ttu-id="39cb4-175">décrit plusieurs outils et techniques permettant de tester vos fonctions.</span><span class="sxs-lookup"><span data-stu-id="39cb4-175">Describes various tools and techniques for testing your functions.</span></span>
* [<span data-ttu-id="39cb4-176">Comment tooscale les fonctions Azure</span><span class="sxs-lookup"><span data-stu-id="39cb4-176">How tooscale Azure Functions</span></span>](functions-scale.md)  
  <span data-ttu-id="39cb4-177">Décrit des plans de service disponibles avec les fonctions d’Azure, y compris le plan d’hébergement hello consommation, et comment toochoose hello adaptée.</span><span class="sxs-lookup"><span data-stu-id="39cb4-177">Discusses service plans available with Azure Functions, including hello Consumption hosting plan, and how toochoose hello right plan.</span></span> 

[!INCLUDE [Getting help note](../../includes/functions-get-help.md)]

