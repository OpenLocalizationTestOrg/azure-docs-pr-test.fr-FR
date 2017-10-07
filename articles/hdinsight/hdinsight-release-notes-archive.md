---
title: "notes d’aaaArchived - composants Hadoop sur Azure HDInsight | Documents Microsoft"
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
ms.openlocfilehash: 7a99c77f4557ca8c1dabe924cc67b2e0a134f8c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="release-notes-archive-for-hadoop-components-on-azure-hdinsight"></a>Notes de publication (archive) pour les composants Hadoop sur Azure HDInsight

Cet article fournit des informations sur hello **antérieure** mises à jour de la mise en production Azure HDInsight. Pour plus d’informations sur les versions plus récentes, consultez [Notes de publication de HDInsight](hdinsight-release-notes.md).

> [!IMPORTANT]
> Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure. Pour plus d’informations, consultez [l’article sur le contrôle de version de HDInsight](hdinsight-component-versioning.md).



## <a name="notes-for-08302016-release-of-hdinsight"></a>Notes relatives à la version du 30/08/2016 de HDInsight
numéros de version complet de Hello pour les clusters HDInsight de basés sur Linux déploiement avec cette version :

| HDI | Version de cluster HDI | HDP | Build HDP | Build d’Ambari |
| --- | --- | --- | --- | --- |
| 3.2 |3.2.1000.0.8268980 |2.2 |2.2.9.1-19 |2.2.1.12-4 |
| 3.3 |3.3.1000.0.8268980 |2.3 |2.3.3.1-25 |2.2.1.12-4 |
| 3.4 |3.4.1000.0.8269383 |2.4 |2.4.2.4-5 |2.2.1.12-4 |

numéros de version complet de Hello pour les clusters HDInsight de basés sur Windows sont déployés avec cette version :

| HDI | Version de cluster HDI | HDP | Build HDP |
| --- | --- | --- | --- |
| 2.1 |2.1.10.1033.2559206 |1.3 |1.3.12.0-01795 |
| 3.0 |3.0.6.1033.2559206 |2.0 |2.0.13.0-2117 |
| 3.1 |3.1.4.1033.2559206 |2.1 |2.1.16.0-2374 |
| 3.2 |3.2.7.1033.2559206 |2.2 |2.2.9.1-11 |
| 3.3 |3.3.0.1033.2559206 |2.3 |2.3.3.1-25 |


