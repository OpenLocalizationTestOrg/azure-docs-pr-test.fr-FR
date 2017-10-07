---
title: "aaaAzure données Lake Store Hive performances instructions de réglage | Documents Microsoft"
description: "Recommandations en matière d’optimisation des performances d’Azure Data Lake Store Hive"
services: data-lake-store
documentationcenter: 
author: stewu
manager: amitkul
editor: stewu
ms.assetid: ebde7b9f-2e51-4d43-b7ab-566417221335
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/19/2016
ms.author: stewu
ms.openlocfilehash: e44daeb6ad3b64e893c709df63b56444a330729f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="performance-tuning-guidance-for-hive-on-hdinsight-and-azure-data-lake-store"></a>Recommandations en matière d’optimisation des performances pour Hive sur HDInsight et Azure Data Lake Store

paramètres par défaut de Hello ont été définies tooprovide bonnes performances sur nombreux différents cas d’usage.  Pour les requêtes d’e/s intensives ruche peut être analysé tooget de meilleures performances avec ADLS.  

## <a name="prerequisites"></a>Composants requis

* **Un abonnement Azure**. Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Un compte Azure Data Lake Store**. Pour obtenir des instructions sur la façon de voir d’un seul, toocreate [prise en main Azure Data Lake Store](data-lake-store-get-started-portal.md)
* **Cluster HDInsight Azure** avec accès tooa compte Data Lake Store. Voir [Créer un cluster HDInsight avec Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md). Assurez-vous que vous activez Bureau à distance de cluster de hello.
* **Exécution de Hive sur HDInsight**.  toolearn sur l’exécution des travaux de la ruche sur HDInsight, consultez [Utilisez Hive dans HDInsight] (https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-use-hive)
* **Instructions d’optimisation des performances sur ADLS**.  Pour les concepts généraux sur les performances, consultez [Data Lake Store Performance Tuning Guidance (Recommandations en matière d’optimisation des performances de Data Lake Store)](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-performance-tuning-guidance)

## <a name="parameters"></a>Paramètres

Voici hello tootune de paramètres plus importante pour améliorer les performances ADLS :

* **Hive.tez.Container.Size** – quantité hello de mémoire utilisée par chaque tâche

* **tez.grouping.min-size** : taille minimale de chaque mappeur

* **tez.grouping.max-size** : taille maximale de chaque mappeur

* **hive.exec.reducer.bytes.per.reducer** : taille de chaque réducteur

**Hive.tez.Container.Size** -taille du conteneur hello détermine la quantité de mémoire est disponible pour chaque tâche.  Il s’agit d’entrée principal de hello pour le contrôle d’accès concurrentiel de hello dans la ruche.  

**taille de tez.GROUPING.min** : ce paramètre vous permet de taille minimale de hello tooset de chaque mappeur.  Si le nombre de hello de mappeurs Tez choisit est inférieure à la valeur hello de ce paramètre, la Tez utilisera la valeur hello définie ici.  

**taille de tez.GROUPING.max** – paramètre hello vous permet de taille maximale de hello tooset de chaque mappeur.  Si le nombre de hello de mappeurs Tez choisit est supérieure à la valeur de ce paramètre hello, Tez utilisera valeur hello définie ici.  

**Hive.Exec.REDUCER.Bytes.per.REDUCER** – ce paramètre définit la taille de hello de chaque réducteur.  Par défaut, chaque réducteur a une taille de 256 Mo.  

## <a name="guidance"></a>Assistance

**Définissez hive.exec.reducer.bytes.per.reducer** – valeur par défaut de hello fonctionne bien lorsque les données de salutation sont décompressées.  Pour les données compressées, vous devez réduire la taille de hello du réducteur de hello.  

**Set hive.tez.container.size** : dans chaque nœud, la mémoire est spécifiée par yarn.nodemanager.resource.memory-mb et doit être correctement définie sur le cluster HDI par défaut.  Pour plus d’informations sur la configuration de la mémoire appropriée hello dans fils, consultez ce [valider](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-hive-out-of-memory-error-oom).

Les charges de travail intensives d’e/s peuvent bénéficier de davantage de parallélisme en réduisant la taille du conteneur Tez hello. Cela permet à utilisateur de hello plusieurs conteneurs qui augmente la concurrence.  Toutefois, certaines requêtes Hive nécessitent une quantité importante de mémoire (par exemple, MapJoin).  Si la tâche hello ne dispose pas de suffisamment de mémoire, vous obtenez une exception de mémoire insuffisante lors de l’exécution.  Si vous recevez des exceptions de mémoire insuffisante, vous devez augmenter les mémoire hello.   

nombre de simultanées Hello de tâches en cours d’exécution ou de parallélisme est délimité par hello totale fils de la mémoire.  Hello de conteneurs de fils indique le nombre de tâches simultané permettre s’exécuter.  toofind hello fils la mémoire par nœud, vous pouvez accéder tooAmbari.  Accédez tooYARN et afficher l’onglet des configurations hello.  mémoire des fils de Hello s’affiche dans cette fenêtre.  

        Total YARN memory = nodes * YARN memory per node
        # of YARN containers = Total YARN memory / Tez container size
les performances de clé tooimproving Hello à l’aide de ADLS sont concurrence de hello tooincrease autant que possible.  Tez calcule automatiquement le nombre de hello de tâches qui doivent être créés afin de vous n’avez pas besoin de tooset il.   

## <a name="example-calculation"></a>Exemple de calcul

Supposons que vous disposez d’un cluster D14 à 8 nœuds.  

    Total YARN memory = nodes * YARN memory per node
    Total YARN memory = 8 nodes * 96GB = 768GB
    # of YARN containers = 768GB / 3072MB = 256

## <a name="limitations"></a>Limites
**Limitation d’ADLS** 

Vous avez atteint les limites de bande passante hello fournie par ADLS, vous devez commencer les échecs des tâches toosee de UIf. Vous pouvez identifier le problème en consultant les erreurs de limitation dans les journaux des tâches.  Vous pouvez réduire le parallélisme de hello en augmentant la taille du conteneur Tez.  Si vous avez besoin de davantage de simultanéité pour votre travail, veuillez nous contacter.   

toocheck si vous sont mise en route limitée, vous devez tooenable hello enregistrement de débogage sur côté client de hello. Voici comment procéder :

1. Placez hello suivant dans Propriétés du log4j hello dans la configuration de la ruche. Cela est possible à partir de la vue de Ambari : log4j.logger.com.microsoft.azure.datalake.store=DEBUG redémarrer tous les nœuds/service hello pour effet de tootake config hello.

2. Si vous l’obtention de sont limitées, vous verrez le code d’erreur HTTP 429 hello dans le fichier journal de ruche hello. fichier journal de ruche Hello est dans /tmp/&lt;utilisateur&gt;/hive.log

## <a name="further-information-on-hive-tuning"></a>Informations supplémentaires sur l’optimisation de Hive

Voici quelques blogs qui vous aideront à optimiser vos requêtes Hive :
* [Optimisation des requêtes Hive pour Hadoop dans HDInsight](https://azure.microsoft.com/en-us/documentation/articles/hdinsight-hadoop-optimize-hive-query/)
* [Résolution des problèmes de performances des requêtes Hive](https://blogs.msdn.microsoft.com/bigdatasupport/2015/08/13/troubleshooting-hive-query-performance-in-hdinsight-hadoop-cluster/)
* [Lancement de la discussion sur l’optimisation de Hive sur HDInsight](https://channel9.msdn.com/events/Machine-Learning-and-Data-Sciences-Conference/Data-Science-Summit-2016/MSDSS25)
