---
title: "Déboguer et analyser les services Hadoop avec des dumps de tas - Azure | Documents Microsoft"
description: "Collectez automatiquement les dumps de tas de services Hadoop et placez-les dans le compte de stockage Azure Blob à des fins de débogage et d’analyse."
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
ms.openlocfilehash: 6d1d4d47d279eb7a1f0bf1f587445683f0ace7a0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="collect-heap-dumps-in-blob-storage-to-debug-and-analyze-hadoop-services"></a><span data-ttu-id="89a5a-103">Collecter les dumps de tas dans le stockage Blob pour les services de débogage et d'analyse Hadoop</span><span class="sxs-lookup"><span data-stu-id="89a5a-103">Collect heap dumps in Blob storage to debug and analyze Hadoop services</span></span>
[!INCLUDE [heapdump-selector](../../includes/hdinsight-selector-heap-dump.md)]

<span data-ttu-id="89a5a-104">Les dumps de tas contiennent un instantané de la mémoire de l’application, y compris des valeurs des variables au moment de la création du dump.</span><span class="sxs-lookup"><span data-stu-id="89a5a-104">Heap dumps contain a snapshot of the application's memory, including the values of variables at the time the dump was created.</span></span> <span data-ttu-id="89a5a-105">Ils sont donc utiles pour diagnostiquer les problèmes qui se produisent au moment de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="89a5a-105">So they are useful for diagnosing problems that occur at run-time.</span></span> <span data-ttu-id="89a5a-106">Il est possible de collecter automatiquement les dumps de tas de services Hadoop et de les placer dans le compte de stockage d’objets blob Azure d’un utilisateur sous HDInsightHeapDumps/.</span><span class="sxs-lookup"><span data-stu-id="89a5a-106">Heap dumps can be automatically collected for Hadoop services and placed inside the Azure Blob storage account of a user under HDInsightHeapDumps/.</span></span>

<span data-ttu-id="89a5a-107">La collection des dumps de tas pour différents services doit être activée pour les services sur des clusters individuels.</span><span class="sxs-lookup"><span data-stu-id="89a5a-107">The collection of heap dumps for various services must be enabled for services on individual clusters.</span></span> <span data-ttu-id="89a5a-108">Par défaut, cette fonctionnalité est désactivée pour un cluster.</span><span class="sxs-lookup"><span data-stu-id="89a5a-108">The default for this feature is to be off for a cluster.</span></span> <span data-ttu-id="89a5a-109">Les dumps de tas pouvant être volumineux, nous vous recommandons de surveiller le compte de stockage d’objets blob dans lequel ils sont enregistrés une fois la collection activée.</span><span class="sxs-lookup"><span data-stu-id="89a5a-109">These heap dumps can be large, so it is advisable to monitor the Blob storage account where they are being saved once the collection has been enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="89a5a-110">Linux est le seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="89a5a-110">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="89a5a-111">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="89a5a-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="89a5a-112">Les informations mentionnées dans cet article s’appliquent uniquement aux clusters HDInsight sur Windows.</span><span class="sxs-lookup"><span data-stu-id="89a5a-112">The information in this article only applies to Windows-based HDInsight.</span></span> <span data-ttu-id="89a5a-113">Pour plus d’informations sur HDInsight sur Linux, consultez la rubrique [Activation des dumps de tas pour les services Hadoop sur HDInsight sur Linux](hdinsight-hadoop-collect-debug-heap-dump-linux.md)</span><span class="sxs-lookup"><span data-stu-id="89a5a-113">For information on Linux-based HDInsight, see [Enable heap dumps for Hadoop services on Linux-based HDInsight](hdinsight-hadoop-collect-debug-heap-dump-linux.md)</span></span>


## <a name="eligible-services-for-heap-dumps"></a><span data-ttu-id="89a5a-114">Services éligibles pour le vidage de tas</span><span class="sxs-lookup"><span data-stu-id="89a5a-114">Eligible services for heap dumps</span></span>
<span data-ttu-id="89a5a-115">Vous pouvez activer des dumps de tas pour les services suivants :</span><span class="sxs-lookup"><span data-stu-id="89a5a-115">You can enable heap dumps for the following services:</span></span>

