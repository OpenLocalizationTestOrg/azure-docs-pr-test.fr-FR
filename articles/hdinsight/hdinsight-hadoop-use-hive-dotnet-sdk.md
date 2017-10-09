---
title: "les requêtes Hive aaaRun à l’aide du SDK .NET HDInsight - Azure | Documents Microsoft"
description: "Découvrez comment toosubmit Hadoop travaux tooAzure HDInsight Hadoop à l’aide du Kit de développement logiciel HDInsight .NET."
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
ms.openlocfilehash: 11f07d90405d3e804774610e242813927df59a03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="run-hive-queries-using-hdinsight-net-sdk"></a><span data-ttu-id="fe000-103">Exécuter des requêtes Hive avec le Kit de développement logiciel (SDK) .NET HDInsight</span><span class="sxs-lookup"><span data-stu-id="fe000-103">Run Hive queries using HDInsight .NET SDK</span></span>
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="fe000-104">Découvrez comment toosubmit ruche interroge à l’aide du Kit de développement logiciel HDInsight .NET.</span><span class="sxs-lookup"><span data-stu-id="fe000-104">Learn how toosubmit Hive queries using HDInsight .NET SDK.</span></span> <span data-ttu-id="fe000-105">Vous écrivez un toosubmit de programme c# une requête Hive pour répertorier les tables de la ruche et afficher les résultats de hello.</span><span class="sxs-lookup"><span data-stu-id="fe000-105">You write a C# program toosubmit a Hive query for listing Hive tables, and display hello results.</span></span>

> [!NOTE]
> <span data-ttu-id="fe000-106">étapes de Hello dans cet article doivent être effectuées à partir d’un client Windows.</span><span class="sxs-lookup"><span data-stu-id="fe000-106">hello steps in this article must be performed from a Windows client.</span></span> <span data-ttu-id="fe000-107">Pour plus d’informations sur l’utilisation d’un Linux, OS X ou Unix client toowork avec Hive, utilisez sélecteur de tabulation hello indiqué en haut de hello d’article de hello.</span><span class="sxs-lookup"><span data-stu-id="fe000-107">For information on using a Linux, OS X, or Unix client toowork with Hive, use hello tab selector shown on hello top of hello article.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="fe000-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="fe000-108">Prerequisites</span></span>
<span data-ttu-id="fe000-109">Avant de commencer cet article, vous devez disposer de hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="fe000-109">Before you begin this article, you must have hello following items:</span></span>

