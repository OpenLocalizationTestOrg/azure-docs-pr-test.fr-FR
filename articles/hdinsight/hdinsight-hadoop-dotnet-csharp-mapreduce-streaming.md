---
title: Utilisation de C# avec MapReduce sur Hadoop dans HDInsight, Azure | Microsoft Docs
description: "Découvrez comment utiliser C# pour créer des solutions MapReduce avec Hadoop dans Azure HDInsight."
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
ms.openlocfilehash: adb454e56378a800c671614735aec78b6851aeb2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="use-c-with-mapreduce-streaming-on-hadoop-in-hdinsight"></a><span data-ttu-id="c00be-103">Utilisation de C# avec Diffusion en continu MapReduce sur Hadoop dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="c00be-103">Use C# with MapReduce streaming on Hadoop in HDInsight</span></span>

<span data-ttu-id="c00be-104">Découvrez comment utiliser C# pour créer une solution MapReduce dans HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c00be-104">Learn how to use C# to create a MapReduce solution on HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c00be-105">Linux est le seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="c00be-105">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="c00be-106">Pour plus d’informations, consultez [Contrôle de version des composants HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="c00be-106">For more information, see [HDInsight component versioning](hdinsight-component-versioning.md).</span></span>

<span data-ttu-id="c00be-107">Diffusion en continu Hadoop est un utilitaire qui vous permet d’exécuter des tâches MapReduce à l’aide d’un script ou d’un exécutable.</span><span class="sxs-lookup"><span data-stu-id="c00be-107">Hadoop streaming is a utility that allows you to run MapReduce jobs using a script or executable.</span></span> <span data-ttu-id="c00be-108">Dans cet exemple, .NET est utilisé pour implémenter le mappeur et le raccord de réduction pour une solution de comptage de mots.</span><span class="sxs-lookup"><span data-stu-id="c00be-108">In this example, .NET is used to implement the mapper and reducer for a word count solution.</span></span>

## <a name="net-on-hdinsight"></a><span data-ttu-id="c00be-109">.NET sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="c00be-109">.NET on HDInsight</span></span>

