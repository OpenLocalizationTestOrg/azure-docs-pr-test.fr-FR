---
title: "Didacticiel Azure Cosmos DB : Créer, interroger et parcourir la console Apache TinkerPops Gremlin | Microsoft Docs"
description: "Un toocreates de démarrage rapide de base de données Azure Cosmos sommets, les bords et les requêtes à l’aide de hello Azure Cosmos DB l’API Graph."
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
ms.openlocfilehash: 9de64c97fec89c45cecba9e14214db472ec76f57
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-create-query-and-traverse-a-graph-in-hello-gremlin-console"></a><span data-ttu-id="1a50c-103">Azure Cosmos DB : Créer, interroger et parcourir un graphique dans la console hello GREMLINE</span><span class="sxs-lookup"><span data-stu-id="1a50c-103">Azure Cosmos DB: Create, query, and traverse a graph in hello Gremlin console</span></span>

<span data-ttu-id="1a50c-104">Azure Cosmos DB est le service de base de données multi-modèle de Microsoft distribué à l’échelle mondiale.</span><span class="sxs-lookup"><span data-stu-id="1a50c-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="1a50c-105">Vous pouvez rapidement créer et interroger des bases de données de graphique, qui bénéficient de distribution globale de hello et des fonctionnalités de mise à l’échelle horizontale au cœur de hello de base de données Azure Cosmos document et clé/valeur.</span><span class="sxs-lookup"><span data-stu-id="1a50c-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="1a50c-106">Ce démarrage rapide montre comment toocreate un compte de base de données Azure Cosmos, base de données et à l’aide du graphique (conteneur) hello portail Azure, puis utilisez hello [GREMLINE Console](https://tinkerpop.apache.org/docs/current/reference/#gremlin-console) de [Apache TinkerPop](http://tinkerpop.apache.org) toowork avec Graphique des données de l’API (version préliminaire).</span><span class="sxs-lookup"><span data-stu-id="1a50c-106">This quick start demonstrates how toocreate an Azure Cosmos DB account, database, and graph (container) using hello Azure portal and then use hello [Gremlin Console](https://tinkerpop.apache.org/docs/current/reference/#gremlin-console) from  [Apache TinkerPop](http://tinkerpop.apache.org) toowork with Graph API (preview) data.</span></span> <span data-ttu-id="1a50c-107">Dans ce didacticiel, vous créez et interrogez les sommets et les bords, mise à jour d’une propriété de sommets, interroger les sommets, parcourent le graphique de hello et supprimer un sommet.</span><span class="sxs-lookup"><span data-stu-id="1a50c-107">In this tutorial, you create and query vertices and edges, updating a vertex property, query vertices, traverse hello graph, and drop a vertex.</span></span>

![Base de données Azure Cosmos à partir de la console d’Apache GREMLINE hello](./media/create-graph-gremlin-console/gremlin-console.png)

<span data-ttu-id="1a50c-109">console de GREMLINE Hello est Groovy/Java s’exécute sur Windows, Mac et Linux.</span><span class="sxs-lookup"><span data-stu-id="1a50c-109">hello Gremlin console is Groovy/Java based and runs on Linux, Mac, and Windows.</span></span> <span data-ttu-id="1a50c-110">Vous pouvez le télécharger depuis hello [Apache TinkerPop site](https://www.apache.org/dyn/closer.lua/tinkerpop/3.2.5/apache-tinkerpop-gremlin-console-3.2.5-bin.zip).</span><span class="sxs-lookup"><span data-stu-id="1a50c-110">You can download it from hello [Apache TinkerPop site](https://www.apache.org/dyn/closer.lua/tinkerpop/3.2.5/apache-tinkerpop-gremlin-console-3.2.5-bin.zip).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1a50c-111">Composants requis</span><span class="sxs-lookup"><span data-stu-id="1a50c-111">Prerequisites</span></span>

<span data-ttu-id="1a50c-112">Vous devez toohave une toocreate d’abonnement Azure un compte de base de données Azure Cosmos pour ce démarrage rapide.</span><span class="sxs-lookup"><span data-stu-id="1a50c-112">You need toohave an Azure subscription toocreate an Azure Cosmos DB account for this quickstart.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

<span data-ttu-id="1a50c-113">Vous devez également tooinstall hello [GREMLINE Console](http://tinkerpop.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="1a50c-113">You also need tooinstall hello [Gremlin Console](http://tinkerpop.apache.org/).</span></span> <span data-ttu-id="1a50c-114">Utilisez la version 3.2.5 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="1a50c-114">Use version 3.2.5 or above.</span></span>

## <a name="create-a-database-account"></a><span data-ttu-id="1a50c-115">Création d'un compte de base de données</span><span class="sxs-lookup"><span data-stu-id="1a50c-115">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a name="add-a-graph"></a><span data-ttu-id="1a50c-116">Ajout d’un graphique</span><span class="sxs-lookup"><span data-stu-id="1a50c-116">Add a graph</span></span>

[!INCLUDE [cosmos-db-create-graph](../../includes/cosmos-db-create-graph.md)]

## <span data-ttu-id="1a50c-117"><a id="ConnectAppService"></a>Se connecter tooyour du service d’applications</span><span class="sxs-lookup"><span data-stu-id="1a50c-117"><a id="ConnectAppService"></a>Connect tooyour app service</span></span>
1. <span data-ttu-id="1a50c-118">Avant de démarrer hello GREMLINE Console, créer ou modifier hello à distance-secure.yaml configuration fichier hello apache-tinkerpop-gremlin-console-3.2.5/conf répertoire.</span><span class="sxs-lookup"><span data-stu-id="1a50c-118">Before starting hello Gremlin Console, create or modify hello remote-secure.yaml configuration file in hello apache-tinkerpop-gremlin-console-3.2.5/conf directory.</span></span>
2. <span data-ttu-id="1a50c-119">Renseignez vos configurations *hôte*, *port*, *nom d’utilisateur*, *mot de passe*, *connectionPool* et *sérialiseur* :</span><span class="sxs-lookup"><span data-stu-id="1a50c-119">Fill in your *host*, *port*, *username*, *password*, *connectionPool*, and *serializer* configurations:</span></span>

    <span data-ttu-id="1a50c-120">Paramètre</span><span class="sxs-lookup"><span data-stu-id="1a50c-120">Setting</span></span>|<span data-ttu-id="1a50c-121">Valeur suggérée</span><span class="sxs-lookup"><span data-stu-id="1a50c-121">Suggested value</span></span>|<span data-ttu-id="1a50c-122">Description</span><span class="sxs-lookup"><span data-stu-id="1a50c-122">Description</span></span>
    ---|---|---
    <span data-ttu-id="1a50c-123">hôtes</span><span class="sxs-lookup"><span data-stu-id="1a50c-123">hosts</span></span>|<span data-ttu-id="1a50c-124">[***.graphs.azure.com]</span><span class="sxs-lookup"><span data-stu-id="1a50c-124">[***.graphs.azure.com]</span></span>|<span data-ttu-id="1a50c-125">Reportez-vous à la capture d’écran ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="1a50c-125">See screenshot below.</span></span> <span data-ttu-id="1a50c-126">Valeur d’URI de GREMLINE hello sur la page de vue d’ensemble de hello Hello portail Azure, entre crochets, suivi d’un hello : 443 / supprimé.</span><span class="sxs-lookup"><span data-stu-id="1a50c-126">This is hello Gremlin URI value on hello Overview page of hello Azure portal, in square brackets, with hello trailing :443/ removed.</span></span><br><br><span data-ttu-id="1a50c-127">Cette valeur peut également être récupérée à partir de l’onglet de clés hello, à l’aide de la valeur de l’URI hello en supprimant https://, la modification de documents toographs et suppression de fin hello : 443 /.</span><span class="sxs-lookup"><span data-stu-id="1a50c-127">This value can also be retrieved from hello Keys tab, using hello URI value by removing https://, changing documents toographs, and removing hello trailing :443/.</span></span>
    <span data-ttu-id="1a50c-128">port</span><span class="sxs-lookup"><span data-stu-id="1a50c-128">port</span></span>|<span data-ttu-id="1a50c-129">443</span><span class="sxs-lookup"><span data-stu-id="1a50c-129">443</span></span>|<span data-ttu-id="1a50c-130">Définissez too443.</span><span class="sxs-lookup"><span data-stu-id="1a50c-130">Set too443.</span></span>
    <span data-ttu-id="1a50c-131">username</span><span class="sxs-lookup"><span data-stu-id="1a50c-131">username</span></span>|<span data-ttu-id="1a50c-132">*Votre nom d’utilisateur*</span><span class="sxs-lookup"><span data-stu-id="1a50c-132">*Your username*</span></span>|<span data-ttu-id="1a50c-133">Hello ressource sous forme de hello `/dbs/<db>/colls/<coll>` où `<db>` est le nom de votre base de données et `<coll>` est votre nom de la collection.</span><span class="sxs-lookup"><span data-stu-id="1a50c-133">hello resource of hello form `/dbs/<db>/colls/<coll>` where `<db>` is your database name and `<coll>` is your collection name.</span></span>
    <span data-ttu-id="1a50c-134">password</span><span class="sxs-lookup"><span data-stu-id="1a50c-134">password</span></span>|<span data-ttu-id="1a50c-135">*Votre clé primaire*</span><span class="sxs-lookup"><span data-stu-id="1a50c-135">*Your primary key*</span></span>| <span data-ttu-id="1a50c-136">Reportez-vous à la deuxième capture d’écran ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="1a50c-136">See second screenshot below.</span></span> <span data-ttu-id="1a50c-137">Il s’agit de votre clé primaire, que vous pouvez récupérer à partir de la page de clés hello Hello portail Azure, dans la zone de clé primaire hello.</span><span class="sxs-lookup"><span data-stu-id="1a50c-137">This is your primary key, which you can retrieve from hello Keys page of hello Azure portal, in hello Primary Key box.</span></span> <span data-ttu-id="1a50c-138">Utilisez le bouton de copie de hello sur le côté gauche de hello de valeur de hello zone toocopy hello.</span><span class="sxs-lookup"><span data-stu-id="1a50c-138">Use hello copy button on hello left side of hello box toocopy hello value.</span></span>
    <span data-ttu-id="1a50c-139">connectionPool</span><span class="sxs-lookup"><span data-stu-id="1a50c-139">connectionPool</span></span>|<span data-ttu-id="1a50c-140">{enableSsl: true}</span><span class="sxs-lookup"><span data-stu-id="1a50c-140">{enableSsl: true}</span></span>|<span data-ttu-id="1a50c-141">Votre paramètre de pool de connexions pour SSL.</span><span class="sxs-lookup"><span data-stu-id="1a50c-141">Your connection pool setting for SSL.</span></span>
    <span data-ttu-id="1a50c-142">serializer</span><span class="sxs-lookup"><span data-stu-id="1a50c-142">serializer</span></span>|<span data-ttu-id="1a50c-143">{ className: org.apache.tinkerpop.gremlin.</span><span class="sxs-lookup"><span data-stu-id="1a50c-143">{ className: org.apache.tinkerpop.gremlin.</span></span><br><span data-ttu-id="1a50c-144">driver.ser.GraphSONMessageSerializerV1d0,</span><span class="sxs-lookup"><span data-stu-id="1a50c-144">driver.ser.GraphSONMessageSerializerV1d0,</span></span><br> <span data-ttu-id="1a50c-145">config: {serializeResultToString: true }}</span><span class="sxs-lookup"><span data-stu-id="1a50c-145">config: { serializeResultToString: true }}</span></span>|<span data-ttu-id="1a50c-146">La valeur toothis et supprimez celles `\n` lors du collage dans la valeur de hello les sauts de ligne.</span><span class="sxs-lookup"><span data-stu-id="1a50c-146">Set toothis value and delete any `\n` line breaks when pasting in hello value.</span></span>

    <span data-ttu-id="1a50c-147">Pour la valeur d’hôtes hello, copiez hello **GREMLINE URI** valeur hello **vue d’ensemble** page : ![afficher et copier des valeur GREMLINE URI hello sur la page de vue d’ensemble de hello Bonjour portail Azure](./media/create-graph-gremlin-console/gremlin-uri.png)</span><span class="sxs-lookup"><span data-stu-id="1a50c-147">For hello hosts value, copy hello **Gremlin URI** value from hello **Overview** page: ![View and copy hello Gremlin URI value on hello Overview page in hello Azure portal](./media/create-graph-gremlin-console/gremlin-uri.png)</span></span>

    <span data-ttu-id="1a50c-148">Pour la valeur de mot de passe de hello, copiez hello **clé primaire** de hello **clés** page : ![afficher et copier les clés de votre clé primaire Bonjour portail Azure, page](./media/create-graph-gremlin-console/keys.png)</span><span class="sxs-lookup"><span data-stu-id="1a50c-148">For hello password value, copy hello **Primary key** from hello **Keys** page: ![View and copy your primary key in hello Azure portal, Keys page](./media/create-graph-gremlin-console/keys.png)</span></span>


3. <span data-ttu-id="1a50c-149">Dans votre Terminal Server, exécutez `bin/gremlin.bat` ou `bin/gremlin.sh` toostart hello [GREMLINE Console](http://tinkerpop.apache.org/docs/3.2.5/tutorials/getting-started/).</span><span class="sxs-lookup"><span data-stu-id="1a50c-149">In your terminal, run `bin/gremlin.bat` or `bin/gremlin.sh` toostart hello [Gremlin Console](http://tinkerpop.apache.org/docs/3.2.5/tutorials/getting-started/).</span></span>
4. <span data-ttu-id="1a50c-150">Dans votre Terminal Server, exécutez `:remote connect tinkerpop.server conf/remote-secure.yaml` tooconnect tooyour du service d’applications.</span><span class="sxs-lookup"><span data-stu-id="1a50c-150">In your terminal, run `:remote connect tinkerpop.server conf/remote-secure.yaml` tooconnect tooyour app service.</span></span>

    > [!TIP]
    > <span data-ttu-id="1a50c-151">Si vous recevez une erreur de hello `No appenders could be found for logger` garantir la mise à jour hello sérialiseur valeur hello à distance-secure.yaml fichier comme décrit à l’étape 2.</span><span class="sxs-lookup"><span data-stu-id="1a50c-151">If you receive hello error `No appenders could be found for logger` ensure that you updated hello serializer value in hello remote-secure.yaml file as described in step 2.</span></span> 

<span data-ttu-id="1a50c-152">Parfait !</span><span class="sxs-lookup"><span data-stu-id="1a50c-152">Great!</span></span> <span data-ttu-id="1a50c-153">Maintenant que nous avons terminé le programme d’installation Bonjour, nous pouvons commencer en cours d’exécution des commandes de la console.</span><span class="sxs-lookup"><span data-stu-id="1a50c-153">Now that we finished hello setup, let's start running some console commands.</span></span>

<span data-ttu-id="1a50c-154">Essayons une simple commande count().</span><span class="sxs-lookup"><span data-stu-id="1a50c-154">Let's try a simple count() command.</span></span> <span data-ttu-id="1a50c-155">Tapez hello qui suit dans la console hello invite hello :</span><span class="sxs-lookup"><span data-stu-id="1a50c-155">Type hello following into hello console at hello prompt:</span></span>
```
:> g.V().count()
```

> [!TIP]
> <span data-ttu-id="1a50c-156">Hello d’avis `:>` qui précède hello `g.V().count()` texte ?</span><span class="sxs-lookup"><span data-stu-id="1a50c-156">Notice hello `:>` that precedes hello `g.V().count()` text?</span></span> 
>
> <span data-ttu-id="1a50c-157">Cela fait partie de la commande hello que vous devez tootype.</span><span class="sxs-lookup"><span data-stu-id="1a50c-157">This is part of hello command you need tootype.</span></span> <span data-ttu-id="1a50c-158">Il est important lors de l’utilisation de la console GREMLINE hello, avec la base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="1a50c-158">It is important when using hello Gremlin console, with Azure Cosmos DB.</span></span>  
>
> <span data-ttu-id="1a50c-159">L’omission de cette `:>` instruit hello console tooexecute commande hello localement, souvent sur un graphique en mémoire.</span><span class="sxs-lookup"><span data-stu-id="1a50c-159">Omitting this `:>` prefix instructs hello console tooexecute hello command locally, often against an in-memory graph.</span></span>
> <span data-ttu-id="1a50c-160">L’utilisation de cette `:>` indique hello console tooexecute une commande à distance, dans ce cas par rapport à la base de données Cosmos (l’émulateur de localhost hello, ou > instance Azure).</span><span class="sxs-lookup"><span data-stu-id="1a50c-160">Using this `:>` tells hello console tooexecute a remote command, in this case against Cosmos DB (either hello localhost emulator, or an > Azure instance).</span></span>


## <a name="create-vertices-and-edges"></a><span data-ttu-id="1a50c-161">Création de vertex et de bords</span><span class="sxs-lookup"><span data-stu-id="1a50c-161">Create vertices and edges</span></span>

<span data-ttu-id="1a50c-162">Commençons par ajouter des vertex pour cinq personnes : *Thomas*, *Mary Kay*, *Robin*, *Ben* et *Jack*.</span><span class="sxs-lookup"><span data-stu-id="1a50c-162">Let's begin by adding five person vertices for *Thomas*, *Mary Kay*, *Robin*, *Ben*, and *Jack*.</span></span>

<span data-ttu-id="1a50c-163">Entrée (Thomas) :</span><span class="sxs-lookup"><span data-stu-id="1a50c-163">Input (Thomas):</span></span>

```
:> g.addV('person').property('firstName', 'Thomas').property('lastName', 'Andersen').property('age', 44).property('userid', 1)
```

<span data-ttu-id="1a50c-164">Output:</span><span class="sxs-lookup"><span data-stu-id="1a50c-164">Output:</span></span>

```
==>[id:796cdccc-2acd-4e58-a324-91d6f6f5ed6d,label:person,type:vertex,properties:[firstName:[[id:f02a749f-b67c-4016-850e-910242d68953,value:Thomas]],lastName:[[id:f5fa3126-8818-4fda-88b0-9bb55145ce5c,value:Andersen]],age:[[id:f6390f9c-e563-433e-acbf-25627628016e,value:44]],userid:[[id:796cdccc-2acd-4e58-a324-91d6f6f5ed6d|userid,value:1]]]]
```
<span data-ttu-id="1a50c-165">Entrée (Mary Kay) :</span><span class="sxs-lookup"><span data-stu-id="1a50c-165">Input (Mary Kay):</span></span>

```
:> g.addV('person').property('firstName', 'Mary Kay').property('lastName', 'Andersen').property('age', 39).property('userid', 2)

```

<span data-ttu-id="1a50c-166">Output:</span><span class="sxs-lookup"><span data-stu-id="1a50c-166">Output:</span></span>

```
==>[id:0ac9be25-a476-4a30-8da8-e79f0119ea5e,label:person,type:vertex,properties:[firstName:[[id:ea0604f8-14ee-4513-a48a-1734a1f28dc0,value:Mary Kay]],lastName:[[id:86d3bba5-fd60-4856-9396-c195ef7d7f4b,value:Andersen]],age:[[id:bc81b78d-30c4-4e03-8f40-50f72eb5f6da,value:39]],userid:[[id:0ac9be25-a476-4a30-8da8-e79f0119ea5e|userid,value:2]]]]

```

<span data-ttu-id="1a50c-167">Entrée (Robin) :</span><span class="sxs-lookup"><span data-stu-id="1a50c-167">Input (Robin):</span></span>

```
:> g.addV('person').property('firstName', 'Robin').property('lastName', 'Wakefield').property('userid', 3)
```

<span data-ttu-id="1a50c-168">Output:</span><span class="sxs-lookup"><span data-stu-id="1a50c-168">Output:</span></span>

```
==>[id:8dc14d6a-8683-4a54-8d74-7eef1fb43a3e,label:person,type:vertex,properties:[firstName:[[id:ec65f078-7a43-4cbe-bc06-e50f2640dc4e,value:Robin]],lastName:[[id:a3937d07-0e88-45d3-a442-26fcdfb042ce,value:Wakefield]],userid:[[id:8dc14d6a-8683-4a54-8d74-7eef1fb43a3e|userid,value:3]]]]
```

<span data-ttu-id="1a50c-169">Entrée (Ben) :</span><span class="sxs-lookup"><span data-stu-id="1a50c-169">Input (Ben):</span></span>

```
:> g.addV('person').property('firstName', 'Ben').property('lastName', 'Miller').property('userid', 4)

```

<span data-ttu-id="1a50c-170">Output:</span><span class="sxs-lookup"><span data-stu-id="1a50c-170">Output:</span></span>

```
==>[id:ee86b670-4d24-4966-9a39-30529284b66f,label:person,type:vertex,properties:[firstName:[[id:a632469b-30fc-4157-840c-b80260871e9a,value:Ben]],lastName:[[id:4a08d307-0719-47c6-84ae-1b0b06630928,value:Miller]],userid:[[id:ee86b670-4d24-4966-9a39-30529284b66f|userid,value:4]]]]
```

<span data-ttu-id="1a50c-171">Entrée (Jack) :</span><span class="sxs-lookup"><span data-stu-id="1a50c-171">Input (Jack):</span></span>

```
:> g.addV('person').property('firstName', 'Jack').property('lastName', 'Connor').property('userid', 5)
```

<span data-ttu-id="1a50c-172">Output:</span><span class="sxs-lookup"><span data-stu-id="1a50c-172">Output:</span></span>

```
==>[id:4c835f2a-ea5b-43bb-9b6b-215488ad8469,label:person,type:vertex,properties:[firstName:[[id:4250824e-4b72-417f-af98-8034aa15559f,value:Jack]],lastName:[[id:44c1d5e1-a831-480a-bf94-5167d133549e,value:Connor]],userid:[[id:4c835f2a-ea5b-43bb-9b6b-215488ad8469|userid,value:5]]]]
```


<span data-ttu-id="1a50c-173">Ensuite, ajoutons des bords pour les relations entre ces personnes.</span><span class="sxs-lookup"><span data-stu-id="1a50c-173">Next, let's add edges for relationships between our people.</span></span>

<span data-ttu-id="1a50c-174">Entrée (Thomas -> Mary Kay) :</span><span class="sxs-lookup"><span data-stu-id="1a50c-174">Input (Thomas -> Mary Kay):</span></span>

```
:> g.V().hasLabel('person').has('firstName', 'Thomas').addE('knows').to(g.V().hasLabel('person').has('firstName', 'Mary Kay'))
```

<span data-ttu-id="1a50c-175">Output:</span><span class="sxs-lookup"><span data-stu-id="1a50c-175">Output:</span></span>

```
==>[id:c12bf9fb-96a1-4cb7-a3f8-431e196e702f,label:knows,type:edge,inVLabel:person,outVLabel:person,inV:0d1fa428-780c-49a5-bd3a-a68d96391d5c,outV:1ce821c6-aa3d-4170-a0b7-d14d2a4d18c3]
```

<span data-ttu-id="1a50c-176">Entrée (Thomas -> Robin) :</span><span class="sxs-lookup"><span data-stu-id="1a50c-176">Input (Thomas -> Robin):</span></span>

```
:> g.V().hasLabel('person').has('firstName', 'Thomas').addE('knows').to(g.V().hasLabel('person').has('firstName', 'Robin'))
```

<span data-ttu-id="1a50c-177">Output:</span><span class="sxs-lookup"><span data-stu-id="1a50c-177">Output:</span></span>

```
==>[id:58319bdd-1d3e-4f17-a106-0ddf18719d15,label:knows,type:edge,inVLabel:person,outVLabel:person,inV:3e324073-ccfc-4ae1-8675-d450858ca116,outV:1ce821c6-aa3d-4170-a0b7-d14d2a4d18c3]
```

<span data-ttu-id="1a50c-178">Entrée (Robin -> Ben) :</span><span class="sxs-lookup"><span data-stu-id="1a50c-178">Input (Robin -> Ben):</span></span>

```
:> g.V().hasLabel('person').has('firstName', 'Robin').addE('knows').to(g.V().hasLabel('person').has('firstName', 'Ben'))
```

<span data-ttu-id="1a50c-179">Output:</span><span class="sxs-lookup"><span data-stu-id="1a50c-179">Output:</span></span>

```
==>[id:889c4d3c-549e-4d35-bc21-a3d1bfa11e00,label:knows,type:edge,inVLabel:person,outVLabel:person,inV:40fd641d-546e-412a-abcc-58fe53891aab,outV:3e324073-ccfc-4ae1-8675-d450858ca116]
```

## <a name="update-a-vertex"></a><span data-ttu-id="1a50c-180">Mise à jour d’un vertex</span><span class="sxs-lookup"><span data-stu-id="1a50c-180">Update a vertex</span></span>

<span data-ttu-id="1a50c-181">Nous allons mettre à jour hello *Thomas* vertex avec une nouvelle durée de vie de *45*.</span><span class="sxs-lookup"><span data-stu-id="1a50c-181">Let's update hello *Thomas* vertex with a new age of *45*.</span></span>

<span data-ttu-id="1a50c-182">Entrée :</span><span class="sxs-lookup"><span data-stu-id="1a50c-182">Input:</span></span>
```
:> g.V().hasLabel('person').has('firstName', 'Thomas').property('age', 45)
```
<span data-ttu-id="1a50c-183">Output:</span><span class="sxs-lookup"><span data-stu-id="1a50c-183">Output:</span></span>

```
==>[id:ae36f938-210e-445a-92df-519f2b64c8ec,label:person,type:vertex,properties:[firstName:[[id:872090b6-6a77-456a-9a55-a59141d4ebc2,value:Thomas]],lastName:[[id:7ee7a39a-a414-4127-89b4-870bc4ef99f3,value:Andersen]],age:[[id:a2a75d5a-ae70-4095-806d-a35abcbfe71d,value:45]]]]
```

## <a name="query-your-graph"></a><span data-ttu-id="1a50c-184">Interrogation de votre graphique</span><span class="sxs-lookup"><span data-stu-id="1a50c-184">Query your graph</span></span>

<span data-ttu-id="1a50c-185">À présent, exécutons différentes requêtes sur votre graphique.</span><span class="sxs-lookup"><span data-stu-id="1a50c-185">Now, let's run a variety of queries against your graph.</span></span>

<span data-ttu-id="1a50c-186">Tout d’abord, nous allons essayez une requête avec un filtre tooreturn, seuls ceux qui est antérieurs à 40 ans.</span><span class="sxs-lookup"><span data-stu-id="1a50c-186">First, let's try a query with a filter tooreturn only people who are older than 40 years old.</span></span>

<span data-ttu-id="1a50c-187">Entrée (requête de filtre) :</span><span class="sxs-lookup"><span data-stu-id="1a50c-187">Input (filter query):</span></span>

```
:> g.V().hasLabel('person').has('age', gt(40))
```

<span data-ttu-id="1a50c-188">Output:</span><span class="sxs-lookup"><span data-stu-id="1a50c-188">Output:</span></span>

```
==>[id:ae36f938-210e-445a-92df-519f2b64c8ec,label:person,type:vertex,properties:[firstName:[[id:872090b6-6a77-456a-9a55-a59141d4ebc2,value:Thomas]],lastName:[[id:7ee7a39a-a414-4127-89b4-870bc4ef99f3,value:Andersen]],age:[[id:a2a75d5a-ae70-4095-806d-a35abcbfe71d,value:45]]]]
```

<span data-ttu-id="1a50c-189">Ensuite, nous allons projet prénom hello pour les personnes hello datent de plus de 40 ans.</span><span class="sxs-lookup"><span data-stu-id="1a50c-189">Next, let's project hello first name for hello people who are older than 40 years old.</span></span>

<span data-ttu-id="1a50c-190">Entrée (filtre + requête de projection) :</span><span class="sxs-lookup"><span data-stu-id="1a50c-190">Input (filter + projection query):</span></span>

```
:> g.V().hasLabel('person').has('age', gt(40)).values('firstName')
```

<span data-ttu-id="1a50c-191">Output:</span><span class="sxs-lookup"><span data-stu-id="1a50c-191">Output:</span></span>

```
==>Thomas
```

## <a name="traverse-your-graph"></a><span data-ttu-id="1a50c-192">Traversée du graphique</span><span class="sxs-lookup"><span data-stu-id="1a50c-192">Traverse your graph</span></span>

<span data-ttu-id="1a50c-193">Nous allons parcourir hello graphique tooreturn tous les amis de Thomas.</span><span class="sxs-lookup"><span data-stu-id="1a50c-193">Let's traverse hello graph tooreturn all of Thomas's friends.</span></span>

<span data-ttu-id="1a50c-194">Entrée (amis de Thomas) :</span><span class="sxs-lookup"><span data-stu-id="1a50c-194">Input (friends of Thomas):</span></span>

```
:> g.V().hasLabel('person').has('firstName', 'Thomas').outE('knows').inV().hasLabel('person')
```

<span data-ttu-id="1a50c-195">Output:</span><span class="sxs-lookup"><span data-stu-id="1a50c-195">Output:</span></span> 

```
==>[id:f04bc00b-cb56-46c4-a3bb-a5870c42f7ff,label:person,type:vertex,properties:[firstName:[[id:14feedec-b070-444e-b544-62be15c7167c,value:Mary Kay]],lastName:[[id:107ab421-7208-45d4-b969-bbc54481992a,value:Andersen]],age:[[id:4b08d6e4-58f5-45df-8e69-6b790b692e0a,value:39]]]]
==>[id:91605c63-4988-4b60-9a30-5144719ae326,label:person,type:vertex,properties:[firstName:[[id:f760e0e6-652a-481a-92b0-1767d9bf372e,value:Robin]],lastName:[[id:352a4caa-bad6-47e3-a7dc-90ff342cf870,value:Wakefield]]]]
```

<span data-ttu-id="1a50c-196">Ensuite, effectuons une couche de suivante hello des sommets.</span><span class="sxs-lookup"><span data-stu-id="1a50c-196">Next, let's get hello next layer of vertices.</span></span> <span data-ttu-id="1a50c-197">Parcourir hello graphique tooreturn tous les amis hello les amis de Thomas.</span><span class="sxs-lookup"><span data-stu-id="1a50c-197">Traverse hello graph tooreturn all hello friends of Thomas's friends.</span></span>

<span data-ttu-id="1a50c-198">Entrée (amis des amis de Thomas) :</span><span class="sxs-lookup"><span data-stu-id="1a50c-198">Input (friends of friends of Thomas):</span></span>

```
:> g.V().hasLabel('person').has('firstName', 'Thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')
```
<span data-ttu-id="1a50c-199">Output:</span><span class="sxs-lookup"><span data-stu-id="1a50c-199">Output:</span></span>

```
==>[id:a801a0cb-ee85-44ee-a502-271685ef212e,label:person,type:vertex,properties:[firstName:[[id:b9489902-d29a-4673-8c09-c2b3fe7f8b94,value:Ben]],lastName:[[id:e084f933-9a4b-4dbc-8273-f0171265cf1d,value:Miller]]]]
```

## <a name="drop-a-vertex"></a><span data-ttu-id="1a50c-200">Suppression d’un vertex</span><span class="sxs-lookup"><span data-stu-id="1a50c-200">Drop a vertex</span></span>

<span data-ttu-id="1a50c-201">Nous allons maintenant supprimer un sommet à partir de la base de données de graphique hello.</span><span class="sxs-lookup"><span data-stu-id="1a50c-201">Let's now delete a vertex from hello graph database.</span></span>

<span data-ttu-id="1a50c-202">Entrée (suppression du vertex de Jack) :</span><span class="sxs-lookup"><span data-stu-id="1a50c-202">Input (drop Jack vertex):</span></span>

```
:> g.V().hasLabel('person').has('firstName', 'Jack').drop()
```

## <a name="clear-your-graph"></a><span data-ttu-id="1a50c-203">Effacement de tout le contenu de votre graphique</span><span class="sxs-lookup"><span data-stu-id="1a50c-203">Clear your graph</span></span>

<span data-ttu-id="1a50c-204">Enfin, nous allons effacer de base de données hello de sommets et de bords.</span><span class="sxs-lookup"><span data-stu-id="1a50c-204">Finally, let's clear hello database of all vertices and edges.</span></span>

<span data-ttu-id="1a50c-205">Entrée :</span><span class="sxs-lookup"><span data-stu-id="1a50c-205">Input:</span></span>

```
:> g.E().drop()
:> g.V().drop()
```

<span data-ttu-id="1a50c-206">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="1a50c-206">Congratulations!</span></span> <span data-ttu-id="1a50c-207">Vous avez terminé ce tutoriel Azure Cosmos DB : API Graph !</span><span class="sxs-lookup"><span data-stu-id="1a50c-207">You've completed this Azure Cosmos DB: Graph API tutorial!</span></span>

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="1a50c-208">Passez en revue les SLA dans hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="1a50c-208">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="1a50c-209">Supprimer des ressources</span><span class="sxs-lookup"><span data-stu-id="1a50c-209">Clean up resources</span></span>

<span data-ttu-id="1a50c-210">Si vous n’allez toocontinue toouse cette application, supprimez toutes les ressources créées par ce démarrage rapide Bonjour portail Azure par hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="1a50c-210">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>  

1. <span data-ttu-id="1a50c-211">À partir du menu de gauche hello Bonjour portail Azure, cliquez sur **groupes de ressources** puis cliquez sur nom hello de ressource hello vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="1a50c-211">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="1a50c-212">Dans la page de votre groupe de ressources, cliquez sur **supprimer**, tapez nom hello de hello ressources toodelete dans la zone de texte hello, puis cliquez sur **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="1a50c-212">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1a50c-213">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1a50c-213">Next steps</span></span>

<span data-ttu-id="1a50c-214">Ce guide de démarrage rapide, vous avez appris comment toocreate un compte de base de données Azure Cosmos, créer un graphique à l’aide de hello Explorateur de données, créer des sommets et des arêtes et parcourir votre graphique à l’aide de la console de GREMLINE hello.</span><span class="sxs-lookup"><span data-stu-id="1a50c-214">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, create a graph using hello Data Explorer, create vertices and edges, and traverse your graph using hello Gremlin console.</span></span> <span data-ttu-id="1a50c-215">Vous pouvez maintenant générer des requêtes plus complexes et implémenter une logique de traversée de graphique puissante, à l’aide de Gremlin.</span><span class="sxs-lookup"><span data-stu-id="1a50c-215">You can now build more complex queries and implement powerful graph traversal logic using Gremlin.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="1a50c-216">Interroger à l’aide de Gremlin</span><span class="sxs-lookup"><span data-stu-id="1a50c-216">Query using Gremlin</span></span>](tutorial-query-graph.md)
