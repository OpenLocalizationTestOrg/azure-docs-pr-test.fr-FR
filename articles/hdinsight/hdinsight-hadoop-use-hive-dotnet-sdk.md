---
title: "Exécuter des requêtes Hive avec le Kit de développement logiciel (SDK) .NET HDInsight - Azure | Microsoft Docs"
description: "Apprenez à envoyer des tâches Hadoop à Azure HDInsight Hadoop à l’aide du Kit de développement logiciel (SDK) .NET HDInsight."
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
ms.assetid: 4e291890-f8b4-426c-b5e8-d4fd512ff042
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: jgao
ms.openlocfilehash: 7b1a5f7ea3b2bda438727dc75a85557ea7930280
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="run-hive-queries-using-hdinsight-net-sdk"></a><span data-ttu-id="d77b5-103">Exécuter des requêtes Hive avec le Kit de développement logiciel (SDK) .NET HDInsight</span><span class="sxs-lookup"><span data-stu-id="d77b5-103">Run Hive queries using HDInsight .NET SDK</span></span>
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="d77b5-104">Découvrez comment envoyer des requêtes Hive avec le Kit de développement logiciel (SDK) .NET HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d77b5-104">Learn how to submit Hive queries using HDInsight .NET SDK.</span></span> <span data-ttu-id="d77b5-105">Vous écrivez un programme C# pour soumettre une requête Hive destinée à répertorier les tables Hive, et vous affichez les résultats.</span><span class="sxs-lookup"><span data-stu-id="d77b5-105">You write a C# program to submit a Hive query for listing Hive tables, and display the results.</span></span>

> [!NOTE]
> <span data-ttu-id="d77b5-106">Les étapes décrites dans cet article doivent être effectuées à partir d'un client Windows.</span><span class="sxs-lookup"><span data-stu-id="d77b5-106">The steps in this article must be performed from a Windows client.</span></span> <span data-ttu-id="d77b5-107">Pour plus d’informations sur l’utilisation d’un client Linux, OS X ou Unix pour utiliser Hive, utilisez le sélecteur d’onglet en haut de l’article.</span><span class="sxs-lookup"><span data-stu-id="d77b5-107">For information on using a Linux, OS X, or Unix client to work with Hive, use the tab selector shown on the top of the article.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="d77b5-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="d77b5-108">Prerequisites</span></span>
<span data-ttu-id="d77b5-109">Avant de commencer cet article, vous devez disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="d77b5-109">Before you begin this article, you must have the following items:</span></span>

