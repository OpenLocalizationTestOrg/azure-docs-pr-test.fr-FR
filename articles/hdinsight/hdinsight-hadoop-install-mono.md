---
title: "Installer ou mettre à jour Mono sur HDInsight - Azure | Microsoft Docs"
description: "Découvrez comment utiliser une version particulière de Mono avec le cluster HDInsight. Mono permet d’exécuter des applications .NET sur des clusters HDInsight sous Linux."
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
ms.openlocfilehash: fd284542e1de65f323f1e3a092689f847e025be6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="install-or-update-mono-on-hdinsight"></a><span data-ttu-id="be80a-104">Installation ou mise à jour de Mono sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="be80a-104">Install or update Mono on HDInsight</span></span>

<span data-ttu-id="be80a-105">Apprenez à installer une version spécifique de [Mono](https://www.mono-project.com) sur HDInsight 3.4 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="be80a-105">Learn how to install a specific version of [Mono](https://www.mono-project.com) on HDInsight 3.4 or higher.</span></span>

<span data-ttu-id="be80a-106">Mono est installé sur HDInsight 3.4 et versions ultérieures et est utilisé pour exécuter des applications .NET.</span><span class="sxs-lookup"><span data-stu-id="be80a-106">Mono is installed on HDInsight 3.4 and higher, and is used to run .NET applications.</span></span> <span data-ttu-id="be80a-107">Pour plus d’informations sur la version de Mono fournie avec chaque version d’HDInsight, consultez [Contrôle de version des composants HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="be80a-107">For information on the version of Mono included with each HDInsight version, see [HDInsight component versioning](hdinsight-component-versioning.md).</span></span> <span data-ttu-id="be80a-108">Pour installer une autre version sur votre cluster, utilisez l’action de script de ce document.</span><span class="sxs-lookup"><span data-stu-id="be80a-108">To install a different version on your cluster, use the script action in this document.</span></span> 

## <a name="how-it-works"></a><span data-ttu-id="be80a-109">Fonctionnement</span><span class="sxs-lookup"><span data-stu-id="be80a-109">How it works</span></span>

<span data-ttu-id="be80a-110">Le script accepte les paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="be80a-110">This script accepts the following parameter:</span></span>

* <span data-ttu-id="be80a-111">__Mono version number__ (Numéro de version de Mono) : la version de Mono à installer.</span><span class="sxs-lookup"><span data-stu-id="be80a-111">__Mono version number__: The version of Mono to install.</span></span> <span data-ttu-id="be80a-112">La version doit être disponible à partir de [https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/](https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/).</span><span class="sxs-lookup"><span data-stu-id="be80a-112">The version must be available from [https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/](https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/).</span></span>

<span data-ttu-id="be80a-113">Le script installe les packages Mono suivants :</span><span class="sxs-lookup"><span data-stu-id="be80a-113">The script installs the following Mono packages:</span></span>

* <span data-ttu-id="be80a-114">__mono-complete__</span><span class="sxs-lookup"><span data-stu-id="be80a-114">__mono-complete__</span></span>

* <span data-ttu-id="be80a-115">__ca-certificates-mono__</span><span class="sxs-lookup"><span data-stu-id="be80a-115">__ca-certificates-mono__</span></span>

## <a name="the-script"></a><span data-ttu-id="be80a-116">Le script</span><span class="sxs-lookup"><span data-stu-id="be80a-116">The script</span></span>

<span data-ttu-id="be80a-117">__Emplacement du script__ : [https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash](https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash)</span><span class="sxs-lookup"><span data-stu-id="be80a-117">__Script location__: [https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash](https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash)</span></span>

<span data-ttu-id="be80a-118">__Conditions requises__ :</span><span class="sxs-lookup"><span data-stu-id="be80a-118">__Requirements__:</span></span>

* <span data-ttu-id="be80a-119">Le script doit être appliqué sur les __nœuds principaux__ et les __nœuds de travail__.</span><span class="sxs-lookup"><span data-stu-id="be80a-119">The script must be applied on the __head nodes__ and __worker nodes__.</span></span>

## <a name="to-use-the-script"></a><span data-ttu-id="be80a-120">Pour utiliser le script</span><span class="sxs-lookup"><span data-stu-id="be80a-120">To use the script</span></span>

<span data-ttu-id="be80a-121">Pour plus d’informations sur l’utilisation de ce script avec HDInsight, consultez le document [Personnalisation de clusters HDInsight basés sur Linux à l'aide d'une action de script](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster).</span><span class="sxs-lookup"><span data-stu-id="be80a-121">For information on how to use this script with HDInsight, see the [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster) document.</span></span> <span data-ttu-id="be80a-122">Vous pouvez utiliser le script avec le portail Azure, Azure PowerShell ou l’interface de ligne de commande Azure.</span><span class="sxs-lookup"><span data-stu-id="be80a-122">You can use the script through the Azure portal, Azure PowerShell, or the Azure CLI.</span></span>

<span data-ttu-id="be80a-123">Tout en respectant le document d’action de script, utilisez l’URI suivant :</span><span class="sxs-lookup"><span data-stu-id="be80a-123">While following the script action document, use the following URI:</span></span>

    https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash

> [!NOTE]
> <span data-ttu-id="be80a-124">Lorsque vous configurez HDInsight avec ce script, définissez le script sur le statut __Persisted__ (Persistant).</span><span class="sxs-lookup"><span data-stu-id="be80a-124">When configuring HDInsight with this script, mark the script as __Persisted__.</span></span> <span data-ttu-id="be80a-125">Ce paramètre permet à HDInsight d’appliquer le script aux nœuds de travail ajoutés par les opérations de mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="be80a-125">This setting allows HDInsight to apply the script to worker nodes added through scaling operations.</span></span>


## <a name="next-steps"></a><span data-ttu-id="be80a-126">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="be80a-126">Next steps</span></span>

<span data-ttu-id="be80a-127">Vous avez appris à mettre à niveau ou installer une version particulière de Mono sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="be80a-127">You have learned how to upgrade or install a specific version of Mono on HDInsight.</span></span> <span data-ttu-id="be80a-128">Pour plus d’informations sur l’utilisation des applications .NET avec Mono sur HDInsight, consultez les documents suivants :</span><span class="sxs-lookup"><span data-stu-id="be80a-128">For more information on using .NET applications with Mono on HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="be80a-129">Utilisation de .NET pour la diffusion MapReduce sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="be80a-129">Use .NET for streaming MapReduce on HDInsight</span></span>](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md)
* [<span data-ttu-id="be80a-130">Utilisation de .NET avec Hive et Pig sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="be80a-130">Use .NET with Hive and Pig on HDInsight</span></span>](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)
* [<span data-ttu-id="be80a-131">Développement de solutions C# avec Storm sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="be80a-131">Develop C# solutions with Storm on HDInsight</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)
* [<span data-ttu-id="be80a-132">Migration de solutions .NET vers une version d’HDInsight pour Linux</span><span class="sxs-lookup"><span data-stu-id="be80a-132">Migrate .NET solutions to Linux-based HDInsight</span></span>](hdinsight-hadoop-migrate-dotnet-to-linux.md)

<span data-ttu-id="be80a-133">Pour plus d’informations sur l’utilisation des actions de script, consultez [Personnalisation de clusters HDInsight basés sur Linux à l’aide d’une d’action de script](hdinsight-hadoop-customize-cluster-linux.md)</span><span class="sxs-lookup"><span data-stu-id="be80a-133">For more information on using script actions, see [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md)</span></span>