---
title: "aaaInstall ou mettre à jour Mono sur HDInsight - Azure | Documents Microsoft"
description: "Découvrez comment toouse une version spécifique de Mono avec le cluster HDInsight. Mono est utilisé toorun .NET applications sur les clusters HDInsight de basés sur Linux."
services: hdinsight
documentationCenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.custom: hdinsightactive
ms.openlocfilehash: 1e8a8aaeff231c93a9e232379448517b326da965
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="install-or-update-mono-on-hdinsight"></a><span data-ttu-id="81e68-104">Installation ou mise à jour de Mono sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="81e68-104">Install or update Mono on HDInsight</span></span>

<span data-ttu-id="81e68-105">Découvrez comment tooinstall une version spécifique de [Mono](https://www.mono-project.com) dans HDInsight 3.4 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="81e68-105">Learn how tooinstall a specific version of [Mono](https://www.mono-project.com) on HDInsight 3.4 or higher.</span></span>

<span data-ttu-id="81e68-106">Mono est installé sur HDInsight 3.4 et versions ultérieures et est utilisé toorun applications .NET.</span><span class="sxs-lookup"><span data-stu-id="81e68-106">Mono is installed on HDInsight 3.4 and higher, and is used toorun .NET applications.</span></span> <span data-ttu-id="81e68-107">Pour plus d’informations sur la version de hello de Mono inclus avec chaque version de HDInsight, consultez [le contrôle de version HDInsight composant](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="81e68-107">For information on hello version of Mono included with each HDInsight version, see [HDInsight component versioning](hdinsight-component-versioning.md).</span></span> <span data-ttu-id="81e68-108">tooinstall une version différente sur votre cluster, utilisez hello script action dans ce document.</span><span class="sxs-lookup"><span data-stu-id="81e68-108">tooinstall a different version on your cluster, use hello script action in this document.</span></span> 

## <a name="how-it-works"></a><span data-ttu-id="81e68-109">Fonctionnement</span><span class="sxs-lookup"><span data-stu-id="81e68-109">How it works</span></span>

<span data-ttu-id="81e68-110">Ce script accepte hello suivant paramètre :</span><span class="sxs-lookup"><span data-stu-id="81e68-110">This script accepts hello following parameter:</span></span>

* <span data-ttu-id="81e68-111">__Numéro de version mono__: version hello de tooinstall Mono.</span><span class="sxs-lookup"><span data-stu-id="81e68-111">__Mono version number__: hello version of Mono tooinstall.</span></span> <span data-ttu-id="81e68-112">version de Hello doit être disponible à partir de [https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/](https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/).</span><span class="sxs-lookup"><span data-stu-id="81e68-112">hello version must be available from [https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/](https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/).</span></span>

<span data-ttu-id="81e68-113">script de Hello installe hello suivant Mono packages :</span><span class="sxs-lookup"><span data-stu-id="81e68-113">hello script installs hello following Mono packages:</span></span>

* <span data-ttu-id="81e68-114">__mono-complete__</span><span class="sxs-lookup"><span data-stu-id="81e68-114">__mono-complete__</span></span>

* <span data-ttu-id="81e68-115">__ca-certificates-mono__</span><span class="sxs-lookup"><span data-stu-id="81e68-115">__ca-certificates-mono__</span></span>

## <a name="hello-script"></a><span data-ttu-id="81e68-116">script de Hello</span><span class="sxs-lookup"><span data-stu-id="81e68-116">hello script</span></span>

<span data-ttu-id="81e68-117">__Emplacement du script__ : [https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash](https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash)</span><span class="sxs-lookup"><span data-stu-id="81e68-117">__Script location__: [https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash](https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash)</span></span>

<span data-ttu-id="81e68-118">__Conditions requises__ :</span><span class="sxs-lookup"><span data-stu-id="81e68-118">__Requirements__:</span></span>

* <span data-ttu-id="81e68-119">script de Hello doit être appliquée sur hello __head nœuds__ et __nœuds worker__.</span><span class="sxs-lookup"><span data-stu-id="81e68-119">hello script must be applied on hello __head nodes__ and __worker nodes__.</span></span>

## <a name="toouse-hello-script"></a><span data-ttu-id="81e68-120">script de hello toouse</span><span class="sxs-lookup"><span data-stu-id="81e68-120">toouse hello script</span></span>

<span data-ttu-id="81e68-121">Pour plus d’informations sur comment toouse ce script avec HDInsight, consultez hello [HDInsight de basés sur Linux de personnaliser des clusters à l’aide d’action de script](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster) document.</span><span class="sxs-lookup"><span data-stu-id="81e68-121">For information on how toouse this script with HDInsight, see hello [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster) document.</span></span> <span data-ttu-id="81e68-122">Vous pouvez utiliser le script hello via hello portail Azure, Azure PowerShell, ou hello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="81e68-122">You can use hello script through hello Azure portal, Azure PowerShell, or hello Azure CLI.</span></span>

<span data-ttu-id="81e68-123">Alors que suit hello document d’action de script, utilisez hello suivant l’URI :</span><span class="sxs-lookup"><span data-stu-id="81e68-123">While following hello script action document, use hello following URI:</span></span>

    https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash

> [!NOTE]
> <span data-ttu-id="81e68-124">Lors de la configuration HDInsight avec ce script, sélectionnez script hello en tant que __Persisted__.</span><span class="sxs-lookup"><span data-stu-id="81e68-124">When configuring HDInsight with this script, mark hello script as __Persisted__.</span></span> <span data-ttu-id="81e68-125">Ce paramètre permet de nœuds de tooworker script hello ajoutées via les opérations de mise à l’échelle HDInsight tooapply.</span><span class="sxs-lookup"><span data-stu-id="81e68-125">This setting allows HDInsight tooapply hello script tooworker nodes added through scaling operations.</span></span>


## <a name="next-steps"></a><span data-ttu-id="81e68-126">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="81e68-126">Next steps</span></span>

<span data-ttu-id="81e68-127">Vous avez appris comment tooupgrade ou installez une version spécifique de Mono sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="81e68-127">You have learned how tooupgrade or install a specific version of Mono on HDInsight.</span></span> <span data-ttu-id="81e68-128">Pour plus d’informations sur l’utilisation des applications .NET avec Mono sur HDInsight, consultez hello suivant des documents :</span><span class="sxs-lookup"><span data-stu-id="81e68-128">For more information on using .NET applications with Mono on HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="81e68-129">Utilisation de .NET pour la diffusion MapReduce sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="81e68-129">Use .NET for streaming MapReduce on HDInsight</span></span>](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md)
* [<span data-ttu-id="81e68-130">Utilisation de .NET avec Hive et Pig sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="81e68-130">Use .NET with Hive and Pig on HDInsight</span></span>](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)
* [<span data-ttu-id="81e68-131">Développement de solutions C# avec Storm sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="81e68-131">Develop C# solutions with Storm on HDInsight</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)
* [<span data-ttu-id="81e68-132">Migrer des solutions .NET basée sur tooLinux de HDInsight</span><span class="sxs-lookup"><span data-stu-id="81e68-132">Migrate .NET solutions tooLinux-based HDInsight</span></span>](hdinsight-hadoop-migrate-dotnet-to-linux.md)

<span data-ttu-id="81e68-133">Pour plus d’informations sur l’utilisation des actions de script, consultez [Personnalisation de clusters HDInsight basés sur Linux à l’aide d’une d’action de script](hdinsight-hadoop-customize-cluster-linux.md)</span><span class="sxs-lookup"><span data-stu-id="81e68-133">For more information on using script actions, see [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md)</span></span>