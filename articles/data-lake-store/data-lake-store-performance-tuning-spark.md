---
title: "aaaAzure instructions de réglage de données Lake Store Spark performances | Documents Microsoft"
description: "Recommandations en matière d’optimisation des performances d’Azure Data Lake Store Spark"
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
ms.openlocfilehash: da1d172e9cb1199ad95605ea1718e78559f79650
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="performance-tuning-guidance-for-spark-on-hdinsight-and-azure-data-lake-store"></a>Recommandations en matière d’optimisation des performances pour Spark sur HDInsight et Azure Data Lake Store

Lors du paramétrage des performances sur Spark, vous devez tooconsider hello des applications qui s’exécuteront sur votre cluster.  Par défaut, vous pouvez exécuter 4 applications simultanément sur votre cluster HDI (Remarque : hello par défaut est sujet toochange).  Vous pouvez décider des applications moins de toouse afin de pouvoir remplacer les paramètres par défaut de hello et d’utiliser le cluster de hello pour ces applications.  

## <a name="prerequisites"></a>Composants requis

* **Un abonnement Azure**. Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Un compte Azure Data Lake Store**. Pour obtenir des instructions sur la façon de voir d’un seul, toocreate [prise en main Azure Data Lake Store](data-lake-store-get-started-portal.md)
* **Cluster HDInsight Azure** avec accès tooa compte Data Lake Store. Voir [Créer un cluster HDInsight avec Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md). Assurez-vous que vous activez Bureau à distance de cluster de hello.
* **Exécution d’un cluster Spark sur Azure Data Lake Store**.  Pour plus d’informations, consultez [données de tooanalyze du cluster utilisez HDInsight Spark dans Data Lake Store](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-use-with-data-lake-store)
* **Instructions d’optimisation des performances sur ADLS**.  Pour les concepts généraux sur les performances, consultez [Data Lake Store Performance Tuning Guidance (Recommandations en matière d’optimisation des performances de Data Lake Store)](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-performance-tuning-guidance) 

## <a name="parameters"></a>Paramètres

Lors de l’exécution des travaux Spark, voici hello principaux paramètres qui peuvent être des performances tooincrease analysé sur ADLS :

* **Num-exécuteurs** -hello du nombre de tâches simultanées qui peuvent être exécutés.

* **Mémoire de l’exécuteur** -hello quantité de mémoire allouée tooeach exécuteur.

* **Cœurs de l’exécuteur** -nombre hello de cœurs allouée tooeach exécuteur.                     

**Num-exécuteurs** Num-exécuteurs définira le nombre maximal de hello de tâches qui peuvent s’exécuter en parallèle.  nombre réel de Hello de tâches pouvant s’exécuter en parallèle est limitée par la mémoire de hello et de ressources processeur disponibles dans votre cluster.

**Mémoire de l’exécuteur** il s’agit quantité hello de mémoire qui est allouée tooeach exécuteur.  mémoire Hello nécessaire pour chaque exécuteur dépend de la tâche de hello.  Pour les opérations complexes, la mémoire de hello doit toobe plus élevée.  Pour les opérations simples telles que la lecture et l’écriture, les besoins en mémoire seront inférieurs.  Hello quantité de mémoire pour chaque exécuteur peut être affichée dans Ambari.  Dans Ambari, accédez tooSpark et afficher l’onglet des configurations hello.  

**Cœurs de l’exécuteur** cela définit hello de noyaux utilisés par l’exécuteur, qui détermine le nombre de hello de threads parallèles qui peuvent être exécutés par l’exécuteur.  Par exemple, si l’exécuteur-cœurs = 2, puis chaque exécuteur peut exécuter des tâches parallèles 2 exécuteur de hello.  Hello exécuteur-cœurs nécessitent dépendra de travail de hello.  Les travaux intensifs en E/S ne nécessitent pas une grande quantité de mémoire par la tâche, ainsi chaque exécuteur peut gérer davantage de tâches parallèles.

