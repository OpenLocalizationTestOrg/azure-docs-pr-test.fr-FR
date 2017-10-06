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
# <a name="use-mongochef-with-an-azure-cosmos-db-api-for-mongodb-account"></a><span data-ttu-id="a7267-104">Utiliser MongoChef avec un compte Azure Cosmos DB : API pour MongoDB</span><span class="sxs-lookup"><span data-stu-id="a7267-104">Use MongoChef with an Azure Cosmos DB: API for MongoDB account</span></span>

<span data-ttu-id="a7267-105">tooconnect tooan base de données Azure Cosmos : API pour MongoDB compte, vous devez :</span><span class="sxs-lookup"><span data-stu-id="a7267-105">tooconnect tooan Azure Cosmos DB: API for MongoDB account, you must:</span></span>

* <span data-ttu-id="a7267-106">Télécharger et installer [MongoChef](http://3t.io/mongochef)</span><span class="sxs-lookup"><span data-stu-id="a7267-106">Download and install [MongoChef](http://3t.io/mongochef)</span></span>
* <span data-ttu-id="a7267-107">Disposer des informations de [chaîne de connexion](connect-mongodb-account.md) de votre compte Azure Cosmos DB : API pour MongoDB</span><span class="sxs-lookup"><span data-stu-id="a7267-107">Have your Azure Cosmos DB: API for MongoDB account [connection string](connect-mongodb-account.md) information</span></span>

## <a name="create-hello-connection-in-mongochef"></a><span data-ttu-id="a7267-108">Créer des connexions de hello dans MongoChef</span><span class="sxs-lookup"><span data-stu-id="a7267-108">Create hello connection in MongoChef</span></span>
<span data-ttu-id="a7267-109">tooadd votre base de données Azure Cosmos : API pour MongoDB compte toohello MongoChef Gestionnaire de connexions, effectuer hello comme suit.</span><span class="sxs-lookup"><span data-stu-id="a7267-109">tooadd your Azure Cosmos DB: API for MongoDB account toohello MongoChef connection manager, perform hello following steps.</span></span>

1. <span data-ttu-id="a7267-110">Récupérer votre base de données Azure Cosmos : API MongoDB informations de connexion à l’aide des instructions de hello [ici](connect-mongodb-account.md).</span><span class="sxs-lookup"><span data-stu-id="a7267-110">Retrieve your Azure Cosmos DB: API for MongoDB connection information using hello instructions [here](connect-mongodb-account.md).</span></span>

    ![Capture d’écran du Panneau de chaîne de connexion hello](./media/mongodb-mongochef/ConnectionStringBlade.png)
2. <span data-ttu-id="a7267-112">Cliquez sur **Connect** tooopen hello du Gestionnaire de connexions, puis cliquez sur **nouvelle connexion**</span><span class="sxs-lookup"><span data-stu-id="a7267-112">Click **Connect** tooopen hello Connection Manager, then click **New Connection**</span></span>

    ![Capture d’écran hello MongoChef du Gestionnaire de connexions](./media/mongodb-mongochef/ConnectionManager.png)
3. <span data-ttu-id="a7267-114">Bonjour **nouvelle connexion** fenêtre hello **serveur** , entrez hello hôte (FQDN) de base de données Azure Cosmos de hello : API pour le PORT de compte et hello MongoDB.</span><span class="sxs-lookup"><span data-stu-id="a7267-114">In hello **New Connection** window, on hello **Server** tab, enter hello HOST (FQDN) of hello Azure Cosmos DB: API for MongoDB account and hello PORT.</span></span>

    ![Capture d’écran de l’onglet de hello MongoChef connexion Gestionnaire de serveur](./media/mongodb-mongochef/ConnectionManagerServerTab.png)
4. <span data-ttu-id="a7267-116">Bonjour **nouvelle connexion** fenêtre hello **authentification** , choisir le Mode d’authentification **Standard (MONGODB-CR ou SCARM-SHA-1)** et entrez le nom d’utilisateur de hello et MOT DE PASSE.</span><span class="sxs-lookup"><span data-stu-id="a7267-116">In hello **New Connection** window, on hello **Authentication** tab, choose Authentication Mode **Standard (MONGODB-CR or SCARM-SHA-1)** and enter hello USERNAME and PASSWORD.</span></span>  <span data-ttu-id="a7267-117">Accepter db de l’authentification par défaut hello (admin) ou fournir votre propre valeur.</span><span class="sxs-lookup"><span data-stu-id="a7267-117">Accept hello default authentication db (admin) or provide your own value.</span></span>

    ![Capture d’écran de l’onglet authentification de hello MongoChef connexion manager](./media/mongodb-mongochef/ConnectionManagerAuthenticationTab.png)
5. <span data-ttu-id="a7267-119">Bonjour **nouvelle connexion** fenêtre hello **SSL** onglet, vérifiez hello **utiliser SSL protocole tooconnect** case à cocher et hello **accepter serveur auto-signé SSL certificats** case d’option.</span><span class="sxs-lookup"><span data-stu-id="a7267-119">In hello **New Connection** window, on hello **SSL** tab, check hello **Use SSL protocol tooconnect** check box and hello **Accept server self-signed SSL certificates** radio button.</span></span>

    ![Capture d’écran de l’onglet SSL hello MongoChef connection manager](./media/mongodb-mongochef/ConnectionManagerSSLTab.png)
6. <span data-ttu-id="a7267-121">Cliquez sur hello **tester la connexion** bouton informations de connexion toovalidate hello, cliquez sur **OK** tooreturn fenêtre de nouvelle connexion toohello, puis cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="a7267-121">Click hello **Test Connection** button toovalidate hello connection information, click **OK** tooreturn toohello New Connection window, and then click **Save**.</span></span>

    ![Capture d’écran de la fenêtre de connexion de test hello MongoChef](./media/mongodb-mongochef/TestConnectionResults.png)

## <a name="use-mongochef-toocreate-a-database-collection-and-documents"></a><span data-ttu-id="a7267-123">Utilisez MongoChef toocreate une base de données, la collection et des documents</span><span class="sxs-lookup"><span data-stu-id="a7267-123">Use MongoChef toocreate a database, collection, and documents</span></span>
<span data-ttu-id="a7267-124">toocreate une base de données, la collection et documents à l’aide de MongoChef, effectuent hello comme suit.</span><span class="sxs-lookup"><span data-stu-id="a7267-124">toocreate a database, collection, and documents using MongoChef, perform hello following steps.</span></span>

1. <span data-ttu-id="a7267-125">Dans **Gestionnaire de connexions**, mettez en surbrillance de la connexion de hello et cliquez sur **connexion**.</span><span class="sxs-lookup"><span data-stu-id="a7267-125">In **Connection Manager**, highlight hello connection and click **Connect**.</span></span>

    ![Capture d’écran hello MongoChef du Gestionnaire de connexions](./media/mongodb-mongochef/ConnectToAccount.png)
2. <span data-ttu-id="a7267-127">Cliquez avec le bouton droit sur un hôte hello et choisissez **ajouter une base de données**.</span><span class="sxs-lookup"><span data-stu-id="a7267-127">Right click hello host and choose **Add Database**.</span></span>  <span data-ttu-id="a7267-128">Spécifiez un nom de base de données, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="a7267-128">Provide a database name and click **OK**.</span></span>

    ![Capture d’écran de hello option de base de données ajouter MongoChef](./media/mongodb-mongochef/AddDatabase1.png)
3. <span data-ttu-id="a7267-130">Cliquez avec le bouton droit sur base de données hello et choisissez **ajouter la Collection**.</span><span class="sxs-lookup"><span data-stu-id="a7267-130">Right click hello database and choose **Add Collection**.</span></span>  <span data-ttu-id="a7267-131">Spécifiez un nom de collection et cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="a7267-131">Provide a collection name and click **Create**.</span></span>

    ![Capture d’écran de hello option d’ajouter la Collection MongoChef](./media/mongodb-mongochef/AddCollection.png)
4. <span data-ttu-id="a7267-133">Cliquez sur hello **Collection** menu article, puis cliquez sur **ajouter un Document**.</span><span class="sxs-lookup"><span data-stu-id="a7267-133">Click hello **Collection** menu item, then click **Add Document**.</span></span>

    ![Capture d’écran de l’élément de menu hello MongoChef ajouter un Document](./media/mongodb-mongochef/AddDocument1.png)
5. <span data-ttu-id="a7267-135">Dans la boîte de dialogue Ajouter un Document hello, collez hello qui suit, puis cliquez sur **ajouter un Document**.</span><span class="sxs-lookup"><span data-stu-id="a7267-135">In hello Add Document dialog, paste hello following and then click **Add Document**.</span></span>

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
6. <span data-ttu-id="a7267-136">Ajouter un autre document, cette fois avec hello suivant le contenu.</span><span class="sxs-lookup"><span data-stu-id="a7267-136">Add another document, this time with hello following content.</span></span>

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
7. <span data-ttu-id="a7267-137">Exécutez un exemple de requête.</span><span class="sxs-lookup"><span data-stu-id="a7267-137">Execute a sample query.</span></span> <span data-ttu-id="a7267-138">Par exemple, recherchez familles avec le nom « Andersen » hello et parents de retour hello et champs d’état.</span><span class="sxs-lookup"><span data-stu-id="a7267-138">For example, search for families with hello last name 'Andersen' and return hello parents and state fields.</span></span>

    ![Capture d’écran des résultats de requête MongoChef](./media/mongodb-mongochef/QueryDocument1.png)

## <a name="next-steps"></a><span data-ttu-id="a7267-140">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a7267-140">Next steps</span></span>
* <span data-ttu-id="a7267-141">Explorez les [exemples](mongodb-samples.md) d’Azure Cosmos DB : API pour MongoDB.</span><span class="sxs-lookup"><span data-stu-id="a7267-141">Explore Azure Cosmos DB: API for MongoDB [samples](mongodb-samples.md).</span></span>