## <a name="08172016---release-of-r-server-on-hdinsight"></a>08/17/2016 - Version de R Server sur HDInsight
* R Server 8.0.5 - principalement une version de résolution d’un bogue. Consultez hello [notes de mise à jour du serveur R](https://msdn.microsoft.com/microsoft-r/notes/r-server-notes) pour plus d’informations.
* Package AzureML sur le nœud de périmètre hello - [ce package de R](https://cran.r-project.org/web/packages/AzureML/vignettes/getting_started.html) Active R modèles toobe publié et utilisé en tant que Azure ML web service.  Consultez hello [« Effectuent un modèle »](hdinsight-hadoop-r-server-overview.md#operationalize-a-model) section de notre [« Vue d’ensemble de R Server sur HDInsight »](hdinsight-hadoop-r-server-overview.md) article pour plus d’informations.
* Dépendances de Linux Hello [top 100 packages R plus populaires](https://github.com/metacran/cranlogs) -ces dépendances de package Linux sont maintenant préinstallés.
* Référentiel CRAN de hello option toouse lors de l’ajout de R packages toohello des nœuds de données. Pour plus d’informations, consultez la section [« Prise en main de R Server sur HDInsight »](hdinsight-hadoop-r-server-get-started.md).
* Hello améliorer la fiabilité de R Server configuration lors de la création de clusters.

## <a name="notes-for-08012016-release-of-hdinsight"></a>Notes pour la version du 01/08/2016 de HDInsight
numéros de version complet de Hello pour les clusters HDInsight de basés sur Linux déploiement avec cette version :

| HDI | Version de cluster HDI | HDP | Build HDP | Build d’Ambari |
| --- | --- | --- | --- | --- |
| 3.2 |3.2.1000.0.8028416 |2.2 |2.2.9.1-19 |2.2.1.12-4 |
| 3.3 |3.3.1000.0.8028416 |2.3 |2.3.3.1-25 |2.2.1.12-4 |
| 3.4 |3.4.1000.0.8053402 |2.4 |2.4.2.4-5 |2.2.1.12-4 |

numéros de version complet de Hello pour les clusters HDInsight de basés sur Windows sont déployés avec cette version :

| HDI | Version de cluster HDI | HDP | Build HDP |
| --- | --- | --- | --- |
| 2.1 |2.1.10.1005.2488842 |1.3 |1.3.12.0-01795 |
| 3.0 |3.0.6.1005.2488842 |2.0 |2.0.13.0-2117 |
| 3.1 |3.1.4.1005.2488842 |2.1 |2.1.16.0-2374 |
| 3.2 |3.2.7.1005.2488842 |2.2 |2.2.9.1-11 |
| 3.3 |3.3.0.1005.2488842 |2.3 |2.3.3.1-25 |

Cette version contient hello après les mises à jour :

| Intitulé | Description | Zone concernée (par exemple, Service, composant ou Kit de développement logiciel) | Type de cluster (par exemple, Spark, Hadoop, HBase ou Storm) | JIRA (le cas échéant) |
| --- | --- | --- | --- | --- |
| Modifications tooHDInsight 3.4 clusters |valeurs par défaut de Hello pour les configurations de ruche suivantes sont modifiés pour de meilleures performances <ul><li>`hive.vectorized.execution.reduce.enabled=true`</li><li>`hive.tez.min.partition.factor=1f`</li><li>`hive.tez.max.partition.factor=3f`</li><li>`tez.shuffle-vertex-manager.min-src-fraction=0.9`</li><li>`tez.shuffle-vertex-manager.max-src-fraction=0.95`</li><li>`tez.runtime.shuffle.connect.timeout= 30000`</li></ul> |Service |Tout |N/A |
| Les correctifs suivants sont inclus dans cette version |HIVE-13632, HIVE-12897,HIVE-12907,HIVE-12908,HIVE-12988,HIVE-13510,HIVE-13572,HIVE-13716,HIVE-13726,HIVE-12505,HIVE-13632,HIVE-13661,HIVE-13705,HIVE-13743,HIVE-13810,HIVE-13857,HIVE-13902,HIVE-13911,HIVE-13933 |de diffusion en continu |Tout |N/A |

## <a name="notes-for-07142016-release-of-hdinsight"></a>Notes pour la version du 14/07/2016 de HDinsight
numéros de version complet de Hello pour les clusters HDInsight de basés sur Linux déploiement avec cette version :

| HDI | Version de cluster HDI | HDP | Build HDP | Build d’Ambari |
| --- | --- | --- | --- | --- |
| 3.2 |3.2.1000.0.7932505 |2.2 |2.2.9.1-11 |2.2.1.12-2 |
| 3.3 |3.3.1000.0.7932505 |2.3 |2.3.3.1-18 |2.2.1.12-2 |
| 3.4 |3.4.1000.0.7933003 |2.4 |2.4.2.0 |2.2.1.12-2 |

numéros de version complet de Hello pour les clusters HDInsight de basés sur Windows sont déployés avec cette version :

| HDI | Version de cluster HDI | HDP | Build HDP |
| --- | --- | --- | --- |
| 2.1 |2.1.10.989.2441725 |1.3 |1.3.12.0-01795 |
| 3.0 |3.0.6.989.2441725 |2.0 |2.0.13.0-2117 |
| 3.1 |3.1.4.989.2441725 |2.1 |2.1.16.0-2374 |
| 3.2 |3.2.7.989.2441725 |2.2 |2.2.9.1-11 |
| 3.3 |3.3.0.989.2441725 |2.3 |2.3.3.1-21 |

## <a name="notes-for-07072016-release-of-hdinsight"></a>Notes pour la version du 07/07/2016 de HDinsight
numéros de version complet de Hello pour les clusters HDInsight de basés sur Linux déploiement avec cette version :

| HDI | Version de cluster HDI | HDP | Build HDP |
| --- | --- | --- | --- |
| 3.2 |3.2.1000.0.7864996 |2.2 |2.2.9.1-11 |
| 3.3 |3.3.1000.0.7864996 |2.3 |2.3.3.1-18 |
| 3.4 |3.4.1000.0.7861906 |2.4 |2.4.2.0 |

numéros de version complet de Hello pour les clusters HDInsight de basés sur Windows sont déployés avec cette version :

| HDI | Version de cluster HDI | HDP | Build HDP |
| --- | --- | --- | --- |
| 2.1 |2.1.10.977.2413853 |1.3 |1.3.12.0-01795 |
| 3.0 |3.0.6.977.2413853 |2.0 |2.0.13.0-2117 |
| 3.1 |3.1.4.977.2413853 |2.1 |2.1.16.0-2374 |
| 3.2 |3.2.7.977.2413853 |2.2 |2.2.9.1-11 |
| 3.3 |3.3.0.977.2413853 |2.3 |2.3.3.1-21 |

Cette version contient hello après les mises à jour :

| Intitulé | Description | Zone concernée (par exemple, Service, composant ou Kit de développement logiciel) | Type de cluster (par exemple, Spark, Hadoop, HBase ou Storm) | JIRA (le cas échéant) |
| --- | --- | --- | --- | --- |
| [Outils HDInsight pour IntelliJ](hdinsight-apache-spark-intellij-tool-plugin.md) |Le plug-in IntelliJ IDEA pour les clusters HDInsight Spark est désormais intégré au kit de ressources Azure pour IntelliJ. Il prend en charge de Windows Azure SDK v2.9.1, kits de développement Java plus récente et inclut toutes les fonctions hello de hello autonome HDInsight Plugin pour IntelliJ. |Outils |Spark |N/A |
| [Outils HDInsight pour Eclipse](hdinsight-apache-spark-eclipse-tool-plugin.md) |Le kit de ressources Azure pour Eclipse prend désormais en charge les clusters HDInsight Spark. Il permet de hello suivant de fonctionnalités : <ul><li>Créer et écrire une application Spark facilement en Scala et en Java, avec la prise en charge des opérations d’auteur première classe pour IntelliSense, la mise en forme automatique, la vérification des erreurs, etc.</li><li>Testez hello Spark application localement.</li><li>Soumettre le cluster de travaux tooHDInsight Spark et récupérer les résultats de hello.</li><li>Connectez-vous à tooAzure et accéder à tous les clusters de Spark hello associés à vos abonnements Azure.</li><li>Accédez à toutes les ressources de stockage hello associé de votre cluster HDInsight Spark.</li></ul> |Outils |Spark |N/A |

À compter de cette version, nous avons remplacé la stratégie mise à jour corrective de système d’exploitation invité hello pour des clusters HDInsight de basés sur Linux. Hello nouvelle stratégie de hello vise toosignificantly réduire le nombre de hello de redémarrages toopatching échéance. Hello nouvelle stratégie correctifs machines virtuelles (VM sur Linux) clusters chaque lundi ou un jeudi commençant à 0 h 00 UTC, Universal Time de manière progressive s’effectue entre les nœuds dans un cluster donné. Toutefois, toutes les machines virtuelles donné redémarre uniquement au maximum une fois tous les 30 jours en raison de la mise à jour corrective tooguest du système d’exploitation. En outre, premier redémarrage de hello pour un cluster nouvellement créé n’a pas lieu plus tôt plus de 30 jours à partir de la date de création de cluster hello.

> [!NOTE]
> Ces modifications s’appliquent uniquement à toonewly créé de clusters égale ou supérieure à la version release.
>
>

## <a name="notes-for-06062016-release-of-hdinsight"></a>Notes relatives à la version du 06/06/2016 de HDInsight
numéros de version complet de Hello pour les clusters HDInsight déployés avec cette version :

| HDP | Version de HDI | Version de Spark | Numéro de Build d’Ambari | Numéro de Build de HDP |
| --- | --- | --- | --- | --- |
| 2.3 |3.3.1000.0.7702215 |1.5.2 |2.2.1.8-2 |2.3.3.1-18 |
| 2.4 |3.4.1000.0.7702224 |1.6.1 |2.2.1.8-2 |2.4.2.0 |

Cette version contient hello après les mises à jour :

| Intitulé | Description | Zone concernée (par exemple, Service, composant ou Kit de développement logiciel) | Type de cluster (par exemple, Spark, Hadoop, HBase ou Storm) | JIRA (le cas échéant) |
| --- | --- | --- | --- | --- |
| Spark sur HDInsight est généralement disponible |Cette version apporte des améliorations dans la source de tooopen productivité Apache Spark sur HDInsight, évolutivité et disponibilité. <ul><li>Leader du marché avec un contrat de niveau de service (SLA) de 99,9 % pour la disponibilité, qui le rend adapté aux charges de travail importantes des entreprises.</li><li>Couche de stockage évolutive avec Azure Data Lake Store.</li><li>Outils de productivité pour chaque phase de développement et d’exploration des données. Des blocs-notes Jupyter avec noyau Spark personnalisé activent l’exploration interactive des données. L’intégration de tableaux de bord de BI tels que Power BI, Tableau et Qlik est intéressante pour un partage de données rapide et une création de rapports continue. Le plug-in IntelliJ est une option fiable de développement à long terme et de débogage d’artefacts de code.</li></ul> |de diffusion en continu |Spark |N/A |
| Outils HDInsight pour IntelliJ |Il s’agit d’un plug-in IntelliJ IDEA pour les clusters HDInsight Spark. Il permet de hello suivant de fonctionnalités :<ul><li>Créer et écrire une application Spark facilement en Scala et en Java, avec la prise en charge des opérations d’auteur première classe pour IntelliSense, la mise en forme automatique, la vérification des erreurs, etc.</li><li>Testez hello Spark application localement.</li><li>Soumettre le cluster de travaux tooHDInsight Spark et récupérer les résultats de hello.</li><li>Connectez-vous à tooAzure et accéder à tous les clusters de Spark hello associés à vos abonnements Azure.</li><li>Accédez à toutes les ressources de stockage hello associé de votre cluster HDInsight Spark.</li><li>Accédez à toutes les hello travaux travail informations d’historique et de votre cluster HDInsight Spark.</li><li>Déboguer les tâches Spark à distance à partir de votre ordinateur de bureau.</li></ul> |Outils |Spark |N/A |

## <a name="notes-for-05132016-release-of-hdinsight"></a>Notes pour la version du 13/05/2016 de HDInsight
numéros de version complet de Hello pour les clusters HDInsight déployés avec cette version :

* HDInsight    (Windows)         2.1.10.875.2159884 (HDP 1.3.12.0-01795 - inchangé)
* HDInsight    (Windows)         3.0.6.875.2159884 (HDP 2.0.13.0-2117 - inchangé)
* HDInsight    (Windows)         3.1.4.922.2266903  (HDP 2.1.15.0-2374 - inchangé)
* HDInsight    (Windows)        3.2.7.922.2266903  (HDP 2.2.9.1-11)
* HDInsight (Windows)        3.3.0.922.2266903  (HDP 2.3.3.1-18)
* HDInsight    (Linux)            3.2.1000.0.7565644   (HDP    2.2.9.1-11)
* HDInsight (Linux)            3.3.1000.0.7565644   (HDP 2.3.3.1-18)
* HDInsight (Linux)            3.4.1000.0.7548380   (HDP 2.4.2.0)

Cette version contient hello après les mises à jour :

| Intitulé | Description | Zone concernée (par exemple, Service, composant ou Kit de développement logiciel) | Type de cluster (par exemple, Spark, Hadoop, HBase ou Storm) | JIRA (le cas échéant) |
| --- | --- | --- | --- | --- |
| Mise à jour de la version Spark et autres correctifs de bogue |Cette version met à jour hello Spark dans HDInsight cluster too1.6.1 et résout les autres bogues. |Service |Spark |N/A |

## <a name="notes-for-04112016-release-of-hdinsight"></a>Notes de publication du 11/04/2016 pour HDInsight
numéros de version complet de Hello pour les clusters HDInsight déployés avec cette version :

* HDInsight    (Windows)         2.1.10.889.2191206 (HDP 1.3.12.0-01795 - inchangé)
* HDInsight    (Windows)         3.0.6.889.2191206 (HDP 2.0.13.0-2117 - inchangé)
* HDInsight    (Windows)         3.1.4.889.2191206  (HDP 2.1.15.0-2374 - inchangé)
* HDInsight    (Windows)        3.2.7.889.2191206  (HDP 2.2.9.1-10)
* HDInsight (Windows)        3.3.0.889.2191206  (HDP 2.3.3.1-16 - inchangé)
* HDInsight    (Linux)            3.2.1000.0.7339916   (HDP 2.2.9.1-10)
* HDInsight (Linux)            3.3.1000.0.7339916   (HDP 2.3.3.1-16)
* HDInsight (Linux)            3.4.1000.0.7338911   (HDP 2.4.1.1-3)
* Kit de développement logiciel (SDK)            1.5.8

Cette version contient hello après les mises à jour :

| Intitulé | Description | Zone concernée (par exemple, Service, composant ou Kit de développement logiciel) | Type de cluster (par exemple, Hadoop, HBase ou Storm) | JIRA (le cas échéant) |
| --- | --- | --- | --- | --- |
| Problèmes de mise à niveau personnalisée du metastore pour HDI 3.4 |La création du cluster échouait si vous utilisiez un metastore personnalisé auparavant utilisé sur une version antérieure d’un autre cluster HDInsight. Il s’agissait d’échéance tooan erreur mise à niveau de script qui a maintenant été corrigé |Création du cluster |Tout |N/A |
| Récupération après blocage de Livy |Fournit la résilience de l’état du travail pour tout travail soumis via Livy |Fiabilité |Spark sous Linux |N/A |
| Haute disponibilité du contenu de Jupyter |Fournit des hello capacité toosave et charge Notebook bloc-notes contenu tooand hello compte de stockage associé au cluster de hello. Pour plus d’informations, consultez [Noyaux disponibles pour les blocs-notes Jupyter](hdinsight-apache-spark-jupyter-notebook-kernels.md). |Blocs-notes |Spark sous Linux |N/A  |
| Suppression de hiveContext dans les blocs-notes Jupyter |Utilisez la commande magique `%%sql` au lieu de la commande magique `%%hive`. SqlContext est toohiveContext équivalent. Pour plus d’informations, consultez [Noyaux disponibles pour les blocs-notes Jupyter](hdinsight-apache-spark-jupyter-notebook-kernels.md) |Blocs-notes |Clusters Spark sur Linux |N/A |
| Désapprobation d’anciennes versions de Spark |Ancienne version Spark 1.3.1 a été supprimée de service de hello sur 31/5 |Service |Clusters Spark sur Windows |N/A |

## <a name="notes-for-03292016-release-of-hdinsight"></a>Notes pour la version du 29/03/2016 de HDInsight
numéros de version complet de Hello pour les clusters HDInsight déployés avec cette version :

* HDInsight    (Windows)         2.1.10.875.2159884 (HDP 1.3.12.0-01795 - inchangé)
* HDInsight    (Windows)         3.0.6.875.2159884 (HDP 2.0.13.0-2117 - inchangé)
* HDInsight    (Windows)         3.1.4.875.2159884  (HDP 2.1.15.0-2374 - inchangé)
* HDInsight    (Windows)        3.2.7.875.2159884  (HDP 2.2.9.1-7 - inchangé)
* HDInsight (Windows)        3.3.0.875.2159884  (HDP 2.3.3.1-16)
* HDInsight    (Linux)            3.2.1000.0.7193255   (HDP    2.2.9.1-8 - inchangé)
* HDInsight (Linux)            3.3.1000.0.7193255   (HDP 2.3.3.1-7 - inchangé)
* HDInsight (Linux)            3.4.1000.0.7195842   (HDP 2.4.1.0-327)
* Kit de développement logiciel (SDK)            1.5.8

Cette version contient hello après les mises à jour :

| Intitulé | Description | Zone concernée (par exemple, Service, composant ou Kit de développement logiciel) | Type de cluster (par exemple, Hadoop, HBase ou Storm) | JIRA (le cas échéant) |
| --- | --- | --- | --- | --- |
| Version 3.4 de HDInsight ajoutée et versions de HDP mises à jour pour tous les clusters HDInsight |Avec cette version, nous avons ajouté HDInsight version 3.4 (basée sur HDP 2.4) et avons également mis à jour d’autres versions de HDP. Les notes de publication de HDP 2.4 sont disponibles [ici](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.4.0/bk_HDP_RelNotes/content/ch_relnotes_v240.html). De plus amples informations sur les versions de HDInsight sont disponibles [ici](hdinsight-component-versioning.md). |de diffusion en continu |Tous les clusters Linux |N/A |
| HDInsight Premium |HDInsight est désormais disponible en deux catégories : Standard et Premium. HDInsight Premium est actuellement en version préliminaire, disponible uniquement pour les clusters Hadoop et Spark sur Linux. Vous pourrez trouver plus d’informations [ici](hdinsight-component-versioning.md#hdinsight-standard-and-hdinsight-premium). |Service |Hadoop et Spark sur Linux |N/A |
| Microsoft R Server |HDInsight Premium fournit Microsoft R Server qui peut être inclus avec les clusters Hadoop et Spark sur Linux. Pour plus d’informations, consultez [Vue d’ensemble : R Server sur HDInsight](hdinsight-hadoop-r-server-overview.md). |Service |Hadoop et Spark sur Linux |N/A |
| Spark 1.6.0 |Les clusters HDInsight 3.4 incluent désormais Spark 1.6.0 |de diffusion en continu |Clusters Spark sur Linux |N/A |
| Améliorations du Bloc-notes Jupyter |Les blocs-notes Jupyter disponibles avec les clusters Spark fournissent désormais des noyaux Spark supplémentaires. Ils incluent également des améliorations comme l’utilisation de %%magic, la visualisation automatique et l’intégration avec les bibliothèques de visualisation Python (par exemple, matplotlib). Pour plus d’informations, consultez [Noyaux disponibles pour les blocs-notes Jupyter](hdinsight-apache-spark-jupyter-notebook-kernels.md). |de diffusion en continu |Clusters Spark sur Linux |N/A |

## <a name="notes-for-03222016-release-of-hdinsight"></a>Notes pour la version du 22/03/2016 de HDInsight
numéros de version complet de Hello pour les clusters HDInsight déployés avec cette version :

* HDInsight    (Windows)         2.1.10.875.2159884 (HDP 1.3.12.0-01795 - inchangé)
* HDInsight    (Windows)         3.0.6.875.2159884 (HDP 2.0.13.0-2117 - inchangé)
* HDInsight    (Windows)         3.1.4.875.2159884  (HDP 2.1.15.0-2374 - inchangé)
* HDInsight    (Windows)        3.2.7.875.2159884  (HDP 2.2.9.1-7 - inchangé)
* HDInsight (Windows)        3.3.0.875.2159884  (HDP 2.3.3.1-16)
* HDInsight    (Linux)            3.2.1000.0.7193255   (HDP    2.2.9.1-8 - inchangé)
* HDInsight (Linux)            3.3.1000.0.7193255   (HDP 2.3.3.1-7 - inchangé)
* Kit de développement logiciel (SDK)            1.5.8

Cette version contient hello après les mises à jour :

| Intitulé | Description | Zone concernée (par exemple, Service, composant ou Kit de développement logiciel) | Type de cluster (par exemple, Hadoop, HBase ou Storm) | JIRA (le cas échéant) |
| --- | --- | --- | --- | --- |
| Versions de HDInsight mises à jour pour tous les clusters HDInsight |Dans cette version, nous avons mis à jour les versions de HDInsight pour tous les clusters HDInsight |de diffusion en continu |Tout |N/A |

## <a name="notes-for-03102016-release-of-hdinsight"></a>Notes pour la version du 10/03/2016 de HDInsight
numéros de version complet de Hello pour les clusters HDInsight déployés avec cette version :

* HDInsight    (Windows)         2.1.10.859.2123216 (HDP 1.3.12.0-01795 - inchangé)
* HDInsight    (Windows)         3.0.6.859.2123216 (HDP 2.0.13.0-2117 - inchangé)
* HDInsight    (Windows)         3.1.4.859.2123216  (HDP 2.1.15.0-2374 - inchangé)
* HDInsight    (Windows)        3.2.7.859.2123216  (HDP 2.2.9.1-7)
* HDInsight (Windows)        3.3.0.859.2123216  (HDP 2.3.3.1-5 - inchangé)
* HDInsight    (Linux)            3.2.1000.7076817   (HDP    2.2.9.1-8)
* HDInsight (Linux)            3.3.1000.7076817   (HDP 2.3.3.1-7)
* Kit de développement logiciel (SDK)            1.5.8

Cette version contient hello après les mises à jour :

| Intitulé | Description | Zone concernée (par exemple, Service, composant ou Kit de développement logiciel) | Type de cluster (par exemple, Hadoop, HBase ou Storm) | JIRA (le cas échéant) |
| --- | --- | --- | --- | --- |
| Versions de HDInsight mises à jour pour tous les clusters HDInsight |Dans cette version, nous avons mis à jour les versions de HDInsight pour tous les clusters HDInsight |de diffusion en continu |Tout |N/A |

## <a name="notes-for-01272016-release-of-hdinsight"></a>Notes relatives à la version de HDInsight du 27/01/2016
numéros de version complet de Hello pour les clusters HDInsight déployés avec cette version :

* HDInsight    (Windows)         2.1.10.817.2028315 (HDP 1.3.12.0-01795 - inchangé)
* HDInsight    (Windows)         3.0.6.817.2028315 (HDP 2.0.13.0-2117 - inchangé)
* HDInsight    (Windows)         3.1.4.817.2028315  (HDP 2.1.15.0-2374 - inchangé)
* HDInsight    (Windows)        3.2.7.817.2028315  (HDP 2.2.9.1-1)
* HDInsight (Windows)        3.3.0.817.2028315  (HDP 2.3.3.1-5 - inchangé)
* HDInsight    (Linux)            3.2.1000.4072335   (HDP    2.2.9.1-1)
* HDInsight (Linux)            3.3.1000.4072335   (HDP 2.3.3.1-1)
* Kit de développement logiciel (SDK)            1.5.8

Cette version contient hello après les mises à jour :

| Intitulé | Description | Zone concernée (par exemple, Service, composant ou Kit de développement logiciel) | Type de cluster (par exemple, Hadoop, HBase ou Storm) | JIRA (le cas échéant) |
| --- | --- | --- | --- | --- |
| Versions de HDInsight mises à jour pour tous les clusters HDInsight |Dans cette version, nous avons mis à jour les versions de HDInsight pour tous les clusters HDInsight |de diffusion en continu |Tout |N/A |

## <a name="notes-for-12022015-release-of-hdinsight"></a>Notes pour la version du 02/12/2015 de HDinsight
numéros de version complet de Hello pour les clusters HDInsight déployés avec cette version :

* HDInsight    (Windows)         2.1.10.763.1931434 (HDP 1.3.12.0-01795 - inchangé)
* HDInsight    (Windows)         3.0.6.763.1931434 (HDP 2.0.13.0-2117 - inchangé)
* HDInsight    (Windows)         3.1.4.763.1931434  (HDP 2.1.15.0-2374 - inchangé)
* HDInsight    (Windows)        3.2.7.763.1931434  (HDP 2.2.7.1-34 - inchangé)
* HDInsight (Windows)        3.3.1000.0           (HDP 2.3.3.1-5)
* HDInsight    (Linux)            3.2.1000.0.6392801 (HDP    2.2.7.1-34 - inchangé)
* HDInsight (Linux)            3.3.1000.0           (HDP 2.3.3.0-3039)
* Kit de développement logiciel (SDK)            1.5.8

Cette version contient hello après les mises à jour :

| Intitulé | Description | Zone concernée (par exemple, Service, composant ou Kit de développement logiciel) | Type de cluster (par exemple, Hadoop, HBase ou Storm) | JIRA (le cas échéant) |
| --- | --- | --- | --- | --- |
| Version 3.3 de HDInsight ajoutée et versions de HDP mises à jour pour tous les clusters HDInsight |Avec cette version, nous avons ajouté HDInsight version 3.3 (basée sur HDP 2.3) et avons également mis à jour d’autres versions de HDP. Les notes de publication de HDP 2.3 sont disponibles [ici](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.3.0/bk_HDP_RelNotes/content/ch_relnotes_v230.html). De plus amples informations sur les versions de HDInsight sont disponibles [ici](hdinsight-component-versioning.md). |de diffusion en continu |Tout |N/A |

## <a name="notes-for-11302015-release-of-hdinsight"></a>Notes relatives à la version du 30/11/2015 de HDInsight
numéros de version complet de Hello pour les clusters HDInsight déployés avec cette version :

* HDInsight    (Windows)         2.1.10.757.1923908 (HDP 1.3.12.0-01795 - inchangé)
* HDInsight    (Windows)         3.0.6.757.1923908  (HDP 2.0.13.0-2117 - inchangé)
* HDInsight    (Windows)         3.1.4.757.1923908  (HDP 2.1.15.0-2374 - inchangé)
* HDInsight    (Windows)        3.2.7.757.1923908  (HDP 2.2.7.1-34)
* HDInsight    (Linux)            3.2.1000.0.6392801 (HDP    2.2.7.1-34)
* Kit de développement logiciel (SDK)            1.5.8

Cette version contient hello après les mises à jour :

| Intitulé | Description | Zone concernée (par exemple, Service, composant ou Kit de développement logiciel) | Type de cluster (par exemple, Hadoop, HBase ou Storm) | JIRA (le cas échéant) |
| --- | --- | --- | --- | --- |
| Versions de HDInsight mises à jour pour tous les clusters HDInsight et les versions HDP pour les clusters HDInsight 3.2 (Windows et Linux) |Avec cette version, les versions de HDInsight et HDP ont été mises à jour |de diffusion en continu |Tout |N/A |

## <a name="notes-for-10272015-release-of-hdinsight"></a>Notes pour la version du 27/10/2015 de HDInsight
numéros de version complet de Hello pour les clusters HDInsight déployés avec cette version :

* HDInsight    (Windows)         2.1.10.726.1866228 (HDP 1.3.12.0-01795 - inchangé)
* HDInsight    (Windows)         3.0.6.726.1866228  (HDP 2.0.13.0-2117 - inchangé)
* HDInsight    (Windows)         3.1.4.726.1866228  (HDP 2.1.15.0-2374 - inchangé)
* HDInsight    (Windows)        3.2.7.726.1866228  (HDP 2.2.7.1-33)
* HDInsight    (Linux)            3.2.1000.0.6035701 (HDP    2.2.7.1-33)
* Kit de développement logiciel (SDK)            1.5.8

Cette version contient hello après les mises à jour :

| Intitulé | Description | Zone concernée (par exemple, Service, composant ou Kit de développement logiciel) | Type de cluster (par exemple, Hadoop, HBase ou Storm) | JIRA (le cas échéant) |
| --- | --- | --- | --- | --- |
| Versions de HDInsight mises à jour pour tous les clusters HDInsight (Windows et Linux) |Avec cette version, les versions de HDInsight et HDP ont été mises à jour |de diffusion en continu |Tout |N/A |
| Résolution des clusters Jupyter pour Windows Spark en lettres majuscules |Les clusters ayant des noms DNS spécifiés en majuscules présentaient les problèmes avec les ordinateurs portables Notebook en raison de la vérification de demande d’origine tooan. correctif de Hello a été nom DNS toochange hello cas de toolower de configuration du bloc-notes. |Service |HDInsight Spark (Windows) |N/A |

## <a name="notes-for-10202015-release-of-hdinsight"></a>Notes pour la version du 20/10/2015 de HDInsight
numéros de version complet de Hello pour les clusters HDInsight déployés avec cette version :

* HDInsight     2.1.10.716.1846990 (Windows)    (HDP 1.3.12.0-01795 - inchangé)
* HDInsight     3.0.6.716.1846990 (Windows)      (HDP 2.0.13.0-2117 - inchangé)
* HDInsight     3.1.4.716.1846990 (Windows)      (HDP 2.1.16.0-2374)
* HDInsight        3.2.7.716.1846990 (Windows)      (HDP 2.2.7.1-0004)
* HDInsight        3.2.1000.0.5930166 (Linux)        (HDP 2.2.7.1-0004)
* Kit de développement logiciel (SDK)            1.5.8

Cette version contient hello après les mises à jour :

| Intitulé | Description | Zone concernée (par exemple, Service, composant ou Kit de développement logiciel) | Type de cluster (par exemple, Hadoop, HBase ou Storm) | JIRA (le cas échéant) |
| --- | --- | --- | --- | --- |
| TooHDP de changement de version par défaut HDP 2.2 |version par défaut de Hello pour les clusters HDInsight Windows est modifié tooHDP 2.2. HDInsight version 3.2 (HDP 2.2) est disponible depuis février 2015. Cette modification renverse uniquement version du cluster hello par défaut, lorsqu’une sélection explicite n’a pas été établie lors de la configuration de cluster de hello hello portail Azure, les applets de commande PowerShell ou les hello SDK. |Service |Tout |N/A |
| Modifications apportées au format des noms de machines virtuelles pour le déploiement de plusieurs HDInsight sur des clusters Linux d’un même réseau virtuel |Cette version prend en charge le déploiement de plusieurs clusters Linux HDInsight sur un même réseau virtuel. Dans le cadre de la mise à jour, format hello des noms d’ordinateur virtuel dans un cluster de hello est passé de nœud principal\*, workernode\* et zookeepernode\* toohn\*, wn\*et zk\* respectivement. Il n’est pas une pratique recommandée de tootake une dépendance directe sur format hello des noms d’ordinateur virtuel, car il s’agit d’objet toochange. Utilisez « nom d’hôte -f » sur ordinateur local de hello ou Ambari APIs toodetermine hello liste des ordinateurs hôtes, mappage hello de composants toohosts. Pour plus d’informations, consultez [https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/hosts.md](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/hosts.md) et [https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/host-components.md](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/host-components.md). |de diffusion en continu |Clusters HDInsight sur Linux |N/A |
| Modifications de configuration |Pour les clusters HDInsight 3.1, hello suivant les configurations est maintenant activé : <ul><li>tez.yarn.ats.enabled et yarn.log.server.url. Cela permet de hello serveur chronologie d’Application et hello journal serveur toobe en mesure de tooserve des journaux.</li></ul>Pour les clusters HDInsight 3.2, hello suivant les configurations ont été modifié : <ul><li>MapReduce.fileoutputcommitter.Algorithm.version a été défini too2. Ainsi, l’utilisation de la version V2 de hello Hello FileOutputCommitter.</li></ul> |Service |Tout |N/A |

## <a name="notes-for-09092015-release-of-hdinsight"></a>Notes relatives à la version du 09/09/2015 de HDInsight
numéros de version complet de Hello pour les clusters HDInsight déployés avec cette version :

* HDInsight     2.1.10.675.1768697 (HDP 1.3.12.0-01795 - inchangé)
* HDInsight     3.0.6.675.1768697  (HDP 2.0.13.0-2117 - inchangé)
* HDInsight     3.1.4.675.1768697  (HDP 2.1.15.0-2334 - inchangé)
* HDInsight        3.2.6.675.1768697  (HDP 2.2.6.1-0012 - inchangé)
* Kit de développement logiciel (SDK)            1.5.8

Cette version contient hello après les mises à jour :

| Intitulé | Description | Zone concernée (par exemple, Service, composant ou Kit de développement logiciel) | Type de cluster (par exemple, Hadoop, HBase ou Storm) | JIRA (le cas échéant) |
| --- | --- | --- | --- | --- |
| Versions de HDInsight mises à jour pour tous les clusters HDInsight |Avec cette version, les versions de HDInsight ont été mises à jour |de diffusion en continu |Tout |N/A |

## <a name="notes-for-07312015-release-of-hdinsight"></a>Notes relatives à la version du 31/07/2015 de HDInsight
numéros de version complet de Hello pour les clusters HDInsight déployés avec cette version :

* HDInsight     2.1.10.640.1695824 (HDP 1.3.12.0-01795 - inchangé)
* HDInsight     3.0.6.640.1695824  (HDP 2.0.13.0-2117 - inchangé)
* HDInsight     3.1.4.640.1695824  (HDP 2.1.15.0-2334 - inchangé)
* HDInsight        3.2.6.640.1695824  (HDP 2.2.6.1-0012 - inchangé)
* Kit de développement logiciel (SDK)            1.5.8

Cette version contient hello après les mises à jour :

| Intitulé | Description | Zone concernée (par exemple, Service, composant ou Kit de développement logiciel) | Type de cluster (par exemple, Hadoop, HBase ou Storm) | JIRA (le cas échéant) |
| --- | --- | --- | --- | --- |
| Correctif du flux de travail de réimageage du nœud de cluster Spark |Correction d’un bogue qui a été à l’origine Spark toonot récupérer après la réinitialisation des nœuds de cluster |Service |Spark |N/A |

## <a name="notes-for-07312015-release-of-hdinsight"></a>Notes relatives à la version du 31/07/2015 de HDInsight
numéros de version complet de Hello pour les clusters HDInsight déployés avec cette version :

* HDInsight     2.1.10.635.1684502 (HDP 1.3.12.0-01795 - inchangé)
* HDInsight     3.0.6.635.1684502  (HDP 2.0.13.0-2117 - inchangé)
* HDInsight     3.1.4.635.1684502  (HDP 2.1.15.0-2334 - inchangé)
* HDInsight        3.2.6.635.1684502  (HDP 2.2.6.1-0012 - inchangé)
* Kit de développement logiciel (SDK)            1.5.8

Cette version contient hello après les mises à jour :

| Intitulé | Description | Zone concernée (par exemple, Service, composant ou Kit de développement logiciel) | Type de cluster (par exemple, Hadoop, HBase ou Storm) | JIRA (le cas échéant) |
| --- | --- | --- | --- | --- |
| Versions de HDInsight mises à jour pour tous les clusters HDInsight |Avec cette version, les versions de HDInsight ont été mises à jour |de diffusion en continu |Tout |N/A |

## <a name="notes-for-07072015-release-of-hdinsight"></a>Notes relatives à la version du 07/07/2015 de HDInsight
numéros de version complet de Hello pour les clusters HDInsight déployés avec cette version :

* HDInsight     2.1.10.610.1630216    (HDP 1.3.12.0-01795 - inchangé)
* HDInsight     3.0.6.610.1630216    (HDP 2.0.13.0-2117 - inchangé)
* HDInsight     3.1.4.610.1630216    (HDP 2.1.15.0-2334 - inchangé)
* HDInsight        3.2.4.610.1630216    (HDP 2.2.6.1-0012)
* Kit de développement logiciel (SDK)            1.5.8

Cette version contient hello après les mises à jour :

| Intitulé | Description | Zone concernée (par exemple, Service, composant ou Kit de développement logiciel) | Type de cluster (par exemple, Hadoop, HBase ou Storm) | JIRA (le cas échéant) |
| --- | --- | --- | --- | --- |
| Versions HDP mises à jour pour les clusters HDInsight 3.2 |Avec cette version, HDInsight 3.2 déploie HDP 2.2.6.1-0012 |de diffusion en continu |Tout |N/A |

## <a name="notes-for-06262015-release-of-hdinsight"></a>Notes relatives à la version du 26/06/2015 de HDInsight
numéros de version complet de Hello pour les clusters HDInsight déployés avec cette version :

* HDInsight     2.1.10.601.1610731    (HDP 1.3.12.0-01795 - inchangé)
* HDInsight     3.0.6.601.1610731    (HDP 2.0.13.0-2117 - inchangé)
* HDInsight     3.1.4.601.1610731    (HDP 2.1.15.0-2334 - inchangé)
* HDInsight        3.2.4.601.1610731    (HDP 2.2.6.1-0011)
* Kit de développement logiciel (SDK)            1.5.8

Cette version contient hello après les mises à jour :

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
numéros de version complet de Hello pour les clusters HDInsight déployés avec cette version :

* HDInsight     2.1.10.596.1601657    (HDP 1.3.12.0-01795 - inchangé)
* HDInsight     3.0.6.596.1601657    (HDP 2.0.13.0-2117 - inchangé)
* HDInsight     3.1.4.596.1601657    (HDP 2.1.15.0-2334)
* HDInsight        3.2.4.596.1601657    (HDP 2.2.6.1-0002)
* Kit de développement logiciel (SDK)            1.5.8

Cette version contient hello après les mises à jour :

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
<td>service de cloud computing Hello ouvre maintenant 5 too8005 8001 ports sur le cluster hello par exemple : sur https://<clustername>.azurehdinsight.net:8001/. Toothese URL sont authentifiés à l’aide de demandes hello même mécanisme de mot de passe de l’authentification de base en tant que le port 443. Ces ports liés toohello même port sur le nœud principal actif de hello. Les actions de script peuvent être utilisés toomake client services écoute sur ces ports sur un cluster de hello toooutside nœud principal et la gamme des hello.</td>
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
<td>Déplacer tooLatest Java de Azure SDK 2.2 pour HDInsight 3.2</td>
<td>Déplacer la version toolatest de hello SDK Azure pour Java utilisé par le pilote WASB hello. dernière version du SDK Hello a quelques correctifs et notes de hello hello identiques sont disponibles dans https://github.com/Azure/azure-storage-java/blob/master/ChangeLog.txt.</td>
<td>Composant principal Hadoop</td>
<td>Tout</td>
<td><a href="https://issues.apache.org/jira/browse/HADOOP-11959" target="_blank">HADOOP-11959</a></td>
</tr>
<tr>
<td>Déplacement tooHDP 2.1.15 pour les clusters HDInsight 3.1</td>
<td>Hortonworks notes de publication pour cette version de hello sont disponibles <a href="http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.15-Win/bk_releasenotes_HDP-Win/content/ch_relnotes-HDP-2.1.15.html" target="_blank">ici</a>.</td>
<td>HDP</td>
<td>Tout</td>
<td>N/A</td>
</tr>
</table>

## <a name="notes-for-06042015-release-of-hdinsight"></a>Notes relatives à la publication du 04/06/2015 de HDInsight
numéros de version complet de Hello pour les clusters HDInsight déployés avec cette version :

* HDInsight     2.1.10.583.1575584    (HDP 1.3.12.0-01795 - inchangé)
* HDInsight     3.0.6.583.1575584    (HDP 2.0.13.0-2117 - inchangé)
* HDInsight     3.1.3.583.1575584    (HDP 2.1.12.1-0003 - inchangé)
* HDInsight        3.2.4.583.1575584    (HDP 2.2.6.1-1)
* Kit de développement logiciel (SDK)            1.5.8

Cette version contient hello après les mises à jour :

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
<td>Cette version corrige un bogue affectant les API de soumission de travail hello qui a provoqué hello du site Web toobe vers le bas après un redémarrage.</td>
<td>Service</td>
<td>Storm</td>
<td>N/A</td>
</tr>
</table>

## <a name="notes-for-06012015-release-of-hdinsight"></a>Notes relatives à la version du 01/06/2015 de HDInsight
numéros de version complet de Hello pour les clusters HDInsight déployés avec cette version :

* HDInsight     2.1.10.577.1563827    (HDP 1.3.12.0-01795 - inchangé)
* HDInsight     3.0.6.577.1563827    (HDP 2.0.13.0-2117 - inchangé)
* HDInsight     3.1.3.577.1563827    (HDP 2.1.12.1-0003 - inchangé)
* HDInsight        3.2.4.577.1563827    (HDP 2.2.6.0-2800 - inchangé)
* Kit de développement logiciel (SDK)            1.5.8

Cette version contient hello après les mises à jour :

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
<td>Cette version résout les bogues liés toocluster de configuration.</td>
<td>Service</td>
<td>Tous les types de cluster</td>
<td>N/A</td>
</tr>
</table>

## <a name="notes-for-05272015-release-of-hdinsight"></a>Notes relatives à la version du 27/05/2015 de HDInsight
numéros de version complet de Hello pour les clusters HDInsight déployés avec cette version :

* HDInsight        3.2.4.570.1554102    (HDP 2.2.6.0-2800)
* Les autres versions de cluster et de Kit de développement logiciel (SDK) ne sont pas déployés dans le cadre de cette version.

Cette version contient hello après les mises à jour :

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
<td>Cette version de HDInsight 3.2 contient HDP 2.2.6 et apporte plusieurs résolutions de bogues importantes tooHDInsight. Hello complet notes de publication sont disponibles sur <a href="http://dev.hortonworks.com.s3.amazonaws.com/HDPDocuments/HDP2/HDP-2.2.6/HDP_RelNotes_v226/index.html">HDP 2.2.6 Release Notes</a>.</td>
<td>HDP</td>
<td>Tous les types de cluster</td>
<td>N/A</td>
</tr>
<tr>
<td>Modification tooDefault fils conteneur mémoire Configuration</td>
<td>Dans cette mise à jour, les conteneurs de tooYARN de mémoire disponible hello par défaut (yarn.nodemanager.resource.memory Mo et allocation yarn.scheduler.maximum-Mo), lancée par le Gestionnaire de nœud, est too5632MB accrue. Cela était too4608MB réduite, mais selon différentes s’exécute, nouvelle valeur de hello doit offrir une meilleure fiabilité et les performances des travaux de toomost, n’est donc une meilleure valeur par défaut. Comme d’habitude, si vous avez une dépendance critique sur cette configuration de la mémoire, définissez la propriété explicitement lors de la création du cluster de hello.</td>
<td>HDP</td>
<td>Tous les types de cluster</td>
<td>N/A</td>
</tr>
<tr>
<td>Parité de configuration par défaut pour les clusters HBase et Storm</td>
<td>Cette mise à jour restaure Hbase et Storm clusters toouse hello les mêmes valeurs fils configuration en tant que clusters Hadoop. Tous les types de cluster sont ainsi égaux.</td>
<td>HDP</td>
<td>Hbase, Storm</td>
<td>N/A</td>
</tr>
</table>

## <a name="notes-for-05202015-release-of-hdinsight"></a>Notes relatives à la version du 20/05/2015 de HDInsight
numéros de version complet de Hello pour les clusters HDInsight déployés avec cette version :

* HDInsight     2.1.10.564.1542093    (HDP 1.3.12.0-01795 - inchangé)
* HDInsight     3.0.6.564.1542093    (HDP 2.0.13.0-2117 - inchangé)
* HDInsight     3.1.3.564.1542093    (HDP 2.1.12.1-0003)
* HDInsight        3.2.4.564.1542093    (HDP 2.2.4.6-2)
* Kit de développement logiciel (SDK)            1.5.8

Cette version contient hello après les mises à jour :

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
<td>packages de cluster Hello mis à jour pour HDInsight Storm amener nouvelle tooSCP.NET de fonctionnalités. Vous avez maintenant accès toonew API dans le Générateur de topologie qui le rendent plus facile toouse EventHubSpout ou Java becs verseurs amovibles. Vous devez mettre à jour votre toowork de kit de développement logiciel client SCP.NET avec nouveaux clusters comme hello contrats ont été mis à jour. Pour plus d’informations sur hello nouvelles API, utilisation et la publication de notes (y compris les correctifs de bogues) font référence toohello fichier Readme inclus dans le package NuGet de SCP.NET de hello.</td>
<td>Outils VS</td>
<td>Clusters HDInsight 3.2 Storm</td>
<td>N/A</td>
</tr>
<tr>
<td>Mise à jour du pilote JDBC</td>
<td>Version prise en charge dans sqljdbc_4.1.5605.100 de toohello de pilote hello mis à jour SQL Server.</td>
<td>Metastore</td>
<td>Tout</td>
<td>N/A</td>
</tr>
</table>

## <a name="notes-for-04272015-release-of-hdinsight"></a>Notes relatives à la version du 27/04/2015 de HDInsight
numéros de version complet de Hello pour les clusters HDInsight déployés avec cette version :

* HDInsight     2.1.10.537.1486660    (HDP 1.3.12.0-01795 - inchangé)
* HDInsight     3.0.6.537.1486660    (HDP 2.0.13.0-2117 - inchangé)
* HDInsight     3.1.3.537.1486660    (HDP 2.1.12.0-2329 - inchangé)
* HDInsight        3.2.3.537.1486660    (HDP 2.2.2.2-4)
* Kit de développement logiciel (SDK)            1.5.8

Cette version contient hello après les mises à jour :

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
<td>Un cluster de créer une demande maintenant attend PUT demande toobe accepté avant d’interrogation sur l’état de hello</td>
<td>Foundation</td>
<td>Hadoop</td>
<td>N/A</td>
</tr>
</table>

## <a name="notes-for-04142015-release-of-hdinsight"></a>Notes relatives à la version du 14/04/2015 de HDInsight
numéros de version complet de Hello pour les clusters HDInsight déployés avec cette version :

* HDInsight     2.1.10.521.1453250    (HDP 1.3.12.0-01795 - inchangé)
* HDInsight     3.0.6.521.1453250    (HDP 2.0.13.0-2117 - inchangé)
* HDInsight     3.1.3.521.1453250    (HDP 2.1.12.0-2329 - inchangé)
* HDInsight        3.2.3.525.1459730    (HDP 2.2.2.2-2)
* Kit de développement logiciel (SDK)            1.5.6

Cette version contient hello après les mises à jour :

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
<td>Des correctifs pour Apache TEZ 2214 et TEZ 1923 sont inclus dans cette version de HDI 3.2. Celles-ci sont nécessaires pour certaines requêtes Hive sur Tez nécessitant tooshuffle une quantité importante de données.
</td>
<td>HDP</td>
<td>Hadoop</td>
<td><a href="https://issues.apache.org/jira/browse/TEZ-2214">TEZ 2214</a></br><a href="https://issues.apache.org/jira/browse/TEZ-1923">TEZ 1923</a></td>
</tr>
</table>

## <a name="notes-for-04062015-release-of-hdinsight"></a>Notes relatives à la version du 06/04/2015 de HDInsight
numéros de version complet de Hello pour les clusters HDInsight déployés avec cette version :

* HDInsight     2.1.10.521.1453250    (HDP 1.3.12.0-01795 - inchangé)
* HDInsight     3.0.6.521.1453250    (HDP 2.0.13.0-2117 - inchangé)
* HDInsight     3.1.3.521.1453250    (HDP 2.1.12.0-2329 - inchangé)
* HDInsight        3.2.3.521.1453250    (HDP 2.2.2.2-1)
* Kit de développement logiciel (SDK)            1.5.6

Cette version contient hello après les mises à jour :

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
<td>Met à jour tooremove certaines classes internes pour HDInsight sur Linux.</td>
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
<td>Service de toohello divers correctifs de bogues</td>
<td>Service</td>
<td>Tout</td>
<td>N/A</td>
</tr>
</table>

## <a name="notes-for-04012015-release-of-hdinsight"></a>Notes relatives à la version du 01/04/2015 de HDInsight
numéros de version complet de Hello pour les clusters HDInsight déployés avec cette version :

* HDInsight     2.1.10.513.1431705    (HDP 1.3.12.0-01795)
* HDInsight     3.0.6.513.1431705    (HDP 2.0.13.0-2117)
* HDInsight     3.1.3.513.1431705    (HDP 2.1.12.0-2329)
* HDInsight        3.2.3.513.1431705    (HDP 2.2.2.1-2600)
* Kit de développement logiciel (SDK)            1.5.5

Cette version contient hello après les mises à jour :

<table border="1">
<tr>
<th>Intitulé</th>
<th>Description</th>
<th>Zone concernée (par exemple, Service, composant ou Kit de développement logiciel)</p></th>
<th>Type de cluster (par exemple, Hadoop, HBase ou Storm)</th>
<th>JIRA (le cas échéant)</th>
</tr>
<tr>
<td>Capacité tooenable/désactiver bureau informations d’identification distantes sur des clusters Windows via le Kit de développement .NET</td>
<td>Assistance par programme pour activer ou désactiver les informations d’identification RDP sur des clusters Windows.</td>
<td>Foundation</td>
<td>Tout</td>
<td>N/A</td>
</tr>
<tr>
<td>Capacité tooenable bureau informations d’identification distantes sur des clusters, ils sont en cours d’approvisionnement</td>
<td>Prise en charge par programme pour activer les informations d’identification du Bureau à distance lors de la création de cluster de hello. Cela supprime le processus en deux étapes de hello pour premier cluster hello approvisionnement et puis l’activation du Bureau à distance.</td>
<td>Foundation</td>
<td>Tout</td>
<td>N/A</td>
</tr>
<tr>
<td>Mise à niveau Python too2.7.8</td>
<td>Correctifs de Python mis à niveau sur les Clusters HDInsight tooPython point 2.7.8, qui contient une sécurité importante pour HDInsight versions 2.1, 3.0, 3.1 et 3.2</td>
<td>Service</td>
<td>Tout</td>
<td>N/A</td>
</tr>
<tr>
<td>Modification de la configuration YARN</td>
<td>Modifié fils configuration applications terminée yarn.resourcemanager.max too1000 pour tous les types de cluster pour les versions de HDInsight 3.1 et 3.2. Cette valeur contrôle uniquement la liste hello des applications terminées Bonjour fils UI. tooget plus d’informations sur les applications qui ont été soumises préalable toohello la liste des applications indiquées sur hello l’interface utilisateur, vous pouvez accéder directement toohello Server de l’historique.</td>
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
<td>Pilote SQL JDBC est sqljdbc_4.0.2206.100 tooversion mis à niveau pour HDInsight version 3.2. Cette version contient des améliorations de sécurité importantes.</td>
<td>HDP</td>
<td>Tout</td>
<td>N/A</td>
</tr>
<tr>
<td>Mise à jour de la configuration JVM</td>
<td>Mise à jour JVM configuration networkaddress.cache.ttl too300 secondes à partir de la valeur par défaut -1 hello pour HDInsight versions 3.1 et 3.2. Cette valeur contrôle hello mise en cache de stratégie pour les recherches de réussie. nom du service de nom hello. Cela permet de corriger un bogue lié toogrowing et réduction des clusters HBase.</td>
<td>Service</td>
<td>hbase</td>
<td>N/A</td>
</tr>
<tr>
<td>Mise à niveau tooAzure stockage SDK pour Java 2.0</td>
<td>HDInsight version 3.2 est mis à niveau toouse hello dernière version de hello SDK de stockage Azure pour Java. Contient plusieurs résolutions de bogues importantes sur la version de hello 0.6.0 actuel.</td>
<td>HDP</td>
<td>Tout</td>
<td>N/A</td>
</tr>
<tr>
<td>Code de mise à niveau tooApache WASB source</td>
<td>HDInsight version 3.2 maintenant utilise hello dernier code de pilote de système de fichiers WASB hello Apache Hadoop. Avec cette modification, hello WASB pilote d’est désormais inclus en tant que fichier jar distinct. Cela est uniquement un changement d’emballage et ne contient-elle pas de n’importe quel toobehavior modifications du pilote WASB hello. nom de Hello de ce fichier JAR est hadoop-azure-2.6.0.jar.</td>
<td>HDP</td>
<td>Tout</td>
<td>N/A</td>
</tr>
<tr>
<td>Mises à jour du nom de fichier jar dans HDInsight 3.2</td>
<td>Cette mise à jour tooHDInsight version 3.2 contient plusieurs résolutions de bogue et quelques fichiers JAR interne empaqueté en tant que partie de HDP ont été mis à niveau. Ces packages HDP JAR fichiers toohello interne et non en direct par les applications client. Les applications doivent package leur propre version des fichiers JAR hello afin qu’une mise à niveau toohello HDP interne fichiers JAR n’arrêtent pas les applications clientes.</td>
<td>HDP</td>
<td>Tout</td>
<td>N/A</td>
</tr>
</table>

## <a name="notes-for-03032015-release-of-hdinsight"></a>Notes relatives à la version du 03/03/2015 de HDInsight
numéros de version complet de Hello pour les clusters HDInsight déployés avec cette version :

* HDInsight     2.1.10.488.1375841    (HDP 1.3.9.0-01351 - inchangé)
* HDInsight     3.0.6.488.1375841    (HDP 2.0.9.0-2097 - inchangé)
* HDInsight     3.1.3.488.1375841    (HDP 2.1.10.0-2290 - inchangé)
* HDInsight        3.2.3.488.1375841    (HDP-2.2.10.0-2340 - inchangé)
* Kit de développement logiciel (SDK)            1.5.0                (inchangé)

Cette version contient hello mise à jour suivante :

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
<td>Nous avons apporté des correctifs qui permettent de hello service tooscale mieux avec une charge accrue avec respect toocluster création hello.</td>
<td>Service</td>
<td>Tout</td>
<td>N/A</td>
</tr>
</table>

## <a name="notes-for-02182015-release-of-hdinsight"></a>Notes relatives à la version du 18/02/2015 de HDInsight
numéros de version complet de Hello pour les clusters HDInsight déployés avec cette version :

* HDInsight     2.1.10.471.1342507    (HDP 1.3.9.0-01351 - inchangé)
* HDInsight     3.0.6.471.1342507    (HDP 2.0.9.0-2097 - inchangé)
* HDInsight     3.1.3.471.1342507    (HDP 2.1.10.0-2290 - inchangé)
* HDInsight        3.2.3.471.1342507    (HDP-2.2.10.0-2340)
* Kit de développement logiciel (SDK)            1.5.0

Cette version contient hello après les mises à jour :

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
<td>Hadoop 2.6/HDP2.2 est disponible avec les clusters HDInsight 3.2. Il contient tooall mises à jour importantes des composants d’open source hello. Pour plus d’informations, consultez Nouveautés dans HDInsight et <a href ="http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.2.0/HDP_2.2.0_Release_Notes_20141202_version/index.html" target="_blank">Notes de version HDP 2.2.0.0</a>.</td>
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
<td>Azure HDInsight est disponible sur plusieurs tailles et types de machine virtuelle. HDInsight peut utiliser les tailles de tooA7 A2 générés à des fins générales ; Nœuds de série D qui caractérisent les disques SSD (SSD) et 60 pour cent des processeurs plus rapides. et tailles A8 et A9 ayant InfiniBand prend en charge pour la mise en réseau rapide.</td>
<td>Service</td>
<td>Tout</td>
<td>N/A</td>
</tr>
<tr>
<td>Mise à l’échelle du cluster</td>
<td>Vous pouvez modifier le nombre hello de nœuds de données pour un cluster HDInsight en cours d’exécution sans avoir toodelete ou créer de nouveau. Actuellement, seuls les types de cluster Hadoop requête et Apache Storm ont cette possibilité, mais prend en charge pour le type de cluster Apache HBase est bientôt toofollow. Pour plus d’informations, consultez la rubrique Gérer les clusters HDInsight.</td>
<td>de diffusion en continu</td>
<td>Hadoop, Storm</td>
<td>N/A</td>
</tr>
<tr>
<td>Outils Visual Studio</td>
<td>En outre toocomplete pour les outils d’Apache Storm, hello pour les outils pour Apache Hive dans Visual Studio a été mis à jour tooinclude saisie semi-automatique des instructions, la validation locale et prise en charge du débogage améliorée. Pour plus d’informations, consultez la page Prise en main de HDInsight Hadoop Tools pour Visual Studio.</td>
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
numéros de version complet de Hello pour les clusters HDInsight déployés avec cette version :

* HDInsight     2.1.10.463.1325367    (HDP 1.3.9.0-01351 - inchangé)
* HDInsight     3.0.6.463.1325367    (HDP 2.0.9.0-2097 - inchangé)
* HDInsight     3.1.2.463.1325367    (HDP 2.1.10.0-2290)
* Kit de développement logiciel (SDK)            N/A

Cette version contient hello après les mises à jour :

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
<td>HDInsight 3.1 est mis à jour toodeploy HDP 2.1.10.0. Pour plus d’informations, consultez les <a href ="http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.10/bk_releasenotes_hdp_2.1/content/ch_relnotes-HDP-2.1.10.html" target="_blank">Notes de publication de HDP-2.1.10</a>. </td>
<td>Logiciels open source</td>
<td>Tout</td>
<td>N/A</td>
</tr>
<tr>
<td>Mises à jour binaires HDP</td>
<td>Les noms de quelques fichiers jar dans HBase ont été mis à jour. Ces fichiers JAR sont utilisés en interne par HBase, afin que les clients ont une dépendance sur les noms de ces fichiers JAR hello n’est pas attendu. Vous avez notamment vu les points suivants :
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
numéros de version complet de Hello pour les clusters HDInsight déployés avec cette version :

* HDInsight     2.1.10.455.1309616    (HDP 1.3.9.0-01351 - inchangé)
* HDInsight     3.0.6.455.1309616    (HDP 2.0.9.0-2097 - inchangé)
* HDInsight     3.1.2.455.1309616    (HDP 2.1.9.0-2196 - inchangé)
* Kit de développement logiciel (SDK)            N/A

Cette version contient hello mise à jour suivante :

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
<td>Nous avons apporté quelques résolutions de bogues importantes qui améliorent la fiabilité hello Hello Clusters HDInsight pendant les mises à niveau Azure.</td>
<td>Service</td>
<td>Tout</td>
<td>N/A</td>
</tr>
</table>

## <a name="notes-for-152015-release-of-hdinsight"></a>Notes relatives à la version du 05/01/2015 de HDInsight
numéros de version complet de Hello pour les clusters HDInsight déployés avec cette version :

* HDInsight     2.1.10.420.1246118    (HDP 1.3.9.0-01351 - inchangé)
* HDInsight     3.0.6.420.1246118    (HDP 2.0.9.0-2097 - inchangé)
* HDInsight     3.1.2.420.1246118    (HDP 2.1.9.0-2196 - inchangé)

Cette version contient hello après les mises à jour :

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
<td><p>Dans cette version, hello console de requête de HDInsight a deux exemples supplémentaires :</p>

<p><b>Analyse de tendances Twitter</b><br>
Les API publiques fournies par des sites comme Twitter représentent une source de données utile pour l'analyse et la compréhension des tendances populaires. Dans ce didacticiel, découvrez comment toouse Hive tooget une liste d’utilisateurs Twitter envoyé hello la plupart des tweets contenant un mot particulier. </p>

<p><b>Recommandation de films Mahout</b><br>
Apache Mahout est une bibliothèque d'apprentissage machine Apache Hadoop. Mahout contient des algorithmes pour le traitement des données (tel que le filtrage, la classification et le clustering). Dans ce didacticiel, utilisez une recommandation moteur toogenerate film basées sur les films vos amis se sont affiché.</p></td>
<td>Console de requête</td>
<td>Hadoop</td>
<td>N/A</td>
</tr>
<tr>
<td>Modifier la valeur toodefault pour la configuration de la ruche : hive.auto.convert.join.noconditionaltask.size</td>
<td><p>Cette configuration de la taille s’applique tooautomatically converti carte jointures. valeur de Hello représente la somme hello des tailles de hello des tables qui peuvent être des cartes toohash converti qui tiennent dans la mémoire. Dans une version antérieure, cette valeur est augmentée de valeur par défaut hello 10 Mo too128 Mo. Toutefois, hello nouvelle valeur de 128 Mo provoquait travaux toofail toolack en raison de la mémoire. Cette version rétablit la valeur par défaut de hello sauvegarder too10 Mo. Les clients peuvent toujours choisir toooverride cette valeur lors de la création du cluster en fonction de leurs requêtes et les tailles de tables. Pour plus d’informations sur ce paramètre et comment toooverride, consultez <a href="http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.0.0.2/ds_Hive/optimize-joins.html#JoinOptimization-OptimizeAutoJoinConversion" target="_blank">optimiser la Conversion de joindre automatiquement</a> dans la documentation de Hortonworks. </p></td>
<td>Hive</td>
<td>Hadoop, Hbase</td>
<td>N/A</td>
</tr>
</table>

## <a name="notes-for-12232014-release-of-hdinsight"></a>Notes relatives à la version du 23/12/2014 de HDInsight
numéros de version complète Hello pour les clusters HDInsight déployés avec cette version sont :

* HDInsight     2.1.10.420.1246783    (version de HDP inchangée)
* HDInsight     3.0.6.420.1246783    (version de HDP inchangée)
* HDInsight     3.1.1.420.1246783    (version de HDP inchangée)

Cette version contient hello mise à jour suivante :

<table border="1">
<tr>
<th>Intitulé</th>
<th>Description</th>
<th>Composant</th>
<th>Type du cluster</th>
<th>JIRA (le cas échéant)</th>
</tr>
<tr>
<td>Échec de la création de cluster intermittents en raison de la charge de tooexcessive</td>
<td><p>Algorithme amélioré pour télécharger les packages HDP lors de la création du cluster permet une gestion plus fiable d’échecs en raison de la charge de tooexcessive.</p></td>
<td>Service</td>
<td>Hadoop, Hbase, Storm</td>
<td>N/A</td>
</tr>
</table>

## <a name="notes-for-12182014-release-of-hdinsight"></a>Notes relatives à la version du 18/12/2014 de HDInsight
Cette version contient hello après mise à jour de composant :

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
<td><p>Personnalisation permet hello vous toocustomize votre Azure HDInsight clusters avec les projets qui sont disponibles à partir de l’écosystème d’Apache Hadoop hello. Avec cette nouvelle fonctionnalité, vous pouvez tester et déployer des tooAzure de projets Hadoop HDInsight. Cette option est activée via hello **Action de Script** fonctionnalité, qui peut modifier les clusters Hadoop de manière arbitraire à l’aide de scripts personnalisés. Cette personnalisation est disponible sur tous les types de clusters HDInsight, dont Hadoop, HBase et Storm. puissance de hello toodemonstrate de cette fonctionnalité, que nous avons documentées hello de tooinstall hello processus populaires <a href = "hdinsight-hadoop-spark-install.md" target="_blank">Spark</a>, <a href = "hdinsight-hadoop-r-scripts.md" target="_blank">R</a>, <a href = "hdinsight-hadoop-solr-install.md" target="_blank">Solr</a>, et <a href = "hdinsight-hadoop-giraph-install.md" target="_blank">Giraph</a> modules. Cette version ajoute la fonctionnalité de hello pour les clients toospecify leur action de script personnalisé via hello portail Azure, fournit également indications et meilleures pratiques sur comment toobuild personnalisées actions à l’aide des méthodes d’assistance de script et fournit des instructions sur la façon tootest action de script Hello. </p></td>
<td>Disponibilité générale des fonctionnalités</td>
<td>Tout</td>
<td>N/A</td>
</tr>
</table>

## <a name="notes-for-12052014-release-of-hdinsight"></a>Notes relatives à la version du 05/12/2014 de HDInsight
numéros de version complète Hello pour les clusters HDInsight déployés avec cette version sont :

* HDInsight     2.1.9.406.1221105    (HDP 1.3.9.0-01351)
* HDInsight     3.0.5.406.1221105    (HDP 2.0.9.0-2097)
* HDInsight     3.1.1.406.1221105    (HDP 2.1.9.0-2196)
* Kit de développement logiciel (SDK) HDInsight N/A

Cette version contient hello après les mises à jour de composant :

<table border="1">
<tr>
<th>Intitulé</th>
<th>Description</th>
<th>Composant</th>
<th>Type du cluster</th>
<th>JIRA (le cas échéant)</th>
</tr>
<tr>
<td>Correctif de bogue : une erreur intermittente lors de l’ajout de grands nombres de la table tooa de partitions dans un DDL Hive </td>
<td><p>S’il existe une erreur de connexion intermittents avec la base de données du magasin de métadonnées hello ruche lors de l’ajout d’un grand nombre de la table de partitions tooa Hive, hello DDL de la ruche peut échouer. Hello suivant isseen instruction dans le journal des erreurs hello ruche si cette erreur se produit : </p><p>"ERROR [main]: ql.Driver (SessionState.java:printError(547)) - FAILED: Execution Error, return code 1 from org.apache.hadoop.hive.ql.exec.DDLTask. MetaException(message:java.lang.RuntimeException: commitTransaction was called but openTransactionCalls = 0. Cela indique probablement qu’il n’y a des appels déséquilibrée tooopenTransaction/commitTransaction) »</p></td>
<td>Hive</td>
<td>Hadoop, Hbase</td>
<td>HIVE-482 (système JIRA interne ne pouvant pas faire l'objet d'une citation externe. Indiqué ici pour référence.)</td>
</tr>
<tr>
<td>Correctif de bogue : blocage occasionnel Bonjour Console de requête HDInsight</td>
<td>Dans ce cas, hello instruction suivante peut être consultée dans hello WebHCat journal pour le travail de lanceur hello WebHCat : <p>« org.apache.hive.hcatalog.templeton.CatchallExceptionMapper | org.apache.hadoop.ipc.RemoteException(org.apache.hadoop.yarn.exceptions.YarnRuntimeException) : pas pu charger le fichier de l’historique {fichier d’historique wasb url toohello} »</p></td>
<td>WebHCat,</td>
<td>Hadoop</td>
<td>HIVE-482 (système JIRA interne ne pouvant pas faire l'objet d'une citation externe. Indiqué ici pour référence.)</td>
</tr>
<tr>
<td>Correctif de bogue : pic occasionnel dans la latence des requêtes Hbase</td>
<td>Si cela se produit, les utilisateurs remarquerez un pic occasionnels de 3 secondes une latence des requêtes de Hbase hello. </td>
<td>Passerelle de cluster HDInsight</td>
<td>HBase</td>
<td>N/A</td>
</tr>
<tr>
<td>Changement du nom du fichier jar HDP</td>
<td>Pour HDI de cluster version 3.0, il existe deux fichiers JAR internes toohello modifications installé par HDP. jetty-6.1.26.jar a été remplacé par jetty-6.1.26.hwx.jar. jetty-util-6.1.26.jar a été remplacé par jetty-util-6.1.26.hwx.jar. Ces modifications s’appliquent les projets tooHadoop, Mahout, WebHCat et Oozie.</td>
<td>Hadoop, Mahout, WebHCat, Oozie</td>
<td>Hadoop, HBase</td>
<td>N/A</td>
</tr>
</table>

## <a name="notes-for-11212014-release-of-hdinsight"></a>Notes relatives à la version du 21/11/2014 de HDInsight
numéros de version complète Hello pour les clusters HDInsight déployés avec cette version sont :

* HDInsight 2.1.9.382.1169709 (pas de changements par rapport à la version du 14/11/2014)
* HDInsight 3.0.5.382.1169709 (pas de changements par rapport à la version du 14/11/2014)
* HDInsight 3.1.1.382.1169709 (pas de changements par rapport à la version du 14/11/2014)
* Kit de développement logiciel (SDK) HDInsight 1.4.0

Cette version contient hello après les mises à jour de composant :

<table border="1">
<tr><th>Intitulé</th><th>Description</th><th>Composant</th><th>Type du cluster</th><th>JIRA (le cas échéant)</th></tr>
<tr>
<td>Accès aux journaux des applications</td>
<td>Capacité tooprogrammatically énumérer les applications qui ont été exécutées sur des clusters et toodownload les journaux spécifiques à l’application ou spécifiques des conteneurs appropriés toohelp débogage problématique.</td>
<td>Foundation</td>
<td>Hadoop</td>
<td>N/A</td>
</tr>
<tr>
<td>Nom de la région capacité toospecify dans IHdInsightClient.DeleteCluster </td>
<td>Bonjour Azure HDInsight SDK fournit hello capacité toospecify un nom de région lors de l’utilisation **DeleteCluster**. Cela permet de débloquer les clients qui contenait des deux ressources portant le même nom dans des régions différentes et qui avaient été toodelete Impossible d’un d’eux.</td>
<td>Foundation</td>
<td>Tout</td>
<td>N/A</td>
</tr>
<tr>
<td>ClusterDetails.DeploymentId</td>
<td>Hello **ClusterDetails** objet retourne un **DeploymentID** champ qui représente un identificateur unique pour le cluster de hello. Il est garanti toobe unique pour la création du cluster tente par hello même noms.</td>
<td>Foundation</td>
<td>Tout</td>
<td>N/A</td>
</tr>
</table>

## <a name="notes-for-11142014-release-of-hdinsight"></a>Notes relatives à la version du 11/14/2014 de HDInsight

numéros de version complète Hello pour les clusters HDInsight déployés avec cette version sont :

* HDInsight 2.1.9.382.1169709
* HDInsight 3.0.5.382.1169709
* HDInsight 3.1.1.382.1169709

Cette version contient hello suivant des nouvelles fonctionnalités, des mises à jour des composants et des correctifs de bogues.

<table border="1">
<tr><th>Intitulé</th><th>Description</th><th>Composant</th><th>Type du cluster</th><th>JIRA (le cas échéant)</th></tr>
<tr>
<td>Action de script (version préliminaire)</td>
<td>Aperçu de la fonctionnalité de personnalisation de cluster hello qui permet la modification d’Hadoop des clusters de manière arbitraire à l’aide de scripts personnalisés. Avec cette fonctionnalité, les utilisateurs peuvent faire des essais avec et déployer des projets qui sont disponibles à partir de hello Apache Hadoop écosystème tooAzure que des clusters HDInsight. Elle est disponible sur tous les types de clusters HDInsight, dont Hadoop, HBase et Storm.</td>
<td>Nouvelle fonctionnalité</td>
<td>Tout</td>
<td>N/A</td>
</tr>
<tr>
<td>Tâches préconfigurées pour l’analyse des journaux Sites Web Azure et Azure Storage</td>
<td>Hello Console de requête HDInsight comprend une galerie de prise en main qui prend en charge des solutions qui fonctionnent sur vos données ou sur les exemples de données.
<p>**Solutions opérationnelles sur vos données** :<br>
Nous avons créé des travaux pour certaines des hello courants données analyse scénarios tooprovide un point de départ pour créer vos propres solutions. Vous pouvez utiliser vos données avec toosee de travail hello son fonctionnement. Lorsque vous êtes prêt, utilisez ensuite ce que vous avez appris toocreate une solution qui est modélisée d’après le travail de prégénérées hello.</p>
<p>**Solutions opérationnelles sur les exemples de données** :<br>
Découvrez comment toowork avec HDInsight en parcourant des scénarios de base (par exemple, l’analyse des journaux web et les données de capteur). Vous apprendrez comment tooanalyze de HDInsight de toouse ces données et comment vous pouvez connecter d’autres données toothis applications et services. Visualisation des données en vous connectant tooMicrosoft Excel fournit un exemple d’alimentation hello de cette approche.</p></td>
<td>Console de requête</td>
<td>Hadoop</td>
<td>N/A</td>
</tr>
<tr>
<td>Résolution du problème de fuite de mémoire dans Templeton</td>
<td>Une fuite de mémoire dans Templeton a été corrigée. Ce problème concernait les clients qui possédaient un cluster de longue durée ou qui envoyaient des centaines de demandes de tâches à la seconde. Hello problème identifié comme tel Templeton 5xx erreurs et de la solution de contournement hello toorestart hello service was. solution de contournement Hello n’est plus nécessaire.</td>
<td>Templeton</td>
<td>Tout</td>
<td>https://issues.apache.org/jira/browse/HADOOP-11248</td>
</tr>
</table>

> [!NOTE]
> nouvelles fonctionnalités toodemonstrate hello mises à disposition par personnalisation du cluster, les procédures de hello à l’aide de Script Action tooinstall Spark et des modules R sur un cluster ont été documentées. Pour plus d'informations, consultez les pages suivantes :

* [Installation et utilisation de Spark 1.0 sur des clusters HDInsight](hdinsight-hadoop-spark-install.md)
* [Installation et utilisation de R sur des clusters HDInsight Hadoop](hdinsight-hadoop-r-scripts.md)

## <a name="notes-for-11072014-release-of-hdinsight"></a>Notes relatives à la version du 07/11/2014 de HDInsight

numéros de version complète Hello pour les clusters HDInsight déploiement avec cette version sont :

* HDInsight 2.1    2.1.9.374.1153876
* HDInsight 3.0    3.0.5.374.1153876
* HDInsight 3.1    3.1.1.374.1153876

Cette version contient hello après les mises à jour de composant :

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
<td>Hello fils chronologie Server (également appelé serveur de l’historique d’Application générique hello) a été activée par défaut. Hello chronologie Server fournit des informations génériques sur des applications terminées (par exemple, l’ID d’application, nom de l’application, état de l’application, heure de soumission d’application et heure de fin d’application).

Informations de cette application peuvent récupérer à partir du nœud principal hello en accédant à hello URI http://headnodehost:8188 ou en exécutant la commande hello fils : fils application - liste - appStates tous.

soit à distance via l’API REST à l’adresse https://{ClusterDnsName}. azurehdinsight.net/ws/v1/applicationhistory/.

Pour plus d’informations, consultez <a href="http://hadoop.apache.org/docs/r2.4.0/hadoop-yarn/hadoop-yarn-site/TimelineServer.html" target="_blank">YARN Timeline Server</a>.</td>
<td>Service, YARN</td>
<td>Hadoop, HBase</td>
<td>N/A</td>
</tr>
<tr>
<td>ID de déploiement de cluster</td>
<td>Depuis la version du Kit de développement logiciel (SDK) 1.3.3.1.5426.29232, les utilisateurs peuvent accéder à un identificateur unique émis par HDInsight pour chaque cluster. Cette toofigure de clients permet des instances uniques de clusters lorsqu’un nom DNS est réutilisé entre créer ou supprimer des scénarios.</td>
<td>Foundation</td>
<td>Tout</td>
<td>N/A</td>
</tr>
</table>

> [!NOTE]
> bogue Hello qui a empêché de numéro de version complet hello d’apparaître dans le portail de hello ou d’être retourné par hello SDK ou par Windows PowerShell a été résolu dans cette version.

## <a name="notes-for-10152014-release"></a>Notes pour la version du 15/10/2014

Cette version du correctif logiciel fixe une fuite de mémoire dans Templeton affectées utilisateurs hello de Templeton. Dans certains cas, les utilisateurs qui testés Templeton fortement seraient Voir erreurs représentées par les codes d’erreur 500 parce que les demandes hello n’aurait pas suffisamment toorun de mémoire. solution de contournement Hello pour résoudre ce problème a été service de Templeton toorestart hello. Ce problème est à présent résolu.

## <a name="notes-for-1072014-release"></a>Notes pour la version du 07/10/2014

* Lors de l’utilisation de Ambari point de terminaison, « https://{clusterDns}.azurehdinsight.net/ambari/api/v1/clusters/{clusterDns}.azurehdinsight.net/services/{servicename}/components/{componentname} », hello *host_name* champ retourne Hello nom de domaine complet (FQDN) du nœud hello au lieu du nom d’hôte uniquement hello. Par exemple, au lieu de retourner «**headnode0**«, vous obtenez hello nom de domaine complet »**headnode0. {} ClusterDNS} .azurehdinsight .net**». Cette modification a été requis toofacilitate les scénarios où plusieurs types de cluster (par exemple, HBase et Hadoop) peuvent être déployées dans un réseau virtuel. Cela se produit, par exemple, lors de l'utilisation de HBase en tant que plateforme principale pour Hadoop.

* Nous avons fourni des nouveaux paramètres de mémoire pour le déploiement par défaut de hello du cluster HDInsight de hello. Précédents paramètres de mémoire par défaut ne pas suffisamment compte pour obtenir des conseils de hello pour nombre hello de cœurs de processeur en cours de déploiement. Ces nouveaux paramètres de mémoire doivent normalement fournir de meilleures valeurs par défaut, conformément aux recommandations de Hortonworks. toochange, consultez la documentation de référence de kit de développement logiciel toohello sur la modification de configuration du cluster. Hello nouveaux paramètres de mémoire qui sont utilisées par le cluster HDInsight core (conteneur de 8) hello par défaut 4 UC sont détaillés dans hello tableau suivant. (hello valeurs utilisées toothis préalable version sont également fournis cités entre parenthèses ci-dessus.)

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

Pour plus d’informations sur les paramètres de configuration de mémoire hello utilisé par des fils et MapReduce sur hello Hortonworks Data Platform qui est utilisé par HDInsight, consultez [déterminer les paramètres de Configuration de la mémoire de HDP](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1-latest/bk_installing_manually_book/content/rpm-chap1-11.html). Hortonworks également un outil de paramètres de toocalculate appropriée de la mémoire.

En ce qui concerne hello Azure PowerShell et hello message d’erreur HDInsight SDK : «*Cluster n’est pas configuré pour l’accès des services HTTP*» :

* Cette erreur est connu [problème de compatibilité](https://social.msdn.microsoft.com/Forums/azure/a7de016d-8de1-4385-b89e-d2e7a1a9d927/hdinsight-powershellsdk-error-cluster-is-not-configured-for-http-services-access?forum=hdinsight) qui peuvent se produire en raison de la différence de tooa dans la version de hello Hello HDInsight SDK ou Azure PowerShell et hello du cluster de hello. Les clusters créés le 15/08 ou ultérieurement prennent en charge la nouvelle capacité d’approvisionnement dans les réseaux virtuels. Mais cette fonctionnalité n’est pas correctement interprétée par les versions antérieures de hello HDInsight SDK ou Azure PowerShell. résultat de Hello est un échec de certaines opérations d’envoi de travail. Si vous utilisez les applets de commande API du Kit de développement logiciel HDInsight ou Azure PowerShell (**utilisation-AzureRmHDInsightCluster** ou **Invoke-AzureRmHDInsightHiveJob**) toosubmit travaux, ces opérations peuvent échouer avec le message d’erreur hello » *Cluster <clustername> n’est pas configuré pour l’accès des services HTTP*. » Ou (en fonction de l’opération de hello), vous pouvez obtenir des autres messages d’erreur, tel que «*Impossible de se connecter toocluster*».
* Ces problèmes de compatibilité sont résolus dans les versions les plus récentes hello de hello HDInsight SDK et Azure PowerShell. Nous vous recommandons de mettre à jour hello HDInsight SDK tooversion 1.3.1.6 ou ultérieure et Azure PowerShell outils tooversion 0.8.8 ou version ultérieure. Vous pouvez obtenir l’accès toohello dernière SDK HDInsight à partir de [pépite](http://nuget.codeplex.com/wikipage?title=Getting%20Started) et hello Azure PowerShell Tools à [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).

## <a name="notes-for-9122014-release-of-hdinsight-31"></a>Notes pour la version du 12/09/2014 de HDinsight 3.1
* Cette version est basée sur Hortonworks Data Platform (HDP) 2.1.5. Pour obtenir la liste des bogues hello résolu dans cette version, consultez hello [résolu dans cette version](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.5/bk_releasenotes_hdp_2.1/content/ch_relnotes-hdp-2.1.5-fixed.html) page hello Hortonworks site.
* Dans le dossier de bibliothèques hello Pig, hello « avro-mapred-1.7.4.jar » a été modifié trop « avro-mapred-1.7.4-hadoop2.jar. » contenu Hello de ce fichier contient un correctif de bogue secondaire qui est sans rupture. Il est recommandé que les clients n’apportez pas une dépendance directe sur nom hello Hello JAR fichier tooavoid sauts lorsque les fichiers sont renommés.

## <a name="notes-for-8212014-release"></a>Notes pour la version du 21/08/2014
* Nous ajoutons hello WebHCat configuration (HIVE-7155), qui définit la limite de mémoire par défaut de hello pour un contrôleur Templeton travail too1 Go suivante. (valeur par défaut de la précédente hello était 512 Mo.)

     templeton.mapper.memory.mb (=1024)

  * Cette modification résout hello avec certaines requêtes Hive en raison des limites de mémoire toolower l’erreur suivante : « Conteneur s’exécute en au-delà des limites de mémoire physique ».
  * toorevert toohello anciennes valeurs par défaut vous pouvez définir cette too512 de valeur de configuration via PowerShell d’Azure au moment de la création de cluster à l’aide de hello de commande suivante :

      Add-AzureRmHDInsightConfigValues -Core @{"templeton.mapper.memory.mb"="512";}
* nom d’hôte Hello du rôle de soigneur hello a été modifié trop*soigneur*. Cela affecte la résolution des noms dans un cluster de hello, mais elle n’affecte pas les API REST externes. Si vous avez des composants qui hello utilisation *zookeepernode* nom d’hôte, vous devez tooupdate les toouse nouveau nom. Hello nouveaux noms pour les nœuds soigneur trois hello sont :

  * zookeeper0
  * zookeeper1
  * zookeeper2
* La matrice de support des versions de HBase est mise à jour. Seule la version HDInsight 3.1 (HBase version 0.98) est prise en charge pour les charges de travail HBase de production. La version 3.0 qui était disponible en tant que version préliminaire ne sera plus prise en charge à l’avenir.

## <a name="notes-about-clusters-created-prior-too8152014"></a>Remarques sur les clusters créés préalable too8/15/2014
Un message d’erreur Azure PowerShell ou HDInsight SDK « Cluster <clustername> n’est pas configuré pour l’accès des services HTTP » (ou en fonction de l’opération de hello, autres messages d’erreur tels que : « Impossible de se connecter toocluster ») peuvent survenir en raison de la différence de version tooa entre Azure PowerShell ou hello HDInsight SDK et un cluster. Les clusters créés le 15/08 ou ultérieurement prennent en charge la nouvelle capacité d’approvisionnement dans les réseaux virtuels. Cette fonctionnalité n’est pas correctement interprétée avec les versions antérieures de hello Azure PowerShell ou hello HDInsight SDK, qui en résulte des échecs d’opérations d’envoi de travail. Si vous utilisez l’API du Kit de développement logiciel HDInsight ou Azure PowerShell applets de commande (par exemple, utilisez-AzureRmHDInsightCluster ou Invoke-AzureRmHDInsightHiveJob) toosubmit travaux, ces opérations peuvent échouer avec l’un des messages d’erreur hello décrits.

Ces problèmes de compatibilité sont résolus dans les versions les plus récentes hello de hello HDInsight SDK et Azure PowerShell. Nous vous recommandons de mettre à jour hello HDInsight SDK tooversion 1.3.1.6 ou ultérieure et Azure PowerShell outils tooversion 0.8.8 ou version ultérieure. Vous pouvez obtenir l’accès toohello dernière SDK HDInsight à partir de [NuGet][nuget-link]. Vous pouvez accéder à des outils de hello Azure PowerShell à l’aide de [Microsoft Web Platform Installer][webpi-link].

## <a name="notes-for-7282014-release"></a>Notes pour la version du 28/07/14
* **HDInsight disponible dans les nouvelles zones**: nous avons développé des régions toothree HDInsight présence géographique. Les clients HDInsight peuvent créer des clusters dans ces régions.
  * Est de l'Asie
  * États-Unis - partie centrale septentrionale
  * Centre-Sud des États-Unis
* HDInsight version 1.6 (HDP 1.1 et Hadoop 1.0.3) et HDInsight version 2.1 (HDP1.3 et Hadoop 1.2) sont supprimés de hello portail Azure. Vous pouvez continuer aux clusters Hadoop toocreate pour ces versions à l’aide de hello applet de commande Azure PowerShell [New-AzureRmHDInsightCluster](http://msdn.microsoft.com/library/dn593744.aspx) ou à l’aide de hello [HDInsight SDK](http://msdn.microsoft.com/library/azure/dn469975.aspx). Pour plus d’informations, consultez [Contrôle de version des composants HDInsight](hdinsight-component-versioning.md).
* Changements concernant Hortonworks Data Platform (HDP) dans cette version :

<table border="1">
<tr><th>HDP</th><th>Changements</th></tr>
<tr><td>HDP 1.3 / HDI 2.1</td><td>Pas de changements</td></tr>
<tr><td>HDP 2.0 / HDI 3.0</td><td>Pas de changements</td></tr>
<tr><td>HDP 2.1 / HDI 3.1</td><td>zookeeper: ['3.4.5.2.1.3.0-1948'] -> ['3.4.5.2.1.3.2-0002']</td></tr>
</table>

## <a name="notes-for-6242014-release"></a>Notes pour la version du 24/06/14
Cette version contient le service HDInsight de toohello améliorations :

* **Disponibilité de HDP 2.1**: 3.1 HDInsight (qui contient HDP 2.1) est généralement disponible et est la version par défaut de hello pour les nouveaux clusters.
* **HBase : amélioration du portail Azure**: nous faisons en sorte que les clusters HBase soient disponibles dans la version préliminaire. Vous pouvez créer des clusters HBase à partir du portail hello avec seulement quelques clics.

Avec HBase, vous pouvez créer diverses charges de travail en temps réel sur HDInsight, à partir de sites Web interactifs qui fonctionnent avec tooservices de jeux de données volumineux le stockage des données de capteur et télémétrie issus de millions de points de terminaison. étape suivante de Hello serait tooanalyze les données de salutation dans ces charges de travail avec des travaux Hadoop, et cela est possible dans HDInsight via Azure PowerShell et le tableau de bord hello ruche du cluster.

### <a name="apache-mahout-preinstalled-on-hdinsight-31"></a>Apache Mahout préinstallé sur HDInsight 3.1
 [Mahout](http://hortonworks.com/hadoop/mahout/) est déjà installé sur des clusters HDInsight 3.1 Hadoop, afin de pouvoir exécuter des travaux de Mahout sans avoir besoin de hello de configuration de cluster supplémentaires. Par exemple, vous pouvez à distance dans un cluster Hadoop en utilisant le protocole RDP (Remote Desktop), et sans étapes supplémentaires, vous pouvez exécuter hello Hello World Mahout commande suivante :

        mahout org.apache.mahout.classifier.df.tools.Describe -p /user/hdp/glass.data -f /user/hdp/glass.info -d I 9 N L

        mahout org.apache.mahout.classifier.df.BreimanExample -d /user/hdp/glass.data -ds /user/hdp/glass.info -i 10 -t 100

Pour obtenir une explication plus complète de cette procédure, consultez la documentation hello pour hello [Breiman exemple](https://mahout.apache.org/users/classification/breiman-example.html) sur le site Web de Apache Mahout hello.

### <a name="hive-queries-can-use-tez-in-hdinsight-31"></a>Les requêtes Hive peuvent utiliser Tez dans HDinsight 3.1
Hive 0.13 est désormais disponible dans HDInsight 3.1 et capable d’exécuter des requêtes avec Tez. Des gains de performances considérables peuvent ainsi être obtenus.
Tez n’est pas activé par défaut pour les requêtes Hive. toouse, vous devez activer la recherche. Vous pouvez activer Tez par hello suivant extrait de code en cours d’exécution :

        set hive.execution.engine=tez;
        select sc_status, count(*), histogram_numeric(sc_bytes,5) from website_logs_orc_local group by sc_status;

Hortonworks a publié une ventilation détaillée des améliorations apportées aux requêtes Hive en termes de performances avec Tez, tel qu'il est fourni dans les benchmarks standard. Pour des détails, consultez la page [Tests de performances d'Apache Hive 13 for Enterprise Hadoop](http://hortonworks.com/blog/benchmarking-apache-hive-13-enterprise-hadoop/).

Pour plus d’informations, consultez l’article [Hive on Tez](https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez) (Hive sur Tez).

### <a name="global-availability"></a>Disponibilité générale
Avec la version de hello de HDInsight sur Hadoop 2.2, Microsoft a apporté HDInsight disponible dans toutes les principales zones géographiques où Azure est disponible. Plus précisément, les centres de données hello ouest Europe et Asie du Sud-est ont été mis en ligne. Ainsi, les clusters de toolocate clients dans un centre de données est fermée et, éventuellement, dans une zone similaire d’exigences de conformité.

### <a name="dos--donts-between-cluster-versions"></a>À faire et ne pas faire entre les versions de clusters
**Les metastores Oozie utilisés avec un cluster HDInsight 3.1 n’ont plus de compatibilité descendante avec les clusters HDInsight 2.1 et ne peuvent pas être utilisés avec cette version précédente**.

Vous ne pouvez plus réutiliser une base de données de metastore Oozie personnalisée déployée avec un cluster HDInsight 3.1 avec un cluster HDInsight 2.1. Cela est le cas de hello même si le magasin de métadonnées hello provient avec un cluster HDInsight 2.1. Ce scénario n’est pas pris en charge, car le schéma du magasin de métadonnées hello mis à jour lorsqu’il est utilisé avec un cluster HDInsight 3.1, donc il n’est plus compatible avec le magasin de métadonnées hello requis par les clusters de hello HDInsight 2.1. Toute tentative de tooreuse un magasin de métadonnées Oozie qui a été utilisé avec un cluster HDInsight 3.1 rendre le cluster HDInsight 2.1 de hello inutilisable.

**Impossible de partager des metastores Oozie entre des clusters.**

Magasin de métadonnées Oozie est des clusters de toospecific jointe et ils ne peuvent pas être partagés entre les clusters.

### <a name="breaking-changes"></a>Dernières modifications
**Syntaxe du préfixe**: hello uniquement « wasb : / / » syntaxe est prise en charge dans HDInsight 3.1 et CTP 3.0 clusters. Hello plus anciens « asv : / / » syntaxe est prise en charge dans HDInsight 2.1 et 1.6 clusters, mais il n’est pas pris en charge dans HDInsight 3.1 ou 3.0 clusters. Cela signifie que tous les travaux soumis tooan HDInsight 3.1 ou 3.0 explicitement de cluster qui utilise hello « asv : / / » syntaxe échouera. Hello « wasb : / / » syntaxe doit être utilisée à la place. En outre, travaux soumis tooany HDInsight 3.1 ou 3.0 clusters qui sont créés avec un magasin de métadonnées existante qui contient explicites fait référence à tooresources à l’aide de hello « asv : / / » syntaxe échouera. Ces magasins de métadonnées doivent toobe recréé à l’aide de hello « wasb : / / » ressources tooaddress de syntaxe.

**Ports**: hello les ports utilisés par hello service HDInsight ont été modifiés. les numéros de port Hello qui étaient utilisés ont été au sein de la plage de ports éphémères hello hello système d’exploitation Windows. Les ports sont alloués automatiquement à partir d’une plage éphémère prédéfinie pour des communications à durée de vie limitée basées sur un protocole Internet. Hello nouvel ensemble de numéros de port de service Hortonworks Data Platform (HDP) autorisées sont en dehors de cette tooavoid plage cela génère des conflits susceptibles de survenir avec hello les ports utilisés par les services en cours d’exécution sur le nœud principal de hello. les nouveaux numéros de port Hello n’entraînent pas les modifications avec rupture. numéros de Hello utilisés sont les suivantes :

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
Hello dépendances suivantes ont été ajoutées dans HDInsight 3.x (HDP2.x) :

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

Hello dépendances suivantes n’existent plus dans HDInsight 3.x (HDP2.x) :

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
Hello version modifications suivantes ont été effectué entre HDInsight 2.x (HDP1.x) et HDInsight 3.x (HDP2.x) :

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
pilote de Java Database Connectivity (JDBC) Hello pour SQL Server est utilisée en interne par HDInsight et n’est pas utilisé pour les opérations externes. Si vous souhaitez tooconnect tooHDInsight à l’aide de base de données de connectivité ODBC (Open), utilisez hello Hive pilote ODBC de Microsoft. Pour plus d’informations, consultez [tooHDInsight Excel de se connecter avec Microsoft ODBC Driver de la ruche de hello](hdinsight-connect-excel-hive-odbc-driver.md).

### <a name="bug-fixes"></a>Résolution des bogues
Avec cette version, nous avons actualisé hello versions HDInsight avec plusieurs résolutions de bogue suivantes :

* HDInsight 2.1 (HDP 1.3)
* HDInsight 3.0 (HDP 2.0)
* HDInsight 3.1 (HDP 2.1)

## <a name="hortonworks-release-notes"></a>Notes de publication de Hortonworks
Notes de publication pour hello plateformes de données Hortonworks (HDPs) qui sont utilisés par les clusters de version de HDInsight sont disponibles à hello emplacements suivants :

* HDInsight version 3.1 utilise une distribution Hadoop basé sur hello [Hortonworks Data Platform 2.1.7][hdp-2-1-7]. Il s’agit de cluster Hadoop de hello par défaut créé à l’aide de hello portail Azure après le 7/11/2014. Clusters HDInsight 3.1 créés avant le 7/11/2014 étaient basées sur hello [Hortonworks Data Platform 2.1.1][hdp-2-1-1]
* HDInsight version 3.0 utilise une distribution Hadoop basé sur hello [Hortonworks Data Platform 2.0][hdp-2-0-8].
* HDInsight version 2.1 utilise une distribution Hadoop basé sur hello [Hortonworks données plateforme 1.3][hdp-1-3-0].
* HDInsight version 1.6 utilise une distribution Hadoop basé sur hello [Hortonworks données plateforme 1.1][hdp-1-1-0].

[hdp-2-1-7]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.7-Win/bk_releasenotes_HDP-Win/content/ch_relnotes-HDP-2.1.7.html

[hdp-2-1-1]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.1/bk_releasenotes_hdp_2.1/content/ch_relnotes-hdp-2.1.1.html

[hdp-2-0-8]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.0.8.0/bk_releasenotes_hdp_2.0/content/ch_relnotes-hdp2.0.8.0.html

[hdp-1-3-0]: http://docs.hortonworks.com/HDPDocuments/HDP1/HDP-1.3.0/bk_releasenotes_hdp_1.x/content/ch_relnotes-hdp1.3.0_1.html

[hdp-1-1-0]: http://docs.hortonworks.com/HDPDocuments/HDP1/HDP-Win-1.1/bk_releasenotes_HDP-Win/content/ch_relnotes-hdp-win-1.1.0_1.html

[nuget-link]: https://www.nuget.org/packages/Microsoft.WindowsAzure.Management.HDInsight/

[webpi-link]: http://go.microsoft.com/?linkid=9811175&clcid=0x409

[hdinsight-install-spark]: ../hdinsight-hadoop-spark-install/
[hdinsight-r-scripts]: ../hdinsight-hadoop-r-scripts/
