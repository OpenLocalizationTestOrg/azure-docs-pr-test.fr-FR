---
title: "Exécuter des travaux Apache Pig avec le Kit de développement .NET pour Hadoop - Azure HDInsight | Documents Microsoft"
description: "Apprenez à utiliser le Kit de développement logiciel (SDK) .NET pour Hadoop afin de soumettre des tâches Pig vers Hadoop sur HDInsight."
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
ms.openlocfilehash: e40d152821b36852c447d5a3adfd39114edbbace
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="run-pig-jobs-using-the-net-sdk-for-hadoop-in-hdinsight"></a><span data-ttu-id="b4583-103">Exécution de tâches Pig à l’aide du Kit de développement logiciel (SDK) .NET pour Hadoop dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="b4583-103">Run Pig jobs using the .NET SDK for Hadoop in HDInsight</span></span>

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="b4583-104">Apprenez à utiliser le Kit de développement logiciel (SDK) .NET pour Hadoop afin de soumettre des travaux Pig vers Hadoop sur Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b4583-104">Learn how to use the .NET SDK for Hadoop to submit Apache Pig jobs to Hadoop on Azure HDInsight.</span></span>

<span data-ttu-id="b4583-105">Le Kit de développement logiciel (SDK) .NET HDInsight fournit des bibliothèques clientes .NET facilitant l'utilisation des clusters HDInsight à partir de .NET.</span><span class="sxs-lookup"><span data-stu-id="b4583-105">The HDInsight .NET SDK provides .NET client libraries that makes it easier to work with HDInsight clusters from .NET.</span></span> <span data-ttu-id="b4583-106">Pig permet de créer des opérations MapReduce en modélisant une série de transformations de données.</span><span class="sxs-lookup"><span data-stu-id="b4583-106">Pig allows you to create MapReduce operations by modeling a series of data transformations.</span></span> <span data-ttu-id="b4583-107">Dans ce document, vous apprenez à utiliser une application de base C# pour soumettre un travail Pig sur un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b4583-107">In this document, you learn how to use a basic C# application to submit a Pig job to an HDInsight cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b4583-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="b4583-108">Prerequisites</span></span>

<span data-ttu-id="b4583-109">Pour effectuer les étapes de cet article, vous avez besoin des éléments suivants.</span><span class="sxs-lookup"><span data-stu-id="b4583-109">To complete the steps in this article, you need the following.</span></span>

* <span data-ttu-id="b4583-110">Un cluster Azure HDInsight (Hadoop sur HDInsight) Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="b4583-110">An Azure HDInsight (Hadoop on HDInsight) cluster (either Windows or Linux-based).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="b4583-111">Linux est le seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="b4583-111">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="b4583-112">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="b4583-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="b4583-113">Visual Studio 2012, 2013, 2015 ou 2017.</span><span class="sxs-lookup"><span data-stu-id="b4583-113">Visual Studio 2012, 2013, 2015 or 2017.</span></span>

## <a name="create-the-application"></a><span data-ttu-id="b4583-114">Création de l’application</span><span class="sxs-lookup"><span data-stu-id="b4583-114">Create the application</span></span>

<span data-ttu-id="b4583-115">Le Kit de développement logiciel (SDK) HDInsight .NET fournit des bibliothèques clientes .NET, ce qui facilite l'utilisation des clusters HDInsight à partir de .NET.</span><span class="sxs-lookup"><span data-stu-id="b4583-115">The HDInsight .NET SDK provides .NET client libraries, which makes it easier to work with HDInsight clusters from .NET.</span></span>

1. <span data-ttu-id="b4583-116">Dans le menu **Fichier** de Visual Studio, sélectionnez **Nouveau**, puis **Projet**.</span><span class="sxs-lookup"><span data-stu-id="b4583-116">From the **File** menu in Visual Studio, select **New** and then select **Project**.</span></span>

2. <span data-ttu-id="b4583-117">Pour le nouveau projet, tapez ou sélectionnez les valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="b4583-117">For the new project, type or select the following values:</span></span>

   | <span data-ttu-id="b4583-118">Propriété</span><span class="sxs-lookup"><span data-stu-id="b4583-118">Property</span></span> | <span data-ttu-id="b4583-119">Valeur</span><span class="sxs-lookup"><span data-stu-id="b4583-119">Value</span></span> |
   | ------ | ------ |
   | <span data-ttu-id="b4583-120">Catégorie</span><span class="sxs-lookup"><span data-stu-id="b4583-120">Category</span></span> | <span data-ttu-id="b4583-121">Modèles/Visual C#/Windows</span><span class="sxs-lookup"><span data-stu-id="b4583-121">Templates/Visual C#/Windows</span></span> |
   | <span data-ttu-id="b4583-122">Modèle</span><span class="sxs-lookup"><span data-stu-id="b4583-122">Template</span></span> | <span data-ttu-id="b4583-123">Application console</span><span class="sxs-lookup"><span data-stu-id="b4583-123">Console Application</span></span> |
   | <span data-ttu-id="b4583-124">Nom</span><span class="sxs-lookup"><span data-stu-id="b4583-124">Name</span></span> | <span data-ttu-id="b4583-125">SubmitPigJob</span><span class="sxs-lookup"><span data-stu-id="b4583-125">SubmitPigJob</span></span> |

