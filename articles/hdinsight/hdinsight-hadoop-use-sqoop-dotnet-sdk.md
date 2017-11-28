---
title: "Exécuter des travaux Sqoop avec .NET et HDInsight - Azure | Microsoft Docs"
description: "Découvrez comment utiliser le Kit de développement logiciel (SDK) .NET HDInsight pour exécuter l’exportation et l’importation Sqoop entre un cluster Hadoop et une base de données SQL Azure."
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
ms.openlocfilehash: c95641fc6d20e2911e007d1974b9e2c2398b3133
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="run-sqoop-jobs-using-net-sdk-for-hadoop-in-hdinsight"></a><span data-ttu-id="2220e-104">Exécuter des tâches Sqoop à l’aide du Kit de développement logiciel (SDK) .NET pour Hadoop dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="2220e-104">Run Sqoop jobs using .NET SDK for Hadoop in HDInsight</span></span>
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="2220e-105">Découvrez comment utiliser le Kit de développement logiciel (SDK) .NET HDInsight pour exécuter des tâches Sqoop dans HDInsight afin d’effectuer des opérations d’importation et d’exportation entre un cluster HDInsight et une base de données SQL Azure ou SQL Server.</span><span class="sxs-lookup"><span data-stu-id="2220e-105">Learn how to use HDInsight .NET SDK to run Sqoop jobs in HDInsight to import and export between HDInsight cluster and Azure SQL database or SQL Server database.</span></span>

> [!NOTE]
> <span data-ttu-id="2220e-106">Les étapes décrites dans cet article peuvent être utilisées avec un cluster HDInsight Windows ou Linux. Toutefois, elles fonctionnent uniquement à partir d’un client Windows.</span><span class="sxs-lookup"><span data-stu-id="2220e-106">The steps in this article can be used with either a Windows-based or Linux-based HDInsight cluster; however, these steps only work from a Windows client.</span></span> <span data-ttu-id="2220e-107">Utilisez le sélecteur d’onglet en haut de cet article pour choisir d’autres méthodes.</span><span class="sxs-lookup"><span data-stu-id="2220e-107">Use the tab selector on the top of this article to choose other methods.</span></span>
> 
> 

### <a name="prerequisites"></a><span data-ttu-id="2220e-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="2220e-108">Prerequisites</span></span>
<span data-ttu-id="2220e-109">Avant de commencer ce didacticiel, vous devez disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="2220e-109">Before you begin this tutorial, you must have the following items:</span></span>

* <span data-ttu-id="2220e-110">**Cluster Hadoop dans HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="2220e-110">**A Hadoop cluster in HDInsight**.</span></span> <span data-ttu-id="2220e-111">Consultez [Création du cluster et de la base de données SQL](hdinsight-use-sqoop.md#create-cluster-and-sql-database).</span><span class="sxs-lookup"><span data-stu-id="2220e-111">See [Create cluster and SQL database](hdinsight-use-sqoop.md#create-cluster-and-sql-database).</span></span>

## <a name="use-sqoop-on-hdinsight-clusters-using-net-sdk"></a><span data-ttu-id="2220e-112">Utiliser Sqoop sur des clusters HDInsight à l’aide du Kit de développement logiciel (SDK) .NET</span><span class="sxs-lookup"><span data-stu-id="2220e-112">Use Sqoop on HDInsight clusters using .NET SDK</span></span>
<span data-ttu-id="2220e-113">Le Kit de développement logiciel (SDK) HDInsight .NET fournit des bibliothèques clientes .NET, ce qui facilite l'utilisation des clusters HDInsight à partir de .NET.</span><span class="sxs-lookup"><span data-stu-id="2220e-113">The HDInsight .NET SDK provides .NET client libraries, which makes it easier to work with HDInsight clusters from .NET.</span></span> <span data-ttu-id="2220e-114">Dans cette section, vous allez créer une application console C# pour exporter la table hivesampletable vers la table de base de données SQL créée précédemment dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="2220e-114">In this section, you create a C# console application to export the hivesampletable to the SQL Database table you created earlier in this tutorial.</span></span>

## <a name="submit-a-sqoop-job"></a><span data-ttu-id="2220e-115">Envoyer un travail Sqoop</span><span class="sxs-lookup"><span data-stu-id="2220e-115">Submit a Sqoop job</span></span>

1. <span data-ttu-id="2220e-116">Créez une application console C# dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2220e-116">Create a C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="2220e-117">Dans la console du gestionnaire de package Visual Studio, exécutez la commande Nuget suivante pour importer le package.</span><span class="sxs-lookup"><span data-stu-id="2220e-117">From the Visual Studio Package Manager Console, run the following Nuget command to import the package.</span></span>
   
        Install-Package Microsoft.Azure.Management.HDInsight.Job
3. <span data-ttu-id="2220e-118">Utilisez le code suivant dans le fichier Program.cs :</span><span class="sxs-lookup"><span data-stu-id="2220e-118">Use the following code in the Program.cs file:</span></span>
   
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
                    System.Console.WriteLine("The application is running ...");
   
                    var clusterCredentials = new BasicAuthenticationCloudCredentials { Username = ExistingClusterUsername, Password = ExistingClusterPassword };
                    _hdiJobManagementClient = new HDInsightJobManagementClient(ExistingClusterUri, clusterCredentials);
   
                    SubmitSqoopJob();
   
                    System.Console.WriteLine("Press ENTER to continue ...");
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
   
                    System.Console.WriteLine("Submitting the Sqoop job to the cluster...");
                    var response = _hdiJobManagementClient.JobManagement.SubmitSqoopJob(parameters);
                    System.Console.WriteLine("Validating that the response is as expected...");
                    System.Console.WriteLine("Response status code is " + response.StatusCode);
                    System.Console.WriteLine("Validating the response object...");
                    System.Console.WriteLine("JobId is " + response.JobSubmissionJsonResponse.Id);
                }
            }
        }
