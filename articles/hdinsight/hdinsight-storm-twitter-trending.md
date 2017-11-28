---
title: rubriques de tendances aaaTwitter avec Apache Storm sur HDInsight | Documents Microsoft
description: "Découvrez comment toouse Trident toocreate une topologie d’Apache Storm qui détermine les rubriques des tendances sur Twitter selon hashtags."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 63b280ea-5c07-4dc8-a35f-dccf5a96ba93
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/14/2017
ms.author: larryfr
ms.openlocfilehash: 0281b495d10833c63868b36856c96369b139c553
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="determine-twitter-trending-topics-with-apache-storm-on-hdinsight"></a><span data-ttu-id="65c61-103">Détermination de rubriques tendances Twitter avec Apache Storm dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="65c61-103">Determine Twitter trending topics with Apache Storm on HDInsight</span></span>

<span data-ttu-id="65c61-104">Découvrez comment toouse Trident toocreate une topologie Storm qui détermine l’analyse de tendances rubriques (balises de hachage) sur Twitter.</span><span class="sxs-lookup"><span data-stu-id="65c61-104">Learn how toouse Trident toocreate a Storm topology that determines trending topics (hash tags) on Twitter.</span></span>

<span data-ttu-id="65c61-105">Trident est une abstraction de haut niveau qui fournit des outils comme les jointures, les agrégations, le regroupement, les fonctions et les filtres.</span><span class="sxs-lookup"><span data-stu-id="65c61-105">Trident is a high-level abstraction that provides tools such as joins, aggregations, grouping, functions, and filters.</span></span> <span data-ttu-id="65c61-106">En outre, Trident ajoute des primitives pour le traitement incrémentiel avec état.</span><span class="sxs-lookup"><span data-stu-id="65c61-106">Additionally, Trident adds primitives for doing stateful, incremental processing.</span></span> <span data-ttu-id="65c61-107">exemple Hello utilisé dans ce document est une topologie Trident avec un bec personnalisé et une fonction.</span><span class="sxs-lookup"><span data-stu-id="65c61-107">hello example used in this document is a Trident topology with a custom spout and function.</span></span> <span data-ttu-id="65c61-108">Il utilise également plusieurs fonctions intégrées fournies par Trident.</span><span class="sxs-lookup"><span data-stu-id="65c61-108">It also uses several built-in functions provided by Trident.</span></span>

## <a name="requirements"></a><span data-ttu-id="65c61-109">Configuration requise</span><span class="sxs-lookup"><span data-stu-id="65c61-109">Requirements</span></span>

* <span data-ttu-id="65c61-110"><a href="http://www.oracle.com/technetwork/java/javase/downloads/index.html" target="_blank">Java et hello JDK 1.8</a></span><span class="sxs-lookup"><span data-stu-id="65c61-110"><a href="http://www.oracle.com/technetwork/java/javase/downloads/index.html" target="_blank">Java and hello JDK 1.8</a></span></span>

* <span data-ttu-id="65c61-111"><a href="http://maven.apache.org/what-is-maven.html" target="_blank">Maven</a></span><span class="sxs-lookup"><span data-stu-id="65c61-111"><a href="http://maven.apache.org/what-is-maven.html" target="_blank">Maven</a></span></span>

* <span data-ttu-id="65c61-112"><a href="http://git-scm.com/" target="_blank">Git</a></span><span class="sxs-lookup"><span data-stu-id="65c61-112"><a href="http://git-scm.com/" target="_blank">Git</a></span></span>

* <span data-ttu-id="65c61-113">Un compte de développeur Twitter</span><span class="sxs-lookup"><span data-stu-id="65c61-113">A Twitter developer account</span></span>

## <a name="download-hello-project"></a><span data-ttu-id="65c61-114">Télécharger le projet de hello</span><span class="sxs-lookup"><span data-stu-id="65c61-114">Download hello project</span></span>

<span data-ttu-id="65c61-115">Utilisez hello suivant du projet de hello tooclone code localement.</span><span class="sxs-lookup"><span data-stu-id="65c61-115">Use hello following code tooclone hello project locally.</span></span>

    git clone https://github.com/Blackmist/TwitterTrending

## <a name="understanding-hello-topology"></a><span data-ttu-id="65c61-116">Présentation de la topologie de hello</span><span class="sxs-lookup"><span data-stu-id="65c61-116">Understanding hello topology</span></span>

