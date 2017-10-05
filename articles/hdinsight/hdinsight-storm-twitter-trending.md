---
title: Rubriques tendances Twitter avec Apache Storm sur HDInsight | Microsoft Docs
description: "Découvrez comment utiliser Trident pour créer une topologie Apache Storm qui détermine les rubriques tendances à partir des hashtags sur Twitter."
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
ms.openlocfilehash: d588221586f151319436525c5098b0bb2694e5f9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="determine-twitter-trending-topics-with-apache-storm-on-hdinsight"></a><span data-ttu-id="a8b5a-103">Détermination de rubriques tendances Twitter avec Apache Storm dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="a8b5a-103">Determine Twitter trending topics with Apache Storm on HDInsight</span></span>

<span data-ttu-id="a8b5a-104">Découvrez comment utiliser Trident pour créer une topologie Storm qui détermine les rubriques tendances (hashtags) sur Twitter.</span><span class="sxs-lookup"><span data-stu-id="a8b5a-104">Learn how to use Trident to create a Storm topology that determines trending topics (hash tags) on Twitter.</span></span>

<span data-ttu-id="a8b5a-105">Trident est une abstraction de haut niveau qui fournit des outils comme les jointures, les agrégations, le regroupement, les fonctions et les filtres.</span><span class="sxs-lookup"><span data-stu-id="a8b5a-105">Trident is a high-level abstraction that provides tools such as joins, aggregations, grouping, functions, and filters.</span></span> <span data-ttu-id="a8b5a-106">En outre, Trident ajoute des primitives pour le traitement incrémentiel avec état.</span><span class="sxs-lookup"><span data-stu-id="a8b5a-106">Additionally, Trident adds primitives for doing stateful, incremental processing.</span></span> <span data-ttu-id="a8b5a-107">L’exemple utilisé dans ce document est une topologie Trident avec un spout et une fonction personnalisés.</span><span class="sxs-lookup"><span data-stu-id="a8b5a-107">The example used in this document is a Trident topology with a custom spout and function.</span></span> <span data-ttu-id="a8b5a-108">Il utilise également plusieurs fonctions intégrées fournies par Trident.</span><span class="sxs-lookup"><span data-stu-id="a8b5a-108">It also uses several built-in functions provided by Trident.</span></span>

## <a name="requirements"></a><span data-ttu-id="a8b5a-109">Configuration requise</span><span class="sxs-lookup"><span data-stu-id="a8b5a-109">Requirements</span></span>

* <span data-ttu-id="a8b5a-110"><a href="http://www.oracle.com/technetwork/java/javase/downloads/index.html" target="_blank">Java et le JDK 1.8</a></span><span class="sxs-lookup"><span data-stu-id="a8b5a-110"><a href="http://www.oracle.com/technetwork/java/javase/downloads/index.html" target="_blank">Java and the JDK 1.8</a></span></span>

* <span data-ttu-id="a8b5a-111"><a href="http://maven.apache.org/what-is-maven.html" target="_blank">Maven</a></span><span class="sxs-lookup"><span data-stu-id="a8b5a-111"><a href="http://maven.apache.org/what-is-maven.html" target="_blank">Maven</a></span></span>

* <span data-ttu-id="a8b5a-112"><a href="http://git-scm.com/" target="_blank">Git</a></span><span class="sxs-lookup"><span data-stu-id="a8b5a-112"><a href="http://git-scm.com/" target="_blank">Git</a></span></span>

* <span data-ttu-id="a8b5a-113">Un compte de développeur Twitter</span><span class="sxs-lookup"><span data-stu-id="a8b5a-113">A Twitter developer account</span></span>

## <a name="download-the-project"></a><span data-ttu-id="a8b5a-114">Téléchargez le projet</span><span class="sxs-lookup"><span data-stu-id="a8b5a-114">Download the project</span></span>

<span data-ttu-id="a8b5a-115">Utilisez le code suivant pour cloner le projet localement.</span><span class="sxs-lookup"><span data-stu-id="a8b5a-115">Use the following code to clone the project locally.</span></span>

    git clone https://github.com/Blackmist/TwitterTrending

## <a name="understanding-the-topology"></a><span data-ttu-id="a8b5a-116">Présentation de la topologie</span><span class="sxs-lookup"><span data-stu-id="a8b5a-116">Understanding the topology</span></span>

<span data-ttu-id="a8b5a-117">Le diagramme suivant présente le flux des données dans cette topologie :</span><span class="sxs-lookup"><span data-stu-id="a8b5a-117">The following diagram shows of how data flows through this topology:</span></span>

