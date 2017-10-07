---
title: "aaaAzure instructions de réglage des performances données Lake Store | Documents Microsoft"
description: "Recommandations en matière d’optimisation des performances d’Azure Data Lake Store"
services: data-lake-store
documentationcenter: 
author: stewu
manager: amitkul
editor: cgronlun
ms.assetid: ebde7b9f-2e51-4d43-b7ab-566417221335
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/30/2017
ms.author: stewu
ms.openlocfilehash: 939faa068c0f81d18d9533956f4d336bc4d0cbe3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tuning-azure-data-lake-store-for-performance"></a>Paramétrage d’Azure Data Lake Store pour les performances

Data Lake Store prend en charge un débit élevé pour l’analyse intensive des E/S et le déplacement des données.  Dans Azure Data Lake Store, à l’aide de débit disponible : quantité de hello de données qui peuvent être lues ou écrites par seconde – est tooget importante des performances optimales hello.  Pour cela, il convient d’effectuer le plus possible de lectures et d’écritures en parallèle.

![Performances de Data Lake Store](./media/data-lake-store-performance-tuning-guidance/throughput.png)

Azure Data Lake Store peut évoluer tooprovide hello nécessaires de débit pour tout scénario d’analytique. Par défaut, un compte Azure Data Lake Store fournit automatiquement suffisamment de débit besoins hello toomeet une vaste catégorie de cas d’usage. Pour les cas de hello où les clients exécutent dans la limite par défaut hello, hello compte ADLS peut être configuré tooprovide plus grand débit en contactant le support technique de Microsoft.

## <a name="data-ingestion"></a>Ingestion de données

Lors de la réception des données à partir d’un tooADLS du système source, il est important de tooconsider qui hello matériel de la source, le matériel de réseau source et tooADLS de connectivité réseau peut être le goulet d’étranglement hello.  

![Performances de Data Lake Store](./media/data-lake-store-performance-tuning-guidance/bottleneck.png)

Il est important de tooensure qui hello le déplacement des données n’est pas affectée par ces facteurs.

### <a name="source-hardware"></a>Matériel source

Si vous utilisez des ordinateurs locaux ou des machines virtuelles dans Azure, vous devez choisir avec soin matériel approprié de hello. Pour le matériel du disque Source, préférez les disques SSD tooHDDs et choisir les disques physiques avec des piles de disques plus rapides. Pour le matériel de réseau Source, utilisez possible de cartes réseau hello plus rapide.  Sur Azure, nous vous recommandons de machines virtuelles de D14 Azure qui présentent le disque correctement puissant de hello et matériel réseau.

### <a name="network-connectivity-tooazure-data-lake-store"></a>Réseau de connectivité tooAzure Data Lake Store