<span data-ttu-id="c00be-110">Les clusters __HDInsight sous Linux__ utilisent [Mono (https://mono-project.com)](https://mono-project.com) pour exécuter des applications .NET.</span><span class="sxs-lookup"><span data-stu-id="c00be-110">__Linux-based HDInsight__ clusters use [Mono (https://mono-project.com)](https://mono-project.com) to run .NET applications.</span></span> <span data-ttu-id="c00be-111">La version 4.2.1 de Mono est incluse dans la version 3.5 de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c00be-111">Mono version 4.2.1 is included with HDInsight version 3.5.</span></span> <span data-ttu-id="c00be-112">Pour plus d’informations sur la version de Mono fournie avec HDInsight, consultez [Versions des composants HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="c00be-112">For more information on the version of Mono included with HDInsight, see [HDInsight component versions](hdinsight-component-versioning.md).</span></span> <span data-ttu-id="c00be-113">Pour utiliser une version particulière de Mono, consultez le document [Installation ou mise à jour de Mono](hdinsight-hadoop-install-mono.md).</span><span class="sxs-lookup"><span data-stu-id="c00be-113">To use a specific version of Mono, see the [Install or update Mono](hdinsight-hadoop-install-mono.md) document.</span></span>

<span data-ttu-id="c00be-114">Pour plus d’informations sur la compatibilité Mono avec les versions de .NET Framework, consultez [Compatibilité Mono](http://www.mono-project.com/docs/about-mono/compatibility/).</span><span class="sxs-lookup"><span data-stu-id="c00be-114">For more information on Mono compatibility with .NET Framework versions, see [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/).</span></span>

## <a name="how-hadoop-streaming-works"></a><span data-ttu-id="c00be-115">Fonctionnement de la diffusion en continu Hadoop</span><span class="sxs-lookup"><span data-stu-id="c00be-115">How Hadoop streaming works</span></span>

<span data-ttu-id="c00be-116">Le processus de base utilisé pour la diffusion en continu dans ce document est la suivante :</span><span class="sxs-lookup"><span data-stu-id="c00be-116">The basic process used for streaming in this document is as follows:</span></span>

1. <span data-ttu-id="c00be-117">Hadoop transmet des données vers le mappeur (mapper.exe dans cet exemple) sur STDIN.</span><span class="sxs-lookup"><span data-stu-id="c00be-117">Hadoop passes data to the mapper (mapper.exe in this example) on STDIN.</span></span>
2. <span data-ttu-id="c00be-118">Le mappeur traite les données et émet des paires clé/valeur séparées par des tabulations sur STDOUT.</span><span class="sxs-lookup"><span data-stu-id="c00be-118">The mapper processes the data, and emits tab-delimited key/value pairs to STDOUT.</span></span>
3. <span data-ttu-id="c00be-119">La sortie est lue par Hadoop, puis transmise au raccord de réduction (reducer.exe dans cet exemple) sur STDIN.</span><span class="sxs-lookup"><span data-stu-id="c00be-119">The output is read by Hadoop, and then passed to the reducer (reducer.exe in this example) on STDIN.</span></span>
4. <span data-ttu-id="c00be-120">Le raccord de réduction lit les paires clé/valeur séparées par des tabulations, traite les données, puis émet le résultat sous forme de paires clé/valeur séparées par des tabulations sur STDOUT.</span><span class="sxs-lookup"><span data-stu-id="c00be-120">The reducer reads the tab-delimited key/value pairs, processes the data, and then emits the result as tab-delimited key/value pairs on STDOUT.</span></span>
5. <span data-ttu-id="c00be-121">La sortie est lue par Hadoop et écrite dans le répertoire de sortie.</span><span class="sxs-lookup"><span data-stu-id="c00be-121">The output is read by Hadoop and written to the output directory.</span></span>

<span data-ttu-id="c00be-122">Pour plus d’informations sur la diffusion en continu, consultez [Diffusion en continu Hadoop (https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html)](https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html).</span><span class="sxs-lookup"><span data-stu-id="c00be-122">For more information on streaming, see [Hadoop Streaming (https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html)](https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c00be-123">Composants requis</span><span class="sxs-lookup"><span data-stu-id="c00be-123">Prerequisites</span></span>

* <span data-ttu-id="c00be-124">Des connaissances en écriture et en génération de code C# qui cible .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="c00be-124">A familiarity with writing and building C# code that targets .NET Framework 4.5.</span></span> <span data-ttu-id="c00be-125">Dans le cadre de ce document, Visual Studio 2017 a été utilisé.</span><span class="sxs-lookup"><span data-stu-id="c00be-125">The steps in this document use Visual Studio 2017.</span></span>

* <span data-ttu-id="c00be-126">Permet de charger des fichiers .exe dans le cluster.</span><span class="sxs-lookup"><span data-stu-id="c00be-126">A way to upload .exe files to the cluster.</span></span> <span data-ttu-id="c00be-127">Les étapes de ce document utilisent Data Lake Tools pour Visual Studio pour télécharger les fichiers vers le stockage principal pour le cluster.</span><span class="sxs-lookup"><span data-stu-id="c00be-127">The steps in this document use the Data Lake Tools for Visual Studio to upload the files to primary storage for the cluster.</span></span>

* <span data-ttu-id="c00be-128">Azure PowerShell ou un client SSH.</span><span class="sxs-lookup"><span data-stu-id="c00be-128">Azure PowerShell or a SSH client.</span></span>

* <span data-ttu-id="c00be-129">Un cluster Hadoop sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c00be-129">A Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="c00be-130">Pour plus d’informations sur la création d’un cluster, consultez [Créer un cluster HDInsight](hdinsight-provision-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="c00be-130">For more information on creating a cluster, see [Create an HDInsight cluster](hdinsight-provision-clusters.md).</span></span>

## <a name="create-the-mapper"></a><span data-ttu-id="c00be-131">Créer le mappeur</span><span class="sxs-lookup"><span data-stu-id="c00be-131">Create the mapper</span></span>

<span data-ttu-id="c00be-132">Dans Visual Studio, créez une nouvelle __Application console__ nommée __mappeur__.</span><span class="sxs-lookup"><span data-stu-id="c00be-132">In Visual Studio, create a new __Console application__ named __mapper__.</span></span> <span data-ttu-id="c00be-133">Utilisez le code suivant pour l’application :</span><span class="sxs-lookup"><span data-stu-id="c00be-133">Use the following code for the application:</span></span>

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
            //Hadoop passes data to the mapper on STDIN
            while((line = Console.ReadLine()) != null)
            {
                // We only want words, so strip out punctuation, numbers, etc.
                var onlyText = Regex.Replace(line, @"\.|;|:|,|[0-9]|'", "");
                // Split at whitespace.
                var words = Regex.Matches(onlyText, @"[\w]+");
                // Loop over the words
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

<span data-ttu-id="c00be-134">Après avoir créé l’application, générez-la pour produire le fichier `/bin/Debug/mapper.exe` dans le répertoire du projet.</span><span class="sxs-lookup"><span data-stu-id="c00be-134">After creating the application, build it to produce the `/bin/Debug/mapper.exe` file in the project directory.</span></span>

## <a name="create-the-reducer"></a><span data-ttu-id="c00be-135">Créer le raccord de réduction</span><span class="sxs-lookup"><span data-stu-id="c00be-135">Create the reducer</span></span>

<span data-ttu-id="c00be-136">Dans Visual Studio, créez une nouvelle __Application console__ nommée __raccord de réduction__.</span><span class="sxs-lookup"><span data-stu-id="c00be-136">In Visual Studio, create a new __Console application__ named __reducer__.</span></span> <span data-ttu-id="c00be-137">Utilisez le code suivant pour l’application :</span><span class="sxs-lookup"><span data-stu-id="c00be-137">Use the following code for the application:</span></span>

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
                // Get the word
                string word = sArr[0];
                // Get the count
                int count = Convert.ToInt32(sArr[1]);

                //Do we already have a count for the word?
                if(words.ContainsKey(word))
                {
                    //If so, increment the count
                    words[word] += count;
                } else
                {
                    //Add the key to the collection
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

<span data-ttu-id="c00be-138">Après avoir créé l’application, générez-la pour produire le fichier `/bin/Debug/reducer.exe` dans le répertoire du projet.</span><span class="sxs-lookup"><span data-stu-id="c00be-138">After creating the application, build it to produce the `/bin/Debug/reducer.exe` file in the project directory.</span></span>

## <a name="upload-to-storage"></a><span data-ttu-id="c00be-139">Téléchargement vers le stockage</span><span class="sxs-lookup"><span data-stu-id="c00be-139">Upload to storage</span></span>

1. <span data-ttu-id="c00be-140">Dans Visual Studio, ouvrez l' **Explorateur de serveurs**.</span><span class="sxs-lookup"><span data-stu-id="c00be-140">In Visual Studio, open **Server Explorer**.</span></span>

2. <span data-ttu-id="c00be-141">Développez **Azure**, puis **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="c00be-141">Expand **Azure**, and then expand **HDInsight**.</span></span>

3. <span data-ttu-id="c00be-142">Si vous y êtes invité, entrez les informations d’identification de votre abonnement Azure, puis cliquez sur **Se connecter**.</span><span class="sxs-lookup"><span data-stu-id="c00be-142">If prompted, enter your Azure subscription credentials, and then click **Sign In**.</span></span>

4. <span data-ttu-id="c00be-143">Développez le cluster HDInsight sur lequel vous souhaitez déployer cette application.</span><span class="sxs-lookup"><span data-stu-id="c00be-143">Expand the HDInsight cluster that you wish to deploy this application to.</span></span> <span data-ttu-id="c00be-144">Une entrée avec le texte __(compte de stockage par défaut)__ est répertoriée.</span><span class="sxs-lookup"><span data-stu-id="c00be-144">An entry with the text __(Default Storage Account)__ is listed.</span></span>

    ![Explorateur de serveurs affichant le compte de stockage pour le cluster](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/storage.png)

    * <span data-ttu-id="c00be-146">Si cette entrée peut être développée, vous utilisez un __compte de stockage Azure__ en tant que stockage par défaut pour le cluster.</span><span class="sxs-lookup"><span data-stu-id="c00be-146">If this entry can be expanded, you are using an __Azure Storage Account__ as default storage for the cluster.</span></span> <span data-ttu-id="c00be-147">Pour afficher les fichiers sur le stockage par défaut pour le cluster, développez l’entrée et double-cliquez sur le __(conteneur par défaut)__.</span><span class="sxs-lookup"><span data-stu-id="c00be-147">To view the files on the default storage for the cluster, expand the entry and then double-click the __(Default Container)__.</span></span>

    * <span data-ttu-id="c00be-148">Si cette entrée ne peut pas être développée, vous utilisez __Azure Data Lake Store__ en tant que stockage par défaut pour le cluster.</span><span class="sxs-lookup"><span data-stu-id="c00be-148">If this entry cannot be expanded, you are using __Azure Data Lake Store__ as the default storage for the cluster.</span></span> <span data-ttu-id="c00be-149">Pour afficher les fichiers sur le stockage par défaut pour le cluster, double-cliquez sur l’entrée __(compte de stockage par défaut)__.</span><span class="sxs-lookup"><span data-stu-id="c00be-149">To view the files on the default storage for the cluster, double-click the __(Default Storage Account)__ entry.</span></span>

5. <span data-ttu-id="c00be-150">Pour charger les fichiers .exe, appliquez l’une des méthodes suivantes :</span><span class="sxs-lookup"><span data-stu-id="c00be-150">To upload the .exe files, use one of the following methods:</span></span>

    * <span data-ttu-id="c00be-151">Si vous utilisez un __compte de stockage Azure__, cliquez sur l’icône de chargement, puis accédez au dossier **bin\debug** pour le projet **Mappeur**.</span><span class="sxs-lookup"><span data-stu-id="c00be-151">If using an __Azure Storage Account__, click the upload icon, and then browse to the **bin\debug** folder for the **mapper** project.</span></span> <span data-ttu-id="c00be-152">Enfin, sélectionnez le fichier **mapper.exe** et cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="c00be-152">Finally, select the **mapper.exe** file and click **Ok**.</span></span>

        ![icône télécharger](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/upload.png)
    
    * <span data-ttu-id="c00be-154">Si vous utilisez __Azure Data Lake Store__, faites un clic droit sur une zone vide de la liste des fichiers, puis sélectionnez __Charger__.</span><span class="sxs-lookup"><span data-stu-id="c00be-154">If using __Azure Data Lake Store__, right-click an empty area in the file listing, and then select __Upload__.</span></span> <span data-ttu-id="c00be-155">Enfin, sélectionnez le fichier **mapper.exe** et cliquez sur **Ouvrir**.</span><span class="sxs-lookup"><span data-stu-id="c00be-155">Finally, select the **mapper.exe** file and click **Open**.</span></span>

    <span data-ttu-id="c00be-156">Une fois que le chargement de __mapper.exe__ est terminé, répétez le processus de chargement pour le fichier __reducer.exe__.</span><span class="sxs-lookup"><span data-stu-id="c00be-156">Once the __mapper.exe__ upload has finished, repeat the upload process for the __reducer.exe__ file.</span></span>

## <a name="run-a-job-using-an-ssh-session"></a><span data-ttu-id="c00be-157">Exécution d’une tâche : avec une session SSH</span><span class="sxs-lookup"><span data-stu-id="c00be-157">Run a job: Using an SSH session</span></span>

1. <span data-ttu-id="c00be-158">Utilisez SSH pour vous connecter au cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c00be-158">Use SSH to connect to the HDInsight cluster.</span></span> <span data-ttu-id="c00be-159">Pour en savoir plus, voir [Utilisation de SSH avec Hadoop Linux sur HDInsight depuis Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="c00be-159">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="c00be-160">Exécutez une des commandes suivantes pour démarrer la tâche MapReduce :</span><span class="sxs-lookup"><span data-stu-id="c00be-160">Use one of the following command to start the MapReduce job:</span></span>

    * <span data-ttu-id="c00be-161">Si vous utilisez __Data Lake Store__ en tant que stockage par défaut :</span><span class="sxs-lookup"><span data-stu-id="c00be-161">If using __Data Lake Store__ as default storage:</span></span>

        ```bash
        yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files adl:///mapper.exe,adl:///reducer.exe -mapper mapper.exe -reducer reducer.exe -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
        ```
    
    * <span data-ttu-id="c00be-162">Si vous utilisez __Stockage Azure__ en tant que stockage par défaut :</span><span class="sxs-lookup"><span data-stu-id="c00be-162">If using __Azure Storage__ as default storage:</span></span>

        ```bash
        yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files wasb:///mapper.exe,wasb:///reducer.exe -mapper mapper.exe -reducer reducer.exe -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
        ```

    <span data-ttu-id="c00be-163">La liste suivante décrit la signification de chaque paramètre :</span><span class="sxs-lookup"><span data-stu-id="c00be-163">The following list describes what each parameter does:</span></span>

    * <span data-ttu-id="c00be-164">`hadoop-streaming.jar` : le fichier jar contenant la fonctionnalité MapReduce de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="c00be-164">`hadoop-streaming.jar`: The jar file that contains the streaming MapReduce functionality.</span></span>
    * <span data-ttu-id="c00be-165">`-files` : ajoute les fichiers `mapper.exe` et `reducer.exe` à cette tâche.</span><span class="sxs-lookup"><span data-stu-id="c00be-165">`-files`: Adds the `mapper.exe` and `reducer.exe` files to this job.</span></span> <span data-ttu-id="c00be-166">`adl:///` ou `wasb:///` devant chaque fichier est le chemin d’accès à la racine du stockage par défaut pour le cluster.</span><span class="sxs-lookup"><span data-stu-id="c00be-166">The `adl:///` or `wasb:///` before each file is the path to the root of default storage for the cluster.</span></span>
    * <span data-ttu-id="c00be-167">`-mapper` : indique le fichier qui implémente le mappeur.</span><span class="sxs-lookup"><span data-stu-id="c00be-167">`-mapper`: Specifies which file implements the mapper.</span></span>
    * <span data-ttu-id="c00be-168">`-reducer` : indique le fichier qui implémente le raccord de réduction.</span><span class="sxs-lookup"><span data-stu-id="c00be-168">`-reducer`: Specifies which file implements the reducer.</span></span>
    * <span data-ttu-id="c00be-169">`-input` : les données d’entrée.</span><span class="sxs-lookup"><span data-stu-id="c00be-169">`-input`: The input data.</span></span>
    * <span data-ttu-id="c00be-170">`-output` : le répertoire de sortie.</span><span class="sxs-lookup"><span data-stu-id="c00be-170">`-output`: The output directory.</span></span>

3. <span data-ttu-id="c00be-171">Une fois la tâche MapReduce terminée, utilisez la commande suivante pour afficher les résultats :</span><span class="sxs-lookup"><span data-stu-id="c00be-171">Once the MapReduce job completes, use the following to view the results:</span></span>

    ```bash
    hdfs dfs -text /example/wordcountout/part-00000
    ```

    <span data-ttu-id="c00be-172">Le texte suivant est un exemple de données renvoyées par cette commande :</span><span class="sxs-lookup"><span data-stu-id="c00be-172">The following text is an example of the data returned by this command:</span></span>

        you     1128
        young   38
        younger 1
        youngest        1
        your    338
        yours   4
        yourself        34
        yourselves      3
        youth   17

## <a name="run-a-job-using-powershell"></a><span data-ttu-id="c00be-173">Exécution d’une tâche : avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="c00be-173">Run a job: Using PowerShell</span></span>

<span data-ttu-id="c00be-174">Utilisez le script PowerShell suivant pour exécuter une tâche MapReduce et télécharger les résultats.</span><span class="sxs-lookup"><span data-stu-id="c00be-174">Use the following PowerShell script to run a MapReduce job and download the results.</span></span>

<span data-ttu-id="c00be-175">[!code-powershell[main](../../powershell_scripts/hdinsight/use-csharp-mapreduce/use-csharp-mapreduce.ps1?range=5-87)]</span><span class="sxs-lookup"><span data-stu-id="c00be-175">[!code-powershell[main](../../powershell_scripts/hdinsight/use-csharp-mapreduce/use-csharp-mapreduce.ps1?range=5-87)]</span></span>

<span data-ttu-id="c00be-176">Ce script vous invite à entrer le nom et le mot de passe du compte de connexion du cluster, ainsi que le nom du cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c00be-176">This script prompts you for the cluster login account name and password, along with the HDInsight cluster name.</span></span> <span data-ttu-id="c00be-177">Une fois la tâche terminée, la sortie est téléchargée vers le fichier `output.txt` dans le répertoire à partir duquel le script est exécuté.</span><span class="sxs-lookup"><span data-stu-id="c00be-177">Once the job completes, the output is downloaded to the `output.txt` file in the directory the script is ran from.</span></span> <span data-ttu-id="c00be-178">Le texte suivant constitue un exemple des données contenues dans le fichier `output.txt` :</span><span class="sxs-lookup"><span data-stu-id="c00be-178">The following text is an example of the data in the `output.txt` file:</span></span>

    you     1128
    young   38
    younger 1
    youngest        1
    your    338
    yours   4
    yourself        34
    yourselves      3
    youth   17

## <a name="next-steps"></a><span data-ttu-id="c00be-179">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c00be-179">Next steps</span></span>

<span data-ttu-id="c00be-180">Pour plus d’informations sur l’utilisation de MapReduce avec HDInsight, consultez [Utilisation de MapReduce avec HDInsight](hdinsight-use-mapreduce.md).</span><span class="sxs-lookup"><span data-stu-id="c00be-180">For more information on using MapReduce with HDInsight, see [Use MapReduce with HDInsight](hdinsight-use-mapreduce.md).</span></span>

<span data-ttu-id="c00be-181">Pour plus d’informations sur l’utilisation de C# avec Hive et Pig, consultez [Utilisation d’une fonction définie par l’utilisateur C# avec Hive et Pig](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="c00be-181">For information on using C# with Hive and Pig, see [Use a C# user defined function with Hive and Pig](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md).</span></span>

<span data-ttu-id="c00be-182">Pour plus d’informations sur l’utilisation de C# avec Storm sur HDInsight, consultez [Développement de topologies C# pour Storm sur HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="c00be-182">For information on using C# with Storm on HDInsight, see [Develop C# topologies for Storm on HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>