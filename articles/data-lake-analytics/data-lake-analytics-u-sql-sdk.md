---
title: "Mettre à l’échelle l’exécution et les tests U-SQL locaux avec le kit SDK Azure Data Lake U-SQL | Microsoft Docs"
description: "Découvrez comment utiliser le Kit SDK Azure Data Lake U-SQL pour mettre à l’échelle l’exécution et les tests locaux de travaux U-SQL avec les interfaces de ligne de commande et de programmation de votre station de travail locale."
services: data-lake-analytics
documentationcenter: 
author: 
manager: 
editor: 
ms.assetid: 
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/01/2017
ms.author: yanacai
ms.openlocfilehash: 55242bcf644ca0e7f30cfe7eada2130451c36e64
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="scale-u-sql-local-run-and-test-with-azure-data-lake-u-sql-sdk"></a><span data-ttu-id="4d867-103">Mettre à l’échelle l’exécution et les tests U-SQL locaux avec le kit SDK Azure Data Lake U-SQL</span><span class="sxs-lookup"><span data-stu-id="4d867-103">Scale U-SQL local run and test with Azure Data Lake U-SQL SDK</span></span>

<span data-ttu-id="4d867-104">Lorsque vous développez un script U-SQL, il est courant de l’exécuter et de le tester localement avant de l’envoyer dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="4d867-104">When developing U-SQL script, it is common to run and test U-SQL script locally before submit it to cloud.</span></span> <span data-ttu-id="4d867-105">Azure Data Lake fournit un package NuGet appelé Kit SDK SQL Azure Data Lake U-SQL pour ce scénario, par le biais duquel vous pouvez facilement mettre à l’échelle l’exécution et les tests U-SQL locaux.</span><span class="sxs-lookup"><span data-stu-id="4d867-105">Azure Data Lake provides a Nuget package called Azure Data Lake U-SQL SDK for this scenario, through which you can easily scale U-SQL local run and test.</span></span> <span data-ttu-id="4d867-106">Il est également possible d’intégrer ce test U-SQL avec le système CI (intégration continue) pour automatiser la compilation et les tests.</span><span class="sxs-lookup"><span data-stu-id="4d867-106">It is also possible to integrate this U-SQL test with CI (Continuous Integration) system to automate the compile and test.</span></span>

<span data-ttu-id="4d867-107">Si vous vous demandez comment exécuter et déboguer un script U-SQL localement et manuellement avec les outils de GUI, vous pouvez pour cela utiliser Azure Data Lake Tools pour Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4d867-107">If you care about how to manually local run and debug U-SQL script with GUI tooling, then you can use Azure Data Lake Tools for Visual Studio for that.</span></span> <span data-ttu-id="4d867-108">Pour plus d’informations, cliquez [ici](data-lake-analytics-data-lake-tools-local-run.md).</span><span class="sxs-lookup"><span data-stu-id="4d867-108">You can learn more from [here](data-lake-analytics-data-lake-tools-local-run.md).</span></span>

## <a name="install-azure-data-lake-u-sql-sdk"></a><span data-ttu-id="4d867-109">Installer le Kit SDK Azure Data Lake U-SQL</span><span class="sxs-lookup"><span data-stu-id="4d867-109">Install Azure Data Lake U-SQL SDK</span></span>