![Topologie](./media/hdinsight-storm-twitter-trending/trident.png)

> [!NOTE]
> <span data-ttu-id="a8b5a-119">Ce diagramme est un affichage très simplifié de la topologie.</span><span class="sxs-lookup"><span data-stu-id="a8b5a-119">This diagram is a simplified view of the topology.</span></span> <span data-ttu-id="a8b5a-120">Plusieurs instances des composants sont réparties entre les nœuds du cluster.</span><span class="sxs-lookup"><span data-stu-id="a8b5a-120">Multiple instances of the components are distributed across the nodes in the cluster.</span></span>


<span data-ttu-id="a8b5a-121">Le code Trident qui implémente la topologie est le suivant :</span><span class="sxs-lookup"><span data-stu-id="a8b5a-121">The Trident code that implements the topology is as follows:</span></span>

    topology.newStream("spout", spout)
        .each(new Fields("tweet"), new HashtagExtractor(), new Fields("hashtag"))
        .groupBy(new Fields("hashtag"))
        .persistentAggregate(new MemoryMapState.Factory(), new Count(), new Fields("count"))
        .newValuesStream()
        .applyAssembly(new FirstN(10, "count"))
        .each(new Fields("hashtag", "count"), new Debug());

<span data-ttu-id="a8b5a-122">Le code effectue les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="a8b5a-122">This code performs the following actions:</span></span>

1. <span data-ttu-id="a8b5a-123">Il crée un flux à partir du spout.</span><span class="sxs-lookup"><span data-stu-id="a8b5a-123">Creates a stream from the spout.</span></span> <span data-ttu-id="a8b5a-124">Le spout extrait les tweets de Twitter et les filtres selon des mots clés spécifiques (amour, musique et café dans cet exemple).</span><span class="sxs-lookup"><span data-stu-id="a8b5a-124">The spout retrieves tweets from Twitter, and filters them for specific keywords (love, music, and coffee in this example).</span></span>

2. <span data-ttu-id="a8b5a-125">HashtagExtractor, une fonction personnalisée, est utilisée pour extraire les hashtags de chaque tweet.</span><span class="sxs-lookup"><span data-stu-id="a8b5a-125">HashtagExtractor, a custom function, is used to extract hash tags from each tweet.</span></span> <span data-ttu-id="a8b5a-126">Les hashtags sont transmis au flux de données.</span><span class="sxs-lookup"><span data-stu-id="a8b5a-126">The hash tags are emitted to the stream.</span></span>

3. <span data-ttu-id="a8b5a-127">Le flux est ensuite regroupé par hashtag et transmis à une agrégation.</span><span class="sxs-lookup"><span data-stu-id="a8b5a-127">The stream is grouped by hash tag, and passed to an aggregator.</span></span> <span data-ttu-id="a8b5a-128">Elle produit un décompte du nombre de fois où chaque hashtag s’est produit.</span><span class="sxs-lookup"><span data-stu-id="a8b5a-128">This aggregator creates a count of how many times each hash tag has occurred.</span></span> <span data-ttu-id="a8b5a-129">Ces données sont conservées en mémoire.</span><span class="sxs-lookup"><span data-stu-id="a8b5a-129">This data is persisted in memory.</span></span> <span data-ttu-id="a8b5a-130">Enfin, un nouveau flux de données contenant le hashtag et le compte est émis.</span><span class="sxs-lookup"><span data-stu-id="a8b5a-130">Finally, a new stream is emitted that contains the hash tag and the count.</span></span>

4. <span data-ttu-id="a8b5a-131">L’assembly **FirstN** est appliqué pour renvoyer uniquement les 10 premières valeurs, sur la base du champ de compte.</span><span class="sxs-lookup"><span data-stu-id="a8b5a-131">The **FirstN** assembly is applied to return only the top 10 values, based on the count field.</span></span>