<span data-ttu-id="65c61-117">diagramme qui suit de Hello montre de façon dont les données circulent dans cette topologie :</span><span class="sxs-lookup"><span data-stu-id="65c61-117">hello following diagram shows of how data flows through this topology:</span></span>

![Topologie](./media/hdinsight-storm-twitter-trending/trident.png)

> [!NOTE]
> <span data-ttu-id="65c61-119">Ce diagramme est une vue simplifiée d’une topologie de hello.</span><span class="sxs-lookup"><span data-stu-id="65c61-119">This diagram is a simplified view of hello topology.</span></span> <span data-ttu-id="65c61-120">Plusieurs instances de composants de hello sont répartis entre les nœuds de hello dans un cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="65c61-120">Multiple instances of hello components are distributed across hello nodes in hello cluster.</span></span>


<span data-ttu-id="65c61-121">Hello code Trident qui implémente la topologie de hello est comme suit :</span><span class="sxs-lookup"><span data-stu-id="65c61-121">hello Trident code that implements hello topology is as follows:</span></span>

    topology.newStream("spout", spout)
        .each(new Fields("tweet"), new HashtagExtractor(), new Fields("hashtag"))
        .groupBy(new Fields("hashtag"))
        .persistentAggregate(new MemoryMapState.Factory(), new Count(), new Fields("count"))
        .newValuesStream()
        .applyAssembly(new FirstN(10, "count"))
        .each(new Fields("hashtag", "count"), new Debug());

<span data-ttu-id="65c61-122">Ce code exécute hello suivant des actions :</span><span class="sxs-lookup"><span data-stu-id="65c61-122">This code performs hello following actions:</span></span>

1. <span data-ttu-id="65c61-123">Crée un flux de données à partir de bec de hello.</span><span class="sxs-lookup"><span data-stu-id="65c61-123">Creates a stream from hello spout.</span></span> <span data-ttu-id="65c61-124">bec de Hello récupère tweet Twitter et les filtres de mots clés spécifiques (love, de musique et coffee dans cet exemple).</span><span class="sxs-lookup"><span data-stu-id="65c61-124">hello spout retrieves tweets from Twitter, and filters them for specific keywords (love, music, and coffee in this example).</span></span>

2. <span data-ttu-id="65c61-125">HashtagExtractor, une fonction personnalisée, est utilisé tooextract les balises de hachage à partir de chaque tweet.</span><span class="sxs-lookup"><span data-stu-id="65c61-125">HashtagExtractor, a custom function, is used tooextract hash tags from each tweet.</span></span> <span data-ttu-id="65c61-126">balises de hachage Hello sont émis toohello flux.</span><span class="sxs-lookup"><span data-stu-id="65c61-126">hello hash tags are emitted toohello stream.</span></span>

3. <span data-ttu-id="65c61-127">flux de Hello est regroupée par balise de hachage et passée tooan aggregator.</span><span class="sxs-lookup"><span data-stu-id="65c61-127">hello stream is grouped by hash tag, and passed tooan aggregator.</span></span> <span data-ttu-id="65c61-128">Elle produit un décompte du nombre de fois où chaque hashtag s’est produit.</span><span class="sxs-lookup"><span data-stu-id="65c61-128">This aggregator creates a count of how many times each hash tag has occurred.</span></span> <span data-ttu-id="65c61-129">Ces données sont conservées en mémoire.</span><span class="sxs-lookup"><span data-stu-id="65c61-129">This data is persisted in memory.</span></span> <span data-ttu-id="65c61-130">Enfin, un flux de données qui contient la balise de hachage hello et nombre de hello est émis.</span><span class="sxs-lookup"><span data-stu-id="65c61-130">Finally, a new stream is emitted that contains hello hash tag and hello count.</span></span>

4. <span data-ttu-id="65c61-131">Hello **FirstN** assembly est tooreturn appliqué uniquement hello 10 premières valeurs, selon le champ nombre d’hello.</span><span class="sxs-lookup"><span data-stu-id="65c61-131">hello **FirstN** assembly is applied tooreturn only hello top 10 values, based on hello count field.</span></span>

