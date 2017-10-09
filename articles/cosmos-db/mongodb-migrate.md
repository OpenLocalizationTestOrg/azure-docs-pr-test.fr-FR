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
# <a name="azure-cosmos-db-import-mongodb-data"></a>Azure Cosmos DB : importer des données MongoDB 

toomigrate des données à partir de MongoDB tooan compte de base de données Azure Cosmos pour une utilisation avec les API de hello pour MongoDB, procédez comme suit :

* Télécharger *mongoimport.exe* ou *mongorestore.exe* de hello [centre de téléchargement MongoDB](https://www.mongodb.com/download-center).
* Obtenir votre [API pour la chaîne de connexion MongoDB](connect-mongodb-account.md).

Si vous importez des données à partir de plan et MongoDB toouse avec hello Azure Cosmos DB, vous devez utiliser des hello [l’outil de Migration de données](import-data.md) tooimport données.

Ce didacticiel couvre hello tâches suivantes :

> [!div class="checklist"]
> * Récupération de votre chaîne de connexion
> * Importation des données MongoDB à l’aide de mongoimport
> * Importation des données MongoDB à l’aide de mongorestore

## <a name="prerequisites"></a>Composants requis

* Augmenter le débit : durée hello de migration de vos données dépend de la quantité de hello de débit que vous définissez pour vos collections. Être sûr de débit de hello tooincrease supérieure aux migrations de données. Une fois que vous avez terminé la migration de hello, réduire les coûts de hello débit toosave. Pour plus d’informations sur l’augmentation du débit Bonjour [portail Azure](https://portal.azure.com), consultez [niveaux de Performance et les niveaux de tarification dans la base de données Azure Cosmos](performance-levels.md).

* Activez SSL : Azure Cosmos DB obéit à des normes et à des exigences strictes en matière de sécurité. Être tooenable que SSL lorsque vous interagissez avec votre compte. les procédures Hello reste hello d’article de hello comprennent comment tooenable SSL pour mongoimport et mongorestore.

## <a name="find-your-connection-string-information-host-port-username-and-password"></a>Recherche des informations de votre chaîne de connexion (hôte, port, nom d’utilisateur et mot de passe)

1. Bonjour [portail Azure](https://portal.azure.com)hello du volet gauche, cliquez sur dans hello **base de données Azure Cosmos** entrée.
2. Bonjour **abonnements** volet, sélectionnez le nom de votre compte.
3. Bonjour **chaîne de connexion** panneau, cliquez sur **chaîne de connexion**.  
Hello droit volet contient toutes les informations de hello que vous avez besoin de toosuccessfully connecter tooyour compte.

    ![Panneau Chaîne de connexion](./media/mongodb-migrate/ConnectionStringBlade.png)

## <a name="import-data-toohello-api-for-mongodb-by-using-mongoimport"></a>Importer des données toohello API pour MongoDB à l’aide de mongoimport

tooimport données tooyour compte de base de données Azure Cosmos, utilisez hello suivant le modèle. Renseignez *hôte*, *nom d’utilisateur*, et *mot de passe* avec les valeurs hello spécifique tooyour compte.  

Modèle :

    mongoimport.exe --host <your_hostname>:10255 -u <your_username> -p <your_password> --db <your_database> --collection <your_collection> --ssl --sslAllowInvalidCertificates --type json --file C:\sample.json

Exemple :  

    mongoimport.exe --host anhoh-host.documents.azure.com:10255 -u anhoh-host -p tkvaVkp4Nnaoirnouenrgisuner2435qwefBH0z256Na24frio34LNQasfaefarfernoimczciqisAXw== --ssl --sslAllowInvalidCertificates --db sampleDB --collection sampleColl --type json --file C:\Users\anhoh\Desktop\*.json

## <a name="import-data-toohello-api-for-mongodb-by-using-mongorestore"></a>Importer des données toohello API pour MongoDB à l’aide de mongorestore

API de tooyour toorestore données MongoDB compte, utilisez hello après l’importation du modèle tooexecute hello. Renseignez *hôte*, *nom d’utilisateur*, et *mot de passe* avec les valeurs hello spécifique tooyour compte.

Modèle :

    mongorestore.exe --host <your_hostname>:10255 -u <your_username> -p <your_password> --db <your_database> --collection <your_collection> --ssl --sslAllowInvalidCertificates <path_to_backup>

Exemple :

    mongorestore.exe --host anhoh-host.documents.azure.com:10255 -u anhoh-host -p tkvaVkp4Nnaoirnouenrgisuner2435qwefBH0z256Na24frio34LNQasfaefarfernoimczciqisAXw== --ssl --sslAllowInvalidCertificates ./dumps/dump-2016-12-07
    
## <a name="guide-for-a-successful-migration"></a>Guide pour une migration réussie

1. Créez au préalable vos collections et mettez-les à l’échelle :
        
    * Par défaut, Azure Cosmos DB approvisionne une nouvelle collection MongoDB avec 1 000 unités de requête (RU). Avant de commencer la migration hello à l’aide de mongoimport, mongorestore ou mongomirror, créer au préalable toutes les collections de hello [portail Azure](https://portal.azure.com) ou à partir d’outils et les pilotes de MongoDB. Si votre collection est supérieure à 10 Go, assurez-vous que toocreate un [partitionnée/partitionnée de collection](partition-data.md) avec une clé de partition approprié.

    * À partir de hello [portail Azure](https://portal.azure.com), augmenter le débit de vos collections à partir de 1 000 RUs pour une collection de partition unique et de 2 500 RUs pour une collection partitionnée uniquement pour la migration de hello. Avec un débit plus élevé hello, vous pouvez éviter la limitation et migrer en moins de temps. Avec toutes les heures de facturation dans base de données Azure Cosmos, vous pouvez réduire le débit de hello immédiatement après les coûts de hello migration toosave.

2. Calculez hello approximative RU frais pour une écriture de document unique :

    a. Se connecter à base de données Azure Cosmos DB MongoDB tooyour de hello MongoDB Shell. Vous trouverez des instructions dans [connecter un tooAzure d’application MongoDB Cosmos DB](connect-mongodb-account.md).
    
    b. Exécuter un exemple de commande d’insertion en utilisant l’une de vos documents exemple hello MongoDB Shell :
    
        ```db.coll.insert({ "playerId": "a067ff", "hashedid": "bb0091", "countryCode": "hk" })```
        
    c. Exécutez ```db.runCommand({getLastRequestStatistics: 1})```. Vous recevez une réponse semblable à celle-ci :
     
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
        
    d. Prenez note de frais de demande hello.
    
3. Déterminer la latence de hello à partir de votre service de cloud de base de données Azure Cosmos de toohello ordinateur :
    
    a. Activer la journalisation documentée de hello MongoDB Shell à l’aide de cette commande :```setVerboseShell(true)```
    
    b. Exécuter une requête simple sur la base de données hello : ```db.coll.find().limit(1)```. Vous recevez une réponse semblable à celle-ci :

        ```
        Fetched 1 record(s) in 100(ms)
        ```
        
4. Supprimer le document hello insérée avant hello tooensure de migration qu’il n’y a aucun document n’est en double. Vous pouvez supprimer des documents à l’aide de cette commande : ```db.coll.remove({})```

5. Calculer hello approximative *batchSize* et *numInsertionWorkers* valeurs :

    * Pour *batchSize*, division hello total configuré RUs par RUs hello consommés à partir de l’écriture de votre document unique à l’étape 3.
    
    * Si elles sont calculées de hello *batchSize* < = 24, utiliser ce numéro en tant que votre *batchSize* valeur.
    
    * Si elles sont calculées de hello *batchSize* > 24, jeu hello *batchSize* too24 de valeur.
    
    * Pour *numInsertionWorkers*, utilisez l’équation suivante : *numInsertionWorkers = (débit approvisionné * latence en secondes) / (taille du lot * RU consommées pour une seule écriture)*.
        
    |Propriété|Valeur|
    |--------|-----|
    |batchSize| 24 |
    |RU approvisionnées | 10000 |
    |Latence | 0,100 s |
    |RU facturée pour 1 écriture de document | 10 unités de requête |
    |numInsertionWorkers | ? |
    
    *numInsertionWorkers = (10 000 RU x 0,1 s) / (24 x 10 RU) = 4,1666*

6. Exécutez la commande de migration finale hello :

   ```
   mongoimport.exe --host anhoh-mongodb.documents.azure.com:10255 -u anhoh-mongodb -p wzRJCyjtLPNuhm53yTwaefawuiefhbauwebhfuabweifbiauweb2YVdl2ZFNZNv8IU89LqFVm5U0bw== --ssl --sslAllowInvalidCertificates --jsonArray --db dabasename --collection collectionName --file "C:\sample.json" --numInsertionWorkers 4 --batchSize 24
   ```

## <a name="next-steps"></a>Étapes suivantes

Vous pouvez continuer l’étape suivante du didacticiel toohello et découvrez comment tooquery MongoDB des données à l’aide de base de données Azure Cosmos. 

> [!div class="nextstepaction"]
>[Comment tooquery MongoDB données ?](../cosmos-db/tutorial-query-mongodb.md)
