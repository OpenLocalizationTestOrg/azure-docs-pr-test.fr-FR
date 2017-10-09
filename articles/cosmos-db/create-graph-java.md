---
title: "aaaCreate une base de données du graphique de base de données Azure Cosmos avec Java | Documents Microsoft"
description: "Présente une Java le code exemple, vous pouvez utiliser un graphique des données tooconnect tooand requête dans la base de données Azure Cosmos à l’aide de GREMLINE."
services: cosmos-db
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: 
ms.assetid: daacbabf-1bb5-497f-92db-079910703046
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/24/2017
ms.author: denlee
ms.openlocfilehash: 595c0fb108f3dbe8c83674f0c9c4b0cdd3ab4c95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-create-a-graph-database-using-java-and-hello-azure-portal"></a><span data-ttu-id="f1c0a-103">Base de données Cosmos Azure : Créer une base de données de graphique à l’aide de Java et hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="f1c0a-103">Azure Cosmos DB: Create a graph database using Java and hello Azure portal</span></span>

<span data-ttu-id="f1c0a-104">Azure Cosmos DB est le service de base de données multi-modèle de Microsoft distribué à l’échelle mondiale.</span><span class="sxs-lookup"><span data-stu-id="f1c0a-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="f1c0a-105">Vous pouvez rapidement créer et interroger des bases de données de graphique, qui bénéficient de distribution globale de hello et des fonctionnalités de mise à l’échelle horizontale au cœur de hello de base de données Azure Cosmos document et clé/valeur.</span><span class="sxs-lookup"><span data-stu-id="f1c0a-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="f1c0a-106">Ce démarrage rapide crée un graphique à l’aide de la base de données hello outils portails Azure pour la base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="f1c0a-106">This quickstart creates a graph database using hello Azure portal tools for Azure Cosmos DB.</span></span> <span data-ttu-id="f1c0a-107">Ce démarrage rapide montre comment tooquickly créer une application de console Java à l’aide d’une base de données de graphique à l’aide de systèmes d’exploitation hello [GREMLINE Java](https://mvnrepository.com/artifact/org.apache.tinkerpop/gremlin-driver) pilote.</span><span class="sxs-lookup"><span data-stu-id="f1c0a-107">This quickstart also shows you how tooquickly create a Java console app using a graph database using hello OSS [Gremlin Java](https://mvnrepository.com/artifact/org.apache.tinkerpop/gremlin-driver) driver.</span></span> <span data-ttu-id="f1c0a-108">instructions Hello dans ce démarrage rapide peuvent être suivies sur n’importe quel système d’exploitation qui est capable d’exécuter Java.</span><span class="sxs-lookup"><span data-stu-id="f1c0a-108">hello instructions in this quickstart can be followed on any operating system that is capable of running Java.</span></span> <span data-ttu-id="f1c0a-109">Ce démarrage rapide permet familiarise avec la création et modification des ressources du graphique dans hello l’interface utilisateur ou par programme, selon ce qui est votre préférence.</span><span class="sxs-lookup"><span data-stu-id="f1c0a-109">This quickstart familiarizes you with creating and modifying graph resources in either hello UI or programmatically, whichever is your preference.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="f1c0a-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="f1c0a-110">Prerequisites</span></span>

* [<span data-ttu-id="f1c0a-111">Java Development Kit (JDK) 1.7+</span><span class="sxs-lookup"><span data-stu-id="f1c0a-111">Java Development Kit (JDK) 1.7+</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
    * <span data-ttu-id="f1c0a-112">Sur Ubuntu, exécutez `apt-get install default-jdk` tooinstall hello JDK.</span><span class="sxs-lookup"><span data-stu-id="f1c0a-112">On Ubuntu, run `apt-get install default-jdk` tooinstall hello JDK.</span></span>
    * <span data-ttu-id="f1c0a-113">Être tooset vraiment hello JAVA_HOME variable toopoint toohello dossier d’environnement sur lequel hello JDK est installé.</span><span class="sxs-lookup"><span data-stu-id="f1c0a-113">Be sure tooset hello JAVA_HOME environment variable toopoint toohello folder where hello JDK is installed.</span></span>
* <span data-ttu-id="f1c0a-114">[Téléchargement](http://maven.apache.org/download.cgi) et [installation](http://maven.apache.org/install.html) d’une archive binaire [Maven](http://maven.apache.org/)</span><span class="sxs-lookup"><span data-stu-id="f1c0a-114">[Download](http://maven.apache.org/download.cgi) and [install](http://maven.apache.org/install.html) a [Maven](http://maven.apache.org/) binary archive</span></span>
    * <span data-ttu-id="f1c0a-115">Sur Ubuntu, vous pouvez exécuter `apt-get install maven` tooinstall Maven.</span><span class="sxs-lookup"><span data-stu-id="f1c0a-115">On Ubuntu, you can run `apt-get install maven` tooinstall Maven.</span></span>
* [<span data-ttu-id="f1c0a-116">Git</span><span class="sxs-lookup"><span data-stu-id="f1c0a-116">Git</span></span>](https://www.git-scm.com/)
    * <span data-ttu-id="f1c0a-117">Sur Ubuntu, vous pouvez exécuter `sudo apt-get install git` tooinstall Git.</span><span class="sxs-lookup"><span data-stu-id="f1c0a-117">On Ubuntu, you can run `sudo apt-get install git` tooinstall Git.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="f1c0a-118">Création d'un compte de base de données</span><span class="sxs-lookup"><span data-stu-id="f1c0a-118">Create a database account</span></span>

<span data-ttu-id="f1c0a-119">Avant de pouvoir créer une base de données du graphique, vous devez toocreate un compte de base de données GREMLINE (graphique) avec la base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="f1c0a-119">Before you can create a graph database, you need toocreate a Gremlin (Graph) database account with Azure Cosmos DB.</span></span>

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a name="add-a-graph"></a><span data-ttu-id="f1c0a-120">Ajout d’un graphique</span><span class="sxs-lookup"><span data-stu-id="f1c0a-120">Add a graph</span></span>

<span data-ttu-id="f1c0a-121">Vous pouvez maintenant utiliser outil Explorateur de données de hello Bonjour toocreate portail Azure une base de données de graphique.</span><span class="sxs-lookup"><span data-stu-id="f1c0a-121">You can now use hello Data Explorer tool in hello Azure portal toocreate a graph database.</span></span> 

1. <span data-ttu-id="f1c0a-122">Bonjour portail Azure, dans le menu de navigation gauche hello, cliquez sur **Explorateur de données (version préliminaire)**.</span><span class="sxs-lookup"><span data-stu-id="f1c0a-122">In hello Azure portal, in hello left navigation menu, click **Data Explorer (Preview)**.</span></span> 
2. <span data-ttu-id="f1c0a-123">Bonjour **Explorateur de données (version préliminaire)** panneau, cliquez sur **nouveau graphique**, puis renseignez page hello à l’aide de hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="f1c0a-123">In hello **Data Explorer (Preview)** blade, click **New Graph**, then fill in hello page using hello following information:</span></span>

    ![Explorateur de données Bonjour portail Azure](./media/create-graph-java/azure-cosmosdb-data-explorer.png)

    <span data-ttu-id="f1c0a-125">Paramètre</span><span class="sxs-lookup"><span data-stu-id="f1c0a-125">Setting</span></span>|<span data-ttu-id="f1c0a-126">Valeur suggérée</span><span class="sxs-lookup"><span data-stu-id="f1c0a-126">Suggested value</span></span>|<span data-ttu-id="f1c0a-127">Description</span><span class="sxs-lookup"><span data-stu-id="f1c0a-127">Description</span></span>
    ---|---|---
    <span data-ttu-id="f1c0a-128">ID de base de données</span><span class="sxs-lookup"><span data-stu-id="f1c0a-128">Database ID</span></span>|<span data-ttu-id="f1c0a-129">sample-database</span><span class="sxs-lookup"><span data-stu-id="f1c0a-129">sample-database</span></span>|<span data-ttu-id="f1c0a-130">ID de Hello pour votre nouvelle base de données.</span><span class="sxs-lookup"><span data-stu-id="f1c0a-130">hello ID for your new database.</span></span> <span data-ttu-id="f1c0a-131">Les noms de base de données doivent inclure entre 1 et 255 caractères et ne peuvent pas contenir `/ \ # ?` ni d’espace de fin.</span><span class="sxs-lookup"><span data-stu-id="f1c0a-131">Database names must be between 1 and 255 characters, and cannot contain `/ \ # ?` or a trailing space.</span></span>
    <span data-ttu-id="f1c0a-132">ID du graphique</span><span class="sxs-lookup"><span data-stu-id="f1c0a-132">Graph ID</span></span>|<span data-ttu-id="f1c0a-133">sample-graph</span><span class="sxs-lookup"><span data-stu-id="f1c0a-133">sample-graph</span></span>|<span data-ttu-id="f1c0a-134">ID de Hello pour votre nouveau graphique.</span><span class="sxs-lookup"><span data-stu-id="f1c0a-134">hello ID for your new graph.</span></span> <span data-ttu-id="f1c0a-135">Les noms de graphique ont hello même caractère spécifications en tant qu’ID de base de données.</span><span class="sxs-lookup"><span data-stu-id="f1c0a-135">Graph names have hello same character requirements as database ids.</span></span>
    <span data-ttu-id="f1c0a-136">Capacité de stockage</span><span class="sxs-lookup"><span data-stu-id="f1c0a-136">Storage Capacity</span></span>| <span data-ttu-id="f1c0a-137">10 Go</span><span class="sxs-lookup"><span data-stu-id="f1c0a-137">10 GB</span></span>|<span data-ttu-id="f1c0a-138">Laissez la valeur par défaut de hello.</span><span class="sxs-lookup"><span data-stu-id="f1c0a-138">Leave hello default value.</span></span> <span data-ttu-id="f1c0a-139">Il s’agit de la capacité de stockage hello de base de données hello.</span><span class="sxs-lookup"><span data-stu-id="f1c0a-139">This is hello storage capacity of hello database.</span></span>
    <span data-ttu-id="f1c0a-140">Throughput</span><span class="sxs-lookup"><span data-stu-id="f1c0a-140">Throughput</span></span>|<span data-ttu-id="f1c0a-141">400 unités de requête</span><span class="sxs-lookup"><span data-stu-id="f1c0a-141">400 RUs</span></span>|<span data-ttu-id="f1c0a-142">Laissez la valeur par défaut de hello.</span><span class="sxs-lookup"><span data-stu-id="f1c0a-142">Leave hello default value.</span></span> <span data-ttu-id="f1c0a-143">Vous pouvez monter le débit hello ultérieurement si vous souhaitez une latence tooreduce.</span><span class="sxs-lookup"><span data-stu-id="f1c0a-143">You can scale up hello throughput later if you want tooreduce latency.</span></span>
    <span data-ttu-id="f1c0a-144">Clé de partition</span><span class="sxs-lookup"><span data-stu-id="f1c0a-144">Partition key</span></span>|<span data-ttu-id="f1c0a-145">Laisser vide</span><span class="sxs-lookup"><span data-stu-id="f1c0a-145">Leave blank</span></span>|<span data-ttu-id="f1c0a-146">Clé de partition hello pour objectif de hello de ce démarrage rapide, laissez vide.</span><span class="sxs-lookup"><span data-stu-id="f1c0a-146">For hello purpose of this quickstart, leave hello partition key blank.</span></span>

3. <span data-ttu-id="f1c0a-147">Une fois le formulaire de hello est rempli, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="f1c0a-147">Once hello form is filled out, click **OK**.</span></span>

## <a name="clone-hello-sample-application"></a><span data-ttu-id="f1c0a-148">Exemple d’application hello de cloner</span><span class="sxs-lookup"><span data-stu-id="f1c0a-148">Clone hello sample application</span></span>

<span data-ttu-id="f1c0a-149">Maintenant nous allons cloner une application graphique à partir de github, définissez la chaîne de connexion hello et exécutez-le.</span><span class="sxs-lookup"><span data-stu-id="f1c0a-149">Now let's clone a graph app from github, set hello connection string, and run it.</span></span> <span data-ttu-id="f1c0a-150">Vous voyez combien il est facile toowork avec des données par programme.</span><span class="sxs-lookup"><span data-stu-id="f1c0a-150">You see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="f1c0a-151">Ouvrez une fenêtre de Terminal Server git, telles que l’interpréteur de commandes git, et `cd` répertoire de travail tooa.</span><span class="sxs-lookup"><span data-stu-id="f1c0a-151">Open a git terminal window, such as git bash, and `cd` tooa working directory.</span></span>  

2. <span data-ttu-id="f1c0a-152">Exécutez hello suivant le dépôt d’exemples de commande tooclone hello.</span><span class="sxs-lookup"><span data-stu-id="f1c0a-152">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-graph-java-getting-started.git
    ```

## <a name="review-hello-code"></a><span data-ttu-id="f1c0a-153">Réviser le code hello</span><span class="sxs-lookup"><span data-stu-id="f1c0a-153">Review hello code</span></span>

<span data-ttu-id="f1c0a-154">Nous allons effectuer une révision rapide de ce qui se passe dans l’application hello.</span><span class="sxs-lookup"><span data-stu-id="f1c0a-154">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="f1c0a-155">Ouvrez hello `Program.java` de fichiers à partir du dossier \src\GetStarted hello et recherchez ces lignes de code.</span><span class="sxs-lookup"><span data-stu-id="f1c0a-155">Open hello `Program.java` file from hello \src\GetStarted folder and find these lines of code.</span></span> 

* <span data-ttu-id="f1c0a-156">Hello GREMLINE `Client` est initialisé à partir de la configuration de hello dans `src/remote.yaml`.</span><span class="sxs-lookup"><span data-stu-id="f1c0a-156">hello Gremlin `Client` is initialized from hello configuration in `src/remote.yaml`.</span></span>

    ```java
    cluster = Cluster.build(new File("src/remote.yaml")).create();
    ...
    client = cluster.connect();
    ```

* <span data-ttu-id="f1c0a-157">Une série d’étapes de GREMLINE sont exécutées à l’aide de hello `client.submit` (méthode).</span><span class="sxs-lookup"><span data-stu-id="f1c0a-157">A series of Gremlin steps are executed using hello `client.submit` method.</span></span>

    ```java
    ResultSet results = client.submit(gremlin);

    CompletableFuture<List<Result>> completableFutureResults = results.all();
    List<Result> resultList = completableFutureResults.get();

    for (Result result : resultList) {
        System.out.println(result.toString());
    }
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="f1c0a-158">Mise à jour de votre chaîne de connexion</span><span class="sxs-lookup"><span data-stu-id="f1c0a-158">Update your connection string</span></span>

1. <span data-ttu-id="f1c0a-159">Fichier de src/remote.yaml hello ouvert.</span><span class="sxs-lookup"><span data-stu-id="f1c0a-159">Open hello src/remote.yaml file.</span></span> 

3. <span data-ttu-id="f1c0a-160">Renseignez vos *hôtes*, *nom d’utilisateur*, et *mot de passe* valeurs hello src/remote.yaml fichier.</span><span class="sxs-lookup"><span data-stu-id="f1c0a-160">Fill in your *hosts*, *username*, and *password* values in hello src/remote.yaml file.</span></span> <span data-ttu-id="f1c0a-161">autres paramètres de hello Hello n’avez pas besoin de toobe modifié.</span><span class="sxs-lookup"><span data-stu-id="f1c0a-161">hello rest of hello settings do not need toobe changed.</span></span>

    <span data-ttu-id="f1c0a-162">Paramètre</span><span class="sxs-lookup"><span data-stu-id="f1c0a-162">Setting</span></span>|<span data-ttu-id="f1c0a-163">Valeur suggérée</span><span class="sxs-lookup"><span data-stu-id="f1c0a-163">Suggested value</span></span>|<span data-ttu-id="f1c0a-164">Description</span><span class="sxs-lookup"><span data-stu-id="f1c0a-164">Description</span></span>
    ---|---|---
    <span data-ttu-id="f1c0a-165">Hôtes</span><span class="sxs-lookup"><span data-stu-id="f1c0a-165">Hosts</span></span>|<span data-ttu-id="f1c0a-166">[***.graphs.azure.com]</span><span class="sxs-lookup"><span data-stu-id="f1c0a-166">[***.graphs.azure.com]</span></span>|<span data-ttu-id="f1c0a-167">Consultez ce tableau de la capture d’écran hello.</span><span class="sxs-lookup"><span data-stu-id="f1c0a-167">See hello screenshot following this table.</span></span> <span data-ttu-id="f1c0a-168">Cette valeur est la valeur de l’URI de GREMLINE hello sur la page de vue d’ensemble de hello Hello portail Azure, entre crochets, suivi d’un hello : 443 / supprimé.</span><span class="sxs-lookup"><span data-stu-id="f1c0a-168">This value is hello Gremlin URI value on hello Overview page of hello Azure portal, in square brackets, with hello trailing :443/ removed.</span></span><br><br><span data-ttu-id="f1c0a-169">Cette valeur peut également être récupérée à partir de l’onglet de clés hello, à l’aide de la valeur de l’URI hello en supprimant https://, la modification de documents toographs et suppression de fin hello : 443 /.</span><span class="sxs-lookup"><span data-stu-id="f1c0a-169">This value can also be retrieved from hello Keys tab, using hello URI value by removing https://, changing documents toographs, and removing hello trailing :443/.</span></span>
    <span data-ttu-id="f1c0a-170">Nom d’utilisateur</span><span class="sxs-lookup"><span data-stu-id="f1c0a-170">Username</span></span>|<span data-ttu-id="f1c0a-171">/dbs/sample-database/colls/sample-graph</span><span class="sxs-lookup"><span data-stu-id="f1c0a-171">/dbs/sample-database/colls/sample-graph</span></span>|<span data-ttu-id="f1c0a-172">Hello ressource sous forme de hello `/dbs/<db>/colls/<coll>` où `<db>` est votre nom de base de données existant et `<coll>` est votre nom existant de la collection.</span><span class="sxs-lookup"><span data-stu-id="f1c0a-172">hello resource of hello form `/dbs/<db>/colls/<coll>` where `<db>` is your existing database name and `<coll>` is your existing collection name.</span></span>
    <span data-ttu-id="f1c0a-173">Mot de passe</span><span class="sxs-lookup"><span data-stu-id="f1c0a-173">Password</span></span>|<span data-ttu-id="f1c0a-174">*Votre clé principale primaire*</span><span class="sxs-lookup"><span data-stu-id="f1c0a-174">*Your primary master key*</span></span>|<span data-ttu-id="f1c0a-175">Consultez ce tableau de la capture d’écran hello deuxième.</span><span class="sxs-lookup"><span data-stu-id="f1c0a-175">See hello second screenshot following this table.</span></span> <span data-ttu-id="f1c0a-176">Cette valeur est la clé primaire, que vous pouvez récupérer à partir de la page de clés hello Hello portail Azure, dans la zone de clé primaire hello.</span><span class="sxs-lookup"><span data-stu-id="f1c0a-176">This value is your primary key, which you can retrieve from hello Keys page of hello Azure portal, in hello Primary Key box.</span></span> <span data-ttu-id="f1c0a-177">Copier la valeur hello à l’aide du bouton de copie hello sur droite hello de zone de hello.</span><span class="sxs-lookup"><span data-stu-id="f1c0a-177">Copy hello value using hello copy button on hello right side of hello box.</span></span>

    <span data-ttu-id="f1c0a-178">Pour la valeur d’hôtes hello, copiez hello **GREMLINE URI** valeur hello **vue d’ensemble** page.</span><span class="sxs-lookup"><span data-stu-id="f1c0a-178">For hello Hosts value, copy hello **Gremlin URI** value from hello **Overview** page.</span></span> <span data-ttu-id="f1c0a-179">S’il est vide, consultez les instructions de hello dans ligne hello hôtes hello précédant la table sur la création de hello GREMLINE URI à partir du Panneau de clés hello.</span><span class="sxs-lookup"><span data-stu-id="f1c0a-179">If it's empty, see hello instructions in hello Hosts row in hello preceding table about creating hello Gremlin URI from hello Keys blade.</span></span>
<span data-ttu-id="f1c0a-180">![Valeur d’URI de GREMLINE hello afficher et copier sur la page de vue d’ensemble de hello Bonjour portail Azure](./media/create-graph-java/gremlin-uri.png)</span><span class="sxs-lookup"><span data-stu-id="f1c0a-180">![View and copy hello Gremlin URI value on hello Overview page in hello Azure portal](./media/create-graph-java/gremlin-uri.png)</span></span>

    <span data-ttu-id="f1c0a-181">Pourquoi la valeur de mot de passe, copiez hello **clé primaire** de hello **clés** panneau : ![afficher et copier les clés de votre clé primaire Bonjour portail Azure, page](./media/create-graph-java/keys.png)</span><span class="sxs-lookup"><span data-stu-id="f1c0a-181">For hello Password value, copy hello **Primary key** from hello **Keys** blade: ![View and copy your primary key in hello Azure portal, Keys page](./media/create-graph-java/keys.png)</span></span>

## <a name="run-hello-console-app"></a><span data-ttu-id="f1c0a-182">Exécutez l’application de console hello</span><span class="sxs-lookup"><span data-stu-id="f1c0a-182">Run hello console app</span></span>

1. <span data-ttu-id="f1c0a-183">Dans la fenêtre de terminal git hello, `cd` dossier azure-cosmos-db-graph-java-getting-started de toohello.</span><span class="sxs-lookup"><span data-stu-id="f1c0a-183">In hello git terminal window, `cd` toohello azure-cosmos-db-graph-java-getting-started folder.</span></span>

2. <span data-ttu-id="f1c0a-184">Dans la fenêtre de terminal git hello, tapez `mvn package` tooinstall hello requis packages Java.</span><span class="sxs-lookup"><span data-stu-id="f1c0a-184">In hello git terminal window, type `mvn package` tooinstall hello required Java packages.</span></span>

3. <span data-ttu-id="f1c0a-185">Dans la fenêtre de terminal git hello, exécutez `mvn exec:java -D exec.mainClass=GetStarted.Program` dans hello toostart de la fenêtre de terminal de votre application Java.</span><span class="sxs-lookup"><span data-stu-id="f1c0a-185">In hello git terminal window, run `mvn exec:java -D exec.mainClass=GetStarted.Program` in hello terminal window toostart your Java application.</span></span>

<span data-ttu-id="f1c0a-186">fenêtre de terminal Hello affiche les sommets hello ajoutés toohello graphique.</span><span class="sxs-lookup"><span data-stu-id="f1c0a-186">hello terminal window displays hello vertices being added toohello graph.</span></span> <span data-ttu-id="f1c0a-187">Une fois que la fin du programme de hello basculer arrière toohello portail Azure dans votre navigateur internet.</span><span class="sxs-lookup"><span data-stu-id="f1c0a-187">Once hello program completes, switch back toohello Azure portal in your internet browser.</span></span> 

<a id="add-sample-data"></a>
## <a name="review-and-add-sample-data"></a><span data-ttu-id="f1c0a-188">Examiner et ajouter des exemples de données</span><span class="sxs-lookup"><span data-stu-id="f1c0a-188">Review and add sample data</span></span>

<span data-ttu-id="f1c0a-189">Vous pouvez maintenant revenir en arrière tooData Explorer et consultez les sommets hello ajouté toohello graphique et ajouter des points de données supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="f1c0a-189">You can now go back tooData Explorer and see hello vertices added toohello graph, and add additional data points.</span></span>

1. <span data-ttu-id="f1c0a-190">Dans l’Explorateur de données, développez hello **base de données exemple**/**exemple de graphique**, cliquez sur **graphique**, puis cliquez sur **appliquer le filtre**.</span><span class="sxs-lookup"><span data-stu-id="f1c0a-190">In Data Explorer, expand hello **sample-database**/**sample-graph**, click **Graph**, and then click **Apply Filter**.</span></span> 

   ![Créer des documents dans l’Explorateur de données Bonjour portail Azure](./media/create-graph-java/azure-cosmosdb-data-explorer-expanded.png)

2. <span data-ttu-id="f1c0a-192">Bonjour **résultats** liste, notez hello nouveaux utilisateurs ajoutés toohello graphique.</span><span class="sxs-lookup"><span data-stu-id="f1c0a-192">In hello **Results** list, notice hello new users added toohello graph.</span></span> <span data-ttu-id="f1c0a-193">Sélectionnez **ben** et notez qu’il s’est connecté toorobin.</span><span class="sxs-lookup"><span data-stu-id="f1c0a-193">Select **ben** and notice that he's connected toorobin.</span></span> <span data-ttu-id="f1c0a-194">Vous pouvez déplacer les sommets hello sur l’Explorateur graphique hello, effectuer un zoom avant et arrière et développez taille hello de surface de l’Explorateur graphique hello.</span><span class="sxs-lookup"><span data-stu-id="f1c0a-194">You can move hello vertices around on hello graph explorer, zoom in and out, and expand hello size of hello graph explorer surface.</span></span> 

   ![Nouvelle sommets dans graphique hello hello portail Azure dans l’Explorateur de données](./media/create-graph-java/azure-cosmosdb-graph-explorer-new.png)

3. <span data-ttu-id="f1c0a-196">Nous allons ajouter quelques nouveau utilisateurs toohello graphique à l’aide de hello Explorateur de données.</span><span class="sxs-lookup"><span data-stu-id="f1c0a-196">Let's add a few new users toohello graph using hello Data Explorer.</span></span> <span data-ttu-id="f1c0a-197">Cliquez sur hello **nouveau sommet** graphique tooyour des données tooadd du bouton.</span><span class="sxs-lookup"><span data-stu-id="f1c0a-197">Click hello **New Vertex** button tooadd data tooyour graph.</span></span>

   ![Créer des documents dans l’Explorateur de données Bonjour portail Azure](./media/create-graph-java/azure-cosmosdb-data-explorer-new-vertex.png)

4. <span data-ttu-id="f1c0a-199">Entrez une étiquette de *personne* puis entrez hello suivante, clés et valeurs toocreate hello premier vertex dans le graphique de hello.</span><span class="sxs-lookup"><span data-stu-id="f1c0a-199">Enter a label of *person* then enter hello following keys and values toocreate hello first vertex in hello graph.</span></span> <span data-ttu-id="f1c0a-200">Notez que vous pouvez créer des propriétés uniques pour chaque personne dans votre graphique.</span><span class="sxs-lookup"><span data-stu-id="f1c0a-200">Notice that you can create unique properties for each person in your graph.</span></span> <span data-ttu-id="f1c0a-201">Clé d’identification uniquement hello est requis.</span><span class="sxs-lookup"><span data-stu-id="f1c0a-201">Only hello id key is required.</span></span>

    <span data-ttu-id="f1c0a-202">key</span><span class="sxs-lookup"><span data-stu-id="f1c0a-202">key</span></span>|<span data-ttu-id="f1c0a-203">value</span><span class="sxs-lookup"><span data-stu-id="f1c0a-203">value</span></span>|<span data-ttu-id="f1c0a-204">Remarques</span><span class="sxs-lookup"><span data-stu-id="f1c0a-204">Notes</span></span>
    ----|----|----
    <span data-ttu-id="f1c0a-205">id</span><span class="sxs-lookup"><span data-stu-id="f1c0a-205">id</span></span>|<span data-ttu-id="f1c0a-206">ashley</span><span class="sxs-lookup"><span data-stu-id="f1c0a-206">ashley</span></span>|<span data-ttu-id="f1c0a-207">Identificateur unique de Hello pour les vertex hello.</span><span class="sxs-lookup"><span data-stu-id="f1c0a-207">hello unique identifier for hello vertex.</span></span> <span data-ttu-id="f1c0a-208">Si vous ne spécifiez aucun id, le système en génère un pour vous.</span><span class="sxs-lookup"><span data-stu-id="f1c0a-208">If you don't specify an id, one is generated for you.</span></span>
    <span data-ttu-id="f1c0a-209">gender</span><span class="sxs-lookup"><span data-stu-id="f1c0a-209">gender</span></span>|<span data-ttu-id="f1c0a-210">female</span><span class="sxs-lookup"><span data-stu-id="f1c0a-210">female</span></span>| 
    <span data-ttu-id="f1c0a-211">tech</span><span class="sxs-lookup"><span data-stu-id="f1c0a-211">tech</span></span> | <span data-ttu-id="f1c0a-212">java</span><span class="sxs-lookup"><span data-stu-id="f1c0a-212">java</span></span> | 

    > [!NOTE]
    > <span data-ttu-id="f1c0a-213">Dans ce guide de démarrage rapide, nous créons une collection non partitionnée.</span><span class="sxs-lookup"><span data-stu-id="f1c0a-213">In this quickstart we create a non-partitioned collection.</span></span> <span data-ttu-id="f1c0a-214">Toutefois, si vous créez une collection partitionnée par spécification d’une clé de partition pendant la création de la collection hello, vous devez clé de partition tooinclude hello en tant que clé dans chaque nouveau sommet.</span><span class="sxs-lookup"><span data-stu-id="f1c0a-214">However, if you create a partitioned collection by specifying a partition key during hello collection creation, then you need tooinclude hello partition key as a key in each new vertex.</span></span> 

5. <span data-ttu-id="f1c0a-215">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="f1c0a-215">Click **OK**.</span></span> <span data-ttu-id="f1c0a-216">Vous devrez peut-être tooexpand votre écran toosee **OK** sous hello écran hello.</span><span class="sxs-lookup"><span data-stu-id="f1c0a-216">You may need tooexpand your screen toosee **OK** on hello bottom of hello screen.</span></span>

6. <span data-ttu-id="f1c0a-217">Cliquez de nouveau sur **New Vertex (Nouveau vertex)** et ajoutez un nouvel utilisateur supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="f1c0a-217">Click **New Vertex** again and add an additional new user.</span></span> <span data-ttu-id="f1c0a-218">Entrez une étiquette de *personne* puis entrez les éléments suivants de hello clés et valeurs :</span><span class="sxs-lookup"><span data-stu-id="f1c0a-218">Enter a label of *person* then enter hello following keys and values:</span></span>

    <span data-ttu-id="f1c0a-219">key</span><span class="sxs-lookup"><span data-stu-id="f1c0a-219">key</span></span>|<span data-ttu-id="f1c0a-220">value</span><span class="sxs-lookup"><span data-stu-id="f1c0a-220">value</span></span>|<span data-ttu-id="f1c0a-221">Remarques</span><span class="sxs-lookup"><span data-stu-id="f1c0a-221">Notes</span></span>
    ----|----|----
    <span data-ttu-id="f1c0a-222">id</span><span class="sxs-lookup"><span data-stu-id="f1c0a-222">id</span></span>|<span data-ttu-id="f1c0a-223">rakesh</span><span class="sxs-lookup"><span data-stu-id="f1c0a-223">rakesh</span></span>|<span data-ttu-id="f1c0a-224">Identificateur unique de Hello pour les vertex hello.</span><span class="sxs-lookup"><span data-stu-id="f1c0a-224">hello unique identifier for hello vertex.</span></span> <span data-ttu-id="f1c0a-225">Si vous ne spécifiez aucun id, le système en génère un pour vous.</span><span class="sxs-lookup"><span data-stu-id="f1c0a-225">If you don't specify an id, one is generated for you.</span></span>
    <span data-ttu-id="f1c0a-226">gender</span><span class="sxs-lookup"><span data-stu-id="f1c0a-226">gender</span></span>|<span data-ttu-id="f1c0a-227">male</span><span class="sxs-lookup"><span data-stu-id="f1c0a-227">male</span></span>| 
    <span data-ttu-id="f1c0a-228">school</span><span class="sxs-lookup"><span data-stu-id="f1c0a-228">school</span></span>|<span data-ttu-id="f1c0a-229">MIT</span><span class="sxs-lookup"><span data-stu-id="f1c0a-229">MIT</span></span>| 

7. <span data-ttu-id="f1c0a-230">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="f1c0a-230">Click **OK**.</span></span> 

8. <span data-ttu-id="f1c0a-231">Cliquez sur **appliquer le filtre** avec la valeur par défaut hello `g.V()` filtre.</span><span class="sxs-lookup"><span data-stu-id="f1c0a-231">Click **Apply Filter** with hello default `g.V()` filter.</span></span> <span data-ttu-id="f1c0a-232">Tous les utilisateurs de hello affichent désormais Bonjour **résultats** liste.</span><span class="sxs-lookup"><span data-stu-id="f1c0a-232">All of hello users now show in hello **Results** list.</span></span> <span data-ttu-id="f1c0a-233">Lorsque vous ajoutez davantage de données, vous pouvez utiliser des filtres toolimit vos résultats.</span><span class="sxs-lookup"><span data-stu-id="f1c0a-233">As you add more data, you can use filters toolimit your results.</span></span> <span data-ttu-id="f1c0a-234">Par défaut, l’Explorateur de données utilise `g.V()` tooretrieve tous les sommets dans un graphique, mais vous peuvent modifier ce tooa différents [requête graph](tutorial-query-graph.md), tel que `g.V().count()`, tooreturn un nombre de tous les sommets hello dans graph hello au format JSON.</span><span class="sxs-lookup"><span data-stu-id="f1c0a-234">By default, Data Explorer uses `g.V()` tooretrieve all vertices in a graph, but you can change that tooa different [graph query](tutorial-query-graph.md), such as `g.V().count()`, tooreturn a count of all hello vertices in hello graph in JSON format.</span></span>

9. <span data-ttu-id="f1c0a-235">À présent, nous pouvons connecter rakesh et ashley.</span><span class="sxs-lookup"><span data-stu-id="f1c0a-235">Now we can connect rakesh and ashley.</span></span> <span data-ttu-id="f1c0a-236">Vérifiez **Alice** activée dans hello **résultats** liste, puis cliquez sur bouton de modification hello suivant trop**cibles** en bas à droite.</span><span class="sxs-lookup"><span data-stu-id="f1c0a-236">Ensure **ashley** in selected in hello **Results** list, then click hello edit button next too**Targets** on lower right side.</span></span> <span data-ttu-id="f1c0a-237">Vous devrez peut-être toowiden votre hello toosee de fenêtre **propriétés** zone.</span><span class="sxs-lookup"><span data-stu-id="f1c0a-237">You may need toowiden your window toosee hello **Properties** area.</span></span>

   ![Modifier la cible d’un sommet dans un graphique hello](./media/create-graph-java/azure-cosmosdb-data-explorer-edit-target.png)

10. <span data-ttu-id="f1c0a-239">Bonjour **cible** zone *rakesh*et Bonjour **étiquette du bord** zone *sait*, puis cliquez sur la case à cocher hello.</span><span class="sxs-lookup"><span data-stu-id="f1c0a-239">In hello **Target** box type *rakesh*, and in hello **Edge label** box type *knows*, and then click hello check box.</span></span>

   ![Ajouter une connexion entre ashley et rakesh dans l’Explorateur de données](./media/create-graph-java/azure-cosmosdb-data-explorer-set-target.png)

11. <span data-ttu-id="f1c0a-241">Sélectionnez à présent **rakesh** à partir de la liste des résultats hello et voir qu’Alice et rakesh sont connectés.</span><span class="sxs-lookup"><span data-stu-id="f1c0a-241">Now select **rakesh** from hello results list and see that ashley and rakesh are connected.</span></span> 

   ![Deux vertex connectés dans l’Explorateur de données](./media/create-graph-java/azure-cosmosdb-graph-explorer.png)

    <span data-ttu-id="f1c0a-243">Vous pouvez également utiliser les procédures de toocreate stockée Explorateur de données, UDF et déclencheurs tooperform ainsi la logique métier côté serveur en tant que le débit de l’échelle.</span><span class="sxs-lookup"><span data-stu-id="f1c0a-243">You can also use Data Explorer toocreate stored procedures, UDFs, and triggers tooperform server-side business logic as well as scale throughput.</span></span> <span data-ttu-id="f1c0a-244">Explorateur de données expose l’ensemble du hello intégrées par programmation l’accès aux données disponibles dans l’API de hello, mais il fournit des données un accès facile tooyour hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="f1c0a-244">Data Explorer exposes all of hello built-in programmatic data access available in hello APIs, but provides easy access tooyour data in hello Azure portal.</span></span>



## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="f1c0a-245">Passez en revue les SLA dans hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="f1c0a-245">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="f1c0a-246">Supprimer des ressources</span><span class="sxs-lookup"><span data-stu-id="f1c0a-246">Clean up resources</span></span>

<span data-ttu-id="f1c0a-247">Si vous n’allez toocontinue toouse cette application, supprimez toutes les ressources créées par ce démarrage rapide Bonjour portail Azure par hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="f1c0a-247">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span> 

1. <span data-ttu-id="f1c0a-248">À partir du menu de gauche hello Bonjour portail Azure, cliquez sur **groupes de ressources** puis cliquez sur nom hello de ressource hello vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="f1c0a-248">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="f1c0a-249">Dans la page de votre groupe de ressources, cliquez sur **supprimer**, tapez nom hello de hello ressources toodelete dans la zone de texte hello, puis cliquez sur **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="f1c0a-249">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f1c0a-250">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f1c0a-250">Next steps</span></span>

<span data-ttu-id="f1c0a-251">Ce guide de démarrage rapide, vous avez appris comment toocreate un compte de base de données Azure Cosmos, créer un graphique à l’aide de hello Explorateur de données et exécuter une application.</span><span class="sxs-lookup"><span data-stu-id="f1c0a-251">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, create a graph using hello Data Explorer, and run an app.</span></span> <span data-ttu-id="f1c0a-252">Vous pouvez maintenant générer des requêtes plus complexes et implémenter une logique de traversée de graphique puissante, à l’aide de Gremlin.</span><span class="sxs-lookup"><span data-stu-id="f1c0a-252">You can now build more complex queries and implement powerful graph traversal logic using Gremlin.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="f1c0a-253">Interroger à l’aide de Gremlin</span><span class="sxs-lookup"><span data-stu-id="f1c0a-253">Query using Gremlin</span></span>](tutorial-query-graph.md)

