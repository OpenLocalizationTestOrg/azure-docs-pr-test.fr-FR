---
title: "les tâches MapReduce aaaSubmit à l’aide du SDK .NET HDInsight - Azure | Documents Microsoft"
description: "Découvrez comment toosubmit MapReduce travaux tooAzure HDInsight Hadoop à l’aide du Kit de développement logiciel HDInsight .NET."
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
ms.openlocfilehash: d00e31400b8fa47982c31d00bfdcdb304bcb0b59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="run-mapreduce-jobs-using-hdinsight-net-sdk"></a><span data-ttu-id="34394-103">Exécuter des travaux MapReduce avec le Kit de développement logiciel (SDK) .NET HDInsight</span><span class="sxs-lookup"><span data-stu-id="34394-103">Run MapReduce jobs using HDInsight .NET SDK</span></span>
[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

<span data-ttu-id="34394-104">Découvrez comment toosubmit MapReduce travaux à l’aide du Kit de développement logiciel HDInsight .NET.</span><span class="sxs-lookup"><span data-stu-id="34394-104">Learn how toosubmit MapReduce jobs using HDInsight .NET SDK.</span></span> <span data-ttu-id="34394-105">Les clusters HDInsight comportent un fichier jar qui contient des exemples MapReduce.</span><span class="sxs-lookup"><span data-stu-id="34394-105">HDInsight clusters come with a jar file with some MapReduce samples.</span></span> <span data-ttu-id="34394-106">le fichier jar Hello est */example/jars/hadoop-mapreduce-examples.jar*.</span><span class="sxs-lookup"><span data-stu-id="34394-106">hello jar file is */example/jars/hadoop-mapreduce-examples.jar*.</span></span>  <span data-ttu-id="34394-107">Un des exemples de hello est *wordcount*.</span><span class="sxs-lookup"><span data-stu-id="34394-107">One of hello samples is *wordcount*.</span></span> <span data-ttu-id="34394-108">Vous développez un c# console application toosubmit un travail wordcount.</span><span class="sxs-lookup"><span data-stu-id="34394-108">You develop a C# console application toosubmit a wordcount job.</span></span>  <span data-ttu-id="34394-109">travail de Hello lit hello */example/data/gutenberg/davinci.txt* fichier et des sorties hello résultats trop*/example/data/davinciwordcount*.</span><span class="sxs-lookup"><span data-stu-id="34394-109">hello job reads hello */example/data/gutenberg/davinci.txt* file, and outputs hello results too*/example/data/davinciwordcount*.</span></span>  <span data-ttu-id="34394-110">Si vous souhaitez toorerun hello application, vous devez nettoyer le dossier de sortie hello.</span><span class="sxs-lookup"><span data-stu-id="34394-110">If you want toorerun hello application, you must clean up hello output folder.</span></span>

> [!NOTE]
> <span data-ttu-id="34394-111">étapes de Hello dans cet article doivent être effectuées à partir d’un client Windows.</span><span class="sxs-lookup"><span data-stu-id="34394-111">hello steps in this article must be performed from a Windows client.</span></span> <span data-ttu-id="34394-112">Pour plus d’informations sur l’utilisation d’un Linux, OS X ou Unix client toowork avec Hive, utilisez sélecteur de tabulation hello indiqué en haut de hello d’article de hello.</span><span class="sxs-lookup"><span data-stu-id="34394-112">For information on using a Linux, OS X, or Unix client toowork with Hive, use hello tab selector shown on hello top of hello article.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="34394-113">Composants requis</span><span class="sxs-lookup"><span data-stu-id="34394-113">Prerequisites</span></span>
<span data-ttu-id="34394-114">Avant de commencer cet article, vous devez disposer de hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="34394-114">Before you begin this article, you must have hello following items:</span></span>

* <span data-ttu-id="34394-115">**Cluster Hadoop dans HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="34394-115">**A Hadoop cluster in HDInsight**.</span></span> <span data-ttu-id="34394-116">Consultez [Prise en main de Hadoop sous Linux dans HDInsight](./hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="34394-116">See [Get started using Linux-based Hadoop in HDInsight](./hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>
* <span data-ttu-id="34394-117">**Visual Studio 2013/2015/2017**.</span><span class="sxs-lookup"><span data-stu-id="34394-117">**Visual Studio 2013/2015/2017**.</span></span>

## <a name="submit-mapreduce-jobs-using-hdinsight-net-sdk"></a><span data-ttu-id="34394-118">Envoi de tâches MapReduce avec le Kit de développement logiciel (SDK) .NET HDInsight</span><span class="sxs-lookup"><span data-stu-id="34394-118">Submit MapReduce jobs using HDInsight .NET SDK</span></span>
<span data-ttu-id="34394-119">Hello HDInsight .NET SDK fournit des bibliothèques de client .NET, ce qui le rend plus facile toowork avec des clusters HDInsight à partir de .NET.</span><span class="sxs-lookup"><span data-stu-id="34394-119">hello HDInsight .NET SDK provides .NET client libraries, which makes it easier toowork with HDInsight clusters from .NET.</span></span> 

<span data-ttu-id="34394-120">**travaux de tooSubmit**</span><span class="sxs-lookup"><span data-stu-id="34394-120">**tooSubmit jobs**</span></span>

1. <span data-ttu-id="34394-121">Créez une application console C# dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="34394-121">Create a C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="34394-122">À partir de la Console du Gestionnaire de Package Nuget de hello, exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="34394-122">From hello Nuget Package Manager Console, run hello following command:</span></span>
   
        Install-Package Microsoft.Azure.Management.HDInsight.Job
3. <span data-ttu-id="34394-123">Utilisez hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="34394-123">Use hello following code:</span></span>
   
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
                    System.Console.WriteLine("hello application is running ...");
   
                    var clusterCredentials = new BasicAuthenticationCloudCredentials { Username = existingClusterUsername, Password = existingClusterPassword };
                    _hdiJobManagementClient = new HDInsightJobManagementClient(existingClusterUri, clusterCredentials);
   
                    SubmitMRJob();
   
                    System.Console.WriteLine("Press ENTER toocontinue ...");
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
   
                    System.Console.WriteLine("Submitting hello MR job toohello cluster...");
                    var jobResponse = _hdiJobManagementClient.JobManagement.SubmitMapReduceJob(paras);
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
                    System.Console.WriteLine("Job output is: ");
                    var storageAccess = new AzureStorageAccess(defaultStorageAccountName, defaultStorageAccountKey,
                        defaultStorageContainerName);
        
                    if (jobDetail.ExitValue == 0)
                    {
                        // Create hello storage account object
                        CloudStorageAccount storageAccount = CloudStorageAccount.Parse("DefaultEndpointsProtocol=https;AccountName=" + 
                            defaultStorageAccountName + 
                            ";AccountKey=" + defaultStorageAccountKey);
        
                        // Create hello blob client.
                        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
        
                        // Retrieve reference tooa previously created container.
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
4. <span data-ttu-id="34394-124">Appuyez sur **F5** application hello de toorun.</span><span class="sxs-lookup"><span data-stu-id="34394-124">Press **F5** toorun hello application.</span></span>

<span data-ttu-id="34394-125">travail de hello toorun vous devez à nouveau, modifier hello travail sortie nom du dossier, dans l’exemple hello, il est « / exemple/données/davinciwordcount ».</span><span class="sxs-lookup"><span data-stu-id="34394-125">toorun hello job again, you must change hello job output folder name, in hello sample, it is "/example/data/davinciwordcount".</span></span>

<span data-ttu-id="34394-126">Hello fin du travail, application hello imprime le contenu hello hello du fichier de sortie « partie-r-00000 ».</span><span class="sxs-lookup"><span data-stu-id="34394-126">When hello job completes successfully, hello application prints hello content of hello output file "part-r-00000".</span></span>

## <a name="next-steps"></a><span data-ttu-id="34394-127">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="34394-127">Next steps</span></span>
<span data-ttu-id="34394-128">Dans cet article, vous avez appris plusieurs façons toocreate un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="34394-128">In this article, you have learned several ways toocreate an HDInsight cluster.</span></span> <span data-ttu-id="34394-129">toolearn, voir hello suivant des articles :</span><span class="sxs-lookup"><span data-stu-id="34394-129">toolearn more, see hello following articles:</span></span>

* <span data-ttu-id="34394-130">Pour soumettre un travail Hive, consultez [Exécuter des requêtes Hive avec le Kit de développement logiciel (SDK) .NET HDInsight](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="34394-130">For submitting a Hive job, see [Run Hive queries using HDInsight .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span></span>
* <span data-ttu-id="34394-131">Pour créer des clusters HDInsight, consultez [Création de clusters Hadoop basés sur Linux dans HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="34394-131">For creating HDInsight clusters, see [Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>
* <span data-ttu-id="34394-132">Pour gérer des clusters HDInsight, consultez [Gestion de clusters Hadoop basés sur Linux dans HDInsight](hdinsight-administer-use-portal-linux.md).</span><span class="sxs-lookup"><span data-stu-id="34394-132">For managing HDInsight clusters, see [Manage Hadoop clusters in HDInsight](hdinsight-administer-use-portal-linux.md).</span></span>
* <span data-ttu-id="34394-133">Formation hello HDInsight .NET SDK, consultez [référence du Kit de développement logiciel HDInsight .NET](https://msdn.microsoft.com/library/mt271028.aspx).</span><span class="sxs-lookup"><span data-stu-id="34394-133">For learning hello HDInsight .NET SDK, see [HDInsight .NET SDK reference](https://msdn.microsoft.com/library/mt271028.aspx).</span></span>
* <span data-ttu-id="34394-134">Pour non interactif authentifier tooAzure, consultez [créer une authentification non interactive les applications .NET HDInsight](hdinsight-create-non-interactive-authentication-dotnet-applications.md).</span><span class="sxs-lookup"><span data-stu-id="34394-134">For non-interactive authenticate tooAzure, see [Create non-interactive authentication .NET HDInsight applications](hdinsight-create-non-interactive-authentication-dotnet-applications.md).</span></span>

