---
title: "Envoi de tâches Hadoop dans HDInsight | Microsoft Docs"
description: "Apprenez à envoyer des tâches Hadoop à Azure HDInsight Hadoop."
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
ms.assetid: 50430b96-2329-4775-9713-19c5795b775f
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 6829ff82afc7fcea9e027ad14ec7ed0c8015a5fe
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="submit-hadoop-jobs-in-hdinsight"></a><span data-ttu-id="2e2a1-103">Envoi de tâches Hadoop dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="2e2a1-103">Submit Hadoop jobs in HDInsight</span></span>

<span data-ttu-id="2e2a1-104">Vous pouvez envoyer des travaux Hadoop à l’aide du Kit de développement logiciel (SDK) .NET, de Curl et d’Azure PowerShell :</span><span class="sxs-lookup"><span data-stu-id="2e2a1-104">You can submit Hadoop jobs using .NET SDK, Curl, and Azure PowerShell:</span></span>

- <span data-ttu-id="2e2a1-105">Utilisation du Kit de développement logiciel (SDK) .NET</span><span class="sxs-lookup"><span data-stu-id="2e2a1-105">Use .NET SDK</span></span>

  - [<span data-ttu-id="2e2a1-106">Créer des applications .NET d’authentification non interactives</span><span class="sxs-lookup"><span data-stu-id="2e2a1-106">Create non-interactive authentication .NET applications</span></span>](hdinsight-create-non-interactive-authentication-dotnet-applications.md)
  - [<span data-ttu-id="2e2a1-107">Exécuter des requêtes Hive avec le Kit de développement logiciel (SDK) .NET HDInsight</span><span class="sxs-lookup"><span data-stu-id="2e2a1-107">Run Hive queries using HDInsight .NET SDK</span></span>](hdinsight-hadoop-use-hive-dotnet-sdk.md)
  - [<span data-ttu-id="2e2a1-108">Exécuter des travaux Pig à l’aide du Kit de développement logiciel (SDK) .NET pour Hadoop dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="2e2a1-108">Run Pig jobs using the .NET SDK for Hadoop in HDInsight</span></span>](hdinsight-hadoop-use-pig-dotnet-sdk.md)
  - [<span data-ttu-id="2e2a1-109">Exécuter des travaux Sqoop à l’aide du Kit de développement logiciel (SDK) .NET pour Hadoop dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="2e2a1-109">Run Sqoop jobs using .NET SDK for Hadoop in HDInsight</span></span>](hdinsight-hadoop-use-sqoop-dotnet-sdk.md)
  - [<span data-ttu-id="2e2a1-110">Exécuter des travaux MapReduce avec le Kit de développement logiciel (SDK) .NET HDInsight</span><span class="sxs-lookup"><span data-stu-id="2e2a1-110">Run MapReduce jobs using HDInsight .NET SDK</span></span>](hdinsight-hadoop-use-mapreduce-dotnet-sdk.md)

- <span data-ttu-id="2e2a1-111">CURL</span><span class="sxs-lookup"><span data-stu-id="2e2a1-111">CURL</span></span>

  - [<span data-ttu-id="2e2a1-112">Exécuter des requêtes Hive avec Hadoop dans HDInsight via Curl</span><span class="sxs-lookup"><span data-stu-id="2e2a1-112">Run Hive queries with Hadoop in HDInsight with Curl</span></span>](hdinsight-hadoop-use-hive-curl.md)
  - [<span data-ttu-id="2e2a1-113">Exécuter des travaux Pig avec Hadoop sur HDInsight à l’aide de Curl</span><span class="sxs-lookup"><span data-stu-id="2e2a1-113">Run Pig jobs with Hadoop on HDInsight by using Curl</span></span>](hdinsight-hadoop-use-pig-curl.md)
  - [<span data-ttu-id="2e2a1-114">Exécuter des travaux Sqoop avec Hadoop dans HDInsight via Curl</span><span class="sxs-lookup"><span data-stu-id="2e2a1-114">Run Sqoop jobs with Hadoop in HDInsight with Curl</span></span>](hdinsight-hadoop-use-sqoop-curl.md)
  - [<span data-ttu-id="2e2a1-115">Exécuter des travaux MapReduce avec Hadoop sur HDInsight à l’aide de Curl</span><span class="sxs-lookup"><span data-stu-id="2e2a1-115">Run MapReduce jobs with Hadoop on HDInsight using Curl</span></span>](hdinsight-hadoop-use-mapreduce-curl.md)

- <span data-ttu-id="2e2a1-116">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2e2a1-116">PowerShell</span></span>

  - [<span data-ttu-id="2e2a1-117">Exécuter des requêtes Hive avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="2e2a1-117">Run Hive queries using PowerShell</span></span>](hdinsight-hadoop-use-hive-powershell.md)
  - [<span data-ttu-id="2e2a1-118">Exécuter des travaux Pig avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="2e2a1-118">Run Pig jobs using PowerShell</span></span>](hdinsight-hadoop-use-pig-powershell.md)
  - [<span data-ttu-id="2e2a1-119">Utiliser Sqoop avec Hadoop dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="2e2a1-119">Use Sqoop with Hadoop in HDInsight</span></span>](hdinsight-hadoop-use-sqoop-powershell.md)
  - [<span data-ttu-id="2e2a1-120">Exécuter des travaux MapReduce avec Hadoop sur HDInsight à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="2e2a1-120">Run MapReduce jobs with Hadoop on HDInsight using PowerShell</span></span>](hdinsight-hadoop-use-mapreduce-powershell.md)

## <a name="see-also"></a><span data-ttu-id="2e2a1-121">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="2e2a1-121">See also</span></span>

- [<span data-ttu-id="2e2a1-122">Documentation Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="2e2a1-122">Azure HDInsight Documentation</span></span>](https://docs.microsoft.com/azure/hdinsight/)