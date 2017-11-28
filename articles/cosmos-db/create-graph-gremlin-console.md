---
title: "Didacticiel Azure Cosmos DB : Créer, interroger et parcourir la console Apache TinkerPops Gremlin | Microsoft Docs"
description: "Démarrage rapide d’Azure Cosmos DB pour créer des vertex, des bords et des requêtes à l’aide de l’API Graph Azure Cosmos DB."
services: cosmos-db
author: dennyglee
manager: jhubbard
editor: monicar
ms.assetid: bf08e031-718a-4a2a-89d6-91e12ff8797d
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: terminal
ms.topic: hero-article
ms.date: 07/27/2017
ms.author: denlee
ms.openlocfilehash: fd5cc93ce1ed2a8c7da090666ef539b338ac61c3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-cosmos-db-create-query-and-traverse-a-graph-in-the-gremlin-console"></a><span data-ttu-id="47631-103">Azure Cosmos DB : Créer, interroger et parcourir la console Gremlin</span><span class="sxs-lookup"><span data-stu-id="47631-103">Azure Cosmos DB: Create, query, and traverse a graph in the Gremlin console</span></span>

<span data-ttu-id="47631-104">Azure Cosmos DB est le service de base de données multi-modèle de Microsoft distribué à l’échelle mondiale.</span><span class="sxs-lookup"><span data-stu-id="47631-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="47631-105">Rapidement, vous avez la possibilité de créer et d’interroger des documents, des paires clé/valeur, et des bases de données orientées graphe, profitant tous de la distribution à l’échelle mondiale et des capacités de mise à l’échelle horizontale au cœur d’Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="47631-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="47631-106">Ce guide de démarrage rapide explique comment créer, à l’aide du portail Azure, un compte Azure Cosmos DB, une base de données, ainsi qu’un graphique (conteneur) et comment utiliser ensuite la [console Gremlin](https://tinkerpop.apache.org/docs/current/reference/#gremlin-console) à partir d’[Apache TinkerPop](http://tinkerpop.apache.org) pour travailler avec les données API Graph (version préliminaire).</span><span class="sxs-lookup"><span data-stu-id="47631-106">This quick start demonstrates how to create an Azure Cosmos DB account, database, and graph (container) using the Azure portal and then use the [Gremlin Console](https://tinkerpop.apache.org/docs/current/reference/#gremlin-console) from  [Apache TinkerPop](http://tinkerpop.apache.org) to work with Graph API (preview) data.</span></span> <span data-ttu-id="47631-107">Dans ce didacticiel, vous créez et interrogez des vertex et des bords, mettez à jour une propriété de vertex, interrogez des vertex, parcourez le graphique et supprimez un vertex.</span><span class="sxs-lookup"><span data-stu-id="47631-107">In this tutorial, you create and query vertices and edges, updating a vertex property, query vertices, traverse the graph, and drop a vertex.</span></span>

![Azure Cosmos DB à partir de la console Apache Gremlin](./media/create-graph-gremlin-console/gremlin-console.png)

<span data-ttu-id="47631-109">La console Gremlin est basée sur Groovy/Java et s’exécute sous Linux, Mac et Windows.</span><span class="sxs-lookup"><span data-stu-id="47631-109">The Gremlin console is Groovy/Java based and runs on Linux, Mac, and Windows.</span></span> <span data-ttu-id="47631-110">Vous pouvez la télécharger à partir du [site Apache TinkerPop](https://www.apache.org/dyn/closer.lua/tinkerpop/3.2.5/apache-tinkerpop-gremlin-console-3.2.5-bin.zip).</span><span class="sxs-lookup"><span data-stu-id="47631-110">You can download it from the [Apache TinkerPop site](https://www.apache.org/dyn/closer.lua/tinkerpop/3.2.5/apache-tinkerpop-gremlin-console-3.2.5-bin.zip).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="47631-111">Composants requis</span><span class="sxs-lookup"><span data-stu-id="47631-111">Prerequisites</span></span>

<span data-ttu-id="47631-112">Vous devez posséder un abonnement Azure pour créer un compte Azure Cosmos DB pour ce démarrage rapide.</span><span class="sxs-lookup"><span data-stu-id="47631-112">You need to have an Azure subscription to create an Azure Cosmos DB account for this quickstart.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

<span data-ttu-id="47631-113">Vous devez également installer la [console Gremlin](http://tinkerpop.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="47631-113">You also need to install the [Gremlin Console](http://tinkerpop.apache.org/).</span></span> <span data-ttu-id="47631-114">Utilisez la version 3.2.5 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="47631-114">Use version 3.2.5 or above.</span></span>

## <a name="create-a-database-account"></a><span data-ttu-id="47631-115">Création d'un compte de base de données</span><span class="sxs-lookup"><span data-stu-id="47631-115">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a name="add-a-graph"></a><span data-ttu-id="47631-116">Ajout d’un graphique</span><span class="sxs-lookup"><span data-stu-id="47631-116">Add a graph</span></span>

[!INCLUDE [cosmos-db-create-graph](../../includes/cosmos-db-create-graph.md)]

## <span data-ttu-id="47631-117"><a id="ConnectAppService"></a>Connexion à votre App Service</span><span class="sxs-lookup"><span data-stu-id="47631-117"><a id="ConnectAppService"></a>Connect to your app service</span></span>
1. <span data-ttu-id="47631-118">Avant de démarrer la console Gremlin, créez ou modifiez le fichier config remote-secure.yaml dans le répertoire apache-tinkerpop-gremlin-console-3.2.5/conf.</span><span class="sxs-lookup"><span data-stu-id="47631-118">Before starting the Gremlin Console, create or modify the remote-secure.yaml configuration file in the apache-tinkerpop-gremlin-console-3.2.5/conf directory.</span></span>
2. <span data-ttu-id="47631-119">Renseignez vos configurations *hôte*, *port*, *nom d’utilisateur*, *mot de passe*, *connectionPool* et *sérialiseur* :</span><span class="sxs-lookup"><span data-stu-id="47631-119">Fill in your *host*, *port*, *username*, *password*, *connectionPool*, and *serializer* configurations:</span></span>

    <span data-ttu-id="47631-120">Paramètre</span><span class="sxs-lookup"><span data-stu-id="47631-120">Setting</span></span>|<span data-ttu-id="47631-121">Valeur suggérée</span><span class="sxs-lookup"><span data-stu-id="47631-121">Suggested value</span></span>|<span data-ttu-id="47631-122">Description</span><span class="sxs-lookup"><span data-stu-id="47631-122">Description</span></span>
    ---|---|---
    <span data-ttu-id="47631-123">hôtes</span><span class="sxs-lookup"><span data-stu-id="47631-123">hosts</span></span>|<span data-ttu-id="47631-124">[***.graphs.azure.com]</span><span class="sxs-lookup"><span data-stu-id="47631-124">[***.graphs.azure.com]</span></span>|<span data-ttu-id="47631-125">Reportez-vous à la capture d’écran ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="47631-125">See screenshot below.</span></span> <span data-ttu-id="47631-126">Il s’agit de la valeur URI Gremlin sur la page Vue d’ensemble du portail Azure, entre crochets, avec la fin : 443/ supprimée.</span><span class="sxs-lookup"><span data-stu-id="47631-126">This is the Gremlin URI value on the Overview page of the Azure portal, in square brackets, with the trailing :443/ removed.</span></span><br><br><span data-ttu-id="47631-127">Cette valeur peut également être récupérée à partir de l’onglet Clés, à l’aide de la valeur URI, en supprimant https://, en changeant les documents en graphiques et en supprimant la fin : 443/.</span><span class="sxs-lookup"><span data-stu-id="47631-127">This value can also be retrieved from the Keys tab, using the URI value by removing https://, changing documents to graphs, and removing the trailing :443/.</span></span>
    <span data-ttu-id="47631-128">port</span><span class="sxs-lookup"><span data-stu-id="47631-128">port</span></span>|<span data-ttu-id="47631-129">443</span><span class="sxs-lookup"><span data-stu-id="47631-129">443</span></span>|<span data-ttu-id="47631-130">Définissez la valeur sur 443.</span><span class="sxs-lookup"><span data-stu-id="47631-130">Set to 443.</span></span>
    <span data-ttu-id="47631-131">username</span><span class="sxs-lookup"><span data-stu-id="47631-131">username</span></span>|<span data-ttu-id="47631-132">*Votre nom d’utilisateur*</span><span class="sxs-lookup"><span data-stu-id="47631-132">*Your username*</span></span>|<span data-ttu-id="47631-133">Ressource sous la forme `/dbs/<db>/colls/<coll>`, où `<db>` est le nom de votre base de données et `<coll>` le nom de votre collection.</span><span class="sxs-lookup"><span data-stu-id="47631-133">The resource of the form `/dbs/<db>/colls/<coll>` where `<db>` is your database name and `<coll>` is your collection name.</span></span>
    <span data-ttu-id="47631-134">password</span><span class="sxs-lookup"><span data-stu-id="47631-134">password</span></span>|<span data-ttu-id="47631-135">*Votre clé primaire*</span><span class="sxs-lookup"><span data-stu-id="47631-135">*Your primary key*</span></span>| <span data-ttu-id="47631-136">Reportez-vous à la deuxième capture d’écran ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="47631-136">See second screenshot below.</span></span> <span data-ttu-id="47631-137">Il s’agit de votre clé primaire, que vous pouvez récupérer à partir de la page Clés du portail Azure, dans la zone Clé primaire.</span><span class="sxs-lookup"><span data-stu-id="47631-137">This is your primary key, which you can retrieve from the Keys page of the Azure portal, in the Primary Key box.</span></span> <span data-ttu-id="47631-138">Utilisez le bouton Copier sur le côté gauche de la zone pour copier la valeur.</span><span class="sxs-lookup"><span data-stu-id="47631-138">Use the copy button on the left side of the box to copy the value.</span></span>
    <span data-ttu-id="47631-139">connectionPool</span><span class="sxs-lookup"><span data-stu-id="47631-139">connectionPool</span></span>|<span data-ttu-id="47631-140">{enableSsl: true}</span><span class="sxs-lookup"><span data-stu-id="47631-140">{enableSsl: true}</span></span>|<span data-ttu-id="47631-141">Votre paramètre de pool de connexions pour SSL.</span><span class="sxs-lookup"><span data-stu-id="47631-141">Your connection pool setting for SSL.</span></span>
    <span data-ttu-id="47631-142">serializer</span><span class="sxs-lookup"><span data-stu-id="47631-142">serializer</span></span>|<span data-ttu-id="47631-143">{ className: org.apache.tinkerpop.gremlin.</span><span class="sxs-lookup"><span data-stu-id="47631-143">{ className: org.apache.tinkerpop.gremlin.</span></span><br><span data-ttu-id="47631-144">driver.ser.GraphSONMessageSerializerV1d0,</span><span class="sxs-lookup"><span data-stu-id="47631-144">driver.ser.GraphSONMessageSerializerV1d0,</span></span><br> <span data-ttu-id="47631-145">config: {serializeResultToString: true }}</span><span class="sxs-lookup"><span data-stu-id="47631-145">config: { serializeResultToString: true }}</span></span>|<span data-ttu-id="47631-146">Définissez le paramètre sur cette valeur et supprimez tous les sauts de ligne `\n` quand vous collez la valeur.</span><span class="sxs-lookup"><span data-stu-id="47631-146">Set to this value and delete any `\n` line breaks when pasting in the value.</span></span>

    <span data-ttu-id="47631-147">Pour la valeur hôtes, copiez la valeur **URI Gremlin** à partir de la page **Vue d’ensemble** : ![Afficher et copier la valeur URI Gremlin sur la page Vue d’ensemble dans le portail Azure](./media/create-graph-gremlin-console/gremlin-uri.png)</span><span class="sxs-lookup"><span data-stu-id="47631-147">For the hosts value, copy the **Gremlin URI** value from the **Overview** page: ![View and copy the Gremlin URI value on the Overview page in the Azure portal](./media/create-graph-gremlin-console/gremlin-uri.png)</span></span>

    <span data-ttu-id="47631-148">Pour la valeur Mot de passe, copiez la **clé primaire** dans la page **Clés** : ![Afficher et copier votre clé primaire dans le portail Azure, la page Clés](./media/create-graph-gremlin-console/keys.png)</span><span class="sxs-lookup"><span data-stu-id="47631-148">For the password value, copy the **Primary key** from the **Keys** page: ![View and copy your primary key in the Azure portal, Keys page](./media/create-graph-gremlin-console/keys.png)</span></span>


3. <span data-ttu-id="47631-149">Dans votre terminal, exécutez `bin/gremlin.bat` ou `bin/gremlin.sh` pour démarrer la [console Gremlin](http://tinkerpop.apache.org/docs/3.2.5/tutorials/getting-started/).</span><span class="sxs-lookup"><span data-stu-id="47631-149">In your terminal, run `bin/gremlin.bat` or `bin/gremlin.sh` to start the [Gremlin Console](http://tinkerpop.apache.org/docs/3.2.5/tutorials/getting-started/).</span></span>
4. <span data-ttu-id="47631-150">Dans votre terminal, exécutez `:remote connect tinkerpop.server conf/remote-secure.yaml` pour vous connecter à votre service d’application.</span><span class="sxs-lookup"><span data-stu-id="47631-150">In your terminal, run `:remote connect tinkerpop.server conf/remote-secure.yaml` to connect to your app service.</span></span>

    > [!TIP]
    > <span data-ttu-id="47631-151">Si vous recevez l’erreur `No appenders could be found for logger`, vérifiez que vous avez mis à jour la valeur de sérialiseur dans le fichier remote-secure.yaml comme décrit à l’étape 2.</span><span class="sxs-lookup"><span data-stu-id="47631-151">If you receive the error `No appenders could be found for logger` ensure that you updated the serializer value in the remote-secure.yaml file as described in step 2.</span></span> 

<span data-ttu-id="47631-152">Parfait !</span><span class="sxs-lookup"><span data-stu-id="47631-152">Great!</span></span> <span data-ttu-id="47631-153">L’installation étant terminée, exécutons quelques commandes de console.</span><span class="sxs-lookup"><span data-stu-id="47631-153">Now that we finished the setup, let's start running some console commands.</span></span>

<span data-ttu-id="47631-154">Essayons une simple commande count().</span><span class="sxs-lookup"><span data-stu-id="47631-154">Let's try a simple count() command.</span></span> <span data-ttu-id="47631-155">Lorsque l’invite de commandes s’affiche, saisissez ce qui suit dans la console :</span><span class="sxs-lookup"><span data-stu-id="47631-155">Type the following into the console at the prompt:</span></span>
```
:> g.V().count()
```

> [!TIP]
> <span data-ttu-id="47631-156">Avez-vous remarqué le signe `:>` qui précède le texte `g.V().count()` ?</span><span class="sxs-lookup"><span data-stu-id="47631-156">Notice the `:>` that precedes the `g.V().count()` text?</span></span> 
>
> <span data-ttu-id="47631-157">il indique la partie de la commande que vous devez saisir.</span><span class="sxs-lookup"><span data-stu-id="47631-157">This is part of the command you need to type.</span></span> <span data-ttu-id="47631-158">Ce signe est important lorsque vous utilisez la console Gremlin avec Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="47631-158">It is important when using the Gremlin console, with Azure Cosmos DB.</span></span>  
>
> <span data-ttu-id="47631-159">Si vous n’indiquez pas ce préfixe `:>`, la console doit exécuter la commande en local, le plus souvent sur un graphique en mémoire.</span><span class="sxs-lookup"><span data-stu-id="47631-159">Omitting this `:>` prefix instructs the console to execute the command locally, often against an in-memory graph.</span></span>
> <span data-ttu-id="47631-160">L’utilisation du signe `:>` indique à la console qu’elle doit exécuter une commande à distance, sur Cosmos DB (l’émulateur localhost ou une instance >Azure) dans le cas présent.</span><span class="sxs-lookup"><span data-stu-id="47631-160">Using this `:>` tells the console to execute a remote command, in this case against Cosmos DB (either the localhost emulator, or an > Azure instance).</span></span>


## <a name="create-vertices-and-edges"></a><span data-ttu-id="47631-161">Création de vertex et de bords</span><span class="sxs-lookup"><span data-stu-id="47631-161">Create vertices and edges</span></span>

<span data-ttu-id="47631-162">Commençons par ajouter des vertex pour cinq personnes : *Thomas*, *Mary Kay*, *Robin*, *Ben* et *Jack*.</span><span class="sxs-lookup"><span data-stu-id="47631-162">Let's begin by adding five person vertices for *Thomas*, *Mary Kay*, *Robin*, *Ben*, and *Jack*.</span></span>

<span data-ttu-id="47631-163">Entrée (Thomas) :</span><span class="sxs-lookup"><span data-stu-id="47631-163">Input (Thomas):</span></span>

```
:> g.addV('person').property('firstName', 'Thomas').property('lastName', 'Andersen').property('age', 44).property('userid', 1)
```

<span data-ttu-id="47631-164">Output:</span><span class="sxs-lookup"><span data-stu-id="47631-164">Output:</span></span>

```
==>[id:796cdccc-2acd-4e58-a324-91d6f6f5ed6d,label:person,type:vertex,properties:[firstName:[[id:f02a749f-b67c-4016-850e-910242d68953,value:Thomas]],lastName:[[id:f5fa3126-8818-4fda-88b0-9bb55145ce5c,value:Andersen]],age:[[id:f6390f9c-e563-433e-acbf-25627628016e,value:44]],userid:[[id:796cdccc-2acd-4e58-a324-91d6f6f5ed6d|userid,value:1]]]]
```
<span data-ttu-id="47631-165">Entrée (Mary Kay) :</span><span class="sxs-lookup"><span data-stu-id="47631-165">Input (Mary Kay):</span></span>

```
:> g.addV('person').property('firstName', 'Mary Kay').property('lastName', 'Andersen').property('age', 39).property('userid', 2)

```

<span data-ttu-id="47631-166">Output:</span><span class="sxs-lookup"><span data-stu-id="47631-166">Output:</span></span>

```
==>[id:0ac9be25-a476-4a30-8da8-e79f0119ea5e,label:person,type:vertex,properties:[firstName:[[id:ea0604f8-14ee-4513-a48a-1734a1f28dc0,value:Mary Kay]],lastName:[[id:86d3bba5-fd60-4856-9396-c195ef7d7f4b,value:Andersen]],age:[[id:bc81b78d-30c4-4e03-8f40-50f72eb5f6da,value:39]],userid:[[id:0ac9be25-a476-4a30-8da8-e79f0119ea5e|userid,value:2]]]]

```

<span data-ttu-id="47631-167">Entrée (Robin) :</span><span class="sxs-lookup"><span data-stu-id="47631-167">Input (Robin):</span></span>

```
:> g.addV('person').property('firstName', 'Robin').property('lastName', 'Wakefield').property('userid', 3)
```

<span data-ttu-id="47631-168">Output:</span><span class="sxs-lookup"><span data-stu-id="47631-168">Output:</span></span>

```
==>[id:8dc14d6a-8683-4a54-8d74-7eef1fb43a3e,label:person,type:vertex,properties:[firstName:[[id:ec65f078-7a43-4cbe-bc06-e50f2640dc4e,value:Robin]],lastName:[[id:a3937d07-0e88-45d3-a442-26fcdfb042ce,value:Wakefield]],userid:[[id:8dc14d6a-8683-4a54-8d74-7eef1fb43a3e|userid,value:3]]]]
```

<span data-ttu-id="47631-169">Entrée (Ben) :</span><span class="sxs-lookup"><span data-stu-id="47631-169">Input (Ben):</span></span>

```
:> g.addV('person').property('firstName', 'Ben').property('lastName', 'Miller').property('userid', 4)

```

<span data-ttu-id="47631-170">Output:</span><span class="sxs-lookup"><span data-stu-id="47631-170">Output:</span></span>

```
==>[id:ee86b670-4d24-4966-9a39-30529284b66f,label:person,type:vertex,properties:[firstName:[[id:a632469b-30fc-4157-840c-b80260871e9a,value:Ben]],lastName:[[id:4a08d307-0719-47c6-84ae-1b0b06630928,value:Miller]],userid:[[id:ee86b670-4d24-4966-9a39-30529284b66f|userid,value:4]]]]
```

<span data-ttu-id="47631-171">Entrée (Jack) :</span><span class="sxs-lookup"><span data-stu-id="47631-171">Input (Jack):</span></span>

```
:> g.addV('person').property('firstName', 'Jack').property('lastName', 'Connor').property('userid', 5)
```

<span data-ttu-id="47631-172">Output:</span><span class="sxs-lookup"><span data-stu-id="47631-172">Output:</span></span>

```
==>[id:4c835f2a-ea5b-43bb-9b6b-215488ad8469,label:person,type:vertex,properties:[firstName:[[id:4250824e-4b72-417f-af98-8034aa15559f,value:Jack]],lastName:[[id:44c1d5e1-a831-480a-bf94-5167d133549e,value:Connor]],userid:[[id:4c835f2a-ea5b-43bb-9b6b-215488ad8469|userid,value:5]]]]
```


<span data-ttu-id="47631-173">Ensuite, ajoutons des bords pour les relations entre ces personnes.</span><span class="sxs-lookup"><span data-stu-id="47631-173">Next, let's add edges for relationships between our people.</span></span>

<span data-ttu-id="47631-174">Entrée (Thomas -> Mary Kay) :</span><span class="sxs-lookup"><span data-stu-id="47631-174">Input (Thomas -> Mary Kay):</span></span>

```
:> g.V().hasLabel('person').has('firstName', 'Thomas').addE('knows').to(g.V().hasLabel('person').has('firstName', 'Mary Kay'))
```

<span data-ttu-id="47631-175">Output:</span><span class="sxs-lookup"><span data-stu-id="47631-175">Output:</span></span>

```
==>[id:c12bf9fb-96a1-4cb7-a3f8-431e196e702f,label:knows,type:edge,inVLabel:person,outVLabel:person,inV:0d1fa428-780c-49a5-bd3a-a68d96391d5c,outV:1ce821c6-aa3d-4170-a0b7-d14d2a4d18c3]
```

<span data-ttu-id="47631-176">Entrée (Thomas -> Robin) :</span><span class="sxs-lookup"><span data-stu-id="47631-176">Input (Thomas -> Robin):</span></span>

```
:> g.V().hasLabel('person').has('firstName', 'Thomas').addE('knows').to(g.V().hasLabel('person').has('firstName', 'Robin'))
```

<span data-ttu-id="47631-177">Output:</span><span class="sxs-lookup"><span data-stu-id="47631-177">Output:</span></span>

```
==>[id:58319bdd-1d3e-4f17-a106-0ddf18719d15,label:knows,type:edge,inVLabel:person,outVLabel:person,inV:3e324073-ccfc-4ae1-8675-d450858ca116,outV:1ce821c6-aa3d-4170-a0b7-d14d2a4d18c3]
```

<span data-ttu-id="47631-178">Entrée (Robin -> Ben) :</span><span class="sxs-lookup"><span data-stu-id="47631-178">Input (Robin -> Ben):</span></span>

```
:> g.V().hasLabel('person').has('firstName', 'Robin').addE('knows').to(g.V().hasLabel('person').has('firstName', 'Ben'))
```

<span data-ttu-id="47631-179">Output:</span><span class="sxs-lookup"><span data-stu-id="47631-179">Output:</span></span>

```
==>[id:889c4d3c-549e-4d35-bc21-a3d1bfa11e00,label:knows,type:edge,inVLabel:person,outVLabel:person,inV:40fd641d-546e-412a-abcc-58fe53891aab,outV:3e324073-ccfc-4ae1-8675-d450858ca116]
```

## <a name="update-a-vertex"></a><span data-ttu-id="47631-180">Mise à jour d’un vertex</span><span class="sxs-lookup"><span data-stu-id="47631-180">Update a vertex</span></span>

<span data-ttu-id="47631-181">Nous allons mettre à jour le vertex *Thomas* avec un nouvel âge : *45*.</span><span class="sxs-lookup"><span data-stu-id="47631-181">Let's update the *Thomas* vertex with a new age of *45*.</span></span>

<span data-ttu-id="47631-182">Entrée :</span><span class="sxs-lookup"><span data-stu-id="47631-182">Input:</span></span>
```
:> g.V().hasLabel('person').has('firstName', 'Thomas').property('age', 45)
```
<span data-ttu-id="47631-183">Output:</span><span class="sxs-lookup"><span data-stu-id="47631-183">Output:</span></span>

```
==>[id:ae36f938-210e-445a-92df-519f2b64c8ec,label:person,type:vertex,properties:[firstName:[[id:872090b6-6a77-456a-9a55-a59141d4ebc2,value:Thomas]],lastName:[[id:7ee7a39a-a414-4127-89b4-870bc4ef99f3,value:Andersen]],age:[[id:a2a75d5a-ae70-4095-806d-a35abcbfe71d,value:45]]]]
```

## <a name="query-your-graph"></a><span data-ttu-id="47631-184">Interrogation de votre graphique</span><span class="sxs-lookup"><span data-stu-id="47631-184">Query your graph</span></span>

<span data-ttu-id="47631-185">À présent, exécutons différentes requêtes sur votre graphique.</span><span class="sxs-lookup"><span data-stu-id="47631-185">Now, let's run a variety of queries against your graph.</span></span>

<span data-ttu-id="47631-186">Tout d’abord, essayons une requête avec un filtre pour retourner uniquement les personnes de plus de 40 ans.</span><span class="sxs-lookup"><span data-stu-id="47631-186">First, let's try a query with a filter to return only people who are older than 40 years old.</span></span>

<span data-ttu-id="47631-187">Entrée (requête de filtre) :</span><span class="sxs-lookup"><span data-stu-id="47631-187">Input (filter query):</span></span>

```
:> g.V().hasLabel('person').has('age', gt(40))
```

<span data-ttu-id="47631-188">Output:</span><span class="sxs-lookup"><span data-stu-id="47631-188">Output:</span></span>

```
==>[id:ae36f938-210e-445a-92df-519f2b64c8ec,label:person,type:vertex,properties:[firstName:[[id:872090b6-6a77-456a-9a55-a59141d4ebc2,value:Thomas]],lastName:[[id:7ee7a39a-a414-4127-89b4-870bc4ef99f3,value:Andersen]],age:[[id:a2a75d5a-ae70-4095-806d-a35abcbfe71d,value:45]]]]
```

<span data-ttu-id="47631-189">Ensuite, projetons le premier nom parmi les personnes de plus de 40 ans.</span><span class="sxs-lookup"><span data-stu-id="47631-189">Next, let's project the first name for the people who are older than 40 years old.</span></span>

<span data-ttu-id="47631-190">Entrée (filtre + requête de projection) :</span><span class="sxs-lookup"><span data-stu-id="47631-190">Input (filter + projection query):</span></span>

```
:> g.V().hasLabel('person').has('age', gt(40)).values('firstName')
```

<span data-ttu-id="47631-191">Output:</span><span class="sxs-lookup"><span data-stu-id="47631-191">Output:</span></span>

```
==>Thomas
```

## <a name="traverse-your-graph"></a><span data-ttu-id="47631-192">Traversée du graphique</span><span class="sxs-lookup"><span data-stu-id="47631-192">Traverse your graph</span></span>

<span data-ttu-id="47631-193">Parcourons le graphique pour retourner tous les amis de Thomas.</span><span class="sxs-lookup"><span data-stu-id="47631-193">Let's traverse the graph to return all of Thomas's friends.</span></span>

<span data-ttu-id="47631-194">Entrée (amis de Thomas) :</span><span class="sxs-lookup"><span data-stu-id="47631-194">Input (friends of Thomas):</span></span>

```
:> g.V().hasLabel('person').has('firstName', 'Thomas').outE('knows').inV().hasLabel('person')
```

<span data-ttu-id="47631-195">Output:</span><span class="sxs-lookup"><span data-stu-id="47631-195">Output:</span></span> 

```
==>[id:f04bc00b-cb56-46c4-a3bb-a5870c42f7ff,label:person,type:vertex,properties:[firstName:[[id:14feedec-b070-444e-b544-62be15c7167c,value:Mary Kay]],lastName:[[id:107ab421-7208-45d4-b969-bbc54481992a,value:Andersen]],age:[[id:4b08d6e4-58f5-45df-8e69-6b790b692e0a,value:39]]]]
==>[id:91605c63-4988-4b60-9a30-5144719ae326,label:person,type:vertex,properties:[firstName:[[id:f760e0e6-652a-481a-92b0-1767d9bf372e,value:Robin]],lastName:[[id:352a4caa-bad6-47e3-a7dc-90ff342cf870,value:Wakefield]]]]
```

<span data-ttu-id="47631-196">Ensuite, nous allons obtenir la couche suivante de vertex.</span><span class="sxs-lookup"><span data-stu-id="47631-196">Next, let's get the next layer of vertices.</span></span> <span data-ttu-id="47631-197">Parcourons le graphique pour retourner tous les amis des amis de Thomas.</span><span class="sxs-lookup"><span data-stu-id="47631-197">Traverse the graph to return all the friends of Thomas's friends.</span></span>

<span data-ttu-id="47631-198">Entrée (amis des amis de Thomas) :</span><span class="sxs-lookup"><span data-stu-id="47631-198">Input (friends of friends of Thomas):</span></span>

```
:> g.V().hasLabel('person').has('firstName', 'Thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')
```
<span data-ttu-id="47631-199">Output:</span><span class="sxs-lookup"><span data-stu-id="47631-199">Output:</span></span>

```
==>[id:a801a0cb-ee85-44ee-a502-271685ef212e,label:person,type:vertex,properties:[firstName:[[id:b9489902-d29a-4673-8c09-c2b3fe7f8b94,value:Ben]],lastName:[[id:e084f933-9a4b-4dbc-8273-f0171265cf1d,value:Miller]]]]
```

## <a name="drop-a-vertex"></a><span data-ttu-id="47631-200">Suppression d’un vertex</span><span class="sxs-lookup"><span data-stu-id="47631-200">Drop a vertex</span></span>

<span data-ttu-id="47631-201">Nous allons à présent supprimer un vertex de la base de données des graphiques.</span><span class="sxs-lookup"><span data-stu-id="47631-201">Let's now delete a vertex from the graph database.</span></span>

<span data-ttu-id="47631-202">Entrée (suppression du vertex de Jack) :</span><span class="sxs-lookup"><span data-stu-id="47631-202">Input (drop Jack vertex):</span></span>

```
:> g.V().hasLabel('person').has('firstName', 'Jack').drop()
```

## <a name="clear-your-graph"></a><span data-ttu-id="47631-203">Effacement de tout le contenu de votre graphique</span><span class="sxs-lookup"><span data-stu-id="47631-203">Clear your graph</span></span>

<span data-ttu-id="47631-204">Enfin, nous allons supprimer tous les vertex et bords de la base de données.</span><span class="sxs-lookup"><span data-stu-id="47631-204">Finally, let's clear the database of all vertices and edges.</span></span>

<span data-ttu-id="47631-205">Entrée :</span><span class="sxs-lookup"><span data-stu-id="47631-205">Input:</span></span>

```
:> g.E().drop()
:> g.V().drop()
```

<span data-ttu-id="47631-206">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="47631-206">Congratulations!</span></span> <span data-ttu-id="47631-207">Vous avez terminé ce tutoriel Azure Cosmos DB : API Graph !</span><span class="sxs-lookup"><span data-stu-id="47631-207">You've completed this Azure Cosmos DB: Graph API tutorial!</span></span>

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="47631-208">Vérification des contrats SLA dans le portail Azure</span><span class="sxs-lookup"><span data-stu-id="47631-208">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="47631-209">Supprimer des ressources</span><span class="sxs-lookup"><span data-stu-id="47631-209">Clean up resources</span></span>

<span data-ttu-id="47631-210">Si vous ne pensez pas continuer à utiliser cette application, supprimez toutes les ressources créées durant ce guide de démarrage rapide dans le Portail Azure en procédant de la façon suivante :</span><span class="sxs-lookup"><span data-stu-id="47631-210">If you're not going to continue to use this app, delete all resources created by this quickstart in the Azure portal with the following steps:</span></span>  

1. <span data-ttu-id="47631-211">Dans le menu de gauche du portail Azure, cliquez sur **Groupes de ressources**, puis sur le nom de la ressource que vous avez créée.</span><span class="sxs-lookup"><span data-stu-id="47631-211">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you created.</span></span> 
2. <span data-ttu-id="47631-212">Dans la page de votre groupe de ressources, cliquez sur **Supprimer**, tapez le nom de la ressource à supprimer dans la zone de texte, puis cliquez sur **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="47631-212">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="47631-213">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="47631-213">Next steps</span></span>

<span data-ttu-id="47631-214">Dans ce démarrage rapide, vous avez appris à créer un compte Azure Cosmos DB, à créer un graphique à l’aide de l’Explorateur de données, à créer des vertex et des bords et à parcourir votre graphique à l’aide de la console Gremlin.</span><span class="sxs-lookup"><span data-stu-id="47631-214">In this quickstart, you've learned how to create an Azure Cosmos DB account, create a graph using the Data Explorer, create vertices and edges, and traverse your graph using the Gremlin console.</span></span> <span data-ttu-id="47631-215">Vous pouvez maintenant générer des requêtes plus complexes et implémenter une logique de traversée de graphique puissante, à l’aide de Gremlin.</span><span class="sxs-lookup"><span data-stu-id="47631-215">You can now build more complex queries and implement powerful graph traversal logic using Gremlin.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="47631-216">Interroger à l’aide de Gremlin</span><span class="sxs-lookup"><span data-stu-id="47631-216">Query using Gremlin</span></span>](tutorial-query-graph.md)
