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
# <a name="use-c-user-defined-functions-with-hive-and-pig-streaming-on-hadoop-in-hdinsight"></a><span data-ttu-id="c345d-103">Utilisation des fonctions définies par l’utilisateur C# avec la diffusion en continu Hive et Pig dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="c345d-103">Use C# user-defined functions with Hive and Pig streaming on Hadoop in HDInsight</span></span>

<span data-ttu-id="c345d-104">Découvrez comment toouse c# défini par l’utilisateur (UDF) de fonctions avec Apache Hive et Pig dans HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c345d-104">Learn how toouse C# user defined functions (UDF) with Apache Hive and Pig on HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c345d-105">étapes de Hello dans ce document fonctionnent avec des clusters HDInsight à la fois basés sur Linux et Windows.</span><span class="sxs-lookup"><span data-stu-id="c345d-105">hello steps in this document work with both Linux-based and Windows-based HDInsight clusters.</span></span> <span data-ttu-id="c345d-106">Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="c345d-106">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="c345d-107">Pour plus d’informations, consultez [Contrôle de version des composants HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="c345d-107">For more information, see [HDInsight component versioning](hdinsight-component-versioning.md).</span></span>

<span data-ttu-id="c345d-108">Les deux Hive et Pig peut passer des applications tooexternal de données pour le traitement.</span><span class="sxs-lookup"><span data-stu-id="c345d-108">Both Hive and Pig can pass data tooexternal applications for processing.</span></span> <span data-ttu-id="c345d-109">Ce processus est appelé _diffusion en continu (streaming)_.</span><span class="sxs-lookup"><span data-stu-id="c345d-109">This process is known as _streaming_.</span></span> <span data-ttu-id="c345d-110">Lorsque vous utilisez une application .NET, les données hello sont transmises toohello application STDIN et application hello retourne les résultats hello dans STDOUT.</span><span class="sxs-lookup"><span data-stu-id="c345d-110">When using a .NET applciation, hello data is passed toohello application on STDIN, and hello application returns hello results on STDOUT.</span></span> <span data-ttu-id="c345d-111">tooread et en écriture à partir de STDIN et STDOUT, vous pouvez utiliser `Console.ReadLine()` et `Console.WriteLine()` à partir d’une application console.</span><span class="sxs-lookup"><span data-stu-id="c345d-111">tooread and write from STDIN and STDOUT, you can use `Console.ReadLine()` and `Console.WriteLine()` from a console application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c345d-112">Composants requis</span><span class="sxs-lookup"><span data-stu-id="c345d-112">Prerequisites</span></span>