Par défaut, deux cœurs YARN virtuels sont définis pour chaque cœur physique lors de l’exécution de Spark sur HDInsight.  Ce nombre offre un bon équilibre de simultanéité et de quantité de changement de contexte à partir de plusieurs threads.  

## <a name="guidance"></a>Assistance

Lors de l’exécution des charges de travail analytique toowork Spark avec des données dans Data Lake Store, nous vous recommandons d’utiliser hello plus récente HDInsight version tooget hello des performances optimales avec Data Lake Store. Lorsque votre projet est plus intensive d’e/s, certains paramètres peuvent être configuré tooimprove performances.  Azure Data Lake Store est une plateforme de stockage hautement évolutive capable de gérer un débit élevé.  Si le travail de hello se compose principalement de lecture ou d’écriture, puis augmenter d’accès concurrentiel pour tooand d’e/s à partir d’Azure Data Lake Store peut accroître les performances.

Il existe quelques approches générales tooincrease concurrence d’accès les tâches intensives d’e/s.

**Étape 1 : Déterminer le nombre d’applications est en cours d’exécution sur votre cluster** – vous devez connaître le nombre d’applications s’exécutent sur le cluster hello notamment hello en cours.  valeurs par défaut Hello pour chaque Spark paramètre suppose qu’il existe 4 applications qui s’exécutent simultanément.  Par conséquent, vous devez uniquement 25 % de cluster hello disponible pour chaque application.  tooget de meilleur performances, vous pouvez remplacer les valeurs par défaut hello en modifiant le nombre de hello d’exécuteurs.  

**Étape 2 : Définir la mémoire de l’exécuteur** : hello première tooset est hello exécuteur en mémoire.  mémoire de Hello sera dépend de la tâche hello que vous êtes toorun de cours.  Vous pouvez augmenter la simultanéité en allouant de moins de mémoire par exécuteur.  Si vous voyez les exceptions de mémoire insuffisante lors de l’exécution de votre travail, vous devez augmenter valeur hello pour ce paramètre.  Un autre est tooget davantage de mémoire par à l’aide d’un cluster avec une quantité supérieure de mémoire ou en augmentant la taille de hello de votre cluster.  Plus de mémoire active plus toobe exécuteurs utilisé, ce qui signifie que plus de concurrence.

**Étape 3 : Définir des cœurs de l’exécuteur** – pour les e/s intensives les charges de travail qui n’ont pas d’opérations complexes, il est bon toostart comportant un grand nombre de nombre de hello tooincrease cœurs de l’exécuteur de tâches en parallèle par l’exécuteur.  Définition des cœurs de l’exécuteur too4 est un bon début.   

    executor-cores = 4
Augmenter le nombre hello de cœurs de l’exécuteur vous donneront plus de parallélisme afin de faire des essais avec différents de cœurs de l’exécuteur.  Pour les travaux qui ont des opérations plus complexes, vous devez réduire le nombre de hello de cœurs par l’exécuteur.  Si la valeur d’Executor-cores est supérieure à 4, puis le garbage collection peut devenir inefficace et dégrader les performances.

**Étape 4 : Déterminer la quantité de mémoire YARN du cluster** : cette information est disponible dans Ambari.  Accédez tooYARN et afficher l’onglet des configurations hello.  mémoire des fils de Hello s’affiche dans cette fenêtre.  
Remarque : lorsque vous vous trouvez dans la fenêtre hello, vous pouvez également voir taille du conteneur fils hello par défaut.  taille du conteneur fils de Hello est hello identique à la mémoire par le paramètre de l’exécuteur.

    Total YARN memory = nodes * YARN memory per node
**Étape 5 : Calculer num-executors**

**Calculer la contrainte de mémoire** -paramètre num-exécuteurs de hello est limitée par la mémoire ou par processeur.  contrainte de mémoire Hello est déterminée par la quantité hello de mémoire fils disponible pour votre application.  Vous devez prendre la mémoire YARN totale et la diviser par executor-memory.  contrainte de Hello doit toobe, déduplication mis à l’échelle de nombre hello d’applications afin de nous diviser par nombre hello d’applications.

    Memory constraint = (total YARN memory / executor memory) / # of apps   
