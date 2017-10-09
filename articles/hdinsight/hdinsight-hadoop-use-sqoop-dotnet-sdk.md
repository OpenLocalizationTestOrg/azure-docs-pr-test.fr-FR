---
title: "travaux de Sqoop aaaRun à l’aide de .NET et HDInsight - Azure | Documents Microsoft"
description: "Découvrez comment toouse HDInsight .NET SDK toorun Sqoop importer et exporter entre un cluster Hadoop et une base de données SQL Azure."
keywords: travail sqoop
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
ms.assetid: 87bacd13-7775-4b71-91da-161cb6224a96
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: afa0a78ba5e5d89c04ba7be4b58dd24aea4f39ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="run-sqoop-jobs-using-net-sdk-for-hadoop-in-hdinsight"></a><span data-ttu-id="b9490-104">Exécuter des tâches Sqoop à l’aide du Kit de développement logiciel (SDK) .NET pour Hadoop dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="b9490-104">Run Sqoop jobs using .NET SDK for Hadoop in HDInsight</span></span>
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="b9490-105">Découvrez comment des travaux toorun du Kit de développement logiciel HDInsight .NET toouse Sqoop dans HDInsight tooimport et d’exportation entre le cluster HDInsight et de la base de données SQL Azure ou base de données SQL Server.</span><span class="sxs-lookup"><span data-stu-id="b9490-105">Learn how toouse HDInsight .NET SDK toorun Sqoop jobs in HDInsight tooimport and export between HDInsight cluster and Azure SQL database or SQL Server database.</span></span>

> [!NOTE]
> <span data-ttu-id="b9490-106">étapes Hello dans cet article peuvent être utilisés avec soit un cluster de HDInsight Windows ou Linux. Toutefois, cette procédure fonctionne uniquement à partir d’un client Windows.</span><span class="sxs-lookup"><span data-stu-id="b9490-106">hello steps in this article can be used with either a Windows-based or Linux-based HDInsight cluster; however, these steps only work from a Windows client.</span></span> <span data-ttu-id="b9490-107">Utilisez sélecteur de tabulation hello haut hello de cet article de toochoose d’autres méthodes.</span><span class="sxs-lookup"><span data-stu-id="b9490-107">Use hello tab selector on hello top of this article toochoose other methods.</span></span>
> 
> 

### <a name="prerequisites"></a><span data-ttu-id="b9490-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="b9490-108">Prerequisites</span></span>
<span data-ttu-id="b9490-109">Avant de commencer ce didacticiel, vous devez disposer des éléments suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="b9490-109">Before you begin this tutorial, you must have hello following items:</span></span>

* <span data-ttu-id="b9490-110">**Cluster Hadoop dans HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="b9490-110">**A Hadoop cluster in HDInsight**.</span></span> <span data-ttu-id="b9490-111">Consultez [Création du cluster et de la base de données SQL](hdinsight-use-sqoop.md#create-cluster-and-sql-database).</span><span class="sxs-lookup"><span data-stu-id="b9490-111">See [Create cluster and SQL database](hdinsight-use-sqoop.md#create-cluster-and-sql-database).</span></span>

## <a name="use-sqoop-on-hdinsight-clusters-using-net-sdk"></a><span data-ttu-id="b9490-112">Utiliser Sqoop sur des clusters HDInsight à l’aide du Kit de développement logiciel (SDK) .NET</span><span class="sxs-lookup"><span data-stu-id="b9490-112">Use Sqoop on HDInsight clusters using .NET SDK</span></span>
<span data-ttu-id="b9490-113">Hello HDInsight .NET SDK fournit des bibliothèques de client .NET, ce qui le rend plus facile toowork avec des clusters HDInsight à partir de .NET.</span><span class="sxs-lookup"><span data-stu-id="b9490-113">hello HDInsight .NET SDK provides .NET client libraries, which makes it easier toowork with HDInsight clusters from .NET.</span></span> <span data-ttu-id="b9490-114">Dans cette section, vous créez une c# console application tooexport hello hivesampletable toohello base de données SQL table que vous avez créé précédemment dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="b9490-114">In this section, you create a C# console application tooexport hello hivesampletable toohello SQL Database table you created earlier in this tutorial.</span></span>

## <a name="submit-a-sqoop-job"></a><span data-ttu-id="b9490-115">Envoyer un travail Sqoop</span><span class="sxs-lookup"><span data-stu-id="b9490-115">Submit a Sqoop job</span></span>

1. <span data-ttu-id="b9490-116">Créez une application console C# dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b9490-116">Create a C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="b9490-117">À partir de hello Console du Gestionnaire de Package Visual Studio, exécutez hello suivant du package de Nuget commande tooimport hello.</span><span class="sxs-lookup"><span data-stu-id="b9490-117">From hello Visual Studio Package Manager Console, run hello following Nuget command tooimport hello package.</span></span>
   
        Install-Package Microsoft.Azure.Management.HDInsight.Job
3. <span data-ttu-id="b9490-118">Utilisez hello suivant de code dans un fichier hello Program.cs :</span><span class="sxs-lookup"><span data-stu-id="b9490-118">Use hello following code in hello Program.cs file:</span></span>
   
        using System.Collections.Generic;
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
   
                    SubmitSqoopJob();
   
                    System.Console.WriteLine("Press ENTER toocontinue ...");
                    System.Console.ReadLine();
                }
   
                private static void SubmitSqoopJob()
                {
                    var sqlDatabaseServerName = "<SQLDatabaseServerName>";
                    var sqlDatabaseLogin = "<SQLDatabaseLogin>";
                    var sqlDatabaseLoginPassword = "<SQLDatabaseLoginPassword>";
                    var sqlDatabaseDatabaseName = "<DatabaseName>";
   
                    var tableName = "<TableName>";
                    var exportDir = "/tutorials/usesqoop/data";
   
                    // Connection string for using Azure SQL Database.
                    // Comment if using SQL Server
                    var connectionString = "jdbc:sqlserver://" + sqlDatabaseServerName + ".database.windows.net;user=" + sqlDatabaseLogin + "@" + sqlDatabaseServerName + ";password=" + sqlDatabaseLoginPassword + ";database=" + sqlDatabaseDatabaseName;
                    // Connection string for using SQL Server.
                    // Uncomment if using SQL Server
                    //var connectionString = "jdbc:sqlserver://" + sqlDatabaseServerName + ";user=" + sqlDatabaseLogin + ";password=" + sqlDatabaseLoginPassword + ";database=" + sqlDatabaseDatabaseName;
   
                    var parameters = new SqoopJobSubmissionParameters
                    {
                        Files = new List<string> { "/user/oozie/share/lib/sqoop/sqljdbc41.jar" }, // This line is required for Linux-based cluster.
                        Command = "export --connect " + connectionString + " --table " + tableName + "_mobile --export-dir " + exportDir + "_mobile --fields-terminated-by \\t -m 1"
                    };
   
                    System.Console.WriteLine("Submitting hello Sqoop job toohello cluster...");
                    var response = _hdiJobManagementClient.JobManagement.SubmitSqoopJob(parameters);
                    System.Console.WriteLine("Validating that hello response is as expected...");
                    System.Console.WriteLine("Response status code is " + response.StatusCode);
                    System.Console.WriteLine("Validating hello response object...");
                    System.Console.WriteLine("JobId is " + response.JobSubmissionJsonResponse.Id);
                }
            }
        }
