---
title: "Chaîne de connexion MongoDB pour un compte Azure Cosmos DB | Microsoft Docs"
description: "Découvrez comment connecter votre application MongoDB à un compte Azure Cosmos DB à l’aide d’une chaîne de connexion MongoDB."
keywords: "chaîne de connexion mongodb"
services: cosmos-db
author: AndrewHoh
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: e36f7375-9329-403b-afd1-4ab49894f75e
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/12/2017
ms.author: anhoh
ms.openlocfilehash: 5a47001705531d971d3181df9c0aa8f957168845
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-a-mongodb-application-to-azure-cosmos-db"></a><span data-ttu-id="ea440-104">Connecter une application MongoDB à Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="ea440-104">Connect a MongoDB application to Azure Cosmos DB</span></span>
<span data-ttu-id="ea440-105">Découvrez comment connecter votre application MongoDB à un compte Azure Cosmos DB à l’aide d’une chaîne de connexion MongoDB.</span><span class="sxs-lookup"><span data-stu-id="ea440-105">Learn how to connect your MongoDB app to an Azure Cosmos DB account by using a MongoDB connection string.</span></span> <span data-ttu-id="ea440-106">Vous pouvez ensuite utiliser une base de données Azure Cosmos DB en tant que magasin de données pour votre application MongoDB.</span><span class="sxs-lookup"><span data-stu-id="ea440-106">You can then use an Azure Cosmos DB database as the data store for your MongoDB app.</span></span> 

<span data-ttu-id="ea440-107">Ce didacticiel fournit deux façons de récupérer les informations de la chaîne de connexion :</span><span class="sxs-lookup"><span data-stu-id="ea440-107">This tutorial provides two ways to retrieve connection string information:</span></span>

