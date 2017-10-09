---
title: topologies de Storm aaaApache avec Visual Studio et c# - Azure HDInsight | Documents Microsoft
description: "Découvrez comment les topologies Storm toocreate en c#. Créer une topologie de nombre simple word dans Visual Studio à l’aide des outils de Hadoop hello pour Visual Studio."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 380d804f-a8c5-4b20-9762-593ec4da5a0d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/02/2017
ms.author: larryfr
ms.openlocfilehash: b3fb01a4dda144fd7fb4141e624e31e667f93753
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-c-topologies-for-apache-storm-by-using-hello-data-lake-tools-for-visual-studio"></a><span data-ttu-id="d2b9d-104">Développer des topologies c# pour Visual Studio à l’aide des outils de Data Lake hello d’Apache Storm</span><span class="sxs-lookup"><span data-stu-id="d2b9d-104">Develop C# topologies for Apache Storm by using hello Data Lake tools for Visual Studio</span></span>

<span data-ttu-id="d2b9d-105">Découvrez comment toocreate une topologie c# Storm à l’aide de hello Azure Data Lake (Hadoop) des outils pour Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-105">Learn how toocreate a C# Storm topology by using hello Azure Data Lake (Hadoop) tools for Visual Studio.</span></span> <span data-ttu-id="d2b9d-106">Ce document décrit hello processus de création d’un projet de Storm dans Visual Studio, tester localement et son déploiement tooan Apache Storm sur cluster Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-106">This document walks through hello process of creating a Storm project in Visual Studio, testing it locally, and deploying it tooan Apache Storm on Azure HDInsight cluster.</span></span>

<span data-ttu-id="d2b9d-107">Vous apprendrez également comment les topologies toocreate hybride qui utilisent des composants de c# et Java.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-107">You also learn how toocreate hybrid topologies that use C# and Java components.</span></span>

> [!NOTE]
> <span data-ttu-id="d2b9d-108">Étapes hello dans ce document reposent sur un environnement de développement Windows avec Visual Studio, projet compilé de hello sont soumis tooeither un cluster HDInsight de basés sur Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-108">While hello steps in this document rely on a Windows development environment with Visual Studio, hello compiled project can be submitted tooeither a Linux or Windows-based HDInsight cluster.</span></span> <span data-ttu-id="d2b9d-109">Seuls les clusters basés sur Linux créés après le 28 octobre 2016 prennent en charge les topologies SCP.NET.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-109">Only Linux-based clusters created after October 28, 2016, support SCP.NET topologies.</span></span>

<span data-ttu-id="d2b9d-110">topologie toouse c# avec un cluster basé sur Linux, vous devez mettre à jour hello Microsoft.SCP.Net.SDK NuGet package utilisé par votre projet de tooversion 0.10.0.6 ou version ultérieur.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-110">toouse a C# topology with a Linux-based cluster, you must update hello Microsoft.SCP.Net.SDK NuGet package used by your project tooversion 0.10.0.6 or later.</span></span> <span data-ttu-id="d2b9d-111">version Hello du package de hello doit également correspondre version majeure de hello de Storm installé sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-111">hello version of hello package must also match hello major version of Storm installed on HDInsight.</span></span>

| <span data-ttu-id="d2b9d-112">Version de HDInsight</span><span class="sxs-lookup"><span data-stu-id="d2b9d-112">HDInsight version</span></span> | <span data-ttu-id="d2b9d-113">Version de Storm</span><span class="sxs-lookup"><span data-stu-id="d2b9d-113">Storm version</span></span> | <span data-ttu-id="d2b9d-114">Version de SCP.NET</span><span class="sxs-lookup"><span data-stu-id="d2b9d-114">SCP.NET version</span></span> | <span data-ttu-id="d2b9d-115">Version Mono par défaut</span><span class="sxs-lookup"><span data-stu-id="d2b9d-115">Default Mono version</span></span> |
|:-----------------:|:-------------:|:---------------:|:--------------------:|
| <span data-ttu-id="d2b9d-116">3.3</span><span class="sxs-lookup"><span data-stu-id="d2b9d-116">3.3</span></span> |<span data-ttu-id="d2b9d-117">0.10.x</span><span class="sxs-lookup"><span data-stu-id="d2b9d-117">0.10.x</span></span> |<span data-ttu-id="d2b9d-118">0.10.x.x</span><span class="sxs-lookup"><span data-stu-id="d2b9d-118">0.10.x.x</span></span></br><span data-ttu-id="d2b9d-119">(uniquement sur HDInsight basé sur Windows)</span><span class="sxs-lookup"><span data-stu-id="d2b9d-119">(only on Windows-based HDInsight)</span></span> | <span data-ttu-id="d2b9d-120">N/D</span><span class="sxs-lookup"><span data-stu-id="d2b9d-120">NA</span></span> |
| <span data-ttu-id="d2b9d-121">3.4</span><span class="sxs-lookup"><span data-stu-id="d2b9d-121">3.4</span></span> | <span data-ttu-id="d2b9d-122">0.10.0.x</span><span class="sxs-lookup"><span data-stu-id="d2b9d-122">0.10.0.x</span></span> | <span data-ttu-id="d2b9d-123">0.10.0.x</span><span class="sxs-lookup"><span data-stu-id="d2b9d-123">0.10.0.x</span></span> | <span data-ttu-id="d2b9d-124">3.2.8</span><span class="sxs-lookup"><span data-stu-id="d2b9d-124">3.2.8</span></span> |
| <span data-ttu-id="d2b9d-125">3,5</span><span class="sxs-lookup"><span data-stu-id="d2b9d-125">3.5</span></span> | <span data-ttu-id="d2b9d-126">1.0.2.x</span><span class="sxs-lookup"><span data-stu-id="d2b9d-126">1.0.2.x</span></span> | <span data-ttu-id="d2b9d-127">1.0.0.x</span><span class="sxs-lookup"><span data-stu-id="d2b9d-127">1.0.0.x</span></span> | <span data-ttu-id="d2b9d-128">4.2.1</span><span class="sxs-lookup"><span data-stu-id="d2b9d-128">4.2.1</span></span> |
| <span data-ttu-id="d2b9d-129">3.6</span><span class="sxs-lookup"><span data-stu-id="d2b9d-129">3.6</span></span> | <span data-ttu-id="d2b9d-130">1.1.0.x</span><span class="sxs-lookup"><span data-stu-id="d2b9d-130">1.1.0.x</span></span> | <span data-ttu-id="d2b9d-131">1.0.0.x</span><span class="sxs-lookup"><span data-stu-id="d2b9d-131">1.0.0.x</span></span> | <span data-ttu-id="d2b9d-132">4.2.8</span><span class="sxs-lookup"><span data-stu-id="d2b9d-132">4.2.8</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="d2b9d-133">Topologies c# sur des clusters basés sur Linux doivent utiliser .NET 4.5 et utiliser toorun Mono sur le cluster HDInsight de hello.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-133">C# topologies on Linux-based clusters must use .NET 4.5, and use Mono toorun on hello HDInsight cluster.</span></span> <span data-ttu-id="d2b9d-134">Pour identifier des incompatibilités éventuelles, voir la page relative à la [compatibilité de Mono](http://www.mono-project.com/docs/about-mono/compatibility/).</span><span class="sxs-lookup"><span data-stu-id="d2b9d-134">Check [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) for potential incompatibilities.</span></span>

## <a name="install-visual-studio"></a><span data-ttu-id="d2b9d-135">Installation de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d2b9d-135">Install Visual Studio</span></span>

<span data-ttu-id="d2b9d-136">Vous pouvez développer les topologies c# avec SCP.NET en utilisant l’une de hello versions de Visual Studio suivantes :</span><span class="sxs-lookup"><span data-stu-id="d2b9d-136">You can develop C# topologies with SCP.NET by using one of hello following versions of Visual Studio:</span></span>

