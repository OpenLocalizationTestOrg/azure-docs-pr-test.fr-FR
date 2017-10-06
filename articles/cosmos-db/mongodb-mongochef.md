---
title: "aaaUse MongoChef pour la base de données Azure Cosmos | Documents Microsoft"
description: "Découvrez comment toouse MongoChef avec une base de données Azure Cosmos : API pour MongoDB compte"
keywords: MongoChef
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
ms.date: 05/23/2017
ms.author: anhoh
ms.openlocfilehash: 4b047797b231c34ccc6f2ed02416525c6228d596
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-mongochef-with-an-azure-cosmos-db-api-for-mongodb-account"></a>Utiliser MongoChef avec un compte Azure Cosmos DB : API pour MongoDB

tooconnect tooan base de données Azure Cosmos : API pour MongoDB compte, vous devez :

* Télécharger et installer [MongoChef](http://3t.io/mongochef)
* Disposer des informations de [chaîne de connexion](connect-mongodb-account.md) de votre compte Azure Cosmos DB : API pour MongoDB

## <a name="create-hello-connection-in-mongochef"></a>Créer des connexions de hello dans MongoChef
tooadd votre base de données Azure Cosmos : API pour MongoDB compte toohello MongoChef Gestionnaire de connexions, effectuer hello comme suit.

1. Récupérer votre base de données Azure Cosmos : API MongoDB informations de connexion à l’aide des instructions de hello [ici](connect-mongodb-account.md).

    ![Capture d’écran du Panneau de chaîne de connexion hello](./media/mongodb-mongochef/ConnectionStringBlade.png)
2. Cliquez sur **Connect** tooopen hello du Gestionnaire de connexions, puis cliquez sur **nouvelle connexion**

    ![Capture d’écran hello MongoChef du Gestionnaire de connexions](./media/mongodb-mongochef/ConnectionManager.png)
3. Bonjour **nouvelle connexion** fenêtre hello **serveur** , entrez hello hôte (FQDN) de base de données Azure Cosmos de hello : API pour le PORT de compte et hello MongoDB.

    ![Capture d’écran de l’onglet de hello MongoChef connexion Gestionnaire de serveur](./media/mongodb-mongochef/ConnectionManagerServerTab.png)
4. Bonjour **nouvelle connexion** fenêtre hello **authentification** , choisir le Mode d’authentification **Standard (MONGODB-CR ou SCARM-SHA-1)** et entrez le nom d’utilisateur de hello et MOT DE PASSE.  Accepter db de l’authentification par défaut hello (admin) ou fournir votre propre valeur.

    ![Capture d’écran de l’onglet authentification de hello MongoChef connexion manager](./media/mongodb-mongochef/ConnectionManagerAuthenticationTab.png)
5. Bonjour **nouvelle connexion** fenêtre hello **SSL** onglet, vérifiez hello **utiliser SSL protocole tooconnect** case à cocher et hello **accepter serveur auto-signé SSL certificats** case d’option.

    ![Capture d’écran de l’onglet SSL hello MongoChef connection manager](./media/mongodb-mongochef/ConnectionManagerSSLTab.png)
6. Cliquez sur hello **tester la connexion** bouton informations de connexion toovalidate hello, cliquez sur **OK** tooreturn fenêtre de nouvelle connexion toohello, puis cliquez sur **enregistrer**.

    ![Capture d’écran de la fenêtre de connexion de test hello MongoChef](./media/mongodb-mongochef/TestConnectionResults.png)

## <a name="use-mongochef-toocreate-a-database-collection-and-documents"></a>Utilisez MongoChef toocreate une base de données, la collection et des documents
toocreate une base de données, la collection et documents à l’aide de MongoChef, effectuent hello comme suit.

1. Dans **Gestionnaire de connexions**, mettez en surbrillance de la connexion de hello et cliquez sur **connexion**.

    ![Capture d’écran hello MongoChef du Gestionnaire de connexions](./media/mongodb-mongochef/ConnectToAccount.png)
2. Cliquez avec le bouton droit sur un hôte hello et choisissez **ajouter une base de données**.  Spécifiez un nom de base de données, puis cliquez sur **OK**.

    ![Capture d’écran de hello option de base de données ajouter MongoChef](./media/mongodb-mongochef/AddDatabase1.png)
3. Cliquez avec le bouton droit sur base de données hello et choisissez **ajouter la Collection**.  Spécifiez un nom de collection et cliquez sur **Créer**.

    ![Capture d’écran de hello option d’ajouter la Collection MongoChef](./media/mongodb-mongochef/AddCollection.png)
4. Cliquez sur hello **Collection** menu article, puis cliquez sur **ajouter un Document**.

    ![Capture d’écran de l’élément de menu hello MongoChef ajouter un Document](./media/mongodb-mongochef/AddDocument1.png)
5. Dans la boîte de dialogue Ajouter un Document hello, collez hello qui suit, puis cliquez sur **ajouter un Document**.

        {
        "_id": "AndersenFamily",
        "lastName": "Andersen",
        "parents": [
               { "firstName": "Thomas" },
               { "firstName": "Mary Kay"}
        ],
        "children": [
           {
               "firstName": "Henriette Thaulow", "gender": "female", "grade": 5,
               "pets": [{ "givenName": "Fluffy" }]
           }
        ],
        "address": { "state": "WA", "county": "King", "city": "seattle" },
        "isRegistered": true
        }
6. Ajouter un autre document, cette fois avec hello suivant le contenu.

        {
        "_id": "WakefieldFamily",
        "parents": [
            { "familyName": "Wakefield", "givenName": "Robin" },
            { "familyName": "Miller", "givenName": "Ben" }
        ],
        "children": [
            {
                "familyName": "Merriam",
                 "givenName": "Jesse",
                "gender": "female", "grade": 1,
                "pets": [
                    { "givenName": "Goofy" },
                    { "givenName": "Shadow" }
                ]
            },
            {
                "familyName": "Miller",
                 "givenName": "Lisa",
                 "gender": "female",
                 "grade": 8 }
        ],
        "address": { "state": "NY", "county": "Manhattan", "city": "NY" },
        "isRegistered": false
        }
7. Exécutez un exemple de requête. Par exemple, recherchez familles avec le nom « Andersen » hello et parents de retour hello et champs d’état.

    ![Capture d’écran des résultats de requête MongoChef](./media/mongodb-mongochef/QueryDocument1.png)

## <a name="next-steps"></a>Étapes suivantes
* Explorez les [exemples](mongodb-samples.md) d’Azure Cosmos DB : API pour MongoDB.
