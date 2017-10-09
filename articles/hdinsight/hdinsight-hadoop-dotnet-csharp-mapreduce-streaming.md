---
title: aaaUse c# avec MapReduce sur Hadoop dans HDInsight - Azure | Documents Microsoft
description: "Découvrez comment toouse c# toocreate MapReduce solutions avec Hadoop dans HDInsight de Azure."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: d83def76-12ad-4538-bb8e-3ba3542b7211
ms.custom: hdinsightactive
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: dd8b684e74155bc1a37d4ab8d6f9033276ef5aa3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-c-with-mapreduce-streaming-on-hadoop-in-hdinsight"></a>Utilisation de C# avec Diffusion en continu MapReduce sur Hadoop dans HDInsight

Découvrez comment toouse c# toocreate une solution MapReduce dans HDInsight.

> [!IMPORTANT]
> Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure. Pour plus d’informations, consultez [Contrôle de version des composants HDInsight](hdinsight-component-versioning.md).

Diffusion en continu Hadoop est un utilitaire qui vous permet des tâches MapReduce toorun à l’aide d’un script ou un exécutable. Dans cet exemple, .NET est utilisé tooimplement hello Mappeur et réducteur pour une solution de nombre de word.

## <a name="net-on-hdinsight"></a>.NET sur HDInsight