* <span data-ttu-id="d2b9d-137">Visual Studio 2012 avec [Update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span><span class="sxs-lookup"><span data-stu-id="d2b9d-137">Visual Studio 2012 with [Update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span></span>

* <span data-ttu-id="d2b9d-138">Visual Studio 2013 avec [Update 4](http://www.microsoft.com/download/details.aspx?id=44921) ou [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)</span><span class="sxs-lookup"><span data-stu-id="d2b9d-138">Visual Studio 2013 with [Update 4](http://www.microsoft.com/download/details.aspx?id=44921) or [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)</span></span>

* <span data-ttu-id="d2b9d-139">Visual Studio 2015 ou [Visual Studio 2015 Community](https://go.microsoft.com/fwlink/?LinkId=532606)</span><span class="sxs-lookup"><span data-stu-id="d2b9d-139">Visual Studio 2015 or [Visual Studio 2015 Community](https://go.microsoft.com/fwlink/?LinkId=532606)</span></span>

* <span data-ttu-id="d2b9d-140">Visual Studio 2017 (toute édition)</span><span class="sxs-lookup"><span data-stu-id="d2b9d-140">Visual Studio 2017 (any edition)</span></span>

## <a name="install-data-lake-tools-for-visual-studio"></a><span data-ttu-id="d2b9d-141">Installer Data Lake Tools pour Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d2b9d-141">Install Data Lake tools for Visual Studio</span></span>

<span data-ttu-id="d2b9d-142">outils de Data Lake tooinstall pour Visual Studio, suivez les étapes de hello dans [prise en main des outils de LAC de données pour Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d2b9d-142">tooinstall Data Lake tools for Visual Studio, follow hello steps in [Get started using Data Lake tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

## <a name="install-java"></a><span data-ttu-id="d2b9d-143">Installer Java</span><span class="sxs-lookup"><span data-stu-id="d2b9d-143">Install Java</span></span>

<span data-ttu-id="d2b9d-144">Lorsque vous soumettez une topologie Storm à partir de Visual Studio, SCP.NET génère un fichier zip qui contient les dépendances et la topologie de hello.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-144">When you submit a Storm topology from Visual Studio, SCP.NET generates a zip file that contains hello topology and dependencies.</span></span> <span data-ttu-id="d2b9d-145">Java est toocreate utilisé ces fichiers, de zip, car elle utilise un format qui n’est plus compatible avec les clusters basés sur Linux.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-145">Java is used toocreate these zip files, because it uses a format that is more compatible with Linux-based clusters.</span></span>

1. <span data-ttu-id="d2b9d-146">Installez hello Kit de développement Java (JDK) 7 ou version ultérieure sur votre environnement de développement.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-146">Install hello Java Developer Kit (JDK) 7 or later on your development environment.</span></span> <span data-ttu-id="d2b9d-147">Vous pouvez obtenir hello JDK Oracle à partir de [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="d2b9d-147">You can get hello Oracle JDK from [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span> <span data-ttu-id="d2b9d-148">Vous pouvez également utiliser d’[autres distributions Java](http://openjdk.java.net/).</span><span class="sxs-lookup"><span data-stu-id="d2b9d-148">You can also use [other Java distributions](http://openjdk.java.net/).</span></span>

2. <span data-ttu-id="d2b9d-149">Hello `JAVA_HOME` environnement variable doit toohello de point de répertoire qui contient Java.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-149">hello `JAVA_HOME` environment variable must point toohello directory that contains Java.</span></span>

3. <span data-ttu-id="d2b9d-150">Hello `PATH` variable d’environnement doit inclure hello `%JAVA_HOME%\bin` active.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-150">hello `PATH` environment variable must include hello `%JAVA_HOME%\bin` directory.</span></span>

<span data-ttu-id="d2b9d-151">Vous pouvez utiliser hello suivant c# console les tooverify d’application que Java et hello JDK sont correctement installés :</span><span class="sxs-lookup"><span data-stu-id="d2b9d-151">You can use hello following C# console application tooverify that Java and hello JDK are correctly installed:</span></span>

```csharp
using System;
using System.IO;
namespace ConsoleApplication2
{
   class Program
   {
       static void Main(string[] args)
       {
           string javaHome = Environment.GetEnvironmentVariable(“JAVA_HOME”);
           if (!string.IsNullOrEmpty(javaHome))
           {
               string jarExe = Path.Combine(javaHome + @”\bin”, “jar.exe”);
               if (File.Exists(jarExe))
               {
                   Console.WriteLine(“JAVA Is Installed properly”);
                    return;
               }
               else
               {
                   Console.WriteLine(“A valid JAVA JDK is not found. Looks like JRE is installed instead of JDK.”);
               }
           }
           else
           {
             Console.WriteLine(“A valid JAVA JDK is not found. JAVA_HOME environment variable is not set.”);
           }
       }  
   }
}
```

## <a name="storm-templates"></a><span data-ttu-id="d2b9d-152">Modèles Storm</span><span class="sxs-lookup"><span data-stu-id="d2b9d-152">Storm templates</span></span>

<span data-ttu-id="d2b9d-153">outils de Data Lake Hello pour Visual Studio fournissent des hello suivant de modèles :</span><span class="sxs-lookup"><span data-stu-id="d2b9d-153">hello Data Lake tools for Visual Studio provide hello following templates:</span></span>

| <span data-ttu-id="d2b9d-154">Type de projet</span><span class="sxs-lookup"><span data-stu-id="d2b9d-154">Project type</span></span> | <span data-ttu-id="d2b9d-155">Illustre le</span><span class="sxs-lookup"><span data-stu-id="d2b9d-155">Demonstrates</span></span> |
| --- | --- |
| <span data-ttu-id="d2b9d-156">Application Storm</span><span class="sxs-lookup"><span data-stu-id="d2b9d-156">Storm Application</span></span> |<span data-ttu-id="d2b9d-157">Projet de topologie Storm vide</span><span class="sxs-lookup"><span data-stu-id="d2b9d-157">An empty Storm topology project.</span></span> |
| <span data-ttu-id="d2b9d-158">Exemple d’enregistreur SQL Azure Storm</span><span class="sxs-lookup"><span data-stu-id="d2b9d-158">Storm Azure SQL Writer Sample</span></span> |<span data-ttu-id="d2b9d-159">Comment toowrite tooAzure base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-159">How toowrite tooAzure SQL Database.</span></span> |
| <span data-ttu-id="d2b9d-160">Exemple de lecteur Azure Cosmos DB Storm</span><span class="sxs-lookup"><span data-stu-id="d2b9d-160">Storm Azure Cosmos DB Reader Sample</span></span> |<span data-ttu-id="d2b9d-161">Comment tooread à partir de la base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-161">How tooread from Azure Cosmos DB.</span></span> |
| <span data-ttu-id="d2b9d-162">Exemple d’enregistreur Azure Cosmos DB Storm</span><span class="sxs-lookup"><span data-stu-id="d2b9d-162">Storm Azure Cosmos DB Writer Sample</span></span> |<span data-ttu-id="d2b9d-163">Comment toowrite tooAzure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-163">How toowrite tooAzure Cosmos DB.</span></span> |
| <span data-ttu-id="d2b9d-164">Exemple de lecteur EventHub Storm</span><span class="sxs-lookup"><span data-stu-id="d2b9d-164">Storm EventHub Reader Sample</span></span> |<span data-ttu-id="d2b9d-165">Comment tooread à partir d’Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-165">How tooread from Azure Event Hubs.</span></span> |
| <span data-ttu-id="d2b9d-166">Exemple d’enregistreur EventHub Storm</span><span class="sxs-lookup"><span data-stu-id="d2b9d-166">Storm EventHub Writer Sample</span></span> |<span data-ttu-id="d2b9d-167">Comment toowrite tooAzure concentrateurs d’événements.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-167">How toowrite tooAzure Event Hubs.</span></span> |
| <span data-ttu-id="d2b9d-168">Exemple de lecteur HBase Storm</span><span class="sxs-lookup"><span data-stu-id="d2b9d-168">Storm HBase Reader Sample</span></span> |<span data-ttu-id="d2b9d-169">Comment tooread HBase sur HDInsight à partir de clusters.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-169">How tooread from HBase on HDInsight clusters.</span></span> |
| <span data-ttu-id="d2b9d-170">Exemple d’enregistreur HBase Storm</span><span class="sxs-lookup"><span data-stu-id="d2b9d-170">Storm HBase Writer Sample</span></span> |<span data-ttu-id="d2b9d-171">Comment les clusters tooHBase toowrite sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-171">How toowrite tooHBase on HDInsight clusters.</span></span> |
| <span data-ttu-id="d2b9d-172">Exemple Storm hybride</span><span class="sxs-lookup"><span data-stu-id="d2b9d-172">Storm Hybrid Sample</span></span> |<span data-ttu-id="d2b9d-173">Comment toouse un composant Java.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-173">How toouse a Java component.</span></span> |
| <span data-ttu-id="d2b9d-174">Exemple Storm</span><span class="sxs-lookup"><span data-stu-id="d2b9d-174">Storm Sample</span></span> |<span data-ttu-id="d2b9d-175">Topologie de comptage de mots de base</span><span class="sxs-lookup"><span data-stu-id="d2b9d-175">A basic word count topology.</span></span> |

> [!WARNING]
> <span data-ttu-id="d2b9d-176">Tous les modèles ne fonctionnent pas avec HDInsight basé sur Linux.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-176">Not all templates will work with Linux-based HDInsight.</span></span> <span data-ttu-id="d2b9d-177">Les packages NuGet utilisés par les modèles hello n’est peut-être pas compatibles avec Mono.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-177">Nuget packages used by hello templates may not be compatible with Mono.</span></span> <span data-ttu-id="d2b9d-178">Vérifiez hello [compatibilité Mono](http://www.mono-project.com/docs/about-mono/compatibility/) de document et utiliser hello [Analyseur de portabilité .NET](hdinsight-hadoop-migrate-dotnet-to-linux.md#automated-portability-analysis) tooidentify des problèmes potentiels.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-178">Check hello [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) document and use hello [.NET Portability Analyzer](hdinsight-hadoop-migrate-dotnet-to-linux.md#automated-portability-analysis) tooidentify potential problems.</span></span>

<span data-ttu-id="d2b9d-179">Dans les étapes de hello dans ce document, vous utilisez hello base Storm Application projet type toocreate une topologie.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-179">In hello steps in this document, you use hello basic Storm Application project type toocreate a topology.</span></span>

### <a name="hbase-templates-notes"></a><span data-ttu-id="d2b9d-180">Remarques sur les modèles HBase</span><span class="sxs-lookup"><span data-stu-id="d2b9d-180">HBase templates notes</span></span>

<span data-ttu-id="d2b9d-181">Hello HBase lecteur et les modèles de writer utilisent hello API REST HBase pas hello API Java HBase toocommunicate avec un HBase sur le cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-181">hello HBase reader and writer templates use hello HBase REST API, not hello HBase Java API, toocommunicate with an HBase on HDInsight cluster.</span></span>

### <a name="eventhub-templates-notes"></a><span data-ttu-id="d2b9d-182">Remarques sur les modèles EventHub</span><span class="sxs-lookup"><span data-stu-id="d2b9d-182">EventHub templates notes</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d2b9d-183">Hello basée sur Java de EventHub bec composant inclus dans le modèle d’EventHub lecteur peuvent ne pas fonctionne avec Storm sur HDInsight version 3.5 ou version ultérieure de hello.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-183">hello Java-based EventHub spout component included with hello EventHub Reader template may not work with Storm on HDInsight version 3.5 or later.</span></span> <span data-ttu-id="d2b9d-184">Une version mise à jour de ce composant est disponible dans la page [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/HDI3.5/lib).</span><span class="sxs-lookup"><span data-stu-id="d2b9d-184">An updated version of this component is available at [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/HDI3.5/lib).</span></span>

<span data-ttu-id="d2b9d-185">Pour un exemple de topologie utilisant ce composant et fonctionnant avec Storm sur HDInsight 3.5, voir [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span><span class="sxs-lookup"><span data-stu-id="d2b9d-185">For an example topology that uses this component and works with Storm on HDInsight 3.5, see [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span></span>

## <a name="create-a-c-topology"></a><span data-ttu-id="d2b9d-186">Création d’une topologie C#</span><span class="sxs-lookup"><span data-stu-id="d2b9d-186">Create a C# topology</span></span>

1. <span data-ttu-id="d2b9d-187">Ouvrez Visual Studio, sélectionnez **Fichier** > **Nouveau**, puis **Projet**.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-187">Open Visual Studio, select **File** > **New**, and then select **Project**.</span></span>

2. <span data-ttu-id="d2b9d-188">À partir de hello **nouveau projet** fenêtre, développez **installé** > **modèles**, puis sélectionnez **Azure Data Lake**.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-188">From hello **New Project** window, expand **Installed** > **Templates**, and select **Azure Data Lake**.</span></span> <span data-ttu-id="d2b9d-189">Dans la liste hello des modèles, sélectionnez **Storm Application**.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-189">From hello list of templates, select **Storm Application**.</span></span> <span data-ttu-id="d2b9d-190">Bas hello écran hello, entrez **WordCount** comme nom de l’application hello de hello.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-190">At hello bottom of hello screen, enter **WordCount** as hello name of hello application.</span></span>

    ![Capture d’écran de la fenêtre Nouveau projet](./media/hdinsight-storm-develop-csharp-visual-studio-topology/new-project.png)

3. <span data-ttu-id="d2b9d-192">Une fois que vous avez créé le projet de hello, vous devez avoir hello fichiers suivants :</span><span class="sxs-lookup"><span data-stu-id="d2b9d-192">After you have created hello project, you should have hello following files:</span></span>

   * <span data-ttu-id="d2b9d-193">**Program.cs**: ce fichier définit la topologie hello pour votre projet.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-193">**Program.cs**: This file defines hello topology for your project.</span></span> <span data-ttu-id="d2b9d-194">Par défaut, une topologie consistant en un seul spout et un seul bolt est créée.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-194">A default topology that consists of one spout and one bolt is created by default.</span></span>

   * <span data-ttu-id="d2b9d-195">**Spout.cs**: un spout d’exemple émettant des nombres aléatoires.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-195">**Spout.cs**: An example spout that emits random numbers.</span></span>

   * <span data-ttu-id="d2b9d-196">**Bolt.cs**: un éclair exemple qui conserve le nombre de numéros émis par bec de hello.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-196">**Bolt.cs**: An example bolt that keeps a count of numbers emitted by hello spout.</span></span>

     <span data-ttu-id="d2b9d-197">Lorsque vous créez le projet de hello, téléchargements de NuGet hello dernières [SCP.NET package](https://www.nuget.org/packages/Microsoft.SCP.Net.SDK/).</span><span class="sxs-lookup"><span data-stu-id="d2b9d-197">When you create hello project, NuGet downloads hello latest [SCP.NET package](https://www.nuget.org/packages/Microsoft.SCP.Net.SDK/).</span></span>

     [!INCLUDE [scp.net version important](../../includes/hdinsight-storm-scpdotnet-version.md)]

### <a name="implement-hello-spout"></a><span data-ttu-id="d2b9d-198">BEC hello de mettre en œuvre</span><span class="sxs-lookup"><span data-stu-id="d2b9d-198">Implement hello spout</span></span>

1. <span data-ttu-id="d2b9d-199">Ouvrez **Spout.cs**.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-199">Open **Spout.cs**.</span></span> <span data-ttu-id="d2b9d-200">Becs verseurs sont données tooread utilisé dans une topologie à partir d’une source externe.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-200">Spouts are used tooread data in a topology from an external source.</span></span> <span data-ttu-id="d2b9d-201">composants principaux de Hello pour un bec sont :</span><span class="sxs-lookup"><span data-stu-id="d2b9d-201">hello main components for a spout are:</span></span>

   * <span data-ttu-id="d2b9d-202">**NextTuple**: appelé par Storm lorsque bec de hello est autorisé tooemit nouveaux tuples.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-202">**NextTuple**: Called by Storm when hello spout is allowed tooemit new tuples.</span></span>

   * <span data-ttu-id="d2b9d-203">**L’accusé de réception** (topologie transactionnelle uniquement) : gère les accusés de réception initiées par d’autres composants dans une topologie hello pour les tuples envoyés à partir de bec de hello.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-203">**Ack** (transactional topology only): Handles acknowledgements initiated by other components in hello topology for tuples sent from hello spout.</span></span> <span data-ttu-id="d2b9d-204">Accuse réception d’un tuple informe bec de hello qu’il a été correctement traité par les composants en aval.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-204">Acknowledging a tuple lets hello spout know that it was processed successfully by downstream components.</span></span>

   * <span data-ttu-id="d2b9d-205">**Échec de** (topologie transactionnelle uniquement) : gère les tuples qui sont fail-le traitement des autres composants de la topologie de hello.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-205">**Fail** (transactional topology only): Handles tuples that are fail-processing other components in hello topology.</span></span> <span data-ttu-id="d2b9d-206">Implémentation d’une méthode de basculement vous permet de toore-émettre hello tuple afin qu’elle peut être traitée à nouveau.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-206">Implementing a Fail method allows you toore-emit hello tuple so that it can be processed again.</span></span>

2. <span data-ttu-id="d2b9d-207">Remplacez le contenu hello Hello **bec** classe avec hello après le texte.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-207">Replace hello contents of hello **Spout** class with hello following text.</span></span> <span data-ttu-id="d2b9d-208">Cet bec émet au hasard une phrase dans la topologie de hello.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-208">This spout randomly emits a sentence into hello topology.</span></span>

    ```csharp
    private Context ctx;
    private Random r = new Random();
    string[] sentences = new string[] {
        "hello cow jumped over hello moon",
        "an apple a day keeps hello doctor away",
        "four score and seven years ago",
        "snow white and hello seven dwarfs",
        "i am at two with nature"
    };

    public Spout(Context ctx)
    {
        // Set hello instance context
        this.ctx = ctx;

        Context.Logger.Info("Generator constructor called");

        // Declare Output schema
        Dictionary<string, List<Type>> outputSchema = new Dictionary<string, List<Type>>();
        // hello schema for hello default output stream is
        // a tuple that contains a string field
        outputSchema.Add("default", new List<Type>() { typeof(string) });
        this.ctx.DeclareComponentSchema(new ComponentStreamSchema(null, outputSchema));
    }

    // Get an instance of hello spout
    public static Spout Get(Context ctx, Dictionary<string, Object> parms)
    {
        return new Spout(ctx);
    }

    public void NextTuple(Dictionary<string, Object> parms)
    {
        Context.Logger.Info("NextTuple enter");
        // hello sentence toobe emitted
        string sentence;

        // Get a random sentence
        sentence = sentences[r.Next(0, sentences.Length - 1)];
        Context.Logger.Info("Emit: {0}", sentence);
        // Emit it
        this.ctx.Emit(new Values(sentence));

        Context.Logger.Info("NextTuple exit");
    }

    public void Ack(long seqId, Dictionary<string, Object> parms)
    {
        // Only used for transactional topologies
    }

    public void Fail(long seqId, Dictionary<string, Object> parms)
    {
        // Only used for transactional topologies
    }
    ```

### <a name="implement-hello-bolts"></a><span data-ttu-id="d2b9d-209">Implémentez hello boulons</span><span class="sxs-lookup"><span data-stu-id="d2b9d-209">Implement hello bolts</span></span>

1. <span data-ttu-id="d2b9d-210">Supprimer hello existant **Bolt.cs** fichier de projet de hello.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-210">Delete hello existing **Bolt.cs** file from hello project.</span></span>

2. <span data-ttu-id="d2b9d-211">Dans **l’Explorateur de solutions**, cliquez sur le projet de hello, puis sélectionnez **ajouter** > **un nouvel élément**.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-211">In **Solution Explorer**, right-click hello project, and select **Add** > **New item**.</span></span> <span data-ttu-id="d2b9d-212">Dans la liste hello, sélectionnez **Storm éclair**, puis entrez **Splitter.cs** comme nom de hello.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-212">From hello list, select **Storm Bolt**, and enter **Splitter.cs** as hello name.</span></span> <span data-ttu-id="d2b9d-213">Répétez cette toocreate processus nommé d’un deuxième éclair **Counter.cs**.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-213">Repeat this process toocreate a second bolt named **Counter.cs**.</span></span>

   * <span data-ttu-id="d2b9d-214">**Splitter.cs** : implémente un bolt qui fractionne les phrases en mots et émet un nouveau flux de mots.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-214">**Splitter.cs**: Implements a bolt that splits sentences into individual words, and emits a new stream of words.</span></span>

   * <span data-ttu-id="d2b9d-215">**Counter.cs**: implémente un éclair qui compte chaque mot et émet un flux de données de mots et le nombre de hello pour chaque mot.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-215">**Counter.cs**: Implements a bolt that counts each word, and emits a new stream of words and hello count for each word.</span></span>

     > [!NOTE]
     > <span data-ttu-id="d2b9d-216">Ces boulons lire et écrire des toostreams, mais vous pouvez également utiliser un toocommunicate éclair avec sources telles que la base de données ou service.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-216">These bolts read and write toostreams, but you can also use a bolt toocommunicate with sources such as a database or service.</span></span>

3. <span data-ttu-id="d2b9d-217">Ouvrez **Splitter.cs**.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-217">Open **Splitter.cs**.</span></span> <span data-ttu-id="d2b9d-218">Il n’a qu’une seule méthode par défaut : **Execute**.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-218">It has only one method by default: **Execute**.</span></span> <span data-ttu-id="d2b9d-219">Hello méthode Execute est appelée lorsque les éclair hello reçoit un tuple pour le traitement.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-219">hello Execute method is called when hello bolt receives a tuple for processing.</span></span> <span data-ttu-id="d2b9d-220">Ici, vous pouvez lire et traiter des tuples entrants et émettre des tuples sortants.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-220">Here, you can read and process incoming tuples, and emit outbound tuples.</span></span>

4. <span data-ttu-id="d2b9d-221">Remplacer le contenu hello Hello **fractionnement** classe avec hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="d2b9d-221">Replace hello contents of hello **Splitter** class with hello following code:</span></span>

    ```csharp
    private Context ctx;

    // Constructor
    public Splitter(Context ctx)
    {
        Context.Logger.Info("Splitter constructor called");
        this.ctx = ctx;

        // Declare Input and Output schemas
        Dictionary<string, List<Type>> inputSchema = new Dictionary<string, List<Type>>();
        // Input contains a tuple with a string field (hello sentence)
        inputSchema.Add("default", new List<Type>() { typeof(string) });
        Dictionary<string, List<Type>> outputSchema = new Dictionary<string, List<Type>>();
        // Outbound contains a tuple with a string field (hello word)
        outputSchema.Add("default", new List<Type>() { typeof(string) });
        this.ctx.DeclareComponentSchema(new ComponentStreamSchema(inputSchema, outputSchema));
    }

    // Get a new instance of hello bolt
    public static Splitter Get(Context ctx, Dictionary<string, Object> parms)
    {
        return new Splitter(ctx);
    }

    // Called when a new tuple is available
    public void Execute(SCPTuple tuple)
    {
        Context.Logger.Info("Execute enter");

        // Get hello sentence from hello tuple
        string sentence = tuple.GetString(0);
        // Split at space characters
        foreach (string word in sentence.Split(' '))
        {
            Context.Logger.Info("Emit: {0}", word);
            //Emit each word
            this.ctx.Emit(new Values(word));
        }

        Context.Logger.Info("Execute exit");
    }
    ```

5. <span data-ttu-id="d2b9d-222">Ouvrez **Counter.cs**et remplacez le contenu de classe hello par qui suit hello :</span><span class="sxs-lookup"><span data-stu-id="d2b9d-222">Open **Counter.cs**, and replace hello class contents with hello following:</span></span>

    ```csharp
    private Context ctx;

    // Dictionary for holding words and counts
    private Dictionary<string, int> counts = new Dictionary<string, int>();

    // Constructor
    public Counter(Context ctx)
    {
        Context.Logger.Info("Counter constructor called");
        // Set instance context
        this.ctx = ctx;

        // Declare Input and Output schemas
        Dictionary<string, List<Type>> inputSchema = new Dictionary<string, List<Type>>();
        // A tuple containing a string field - hello word
        inputSchema.Add("default", new List<Type>() { typeof(string) });

        Dictionary<string, List<Type>> outputSchema = new Dictionary<string, List<Type>>();
        // A tuple containing a string and integer field - hello word and hello word count
        outputSchema.Add("default", new List<Type>() { typeof(string), typeof(int) });
        this.ctx.DeclareComponentSchema(new ComponentStreamSchema(inputSchema, outputSchema));
    }

    // Get a new instance
    public static Counter Get(Context ctx, Dictionary<string, Object> parms)
    {
        return new Counter(ctx);
    }

    // Called when a new tuple is available
    public void Execute(SCPTuple tuple)
    {
        Context.Logger.Info("Execute enter");

        // Get hello word from hello tuple
        string word = tuple.GetString(0);
        // Do we already have an entry for hello word in hello dictionary?
        // If no, create one with a count of 0
        int count = counts.ContainsKey(word) ? counts[word] : 0;
        // Increment hello count
        count++;
        // Update hello count in hello dictionary
        counts[word] = count;

        Context.Logger.Info("Emit: {0}, count: {1}", word, count);
        // Emit hello word and count information
        this.ctx.Emit(Constants.DEFAULT_STREAM_ID, new List<SCPTuple> { tuple }, new Values(word, count));
        Context.Logger.Info("Execute exit");
    }
    ```

### <a name="define-hello-topology"></a><span data-ttu-id="d2b9d-223">Définir la topologie de hello</span><span class="sxs-lookup"><span data-stu-id="d2b9d-223">Define hello topology</span></span>

<span data-ttu-id="d2b9d-224">Becs verseurs et boulons sont organisés dans un graphique, qui définit comment les données de salutation transitent entre les composants.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-224">Spouts and bolts are arranged in a graph, which defines how hello data flows between components.</span></span> <span data-ttu-id="d2b9d-225">Dans cette topologie, le graphique de hello est la suivante :</span><span class="sxs-lookup"><span data-stu-id="d2b9d-225">For this topology, hello graph is as follows:</span></span>

![Diagramme illustrant l’organisation des composants](./media/hdinsight-storm-develop-csharp-visual-studio-topology/wordcount-topology.png)

<span data-ttu-id="d2b9d-227">Les phrases sont émis à partir de bec de hello et sont distribuées tooinstances d’éclair de fractionnement hello.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-227">Sentences are emitted from hello spout, and are distributed tooinstances of hello Splitter bolt.</span></span> <span data-ttu-id="d2b9d-228">éclair de fractionnement Hello divise les phrases hello en mots, qui sont éclair de compteur toohello distribuée.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-228">hello Splitter bolt breaks hello sentences into words, which are distributed toohello Counter bolt.</span></span>

<span data-ttu-id="d2b9d-229">Étant donné que le nombre de mots est conservé localement dans l’instance de compteur hello, nous souhaitons toomake que par des mots spécifiques de flux toohello même instance de compteur d’éclair.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-229">Because word count is held locally in hello Counter instance, we want toomake sure that specific words flow toohello same Counter bolt instance.</span></span> <span data-ttu-id="d2b9d-230">afin de garantir que chaque instance suit un mot donné.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-230">Each instance keeps track of specific words.</span></span> <span data-ttu-id="d2b9d-231">Étant donné qu’éclair de fractionnement hello ne conserve aucun état, vraiment peu quelle instance de séparateur de hello reçoit le phrase.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-231">Since hello Splitter bolt maintains no state, it really doesn't matter which instance of hello splitter receives which sentence.</span></span>

<span data-ttu-id="d2b9d-232">Ouvrez **Program.cs**.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-232">Open **Program.cs**.</span></span> <span data-ttu-id="d2b9d-233">méthode important Hello est **GetTopologyBuilder**, qui est la topologie de hello toodefine utilisé est soumis tooStorm.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-233">hello important method is **GetTopologyBuilder**, which is used toodefine hello topology that is submitted tooStorm.</span></span> <span data-ttu-id="d2b9d-234">Remplacez le contenu hello de **GetTopologyBuilder** avec hello suivant la topologie de hello tooimplement code décrit précédemment :</span><span class="sxs-lookup"><span data-stu-id="d2b9d-234">Replace hello contents of **GetTopologyBuilder** with hello following code tooimplement hello topology described previously:</span></span>

```csharp
// Create a new topology named 'WordCount'
TopologyBuilder topologyBuilder = new TopologyBuilder("WordCount" + DateTime.Now.ToString("yyyyMMddHHmmss"));

// Add hello spout toohello topology.
// Name hello component 'sentences'
// Name hello field that is emitted as 'sentence'
topologyBuilder.SetSpout(
    "sentences",
    Spout.Get,
    new Dictionary<string, List<string>>()
    {
        {Constants.DEFAULT_STREAM_ID, new List<string>(){"sentence"}}
    },
    1);
// Add hello splitter bolt toohello topology.
// Name hello component 'splitter'
// Name hello field that is emitted 'word'
// Use suffleGrouping toodistribute incoming tuples
//   from hello 'sentences' spout across instances
//   of hello splitter
topologyBuilder.SetBolt(
    "splitter",
    Splitter.Get,
    new Dictionary<string, List<string>>()
    {
        {Constants.DEFAULT_STREAM_ID, new List<string>(){"word"}}
    },
    1).shuffleGrouping("sentences");

// Add hello counter bolt toohello topology.
// Name hello component 'counter'
// Name hello fields that are emitted 'word' and 'count'
// Use fieldsGrouping tooensure that tuples are routed
//   toocounter instances based on hello contents of field
//   position 0 (hello word). This could also have been
//   List<string>(){"word"}.
//   This ensures that hello word 'jumped', for example, will always
//   go toohello same instance
topologyBuilder.SetBolt(
    "counter",
    Counter.Get,
    new Dictionary<string, List<string>>()
    {
        {Constants.DEFAULT_STREAM_ID, new List<string>(){"word", "count"}}
    },
    1).fieldsGrouping("splitter", new List<int>() { 0 });

// Add topology config
topologyBuilder.SetTopologyConfig(new Dictionary<string, string>()
{
    {"topology.kryo.register","[\"[B\"]"}
});

return topologyBuilder;
```

## <a name="submit-hello-topology"></a><span data-ttu-id="d2b9d-235">Envoyer de topologie hello</span><span class="sxs-lookup"><span data-stu-id="d2b9d-235">Submit hello topology</span></span>

1. <span data-ttu-id="d2b9d-236">Dans **l’Explorateur de solutions**, cliquez sur le projet de hello, puis sélectionnez **envoyer tooStorm sur HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-236">In **Solution Explorer**, right-click hello project, and select **Submit tooStorm on HDInsight**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="d2b9d-237">Si vous y êtes invité, entrez les informations d’identification de l’hello pour votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-237">If prompted, enter hello credentials for your Azure subscription.</span></span> <span data-ttu-id="d2b9d-238">Si vous avez plusieurs abonnements, connectez-vous toohello qui contient votre Storm sur le cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-238">If you have more than one subscription, sign in toohello one that contains your Storm on HDInsight cluster.</span></span>

2. <span data-ttu-id="d2b9d-239">Sélectionnez votre Storm sur le cluster HDInsight à partir de hello **Cluster Storm** liste déroulante et sélectionnez **Submit**.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-239">Select your Storm on HDInsight cluster from hello **Storm Cluster** drop-down list, and then select **Submit**.</span></span> <span data-ttu-id="d2b9d-240">Vous pouvez surveiller si l’envoi de hello réussit à l’aide de hello **sortie** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-240">You can monitor if hello submission is successful by using hello **Output** window.</span></span>

3. <span data-ttu-id="d2b9d-241">Lors de la topologie de hello a été envoyé avec succès, hello **Storm Topologies** pour le cluster de hello doit apparaître.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-241">When hello topology has been successfully submitted, hello **Storm Topologies** for hello cluster should appear.</span></span> <span data-ttu-id="d2b9d-242">Sélectionnez hello **WordCount** topologie de hello liste tooview informations hello topologie en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-242">Select hello **WordCount** topology from hello list tooview information about hello running topology.</span></span>

   > [!NOTE]
   > <span data-ttu-id="d2b9d-243">Vous pouvez également afficher les **Topologies Storm** dans l’**Explorateur de serveurs**.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-243">You can also view **Storm Topologies** from **Server Explorer**.</span></span> <span data-ttu-id="d2b9d-244">Développez **Azure** > **HDInsight**, cliquez avec le bouton droit sur un Storm sur le cluster HDInsight, puis sélectionnez **Afficher les topologies Storm**.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-244">Expand **Azure** > **HDInsight**, right-click a Storm on HDInsight cluster, and then select **View Storm Topologies**.</span></span>

    <span data-ttu-id="d2b9d-245">tooview plus d’informations sur les composants de hello de topologie de hello, double-cliquez sur composant hello dans le diagramme de hello.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-245">tooview information about hello components in hello topology, double-click hello component in hello diagram.</span></span>

4. <span data-ttu-id="d2b9d-246">À partir de hello **récapitulatif de la topologie** afficher, cliquez sur **Kill** topologie de hello toostop.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-246">From hello **Topology Summary** view, click **Kill** toostop hello topology.</span></span>

   > [!NOTE]
   > <span data-ttu-id="d2b9d-247">Les topologies Storm continuer toorun jusqu'à ce qu’ils sont désactivés ou cluster de hello est supprimé.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-247">Storm topologies continue toorun until they are deactivated, or hello cluster is deleted.</span></span>

## <a name="transactional-topology"></a><span data-ttu-id="d2b9d-248">Topologie transactionnelle</span><span class="sxs-lookup"><span data-stu-id="d2b9d-248">Transactional topology</span></span>

<span data-ttu-id="d2b9d-249">topologie de précédente Hello est non transactionnelle.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-249">hello previous topology is non-transactional.</span></span> <span data-ttu-id="d2b9d-250">composants Hello dans la topologie de hello n’implémentent pas de messages tooreplaying de fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-250">hello components in hello topology do not implement functionality tooreplaying messages.</span></span> <span data-ttu-id="d2b9d-251">Pour obtenir un exemple d’une topologie transactionnelle, créez un projet et sélectionnez **Storm exemple** en tant que type de projet hello.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-251">For an example of a transactional topology, create a project and select **Storm Sample** as hello project type.</span></span>

<span data-ttu-id="d2b9d-252">Topologies transactionnelles implémentent hello suivant toosupport la relecture des données :</span><span class="sxs-lookup"><span data-stu-id="d2b9d-252">Transactional topologies implement hello following toosupport replay of data:</span></span>

* <span data-ttu-id="d2b9d-253">**La mise en cache des métadonnées**: bec de hello doit stocker des métadonnées sur les données de salutation émises, afin que les données de salutation peuvent être récupérées et émises à nouveau si une défaillance se produit.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-253">**Metadata caching**: hello spout must store metadata about hello data emitted, so that hello data can be retrieved and emitted again if a failure occurs.</span></span> <span data-ttu-id="d2b9d-254">Étant donné que les données hello émises par exemple hello sont petites, les données brutes de hello pour chaque tuple sont stockées dans un dictionnaire pour la relecture.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-254">Because hello data emitted by hello sample is small, hello raw data for each tuple is stored in a dictionary for replay.</span></span>

* <span data-ttu-id="d2b9d-255">**L’accusé de réception**: chaque éclair dans une topologie de hello peut appeler `this.ctx.Ack(tuple)` tooacknowledge qu’il a correctement traité un tuple.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-255">**Ack**: Each bolt in hello topology can call `this.ctx.Ack(tuple)` tooacknowledge that it has successfully processed a tuple.</span></span> <span data-ttu-id="d2b9d-256">Lorsque tous les boulons ont reçu hello tuple, hello `Ack` méthode de bec de hello est appelée.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-256">When all bolts have acked hello tuple, hello `Ack` method of hello spout is invoked.</span></span> <span data-ttu-id="d2b9d-257">Hello `Ack` méthode permet de hello bec tooremove données qui a été mis en cache pour la relecture.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-257">hello `Ack` method allows hello spout tooremove data that was cached for replay.</span></span>

* <span data-ttu-id="d2b9d-258">**Échec de**: chaque éclair peut appeler `this.ctx.Fail(tuple)` tooindicate que le traitement a échoué pour un tuple.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-258">**Fail**: Each bolt can call `this.ctx.Fail(tuple)` tooindicate that processing has failed for a tuple.</span></span> <span data-ttu-id="d2b9d-259">Échec de Hello propage toohello `Fail` méthode bec hello, où hello tuple puisse être relue à l’aide des métadonnées mises en cache.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-259">hello failure propagates toohello `Fail` method of hello spout, where hello tuple can be replayed by using cached metadata.</span></span>

* <span data-ttu-id="d2b9d-260">**ID de séquence** : lors de l’émission d’un tuple, un ID de séquence unique peut être spécifié.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-260">**Sequence ID**: When emitting a tuple, a unique sequence ID can be specified.</span></span> <span data-ttu-id="d2b9d-261">Cette valeur identifie un tuple hello pour le traitement de relecture (accusé de réception et échec).</span><span class="sxs-lookup"><span data-stu-id="d2b9d-261">This value identifies hello tuple for replay (Ack and Fail) processing.</span></span> <span data-ttu-id="d2b9d-262">Par exemple, hello bec Bonjour **Storm exemple** projet utilise suivant de hello lors de l’émission de données :</span><span class="sxs-lookup"><span data-stu-id="d2b9d-262">For example, hello spout in hello **Storm Sample** project uses hello following when emitting data:</span></span>

        this.ctx.Emit(Constants.DEFAULT_STREAM_ID, new Values(sentence), lastSeqId);

    <span data-ttu-id="d2b9d-263">Ce code émet un tuple qui contient un flux par défaut de toohello phrase, dont la valeur d’ID de séquence hello contenue dans **lastSeqId**.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-263">This code emits a tuple that contains a sentence toohello default stream, with hello sequence ID value contained in **lastSeqId**.</span></span> <span data-ttu-id="d2b9d-264">Dans cet exemple, **lastSeqId** est incrémenté pour chaque tuple émis.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-264">For this example, **lastSeqId** is incremented for every tuple emitted.</span></span>

<span data-ttu-id="d2b9d-265">Comme illustré dans hello **Storm exemple** projet d’équipe, si un composant est transactionnels peut être définie lors de l’exécution, en fonction de configuration.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-265">As demonstrated in hello **Storm Sample** project, whether a component is transactional can be set at runtime, based on configuration.</span></span>

## <a name="hybrid-topology-with-c-and-java"></a><span data-ttu-id="d2b9d-266">Topologie hybride avec C# et Java</span><span class="sxs-lookup"><span data-stu-id="d2b9d-266">Hybrid topology with C# and Java</span></span>

<span data-ttu-id="d2b9d-267">Vous pouvez également utiliser les outils de LAC de données pour les topologies Visual Studio toocreate hybride, où certains composants sont c# et d’autres sont Java.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-267">You can also use Data Lake tools for Visual Studio toocreate hybrid topologies, where some components are C# and others are Java.</span></span>

<span data-ttu-id="d2b9d-268">Pour un exemple de topologie hybride, créez un projet, puis sélectionnez **Exemple Storm hybride**.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-268">For an example of a hybrid topology, create a project and select **Storm Hybrid Sample**.</span></span> <span data-ttu-id="d2b9d-269">Ce type de l’exemple montre comment hello suivant concepts :</span><span class="sxs-lookup"><span data-stu-id="d2b9d-269">This sample type demonstrates hello following concepts:</span></span>

* <span data-ttu-id="d2b9d-270">**Spout Java** et **bolt C#** : définis dans **HybridTopology_javaSpout_csharpBolt**.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-270">**Java spout** and **C# bolt**: Defined in **HybridTopology_javaSpout_csharpBolt**.</span></span>

    * <span data-ttu-id="d2b9d-271">Une version transactionnelle est définie dans **HybridTopologyTx_javaSpout_csharpBolt**.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-271">A transactional version is defined in **HybridTopologyTx_javaSpout_csharpBolt**.</span></span>

* <span data-ttu-id="d2b9d-272">**Spout C#** et **bolt Java** : définis dans **HybridTopology_csharpSpout_javaBolt**.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-272">**C# spout** and **Java bolt**: Defined in **HybridTopology_csharpSpout_javaBolt**.</span></span>

    * <span data-ttu-id="d2b9d-273">Une version transactionnelle est définie dans **HybridTopologyTx_csharpSpout_javaBolt**.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-273">A transactional version is defined in **HybridTopologyTx_csharpSpout_javaBolt**.</span></span>

  > [!NOTE]
  > <span data-ttu-id="d2b9d-274">Cette version montre également comment toouse Clojure code à partir d’un fichier texte comme un composant Java.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-274">This version also demonstrates how toouse Clojure code from a text file as a Java component.</span></span>


<span data-ttu-id="d2b9d-275">topologie hello tooswitch qui est utilisé lorsque le projet de hello est envoyé, il suffit de déplacer hello `[Active(true)]` instruction toohello topologie toouse, avant de le soumettre toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-275">tooswitch hello topology that is used when hello project is submitted, simply move hello `[Active(true)]` statement toohello topology you want toouse, before submitting it toohello cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="d2b9d-276">Tous les fichiers Java hello requises sont fournies dans le cadre de ce projet Bonjour **JavaDependency** dossier.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-276">All hello Java files that are required are provided as part of this project in hello **JavaDependency** folder.</span></span>

<span data-ttu-id="d2b9d-277">Considérez les éléments suivants de hello lorsque vous créez et envoi d’une topologie hybride :</span><span class="sxs-lookup"><span data-stu-id="d2b9d-277">Consider hello following when you are creating and submitting a hybrid topology:</span></span>

* <span data-ttu-id="d2b9d-278">Vous devez utiliser **JavaComponentConstructor** toocreate une instance de hello classe Java pour un bec ou un éclair.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-278">You must use **JavaComponentConstructor** toocreate an instance of hello Java class for a spout or bolt.</span></span>

* <span data-ttu-id="d2b9d-279">Vous devez utiliser **microsoft.scp.storm.multilang.CustomizedInteropJSONSerializer** tooJSON les objets de données de tooserialize dans ou en dehors des composants Java à partir de Java.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-279">You should use **microsoft.scp.storm.multilang.CustomizedInteropJSONSerializer** tooserialize data into or out of Java components from Java objects tooJSON.</span></span>

* <span data-ttu-id="d2b9d-280">Lorsque vous soumettez un serveur de toohello hello topologie, vous devez utiliser hello **des configurations supplémentaires** hello de toospecify option **chemins d’accès de Java**.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-280">When submitting hello topology toohello server, you must use hello **Additional configurations** option toospecify hello **Java File paths**.</span></span> <span data-ttu-id="d2b9d-281">chemin d’accès Hello spécifié doit être le répertoire hello qui contient les fichiers JAR hello qui contiennent vos classes Java.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-281">hello path specified should be hello directory that contains hello JAR files that contain your Java classes.</span></span>

### <a name="azure-event-hubs"></a><span data-ttu-id="d2b9d-282">Hubs d'événements Azure</span><span class="sxs-lookup"><span data-stu-id="d2b9d-282">Azure Event Hubs</span></span>

<span data-ttu-id="d2b9d-283">SCP.NET version 0.9.4.203 introduit une nouvelle classe et la méthode spécifiquement pour l’utilisation avec bec de concentrateur d’événements hello (bec Java qui lit à partir de concentrateurs d’événements).</span><span class="sxs-lookup"><span data-stu-id="d2b9d-283">SCP.NET version 0.9.4.203 introduces a new class and method specifically for working with hello Event Hub spout (a Java spout that reads from Event Hubs).</span></span> <span data-ttu-id="d2b9d-284">Lorsque vous créez une topologie qui utilise un bec concentrateur d’événements, utilisez hello méthodes suivantes :</span><span class="sxs-lookup"><span data-stu-id="d2b9d-284">When you create a topology that uses an Event Hub spout, use hello following methods:</span></span>

* <span data-ttu-id="d2b9d-285">**EventHubSpoutConfig** classe : crée un objet qui contient la configuration de hello de composant de bec hello.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-285">**EventHubSpoutConfig** class: Creates an object that contains hello configuration for hello spout component.</span></span>

* <span data-ttu-id="d2b9d-286">**TopologyBuilder.SetEventHubSpout** méthode : ajoute la topologie de toohello hello concentrateur d’événements bec de composant.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-286">**TopologyBuilder.SetEventHubSpout** method: Adds hello Event Hub spout component toohello topology.</span></span>

> [!NOTE]
> <span data-ttu-id="d2b9d-287">Vous devez toujours utiliser hello **CustomizedInteropJSONSerializer** tooserialize données produites par bec de hello.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-287">You must still use hello **CustomizedInteropJSONSerializer** tooserialize data produced by hello spout.</span></span>

## <span data-ttu-id="d2b9d-288"><a id="configurationmanager"></a>Utiliser ConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="d2b9d-288"><a id="configurationmanager"></a>Use ConfigurationManager</span></span>

<span data-ttu-id="d2b9d-289">N’utilisez pas **ConfigurationManager** tooretrieve configuration des valeurs à partir de boulon et bec de composants.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-289">Don't use **ConfigurationManager** tooretrieve configuration values from bolt and spout components.</span></span> <span data-ttu-id="d2b9d-290">Cela est susceptible d’entraîner une exception de pointeur null.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-290">Doing so can cause a null pointer exception.</span></span> <span data-ttu-id="d2b9d-291">Au lieu de cela, la configuration hello pour votre projet est passée dans une topologie de Storm hello comme une paire clé / valeur dans le contexte de topologie hello.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-291">Instead, hello configuration for your project is passed into hello Storm topology as a key and value pair in hello topology context.</span></span> <span data-ttu-id="d2b9d-292">Chaque composant qui s’appuie sur des valeurs de configuration doit les récupérer à partir du contexte de hello lors de l’initialisation.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-292">Each component that relies on configuration values must retrieve them from hello context during initialization.</span></span>

<span data-ttu-id="d2b9d-293">Hello de code suivant montre comment tooretrieve ces valeurs :</span><span class="sxs-lookup"><span data-stu-id="d2b9d-293">hello following code demonstrates how tooretrieve these values:</span></span>

```csharp
public class MyComponent : ISCPBolt
{
    // toohold configuration information loaded from context
    Configuration configuration;
    ...
    public MyComponent(Context ctx, Dictionary<string, Object> parms)
    {
        // Save a copy of hello context for this component instance
        this.ctx = ctx;
        // If it exists, load hello configuration for hello component
        if(parms.ContainsKey(Constants.USER_CONFIG))
        {
            this.configuration = parms[Constants.USER_CONFIG] as System.Configuration.Configuration;
        }
        // Retrieve hello value of "Foo" from configuration
        var foo = this.configuration.AppSettings.Settings["Foo"].Value;
    }
    ...
}
```

<span data-ttu-id="d2b9d-294">Si vous utilisez un `Get` tooreturn méthode une instance de votre composant, vous devez vous assurer qu’il passe à la fois hello `Context` et `Dictionary<string, Object>` constructeur toohello de paramètres.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-294">If you use a `Get` method tooreturn an instance of your component, you must ensure that it passes both hello `Context` and `Dictionary<string, Object>` parameters toohello constructor.</span></span> <span data-ttu-id="d2b9d-295">exemple Hello est un base `Get` méthode qui se passe correctement les valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="d2b9d-295">hello following example is a basic `Get` method that properly passes these values:</span></span>

```csharp
public static MyComponent Get(Context ctx, Dictionary<string, Object> parms)
{
    return new MyComponent(ctx, parms);
}
```

## <a name="how-tooupdate-scpnet"></a><span data-ttu-id="d2b9d-296">Comment tooupdate SCP.NET</span><span class="sxs-lookup"><span data-stu-id="d2b9d-296">How tooupdate SCP.NET</span></span>

<span data-ttu-id="d2b9d-297">Les dernières versions de SCP.NET prennent en charge la mise à niveau du package via NuGet.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-297">Recent releases of SCP.NET support package upgrade through NuGet.</span></span> <span data-ttu-id="d2b9d-298">Vous recevez une notification de mise à niveau dès qu’une nouvelle mise à jour est disponible.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-298">When a new update is available, you receive an upgrade notification.</span></span> <span data-ttu-id="d2b9d-299">vérification de toomanually pour une mise à niveau, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="d2b9d-299">toomanually check for an upgrade, follow these steps:</span></span>

1. <span data-ttu-id="d2b9d-300">Dans **l’Explorateur de solutions**, cliquez sur le projet de hello, puis sélectionnez **gérer les Packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-300">In **Solution Explorer**, right-click hello project, and select **Manage NuGet Packages**.</span></span>

2. <span data-ttu-id="d2b9d-301">Dans le Gestionnaire de package hello, sélectionnez **mises à jour**.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-301">From hello package manager, select **Updates**.</span></span> <span data-ttu-id="d2b9d-302">Si une mise à jour est disponible, elle est affichée.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-302">If an update is available, it is listed.</span></span> <span data-ttu-id="d2b9d-303">Cliquez sur **mise à jour** pour hello package tooinstall il.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-303">Click **Update** for hello package tooinstall it.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d2b9d-304">Si votre projet a été créé avec une version antérieure de SCP.NET qui n’utilise pas de NuGet, vous devez effectuer hello suivant la version la plus récente tooa tooupdate comme suit :</span><span class="sxs-lookup"><span data-stu-id="d2b9d-304">If your project was created with an earlier version of SCP.NET that did not use NuGet, you must perform hello following steps tooupdate tooa newer version:</span></span>
>
> 1. <span data-ttu-id="d2b9d-305">Dans **l’Explorateur de solutions**, cliquez sur le projet de hello, puis sélectionnez **gérer les Packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-305">In **Solution Explorer**, right-click hello project, and select **Manage NuGet Packages**.</span></span>
> 2. <span data-ttu-id="d2b9d-306">À l’aide de hello **recherche** champ, recherchez et ajoutez, **Microsoft.SCP.Net.SDK** toohello projet.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-306">Using hello **Search** field, search for, and then add, **Microsoft.SCP.Net.SDK** toohello project.</span></span>

## <a name="troubleshoot-common-issues-with-topologies"></a><span data-ttu-id="d2b9d-307">Dépanner des problèmes courants avec les topologies</span><span class="sxs-lookup"><span data-stu-id="d2b9d-307">Troubleshoot common issues with topologies</span></span>

### <a name="null-pointer-exceptions"></a><span data-ttu-id="d2b9d-308">Exceptions de pointeur null</span><span class="sxs-lookup"><span data-stu-id="d2b9d-308">Null pointer exceptions</span></span>

<span data-ttu-id="d2b9d-309">Lorsque vous utilisez une topologie c# avec un cluster HDInsight de basés sur Linux, boulon et bec des composants qui utilisent **ConfigurationManager** tooread les paramètres de configuration lors de l’exécution peuvent retourner des exceptions de pointeur null.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-309">When you are using a C# topology with a Linux-based HDInsight cluster, bolt and spout components that use **ConfigurationManager** tooread configuration settings at runtime may return null pointer exceptions.</span></span>

<span data-ttu-id="d2b9d-310">configuration Hello pour votre projet est passée dans la topologie de Storm hello comme une paire clé / valeur dans le contexte de topologie hello.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-310">hello configuration for your project is passed into hello Storm topology as a key and value pair in hello topology context.</span></span> <span data-ttu-id="d2b9d-311">Il peut être récupéré à partir de l’objet dictionnaire hello passé tooyour composants lorsqu’elles sont initialisées.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-311">It can be retrieved from hello dictionary object that is passed tooyour components when they are initialized.</span></span>

<span data-ttu-id="d2b9d-312">Pour plus d’informations, consultez hello [ConfigurationManager](#configurationmanager) section de ce document.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-312">For more information, see hello [ConfigurationManager](#configurationmanager) section of this document.</span></span>

### <a name="systemtypeloadexception"></a><span data-ttu-id="d2b9d-313">System.TypeLoadException</span><span class="sxs-lookup"><span data-stu-id="d2b9d-313">System.TypeLoadException</span></span>

<span data-ttu-id="d2b9d-314">Lorsque vous utilisez une topologie c# avec un cluster HDInsight de basés sur Linux, vous pouvez rencontrer hello l’erreur suivante :</span><span class="sxs-lookup"><span data-stu-id="d2b9d-314">When you are using a C# topology with a Linux-based HDInsight cluster, you may encounter hello following error:</span></span>

    System.TypeLoadException: Failure has occurred while loading a type.

<span data-ttu-id="d2b9d-315">Cette erreur se produit lorsque vous utilisez un fichier binaire qui n’est pas compatible avec la version de hello de .NET Mono prend en charge.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-315">This error occurs when you use a binary that is not compatible with hello version of .NET that Mono supports.</span></span>

<span data-ttu-id="d2b9d-316">Pour les clusters HDInsight basés sur Linux, vous devez vous assurer que votre projet utilise des fichiers binaires compilés pour .NET 4.5.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-316">For Linux-based HDInsight clusters, make sure that your project uses binaries compiled for .NET 4.5.</span></span>

### <a name="test-a-topology-locally"></a><span data-ttu-id="d2b9d-317">Test local d’une topologie</span><span class="sxs-lookup"><span data-stu-id="d2b9d-317">Test a topology locally</span></span>

<span data-ttu-id="d2b9d-318">Bien qu’il soit facile toodeploy un cluster de tooa topologie, dans certains cas, vous devrez peut-être tootest une topologie localement.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-318">Although it is easy toodeploy a topology tooa cluster, in some cases, you may need tootest a topology locally.</span></span> <span data-ttu-id="d2b9d-319">Utilisez hello suivant les étapes toorun et tester l’exemple de topologie hello dans ce didacticiel localement dans votre environnement de développement.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-319">Use hello following steps toorun and test hello example topology in this tutorial locally in your development environment.</span></span>

> [!WARNING]
> <span data-ttu-id="d2b9d-320">Le test local fonctionne uniquement pour les topologies exclusivement C# de base.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-320">Local testing only works for basic, C#-only topologies.</span></span> <span data-ttu-id="d2b9d-321">Vous ne pouvez pas employer le test local pour les topologies hybrides ou celles qui utilisent plusieurs flux de données.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-321">You cannot use local testing for hybrid topologies or topologies that use multiple streams.</span></span>

1. <span data-ttu-id="d2b9d-322">Dans **l’Explorateur de solutions**, cliquez sur le projet de hello, puis sélectionnez **propriétés**.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-322">In **Solution Explorer**, right-click hello project, and select **Properties**.</span></span> <span data-ttu-id="d2b9d-323">Dans Propriétés du projet hello, modifiez hello **type de sortie** trop**Application Console**.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-323">In hello project properties, change hello **Output type** too**Console Application**.</span></span>

    ![Capture d’écran des propriétés du projet, avec le type de sortie en surbrillance](./media/hdinsight-storm-develop-csharp-visual-studio-topology/outputtype.png)

   > [!NOTE]
   > <span data-ttu-id="d2b9d-325">N’oubliez pas de toochange hello **type de sortie** sauvegarder trop**bibliothèque de classes** avant de déployer hello topologie tooa cluster.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-325">Remember toochange hello **Output type** back too**Class Library** before you deploy hello topology tooa cluster.</span></span>

2. <span data-ttu-id="d2b9d-326">Dans **l’Explorateur de solutions**, cliquez sur le projet de hello, puis sélectionnez **ajouter** > **un nouvel élément**.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-326">In **Solution Explorer**, right-click hello project, and then select **Add** > **New Item**.</span></span> <span data-ttu-id="d2b9d-327">Sélectionnez **classe**, puis entrez **LocalTest.cs** en tant que nom de la classe hello.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-327">Select **Class**, and enter **LocalTest.cs** as hello class name.</span></span> <span data-ttu-id="d2b9d-328">Enfin, cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-328">Finally, click **Add**.</span></span>

3. <span data-ttu-id="d2b9d-329">Ouvrez **LocalTest.cs**et ajoutez hello suivant **à l’aide de** instruction hello début :</span><span class="sxs-lookup"><span data-stu-id="d2b9d-329">Open **LocalTest.cs**, and add hello following **using** statement at hello top:</span></span>

    ```csharp
    using Microsoft.SCP;
    ```

4. <span data-ttu-id="d2b9d-330">Suivant de hello d’utilisation de code en tant que contenu hello Hello **LocalTest** classe :</span><span class="sxs-lookup"><span data-stu-id="d2b9d-330">Use hello following code as hello contents of hello **LocalTest** class:</span></span>

    ```csharp
    // Drives hello topology components
    public void RunTestCase()
    {
        // An empty dictionary for use when creating components
        Dictionary<string, Object> emptyDictionary = new Dictionary<string, object>();

        #region Test hello spout
        {
            Console.WriteLine("Starting spout");
            // LocalContext is a local-mode context that can be used tooinitialize
            // components in hello development environment.
            LocalContext spoutCtx = LocalContext.Get();
            // Get a new instance of hello spout, using hello local context
            Spout sentences = Spout.Get(spoutCtx, emptyDictionary);

            // Emit 10 tuples
            for (int i = 0; i < 10; i++)
            {
                sentences.NextTuple(emptyDictionary);
            }
            // Use LocalContext toopersist hello data stream toofile
            spoutCtx.WriteMsgQueueToFile("sentences.txt");
            Console.WriteLine("Spout finished");
        }
        #endregion

        #region Test hello splitter bolt
        {
            Console.WriteLine("Starting splitter bolt");
            // LocalContext is a local-mode context that can be used tooinitialize
            // components in hello development environment.
            LocalContext splitterCtx = LocalContext.Get();
            // Get a new instance of hello bolt
            Splitter splitter = Splitter.Get(splitterCtx, emptyDictionary);

            // Set hello data stream toohello data created by hello spout
            splitterCtx.ReadFromFileToMsgQueue("sentences.txt");
            // Get a batch of tuples from hello stream
            List<SCPTuple> batch = splitterCtx.RecvFromMsgQueue();
            // Process each tuple in hello batch
            foreach (SCPTuple tuple in batch)
            {
                splitter.Execute(tuple);
            }
            // Use LocalContext toopersist hello data stream toofile
            splitterCtx.WriteMsgQueueToFile("splitter.txt");
            Console.WriteLine("Splitter bolt finished");
        }
        #endregion

        #region Test hello counter bolt
        {
            Console.WriteLine("Starting counter bolt");
            // LocalContext is a local-mode context that can be used tooinitialize
            // components in hello development environment.
            LocalContext counterCtx = LocalContext.Get();
            // Get a new instance of hello bolt
            Counter counter = Counter.Get(counterCtx, emptyDictionary);

            // Set hello data stream toohello data created by splitter bolt
            counterCtx.ReadFromFileToMsgQueue("splitter.txt");
            // Get a batch of tuples from hello stream
            List<SCPTuple> batch = counterCtx.RecvFromMsgQueue();
            // Process each tuple in hello batch
            foreach (SCPTuple tuple in batch)
            {
                counter.Execute(tuple);
            }
            // Use LocalContext toopersist hello data stream toofile
            counterCtx.WriteMsgQueueToFile("counter.txt");
            Console.WriteLine("Counter bolt finished");
        }
        #endregion
    }
    ```

    <span data-ttu-id="d2b9d-331">Prendre un tooread moment par le biais des commentaires de code hello.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-331">Take a moment tooread through hello code comments.</span></span> <span data-ttu-id="d2b9d-332">Ce code utilise **LocalContext** toorun des composants de hello dans l’environnement de développement hello et il persiste le flux de données hello entre composants tootext fichiers sur le disque local hello.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-332">This code uses **LocalContext** toorun hello components in hello development environment, and it persists hello data stream between components tootext files on hello local drive.</span></span>

1. <span data-ttu-id="d2b9d-333">Ouvrez **Program.cs**et ajoutez hello suivant toohello **Main** méthode :</span><span class="sxs-lookup"><span data-stu-id="d2b9d-333">Open **Program.cs**, and add hello following toohello **Main** method:</span></span>

    ```csharp
    Console.WriteLine("Starting tests");
    System.Environment.SetEnvironmentVariable("microsoft.scp.logPrefix", "WordCount-LocalTest");
    // Initialize hello runtime
    SCPRuntime.Initialize();

    //If we are not running under hello local context, throw an error
    if (Context.pluginType != SCPPluginType.SCP_NET_LOCAL)
    {
        throw new Exception(string.Format("unexpected pluginType: {0}", Context.pluginType));
    }
    // Create test instance
    LocalTest tests = new LocalTest();
    // Run tests
    tests.RunTestCase();
    Console.WriteLine("Tests finished");
    Console.ReadKey();
    ```

2. <span data-ttu-id="d2b9d-334">Enregistrer les modifications de hello, puis cliquez sur **F5** ou sélectionnez **déboguer** > **démarrer le débogage** projet hello de toostart.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-334">Save hello changes, and then click **F5** or select **Debug** > **Start Debugging** toostart hello project.</span></span> <span data-ttu-id="d2b9d-335">Une fenêtre de console doit apparaître et l’état du journal en tant que la progression des tests hello.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-335">A console window should appear, and log status as hello tests progress.</span></span> <span data-ttu-id="d2b9d-336">Lorsque **Tests terminé** s’affiche, appuyez sur n’importe quelle fenêtre de hello tooclose clé.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-336">When **Tests finished** appears, press any key tooclose hello window.</span></span>

3. <span data-ttu-id="d2b9d-337">Utilisez **l’Explorateur Windows** directory hello toolocate qui contient votre projet.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-337">Use **Windows Explorer** toolocate hello directory that contains your project.</span></span> <span data-ttu-id="d2b9d-338">Par exemple : **C:\Utilisateurs\<votre_nom_utilisateur>\Documents\Visual Studio 2013\Projects\WordCount\WordCount**.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-338">For example: **C:\Users\<your_user_name>\Documents\Visual Studio 2013\Projects\WordCount\WordCount**.</span></span> <span data-ttu-id="d2b9d-339">Dans ce répertoire, ouvrez **Bin**, puis cliquez sur **Débogage**.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-339">In this directory, open **Bin**, and then click **Debug**.</span></span> <span data-ttu-id="d2b9d-340">Vous devez voir les fichiers de texte hello qui ont été générés lors de l’exécution de tests de hello : sentences.txt, counter.txt et splitter.txt.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-340">You should see hello text files that were produced when hello tests ran: sentences.txt, counter.txt, and splitter.txt.</span></span> <span data-ttu-id="d2b9d-341">Ouvrez chaque fichier texte et inspecter les données de salutation.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-341">Open each text file and inspect hello data.</span></span>

   > [!NOTE]
   > <span data-ttu-id="d2b9d-342">Les chaînes de données sont conservées sous forme de tableau de valeurs décimales dans ces fichiers.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-342">String data persists as an array of decimal values in these files.</span></span> <span data-ttu-id="d2b9d-343">Par exemple, \[[97,103,111]] Bonjour **splitter.txt** fichier hello est *et*.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-343">For example, \[[97,103,111]] in hello **splitter.txt** file is hello word *and*.</span></span>

> [!NOTE]
> <span data-ttu-id="d2b9d-344">Être vraiment tooset hello **type de projet** sauvegarder trop**bibliothèque de classes** avant de déployer tooa Storm sur le cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-344">Be sure tooset hello **Project type** back too**Class Library** before deploying tooa Storm on HDInsight cluster.</span></span>

### <a name="log-information"></a><span data-ttu-id="d2b9d-345">Enregistrement d’informations</span><span class="sxs-lookup"><span data-stu-id="d2b9d-345">Log information</span></span>

<span data-ttu-id="d2b9d-346">Vous pouvez facilement enregistrer des informations à partir de vos composants de topologie à l’aide de `Context.Logger`.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-346">You can easily log information from your topology components by using `Context.Logger`.</span></span> <span data-ttu-id="d2b9d-347">Par exemple, suivant de hello crée une entrée de journal d’information :</span><span class="sxs-lookup"><span data-stu-id="d2b9d-347">For example, hello following creates an informational log entry:</span></span>

```csharp
Context.Logger.Info("Component started");
```

<span data-ttu-id="d2b9d-348">Informations enregistrées peuvent être consultées dans hello **journal du Service Hadoop**, qui se trouve dans **l’Explorateur de serveurs**.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-348">Logged information can be viewed from hello **Hadoop Service Log**, which is found in **Server Explorer**.</span></span> <span data-ttu-id="d2b9d-349">Entrée de hello pour votre Storm sur le cluster HDInsight, puis **journal du Service Hadoop**.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-349">Expand hello entry for your Storm on HDInsight cluster, and then expand **Hadoop Service Log**.</span></span> <span data-ttu-id="d2b9d-350">Enfin, sélectionnez tooview de fichier journal hello.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-350">Finally, select hello log file tooview.</span></span>

> [!NOTE]
> <span data-ttu-id="d2b9d-351">Hello journaux sont stockés dans hello compte de stockage Azure qui est utilisé par votre cluster.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-351">hello logs are stored in hello Azure storage account that is used by your cluster.</span></span> <span data-ttu-id="d2b9d-352">journaux de hello tooview dans Visual Studio, vous devez vous connecter toohello abonnement Azure propriétaire du compte de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-352">tooview hello logs in Visual Studio, you must sign in toohello Azure subscription that owns hello storage account.</span></span>

### <a name="view-error-information"></a><span data-ttu-id="d2b9d-353">Afficher les informations relatives aux erreurs</span><span class="sxs-lookup"><span data-stu-id="d2b9d-353">View error information</span></span>

<span data-ttu-id="d2b9d-354">tooview les erreurs qui se sont produites dans une topologie en cours d’exécution, utilisez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="d2b9d-354">tooview errors that have occurred in a running topology, use hello following steps:</span></span>

1. <span data-ttu-id="d2b9d-355">À partir de **l’Explorateur de serveurs**, avec le bouton droit hello Storm sur le cluster HDInsight, puis sélectionnez **topologies de vue Storm**.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-355">From **Server Explorer**, right-click hello Storm on HDInsight cluster, and select **View Storm topologies**.</span></span>

2. <span data-ttu-id="d2b9d-356">Pourquoi **bec** et **boulons**, hello **dernière erreur** colonne contienne des informations sur la dernière erreur de hello.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-356">For hello **Spout** and **Bolts**, hello **Last Error** column contains information on hello last error.</span></span>

3. <span data-ttu-id="d2b9d-357">Sélectionnez hello **Id de bec** ou **éclair Id** pour le composant hello qui comporte une erreur répertoriée.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-357">Select hello **Spout Id** or **Bolt Id** for hello component that has an error listed.</span></span> <span data-ttu-id="d2b9d-358">Sur page de détails hello erreur affichée, d’autres informations sont répertoriées dans hello **erreurs** section bas hello de page de hello.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-358">On hello details page that is displayed, additional error information is listed in hello **Errors** section at hello bottom of hello page.</span></span>

4. <span data-ttu-id="d2b9d-359">tooobtain plus d’informations, sélectionnez un **Port** de hello **exécuteurs** section de la page de hello, journal toosee hello Storm travail hello dernières minutes.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-359">tooobtain more information, select a **Port** from hello **Executors** section of hello page, toosee hello Storm worker log for hello last few minutes.</span></span>

### <a name="errors-submitting-topologies"></a><span data-ttu-id="d2b9d-360">Erreurs lors de la soumission des topologies</span><span class="sxs-lookup"><span data-stu-id="d2b9d-360">Errors submitting topologies</span></span>

<span data-ttu-id="d2b9d-361">Si vous rencontrez des erreurs soumettant une tooHDInsight topologie, vous trouverez les journaux pour les composants côté serveur hello qui gèrent la soumission de topologie sur votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-361">If you encounter errors submitting a topology tooHDInsight, you can find logs for hello server-side components that handle topology submission on your HDInsight cluster.</span></span> <span data-ttu-id="d2b9d-362">tooretrieve ces journaux, hello utilisez commande suivante à partir d’une ligne de commande :</span><span class="sxs-lookup"><span data-stu-id="d2b9d-362">tooretrieve these logs, use hello following command from a command line:</span></span>

    scp sshuser@clustername-ssh.azurehdinsight.net:/var/log/hdinsight-scpwebapi/hdinsight-scpwebapi.out .

<span data-ttu-id="d2b9d-363">Remplacez __sshuser__ avec hello compte d’utilisateur SSH pour le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-363">Replace __sshuser__ with hello SSH user account for hello cluster.</span></span> <span data-ttu-id="d2b9d-364">Remplacez __clustername__ avec nom hello du cluster HDInsight de hello.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-364">Replace __clustername__ with hello name of hello HDInsight cluster.</span></span> <span data-ttu-id="d2b9d-365">Pour en savoir plus sur l’utilisation de `scp` et de `ssh` avec HDInsight, voir [Utilisation de SSH avec HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="d2b9d-365">For more information on using `scp` and `ssh` with HDInsight, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="d2b9d-366">Les envois peuvent échouer pour plusieurs raisons :</span><span class="sxs-lookup"><span data-stu-id="d2b9d-366">Submissions can fail for multiple reasons:</span></span>

* <span data-ttu-id="d2b9d-367">JDK n’est pas installé ou n’est pas dans le chemin d’accès hello.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-367">JDK is not installed or is not in hello path.</span></span>
* <span data-ttu-id="d2b9d-368">Dépendances de Java requises ne sont pas inclus dans l’envoi de hello.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-368">Required Java dependencies are not included in hello submission.</span></span>
* <span data-ttu-id="d2b9d-369">Dépendances incompatibles.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-369">Incompatible dependencies.</span></span>
* <span data-ttu-id="d2b9d-370">Dupliquer les noms de topologie.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-370">Duplicate topology names.</span></span>

<span data-ttu-id="d2b9d-371">Si hello `hdinsight-scpwebapi.out` journal contient un `FileNotFoundException`, cela peut être dû à hello conditions suivantes :</span><span class="sxs-lookup"><span data-stu-id="d2b9d-371">If hello `hdinsight-scpwebapi.out` log contains a `FileNotFoundException`, this might be caused by hello following conditions:</span></span>

* <span data-ttu-id="d2b9d-372">Hello JDK n’est pas un chemin d’accès de hello sur l’environnement de développement hello.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-372">hello JDK is not in hello path on hello development environment.</span></span> <span data-ttu-id="d2b9d-373">Vérifiez que hello JDK est installé dans l’environnement de développement hello et que `%JAVA_HOME%/bin` est dans le chemin d’accès hello.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-373">Verify that hello JDK is installed in hello development environment, and that `%JAVA_HOME%/bin` is in hello path.</span></span>
* <span data-ttu-id="d2b9d-374">Il manque une dépendance Java.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-374">You are missing a Java dependency.</span></span> <span data-ttu-id="d2b9d-375">Assurez-vous que vous incluez tous les fichiers .jar requis dans le cadre de l’envoi de hello.</span><span class="sxs-lookup"><span data-stu-id="d2b9d-375">Make sure you are including any required .jar files as part of hello submission.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d2b9d-376">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d2b9d-376">Next steps</span></span>

<span data-ttu-id="d2b9d-377">Pour un exemple de traitement des données à partir des Event Hubs, voir [Traiter des événements d’Azure Event Hubs avec Storm sur HDInsight](hdinsight-storm-develop-csharp-event-hub-topology.md).</span><span class="sxs-lookup"><span data-stu-id="d2b9d-377">For an example of processing data from Event Hubs, see [Process events from Azure Event Hubs with Storm on HDInsight](hdinsight-storm-develop-csharp-event-hub-topology.md).</span></span>

<span data-ttu-id="d2b9d-378">Pour obtenir un exemple de topologie C# qui fractionne les données de flux en plusieurs flux de données, consultez la rubrique [Exemple c# Storm](https://github.com/Blackmist/csharp-storm-example).</span><span class="sxs-lookup"><span data-stu-id="d2b9d-378">For an example of a C# topology that splits stream data into multiple streams, see [C# Storm example](https://github.com/Blackmist/csharp-storm-example).</span></span>

<span data-ttu-id="d2b9d-379">toodiscover plus d’informations sur la création de topologies de c#, consultez [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/SCPNet-GettingStarted.md).</span><span class="sxs-lookup"><span data-stu-id="d2b9d-379">toodiscover more information about creating C# topologies, see [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/SCPNet-GettingStarted.md).</span></span>

<span data-ttu-id="d2b9d-380">Pour plus toowork manières avec HDInsight et Storm plus sur les échantillons de HDInsight, consultez hello suivant des documents :</span><span class="sxs-lookup"><span data-stu-id="d2b9d-380">For more ways toowork with HDInsight and more Storm on HDInsight samples, see hello following documents:</span></span>

<span data-ttu-id="d2b9d-381">**Microsoft SCP.NET**</span><span class="sxs-lookup"><span data-stu-id="d2b9d-381">**Microsoft SCP.NET**</span></span>

* [<span data-ttu-id="d2b9d-382">Guide de programmation SCP</span><span class="sxs-lookup"><span data-stu-id="d2b9d-382">SCP programming guide</span></span>](hdinsight-storm-scp-programming-guide.md)

<span data-ttu-id="d2b9d-383">**Apache Storm sur HDInsight**</span><span class="sxs-lookup"><span data-stu-id="d2b9d-383">**Apache Storm on HDInsight**</span></span>

* [<span data-ttu-id="d2b9d-384">Déploiement et analyse des topologies avec Apache Storm sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="d2b9d-384">Deploy and monitor topologies with Apache Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology.md)
* [<span data-ttu-id="d2b9d-385">Exemples de topologies pour Storm dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="d2b9d-385">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)

<span data-ttu-id="d2b9d-386">**Apache Hadoop sur HDInsight**</span><span class="sxs-lookup"><span data-stu-id="d2b9d-386">**Apache Hadoop on HDInsight**</span></span>

* [<span data-ttu-id="d2b9d-387">Utilisation de Hive avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="d2b9d-387">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="d2b9d-388">Utilisation de Pig avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="d2b9d-388">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="d2b9d-389">Utilisation de MapReduce avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="d2b9d-389">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="d2b9d-390">**Apache HBase sur HDInsight**</span><span class="sxs-lookup"><span data-stu-id="d2b9d-390">**Apache HBase on HDInsight**</span></span>

* [<span data-ttu-id="d2b9d-391">Prise en main de HBase sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="d2b9d-391">Getting started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started.md)
