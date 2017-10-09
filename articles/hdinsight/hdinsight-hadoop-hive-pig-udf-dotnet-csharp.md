---
title: aaaUse c# avec Hive et Pig sur Hadoop dans HDInsight - Azure | Documents Microsoft
description: "Découvrez comment toouse c# défini par l’utilisateur (UDF) de fonctions avec Hive et Pig de diffusion en continu dans Azure HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: d83def76-12ad-4538-bb8e-3ba3542b7211
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: dd35409766f2dafe4d8050c3f9bc351949473ad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-c-user-defined-functions-with-hive-and-pig-streaming-on-hadoop-in-hdinsight"></a>Utilisation des fonctions définies par l’utilisateur C# avec la diffusion en continu Hive et Pig dans HDInsight

Découvrez comment toouse c# défini par l’utilisateur (UDF) de fonctions avec Apache Hive et Pig dans HDInsight.

> [!IMPORTANT]
> étapes de Hello dans ce document fonctionnent avec des clusters HDInsight à la fois basés sur Linux et Windows. Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure. Pour plus d’informations, consultez [Contrôle de version des composants HDInsight](hdinsight-component-versioning.md).

Les deux Hive et Pig peut passer des applications tooexternal de données pour le traitement. Ce processus est appelé _diffusion en continu (streaming)_. Lorsque vous utilisez une application .NET, les données hello sont transmises toohello application STDIN et application hello retourne les résultats hello dans STDOUT. tooread et en écriture à partir de STDIN et STDOUT, vous pouvez utiliser `Console.ReadLine()` et `Console.WriteLine()` à partir d’une application console.

## <a name="prerequisites"></a>Composants requis