> [!NOTE]
> <span data-ttu-id="a8b5a-132">Pour plus d’informations sur l’utilisation de Trident, consultez la [Présentation de l’API Trident](http://storm.apache.org/releases/current/Trident-API-Overview.html).</span><span class="sxs-lookup"><span data-stu-id="a8b5a-132">For more information on working with Trident, see the [Trident API overview](http://storm.apache.org/releases/current/Trident-API-Overview.html) document.</span></span>

### <a name="the-spout"></a><span data-ttu-id="a8b5a-133">Le spout</span><span class="sxs-lookup"><span data-stu-id="a8b5a-133">The spout</span></span>

<span data-ttu-id="a8b5a-134">Le spout **TwitterSpout** utilise [Twitter4j](http://twitter4j.org/en/) pour extraire des tweets de Twitter.</span><span class="sxs-lookup"><span data-stu-id="a8b5a-134">The spout, **TwitterSpout**, uses [Twitter4j](http://twitter4j.org/en/) to retrieve tweets from Twitter.</span></span> <span data-ttu-id="a8b5a-135">Un filtre est créé pour les mots __aime__, **musique** et **café**.</span><span class="sxs-lookup"><span data-stu-id="a8b5a-135">A filter is created for the words __love__, **music**, and **coffee**.</span></span> <span data-ttu-id="a8b5a-136">Les tweets (status) entrants qui correspondent au filtre sont stockés dans une file d’attente de blocage liée.</span><span class="sxs-lookup"><span data-stu-id="a8b5a-136">Incoming tweets (status) that match the filter are stored in a linked blocking queue.</span></span> <span data-ttu-id="a8b5a-137">Enfin, les éléments sont retirés de la file d’attente et émis dans la topologie.</span><span class="sxs-lookup"><span data-stu-id="a8b5a-137">Finally, items are pulled off the queue and emitted to the topology.</span></span>

### <a name="the-hashtagextractor"></a><span data-ttu-id="a8b5a-138">HashtagExtractor</span><span class="sxs-lookup"><span data-stu-id="a8b5a-138">The HashtagExtractor</span></span>

<span data-ttu-id="a8b5a-139">Pour extraire les hashtags, [getHashtagEntities](http://twitter4j.org/javadoc/twitter4j/EntitySupport.html#getHashtagEntities--) est utilisé pour récupérer tous les hashtags contenus dans le tweet.</span><span class="sxs-lookup"><span data-stu-id="a8b5a-139">To extract hash tags, [getHashtagEntities](http://twitter4j.org/javadoc/twitter4j/EntitySupport.html#getHashtagEntities--) is used to retrieve all hash tags that are contained in the tweet.</span></span> <span data-ttu-id="a8b5a-140">Ils sont transmis au flux de données.</span><span class="sxs-lookup"><span data-stu-id="a8b5a-140">These are then emitted to the stream.</span></span>

## <a name="configure-twitter"></a><span data-ttu-id="a8b5a-141">Configurer Twitter</span><span class="sxs-lookup"><span data-stu-id="a8b5a-141">Configure Twitter</span></span>

<span data-ttu-id="a8b5a-142">Procédez comme suit pour inscrire une nouvelle application Twitter et obtenir les informations de jeton consommateur et d’accès nécessaires pour lire à partir de Twitter :</span><span class="sxs-lookup"><span data-stu-id="a8b5a-142">Use the following steps to register a new Twitter application and obtain the consumer and access token information needed to read from Twitter:</span></span>

1. <span data-ttu-id="a8b5a-143">Accédez à [Applications Twitter](https://apps.twitter.com) et cliquez sur le bouton **Créer une nouvelle application**.</span><span class="sxs-lookup"><span data-stu-id="a8b5a-143">Go to [Twitter Apps](https://apps.twitter.com) and click the **Create new app** button.</span></span> <span data-ttu-id="a8b5a-144">Lorsque vous remplissez le formulaire, laissez le champ **URL de rappel** vide.</span><span class="sxs-lookup"><span data-stu-id="a8b5a-144">When filling in the form, leave the **Callback URL** field empty.</span></span>

2. <span data-ttu-id="a8b5a-145">Lorsque l’application est créée, cliquez sur l'onglet **Clés et jetons d'accès** .</span><span class="sxs-lookup"><span data-stu-id="a8b5a-145">When the app is created, click the **Keys and Access Tokens** tab.</span></span>

3. <span data-ttu-id="a8b5a-146">Copiez les informations de **Clé du client** et de **Question secrète du client**.</span><span class="sxs-lookup"><span data-stu-id="a8b5a-146">Copy the **Consumer Key** and **Consumer Secret** information.</span></span>

4. <span data-ttu-id="a8b5a-147">En bas de la page, sélectionnez **Créer mon jeton d’accès** si aucun jeton n’existe.</span><span class="sxs-lookup"><span data-stu-id="a8b5a-147">At the bottom of the page, select **Create my access token** if no tokens exist.</span></span> <span data-ttu-id="a8b5a-148">Lorsque les jetons sont créés, copiez les informations de **Jeton d’accès** et de **Question secrète du jeton d’accès**.</span><span class="sxs-lookup"><span data-stu-id="a8b5a-148">When the tokens have been created, copy the **Access Token** and **Access Token Secret** information.</span></span>

5. <span data-ttu-id="a8b5a-149">Dans le projet **TwitterSpoutTopology** que vous avez cloné auparavant, ouvrez le fichier **resources/twitter4j.properties**, ajoutez les informations collectées dans les étapes précédentes, puis enregistrez le fichier.</span><span class="sxs-lookup"><span data-stu-id="a8b5a-149">In the **TwitterSpoutTopology** project you previously cloned, open the **resources/twitter4j.properties** file, add the information you gathered in the previous steps, and then save the file.</span></span>

## <a name="build-the-topology"></a><span data-ttu-id="a8b5a-150">Génération de la topologie</span><span class="sxs-lookup"><span data-stu-id="a8b5a-150">Build the topology</span></span>

<span data-ttu-id="a8b5a-151">Utilisez le code suivant pour générer le projet :</span><span class="sxs-lookup"><span data-stu-id="a8b5a-151">Use the following code to build the project:</span></span>

        cd [directoryname]
        mvn compile

## <a name="test-the-topology"></a><span data-ttu-id="a8b5a-152">Test de la topologie</span><span class="sxs-lookup"><span data-stu-id="a8b5a-152">Test the topology</span></span>

<span data-ttu-id="a8b5a-153">Utilisez la commande suivante pour tester la topologie en local :</span><span class="sxs-lookup"><span data-stu-id="a8b5a-153">Use the following command to test the topology locally:</span></span>

    mvn compile exec:java -Dstorm.topology=com.microsoft.example.TwitterTrendingTopology

<span data-ttu-id="a8b5a-154">Après le démarrage de la topologie, vous devez voir des informations de débogage contenant les hashtags et les décomptes émis par la topologie.</span><span class="sxs-lookup"><span data-stu-id="a8b5a-154">After the topology starts, you should see debug information that contains the hash tags and counts emitted by the topology.</span></span> <span data-ttu-id="a8b5a-155">Le résultat doit ressembler au texte suivant :</span><span class="sxs-lookup"><span data-stu-id="a8b5a-155">The output should appear similar to the following text:</span></span>

    DEBUG: [Quicktellervalentine, 7]
    DEBUG: [GRAMMYs, 7]
    DEBUG: [AskSam, 7]
    DEBUG: [poppunk, 1]
    DEBUG: [rock, 1]
    DEBUG: [punkrock, 1]
    DEBUG: [band, 1]
    DEBUG: [punk, 1]
    DEBUG: [indonesiapunkrock, 1]

## <a name="next-steps"></a><span data-ttu-id="a8b5a-156">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a8b5a-156">Next steps</span></span>

<span data-ttu-id="a8b5a-157">Maintenant que vous avez testé la topologie localement, découvrez comment déployer cette topologie : [Déploiement et gestion des topologies Storm sur HDInsight](hdinsight-storm-deploy-monitor-topology.md).</span><span class="sxs-lookup"><span data-stu-id="a8b5a-157">Now that you have tested the topology locally, discover how to deploy the topology: [Deploy and manage Apache Storm topologies on HDInsight](hdinsight-storm-deploy-monitor-topology.md).</span></span>

<span data-ttu-id="a8b5a-158">Les rubriques Storm suivantes peuvent également vous intéresser :</span><span class="sxs-lookup"><span data-stu-id="a8b5a-158">You may also be interested in the following Storm topics:</span></span>

* [<span data-ttu-id="a8b5a-159">Développement de topologies Java pour Storm sur HDInsight à l’aide de Maven</span><span class="sxs-lookup"><span data-stu-id="a8b5a-159">Develop Java topologies for Storm on HDInsight using Maven</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="a8b5a-160">Développement de topologies C# pour Storm sur HDInsight à l’aide de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a8b5a-160">Develop C# topologies for Storm on HDInsight using Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)

<span data-ttu-id="a8b5a-161">Pour obtenir plus d'exemples Storm pour HDInsight :</span><span class="sxs-lookup"><span data-stu-id="a8b5a-161">For more Storm examples for HDInsight:</span></span>

* [<span data-ttu-id="a8b5a-162">Exemples de topologies pour Storm dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="a8b5a-162">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)

