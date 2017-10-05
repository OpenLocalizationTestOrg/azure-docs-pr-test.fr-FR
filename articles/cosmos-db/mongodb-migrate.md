---
title: "Utiliser mongoimport et mongorestore avec l’API Azure Cosmos DB pour MongoDB | Microsoft Docs"
description: "Découvrez comment utiliser mongoimport et mongorestore pour importer des données dans un compte API pour MongoDB"
keywords: mongoimport, mongorestore
services: cosmos-db
author: AndrewHoh
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: 352c5fb9-8772-4c5f-87ac-74885e63ecac
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/12/2017
ms.author: anhoh
ms.custom: mvc
ms.openlocfilehash: 1555f13c3ea88b61be0ea240b51218b83f6f9724
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-cosmos-db-import-mongodb-data"></a><span data-ttu-id="d6e22-104">Azure Cosmos DB : importer des données MongoDB</span><span class="sxs-lookup"><span data-stu-id="d6e22-104">Azure Cosmos DB: Import MongoDB data</span></span> 

<span data-ttu-id="d6e22-105">Pour migrer des données de MongoDB vers un compte Azure Cosmos DB en vue d’une utilisation avec l’API pour MongoDB, vous devez :</span><span class="sxs-lookup"><span data-stu-id="d6e22-105">To migrate data from MongoDB to an Azure Cosmos DB account for use with the API for MongoDB, you must:</span></span>