4. <span data-ttu-id="b9490-119">Appuyez sur **F5** programme de hello toorun.</span><span class="sxs-lookup"><span data-stu-id="b9490-119">Press **F5** toorun hello program.</span></span> 

## <a name="limitations"></a><span data-ttu-id="b9490-120">Limites</span><span class="sxs-lookup"><span data-stu-id="b9490-120">Limitations</span></span>
* <span data-ttu-id="b9490-121">L’exportation en bloc - basés sur Linux avec un HDInsight, hello Sqoop connecteur utilisé tooexport données tooMicrosoft SQL Server ou base de données SQL Azure ne prend actuellement pas en charge les insertions en bloc.</span><span class="sxs-lookup"><span data-stu-id="b9490-121">Bulk export - With Linux-based HDInsight, hello Sqoop connector used tooexport data tooMicrosoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>
* <span data-ttu-id="b9490-122">Le traitement par lot - Hdinsight basés sur Linux, lorsque vous utilisez hello `-batch` commutateur lorsque vous effectuez des insertions, Sqoop effectue plusieurs insertions au lieu de traitement par lot des opérations d’insertion hello.</span><span class="sxs-lookup"><span data-stu-id="b9490-122">Batching - With Linux-based HDInsight, When using hello `-batch` switch when performing inserts, Sqoop performs multiple inserts instead of batching hello insert operations.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b9490-123">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b9490-123">Next steps</span></span>
<span data-ttu-id="b9490-124">Maintenant que vous avez appris comment toouse Sqoop.</span><span class="sxs-lookup"><span data-stu-id="b9490-124">Now you have learned how toouse Sqoop.</span></span> <span data-ttu-id="b9490-125">toolearn, voir :</span><span class="sxs-lookup"><span data-stu-id="b9490-125">toolearn more, see:</span></span>

* <span data-ttu-id="b9490-126">[Utilisation d'Oozie avec HDInsight](hdinsight-use-oozie.md): utilisez l’action Sqoop dans un flux de travail Oozie.</span><span class="sxs-lookup"><span data-stu-id="b9490-126">[Use Oozie with HDInsight](hdinsight-use-oozie.md): Use Sqoop action in an Oozie workflow.</span></span>
* <span data-ttu-id="b9490-127">[Analyser des données de retard de vol avec HDInsight](hdinsight-analyze-flight-delay-data.md): utiliser la ruche de vol de tooanalyze retarder des données et ensuite utiliser la base de données Sqoop tooexport données tooan SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="b9490-127">[Analyze flight delay data using HDInsight](hdinsight-analyze-flight-delay-data.md): Use Hive tooanalyze flight delay data, and then use Sqoop tooexport data tooan Azure SQL database.</span></span>
* <span data-ttu-id="b9490-128">[Télécharger des données tooHDInsight](hdinsight-upload-data.md): trouver d’autres méthodes pour le téléchargement des données tooHDInsight/Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="b9490-128">[Upload data tooHDInsight](hdinsight-upload-data.md): Find other methods for uploading data tooHDInsight/Azure Blob storage.</span></span>

