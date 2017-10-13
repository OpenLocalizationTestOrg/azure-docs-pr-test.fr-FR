---
title: "Notes de publication archivées - Composants Hadoop sur Azure HDInsight | Documents Microsoft"
description: "Notes de publication archivées pour des versions plus anciennes des composants Hadoop pour Azure HDInsight."
services: hdinsight
documentationcenter: 
editor: cgronlun
manager: jhubbard
author: nitinme
tags: azure-portal
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: 04278aac85171601b5801b0890d14a9076060444
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="release-notes-archive-for-hadoop-components-on-azure-hdinsight"></a>Notes de publication (archive) pour les composants Hadoop sur Azure HDInsight

Cet article fournit des informations sur les mises à jour **antérieures** des versions d’Azure HDInsight. Pour plus d’informations sur les versions plus récentes, consultez [Notes de publication de HDInsight](hdinsight-release-notes.md).

> [!IMPORTANT]
> Linux est le seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure. Pour plus d’informations, consultez [l’article sur le contrôle de version de HDInsight](hdinsight-component-versioning.md).



## <a name="notes-for-08302016-release-of-hdinsight"></a>Notes relatives à la version du 30/08/2016 de HDInsight
Numéros de version complets des clusters HDInsight sous Linux déployés avec cette version :

| HDI | Version de cluster HDI | HDP | Build HDP | Build d’Ambari |
| --- | --- | --- | --- | --- |
| 3.2 |3.2.1000.0.8268980 |2.2 |2.2.9.1-19 |2.2.1.12-4 |
| 3.3 |3.3.1000.0.8268980 |2.3 |2.3.3.1-25 |2.2.1.12-4 |
| 3.4 |3.4.1000.0.8269383 |2.4 |2.4.2.4-5 |2.2.1.12-4 |

Numéros de version complets des clusters HDInsight sous Windows déployés avec cette version :

| HDI | Version de cluster HDI | HDP | Build HDP |
| --- | --- | --- | --- |
| 2.1 |2.1.10.1033.2559206 |1.3 |1.3.12.0-01795 |
| 3.0 |3.0.6.1033.2559206 |2.0 |2.0.13.0-2117 |
| 3.1 |3.1.4.1033.2559206 |2.1 |2.1.16.0-2374 |
| 3.2 |3.2.7.1033.2559206 |2.2 |2.2.9.1-11 |
| 3.3 |3.3.0.1033.2559206 |2.3 |2.3.3.1-25 |


