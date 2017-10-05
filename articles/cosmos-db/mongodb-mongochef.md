---
title: Utiliser MongoChef pour Azure Cosmos DB | Microsoft Docs
description: "Découvrez comment utiliser MongoChef avec un compte Azure Cosmos DB : API pour MongoDB"
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
ms.openlocfilehash: 54c9799bd646b827f602e2ea2f9a15a4fc853f00
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="use-mongochef-with-an-azure-cosmos-db-api-for-mongodb-account"></a><span data-ttu-id="feaff-104">Utiliser MongoChef avec un compte Azure Cosmos DB : API pour MongoDB</span><span class="sxs-lookup"><span data-stu-id="feaff-104">Use MongoChef with an Azure Cosmos DB: API for MongoDB account</span></span>

<span data-ttu-id="feaff-105">Pour vous connecter à un compte Azure Cosmos DB : API pour MongoDB, vous devez :</span><span class="sxs-lookup"><span data-stu-id="feaff-105">To connect to an Azure Cosmos DB: API for MongoDB account, you must:</span></span>

* <span data-ttu-id="feaff-106">Télécharger et installer [MongoChef](http://3t.io/mongochef)</span><span class="sxs-lookup"><span data-stu-id="feaff-106">Download and install [MongoChef](http://3t.io/mongochef)</span></span>
* <span data-ttu-id="feaff-107">Disposer des informations de [chaîne de connexion](connect-mongodb-account.md) de votre compte Azure Cosmos DB : API pour MongoDB</span><span class="sxs-lookup"><span data-stu-id="feaff-107">Have your Azure Cosmos DB: API for MongoDB account [connection string](connect-mongodb-account.md) information</span></span>

## <a name="create-the-connection-in-mongochef"></a><span data-ttu-id="feaff-108">Créer la connexion dans MongoChef</span><span class="sxs-lookup"><span data-stu-id="feaff-108">Create the connection in MongoChef</span></span>
<span data-ttu-id="feaff-109">Pour ajouter votre compte Azure Cosmos DB : API pour MongoDB au gestionnaire de connexions MongoChef, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="feaff-109">To add your Azure Cosmos DB: API for MongoDB account to the MongoChef connection manager, perform the following steps.</span></span>

1. <span data-ttu-id="feaff-110">Récupérez vos informations de connexion Azure Cosmos DB : API pour MongoDB à l’aide des instructions [ici](connect-mongodb-account.md).</span><span class="sxs-lookup"><span data-stu-id="feaff-110">Retrieve your Azure Cosmos DB: API for MongoDB connection information using the instructions [here](connect-mongodb-account.md).</span></span>

    ![Capture d’écran du panneau Chaîne de connexion](./media/mongodb-mongochef/ConnectionStringBlade.png)
2. <span data-ttu-id="feaff-112">Cliquez sur **Connexion** pour ouvrir le gestionnaire de connexions, puis cliquez sur **Nouvelle connexion**.</span><span class="sxs-lookup"><span data-stu-id="feaff-112">Click **Connect** to open the Connection Manager, then click **New Connection**</span></span>

    ![Capture d’écran du Gestionnaire de connexions MongoChef](./media/mongodb-mongochef/ConnectionManager.png)
3. <span data-ttu-id="feaff-114">Sous l’onglet **Serveur** de la fenêtre **Nouvelle connexion**, entrez l’HÔTE (FQDN) du compte Azure Cosmos DB : API pour MongoDB et le PORT.</span><span class="sxs-lookup"><span data-stu-id="feaff-114">In the **New Connection** window, on the **Server** tab, enter the HOST (FQDN) of the Azure Cosmos DB: API for MongoDB account and the PORT.</span></span>

    ![Capture d’écran de l’onglet Serveur du Gestionnaire de connexions MongoChef](./media/mongodb-mongochef/ConnectionManagerServerTab.png)
4. <span data-ttu-id="feaff-116">Dans la fenêtre **Nouvelle connexion**, sous l’onglet **Authentification**, choisissez le mode d’authentification **Standard (MONGODB-CR ou SCARM-SHA-1)** et entrez les NOM D’UTILISATEUR et MOT DE PASSE.</span><span class="sxs-lookup"><span data-stu-id="feaff-116">In the **New Connection** window, on the **Authentication** tab, choose Authentication Mode **Standard (MONGODB-CR or SCARM-SHA-1)** and enter the USERNAME and PASSWORD.</span></span>  <span data-ttu-id="feaff-117">Acceptez la base de données d’authentification par défaut (admin) ou indiquez votre propre valeur.</span><span class="sxs-lookup"><span data-stu-id="feaff-117">Accept the default authentication db (admin) or provide your own value.</span></span>

    ![Capture d’écran de l’onglet Authentification du Gestionnaire de connexions MongoChef](./media/mongodb-mongochef/ConnectionManagerAuthenticationTab.png)
5. <span data-ttu-id="feaff-119">Dans la fenêtre **Nouvelle connexion**, sous l’onglet **SSL**, cochez la case **Utiliser le protocole SSL pour se connecter** et sélectionnez **Accepter les certificats SSL auto-signés**.</span><span class="sxs-lookup"><span data-stu-id="feaff-119">In the **New Connection** window, on the **SSL** tab, check the **Use SSL protocol to connect** check box and the **Accept server self-signed SSL certificates** radio button.</span></span>

    ![Capture d’écran de l’onglet SSL du Gestionnaire de connexions MongoChef](./media/mongodb-mongochef/ConnectionManagerSSLTab.png)
6. <span data-ttu-id="feaff-121">Cliquez sur le bouton **Tester la connexion** pour valider les informations de connexion, cliquez sur **OK** pour revenir à la fenêtre Nouvelle connexion, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="feaff-121">Click the **Test Connection** button to validate the connection information, click **OK** to return to the New Connection window, and then click **Save**.</span></span>

    ![Capture d’écran de la fenêtre Tester la connexion de MongoChef](./media/mongodb-mongochef/TestConnectionResults.png)

## <a name="use-mongochef-to-create-a-database-collection-and-documents"></a><span data-ttu-id="feaff-123">Utiliser MongoChef pour créer une base de données, une collection et des documents</span><span class="sxs-lookup"><span data-stu-id="feaff-123">Use MongoChef to create a database, collection, and documents</span></span>
<span data-ttu-id="feaff-124">Pour créer une base de données, une collection et des documents à l’aide de MongoChef, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="feaff-124">To create a database, collection, and documents using MongoChef, perform the following steps.</span></span>

1. <span data-ttu-id="feaff-125">Dans le **Gestionnaire de connexions**, sélectionnez la connexion et cliquez sur **Connexion**.</span><span class="sxs-lookup"><span data-stu-id="feaff-125">In **Connection Manager**, highlight the connection and click **Connect**.</span></span>

    ![Capture d’écran du Gestionnaire de connexions MongoChef](./media/mongodb-mongochef/ConnectToAccount.png)
2. <span data-ttu-id="feaff-127">Cliquez avec le bouton droit sur l’hôte et choisissez **Ajouter une base de données**.</span><span class="sxs-lookup"><span data-stu-id="feaff-127">Right click the host and choose **Add Database**.</span></span>  <span data-ttu-id="feaff-128">Spécifiez un nom de base de données, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="feaff-128">Provide a database name and click **OK**.</span></span>

    ![Capture d’écran de l’option Ajouter une base de données de MongoChef](./media/mongodb-mongochef/AddDatabase1.png)
3. <span data-ttu-id="feaff-130">Cliquez avec le bouton droit sur la base de données et sélectionnez **Ajouter une collection**.</span><span class="sxs-lookup"><span data-stu-id="feaff-130">Right click the database and choose **Add Collection**.</span></span>  <span data-ttu-id="feaff-131">Spécifiez un nom de collection et cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="feaff-131">Provide a collection name and click **Create**.</span></span>

    ![Capture d’écran de l’option Ajouter une collection de MongoChef](./media/mongodb-mongochef/AddCollection.png)
4. <span data-ttu-id="feaff-133">Cliquez sur l’élément de menu **Collection**, puis cliquez sur **Ajouter un document**.</span><span class="sxs-lookup"><span data-stu-id="feaff-133">Click the **Collection** menu item, then click **Add Document**.</span></span>

    ![Capture d’écran de l’option Ajouter un document de MongoChef](./media/mongodb-mongochef/AddDocument1.png)
5. <span data-ttu-id="feaff-135">Dans la boîte de dialogue Ajouter un document, collez les éléments suivants, puis cliquez sur **Ajouter un document**.</span><span class="sxs-lookup"><span data-stu-id="feaff-135">In the Add Document dialog, paste the following and then click **Add Document**.</span></span>

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
6. <span data-ttu-id="feaff-136">Ajoutez un autre document, cette fois avec le contenu suivant.</span><span class="sxs-lookup"><span data-stu-id="feaff-136">Add another document, this time with the following content.</span></span>

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
7. <span data-ttu-id="feaff-137">Exécutez un exemple de requête.</span><span class="sxs-lookup"><span data-stu-id="feaff-137">Execute a sample query.</span></span> <span data-ttu-id="feaff-138">Par exemple, recherchez des familles portant le nom « Andersen » en retournant les champs parents et état.</span><span class="sxs-lookup"><span data-stu-id="feaff-138">For example, search for families with the last name 'Andersen' and return the parents and state fields.</span></span>

    ![Capture d’écran des résultats de requête MongoChef](./media/mongodb-mongochef/QueryDocument1.png)

## <a name="next-steps"></a><span data-ttu-id="feaff-140">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="feaff-140">Next steps</span></span>
* <span data-ttu-id="feaff-141">Explorez les [exemples](mongodb-samples.md) d’Azure Cosmos DB : API pour MongoDB.</span><span class="sxs-lookup"><span data-stu-id="feaff-141">Explore Azure Cosmos DB: API for MongoDB [samples](mongodb-samples.md).</span></span>
