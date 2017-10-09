---
title: "tâches d’aaaRun Apache Pig avec le Kit de développement .NET pour Hadoop - Azure HDInsight | Documents Microsoft"
description: "Découvrez comment toouse hello .NET SDK pour tooHadoop de tâches Pig Hadoop toosubmit sur HDInsight."
services: hdinsight
documentationcenter: .net
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: fa11d49a-328c-47e7-b16d-e7ed2a453195
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/15/2017
ms.author: larryfr
ms.openlocfilehash: 1d4ceebd7c168372d23fe29a088f04676686de30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="run-pig-jobs-using-hello-net-sdk-for-hadoop-in-hdinsight"></a><span data-ttu-id="30ad7-103">Exécuter des travaux Pig à l’aide de hello .NET SDK pour Hadoop dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="30ad7-103">Run Pig jobs using hello .NET SDK for Hadoop in HDInsight</span></span>

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="30ad7-104">Découvrez comment toouse hello .NET SDK pour Hadoop toosubmit Apache Pig travaux tooHadoop sur Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="30ad7-104">Learn how toouse hello .NET SDK for Hadoop toosubmit Apache Pig jobs tooHadoop on Azure HDInsight.</span></span>

<span data-ttu-id="30ad7-105">Hello HDInsight .NET SDK fournit des bibliothèques clientes .NET qui le rend plus facile toowork avec des clusters HDInsight à partir de .NET.</span><span class="sxs-lookup"><span data-stu-id="30ad7-105">hello HDInsight .NET SDK provides .NET client libraries that makes it easier toowork with HDInsight clusters from .NET.</span></span> <span data-ttu-id="30ad7-106">Pig vous permet de toocreate MapReduce opérations en une série de transformations de données de modélisation.</span><span class="sxs-lookup"><span data-stu-id="30ad7-106">Pig allows you toocreate MapReduce operations by modeling a series of data transformations.</span></span> <span data-ttu-id="30ad7-107">Dans ce document, vous découvrez comment toouse base c# application toosubmit un Pig travail tooan HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="30ad7-107">In this document, you learn how toouse a basic C# application toosubmit a Pig job tooan HDInsight cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="30ad7-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="30ad7-108">Prerequisites</span></span>

<span data-ttu-id="30ad7-109">toocomplete hello étapes décrites dans cet article, hello éléments suivants sont nécessaires.</span><span class="sxs-lookup"><span data-stu-id="30ad7-109">toocomplete hello steps in this article, you need hello following.</span></span>

* <span data-ttu-id="30ad7-110">Un cluster Azure HDInsight (Hadoop sur HDInsight) Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="30ad7-110">An Azure HDInsight (Hadoop on HDInsight) cluster (either Windows or Linux-based).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="30ad7-111">Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="30ad7-111">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="30ad7-112">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="30ad7-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="30ad7-113">Visual Studio 2012, 2013, 2015 ou 2017.</span><span class="sxs-lookup"><span data-stu-id="30ad7-113">Visual Studio 2012, 2013, 2015 or 2017.</span></span>

## <a name="create-hello-application"></a><span data-ttu-id="30ad7-114">Créer l’application hello</span><span class="sxs-lookup"><span data-stu-id="30ad7-114">Create hello application</span></span>

<span data-ttu-id="30ad7-115">Hello HDInsight .NET SDK fournit des bibliothèques de client .NET, ce qui le rend plus facile toowork avec des clusters HDInsight à partir de .NET.</span><span class="sxs-lookup"><span data-stu-id="30ad7-115">hello HDInsight .NET SDK provides .NET client libraries, which makes it easier toowork with HDInsight clusters from .NET.</span></span>

1. <span data-ttu-id="30ad7-116">À partir de hello **fichier** menu dans Visual Studio, sélectionnez **nouveau** , puis sélectionnez **projet**.</span><span class="sxs-lookup"><span data-stu-id="30ad7-116">From hello **File** menu in Visual Studio, select **New** and then select **Project**.</span></span>

2. <span data-ttu-id="30ad7-117">Nouveau projet de hello, type ou sélectionnez hello suivant des valeurs :</span><span class="sxs-lookup"><span data-stu-id="30ad7-117">For hello new project, type or select hello following values:</span></span>

   | <span data-ttu-id="30ad7-118">Propriété</span><span class="sxs-lookup"><span data-stu-id="30ad7-118">Property</span></span> | <span data-ttu-id="30ad7-119">Valeur</span><span class="sxs-lookup"><span data-stu-id="30ad7-119">Value</span></span> |
   | ------ | ------ |
   | <span data-ttu-id="30ad7-120">Catégorie</span><span class="sxs-lookup"><span data-stu-id="30ad7-120">Category</span></span> | <span data-ttu-id="30ad7-121">Modèles/Visual C#/Windows</span><span class="sxs-lookup"><span data-stu-id="30ad7-121">Templates/Visual C#/Windows</span></span> |
   | <span data-ttu-id="30ad7-122">Modèle</span><span class="sxs-lookup"><span data-stu-id="30ad7-122">Template</span></span> | <span data-ttu-id="30ad7-123">Application console</span><span class="sxs-lookup"><span data-stu-id="30ad7-123">Console Application</span></span> |
   | <span data-ttu-id="30ad7-124">Nom</span><span class="sxs-lookup"><span data-stu-id="30ad7-124">Name</span></span> | <span data-ttu-id="30ad7-125">SubmitPigJob</span><span class="sxs-lookup"><span data-stu-id="30ad7-125">SubmitPigJob</span></span> |