__HDInsight de basés sur Linux__ utilisation des clusters [Mono (https://mono-project.com)](https://mono-project.com) toorun les applications .NET. La version 4.2.1 de Mono est incluse dans la version 3.5 de HDInsight. Pour plus d’informations sur la version de hello de Mono inclus avec HDInsight, consultez [versions des composants HDInsight](hdinsight-component-versioning.md). toouse une version spécifique de Mono, consultez hello [installation ou mise à jour Mono](hdinsight-hadoop-install-mono.md) document.

Pour plus d’informations sur la compatibilité Mono avec les versions de .NET Framework, consultez [Compatibilité Mono](http://www.mono-project.com/docs/about-mono/compatibility/).

## <a name="how-hadoop-streaming-works"></a>Fonctionnement de la diffusion en continu Hadoop

processus de base Hello utilisé pour la diffusion en continu dans ce document est la suivante :

1. Hadoop passe STDIN Mappeur des données de toohello (mapper.exe dans cet exemple).
2. le Mappeur Hello traite les données de hello et émet tooSTDOUT de paires clé/valeur délimité par des tabulations.
3. sortie de Hello est lu par Hadoop et puis transmise STDIN toohello réducteur (reducer.exe dans cet exemple).
4. Réducteur de Hello lit les paires clé/valeur de hello délimité par des tabulations, traite les données de hello, puis émet les résultats hello sous forme de paires clé/valeur délimité par des tabulations dans STDOUT.
5. sortie de Hello est lu par Hadoop et écrit le répertoire de sortie toohello.

Pour plus d’informations sur la diffusion en continu, consultez [Diffusion en continu Hadoop (https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html)](https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html).

## <a name="prerequisites"></a>Composants requis

* Des connaissances en écriture et en génération de code C# qui cible .NET Framework 4.5. les étapes dans ce document utilisent Visual Studio 2017 Hello.

* Les fichiers d’une façon tooupload .exe toohello cluster. Hello étapes de ce document utilisent hello Data Lake Tools pour Visual Studio tooupload hello fichiers tooprimary stockage pour hello cluster.

* Azure PowerShell ou un client SSH.

* Un cluster Hadoop sur HDInsight. Pour plus d’informations sur la création d’un cluster, consultez [Créer un cluster HDInsight](hdinsight-provision-clusters.md).

## <a name="create-hello-mapper"></a>Créer le mappeur de hello

Dans Visual Studio, créez une nouvelle __Application console__ nommée __mappeur__. Utilisez hello suivant le code de l’application hello :

```csharp
using System;
using System.Text.RegularExpressions;

namespace mapper
{
    class Program
    {
        static void Main(string[] args)
        {
            string line;
            //Hadoop passes data toohello mapper on STDIN
            while((line = Console.ReadLine()) != null)
            {
                // We only want words, so strip out punctuation, numbers, etc.
                var onlyText = Regex.Replace(line, @"\.|;|:|,|[0-9]|'", "");
                // Split at whitespace.
                var words = Regex.Matches(onlyText, @"[\w]+");
                // Loop over hello words
                foreach(var word in words)
                {
                    //Emit tab-delimited key/value pairs.
                    //In this case, a word and a count of 1.
                    Console.WriteLine("{0}\t1",word);
                }
            }
        }
    }
}
```

Après avoir créé l’application hello, générez-le tooproduce hello `/bin/Debug/mapper.exe` fichier dans le répertoire du projet hello.

## <a name="create-hello-reducer"></a>Créer le réducteur de hello

Dans Visual Studio, créez une nouvelle __Application console__ nommée __raccord de réduction__. Utilisez hello suivant le code de l’application hello :

```csharp
using System;
using System.Collections.Generic;

namespace reducer
{
    class Program
    {
        static void Main(string[] args)
        {
            //Dictionary for holding a count of words
            Dictionary<string, int> words = new Dictionary<string, int>();

            string line;
            //Read from STDIN
            while ((line = Console.ReadLine()) != null)
            {
                // Data from Hadoop is tab-delimited key/value pairs
                var sArr = line.Split('\t');
                // Get hello word
                string word = sArr[0];
                // Get hello count
                int count = Convert.ToInt32(sArr[1]);

                //Do we already have a count for hello word?
                if(words.ContainsKey(word))
                {
                    //If so, increment hello count
                    words[word] += count;
                } else
                {
                    //Add hello key toohello collection
                    words.Add(word, count);
                }
            }
            //Finally, emit each word and count
            foreach (var word in words)
            {
                //Emit tab-delimited key/value pairs.
                //In this case, a word and a count of 1.
                Console.WriteLine("{0}\t{1}", word.Key, word.Value);
            }
        }
    }
}
```

Après avoir créé l’application hello, générez-le tooproduce hello `/bin/Debug/reducer.exe` fichier dans le répertoire du projet hello.

## <a name="upload-toostorage"></a>Télécharger toostorage

1. Dans Visual Studio, ouvrez l' **Explorateur de serveurs**.

2. Développez **Azure**, puis **HDInsight**.

3. Si vous y êtes invité, entrez les informations d’identification de votre abonnement Azure, puis cliquez sur **Se connecter**.

4. Développez le cluster HDInsight hello que vous souhaitez toodeploy cette application. Une entrée avec texte hello __(compte de stockage par défaut)__ est répertorié.

    ![Explorateur de serveurs avec le compte de stockage hello pour le cluster de hello](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/storage.png)

    * Si cette entrée peut être développée, vous utilisez un __compte de stockage Azure__ comme stockage par défaut pour le cluster de hello. fichiers hello tooview sur le stockage par défaut hello pour cluster de hello, développez l’entrée de hello et puis double-cliquez sur hello __(conteneur par défaut)__.

    * Si cette entrée ne peut pas être développée, vous utilisez __Azure Data Lake Store__ comme du stockage par défaut pour le cluster de hello hello. fichiers hello tooview sur le stockage par défaut hello pour cluster de hello, double-cliquez sur hello __(compte de stockage par défaut)__ entrée.

5. fichiers .exe de hello tooupload, utilisez une des méthodes suivantes de hello :

    * Si vous utilisez un __compte de stockage Azure__, sur l’icône de téléchargement hello et puis parcourir toohello **bin\debug** dossier hello **Mappeur** projet. Enfin, sélectionnez hello **mapper.exe** de fichier et cliquez sur **Ok**.

        ![icône télécharger](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/upload.png)
    
    * Si vous utilisez __Azure Data Lake Store__, cliquez sur une zone vide dans la liste des fichiers hello, puis sélectionnez __télécharger__. Enfin, sélectionnez hello **mapper.exe** de fichier et cliquez sur **ouvrir**.

    Une fois hello __mapper.exe__ téléchargement terminé, le processus de téléchargement hello Répétez ces étapes pour hello __reducer.exe__ fichier.

## <a name="run-a-job-using-an-ssh-session"></a>Exécution d’une tâche : avec une session SSH

1. Utiliser SSH tooconnect toohello HDInsight cluster. Pour en savoir plus, voir [Utilisation de SSH avec Hadoop Linux sur HDInsight depuis Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Utilisez une des hello suivant tâche MapReduce de commande toostart hello :

    * Si vous utilisez __Data Lake Store__ en tant que stockage par défaut :

        ```bash
        yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files adl:///mapper.exe,adl:///reducer.exe -mapper mapper.exe -reducer reducer.exe -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
        ```
    
    * Si vous utilisez __Stockage Azure__ en tant que stockage par défaut :

        ```bash
        yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files wasb:///mapper.exe,wasb:///reducer.exe -mapper mapper.exe -reducer reducer.exe -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
        ```

    Hello suivant liste décrit ce que fait chaque paramètre :

    * `hadoop-streaming.jar`: fichier jar hello contenant hello MapReduce fonctionnalité de diffusion en continu.
    * `-files`: Ajoute hello `mapper.exe` et `reducer.exe` travail toothis des fichiers. Hello `adl:///` ou `wasb:///` avant chaque fichier racine de toohello hello chemin d’accès de stockage par défaut pour le cluster de hello.
    * `-mapper`: Spécifie le fichier qui implémente le Mappeur hello.
    * `-reducer`: Spécifie le fichier qui implémente le réducteur de hello.
    * `-input`: hello les données d’entrée.
    * `-output`: répertoire de sortie hello.

3. Une fois la tâche MapReduce de hello est terminée, utilisez hello suivant des résultats de hello tooview :

    ```bash
    hdfs dfs -text /example/wordcountout/part-00000
    ```

    Hello texte suivant est un exemple de données hello retournés par cette commande :

        you     1128
        young   38
        younger 1
        youngest        1
        your    338
        yours   4
        yourself        34
        yourselves      3
        youth   17

## <a name="run-a-job-using-powershell"></a>Exécution d’une tâche : avec PowerShell

Utilisez hello suivant toorun de script PowerShell une tâche MapReduce et télécharger les résultats de hello.

[!code-powershell[main](../../powershell_scripts/hdinsight/use-csharp-mapreduce/use-csharp-mapreduce.ps1?range=5-87)]

Ce script vous invite pour le nom de compte de connexion de cluster hello et le mot de passe, ainsi que le nom du cluster HDInsight hello. Une fois que hello est terminée, sortie de hello est téléchargé toohello `output.txt` fichier de script de hello directory hello est exécuté à partir de. Bonjour texte suivant est un exemple de données hello Bonjour `output.txt` fichier :

    you     1128
    young   38
    younger 1
    youngest        1
    your    338
    yours   4
    yourself        34
    yourselves      3
    youth   17

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur l’utilisation de MapReduce avec HDInsight, consultez [Utilisation de MapReduce avec HDInsight](hdinsight-use-mapreduce.md).

Pour plus d’informations sur l’utilisation de C# avec Hive et Pig, consultez [Utilisation d’une fonction définie par l’utilisateur C# avec Hive et Pig](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md).

Pour plus d’informations sur l’utilisation de C# avec Storm sur HDInsight, consultez [Développement de topologies C# pour Storm sur HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md).