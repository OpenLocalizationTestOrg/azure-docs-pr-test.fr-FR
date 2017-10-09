---
title: "aaaUse mongoimport et mongorestore avec hello API de base de données Azure Cosmos pour MongoDB | Documents Microsoft"
description: "Découvrez comment toouse mongoimport et mongorestore tooimport données tooan API pour MongoDB compte"
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
ms.openlocfilehash: 921354bc7b09a076a73e0cbf5e4aabcc9e83d5a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-import-mongodb-data"></a><span data-ttu-id="bba5a-104">Azure Cosmos DB : importer des données MongoDB</span><span class="sxs-lookup"><span data-stu-id="bba5a-104">Azure Cosmos DB: Import MongoDB data</span></span> 

<span data-ttu-id="bba5a-105">toomigrate des données à partir de MongoDB tooan compte de base de données Azure Cosmos pour une utilisation avec les API de hello pour MongoDB, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="bba5a-105">toomigrate data from MongoDB tooan Azure Cosmos DB account for use with hello API for MongoDB, you must:</span></span>

* <span data-ttu-id="bba5a-106">Télécharger *mongoimport.exe* ou *mongorestore.exe* de hello [centre de téléchargement MongoDB](https://www.mongodb.com/download-center).</span><span class="sxs-lookup"><span data-stu-id="bba5a-106">Download either *mongoimport.exe* or *mongorestore.exe* from hello [MongoDB Download Center](https://www.mongodb.com/download-center).</span></span>
* <span data-ttu-id="bba5a-107">Obtenir votre [API pour la chaîne de connexion MongoDB](connect-mongodb-account.md).</span><span class="sxs-lookup"><span data-stu-id="bba5a-107">Get your [API for MongoDB connection string](connect-mongodb-account.md).</span></span>

<span data-ttu-id="bba5a-108">Si vous importez des données à partir de plan et MongoDB toouse avec hello Azure Cosmos DB, vous devez utiliser des hello [l’outil de Migration de données](import-data.md) tooimport données.</span><span class="sxs-lookup"><span data-stu-id="bba5a-108">If you are importing data from MongoDB and plan toouse it with hello Azure Cosmos DB, you should use hello [Data Migration tool](import-data.md) tooimport data.</span></span>

<span data-ttu-id="bba5a-109">Ce didacticiel couvre hello tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="bba5a-109">This tutorial covers hello following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="bba5a-110">Récupération de votre chaîne de connexion</span><span class="sxs-lookup"><span data-stu-id="bba5a-110">Retrieving your connection string</span></span>
> * <span data-ttu-id="bba5a-111">Importation des données MongoDB à l’aide de mongoimport</span><span class="sxs-lookup"><span data-stu-id="bba5a-111">Importing MongoDB data by using mongoimport</span></span>
> * <span data-ttu-id="bba5a-112">Importation des données MongoDB à l’aide de mongorestore</span><span class="sxs-lookup"><span data-stu-id="bba5a-112">Importing MongoDB data by using mongorestore</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bba5a-113">Composants requis</span><span class="sxs-lookup"><span data-stu-id="bba5a-113">Prerequisites</span></span>

* <span data-ttu-id="bba5a-114">Augmenter le débit : durée hello de migration de vos données dépend de la quantité de hello de débit que vous définissez pour vos collections.</span><span class="sxs-lookup"><span data-stu-id="bba5a-114">Increase throughput: hello duration of your data migration depends on hello amount of throughput you set up for your collections.</span></span> <span data-ttu-id="bba5a-115">Être sûr de débit de hello tooincrease supérieure aux migrations de données.</span><span class="sxs-lookup"><span data-stu-id="bba5a-115">Be sure tooincrease hello throughput for larger data migrations.</span></span> <span data-ttu-id="bba5a-116">Une fois que vous avez terminé la migration de hello, réduire les coûts de hello débit toosave.</span><span class="sxs-lookup"><span data-stu-id="bba5a-116">After you've completed hello migration, decrease hello throughput toosave costs.</span></span> <span data-ttu-id="bba5a-117">Pour plus d’informations sur l’augmentation du débit Bonjour [portail Azure](https://portal.azure.com), consultez [niveaux de Performance et les niveaux de tarification dans la base de données Azure Cosmos](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="bba5a-117">For more information about increasing throughput in hello [Azure portal](https://portal.azure.com), see [Performance levels and pricing tiers in Azure Cosmos DB](performance-levels.md).</span></span>

* <span data-ttu-id="bba5a-118">Activez SSL : Azure Cosmos DB obéit à des normes et à des exigences strictes en matière de sécurité.</span><span class="sxs-lookup"><span data-stu-id="bba5a-118">Enable SSL: Azure Cosmos DB has strict security requirements and standards.</span></span> <span data-ttu-id="bba5a-119">Être tooenable que SSL lorsque vous interagissez avec votre compte.</span><span class="sxs-lookup"><span data-stu-id="bba5a-119">Be sure tooenable SSL when you interact with your account.</span></span> <span data-ttu-id="bba5a-120">les procédures Hello reste hello d’article de hello comprennent comment tooenable SSL pour mongoimport et mongorestore.</span><span class="sxs-lookup"><span data-stu-id="bba5a-120">hello procedures in hello rest of hello article include how tooenable SSL for mongoimport and mongorestore.</span></span>

## <a name="find-your-connection-string-information-host-port-username-and-password"></a><span data-ttu-id="bba5a-121">Recherche des informations de votre chaîne de connexion (hôte, port, nom d’utilisateur et mot de passe)</span><span class="sxs-lookup"><span data-stu-id="bba5a-121">Find your connection string information (host, port, username, and password)</span></span>

1. <span data-ttu-id="bba5a-122">Bonjour [portail Azure](https://portal.azure.com)hello du volet gauche, cliquez sur dans hello **base de données Azure Cosmos** entrée.</span><span class="sxs-lookup"><span data-stu-id="bba5a-122">In hello [Azure portal](https://portal.azure.com), in hello left pane, click hello **Azure Cosmos DB** entry.</span></span>
2. <span data-ttu-id="bba5a-123">Bonjour **abonnements** volet, sélectionnez le nom de votre compte.</span><span class="sxs-lookup"><span data-stu-id="bba5a-123">In hello **Subscriptions** pane, select your account name.</span></span>
3. <span data-ttu-id="bba5a-124">Bonjour **chaîne de connexion** panneau, cliquez sur **chaîne de connexion**.</span><span class="sxs-lookup"><span data-stu-id="bba5a-124">In hello **Connection String** blade, click **Connection String**.</span></span>  
<span data-ttu-id="bba5a-125">Hello droit volet contient toutes les informations de hello que vous avez besoin de toosuccessfully connecter tooyour compte.</span><span class="sxs-lookup"><span data-stu-id="bba5a-125">hello right pane contains all hello information that you need toosuccessfully connect tooyour account.</span></span>

    ![Panneau Chaîne de connexion](./media/mongodb-migrate/ConnectionStringBlade.png)

## <a name="import-data-toohello-api-for-mongodb-by-using-mongoimport"></a><span data-ttu-id="bba5a-127">Importer des données toohello API pour MongoDB à l’aide de mongoimport</span><span class="sxs-lookup"><span data-stu-id="bba5a-127">Import data toohello API for MongoDB by using mongoimport</span></span>

<span data-ttu-id="bba5a-128">tooimport données tooyour compte de base de données Azure Cosmos, utilisez hello suivant le modèle.</span><span class="sxs-lookup"><span data-stu-id="bba5a-128">tooimport data tooyour Azure Cosmos DB account, use hello following template.</span></span> <span data-ttu-id="bba5a-129">Renseignez *hôte*, *nom d’utilisateur*, et *mot de passe* avec les valeurs hello spécifique tooyour compte.</span><span class="sxs-lookup"><span data-stu-id="bba5a-129">Fill in *host*, *username*, and *password* with hello values that are specific tooyour account.</span></span>  

<span data-ttu-id="bba5a-130">Modèle :</span><span class="sxs-lookup"><span data-stu-id="bba5a-130">Template:</span></span>

    mongoimport.exe --host <your_hostname>:10255 -u <your_username> -p <your_password> --db <your_database> --collection <your_collection> --ssl --sslAllowInvalidCertificates --type json --file C:\sample.json

<span data-ttu-id="bba5a-131">Exemple :</span><span class="sxs-lookup"><span data-stu-id="bba5a-131">Example:</span></span>  

    mongoimport.exe --host anhoh-host.documents.azure.com:10255 -u anhoh-host -p tkvaVkp4Nnaoirnouenrgisuner2435qwefBH0z256Na24frio34LNQasfaefarfernoimczciqisAXw== --ssl --sslAllowInvalidCertificates --db sampleDB --collection sampleColl --type json --file C:\Users\anhoh\Desktop\*.json

## <a name="import-data-toohello-api-for-mongodb-by-using-mongorestore"></a><span data-ttu-id="bba5a-132">Importer des données toohello API pour MongoDB à l’aide de mongorestore</span><span class="sxs-lookup"><span data-stu-id="bba5a-132">Import data toohello API for MongoDB by using mongorestore</span></span>

<span data-ttu-id="bba5a-133">API de tooyour toorestore données MongoDB compte, utilisez hello après l’importation du modèle tooexecute hello.</span><span class="sxs-lookup"><span data-stu-id="bba5a-133">toorestore data tooyour API for MongoDB account, use hello following template tooexecute hello import.</span></span> <span data-ttu-id="bba5a-134">Renseignez *hôte*, *nom d’utilisateur*, et *mot de passe* avec les valeurs hello spécifique tooyour compte.</span><span class="sxs-lookup"><span data-stu-id="bba5a-134">Fill in *host*, *username*, and *password* with hello values that are specific tooyour account.</span></span>

<span data-ttu-id="bba5a-135">Modèle :</span><span class="sxs-lookup"><span data-stu-id="bba5a-135">Template:</span></span>

    mongorestore.exe --host <your_hostname>:10255 -u <your_username> -p <your_password> --db <your_database> --collection <your_collection> --ssl --sslAllowInvalidCertificates <path_to_backup>

<span data-ttu-id="bba5a-136">Exemple :</span><span class="sxs-lookup"><span data-stu-id="bba5a-136">Example:</span></span>

    mongorestore.exe --host anhoh-host.documents.azure.com:10255 -u anhoh-host -p tkvaVkp4Nnaoirnouenrgisuner2435qwefBH0z256Na24frio34LNQasfaefarfernoimczciqisAXw== --ssl --sslAllowInvalidCertificates ./dumps/dump-2016-12-07
    
## <a name="guide-for-a-successful-migration"></a><span data-ttu-id="bba5a-137">Guide pour une migration réussie</span><span class="sxs-lookup"><span data-stu-id="bba5a-137">Guide for a successful migration</span></span>

1. <span data-ttu-id="bba5a-138">Créez au préalable vos collections et mettez-les à l’échelle :</span><span class="sxs-lookup"><span data-stu-id="bba5a-138">Pre-create and scale your collections:</span></span>
        
    * <span data-ttu-id="bba5a-139">Par défaut, Azure Cosmos DB approvisionne une nouvelle collection MongoDB avec 1 000 unités de requête (RU).</span><span class="sxs-lookup"><span data-stu-id="bba5a-139">By default, Azure Cosmos DB provisions a new MongoDB collection with 1,000 request units (RUs).</span></span> <span data-ttu-id="bba5a-140">Avant de commencer la migration hello à l’aide de mongoimport, mongorestore ou mongomirror, créer au préalable toutes les collections de hello [portail Azure](https://portal.azure.com) ou à partir d’outils et les pilotes de MongoDB.</span><span class="sxs-lookup"><span data-stu-id="bba5a-140">Before you start hello migration by using mongoimport, mongorestore, or mongomirror, pre-create all your collections from hello [Azure portal](https://portal.azure.com) or from MongoDB drivers and tools.</span></span> <span data-ttu-id="bba5a-141">Si votre collection est supérieure à 10 Go, assurez-vous que toocreate un [partitionnée/partitionnée de collection](partition-data.md) avec une clé de partition approprié.</span><span class="sxs-lookup"><span data-stu-id="bba5a-141">If your collection is greater than 10 GB, make sure toocreate a [sharded/partitioned collection](partition-data.md) with an appropriate shard key.</span></span>

    * <span data-ttu-id="bba5a-142">À partir de hello [portail Azure](https://portal.azure.com), augmenter le débit de vos collections à partir de 1 000 RUs pour une collection de partition unique et de 2 500 RUs pour une collection partitionnée uniquement pour la migration de hello.</span><span class="sxs-lookup"><span data-stu-id="bba5a-142">From hello [Azure portal](https://portal.azure.com), increase your collections' throughput from 1,000 RUs for a single partition collection and 2,500 RUs for a sharded collection just for hello migration.</span></span> <span data-ttu-id="bba5a-143">Avec un débit plus élevé hello, vous pouvez éviter la limitation et migrer en moins de temps.</span><span class="sxs-lookup"><span data-stu-id="bba5a-143">With hello higher throughput, you can avoid throttling and migrate in less time.</span></span> <span data-ttu-id="bba5a-144">Avec toutes les heures de facturation dans base de données Azure Cosmos, vous pouvez réduire le débit de hello immédiatement après les coûts de hello migration toosave.</span><span class="sxs-lookup"><span data-stu-id="bba5a-144">With hourly billing in Azure Cosmos DB, you can reduce hello throughput immediately after hello migration toosave costs.</span></span>

2. <span data-ttu-id="bba5a-145">Calculez hello approximative RU frais pour une écriture de document unique :</span><span class="sxs-lookup"><span data-stu-id="bba5a-145">Calculate hello approximate RU charge for a single document write:</span></span>

    <span data-ttu-id="bba5a-146">a.</span><span class="sxs-lookup"><span data-stu-id="bba5a-146">a.</span></span> <span data-ttu-id="bba5a-147">Se connecter à base de données Azure Cosmos DB MongoDB tooyour de hello MongoDB Shell.</span><span class="sxs-lookup"><span data-stu-id="bba5a-147">Connect tooyour Azure Cosmos DB MongoDB database from hello MongoDB Shell.</span></span> <span data-ttu-id="bba5a-148">Vous trouverez des instructions dans [connecter un tooAzure d’application MongoDB Cosmos DB](connect-mongodb-account.md).</span><span class="sxs-lookup"><span data-stu-id="bba5a-148">You can find instructions in [Connect a MongoDB application tooAzure Cosmos DB](connect-mongodb-account.md).</span></span>
    
    <span data-ttu-id="bba5a-149">b.</span><span class="sxs-lookup"><span data-stu-id="bba5a-149">b.</span></span> <span data-ttu-id="bba5a-150">Exécuter un exemple de commande d’insertion en utilisant l’une de vos documents exemple hello MongoDB Shell :</span><span class="sxs-lookup"><span data-stu-id="bba5a-150">Run a sample insert command by using one of your sample documents from hello MongoDB Shell:</span></span>
    
        ```db.coll.insert({ "playerId": "a067ff", "hashedid": "bb0091", "countryCode": "hk" })```
        
    <span data-ttu-id="bba5a-151">c.</span><span class="sxs-lookup"><span data-stu-id="bba5a-151">c.</span></span> <span data-ttu-id="bba5a-152">Exécutez ```db.runCommand({getLastRequestStatistics: 1})```. Vous recevez une réponse semblable à celle-ci :</span><span class="sxs-lookup"><span data-stu-id="bba5a-152">Run ```db.runCommand({getLastRequestStatistics: 1})``` and you will receive a response like this one:</span></span>
     
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
        
    <span data-ttu-id="bba5a-153">d.</span><span class="sxs-lookup"><span data-stu-id="bba5a-153">d.</span></span> <span data-ttu-id="bba5a-154">Prenez note de frais de demande hello.</span><span class="sxs-lookup"><span data-stu-id="bba5a-154">Take note of hello request charge.</span></span>
    
3. <span data-ttu-id="bba5a-155">Déterminer la latence de hello à partir de votre service de cloud de base de données Azure Cosmos de toohello ordinateur :</span><span class="sxs-lookup"><span data-stu-id="bba5a-155">Determine hello latency from your machine toohello Azure Cosmos DB cloud service:</span></span>
    
    <span data-ttu-id="bba5a-156">a.</span><span class="sxs-lookup"><span data-stu-id="bba5a-156">a.</span></span> <span data-ttu-id="bba5a-157">Activer la journalisation documentée de hello MongoDB Shell à l’aide de cette commande :```setVerboseShell(true)```</span><span class="sxs-lookup"><span data-stu-id="bba5a-157">Enable verbose logging from hello MongoDB Shell by using this command: ```setVerboseShell(true)```</span></span>
    
    <span data-ttu-id="bba5a-158">b.</span><span class="sxs-lookup"><span data-stu-id="bba5a-158">b.</span></span> <span data-ttu-id="bba5a-159">Exécuter une requête simple sur la base de données hello : ```db.coll.find().limit(1)```.</span><span class="sxs-lookup"><span data-stu-id="bba5a-159">Run a simple query against hello database: ```db.coll.find().limit(1)```.</span></span> <span data-ttu-id="bba5a-160">Vous recevez une réponse semblable à celle-ci :</span><span class="sxs-lookup"><span data-stu-id="bba5a-160">You will receive a response like this one:</span></span>

        ```
        Fetched 1 record(s) in 100(ms)
        ```
        
4. <span data-ttu-id="bba5a-161">Supprimer le document hello insérée avant hello tooensure de migration qu’il n’y a aucun document n’est en double.</span><span class="sxs-lookup"><span data-stu-id="bba5a-161">Remove hello inserted document before hello migration tooensure that there are no duplicate documents.</span></span> <span data-ttu-id="bba5a-162">Vous pouvez supprimer des documents à l’aide de cette commande : ```db.coll.remove({})```</span><span class="sxs-lookup"><span data-stu-id="bba5a-162">You can remove documents by using this command: ```db.coll.remove({})```</span></span>

5. <span data-ttu-id="bba5a-163">Calculer hello approximative *batchSize* et *numInsertionWorkers* valeurs :</span><span class="sxs-lookup"><span data-stu-id="bba5a-163">Calculate hello approximate *batchSize* and *numInsertionWorkers* values:</span></span>

    * <span data-ttu-id="bba5a-164">Pour *batchSize*, division hello total configuré RUs par RUs hello consommés à partir de l’écriture de votre document unique à l’étape 3.</span><span class="sxs-lookup"><span data-stu-id="bba5a-164">For *batchSize*, divide hello total provisioned RUs by hello RUs consumed from your single document write in step 3.</span></span>
    
    * <span data-ttu-id="bba5a-165">Si elles sont calculées de hello *batchSize* < = 24, utiliser ce numéro en tant que votre *batchSize* valeur.</span><span class="sxs-lookup"><span data-stu-id="bba5a-165">If hello calculated *batchSize* <= 24, use that number as your *batchSize* value.</span></span>
    
    * <span data-ttu-id="bba5a-166">Si elles sont calculées de hello *batchSize* > 24, jeu hello *batchSize* too24 de valeur.</span><span class="sxs-lookup"><span data-stu-id="bba5a-166">If hello calculated *batchSize* > 24, set hello *batchSize* value too24.</span></span>
    
    * <span data-ttu-id="bba5a-167">Pour *numInsertionWorkers*, utilisez l’équation suivante : *numInsertionWorkers = (débit approvisionné * latence en secondes) / (taille du lot * RU consommées pour une seule écriture)*.</span><span class="sxs-lookup"><span data-stu-id="bba5a-167">For *numInsertionWorkers*, use this equation:   *numInsertionWorkers =  (provisioned throughput * latency in seconds) / (batch size * consumed RUs for a single write)*.</span></span>
        
    |<span data-ttu-id="bba5a-168">Propriété</span><span class="sxs-lookup"><span data-stu-id="bba5a-168">Property</span></span>|<span data-ttu-id="bba5a-169">Valeur</span><span class="sxs-lookup"><span data-stu-id="bba5a-169">Value</span></span>|
    |--------|-----|
    |<span data-ttu-id="bba5a-170">batchSize</span><span class="sxs-lookup"><span data-stu-id="bba5a-170">batchSize</span></span>| <span data-ttu-id="bba5a-171">24</span><span class="sxs-lookup"><span data-stu-id="bba5a-171">24</span></span> |
    |<span data-ttu-id="bba5a-172">RU approvisionnées</span><span class="sxs-lookup"><span data-stu-id="bba5a-172">RUs provisioned</span></span> | <span data-ttu-id="bba5a-173">10000</span><span class="sxs-lookup"><span data-stu-id="bba5a-173">10000</span></span> |
    |<span data-ttu-id="bba5a-174">Latence</span><span class="sxs-lookup"><span data-stu-id="bba5a-174">Latency</span></span> | <span data-ttu-id="bba5a-175">0,100 s</span><span class="sxs-lookup"><span data-stu-id="bba5a-175">0.100 s</span></span> |
    |<span data-ttu-id="bba5a-176">RU facturée pour 1 écriture de document</span><span class="sxs-lookup"><span data-stu-id="bba5a-176">RU charged for 1 doc write</span></span> | <span data-ttu-id="bba5a-177">10 unités de requête</span><span class="sxs-lookup"><span data-stu-id="bba5a-177">10 RUs</span></span> |
    |<span data-ttu-id="bba5a-178">numInsertionWorkers</span><span class="sxs-lookup"><span data-stu-id="bba5a-178">numInsertionWorkers</span></span> | <span data-ttu-id="bba5a-179">?</span><span class="sxs-lookup"><span data-stu-id="bba5a-179">?</span></span> |
    
    <span data-ttu-id="bba5a-180">*numInsertionWorkers = (10 000 RU x 0,1 s) / (24 x 10 RU) = 4,1666*</span><span class="sxs-lookup"><span data-stu-id="bba5a-180">*numInsertionWorkers = (10000 RUs x 0.1 s) / (24 x 10 RUs) = 4.1666*</span></span>

6. <span data-ttu-id="bba5a-181">Exécutez la commande de migration finale hello :</span><span class="sxs-lookup"><span data-stu-id="bba5a-181">Run hello final migration command:</span></span>

   ```
   mongoimport.exe --host anhoh-mongodb.documents.azure.com:10255 -u anhoh-mongodb -p wzRJCyjtLPNuhm53yTwaefawuiefhbauwebhfuabweifbiauweb2YVdl2ZFNZNv8IU89LqFVm5U0bw== --ssl --sslAllowInvalidCertificates --jsonArray --db dabasename --collection collectionName --file "C:\sample.json" --numInsertionWorkers 4 --batchSize 24
   ```

## <a name="next-steps"></a><span data-ttu-id="bba5a-182">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bba5a-182">Next steps</span></span>

<span data-ttu-id="bba5a-183">Vous pouvez continuer l’étape suivante du didacticiel toohello et découvrez comment tooquery MongoDB des données à l’aide de base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="bba5a-183">You can proceed toohello next tutorial and learn how tooquery MongoDB data by using Azure Cosmos DB.</span></span> 

> [!div class="nextstepaction"]
>[<span data-ttu-id="bba5a-184">Comment tooquery MongoDB données ?</span><span class="sxs-lookup"><span data-stu-id="bba5a-184">How tooquery MongoDB data?</span></span>](../cosmos-db/tutorial-query-mongodb.md)