* <span data-ttu-id="d6e22-106">télécharger *mongoimport.exe* ou *mongorestore.exe* depuis le [centre de téléchargement MongoDB](https://www.mongodb.com/download-center) ;</span><span class="sxs-lookup"><span data-stu-id="d6e22-106">Download either *mongoimport.exe* or *mongorestore.exe* from the [MongoDB Download Center](https://www.mongodb.com/download-center).</span></span>
* <span data-ttu-id="d6e22-107">Obtenir votre [API pour la chaîne de connexion MongoDB](connect-mongodb-account.md).</span><span class="sxs-lookup"><span data-stu-id="d6e22-107">Get your [API for MongoDB connection string](connect-mongodb-account.md).</span></span>

<span data-ttu-id="d6e22-108">Si vous importez des données à partir de MongoDB et planifiez de les utiliser avec Azure Cosmos DB, vous devez avoir recours à [l’outil de migration de données](import-data.md) pour importer les données.</span><span class="sxs-lookup"><span data-stu-id="d6e22-108">If you are importing data from MongoDB and plan to use it with the Azure Cosmos DB, you should use the [Data Migration tool](import-data.md) to import data.</span></span>

<span data-ttu-id="d6e22-109">Ce didacticiel décrit les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="d6e22-109">This tutorial covers the following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d6e22-110">Récupération de votre chaîne de connexion</span><span class="sxs-lookup"><span data-stu-id="d6e22-110">Retrieving your connection string</span></span>
> * <span data-ttu-id="d6e22-111">Importation des données MongoDB à l’aide de mongoimport</span><span class="sxs-lookup"><span data-stu-id="d6e22-111">Importing MongoDB data by using mongoimport</span></span>
> * <span data-ttu-id="d6e22-112">Importation des données MongoDB à l’aide de mongorestore</span><span class="sxs-lookup"><span data-stu-id="d6e22-112">Importing MongoDB data by using mongorestore</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d6e22-113">Composants requis</span><span class="sxs-lookup"><span data-stu-id="d6e22-113">Prerequisites</span></span>

* <span data-ttu-id="d6e22-114">Augmentez le débit : la durée de la migration des données dépend de la quantité de débit que vous définissez pour vos collections.</span><span class="sxs-lookup"><span data-stu-id="d6e22-114">Increase throughput: The duration of your data migration depends on the amount of throughput you set up for your collections.</span></span> <span data-ttu-id="d6e22-115">Veillez à augmenter le débit pour les migrations de données plus importantes.</span><span class="sxs-lookup"><span data-stu-id="d6e22-115">Be sure to increase the throughput for larger data migrations.</span></span> <span data-ttu-id="d6e22-116">Une fois que vous avez effectué la migration, diminuez le débit pour réduire les coûts.</span><span class="sxs-lookup"><span data-stu-id="d6e22-116">After you've completed the migration, decrease the throughput to save costs.</span></span> <span data-ttu-id="d6e22-117">Pour plus d’informations sur l’augmentation du débit dans le [portail Azure](https://portal.azure.com), consultez les [niveaux de performances et niveaux tarifaires dans Azure Cosmos DB](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="d6e22-117">For more information about increasing throughput in the [Azure portal](https://portal.azure.com), see [Performance levels and pricing tiers in Azure Cosmos DB](performance-levels.md).</span></span>

* <span data-ttu-id="d6e22-118">Activez SSL : Azure Cosmos DB obéit à des normes et à des exigences strictes en matière de sécurité.</span><span class="sxs-lookup"><span data-stu-id="d6e22-118">Enable SSL: Azure Cosmos DB has strict security requirements and standards.</span></span> <span data-ttu-id="d6e22-119">Veillez à activer SSL lorsque vous interagissez avec votre compte.</span><span class="sxs-lookup"><span data-stu-id="d6e22-119">Be sure to enable SSL when you interact with your account.</span></span> <span data-ttu-id="d6e22-120">Les procédures décrites dans la suite de cet article incluent l’activation du protocole SSL pour mongoimport et mongorestore.</span><span class="sxs-lookup"><span data-stu-id="d6e22-120">The procedures in the rest of the article include how to enable SSL for mongoimport and mongorestore.</span></span>

## <a name="find-your-connection-string-information-host-port-username-and-password"></a><span data-ttu-id="d6e22-121">Recherche des informations de votre chaîne de connexion (hôte, port, nom d’utilisateur et mot de passe)</span><span class="sxs-lookup"><span data-stu-id="d6e22-121">Find your connection string information (host, port, username, and password)</span></span>

1. <span data-ttu-id="d6e22-122">Dans le volet de gauche du [portail Azure](https://portal.azure.com), cliquez sur l’entrée **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="d6e22-122">In the [Azure portal](https://portal.azure.com), in the left pane, click the **Azure Cosmos DB** entry.</span></span>
2. <span data-ttu-id="d6e22-123">Dans le volet **Abonnements**, sélectionnez le nom de votre compte.</span><span class="sxs-lookup"><span data-stu-id="d6e22-123">In the **Subscriptions** pane, select your account name.</span></span>
3. <span data-ttu-id="d6e22-124">Dans le panneau **Chaîne de connexion**, cliquez sur **Chaîne de connexion**.</span><span class="sxs-lookup"><span data-stu-id="d6e22-124">In the **Connection String** blade, click **Connection String**.</span></span>  
<span data-ttu-id="d6e22-125">Le volet droit contient toutes les informations dont vous avez besoin pour vous connecter à votre compte.</span><span class="sxs-lookup"><span data-stu-id="d6e22-125">The right pane contains all the information that you need to successfully connect to your account.</span></span>

    ![Panneau Chaîne de connexion](./media/mongodb-migrate/ConnectionStringBlade.png)

## <a name="import-data-to-the-api-for-mongodb-by-using-mongoimport"></a><span data-ttu-id="d6e22-127">Importer des données dans l’API pour MongoDB avec mongoimport</span><span class="sxs-lookup"><span data-stu-id="d6e22-127">Import data to the API for MongoDB by using mongoimport</span></span>

<span data-ttu-id="d6e22-128">Pour importer des données dans votre compte Azure Cosmos DB, utilisez le modèle suivant.</span><span class="sxs-lookup"><span data-stu-id="d6e22-128">To import data to your Azure Cosmos DB account, use the following template.</span></span> <span data-ttu-id="d6e22-129">Renseignez *l’hôte*, *le nom d’utilisateur*, et *le mot de passe* avec les valeurs qui sont spécifiques à votre compte.</span><span class="sxs-lookup"><span data-stu-id="d6e22-129">Fill in *host*, *username*, and *password* with the values that are specific to your account.</span></span>  

<span data-ttu-id="d6e22-130">Modèle :</span><span class="sxs-lookup"><span data-stu-id="d6e22-130">Template:</span></span>

    mongoimport.exe --host <your_hostname>:10255 -u <your_username> -p <your_password> --db <your_database> --collection <your_collection> --ssl --sslAllowInvalidCertificates --type json --file C:\sample.json

<span data-ttu-id="d6e22-131">Exemple :</span><span class="sxs-lookup"><span data-stu-id="d6e22-131">Example:</span></span>  

    mongoimport.exe --host anhoh-host.documents.azure.com:10255 -u anhoh-host -p tkvaVkp4Nnaoirnouenrgisuner2435qwefBH0z256Na24frio34LNQasfaefarfernoimczciqisAXw== --ssl --sslAllowInvalidCertificates --db sampleDB --collection sampleColl --type json --file C:\Users\anhoh\Desktop\*.json

## <a name="import-data-to-the-api-for-mongodb-by-using-mongorestore"></a><span data-ttu-id="d6e22-132">Importer des données dans l’API pour MongoDB avec mongorestore</span><span class="sxs-lookup"><span data-stu-id="d6e22-132">Import data to the API for MongoDB by using mongorestore</span></span>

<span data-ttu-id="d6e22-133">Pour restaurer des données dans votre API pour compte MongoDB, utilisez le modèle suivant afin d’exécuter l’importation.</span><span class="sxs-lookup"><span data-stu-id="d6e22-133">To restore data to your API for MongoDB account, use the following template to execute the import.</span></span> <span data-ttu-id="d6e22-134">Renseignez *l’hôte*, *le nom d’utilisateur*, et *le mot de passe* avec les valeurs qui sont spécifiques à votre compte.</span><span class="sxs-lookup"><span data-stu-id="d6e22-134">Fill in *host*, *username*, and *password* with the values that are specific to your account.</span></span>

<span data-ttu-id="d6e22-135">Modèle :</span><span class="sxs-lookup"><span data-stu-id="d6e22-135">Template:</span></span>

    mongorestore.exe --host <your_hostname>:10255 -u <your_username> -p <your_password> --db <your_database> --collection <your_collection> --ssl --sslAllowInvalidCertificates <path_to_backup>

<span data-ttu-id="d6e22-136">Exemple :</span><span class="sxs-lookup"><span data-stu-id="d6e22-136">Example:</span></span>

    mongorestore.exe --host anhoh-host.documents.azure.com:10255 -u anhoh-host -p tkvaVkp4Nnaoirnouenrgisuner2435qwefBH0z256Na24frio34LNQasfaefarfernoimczciqisAXw== --ssl --sslAllowInvalidCertificates ./dumps/dump-2016-12-07
    
## <a name="guide-for-a-successful-migration"></a><span data-ttu-id="d6e22-137">Guide pour une migration réussie</span><span class="sxs-lookup"><span data-stu-id="d6e22-137">Guide for a successful migration</span></span>

1. <span data-ttu-id="d6e22-138">Créez au préalable vos collections et mettez-les à l’échelle :</span><span class="sxs-lookup"><span data-stu-id="d6e22-138">Pre-create and scale your collections:</span></span>
        
    * <span data-ttu-id="d6e22-139">Par défaut, Azure Cosmos DB approvisionne une nouvelle collection MongoDB avec 1 000 unités de requête (RU).</span><span class="sxs-lookup"><span data-stu-id="d6e22-139">By default, Azure Cosmos DB provisions a new MongoDB collection with 1,000 request units (RUs).</span></span> <span data-ttu-id="d6e22-140">Avant de commencer la migration à l’aide de mongoimport, mongorestore ou mongomirror, créez au préalable l’ensemble des collections à partir du [portail Azure](https://portal.azure.com) ou à partir d’outils et de pilotes MongoDB.</span><span class="sxs-lookup"><span data-stu-id="d6e22-140">Before you start the migration by using mongoimport, mongorestore, or mongomirror, pre-create all your collections from the [Azure portal](https://portal.azure.com) or from MongoDB drivers and tools.</span></span> <span data-ttu-id="d6e22-141">Si la taille de votre collection est supérieure à 10 Go, veillez à créer une [collection partitionnée](partition-data.md) avec une clé de partition appropriée.</span><span class="sxs-lookup"><span data-stu-id="d6e22-141">If your collection is greater than 10 GB, make sure to create a [sharded/partitioned collection](partition-data.md) with an appropriate shard key.</span></span>

    * <span data-ttu-id="d6e22-142">Dans le [portail Azure](https://portal.azure.com), augmentez le débit de vos collections à partir de 1 000 RU pour une collection à partition unique et de 2 500 RU pour une collection partitionnée uniquement pour la migration.</span><span class="sxs-lookup"><span data-stu-id="d6e22-142">From the [Azure portal](https://portal.azure.com), increase your collections' throughput from 1,000 RUs for a single partition collection and 2,500 RUs for a sharded collection just for the migration.</span></span> <span data-ttu-id="d6e22-143">Si le débit est plus élevé, vous pouvez éviter la limitation et procéder à une migration plus rapide.</span><span class="sxs-lookup"><span data-stu-id="d6e22-143">With the higher throughput, you can avoid throttling and migrate in less time.</span></span> <span data-ttu-id="d6e22-144">Avec une facturation à l’heure dans Azure Cosmos DB, vous pouvez réduire immédiatement le débit à l’issue de la migration afin de réduire les coûts.</span><span class="sxs-lookup"><span data-stu-id="d6e22-144">With hourly billing in Azure Cosmos DB, you can reduce the throughput immediately after the migration to save costs.</span></span>

2. <span data-ttu-id="d6e22-145">Calculez les frais approximatifs d’unités de requête pour une écriture de document unique :</span><span class="sxs-lookup"><span data-stu-id="d6e22-145">Calculate the approximate RU charge for a single document write:</span></span>

    <span data-ttu-id="d6e22-146">a.</span><span class="sxs-lookup"><span data-stu-id="d6e22-146">a.</span></span> <span data-ttu-id="d6e22-147">Connectez-vous à votre base de données Azure Cosmos DB MongoDB à partir de l’interpréteur de commandes MongoDB.</span><span class="sxs-lookup"><span data-stu-id="d6e22-147">Connect to your Azure Cosmos DB MongoDB database from the MongoDB Shell.</span></span> <span data-ttu-id="d6e22-148">Pour plus d’informations, voir [Connecter une application MongoDB à Azure Cosmos DB](connect-mongodb-account.md).</span><span class="sxs-lookup"><span data-stu-id="d6e22-148">You can find instructions in [Connect a MongoDB application to Azure Cosmos DB](connect-mongodb-account.md).</span></span>
    
    <span data-ttu-id="d6e22-149">b.</span><span class="sxs-lookup"><span data-stu-id="d6e22-149">b.</span></span> <span data-ttu-id="d6e22-150">Exécutez un exemple de commande d’insertion en utilisant l’un des exemples de documents de l’interpréteur de commandes MongoDB :</span><span class="sxs-lookup"><span data-stu-id="d6e22-150">Run a sample insert command by using one of your sample documents from the MongoDB Shell:</span></span>
    
        ```db.coll.insert({ "playerId": "a067ff", "hashedid": "bb0091", "countryCode": "hk" })```
        
    <span data-ttu-id="d6e22-151">c.</span><span class="sxs-lookup"><span data-stu-id="d6e22-151">c.</span></span> <span data-ttu-id="d6e22-152">Exécutez ```db.runCommand({getLastRequestStatistics: 1})```. Vous recevez une réponse semblable à celle-ci :</span><span class="sxs-lookup"><span data-stu-id="d6e22-152">Run ```db.runCommand({getLastRequestStatistics: 1})``` and you will receive a response like this one:</span></span>
     
        ```
        globaldb:PRIMARY> db.runCommand({getLastRequestStatistics: 1})
        {
            "_t": "GetRequestStatisticsResponse",
            "ok": 1,
            "CommandName": "insert",
            "RequestCharge": 10,
            "RequestDurationInMilliSeconds": NumberLong(50)
        }
        ```
        
    <span data-ttu-id="d6e22-153">d.</span><span class="sxs-lookup"><span data-stu-id="d6e22-153">d.</span></span> <span data-ttu-id="d6e22-154">Prenez note de frais de requête.</span><span class="sxs-lookup"><span data-stu-id="d6e22-154">Take note of the request charge.</span></span>
    
3. <span data-ttu-id="d6e22-155">Déterminez la latence de votre machine au service cloud Azure Cosmos DB :</span><span class="sxs-lookup"><span data-stu-id="d6e22-155">Determine the latency from your machine to the Azure Cosmos DB cloud service:</span></span>
    
    <span data-ttu-id="d6e22-156">a.</span><span class="sxs-lookup"><span data-stu-id="d6e22-156">a.</span></span> <span data-ttu-id="d6e22-157">Activez la journalisation détaillée à partir de l’interpréteur de commandes MongoDB à l’aide de cette commande : ```setVerboseShell(true)```</span><span class="sxs-lookup"><span data-stu-id="d6e22-157">Enable verbose logging from the MongoDB Shell by using this command: ```setVerboseShell(true)```</span></span>
    
    <span data-ttu-id="d6e22-158">b.</span><span class="sxs-lookup"><span data-stu-id="d6e22-158">b.</span></span> <span data-ttu-id="d6e22-159">Exécutez une requête simple dans la base de données : ```db.coll.find().limit(1)```.</span><span class="sxs-lookup"><span data-stu-id="d6e22-159">Run a simple query against the database: ```db.coll.find().limit(1)```.</span></span> <span data-ttu-id="d6e22-160">Vous recevez une réponse semblable à celle-ci :</span><span class="sxs-lookup"><span data-stu-id="d6e22-160">You will receive a response like this one:</span></span>

        ```
        Fetched 1 record(s) in 100(ms)
        ```
        
4. <span data-ttu-id="d6e22-161">Supprimez le document inséré avant la migration pour vous assurer de l’absence de documents en double.</span><span class="sxs-lookup"><span data-stu-id="d6e22-161">Remove the inserted document before the migration to ensure that there are no duplicate documents.</span></span> <span data-ttu-id="d6e22-162">Vous pouvez supprimer des documents à l’aide de cette commande : ```db.coll.remove({})```</span><span class="sxs-lookup"><span data-stu-id="d6e22-162">You can remove documents by using this command: ```db.coll.remove({})```</span></span>

5. <span data-ttu-id="d6e22-163">Calculez les valeurs *batchSize* et *numInsertionWorkers* approximatives :</span><span class="sxs-lookup"><span data-stu-id="d6e22-163">Calculate the approximate *batchSize* and *numInsertionWorkers* values:</span></span>

    * <span data-ttu-id="d6e22-164">Pour la valeur *batchSize*, divisez le total des unités RU approvisionnées par les unités RU consommées par l’écriture de votre document unique à l’étape 3.</span><span class="sxs-lookup"><span data-stu-id="d6e22-164">For *batchSize*, divide the total provisioned RUs by the RUs consumed from your single document write in step 3.</span></span>
    
    * <span data-ttu-id="d6e22-165">Si la valeur *batchSize* calculée est inférieure ou égale à 24, utilisez-la comme valeur *batchSize*.</span><span class="sxs-lookup"><span data-stu-id="d6e22-165">If the calculated *batchSize* <= 24, use that number as your *batchSize* value.</span></span>
    
    * <span data-ttu-id="d6e22-166">Si la valeur *batchSize* calculée est supérieure à 24, définissez la valeur *batchSize* sur 24.</span><span class="sxs-lookup"><span data-stu-id="d6e22-166">If the calculated *batchSize* > 24, set the *batchSize* value to 24.</span></span>
    
    * <span data-ttu-id="d6e22-167">Pour *numInsertionWorkers*, utilisez l’équation suivante : *numInsertionWorkers = (débit approvisionné * latence en secondes) / (taille du lot * RU consommées pour une seule écriture)*.</span><span class="sxs-lookup"><span data-stu-id="d6e22-167">For *numInsertionWorkers*, use this equation:   *numInsertionWorkers =  (provisioned throughput * latency in seconds) / (batch size * consumed RUs for a single write)*.</span></span>
        
    |<span data-ttu-id="d6e22-168">Propriété</span><span class="sxs-lookup"><span data-stu-id="d6e22-168">Property</span></span>|<span data-ttu-id="d6e22-169">Valeur</span><span class="sxs-lookup"><span data-stu-id="d6e22-169">Value</span></span>|
    |--------|-----|
    |<span data-ttu-id="d6e22-170">batchSize</span><span class="sxs-lookup"><span data-stu-id="d6e22-170">batchSize</span></span>| <span data-ttu-id="d6e22-171">24</span><span class="sxs-lookup"><span data-stu-id="d6e22-171">24</span></span> |
    |<span data-ttu-id="d6e22-172">RU approvisionnées</span><span class="sxs-lookup"><span data-stu-id="d6e22-172">RUs provisioned</span></span> | <span data-ttu-id="d6e22-173">10000</span><span class="sxs-lookup"><span data-stu-id="d6e22-173">10000</span></span> |
    |<span data-ttu-id="d6e22-174">Latence</span><span class="sxs-lookup"><span data-stu-id="d6e22-174">Latency</span></span> | <span data-ttu-id="d6e22-175">0,100 s</span><span class="sxs-lookup"><span data-stu-id="d6e22-175">0.100 s</span></span> |
    |<span data-ttu-id="d6e22-176">RU facturée pour 1 écriture de document</span><span class="sxs-lookup"><span data-stu-id="d6e22-176">RU charged for 1 doc write</span></span> | <span data-ttu-id="d6e22-177">10 unités de requête</span><span class="sxs-lookup"><span data-stu-id="d6e22-177">10 RUs</span></span> |
    |<span data-ttu-id="d6e22-178">numInsertionWorkers</span><span class="sxs-lookup"><span data-stu-id="d6e22-178">numInsertionWorkers</span></span> | <span data-ttu-id="d6e22-179">?</span><span class="sxs-lookup"><span data-stu-id="d6e22-179">?</span></span> |
    
    <span data-ttu-id="d6e22-180">*numInsertionWorkers = (10 000 RU x 0,1 s) / (24 x 10 RU) = 4,1666*</span><span class="sxs-lookup"><span data-stu-id="d6e22-180">*numInsertionWorkers = (10000 RUs x 0.1 s) / (24 x 10 RUs) = 4.1666*</span></span>

6. <span data-ttu-id="d6e22-181">Exécutez la commande de migration finale :</span><span class="sxs-lookup"><span data-stu-id="d6e22-181">Run the final migration command:</span></span>

   ```
   mongoimport.exe --host anhoh-mongodb.documents.azure.com:10255 -u anhoh-mongodb -p wzRJCyjtLPNuhm53yTwaefawuiefhbauwebhfuabweifbiauweb2YVdl2ZFNZNv8IU89LqFVm5U0bw== --ssl --sslAllowInvalidCertificates --jsonArray --db dabasename --collection collectionName --file "C:\sample.json" --numInsertionWorkers 4 --batchSize 24
   ```

## <a name="next-steps"></a><span data-ttu-id="d6e22-182">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d6e22-182">Next steps</span></span>

<span data-ttu-id="d6e22-183">Vous pouvez passer au didacticiel suivant et découvrir comment interroger les données MongoDB à l’aide d’Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d6e22-183">You can proceed to the next tutorial and learn how to query MongoDB data by using Azure Cosmos DB.</span></span> 

> [!div class="nextstepaction"]
>[<span data-ttu-id="d6e22-184">Comment interroger les données MongoDB ?</span><span class="sxs-lookup"><span data-stu-id="d6e22-184">How to query MongoDB data?</span></span>](../cosmos-db/tutorial-query-mongodb.md)