## <a name="08172016---release-of-r-server-on-hdinsight"></a>08/17/2016 - Version de R Server sur HDInsight
* R Server 8.0.5 - principalement une version de résolution d’un bogue. Consultez les [Notes de publication de R Server](https://msdn.microsoft.com/microsoft-r/notes/r-server-notes) pour plus d’informations.
* Package AzureML sur le nœud edge – [ce package R](https://cran.r-project.org/web/packages/AzureML/vignettes/getting_started.html) permet de publier et d’utiliser des modèles R en tant que services web Azure ML.  Consultez la section [« Opérationnaliser un modèle »](hdinsight-hadoop-r-server-overview.md#operationalize-a-model) de notre article [« Vue d’ensemble de R Server sur HDInsight »](hdinsight-hadoop-r-server-overview.md) pour plus d’informations.
* Dépendances Linux des [100 packages R les plus populaires](https://github.com/metacran/cranlogs) : ces dépendances de packages Linux sont désormais installées.
* Possibilité d’utiliser le référentiel CRAN lors de l’ajout de packages R aux nœuds de données. Pour plus d’informations, consultez la section [« Prise en main de R Server sur HDInsight »](hdinsight-hadoop-r-server-get-started.md).
* Amélioration de la fiabilité de l’approvisionnement de R Server lors de la création de clusters.

## <a name="notes-for-08012016-release-of-hdinsight"></a>Notes pour la version du 01/08/2016 de HDInsight
Numéros de version complets des clusters HDInsight sous Linux déployés avec cette version :

| HDI | Version de cluster HDI | HDP | Build HDP | Build d’Ambari |
| --- | --- | --- | --- | --- |
| 3.2 |3.2.1000.0.8028416 |2.2 |2.2.9.1-19 |2.2.1.12-4 |
| 3.3 |3.3.1000.0.8028416 |2.3 |2.3.3.1-25 |2.2.1.12-4 |
| 3.4 |3.4.1000.0.8053402 |2.4 |2.4.2.4-5 |2.2.1.12-4 |

Numéros de version complets des clusters HDInsight sous Windows déployés avec cette version :

| HDI | Version de cluster HDI | HDP | Build HDP |
| --- | --- | --- | --- |
| 2.1 |2.1.10.1005.2488842 |1.3 |1.3.12.0-01795 |
| 3.0 |3.0.6.1005.2488842 |2.0 |2.0.13.0-2117 |
| 3.1 |3.1.4.1005.2488842 |2.1 |2.1.16.0-2374 |
| 3.2 |3.2.7.1005.2488842 |2.2 |2.2.9.1-11 |
| 3.3 |3.3.0.1005.2488842 |2.3 |2.3.3.1-25 |

Cette version contient les mises à jour suivantes :

| Intitulé | Description | Zone concernée (par exemple, Service, composant ou Kit de développement logiciel) | Type de cluster (par exemple, Spark, Hadoop, HBase ou Storm) | JIRA (le cas échéant) |
| --- | --- | --- | --- | --- |
| Modifications apportées aux clusters HDInsight 3.4 |Les valeurs par défaut des configurations de Hive suivantes sont modifiées pour optimiser les performances <ul><li>`hive.vectorized.execution.reduce.enabled=true`</li><li>`hive.tez.min.partition.factor=1f`</li><li>`hive.tez.max.partition.factor=3f`</li><li>`tez.shuffle-vertex-manager.min-src-fraction=0.9`</li><li>`tez.shuffle-vertex-manager.max-src-fraction=0.95`</li><li>`tez.runtime.shuffle.connect.timeout= 30000`</li></ul> |Service |Tout |N/A |
| Les correctifs suivants sont inclus dans cette version |HIVE-13632, HIVE-12897,HIVE-12907,HIVE-12908,HIVE-12988,HIVE-13510,HIVE-13572,HIVE-13716,HIVE-13726,HIVE-12505,HIVE-13632,HIVE-13661,HIVE-13705,HIVE-13743,HIVE-13810,HIVE-13857,HIVE-13902,HIVE-13911,HIVE-13933 |de diffusion en continu |Tout |N/A |

## <a name="notes-for-07142016-release-of-hdinsight"></a>Notes pour la version du 14/07/2016 de HDinsight
Numéros de version complets des clusters HDInsight sous Linux déployés avec cette version :

| HDI | Version de cluster HDI | HDP | Build HDP | Build d’Ambari |
| --- | --- | --- | --- | --- |
| 3.2 |3.2.1000.0.7932505 |2.2 |2.2.9.1-11 |2.2.1.12-2 |
| 3.3 |3.3.1000.0.7932505 |2.3 |2.3.3.1-18 |2.2.1.12-2 |
| 3.4 |3.4.1000.0.7933003 |2.4 |2.4.2.0 |2.2.1.12-2 |

Numéros de version complets des clusters HDInsight sous Windows déployés avec cette version :

| HDI | Version de cluster HDI | HDP | Build HDP |
| --- | --- | --- | --- |
| 2.1 |2.1.10.989.2441725 |1.3 |1.3.12.0-01795 |
| 3.0 |3.0.6.989.2441725 |2.0 |2.0.13.0-2117 |
| 3.1 |3.1.4.989.2441725 |2.1 |2.1.16.0-2374 |
| 3.2 |3.2.7.989.2441725 |2.2 |2.2.9.1-11 |
| 3.3 |3.3.0.989.2441725 |2.3 |2.3.3.1-21 |

## <a name="notes-for-07072016-release-of-hdinsight"></a>Notes pour la version du 07/07/2016 de HDinsight
Numéros de version complets des clusters HDInsight sous Linux déployés avec cette version :

| HDI | Version de cluster HDI | HDP | Build HDP |
| --- | --- | --- | --- |
| 3.2 |3.2.1000.0.7864996 |2.2 |2.2.9.1-11 |
| 3.3 |3.3.1000.0.7864996 |2.3 |2.3.3.1-18 |
| 3.4 |3.4.1000.0.7861906 |2.4 |2.4.2.0 |

Numéros de version complets des clusters HDInsight sous Windows déployés avec cette version :

| HDI | Version de cluster HDI | HDP | Build HDP |
| --- | --- | --- | --- |
| 2.1 |2.1.10.977.2413853 |1.3 |1.3.12.0-01795 |
| 3.0 |3.0.6.977.2413853 |2.0 |2.0.13.0-2117 |
| 3.1 |3.1.4.977.2413853 |2.1 |2.1.16.0-2374 |
| 3.2 |3.2.7.977.2413853 |2.2 |2.2.9.1-11 |
| 3.3 |3.3.0.977.2413853 |2.3 |2.3.3.1-21 |

Cette version contient les mises à jour suivantes :

| Intitulé | Description | Zone concernée (par exemple, Service, composant ou Kit de développement logiciel) | Type de cluster (par exemple, Spark, Hadoop, HBase ou Storm) | JIRA (le cas échéant) |
| --- | --- | --- | --- | --- |
| [Outils HDInsight pour IntelliJ](hdinsight-apache-spark-intellij-tool-plugin.md) |Le plug-in IntelliJ IDEA pour les clusters HDInsight Spark est désormais intégré au kit de ressources Azure pour IntelliJ. Il prend en charge Azure SDK v2.9.1, les kits de développement Java les plus récents et inclut toutes les fonctionnalités de la version autonome de HDInsight Plugin pour IntelliJ. |Outils |Spark |N/A |
| [Outils HDInsight pour Eclipse](hdinsight-apache-spark-eclipse-tool-plugin.md) |Le kit de ressources Azure pour Eclipse prend désormais en charge les clusters HDInsight Spark. Il fournit les fonctionnalités suivantes : <ul><li>Créer et écrire une application Spark facilement en Scala et en Java, avec la prise en charge des opérations d’auteur première classe pour IntelliSense, la mise en forme automatique, la vérification des erreurs, etc.</li><li>Tester l’application Spark localement.</li><li>Envoyer des travaux au cluster HDInsight Spark et récupérer les résultats.</li><li>Connectez-vous à Azure et accédez à tous les clusters Spark associés à vos abonnements Azure.</li><li>Accéder à toutes les ressources de stockage associées de votre cluster HDInsight Spark.</li></ul> |Outils |Spark |N/A |

À compter de cette version, nous avons modifié la stratégie de gestion des mises à jour correctives du système d’exploitation invité pour les clusters HDInsight sous Linux. L’objectif de la nouvelle stratégie est de réduire considérablement le nombre de redémarrages dus à la mise à jour corrective. La nouvelle stratégie exécute les correctifs sur des machines virtuelles dans des clusters Linux chaque lundi ou jeudi à partir de minuit (UTC) de manière échelonnée sur les nœuds dans tout cluster donné. Toutefois, toute machine virtuelle donnée ne redémarre qu’une fois tous les 30 jours au maximum en raison de la mise à jour corrective du système d’exploitation invité. En outre, le premier redémarrage d’un cluster nouvellement créé a lieu au plus tôt 30 jours après la date de création du cluster.

> [!NOTE]
> Ces modifications s’appliquent uniquement aux clusters créés dans cette version au minimum.
>
>

## <a name="notes-for-06062016-release-of-hdinsight"></a>Notes relatives à la version du 06/06/2016 de HDInsight
Les numéros de version complets des clusters HDInsight déployés avec cette version sont les suivants :

| HDP | Version de HDI | Version de Spark | Numéro de Build d’Ambari | Numéro de Build de HDP |
| --- | --- | --- | --- | --- |
| 2.3 |3.3.1000.0.7702215 |1.5.2 |2.2.1.8-2 |2.3.3.1-18 |
| 2.4 |3.4.1000.0.7702224 |1.6.1 |2.2.1.8-2 |2.4.2.0 |

Cette version contient les mises à jour suivantes :

| Intitulé | Description | Zone concernée (par exemple, Service, composant ou Kit de développement logiciel) | Type de cluster (par exemple, Spark, Hadoop, HBase ou Storm) | JIRA (le cas échéant) |
| --- | --- | --- | --- | --- |
| Spark sur HDInsight est généralement disponible |Cette version apporte des améliorations en matière de disponibilité, d’extensibilité et de productivité à Apache Spark sur HDInsight open source. <ul><li>Leader du marché avec un contrat de niveau de service (SLA) de 99,9 % pour la disponibilité, qui le rend adapté aux charges de travail importantes des entreprises.</li><li>Couche de stockage évolutive avec Azure Data Lake Store.</li><li>Outils de productivité pour chaque phase de développement et d’exploration des données. Des blocs-notes Jupyter avec noyau Spark personnalisé activent l’exploration interactive des données. L’intégration de tableaux de bord de BI tels que Power BI, Tableau et Qlik est intéressante pour un partage de données rapide et une création de rapports continue. Le plug-in IntelliJ est une option fiable de développement à long terme et de débogage d’artefacts de code.</li></ul> |de diffusion en continu |Spark |N/A |
| Outils HDInsight pour IntelliJ |Il s’agit d’un plug-in IntelliJ IDEA pour les clusters HDInsight Spark. Il fournit les fonctionnalités suivantes :<ul><li>Créer et écrire une application Spark facilement en Scala et en Java, avec la prise en charge des opérations d’auteur première classe pour IntelliSense, la mise en forme automatique, la vérification des erreurs, etc.</li><li>Tester l’application Spark localement.</li><li>Envoyer des travaux au cluster HDInsight Spark et récupérer les résultats.</li><li>Connectez-vous à Azure et accédez à tous les clusters Spark associés à vos abonnements Azure.</li><li>Accéder à toutes les ressources de stockage associées de votre cluster HDInsight Spark.</li><li>Accéder à toutes les informations et à tout l’historique des tâches pour votre cluster HDInsight Spark.</li><li>Déboguer les tâches Spark à distance à partir de votre ordinateur de bureau.</li></ul> |Outils |Spark |N/A |

## <a name="notes-for-05132016-release-of-hdinsight"></a>Notes pour la version du 13/05/2016 de HDInsight
Les numéros de version complets des clusters HDInsight déployés avec cette version sont les suivants :

* HDInsight    (Windows)         2.1.10.875.2159884 (HDP 1.3.12.0-01795 - inchangé)
* HDInsight    (Windows)         3.0.6.875.2159884 (HDP 2.0.13.0-2117 - inchangé)
* HDInsight    (Windows)         3.1.4.922.2266903  (HDP 2.1.15.0-2374 - inchangé)
* HDInsight    (Windows)        3.2.7.922.2266903  (HDP 2.2.9.1-11)
* HDInsight (Windows)        3.3.0.922.2266903  (HDP 2.3.3.1-18)
* HDInsight    (Linux)            3.2.1000.0.7565644   (HDP    2.2.9.1-11)
* HDInsight (Linux)            3.3.1000.0.7565644   (HDP 2.3.3.1-18)
* HDInsight (Linux)            3.4.1000.0.7548380   (HDP 2.4.2.0)

Cette version contient les mises à jour suivantes :

| Intitulé | Description | Zone concernée (par exemple, Service, composant ou Kit de développement logiciel) | Type de cluster (par exemple, Spark, Hadoop, HBase ou Storm) | JIRA (le cas échéant) |
| --- | --- | --- | --- | --- |
| Mise à jour de la version Spark et autres correctifs de bogue |Cette version met à jour la version de Spark dans le cluster HDInsight vers 1.6.1 et corrige d’autres bogues |de diffusion en continu |Spark |N/A |

## <a name="notes-for-04112016-release-of-hdinsight"></a>Notes de publication du 11/04/2016 pour HDInsight
Les numéros de version complets des clusters HDInsight déployés avec cette version sont les suivants :

* HDInsight    (Windows)         2.1.10.889.2191206 (HDP 1.3.12.0-01795 - inchangé)
* HDInsight    (Windows)         3.0.6.889.2191206 (HDP 2.0.13.0-2117 - inchangé)
* HDInsight    (Windows)         3.1.4.889.2191206  (HDP 2.1.15.0-2374 - inchangé)
* HDInsight    (Windows)        3.2.7.889.2191206  (HDP 2.2.9.1-10)
* HDInsight (Windows)        3.3.0.889.2191206  (HDP 2.3.3.1-16 - inchangé)
* HDInsight    (Linux)            3.2.1000.0.7339916   (HDP 2.2.9.1-10)
* HDInsight (Linux)            3.3.1000.0.7339916   (HDP 2.3.3.1-16)
* HDInsight (Linux)            3.4.1000.0.7338911   (HDP 2.4.1.1-3)
* Kit de développement logiciel (SDK)            1.5.8

Cette version contient les mises à jour suivantes :

| Intitulé | Description | Zone concernée (par exemple, Service, composant ou Kit de développement logiciel) | Type de cluster (par exemple, Hadoop, HBase ou Storm) | JIRA (le cas échéant) |
| --- | --- | --- | --- | --- |
| Problèmes de mise à niveau personnalisée du metastore pour HDI 3.4 |La création du cluster échouait si vous utilisiez un metastore personnalisé auparavant utilisé sur une version antérieure d’un autre cluster HDInsight. Cela était dû à une erreur de script de mise à niveau qui a maintenant été résolue |Création du cluster |Tout |N/A |
| Récupération après blocage de Livy |Fournit la résilience de l’état du travail pour tout travail soumis via Livy |Fiabilité |Spark sous Linux |N/A |
| Haute disponibilité du contenu de Jupyter |Fournit la capacité d’enregistrer et de charger les contenus des blocs-notes Jupyter depuis et vers le compte de stockage associé au cluster. Pour plus d’informations, consultez [Noyaux disponibles pour les blocs-notes Jupyter](hdinsight-apache-spark-jupyter-notebook-kernels.md). |Blocs-notes |Spark sous Linux |N/A  |
| Suppression de hiveContext dans les blocs-notes Jupyter |Utilisez la commande magique `%%sql` au lieu de la commande magique `%%hive`. SqlContext est équivalent à hiveContext. Pour plus d’informations, consultez [Noyaux disponibles pour les blocs-notes Jupyter](hdinsight-apache-spark-jupyter-notebook-kernels.md) |Blocs-notes |Clusters Spark sur Linux |N/A |
| Désapprobation d’anciennes versions de Spark |La version 1.3.1 de Spark a été retirée du service le 31/05. |Service |Clusters Spark sur Windows |N/A |

## <a name="notes-for-03292016-release-of-hdinsight"></a>Notes pour la version du 29/03/2016 de HDInsight
Les numéros de version complets des clusters HDInsight déployés avec cette version sont les suivants :

* HDInsight    (Windows)         2.1.10.875.2159884 (HDP 1.3.12.0-01795 - inchangé)
* HDInsight    (Windows)         3.0.6.875.2159884 (HDP 2.0.13.0-2117 - inchangé)
* HDInsight    (Windows)         3.1.4.875.2159884  (HDP 2.1.15.0-2374 - inchangé)
* HDInsight    (Windows)        3.2.7.875.2159884  (HDP 2.2.9.1-7 - inchangé)
* HDInsight (Windows)        3.3.0.875.2159884  (HDP 2.3.3.1-16)
* HDInsight    (Linux)            3.2.1000.0.7193255   (HDP    2.2.9.1-8 - inchangé)
* HDInsight (Linux)            3.3.1000.0.7193255   (HDP 2.3.3.1-7 - inchangé)
* HDInsight (Linux)            3.4.1000.0.7195842   (HDP 2.4.1.0-327)
* Kit de développement logiciel (SDK)            1.5.8

Cette version contient les mises à jour suivantes :

| Intitulé | Description | Zone concernée (par exemple, Service, composant ou Kit de développement logiciel) | Type de cluster (par exemple, Hadoop, HBase ou Storm) | JIRA (le cas échéant) |
| --- | --- | --- | --- | --- |
| Version 3.4 de HDInsight ajoutée et versions de HDP mises à jour pour tous les clusters HDInsight |Avec cette version, nous avons ajouté HDInsight version 3.4 (basée sur HDP 2.4) et avons également mis à jour d’autres versions de HDP. Les notes de publication de HDP 2.4 sont disponibles [ici](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.4.0/bk_HDP_RelNotes/content/ch_relnotes_v240.html). De plus amples informations sur les versions de HDInsight sont disponibles [ici](hdinsight-component-versioning.md). |de diffusion en continu |Tous les clusters Linux |N/A |
| HDInsight Premium |HDInsight est désormais disponible en deux catégories : Standard et Premium. HDInsight Premium est actuellement en version préliminaire, disponible uniquement pour les clusters Hadoop et Spark sur Linux. Vous pourrez trouver plus d’informations [ici](hdinsight-component-versioning.md#hdinsight-standard-and-hdinsight-premium). |Service |Hadoop et Spark sur Linux |N/A |
| Microsoft R Server |HDInsight Premium fournit Microsoft R Server qui peut être inclus avec les clusters Hadoop et Spark sur Linux. Pour plus d’informations, consultez [Vue d’ensemble : R Server sur HDInsight](hdinsight-hadoop-r-server-overview.md). |Service |Hadoop et Spark sur Linux |N/A |
| Spark 1.6.0 |Les clusters HDInsight 3.4 incluent désormais Spark 1.6.0 |de diffusion en continu |Clusters Spark sur Linux |N/A |
| Améliorations du Bloc-notes Jupyter |Les blocs-notes Jupyter disponibles avec les clusters Spark fournissent désormais des noyaux Spark supplémentaires. Ils incluent également des améliorations comme l’utilisation de %%magic, la visualisation automatique et l’intégration avec les bibliothèques de visualisation Python (par exemple, matplotlib). Pour plus d’informations, consultez [Noyaux disponibles pour les blocs-notes Jupyter](hdinsight-apache-spark-jupyter-notebook-kernels.md). |de diffusion en continu |Clusters Spark sur Linux |N/A |

## <a name="notes-for-03222016-release-of-hdinsight"></a>Notes pour la version du 22/03/2016 de HDInsight
Les numéros de version complets des clusters HDInsight déployés avec cette version sont les suivants :

* HDInsight    (Windows)         2.1.10.875.2159884 (HDP 1.3.12.0-01795 - inchangé)
* HDInsight    (Windows)         3.0.6.875.2159884 (HDP 2.0.13.0-2117 - inchangé)
* HDInsight    (Windows)         3.1.4.875.2159884  (HDP 2.1.15.0-2374 - inchangé)
* HDInsight    (Windows)        3.2.7.875.2159884  (HDP 2.2.9.1-7 - inchangé)
* HDInsight (Windows)        3.3.0.875.2159884  (HDP 2.3.3.1-16)
* HDInsight    (Linux)            3.2.1000.0.7193255   (HDP    2.2.9.1-8 - inchangé)
* HDInsight (Linux)            3.3.1000.0.7193255   (HDP 2.3.3.1-7 - inchangé)
* Kit de développement logiciel (SDK)            1.5.8

Cette version contient les mises à jour suivantes :

| Intitulé | Description | Zone concernée (par exemple, Service, composant ou Kit de développement logiciel) | Type de cluster (par exemple, Hadoop, HBase ou Storm) | JIRA (le cas échéant) |
| --- | --- | --- | --- | --- |
| Versions de HDInsight mises à jour pour tous les clusters HDInsight |Dans cette version, nous avons mis à jour les versions de HDInsight pour tous les clusters HDInsight |de diffusion en continu |Tout |N/A |

## <a name="notes-for-03102016-release-of-hdinsight"></a>Notes pour la version du 10/03/2016 de HDInsight
Les numéros de version complets des clusters HDInsight déployés avec cette version sont les suivants :

* HDInsight    (Windows)         2.1.10.859.2123216 (HDP 1.3.12.0-01795 - inchangé)
* HDInsight    (Windows)         3.0.6.859.2123216 (HDP 2.0.13.0-2117 - inchangé)
* HDInsight    (Windows)         3.1.4.859.2123216  (HDP 2.1.15.0-2374 - inchangé)
* HDInsight    (Windows)        3.2.7.859.2123216  (HDP 2.2.9.1-7)
* HDInsight (Windows)        3.3.0.859.2123216  (HDP 2.3.3.1-5 - inchangé)
* HDInsight    (Linux)            3.2.1000.7076817   (HDP    2.2.9.1-8)
* HDInsight (Linux)            3.3.1000.7076817   (HDP 2.3.3.1-7)
* Kit de développement logiciel (SDK)            1.5.8

Cette version contient les mises à jour suivantes :

| Intitulé | Description | Zone concernée (par exemple, Service, composant ou Kit de développement logiciel) | Type de cluster (par exemple, Hadoop, HBase ou Storm) | JIRA (le cas échéant) |
| --- | --- | --- | --- | --- |
| Versions de HDInsight mises à jour pour tous les clusters HDInsight |Dans cette version, nous avons mis à jour les versions de HDInsight pour tous les clusters HDInsight |de diffusion en continu |Tout |N/A |

## <a name="notes-for-01272016-release-of-hdinsight"></a>Notes relatives à la version de HDInsight du 27/01/2016
Les numéros de version complets des clusters HDInsight déployés avec cette version sont les suivants :

* HDInsight    (Windows)         2.1.10.817.2028315 (HDP 1.3.12.0-01795 - inchangé)
* HDInsight    (Windows)         3.0.6.817.2028315 (HDP 2.0.13.0-2117 - inchangé)
* HDInsight    (Windows)         3.1.4.817.2028315  (HDP 2.1.15.0-2374 - inchangé)
* HDInsight    (Windows)        3.2.7.817.2028315  (HDP 2.2.9.1-1)
* HDInsight (Windows)        3.3.0.817.2028315  (HDP 2.3.3.1-5 - inchangé)
* HDInsight    (Linux)            3.2.1000.4072335   (HDP    2.2.9.1-1)
* HDInsight (Linux)            3.3.1000.4072335   (HDP 2.3.3.1-1)
* Kit de développement logiciel (SDK)            1.5.8

Cette version contient les mises à jour suivantes :

| Intitulé | Description | Zone concernée (par exemple, Service, composant ou Kit de développement logiciel) | Type de cluster (par exemple, Hadoop, HBase ou Storm) | JIRA (le cas échéant) |
| --- | --- | --- | --- | --- |
| Versions de HDInsight mises à jour pour tous les clusters HDInsight |Dans cette version, nous avons mis à jour les versions de HDInsight pour tous les clusters HDInsight |de diffusion en continu |Tout |N/A |

## <a name="notes-for-12022015-release-of-hdinsight"></a>Notes pour la version du 02/12/2015 de HDinsight
Les numéros de version complets des clusters HDInsight déployés avec cette version sont les suivants :

* HDInsight    (Windows)         2.1.10.763.1931434 (HDP 1.3.12.0-01795 - inchangé)
* HDInsight    (Windows)         3.0.6.763.1931434 (HDP 2.0.13.0-2117 - inchangé)
* HDInsight    (Windows)         3.1.4.763.1931434  (HDP 2.1.15.0-2374 - inchangé)
* HDInsight    (Windows)        3.2.7.763.1931434  (HDP 2.2.7.1-34 - inchangé)
* HDInsight (Windows)        3.3.1000.0           (HDP 2.3.3.1-5)
* HDInsight    (Linux)            3.2.1000.0.6392801 (HDP    2.2.7.1-34 - inchangé)
* HDInsight (Linux)            3.3.1000.0           (HDP 2.3.3.0-3039)
* Kit de développement logiciel (SDK)            1.5.8

Cette version contient les mises à jour suivantes :

| Intitulé | Description | Zone concernée (par exemple, Service, composant ou Kit de développement logiciel) | Type de cluster (par exemple, Hadoop, HBase ou Storm) | JIRA (le cas échéant) |
| --- | --- | --- | --- | --- |
| Version 3.3 de HDInsight ajoutée et versions de HDP mises à jour pour tous les clusters HDInsight |Avec cette version, nous avons ajouté HDInsight version 3.3 (basée sur HDP 2.3) et avons également mis à jour d’autres versions de HDP. Les notes de publication de HDP 2.3 sont disponibles [ici](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.3.0/bk_HDP_RelNotes/content/ch_relnotes_v230.html). De plus amples informations sur les versions de HDInsight sont disponibles [ici](hdinsight-component-versioning.md). |de diffusion en continu |Tout |N/A |

## <a name="notes-for-11302015-release-of-hdinsight"></a>Notes relatives à la version du 30/11/2015 de HDInsight
Les numéros de version complets des clusters HDInsight déployés avec cette version sont les suivants :

* HDInsight    (Windows)         2.1.10.757.1923908 (HDP 1.3.12.0-01795 - inchangé)
* HDInsight    (Windows)         3.0.6.757.1923908  (HDP 2.0.13.0-2117 - inchangé)
* HDInsight    (Windows)         3.1.4.757.1923908  (HDP 2.1.15.0-2374 - inchangé)
* HDInsight    (Windows)        3.2.7.757.1923908  (HDP 2.2.7.1-34)
* HDInsight    (Linux)            3.2.1000.0.6392801 (HDP    2.2.7.1-34)
* Kit de développement logiciel (SDK)            1.5.8

Cette version contient les mises à jour suivantes :

| Intitulé | Description | Zone concernée (par exemple, Service, composant ou Kit de développement logiciel) | Type de cluster (par exemple, Hadoop, HBase ou Storm) | JIRA (le cas échéant) |
| --- | --- | --- | --- | --- |
| Versions de HDInsight mises à jour pour tous les clusters HDInsight et les versions HDP pour les clusters HDInsight 3.2 (Windows et Linux) |Avec cette version, les versions de HDInsight et HDP ont été mises à jour |de diffusion en continu |Tout |N/A |

## <a name="notes-for-10272015-release-of-hdinsight"></a>Notes pour la version du 27/10/2015 de HDInsight
Les numéros de version complets des clusters HDInsight déployés avec cette version sont les suivants :

* HDInsight    (Windows)         2.1.10.726.1866228 (HDP 1.3.12.0-01795 - inchangé)
* HDInsight    (Windows)         3.0.6.726.1866228  (HDP 2.0.13.0-2117 - inchangé)
* HDInsight    (Windows)         3.1.4.726.1866228  (HDP 2.1.15.0-2374 - inchangé)
* HDInsight    (Windows)        3.2.7.726.1866228  (HDP 2.2.7.1-33)
* HDInsight    (Linux)            3.2.1000.0.6035701 (HDP    2.2.7.1-33)
* Kit de développement logiciel (SDK)            1.5.8

Cette version contient les mises à jour suivantes :

| Intitulé | Description | Zone concernée (par exemple, Service, composant ou Kit de développement logiciel) | Type de cluster (par exemple, Hadoop, HBase ou Storm) | JIRA (le cas échéant) |
| --- | --- | --- | --- | --- |
| Versions de HDInsight mises à jour pour tous les clusters HDInsight (Windows et Linux) |Avec cette version, les versions de HDInsight et HDP ont été mises à jour |de diffusion en continu |Tout |N/A |
| Résolution des clusters Jupyter pour Windows Spark en lettres majuscules |Les clusters qui avaient des noms DNS spécifiés en majuscules rencontraient des problèmes avec les blocs-notes Jupyter en raison d’une demande de vérification d’origine. La solution a consisté à modifier le nom DNS de la configuration de Jupyter en minuscules. |de diffusion en continu |HDInsight Spark (Windows) |N/A |

## <a name="notes-for-10202015-release-of-hdinsight"></a>Notes pour la version du 20/10/2015 de HDInsight
Les numéros de version complets des clusters HDInsight déployés avec cette version sont les suivants :

* HDInsight     2.1.10.716.1846990 (Windows)    (HDP 1.3.12.0-01795 - inchangé)
* HDInsight     3.0.6.716.1846990 (Windows)      (HDP 2.0.13.0-2117 - inchangé)
* HDInsight     3.1.4.716.1846990 (Windows)      (HDP 2.1.16.0-2374)
* HDInsight        3.2.7.716.1846990 (Windows)      (HDP 2.2.7.1-0004)
* HDInsight        3.2.1000.0.5930166 (Linux)        (HDP 2.2.7.1-0004)
* Kit de développement logiciel (SDK)            1.5.8

Cette version contient les mises à jour suivantes :

| Intitulé | Description | Zone concernée (par exemple, Service, composant ou Kit de développement logiciel) | Type de cluster (par exemple, Hadoop, HBase ou Storm) | JIRA (le cas échéant) |
| --- | --- | --- | --- | --- |
| Version HDP par défaut passée à HDP 2.2 |La version par défaut pour les clusters HDInsight Windows passe à HDP 2.2. HDInsight version 3.2 (HDP 2.2) est disponible depuis février 2015. Cette modification permet uniquement de basculer vers la version de cluster par défaut quand aucune sélection explicite n'a été effectuée lors de l’approvisionnement du cluster à l'aide du portail Azure, des applets de commande PowerShell ou du Kit de développement logiciel (SDK). |de diffusion en continu |Tout |N/A |
| Modifications apportées au format des noms de machines virtuelles pour le déploiement de plusieurs HDInsight sur des clusters Linux d’un même réseau virtuel |Cette version prend en charge le déploiement de plusieurs clusters Linux HDInsight sur un même réseau virtuel. Dans le cadre de cette mise à jour, le format de nom des machines virtuelles du cluster est passé de headnode\*, workernode\* et zookeepernode\* à hn\*, wn\* et zk\*, respectivement. Il est déconseillé d’établir une dépendance directe sur le format des noms de machines virtuelles car ces noms sont susceptibles d’être modifiés. Utilisez « hostname -f » sur l’ordinateur local ou des API Ambari pour déterminer la liste des hôtes et le mappage des composants aux hôtes. Pour plus d’informations, consultez [https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/hosts.md](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/hosts.md) et [https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/host-components.md](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/host-components.md). |de diffusion en continu |Clusters HDInsight sur Linux |N/A |
| Modifications de configuration |Pour les clusters HDInsight 3.1, les configurations suivantes sont maintenant activées :  <ul><li>tez.yarn.ats.enabled et yarn.log.server.url. Cela permet à Application Timeline Server et à Log Server de générer des journaux.</li></ul>Pour les clusters HDInsight 3.2, les configurations suivantes ont été modifiées : <ul><li>mapreduce.fileoutputcommitter.algorithm.version a été défini sur 2. Cela permet d’utiliser la version V2 de FileOutputCommitter.</li></ul> |de diffusion en continu |Tout |N/A |

## <a name="notes-for-09092015-release-of-hdinsight"></a>Notes relatives à la version du 09/09/2015 de HDInsight
Les numéros de version complets des clusters HDInsight déployés avec cette version sont les suivants :

* HDInsight     2.1.10.675.1768697 (HDP 1.3.12.0-01795 - inchangé)
* HDInsight     3.0.6.675.1768697  (HDP 2.0.13.0-2117 - inchangé)
* HDInsight     3.1.4.675.1768697  (HDP 2.1.15.0-2334 - inchangé)
* HDInsight        3.2.6.675.1768697  (HDP 2.2.6.1-0012 - inchangé)
* Kit de développement logiciel (SDK)            1.5.8

Cette version contient les mises à jour suivantes :

| Intitulé | Description | Zone concernée (par exemple, Service, composant ou Kit de développement logiciel) | Type de cluster (par exemple, Hadoop, HBase ou Storm) | JIRA (le cas échéant) |
| --- | --- | --- | --- | --- |
| Versions de HDInsight mises à jour pour tous les clusters HDInsight |Avec cette version, les versions de HDInsight ont été mises à jour |de diffusion en continu |Tout |N/A |

## <a name="notes-for-07312015-release-of-hdinsight"></a>Notes relatives à la version du 31/07/2015 de HDInsight
Les numéros de version complets des clusters HDInsight déployés avec cette version sont les suivants :

* HDInsight     2.1.10.640.1695824 (HDP 1.3.12.0-01795 - inchangé)
* HDInsight     3.0.6.640.1695824  (HDP 2.0.13.0-2117 - inchangé)
* HDInsight     3.1.4.640.1695824  (HDP 2.1.15.0-2334 - inchangé)
* HDInsight        3.2.6.640.1695824  (HDP 2.2.6.1-0012 - inchangé)
* Kit de développement logiciel (SDK)            1.5.8

Cette version contient les mises à jour suivantes :

| Intitulé | Description | Zone concernée (par exemple, Service, composant ou Kit de développement logiciel) | Type de cluster (par exemple, Hadoop, HBase ou Storm) | JIRA (le cas échéant) |
| --- | --- | --- | --- | --- |
| Correctif du flux de travail de réimageage du nœud de cluster Spark |Corrige un bogue qui empêchait la récupération des nœuds du cluster Spark après le réimageage. |Service |Spark |N/A |

## <a name="notes-for-07312015-release-of-hdinsight"></a>Notes relatives à la version du 31/07/2015 de HDInsight
Les numéros de version complets des clusters HDInsight déployés avec cette version sont les suivants :

* HDInsight     2.1.10.635.1684502 (HDP 1.3.12.0-01795 - inchangé)
* HDInsight     3.0.6.635.1684502  (HDP 2.0.13.0-2117 - inchangé)
* HDInsight     3.1.4.635.1684502  (HDP 2.1.15.0-2334 - inchangé)
* HDInsight        3.2.6.635.1684502  (HDP 2.2.6.1-0012 - inchangé)
* Kit de développement logiciel (SDK)            1.5.8

Cette version contient les mises à jour suivantes :

| Intitulé | Description | Zone concernée (par exemple, Service, composant ou Kit de développement logiciel) | Type de cluster (par exemple, Hadoop, HBase ou Storm) | JIRA (le cas échéant) |
| --- | --- | --- | --- | --- |
| Versions de HDInsight mises à jour pour tous les clusters HDInsight |Avec cette version, les versions de HDInsight ont été mises à jour |de diffusion en continu |Tout |N/A |

## <a name="notes-for-07072015-release-of-hdinsight"></a>Notes relatives à la version du 07/07/2015 de HDInsight
Les numéros de version complets des clusters HDInsight déployés avec cette version sont les suivants :

* HDInsight     2.1.10.610.1630216    (HDP 1.3.12.0-01795 - inchangé)
* HDInsight     3.0.6.610.1630216    (HDP 2.0.13.0-2117 - inchangé)
* HDInsight     3.1.4.610.1630216    (HDP 2.1.15.0-2334 - inchangé)
* HDInsight        3.2.4.610.1630216    (HDP 2.2.6.1-0012)
* Kit de développement logiciel (SDK)            1.5.8

Cette version contient les mises à jour suivantes :

| Intitulé | Description | Zone concernée (par exemple, Service, composant ou Kit de développement logiciel) | Type de cluster (par exemple, Hadoop, HBase ou Storm) | JIRA (le cas échéant) |
| --- | --- | --- | --- | --- |
| Versions HDP mises à jour pour les clusters HDInsight 3.2 |Avec cette version, HDInsight 3.2 déploie HDP 2.2.6.1-0012 |de diffusion en continu |Tout |N/A |

## <a name="notes-for-06262015-release-of-hdinsight"></a>Notes relatives à la version du 26/06/2015 de HDInsight
Les numéros de version complets des clusters HDInsight déployés avec cette version sont les suivants :

* HDInsight     2.1.10.601.1610731    (HDP 1.3.12.0-01795 - inchangé)
* HDInsight     3.0.6.601.1610731    (HDP 2.0.13.0-2117 - inchangé)
* HDInsight     3.1.4.601.1610731    (HDP 2.1.15.0-2334 - inchangé)
* HDInsight        3.2.4.601.1610731    (HDP 2.2.6.1-0011)
* Kit de développement logiciel (SDK)            1.5.8

Cette version contient les mises à jour suivantes :

<table border="1">
<tr>
<th>Intitulé</th>
<th>Description</th>
<th>Zone concernée (par exemple, Service, composant ou Kit de développement logiciel)</p></th>
<th>Type de cluster (par exemple, Hadoop, HBase ou Storm)</th>
<th>JIRA (le cas échéant)</th>
</tr>
<tr>
<td>Versions HDP mises à jour pour les clusters HDInsight 3.2</td>
<td>Avec cette version, HDInsight 3.2 déploie HDP 2.2.6.1</td>
<td>de diffusion en continu</td>
<td>Tout</td>
<td>N/A</td>
</tr>
</table>

## <a name="notes-for-06182015-release-of-hdinsight"></a>Notes relatives à la version du 18/06/2015 de HDInsight
Les numéros de version complets des clusters HDInsight déployés avec cette version sont les suivants :

* HDInsight     2.1.10.596.1601657    (HDP 1.3.12.0-01795 - inchangé)
* HDInsight     3.0.6.596.1601657    (HDP 2.0.13.0-2117 - inchangé)
* HDInsight     3.1.4.596.1601657    (HDP 2.1.15.0-2334)
* HDInsight        3.2.4.596.1601657    (HDP 2.2.6.1-0002)
* Kit de développement logiciel (SDK)            1.5.8

Cette version contient les mises à jour suivantes :

<table border="1">
<tr>
<th>Intitulé</th>
<th>Description</th>
<th>Zone concernée (par exemple, Service, composant ou Kit de développement logiciel)</p></th>
<th>Type de cluster (par exemple, Hadoop, HBase ou Storm)</th>
<th>JIRA (le cas échéant)</th>
</tr>
<tr>
<td>Ports HTTPS supplémentaires ouverts</td>
<td>Le service cloud ouvre désormais 5 ports 8001 à 8005 sur le cluster, par exemple sur https://<clustername>.azurehdinsight.net:8001/. Les demandes vers ces URL sont authentifiées à l’aide du même mécanisme de mot de passe d’authentification de base que le port&#160;443. Ces ports sont liés au même port sur le nœud principal actif. Les actions de script peuvent être utilisées pour que les services clients écoutent sur ces ports sur le nœud principal et soient routés à l’extérieur du cluster.</td>
<td>Service cloud</td>
<td>Tous</td>
<td>N/A</td>
</tr>
<tr>
<td>Problème de lecture aléatoire MapReduce intermittente pour HDInsight 3.2</td>
<td>Correction d’une condition critique rare et intermittente dans Map Reduce Shuffle sur des clusters de grande taille, entraînant des échecs de tâches occasionnels. Voir <a href="https://issues.apache.org/jira/browse/MAPREDUCE-6361" target="_blank">MAPREDUCE-6361</a> pour plus d’informations.</td>
<td>Composant principal Hadoop</td>
<td>Tout</td>
<td><a href="https://issues.apache.org/jira/browse/MAPREDUCE-6361" target="_blank">MAPREDUCE-6361</a></td>
</tr>
<tr>
<td>Migration vers la dernière version du Kit de développement logiciel (SDK) Azure Java 2.2 pour HDInsight 3.2</td>
<td>Migration vers la version la plus récente du Kit de développement logiciel (SDK) Azure pour Java utilisé par le pilote WASB. La dernière version du Kit de développement logiciel (SDK) inclut quelques correctifs et les notes de publication associées sont disponibles à la page https://github.com/Azure/azure-storage-java/blob/master/ChangeLog.txt.</td>
<td>Composant principal Hadoop</td>
<td>Tout</td>
<td><a href="https://issues.apache.org/jira/browse/HADOOP-11959" target="_blank">HADOOP-11959</a></td>
</tr>
<tr>
<td>Migration vers HDP 2.1.15 pour les clusters HDInsight 3.1</td>
<td>Les notes de publication Hortonworks pour cette version sont disponibles <a href="http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.15-Win/bk_releasenotes_HDP-Win/content/ch_relnotes-HDP-2.1.15.html" target="_blank">ici</a>.</td>
<td>HDP</td>
<td>Tout</td>
<td>N/A</td>
</tr>
</table>

## <a name="notes-for-06042015-release-of-hdinsight"></a>Notes relatives à la publication du 04/06/2015 de HDInsight
Les numéros de version complets des clusters HDInsight déployés avec cette version sont les suivants :

* HDInsight     2.1.10.583.1575584    (HDP 1.3.12.0-01795 - inchangé)
* HDInsight     3.0.6.583.1575584    (HDP 2.0.13.0-2117 - inchangé)
* HDInsight     3.1.3.583.1575584    (HDP 2.1.12.1-0003 - inchangé)
* HDInsight        3.2.4.583.1575584    (HDP 2.2.6.1-1)
* Kit de développement logiciel (SDK)            1.5.8

Cette version contient les mises à jour suivantes :

<table border="1">
<tr>
<th>Intitulé</th>
<th>Description</th>
<th>Zone concernée (par exemple, Service, composant ou Kit de développement logiciel)</p></th>
<th>Type de cluster (par exemple, Hadoop, HBase ou Storm)</th>
<th>JIRA (le cas échéant)</th>
</tr>
<tr>
<td>Correction d’une erreur de passerelle incorrecte 502 pour les clusters Storm</td>
<td>Cette version corrige un bogue qui concerne l’API de soumission de travaux qui a provoqué l’inactivité du site web après un redémarrage.</td>
<td>de diffusion en continu</td>
<td>Storm</td>
<td>N/A</td>
</tr>
</table>

## <a name="notes-for-06012015-release-of-hdinsight"></a>Notes relatives à la version du 01/06/2015 de HDInsight
Les numéros de version complets des clusters HDInsight déployés avec cette version sont les suivants :

* HDInsight     2.1.10.577.1563827    (HDP 1.3.12.0-01795 - inchangé)
* HDInsight     3.0.6.577.1563827    (HDP 2.0.13.0-2117 - inchangé)
* HDInsight     3.1.3.577.1563827    (HDP 2.1.12.1-0003 - inchangé)
* HDInsight        3.2.4.577.1563827    (HDP 2.2.6.0-2800 - inchangé)
* Kit de développement logiciel (SDK)            1.5.8

Cette version contient les mises à jour suivantes :

<table border="1">
<tr>
<th>Intitulé</th>
<th>Description</th>
<th>Zone concernée (par exemple, Service, composant ou Kit de développement logiciel)</p></th>
<th>Type de cluster (par exemple, Hadoop, HBase ou Storm)</th>
<th>JIRA (le cas échéant)</th>
</tr>
<tr>
<td>Divers correctifs de bogues</td>
<td>Cette version résout les bogues liés à l’approvisionnement de clusters.</td>
<td>de diffusion en continu</td>
<td>Tous les types de cluster</td>
<td>N/A</td>
</tr>
</table>

## <a name="notes-for-05272015-release-of-hdinsight"></a>Notes relatives à la version du 27/05/2015 de HDInsight
Les numéros de version complets des clusters HDInsight déployés avec cette version sont les suivants :

* HDInsight        3.2.4.570.1554102    (HDP 2.2.6.0-2800)
* Les autres versions de cluster et de Kit de développement logiciel (SDK) ne sont pas déployés dans le cadre de cette version.

Cette version contient les mises à jour suivantes :

<table border="1">
<tr>
<th>Intitulé</th>
<th>Description</th>
<th>Zone concernée (par exemple, Service, composant ou Kit de développement logiciel)</p></th>
<th>Type de cluster (par exemple, Hadoop, HBase ou Storm)</th>
<th>JIRA (le cas échéant)</th>
</tr>
<tr>
<td>Mise à jour HDP 2.2</td>
<td>Cette version de HDInsight 3.2 contient HDP 2.2.6 et apporte plusieurs résolutions de bogues importantes dans HDInsight. Les notes de publication complètes sont disponibles à l’adresse <a href="http://dev.hortonworks.com.s3.amazonaws.com/HDPDocuments/HDP2/HDP-2.2.6/HDP_RelNotes_v226/index.html">Notes de publication HDP 2.2.6</a>.</td>
<td>HDP</td>
<td>Tous les types de cluster</td>
<td>N/A</td>
</tr>
<tr>
<td>Modification de la configuration de mémoire de conteneur YARN par défaut</td>
<td>Dans cette mise à jour, la mémoire disponible par défaut pour les conteneurs YARN (yarn.nodemanager.resource.memory-mb et yarn.scheduler.maximum-allocation-mb), lancée par le Gestionnaire de nœuds, est passée à 5 632 Mo. Elle était auparavant de 4 608 Mo, mais selon les diverses exécutions de tâches, la nouvelle valeur doit offrir une meilleure fiabilité et de meilleures performances pour la plupart des tâches. Elle constitue donc le meilleur choix par défaut. Comme d’habitude, si vous avez une dépendance critique par rapport à cette configuration de mémoire, définissez-la de façon explicite lors de la création du cluster.</td>
<td>HDP</td>
<td>Tous les types de cluster</td>
<td>N/A</td>
</tr>
<tr>
<td>Parité de configuration par défaut pour les clusters HBase et Storm</td>
<td>Cette mise à jour restaure les clusters Hbase et Storm de manière à ce qu’ils utilisent les mêmes valeurs de configurations YARN que les clusters Hadoop. Tous les types de cluster sont ainsi égaux.</td>
<td>HDP</td>
<td>Hbase, Storm</td>
<td>N/A</td>
</tr>
</table>

## <a name="notes-for-05202015-release-of-hdinsight"></a>Notes relatives à la version du 20/05/2015 de HDInsight
Les numéros de version complets des clusters HDInsight déployés avec cette version sont les suivants :

* HDInsight     2.1.10.564.1542093    (HDP 1.3.12.0-01795 - inchangé)
* HDInsight     3.0.6.564.1542093    (HDP 2.0.13.0-2117 - inchangé)
* HDInsight     3.1.3.564.1542093    (HDP 2.1.12.1-0003)
* HDInsight        3.2.4.564.1542093    (HDP 2.2.4.6-2)
* Kit de développement logiciel (SDK)            1.5.8

Cette version contient les mises à jour suivantes :

<table border="1">
<tr>
<th>Intitulé</th>
<th>Description</th>
<th>Zone concernée (par exemple, Service, composant ou Kit de développement logiciel)</p></th>
<th>Type de cluster (par exemple, Hadoop, HBase ou Storm)</th>
<th>JIRA (le cas échéant)</th>
</tr>
<tr>
<td>Prise en charge de EventHub avec SCP.NET</td>
<td>Les packages de cluster mis à jour pour HDInsight Storm apportent de nouvelles fonctionnalités à SCP.NET. Vous avez désormais accès aux nouvelles API dans le générateur de topologie, ce qui facilite l’utilisation de « spouts » EventHub ou Java. Vous devez mettre à jour le Kit de développement logiciel (SDK) de votre client SCP.NET pour utiliser les nouveaux clusters, car les contrats ont été mis à jour. Pour plus d’informations sur les nouvelles API, l’utilisation et les notes de version (y compris les correctifs de bogues), consultez le fichier Readme inclus dans le package NuGet SCP.NET.</td>
<td>Outils VS</td>
<td>Clusters HDInsight 3.2 Storm</td>
<td>N/A</td>
</tr>
<tr>
<td>Mise à jour du pilote JDBC</td>
<td>Mise à jour du pilote vers la version de SQL Server prise en charge dans sqljdbc_4.1.5605.100.</td>
<td>Metastore</td>
<td>Tout</td>
<td>N/A</td>
</tr>
</table>

## <a name="notes-for-04272015-release-of-hdinsight"></a>Notes relatives à la version du 27/04/2015 de HDInsight
Les numéros de version complets des clusters HDInsight déployés avec cette version sont les suivants :

* HDInsight     2.1.10.537.1486660    (HDP 1.3.12.0-01795 - inchangé)
* HDInsight     3.0.6.537.1486660    (HDP 2.0.13.0-2117 - inchangé)
* HDInsight     3.1.3.537.1486660    (HDP 2.1.12.0-2329 - inchangé)
* HDInsight        3.2.3.537.1486660    (HDP 2.2.2.2-4)
* Kit de développement logiciel (SDK)            1.5.8

Cette version contient les mises à jour suivantes :

<table border="1">
<tr>
<th>Intitulé</th>
<th>Description</th>
<th>Zone concernée (par exemple, Service, composant ou Kit de développement logiciel)</p></th>
<th>Type de cluster (par exemple, Hadoop, HBase ou Storm)</th>
<th>JIRA (le cas échéant)</th>
</tr>
<tr>
<td>Correctif des dépendances DLL</td>
<td>Suppression de la dépendance de HDInsight sur l’Infrastructure de tests unitaires.</td>
<td>Foundation</td>
<td>Hadoop</td>
<td>N/A</td>
</tr>
<tr>
<td>Correctif de bogue pour une condition de concurrence</td>
<td>Une demande de création de cluster attend maintenant l’acceptation de la requête PUT avant d’interroger l’état</td>
<td>Foundation</td>
<td>Hadoop</td>
<td>N/A</td>
</tr>
</table>

## <a name="notes-for-04142015-release-of-hdinsight"></a>Notes relatives à la version du 14/04/2015 de HDInsight
Les numéros de version complets des clusters HDInsight déployés avec cette version sont les suivants :

* HDInsight     2.1.10.521.1453250    (HDP 1.3.12.0-01795 - inchangé)
* HDInsight     3.0.6.521.1453250    (HDP 2.0.13.0-2117 - inchangé)
* HDInsight     3.1.3.521.1453250    (HDP 2.1.12.0-2329 - inchangé)
* HDInsight        3.2.3.525.1459730    (HDP 2.2.2.2-2)
* Kit de développement logiciel (SDK)            1.5.6

Cette version contient les mises à jour suivantes :

<table border="1">
<tr>
<th>Intitulé</th>
<th>Description</th>
<th>Zone concernée (par exemple, Service, composant ou Kit de développement logiciel)</p></th>
<th>Type de cluster (par exemple, Hadoop, HBase ou Storm)</th>
<th>JIRA (le cas échéant)</th>
</tr>
<tr>
<td>Résolution des bogues Tez</td>
<td>Des correctifs pour Apache TEZ 2214 et TEZ 1923 sont inclus dans cette version de HDI 3.2. Ils sont nécessaires pour certaines requêtes Hive sur Tez nécessitant de lire aléatoirement une quantité importante de données.
</td>
<td>HDP</td>
<td>Hadoop</td>
<td><a href="https://issues.apache.org/jira/browse/TEZ-2214">TEZ 2214</a></br><a href="https://issues.apache.org/jira/browse/TEZ-1923">TEZ 1923</a></td>
</tr>
</table>

## <a name="notes-for-04062015-release-of-hdinsight"></a>Notes relatives à la version du 06/04/2015 de HDInsight
Les numéros de version complets des clusters HDInsight déployés avec cette version sont les suivants :

* HDInsight     2.1.10.521.1453250    (HDP 1.3.12.0-01795 - inchangé)
* HDInsight     3.0.6.521.1453250    (HDP 2.0.13.0-2117 - inchangé)
* HDInsight     3.1.3.521.1453250    (HDP 2.1.12.0-2329 - inchangé)
* HDInsight        3.2.3.521.1453250    (HDP 2.2.2.2-1)
* Kit de développement logiciel (SDK)            1.5.6

Cette version contient les mises à jour suivantes :

<table border="1">
<tr>
<th>Intitulé</th>
<th>Description</th>
<th>Zone concernée (par exemple, Service, composant ou Kit de développement logiciel)</p></th>
<th>Type de cluster (par exemple, Hadoop, HBase ou Storm)</th>
<th>JIRA (le cas échéant)</th>
</tr>
<tr>
<td>Kit de développement logiciel (SDK) .NET de HDInsight 1.5.6</td>
<td>Mises à jour pour supprimer certaines classes internes pour HDInsight sur Linux.</td>
<td>Foundation</td>
<td>Hadoop</td>
<td>N/A</td>
</tr>
<tr>
<td>Bibliothèque Avro 1.5.6</td>
<td>Ajout de <b>KnownTypeAttribute</b> pour la méthode <b>GetAllKnownTypes</b>. NullReferenceException corrigée lorsqu’un type est null pour la méthode GetAllKnownTypes.</td>
<td>Foundation</td>
<td>Hadoop</td>
<td>N/A</td>
</tr>
<tr>
<td>Résolution des bogues</td>
<td>Divers correctifs de bogues pour le service</td>
<td>de diffusion en continu</td>
<td>Tout</td>
<td>N/A</td>
</tr>
</table>

## <a name="notes-for-04012015-release-of-hdinsight"></a>Notes relatives à la version du 01/04/2015 de HDInsight
Les numéros de version complets des clusters HDInsight déployés avec cette version sont les suivants :

* HDInsight     2.1.10.513.1431705    (HDP 1.3.12.0-01795)
* HDInsight     3.0.6.513.1431705    (HDP 2.0.13.0-2117)
* HDInsight     3.1.3.513.1431705    (HDP 2.1.12.0-2329)
* HDInsight        3.2.3.513.1431705    (HDP 2.2.2.1-2600)
* Kit de développement logiciel (SDK)            1.5.5

Cette version contient les mises à jour suivantes :

<table border="1">
<tr>
<th>Intitulé</th>
<th>Description</th>
<th>Zone concernée (par exemple, Service, composant ou Kit de développement logiciel)</p></th>
<th>Type de cluster (par exemple, Hadoop, HBase ou Storm)</th>
<th>JIRA (le cas échéant)</th>
</tr>
<tr>
<td>Possibilité d’activer ou de désactiver les informations d’identification de Bureau à distance sur des clusters Windows via le Kit de développement (SDK) .NET</td>
<td>Assistance par programme pour activer ou désactiver les informations d’identification RDP sur des clusters Windows.</td>
<td>Foundation</td>
<td>Tout</td>
<td>N/A</td>
</tr>
<tr>
<td>Possibilité d’activer les informations d’identification de bureau à distance sur des clusters pendant qu’ils sont en cours d’approvisionnement</td>
<td>Prise en charge par programme pour activer les informations d’identification de bureau à distance lors de la création du cluster. Cela supprime le processus en deux étapes pour configurer le cluster avant d’activer le bureau à distance.</td>
<td>Foundation</td>
<td>Tout</td>
<td>N/A</td>
</tr>
<tr>
<td>Mise à niveau de Python vers la version 2.7.8</td>
<td>Python mis à niveau sur les clusters HDInsight vers 2.7.8, qui contient des correctifs de sécurité importants pour les versions 2.1, 3.0, 3.1 et 3.2 de HDInsight</td>
<td>de diffusion en continu</td>
<td>Tout</td>
<td>N/A</td>
</tr>
<tr>
<td>Modification de la configuration YARN</td>
<td>Modification de la configuration YARN yarn.resourcemanager.max-completed-applications à 1000 pour tous les types de cluster des versions 3.1 et 3.2 de HDInsight. Cette valeur contrôle uniquement la liste des applications terminées dans l’interface utilisateur YARN. Pour obtenir des informations sur les applications qui ont été envoyées avant la liste des applications affichées dans l’interface utilisateur, vous pouvez accéder directement au serveur de l’historique.</td>
<td>YARN</td>
<td>Tout</td>
<td>N/A</td>
</tr>
<tr>
<td>Redimensionnement des nœuds dans un cluster HBase</td>
<td>Les clusters HBase permettent à présent le redimensionnement de nœuds (haut et bas) pour les versions de HDInsight 3.1 et 3.2</td>
<td>de diffusion en continu</td>
<td>hbase</td>
<td>N/A</td>
</tr>
<tr>
<td>Mise à niveau de JBDC</td>
<td>Mise à niveau du pilote JDBC SQL vers la version sqljdbc_4.0.2206.100 pour HDInsight version 3.2. Cette version contient des améliorations de sécurité importantes.</td>
<td>HDP</td>
<td>Tout</td>
<td>N/A</td>
</tr>
<tr>
<td>Mise à jour de la configuration JVM</td>
<td>Mise à jour de la configuration JVM networkaddress.cache.ttl à 300 secondes à partir de la valeur par défaut de -1 pour HDInsight version 3.1 et 3.2. Cette valeur de configuration contrôle la stratégie de mise en cache pour les recherches de nom réussies à partir du service de noms. Cela résout un bogue lié à l’agrandissement et à la réduction des clusters HBase.</td>
<td>de diffusion en continu</td>
<td>hbase</td>
<td>N/A</td>
</tr>
<tr>
<td>Mise à niveau vers le Kit de développement logiciel (SDK) Azure Storage pour Java 2.0</td>
<td>Mise à niveau de HDInsight version 3.2 pour utiliser la dernière version du Kit de développement logiciel (SDK) Azure Storage pour Java. Contient plusieurs résolutions de bogues importantes pour la version 0.6.0 actuelle.</td>
<td>HDP</td>
<td>Tout</td>
<td>N/A</td>
</tr>
<tr>
<td>Mise à niveau vers le code source WASB Apache</td>
<td>HDInsight version 3.2 utilise maintenant la dernière version de code pour le pilote de système de fichiers WASB d’Apache Hadoop. Avec cette modification, le pilote WASB est maintenant fourni comme un fichier jar distinct. C’est un simple changement d’empaquetage qui ne modifie aucunement le comportement du pilote WASB. Le nom de ce fichier jar est hadoop-azure-2.6.0.jar.</td>
<td>HDP</td>
<td>Tout</td>
<td>N/A</td>
</tr>
<tr>
<td>Mises à jour du nom de fichier jar dans HDInsight 3.2</td>
<td>Cette mise à jour vers HDInsight version 3.2 contient plusieurs résolutions de bogues et quelques JAR internes packagés en tant que partie de HDP ont été mis à niveau. Ces derniers sont internes au package HDP et ne sont pas destinés à une utilisation directe par les applications client. Les applications doivent packager leur propre version des fichiers jar afin qu’une mise à niveau vers les fichiers jar HDP internes n’interrompent pas les applications client.</td>
<td>HDP</td>
<td>Tout</td>
<td>N/A</td>
</tr>
</table>

## <a name="notes-for-03032015-release-of-hdinsight"></a>Notes relatives à la version du 03/03/2015 de HDInsight
Les numéros de version complets des clusters HDInsight déployés avec cette version sont les suivants :

* HDInsight     2.1.10.488.1375841    (HDP 1.3.9.0-01351 - inchangé)
* HDInsight     3.0.6.488.1375841    (HDP 2.0.9.0-2097 - inchangé)
* HDInsight     3.1.3.488.1375841    (HDP 2.1.10.0-2290 - inchangé)
* HDInsight        3.2.3.488.1375841    (HDP-2.2.10.0-2340 - inchangé)
* Kit de développement logiciel (SDK)            1.5.0                (inchangé)

Cette version contient la mise à jour suivante :

<table border="1">
<tr>
<th>Intitulé</th>
<th>Description</th>
<th>Zone concernée (par exemple, Service, composant ou Kit de développement logiciel)</p></th>
<th>Type de cluster (par exemple, Hadoop, HBase ou Storm)</th>
<th>JIRA</th>
</tr>
<tr>
<td>Améliorations de la fiabilité</td>
<td>Nous avons apporté des correctifs qui permettent une meilleure mise à l’échelle du service avec une charge accrue par rapport à la création du cluster.</td>
<td>de diffusion en continu</td>
<td>Tout</td>
<td>N/A</td>
</tr>
</table>

## <a name="notes-for-02182015-release-of-hdinsight"></a>Notes relatives à la version du 18/02/2015 de HDInsight
Les numéros de version complets des clusters HDInsight déployés avec cette version sont les suivants :

* HDInsight     2.1.10.471.1342507    (HDP 1.3.9.0-01351 - inchangé)
* HDInsight     3.0.6.471.1342507    (HDP 2.0.9.0-2097 - inchangé)
* HDInsight     3.1.3.471.1342507    (HDP 2.1.10.0-2290 - inchangé)
* HDInsight        3.2.3.471.1342507    (HDP-2.2.10.0-2340)
* Kit de développement logiciel (SDK)            1.5.0

Cette version contient les mises à jour suivantes :

<table border="1">
<tr>
<th>Intitulé</th>
<th>Description</th>
<th>Zone concernée (par exemple, Service, composant ou Kit de développement logiciel)</p></th>
<th>Type de cluster (par exemple, Hadoop, HBase ou Storm)</th>
<th>JIRA (le cas échéant)</th>
</tr>
<tr>
<td>Clusters HDInsight 3.2</td>
<td>Hadoop 2.6/HDP2.2 est disponible avec les clusters HDInsight 3.2. Il contient des mises à jour importantes pour tous les composants open source. Pour plus d’informations, consultez Nouveautés dans HDInsight et <a href ="http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.2.0/HDP_2.2.0_Release_Notes_20141202_version/index.html" target="_blank">Notes de version HDP 2.2.0.0</a>.</td>
<td>Logiciels open source</td>
<td>Tout</td>
<td>N/A </td>
</tr>
<tr>
<td>HDInsight sous Linux (version préliminaire)</td>
<td>Les clusters peuvent être déployés en cours d’exécution sur Ubuntu Linux. Pour plus d’informations, consultez Didacticiel Hadoop : prise en main de Hadoop dans HDInsight.</td>
<td>Service</td>
<td>Hadoop</td>
<td>N/A</td>
</tr>
<tr>
<td>Disponibilité générale de Storm</td>
<td>Les clusters Apache Storm sont généralement disponibles. Pour plus d’informations, consultez Prise en main d’Apache Storm sur HDInsight à l’aide des exemples storm-starter.</td>
<td>Service</td>
<td>Storm</td>
<td>N/A</td>
</tr>
<tr>
<td>Tailles de machines virtuelles</td>
<td>Azure HDInsight est disponible sur plusieurs tailles et types de machine virtuelle. Les clusters HDInsight peuvent utiliser des tailles A2 à A7 conçues pour un usage général ; des nœuds de série D possédant des disques SSD et des processeurs 60 % plus rapides ; et des tailles A8 et A9 prenant en charge InfiniBand pour une mise en réseau rapide.</td>
<td>de diffusion en continu</td>
<td>Tout</td>
<td>N/A</td>
</tr>
<tr>
<td>Mise à l’échelle du cluster</td>
<td>Vous pouvez modifier le nombre de nœuds de données pour un cluster HDInsight en cours d’exécution sans avoir à le supprimer ou à le recréer. Actuellement, seuls les types de cluster Hadoop Query et Apache Storm disposent de cette fonction, mais le type de cluster Apache HBase en sera bientôt équipé. Pour plus d’informations, consultez la rubrique Gérer les clusters HDInsight.</td>
<td>de diffusion en continu</td>
<td>Hadoop, Storm</td>
<td>N/A</td>
</tr>
<tr>
<td>Outils Visual Studio</td>
<td>En plus d’outils complets pour Apache Storm, les outils Apache Hive dans Visual Studio ont été mis à jour pour inclure la saisie semi-automatique des instructions, la validation locale et une meilleure prise en charge du débogage. Pour plus d’informations, consultez la page Prise en main de HDInsight Hadoop Tools pour Visual Studio.</td>
<td>Outils</td>
<td>Hadoop</td>
<td>N/A </td>
</tr>
<td>Connecteur Hadoop pour Azure Cosmos DB</td>
<td>Avec le connecteur Hadoop pour Azure Cosmos DB, vous pouvez effectuer des agrégations complexes, des analyses et des manipulations sur vos documents JSON sans schéma stockés dans des collections Azure Cosmos DB ou des comptes de base de données. Pour plus d’informations et un didacticiel, voir Exécuter des tâches Hadoop avec Azure Cosmos DB et HDInsight.</td>
<td>Service</td>
<td>Hadoop</td>
<td>N/A</td>
</tr>
<tr>
<td>Résolution des bogues</td>
<td>Nous avons appliqués divers correctifs mineurs pour les services HDInsight. Aucune modification du comportement n’est attendue pour les clients.</td>
<td>de diffusion en continu</td>
<td>Tout</td>
<td>N/A</td>
</tr>
</table>

## <a name="notes-for-02062015-release-of-hdinsight"></a>Notes relatives à la version du 06/02/2015 de HDInsight
Les numéros de version complets des clusters HDInsight déployés avec cette version sont les suivants :

* HDInsight     2.1.10.463.1325367    (HDP 1.3.9.0-01351 - inchangé)
* HDInsight     3.0.6.463.1325367    (HDP 2.0.9.0-2097 - inchangé)
* HDInsight     3.1.2.463.1325367    (HDP 2.1.10.0-2290)
* Kit de développement logiciel (SDK)            N/A

Cette version contient les mises à jour suivantes :

<table border="1">
<tr>
<th>Intitulé</th>
<th>Description</th>
<th>Zone concernée (par exemple, Service, composant ou Kit de développement logiciel)</p></th>
<th>Type de cluster (par exemple, Hadoop, HBase ou Storm)</th>
<th>JIRA (le cas échéant)</th>
</tr>
<tr>
<td>Résolution des bogues</td>
<td>Nous avons appliqués divers correctifs mineurs pour les services HDInsight. Aucune modification du comportement n’est attendue pour les clients.</td>
<td>de diffusion en continu</td>
<td>Tout</td>
<td>N/A</td>
</tr>
<tr>
<td>Mise à jour de maintenance HDP 2.1</td>
<td>Mise à jour de HDInsight 3.1 pour déployer HDP 2.1.10.0. Pour plus d’informations, consultez les <a href ="http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.10/bk_releasenotes_hdp_2.1/content/ch_relnotes-HDP-2.1.10.html" target="_blank">Notes de publication de HDP-2.1.10</a>. </td>
<td>Logiciels open source</td>
<td>Tout</td>
<td>N/A</td>
</tr>
<tr>
<td>Mises à jour binaires HDP</td>
<td>Les noms de quelques fichiers jar dans HBase ont été mis à jour. Ces fichiers jar sont utilisées en interne par HBase, il n’est donc pas prévu que les clients aient une dépendance sur les noms de ces fichiers jar. Vous avez notamment vu les points suivants :
<ul>
<li>./lib/jetty-6.1.26.hwx.jar</li>
<li>./lib/jetty-sslengine-6.1.26.hwx.jar</li>
<li>./lib/jetty-util-6.1.26.hwx.jar</li>
</ul>
</td>
<td>Logiciels open source</td>
<td>HBase</td>
<td>N/A</td>
</tr>
</table>

## <a name="notes-for-1292015-release-of-hdinsight"></a>Notes relatives à la version du 29/01/2015 de HDInsight
Les numéros de version complets des clusters HDInsight déployés avec cette version sont les suivants :

* HDInsight     2.1.10.455.1309616    (HDP 1.3.9.0-01351 - inchangé)
* HDInsight     3.0.6.455.1309616    (HDP 2.0.9.0-2097 - inchangé)
* HDInsight     3.1.2.455.1309616    (HDP 2.1.9.0-2196 - inchangé)
* Kit de développement logiciel (SDK)            N/A

Cette version contient la mise à jour suivante :

<table border="1">

<tr>
<th>Intitulé</th>
<th>Description</th>
<th>Zone concernée (par exemple, Service, composant ou Kit de développement logiciel)</p></th>
<th>Type de cluster (par exemple, Hadoop, HBase ou Storm)</th>
<th>JIRA (le cas échéant)</th>
</tr>
<tr>
<td>Résolution des bogues</td>
<td>Nous avons apporté quelques correctifs de bogues importants qui améliorent la fiabilité des clusters HDInsight lors des mises à niveau d’Azure.</td>
<td>de diffusion en continu</td>
<td>Tout</td>
<td>N/A</td>
</tr>
</table>

## <a name="notes-for-152015-release-of-hdinsight"></a>Notes relatives à la version du 05/01/2015 de HDInsight
Les numéros de version complets des clusters HDInsight déployés avec cette version sont les suivants :

* HDInsight     2.1.10.420.1246118    (HDP 1.3.9.0-01351 - inchangé)
* HDInsight     3.0.6.420.1246118    (HDP 2.0.9.0-2097 - inchangé)
* HDInsight     3.1.2.420.1246118    (HDP 2.1.9.0-2196 - inchangé)

Cette version contient les mises à jour suivantes :

<table border="1">

<tr>
<th>Intitulé</th>
<th>Description</th>
<th>Composant</th>
<th>Type du cluster</th>
<th>JIRA (le cas échéant)</th>
</tr>
<tr>
<td>Exemples pour l’analyse de tendances Twitter et recommandations de films basées sur Mahout</td>
<td><p>Dans cette version, la console de requête HDInsight comporte deux exemples supplémentaires :</p>

<p><b>Analyse de tendances Twitter</b><br>
Les API publiques fournies par des sites comme Twitter représentent une source de données utile pour l'analyse et la compréhension des tendances populaires. Dans ce didacticiel, découvrez comment utiliser Hive pour obtenir une liste d'utilisateurs Twitter qui ont envoyé des tweets contenant un mot particulier. </p>

<p><b>Recommandation de films Mahout</b><br>
Apache Mahout est une bibliothèque d'apprentissage machine Apache Hadoop. Mahout contient des algorithmes pour le traitement des données (tel que le filtrage, la classification et le clustering). Dans ce didacticiel, utilisez un moteur de recommandation pour générer des recommandations en fonction des films vus par vos amis.</p></td>
<td>Console de requête</td>
<td>Hadoop</td>
<td>N/A</td>
</tr>
<tr>
<td>Rétablissement de la valeur par défaut de la configuration Hive : hive.auto.convert.join.noconditionaltask.size</td>
<td><p>Cette configuration de taille s’applique aux jointures de mappage converties automatiquement. La valeur représente la somme de la taille des tables qui peuvent être converties en configurations de hachage en mémoire. Dans une version antérieure, cette valeur faisait passer la valeur par défaut de 10&#160;Mo à 128&#160;Mo. Toutefois, la nouvelle valeur de 128&#160;Mo provoquait l’échec des tâches en raison d’un manque de mémoire. Cette version rétablit la valeur par défaut à 10&#160;Mo. Les clients peuvent toujours choisir de remplacer cette valeur lors de la création du cluster, en fonction de la taille de leurs requêtes et de leurs tables. Pour plus d’informations sur ce paramètre et la manière de le remplacer, consultez <a href="http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.0.0.2/ds_Hive/optimize-joins.html#JoinOptimization-OptimizeAutoJoinConversion" target="_blank">Optimisation de la conversion de jonction automatique</a> dans la documentation Hortonworks. </p></td>
<td>Hive</td>
<td>Hadoop, Hbase</td>
<td>N/A</td>
</tr>
</table>

## <a name="notes-for-12232014-release-of-hdinsight"></a>Notes relatives à la version du 23/12/2014 de HDInsight
Les numéros de version complets des clusters HDInsight déployés avec cette version sont les suivants :

* HDInsight     2.1.10.420.1246783    (version de HDP inchangée)
* HDInsight     3.0.6.420.1246783    (version de HDP inchangée)
* HDInsight     3.1.1.420.1246783    (version de HDP inchangée)

Cette version contient la mise à jour suivante :

<table border="1">
<tr>
<th>Intitulé</th>
<th>Description</th>
<th>Composant</th>
<th>Type du cluster</th>
<th>JIRA (le cas échéant)</th>
</tr>
<tr>
<td>Défaillances intermittentes de la création de cluster dues à une charge excessive</td>
<td><p>L'algorithme amélioré pour le téléchargement des packages HDP lors de la création du cluster permet une gestion plus robuste des défaillances dues à une charge excessive.</p></td>
<td>de diffusion en continu</td>
<td>Hadoop, Hbase, Storm</td>
<td>N/A</td>
</tr>
</table>

## <a name="notes-for-12182014-release-of-hdinsight"></a>Notes relatives à la version du 18/12/2014 de HDInsight
Cette version contient la mise à jour de composant suivante :

<table border="1">
<tr>
<th>Intitulé</th>
<th>Description</th>
<th>Composant</th>
<th>Type du cluster</th>
<th>JIRA (le cas échéant)</th>
</tr>
<tr>
<td><a href = "hdinsight-hadoop-customize-cluster.md" target="_blank">Disponibilité générale de la personnalisation du cluster</a></td>
<td><p>La personnalisation offre la possibilité de personnaliser les clusters Azure HDInsight avec les projets disponibles dans l’écosystème Hadoop Apache. Avec cette nouvelle fonctionnalité, vous pouvez tester et déployer des projets Hadoop vers Azure HDInsight. Cette option est activée par la fonctionnalité **Action de Script**, qui peut modifier les clusters Hadoop de façon arbitraire à l’aide de scripts personnalisés. Cette personnalisation est disponible sur tous les types de clusters HDInsight, dont Hadoop, HBase et Storm. Pour présenter les capacités de cette fonction, nous avons décrit le processus d’installation des modules courants <a href = "hdinsight-hadoop-spark-install.md" target="_blank">Spark</a>, <a href = "hdinsight-hadoop-r-scripts.md" target="_blank">R</a>, <a href = "hdinsight-hadoop-solr-install.md" target="_blank">Solr</a> et <a href = "hdinsight-hadoop-giraph-install.md" target="_blank">Giraph</a>. Elle fournit aussi des directives et meilleures pratiques sur la création d’actions de script personnalisées à l’aide des méthodes d’assistance et offre enfin des instructions sur le test de l’action de script. </p></td>
<td>Disponibilité générale des fonctionnalités</td>
<td>Tout</td>
<td>N/A</td>
</tr>
</table>

## <a name="notes-for-12052014-release-of-hdinsight"></a>Notes relatives à la version du 05/12/2014 de HDInsight
Les numéros de version complets des clusters HDInsight déployés avec cette version sont les suivants :

* HDInsight     2.1.9.406.1221105    (HDP 1.3.9.0-01351)
* HDInsight     3.0.5.406.1221105    (HDP 2.0.9.0-2097)
* HDInsight     3.1.1.406.1221105    (HDP 2.1.9.0-2196)
* Kit de développement logiciel (SDK) HDInsight N/A

Cette version contient les mises à jour de composant suivantes :

<table border="1">
<tr>
<th>Intitulé</th>
<th>Description</th>
<th>Composant</th>
<th>Type du cluster</th>
<th>JIRA (le cas échéant)</th>
</tr>
<tr>
<td>Correctif de bogue : erreurs intermittentes lors de l’ajout d’un grand nombre de partitions à une table dans un fichier DDL Hive. </td>
<td><p>En cas d’erreur de connexion intermittente à la base de données de metastore Hive lors de l’ajout d’un grand nombre de partitions à une table Hive, le fichier DDL Hive peut échouer. L’instruction suivante est alors affichée dans le journal d’erreurs Hive : </p><p>"ERROR [main]: ql.Driver (SessionState.java:printError(547)) - FAILED: Execution Error, return code 1 from org.apache.hadoop.hive.ql.exec.DDLTask. MetaException(message:java.lang.RuntimeException: commitTransaction was called but openTransactionCalls = 0. This probably indicates that there are unbalanced calls to openTransaction/commitTransaction) »</p></td>
<td>Hive</td>
<td>Hadoop, Hbase</td>
<td>HIVE-482 (système JIRA interne ne pouvant pas faire l'objet d'une citation externe. Indiqué ici pour référence.)</td>
</tr>
<tr>
<td>Correctif de bogue : blocage occasionnel dans la console de requête HDInsight</td>
<td>Lorsque cela se produit, l'instruction suivante est affichée dans le journal WebHCat pour la tâche du lanceur WebHCat : <p>"org.apache.hive.hcatalog.templeton.CatchallExceptionMapper | org.apache.hadoop.ipc.RemoteException(org.apache.hadoop.yarn.exceptions.YarnRuntimeException): Could not load history file {wasb url to the history file}"</p></td>
<td>WebHCat,</td>
<td>Hadoop</td>
<td>HIVE-482 (système JIRA interne ne pouvant pas faire l'objet d'une citation externe. Indiqué ici pour référence.)</td>
</tr>
<tr>
<td>Correctif de bogue : pic occasionnel dans la latence des requêtes Hbase</td>
<td>Si cela se produit, les utilisateurs constatent un pic occasionnel de 3 secondes dans la latence des requêtes Hbase. </td>
<td>Passerelle de cluster HDInsight</td>
<td>HBase</td>
<td>N/A</td>
</tr>
<tr>
<td>Changement du nom du fichier jar HDP</td>
<td>Pour le cluster HDI version 3.0, quelques modifications ont été apportées aux fichiers JAR internes installés par HDP. jetty-6.1.26.jar a été remplacé par jetty-6.1.26.hwx.jar. jetty-util-6.1.26.jar a été remplacé par jetty-util-6.1.26.hwx.jar. Ces modifications s'appliquent aux projets Hadoop, Mahout, WebHCat et Oozie.</td>
<td>Hadoop, Mahout, WebHCat, Oozie</td>
<td>Hadoop, HBase</td>
<td>N/A</td>
</tr>
</table>

## <a name="notes-for-11212014-release-of-hdinsight"></a>Notes relatives à la version du 21/11/2014 de HDInsight
Les numéros de version complets des clusters HDInsight déployés avec cette version sont les suivants :

* HDInsight 2.1.9.382.1169709 (pas de changements par rapport à la version du 14/11/2014)
* HDInsight 3.0.5.382.1169709 (pas de changements par rapport à la version du 14/11/2014)
* HDInsight 3.1.1.382.1169709 (pas de changements par rapport à la version du 14/11/2014)
* Kit de développement logiciel (SDK) HDInsight 1.4.0

Cette version contient les mises à jour de composant suivantes :

<table border="1">
<tr><th>Intitulé</th><th>Description</th><th>Composant</th><th>Type du cluster</th><th>JIRA (le cas échéant)</th></tr>
<tr>
<td>Accès aux journaux des applications</td>
<td>Possibilité d’énumérer, par programme, les applications qui ont été exécutées sur vos clusters et de télécharger des journaux spécifiques d’un conteneur ou d’une application afin de faciliter le débogage d’applications problématiques.</td>
<td>Foundation</td>
<td>Hadoop</td>
<td>N/A</td>
</tr>
<tr>
<td>Possibilité de spécifier le nom de la région dans IHdInsightClient.DeleteCluster </td>
<td>Le Kit de développement logiciel (SDK) Azure HDInsight permet d’indiquer un nom de région lors de l’utilisation de **DeleteCluster**. Cela permet de débloquer les clients qui avaient deux ressources avec le même nom dans des régions différentes et étaient dans l’impossibilité de les supprimer.</td>
<td>Foundation</td>
<td>Tout</td>
<td>N/A</td>
</tr>
<tr>
<td>ClusterDetails.DeploymentId</td>
<td>L’objet **ClusterDetails** renvoie désormais un champ **DeploymentID** qui représente un identificateur unique du cluster. Son unicité est garantie parmi les tentatives de création de cluster portant les mêmes noms.</td>
<td>Foundation</td>
<td>Tout</td>
<td>N/A</td>
</tr>
</table>

## <a name="notes-for-11142014-release-of-hdinsight"></a>Notes relatives à la version du 11/14/2014 de HDInsight

Les numéros de version complets des clusters HDInsight déployés avec cette version sont les suivants :

* HDInsight 2.1.9.382.1169709
* HDInsight 3.0.5.382.1169709
* HDInsight 3.1.1.382.1169709

Cette version comprend les nouveautés suivantes (fonctions, mises à jour de composants et résolutions de bogues).

<table border="1">
<tr><th>Intitulé</th><th>Description</th><th>Composant</th><th>Type du cluster</th><th>JIRA (le cas échéant)</th></tr>
<tr>
<td>Action de script (version préliminaire)</td>
<td>Version préliminaire de la fonctionnalité de personnalisation des clusters qui permet de modifier les clusters Hadoop de manière arbitraire à l’aide de scripts personnalisés. Cette fonctionnalité offre aux utilisateurs la possibilité de tester et de déployer des projets disponibles dans l’écosystème Apache Hadoop vers les clusters Azure HDInsight. Elle est disponible sur tous les types de clusters HDInsight, dont Hadoop, HBase et Storm.</td>
<td>Nouvelle fonctionnalité</td>
<td>Tout</td>
<td>N/A</td>
</tr>
<tr>
<td>Tâches préconfigurées pour l’analyse des journaux Sites Web Azure et Azure Storage</td>
<td>La console de requête HDInsight s’accompagne d’une galerie de prise en main qui prend en charge les solutions qui fonctionnent sur vos données ou sur les exemples de données.
<p>**Solutions opérationnelles sur vos données** :<br>
Nous avons créé des tâches pour certains des scénarios d’analyse de données les plus courants afin de fournir un point de départ pour créer vos propres solutions. Vous pouvez utiliser vos propres données avec la tâche pour savoir comment elles fonctionnent. Lorsque vous êtes prêt, mettez en pratique ce que vous avez appris afin de créer votre propre solution sur la base de la tâche préconfigurée.</p>
<p>**Solutions opérationnelles sur les exemples de données** :<br>
Découvrez comment utiliser HDInsight en parcourant des scénarios de base, tels que l’analyse de journaux web et de données de capteur. Vous y apprenez à utiliser HDInsight pour analyser de telles données et à connecter d’autres applications et services à ces données. La visualisation de données en se connectant à Microsoft Excel illustre parfaitement la puissance de cette méthode.</p></td>
<td>Console de requête</td>
<td>Hadoop</td>
<td>N/A</td>
</tr>
<tr>
<td>Résolution du problème de fuite de mémoire dans Templeton</td>
<td>Une fuite de mémoire dans Templeton a été corrigée. Ce problème concernait les clients qui possédaient un cluster de longue durée ou qui envoyaient des centaines de demandes de tâches à la seconde. Ce problème se manifestait sous la forme d'erreurs Templeton 5xx et la solution consistait à redémarrer service. Cette solution n'est plus nécessaire.</td>
<td>Templeton</td>
<td>Tout</td>
<td>https://issues.apache.org/jira/browse/HADOOP-11248</td>
</tr>
</table>

> [!NOTE]
> Pour démontrer les nouvelles fonctionnalités rendues disponibles par la personnalisation de cluster, les procédures qui utilisent des actions de script pour installer les modules Spark et R sur un cluster ont été documentées. Pour plus d'informations, consultez les pages suivantes :

* [Installation et utilisation de Spark 1.0 sur des clusters HDInsight](hdinsight-hadoop-spark-install.md)
* [Installation et utilisation de R sur des clusters HDInsight Hadoop](hdinsight-hadoop-r-scripts.md)

## <a name="notes-for-11072014-release-of-hdinsight"></a>Notes relatives à la version du 07/11/2014 de HDInsight

Les numéros de version complets des clusters HDInsight déployés avec cette version sont les suivants :

* HDInsight 2.1    2.1.9.374.1153876
* HDInsight 3.0    3.0.5.374.1153876
* HDInsight 3.1    3.1.1.374.1153876

Cette version contient les mises à jour de composant suivantes :

<table border="1">
<tr><th>Intitulé</th><th>Description</th><th>Composant</th><th>Type du cluster</th><th>JIRA (le cas échéant)</th></tr>
<tr>
<td>HDP 2.1.7</td>
<td>Cette version est basée sur Hortonworks Data Platform (HDP) 2.1.7. Pour plus d’informations, consultez les <a href="http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.7-Win/bk_releasenotes_HDP-Win/content/ch_relnotes-HDP-2.1.7.html" target="_blank">Notes de publication de HDP-2.1.7</a>.</td>
<td>HDP</td>
<td>Tout</td>
<td>N/A</td>
</tr>
<tr>
<td>YARN Timeline Server</td>
<td>YARN Timeline Server (connu également sous le nom de Generic Application History Server) a été activé par défaut. Ce serveur fournit des informations génériques sur les applications terminées, telles que l’ID, le nom, l’état, l’heure d’envoi et l’heure de fin de l’application.

Ces informations peuvent être extraites du nœud principal, soit en accédant à l’URI http://headnodehost:8188, soit en exécutant la commande YARN : yarn application -list -appStates ALL.

soit à distance via l’API REST à l’adresse https://{ClusterDnsName}. azurehdinsight.net/ws/v1/applicationhistory/.

Pour plus d’informations, consultez <a href="http://hadoop.apache.org/docs/r2.4.0/hadoop-yarn/hadoop-yarn-site/TimelineServer.html" target="_blank">YARN Timeline Server</a>.</td>
<td>Service, YARN</td>
<td>Hadoop, HBase</td>
<td>N/A</td>
</tr>
<tr>
<td>ID de déploiement de cluster</td>
<td>Depuis la version du Kit de développement logiciel (SDK) 1.3.3.1.5426.29232, les utilisateurs peuvent accéder à un identificateur unique émis par HDInsight pour chaque cluster. Cela permet aux clients de résoudre les instances uniques de clusters lorsqu’un nom DNS est réutilisé dans des scénarios de création/suppression.</td>
<td>Foundation</td>
<td>Tout</td>
<td>N/A</td>
</tr>
</table>

> [!NOTE]
> L’erreur qui empêchait la version complète # de s’afficher dans le portail ou d’être renvoyée par le Kit de développement logiciel (SDK) ou par PowerShell a été corrigée dans cette version.

## <a name="notes-for-10152014-release"></a>Notes pour la version du 15/10/2014

Cette version de correctif logiciel a résolu un problème de fuite de mémoire dans Templeton qui affectait les utilisateurs réguliers de Templeton. Dans certains cas, les utilisateurs réguliers de Templeton faisaient face à des erreurs ayant le code d’erreur 500, car leurs demandes ne disposaient pas d’assez de mémoire pour s’exécuter. La solution de contournement pour ce problème consistait à redémarrer le service Templeton. Ce problème est à présent résolu.

## <a name="notes-for-1072014-release"></a>Notes pour la version du 07/10/2014

* Lors de l’utilisation du point de terminaison Ambari, « https://{clusterDns}.azurehdinsight.net/ambari/api/v1/clusters/{clusterDns}.azurehdinsight.net/services/{servicename}/components/{componentname} », le champ *host_name* renvoie à présent le nom de domaine complet du nœud au lieu du seul nom d’hôte. Par exemple, au lieu de renvoyer « **headnode0** », vous pouvez obtenir le nom de domaine complet « **headnode0.{ClusterDNS}.azurehdinsight.net** ». Cette modification était nécessaire pour permettre les scénarios dans lesquels plusieurs types de cluster tels que HBase et Hadoop sont déployés dans un réseau virtuel. Cela se produit, par exemple, lors de l'utilisation de HBase en tant que plateforme principale pour Hadoop.

* Nous avons fourni de nouveaux paramètres de mémoire pour le déploiement par défaut d'un cluster HDInsight. Les précédents paramètres de mémoire ne prenaient pas correctement en compte les conseils relatifs au nombre de cœurs de processeurs déployés. Ces nouveaux paramètres de mémoire doivent normalement fournir de meilleures valeurs par défaut, conformément aux recommandations de Hortonworks. Pour les modifier, veuillez consulter la documentation de référence du Kit de développement logiciel (SDK) relative à la modification de la configuration du cluster. Les nouveaux paramètres de mémoire utilisés par le cluster HDInsight quadricœur (8 conteneurs) par défaut sont répertoriés dans le tableau suivant. Les valeurs utilisées avant cette version sont également indiquées entre parenthèses.

<table border="1">
<tr><th>Composant</th><th>Allocation de mémoire</th></tr>
<tr><td> yarn.scheduler.minimum-allocation</td><td>768 Mo (précédemment 512 Mo)</td></tr>
<tr><td> yarn.scheduler.maximum-allocation</td><td>6144 Mo (inchangé)</td></tr>
<tr><td>yarn.nodemanager.resource.memory</td><td>6144 Mo (inchangé)</td></tr>
<tr><td>mapreduce.map.memory</td><td>768 Mo (précédemment 512 Mo)</td></tr>
<tr><td>mapreduce.map.java.opts</td><td>opts=-Xmx512m (précédemment -Xmx410m)</td></tr>
<tr><td>mapreduce.reduce.memory</td><td>1536 Mo (précédemment 1024 Mo)</td></tr>
<tr><td>mapreduce.reduce.java.opts</td><td>opts=-Xmx1024m (précédemment -Xmx819m)</td></tr>
<tr><td>yarn.app.mapreduce.am.resource</td><td>768 Mo (précédemment 1024 Mo)</td></tr>
<tr><td>yarn.app.mapreduce.am.command</td><td>opts=-Xmx512m (précédemment -Xmx819m)</td></tr>
<tr><td>mapreduce.task.io.sort</td><td>256 Mo (précédemment 200 Mo)</td></tr>
<tr><td>tez.am.resource.memory</td><td>1536 Mo (inchangé)</td></tr>
</table>

Pour plus d’informations sur les paramètres de configuration de mémoire utilisés par YARN et MapReduce sur la plateforme de données Hortonworks utilisée par HDInsight, consultez la page [Déterminer les paramètres de configuration de la mémoire HDP](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1-latest/bk_installing_manually_book/content/rpm-chap1-11.html). Hortonworks a également fourni un outil permettant de calculer les paramètres de mémoire adéquats.

En ce qui concerne Azure PowerShell et le message d’erreur du Kit de développement logiciel (SDK) HDInsight : «*Le cluster n’est pas configuré pour l’accès aux services HTTP*» :

* Cette erreur est un [problème de compatibilité](https://social.msdn.microsoft.com/Forums/azure/a7de016d-8de1-4385-b89e-d2e7a1a9d927/hdinsight-powershellsdk-error-cluster-is-not-configured-for-http-services-access?forum=hdinsight) connu pouvant survenir en raison d’une différence entre la version du Kit de développement logiciel (SDK) HDInsight ou d’Azure PowerShell et la version du cluster. Les clusters créés le 15/08 ou ultérieurement prennent en charge la nouvelle capacité d’approvisionnement dans les réseaux virtuels. Mais cette capacité n’est pas interprétée correctement par les versions antérieures du Kit de développement logiciel (SDK) HDInsight ou Azure PowerShell. Il en résulte un échec dans certaines opérations de soumission de tâches. Si vous utilisez des API du Kit de développement logiciel (SDK) HDInsight ou des applets de commande Azure PowerShell (**Use-AzureRmHDInsightCluster** ou **Invoke-AzureRmHDInsightHiveJob**) pour envoyer des tâches, ces opérations peuvent échouer avec le message d’erreur « *Le cluster <clustername> n’est pas configuré pour l’accès aux services HTTP* ». Ou, en fonction de l’opération, vous pouvez recevoir d’autres types de message d’erreur tels que «*Impossible de se connecter au cluster*».
* Ces problèmes de compatibilité sont résolus dans les dernières versions du Kit de développement logiciel (SDK) HDInsight et Azure PowerShell. Nous vous recommandons de mettre à jour le Kit de développement logiciel (SDK) HDInsight vers la version 1.3.1.6 ou ultérieure et les outils Azure PowerShell vers la version 0.8.8 ou ultérieure. Vous pouvez accéder au dernier Kit de développement logiciel (SDK) HDInsight à partir de [NuGet](http://nuget.codeplex.com/wikipage?title=Getting%20Started) et aux outils Azure PowerShell les plus récents sur la page [Installation et configuration d’Azure PowerShell](/powershell/azure/overview).

## <a name="notes-for-9122014-release-of-hdinsight-31"></a>Notes pour la version du 12/09/2014 de HDinsight 3.1
* Cette version est basée sur Hortonworks Data Platform (HDP) 2.1.5. Pour obtenir la liste des bogues corrigés dans cette version, consultez la page [Erreurs corrigées dans cette version](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.5/bk_releasenotes_hdp_2.1/content/ch_relnotes-hdp-2.1.5-fixed.html) sur le site Hortonworks.
* Dans le dossier de bibliothèques Pig, le fichier « avro-mapred-1.7.4.jar » a été remplacé par « avro-mapred-1.7.4-hadoop2.jar. » Ce fichier contient une résolution de bogue mineur ne provoquant pas d’arrêt. Nous recommandons aux clients de ne pas établir de dépendance directe sur le nom du fichier jar en lui-même, pour éviter tout arrêt intempestif lorsque des fichiers sont renommés.

## <a name="notes-for-8212014-release"></a>Notes pour la version du 21/08/2014
* Nous ajoutons la nouvelle configuration WebHCat suivante (HIVE-7155) qui fixe la limite de mémoire par défaut pour une tâche de contrôleur Templeton à 1 Go : (L’ancienne valeur par défaut était de 512 Mo.)

     templeton.mapper.memory.mb (=1024)

  * Cette modification résout l’erreur suivante que certaines requêtes Hive rencontraient en raison des limites de mémoire plus basses : « Le conteneur a dépassé les limites de la mémoire physique. »
  * Pour revenir aux anciens paramètres par défaut, vous pouvez définir cette valeur de configuration sur 512 via Azure PowerShell au moment de la création du cluster, avec la commande suivante :

      Add-AzureRmHDInsightConfigValues -Core @{"templeton.mapper.memory.mb"="512";}
* Le nom d’hôte du rôle zookeeper a été remplacé par *zookeeper*. Cela a une incidence sur la résolution de noms dans le cluster, mais pas sur les API REST externes. Si vous avez des composants qui utilisent le nom d’hôte *zookeepernode* , vous devez les mettre à jour pour qu’ils utilisent le nouveau nom. Les nouveaux noms des trois nœuds zookeeper sont les suivants :

  * zookeeper0
  * zookeeper1
  * zookeeper2
* La matrice de support des versions de HBase est mise à jour. Seule la version HDInsight 3.1 (HBase version 0.98) est prise en charge pour les charges de travail HBase de production. La version 3.0 qui était disponible en tant que version préliminaire ne sera plus prise en charge à l’avenir.

## <a name="notes-about-clusters-created-prior-to-8152014"></a>Notes sur les clusters créés avant le 15/08/2014
Vous pouvez rencontrer une erreur de Kit de développement logiciel (SDK) HDInsight ou Azure PowerShell dont le message est « Le cluster <clustername> n’est pas configuré pour l’accès aux services HTTP » (ou, en fonction de l’opération, d’autres messages comme : « Impossible de se connecter au cluster ») en raison d’une différence de version entre le Kit de développement logiciel (SDK) HDInsight ou Azure PowerShell et un cluster. Les clusters créés le 15/08 ou ultérieurement prennent en charge la nouvelle capacité d’approvisionnement dans les réseaux virtuels. Cette capacité n’est pas interprétée correctement par les versions antérieures du Kit de développement logiciel (SDK) HDinsight ou Azure PowerShell, ce qui entraîne des défaillances d’opérations d’envoi de tâche. Si vous utilisez des API de Kit de développement logiciel (SDK) HDInsight ou des applets de commande PowerShell (comme Use-AzureRmHDInsightCluster ou Invoke-AzureRmHDInsightHiveJob) pour envoyer des tâches, il est possible que ces opérations échouent en affichant l’un des messages d’erreur décrits plus haut.

Ces problèmes de compatibilité sont résolus dans les dernières versions du Kit de développement logiciel (SDK) HDInsight et Azure PowerShell. Nous vous recommandons de mettre à jour le Kit de développement logiciel (SDK) HDInsight vers la version 1.3.1.6 ou ultérieure et les outils Azure PowerShell vers la version 0.8.8 ou ultérieure. Vous pouvez accéder au Kit de développement logiciel (SDK) HDInsight le plus récent depuis [NuGet][nuget-link]. Vous pouvez accéder à Azure PowerShell Tools à l’aide de [Microsoft Web Platform Installer][webpi-link].

## <a name="notes-for-7282014-release"></a>Notes pour la version du 28/07/14
* **HDInsight disponible dans de nouvelles régions** : nous avons étendu la présence géographique de HDInsight à trois nouvelles régions. Les clients HDInsight peuvent créer des clusters dans ces régions.
  * Est de l'Asie
  * États-Unis - partie centrale septentrionale
  * Centre-Sud des États-Unis
* Suppression en cours de HDInsight version 1.6 (HDP 1.1 et Hadoop 1.0.3) et de HDInsight version 2.1 (HDP 1.3 et Hadoop 1.2) du portail Azure. Vous pouvez continuer à créer des clusters Hadoop pour ces versions avec l’applet de commande Azure PowerShell [New-AzureRmHDInsightCluster](http://msdn.microsoft.com/library/dn593744.aspx) ou avec le [Kit de développement logiciel (SDK) HDInsight](http://msdn.microsoft.com/library/azure/dn469975.aspx). Pour plus d’informations, consultez [Contrôle de version des composants HDInsight](hdinsight-component-versioning.md).
* Changements concernant Hortonworks Data Platform (HDP) dans cette version :

<table border="1">
<tr><th>HDP</th><th>Changements</th></tr>
<tr><td>HDP 1.3 / HDI 2.1</td><td>Pas de changements</td></tr>
<tr><td>HDP 2.0 / HDI 3.0</td><td>Pas de changements</td></tr>
<tr><td>HDP 2.1 / HDI 3.1</td><td>zookeeper: ['3.4.5.2.1.3.0-1948'] -> ['3.4.5.2.1.3.2-0002']</td></tr>
</table>

## <a name="notes-for-6242014-release"></a>Notes pour la version du 24/06/14
Cette version inclut des améliorations du service HDInsight :

* **Disponibilité de HDP 2.1**: HDInsight 3.1, qui contient HDP 2.1, est désormais disponible pour le grand public et constitue la version par défaut pour les nouveaux clusters.
* **HBase : amélioration du portail Azure**: nous faisons en sorte que les clusters HBase soient disponibles dans la version préliminaire. Vous pouvez créer des clusters HBase à partir du portail en quelques clics.

Avec HBase, vous pouvez créer différentes charges de travail en temps réel sur HDInsight, de sites web interactifs fonctionnant avec des jeux de données volumineux à des services stockant les données de capteur et de télémétrie provenant de millions de points de terminaison. L’étape suivante consisterait à analyser les données dans ces charges de travail avec des tâches Hadoop, ce qui est possible dans HDInsight grâce, notamment, à Azure PowerShell et au tableau de bord de cluster Hive.

### <a name="apache-mahout-preinstalled-on-hdinsight-31"></a>Apache Mahout préinstallé sur HDInsight 3.1
 [Mahout](http://hortonworks.com/hadoop/mahout/) est préinstallé sur les clusters Hadoop HDInsight 3.1, afin de pouvoir exécuter des tâches Mahout sans configuration de cluster supplémentaire. Par exemple, vous pouvez vous connecter à distance à un cluster Hadoop avec le protocole RDP (Remote Desktop Protocol) et exécuter la commande Mahout Hello World suivante sans étape supplémentaire :

        mahout org.apache.mahout.classifier.df.tools.Describe -p /user/hdp/glass.data -f /user/hdp/glass.info -d I 9 N L

        mahout org.apache.mahout.classifier.df.BreimanExample -d /user/hdp/glass.data -ds /user/hdp/glass.info -i 10 -t 100

Pour une explication plus complète de cette procédure, consultez la documentation de l’ [Exemple Breiman](https://mahout.apache.org/users/classification/breiman-example.html) sur le site web Apache Mahout.

### <a name="hive-queries-can-use-tez-in-hdinsight-31"></a>Les requêtes Hive peuvent utiliser Tez dans HDinsight 3.1
Hive 0.13 est désormais disponible dans HDInsight 3.1 et capable d’exécuter des requêtes avec Tez. Des gains de performances considérables peuvent ainsi être obtenus.
Tez n’est pas activé par défaut pour les requêtes Hive. Vous devez choisir de l’utiliser. Vous pouvez activer Tez en exécutant l’extrait de code suivant :

        set hive.execution.engine=tez;
        select sc_status, count(*), histogram_numeric(sc_bytes,5) from website_logs_orc_local group by sc_status;

Hortonworks a publié une ventilation détaillée des améliorations apportées aux requêtes Hive en termes de performances avec Tez, tel qu'il est fourni dans les benchmarks standard. Pour des détails, consultez la page [Tests de performances d'Apache Hive 13 for Enterprise Hadoop](http://hortonworks.com/blog/benchmarking-apache-hive-13-enterprise-hadoop/).

Pour plus d’informations, consultez l’article [Hive on Tez](https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez) (Hive sur Tez).

### <a name="global-availability"></a>Disponibilité générale
Avec le lancement de HDInsight sur Hadoop 2.2, Microsoft a fait en sorte que HDInsight soit disponible dans les principales régions où Azure est disponible. Plus précisément, l’Europe de l’Ouest et le Sud-Est asiatique ont été mis en ligne. Cela permet aux clients de rechercher des clusters dans un centre de données proche et, potentiellement, dans une zone avec des exigences de conformité similaires.

### <a name="dos--donts-between-cluster-versions"></a>À faire et ne pas faire entre les versions de clusters
**Les metastores Oozie utilisés avec un cluster HDInsight 3.1 n’ont plus de compatibilité descendante avec les clusters HDInsight 2.1 et ne peuvent pas être utilisés avec cette version précédente**.

Vous ne pouvez plus réutiliser une base de données de metastore Oozie personnalisée déployée avec un cluster HDInsight 3.1 avec un cluster HDInsight 2.1. Cela est valable même si le metastore a été créé avec un cluster HDInsight 2.1. Ce scénario n’est pas pris en charge, car le schéma du metastore est mis à niveau lorsqu’il est utilisé avec un cluster HDInsight 3.1. Il n’est donc plus compatible avec le metastore requis par les clusters HDInsight 2.1. Toute tentative de réutilisation d’un metastore Oozie utilisé avec un cluster HDInsight 3.1 rend le cluster HDInsight 2.1 inutilisable.

**Impossible de partager des metastores Oozie entre des clusters.**

Les metastores Oozie sont joints à des clusters spécifiques. Vous ne pouvez donc pas les partager entre différents clusters.

### <a name="breaking-changes"></a>Dernières modifications
**Syntaxe du préfixe** : seule la syntaxe « wasb:// » est prise en charge dans les clusters HDInsight 3.1 et 3.0. L’ancienne syntaxe « asv:// » est prise en charge dans les clusters HDInsight 2.1 et 1.6, mais elle n’est pas prise en charge dans les clusters HDInsight 3.1 ou 3.0. Cela signifie que toutes les tâches envoyées vers un cluster HDInsight 3.1 ou 3.0 utilisant explicitement la syntaxe « asv:// » échoueront. Vous devez utiliser la syntaxe « wasb:// » à la place. De même, les tâches créées avec un metastore existant contenant des références explicites aux ressources utilisant la syntaxe « asv:// » et envoyées vers un cluster HDInsight 3.1 ou 3.0 échouent également. Vous devez recréer ces metastores en utilisant la syntaxe « wasb:// » pour adresser les ressources.

**Ports**: les ports utilisés par le service HDInsight ont changé. Les numéros de ports utilisés étaient inclus dans la plage de ports éphémères du système d’exploitation Windows. Les ports sont alloués automatiquement à partir d’une plage éphémère prédéfinie pour des communications à durée de vie limitée basées sur un protocole Internet. Le nouvel ensemble de numéros de ports du service HDP (Hortonworks Data Platform) autorisés est à l’extérieur de cette plage pour éviter tout conflit avec les ports utilisés par les services exécutés sur le nœud principal. Les nouveaux numéros de ports ne devraient pas entraîner des modifications radicales. Les numéros utilisés sont les suivants :

 **HDInsight 1.6 (HDP 1.1)**

<table border="1">
<tr><th>Nom</th><th>Valeur</th></tr>
<tr><td>dfs.http.address</td><td>namenodehost:30070</td></tr>
<tr><td>dfs.datanode.address</td><td>0.0.0.0:30010</td></tr>
<tr><td>dfs.datanode.http.address</td><td>0.0.0.0:30075</td></tr>
<tr><td>dfs.datanode.ipc.address</td><td>0.0.0.0:30020</td></tr>
<tr><td>dfs.secondary.http.address</td><td>0.0.0.0:30090</td></tr>
<tr><td>mapred.job.tracker.http.address</td><td>jobtrackerhost:30030</td></tr>
<tr><td>mapred.task.tracker.http.address</td><td>0.0.0.0:30060</td></tr>
<tr><td>mapreduce.history.server.http.address</td><td>0.0.0.0:31111</td></tr>
<tr><td>templeton.port</td><td>30111</td></tr>
</table>

 **HDInsight 3.1 et 3.0 (HDP 2.1 et 2.0)**

<table border="1">
<tr><th>Nom</th><th>Valeur</th></tr>
<tr><td>dfs.namenode.http-address</td><td>namenodehost:30070</td></tr>
<tr><td>dfs.namenode.https-address</td><td>headnodehost:30470</td></tr>
<tr><td>dfs.datanode.address</td><td>0.0.0.0:30010</td></tr>
<tr><td>dfs.datanode.http.address</td><td>0.0.0.0:30075</td></tr>
<tr><td>dfs.datanode.ipc.address</td><td>0.0.0.0:30020</td></tr>
<tr><td>dfs.namenode.secondary.http-address</td><td>0.0.0.0:30090</td></tr>
<tr><td>yarn.nodemanager.webapp.address</td><td>0.0.0.0:30060</td></tr>
<tr><td>templeton.port</td><td>30111</td></tr>
</table>

### <a name="dependencies"></a>Dépendances
Les dépendances suivantes ont été ajoutées à HDInsight 3.x (HDP2.x) :

* guice-servlet
* optiq-core
* javax.inject
* activation
* jsr305
* geronimo-jaspic_1.0_spec
* jul-to-slf4j
* java-xmlbuilder
* ant
* commons-compiler
* jdo-api
* commons-math3
* paranamer
* jaxb-impl
* stringtemplate
* eigenbase-xom
* jersey-servlet
* commons-exec
* jaxb-api
* jetty-all-server
* janino
* xercesImpl
* optiq-avatica
* jta
* eigenbase-properties
* groovy-all
* hamcrest-core
* mail
* linq4j
* jpam
* jersey-client
* aopalliance
* geronimo-annotation_1.0_spec
* ant-launcher
* jersey-guice
* xml-apis
* stax-api
* asm-commons
* asm-tree
* wadl
* geronimo-jta_1.1_spec
* guice
* leveldbjni-all
* velocity
* jettison
* snappy-java
* jetty-all
* commons-dbcp

Les dépendances suivantes n'existent plus dans HDInsight 3.x (HDP2.x) :

* jdeb
* kfs
* sqlline
* ivy
* aspectjrt
* json
* core
* jdo2-api
* avro-mapred
* datanucleus-enhancer
* jsp
* commons-logging-api
* commons-math
* JavaEWAH
* aspectjtools
* javolution
* hdfsproxy
* hbase
* snappy

### <a name="version-changes"></a>Changements de version
Les changements de version suivants ont eu lieu entre HDInsight 2.x (HDP1.x) et HDInsight 3.x (HDP2.x) :

* metrics-core : [« 2.1.2 »] -> [« 3.0.0 »]
* derbynet : [« 10.4.2.0 »] -> [« 10.10.1.1 »]
* datanucleus : [« rdbms-3.0.8 »] -> [« rdbms-3.2.9 »]
* jasper-compiler : [« 5.5.12 »] -> [« 5.5.23 »]
* log4j : [« 1.2.15 »], [« 1.2.16 »] -> [« 1.2.16 », « 1.2.17 »]
* derbyclient : [« 10.4.2.0 »] -> [« 10.10.1.1 »]
* httpcore : [« 4.2.4 »] -> [« 4.2.5 »]
* hsqldb : [« 1.8.0.10 »] -> [« 2.0.0 »]
* jets3t : [« 0.6.1 »] -> [« 0.9.0 »]
* protobuf-java : [« 2.4.1 »] -> [« 2.5.0 »]
* derby : [« 10.4.2.0 »] -> [« 10.10.1.1 »]
* jasper : [« runtime-5.5.12 »] -> [« runtime-5.5.23 »]
* commons-daemon : [« 1.0.1 »] -> [« 1.0.13 »]
* datanucleus-core : [« 3.0.9 »] -> [« 3.2.10 »]
* datanucleus-api-jdo : [« 3.0.7 »] -> [« 3.2.6 »]
* zookeeper : [« 3.4.5.1.3.9.0-01320 »] -> [« 3.4.5.2.1.3.0-1948 »]
* bonecp : [« 0.7.1.RELEASE »] -> [« 
* 0.8.0.RELEASE »]

### <a name="drivers"></a>Pilotes
Le pilote JDBC pour SQL Server est utilisé en interne par HDInsight et n’est pas employé pour les opérations externes. Si vous voulez vous connecter à HDInsight avec ODBC, utilisez le pilote ODBC Hive de Microsoft. Pour plus d’informations, consultez la page [Connexion d’Excel à HDInsight avec le pilote ODBC Hive de Microsoft](hdinsight-connect-excel-hive-odbc-driver.md).

### <a name="bug-fixes"></a>Résolution des bogues
Dans cette version, nous avons actualisé les versions suivantes de HDInsight avec la résolution de plusieurs bogues :

* HDInsight 2.1 (HDP 1.3)
* HDInsight 3.0 (HDP 2.0)
* HDInsight 3.1 (HDP 2.1)

## <a name="hortonworks-release-notes"></a>Notes de publication de Hortonworks
Les notes de publication des plateformes de données Hortonworks (HDP) utilisées par les versions de cluster HDInsight sont disponibles aux emplacements suivants :

* Le cluster HDInsight version 3.1 utilise une distribution Hadoop basée sur [Hortonworks Data Platform 2.1.7][hdp-2-1-7]. Il s’agit du cluster Hadoop par défaut créé lors de l’utilisation du portail Azure après le 07/11/2014. Les clusters HDInsight 3.1 créés avant le 07/11/2014 étaient basés sur [Hortonworks Data Platform 2.1.1][hdp-2-1-1]
* Le cluster HDInsight version 3.0 utilise une distribution Hadoop basée sur [Hortonworks Data Platform 2.0][hdp-2-0-8].
* Le cluster HDInsight version 2.1 utilise une distribution Hadoop basée sur [Hortonworks Data Platform 1.3][hdp-1-3-0].
* Le cluster HDInsight version 1.6 utilise une distribution Hadoop basée sur [Hortonworks Data Platform 1.1][hdp-1-1-0].

[hdp-2-1-7]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.7-Win/bk_releasenotes_HDP-Win/content/ch_relnotes-HDP-2.1.7.html

[hdp-2-1-1]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.1/bk_releasenotes_hdp_2.1/content/ch_relnotes-hdp-2.1.1.html

[hdp-2-0-8]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.0.8.0/bk_releasenotes_hdp_2.0/content/ch_relnotes-hdp2.0.8.0.html

[hdp-1-3-0]: http://docs.hortonworks.com/HDPDocuments/HDP1/HDP-1.3.0/bk_releasenotes_hdp_1.x/content/ch_relnotes-hdp1.3.0_1.html

[hdp-1-1-0]: http://docs.hortonworks.com/HDPDocuments/HDP1/HDP-Win-1.1/bk_releasenotes_HDP-Win/content/ch_relnotes-hdp-win-1.1.0_1.html

[nuget-link]: https://www.nuget.org/packages/Microsoft.WindowsAzure.Management.HDInsight/

[webpi-link]: http://go.microsoft.com/?linkid=9811175&clcid=0x409

[hdinsight-install-spark]: ../hdinsight-hadoop-spark-install/
[hdinsight-r-scripts]: ../hdinsight-hadoop-r-scripts/
