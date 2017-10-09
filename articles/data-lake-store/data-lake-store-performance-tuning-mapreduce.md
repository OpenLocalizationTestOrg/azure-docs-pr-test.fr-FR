---
title: "aaaAzure instructions de réglage de données Lake Store MapReduce performances | Documents Microsoft"
description: "Recommandations en matière d’optimisation des performances d’Azure Data Lake Store MapReduce"
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
ms.openlocfilehash: e21414a23530e65613c85156af0209c88ec54d2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="performance-tuning-guidance-for-mapreduce-on-hdinsight-and-azure-data-lake-store"></a>Recommandations en matière d’optimisation des performances pour MapReduce sur HDInsight et Azure Data Lake Store


## <a name="prerequisites"></a>Composants requis

* **Un abonnement Azure**. Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Un compte Azure Data Lake Store**. Pour obtenir des instructions sur la façon de voir d’un seul, toocreate [prise en main Azure Data Lake Store](data-lake-store-get-started-portal.md)
* **Cluster HDInsight Azure** avec accès tooa compte Data Lake Store. Voir [Créer un cluster HDInsight avec Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md). Assurez-vous que vous activez Bureau à distance de cluster de hello.
* **Utilisation de MapReduce sur HDInsight**.  Pour plus d’informations, consultez [Utilisation de MapReduce sur Hadoop sur HDInsight](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-use-mapreduce)  
* **Instructions d’optimisation des performances sur ADLS**.  Pour les concepts généraux sur les performances, consultez [Data Lake Store Performance Tuning Guidance (Recommandations en matière d’optimisation des performances de Data Lake Store)](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-performance-tuning-guidance)  

## <a name="parameters"></a>Paramètres

Lors de l’exécution des travaux MapReduce, voici les paramètres les plus importants hello que vous pouvez configurer les performances tooincrease sur ADLS :

* **MapReduce.Map.Memory.MB** – quantité hello du mappeur de mémoire tooallocate tooeach
* **MapReduce.job.Maps** – hello du nombre de tâches de mappage par travail
* **MapReduce.reduce.Memory.MB** – quantité hello du réducteur de mémoire tooallocate tooeach
* **MapReduce.job.Reduces** – hello nombre de réduire les tâches par travail

**MapReduce.Map.Memory / Mapreduce.reduce.memory** ce nombre doit être ajustée en fonction de la quantité de mémoire est nécessaire pour le mappage de hello et/ou de réduire les tâches.  valeurs par défaut Hello mapreduce.map.memory et mapreduce.reduce.memory peuvent être affichés dans Ambari via la configuration des fils hello.  Dans Ambari, accédez tooYARN et afficher l’onglet des configurations hello.  mémoire des fils de Hello s’affiche.  

**MapReduce.job.Maps / Mapreduce.job.reduces** Cela déterminera le nombre maximal de hello de mappeurs ou REDUCTEURS toobe créé.  nombre Hello de fractionnements détermine combien de mappeurs seront créées pour la tâche MapReduce de hello.  Par conséquent, vous pouvez obtenir des mappeurs de moins que vous avez demandé s’il existe moins fractionnements que nombre hello de mappeurs demandé.       

## <a name="guidance"></a>Assistance

**Étape 1 : Déterminer le nombre de travaux en cours d’exécution** -par défaut, MapReduce utilisera le cluster entier de hello pour votre travail.  Vous pouvez utiliser moins de cluster de hello à l’aide des mappeurs de moins qu’il ne sont conteneurs disponibles.  conseils Hello dans ce document part du principe que votre application est hello uniquement en cours d’exécution sur votre cluster.      

**Étape 2 : Définir mapreduce.map.memory/mapreduce.reduce.memory** : hello la taille de la mémoire hello de carte et réduire les tâches seront dépendantes de votre travail spécifique.  Vous pouvez réduire la taille de la mémoire hello si vous souhaitez tooincrease concurrence.  nombre de Hello de l’exécution simultanée de tâches dépend de nombre hello de conteneurs.  En réduisant la quantité de hello de mémoire par le Mappeur ou réducteur, plusieurs conteneurs peuvent être créés, qui permettent plusieurs toorun de mappeurs ou REDUCTEURS simultanément.  Baisse hello quantité de mémoire trop risque de certains toorun processus mémoire insuffisante.  Si vous obtenez une erreur de segment de mémoire lors de l’exécution de votre travail, vous devez augmenter la mémoire hello par le Mappeur ou réducteur.  Vous devez prendre en compte le fait que l’ajout de conteneurs ajoute une charge pour chaque conteneur supplémentaire, ce qui peut dégrader les performances.  Une autre alternative est tooget plus de mémoire en à l’aide d’un cluster avec une quantité supérieure de mémoire ou en augmentant de nombre de hello de nœuds dans votre cluster.  Plus de mémoire active plus toobe conteneurs utilisé, ce qui signifie que plus de concurrence.  

