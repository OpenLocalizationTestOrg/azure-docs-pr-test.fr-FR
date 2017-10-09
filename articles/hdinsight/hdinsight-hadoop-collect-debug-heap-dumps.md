---
title: aaaDebug et analyser les services Hadoop avec des dumps de tas - Azure | Documents Microsoft
description: "Collecter les vidages de segment de mémoire pour les services de Hadoop et à l’intérieur de hello compte de stockage d’objets Blob Azure pour le débogage et analyse automatiquement."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: e4ec4ebb-fd32-4668-8382-f956581485c4
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 70fbc2d6d97d35b0d7b1d9149673b02ae1878eb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="collect-heap-dumps-in-blob-storage-toodebug-and-analyze-hadoop-services"></a>Collecter les vidages de segment de mémoire dans toodebug de stockage d’objets Blob et d’analyser les services Hadoop
[!INCLUDE [heapdump-selector](../../includes/hdinsight-selector-heap-dump.md)]

Dumps de tas contiennent un instantané de la mémoire de l’application hello, y compris les valeurs hello des variables au moment de hello création du dump hello. Ils sont donc utiles pour diagnostiquer les problèmes qui se produisent au moment de l’exécution. Dumps de tas peuvent être collectées pour les services de Hadoop et placées à l’intérieur de hello compte de stockage d’objets Blob Azure d’un utilisateur sous HDInsightHeapDumps automatiquement /.

collection Hello des vidages sur le segment de mémoire pour divers services doit être activée pour les services sur les clusters individuels. valeur par défaut de Hello pour cette fonctionnalité est toobe désactivée pour un cluster. Ces images de segment de mémoire peuvent être volumineuses, afin qu’il soit compte de stockage Blob hello toomonitor opportun où ils sont sauvegardés une fois que la collection de hello a été activée.

> [!IMPORTANT]
> Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure. Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement). informations Hello dans cet article s’applique uniquement à base tooWindows de HDInsight. Pour plus d’informations sur HDInsight sur Linux, consultez la rubrique [Activation des dumps de tas pour les services Hadoop sur HDInsight sur Linux](hdinsight-hadoop-collect-debug-heap-dump-linux.md)


## <a name="eligible-services-for-heap-dumps"></a>Services éligibles pour le vidage de tas
Vous pouvez activer les vidages de segment de mémoire pour hello suivant services :

* **hcatalog** - tempelton
* **hive** - hiveserver2, metastore, derbyserver
* **mapreduce** - jobhistoryserver
* **yarn** - resourcemanager, nodemanager, timelineserver
* **hdfs** - datanode, secondarynamenode, namenode

## <a name="configuration-elements-that-enable-heap-dumps"></a>Éléments de configuration permettant d’activer le vidage de tas
tooturn sur les dumps de segment de mémoire pour un service, vous avez besoin d’éléments de configuration approprié tooset hello dans la section de hello pour ce service, qui est spécifié par **service_name**.

    "javaargs.<service_name>.XX:+HeapDumpOnOutOfMemoryError" = "-XX:+HeapDumpOnOutOfMemoryError",
    "javaargs.<service_name>.XX:HeapDumpPath" = "-XX:HeapDumpPath=c:\Dumps\<service_name>_%date:~4,2%%date:~7,2%%date:~10,2%%time:~0,2%%time:~3,2%%time:~6,2%.hprof"

Hello valeur **service_name** peut être un des services hello répertoriés ici : tempelton, hiveserver2, le magasin de métadonnées, derbyserver, jobhistoryserver, resourcemanager, nodemanager, timelineserver, datanode, secondarynamenode, ou namenode.

## <a name="enable-using-azure-powershell"></a>Activer à l’aide d’Azure PowerShell
Par exemple, tooturn sur les dumps de segment de mémoire à l’aide d’Azure PowerShell pour jobhistoryserver, vous pouvez utiliser hello script suivant :

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

    $MapRedConfigValues = new-object 'Microsoft.WindowsAzure.Management.HDInsight.Cmdlet.DataObjects.AzureHDInsightMapReduceConfiguration'

    $MapRedConfigValues.Configuration = @{ "javaargs.jobhistoryserver.XX:+HeapDumpOnOutOfMemoryError"="-XX:+HeapDumpOnOutOfMemoryError" ; "javaargs.jobhistoryserver.XX:HeapDumpPath" = "-XX:HeapDumpPath=c:\\Dumps\\jobhistoryserver_%date:~4,2%_%date:~7,2%_%date:~10,2%_%time:~0,2%_%time:~3,2%_%time:~6,2%.hprof" }

## <a name="enable-using-net-sdk"></a>Activer avec le kit de développement logiciel (SDK) .NET
Par exemple, tooturn sur des dumps de tas à l’aide de hello Azure HDInsight .NET SDK pour jobhistoryserver, vous pouvez utiliser hello suivant de code :

    clusterInfo.MapReduceConfiguration.ConfigurationCollection.Add(new KeyValuePair<string, string>("javaargs.jobhistoryserver.XX:+HeapDumpOnOutOfMemoryError", "-XX:+HeapDumpOnOutOfMemoryError"));

    clusterInfo.MapReduceConfiguration.ConfigurationCollection.Add(new KeyValuePair<string, string>("javaargs.jobhistoryserver.XX:HeapDumpPath", "-XX:HeapDumpPath=c:\\Dumps\\jobhistoryserver_%date:~4,2%_%date:~7,2%_%date:~10,2%_%time:~0,2%_%time:~3,2%_%time:~6,2%.hprof"));
