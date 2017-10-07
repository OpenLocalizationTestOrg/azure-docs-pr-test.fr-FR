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
# <a name="determine-twitter-trending-topics-with-apache-storm-on-hdinsight"></a>Détermination de rubriques tendances Twitter avec Apache Storm dans HDInsight

Découvrez comment toouse Trident toocreate une topologie Storm qui détermine l’analyse de tendances rubriques (balises de hachage) sur Twitter.

Trident est une abstraction de haut niveau qui fournit des outils comme les jointures, les agrégations, le regroupement, les fonctions et les filtres. En outre, Trident ajoute des primitives pour le traitement incrémentiel avec état. exemple Hello utilisé dans ce document est une topologie Trident avec un bec personnalisé et une fonction. Il utilise également plusieurs fonctions intégrées fournies par Trident.

## <a name="requirements"></a>Configuration requise

* <a href="http://www.oracle.com/technetwork/java/javase/downloads/index.html" target="_blank">Java et hello JDK 1.8</a>

* <a href="http://maven.apache.org/what-is-maven.html" target="_blank">Maven</a>

* <a href="http://git-scm.com/" target="_blank">Git</a>

* Un compte de développeur Twitter

## <a name="download-hello-project"></a>Télécharger le projet de hello

Utilisez hello suivant du projet de hello tooclone code localement.

    git clone https://github.com/Blackmist/TwitterTrending

## <a name="understanding-hello-topology"></a>Présentation de la topologie de hello

diagramme qui suit de Hello montre de façon dont les données circulent dans cette topologie :

![Topologie](./media/hdinsight-storm-twitter-trending/trident.png)

> [!NOTE]
> Ce diagramme est une vue simplifiée d’une topologie de hello. Plusieurs instances de composants de hello sont répartis entre les nœuds de hello dans un cluster de hello.


Hello code Trident qui implémente la topologie de hello est comme suit :

    topology.newStream("spout", spout)
        .each(new Fields("tweet"), new HashtagExtractor(), new Fields("hashtag"))
        .groupBy(new Fields("hashtag"))
        .persistentAggregate(new MemoryMapState.Factory(), new Count(), new Fields("count"))
        .newValuesStream()
        .applyAssembly(new FirstN(10, "count"))
        .each(new Fields("hashtag", "count"), new Debug());

Ce code exécute hello suivant des actions :

1. Crée un flux de données à partir de bec de hello. bec de Hello récupère tweet Twitter et les filtres de mots clés spécifiques (love, de musique et coffee dans cet exemple).

2. HashtagExtractor, une fonction personnalisée, est utilisé tooextract les balises de hachage à partir de chaque tweet. balises de hachage Hello sont émis toohello flux.

3. flux de Hello est regroupée par balise de hachage et passée tooan aggregator. Elle produit un décompte du nombre de fois où chaque hashtag s’est produit. Ces données sont conservées en mémoire. Enfin, un flux de données qui contient la balise de hachage hello et nombre de hello est émis.

4. Hello **FirstN** assembly est tooreturn appliqué uniquement hello 10 premières valeurs, selon le champ nombre d’hello.

> [!NOTE]
> Pour plus d’informations sur l’utilisation des Trident, consultez hello [présentation de l’API de Trident](http://storm.apache.org/releases/current/Trident-API-Overview.html) document.

### <a name="hello-spout"></a>bec de Hello

bec de Hello, **TwitterSpout**, utilise [Twitter4j](http://twitter4j.org/en/) tweets tooretrieve de Twitter. Un filtre est créé pour les mots hello __adorer__, **musique**, et **café**. Entrants tweets (état) qui correspondent au filtre de hello sont stockés dans une file d’attente de blocage lié. Enfin, les éléments sont extraites en file d’attente hello et émis toohello topologie.

### <a name="hello-hashtagextractor"></a>Hello HashtagExtractor

balises de hachage tooextract, [getHashtagEntities](http://twitter4j.org/javadoc/twitter4j/EntitySupport.html#getHashtagEntities--) est tooretrieve utilisé toutes les balises de hachage qui sont contenus dans un tweet de hello. Ces sont ensuite le flux de données toohello émis.

## <a name="configure-twitter"></a>Configurer Twitter

Utilisez hello suivant les étapes tooregister une nouvelle application Twitter et obtenir des tooread du jeton informations nécessaires hello consommateur et d’accès Twitter :

1. Accédez trop[Twitter des applications](https://apps.twitter.com) et cliquez sur hello **créer une nouvelle application** bouton. Lors du remplissage sous forme de hello, laissez hello **URL de rappel** champ vide.

2. Lors de l’application hello est créée, cliquez sur hello **clés et les jetons d’accès** onglet.

3. Hello de copie **clé de consommateur** et **Secret de consommateur** plus d’informations.

4. Au bas de hello de page de hello, sélectionnez **créer mon jeton d’accès** si aucun jeton n’existe. Création des jetons de hello, hello de copie **jeton d’accès** et **Secret du jeton d’accès** plus d’informations.

5. Bonjour **TwitterSpoutTopology** projet que vous avez précédemment cloné, ouvrez hello **resources/twitter4j.properties** de fichiers, ajouter des informations hello collectées dans les étapes précédentes hello, puis enregistrez le fichier de hello .

## <a name="build-hello-topology"></a>Créez une topologie de hello

Utilisez hello suivant du projet de code toobuild hello :

        cd [directoryname]
        mvn compile

## <a name="test-hello-topology"></a>Topologie de hello de test

Utilisez hello suivant topologie commande tootest hello localement :

    mvn compile exec:java -Dstorm.topology=com.microsoft.example.TwitterTrendingTopology

Après le démarrage de la topologie de hello, vous devez voir les informations de débogage qui contient le hachage de hello balises et les nombres émises par une topologie de hello. une sortie Hello doit apparaître toohello similaire après le texte :

    DEBUG: [Quicktellervalentine, 7]
    DEBUG: [GRAMMYs, 7]
    DEBUG: [AskSam, 7]
    DEBUG: [poppunk, 1]
    DEBUG: [rock, 1]
    DEBUG: [punkrock, 1]
    DEBUG: [band, 1]
    DEBUG: [punk, 1]
    DEBUG: [indonesiapunkrock, 1]

## <a name="next-steps"></a>Étapes suivantes

Maintenant que vous avez testé la topologie hello localement, découvrez comment toodeploy hello topologie : [déployer et gérer les topologies d’Apache Storm sur HDInsight](hdinsight-storm-deploy-monitor-topology.md).

Vous pouvez également être intéressé par hello Storm rubriques suivantes :

* [Développement de topologies Java pour Storm sur HDInsight à l’aide de Maven](hdinsight-storm-develop-java-topology.md)
* [Développement de topologies C# pour Storm sur HDInsight à l’aide de Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md)

Pour obtenir plus d'exemples Storm pour HDInsight :

* [Exemples de topologies pour Storm dans HDInsight](hdinsight-storm-example-topology.md)