**Calculer la contrainte de processeur** -hello contrainte de l’UC est calculée comme hello total cœurs virtuels divisés par un nombre de cœurs par l’exécuteur hello.  Il existe 2 cœurs virtuels pour chaque noyau physique.  Contrainte de mémoire toohello semblables, nous avons division par nombre hello d’applications.

    virtual cores = (nodes in cluster * # of physical cores in node * 2)
    CPU constraint = (total virtual cores / # of cores per executor) / # of apps
**Définir les exécuteurs de num** – paramètre num-exécuteurs de hello est déterminée en prenant hello minimale de la contrainte de mémoire hello et une contrainte hello du processeur. 

    num-executors = Min (total virtual Cores / # of cores per executor, available YARN memory / executor-memory)   
Définir un nombre plus élevé pour num-executors’augmente pas nécessairement les performances.  Vous devez prendre en compte le fait que l’ajout d’exécuteurs ajoute une charge pour chaque exécuteur supplémentaire, ce qui peut dégrader les performances.  Num-exécuteurs est limitée par les ressources de cluster hello.    

## <a name="example-calculation"></a>Exemple de calcul

Supposons que vous disposez actuellement d’un cluster composé de 8 nœuds D4v2 qui est en cours d’exécution 2 applications y compris hello celui que vous allez toorun.  

**Étape 1 : Déterminer le nombre d’applications est en cours d’exécution sur votre cluster** – vous savez que vous disposez de 2 des applications sur votre cluster, y compris hello une que vous vous apprêtez toorun.  

**Étape 2 : Configurer executor-memory** : pour cet exemple, nous déterminons que 6 Go pour executor-memory sera suffisant pour les travaux intensifs en E/S.  

    executor-memory = 6GB
**Étape 3 : Définir des cœurs de l’exécuteur** – dans la mesure où il s’agit d’un travail d’e/s intensif, nous pouvons définir nombre hello de cœurs pour chaque too4 exécuteur.  Définition de cœurs par l’exécuteur toolarger que 4 peut entraîner des problèmes de garbage collection.  

    executor-cores = 4
**Étape 4 : Déterminer la quantité de mémoire fils cluster** – nous naviguons toofind tooAmbari out que chaque D4v2 a 25 Go de mémoire de fils.  Étant donné que 8 nœuds, la mémoire disponible fils hello est multipliée par 8.

    Total YARN memory = nodes * YARN memory* per node
    Total YARN memory = 8 nodes * 25GB = 200GB
**Étape 5 : Calculer les exécuteurs de num** – paramètre num-exécuteurs de hello est déterminée en prenant hello minimale de la contrainte de mémoire hello et la contrainte de l’UC de hello divisé par hello # d’applications qui s’exécutent sur Spark.    

**Calculer la contrainte de mémoire** : contrainte de mémoire hello est calculée en tant que mémoire fils totale hello divisée par la mémoire hello par l’exécuteur.

    Memory constraint = (total YARN memory / executor memory) / # of apps   
    Memory constraint = (200GB / 6GB) / 2   
    Memory constraint = 16 (rounded)
**Calculer la contrainte de processeur** -hello contrainte de l’UC est calculée comme hello cœurs fils total divisés par un nombre de cœurs par l’exécuteur hello.
    
    YARN cores = nodes in cluster * # of cores per node * 2   
    YARN cores = 8 nodes * 8 cores per D14 * 2 = 128
    CPU constraint = (total YARN cores / # of cores per executor) / # of apps
    CPU constraint = (128 / 4) / 2
    CPU constraint = 16
**Définir num-executors**

    num-executors = Min (memory constraint, CPU constraint)
    num-executors = Min (16, 16)
    num-executors = 16    