3. <span data-ttu-id="b4583-126">Cliquez sur **OK** pour créer le projet.</span><span class="sxs-lookup"><span data-stu-id="b4583-126">Click **OK** to create the project.</span></span>

4. <span data-ttu-id="b4583-127">À partir du menu **Outils**, sélectionnez **Gestionnaire de package de bibliothèque** ou **Gestionnaire de package Nuget**, puis sélectionnez **Console du gestionnaire de package**.</span><span class="sxs-lookup"><span data-stu-id="b4583-127">From the **Tools** menu, select **Library Package Manager** or **Nuget Package Manager**, and then select **Package Manager Console**.</span></span>

5. <span data-ttu-id="b4583-128">Pour installer les packages du Kit de développement logiciel (SDK) .NET, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="b4583-128">To install the .NET SDK packages, use the following command:</span></span>

        Install-Package Microsoft.Azure.Management.HDInsight.Job

6. <span data-ttu-id="b4583-129">Dans l'Explorateur de solutions, double-cliquez sur **Program.cs** pour l'ouvrir.</span><span class="sxs-lookup"><span data-stu-id="b4583-129">From Solution Explorer, double-click **Program.cs** to open it.</span></span> <span data-ttu-id="b4583-130">Remplacez le code existant par ce qui suit.</span><span class="sxs-lookup"><span data-stu-id="b4583-130">Replace the existing code with the following.</span></span>

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
                System.Console.WriteLine("The application is running ...");

                var clusterCredentials = new BasicAuthenticationCloudCredentials { Username = ExistingClusterUsername, Password = ExistingClusterPassword };
                _hdiJobManagementClient = new HDInsightJobManagementClient(ExistingClusterUri, clusterCredentials);

                SubmitPigJob();

                System.Console.WriteLine("Press ENTER to continue ...");
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

                System.Console.WriteLine("Submitting the Pig job to the cluster...");
                var response = _hdiJobManagementClient.JobManagement.SubmitPigJob(parameters);
                System.Console.WriteLine("Validating that the response is as expected...");
                System.Console.WriteLine("Response status code is " + response.StatusCode);
                System.Console.WriteLine("Validating the response object...");
                System.Console.WriteLine("JobId is " + response.JobSubmissionJsonResponse.Id);
            }
        }
    }
    ```

7. <span data-ttu-id="b4583-131">Pour démarrer l’application, appuyez sur **F5**.</span><span class="sxs-lookup"><span data-stu-id="b4583-131">To start the application, press **F5**.</span></span>

8. <span data-ttu-id="b4583-132">Pour quitter l’application, appuyez sur **Entrée**.</span><span class="sxs-lookup"><span data-stu-id="b4583-132">To exit the application, press **ENTER**.</span></span>

## <a name="summary"></a><span data-ttu-id="b4583-133">Résumé</span><span class="sxs-lookup"><span data-stu-id="b4583-133">Summary</span></span>

<span data-ttu-id="b4583-134">Comme vous pouvez le voir, le Kit de développement logiciel (SDK) .NET pour Hadoop vous permet de créer des applications .NET qui envoient des tâches Pig à un cluster HDInsight, et de surveiller l’état du travail.</span><span class="sxs-lookup"><span data-stu-id="b4583-134">As you can see, the .NET SDK for Hadoop allows you to create .NET applications that submit Pig jobs to an HDInsight cluster, and monitor the job status.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b4583-135">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b4583-135">Next steps</span></span>

<span data-ttu-id="b4583-136">Pour plus d’informations sur Pig dans HDInsight, consultez [Utilisation de Pig avec Hadoop sur HDInsight](hdinsight-use-pig.md).</span><span class="sxs-lookup"><span data-stu-id="b4583-136">For information on Pig in HDInsight, see [Use Pig with Hadoop on HDInsight](hdinsight-use-pig.md).</span></span>

<span data-ttu-id="b4583-137">Pour plus d’informations sur l’utilisation de Hadoop sur HDInsight, consultez les documents suivants :</span><span class="sxs-lookup"><span data-stu-id="b4583-137">For more information on using Hadoop on HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="b4583-138">Utilisation de Hive avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="b4583-138">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="b4583-139">Utilisation de MapReduce avec Hadoop sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="b4583-139">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

[preview-portal]: https://portal.azure.com/