> [!NOTE]
> <span data-ttu-id="65c61-132">Pour plus d’informations sur l’utilisation des Trident, consultez hello [présentation de l’API de Trident](http://storm.apache.org/releases/current/Trident-API-Overview.html) document.</span><span class="sxs-lookup"><span data-stu-id="65c61-132">For more information on working with Trident, see hello [Trident API overview](http://storm.apache.org/releases/current/Trident-API-Overview.html) document.</span></span>

### <a name="hello-spout"></a><span data-ttu-id="65c61-133">bec de Hello</span><span class="sxs-lookup"><span data-stu-id="65c61-133">hello spout</span></span>

<span data-ttu-id="65c61-134">bec de Hello, **TwitterSpout**, utilise [Twitter4j](http://twitter4j.org/en/) tweets tooretrieve de Twitter.</span><span class="sxs-lookup"><span data-stu-id="65c61-134">hello spout, **TwitterSpout**, uses [Twitter4j](http://twitter4j.org/en/) tooretrieve tweets from Twitter.</span></span> <span data-ttu-id="65c61-135">Un filtre est créé pour les mots hello __adorer__, **musique**, et **café**.</span><span class="sxs-lookup"><span data-stu-id="65c61-135">A filter is created for hello words __love__, **music**, and **coffee**.</span></span> <span data-ttu-id="65c61-136">Entrants tweets (état) qui correspondent au filtre de hello sont stockés dans une file d’attente de blocage lié.</span><span class="sxs-lookup"><span data-stu-id="65c61-136">Incoming tweets (status) that match hello filter are stored in a linked blocking queue.</span></span> <span data-ttu-id="65c61-137">Enfin, les éléments sont extraites en file d’attente hello et émis toohello topologie.</span><span class="sxs-lookup"><span data-stu-id="65c61-137">Finally, items are pulled off hello queue and emitted toohello topology.</span></span>

### <a name="hello-hashtagextractor"></a><span data-ttu-id="65c61-138">Hello HashtagExtractor</span><span class="sxs-lookup"><span data-stu-id="65c61-138">hello HashtagExtractor</span></span>

<span data-ttu-id="65c61-139">balises de hachage tooextract, [getHashtagEntities](http://twitter4j.org/javadoc/twitter4j/EntitySupport.html#getHashtagEntities--) est tooretrieve utilisé toutes les balises de hachage qui sont contenus dans un tweet de hello.</span><span class="sxs-lookup"><span data-stu-id="65c61-139">tooextract hash tags, [getHashtagEntities](http://twitter4j.org/javadoc/twitter4j/EntitySupport.html#getHashtagEntities--) is used tooretrieve all hash tags that are contained in hello tweet.</span></span> <span data-ttu-id="65c61-140">Ces sont ensuite le flux de données toohello émis.</span><span class="sxs-lookup"><span data-stu-id="65c61-140">These are then emitted toohello stream.</span></span>

## <a name="configure-twitter"></a><span data-ttu-id="65c61-141">Configurer Twitter</span><span class="sxs-lookup"><span data-stu-id="65c61-141">Configure Twitter</span></span>

<span data-ttu-id="65c61-142">Utilisez hello suivant les étapes tooregister une nouvelle application Twitter et obtenir des tooread du jeton informations nécessaires hello consommateur et d’accès Twitter :</span><span class="sxs-lookup"><span data-stu-id="65c61-142">Use hello following steps tooregister a new Twitter application and obtain hello consumer and access token information needed tooread from Twitter:</span></span>

1. <span data-ttu-id="65c61-143">Accédez trop[Twitter des applications](https://apps.twitter.com) et cliquez sur hello **créer une nouvelle application** bouton.</span><span class="sxs-lookup"><span data-stu-id="65c61-143">Go too[Twitter Apps](https://apps.twitter.com) and click hello **Create new app** button.</span></span> <span data-ttu-id="65c61-144">Lors du remplissage sous forme de hello, laissez hello **URL de rappel** champ vide.</span><span class="sxs-lookup"><span data-stu-id="65c61-144">When filling in hello form, leave hello **Callback URL** field empty.</span></span>

2. <span data-ttu-id="65c61-145">Lors de l’application hello est créée, cliquez sur hello **clés et les jetons d’accès** onglet.</span><span class="sxs-lookup"><span data-stu-id="65c61-145">When hello app is created, click hello **Keys and Access Tokens** tab.</span></span>

3. <span data-ttu-id="65c61-146">Hello de copie **clé de consommateur** et **Secret de consommateur** plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="65c61-146">Copy hello **Consumer Key** and **Consumer Secret** information.</span></span>

4. <span data-ttu-id="65c61-147">Au bas de hello de page de hello, sélectionnez **créer mon jeton d’accès** si aucun jeton n’existe.</span><span class="sxs-lookup"><span data-stu-id="65c61-147">At hello bottom of hello page, select **Create my access token** if no tokens exist.</span></span> <span data-ttu-id="65c61-148">Création des jetons de hello, hello de copie **jeton d’accès** et **Secret du jeton d’accès** plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="65c61-148">When hello tokens have been created, copy hello **Access Token** and **Access Token Secret** information.</span></span>

5. <span data-ttu-id="65c61-149">Bonjour **TwitterSpoutTopology** projet que vous avez précédemment cloné, ouvrez hello **resources/twitter4j.properties** de fichiers, ajouter des informations hello collectées dans les étapes précédentes hello, puis enregistrez le fichier de hello .</span><span class="sxs-lookup"><span data-stu-id="65c61-149">In hello **TwitterSpoutTopology** project you previously cloned, open hello **resources/twitter4j.properties** file, add hello information you gathered in hello previous steps, and then save hello file.</span></span>

## <a name="build-hello-topology"></a><span data-ttu-id="65c61-150">Créez une topologie de hello</span><span class="sxs-lookup"><span data-stu-id="65c61-150">Build hello topology</span></span>

<span data-ttu-id="65c61-151">Utilisez hello suivant du projet de code toobuild hello :</span><span class="sxs-lookup"><span data-stu-id="65c61-151">Use hello following code toobuild hello project:</span></span>

        cd [directoryname]
        mvn compile

## <a name="test-hello-topology"></a><span data-ttu-id="65c61-152">Topologie de hello de test</span><span class="sxs-lookup"><span data-stu-id="65c61-152">Test hello topology</span></span>

<span data-ttu-id="65c61-153">Utilisez hello suivant topologie commande tootest hello localement :</span><span class="sxs-lookup"><span data-stu-id="65c61-153">Use hello following command tootest hello topology locally:</span></span>

    mvn compile exec:java -Dstorm.topology=com.microsoft.example.TwitterTrendingTopology

<span data-ttu-id="65c61-154">Après le démarrage de la topologie de hello, vous devez voir les informations de débogage qui contient le hachage de hello balises et les nombres émises par une topologie de hello.</span><span class="sxs-lookup"><span data-stu-id="65c61-154">After hello topology starts, you should see debug information that contains hello hash tags and counts emitted by hello topology.</span></span> <span data-ttu-id="65c61-155">une sortie Hello doit apparaître toohello similaire après le texte :</span><span class="sxs-lookup"><span data-stu-id="65c61-155">hello output should appear similar toohello following text:</span></span>

    DEBUG: [Quicktellervalentine, 7]
    DEBUG: [GRAMMYs, 7]
    DEBUG: [AskSam, 7]
    DEBUG: [poppunk, 1]
    DEBUG: [rock, 1]
    DEBUG: [punkrock, 1]
    DEBUG: [band, 1]
    DEBUG: [punk, 1]
    DEBUG: [indonesiapunkrock, 1]

## <a name="next-steps"></a><span data-ttu-id="65c61-156">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="65c61-156">Next steps</span></span>

<span data-ttu-id="65c61-157">Maintenant que vous avez testé la topologie hello localement, découvrez comment toodeploy hello topologie : [déployer et gérer les topologies d’Apache Storm sur HDInsight](hdinsight-storm-deploy-monitor-topology.md).</span><span class="sxs-lookup"><span data-stu-id="65c61-157">Now that you have tested hello topology locally, discover how toodeploy hello topology: [Deploy and manage Apache Storm topologies on HDInsight](hdinsight-storm-deploy-monitor-topology.md).</span></span>

<span data-ttu-id="65c61-158">Vous pouvez également être intéressé par hello Storm rubriques suivantes :</span><span class="sxs-lookup"><span data-stu-id="65c61-158">You may also be interested in hello following Storm topics:</span></span>

* [<span data-ttu-id="65c61-159">Développement de topologies Java pour Storm sur HDInsight à l’aide de Maven</span><span class="sxs-lookup"><span data-stu-id="65c61-159">Develop Java topologies for Storm on HDInsight using Maven</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="65c61-160">Développement de topologies C# pour Storm sur HDInsight à l’aide de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="65c61-160">Develop C# topologies for Storm on HDInsight using Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)

<span data-ttu-id="65c61-161">Pour obtenir plus d'exemples Storm pour HDInsight :</span><span class="sxs-lookup"><span data-stu-id="65c61-161">For more Storm examples for HDInsight:</span></span>

* [<span data-ttu-id="65c61-162">Exemples de topologies pour Storm dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="65c61-162">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)