* <span data-ttu-id="89a5a-116">**hcatalog** - tempelton</span><span class="sxs-lookup"><span data-stu-id="89a5a-116">**hcatalog** - tempelton</span></span>
* <span data-ttu-id="89a5a-117">**hive** - hiveserver2, metastore, derbyserver</span><span class="sxs-lookup"><span data-stu-id="89a5a-117">**hive** - hiveserver2, metastore, derbyserver</span></span>
* <span data-ttu-id="89a5a-118">**mapreduce** - jobhistoryserver</span><span class="sxs-lookup"><span data-stu-id="89a5a-118">**mapreduce** - jobhistoryserver</span></span>
* <span data-ttu-id="89a5a-119">**yarn** - resourcemanager, nodemanager, timelineserver</span><span class="sxs-lookup"><span data-stu-id="89a5a-119">**yarn** - resourcemanager, nodemanager, timelineserver</span></span>
* <span data-ttu-id="89a5a-120">**hdfs** - datanode, secondarynamenode, namenode</span><span class="sxs-lookup"><span data-stu-id="89a5a-120">**hdfs** - datanode, secondarynamenode, namenode</span></span>

## <a name="configuration-elements-that-enable-heap-dumps"></a><span data-ttu-id="89a5a-121">Éléments de configuration permettant d’activer le vidage de tas</span><span class="sxs-lookup"><span data-stu-id="89a5a-121">Configuration elements that enable heap dumps</span></span>
<span data-ttu-id="89a5a-122">Pour activer des dumps de tas sur un service, vous devez définir les éléments de configuration appropriés dans la section de ce service, qui est spécifié par **service_name**.</span><span class="sxs-lookup"><span data-stu-id="89a5a-122">To turn on heap dumps for a service, you need to set the appropriate configuration elements in the section for that service, which is specified by **service_name**.</span></span>

    "javaargs.<service_name>.XX:+HeapDumpOnOutOfMemoryError" = "-XX:+HeapDumpOnOutOfMemoryError",
    "javaargs.<service_name>.XX:HeapDumpPath" = "-XX:HeapDumpPath=c:\Dumps\<service_name>_%date:~4,2%%date:~7,2%%date:~10,2%%time:~0,2%%time:~3,2%%time:~6,2%.hprof"

<span data-ttu-id="89a5a-123">La valeur de **service_name** peut être l’un des services répertoriés ci-dessus : tempelton, hiveserver2, metastore, derbyserver, jobhistoryserver, resourcemanager, nodemanager, timelineserver, datanode, secondarynamenode ou namenode.</span><span class="sxs-lookup"><span data-stu-id="89a5a-123">The value of **service_name** can be any of the services listed here: tempelton, hiveserver2, metastore, derbyserver, jobhistoryserver, resourcemanager, nodemanager, timelineserver, datanode, secondarynamenode, or namenode.</span></span>

## <a name="enable-using-azure-powershell"></a><span data-ttu-id="89a5a-124">Activer à l’aide d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="89a5a-124">Enable using Azure PowerShell</span></span>
<span data-ttu-id="89a5a-125">Par exemple, pour activer les dumps de tas à l’aide d’Azure PowerShell pour jobhistoryserver, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="89a5a-125">For example, to turn on heap dumps by using Azure PowerShell for jobhistoryserver, you can use the following script:</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

    $MapRedConfigValues = new-object 'Microsoft.WindowsAzure.Management.HDInsight.Cmdlet.DataObjects.AzureHDInsightMapReduceConfiguration'

    $MapRedConfigValues.Configuration = @{ "javaargs.jobhistoryserver.XX:+HeapDumpOnOutOfMemoryError"="-XX:+HeapDumpOnOutOfMemoryError" ; "javaargs.jobhistoryserver.XX:HeapDumpPath" = "-XX:HeapDumpPath=c:\\Dumps\\jobhistoryserver_%date:~4,2%_%date:~7,2%_%date:~10,2%_%time:~0,2%_%time:~3,2%_%time:~6,2%.hprof" }

## <a name="enable-using-net-sdk"></a><span data-ttu-id="89a5a-126">Activer avec le kit de développement logiciel (SDK) .NET</span><span class="sxs-lookup"><span data-stu-id="89a5a-126">Enable using .NET SDK</span></span>
<span data-ttu-id="89a5a-127">Par exemple, pour activer les dumps de tas à l’aide du Kit de développement logiciel (SDK) Azure HDInsight .NET pour jobhistoryserver, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="89a5a-127">For example, to turn on heap dumps by using the Azure HDInsight .NET SDK for jobhistoryserver, you can use the following code:</span></span>

    clusterInfo.MapReduceConfiguration.ConfigurationCollection.Add(new KeyValuePair<string, string>("javaargs.jobhistoryserver.XX:+HeapDumpOnOutOfMemoryError", "-XX:+HeapDumpOnOutOfMemoryError"));

    clusterInfo.MapReduceConfiguration.ConfigurationCollection.Add(new KeyValuePair<string, string>("javaargs.jobhistoryserver.XX:HeapDumpPath", "-XX:HeapDumpPath=c:\\Dumps\\jobhistoryserver_%date:~4,2%_%date:~7,2%_%date:~10,2%_%time:~0,2%_%time:~3,2%_%time:~6,2%.hprof"));