* <span data-ttu-id="c345d-113">Des connaissances en écriture et en génération de code C# qui cible .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="c345d-113">A familiarity with writing and building C# code that targets .NET Framework 4.5.</span></span>

    * <span data-ttu-id="c345d-114">Utilisez n’importe quel IDE souhaité.</span><span class="sxs-lookup"><span data-stu-id="c345d-114">Use whatever IDE you want.</span></span> <span data-ttu-id="c345d-115">Nous vous conseillons d’utiliser [Visual Studio](https://www.visualstudio.com/vs) 2015, 2017 ou [Visual Studio Code](https://code.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="c345d-115">We recommend [Visual Studio](https://www.visualstudio.com/vs) 2015, 2017, or [Visual Studio Code](https://code.visualstudio.com/).</span></span> <span data-ttu-id="c345d-116">les étapes dans ce document utilisent Visual Studio 2017 Hello.</span><span class="sxs-lookup"><span data-stu-id="c345d-116">hello steps in this document use Visual Studio 2017.</span></span>

* <span data-ttu-id="c345d-117">Les fichiers d’une façon tooupload .exe toohello cluster et l’exécution des travaux Pig et Hive.</span><span class="sxs-lookup"><span data-stu-id="c345d-117">A way tooupload .exe files toohello cluster and run Pig and Hive jobs.</span></span> <span data-ttu-id="c345d-118">Nous vous recommandons hello Data Lake Tools pour Visual Studio, Azure PowerShell et CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="c345d-118">We recommend hello Data Lake Tools for Visual Studio, Azure PowerShell and Azure CLI.</span></span> <span data-ttu-id="c345d-119">Hello étapes de ce document utilisent hello Data Lake Tools pour les fichiers de Visual Studio tooupload hello et exécuter la requête de Hive exemple hello.</span><span class="sxs-lookup"><span data-stu-id="c345d-119">hello steps in this document use hello Data Lake Tools for Visual Studio tooupload hello files and run hello example Hive query.</span></span>

    <span data-ttu-id="c345d-120">Pour plus d’informations sur d’autres requêtes de façons toorun Hive et les travaux de Pig, consultez hello suivant des documents :</span><span class="sxs-lookup"><span data-stu-id="c345d-120">For information on other ways toorun Hive queries and Pig jobs, see hello following documents:</span></span>

    * [<span data-ttu-id="c345d-121">Utilisation d’Apache Hive avec HDInsight</span><span class="sxs-lookup"><span data-stu-id="c345d-121">Use Apache Hive with HDInsight</span></span>](hdinsight-use-hive.md)

    * [<span data-ttu-id="c345d-122">Utilisation d’Apache Pig avec HDInsight</span><span class="sxs-lookup"><span data-stu-id="c345d-122">Use Apache Pig with HDInsight</span></span>](hdinsight-use-pig.md)

* <span data-ttu-id="c345d-123">Un cluster Hadoop sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c345d-123">A Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="c345d-124">Pour plus d’informations sur la création d’un cluster, consultez [Créer un cluster HDInsight](hdinsight-provision-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="c345d-124">For more information on creating a cluster, see [Create an HDInsight cluster](hdinsight-provision-clusters.md).</span></span>

## <a name="net-on-hdinsight"></a><span data-ttu-id="c345d-125">.NET sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="c345d-125">.NET on HDInsight</span></span>

* <span data-ttu-id="c345d-126">__HDInsight de basés sur Linux__ à l’aide de clusters [Mono (https://mono-project.com)](https://mono-project.com) toorun les applications .NET.</span><span class="sxs-lookup"><span data-stu-id="c345d-126">__Linux-based HDInsight__ clusters using [Mono (https://mono-project.com)](https://mono-project.com) toorun .NET applications.</span></span> <span data-ttu-id="c345d-127">La version 4.2.1 de Mono est incluse dans la version 3.5 de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c345d-127">Mono version 4.2.1 is included with HDInsight version 3.5.</span></span>

    <span data-ttu-id="c345d-128">Pour plus d’informations sur la compatibilité Mono avec les versions de .NET Framework, consultez [Compatibilité Mono](http://www.mono-project.com/docs/about-mono/compatibility/).</span><span class="sxs-lookup"><span data-stu-id="c345d-128">For more information on Mono compatibility with .NET Framework versions, see [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/).</span></span>

    <span data-ttu-id="c345d-129">toouse une version spécifique de Mono, consultez hello [installation ou mise à jour Mono](hdinsight-hadoop-install-mono.md) document.</span><span class="sxs-lookup"><span data-stu-id="c345d-129">toouse a specific version of Mono, see hello [Install or update Mono](hdinsight-hadoop-install-mono.md) document.</span></span>

* <span data-ttu-id="c345d-130">__HDInsight de basés sur Windows__ clusters utilisent les applications de .NET toorun hello CLR .NET de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="c345d-130">__Windows-based HDInsight__ clusters use hello Microsoft .NET CLR toorun .NET applications.</span></span>

<span data-ttu-id="c345d-131">Pour plus d’informations sur la version de hello de hello .NET framework et de Mono fournie avec les versions HDInsight, consultez [versions des composants HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="c345d-131">For more information on hello version of hello .NET framework and Mono included with HDInsight versions, see [HDInsight component versions](hdinsight-component-versioning.md).</span></span>

## <a name="create-hello-c-projects"></a><span data-ttu-id="c345d-132">Créer hello C\# projets</span><span class="sxs-lookup"><span data-stu-id="c345d-132">Create hello C\# projects</span></span>

### <a name="hive-udf"></a><span data-ttu-id="c345d-133">UDF Hive</span><span class="sxs-lookup"><span data-stu-id="c345d-133">Hive UDF</span></span>

1. <span data-ttu-id="c345d-134">Ouvrez Visual Studio et créez une solution.</span><span class="sxs-lookup"><span data-stu-id="c345d-134">Open Visual Studio and create a solution.</span></span> <span data-ttu-id="c345d-135">Pour le type de projet hello, sélectionnez **l’application Console (.NET Framework)**et un nouveau projet de nom hello **HiveCSharp**.</span><span class="sxs-lookup"><span data-stu-id="c345d-135">For hello project type, select **Console App (.NET Framework)**, and name hello new project **HiveCSharp**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="c345d-136">Si vous utilisez un cluster HDInsight sous Linux, sélectionnez __.NET Framework 4.5__.</span><span class="sxs-lookup"><span data-stu-id="c345d-136">Select __.NET Framework 4.5__ if you are using a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="c345d-137">Pour plus d’informations sur la compatibilité Mono avec les versions de .NET Framework, consultez [Compatibilité Mono](http://www.mono-project.com/docs/about-mono/compatibility/).</span><span class="sxs-lookup"><span data-stu-id="c345d-137">For more information on Mono compatibility with .NET Framework versions, see [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/).</span></span>

2. <span data-ttu-id="c345d-138">Remplacez le contenu hello de **Program.cs** avec les éléments suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="c345d-138">Replace hello contents of **Program.cs** with hello following:</span></span>

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

3. <span data-ttu-id="c345d-139">Générez le projet de hello.</span><span class="sxs-lookup"><span data-stu-id="c345d-139">Build hello project.</span></span>

### <a name="pig-udf"></a><span data-ttu-id="c345d-140">UDF Pig</span><span class="sxs-lookup"><span data-stu-id="c345d-140">Pig UDF</span></span>

1. <span data-ttu-id="c345d-141">Ouvrez Visual Studio et créez une solution.</span><span class="sxs-lookup"><span data-stu-id="c345d-141">Open Visual Studio and create a solution.</span></span> <span data-ttu-id="c345d-142">Pour le type de projet hello, sélectionnez **Application Console**et un nouveau projet de nom hello **PigUDF**.</span><span class="sxs-lookup"><span data-stu-id="c345d-142">For hello project type, select **Console Application**, and name hello new project **PigUDF**.</span></span>

2. <span data-ttu-id="c345d-143">Remplacez le contenu hello Hello **Program.cs** fichier avec hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="c345d-143">Replace hello contents of hello **Program.cs** file with hello following code:</span></span>

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

    <span data-ttu-id="c345d-144">Cette application traite les lignes hello envoyés à partir de Pig et remise en forme les lignes qui commencent par `java.lang.Exception`.</span><span class="sxs-lookup"><span data-stu-id="c345d-144">This application parses hello lines sent from Pig, and reformat lines that begin with `java.lang.Exception`.</span></span>

3. <span data-ttu-id="c345d-145">Enregistrer **Program.cs**, puis générez le projet de hello.</span><span class="sxs-lookup"><span data-stu-id="c345d-145">Save **Program.cs**, and then build hello project.</span></span>

## <a name="upload-toostorage"></a><span data-ttu-id="c345d-146">Télécharger toostorage</span><span class="sxs-lookup"><span data-stu-id="c345d-146">Upload toostorage</span></span>

1. <span data-ttu-id="c345d-147">Dans Visual Studio, ouvrez l' **Explorateur de serveurs**.</span><span class="sxs-lookup"><span data-stu-id="c345d-147">In Visual Studio, open **Server Explorer**.</span></span>

2. <span data-ttu-id="c345d-148">Développez **Azure**, puis **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="c345d-148">Expand **Azure**, and then expand **HDInsight**.</span></span>

3. <span data-ttu-id="c345d-149">Si vous y êtes invité, entrez les informations d’identification de votre abonnement Azure, puis cliquez sur **Se connecter**.</span><span class="sxs-lookup"><span data-stu-id="c345d-149">If prompted, enter your Azure subscription credentials, and then click **Sign In**.</span></span>

4. <span data-ttu-id="c345d-150">Développez le cluster HDInsight hello que vous souhaitez toodeploy cette application.</span><span class="sxs-lookup"><span data-stu-id="c345d-150">Expand hello HDInsight cluster that you wish toodeploy this application to.</span></span> <span data-ttu-id="c345d-151">Une entrée avec texte hello __(compte de stockage par défaut)__ est répertorié.</span><span class="sxs-lookup"><span data-stu-id="c345d-151">An entry with hello text __(Default Storage Account)__ is listed.</span></span>

    ![Explorateur de serveurs avec le compte de stockage hello pour le cluster de hello](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/storage.png)

    * <span data-ttu-id="c345d-153">Si cette entrée peut être développée, vous utilisez un __compte de stockage Azure__ comme stockage par défaut pour le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="c345d-153">If this entry can be expanded, you are using an __Azure Storage Account__ as default storage for hello cluster.</span></span> <span data-ttu-id="c345d-154">fichiers hello tooview sur le stockage par défaut hello pour cluster de hello, développez l’entrée de hello et puis double-cliquez sur hello __(conteneur par défaut)__.</span><span class="sxs-lookup"><span data-stu-id="c345d-154">tooview hello files on hello default storage for hello cluster, expand hello entry and then double-click hello __(Default Container)__.</span></span>

    * <span data-ttu-id="c345d-155">Si cette entrée ne peut pas être développée, vous utilisez __Azure Data Lake Store__ comme du stockage par défaut pour le cluster de hello hello.</span><span class="sxs-lookup"><span data-stu-id="c345d-155">If this entry cannot be expanded, you are using __Azure Data Lake Store__ as hello default storage for hello cluster.</span></span> <span data-ttu-id="c345d-156">fichiers hello tooview sur le stockage par défaut hello pour cluster de hello, double-cliquez sur hello __(compte de stockage par défaut)__ entrée.</span><span class="sxs-lookup"><span data-stu-id="c345d-156">tooview hello files on hello default storage for hello cluster, double-click hello __(Default Storage Account)__ entry.</span></span>

6. <span data-ttu-id="c345d-157">fichiers .exe de hello tooupload, utilisez une des méthodes suivantes de hello :</span><span class="sxs-lookup"><span data-stu-id="c345d-157">tooupload hello .exe files, use one of hello following methods:</span></span>

    * <span data-ttu-id="c345d-158">Si vous utilisez un __compte de stockage Azure__, sur l’icône de téléchargement hello et puis parcourir toohello **bin\debug** dossier hello **HiveCSharp** projet.</span><span class="sxs-lookup"><span data-stu-id="c345d-158">If using an __Azure Storage Account__, click hello upload icon, and then browse toohello **bin\debug** folder for hello **HiveCSharp** project.</span></span> <span data-ttu-id="c345d-159">Enfin, sélectionnez hello **HiveCSharp.exe** de fichier et cliquez sur **Ok**.</span><span class="sxs-lookup"><span data-stu-id="c345d-159">Finally, select hello **HiveCSharp.exe** file and click **Ok**.</span></span>

        ![icône télécharger](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/upload.png)
    
    * <span data-ttu-id="c345d-161">Si vous utilisez __Azure Data Lake Store__, cliquez sur une zone vide dans la liste des fichiers hello, puis sélectionnez __télécharger__.</span><span class="sxs-lookup"><span data-stu-id="c345d-161">If using __Azure Data Lake Store__, right-click an empty area in hello file listing, and then select __Upload__.</span></span> <span data-ttu-id="c345d-162">Enfin, sélectionnez hello **HiveCSharp.exe** de fichier et cliquez sur **ouvrir**.</span><span class="sxs-lookup"><span data-stu-id="c345d-162">Finally, select hello **HiveCSharp.exe** file and click **Open**.</span></span>

    <span data-ttu-id="c345d-163">Une fois hello __HiveCSharp.exe__ téléchargement terminé, le processus de téléchargement hello Répétez ces étapes pour hello __PigUDF.exe__ fichier.</span><span class="sxs-lookup"><span data-stu-id="c345d-163">Once hello __HiveCSharp.exe__ upload has finished, repeat hello upload process for hello __PigUDF.exe__ file.</span></span>

## <a name="run-a-hive-query"></a><span data-ttu-id="c345d-164">Exécution d'une tâche Hive</span><span class="sxs-lookup"><span data-stu-id="c345d-164">Run a Hive query</span></span>

1. <span data-ttu-id="c345d-165">Dans Visual Studio, ouvrez l' **Explorateur de serveurs**.</span><span class="sxs-lookup"><span data-stu-id="c345d-165">In Visual Studio, open **Server Explorer**.</span></span>

2. <span data-ttu-id="c345d-166">Développez **Azure**, puis **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="c345d-166">Expand **Azure**, and then expand **HDInsight**.</span></span>

3. <span data-ttu-id="c345d-167">Cluster de hello avec le bouton que vous avez déployé hello **HiveCSharp** application et sélectionnez **écrire une requête Hive**.</span><span class="sxs-lookup"><span data-stu-id="c345d-167">Right-click hello cluster that you deployed hello **HiveCSharp** application to, and then select **Write a Hive Query**.</span></span>

4. <span data-ttu-id="c345d-168">Utilisez hello après le texte de la requête de ruche hello :</span><span class="sxs-lookup"><span data-stu-id="c345d-168">Use hello following text for hello Hive query:</span></span>

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
    > <span data-ttu-id="c345d-169">Supprimez les commentaires hello `add file` instruction qui correspond au type hello de stockage par défaut utilisés pour votre cluster.</span><span class="sxs-lookup"><span data-stu-id="c345d-169">Uncomment hello `add file` statement that matches hello type of default storage used for your cluster.</span></span>

    <span data-ttu-id="c345d-170">Cette requête sélectionne hello `clientid`, `devicemake`, et `devicemodel` des champs `hivesampletable`et transmet les champs hello toohello HiveCSharp.exe application.</span><span class="sxs-lookup"><span data-stu-id="c345d-170">This query selects hello `clientid`, `devicemake`, and `devicemodel` fields from `hivesampletable`, and passes hello fields toohello HiveCSharp.exe application.</span></span> <span data-ttu-id="c345d-171">requête de Hello attend hello tooreturn trois champs de l’application, qui sont stockées en tant que `clientid`, `phoneLabel`, et `phoneHash`.</span><span class="sxs-lookup"><span data-stu-id="c345d-171">hello query expects hello application tooreturn three fields, which are stored as `clientid`, `phoneLabel`, and `phoneHash`.</span></span> <span data-ttu-id="c345d-172">requête de Hello attend également toofind HiveCSharp.exe racine hello hello par défaut du conteneur de stockage.</span><span class="sxs-lookup"><span data-stu-id="c345d-172">hello query also expects toofind HiveCSharp.exe in hello root of hello default storage container.</span></span>

5. <span data-ttu-id="c345d-173">Cliquez sur **Submit** le cluster HDInsight toohello toosubmit hello travail.</span><span class="sxs-lookup"><span data-stu-id="c345d-173">Click **Submit** toosubmit hello job toohello HDInsight cluster.</span></span> <span data-ttu-id="c345d-174">Hello **récapitulatif de la ruche** fenêtre s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="c345d-174">hello **Hive Job Summary** window opens.</span></span>

6. <span data-ttu-id="c345d-175">Cliquez sur **Actualiser** hello toorefresh synthèse jusqu'à **état du travail** change également**terminé**.</span><span class="sxs-lookup"><span data-stu-id="c345d-175">Click **Refresh** toorefresh hello summary until **Job Status** changes too**Completed**.</span></span> <span data-ttu-id="c345d-176">sortie de la tâche de hello tooview, cliquez sur **sortie de travail**.</span><span class="sxs-lookup"><span data-stu-id="c345d-176">tooview hello job output, click **Job Output**.</span></span>

## <a name="run-a-pig-job"></a><span data-ttu-id="c345d-177">Exécution d’une tâche Pig</span><span class="sxs-lookup"><span data-stu-id="c345d-177">Run a Pig job</span></span>

1. <span data-ttu-id="c345d-178">Utilisez une des hello suivant du cluster HDInsight de méthodes tooconnect tooyour :</span><span class="sxs-lookup"><span data-stu-id="c345d-178">Use one of hello following methods tooconnect tooyour HDInsight cluster:</span></span>

    * <span data-ttu-id="c345d-179">Si vous utilisez un cluster HDInsight __sous Linux__, utilisez SSH.</span><span class="sxs-lookup"><span data-stu-id="c345d-179">If you are using a __Linux-based__ HDInsight cluster, use SSH.</span></span> <span data-ttu-id="c345d-180">Par exemple, `ssh sshuser@mycluster-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="c345d-180">For example, `ssh sshuser@mycluster-ssh.azurehdinsight.net`.</span></span> <span data-ttu-id="c345d-181">Pour plus d’informations, consultez la rubrique [Utilisation de SSH avec HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)</span><span class="sxs-lookup"><span data-stu-id="c345d-181">For more information, see [Use SSH withHDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>
    
    * <span data-ttu-id="c345d-182">Si vous utilisez un __basé sur Windows__ cluster HDInsight, [cluster toohello de se connecter à l’aide du Bureau à distance](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)</span><span class="sxs-lookup"><span data-stu-id="c345d-182">If you are using a __Windows-based__ HDInsight cluster, [Connect toohello cluster using Remote Desktop](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)</span></span>

2. <span data-ttu-id="c345d-183">Utilisez une hello ligne de commande commande toostart hello Pig :</span><span class="sxs-lookup"><span data-stu-id="c345d-183">Use one hello following command toostart hello Pig command line:</span></span>

        pig

    > [!IMPORTANT]
    > <span data-ttu-id="c345d-184">Si vous utilisez un cluster Windows, utilisez hello suivant à la place les commandes :</span><span class="sxs-lookup"><span data-stu-id="c345d-184">If you are using a Windows-based cluster, use hello following commands instead:</span></span>
    > ```
    > cd %PIG_HOME%
    > bin\pig
    > ```

    <span data-ttu-id="c345d-185">Une invite `grunt>` s’affiche.</span><span class="sxs-lookup"><span data-stu-id="c345d-185">A `grunt>` prompt is displayed.</span></span>

3. <span data-ttu-id="c345d-186">Entrez hello suivant toorun un travail Pig qui utilise l’application de .NET Framework hello :</span><span class="sxs-lookup"><span data-stu-id="c345d-186">Enter hello following toorun a Pig job that uses hello .NET Framework application:</span></span>

        DEFINE streamer `PigUDF.exe` CACHE('/PigUDF.exe');
        LOGS = LOAD '/example/data/sample.log' as (LINE:chararray);
        LOG = FILTER LOGS by LINE is not null;
        DETAILS = STREAM LOG through streamer as (col1, col2, col3, col4, col5);
        DUMP DETAILS;

    <span data-ttu-id="c345d-187">Hello `DEFINE` instruction crée un alias de `streamer` pour les applications pigudf.exe hello, et `CACHE` charge à partir de stockage par défaut pour le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="c345d-187">hello `DEFINE` statement creates an alias of `streamer` for hello pigudf.exe applications, and `CACHE` loads it from default storage for hello cluster.</span></span> <span data-ttu-id="c345d-188">Une version ultérieure, `streamer` est utilisé avec hello `STREAM` opérateur tooprocess hello lignes uniques contenus dans les journaux et de données de retour hello sous la forme d’une série de colonnes.</span><span class="sxs-lookup"><span data-stu-id="c345d-188">Later, `streamer` is used with hello `STREAM` operator tooprocess hello single lines contained in LOG and return hello data as a series of columns.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c345d-189">nom de l’application Hello qui est utilisé pour la diffusion en continu doit être entouré de hello \` (backtick) de caractères quand un alias, et ' (apostrophe) lorsqu’il est utilisé avec `SHIP\`.</span><span class="sxs-lookup"><span data-stu-id="c345d-189">hello application name that is used for streaming must be surrounded by hello \` (backtick) character when aliased, and ' (single quote) when used with `SHIP\`.</span></span>

4. <span data-ttu-id="c345d-190">Après avoir entré la dernière ligne de hello, hello doit démarrer.</span><span class="sxs-lookup"><span data-stu-id="c345d-190">After entering hello last line, hello job should start.</span></span> <span data-ttu-id="c345d-191">Il retourne toohello similaire de sortie suivant du texte :</span><span class="sxs-lookup"><span data-stu-id="c345d-191">It returns output similar toohello following text:</span></span>

        (2012-02-03 20:11:56 SampleClass5 [WARN] problem finding id 1358451042 - java.lang.Exception)
        (2012-02-03 20:11:56 SampleClass5 [DEBUG] detail for id 1976092771)
        (2012-02-03 20:11:56 SampleClass5 [TRACE] verbose detail for id 1317358561)
        (2012-02-03 20:11:56 SampleClass5 [TRACE] verbose detail for id 1737534798)
        (2012-02-03 20:11:56 SampleClass7 [DEBUG] detail for id 1475865947)

## <a name="next-steps"></a><span data-ttu-id="c345d-192">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c345d-192">Next steps</span></span>

<span data-ttu-id="c345d-193">Dans ce document, vous avez appris comment toouse une application .NET Framework à partir de Hive et Pig dans HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c345d-193">In this document, you have learned how toouse a .NET Framework application from Hive and Pig on HDInsight.</span></span> <span data-ttu-id="c345d-194">Si vous souhaitez que toolearn toouse Python avec Hive et Pig, voir [utilisation de Python avec Hive et Pig dans HDInsight](hdinsight-python.md).</span><span class="sxs-lookup"><span data-stu-id="c345d-194">If you would like toolearn how toouse Python with Hive and Pig, see [Use Python with Hive and Pig in HDInsight](hdinsight-python.md).</span></span>

<span data-ttu-id="c345d-195">Pour les autres façons toouse Pig et Hive et toolearn sur l’utilisation de MapReduce, consultez hello suivant des documents :</span><span class="sxs-lookup"><span data-stu-id="c345d-195">For other ways toouse Pig and Hive, and toolearn about using MapReduce, see hello following documents:</span></span>

* [<span data-ttu-id="c345d-196">Utilisation de Hive avec HDInsight</span><span class="sxs-lookup"><span data-stu-id="c345d-196">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="c345d-197">Utilisation de Pig avec HDInsight</span><span class="sxs-lookup"><span data-stu-id="c345d-197">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="c345d-198">Utilisation de MapReduce avec HDInsight</span><span class="sxs-lookup"><span data-stu-id="c345d-198">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)
