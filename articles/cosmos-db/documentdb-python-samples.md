---
title: "exemples de Python aaaDocumentDB API pour la base de données Azure Cosmos | Documents Microsoft"
description: "Recherchez des exemples Python sur GitHub pour les tâches courantes dans Azure Cosmos DB, y compris les opérations CRUD."
keywords: Exemples Python
services: cosmos-db
author: moderakh
manager: jhubbard
editor: monicar
documentationcenter: python
ms.assetid: 7f4f8db3-e9db-4645-92ef-7819d486a349
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/24/2016
ms.author: moderakh
ms.openlocfilehash: d8f240782b0997f2d32b68d310dc6f4ff6cb36d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-python-examples"></a><span data-ttu-id="d10c6-104">Exemples Python pour Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="d10c6-104">Azure Cosmos DB Python examples</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d10c6-105">Exemples .NET</span><span class="sxs-lookup"><span data-stu-id="d10c6-105">.NET Examples</span></span>](documentdb-dotnet-samples.md)
> * [<span data-ttu-id="d10c6-106">Exemples Node.js</span><span class="sxs-lookup"><span data-stu-id="d10c6-106">Node.js Examples</span></span>](documentdb-nodejs-samples.md)
> * [<span data-ttu-id="d10c6-107">Exemples Python</span><span class="sxs-lookup"><span data-stu-id="d10c6-107">Python Examples</span></span>](documentdb-python-samples.md)
> * [<span data-ttu-id="d10c6-108">Galerie d’exemples de code Azure</span><span class="sxs-lookup"><span data-stu-id="d10c6-108">Azure Code Sample Gallery</span></span>](https://azure.microsoft.com/documentation/samples/?service=documentdb)
> 
> 

<span data-ttu-id="d10c6-109">Exemples de solutions qui effectuent des opérations CRUD et autres opérations courantes sur les ressources de base de données Azure Cosmos sont inclus dans hello [azure-documentdb-python](https://github.com/Azure/azure-documentdb-python/tree/master/samples) référentiel GitHub.</span><span class="sxs-lookup"><span data-stu-id="d10c6-109">Sample solutions that perform CRUD operations and other common operations on Azure Cosmos DB resources are included in hello [azure-documentdb-python](https://github.com/Azure/azure-documentdb-python/tree/master/samples) GitHub repository.</span></span> <span data-ttu-id="d10c6-110">Cet article fournit :</span><span class="sxs-lookup"><span data-stu-id="d10c6-110">This article provides:</span></span>

* <span data-ttu-id="d10c6-111">Tâches toohello de liens dans chacun des fichiers de projet exemple hello Python.</span><span class="sxs-lookup"><span data-stu-id="d10c6-111">Links toohello tasks in each of hello Python example project files.</span></span> 
* <span data-ttu-id="d10c6-112">Liens toohello liés contenu de référence d’API.</span><span class="sxs-lookup"><span data-stu-id="d10c6-112">Links toohello related API reference content.</span></span>

<span data-ttu-id="d10c6-113">**Configuration requise**</span><span class="sxs-lookup"><span data-stu-id="d10c6-113">**Prerequisites**</span></span>

1. <span data-ttu-id="d10c6-114">Vous avez besoin une toouse compte Azure ces exemples Python :</span><span class="sxs-lookup"><span data-stu-id="d10c6-114">You need an Azure account toouse these Python examples:</span></span>
   * <span data-ttu-id="d10c6-115">Vous pouvez [ouvrir un compte Azure gratuitement](https://azure.microsoft.com/pricing/free-trial/): vous obtenez des crédits vous pouvez utiliser tootry à payer des services Azure et même après qu’ils soient utilisés jusqu'à vous pouvez conserver le compte de hello et libérer de l’utilisation des services Azure, comme les sites Web.</span><span class="sxs-lookup"><span data-stu-id="d10c6-115">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/): You get credits you can use tootry out paid Azure services, and even after they're used up you can keep hello account and use free Azure services, such as Websites.</span></span> <span data-ttu-id="d10c6-116">Votre carte de crédit ne sera jamais facturé, sauf si vous explicitement modifiez vos paramètres et demandez toobe facturé.</span><span class="sxs-lookup"><span data-stu-id="d10c6-116">Your credit card will never be charged, unless you explicitly change your settings and ask toobe charged.</span></span>
     * <span data-ttu-id="d10c6-117">Vous pouvez [activer les avantages de votre abonnement Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/): ce dernier vous donne droit chaque mois à des crédits dont vous pouvez vous servir pour les services Azure payants.</span><span class="sxs-lookup"><span data-stu-id="d10c6-117">You can [activate Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/): Your Visual Studio subscription gives you credits every month that you can use for paid Azure services.</span></span>
2. <span data-ttu-id="d10c6-118">Vous devez également hello [Python SDK](documentdb-sdk-python.md).</span><span class="sxs-lookup"><span data-stu-id="d10c6-118">You also need hello [Python SDK](documentdb-sdk-python.md).</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="d10c6-119">Chaque exemple est autonome, se définit lui-même et se nettoie automatiquement.</span><span class="sxs-lookup"><span data-stu-id="d10c6-119">Each sample is self-contained, it sets itself up and cleans up after itself.</span></span> <span data-ttu-id="d10c6-120">Par conséquent, les exemples hello émettre plusieurs appels trop[document_client. CreateCollection](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html).</span><span class="sxs-lookup"><span data-stu-id="d10c6-120">As such, hello samples issue multiple calls too[document_client.CreateCollection](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html).</span></span> <span data-ttu-id="d10c6-121">Chaque fois que cela est fait à votre abonnement sera facturé pour une heure de l’utilisation par le niveau de performances de hello de collection hello en cours de création.</span><span class="sxs-lookup"><span data-stu-id="d10c6-121">Each time this is done your subscription will be billed for 1 hour of usage per hello performance tier of hello collection being created.</span></span> 
   > 
   > 

## <a name="database-examples"></a><span data-ttu-id="d10c6-122">Exemples de base de données</span><span class="sxs-lookup"><span data-stu-id="d10c6-122">Database examples</span></span>
<span data-ttu-id="d10c6-123">Hello [Program.py](https://github.com/Azure/azure-documentdb-python/tree/master/samples/DatabaseManagement/Program.py) fichier Hello [DatabaseManagement](https://github.com/Azure/azure-documentdb-python/tree/master/samples/DatabaseManagement) projet présente des tâches de hello tooperform suivant.</span><span class="sxs-lookup"><span data-stu-id="d10c6-123">hello [Program.py](https://github.com/Azure/azure-documentdb-python/tree/master/samples/DatabaseManagement/Program.py) file of hello [DatabaseManagement](https://github.com/Azure/azure-documentdb-python/tree/master/samples/DatabaseManagement) project shows how tooperform hello following tasks.</span></span>

| <span data-ttu-id="d10c6-124">Task</span><span class="sxs-lookup"><span data-stu-id="d10c6-124">Task</span></span> | <span data-ttu-id="d10c6-125">Informations de référence sur l'API</span><span class="sxs-lookup"><span data-stu-id="d10c6-125">API reference</span></span> |
| --- | --- |
| [<span data-ttu-id="d10c6-126">Créer une base de données</span><span class="sxs-lookup"><span data-stu-id="d10c6-126">Create a database</span></span>](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/DatabaseManagement/Program.py#L65-L76) |[<span data-ttu-id="d10c6-127">document_client.CreateDatabase</span><span class="sxs-lookup"><span data-stu-id="d10c6-127">document_client.CreateDatabase</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html) |
| [<span data-ttu-id="d10c6-128">Demander un compte pour une base de données</span><span class="sxs-lookup"><span data-stu-id="d10c6-128">Query an account for a database</span></span>](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/DatabaseManagement/Program.py#L49-L62) |[<span data-ttu-id="d10c6-129">document_client.QueryDatabases</span><span class="sxs-lookup"><span data-stu-id="d10c6-129">document_client.QueryDatabases</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html) |
| [<span data-ttu-id="d10c6-130">Lire une base de données par identifiant</span><span class="sxs-lookup"><span data-stu-id="d10c6-130">Read a database by Id</span></span>](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/DatabaseManagement/Program.py#L79-L96) |[<span data-ttu-id="d10c6-131">document_client.ReadDatabase</span><span class="sxs-lookup"><span data-stu-id="d10c6-131">document_client.ReadDatabase</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html) |
| [<span data-ttu-id="d10c6-132">Répertorier les bases de données pour un compte</span><span class="sxs-lookup"><span data-stu-id="d10c6-132">List databases for an account</span></span>](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/DatabaseManagement/Program.py#L99-L110) |[<span data-ttu-id="d10c6-133">document_client.ReadDatabases</span><span class="sxs-lookup"><span data-stu-id="d10c6-133">document_client.ReadDatabases</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html) |
| [<span data-ttu-id="d10c6-134">Supprimer une base de données</span><span class="sxs-lookup"><span data-stu-id="d10c6-134">Delete a database</span></span>](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/DatabaseManagement/Program.py#L113-L126) |[<span data-ttu-id="d10c6-135">document_client.DeleteDatabase</span><span class="sxs-lookup"><span data-stu-id="d10c6-135">document_client.DeleteDatabase</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html) |

## <a name="collection-examples"></a><span data-ttu-id="d10c6-136">Exemples de collection</span><span class="sxs-lookup"><span data-stu-id="d10c6-136">Collection examples</span></span>
<span data-ttu-id="d10c6-137">Hello [Program.py](https://github.com/Azure/azure-documentdb-python/tree/master/samples/CollectionManagement/Program.py) fichier Hello [CollectionManagement](https://github.com/Azure/azure-documentdb-python/tree/master/samples/CollectionManagement) projet présente des tâches de hello tooperform suivant.</span><span class="sxs-lookup"><span data-stu-id="d10c6-137">hello [Program.py](https://github.com/Azure/azure-documentdb-python/tree/master/samples/CollectionManagement/Program.py) file of hello [CollectionManagement](https://github.com/Azure/azure-documentdb-python/tree/master/samples/CollectionManagement) project shows how tooperform hello following tasks.</span></span>

| <span data-ttu-id="d10c6-138">Task</span><span class="sxs-lookup"><span data-stu-id="d10c6-138">Task</span></span> | <span data-ttu-id="d10c6-139">Informations de référence sur l'API</span><span class="sxs-lookup"><span data-stu-id="d10c6-139">API reference</span></span> |
| --- | --- |
| [<span data-ttu-id="d10c6-140">Création d'une collection</span><span class="sxs-lookup"><span data-stu-id="d10c6-140">Create a collection</span></span>](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L84-L135) |[<span data-ttu-id="d10c6-141">document_client.CreateCollection</span><span class="sxs-lookup"><span data-stu-id="d10c6-141">document_client.CreateCollection</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |
| [<span data-ttu-id="d10c6-142">Lire une liste de toutes les collections d’une base de données</span><span class="sxs-lookup"><span data-stu-id="d10c6-142">Read a list of all collections in a database</span></span>](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L198-L225) |[<span data-ttu-id="d10c6-143">document_client.ListCollections</span><span class="sxs-lookup"><span data-stu-id="d10c6-143">document_client.ListCollections</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |
| [<span data-ttu-id="d10c6-144">Obtenir une collection par identifiant</span><span class="sxs-lookup"><span data-stu-id="d10c6-144">Get a collection by Id</span></span>](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L178-L195) |[<span data-ttu-id="d10c6-145">document_client.ReadCollection</span><span class="sxs-lookup"><span data-stu-id="d10c6-145">document_client.ReadCollection</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |
| [<span data-ttu-id="d10c6-146">Obtenir le niveau de performances d’une collection</span><span class="sxs-lookup"><span data-stu-id="d10c6-146">Get performance tier of a collection</span></span>](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L139-L161) |[<span data-ttu-id="d10c6-147">DocumentQueryable.QueryOffers</span><span class="sxs-lookup"><span data-stu-id="d10c6-147">DocumentQueryable.QueryOffers</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |
| [<span data-ttu-id="d10c6-148">Modifier le niveau de performances d’une collection</span><span class="sxs-lookup"><span data-stu-id="d10c6-148">Change performance tier of a collection</span></span>](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L163-L175) |[<span data-ttu-id="d10c6-149">document_client.ReplaceOffer</span><span class="sxs-lookup"><span data-stu-id="d10c6-149">document_client.ReplaceOffer</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |
| [<span data-ttu-id="d10c6-150">Supprimer une collection</span><span class="sxs-lookup"><span data-stu-id="d10c6-150">Delete a collection</span></span>](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L212-L225) |[<span data-ttu-id="d10c6-151">document_client.DeleteCollection</span><span class="sxs-lookup"><span data-stu-id="d10c6-151">document_client.DeleteCollection</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |
