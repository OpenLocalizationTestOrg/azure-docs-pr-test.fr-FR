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
# <a name="run-sqoop-jobs-using-net-sdk-for-hadoop-in-hdinsight"></a>Exécuter des tâches Sqoop à l’aide du Kit de développement logiciel (SDK) .NET pour Hadoop dans HDInsight
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

Découvrez comment des travaux toorun du Kit de développement logiciel HDInsight .NET toouse Sqoop dans HDInsight tooimport et d’exportation entre le cluster HDInsight et de la base de données SQL Azure ou base de données SQL Server.

> [!NOTE]
> étapes Hello dans cet article peuvent être utilisés avec soit un cluster de HDInsight Windows ou Linux. Toutefois, cette procédure fonctionne uniquement à partir d’un client Windows. Utilisez sélecteur de tabulation hello haut hello de cet article de toochoose d’autres méthodes.
> 
> 

### <a name="prerequisites"></a>Composants requis
Avant de commencer ce didacticiel, vous devez disposer des éléments suivants de hello :

* **Cluster Hadoop dans HDInsight**. Consultez [Création du cluster et de la base de données SQL](hdinsight-use-sqoop.md#create-cluster-and-sql-database).

## <a name="use-sqoop-on-hdinsight-clusters-using-net-sdk"></a>Utiliser Sqoop sur des clusters HDInsight à l’aide du Kit de développement logiciel (SDK) .NET
Hello HDInsight .NET SDK fournit des bibliothèques de client .NET, ce qui le rend plus facile toowork avec des clusters HDInsight à partir de .NET. Dans cette section, vous créez une c# console application tooexport hello hivesampletable toohello base de données SQL table que vous avez créé précédemment dans ce didacticiel.

## <a name="submit-a-sqoop-job"></a>Envoyer un travail Sqoop

1. Créez une application console C# dans Visual Studio.
2. À partir de hello Console du Gestionnaire de Package Visual Studio, exécutez hello suivant du package de Nuget commande tooimport hello.
   
        Install-Package Microsoft.Azure.Management.HDInsight.Job
3. Utilisez hello suivant de code dans un fichier hello Program.cs :
   
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
4. Appuyez sur **F5** programme de hello toorun. 

## <a name="limitations"></a>Limites
* L’exportation en bloc - basés sur Linux avec un HDInsight, hello Sqoop connecteur utilisé tooexport données tooMicrosoft SQL Server ou base de données SQL Azure ne prend actuellement pas en charge les insertions en bloc.
* Le traitement par lot - Hdinsight basés sur Linux, lorsque vous utilisez hello `-batch` commutateur lorsque vous effectuez des insertions, Sqoop effectue plusieurs insertions au lieu de traitement par lot des opérations d’insertion hello.

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez appris comment toouse Sqoop. toolearn, voir :

* [Utilisation d'Oozie avec HDInsight](hdinsight-use-oozie.md): utilisez l’action Sqoop dans un flux de travail Oozie.
* [Analyser des données de retard de vol avec HDInsight](hdinsight-analyze-flight-delay-data.md): utiliser la ruche de vol de tooanalyze retarder des données et ensuite utiliser la base de données Sqoop tooexport données tooan SQL Azure.
* [Télécharger des données tooHDInsight](hdinsight-upload-data.md): trouver d’autres méthodes pour le téléchargement des données tooHDInsight/Azure Blob storage.

