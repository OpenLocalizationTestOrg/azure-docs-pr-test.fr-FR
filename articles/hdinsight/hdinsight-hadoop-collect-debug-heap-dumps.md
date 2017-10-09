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
# <a name="collect-heap-dumps-in-blob-storage-toodebug-and-analyze-hadoop-services"></a><span data-ttu-id="e649e-103">Collecter les vidages de segment de mémoire dans toodebug de stockage d’objets Blob et d’analyser les services Hadoop</span><span class="sxs-lookup"><span data-stu-id="e649e-103">Collect heap dumps in Blob storage toodebug and analyze Hadoop services</span></span>
[!INCLUDE [heapdump-selector](../../includes/hdinsight-selector-heap-dump.md)]

<span data-ttu-id="e649e-104">Dumps de tas contiennent un instantané de la mémoire de l’application hello, y compris les valeurs hello des variables au moment de hello création du dump hello.</span><span class="sxs-lookup"><span data-stu-id="e649e-104">Heap dumps contain a snapshot of hello application's memory, including hello values of variables at hello time hello dump was created.</span></span> <span data-ttu-id="e649e-105">Ils sont donc utiles pour diagnostiquer les problèmes qui se produisent au moment de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="e649e-105">So they are useful for diagnosing problems that occur at run-time.</span></span> <span data-ttu-id="e649e-106">Dumps de tas peuvent être collectées pour les services de Hadoop et placées à l’intérieur de hello compte de stockage d’objets Blob Azure d’un utilisateur sous HDInsightHeapDumps automatiquement /.</span><span class="sxs-lookup"><span data-stu-id="e649e-106">Heap dumps can be automatically collected for Hadoop services and placed inside hello Azure Blob storage account of a user under HDInsightHeapDumps/.</span></span>

<span data-ttu-id="e649e-107">collection Hello des vidages sur le segment de mémoire pour divers services doit être activée pour les services sur les clusters individuels.</span><span class="sxs-lookup"><span data-stu-id="e649e-107">hello collection of heap dumps for various services must be enabled for services on individual clusters.</span></span> <span data-ttu-id="e649e-108">valeur par défaut de Hello pour cette fonctionnalité est toobe désactivée pour un cluster.</span><span class="sxs-lookup"><span data-stu-id="e649e-108">hello default for this feature is toobe off for a cluster.</span></span> <span data-ttu-id="e649e-109">Ces images de segment de mémoire peuvent être volumineuses, afin qu’il soit compte de stockage Blob hello toomonitor opportun où ils sont sauvegardés une fois que la collection de hello a été activée.</span><span class="sxs-lookup"><span data-stu-id="e649e-109">These heap dumps can be large, so it is advisable toomonitor hello Blob storage account where they are being saved once hello collection has been enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e649e-110">Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="e649e-110">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="e649e-111">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="e649e-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="e649e-112">informations Hello dans cet article s’applique uniquement à base tooWindows de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e649e-112">hello information in this article only applies tooWindows-based HDInsight.</span></span> <span data-ttu-id="e649e-113">Pour plus d’informations sur HDInsight sur Linux, consultez la rubrique [Activation des dumps de tas pour les services Hadoop sur HDInsight sur Linux](hdinsight-hadoop-collect-debug-heap-dump-linux.md)</span><span class="sxs-lookup"><span data-stu-id="e649e-113">For information on Linux-based HDInsight, see [Enable heap dumps for Hadoop services on Linux-based HDInsight](hdinsight-hadoop-collect-debug-heap-dump-linux.md)</span></span>


## <a name="eligible-services-for-heap-dumps"></a><span data-ttu-id="e649e-114">Services éligibles pour le vidage de tas</span><span class="sxs-lookup"><span data-stu-id="e649e-114">Eligible services for heap dumps</span></span>
<span data-ttu-id="e649e-115">Vous pouvez activer les vidages de segment de mémoire pour hello suivant services :</span><span class="sxs-lookup"><span data-stu-id="e649e-115">You can enable heap dumps for hello following services:</span></span>

* <span data-ttu-id="e649e-116">**hcatalog** - tempelton</span><span class="sxs-lookup"><span data-stu-id="e649e-116">**hcatalog** - tempelton</span></span>
* <span data-ttu-id="e649e-117">**hive** - hiveserver2, metastore, derbyserver</span><span class="sxs-lookup"><span data-stu-id="e649e-117">**hive** - hiveserver2, metastore, derbyserver</span></span>
* <span data-ttu-id="e649e-118">**mapreduce** - jobhistoryserver</span><span class="sxs-lookup"><span data-stu-id="e649e-118">**mapreduce** - jobhistoryserver</span></span>
* <span data-ttu-id="e649e-119">**yarn** - resourcemanager, nodemanager, timelineserver</span><span class="sxs-lookup"><span data-stu-id="e649e-119">**yarn** - resourcemanager, nodemanager, timelineserver</span></span>
* <span data-ttu-id="e649e-120">**hdfs** - datanode, secondarynamenode, namenode</span><span class="sxs-lookup"><span data-stu-id="e649e-120">**hdfs** - datanode, secondarynamenode, namenode</span></span>

