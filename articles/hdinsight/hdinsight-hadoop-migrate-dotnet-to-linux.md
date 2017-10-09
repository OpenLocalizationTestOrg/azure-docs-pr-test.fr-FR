---
title: "aaaUse .NET avec Hadoop MapReduce dans HDInsight basés sur Linux - Azure | Documents Microsoft"
description: "Découvrez comment les applications .NET toouse de diffusion en continu MapReduce sur HDInsight de basés sur Linux."
services: hdinsight
documentationCenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 5a4e6dc1b4dafa8cc40780e3371fa4b8ba3e3d48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-net-solutions-for-windows-based-hdinsight-toolinux-based-hdinsight"></a><span data-ttu-id="c2162-103">Migrer des solutions .NET pour HDInsight de basés sur Windows basée sur les tooLinux de HDInsight</span><span class="sxs-lookup"><span data-stu-id="c2162-103">Migrate .NET solutions for Windows-based HDInsight tooLinux-based HDInsight</span></span>

<span data-ttu-id="c2162-104">Utilisation des clusters basés sur Linux de HDInsight [Mono (https://mono-project.com)](https://mono-project.com) toorun les applications .NET.</span><span class="sxs-lookup"><span data-stu-id="c2162-104">Linux-based HDInsight clusters use [Mono (https://mono-project.com)](https://mono-project.com) toorun .NET applications.</span></span> <span data-ttu-id="c2162-105">Mono vous permet de composants de .NET toouse telles que les applications MapReduce hdinsight de basés sur Linux.</span><span class="sxs-lookup"><span data-stu-id="c2162-105">Mono allows you toouse .NET components such as MapReduce applications with Linux-based HDInsight.</span></span> <span data-ttu-id="c2162-106">Dans ce document, découvrez comment les solutions de .NET toomigrate créé pour toowork des clusters basés sur Windows de HDInsight avec Mono sur HDInsight de basés sur Linux.</span><span class="sxs-lookup"><span data-stu-id="c2162-106">In this document, learn how toomigrate .NET solutions created for Windows-based HDInsight clusters toowork with Mono on Linux-based HDInsight.</span></span>

## <a name="mono-compatibility-with-net"></a><span data-ttu-id="c2162-107">Compatibilité de Mono avec .NET</span><span class="sxs-lookup"><span data-stu-id="c2162-107">Mono compatibility with .NET</span></span>

<span data-ttu-id="c2162-108">La version 4.2.1 de Mono est incluse dans la version 3.5 de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c2162-108">Mono version 4.2.1 is included with HDInsight version 3.5.</span></span> <span data-ttu-id="c2162-109">Pour plus d’informations sur la version de hello de Mono inclus avec HDInsight, consultez [versions des composants HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="c2162-109">For more information on hello version of Mono included with HDInsight, see [HDInsight component versions](hdinsight-component-versioning.md).</span></span> <span data-ttu-id="c2162-110">tooinstall une version spécifique de Mono, consultez hello [installation ou mise à jour Mono](hdinsight-hadoop-install-mono.md) document.</span><span class="sxs-lookup"><span data-stu-id="c2162-110">tooinstall a specific version of Mono, see hello [Install or update Mono](hdinsight-hadoop-install-mono.md) document.</span></span>

<span data-ttu-id="c2162-111">Pour plus d’informations sur la compatibilité entre Mono et .NET, consultez hello [compatibilité Mono (http://www.mono-project.com/docs/about-mono/compatibility/)](http://www.mono-project.com/docs/about-mono/compatibility/) document.</span><span class="sxs-lookup"><span data-stu-id="c2162-111">For detailed information on compatibility between Mono and .NET, see hello [Mono compatibility (http://www.mono-project.com/docs/about-mono/compatibility/)](http://www.mono-project.com/docs/about-mono/compatibility/) document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c2162-112">infrastructure SCP.NET Hello est compatible avec Mono.</span><span class="sxs-lookup"><span data-stu-id="c2162-112">hello SCP.NET framework is compatible with Mono.</span></span> <span data-ttu-id="c2162-113">Pour plus d’informations sur l’utilisation de SCP.NET avec Mono, consultez [topologies de toodevelop C# utilisez Visual Studio d’Apache Storm sur HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="c2162-113">For more information on using SCP.NET with Mono, see [Use Visual Studio toodevelop C# topologies for Apache Storm on HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

## <a name="automated-portability-analysis"></a><span data-ttu-id="c2162-114">Analyse de portabilité automatisée</span><span class="sxs-lookup"><span data-stu-id="c2162-114">Automated portability analysis</span></span>

<span data-ttu-id="c2162-115">Hello [Analyseur de portabilité .NET](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer) peut être utilisé toogenerate un rapport des incompatibilités entre votre application et de Mono.</span><span class="sxs-lookup"><span data-stu-id="c2162-115">hello [.NET Portability Analyzer](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer) can be used toogenerate a report of incompatibilities between your application and Mono.</span></span> <span data-ttu-id="c2162-116">Utilisez hello suivant les étapes tooconfigure hello analyseur toocheck votre application pour une portabilité Mono :</span><span class="sxs-lookup"><span data-stu-id="c2162-116">Use hello following steps tooconfigure hello analyzer toocheck your application for Mono portability:</span></span>

1. <span data-ttu-id="c2162-117">Installer hello [Analyseur de portabilité .NET](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer).</span><span class="sxs-lookup"><span data-stu-id="c2162-117">Install hello [.NET Portability Analyzer](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer).</span></span> <span data-ttu-id="c2162-118">Pendant l’installation, sélectionnez la version hello de toouse de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c2162-118">During installation, select hello version of Visual Studio toouse.</span></span>

2. <span data-ttu-id="c2162-119">À partir de Visual Studio 2015, sélectionnez __analyser__ > __paramètres d’analyseur de portabilité__et vous assurer que __4.5__ est archivé hello __Mono__  section.</span><span class="sxs-lookup"><span data-stu-id="c2162-119">From Visual Studio 2015, select __Analyze__ > __Portability Analyzer Settings__, and make sure that __4.5__ is checked in hello __Mono__ section.</span></span>

    ![4.5 archivé Mono section pour les paramètres d’analyseur hello](./media/hdinsight-hadoop-migrate-dotnet-to-linux/portability-analyzer-settings.png)

    <span data-ttu-id="c2162-121">Sélectionnez __OK__ configuration de hello toosave.</span><span class="sxs-lookup"><span data-stu-id="c2162-121">Select __OK__ toosave hello configuration.</span></span>

3. <span data-ttu-id="c2162-122">Sélectionnez __Analyser__ > __Analyser la portabilité d’Assembly__.</span><span class="sxs-lookup"><span data-stu-id="c2162-122">Select __Analyze__ > __Analyze Assembly Portability__.</span></span> <span data-ttu-id="c2162-123">Sélectionnez assembly hello qui contient votre solution, puis __ouvrir__ toobegin analyse.</span><span class="sxs-lookup"><span data-stu-id="c2162-123">Select hello assembly that contains your solution, and then select __Open__ toobegin analysis.</span></span>

4. <span data-ttu-id="c2162-124">Une fois l’analyse terminée, sélectionnez __Analyser__ > __Afficher les rapports d’analyse__.</span><span class="sxs-lookup"><span data-stu-id="c2162-124">Once analysis is complete, select __Analyze__ > __View analysis reports__.</span></span> <span data-ttu-id="c2162-125">Dans __résultats de l’analyse portabilité__, sélectionnez __ouvrir rapport__ tooopen un rapport.</span><span class="sxs-lookup"><span data-stu-id="c2162-125">In __Portability Analysis Results__, select __Open report__ tooopen a report.</span></span>

    ![Boîte de dialogue des résultats de l’analyseur de portabilité](./media/hdinsight-hadoop-migrate-dotnet-to-linux/portability-analyzer-results.png)

> [!IMPORTANT]
> <span data-ttu-id="c2162-127">Analyseur de Hello ne peut pas intercepter tous les problèmes avec votre solution.</span><span class="sxs-lookup"><span data-stu-id="c2162-127">hello analyzer cannot catch every problem with your solution.</span></span> <span data-ttu-id="c2162-128">Par exemple, un chemin de fichier de `c:\temp\file.txt` est considéré comme OK car Mono s’exécute sur Windows et le chemin d’accès de hello est valide dans ce contexte.</span><span class="sxs-lookup"><span data-stu-id="c2162-128">For example, a file path of `c:\temp\file.txt` is considered OK because Mono runs on Windows and hello path is valid in that context.</span></span> <span data-ttu-id="c2162-129">Toutefois, le chemin d’accès hello n’est pas valide sur une plate-forme Linux.</span><span class="sxs-lookup"><span data-stu-id="c2162-129">However, hello path is not valid on a Linux platform.</span></span>

## <a name="manual-portability-analysis"></a><span data-ttu-id="c2162-130">Analyse de portabilité manuelle</span><span class="sxs-lookup"><span data-stu-id="c2162-130">Manual portability analysis</span></span>

<span data-ttu-id="c2162-131">Effectuer un audit manuel de votre code à l’aide des informations de hello Bonjour [la portabilité des applications (http://www.mono-project.com/docs/getting-started/application-portability/)](http://www.mono-project.com/docs/getting-started/application-portability/) document.</span><span class="sxs-lookup"><span data-stu-id="c2162-131">Perform a manual audit of your code using hello information in hello [Application Portability (http://www.mono-project.com/docs/getting-started/application-portability/)](http://www.mono-project.com/docs/getting-started/application-portability/) document.</span></span>

## <a name="modify-and-build"></a><span data-ttu-id="c2162-132">Modifier et générer</span><span class="sxs-lookup"><span data-stu-id="c2162-132">Modify and build</span></span>

<span data-ttu-id="c2162-133">Vous pouvez continuer à toouse Visual Studio toobuild vos solutions .NET pour HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c2162-133">You can continue toouse Visual Studio toobuild your .NET solutions for HDInsight.</span></span> <span data-ttu-id="c2162-134">Toutefois, vous devez vérifier que ce projet hello est configuré toouse .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="c2162-134">However, you must ensure that hello project is configured toouse .NET Framework 4.5.</span></span>

## <a name="deploy-and-test"></a><span data-ttu-id="c2162-135">Déploiement et test</span><span class="sxs-lookup"><span data-stu-id="c2162-135">Deploy and test</span></span>

<span data-ttu-id="c2162-136">Une fois que vous avez modifié votre solution à l’aide de recommandations hello à partir de hello Analyseur de portabilité .NET ou d’une analyse manuelle, vous devez la tester avec HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c2162-136">Once you have modified your solution using hello recommendations from hello .NET Portability Analyzer or from a manual analysis, you must test it with HDInsight.</span></span> <span data-ttu-id="c2162-137">Test de solution hello sur un cluster HDInsight de basés sur Linux peut révéler des problèmes subtils toobe corrigé.</span><span class="sxs-lookup"><span data-stu-id="c2162-137">Testing hello solution on a Linux-based HDInsight cluster may reveal subtle problems that need toobe corrected.</span></span> <span data-ttu-id="c2162-138">Nous vous recommandons d’activer la fonction de journalisation supplémentaire dans votre application lors de son test.</span><span class="sxs-lookup"><span data-stu-id="c2162-138">We recommend that you enable additional logging in your application while testing it.</span></span>

<span data-ttu-id="c2162-139">Pour plus d’informations sur l’accès aux journaux, consultez hello suivant des documents :</span><span class="sxs-lookup"><span data-stu-id="c2162-139">For more information on accessing logs, see hello following documents:</span></span>

* [<span data-ttu-id="c2162-140">Accéder aux journaux des applications YARN dans HDInsight sous Linux</span><span class="sxs-lookup"><span data-stu-id="c2162-140">Access YARN application logs on Linux-based HDInsight</span></span>](hdinsight-hadoop-access-yarn-app-logs-linux.md)

## <a name="next-steps"></a><span data-ttu-id="c2162-141">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c2162-141">Next steps</span></span>

* [<span data-ttu-id="c2162-142">Utilisation de C# avec MapReduce dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="c2162-142">Use C# with MapReduce on HDInsight</span></span>](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md)

* [<span data-ttu-id="c2162-143">Utilisation des fonctions définies par l’utilisateur C# avec Hive et Pig</span><span class="sxs-lookup"><span data-stu-id="c2162-143">Use C# user defined functions with Hive and Pig</span></span>](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

* [<span data-ttu-id="c2162-144">Développement de topologies C# pour Storm sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="c2162-144">Develop C# topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)