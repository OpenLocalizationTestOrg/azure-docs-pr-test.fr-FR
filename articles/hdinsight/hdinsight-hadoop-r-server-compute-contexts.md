---
title: options de contexte aaaCompute pour R Server sur HDInsight - Azure | Documents Microsoft
description: En savoir plus sur hello calcul autre contexte options disponibles toousers avec R Server sur HDInsight
services: HDInsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 0deb0b1c-4094-459b-94fc-ec9b774c1f8a
ms.service: HDInsight
ms.custom: hdinsightactive
ms.devlang: R
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/19/2017
ms.author: bradsev
ms.openlocfilehash: b3b0d0cc3caa390797dcff8c73d66cd3ad78bcaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="compute-context-options-for-r-server-on-hdinsight"></a>Options de contexte de calcul pour R Server sur HDInsight (version préliminaire)

Microsoft R Server sur Azure HDInsight contrôle l’exécution des appels par le paramètre de contexte de calcul hello. Cet article présente hello les options disponible toospecify si et comment l’exécution est mis en parallèle sur les cœurs de nœud de périmètre hello ou cluster HDInsight.

nœud de périmètre Hello d’un cluster fournit un emplacement pratique tooconnect toohello cluster toorun vos scripts R. Avec un nœud de périmètre, vous avez des fonctions d’option Hello en cours d’exécution parallélisée distributed hello de ScaleR entre les cœurs hello du serveur de nœud hello edge. Vous pouvez également exécuter les sur les nœuds hello du cluster de hello à l’aide de ScaleR Hadoop MapReduce ou Spark contextes de calcul.