* <span data-ttu-id="fe000-110">**Cluster Hadoop dans HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="fe000-110">**A Hadoop cluster in HDInsight**.</span></span> <span data-ttu-id="fe000-111">Consultez [Prise en main de Hadoop sous Linux dans HDInsight](./hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="fe000-111">See [Get started using Linux-based Hadoop in HDInsight](./hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>
* <span data-ttu-id="fe000-112">**Visual Studio 2013/2015/2017**.</span><span class="sxs-lookup"><span data-stu-id="fe000-112">**Visual Studio 2013/2015/2017**.</span></span>

## <a name="submit-hive-queries-using-hdinsight-net-sdk"></a><span data-ttu-id="fe000-113">Envoyer des requêtes Hive avec le Kit de développement logiciel (SDK) .NET HDInsight</span><span class="sxs-lookup"><span data-stu-id="fe000-113">Submit Hive queries using HDInsight .NET SDK</span></span>
<span data-ttu-id="fe000-114">Hello HDInsight .NET SDK fournit des bibliothèques de client .NET, ce qui le rend plus facile toowork avec des clusters HDInsight à partir de .NET.</span><span class="sxs-lookup"><span data-stu-id="fe000-114">hello HDInsight .NET SDK provides .NET client libraries, which makes it easier toowork with HDInsight clusters from .NET.</span></span> 

<span data-ttu-id="fe000-115">**travaux de tooSubmit**</span><span class="sxs-lookup"><span data-stu-id="fe000-115">**tooSubmit jobs**</span></span>

1. <span data-ttu-id="fe000-116">Créez une application console C# dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fe000-116">Create a C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="fe000-117">À partir de la Console du Gestionnaire de Package Nuget de hello, exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="fe000-117">From hello Nuget Package Manager Console, run hello following command:</span></span>
   
        Install-Package Microsoft.Azure.Management.HDInsight.Job
3. <span data-ttu-id="fe000-118">Utilisez hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="fe000-118">Use hello following code:</span></span>

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
                    System.Console.WriteLine("hello application is running ...");
   
                    var clusterCredentials = new BasicAuthenticationCloudCredentials { Username = ExistingClusterUsername, Password = ExistingClusterPassword };
                    _hdiJobManagementClient = new HDInsightJobManagementClient(ExistingClusterUri, clusterCredentials);
   
                    SubmitHiveJob();
   
                    System.Console.WriteLine("Press ENTER toocontinue ...");
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
   
                    System.Console.WriteLine("Submitting hello Hive job toohello cluster...");
                    var jobResponse = _hdiJobManagementClient.JobManagement.SubmitHiveJob(parameters);
                    var jobId = jobResponse.JobSubmissionJsonResponse.Id;
                    System.Console.WriteLine("Response status code is " + jobResponse.StatusCode);
                    System.Console.WriteLine("JobId is " + jobId);
   
                    System.Console.WriteLine("Waiting for hello job completion ...");
   
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
4. <span data-ttu-id="fe000-119">Appuyez sur **F5** application hello de toorun.</span><span class="sxs-lookup"><span data-stu-id="fe000-119">Press **F5** toorun hello application.</span></span>

<span data-ttu-id="fe000-120">sortie Hello de l’application hello doit être similaire à :</span><span class="sxs-lookup"><span data-stu-id="fe000-120">hello output of hello application shall be similar to:</span></span>

![Résultat de la tâche HDInsight Hadoop Hive](./media/hdinsight-hadoop-use-hive-dotnet-sdk/hdinsight-hadoop-use-hive-net-sdk-output.png)

## <a name="next-steps"></a><span data-ttu-id="fe000-122">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="fe000-122">Next steps</span></span>
<span data-ttu-id="fe000-123">Dans cet article, vous avez appris plusieurs façons toocreate un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fe000-123">In this article, you have learned several ways toocreate an HDInsight cluster.</span></span> <span data-ttu-id="fe000-124">toolearn, voir hello suivant des articles :</span><span class="sxs-lookup"><span data-stu-id="fe000-124">toolearn more, see hello following articles:</span></span>

* <span data-ttu-id="fe000-125">[Prise en main d’Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="fe000-125">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="fe000-126">[Création de clusters Hadoop dans HDInsight][hdinsight-provision]</span><span class="sxs-lookup"><span data-stu-id="fe000-126">[Create Hadoop clusters in HDInsight][hdinsight-provision]</span></span>
* [<span data-ttu-id="fe000-127">Gérer les clusters Hadoop dans HDInsight à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="fe000-127">Manage Hadoop clusters in HDInsight by using hello Azure portal</span></span>](hdinsight-administer-use-management-portal.md)
* [<span data-ttu-id="fe000-128">Référence du Kit de développement logiciel (SDK) .NET de HDInsight</span><span class="sxs-lookup"><span data-stu-id="fe000-128">HDInsight .NET SDK reference</span></span>](https://msdn.microsoft.com/library/mt271028.aspx)
* [<span data-ttu-id="fe000-129">Utilisation de Pig avec HDInsight</span><span class="sxs-lookup"><span data-stu-id="fe000-129">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="fe000-130">Utilisation de Sqoop avec HDInsight</span><span class="sxs-lookup"><span data-stu-id="fe000-130">Use Sqoop with HDInsight</span></span>](hdinsight-use-sqoop-mac-linux.md)
* [<span data-ttu-id="fe000-131">Créer des applications .NET HDInsight d’authentification non interactives</span><span class="sxs-lookup"><span data-stu-id="fe000-131">Create non-interactive authentication .NET HDInsight applications</span></span>](hdinsight-create-non-interactive-authentication-dotnet-applications.md)

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md