**Étape 3 : Déterminer la mémoire des fils Total** -tootune mapreduce.job.maps/mapreduce.job.reduces, vous devez envisager montant hello de mémoire fils totale disponible pour utilisation.  Ces informations sont disponibles dans Ambari.  Accédez tooYARN et afficher l’onglet des configurations hello.  mémoire des fils de Hello s’affiche dans cette fenêtre.  Vous devez multiplier hello fils de mémoire avec nombre hello de nœuds dans votre cluster tooget hello fils mémoire.

    Total YARN memory = nodes * YARN memory per node
Si vous utilisez un cluster vide, mémoire peut être hello fils mémoire totale de votre cluster.  Si d’autres applications utilisent la mémoire, vous pouvez choisir tooonly utiliser une partie de mémoire de votre cluster en réduisant le nombre de hello de mappeurs ou REDUCTEURS toohello de conteneurs, vous souhaitez toouse.  

**Étape 4 : Calculer le nombre de conteneurs de fils** – les conteneurs fils dictent quantité hello de concurrence disponible pour le travail de hello.  Prenez la mémoire YARN totale et divisez-la par mapreduce.map.memory.  

    # of YARN containers = total YARN memory / mapreduce.map.memory

**Étape 5 : Définir mapreduce.job.maps/mapreduce.job.reduces** mapreduce.job.maps/mapreduce.job.reduces tooat de définir plus petit nombre de hello de conteneurs disponibles.  Vous pouvez faire des essais supplémentaires en augmentant le nombre de hello de toosee REDUCTEURS et mappeurs si vous obtenez de meilleures performances.  N’oubliez pas que les mappeurs supplémentaires ajouteront une charge, ainsi un trop grand nombre de mappeurs peut dégrader les performances.  

Processeur de planification et d’isolation de l’UC sont désactivés par défaut pour le nombre de hello de conteneurs de fils est limité par la mémoire.

## <a name="example-calculation"></a>Exemple de calcul

Supposons que vous disposez actuellement d’un cluster composé de 8 nœuds D14 et que vous souhaitez toorun un travail intensif d’e/s.  Vous devez effectuer des calculs hello sont :

**Étape 1 : Déterminer le nombre de travaux en cours d’exécution** -dans notre exemple, nous supposons que notre tâche est hello qu’une seule exécution.  

**Étape 2 : Configurer mapreduce.map.memory/mapreduce.reduce.memory** : dans notre exemple, vous exécutez une tâche intensive en E/S et décidez que 3 Go de mémoire suffiront pour les tâches de mappage.

    mapreduce.map.memory = 3GB
**Étape 3 : Déterminer la mémoire YARN totale**

    total memory from hello cluster is 8 nodes * 96GB of YARN memory for a D14 = 768GB
**Étape 4 : Calculer le nombre de conteneurs YARN**

    # of YARN containers = 768GB of available memory / 3 GB of memory =   256

**Étape 5 : Définir mapreduce.job.maps/mapreduce.job.reduces**

    mapreduce.map.jobs = 256

## <a name="limitations"></a>Limites

**Limitation d’ADLS**

En tant que service mutualisé, ADLS définit des limites de bande passante de niveau de compte.  Si vous rencontrez ces limites, vous allez démarrer toosee échecs des tâches. Vous pouvez identifier le problème en consultant les erreurs de limitation dans les journaux des tâches.  Si vous avez besoin de davantage de bande passante pour votre travail, veuillez nous contacter.   

toocheck si vous sont mise en route limitée, vous devez tooenable hello enregistrement de débogage sur côté client de hello. Voici comment procéder :

1. Put hello suivants dans Propriétés du log4j hello dans Ambari > fils > Config > Avancé log4j fils : log4j.logger.com.microsoft.azure.datalake.store=DEBUG

2. Redémarrez tous les nœuds/service hello pour effet de tootake config hello.

3. Si vous l’obtention de sont limitées, vous verrez le code d’erreur HTTP 429 hello dans le fichier journal de fils hello. fichier de journal fils Hello est /tmp/&lt;utilisateur&gt;/yarn.log

## <a name="examples-toorun"></a>Exemples tooRun

toodemonstrate comment MapReduce s’exécute sur Azure Data Lake Store, Voici un exemple de code qui a été exécuté sur un cluster avec hello suivant les paramètres :

* D14v2 16 nœuds
* Cluster Hadoop exécutant HDI 3.6

Pour un point de départ, voici quelques toorun de commandes exemple MapReduce Teragen, Terasort et Teravalidate.  Vous pouvez ajuster ces commandes en fonction de vos ressources.

**Teragen**

    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teragen -Dmapreduce.job.maps=2048 -Dmapreduce.map.memory.mb=3072 10000000000 adl://example/data/1TB-sort-input

**Terasort**

    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar terasort -Dmapreduce.job.maps=2048 -Dmapreduce.map.memory.mb=3072 -Dmapreduce.job.reduces=512 -Dmapreduce.reduce.memory.mb=3072 adl://example/data/1TB-sort-input adl://example/data/1TB-sort-output

**Teravalidate**

    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teravalidate -Dmapreduce.job.maps=512 -Dmapreduce.map.memory.mb=3072 adl://example/data/1TB-sort-output adl://example/data/1TB-sort-validate