## <a name="microsoft-r-server-on-azure-hdinsight"></a>Microsoft R Server dans Azure HDInsight
[Microsoft R Server sur Azure HDInsight](hdinsight-hadoop-r-server-overview.md) fournit les dernières fonctionnalités de hello pour analytique de basé sur R. Il peut utiliser des données stockées dans un conteneur HDFS dans votre [objets Blob Azure](../storage/common/storage-introduction.md "le stockage Blob Azure") compte de stockage, d’un magasin de LAC de données ou d’un système de fichiers Linux local hello. Étant donné que R Server repose sur R open source, hello R des applications que vous générez peuvent appliquer un des packages hello 8000 + R open source. Ils peuvent également utiliser des routines de hello dans [RevoScaleR](https://msdn.microsoft.com/microsoft-r/scaler/scaler), données analytique package de Microsoft qui est inclus avec R Server.  

## <a name="compute-contexts-for-an-edge-node"></a>Contextes de calcul pour un nœud de périmètre
En général, un script R qui est exécuté sur le nœud de périmètre hello dans R Server s’exécute au sein de l’interpréteur de hello R sur ce nœud. les exceptions de Hello sont les étapes qui appellent une fonction ScaleR. les appels ScaleR Hello exécutent dans un environnement de calcul qui est déterminé par la façon dont vous définissez le contexte de calcul ScaleR hello.  Lorsque vous exécutez votre script R à partir d’un nœud, les valeurs possibles hello Hello de calcul sont de contexte :

- local séquentiel (*« local »*)
- local parallèle (*« localpar »*)
- Map Reduce
- Spark

Hello *'local'* et *'localpar'* options diffèrent uniquement par la procédure **rxExec** appels sont exécutés. Ils sont tous deux exécutent autres appels de fonction de réception de manière parallèle sur tous les cœurs sauf indication contraire, via l’utilisation de hello ScaleR **numCoresToUse** option, par exemple `rxOptions(numCoresToUse=6)`. Les options d’exécution parallèle offrent des performances optimales.

Hello tableau suivant résume les hello que différents tooset d’options de contexte l’exécution des appels de calcul :

| Contexte de calcul  | Comment tooset                      | Contexte d’exécution                        |
| ---------------- | ------------------------------- | ---------------------------------------- |
| Local sequential | rxSetComputeContext(‘local’)    | Exécution de parallélisée inter-cœurs hello serveur nœud edge hello, à l’exception des appels rxExec, qui sont exécutées en série |
| Local parallel   | rxSetComputeContext(‘localpar’) | Exécution de parallélisée inter-cœurs hello du serveur de nœud hello edge |
| Spark            | RxSpark()                       | Parallélisée exécution distribuée via Spark sur les nœuds de hello du cluster HDI de hello |
| Map Reduce       | RxHadoopMR()                    | Parallélisée exécution distribuée via MapReduce entre les nœuds hello du cluster HDI de hello |

## <a name="guidelines-for-deciding-on-a-compute-context"></a>Conseils pour le choix d’un contexte de calcul

Hello trois options que vous choisissez qui fournissent l’exécution parallélisée dépend hello nature de votre travail de l’analytique, taille de hello et emplacement hello de vos données. Il n’existe aucune formule simple qui vous indique ce qui toouse de contexte de calcul. Il existe, toutefois, certains principes fondamentaux qui peuvent vous aider à faire hello bon choix, ou, au minimum, vous aider à réduire vos choix avant d’exécuter un test d’évaluation. Ces principes sont les suivants :

- système de fichiers Linux local Hello est plus rapide que HDFS.
- Analyses répétées sont plus rapides si les données de salutation sont locales, et s’il s’agit de XDF.
- Il est préférable de toostream de petites quantités de données à partir d’une source de données de texte. Si la quantité hello de données est plus grande, convertissez-la tooXDF avant l’analyse.
- surcharge Hello de copie ou de diffusion en continu de nœud de périmètre hello données toohello pour l’analyse devient ingérable de très grandes quantités de données.
- Spark est plus rapide que Map Reduce pour l’analyse dans Hadoop.

Étant donné ces principes, hello sections suivantes offrent certaines règles générales pour la sélection d’un contexte de calcul.

### <a name="local"></a>Local
* Si la quantité de hello de tooanalyze de données est petite et ne nécessite pas d’analyses répétées, puis diffuser en continu directement dans hello analyse routines à l’aide *'local'* ou *'localpar'*.
* Si hello tooanalyze de données est petite ou moyenne et nécessite des analyses répétées, puis copier le système de fichiers local toohello, importez-le tooXDF et analyser via *'local'* ou *'localpar'*.

### <a name="hadoop-spark"></a>Hadoop Spark
* Si la quantité de hello de tooanalyze de données est importante, puis l’importer tooa Spark de trame de données à l’aide de **RxHiveData** ou **RxParquetData**, ou tooXDF dans HDFS (sauf si le stockage est un problème) et les analyser à l’aide de hello Spark contexte de calcul.

### <a name="hadoop-map-reduce"></a>Hadoop Map Reduce
* Utiliser le contexte de calcul MapReduce hello uniquement si vous rencontrez un problème insurmontable avec le contexte de calcul Spark hello, car il est généralement plus long.  

## <a name="inline-help-on-rxsetcomputecontext"></a>Aide en ligne sur rxSetComputeContext
Pour plus d’informations et des exemples de ScaleR contextes de calcul, consultez hello inline l’aide de R sur la méthode de rxSetComputeContext hello, par exemple :

    > ?rxSetComputeContext

Vous pouvez également faire référence toohello «[ScaleR Distributed Computing Guide](https://msdn.microsoft.com/microsoft-r/scaler-distributed-computing)» qui est disponible à partir de hello [R Server MSDN](https://msdn.microsoft.com/library/mt674634.aspx "R Server sur MSDN") bibliothèque.

## <a name="next-steps"></a>Étapes suivantes
Dans cet article, vous avez appris les options hello toospecify disponible si et comment l’exécution est mis en parallèle sur les cœurs de nœud de périmètre hello ou cluster HDInsight. toolearn en savoir plus sur les clusters comment toouse R Server hdinsight, consultez hello rubriques suivantes :

* [Vue d’ensemble : R Server sur HDInsight (version préliminaire)](hdinsight-hadoop-r-server-overview.md)
* [Commencer à utiliser R Server sur HDInsight (version préliminaire)](hdinsight-hadoop-r-server-get-started.md)
* [Ajouter RStudio Server tooHDInsight (si elle ne pas lors de la création du cluster)](hdinsight-hadoop-r-server-install-r-studio.md)
* [Options d’Azure Storage pour R Server sur HDInsight](hdinsight-hadoop-r-server-storage.md)

