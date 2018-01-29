---
title: "Exécuter des programmes MapReduce personnalisés - Azure HDInsight | Microsoft Docs"
description: "Quand et comment exécuter des programmes MapReduce personnalisés dans HDInsight."
services: hdinsight
documentationcenter: 
author: ashishthaps
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/04/2017
ms.author: ashishth
ms.openlocfilehash: 8e65c946d2cfcc830a1b9fa59b3f7886857f4f7d
ms.sourcegitcommit: be9a42d7b321304d9a33786ed8e2b9b972a5977e
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/19/2018
---
# <a name="run-custom-mapreduce-programs"></a>Exécuter des programmes MapReduce personnalisés

Les systèmes de données volumineux basés sur Hadoop tels que HDInsight permettent de traiter des données à l’aide d’un large éventail d’outils et de technologies. Le tableau suivant décrit les principaux avantages et les considérations de chacun de ces mécanismes.

| Mécanisme de requête | Avantages | Considérations |
| --- | --- | --- |
| **Hive avec HiveQL** | <ul><li>Une excellente solution pour le traitement par lots et l’analyse de grandes quantités de données immuables, pour le résumé des données et pour l’interrogation à la demande. Il utilise une syntaxe de type SQL classique.</li><li>Il peut être utilisé pour générer des tables de données persistantes qui peuvent être facilement partitionnées et indexées.</li><li>Différentes tables et vues externes peuvent être créées sur les mêmes données.</li><li>Il prend en charge une implémentation d’entrepôt de données simple qui fournit des fonctionnalités considérables de montée en charge et de tolérance de panne pour le traitement et le stockage des données.</li></ul> | <ul><li>Il requiert que les données sources possèdent au moins une structure identifiable.</li><li>Il n’est pas approprié pour les requêtes en temps réel et les mises à jour au niveau des lignes. Il est idéal pour les traitements par lots sur des jeux de données volumineux.</li><li>Il est possible qu’il ne puisse pas effectuer certains types de tâches de traitement complexes.</li></ul> |
| **Pig avec Pig Latin** | <ul><li>Une excellente solution pour la manipulation de données sous forme de jeux, la fusion et le filtrage de jeux de données, l’application de fonctions à des enregistrements ou des groupes d’enregistrements, et la restructuration de données par définition de colonnes, regroupement de valeurs ou conversion de colonnes en lignes.</li><li>Il peut utiliser une approche basée sur les flux de travail comme séquence d’opérations sur les données.</li></ul> | <ul><li>Pig Latin peut sembler moins familier et plus difficile à utiliser que HiveQL pour les utilisateurs de SQL.</li><li>La sortie par défaut est généralement un fichier texte et peut donc être plus difficile à utiliser avec des outils de visualisation comme Excel. En général, vous placez une table Hive sur la sortie.</li></ul> |
| **Custom map/reduce** | <ul><li>Il offre un contrôle total sur les phases de mappage et réduction ainsi que sur l’exécution.</li><li>Les requêtes peuvent être optimisées de manière à atteindre les performances maximales du cluster, ou pour minimiser la charge sur les serveurs et le réseau.</li><li>Les composants peuvent être écrits dans divers langages courants.</li></ul> | <ul><li>Il est plus difficile à utiliser que Pig ou Hive, car vous devez créer vos propres composants map et reduce.</li><li>Les processus qui nécessitent de joindre des jeux de données sont plus difficiles à implémenter.</li><li>Bien que des infrastructures de test soient disponibles, le débogage du code est plus complexe que pour une application normale, car le code s’exécute comme un traitement par lots sous le contrôle du planificateur de travaux Hadoop.</li></ul> |
| **HCatalog** | <ul><li>Il résume les informations de chemin d’accès du stockage, ce qui simplifie l’administration et n’oblige pas les utilisateurs à savoir où sont stockées les données.</li><li>Il fournit la notification d’événements tels que la disponibilité des données, ce qui permet à d’autres outils comme Oozie de détecter l’heure d’exécution des opérations.</li><li>Il présente une vue relationnelle des données, notamment le partitionnement par clé, et facilite l’accès aux données.</li></ul> | <ul><li>Il prend en charge les formats de fichier RCFile, texte CSV, texte JSON, SequenceFile et ORC par défaut, mais vous devrez probablement écrire une méthode SerDe personnalisée pour les autres formats.</li><li>HCatalog n’est pas thread-safe.</li><li>Il existe des restrictions sur les types de données des colonnes lors de l’utilisation du chargeur HCatalog dans des scripts Pig. Pour plus d’informations, consultez [Types de données HCatLoader](http://cwiki.apache.org/confluence/display/Hive/HCatalog%20LoadStore#HCatalogLoadStore-HCatLoaderDataTypes) dans la documentation HCatalog Apache.</li></ul> |

En général, vous utilisez l’approche la plus simple permettant de fournir les résultats recherchés. Par exemple, vous pouvez obtenir ces résultats en utilisant simplement Hive, mais pour les scénarios plus complexes, vous devrez peut-être utiliser Pig, ou encore écrire vos propres composants map et reduce. Vous pouvez également décider, après avoir essayé Hive ou Pig, que des composants map et reduce personnalisés pourraient offrir de meilleures performances en vous permettant d’affiner et d’optimiser le traitement.

## <a name="custom-mapreduce-components"></a>Composants map/reduce personnalisés

Le code map/reduce est composé de deux fonctions distinctes implémentées en tant que composants **map** et **reduce**. Le composant **map** est exécuté en parallèle sur plusieurs nœuds de cluster, chacun appliquant le mappage à son propre sous-ensemble de données. Le composant **reduce** rassemble et résume les résultats de toutes les fonctions de mappage. Pour plus d’informations sur ces deux composants, consultez [Utilisation de MapReduce dans Hadoop sur HDInsight](hdinsight-use-mapreduce.md).

Dans la plupart des scénarios de traitement HDInsight, il est plus simple et plus efficace d’utiliser une abstraction de haut niveau telle que Pig ou Hive. Vous pouvez également créer des composants map et reduce personnalisés à utiliser dans des scripts Hive pour un traitement plus sophistiqué.

Les composants map/reduce sont généralement écrits en Java. Hadoop fournit une interface de streaming qui permet également d’utiliser des composants développés dans d’autres langages tels que C#, F#, Visual Basic, Python et JavaScript.

* Pour connaître la procédure de développement de programmes Java MapReduce personnalisés, consultez [Développement de programmes Java MapReduce pour Hadoop dans HDInsight](apache-hadoop-develop-deploy-java-mapreduce-linux.md).
* Pour voir un exemple utilisant Python, consultez [Développement de programmes MapReduce de diffusion en continu Python pour HDInsight](apache-hadoop-streaming-python.md).

Vous devez envisager de créer vos propres composants map et reduce dans les conditions suivantes :

* Vous devez traiter des données totalement non structurées à l’aide d’une analyse et d’une logique personnalisée pour en tirer des informations structurées.
* Vous souhaitez effectuer des tâches complexes difficiles (voire impossibles) à exprimer en Pig ou Hive sans avoir recours à la création d’une fonction définie par l’utilisateur. Par exemple, vous devrez peut-être utiliser un service de géocodage externe pour convertir des coordonnées de latitude et de longitude ou des adresses IP dans les données sources en noms d’emplacements géographiques.
* Vous souhaitez réutiliser votre code .NET, Python ou JavaScript existant dans les composants map/reduce à l’aide de l’interface de streaming Hadoop.

## <a name="upload-and-run-your-custom-mapreduce-program"></a>Charger et exécuter votre programme MapReduce personnalisé

Les programmes MapReduce les plus courants sont écrits en Java et compilés dans un fichier jar.

1. Une fois que vous avez développé, compilé et testé votre programme MapReduce, utilisez la commande `scp` pour charger votre fichier jar dans le nœud principal.

    ```bash
    scp mycustomprogram.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    Remplacez **USERNAME** par le compte d’utilisateur SSH de votre cluster. Remplacez **CLUSTERNAME** par le nom du cluster. Si vous utilisez un mot de passe pour sécuriser votre compte SSH, vous êtes invité à le saisir. Si vous avez utilisé un certificat, vous devrez peut-être utiliser le paramètre `-i` pour spécifier le fichier de clé privée.

2. Connectez-vous au cluster à l’aide de [SSH](../hdinsight-hadoop-linux-use-ssh-unix.md).

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

3. À partir de la session SSH, exécutez votre programme MapReduce via YARN.

    ```bash
    yarn jar mycustomprogram.jar mynamespace.myclass /example/data/sample.log /example/data/logoutput
    ```

    Cette commande envoie la tâche MapReduce à YARN. Le fichier d’entrée est `/example/data/sample.log`, et le répertoire de sortie est `/example/data/logoutput`. Le fichier d’entrée et tous les fichiers de sortie sont stockés dans le stockage par défaut du cluster.

## <a name="next-steps"></a>étapes suivantes

* [Utilisation de C# avec streaming MapReduce sur Hadoop dans HDInsight](apache-hadoop-dotnet-csharp-mapreduce-streaming.md)
* [Développer des programmes MapReduce Java pour Hadoop sur HDInsight](apache-hadoop-develop-deploy-java-mapreduce-linux.md)
* [Développement de programmes MapReduce de diffusion en continu Python pour HDInsight](apache-hadoop-streaming-python.md)
* [Utiliser le kit de ressources Azure pour Eclipse afin de créer des applications Spark pour un cluster HDInsight](../spark/apache-spark-eclipse-tool-plugin.md)
* [Utiliser des fonctions définies par l’utilisateur (UDF) Python avec Hive et Pig dans HDInsight](python-udf-hdinsight.md)
