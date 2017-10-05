---
title: "Soumettre des travaux MapReduce avec le Kit de développement logiciel (SDK) .NET HDInsight - Azure | Microsoft Docs"
description: "Apprenez à envoyer des travaux MapReduce à Azure HDInsight Hadoop à l’aide du Kit de développement logiciel (SDK) .NET HDInsight."
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
ms.assetid: c85e44b0-85fd-4185-ad1c-c34a9fe5ef44
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: jgao
ms.openlocfilehash: 015435270c31bafea0ebf5303b459338755c1410
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="run-mapreduce-jobs-using-hdinsight-net-sdk"></a><span data-ttu-id="f758c-103">Exécuter des travaux MapReduce avec le Kit de développement logiciel (SDK) .NET HDInsight</span><span class="sxs-lookup"><span data-stu-id="f758c-103">Run MapReduce jobs using HDInsight .NET SDK</span></span>
[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

<span data-ttu-id="f758c-104">Apprenez à envoyer des travaux MapReduce à l’aide du Kit de développement logiciel (SDK) .NET HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f758c-104">Learn how to submit MapReduce jobs using HDInsight .NET SDK.</span></span> <span data-ttu-id="f758c-105">Les clusters HDInsight comportent un fichier jar qui contient des exemples MapReduce.</span><span class="sxs-lookup"><span data-stu-id="f758c-105">HDInsight clusters come with a jar file with some MapReduce samples.</span></span> <span data-ttu-id="f758c-106">Le fichier jar est le suivant : */example/jars/hadoop-mapreduce-examples.jar*.</span><span class="sxs-lookup"><span data-stu-id="f758c-106">The jar file is */example/jars/hadoop-mapreduce-examples.jar*.</span></span>  <span data-ttu-id="f758c-107">Un des exemples est *wordcount*.</span><span class="sxs-lookup"><span data-stu-id="f758c-107">One of the samples is *wordcount*.</span></span> <span data-ttu-id="f758c-108">Vous développez une application de console C# pour envoyer une tâche wordcount.</span><span class="sxs-lookup"><span data-stu-id="f758c-108">You develop a C# console application to submit a wordcount job.</span></span>  <span data-ttu-id="f758c-109">Le travail lit le fichier */example/data/gutenberg/davinci.txt* et renvoie les résultats vers */example/data/davinciwordcount*.</span><span class="sxs-lookup"><span data-stu-id="f758c-109">The job reads the */example/data/gutenberg/davinci.txt* file, and outputs the results to */example/data/davinciwordcount*.</span></span>  <span data-ttu-id="f758c-110">Si vous souhaitez réexécuter l’application, vous devez nettoyer le dossier de sortie.</span><span class="sxs-lookup"><span data-stu-id="f758c-110">If you want to rerun the application, you must clean up the output folder.</span></span>

> [!NOTE]
> <span data-ttu-id="f758c-111">Les étapes décrites dans cet article doivent être effectuées à partir d'un client Windows.</span><span class="sxs-lookup"><span data-stu-id="f758c-111">The steps in this article must be performed from a Windows client.</span></span> <span data-ttu-id="f758c-112">Pour plus d’informations sur l’utilisation d’un client Linux, OS X ou Unix pour utiliser Hive, utilisez le sélecteur d’onglet en haut de l’article.</span><span class="sxs-lookup"><span data-stu-id="f758c-112">For information on using a Linux, OS X, or Unix client to work with Hive, use the tab selector shown on the top of the article.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="f758c-113">Composants requis</span><span class="sxs-lookup"><span data-stu-id="f758c-113">Prerequisites</span></span>
<span data-ttu-id="f758c-114">Avant de commencer cet article, vous devez disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="f758c-114">Before you begin this article, you must have the following items:</span></span>

* <span data-ttu-id="f758c-115">**Cluster Hadoop dans HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="f758c-115">**A Hadoop cluster in HDInsight**.</span></span> <span data-ttu-id="f758c-116">Consultez [Prise en main de Hadoop sous Linux dans HDInsight](./hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f758c-116">See [Get started using Linux-based Hadoop in HDInsight](./hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>
* <span data-ttu-id="f758c-117">**Visual Studio 2013/2015/2017**.</span><span class="sxs-lookup"><span data-stu-id="f758c-117">**Visual Studio 2013/2015/2017**.</span></span>

## <a name="submit-mapreduce-jobs-using-hdinsight-net-sdk"></a><span data-ttu-id="f758c-118">Envoi de tâches MapReduce avec le Kit de développement logiciel (SDK) .NET HDInsight</span><span class="sxs-lookup"><span data-stu-id="f758c-118">Submit MapReduce jobs using HDInsight .NET SDK</span></span>
<span data-ttu-id="f758c-119">Le Kit de développement logiciel (SDK) HDInsight .NET fournit des bibliothèques clientes .NET, ce qui facilite l'utilisation des clusters HDInsight à partir de .NET.</span><span class="sxs-lookup"><span data-stu-id="f758c-119">The HDInsight .NET SDK provides .NET client libraries, which makes it easier to work with HDInsight clusters from .NET.</span></span> 

<span data-ttu-id="f758c-120">**Pour soumettre les travaux**</span><span class="sxs-lookup"><span data-stu-id="f758c-120">**To Submit jobs**</span></span>

1. <span data-ttu-id="f758c-121">Créez une application console C# dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f758c-121">Create a C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="f758c-122">À partir de la console du gestionnaire de package NuGet, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f758c-122">From the Nuget Package Manager Console, run the following command:</span></span>
   
        Install-Package Microsoft.Azure.Management.HDInsight.Job
3. <span data-ttu-id="f758c-123">Utilisez le code suivant :</span><span class="sxs-lookup"><span data-stu-id="f758c-123">Use the following code:</span></span>
   
        using System.Collections.Generic;
        using System.IO;
        using System.Text;
        using System.Threading;
        using Microsoft.Azure.Management.HDInsight.Job;
        using Microsoft.Azure.Management.HDInsight.Job.Models;
        using Hyak.Common;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Blob;

        namespace SubmitHDInsightJobDotNet
        {
            class Program
            {
                private static HDInsightJobManagementClient _hdiJobManagementClient;
   
                private const string existingClusterName = "<Your HDInsight Cluster Name>";
                private const string existingClusterUri = existingClusterName + ".azurehdinsight.net";
                private const string existingClusterUsername = "<Cluster Username>";
                private const string existingClusterPassword = "<Cluster User Password>";
   
                private const string defaultStorageAccountName = "<Default Storage Account Name>"; //<StorageAccountName>.blob.core.windows.net
                private const string defaultStorageAccountKey = "<Default Storage Account Key>";
                private const string defaultStorageContainerName = "<Default Blob Container Name>";

                private const string sourceFile = "/example/data/gutenberg/davinci.txt";  
                private const string outputFolder = "/example/data/davinciwordcount";
   
                static void Main(string[] args)
                {
                    System.Console.WriteLine("The application is running ...");
   
                    var clusterCredentials = new BasicAuthenticationCloudCredentials { Username = existingClusterUsername, Password = existingClusterPassword };
                    _hdiJobManagementClient = new HDInsightJobManagementClient(existingClusterUri, clusterCredentials);
   
                    SubmitMRJob();
   
                    System.Console.WriteLine("Press ENTER to continue ...");
                    System.Console.ReadLine();
                }
   
                private static void SubmitMRJob()
                {
                    List<string> args = new List<string> { { "/example/data/gutenberg/davinci.txt" }, { "/example/data/davinciwordcount" } };
   
                    var paras = new MapReduceJobSubmissionParameters
                    {
                        JarFile = @"/example/jars/hadoop-mapreduce-examples.jar",
                        JarClass = "wordcount",
                        Arguments = args
                    };
   
                    System.Console.WriteLine("Submitting the MR job to the cluster...");
                    var jobResponse = _hdiJobManagementClient.JobManagement.SubmitMapReduceJob(paras);
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
                    System.Console.WriteLine("Job output is: ");
                    var storageAccess = new AzureStorageAccess(defaultStorageAccountName, defaultStorageAccountKey,
                        defaultStorageContainerName);
        
                    if (jobDetail.ExitValue == 0)
                    {
                        // Create the storage account object
                        CloudStorageAccount storageAccount = CloudStorageAccount.Parse("DefaultEndpointsProtocol=https;AccountName=" + 
                            defaultStorageAccountName + 
                            ";AccountKey=" + defaultStorageAccountKey);
        
                        // Create the blob client.
                        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
        
                        // Retrieve reference to a previously created container.
                        CloudBlobContainer container = blobClient.GetContainerReference(defaultStorageContainerName);
        
                        CloudBlockBlob blockBlob = container.GetBlockBlobReference(outputFolder.Substring(1) + "/part-r-00000");
        
                        using (var stream = blockBlob.OpenRead())
                        {
                            using (StreamReader reader = new StreamReader(stream))
                            {
                                while (!reader.EndOfStream)
                                {
                                    System.Console.WriteLine(reader.ReadLine());
                                }
                            }
                        }
                    }
                    else
                    {
                        // fetch stderr output in case of failure
                        var output = _hdiJobManagementClient.JobManagement.GetJobErrorLogs(jobId, storageAccess); 
        
                        using (var reader = new StreamReader(output, Encoding.UTF8))
                        {
                            string value = reader.ReadToEnd();
                            System.Console.WriteLine(value);
                        }
        
                    }
                }
            }
        }
4. <span data-ttu-id="f758c-124">Appuyez sur **F5** pour exécuter l'application.</span><span class="sxs-lookup"><span data-stu-id="f758c-124">Press **F5** to run the application.</span></span>

<span data-ttu-id="f758c-125">Pour réexécuter le travail, vous devez modifier le nom du dossier de sortie du travail. Dans l’exemple, il s’agit de « /example/data/davinciwordcount ».</span><span class="sxs-lookup"><span data-stu-id="f758c-125">To run the job again, you must change the job output folder name, in the sample, it is "/example/data/davinciwordcount".</span></span>

<span data-ttu-id="f758c-126">Lorsque la tâche se termine correctement, l’application imprime le contenu du fichier de sortie « part-r-00000 ».</span><span class="sxs-lookup"><span data-stu-id="f758c-126">When the job completes successfully, the application prints the content of the output file "part-r-00000".</span></span>

## <a name="next-steps"></a><span data-ttu-id="f758c-127">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f758c-127">Next steps</span></span>
<span data-ttu-id="f758c-128">Cet article vous a présenté différentes méthodes pour créer un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f758c-128">In this article, you have learned several ways to create an HDInsight cluster.</span></span> <span data-ttu-id="f758c-129">Pour en savoir plus, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="f758c-129">To learn more, see the following articles:</span></span>

* <span data-ttu-id="f758c-130">Pour soumettre un travail Hive, consultez [Exécuter des requêtes Hive avec le Kit de développement logiciel (SDK) .NET HDInsight](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="f758c-130">For submitting a Hive job, see [Run Hive queries using HDInsight .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span></span>
* <span data-ttu-id="f758c-131">Pour créer des clusters HDInsight, consultez [Création de clusters Hadoop basés sur Linux dans HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="f758c-131">For creating HDInsight clusters, see [Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>
* <span data-ttu-id="f758c-132">Pour gérer des clusters HDInsight, consultez [Gestion de clusters Hadoop basés sur Linux dans HDInsight](hdinsight-administer-use-portal-linux.md).</span><span class="sxs-lookup"><span data-stu-id="f758c-132">For managing HDInsight clusters, see [Manage Hadoop clusters in HDInsight](hdinsight-administer-use-portal-linux.md).</span></span>
* <span data-ttu-id="f758c-133">Pour découvrir le Kit de développement logiciel (SDK) .NET HDInsight, consultez [Référence du Kit de développement logiciel (SDK) .NET de HDInsight](https://msdn.microsoft.com/library/mt271028.aspx).</span><span class="sxs-lookup"><span data-stu-id="f758c-133">For learning the HDInsight .NET SDK, see [HDInsight .NET SDK reference](https://msdn.microsoft.com/library/mt271028.aspx).</span></span>
* <span data-ttu-id="f758c-134">Pour l’authentification non interactive sur Azure, consultez [Créer des applications HDInsight .NET d’authentification non interactive](hdinsight-create-non-interactive-authentication-dotnet-applications.md).</span><span class="sxs-lookup"><span data-stu-id="f758c-134">For non-interactive authenticate to Azure, see [Create non-interactive authentication .NET HDInsight applications](hdinsight-create-non-interactive-authentication-dotnet-applications.md).</span></span>

