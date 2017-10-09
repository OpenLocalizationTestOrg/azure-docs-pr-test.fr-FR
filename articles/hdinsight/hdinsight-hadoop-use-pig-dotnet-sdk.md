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
# <a name="run-pig-jobs-using-hello-net-sdk-for-hadoop-in-hdinsight"></a>Exécuter des travaux Pig à l’aide de hello .NET SDK pour Hadoop dans HDInsight

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

Découvrez comment toouse hello .NET SDK pour Hadoop toosubmit Apache Pig travaux tooHadoop sur Azure HDInsight.

Hello HDInsight .NET SDK fournit des bibliothèques clientes .NET qui le rend plus facile toowork avec des clusters HDInsight à partir de .NET. Pig vous permet de toocreate MapReduce opérations en une série de transformations de données de modélisation. Dans ce document, vous découvrez comment toouse base c# application toosubmit un Pig travail tooan HDInsight cluster.

## <a name="prerequisites"></a>Composants requis

toocomplete hello étapes décrites dans cet article, hello éléments suivants sont nécessaires.

* Un cluster Azure HDInsight (Hadoop sur HDInsight) Windows ou Linux.

  > [!IMPORTANT]
  > Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure. Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* Visual Studio 2012, 2013, 2015 ou 2017.

## <a name="create-hello-application"></a>Créer l’application hello

Hello HDInsight .NET SDK fournit des bibliothèques de client .NET, ce qui le rend plus facile toowork avec des clusters HDInsight à partir de .NET.

1. À partir de hello **fichier** menu dans Visual Studio, sélectionnez **nouveau** , puis sélectionnez **projet**.

2. Nouveau projet de hello, type ou sélectionnez hello suivant des valeurs :

   | Propriété | Valeur |
   | ------ | ------ |
   | Catégorie | Modèles/Visual C#/Windows |
   | Modèle | Application console |
   | Nom | SubmitPigJob |

3. Cliquez sur **OK** projet hello de toocreate.

4. À partir de hello **outils** menu, sélectionnez **Gestionnaire de Package de bibliothèque** ou **Gestionnaire de Package Nuget**, puis sélectionnez **Package Manager Console**.

5. packages de développement .NET SDK tooinstall hello, utilisez hello de commande suivante :

        Install-Package Microsoft.Azure.Management.HDInsight.Job

6. Dans l’Explorateur de solutions, double-cliquez sur **Program.cs** tooopen il. Remplacez le code existant hello suivant de hello.

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

7. application de hello toostart, appuyez sur **F5**.

8. application de hello tooexit, appuyez sur **entrée**.

## <a name="summary"></a>Résumé

Comme vous pouvez le voir, hello .NET SDK pour Hadoop vous permet des applications .NET toocreate soumettre le cluster HDInsight de Pig travaux tooan et de surveillance d’état du travail hello.

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur Pig dans HDInsight, consultez [Utilisation de Pig avec Hadoop sur HDInsight](hdinsight-use-pig.md).

Pour plus d’informations sur l’utilisation de Hadoop sur HDInsight, consultez hello suivant des documents :

* [Utilisation de Hive avec Hadoop sur HDInsight](hdinsight-use-hive.md)
* [Utilisation de MapReduce avec Hadoop sur HDInsight](hdinsight-use-mapreduce.md)

[preview-portal]: https://portal.azure.com/