3. <span data-ttu-id="30ad7-126">Cliquez sur **OK** projet hello de toocreate.</span><span class="sxs-lookup"><span data-stu-id="30ad7-126">Click **OK** toocreate hello project.</span></span>

4. <span data-ttu-id="30ad7-127">À partir de hello **outils** menu, sélectionnez **Gestionnaire de Package de bibliothèque** ou **Gestionnaire de Package Nuget**, puis sélectionnez **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="30ad7-127">From hello **Tools** menu, select **Library Package Manager** or **Nuget Package Manager**, and then select **Package Manager Console**.</span></span>

5. <span data-ttu-id="30ad7-128">packages de développement .NET SDK tooinstall hello, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="30ad7-128">tooinstall hello .NET SDK packages, use hello following command:</span></span>

        Install-Package Microsoft.Azure.Management.HDInsight.Job

6. <span data-ttu-id="30ad7-129">Dans l’Explorateur de solutions, double-cliquez sur **Program.cs** tooopen il.</span><span class="sxs-lookup"><span data-stu-id="30ad7-129">From Solution Explorer, double-click **Program.cs** tooopen it.</span></span> <span data-ttu-id="30ad7-130">Remplacez le code existant hello suivant de hello.</span><span class="sxs-lookup"><span data-stu-id="30ad7-130">Replace hello existing code with hello following.</span></span>

    ```csharp
    using Microsoft.Azure.Management.HDInsight.Job;
    using Microsoft.Azure.Management.HDInsight.Job.Models;
    using Hyak.Common;

    namespace SubmitHDInsightJobDotNet
    {
        class Program
        {
            private static HDInsightJobManagementClient _hdiJobManagementClient;

            private const string ExistingClusterName = "<Your HDInsight Cluster Name>";
            private const string ExistingClusterUri = ExistingClusterName + ".azurehdinsight.net";
            private const string ExistingClusterUsername = "<Cluster Username>";
            private const string ExistingClusterPassword = "<Cluster User Password>";

            static void Main(string[] args)
            {
                System.Console.WriteLine("hello application is running ...");

                var clusterCredentials = new BasicAuthenticationCloudCredentials { Username = ExistingClusterUsername, Password = ExistingClusterPassword };
                _hdiJobManagementClient = new HDInsightJobManagementClient(ExistingClusterUri, clusterCredentials);

                SubmitPigJob();

                System.Console.WriteLine("Press ENTER toocontinue ...");
                System.Console.ReadLine();
            }

            private static void SubmitPigJob()
            {
                var parameters = new PigJobSubmissionParameters
                {
                    Query = @"LOGS = LOAD '/example/data/sample.log';
                                LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
                                FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
                                GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
                                FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
                                RESULT = order FREQUENCIES by COUNT desc;
                                DUMP RESULT;"
                };

                System.Console.WriteLine("Submitting hello Pig job toohello cluster...");
                var response = _hdiJobManagementClient.JobManagement.SubmitPigJob(parameters);
                System.Console.WriteLine("Validating that hello response is as expected...");
                System.Console.WriteLine("Response status code is " + response.StatusCode);
                System.Console.WriteLine("Validating hello response object...");
                System.Console.WriteLine("JobId is " + response.JobSubmissionJsonResponse.Id);
            }
        }
    }
    ```

7. <span data-ttu-id="30ad7-131">application de hello toostart, appuyez sur **F5**.</span><span class="sxs-lookup"><span data-stu-id="30ad7-131">toostart hello application, press **F5**.</span></span>

8. <span data-ttu-id="30ad7-132">application de hello tooexit, appuyez sur **entrée**.</span><span class="sxs-lookup"><span data-stu-id="30ad7-132">tooexit hello application, press **ENTER**.</span></span>

## <a name="summary"></a><span data-ttu-id="30ad7-133">Résumé</span><span class="sxs-lookup"><span data-stu-id="30ad7-133">Summary</span></span>

<span data-ttu-id="30ad7-134">Comme vous pouvez le voir, hello .NET SDK pour Hadoop vous permet des applications .NET toocreate soumettre le cluster HDInsight de Pig travaux tooan et de surveillance d’état du travail hello.</span><span class="sxs-lookup"><span data-stu-id="30ad7-134">As you can see, hello .NET SDK for Hadoop allows you toocreate .NET applications that submit Pig jobs tooan HDInsight cluster, and monitor hello job status.</span></span>

## <a name="next-steps"></a><span data-ttu-id="30ad7-135">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="30ad7-135">Next steps</span></span>

<span data-ttu-id="30ad7-136">Pour plus d’informations sur Pig dans HDInsight, consultez [Utilisation de Pig avec Hadoop sur HDInsight](hdinsight-use-pig.md).</span><span class="sxs-lookup"><span data-stu-id="30ad7-136">For information on Pig in HDInsight, see [Use Pig with Hadoop on HDInsight](hdinsight-use-pig.md).</span></span>

<span data-ttu-id="30ad7-137">Pour plus d’informations sur l’utilisation de Hadoop sur HDInsight, consultez hello suivant des documents :</span><span class="sxs-lookup"><span data-stu-id="30ad7-137">For more information on using Hadoop on HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="30ad7-138">Utilisation de Hive avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="30ad7-138">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="30ad7-139">Utilisation de MapReduce avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="30ad7-139">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

[preview-portal]: https://portal.azure.com/
