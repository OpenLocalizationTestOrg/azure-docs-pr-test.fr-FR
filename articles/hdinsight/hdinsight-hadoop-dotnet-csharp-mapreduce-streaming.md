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
# <a name="use-c-with-mapreduce-streaming-on-hadoop-in-hdinsight"></a><span data-ttu-id="4ae0d-103">Utilisation de C# avec Diffusion en continu MapReduce sur Hadoop dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="4ae0d-103">Use C# with MapReduce streaming on Hadoop in HDInsight</span></span>

<span data-ttu-id="4ae0d-104">Découvrez comment toouse c# toocreate une solution MapReduce dans HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4ae0d-104">Learn how toouse C# toocreate a MapReduce solution on HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4ae0d-105">Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="4ae0d-105">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="4ae0d-106">Pour plus d’informations, consultez [Contrôle de version des composants HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="4ae0d-106">For more information, see [HDInsight component versioning](hdinsight-component-versioning.md).</span></span>

<span data-ttu-id="4ae0d-107">Diffusion en continu Hadoop est un utilitaire qui vous permet des tâches MapReduce toorun à l’aide d’un script ou un exécutable.</span><span class="sxs-lookup"><span data-stu-id="4ae0d-107">Hadoop streaming is a utility that allows you toorun MapReduce jobs using a script or executable.</span></span> <span data-ttu-id="4ae0d-108">Dans cet exemple, .NET est utilisé tooimplement hello Mappeur et réducteur pour une solution de nombre de word.</span><span class="sxs-lookup"><span data-stu-id="4ae0d-108">In this example, .NET is used tooimplement hello mapper and reducer for a word count solution.</span></span>

## <a name="net-on-hdinsight"></a><span data-ttu-id="4ae0d-109">.NET sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="4ae0d-109">.NET on HDInsight</span></span>