* <span data-ttu-id="d77b5-110">**Cluster Hadoop dans HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="d77b5-110">**A Hadoop cluster in HDInsight**.</span></span> <span data-ttu-id="d77b5-111">Consultez [Prise en main de Hadoop sous Linux dans HDInsight](./hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d77b5-111">See [Get started using Linux-based Hadoop in HDInsight](./hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>
* <span data-ttu-id="d77b5-112">**Visual Studio 2013/2015/2017**.</span><span class="sxs-lookup"><span data-stu-id="d77b5-112">**Visual Studio 2013/2015/2017**.</span></span>

## <a name="submit-hive-queries-using-hdinsight-net-sdk"></a><span data-ttu-id="d77b5-113">Envoyer des requêtes Hive avec le Kit de développement logiciel (SDK) .NET HDInsight</span><span class="sxs-lookup"><span data-stu-id="d77b5-113">Submit Hive queries using HDInsight .NET SDK</span></span>
<span data-ttu-id="d77b5-114">Le Kit de développement logiciel (SDK) HDInsight .NET fournit des bibliothèques clientes .NET, ce qui facilite l'utilisation des clusters HDInsight à partir de .NET.</span><span class="sxs-lookup"><span data-stu-id="d77b5-114">The HDInsight .NET SDK provides .NET client libraries, which makes it easier to work with HDInsight clusters from .NET.</span></span> 

<span data-ttu-id="d77b5-115">**Pour soumettre les travaux**</span><span class="sxs-lookup"><span data-stu-id="d77b5-115">**To Submit jobs**</span></span>

1. <span data-ttu-id="d77b5-116">Créez une application console C# dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d77b5-116">Create a C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="d77b5-117">À partir de la console du gestionnaire de package NuGet, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="d77b5-117">From the Nuget Package Manager Console, run the following command:</span></span>
   
        Install-Package Microsoft.Azure.Management.HDInsight.Job
3. <span data-ttu-id="d77b5-118">Utilisez le code suivant :</span><span class="sxs-lookup"><span data-stu-id="d77b5-118">Use the following code:</span></span>

    ```csharp
        using System.Collections.Generic;
        using System.IO;
        using System.Text;
        using System.Threading;
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
   
                private const string DefaultStorageAccountName = "<Default Storage Account Name>";
                private const string DefaultStorageAccountKey = "<Default Storage Account Key>";
                private const string DefaultStorageContainerName = "<Default Blob Container Name>";
   
                static void Main(string[] args)
                {
                    System.Console.WriteLine("The application is running ...");
   
                    var clusterCredentials = new BasicAuthenticationCloudCredentials { Username = ExistingClusterUsername, Password = ExistingClusterPassword };
                    _hdiJobManagementClient = new HDInsightJobManagementClient(ExistingClusterUri, clusterCredentials);
   
                    SubmitHiveJob();
   
                    System.Console.WriteLine("Press ENTER to continue ...");
                    System.Console.ReadLine();
                }
   
                private static void SubmitHiveJob()
                {
                    Dictionary<string, string> defines = new Dictionary<string, string> { { "hive.execution.engine", "tez" }, { "hive.exec.reducers.max", "1" } };
                    List<string> args = new List<string> { { "argA" }, { "argB" } };
                    var parameters = new HiveJobSubmissionParameters
                    {
                        Query = "SHOW TABLES",
                        Defines = defines,
                        Arguments = args
                    };
   
                    System.Console.WriteLine("Submitting the Hive job to the cluster...");
                    var jobResponse = _hdiJobManagementClient.JobManagement.SubmitHiveJob(parameters);
                    var jobId = jobResponse.JobSubmissionJsonResponse.Id;
                    System.Console.WriteLine("Response status code is " + jobResponse.StatusCode);
                    System.Console.WriteLine("JobId is " + jobId);
   
                    System.Console.WriteLine("Waiting for the job completion ...");
   
                    // Wait for job completion
                    var jobDetail = _hdiJobManagementClient.JobManagement.GetJob(jobId).JobDetail;
                    while (!jobDetail.Status.JobComplete)
                    {
                        Thread.Sleep(1000);
                        jobDetail = _hdiJobManagementClient.JobManagement.GetJob(jobId).JobDetail;
                    }
   
                    // Get job output
                    var storageAccess = new AzureStorageAccess(DefaultStorageAccountName, DefaultStorageAccountKey,
                        DefaultStorageContainerName);
                    var output = (jobDetail.ExitValue == 0)
                        ? _hdiJobManagementClient.JobManagement.GetJobOutput(jobId, storageAccess) // fetch stdout output in case of success
                        : _hdiJobManagementClient.JobManagement.GetJobErrorLogs(jobId, storageAccess); // fetch stderr output in case of failure
   
                    System.Console.WriteLine("Job output is: ");
   
                    using (var reader = new StreamReader(output, Encoding.UTF8))
                    {
                        string value = reader.ReadToEnd();
                        System.Console.WriteLine(value);
                    }
                }
            }
        }
    ```
4. <span data-ttu-id="d77b5-119">Appuyez sur **F5** pour exécuter l'application.</span><span class="sxs-lookup"><span data-stu-id="d77b5-119">Press **F5** to run the application.</span></span>

<span data-ttu-id="d77b5-120">Le résultat de l’application doit être similaire à :</span><span class="sxs-lookup"><span data-stu-id="d77b5-120">The output of the application shall be similar to:</span></span>

![Résultat de la tâche HDInsight Hadoop Hive](./media/hdinsight-hadoop-use-hive-dotnet-sdk/hdinsight-hadoop-use-hive-net-sdk-output.png)

## <a name="next-steps"></a><span data-ttu-id="d77b5-122">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d77b5-122">Next steps</span></span>
<span data-ttu-id="d77b5-123">Cet article vous a présenté différentes méthodes pour créer un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d77b5-123">In this article, you have learned several ways to create an HDInsight cluster.</span></span> <span data-ttu-id="d77b5-124">Pour en savoir plus, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="d77b5-124">To learn more, see the following articles:</span></span>

* <span data-ttu-id="d77b5-125">[Prise en main d’Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="d77b5-125">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="d77b5-126">[Création de clusters Hadoop dans HDInsight][hdinsight-provision]</span><span class="sxs-lookup"><span data-stu-id="d77b5-126">[Create Hadoop clusters in HDInsight][hdinsight-provision]</span></span>
* [<span data-ttu-id="d77b5-127">Gestion des clusters Hadoop dans HDInsight au moyen du portail Azure</span><span class="sxs-lookup"><span data-stu-id="d77b5-127">Manage Hadoop clusters in HDInsight by using the Azure portal</span></span>](hdinsight-administer-use-management-portal.md)
* [<span data-ttu-id="d77b5-128">Référence du Kit de développement logiciel (SDK) .NET de HDInsight</span><span class="sxs-lookup"><span data-stu-id="d77b5-128">HDInsight .NET SDK reference</span></span>](https://msdn.microsoft.com/library/mt271028.aspx)
* [<span data-ttu-id="d77b5-129">Utilisation de Pig avec HDInsight</span><span class="sxs-lookup"><span data-stu-id="d77b5-129">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="d77b5-130">Utilisation de Sqoop avec HDInsight</span><span class="sxs-lookup"><span data-stu-id="d77b5-130">Use Sqoop with HDInsight</span></span>](hdinsight-use-sqoop-mac-linux.md)
* [<span data-ttu-id="d77b5-131">Créer des applications .NET HDInsight d’authentification non interactives</span><span class="sxs-lookup"><span data-stu-id="d77b5-131">Create non-interactive authentication .NET HDInsight applications</span></span>](hdinsight-create-non-interactive-authentication-dotnet-applications.md)

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md