## <a name="configuration-elements-that-enable-heap-dumps"></a><span data-ttu-id="e649e-121">Éléments de configuration permettant d’activer le vidage de tas</span><span class="sxs-lookup"><span data-stu-id="e649e-121">Configuration elements that enable heap dumps</span></span>
<span data-ttu-id="e649e-122">tooturn sur les dumps de segment de mémoire pour un service, vous avez besoin d’éléments de configuration approprié tooset hello dans la section de hello pour ce service, qui est spécifié par **service_name**.</span><span class="sxs-lookup"><span data-stu-id="e649e-122">tooturn on heap dumps for a service, you need tooset hello appropriate configuration elements in hello section for that service, which is specified by **service_name**.</span></span>

    "javaargs.<service_name>.XX:+HeapDumpOnOutOfMemoryError" = "-XX:+HeapDumpOnOutOfMemoryError",
    "javaargs.<service_name>.XX:HeapDumpPath" = "-XX:HeapDumpPath=c:\Dumps\<service_name>_%date:~4,2%%date:~7,2%%date:~10,2%%time:~0,2%%time:~3,2%%time:~6,2%.hprof"

<span data-ttu-id="e649e-123">Hello valeur **service_name** peut être un des services hello répertoriés ici : tempelton, hiveserver2, le magasin de métadonnées, derbyserver, jobhistoryserver, resourcemanager, nodemanager, timelineserver, datanode, secondarynamenode, ou namenode.</span><span class="sxs-lookup"><span data-stu-id="e649e-123">hello value of **service_name** can be any of hello services listed here: tempelton, hiveserver2, metastore, derbyserver, jobhistoryserver, resourcemanager, nodemanager, timelineserver, datanode, secondarynamenode, or namenode.</span></span>

## <a name="enable-using-azure-powershell"></a><span data-ttu-id="e649e-124">Activer à l’aide d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="e649e-124">Enable using Azure PowerShell</span></span>
<span data-ttu-id="e649e-125">Par exemple, tooturn sur les dumps de segment de mémoire à l’aide d’Azure PowerShell pour jobhistoryserver, vous pouvez utiliser hello script suivant :</span><span class="sxs-lookup"><span data-stu-id="e649e-125">For example, tooturn on heap dumps by using Azure PowerShell for jobhistoryserver, you can use hello following script:</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

    $MapRedConfigValues = new-object 'Microsoft.WindowsAzure.Management.HDInsight.Cmdlet.DataObjects.AzureHDInsightMapReduceConfiguration'

    $MapRedConfigValues.Configuration = @{ "javaargs.jobhistoryserver.XX:+HeapDumpOnOutOfMemoryError"="-XX:+HeapDumpOnOutOfMemoryError" ; "javaargs.jobhistoryserver.XX:HeapDumpPath" = "-XX:HeapDumpPath=c:\\Dumps\\jobhistoryserver_%date:~4,2%_%date:~7,2%_%date:~10,2%_%time:~0,2%_%time:~3,2%_%time:~6,2%.hprof" }

## <a name="enable-using-net-sdk"></a><span data-ttu-id="e649e-126">Activer avec le kit de développement logiciel (SDK) .NET</span><span class="sxs-lookup"><span data-stu-id="e649e-126">Enable using .NET SDK</span></span>
<span data-ttu-id="e649e-127">Par exemple, tooturn sur des dumps de tas à l’aide de hello Azure HDInsight .NET SDK pour jobhistoryserver, vous pouvez utiliser hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="e649e-127">For example, tooturn on heap dumps by using hello Azure HDInsight .NET SDK for jobhistoryserver, you can use hello following code:</span></span>

    clusterInfo.MapReduceConfiguration.ConfigurationCollection.Add(new KeyValuePair<string, string>("javaargs.jobhistoryserver.XX:+HeapDumpOnOutOfMemoryError", "-XX:+HeapDumpOnOutOfMemoryError"));

    clusterInfo.MapReduceConfiguration.ConfigurationCollection.Add(new KeyValuePair<string, string>("javaargs.jobhistoryserver.XX:HeapDumpPath", "-XX:HeapDumpPath=c:\\Dumps\\jobhistoryserver_%date:~4,2%_%date:~7,2%_%date:~10,2%_%time:~0,2%_%time:~3,2%_%time:~6,2%.hprof"));