4. <span data-ttu-id="2220e-119">Appuyez sur **F5** pour exécuter le programme.</span><span class="sxs-lookup"><span data-stu-id="2220e-119">Press **F5** to run the program.</span></span> 

## <a name="limitations"></a><span data-ttu-id="2220e-120">Limitations</span><span class="sxs-lookup"><span data-stu-id="2220e-120">Limitations</span></span>
* <span data-ttu-id="2220e-121">Exportation en bloc : avec HDInsight sous Linux, le connecteur Sqoop utilisé pour exporter des données vers Microsoft SQL Server ou la base de données SQL Azure ne prend pas en charge les insertions en bloc.</span><span class="sxs-lookup"><span data-stu-id="2220e-121">Bulk export - With Linux-based HDInsight, the Sqoop connector used to export data to Microsoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>
* <span data-ttu-id="2220e-122">Traitement par lots : avec HDInsight sous Linux, lorsque vous utilisez le commutateur `-batch` pour effectuer des insertions, Sqoop effectue plusieurs insertions plutôt qu’un traitement par lots des opérations d’insertion.</span><span class="sxs-lookup"><span data-stu-id="2220e-122">Batching - With Linux-based HDInsight, When using the `-batch` switch when performing inserts, Sqoop performs multiple inserts instead of batching the insert operations.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2220e-123">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2220e-123">Next steps</span></span>
<span data-ttu-id="2220e-124">Vous maîtrisez à présent l'utilisation de Sqoop.</span><span class="sxs-lookup"><span data-stu-id="2220e-124">Now you have learned how to use Sqoop.</span></span> <span data-ttu-id="2220e-125">Pour plus d'informations, consultez les rubriques suivantes :</span><span class="sxs-lookup"><span data-stu-id="2220e-125">To learn more, see:</span></span>

* <span data-ttu-id="2220e-126">[Utilisation d'Oozie avec HDInsight](hdinsight-use-oozie.md): utilisez l’action Sqoop dans un flux de travail Oozie.</span><span class="sxs-lookup"><span data-stu-id="2220e-126">[Use Oozie with HDInsight](hdinsight-use-oozie.md): Use Sqoop action in an Oozie workflow.</span></span>
* <span data-ttu-id="2220e-127">[Analyse des données sur les retards de vol avec HDInsight](hdinsight-analyze-flight-delay-data.md): utilisez Hive pour analyser des données sur les retards de vol, puis utilisez Sqoop pour exporter ces données vers une base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="2220e-127">[Analyze flight delay data using HDInsight](hdinsight-analyze-flight-delay-data.md): Use Hive to analyze flight delay data, and then use Sqoop to export data to an Azure SQL database.</span></span>
* <span data-ttu-id="2220e-128">[Téléchargement de données vers HDInsight](hdinsight-upload-data.md): découvrez d'autres méthodes pour télécharger des données vers HDInsight ou le stockage d'objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="2220e-128">[Upload data to HDInsight](hdinsight-upload-data.md): Find other methods for uploading data to HDInsight/Azure Blob storage.</span></span>

