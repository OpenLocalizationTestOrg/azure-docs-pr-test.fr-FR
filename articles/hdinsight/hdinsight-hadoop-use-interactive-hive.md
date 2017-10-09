---
title: aaaUse Hive Interactive dans HDInsight - Azure | Documents Microsoft
description: "Découvrez comment toouse Interactive Hive (Hive sur LLAP) dans HDInsight."
keywords: 
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 0957643c-4936-48a3-84a3-5dc83db4ab1a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 9e751a08091d18bc1b3d070468feef87f6828c61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-interactive-hive-in-hdinsight-preview"></a>Utilisation de Hive interactif dans HDInsight (version préliminaire)
Hive interactif (également appelé [Live Long and Process](https://cwiki.apache.org/confluence/display/Hive/LLAP)) est un nouveau [type de cluster](hdinsight-hadoop-provision-linux-clusters.md#cluster-types) HDInsight.  Hive interactif permet la mise en mémoire cache ce qui rend les requêtes Hive beaucoup plus interactives et rapides. Cette nouvelle fonctionnalité rend les HDInsight d'entre hello la plupart des performantes, flexible et ouvert Big Data solutions monde de cloud de hello des caches en mémoire (à l’aide de la ruche et Spark) et la gestion avancée analytique via une profonde intégration avec R Services. 

cluster de la ruche interactif Hello est différent de cluster Hadoop de hello. Il contient uniquement le service de ruche hello. 

> [!NOTE]
> MapReduce, Pig, Sqoop, Oozie et d’autres services seront prochainement supprimés de ce type de cluster.
> Hello service Hive dans le cluster de la ruche interactif hello est uniquement accessible via hello Ambari ruche vue, Beeline et la ruche ODBC. Il n’est pas accessible via la console Hive, Templeton, l’interface de ligne de commande Azure et Azure PowerShell. 
> 
> 

## <a name="create-an-interactive-hive-cluster"></a>Création d’un cluster Hive interactif
Le cluster Hive interactif est uniquement pris en charge sur les clusters basés sur Linux. Pour des informations sur la création de clusters HDInsight, consultez [Création de clusters Hadoop basés sur Linux dans HDInsight](hdinsight-hadoop-provision-linux-clusters.md).

## <a name="execute-hive-from-interactive-hive"></a>Exécution de Hive à partir de Hive interactif
Il existe différentes options vous permettant d’exécuter des requêtes Hive :

* Exécutez Hive à l’aide de hello Ambari ruche vue
  
    Pour hello d’informations sur l’utilisation de hello Hive une vue, consultez [hello d’utiliser la ruche de vue avec Hadoop dans HDInsight](hdinsight-hadoop-use-hive-ambari-view.md).
* Exécution de Hive à l’aide de Beeline
  
    Pour plus d’informations hello sur l’utilisation de Beeline sur HDInsight, consultez [utilisez Hive avec Hadoop dans HDInsight avec Beeline](hdinsight-hadoop-use-hive-beeline.md).
  
    Vous utilisez Beeline à partir de nœud principal de hello ou un nœud vide.  L’utilisation de Beeline à partir d’un nœud de périmètre vide est recommandée.  Pour des informations sur la création d’un cluster HDInsight avec un nœud de périmètre vide, consultez [Utiliser des nœuds de périmètre vides dans HDInsight](hdinsight-apps-use-edge-node.md).
* Exécution de Hive à l’aide d’ODBC Hive
  
    Pour plus d’informations hello sur l’utilisation de la ruche de ODBC, consultez [tooHadoop Excel de se connecter avec le pilote Microsoft ODBC de la ruche de hello](hdinsight-connect-excel-hive-odbc-driver.md).

**hello toofind chaîne de connexion JDBC :**

1. Ouverture de session tooAmbari à l’aide de hello suivant l’URL : https://<ClusterName>. AzureHDInsight.net.
2. Cliquez sur **la ruche** à partir du menu de gauche hello.
3. Cliquez sur hello mis en surbrillance icône toocopy hello URL :
   
   ![HDInsight Hadoop Hive interactif LLAP JDBC](./media/hdinsight-hadoop-use-interactive-hive/hdinsight-hadoop-use-interactive-hive-jdbc.png)

## <a name="see-also"></a>Voir aussi
* [Créer des clusters basés sur Linux de Hadoop dans HDInsight](hdinsight-hadoop-provision-linux-clusters.md): Découvrez comment toocreate Hive interactif clusters dans HDInsight.
* [Utiliser la ruche avec Hadoop dans HDInsight avec Beeline](hdinsight-hadoop-use-hive-beeline.md): Découvrez comment requêtes Hive de toouse Beeline toosubmit.
* [Rejoignez Excel tooHadoop hello Hive pilote ODBC de Microsoft](hdinsight-connect-excel-hive-odbc-driver.md): Découvrez comment tooconnect Excel tooHive.

