---
title: "chaîne de connexion aaaMongoDB pour un compte de base de données Azure Cosmos | Documents Microsoft"
description: "Découvrez comment tooconnect votre tooan d’application MongoDB Azure Cosmos DB compte à l’aide d’une chaîne de connexion MongoDB."
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
ms.openlocfilehash: c0b81cb49a10e09e3f02411b91731c7f980ec47d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-mongodb-application-tooazure-cosmos-db"></a><span data-ttu-id="a99ae-104">Se connecter à un tooAzure d’application MongoDB Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="a99ae-104">Connect a MongoDB application tooAzure Cosmos DB</span></span>
<span data-ttu-id="a99ae-105">Découvrez comment tooconnect votre tooan d’application MongoDB Azure Cosmos DB compte à l’aide d’une chaîne de connexion MongoDB.</span><span class="sxs-lookup"><span data-stu-id="a99ae-105">Learn how tooconnect your MongoDB app tooan Azure Cosmos DB account by using a MongoDB connection string.</span></span> <span data-ttu-id="a99ae-106">Vous pouvez ensuite utiliser une base de données de la base de données Azure Cosmos en tant que données de hello stocker pour votre application MongoDB.</span><span class="sxs-lookup"><span data-stu-id="a99ae-106">You can then use an Azure Cosmos DB database as hello data store for your MongoDB app.</span></span> 

<span data-ttu-id="a99ae-107">Ce didacticiel fournit des informations de chaîne de connexion tooretrieve deux façons :</span><span class="sxs-lookup"><span data-stu-id="a99ae-107">This tutorial provides two ways tooretrieve connection string information:</span></span>