<span data-ttu-id="4d867-110">Vous pouvez obtenir le Kit SDK Azure Data Lake U-SQL [ici](https://www.nuget.org/packages/Microsoft.Azure.DataLake.USQL.SDK/) sur Nuget.org.</span><span class="sxs-lookup"><span data-stu-id="4d867-110">You can get the Azure Data Lake U-SQL SDK [here](https://www.nuget.org/packages/Microsoft.Azure.DataLake.USQL.SDK/) on Nuget.org.</span></span> <span data-ttu-id="4d867-111">Avant de l’utiliser, vous devez vérifier que vous disposez des dépendances suivantes.</span><span class="sxs-lookup"><span data-stu-id="4d867-111">And before using it, you need to make sure you have dependencies as follows.</span></span>

### <a name="dependencies"></a><span data-ttu-id="4d867-112">Dépendances</span><span class="sxs-lookup"><span data-stu-id="4d867-112">Dependencies</span></span>

<span data-ttu-id="4d867-113">Le kit SDK U-SQL Data Lake requiert les dépendances suivantes :</span><span class="sxs-lookup"><span data-stu-id="4d867-113">The Data Lake U-SQL SDK requires the following dependencies:</span></span>

- <span data-ttu-id="4d867-114">[Microsoft .NET Framework 4.6 ou une version ultérieure](https://www.microsoft.com/download/details.aspx?id=17851).</span><span class="sxs-lookup"><span data-stu-id="4d867-114">[Microsoft .NET Framework 4.6 or newer](https://www.microsoft.com/download/details.aspx?id=17851).</span></span>
- <span data-ttu-id="4d867-115">Microsoft Visual C++ 14 et le Kit SDK Windows 10.0.10240.0 ou une version plus récente (appelé CppSDK dans cet article).</span><span class="sxs-lookup"><span data-stu-id="4d867-115">Microsoft Visual C++ 14 and Windows SDK 10.0.10240.0 or newer (which is called CppSDK in this article).</span></span> <span data-ttu-id="4d867-116">Il existe deux façons d’obtenir CppSDK :</span><span class="sxs-lookup"><span data-stu-id="4d867-116">There are two ways to get CppSDK:</span></span>

    - <span data-ttu-id="4d867-117">Installez [Visual Studio Community Edition](https://developer.microsoft.com/downloads/vs-thankyou).</span><span class="sxs-lookup"><span data-stu-id="4d867-117">Install [Visual Studio Community Edition](https://developer.microsoft.com/downloads/vs-thankyou).</span></span> <span data-ttu-id="4d867-118">Vous devez disposer d’un sous-dossier \Windows Kits\10 dans le dossier Program Files, par exemple C:\Program Files (x86)\Windows Kits\10\.</span><span class="sxs-lookup"><span data-stu-id="4d867-118">You'll have a \Windows Kits\10 folder under the Program Files folder--for example, C:\Program Files (x86)\Windows Kits\10\.</span></span> <span data-ttu-id="4d867-119">Vous trouverez également la version du SDK Windows 10 sous \Windows Kits\10\Lib.</span><span class="sxs-lookup"><span data-stu-id="4d867-119">You'll also find the Windows 10 SDK version under \Windows Kits\10\Lib.</span></span> <span data-ttu-id="4d867-120">Si vous ne voyez pas ces dossiers, réinstallez Visual Studio et veillez à sélectionner le kit SDK Windows 10 lors de l’installation.</span><span class="sxs-lookup"><span data-stu-id="4d867-120">If you don’t see these folders, reinstall Visual Studio and be sure to select the Windows 10 SDK during the installation.</span></span> <span data-ttu-id="4d867-121">S’il est installé avec Visual Studio, le compilateur local U-SQL le trouvera automatiquement.</span><span class="sxs-lookup"><span data-stu-id="4d867-121">If you have this installed with Visual Studio, the U-SQL local compiler will find it automatically.</span></span>

    ![Data Lake Tools pour Visual Studio exécution locale Windows 10 SDK](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-windows-10-sdk.png)

    - <span data-ttu-id="4d867-123">Installez [Data Lake Tools for Visual Studio](http://aka.ms/adltoolsvs).</span><span class="sxs-lookup"><span data-stu-id="4d867-123">Install [Data Lake Tools for Visual Studio](http://aka.ms/adltoolsvs).</span></span> <span data-ttu-id="4d867-124">Vous trouverez les fichiers Visual C++ et le kit SDK Windows préconfigurés sous C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Microsoft\ADL Tools\X.X.XXXX.X\CppSDK.</span><span class="sxs-lookup"><span data-stu-id="4d867-124">You can find the prepackaged Visual C++ and Windows SDK files at C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Microsoft\ADL Tools\X.X.XXXX.X\CppSDK.</span></span> <span data-ttu-id="4d867-125">Dans ce cas, le compilateur U-SQL local ne trouve pas ces dépendances automatiquement.</span><span class="sxs-lookup"><span data-stu-id="4d867-125">In this case, the U-SQL local compiler cannot find the dependencies automatically.</span></span> <span data-ttu-id="4d867-126">Vous devez spécifier le chemin d’accès CppSDK pour lui.</span><span class="sxs-lookup"><span data-stu-id="4d867-126">You need to specify the CppSDK path for it.</span></span> <span data-ttu-id="4d867-127">Vous pouvez copier les fichiers vers un autre emplacement ou les utiliser tels quels.</span><span class="sxs-lookup"><span data-stu-id="4d867-127">You can either copy the files to another location or use it as is.</span></span>

## <a name="understand-basic-concepts"></a><span data-ttu-id="4d867-128">Comprendre les concepts de base</span><span class="sxs-lookup"><span data-stu-id="4d867-128">Understand basic concepts</span></span>

### <a name="data-root"></a><span data-ttu-id="4d867-129">Racine de données</span><span class="sxs-lookup"><span data-stu-id="4d867-129">Data root</span></span>

<span data-ttu-id="4d867-130">Ce dossier est un « magasin local » pour le compte de calcul local.</span><span class="sxs-lookup"><span data-stu-id="4d867-130">The data-root folder is a "local store" for the local compute account.</span></span> <span data-ttu-id="4d867-131">Il est équivalent au compte Azure Data Lake Store d’un compte Data Lake Analytics dans Azure.</span><span class="sxs-lookup"><span data-stu-id="4d867-131">It's equivalent to the Azure Data Lake Store account of a Data Lake Analytics account.</span></span> <span data-ttu-id="4d867-132">Basculer vers un dossier racine de données différent revient à basculer vers un autre compte de magasin.</span><span class="sxs-lookup"><span data-stu-id="4d867-132">Switching to a different data-root folder is just like switching to a different store account.</span></span> <span data-ttu-id="4d867-133">Si vous souhaitez accéder aux données généralement partagées avec des dossiers racines de données différents, vous devez utiliser des chemins d’accès absolus dans vos scripts.</span><span class="sxs-lookup"><span data-stu-id="4d867-133">If you want to access commonly shared data with different data-root folders, you must use absolute paths in your scripts.</span></span> <span data-ttu-id="4d867-134">Vous pouvez aussi créer des liens symboliques de système de fichiers (par exemple, **mklink** sur NTFS) sous le dossier racine de données, afin de pointer vers les données partagées.</span><span class="sxs-lookup"><span data-stu-id="4d867-134">Or, create file system symbolic links (for example, **mklink** on NTFS) under the data-root folder to point to the shared data.</span></span>

<span data-ttu-id="4d867-135">Le dossier racine de données est utilisé pour :</span><span class="sxs-lookup"><span data-stu-id="4d867-135">The data-root folder is used to:</span></span>

- <span data-ttu-id="4d867-136">Stocker les métadonnées locales, notamment des bases de données, des tables, des fonctions table (TVF) et des assemblys.</span><span class="sxs-lookup"><span data-stu-id="4d867-136">Store local metadata, including databases, tables, table-valued functions (TVFs), and assemblies.</span></span>
- <span data-ttu-id="4d867-137">Rechercher les chemins d’entrée et de sortie qui sont définis comme des chemins relatifs dans U-SQL.</span><span class="sxs-lookup"><span data-stu-id="4d867-137">Look up the input and output paths that are defined as relative paths in U-SQL.</span></span> <span data-ttu-id="4d867-138">Les chemins relatifs facilitent le déploiement de vos projets U-SQL dans Azure.</span><span class="sxs-lookup"><span data-stu-id="4d867-138">Using relative paths makes it easier to deploy your U-SQL projects to Azure.</span></span>

### <a name="file-path-in-u-sql"></a><span data-ttu-id="4d867-139">Chemin d’accès des fichiers dans U-SQL</span><span class="sxs-lookup"><span data-stu-id="4d867-139">File path in U-SQL</span></span>

<span data-ttu-id="4d867-140">Vous pouvez utiliser un chemin d’accès relatif et un chemin d’accès absolu local dans des scripts SQL-U.</span><span class="sxs-lookup"><span data-stu-id="4d867-140">You can use both a relative path and a local absolute path in U-SQL scripts.</span></span> <span data-ttu-id="4d867-141">Le chemin d’accès relatif dépend du chemin d’accès au dossier racine de données spécifié.</span><span class="sxs-lookup"><span data-stu-id="4d867-141">The relative path is relative to the specified data-root folder path.</span></span> <span data-ttu-id="4d867-142">Il est recommandé d’utiliser « / » en tant que séparateur de chemin afin de rendre vos scripts compatibles avec le côté serveur.</span><span class="sxs-lookup"><span data-stu-id="4d867-142">We recommend that you use "/" as the path separator to make your scripts compatible with the server side.</span></span> <span data-ttu-id="4d867-143">Voici quelques exemples de chemins relatifs, avec leurs chemins absolus équivalents.</span><span class="sxs-lookup"><span data-stu-id="4d867-143">Here are some examples of relative paths and their equivalent absolute paths.</span></span> <span data-ttu-id="4d867-144">Dans ces exemples, le chemin C:\LocalRunDataRoot correspond à la racine de données.</span><span class="sxs-lookup"><span data-stu-id="4d867-144">In these examples, C:\LocalRunDataRoot is the data-root folder.</span></span>

|<span data-ttu-id="4d867-145">Chemin relatif</span><span class="sxs-lookup"><span data-stu-id="4d867-145">Relative path</span></span>|<span data-ttu-id="4d867-146">Chemin absolu</span><span class="sxs-lookup"><span data-stu-id="4d867-146">Absolute path</span></span>|
|-------------|-------------|
|<span data-ttu-id="4d867-147">/abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="4d867-147">/abc/def/input.csv</span></span> |<span data-ttu-id="4d867-148">C:\LocalRunDataRoot\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="4d867-148">C:\LocalRunDataRoot\abc\def\input.csv</span></span>|
|<span data-ttu-id="4d867-149">abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="4d867-149">abc/def/input.csv</span></span>  |<span data-ttu-id="4d867-150">C:\LocalRunDataRoot\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="4d867-150">C:\LocalRunDataRoot\abc\def\input.csv</span></span>|
|<span data-ttu-id="4d867-151">D:/abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="4d867-151">D:/abc/def/input.csv</span></span> |<span data-ttu-id="4d867-152">D:\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="4d867-152">D:\abc\def\input.csv</span></span>|

### <a name="working-directory"></a><span data-ttu-id="4d867-153">Répertoire de travail</span><span class="sxs-lookup"><span data-stu-id="4d867-153">Working directory</span></span>

<span data-ttu-id="4d867-154">Lors d’une exécution locale du script U-SQL, un répertoire de travail est créé pendant la compilation sous le répertoire d’exécution actif.</span><span class="sxs-lookup"><span data-stu-id="4d867-154">When running the U-SQL script locally, a working directory is created during compilation under current running directory.</span></span> <span data-ttu-id="4d867-155">Outre les sorties de compilation, les fichiers exécutables nécessaires à l’exécution locale seront copiés sous forme de clichés instantanés dans ce répertoire de travail.</span><span class="sxs-lookup"><span data-stu-id="4d867-155">In addition to the compilation outputs, the needed runtime files for local execution will be shadow copied to this working directory.</span></span> <span data-ttu-id="4d867-156">Le dossier racine du répertoire de travail se nomme « ScopeWorkDir » et les fichiers sous le répertoire de travail sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="4d867-156">The working directory root folder is called "ScopeWorkDir" and the files under the working directory are as follows:</span></span>

|<span data-ttu-id="4d867-157">Répertoire/fichier</span><span class="sxs-lookup"><span data-stu-id="4d867-157">Directory/file</span></span>|<span data-ttu-id="4d867-158">Répertoire/fichier</span><span class="sxs-lookup"><span data-stu-id="4d867-158">Directory/file</span></span>|<span data-ttu-id="4d867-159">Répertoire/fichier</span><span class="sxs-lookup"><span data-stu-id="4d867-159">Directory/file</span></span>|<span data-ttu-id="4d867-160">Définition</span><span class="sxs-lookup"><span data-stu-id="4d867-160">Definition</span></span>|<span data-ttu-id="4d867-161">Description</span><span class="sxs-lookup"><span data-stu-id="4d867-161">Description</span></span>|
|--------------|--------------|--------------|----------|-----------|
|<span data-ttu-id="4d867-162">C6A101DDCB470506</span><span class="sxs-lookup"><span data-stu-id="4d867-162">C6A101DDCB470506</span></span>| | |<span data-ttu-id="4d867-163">Chaîne de hachage de la version exécutable</span><span class="sxs-lookup"><span data-stu-id="4d867-163">Hash string of runtime version</span></span>|<span data-ttu-id="4d867-164">Cliché instantané des fichiers exécutables nécessaires à l'exécution locale</span><span class="sxs-lookup"><span data-stu-id="4d867-164">Shadow copy of runtime files needed for local execution</span></span>|
| |<span data-ttu-id="4d867-165">Script_66AE4909AA0ED06C</span><span class="sxs-lookup"><span data-stu-id="4d867-165">Script_66AE4909AA0ED06C</span></span>| |<span data-ttu-id="4d867-166">Nom de script + chaîne de hachage du chemin du script</span><span class="sxs-lookup"><span data-stu-id="4d867-166">Script name + hash string of script path</span></span>|<span data-ttu-id="4d867-167">Résultats de la compilation et journalisation des étapes d'exécution</span><span class="sxs-lookup"><span data-stu-id="4d867-167">Compilation outputs and execution step logging</span></span>|
| | |<span data-ttu-id="4d867-168">\_script\_.abr</span><span class="sxs-lookup"><span data-stu-id="4d867-168">\_script\_.abr</span></span>|<span data-ttu-id="4d867-169">Sortie du compilateur</span><span class="sxs-lookup"><span data-stu-id="4d867-169">Compiler output</span></span>|<span data-ttu-id="4d867-170">Fichier algèbre</span><span class="sxs-lookup"><span data-stu-id="4d867-170">Algebra file</span></span>|
| | |<span data-ttu-id="4d867-171">\_ScopeCodeGen\_.*</span><span class="sxs-lookup"><span data-stu-id="4d867-171">\_ScopeCodeGen\_.*</span></span>|<span data-ttu-id="4d867-172">Sortie du compilateur</span><span class="sxs-lookup"><span data-stu-id="4d867-172">Compiler output</span></span>|<span data-ttu-id="4d867-173">Code géré généré</span><span class="sxs-lookup"><span data-stu-id="4d867-173">Generated managed code</span></span>|
| | |<span data-ttu-id="4d867-174">\_ScopeCodeGenEngine\_.*</span><span class="sxs-lookup"><span data-stu-id="4d867-174">\_ScopeCodeGenEngine\_.*</span></span>|<span data-ttu-id="4d867-175">Sortie du compilateur</span><span class="sxs-lookup"><span data-stu-id="4d867-175">Compiler output</span></span>|<span data-ttu-id="4d867-176">Code natif généré</span><span class="sxs-lookup"><span data-stu-id="4d867-176">Generated native code</span></span>|
| | |<span data-ttu-id="4d867-177">referenced assemblies</span><span class="sxs-lookup"><span data-stu-id="4d867-177">referenced assemblies</span></span>|<span data-ttu-id="4d867-178">Référence d’assembly</span><span class="sxs-lookup"><span data-stu-id="4d867-178">Assembly reference</span></span>|<span data-ttu-id="4d867-179">Fichiers d’assemblys de référence</span><span class="sxs-lookup"><span data-stu-id="4d867-179">Referenced assembly files</span></span>|
| | |<span data-ttu-id="4d867-180">deployed_resources</span><span class="sxs-lookup"><span data-stu-id="4d867-180">deployed_resources</span></span>|<span data-ttu-id="4d867-181">Déploiement de ressources</span><span class="sxs-lookup"><span data-stu-id="4d867-181">Resource deployment</span></span>|<span data-ttu-id="4d867-182">Fichiers de déploiement de ressources</span><span class="sxs-lookup"><span data-stu-id="4d867-182">Resource deployment files</span></span>|
| | |<span data-ttu-id="4d867-183">xxxxxxxx.xxx[1..n]\_\*.*</span><span class="sxs-lookup"><span data-stu-id="4d867-183">xxxxxxxx.xxx[1..n]\_\*.*</span></span>|<span data-ttu-id="4d867-184">Journal d’exécution</span><span class="sxs-lookup"><span data-stu-id="4d867-184">Execution log</span></span>|<span data-ttu-id="4d867-185">Journal des étapes d'exécution</span><span class="sxs-lookup"><span data-stu-id="4d867-185">Log of execution steps</span></span>|


## <a name="use-the-sdk-from-the-command-line"></a><span data-ttu-id="4d867-186">Utiliser le Kit de développement logiciel (SDK) depuis la ligne de commande</span><span class="sxs-lookup"><span data-stu-id="4d867-186">Use the SDK from the command line</span></span>

### <a name="command-line-interface-of-the-helper-application"></a><span data-ttu-id="4d867-187">Interface de ligne de commande de l’application d’assistance</span><span class="sxs-lookup"><span data-stu-id="4d867-187">Command-line interface of the helper application</span></span>

<span data-ttu-id="4d867-188">Sous SDK directory\build\runtime, le fichier LocalRunHelper.exe correspond à l’application d’assistance de ligne de commande qui fournit des interfaces pour la plupart des fonctions d’exécution locale couramment utilisées.</span><span class="sxs-lookup"><span data-stu-id="4d867-188">Under SDK directory\build\runtime, LocalRunHelper.exe is the command-line helper application that provides interfaces to most of the commonly used local-run functions.</span></span> <span data-ttu-id="4d867-189">Notez que la commande et les commutateurs d’arguments respectent la casse.</span><span class="sxs-lookup"><span data-stu-id="4d867-189">Note that both the command and the argument switches are case-sensitive.</span></span> <span data-ttu-id="4d867-190">Pour l’appeler :</span><span class="sxs-lookup"><span data-stu-id="4d867-190">To invoke it:</span></span>

    LocalRunHelper.exe <command> <Required-Command-Arguments> [Optional-Command-Arguments]

<span data-ttu-id="4d867-191">Exécutez le fichier LocalRunHelper.exe sans argument ou avec le commutateur **help** pour afficher les informations d’aide :</span><span class="sxs-lookup"><span data-stu-id="4d867-191">Run LocalRunHelper.exe without arguments or with the **help** switch to show the help information:</span></span>

    > LocalRunHelper.exe help

        Command 'help' :  Show usage information
        Command 'compile' :  Compile the script
        Required Arguments :
            -Script param
                    Script File Path
        Optional Arguments :
            -Shallow [default value 'False']
                    Shallow compile

<span data-ttu-id="4d867-192">Dans les informations d’aide :</span><span class="sxs-lookup"><span data-stu-id="4d867-192">In the help information:</span></span>

-  <span data-ttu-id="4d867-193">Le paramètre **Commande** fournit le nom de la commande.</span><span class="sxs-lookup"><span data-stu-id="4d867-193">**Command** gives the command’s name.</span></span>  
-  <span data-ttu-id="4d867-194">Le paramètre **Argument obligatoire** répertorie les arguments qui doivent être fournis.</span><span class="sxs-lookup"><span data-stu-id="4d867-194">**Required Argument** lists arguments that must be supplied.</span></span>  
-  <span data-ttu-id="4d867-195">Le paramètre **Argument facultatif** répertorie les arguments facultatifs, avec des valeurs par défaut.</span><span class="sxs-lookup"><span data-stu-id="4d867-195">**Optional Argument** lists arguments that are optional, with default values.</span></span>  <span data-ttu-id="4d867-196">Les arguments booléens facultatifs n’incluent aucun paramètre, et leur valeur est négative par défaut.</span><span class="sxs-lookup"><span data-stu-id="4d867-196">Optional Boolean arguments don’t have parameters, and their appearances mean negative to their default value.</span></span>

### <a name="return-value-and-logging"></a><span data-ttu-id="4d867-197">Valeur de retour et journalisation</span><span class="sxs-lookup"><span data-stu-id="4d867-197">Return value and logging</span></span>

<span data-ttu-id="4d867-198">L’application d’assistance renvoie la valeur **0** (réussite) et **-1** (échec).</span><span class="sxs-lookup"><span data-stu-id="4d867-198">The helper application returns **0** for success and **-1** for failure.</span></span> <span data-ttu-id="4d867-199">Par défaut, l’assistant envoie tous les messages vers la console active.</span><span class="sxs-lookup"><span data-stu-id="4d867-199">By default, the helper sends all messages to the current console.</span></span> <span data-ttu-id="4d867-200">Toutefois, la plupart des commandes prennent en charge l’argument facultatif **-MessageOut path_to_log_file** qui redirige les sorties vers un fichier journal.</span><span class="sxs-lookup"><span data-stu-id="4d867-200">However, most of the commands support the **-MessageOut path_to_log_file** optional argument that redirects the outputs to a log file.</span></span>

### <a name="environment-variable-configuring"></a><span data-ttu-id="4d867-201">Configuration de la variable d’environnement</span><span class="sxs-lookup"><span data-stu-id="4d867-201">Environment variable configuring</span></span>

<span data-ttu-id="4d867-202">L’exécution U-SQL locale requiert une racine de données spécifiée comme compte de stockage local, ainsi qu’un chemin d’accès CppSDK spécifié pour les dépendances.</span><span class="sxs-lookup"><span data-stu-id="4d867-202">U-SQL local run needs a specified data root as local storage account, as well as a specified CppSDK path for dependencies.</span></span> <span data-ttu-id="4d867-203">Vous pouvez définir l’argument en ligne de commande ou définir leur variable d’environnement.</span><span class="sxs-lookup"><span data-stu-id="4d867-203">You can both set the argument in command-line or set environment variable for them.</span></span>

- <span data-ttu-id="4d867-204">Définissez la variable d’environnement **SCOPE_CPP_SDK**.</span><span class="sxs-lookup"><span data-stu-id="4d867-204">Set the **SCOPE_CPP_SDK** environment variable.</span></span>

    <span data-ttu-id="4d867-205">Si vous obtenez Microsoft Visual C++ et le kit SDK Windows en installant Data Lake Tools pour Visual Studio, vérifiez que vous disposez du dossier suivant :</span><span class="sxs-lookup"><span data-stu-id="4d867-205">If you get Microsoft Visual C++ and the Windows SDK by installing Data Lake Tools for Visual Studio, verify that you have the following folder:</span></span>

        C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Microsoft\Microsoft Azure Data Lake Tools for Visual Studio 2015\X.X.XXXX.X\CppSDK

    <span data-ttu-id="4d867-206">Définissez une nouvelle variable d’environnement appelée **SCOPE_CPP_SDK**, qui pointe vers ce répertoire.</span><span class="sxs-lookup"><span data-stu-id="4d867-206">Define a new environment variable called **SCOPE_CPP_SDK** to point to this directory.</span></span> <span data-ttu-id="4d867-207">Vous pouvez aussi copier le dossier vers un autre emplacement et spécifiez **SCOPE_CPP_SDK**.</span><span class="sxs-lookup"><span data-stu-id="4d867-207">Or copy the folder to the other location and specify **SCOPE_CPP_SDK** as that.</span></span>

    <span data-ttu-id="4d867-208">Outre la définition de la variable d’environnement, vous pouvez également spécifier l’argument **-CppSDK** lorsque vous utilisez la ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="4d867-208">In addition to setting the environment variable, you can specify the **-CppSDK** argument when you're using the command line.</span></span> <span data-ttu-id="4d867-209">Cet argument remplace votre variable d’environnement CppSDK par défaut.</span><span class="sxs-lookup"><span data-stu-id="4d867-209">This argument overwrites your default CppSDK environment variable.</span></span>

- <span data-ttu-id="4d867-210">Définissez la variable d’environnement **LOCALRUN_DATAROOT**.</span><span class="sxs-lookup"><span data-stu-id="4d867-210">Set the **LOCALRUN_DATAROOT** environment variable.</span></span>

    <span data-ttu-id="4d867-211">Définissez une variable d’environnement appelée **LOCALRUN_DATAROOT**, qui pointe vers la racine de données.</span><span class="sxs-lookup"><span data-stu-id="4d867-211">Define a new environment variable called **LOCALRUN_DATAROOT** that points to the data root.</span></span>

    <span data-ttu-id="4d867-212">Outre la définition de la variable d’environnement, vous pouvez spécifier l’argument **-DataRoot** avec le chemin vers la racine de données lorsque vous utilisez une ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="4d867-212">In addition to setting the environment variable, you can specify the **-DataRoot** argument with the data-root path when you're using a command line.</span></span> <span data-ttu-id="4d867-213">Cet argument remplace votre variable d’environnement de racine de données par défaut.</span><span class="sxs-lookup"><span data-stu-id="4d867-213">This argument overwrites your default data-root environment variable.</span></span> <span data-ttu-id="4d867-214">Vous devez ajouter cet argument à chaque ligne de commande que vous exécutez, afin de pouvoir remplacer la variable d’environnement de racine de données par défaut, pour toutes les opérations.</span><span class="sxs-lookup"><span data-stu-id="4d867-214">You need to add this argument to every command line you're running so that you can overwrite the default data-root environment variable for all operations.</span></span>

### <a name="sdk-command-line-usage-samples"></a><span data-ttu-id="4d867-215">Exemples d’utilisation en ligne de commande du Kit SDK</span><span class="sxs-lookup"><span data-stu-id="4d867-215">SDK command line usage samples</span></span>

#### <a name="compile-and-run"></a><span data-ttu-id="4d867-216">Compilation et exécution</span><span class="sxs-lookup"><span data-stu-id="4d867-216">Compile and run</span></span>

<span data-ttu-id="4d867-217">La commande **run** sert à compiler le script, puis à exécuter les résultats compilés.</span><span class="sxs-lookup"><span data-stu-id="4d867-217">The **run** command is used to compile the script and then execute compiled results.</span></span> <span data-ttu-id="4d867-218">Ses arguments de ligne de commande sont une combinaison des commandes **compile** et **execute**.</span><span class="sxs-lookup"><span data-stu-id="4d867-218">Its command-line arguments are a combination of those from **compile** and **execute**.</span></span>

    LocalRunHelper run -Script path_to_usql_script.usql [optional_arguments]

<span data-ttu-id="4d867-219">Voici les arguments facultatifs de **run** :</span><span class="sxs-lookup"><span data-stu-id="4d867-219">The following are optional arguments for **run**:</span></span>


|<span data-ttu-id="4d867-220">Argument</span><span class="sxs-lookup"><span data-stu-id="4d867-220">Argument</span></span>|<span data-ttu-id="4d867-221">Valeur par défaut</span><span class="sxs-lookup"><span data-stu-id="4d867-221">Default value</span></span>|<span data-ttu-id="4d867-222">Description</span><span class="sxs-lookup"><span data-stu-id="4d867-222">Description</span></span>|
|--------|-------------|-----------|
|<span data-ttu-id="4d867-223">-CodeBehind</span><span class="sxs-lookup"><span data-stu-id="4d867-223">-CodeBehind</span></span>|<span data-ttu-id="4d867-224">False</span><span class="sxs-lookup"><span data-stu-id="4d867-224">False</span></span>|<span data-ttu-id="4d867-225">Le script a du code-behind .cs</span><span class="sxs-lookup"><span data-stu-id="4d867-225">The script has .cs code behind</span></span>|
|<span data-ttu-id="4d867-226">-CppSDK</span><span class="sxs-lookup"><span data-stu-id="4d867-226">-CppSDK</span></span>| |<span data-ttu-id="4d867-227">Répertoire CppSDK</span><span class="sxs-lookup"><span data-stu-id="4d867-227">CppSDK Directory</span></span>|
|<span data-ttu-id="4d867-228">-DataRoot</span><span class="sxs-lookup"><span data-stu-id="4d867-228">-DataRoot</span></span>| <span data-ttu-id="4d867-229">Variable d’environnement DataRoot</span><span class="sxs-lookup"><span data-stu-id="4d867-229">DataRoot environment variable</span></span>|<span data-ttu-id="4d867-230">DataRoot pour l’exécution locale, par défaut la variable d’environnement « LOCALRUN_DATAROOT »</span><span class="sxs-lookup"><span data-stu-id="4d867-230">DataRoot for local run, default to 'LOCALRUN_DATAROOT' environment variable</span></span>|
|<span data-ttu-id="4d867-231">-MessageOut</span><span class="sxs-lookup"><span data-stu-id="4d867-231">-MessageOut</span></span>| |<span data-ttu-id="4d867-232">Vidage des messages de la console dans un fichier</span><span class="sxs-lookup"><span data-stu-id="4d867-232">Dump messages on console to a file</span></span>|
|<span data-ttu-id="4d867-233">-Parallel</span><span class="sxs-lookup"><span data-stu-id="4d867-233">-Parallel</span></span>|<span data-ttu-id="4d867-234">1</span><span class="sxs-lookup"><span data-stu-id="4d867-234">1</span></span>|<span data-ttu-id="4d867-235">Exécuter le plan avec le parallélisme spécifié</span><span class="sxs-lookup"><span data-stu-id="4d867-235">Run the plan with the specified parallelism</span></span>|
|<span data-ttu-id="4d867-236">-References</span><span class="sxs-lookup"><span data-stu-id="4d867-236">-References</span></span>| |<span data-ttu-id="4d867-237">Liste des chemins d’accès vers des assemblys de référence supplémentaires ou des fichiers de données de code-behind, séparés par ';'</span><span class="sxs-lookup"><span data-stu-id="4d867-237">List of paths to extra reference assemblies or data files of code behind, separated by ';'</span></span>|
|<span data-ttu-id="4d867-238">-UdoRedirect</span><span class="sxs-lookup"><span data-stu-id="4d867-238">-UdoRedirect</span></span>|<span data-ttu-id="4d867-239">False</span><span class="sxs-lookup"><span data-stu-id="4d867-239">False</span></span>|<span data-ttu-id="4d867-240">Générer la configuration de redirection d’assembly Udo</span><span class="sxs-lookup"><span data-stu-id="4d867-240">Generate Udo assembly redirect config</span></span>|
|<span data-ttu-id="4d867-241">-UseDatabase</span><span class="sxs-lookup"><span data-stu-id="4d867-241">-UseDatabase</span></span>|<span data-ttu-id="4d867-242">master</span><span class="sxs-lookup"><span data-stu-id="4d867-242">master</span></span>|<span data-ttu-id="4d867-243">Base de données à utiliser pour l’inscription temporaire des assemblys et du code-behind</span><span class="sxs-lookup"><span data-stu-id="4d867-243">Database to use for code behind temporary assembly registration</span></span>|
|<span data-ttu-id="4d867-244">-Verbose</span><span class="sxs-lookup"><span data-stu-id="4d867-244">-Verbose</span></span>|<span data-ttu-id="4d867-245">False</span><span class="sxs-lookup"><span data-stu-id="4d867-245">False</span></span>|<span data-ttu-id="4d867-246">Afficher les sorties détaillées du runtime</span><span class="sxs-lookup"><span data-stu-id="4d867-246">Show detailed outputs from runtime</span></span>|
|<span data-ttu-id="4d867-247">-WorkDir</span><span class="sxs-lookup"><span data-stu-id="4d867-247">-WorkDir</span></span>|<span data-ttu-id="4d867-248">Répertoire actif</span><span class="sxs-lookup"><span data-stu-id="4d867-248">Current Directory</span></span>|<span data-ttu-id="4d867-249">Répertoire des sorties et de l’utilisation du compilateur</span><span class="sxs-lookup"><span data-stu-id="4d867-249">Directory for compiler usage and outputs</span></span>|
|<span data-ttu-id="4d867-250">-RunScopeCEP</span><span class="sxs-lookup"><span data-stu-id="4d867-250">-RunScopeCEP</span></span>|<span data-ttu-id="4d867-251">0</span><span class="sxs-lookup"><span data-stu-id="4d867-251">0</span></span>|<span data-ttu-id="4d867-252">Mode ScopeCEP à utiliser</span><span class="sxs-lookup"><span data-stu-id="4d867-252">ScopeCEP mode to use</span></span>|
|<span data-ttu-id="4d867-253">-ScopeCEPTempPath</span><span class="sxs-lookup"><span data-stu-id="4d867-253">-ScopeCEPTempPath</span></span>|<span data-ttu-id="4d867-254">temp</span><span class="sxs-lookup"><span data-stu-id="4d867-254">temp</span></span>|<span data-ttu-id="4d867-255">Chemin d’accès temporaire à utiliser pour la diffusion en continu de données</span><span class="sxs-lookup"><span data-stu-id="4d867-255">Temp path to use for streaming data</span></span>|
|<span data-ttu-id="4d867-256">-OptFlags</span><span class="sxs-lookup"><span data-stu-id="4d867-256">-OptFlags</span></span>| |<span data-ttu-id="4d867-257">Liste séparée par des virgules d’indicateurs d’optimiseur</span><span class="sxs-lookup"><span data-stu-id="4d867-257">Comma-separated list of optimizer flags</span></span>|


<span data-ttu-id="4d867-258">Voici un exemple :</span><span class="sxs-lookup"><span data-stu-id="4d867-258">Here's an example:</span></span>

    LocalRunHelper run -Script d:\test\test1.usql -WorkDir d:\test\bin -CodeBehind -References "d:\asm\ref1.dll;d:\asm\ref2.dll" -UseDatabase testDB –Parallel 5 -Verbose

<span data-ttu-id="4d867-259">En plus de combiner les commandes **compile** et **execute**, vous pouvez compiler et exécuter séparément les fichiers exécutables compilés.</span><span class="sxs-lookup"><span data-stu-id="4d867-259">Besides combining **compile** and **execute**, you can compile and execute the compiled executables separately.</span></span>

#### <a name="compile-a-u-sql-script"></a><span data-ttu-id="4d867-260">Compiler un script U-SQL</span><span class="sxs-lookup"><span data-stu-id="4d867-260">Compile a U-SQL script</span></span>

<span data-ttu-id="4d867-261">La commande **compile** permet de compiler un script U-SQL vers des exécutables.</span><span class="sxs-lookup"><span data-stu-id="4d867-261">The **compile** command is used to compile a U-SQL script to executables.</span></span>

    LocalRunHelper compile -Script path_to_usql_script.usql [optional_arguments]

<span data-ttu-id="4d867-262">Voici les arguments facultatifs de **compile** :</span><span class="sxs-lookup"><span data-stu-id="4d867-262">The following are optional arguments for **compile**:</span></span>


|<span data-ttu-id="4d867-263">Argument</span><span class="sxs-lookup"><span data-stu-id="4d867-263">Argument</span></span>|<span data-ttu-id="4d867-264">Description</span><span class="sxs-lookup"><span data-stu-id="4d867-264">Description</span></span>|
|--------|-----------|
| <span data-ttu-id="4d867-265">-CodeBehind [valeur par défaut 'False']</span><span class="sxs-lookup"><span data-stu-id="4d867-265">-CodeBehind [default value 'False']</span></span>|<span data-ttu-id="4d867-266">Le script a du code-behind .cs</span><span class="sxs-lookup"><span data-stu-id="4d867-266">The script has .cs code behind</span></span>|
| <span data-ttu-id="4d867-267">-CppSDK [valeur par défaut '']</span><span class="sxs-lookup"><span data-stu-id="4d867-267">-CppSDK [default value '']</span></span>|<span data-ttu-id="4d867-268">Répertoire CppSDK</span><span class="sxs-lookup"><span data-stu-id="4d867-268">CppSDK Directory</span></span>|
| <span data-ttu-id="4d867-269">-DataRoot [valeur par défaut ’DataRoot environment variable’]</span><span class="sxs-lookup"><span data-stu-id="4d867-269">-DataRoot [default value 'DataRoot environment variable']</span></span>|<span data-ttu-id="4d867-270">DataRoot pour l’exécution locale, par défaut la variable d’environnement « LOCALRUN_DATAROOT »</span><span class="sxs-lookup"><span data-stu-id="4d867-270">DataRoot for local run, default to 'LOCALRUN_DATAROOT' environment variable</span></span>|
| <span data-ttu-id="4d867-271">-MessageOut [valeur par défaut '']</span><span class="sxs-lookup"><span data-stu-id="4d867-271">-MessageOut [default value '']</span></span>|<span data-ttu-id="4d867-272">Vidage des messages de la console dans un fichier</span><span class="sxs-lookup"><span data-stu-id="4d867-272">Dump messages on console to a file</span></span>|
| <span data-ttu-id="4d867-273">-References [valeur par défaut '']</span><span class="sxs-lookup"><span data-stu-id="4d867-273">-References [default value '']</span></span>|<span data-ttu-id="4d867-274">Liste des chemins d’accès vers des assemblys de référence supplémentaires ou des fichiers de données de code-behind, séparés par ';'</span><span class="sxs-lookup"><span data-stu-id="4d867-274">List of paths to extra reference assemblies or data files of code behind, separated by ';'</span></span>|
| <span data-ttu-id="4d867-275">-Shallow [valeur par défaut 'False']</span><span class="sxs-lookup"><span data-stu-id="4d867-275">-Shallow [default value 'False']</span></span>|<span data-ttu-id="4d867-276">Compilation superficielle</span><span class="sxs-lookup"><span data-stu-id="4d867-276">Shallow compile</span></span>|
| <span data-ttu-id="4d867-277">-UdoRedirect [valeur par défaut 'False']</span><span class="sxs-lookup"><span data-stu-id="4d867-277">-UdoRedirect [default value 'False']</span></span>|<span data-ttu-id="4d867-278">Générer la configuration de redirection d’assembly Udo</span><span class="sxs-lookup"><span data-stu-id="4d867-278">Generate Udo assembly redirect config</span></span>|
| <span data-ttu-id="4d867-279">-UseDatabase [valeur par défaut 'master']</span><span class="sxs-lookup"><span data-stu-id="4d867-279">-UseDatabase [default value 'master']</span></span>|<span data-ttu-id="4d867-280">Base de données à utiliser pour l’inscription temporaire des assemblys et du code-behind</span><span class="sxs-lookup"><span data-stu-id="4d867-280">Database to use for code behind temporary assembly registration</span></span>|
| <span data-ttu-id="4d867-281">-WorkDir [valeur par défaut ’Current Directory’]</span><span class="sxs-lookup"><span data-stu-id="4d867-281">-WorkDir [default value 'Current Directory']</span></span>|<span data-ttu-id="4d867-282">Répertoire des sorties et de l’utilisation du compilateur</span><span class="sxs-lookup"><span data-stu-id="4d867-282">Directory for compiler usage and outputs</span></span>|
| <span data-ttu-id="4d867-283">-RunScopeCEP [valeur par défaut ’0’]</span><span class="sxs-lookup"><span data-stu-id="4d867-283">-RunScopeCEP [default value '0']</span></span>|<span data-ttu-id="4d867-284">Mode ScopeCEP à utiliser</span><span class="sxs-lookup"><span data-stu-id="4d867-284">ScopeCEP mode to use</span></span>|
| <span data-ttu-id="4d867-285">-ScopeCEPTempPath [valeur par défaut ’temp’]</span><span class="sxs-lookup"><span data-stu-id="4d867-285">-ScopeCEPTempPath [default value 'temp']</span></span>|<span data-ttu-id="4d867-286">Chemin d’accès temporaire à utiliser pour la diffusion en continu de données</span><span class="sxs-lookup"><span data-stu-id="4d867-286">Temp path to use for streaming data</span></span>|
| <span data-ttu-id="4d867-287">-OptFlags [valeur par défaut ’’]</span><span class="sxs-lookup"><span data-stu-id="4d867-287">-OptFlags [default value '']</span></span>|<span data-ttu-id="4d867-288">Liste séparée par des virgules d’indicateurs d’optimiseur</span><span class="sxs-lookup"><span data-stu-id="4d867-288">Comma-separated list of optimizer flags</span></span>|


<span data-ttu-id="4d867-289">Voici quelques exemples d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="4d867-289">Here are some usage examples.</span></span>

<span data-ttu-id="4d867-290">Compilez un script U-SQL :</span><span class="sxs-lookup"><span data-stu-id="4d867-290">Compile a U-SQL script:</span></span>

    LocalRunHelper compile -Script d:\test\test1.usql

<span data-ttu-id="4d867-291">Compilez un script SQL-U et définissez le dossier racine de données.</span><span class="sxs-lookup"><span data-stu-id="4d867-291">Compile a U-SQL script and set the data-root folder.</span></span> <span data-ttu-id="4d867-292">Notez que cette opération remplace la variable d’environnement définie.</span><span class="sxs-lookup"><span data-stu-id="4d867-292">Note that this will overwrite the set environment variable.</span></span>

    LocalRunHelper compile -Script d:\test\test1.usql –DataRoot c:\DataRoot

<span data-ttu-id="4d867-293">Compilez un script U-SQL et définissez un répertoire de travail, un assembly de référence et une base de données :</span><span class="sxs-lookup"><span data-stu-id="4d867-293">Compile a U-SQL script and set a working directory, reference assembly, and database:</span></span>

    LocalRunHelper compile -Script d:\test\test1.usql -WorkDir d:\test\bin -References "d:\asm\ref1.dll;d:\asm\ref2.dll" -UseDatabase testDB

#### <a name="execute-compiled-results"></a><span data-ttu-id="4d867-294">Exécuter les résultats compilés</span><span class="sxs-lookup"><span data-stu-id="4d867-294">Execute compiled results</span></span>

<span data-ttu-id="4d867-295">La commande **execute** est utilisée pour exécuter les résultats compilés.</span><span class="sxs-lookup"><span data-stu-id="4d867-295">The **execute** command is used to execute compiled results.</span></span>   

    LocalRunHelper execute -Algebra path_to_compiled_algebra_file [optional_arguments]

<span data-ttu-id="4d867-296">Voici les arguments facultatifs **d’execute** :</span><span class="sxs-lookup"><span data-stu-id="4d867-296">The following are optional arguments for **execute**:</span></span>

|<span data-ttu-id="4d867-297">Argument</span><span class="sxs-lookup"><span data-stu-id="4d867-297">Argument</span></span>|<span data-ttu-id="4d867-298">Description</span><span class="sxs-lookup"><span data-stu-id="4d867-298">Description</span></span>|
|--------|-----------|
|<span data-ttu-id="4d867-299">-DataRoot [valeur par défaut '']</span><span class="sxs-lookup"><span data-stu-id="4d867-299">-DataRoot [default value '']</span></span>|<span data-ttu-id="4d867-300">Racine de données pour l’exécution des métadonnées.</span><span class="sxs-lookup"><span data-stu-id="4d867-300">Data root for metadata execution.</span></span> <span data-ttu-id="4d867-301">La valeur par défaut correspond à la variable d’environnement **LOCALRUN_DATAROOT**.</span><span class="sxs-lookup"><span data-stu-id="4d867-301">It defaults to the **LOCALRUN_DATAROOT** environment variable.</span></span>|
|<span data-ttu-id="4d867-302">-MessageOut [valeur par défaut '']</span><span class="sxs-lookup"><span data-stu-id="4d867-302">-MessageOut [default value '']</span></span>|<span data-ttu-id="4d867-303">Videz les messages de la console dans un fichier.</span><span class="sxs-lookup"><span data-stu-id="4d867-303">Dump messages on the console to a file.</span></span>|
|<span data-ttu-id="4d867-304">-Parallel [valeur par défaut '1']</span><span class="sxs-lookup"><span data-stu-id="4d867-304">-Parallel [default value '1']</span></span>|<span data-ttu-id="4d867-305">Indicateur de lancement des étapes d’exécution locale générées avec le niveau de parallélisme spécifié.</span><span class="sxs-lookup"><span data-stu-id="4d867-305">Indicator to run the generated local-run steps with the specified parallelism level.</span></span>|
|<span data-ttu-id="4d867-306">-Verbose [valeur par défaut 'False']</span><span class="sxs-lookup"><span data-stu-id="4d867-306">-Verbose [default value 'False']</span></span>|<span data-ttu-id="4d867-307">Indicateur affichant les sorties détaillées du runtime.</span><span class="sxs-lookup"><span data-stu-id="4d867-307">Indicator to show detailed outputs from runtime.</span></span>|

<span data-ttu-id="4d867-308">Voici un exemple d’utilisation :</span><span class="sxs-lookup"><span data-stu-id="4d867-308">Here's a usage example:</span></span>

    LocalRunHelper execute -Algebra d:\test\workdir\C6A101DDCB470506\Script_66AE4909AA0ED06C\__script__.abr –DataRoot c:\DataRoot –Parallel 5


## <a name="use-the-sdk-with-programming-interfaces"></a><span data-ttu-id="4d867-309">Utiliser le kit SDK avec des interfaces de programmation</span><span class="sxs-lookup"><span data-stu-id="4d867-309">Use the SDK with programming interfaces</span></span>

<span data-ttu-id="4d867-310">Les interfaces de programmation se trouvent toutes dans LocalRunHelper.exe.</span><span class="sxs-lookup"><span data-stu-id="4d867-310">The programming interfaces are all located in the LocalRunHelper.exe.</span></span> <span data-ttu-id="4d867-311">Vous pouvez les utiliser pour intégrer les fonctionnalités du kit SDK U-SQL, et l’infrastructure de test C# pour mettre à l’échelle votre test local du script SQL-U.</span><span class="sxs-lookup"><span data-stu-id="4d867-311">You can use them to integrate the functionality of the U-SQL SDK and the C# test framework to scale your U-SQL script local test.</span></span> <span data-ttu-id="4d867-312">Dans cet article, je vais utiliser le projet de test unitaire C# standard pour montrer comment utiliser ces interfaces afin de tester un script U-SQL.</span><span class="sxs-lookup"><span data-stu-id="4d867-312">In this article, I will use the standard C# unit test project to show how to use these interfaces to test your U-SQL script.</span></span>

### <a name="step-1-create-c-unit-test-project-and-configuration"></a><span data-ttu-id="4d867-313">Étape 1 : Créer une configuration et un projet de test unitaire C#</span><span class="sxs-lookup"><span data-stu-id="4d867-313">Step 1: Create C# unit test project and configuration</span></span>

- <span data-ttu-id="4d867-314">Créez un projet de test unitaire C# dans Fichier > Nouveau > Projet > Visual C# > Test > Projet de test unitaire.</span><span class="sxs-lookup"><span data-stu-id="4d867-314">Create a C# unit test project through File > New > Project > Visual C# > Test > Unit Test Project.</span></span>
- <span data-ttu-id="4d867-315">Ajoutez LocalRunHelper.exe comme référence du projet.</span><span class="sxs-lookup"><span data-stu-id="4d867-315">Add LocalRunHelper.exe as a reference for the project.</span></span> <span data-ttu-id="4d867-316">LocalRunHelper.exe se trouve dans \build\runtime\LocalRunHelper.exe, dans le package NuGet.</span><span class="sxs-lookup"><span data-stu-id="4d867-316">The LocalRunHelper.exe is located at \build\runtime\LocalRunHelper.exe in Nuget package.</span></span>

    ![Kit SDK Azure Data Lake U-SQL - Ajouter une référence](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-add-reference.png)

- <span data-ttu-id="4d867-318">Le Kit SDK U-SQL prend en charge **uniquement** l’environnement x64 ; veillez donc à définir la plateforme cible de build sur x64.</span><span class="sxs-lookup"><span data-stu-id="4d867-318">U-SQL SDK **only** support x64 environment, make sure to set build platform target as x64.</span></span> <span data-ttu-id="4d867-319">Vous pouvez le faire dans Propriété du projet > Build > Plateforme cible.</span><span class="sxs-lookup"><span data-stu-id="4d867-319">You can set that through Project Property > Build > Platform target.</span></span>

    ![Kit SDK Azure Data Lake U-SQL - Configurer un projet x64](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-configure-x64.png)

- <span data-ttu-id="4d867-321">Veillez à définir votre environnement de test sur x64.</span><span class="sxs-lookup"><span data-stu-id="4d867-321">Make sure to set your test environment as x64.</span></span> <span data-ttu-id="4d867-322">Dans Visual Studio, vous pouvez le faire dans Test > Paramètres de test > Architecture de processeur par défaut > x64.</span><span class="sxs-lookup"><span data-stu-id="4d867-322">In Visual Studio, you can set it through Test > Test Settings > Default Processor Architecture > x64.</span></span>

    ![Kit SDK Azure Data Lake U-SQL - Configurer un environnement de test x64](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-configure-test-x64.png)

- <span data-ttu-id="4d867-324">Veillez à copier tous les fichiers de dépendance sous NugetPackage\build\runtime\ dans le répertoire de travail qui se trouve généralement sous ProjectFolder\bin\x64\Debug.</span><span class="sxs-lookup"><span data-stu-id="4d867-324">Make sure to copy all dependency files under NugetPackage\build\runtime\ to project working directory which is usually under ProjectFolder\bin\x64\Debug.</span></span>

### <a name="step-2-create-u-sql-script-test-case"></a><span data-ttu-id="4d867-325">Étape 2 : Créer des cas de test du script U-SQL</span><span class="sxs-lookup"><span data-stu-id="4d867-325">Step 2: Create U-SQL script test case</span></span>

<span data-ttu-id="4d867-326">Voici l’exemple de code de test du script U-SQL.</span><span class="sxs-lookup"><span data-stu-id="4d867-326">Below is the sample code for U-SQL script test.</span></span> <span data-ttu-id="4d867-327">Pour le test, vous devez préparer les scripts, les fichiers d’entrée et les fichiers sortie attendus.</span><span class="sxs-lookup"><span data-stu-id="4d867-327">For testing, you need to prepare scripts, input files and expected output files.</span></span>

    using System;
    using Microsoft.VisualStudio.TestTools.UnitTesting;
    using System.IO;
    using System.Text;
    using System.Security.Cryptography;
    using Microsoft.Analytics.LocalRun;

    namespace UnitTestProject1
    {
        [TestClass]
        public class USQLUnitTest
        {
            [TestMethod]
            public void TestUSQLScript()
            {
                //Specify the local run message output path
                StreamWriter MessageOutput = new StreamWriter("../../../log.txt");

                LocalRunHelper localrun = new LocalRunHelper(MessageOutput);

                //Configure the DateRoot path, Script Path and CPPSDK path
                localrun.DataRoot = "../../../";
                localrun.ScriptPath = "../../../Script/Script.usql";
                localrun.CppSdkDir = "../../../CppSDK";

                //Run U-SQL script
                localrun.DoRun();

                //Script output 
                string Result = Path.Combine(localrun.DataRoot, "Output/result.csv");

                //Expected script output
                string ExpectedResult = "../../../ExpectedOutput/result.csv";

                Test.Helpers.FileAssert.AreEqual(Result, ExpectedResult);

                //Don't forget to close MessageOutput to get logs into file
                MessageOutput.Close();
            }
        }
    }

    namespace Test.Helpers
    {
        public static class FileAssert
        {
            static string GetFileHash(string filename)
            {
                Assert.IsTrue(File.Exists(filename));

                using (var hash = new SHA1Managed())
                {
                    var clearBytes = File.ReadAllBytes(filename);
                    var hashedBytes = hash.ComputeHash(clearBytes);
                    return ConvertBytesToHex(hashedBytes);
                }
            }

            static string ConvertBytesToHex(byte[] bytes)
            {
                var sb = new StringBuilder();

                for (var i = 0; i < bytes.Length; i++)
                {
                    sb.Append(bytes[i].ToString("x"));
                }
                return sb.ToString();
            }

            public static void AreEqual(string filename1, string filename2)
            {
                string hash1 = GetFileHash(filename1);
                string hash2 = GetFileHash(filename2);

                Assert.AreEqual(hash1, hash2);
            }
        }
    }


### <a name="programming-interfaces-in-localrunhelperexe"></a><span data-ttu-id="4d867-328">Interfaces de programmation dans LocalRunHelper.exe</span><span class="sxs-lookup"><span data-stu-id="4d867-328">Programming interfaces in LocalRunHelper.exe</span></span>

<span data-ttu-id="4d867-329">LocalRunHelper.exe fournit les interfaces de programmation pour la compilation, l’exécution, etc. U-SQL locales. Les interfaces sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="4d867-329">LocalRunHelper.exe provides the programming interfaces for U-SQL local compile, run, etc. The interfaces are listed as follows.</span></span>

<span data-ttu-id="4d867-330">**Constructeur**</span><span class="sxs-lookup"><span data-stu-id="4d867-330">**Constructor**</span></span>

<span data-ttu-id="4d867-331">public LocalRunHelper([System.IO.TextWriter messageOutput = null])</span><span class="sxs-lookup"><span data-stu-id="4d867-331">public LocalRunHelper([System.IO.TextWriter messageOutput = null])</span></span>

|<span data-ttu-id="4d867-332">Paramètre</span><span class="sxs-lookup"><span data-stu-id="4d867-332">Parameter</span></span>|<span data-ttu-id="4d867-333">Type</span><span class="sxs-lookup"><span data-stu-id="4d867-333">Type</span></span>|<span data-ttu-id="4d867-334">Description</span><span class="sxs-lookup"><span data-stu-id="4d867-334">Description</span></span>|
|---------|----|-----------|
|<span data-ttu-id="4d867-335">messageOutput</span><span class="sxs-lookup"><span data-stu-id="4d867-335">messageOutput</span></span>|<span data-ttu-id="4d867-336">System.IO.TextWriter</span><span class="sxs-lookup"><span data-stu-id="4d867-336">System.IO.TextWriter</span></span>|<span data-ttu-id="4d867-337">pour les messages de sortie, donner la valeur null pour utiliser la Console</span><span class="sxs-lookup"><span data-stu-id="4d867-337">for output messages, set to null to use Console</span></span>|

<span data-ttu-id="4d867-338">**Propriétés**</span><span class="sxs-lookup"><span data-stu-id="4d867-338">**Properties**</span></span>

|<span data-ttu-id="4d867-339">Propriété</span><span class="sxs-lookup"><span data-stu-id="4d867-339">Property</span></span>|<span data-ttu-id="4d867-340">Type</span><span class="sxs-lookup"><span data-stu-id="4d867-340">Type</span></span>|<span data-ttu-id="4d867-341">Description</span><span class="sxs-lookup"><span data-stu-id="4d867-341">Description</span></span>|
|--------|----|-----------|
|<span data-ttu-id="4d867-342">AlgebraPath</span><span class="sxs-lookup"><span data-stu-id="4d867-342">AlgebraPath</span></span>|<span data-ttu-id="4d867-343">string</span><span class="sxs-lookup"><span data-stu-id="4d867-343">string</span></span>|<span data-ttu-id="4d867-344">Chemin d’accès du fichier d’algèbre (le fichier d’algèbre est un des résultats de la compilation)</span><span class="sxs-lookup"><span data-stu-id="4d867-344">The path to algebra file (algebra file is one of the compilation results)</span></span>|
|<span data-ttu-id="4d867-345">CodeBehindReferences</span><span class="sxs-lookup"><span data-stu-id="4d867-345">CodeBehindReferences</span></span>|<span data-ttu-id="4d867-346">string</span><span class="sxs-lookup"><span data-stu-id="4d867-346">string</span></span>|<span data-ttu-id="4d867-347">Si le script a des références code-behind supplémentaires, spécifiez les chemins d’accès séparés par « ; »</span><span class="sxs-lookup"><span data-stu-id="4d867-347">If the script has additional code behind references, specify the paths separated with ';'</span></span>|
|<span data-ttu-id="4d867-348">CppSdkDir</span><span class="sxs-lookup"><span data-stu-id="4d867-348">CppSdkDir</span></span>|<span data-ttu-id="4d867-349">string</span><span class="sxs-lookup"><span data-stu-id="4d867-349">string</span></span>|<span data-ttu-id="4d867-350">Répertoire CppSDK</span><span class="sxs-lookup"><span data-stu-id="4d867-350">CppSDK directory</span></span>|
|<span data-ttu-id="4d867-351">CurrentDir</span><span class="sxs-lookup"><span data-stu-id="4d867-351">CurrentDir</span></span>|<span data-ttu-id="4d867-352">string</span><span class="sxs-lookup"><span data-stu-id="4d867-352">string</span></span>|<span data-ttu-id="4d867-353">Répertoire actif</span><span class="sxs-lookup"><span data-stu-id="4d867-353">Current directory</span></span>|
|<span data-ttu-id="4d867-354">DataRoot</span><span class="sxs-lookup"><span data-stu-id="4d867-354">DataRoot</span></span>|<span data-ttu-id="4d867-355">string</span><span class="sxs-lookup"><span data-stu-id="4d867-355">string</span></span>|<span data-ttu-id="4d867-356">Chemin d’accès de la racine de données</span><span class="sxs-lookup"><span data-stu-id="4d867-356">Data root path</span></span>|
|<span data-ttu-id="4d867-357">DebuggerMailPath</span><span class="sxs-lookup"><span data-stu-id="4d867-357">DebuggerMailPath</span></span>|<span data-ttu-id="4d867-358">string</span><span class="sxs-lookup"><span data-stu-id="4d867-358">string</span></span>|<span data-ttu-id="4d867-359">Chemin d’accès du port d’insertion/éjection du débogueur</span><span class="sxs-lookup"><span data-stu-id="4d867-359">The path to debugger mailslot</span></span>|
|<span data-ttu-id="4d867-360">GenerateUdoRedirect</span><span class="sxs-lookup"><span data-stu-id="4d867-360">GenerateUdoRedirect</span></span>|<span data-ttu-id="4d867-361">valeur booléenne</span><span class="sxs-lookup"><span data-stu-id="4d867-361">bool</span></span>|<span data-ttu-id="4d867-362">Si vous souhaitez générer une configuration de remplacement de redirection de chargement d’assembly</span><span class="sxs-lookup"><span data-stu-id="4d867-362">If we want to generate assembly loading redirection override config</span></span>|
|<span data-ttu-id="4d867-363">HasCodeBehind</span><span class="sxs-lookup"><span data-stu-id="4d867-363">HasCodeBehind</span></span>|<span data-ttu-id="4d867-364">valeur booléenne</span><span class="sxs-lookup"><span data-stu-id="4d867-364">bool</span></span>|<span data-ttu-id="4d867-365">Si le script a du code-behind</span><span class="sxs-lookup"><span data-stu-id="4d867-365">If the script has code behind</span></span>|
|<span data-ttu-id="4d867-366">InputDir</span><span class="sxs-lookup"><span data-stu-id="4d867-366">InputDir</span></span>|<span data-ttu-id="4d867-367">string</span><span class="sxs-lookup"><span data-stu-id="4d867-367">string</span></span>|<span data-ttu-id="4d867-368">Répertoire des données d’entrée</span><span class="sxs-lookup"><span data-stu-id="4d867-368">Directory for input data</span></span>|
|<span data-ttu-id="4d867-369">MessagePath</span><span class="sxs-lookup"><span data-stu-id="4d867-369">MessagePath</span></span>|<span data-ttu-id="4d867-370">string</span><span class="sxs-lookup"><span data-stu-id="4d867-370">string</span></span>|<span data-ttu-id="4d867-371">Chemin d’accès du fichier de vidage des messages</span><span class="sxs-lookup"><span data-stu-id="4d867-371">Message dump file path</span></span>|
|<span data-ttu-id="4d867-372">OutputDir</span><span class="sxs-lookup"><span data-stu-id="4d867-372">OutputDir</span></span>|<span data-ttu-id="4d867-373">string</span><span class="sxs-lookup"><span data-stu-id="4d867-373">string</span></span>|<span data-ttu-id="4d867-374">Répertoire des données de sortie</span><span class="sxs-lookup"><span data-stu-id="4d867-374">Directory for output data</span></span>|
|<span data-ttu-id="4d867-375">Parallélisme</span><span class="sxs-lookup"><span data-stu-id="4d867-375">Parallelism</span></span>|<span data-ttu-id="4d867-376">int</span><span class="sxs-lookup"><span data-stu-id="4d867-376">int</span></span>|<span data-ttu-id="4d867-377">Parallélisme pour exécuter l’algèbre</span><span class="sxs-lookup"><span data-stu-id="4d867-377">Parallelism to run the algebra</span></span>|
|<span data-ttu-id="4d867-378">ParentPid</span><span class="sxs-lookup"><span data-stu-id="4d867-378">ParentPid</span></span>|<span data-ttu-id="4d867-379">int</span><span class="sxs-lookup"><span data-stu-id="4d867-379">int</span></span>|<span data-ttu-id="4d867-380">PID du parent que le service surveille pour quitter, donner la valeur 0 ou une valeur négative pour ignorer</span><span class="sxs-lookup"><span data-stu-id="4d867-380">PID of the parent on which the service monitors to exit, set to 0 or negative to ignore</span></span>|
|<span data-ttu-id="4d867-381">ResultPath</span><span class="sxs-lookup"><span data-stu-id="4d867-381">ResultPath</span></span>|<span data-ttu-id="4d867-382">string</span><span class="sxs-lookup"><span data-stu-id="4d867-382">string</span></span>|<span data-ttu-id="4d867-383">Chemin d’accès du fichier de vidage des résultats</span><span class="sxs-lookup"><span data-stu-id="4d867-383">Result dump file path</span></span>|
|<span data-ttu-id="4d867-384">RuntimeDir</span><span class="sxs-lookup"><span data-stu-id="4d867-384">RuntimeDir</span></span>|<span data-ttu-id="4d867-385">string</span><span class="sxs-lookup"><span data-stu-id="4d867-385">string</span></span>|<span data-ttu-id="4d867-386">Répertoire du runtime</span><span class="sxs-lookup"><span data-stu-id="4d867-386">Runtime directory</span></span>|
|<span data-ttu-id="4d867-387">ScriptPath</span><span class="sxs-lookup"><span data-stu-id="4d867-387">ScriptPath</span></span>|<span data-ttu-id="4d867-388">string</span><span class="sxs-lookup"><span data-stu-id="4d867-388">string</span></span>|<span data-ttu-id="4d867-389">Emplacement du script</span><span class="sxs-lookup"><span data-stu-id="4d867-389">Where to find the script</span></span>|
|<span data-ttu-id="4d867-390">Shallow</span><span class="sxs-lookup"><span data-stu-id="4d867-390">Shallow</span></span>|<span data-ttu-id="4d867-391">valeur booléenne</span><span class="sxs-lookup"><span data-stu-id="4d867-391">bool</span></span>|<span data-ttu-id="4d867-392">Compilation superficielle ou non</span><span class="sxs-lookup"><span data-stu-id="4d867-392">Shallow compile or not</span></span>|
|<span data-ttu-id="4d867-393">TempDir</span><span class="sxs-lookup"><span data-stu-id="4d867-393">TempDir</span></span>|<span data-ttu-id="4d867-394">string</span><span class="sxs-lookup"><span data-stu-id="4d867-394">string</span></span>|<span data-ttu-id="4d867-395">Répertoire Temp</span><span class="sxs-lookup"><span data-stu-id="4d867-395">Temp directory</span></span>|
|<span data-ttu-id="4d867-396">UseDataBase</span><span class="sxs-lookup"><span data-stu-id="4d867-396">UseDataBase</span></span>|<span data-ttu-id="4d867-397">string</span><span class="sxs-lookup"><span data-stu-id="4d867-397">string</span></span>|<span data-ttu-id="4d867-398">Spécifiez la base de données à utiliser pour l’inscription des assemblys temporaires du code-behind, MASTER par défaut</span><span class="sxs-lookup"><span data-stu-id="4d867-398">Specify the database to use for code behind temporary assembly registration, master by default</span></span>|
|<span data-ttu-id="4d867-399">WorkDir</span><span class="sxs-lookup"><span data-stu-id="4d867-399">WorkDir</span></span>|<span data-ttu-id="4d867-400">string</span><span class="sxs-lookup"><span data-stu-id="4d867-400">string</span></span>|<span data-ttu-id="4d867-401">Répertoire de travail favori</span><span class="sxs-lookup"><span data-stu-id="4d867-401">Preferred working directory</span></span>|


<span data-ttu-id="4d867-402">**Méthode**</span><span class="sxs-lookup"><span data-stu-id="4d867-402">**Method**</span></span>

|<span data-ttu-id="4d867-403">Méthode</span><span class="sxs-lookup"><span data-stu-id="4d867-403">Method</span></span>|<span data-ttu-id="4d867-404">Description</span><span class="sxs-lookup"><span data-stu-id="4d867-404">Description</span></span>|<span data-ttu-id="4d867-405">Renvoie</span><span class="sxs-lookup"><span data-stu-id="4d867-405">Return</span></span>|<span data-ttu-id="4d867-406">Paramètre</span><span class="sxs-lookup"><span data-stu-id="4d867-406">Parameter</span></span>|
|------|-----------|------|---------|
|<span data-ttu-id="4d867-407">public bool DoCompile()</span><span class="sxs-lookup"><span data-stu-id="4d867-407">public bool DoCompile()</span></span>|<span data-ttu-id="4d867-408">Compilation du script U-SQL</span><span class="sxs-lookup"><span data-stu-id="4d867-408">Compile the U-SQL script</span></span>|<span data-ttu-id="4d867-409">True en cas de réussite</span><span class="sxs-lookup"><span data-stu-id="4d867-409">True on success</span></span>| |
|<span data-ttu-id="4d867-410">public bool DoExec()</span><span class="sxs-lookup"><span data-stu-id="4d867-410">public bool DoExec()</span></span>|<span data-ttu-id="4d867-411">Exécution du résultat compilé</span><span class="sxs-lookup"><span data-stu-id="4d867-411">Execute the compiled result</span></span>|<span data-ttu-id="4d867-412">True en cas de réussite</span><span class="sxs-lookup"><span data-stu-id="4d867-412">True on success</span></span>| |
|<span data-ttu-id="4d867-413">public bool DoRun()</span><span class="sxs-lookup"><span data-stu-id="4d867-413">public bool DoRun()</span></span>|<span data-ttu-id="4d867-414">Lancement du script U-SQL (compile + execute)</span><span class="sxs-lookup"><span data-stu-id="4d867-414">Run the U-SQL script (Compile + Execute)</span></span>|<span data-ttu-id="4d867-415">True en cas de réussite</span><span class="sxs-lookup"><span data-stu-id="4d867-415">True on success</span></span>| |
|<span data-ttu-id="4d867-416">public bool IsValidRuntimeDir(string chemin-d’accès)</span><span class="sxs-lookup"><span data-stu-id="4d867-416">public bool IsValidRuntimeDir(string path)</span></span>|<span data-ttu-id="4d867-417">Vérification de la validité du chemin d’accès du runtime fourni</span><span class="sxs-lookup"><span data-stu-id="4d867-417">Check if the given path is valid runtime path</span></span>|<span data-ttu-id="4d867-418">True en cas de validité</span><span class="sxs-lookup"><span data-stu-id="4d867-418">True for valid</span></span>|<span data-ttu-id="4d867-419">Chemin d’accès du répertoire du runtime</span><span class="sxs-lookup"><span data-stu-id="4d867-419">The path of runtime directory</span></span>|


## <a name="faq-about-common-issue"></a><span data-ttu-id="4d867-420">FAQ sur les problèmes courants</span><span class="sxs-lookup"><span data-stu-id="4d867-420">FAQ about common issue</span></span>

### <a name="error-1"></a><span data-ttu-id="4d867-421">Erreur 1 :</span><span class="sxs-lookup"><span data-stu-id="4d867-421">Error 1:</span></span>
<span data-ttu-id="4d867-422">E_CSC_SYSTEM_INTERNAL : Erreur interne !</span><span class="sxs-lookup"><span data-stu-id="4d867-422">E_CSC_SYSTEM_INTERNAL: Internal error!</span></span> <span data-ttu-id="4d867-423">Impossible de charger le fichier ou l’assembly « ScopeEngineManaged.dll » ou une de ses dépendances.</span><span class="sxs-lookup"><span data-stu-id="4d867-423">Could not load file or assembly 'ScopeEngineManaged.dll' or one of its dependencies.</span></span> <span data-ttu-id="4d867-424">Le module spécifié est introuvable.</span><span class="sxs-lookup"><span data-stu-id="4d867-424">The specified module could not be found.</span></span>

<span data-ttu-id="4d867-425">Vérifiez les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="4d867-425">Please check the following:</span></span>

- <span data-ttu-id="4d867-426">Assurez-vous que vous avez un environnement x64.</span><span class="sxs-lookup"><span data-stu-id="4d867-426">Make sure you have x64 environment.</span></span> <span data-ttu-id="4d867-427">La plateforme cible de build et de l’environnement de test doit être x64. Consultez la section **Étape 1 : Créer une configuration et un projet de test unitaire C#** ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="4d867-427">The build target platform and the test environment should be x64, refer to **Step 1: Create C# unit test project and configuration** above.</span></span>
- <span data-ttu-id="4d867-428">Vérifiez que vous avez copié tous les fichiers de dépendance sous NugetPackage\build\runtime\ dans le répertoire de travail du projet.</span><span class="sxs-lookup"><span data-stu-id="4d867-428">Make sure you have copied all dependency files under NugetPackage\build\runtime\ to project working directory.</span></span>


## <a name="next-steps"></a><span data-ttu-id="4d867-429">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4d867-429">Next steps</span></span>

* <span data-ttu-id="4d867-430">Pour connaître U-SQL, voir [Prise en main du langage U-SQL d’Analytique Data Lake Azure](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="4d867-430">To learn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
* <span data-ttu-id="4d867-431">Pour consigner les informations de diagnostic, voir [Accès aux journaux de diagnostic d’Azure Data Lake Analytics](data-lake-analytics-diagnostic-logs.md).</span><span class="sxs-lookup"><span data-stu-id="4d867-431">To log diagnostics information, see [Accessing diagnostics logs for Azure Data Lake Analytics](data-lake-analytics-diagnostic-logs.md).</span></span>
* <span data-ttu-id="4d867-432">Pour consulter une requête plus complexe, voir [Analyse de journaux des sites web à l’aide d’Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="4d867-432">To see a more complex query, see [Analyze website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="4d867-433">Pour afficher les détails d’un travail, voir [Utilisation de l’Explorateur de travaux et de la Vue des travaux pour les travaux Azure Data Lake Analytics](data-lake-analytics-data-lake-tools-view-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="4d867-433">To view job details, see [Use Job Browser and Job View for Azure Data Lake Analytics jobs](data-lake-analytics-data-lake-tools-view-jobs.md).</span></span>
* <span data-ttu-id="4d867-434">Pour utiliser la vue d’exécution du vertex, voir [Utilisation de la vue d’exécution du vertex dans Data Lake Tools pour Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).</span><span class="sxs-lookup"><span data-stu-id="4d867-434">To use the vertex execution view, see [Use the Vertex Execution View in Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).</span></span>
