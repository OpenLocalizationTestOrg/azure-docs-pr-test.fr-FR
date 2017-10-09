---
title: aaaUse Hadoop Pig dans HDInsight | Documents Microsoft
description: "Découvrez comment toouse porc avec Hadoop dans HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: acfeb52b-4b81-4a7d-af77-3e9908407404
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/15/2017
ms.author: larryfr
ms.openlocfilehash: 90850f2c742b8954c66ce277127e01b14fc3906f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-pig-with-hadoop-on-hdinsight"></a>Utilisation de Pig avec Hadoop sur HDInsight

Découvrez comment toouse [Apache Pig](http://pig.apache.org/) avec HDInsight...

Pig est une plateforme qui permet de créer des programmes pour Hadoop dans un langage procédural appelé *Pig Latin*. Pig est un autre tooJava pour la création de *MapReduce* solutions et il est inclus dans Azure HDInsight. Utilisez hello suivant hello toodiscover de table que Pig peut être utilisé avec HDInsight de différentes manières :

| **Utilisez-le** si vous souhaitez... | ... un interpréteur de commandes **interactif** | ... un traitement par **lots** | ...avec ce **système d’exploitation cluster** | ...depuis ce **système d’exploitation cluster** |
|:--- |:---:|:---:|:--- |:--- |
| [SSH](hdinsight-hadoop-use-pig-ssh.md) |✔ |✔ |Linux |Linux, Unix, Mac OS X ou Windows |
| [API REST](hdinsight-hadoop-use-pig-curl.md) |&nbsp; |✔ |Linux ou Windows |Linux, Unix, Mac OS X ou Windows |
| [Kit de développement logiciel (SDK) .NET pour Hadoop](hdinsight-hadoop-use-pig-dotnet-sdk.md) |&nbsp; |✔ |Linux ou Windows |Windows (pour l’instant) |
| [Windows PowerShell](hdinsight-hadoop-use-pig-powershell.md) |&nbsp; |✔ |Linux ou Windows |Windows |
| [Bureau à distance](hdinsight-hadoop-use-pig-remote-desktop.md) (HDInsight 3.2 et 3.3) |✔ |✔ |Windows |Windows |

> [!IMPORTANT]
> Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure. Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a id="why"></a>Pourquoi utiliser Pig ?

Un des défis hello de traitement de données à l’aide de MapReduce dans Hadoop implémente votre logique de traitement à l’aide uniquement sur une carte et une fonction de la réduire. Pour un traitement complexe, fréquence à laquelle vous avez toobreak le traitement en plusieurs opérations MapReduce qui sont chaînées tooachieve de résultats hello souhaité.

Pig vous permet de toodefine traitant comme une série de transformations qui hello du flux de données via la sortie de tooproduce hello souhaité.

langage Hello Pig permet de vous toodescribe hello flux de données d’entrée brute, via une ou plusieurs transformations, la sortie de hello souhaité tooproduce. Les programmes Pig Latin suivent le modèle général suivant :

* **Charge**: lire toobe données manipulée hello système de fichiers

* **Transformer**: manipuler les données de salutation

* **Dump ou stocker**: toohello l’écran de données de sortie ou de le stocker pour le traitement

### <a name="user-defined-functions"></a>Fonctions définies par l’utilisateur

Pig Latin prend également en charge les fonctions définies par l’utilisateur (UDF), qui vous permet de tooinvoke des composants externes qui implémentent la logique qui est difficile toomodel dans Pig Latin.

Pour plus d’informations sur Pig Latin, consultez les pages [Manuel de référence Pig Latin 1](http://pig.apache.org/docs/r0.7.0/piglatin_ref1.html) et [Manuel de référence Pig Latin 2](http://pig.apache.org/docs/r0.7.0/piglatin_ref2.html).

Pour obtenir un exemple d’utilisation des UDF avec Pig, consultez hello suivant des documents :

* [Utilisation de DataFu avec Pig dans HDInsight](hdinsight-hadoop-use-pig-datafu-udf.md) : DataFu est une collection de fonctions définies par l’utilisateur utiles gérées par Apache
* [Utilisation de Python avec Hive et Pig dans HDInsight](hdinsight-python.md)
* [Utilisation de C# avec Hive et Pig dans HDInsight](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

## <a id="data"></a>Exemple de données

HDInsight fournit différents jeux de données d’exemple, qui sont stockées dans hello `/example/data` et `/HdiSamples` répertoires. Ces répertoires sont dans le stockage par défaut hello pour votre cluster. exemple de Pig Hello dans ce document utilise hello *log4j* à partir du fichier `/example/data/sample.log`.

Chaque journal à l’intérieur du fichier de hello se compose d’une ligne de champs qui contient un `[LOG LEVEL]` champ tooshow hello hello et type de niveau de gravité, par exemple :

    2012-02-03 20:26:41 SampleClass3 [ERROR] verbose detail for id 1527353937

Dans l’exemple précédent de hello, niveau de journal hello est erreur.

> [!NOTE]
> Vous pouvez également générer un fichier log4j à l’aide de hello [Apache Log4j](http://en.wikipedia.org/wiki/Log4j) journalisation de l’outil, puis le télécharger cet objet blob tooyour de fichier. Consultez [tooHDInsight de télécharger des données](hdinsight-upload-data.md) pour obtenir des instructions. Pour plus d'informations sur l'utilisation du stockage d'objets blob Azure avec HDInsight, consultez la page [Utilisation du stockage d'objets blob Azure avec HDInsight](hdinsight-hadoop-use-blob-storage.md).

## <a id="job"></a>Exemple de travail

tâche Pig Latin suivante Hello charge hello `sample.log` fichier de stockage par défaut de hello pour votre cluster HDInsight. Il effectue ensuite une série de transformations qui entraîne le nombre d’illustrant le nombre de fois où chaque données d’entrée de journal au niveau hello s’est produite dans. les résultats de Hello sont écrits tooSTDOUT.

    LOGS = LOAD 'wasb:///example/data/sample.log';
    LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
    FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
    GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
    FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
    RESULT = order FREQUENCIES by COUNT desc;
    DUMP RESULT;

Hello image suivante affiche un résumé de chaque transformation ne toohello. les données.

![Représentation graphique des transformations de hello][image-hdi-pig-data-transformation]

## <a id="run"></a>Exécuter la tâche Pig Latin de hello

HDInsight peut exécuter des tâches Pig Latin de différentes façons. Utilisez hello suivant toodecide table quelle méthode vous consiste, puis suivez le lien hello pour une procédure pas à pas.

| **Utilisez-le** si vous souhaitez... | ... un interpréteur de commandes **interactif** | ... un traitement par **lots** | ...avec ce **système d’exploitation cluster** | ... depuis ce **client** |
|:--- |:---:|:---:|:--- |:--- |
| [SSH](hdinsight-hadoop-use-pig-ssh.md) |✔ |✔ |Linux |Linux, Unix, Mac OS X ou Windows |
| [Curl](hdinsight-hadoop-use-pig-curl.md) |&nbsp; |✔ |Linux ou Windows |Linux, Unix, Mac OS X ou Windows |
| [Kit de développement logiciel (SDK) .NET pour Hadoop](hdinsight-hadoop-use-pig-dotnet-sdk.md) |&nbsp; |✔ |Linux ou Windows |Windows (pour l’instant) |
| [Windows PowerShell](hdinsight-hadoop-use-pig-powershell.md) |&nbsp; |✔ |Linux ou Windows |Windows |
| [Bureau à distance](hdinsight-hadoop-use-pig-remote-desktop.md) (HDInsight 3.2 et 3.3) |✔ |✔ |Windows |Windows |

> [!IMPORTANT]
> Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure. Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="pig-and-sql-server-integration-services"></a>Pig et SQL Server Integration Services

Vous pouvez utiliser SQL Server Integration Services (SSIS) toorun un travail Pig. Bonjour Azure Feature Pack pour SSIS fournit hello suivant des composants qui fonctionnent avec des travaux Pig dans HDInsight.

* [Tâche d’Azure HDInsight Pig][pigtask]

* [Gestionnaire de connexions d’abonnement Azure][connectionmanager]

En savoir plus sur hello Azure Feature Pack pour SSIS [ici][ssispack].

## <a id="nextsteps"></a>Étapes suivantes
Maintenant que vous avez appris comment toouse Pig hdinsight, hello utilisation suivant lie tooexplore autres toowork manières avec Azure HDInsight.

* [Télécharger des données tooHDInsight][hdinsight-upload-data]
* [Utilisation de Hive avec HDInsight][hdinsight-use-hive]
* [Utilisation de Sqoop avec HDInsight](hdinsight-use-sqoop.md)
* [Utilisation d’Oozie avec HDInsight](hdinsight-use-oozie.md)
* [Utilisation des tâches MapReduce avec HDInsight][hdinsight-use-mapreduce]

[apachepig-home]: http://pig.apache.org/
[putty]: http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html
[curl]: http://curl.haxx.se/
[pigtask]: http://msdn.microsoft.com/library/mt146781(v=sql.120).aspx
[connectionmanager]: http://msdn.microsoft.com/library/mt146773(v=sql.120).aspx
[ssispack]: http://msdn.microsoft.com/library/mt146770(v=sql.120).aspx


[hdinsight-upload-data]: hdinsight-upload-data.md

[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md

[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md#mapreduce-sdk

[Powershell-install-configure]: /powershell/azureps-cmdlets-docs

[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx


[image-hdi-pig-data-transformation]: ./media/hdinsight-use-pig/HDI.DataTransformation.gif