- <span data-ttu-id="a99ae-108">[Hello quick start (méthode)](#QuickstartConnection), pour une utilisation avec les pilotes .NET, Node.js, MongoDB Shell, Java et Python</span><span class="sxs-lookup"><span data-stu-id="a99ae-108">[hello quick start method](#QuickstartConnection), for use with .NET, Node.js, MongoDB Shell, Java, and Python drivers</span></span>
- <span data-ttu-id="a99ae-109">[Hello de méthode de chaîne de connexion personnalisée](#GetCustomConnection), pour une utilisation avec d’autres pilotes</span><span class="sxs-lookup"><span data-stu-id="a99ae-109">[hello custom connection string method](#GetCustomConnection), for use with other drivers</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a99ae-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="a99ae-110">Prerequisites</span></span>

- <span data-ttu-id="a99ae-111">Un compte Azure.</span><span class="sxs-lookup"><span data-stu-id="a99ae-111">An Azure account.</span></span> <span data-ttu-id="a99ae-112">Si vous ne possédez pas de compte Azure, vous pouvez créer un [compte Azure gratuit](https://azure.microsoft.com/free/) dès maintenant.</span><span class="sxs-lookup"><span data-stu-id="a99ae-112">If you don't have an Azure account, create a [free Azure account](https://azure.microsoft.com/free/) now.</span></span> 
- <span data-ttu-id="a99ae-113">Un compte Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="a99ae-113">An Azure Cosmos DB account.</span></span> <span data-ttu-id="a99ae-114">Pour obtenir des instructions, consultez [créer une application web de MongoDB API avec .NET et hello Azure portal](create-mongodb-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="a99ae-114">For instructions, see [Build a MongoDB API web app with .NET and hello Azure portal](create-mongodb-dotnet.md).</span></span>

## <span data-ttu-id="a99ae-115"><a id="QuickstartConnection"></a>Obtenir la chaîne de connexion MongoDB hello à l’aide de démarrage rapide de hello</span><span class="sxs-lookup"><span data-stu-id="a99ae-115"><a id="QuickstartConnection"></a>Get hello MongoDB connection string by using hello quick start</span></span>
1. <span data-ttu-id="a99ae-116">Dans un navigateur Internet, connectez-vous toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a99ae-116">In an Internet browser, sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a99ae-117">Bonjour **base de données Azure Cosmos** panneau, sélectionnez hello des API pour MongoDB compte.</span><span class="sxs-lookup"><span data-stu-id="a99ae-117">In hello **Azure Cosmos DB** blade, select hello API for MongoDB account.</span></span> 
3. <span data-ttu-id="a99ae-118">Dans le volet gauche de hello du Panneau de compte hello, cliquez sur **démarrage rapide**.</span><span class="sxs-lookup"><span data-stu-id="a99ae-118">In hello left pane of hello account blade, click **Quick start**.</span></span> 
4. <span data-ttu-id="a99ae-119">Choisissez votre plateforme (**.NET**, **Node.js**, **MongoDB Shell**, **Java** ou **Python**).</span><span class="sxs-lookup"><span data-stu-id="a99ae-119">Choose your platform (**.NET**, **Node.js**, **MongoDB Shell**, **Java**, **Python**).</span></span> <span data-ttu-id="a99ae-120">Si votre pilote ou outil n’est pas répertorié, ne vous inquiétez pas, nous développons en permanence de nouveaux extraits de code de connexion.</span><span class="sxs-lookup"><span data-stu-id="a99ae-120">If you don't see your driver or tool listed, don't worry--we continuously document more connection code snippets.</span></span> <span data-ttu-id="a99ae-121">Veuillez commenter ci-dessous vous aimeriez toosee.</span><span class="sxs-lookup"><span data-stu-id="a99ae-121">Please comment below on what you'd like toosee.</span></span> <span data-ttu-id="a99ae-122">toolearn comment toocraft votre propre connexion, lecture [obtenir des informations de chaîne de connexion du compte hello](#GetCustomConnection).</span><span class="sxs-lookup"><span data-stu-id="a99ae-122">toolearn how toocraft your own connection, read [Get hello account's connection string information](#GetCustomConnection).</span></span>
5. <span data-ttu-id="a99ae-123">Copiez et collez l’extrait de code hello dans votre application MongoDB.</span><span class="sxs-lookup"><span data-stu-id="a99ae-123">Copy and paste hello code snippet into your MongoDB app.</span></span>

    ![Panneau Démarrage rapide](./media/connect-mongodb-account/QuickStartBlade.png)

## <span data-ttu-id="a99ae-125"><a id="GetCustomConnection"></a>Obtenir toocustomize de chaîne de connexion de MongoDB hello</span><span class="sxs-lookup"><span data-stu-id="a99ae-125"><a id="GetCustomConnection"></a> Get hello MongoDB connection string toocustomize</span></span>
1. <span data-ttu-id="a99ae-126">Dans un navigateur Internet, connectez-vous toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a99ae-126">In an Internet browser, sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a99ae-127">Bonjour **base de données Azure Cosmos** panneau, sélectionnez hello des API pour MongoDB compte.</span><span class="sxs-lookup"><span data-stu-id="a99ae-127">In hello **Azure Cosmos DB** blade, select hello API for MongoDB account.</span></span> 
3. <span data-ttu-id="a99ae-128">Dans le volet gauche de hello du Panneau de compte hello, cliquez sur **chaîne de connexion**.</span><span class="sxs-lookup"><span data-stu-id="a99ae-128">In hello left pane of hello account blade, click **Connection String**.</span></span> 
4. <span data-ttu-id="a99ae-129">Hello **chaîne de connexion** panneau s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="a99ae-129">hello **Connection String** blade opens.</span></span> <span data-ttu-id="a99ae-130">Il a toohello compte de tous les hello informations tooconnect nécessaires à l’aide d’un pilote pour MongoDB, y compris une chaîne de connexion prédéfini.</span><span class="sxs-lookup"><span data-stu-id="a99ae-130">It has all hello information necessary tooconnect toohello account by using a driver for MongoDB, including a preconstructed connection string.</span></span>

    ![Panneau Chaîne de connexion](./media/connect-mongodb-account/ConnectionStringBlade.png)

## <a name="connection-string-requirements"></a><span data-ttu-id="a99ae-132">Exigences relatives à la chaîne de connexion</span><span class="sxs-lookup"><span data-stu-id="a99ae-132">Connection string requirements</span></span>
> [!Important]
> <span data-ttu-id="a99ae-133">Azure Cosmos DB obéit à des normes et à des exigences strictes en matière de sécurité.</span><span class="sxs-lookup"><span data-stu-id="a99ae-133">Azure Cosmos DB has strict security requirements and standards.</span></span> <span data-ttu-id="a99ae-134">Les comptes Azure Cosmos DB requièrent une authentification et une communication sécurisée via *SSL*.</span><span class="sxs-lookup"><span data-stu-id="a99ae-134">Azure Cosmos DB accounts require authentication and secure communication via *SSL*.</span></span> 
>
>

<span data-ttu-id="a99ae-135">Base de données Azure Cosmos prend en charge hello MongoDB connexion chaîne URI format standard, avec quelques exigences spécifiques : comptes de base de données Azure Cosmos requièrent l’authentification et communication sécurisée via SSL.</span><span class="sxs-lookup"><span data-stu-id="a99ae-135">Azure Cosmos DB supports hello standard MongoDB connection string URI format, with a couple of specific requirements: Azure Cosmos DB accounts require authentication and secure communication via SSL.</span></span> <span data-ttu-id="a99ae-136">Par conséquent, le format de chaîne de connexion hello est :</span><span class="sxs-lookup"><span data-stu-id="a99ae-136">So, hello connection string format is:</span></span>

    mongodb://username:password@host:port/[database]?ssl=true

<span data-ttu-id="a99ae-137">les valeurs de cette chaîne Hello sont disponibles dans hello **chaîne de connexion** panneau présentée précédemment :</span><span class="sxs-lookup"><span data-stu-id="a99ae-137">hello values of this string are available in hello **Connection String** blade shown earlier:</span></span>

* <span data-ttu-id="a99ae-138">Nom d’utilisateur (obligatoire) : nom du compte Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="a99ae-138">Username (required): Azure Cosmos DB account name.</span></span>
* <span data-ttu-id="a99ae-139">Mot de passe (obligatoire) : mot de passe du compte Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="a99ae-139">Password (required): Azure Cosmos DB account password.</span></span>
* <span data-ttu-id="a99ae-140">Hôte (obligatoire) : nom de domaine complet de hello compte de base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="a99ae-140">Host (required): FQDN of hello Azure Cosmos DB account.</span></span>
* <span data-ttu-id="a99ae-141">Port (obligatoire) : 10255.</span><span class="sxs-lookup"><span data-stu-id="a99ae-141">Port (required): 10255.</span></span>
* <span data-ttu-id="a99ae-142">Base de données (facultatif) : base de données hello hello connexion utilise.</span><span class="sxs-lookup"><span data-stu-id="a99ae-142">Database (optional): hello database that hello connection uses.</span></span> <span data-ttu-id="a99ae-143">Si aucune base de données n’est fourni, la base de données par défaut hello est « test ».</span><span class="sxs-lookup"><span data-stu-id="a99ae-143">If no database is provided, hello default database is "test."</span></span>
* <span data-ttu-id="a99ae-144">ssl = true (obligatoire)</span><span class="sxs-lookup"><span data-stu-id="a99ae-144">ssl=true (required)</span></span>

<span data-ttu-id="a99ae-145">Par exemple, considérez compte hello hello **chaîne de connexion** panneau.</span><span class="sxs-lookup"><span data-stu-id="a99ae-145">For example, consider hello account shown in hello **Connection String** blade.</span></span> <span data-ttu-id="a99ae-146">Exemple de chaîne de connexion valide :</span><span class="sxs-lookup"><span data-stu-id="a99ae-146">A valid connection string is:</span></span>

    mongodb://contoso123:0Fc3IolnL12312asdfawejunASDF@asdfYXX2t8a97kghVcUzcDv98hawelufhawefafnoQRGwNj2nMPL1Y9qsIr9Srdw==@anhohmongo.documents.azure.com:10255/mydatabase?ssl=true

## <a name="next-steps"></a><span data-ttu-id="a99ae-147">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a99ae-147">Next steps</span></span>
* <span data-ttu-id="a99ae-148">Découvrez comment trop[utiliser MongoChef](mongodb-mongochef.md) avec une API de base de données Azure Cosmos pour MongoDB compte.</span><span class="sxs-lookup"><span data-stu-id="a99ae-148">Learn how too[use MongoChef](mongodb-mongochef.md) with an Azure Cosmos DB API for MongoDB account.</span></span>
* <span data-ttu-id="a99ae-149">Explorer les API de base de données Azure Cosmos de hello pour MongoDB en consultant [exemples](mongodb-samples.md).</span><span class="sxs-lookup"><span data-stu-id="a99ae-149">Explore hello Azure Cosmos DB API for MongoDB by viewing [samples](mongodb-samples.md).</span></span>