Hello connectivité entre vos données sources et le magasin d’Azure Data Lake peut parfois être goulot d’étranglement hello. Lorsque vos données sources sont locales, envisagez d’utiliser une liaison dédiée avec [Azure ExpressRoute](https://azure.microsoft.com/en-us/services/expressroute/). Si vos données sources dans Azure, les performances de hello convient le mieux lorsque les données de salutation sont Bonjour même région Azure que hello Data Lake Store.

### <a name="configure-data-ingestion-tools-for-maximum-parallelization"></a>Configuration des outils d’ingestion des données pour une parallélisation maximale

Une fois que vous avez traité matériel de source de hello réseau et les goulots d’étranglement de la connectivité ci-dessus, vous êtes prêt tooconfigure vos outils de réception. Hello tableau suivant résume les paramètres de clé hello pour plusieurs outils d’ingestion populaires et fournit détaillées de réglage des performances articles pour eux.  toolearn plus d’informations sur les outils toouse pour votre scénario, visitez ce [article](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-data-scenarios).

| Outil               | Paramètres     | Détails supplémentaires                                                                 |
|--------------------|------------------------------------------------------|------------------------------|
| PowerShell       | PerFileThreadCount, ConcurrentFileCount |  [Lien](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-get-started-powershell#performance-guidance-while-using-powershell)   |
| AdlCopy    | Unités Azure Data Lake Analytics  |   [Lien](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-copy-data-azure-storage-blob#performance-considerations-for-using-adlcopy)         |
| DistCp            | -m (mappeur)   | [Lien](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-copy-data-wasb-distcp#performance-considerations-while-using-distcp)                             |
| Azure Data Factory| parallelCopies    | [Lien](../data-factory/data-factory-copy-activity-performance.md)                          |
| Sqoop           | fs.azure.block.size, -m (mappeur)    |   [Lien](https://blogs.msdn.microsoft.com/bigdatasupport/2015/02/17/sqoop-job-performance-tuning-in-hdinsight-hadoop/)        |

## <a name="structure-your-data-set"></a>Structure de votre jeu de données

Lorsque les données stockées dans Data Lake Store, la taille du fichier hello, nombre de fichiers et la structure de dossiers ont un impact sur les performances.  Hello section suivante décrit les meilleures pratiques dans ces domaines.  

### <a name="file-size"></a>Taille du fichier

En règle générale, les moteurs d’analytique comme HDInsight et Azure Data Lake Analytics affichent une surcharge par fichier.  Si vous stockez vos données sous forme de petits fichiers nombreux, cela peut nuire aux performances.  

De manière générale, organisez vos données dans de grands fichiers pour des performances optimales.  Il convient d’organiser les jeux de données dans des fichiers de 256 Mo ou plus. Dans certains cas, comme des images et des données binaires, il n’est pas possible de tooprocess leur en parallèle.  Dans ces cas, il est recommandé de tookeep des fichiers individuels moins de 2 Go.

Parfois, des pipelines de données ont un contrôle limité sur les données brutes hello qui possède un grand nombre de petits fichiers.  Il est recommandé de toohave un processus « cuisine » qui génère la plus grande fichiers toouse pour les applications en aval.  

### <a name="organizing-time-series-data-in-folders"></a>Organisation des données de série chronologique dans des dossiers

Pour les charges de travail Hive et ADLA, nettoyage de partition de données de série chronologique peut aider à certaines requêtes uniquement un sous-ensemble des données hello qui améliore les performances de lecture.    

Ces pipelines d’ingestion des données de série chronologique, organisent souvent leurs fichiers selon une structure d’appellation très structurée pour les fichiers et les dossiers. Découvrez ci-après un exemple très courant de données structurées par date :

    \DataSet\YYYY\MM\DD\datafile_YYYY_MM_DD.tsv

Notez que les informations de date/heure hello apparaissent à la fois en tant que dossiers et nom de fichier hello.

Date et heure, hello Voici un modèle commun

    \DataSet\YYYY\MM\DD\HH\mm\datafile_YYYY_MM_DD_HH_mm.tsv

Là encore, choix hello avec l’organisation de fichiers et de dossiers hello conseillé d’optimiser les tailles de fichiers supérieures hello et un nombre raisonnable de fichiers dans chaque dossier.

## <a name="optimizing-io-intensive-jobs-on-hadoop-and-spark-workloads-on-hdinsight"></a>Optimisation des tâches à usage intensif d’E/S sur les charges de travail Hadoop et Spark sur HDInsight

Travaux se répartissent dans hello suivant trois catégories :

* **Usage intensif du processeur.**  Ces tâches nécessitent de longues heures de calcul avec un minimum de temps d’E/S.  L’exemple inclut les tâches de traitement en langage naturel et Machine Learning.  
* **Utilisation intensive de la mémoire.**  Ces tâches utilisent beaucoup de mémoire.  Exemples : PageRank et travaux d’analytique en temps réel.  
* **Usage intensif des E/S.**  La plus grande partie du temps de ces tâches est consacrée aux E/S.  Exemple courant : tâche de copie qui ne traite que les opérations de lecture et écriture.  D’autres exemples incluent les travaux de préparation de données lire une grande quantité de données, effectue une transformation de données, et puis écritures hello magasin de données toohello précédent.  

Hello suivant instructions est uniquement applicables travaux intensifs tooI/O.

### <a name="general-considerations-for-an-hdinsight-cluster"></a>Considérations générales pour les clusters HDInsight

* **Versions HDInsight.** Pour de meilleures performances, utilisez hello dernière version de HDInsight.
* **Régions.** Placez hello Data Lake Store Bonjour même région que le cluster HDInsight de hello.  

Un cluster HDInsight est composé de deux nœuds principaux et de nœuds Worker. Chaque nœud de travail fournit un nombre spécifique de cœurs et la mémoire, ce qui est déterminé par hello type d’ordinateurs virtuels.  Lorsque vous exécutez une tâche, fils est négociateur de ressource hello qui alloue la mémoire disponible hello et conteneurs toocreate de cœurs.  Chaque conteneur s’exécute la tâche de hello hello tâches toocomplete nécessaires.  Conteneurs sont exécutés dans des tâches parallèles tooprocess rapidement. Par conséquent, l’exécution du plus grand nombre possible de conteneurs en parallèle permet d’améliorer les performances.

Il existe trois couches au sein d’un cluster HDInsight qui peut être analysé tooincrease hello le nombre de conteneurs et utilisent débit toutes disponible.  

* **Couche physique**
* **Couche YARN**
* **Couche de charge de travail**

### <a name="physical-layer"></a>Couche physique

**Exécutez le cluster avec le plus de nœuds et/ou les plus grosses machines virtuelles.**  Un cluster plus grand activera vous toorun plusieurs conteneurs fils comme indiqué dans l’image hello ci-dessous.

![Performances de Data Lake Store](./media/data-lake-store-performance-tuning-guidance/VM.png)

**Utilisez des machines virtuelles avec davantage de bande passante réseau.**  bande passante Hello peut être un goulot d’étranglement s’il existe moins de bande passante réseau que le débit de Data Lake Store.  La taille de la bande passante réseau varie en fonction des machines virtuelles.  Choisissez un type de machine virtuelle qui a hello plus grand possible la bande passante réseau.

### <a name="yarn-layer"></a>Couche YARN

**Utilisez des conteneurs YARN plus petits.**  Réduire la taille de hello de chaque toocreate de conteneur fils plusieurs conteneurs avec hello même quantité de ressources.

![Performances de Data Lake Store](./media/data-lake-store-performance-tuning-guidance/small-containers.png)

En fonction de votre charge de travail, il y aura toujours une taille de conteneur YARN minimale requise. Si vous sélectionnez un conteneur trop petit, vos tâches rencontreront des problèmes de mémoire insuffisante. En général, les conteneurs YARN ne doivent pas être inférieurs à 1 Go. Il s’agit des conteneurs de fils de 3 Go toosee communs. Pour certaines charges de travail, des conteneurs YARN plus grands peuvent être nécessaires.  

**Augmentez le nombre de cœurs par conteneur YARN.**  Augmentez le nombre hello de cœurs alloué tooeach conteneur tooincrease hello nombre de tâches parallèles qui s’exécutent dans chaque conteneur.  Cela fonctionne pour des applications comme Spark qui exécutent plusieurs tâches par conteneur.  Pour les applications telles que la ruche qui exécutent un seul thread dans chaque conteneur, il est mieux toohave plusieurs conteneurs plutôt que davantage de cœurs par conteneur.   

### <a name="workload-layer"></a>Couche de charge de travail

**Utilisez tous les conteneurs disponibles.**  Définir nombre hello de tâches toobe égal ou supérieur au nombre de hello de conteneurs disponibles afin que toutes les ressources sont utilisées.

![Performances de Data Lake Store](./media/data-lake-store-performance-tuning-guidance/use-containers.png)

**L’échec des tâches est coûteux.** Si chaque tâche possède une grande quantité de données tooprocess, échec d’une tâche entraîne une nouvelle tentative coûteuse.  Par conséquent, il est mieux toocreate davantage de tâches, chacun traitant une petite quantité de données.

Dans Ajout toohello indications ci-dessus, chaque application possède des paramètres différents de tootune disponibles pour cette application spécifique. Hello ci-dessous répertorie certaines des hello tooget paramètres et des liens en main de réglage des performances pour chaque application.

| Charge de travail               | Tâches tooset de paramètre                                                         |
|--------------------|-------------------------------------------------------------------------------------|
| [Spark sur HDInsight](data-lake-store-performance-tuning-spark.md)       | <ul><li>Num-executors</li><li>Executor-memory</li><li>Executor-cores</li></ul> |
| [Hive sur HDInsight](data-lake-store-performance-tuning-hive.md)    | <ul><li>hive.tez.container.size</li></ul>         |
| [MapReduce sur HDInsight](data-lake-store-performance-tuning-mapreduce.md)            | <ul><li>Mapreduce.map.memory</li><li>Mapreduce.job.maps</li><li>Mapreduce.reduce.memory</li><li>Mapreduce.job.reduces</li></ul> |
| [Storm sur HDInsight](data-lake-store-performance-tuning-storm.md)| <ul><li>Nombre de processus de travail</li><li>Nombre d’instances d’exécuteur de spout</li><li>Nombre d’instances d’exécuteur de bolt </li><li>Nombre de tâches de spout</li><li>Nombre de tâches de bolt</li></ul>|

## <a name="see-also"></a>Voir aussi
* [Présentation d’Azure Data Lake Store](data-lake-store-overview.md)
* [Prise en main d'Azure Data Lake Analytics](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