<span data-ttu-id="4ae0d-110">__HDInsight de basés sur Linux__ utilisation des clusters [Mono (https://mono-project.com)](https://mono-project.com) toorun les applications .NET.</span><span class="sxs-lookup"><span data-stu-id="4ae0d-110">__Linux-based HDInsight__ clusters use [Mono (https://mono-project.com)](https://mono-project.com) toorun .NET applications.</span></span> <span data-ttu-id="4ae0d-111">La version 4.2.1 de Mono est incluse dans la version 3.5 de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4ae0d-111">Mono version 4.2.1 is included with HDInsight version 3.5.</span></span> <span data-ttu-id="4ae0d-112">Pour plus d’informations sur la version de hello de Mono inclus avec HDInsight, consultez [versions des composants HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="4ae0d-112">For more information on hello version of Mono included with HDInsight, see [HDInsight component versions](hdinsight-component-versioning.md).</span></span> <span data-ttu-id="4ae0d-113">toouse une version spécifique de Mono, consultez hello [installation ou mise à jour Mono](hdinsight-hadoop-install-mono.md) document.</span><span class="sxs-lookup"><span data-stu-id="4ae0d-113">toouse a specific version of Mono, see hello [Install or update Mono](hdinsight-hadoop-install-mono.md) document.</span></span>

<span data-ttu-id="4ae0d-114">Pour plus d’informations sur la compatibilité Mono avec les versions de .NET Framework, consultez [Compatibilité Mono](http://www.mono-project.com/docs/about-mono/compatibility/).</span><span class="sxs-lookup"><span data-stu-id="4ae0d-114">For more information on Mono compatibility with .NET Framework versions, see [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/).</span></span>

## <a name="how-hadoop-streaming-works"></a><span data-ttu-id="4ae0d-115">Fonctionnement de la diffusion en continu Hadoop</span><span class="sxs-lookup"><span data-stu-id="4ae0d-115">How Hadoop streaming works</span></span>

<span data-ttu-id="4ae0d-116">processus de base Hello utilisé pour la diffusion en continu dans ce document est la suivante :</span><span class="sxs-lookup"><span data-stu-id="4ae0d-116">hello basic process used for streaming in this document is as follows:</span></span>

1. <span data-ttu-id="4ae0d-117">Hadoop passe STDIN Mappeur des données de toohello (mapper.exe dans cet exemple).</span><span class="sxs-lookup"><span data-stu-id="4ae0d-117">Hadoop passes data toohello mapper (mapper.exe in this example) on STDIN.</span></span>
2. <span data-ttu-id="4ae0d-118">le Mappeur Hello traite les données de hello et émet tooSTDOUT de paires clé/valeur délimité par des tabulations.</span><span class="sxs-lookup"><span data-stu-id="4ae0d-118">hello mapper processes hello data, and emits tab-delimited key/value pairs tooSTDOUT.</span></span>
3. <span data-ttu-id="4ae0d-119">sortie de Hello est lu par Hadoop et puis transmise STDIN toohello réducteur (reducer.exe dans cet exemple).</span><span class="sxs-lookup"><span data-stu-id="4ae0d-119">hello output is read by Hadoop, and then passed toohello reducer (reducer.exe in this example) on STDIN.</span></span>
4. <span data-ttu-id="4ae0d-120">Réducteur de Hello lit les paires clé/valeur de hello délimité par des tabulations, traite les données de hello, puis émet les résultats hello sous forme de paires clé/valeur délimité par des tabulations dans STDOUT.</span><span class="sxs-lookup"><span data-stu-id="4ae0d-120">hello reducer reads hello tab-delimited key/value pairs, processes hello data, and then emits hello result as tab-delimited key/value pairs on STDOUT.</span></span>
5. <span data-ttu-id="4ae0d-121">sortie de Hello est lu par Hadoop et écrit le répertoire de sortie toohello.</span><span class="sxs-lookup"><span data-stu-id="4ae0d-121">hello output is read by Hadoop and written toohello output directory.</span></span>

<span data-ttu-id="4ae0d-122">Pour plus d’informations sur la diffusion en continu, consultez [Diffusion en continu Hadoop (https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html)](https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html).</span><span class="sxs-lookup"><span data-stu-id="4ae0d-122">For more information on streaming, see [Hadoop Streaming (https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html)](https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4ae0d-123">Composants requis</span><span class="sxs-lookup"><span data-stu-id="4ae0d-123">Prerequisites</span></span>

* <span data-ttu-id="4ae0d-124">Des connaissances en écriture et en génération de code C# qui cible .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="4ae0d-124">A familiarity with writing and building C# code that targets .NET Framework 4.5.</span></span> <span data-ttu-id="4ae0d-125">les étapes dans ce document utilisent Visual Studio 2017 Hello.</span><span class="sxs-lookup"><span data-stu-id="4ae0d-125">hello steps in this document use Visual Studio 2017.</span></span>

* <span data-ttu-id="4ae0d-126">Les fichiers d’une façon tooupload .exe toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="4ae0d-126">A way tooupload .exe files toohello cluster.</span></span> <span data-ttu-id="4ae0d-127">Hello étapes de ce document utilisent hello Data Lake Tools pour Visual Studio tooupload hello fichiers tooprimary stockage pour hello cluster.</span><span class="sxs-lookup"><span data-stu-id="4ae0d-127">hello steps in this document use hello Data Lake Tools for Visual Studio tooupload hello files tooprimary storage for hello cluster.</span></span>

* <span data-ttu-id="4ae0d-128">Azure PowerShell ou un client SSH.</span><span class="sxs-lookup"><span data-stu-id="4ae0d-128">Azure PowerShell or a SSH client.</span></span>

* <span data-ttu-id="4ae0d-129">Un cluster Hadoop sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4ae0d-129">A Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="4ae0d-130">Pour plus d’informations sur la création d’un cluster, consultez [Créer un cluster HDInsight](hdinsight-provision-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="4ae0d-130">For more information on creating a cluster, see [Create an HDInsight cluster](hdinsight-provision-clusters.md).</span></span>

## <a name="create-hello-mapper"></a><span data-ttu-id="4ae0d-131">Créer le mappeur de hello</span><span class="sxs-lookup"><span data-stu-id="4ae0d-131">Create hello mapper</span></span>

<span data-ttu-id="4ae0d-132">Dans Visual Studio, créez une nouvelle __Application console__ nommée __mappeur__.</span><span class="sxs-lookup"><span data-stu-id="4ae0d-132">In Visual Studio, create a new __Console application__ named __mapper__.</span></span> <span data-ttu-id="4ae0d-133">Utilisez hello suivant le code de l’application hello :</span><span class="sxs-lookup"><span data-stu-id="4ae0d-133">Use hello following code for hello application:</span></span>

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

<span data-ttu-id="4ae0d-134">Après avoir créé l’application hello, générez-le tooproduce hello `/bin/Debug/mapper.exe` fichier dans le répertoire du projet hello.</span><span class="sxs-lookup"><span data-stu-id="4ae0d-134">After creating hello application, build it tooproduce hello `/bin/Debug/mapper.exe` file in hello project directory.</span></span>

## <a name="create-hello-reducer"></a><span data-ttu-id="4ae0d-135">Créer le réducteur de hello</span><span class="sxs-lookup"><span data-stu-id="4ae0d-135">Create hello reducer</span></span>

<span data-ttu-id="4ae0d-136">Dans Visual Studio, créez une nouvelle __Application console__ nommée __raccord de réduction__.</span><span class="sxs-lookup"><span data-stu-id="4ae0d-136">In Visual Studio, create a new __Console application__ named __reducer__.</span></span> <span data-ttu-id="4ae0d-137">Utilisez hello suivant le code de l’application hello :</span><span class="sxs-lookup"><span data-stu-id="4ae0d-137">Use hello following code for hello application:</span></span>

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

<span data-ttu-id="4ae0d-138">Après avoir créé l’application hello, générez-le tooproduce hello `/bin/Debug/reducer.exe` fichier dans le répertoire du projet hello.</span><span class="sxs-lookup"><span data-stu-id="4ae0d-138">After creating hello application, build it tooproduce hello `/bin/Debug/reducer.exe` file in hello project directory.</span></span>

## <a name="upload-toostorage"></a><span data-ttu-id="4ae0d-139">Télécharger toostorage</span><span class="sxs-lookup"><span data-stu-id="4ae0d-139">Upload toostorage</span></span>

1. <span data-ttu-id="4ae0d-140">Dans Visual Studio, ouvrez l' **Explorateur de serveurs**.</span><span class="sxs-lookup"><span data-stu-id="4ae0d-140">In Visual Studio, open **Server Explorer**.</span></span>

2. <span data-ttu-id="4ae0d-141">Développez **Azure**, puis **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="4ae0d-141">Expand **Azure**, and then expand **HDInsight**.</span></span>

3. <span data-ttu-id="4ae0d-142">Si vous y êtes invité, entrez les informations d’identification de votre abonnement Azure, puis cliquez sur **Se connecter**.</span><span class="sxs-lookup"><span data-stu-id="4ae0d-142">If prompted, enter your Azure subscription credentials, and then click **Sign In**.</span></span>

4. <span data-ttu-id="4ae0d-143">Développez le cluster HDInsight hello que vous souhaitez toodeploy cette application.</span><span class="sxs-lookup"><span data-stu-id="4ae0d-143">Expand hello HDInsight cluster that you wish toodeploy this application to.</span></span> <span data-ttu-id="4ae0d-144">Une entrée avec texte hello __(compte de stockage par défaut)__ est répertorié.</span><span class="sxs-lookup"><span data-stu-id="4ae0d-144">An entry with hello text __(Default Storage Account)__ is listed.</span></span>

    ![Explorateur de serveurs avec le compte de stockage hello pour le cluster de hello](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/storage.png)

    * <span data-ttu-id="4ae0d-146">Si cette entrée peut être développée, vous utilisez un __compte de stockage Azure__ comme stockage par défaut pour le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="4ae0d-146">If this entry can be expanded, you are using an __Azure Storage Account__ as default storage for hello cluster.</span></span> <span data-ttu-id="4ae0d-147">fichiers hello tooview sur le stockage par défaut hello pour cluster de hello, développez l’entrée de hello et puis double-cliquez sur hello __(conteneur par défaut)__.</span><span class="sxs-lookup"><span data-stu-id="4ae0d-147">tooview hello files on hello default storage for hello cluster, expand hello entry and then double-click hello __(Default Container)__.</span></span>

    * <span data-ttu-id="4ae0d-148">Si cette entrée ne peut pas être développée, vous utilisez __Azure Data Lake Store__ comme du stockage par défaut pour le cluster de hello hello.</span><span class="sxs-lookup"><span data-stu-id="4ae0d-148">If this entry cannot be expanded, you are using __Azure Data Lake Store__ as hello default storage for hello cluster.</span></span> <span data-ttu-id="4ae0d-149">fichiers hello tooview sur le stockage par défaut hello pour cluster de hello, double-cliquez sur hello __(compte de stockage par défaut)__ entrée.</span><span class="sxs-lookup"><span data-stu-id="4ae0d-149">tooview hello files on hello default storage for hello cluster, double-click hello __(Default Storage Account)__ entry.</span></span>

5. <span data-ttu-id="4ae0d-150">fichiers .exe de hello tooupload, utilisez une des méthodes suivantes de hello :</span><span class="sxs-lookup"><span data-stu-id="4ae0d-150">tooupload hello .exe files, use one of hello following methods:</span></span>

    * <span data-ttu-id="4ae0d-151">Si vous utilisez un __compte de stockage Azure__, sur l’icône de téléchargement hello et puis parcourir toohello **bin\debug** dossier hello **Mappeur** projet.</span><span class="sxs-lookup"><span data-stu-id="4ae0d-151">If using an __Azure Storage Account__, click hello upload icon, and then browse toohello **bin\debug** folder for hello **mapper** project.</span></span> <span data-ttu-id="4ae0d-152">Enfin, sélectionnez hello **mapper.exe** de fichier et cliquez sur **Ok**.</span><span class="sxs-lookup"><span data-stu-id="4ae0d-152">Finally, select hello **mapper.exe** file and click **Ok**.</span></span>

        ![icône télécharger](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/upload.png)
    
    * <span data-ttu-id="4ae0d-154">Si vous utilisez __Azure Data Lake Store__, cliquez sur une zone vide dans la liste des fichiers hello, puis sélectionnez __télécharger__.</span><span class="sxs-lookup"><span data-stu-id="4ae0d-154">If using __Azure Data Lake Store__, right-click an empty area in hello file listing, and then select __Upload__.</span></span> <span data-ttu-id="4ae0d-155">Enfin, sélectionnez hello **mapper.exe** de fichier et cliquez sur **ouvrir**.</span><span class="sxs-lookup"><span data-stu-id="4ae0d-155">Finally, select hello **mapper.exe** file and click **Open**.</span></span>

    <span data-ttu-id="4ae0d-156">Une fois hello __mapper.exe__ téléchargement terminé, le processus de téléchargement hello Répétez ces étapes pour hello __reducer.exe__ fichier.</span><span class="sxs-lookup"><span data-stu-id="4ae0d-156">Once hello __mapper.exe__ upload has finished, repeat hello upload process for hello __reducer.exe__ file.</span></span>

## <a name="run-a-job-using-an-ssh-session"></a><span data-ttu-id="4ae0d-157">Exécution d’une tâche : avec une session SSH</span><span class="sxs-lookup"><span data-stu-id="4ae0d-157">Run a job: Using an SSH session</span></span>

1. <span data-ttu-id="4ae0d-158">Utiliser SSH tooconnect toohello HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="4ae0d-158">Use SSH tooconnect toohello HDInsight cluster.</span></span> <span data-ttu-id="4ae0d-159">Pour en savoir plus, voir [Utilisation de SSH avec Hadoop Linux sur HDInsight depuis Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="4ae0d-159">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="4ae0d-160">Utilisez une des hello suivant tâche MapReduce de commande toostart hello :</span><span class="sxs-lookup"><span data-stu-id="4ae0d-160">Use one of hello following command toostart hello MapReduce job:</span></span>

    * <span data-ttu-id="4ae0d-161">Si vous utilisez __Data Lake Store__ en tant que stockage par défaut :</span><span class="sxs-lookup"><span data-stu-id="4ae0d-161">If using __Data Lake Store__ as default storage:</span></span>

        ```bash
        yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files adl:///mapper.exe,adl:///reducer.exe -mapper mapper.exe -reducer reducer.exe -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
        ```
    
    * <span data-ttu-id="4ae0d-162">Si vous utilisez __Stockage Azure__ en tant que stockage par défaut :</span><span class="sxs-lookup"><span data-stu-id="4ae0d-162">If using __Azure Storage__ as default storage:</span></span>

        ```bash
        yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files wasb:///mapper.exe,wasb:///reducer.exe -mapper mapper.exe -reducer reducer.exe -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
        ```

    <span data-ttu-id="4ae0d-163">Hello suivant liste décrit ce que fait chaque paramètre :</span><span class="sxs-lookup"><span data-stu-id="4ae0d-163">hello following list describes what each parameter does:</span></span>

    * <span data-ttu-id="4ae0d-164">`hadoop-streaming.jar`: fichier jar hello contenant hello MapReduce fonctionnalité de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="4ae0d-164">`hadoop-streaming.jar`: hello jar file that contains hello streaming MapReduce functionality.</span></span>
    * <span data-ttu-id="4ae0d-165">`-files`: Ajoute hello `mapper.exe` et `reducer.exe` travail toothis des fichiers.</span><span class="sxs-lookup"><span data-stu-id="4ae0d-165">`-files`: Adds hello `mapper.exe` and `reducer.exe` files toothis job.</span></span> <span data-ttu-id="4ae0d-166">Hello `adl:///` ou `wasb:///` avant chaque fichier racine de toohello hello chemin d’accès de stockage par défaut pour le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="4ae0d-166">hello `adl:///` or `wasb:///` before each file is hello path toohello root of default storage for hello cluster.</span></span>
    * <span data-ttu-id="4ae0d-167">`-mapper`: Spécifie le fichier qui implémente le Mappeur hello.</span><span class="sxs-lookup"><span data-stu-id="4ae0d-167">`-mapper`: Specifies which file implements hello mapper.</span></span>
    * <span data-ttu-id="4ae0d-168">`-reducer`: Spécifie le fichier qui implémente le réducteur de hello.</span><span class="sxs-lookup"><span data-stu-id="4ae0d-168">`-reducer`: Specifies which file implements hello reducer.</span></span>
    * <span data-ttu-id="4ae0d-169">`-input`: hello les données d’entrée.</span><span class="sxs-lookup"><span data-stu-id="4ae0d-169">`-input`: hello input data.</span></span>
    * <span data-ttu-id="4ae0d-170">`-output`: répertoire de sortie hello.</span><span class="sxs-lookup"><span data-stu-id="4ae0d-170">`-output`: hello output directory.</span></span>

3. <span data-ttu-id="4ae0d-171">Une fois la tâche MapReduce de hello est terminée, utilisez hello suivant des résultats de hello tooview :</span><span class="sxs-lookup"><span data-stu-id="4ae0d-171">Once hello MapReduce job completes, use hello following tooview hello results:</span></span>

    ```bash
    hdfs dfs -text /example/wordcountout/part-00000
    ```

    <span data-ttu-id="4ae0d-172">Hello texte suivant est un exemple de données hello retournés par cette commande :</span><span class="sxs-lookup"><span data-stu-id="4ae0d-172">hello following text is an example of hello data returned by this command:</span></span>

        you     1128
        young   38
        younger 1
        youngest        1
        your    338
        yours   4
        yourself        34
        yourselves      3
        youth   17

## <a name="run-a-job-using-powershell"></a><span data-ttu-id="4ae0d-173">Exécution d’une tâche : avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="4ae0d-173">Run a job: Using PowerShell</span></span>

<span data-ttu-id="4ae0d-174">Utilisez hello suivant toorun de script PowerShell une tâche MapReduce et télécharger les résultats de hello.</span><span class="sxs-lookup"><span data-stu-id="4ae0d-174">Use hello following PowerShell script toorun a MapReduce job and download hello results.</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/use-csharp-mapreduce/use-csharp-mapreduce.ps1?range=5-87)]

<span data-ttu-id="4ae0d-175">Ce script vous invite pour le nom de compte de connexion de cluster hello et le mot de passe, ainsi que le nom du cluster HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="4ae0d-175">This script prompts you for hello cluster login account name and password, along with hello HDInsight cluster name.</span></span> <span data-ttu-id="4ae0d-176">Une fois que hello est terminée, sortie de hello est téléchargé toohello `output.txt` fichier de script de hello directory hello est exécuté à partir de.</span><span class="sxs-lookup"><span data-stu-id="4ae0d-176">Once hello job completes, hello output is downloaded toohello `output.txt` file in hello directory hello script is ran from.</span></span> <span data-ttu-id="4ae0d-177">Bonjour texte suivant est un exemple de données hello Bonjour `output.txt` fichier :</span><span class="sxs-lookup"><span data-stu-id="4ae0d-177">hello following text is an example of hello data in hello `output.txt` file:</span></span>

    you     1128
    young   38
    younger 1
    youngest        1
    your    338
    yours   4
    yourself        34
    yourselves      3
    youth   17

## <a name="next-steps"></a><span data-ttu-id="4ae0d-178">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4ae0d-178">Next steps</span></span>

<span data-ttu-id="4ae0d-179">Pour plus d’informations sur l’utilisation de MapReduce avec HDInsight, consultez [Utilisation de MapReduce avec HDInsight](hdinsight-use-mapreduce.md).</span><span class="sxs-lookup"><span data-stu-id="4ae0d-179">For more information on using MapReduce with HDInsight, see [Use MapReduce with HDInsight](hdinsight-use-mapreduce.md).</span></span>

<span data-ttu-id="4ae0d-180">Pour plus d’informations sur l’utilisation de C# avec Hive et Pig, consultez [Utilisation d’une fonction définie par l’utilisateur C# avec Hive et Pig](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="4ae0d-180">For information on using C# with Hive and Pig, see [Use a C# user defined function with Hive and Pig](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md).</span></span>

<span data-ttu-id="4ae0d-181">Pour plus d’informations sur l’utilisation de C# avec Storm sur HDInsight, consultez [Développement de topologies C# pour Storm sur HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="4ae0d-181">For information on using C# with Storm on HDInsight, see [Develop C# topologies for Storm on HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>