- <span data-ttu-id="ea440-108">[Méthode du démarrage rapide](#QuickstartConnection), à utiliser avec les pilotes .NET, Node.js, MongoDB Shell, Java et Python.</span><span class="sxs-lookup"><span data-stu-id="ea440-108">[The quick start method](#QuickstartConnection), for use with .NET, Node.js, MongoDB Shell, Java, and Python drivers</span></span>
- <span data-ttu-id="ea440-109">[Méthode de la chaîne de connexion personnalisée](#GetCustomConnection), à utiliser avec d’autres pilotes.</span><span class="sxs-lookup"><span data-stu-id="ea440-109">[The custom connection string method](#GetCustomConnection), for use with other drivers</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ea440-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="ea440-110">Prerequisites</span></span>

- <span data-ttu-id="ea440-111">Un compte Azure.</span><span class="sxs-lookup"><span data-stu-id="ea440-111">An Azure account.</span></span> <span data-ttu-id="ea440-112">Si vous ne possédez pas de compte Azure, vous pouvez créer un [compte Azure gratuit](https://azure.microsoft.com/free/) dès maintenant.</span><span class="sxs-lookup"><span data-stu-id="ea440-112">If you don't have an Azure account, create a [free Azure account](https://azure.microsoft.com/free/) now.</span></span> 
- <span data-ttu-id="ea440-113">Un compte Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="ea440-113">An Azure Cosmos DB account.</span></span> <span data-ttu-id="ea440-114">Pour des instructions, voir [Développer une application web API MongoDB avec .NET et le portail Azure](create-mongodb-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="ea440-114">For instructions, see [Build a MongoDB API web app with .NET and the Azure portal](create-mongodb-dotnet.md).</span></span>

## <span data-ttu-id="ea440-115"><a id="QuickstartConnection"></a>Obtenir la chaîne de connexion MongoDB à l’aide du démarrage rapide</span><span class="sxs-lookup"><span data-stu-id="ea440-115"><a id="QuickstartConnection"></a>Get the MongoDB connection string by using the quick start</span></span>
1. <span data-ttu-id="ea440-116">Dans un navigateur Internet, connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ea440-116">In an Internet browser, sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="ea440-117">Dans le panneau **Azure Cosmos DB**, sélectionnez l’API pour le compte MongoDB.</span><span class="sxs-lookup"><span data-stu-id="ea440-117">In the **Azure Cosmos DB** blade, select the API for MongoDB account.</span></span> 
3. <span data-ttu-id="ea440-118">Dans le volet gauche du panneau Compte, cliquez sur **Démarrage rapide**.</span><span class="sxs-lookup"><span data-stu-id="ea440-118">In the left pane of the account blade, click **Quick start**.</span></span> 
4. <span data-ttu-id="ea440-119">Choisissez votre plateforme (**.NET**, **Node.js**, **MongoDB Shell**, **Java** ou **Python**).</span><span class="sxs-lookup"><span data-stu-id="ea440-119">Choose your platform (**.NET**, **Node.js**, **MongoDB Shell**, **Java**, **Python**).</span></span> <span data-ttu-id="ea440-120">Si votre pilote ou outil n’est pas répertorié, ne vous inquiétez pas, nous développons en permanence de nouveaux extraits de code de connexion.</span><span class="sxs-lookup"><span data-stu-id="ea440-120">If you don't see your driver or tool listed, don't worry--we continuously document more connection code snippets.</span></span> <span data-ttu-id="ea440-121">Entrez ci-dessous un commentaire sur ce que vous voudriez voir.</span><span class="sxs-lookup"><span data-stu-id="ea440-121">Please comment below on what you'd like to see.</span></span> <span data-ttu-id="ea440-122">Pour savoir comment créer votre propre connexion, lisez [Obtenir les informations de chaîne de connexion du compte](#GetCustomConnection).</span><span class="sxs-lookup"><span data-stu-id="ea440-122">To learn how to craft your own connection, read [Get the account's connection string information](#GetCustomConnection).</span></span>
5. <span data-ttu-id="ea440-123">Copiez et collez l’extrait de code dans votre application MongoDB.</span><span class="sxs-lookup"><span data-stu-id="ea440-123">Copy and paste the code snippet into your MongoDB app.</span></span>

    ![Panneau Démarrage rapide](./media/connect-mongodb-account/QuickStartBlade.png)

## <span data-ttu-id="ea440-125"><a id="GetCustomConnection"></a> Obtenir la chaîne de connexion MongoDB à personnaliser</span><span class="sxs-lookup"><span data-stu-id="ea440-125"><a id="GetCustomConnection"></a> Get the MongoDB connection string to customize</span></span>
1. <span data-ttu-id="ea440-126">Dans un navigateur Internet, connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ea440-126">In an Internet browser, sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="ea440-127">Dans le panneau **Azure Cosmos DB**, sélectionnez l’API pour le compte MongoDB.</span><span class="sxs-lookup"><span data-stu-id="ea440-127">In the **Azure Cosmos DB** blade, select the API for MongoDB account.</span></span> 
3. <span data-ttu-id="ea440-128">Dans le volet gauche du panneau Compte, cliquez sur **Chaîne de connexion**.</span><span class="sxs-lookup"><span data-stu-id="ea440-128">In the left pane of the account blade, click **Connection String**.</span></span> 
4. <span data-ttu-id="ea440-129">Le panneau **Chaîne de connexion** s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="ea440-129">The **Connection String** blade opens.</span></span> <span data-ttu-id="ea440-130">Il affiche toutes les informations nécessaires pour la connexion au compte à l’aide d’un pilote pour MongoDB, dont une chaîne de connexion prédéfinie.</span><span class="sxs-lookup"><span data-stu-id="ea440-130">It has all the information necessary to connect to the account by using a driver for MongoDB, including a preconstructed connection string.</span></span>

    ![Panneau Chaîne de connexion](./media/connect-mongodb-account/ConnectionStringBlade.png)

## <a name="connection-string-requirements"></a><span data-ttu-id="ea440-132">Exigences relatives à la chaîne de connexion</span><span class="sxs-lookup"><span data-stu-id="ea440-132">Connection string requirements</span></span>
> [!Important]
> <span data-ttu-id="ea440-133">Azure Cosmos DB obéit à des normes et à des exigences strictes en matière de sécurité.</span><span class="sxs-lookup"><span data-stu-id="ea440-133">Azure Cosmos DB has strict security requirements and standards.</span></span> <span data-ttu-id="ea440-134">Les comptes Azure Cosmos DB requièrent une authentification et une communication sécurisée via *SSL*.</span><span class="sxs-lookup"><span data-stu-id="ea440-134">Azure Cosmos DB accounts require authentication and secure communication via *SSL*.</span></span> 
>
>

<span data-ttu-id="ea440-135">Azure Cosmos DB prend en charge le format d’URI de chaîne de connexion MongoDB standard, sous réserve que quelques exigences spécifiques soient satisfaites : les comptes Azure Cosmos DB requièrent une authentification et une communication sécurisée via SSL.</span><span class="sxs-lookup"><span data-stu-id="ea440-135">Azure Cosmos DB supports the standard MongoDB connection string URI format, with a couple of specific requirements: Azure Cosmos DB accounts require authentication and secure communication via SSL.</span></span> <span data-ttu-id="ea440-136">Le format de chaîne de connexion est donc :</span><span class="sxs-lookup"><span data-stu-id="ea440-136">So, the connection string format is:</span></span>

    mongodb://username:password@host:port/[database]?ssl=true

<span data-ttu-id="ea440-137">Les valeurs de cette chaîne sont disponibles dans le panneau **Chaîne de connexion** illustré précédemment :</span><span class="sxs-lookup"><span data-stu-id="ea440-137">The values of this string are available in the **Connection String** blade shown earlier:</span></span>

* <span data-ttu-id="ea440-138">Nom d’utilisateur (obligatoire) : nom du compte Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="ea440-138">Username (required): Azure Cosmos DB account name.</span></span>
* <span data-ttu-id="ea440-139">Mot de passe (obligatoire) : mot de passe du compte Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="ea440-139">Password (required): Azure Cosmos DB account password.</span></span>
* <span data-ttu-id="ea440-140">Hôte (obligatoire) : nom de domaine complet (FQDN) du compte Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="ea440-140">Host (required): FQDN of the Azure Cosmos DB account.</span></span>
* <span data-ttu-id="ea440-141">Port (obligatoire) : 10255.</span><span class="sxs-lookup"><span data-stu-id="ea440-141">Port (required): 10255.</span></span>
* <span data-ttu-id="ea440-142">Base de données (facultatif) : base de données utilisée par la connexion.</span><span class="sxs-lookup"><span data-stu-id="ea440-142">Database (optional): The database that the connection uses.</span></span> <span data-ttu-id="ea440-143">Si aucune base de données n’est fournie, la base de données par défaut est « test ».</span><span class="sxs-lookup"><span data-stu-id="ea440-143">If no database is provided, the default database is "test."</span></span>
* <span data-ttu-id="ea440-144">ssl = true (obligatoire)</span><span class="sxs-lookup"><span data-stu-id="ea440-144">ssl=true (required)</span></span>

<span data-ttu-id="ea440-145">Par exemple, observez le compte figurant dans le panneau **Chaîne de connexion**.</span><span class="sxs-lookup"><span data-stu-id="ea440-145">For example, consider the account shown in the **Connection String** blade.</span></span> <span data-ttu-id="ea440-146">Exemple de chaîne de connexion valide :</span><span class="sxs-lookup"><span data-stu-id="ea440-146">A valid connection string is:</span></span>

    mongodb://contoso123:0Fc3IolnL12312asdfawejunASDF@asdfYXX2t8a97kghVcUzcDv98hawelufhawefafnoQRGwNj2nMPL1Y9qsIr9Srdw==@anhohmongo.documents.azure.com:10255/mydatabase?ssl=true

## <a name="next-steps"></a><span data-ttu-id="ea440-147">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ea440-147">Next steps</span></span>
* <span data-ttu-id="ea440-148">Découvrez comment [utiliser MongoChef](mongodb-mongochef.md) avec une API Azure Cosmos DB pour le compte MongoDB.</span><span class="sxs-lookup"><span data-stu-id="ea440-148">Learn how to [use MongoChef](mongodb-mongochef.md) with an Azure Cosmos DB API for MongoDB account.</span></span>
* <span data-ttu-id="ea440-149">Découvrez l’API Azure Cosmos DB pour le compte MongoDB en consultant les [exemples](mongodb-samples.md).</span><span class="sxs-lookup"><span data-stu-id="ea440-149">Explore the Azure Cosmos DB API for MongoDB by viewing [samples](mongodb-samples.md).</span></span>