* Des connaissances en écriture et en génération de code C# qui cible .NET Framework 4.5.

    * Utilisez n’importe quel IDE souhaité. Nous vous conseillons d’utiliser [Visual Studio](https://www.visualstudio.com/vs) 2015, 2017 ou [Visual Studio Code](https://code.visualstudio.com/). les étapes dans ce document utilisent Visual Studio 2017 Hello.

* Les fichiers d’une façon tooupload .exe toohello cluster et l’exécution des travaux Pig et Hive. Nous vous recommandons hello Data Lake Tools pour Visual Studio, Azure PowerShell et CLI d’Azure. Hello étapes de ce document utilisent hello Data Lake Tools pour les fichiers de Visual Studio tooupload hello et exécuter la requête de Hive exemple hello.

    Pour plus d’informations sur d’autres requêtes de façons toorun Hive et les travaux de Pig, consultez hello suivant des documents :

    * [Utilisation d’Apache Hive avec HDInsight](hdinsight-use-hive.md)

    * [Utilisation d’Apache Pig avec HDInsight](hdinsight-use-pig.md)

* Un cluster Hadoop sur HDInsight. Pour plus d’informations sur la création d’un cluster, consultez [Créer un cluster HDInsight](hdinsight-provision-clusters.md).

## <a name="net-on-hdinsight"></a>.NET sur HDInsight

* __HDInsight de basés sur Linux__ à l’aide de clusters [Mono (https://mono-project.com)](https://mono-project.com) toorun les applications .NET. La version 4.2.1 de Mono est incluse dans la version 3.5 de HDInsight.

    Pour plus d’informations sur la compatibilité Mono avec les versions de .NET Framework, consultez [Compatibilité Mono](http://www.mono-project.com/docs/about-mono/compatibility/).

    toouse une version spécifique de Mono, consultez hello [installation ou mise à jour Mono](hdinsight-hadoop-install-mono.md) document.

* __HDInsight de basés sur Windows__ clusters utilisent les applications de .NET toorun hello CLR .NET de Microsoft.

Pour plus d’informations sur la version de hello de hello .NET framework et de Mono fournie avec les versions HDInsight, consultez [versions des composants HDInsight](hdinsight-component-versioning.md).

## <a name="create-hello-c-projects"></a>Créer hello C\# projets

### <a name="hive-udf"></a>UDF Hive

1. Ouvrez Visual Studio et créez une solution. Pour le type de projet hello, sélectionnez **l’application Console (.NET Framework)**et un nouveau projet de nom hello **HiveCSharp**.

    > [!IMPORTANT]
    > Si vous utilisez un cluster HDInsight sous Linux, sélectionnez __.NET Framework 4.5__. Pour plus d’informations sur la compatibilité Mono avec les versions de .NET Framework, consultez [Compatibilité Mono](http://www.mono-project.com/docs/about-mono/compatibility/).

2. Remplacez le contenu hello de **Program.cs** avec les éléments suivants de hello :

    ```csharp
    using System;
    using System.Security.Cryptography;
    using System.Text;
    using System.Threading.Tasks;

    namespace HiveCSharp
    {
        class Program
        {
            static void Main(string[] args)
            {
                string line;
                // Read stdin in a loop
                while ((line = Console.ReadLine()) != null)
                {
                    // Parse hello string, trimming line feeds
                    // and splitting fields at tabs
                    line = line.TrimEnd('\n');
                    string[] field = line.Split('\t');
                    string phoneLabel = field[1] + ' ' + field[2];
                    // Emit new data toostdout, delimited by tabs
                    Console.WriteLine("{0}\t{1}\t{2}", field[0], phoneLabel, GetMD5Hash(phoneLabel));
                }
            }
            /// <summary>
            /// Returns an MD5 hash for hello given string
            /// </summary>
            /// <param name="input">string value</param>
            /// <returns>an MD5 hash</returns>
            static string GetMD5Hash(string input)
            {
                // Step 1, calculate MD5 hash from input
                MD5 md5 = System.Security.Cryptography.MD5.Create();
                byte[] inputBytes = System.Text.Encoding.ASCII.GetBytes(input);
                byte[] hash = md5.ComputeHash(inputBytes);

                // Step 2, convert byte array toohex string
                StringBuilder sb = new StringBuilder();
                for (int i = 0; i < hash.Length; i++)
                {
                    sb.Append(hash[i].ToString("x2"));
                }
                return sb.ToString();
            }
        }
    }
    ```

3. Générez le projet de hello.

### <a name="pig-udf"></a>UDF Pig

1. Ouvrez Visual Studio et créez une solution. Pour le type de projet hello, sélectionnez **Application Console**et un nouveau projet de nom hello **PigUDF**.

2. Remplacez le contenu hello Hello **Program.cs** fichier avec hello suivant de code :

    ```csharp
    using System;

    namespace PigUDF
    {
        class Program
        {
            static void Main(string[] args)
            {
                string line;
                // Read stdin in a loop
                while ((line = Console.ReadLine()) != null)
                {
                    // Fix formatting on lines that begin with an exception
                    if(line.StartsWith("java.lang.Exception"))
                    {
                        // Trim hello error info off hello beginning and add a note toohello end of hello line
                        line = line.Remove(0, 21) + " - java.lang.Exception";
                    }
                    // Split hello fields apart at tab characters
                    string[] field = line.Split('\t');
                    // Put fields back together for writing
                    Console.WriteLine(String.Join("\t",field));
                }
            }
        }
    }
    ```

    Cette application traite les lignes hello envoyés à partir de Pig et remise en forme les lignes qui commencent par `java.lang.Exception`.

3. Enregistrer **Program.cs**, puis générez le projet de hello.

## <a name="upload-toostorage"></a>Télécharger toostorage

1. Dans Visual Studio, ouvrez l' **Explorateur de serveurs**.

2. Développez **Azure**, puis **HDInsight**.

3. Si vous y êtes invité, entrez les informations d’identification de votre abonnement Azure, puis cliquez sur **Se connecter**.

4. Développez le cluster HDInsight hello que vous souhaitez toodeploy cette application. Une entrée avec texte hello __(compte de stockage par défaut)__ est répertorié.

    ![Explorateur de serveurs avec le compte de stockage hello pour le cluster de hello](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/storage.png)

    * Si cette entrée peut être développée, vous utilisez un __compte de stockage Azure__ comme stockage par défaut pour le cluster de hello. fichiers hello tooview sur le stockage par défaut hello pour cluster de hello, développez l’entrée de hello et puis double-cliquez sur hello __(conteneur par défaut)__.

    * Si cette entrée ne peut pas être développée, vous utilisez __Azure Data Lake Store__ comme du stockage par défaut pour le cluster de hello hello. fichiers hello tooview sur le stockage par défaut hello pour cluster de hello, double-cliquez sur hello __(compte de stockage par défaut)__ entrée.

6. fichiers .exe de hello tooupload, utilisez une des méthodes suivantes de hello :

    * Si vous utilisez un __compte de stockage Azure__, sur l’icône de téléchargement hello et puis parcourir toohello **bin\debug** dossier hello **HiveCSharp** projet. Enfin, sélectionnez hello **HiveCSharp.exe** de fichier et cliquez sur **Ok**.

        ![icône télécharger](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/upload.png)
    
    * Si vous utilisez __Azure Data Lake Store__, cliquez sur une zone vide dans la liste des fichiers hello, puis sélectionnez __télécharger__. Enfin, sélectionnez hello **HiveCSharp.exe** de fichier et cliquez sur **ouvrir**.

    Une fois hello __HiveCSharp.exe__ téléchargement terminé, le processus de téléchargement hello Répétez ces étapes pour hello __PigUDF.exe__ fichier.

## <a name="run-a-hive-query"></a>Exécution d'une tâche Hive

1. Dans Visual Studio, ouvrez l' **Explorateur de serveurs**.

2. Développez **Azure**, puis **HDInsight**.

3. Cluster de hello avec le bouton que vous avez déployé hello **HiveCSharp** application et sélectionnez **écrire une requête Hive**.

4. Utilisez hello après le texte de la requête de ruche hello :

    ```hiveql
    -- Uncomment hello following if you are using Azure Storage
    -- add file wasb:///HiveCSharp.exe;
    -- Uncomment hello following if you are using Azure Data Lake Store
    -- add file adl:///HiveCSharp.exe;

    SELECT TRANSFORM (clientid, devicemake, devicemodel)
    USING 'HiveCSharp.exe' AS
    (clientid string, phoneLabel string, phoneHash string)
    FROM hivesampletable
    ORDER BY clientid LIMIT 50;
    ```

    > [!IMPORTANT]
    > Supprimez les commentaires hello `add file` instruction qui correspond au type hello de stockage par défaut utilisés pour votre cluster.

    Cette requête sélectionne hello `clientid`, `devicemake`, et `devicemodel` des champs `hivesampletable`et transmet les champs hello toohello HiveCSharp.exe application. requête de Hello attend hello tooreturn trois champs de l’application, qui sont stockées en tant que `clientid`, `phoneLabel`, et `phoneHash`. requête de Hello attend également toofind HiveCSharp.exe racine hello hello par défaut du conteneur de stockage.

5. Cliquez sur **Submit** le cluster HDInsight toohello toosubmit hello travail. Hello **récapitulatif de la ruche** fenêtre s’ouvre.

6. Cliquez sur **Actualiser** hello toorefresh synthèse jusqu'à **état du travail** change également**terminé**. sortie de la tâche de hello tooview, cliquez sur **sortie de travail**.

## <a name="run-a-pig-job"></a>Exécution d’une tâche Pig

1. Utilisez une des hello suivant du cluster HDInsight de méthodes tooconnect tooyour :

    * Si vous utilisez un cluster HDInsight __sous Linux__, utilisez SSH. Par exemple, `ssh sshuser@mycluster-ssh.azurehdinsight.net`. Pour plus d’informations, consultez la rubrique [Utilisation de SSH avec HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)
    
    * Si vous utilisez un __basé sur Windows__ cluster HDInsight, [cluster toohello de se connecter à l’aide du Bureau à distance](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)

2. Utilisez une hello ligne de commande commande toostart hello Pig :

        pig

    > [!IMPORTANT]
    > Si vous utilisez un cluster Windows, utilisez hello suivant à la place les commandes :
    > ```
    > cd %PIG_HOME%
    > bin\pig
    > ```

    Une invite `grunt>` s’affiche.

3. Entrez hello suivant toorun un travail Pig qui utilise l’application de .NET Framework hello :

        DEFINE streamer `PigUDF.exe` CACHE('/PigUDF.exe');
        LOGS = LOAD '/example/data/sample.log' as (LINE:chararray);
        LOG = FILTER LOGS by LINE is not null;
        DETAILS = STREAM LOG through streamer as (col1, col2, col3, col4, col5);
        DUMP DETAILS;

    Hello `DEFINE` instruction crée un alias de `streamer` pour les applications pigudf.exe hello, et `CACHE` charge à partir de stockage par défaut pour le cluster de hello. Une version ultérieure, `streamer` est utilisé avec hello `STREAM` opérateur tooprocess hello lignes uniques contenus dans les journaux et de données de retour hello sous la forme d’une série de colonnes.

    > [!NOTE]
    > nom de l’application Hello qui est utilisé pour la diffusion en continu doit être entouré de hello \` (backtick) de caractères quand un alias, et ' (apostrophe) lorsqu’il est utilisé avec `SHIP`.

4. Après avoir entré la dernière ligne de hello, hello doit démarrer. Il retourne toohello similaire de sortie suivant du texte :

        (2012-02-03 20:11:56 SampleClass5 [WARN] problem finding id 1358451042 - java.lang.Exception)
        (2012-02-03 20:11:56 SampleClass5 [DEBUG] detail for id 1976092771)
        (2012-02-03 20:11:56 SampleClass5 [TRACE] verbose detail for id 1317358561)
        (2012-02-03 20:11:56 SampleClass5 [TRACE] verbose detail for id 1737534798)
        (2012-02-03 20:11:56 SampleClass7 [DEBUG] detail for id 1475865947)

## <a name="next-steps"></a>Étapes suivantes

Dans ce document, vous avez appris comment toouse une application .NET Framework à partir de Hive et Pig dans HDInsight. Si vous souhaitez que toolearn toouse Python avec Hive et Pig, voir [utilisation de Python avec Hive et Pig dans HDInsight](hdinsight-python.md).

Pour les autres façons toouse Pig et Hive et toolearn sur l’utilisation de MapReduce, consultez hello suivant des documents :

* [Utilisation de Hive avec HDInsight](hdinsight-use-hive.md)
* [Utilisation de Pig avec HDInsight](hdinsight-use-pig.md)
* [Utilisation de MapReduce avec HDInsight](hdinsight-use-mapreduce.md)
