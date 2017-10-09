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
# <a name="run-mapreduce-jobs-using-hdinsight-net-sdk"></a>Exécuter des travaux MapReduce avec le Kit de développement logiciel (SDK) .NET HDInsight
[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

Découvrez comment toosubmit MapReduce travaux à l’aide du Kit de développement logiciel HDInsight .NET. Les clusters HDInsight comportent un fichier jar qui contient des exemples MapReduce. le fichier jar Hello est */example/jars/hadoop-mapreduce-examples.jar*.  Un des exemples de hello est *wordcount*. Vous développez un c# console application toosubmit un travail wordcount.  travail de Hello lit hello */example/data/gutenberg/davinci.txt* fichier et des sorties hello résultats trop*/example/data/davinciwordcount*.  Si vous souhaitez toorerun hello application, vous devez nettoyer le dossier de sortie hello.

> [!NOTE]
> étapes de Hello dans cet article doivent être effectuées à partir d’un client Windows. Pour plus d’informations sur l’utilisation d’un Linux, OS X ou Unix client toowork avec Hive, utilisez sélecteur de tabulation hello indiqué en haut de hello d’article de hello.
> 
> 

## <a name="prerequisites"></a>Composants requis
Avant de commencer cet article, vous devez disposer de hello éléments suivants :

* **Cluster Hadoop dans HDInsight**. Consultez [Prise en main de Hadoop sous Linux dans HDInsight](./hdinsight-hadoop-linux-tutorial-get-started.md).
* **Visual Studio 2013/2015/2017**.

## <a name="submit-mapreduce-jobs-using-hdinsight-net-sdk"></a>Envoi de tâches MapReduce avec le Kit de développement logiciel (SDK) .NET HDInsight
Hello HDInsight .NET SDK fournit des bibliothèques de client .NET, ce qui le rend plus facile toowork avec des clusters HDInsight à partir de .NET. 

**travaux de tooSubmit**

1. Créez une application console C# dans Visual Studio.
2. À partir de la Console du Gestionnaire de Package Nuget de hello, exécutez hello de commande suivante :
   
        Install-Package Microsoft.Azure.Management.HDInsight.Job
3. Utilisez hello suivant de code :
   
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
4. Appuyez sur **F5** application hello de toorun.

travail de hello toorun vous devez à nouveau, modifier hello travail sortie nom du dossier, dans l’exemple hello, il est « / exemple/données/davinciwordcount ».

Hello fin du travail, application hello imprime le contenu hello hello du fichier de sortie « partie-r-00000 ».

## <a name="next-steps"></a>Étapes suivantes
Dans cet article, vous avez appris plusieurs façons toocreate un cluster HDInsight. toolearn, voir hello suivant des articles :

* Pour soumettre un travail Hive, consultez [Exécuter des requêtes Hive avec le Kit de développement logiciel (SDK) .NET HDInsight](hdinsight-hadoop-use-hive-dotnet-sdk.md).
* Pour créer des clusters HDInsight, consultez [Création de clusters Hadoop basés sur Linux dans HDInsight](hdinsight-hadoop-provision-linux-clusters.md).
* Pour gérer des clusters HDInsight, consultez [Gestion de clusters Hadoop basés sur Linux dans HDInsight](hdinsight-administer-use-portal-linux.md).
* Formation hello HDInsight .NET SDK, consultez [référence du Kit de développement logiciel HDInsight .NET](https://msdn.microsoft.com/library/mt271028.aspx).
* Pour non interactif authentifier tooAzure, consultez [créer une authentification non interactive les applications .NET HDInsight](hdinsight-create-non-interactive-authentication-dotnet-applications.md).

