---
title: "aaaScale U-SQL local exécuter et tester avec le Kit de développement logiciel Azure données Lake U-SQL | Documents Microsoft"
description: "Découvrez comment les travaux de tooscale U-SQL de SQL-U de LAC de données Azure SDK toouse local exécute et de test avec la ligne de commande et les interfaces de programmation sur votre station de travail locale."
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
ms.openlocfilehash: 2b0a16229789268e333f723ff6fc2c3efdc29905
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-u-sql-local-run-and-test-with-azure-data-lake-u-sql-sdk"></a><span data-ttu-id="184e9-103">Mettre à l’échelle l’exécution et les tests U-SQL locaux avec le kit SDK Azure Data Lake U-SQL</span><span class="sxs-lookup"><span data-stu-id="184e9-103">Scale U-SQL local run and test with Azure Data Lake U-SQL SDK</span></span>

<span data-ttu-id="184e9-104">Lors du développement de script U-SQL, il est commun toorun et le script de test U-SQL localement soumet avant toocloud.</span><span class="sxs-lookup"><span data-stu-id="184e9-104">When developing U-SQL script, it is common toorun and test U-SQL script locally before submit it toocloud.</span></span> <span data-ttu-id="184e9-105">Azure Data Lake fournit un package NuGet appelé Kit SDK SQL Azure Data Lake U-SQL pour ce scénario, par le biais duquel vous pouvez facilement mettre à l’échelle l’exécution et les tests U-SQL locaux.</span><span class="sxs-lookup"><span data-stu-id="184e9-105">Azure Data Lake provides a Nuget package called Azure Data Lake U-SQL SDK for this scenario, through which you can easily scale U-SQL local run and test.</span></span> <span data-ttu-id="184e9-106">Il est également possible de toointegrate cette U-SQL de test avec l’élément de configuration (intégration continue) système tooautomate hello compiler et tester.</span><span class="sxs-lookup"><span data-stu-id="184e9-106">It is also possible toointegrate this U-SQL test with CI (Continuous Integration) system tooautomate hello compile and test.</span></span>

<span data-ttu-id="184e9-107">Si vous vous souciez comment toomanually local exécuter et déboguer le script U-SQL avec les outils de l’interface utilisateur graphique, vous pouvez ensuite utiliser Azure Data Lake Tools pour Visual Studio pour que.</span><span class="sxs-lookup"><span data-stu-id="184e9-107">If you care about how toomanually local run and debug U-SQL script with GUI tooling, then you can use Azure Data Lake Tools for Visual Studio for that.</span></span> <span data-ttu-id="184e9-108">Pour plus d’informations, cliquez [ici](data-lake-analytics-data-lake-tools-local-run.md).</span><span class="sxs-lookup"><span data-stu-id="184e9-108">You can learn more from [here](data-lake-analytics-data-lake-tools-local-run.md).</span></span>

## <a name="install-azure-data-lake-u-sql-sdk"></a><span data-ttu-id="184e9-109">Installer le Kit SDK Azure Data Lake U-SQL</span><span class="sxs-lookup"><span data-stu-id="184e9-109">Install Azure Data Lake U-SQL SDK</span></span>

<span data-ttu-id="184e9-110">Vous pouvez obtenir hello SQL-U de LAC de données Azure SDK [ici](https://www.nuget.org/packages/Microsoft.Azure.DataLake.USQL.SDK/) sur Nuget.org. Et avant de l’utiliser, vous devez toomake que vous disposez des dépendances comme suit.</span><span class="sxs-lookup"><span data-stu-id="184e9-110">You can get hello Azure Data Lake U-SQL SDK [here](https://www.nuget.org/packages/Microsoft.Azure.DataLake.USQL.SDK/) on Nuget.org. And before using it, you need toomake sure you have dependencies as follows.</span></span>

### <a name="dependencies"></a><span data-ttu-id="184e9-111">Dépendances</span><span class="sxs-lookup"><span data-stu-id="184e9-111">Dependencies</span></span>

<span data-ttu-id="184e9-112">Hello données Lake U-SQL SDK nécessite hello suivant des dépendances :</span><span class="sxs-lookup"><span data-stu-id="184e9-112">hello Data Lake U-SQL SDK requires hello following dependencies:</span></span>

- <span data-ttu-id="184e9-113">[Microsoft .NET Framework 4.6 ou une version ultérieure](https://www.microsoft.com/download/details.aspx?id=17851).</span><span class="sxs-lookup"><span data-stu-id="184e9-113">[Microsoft .NET Framework 4.6 or newer](https://www.microsoft.com/download/details.aspx?id=17851).</span></span>
- <span data-ttu-id="184e9-114">Microsoft Visual C++ 14 et le Kit SDK Windows 10.0.10240.0 ou une version plus récente (appelé CppSDK dans cet article).</span><span class="sxs-lookup"><span data-stu-id="184e9-114">Microsoft Visual C++ 14 and Windows SDK 10.0.10240.0 or newer (which is called CppSDK in this article).</span></span> <span data-ttu-id="184e9-115">Il existe deux façons tooget CppSDK :</span><span class="sxs-lookup"><span data-stu-id="184e9-115">There are two ways tooget CppSDK:</span></span>

    - <span data-ttu-id="184e9-116">Installez [Visual Studio Community Edition](https://developer.microsoft.com/downloads/vs-thankyou).</span><span class="sxs-lookup"><span data-stu-id="184e9-116">Install [Visual Studio Community Edition](https://developer.microsoft.com/downloads/vs-thankyou).</span></span> <span data-ttu-id="184e9-117">Vous avez un dossier \Windows Kits\10 sous le dossier Program Files hello : par exemple, C:\Program Files (x86) \Windows Kits\10\.</span><span class="sxs-lookup"><span data-stu-id="184e9-117">You'll have a \Windows Kits\10 folder under hello Program Files folder--for example, C:\Program Files (x86)\Windows Kits\10\.</span></span> <span data-ttu-id="184e9-118">Vous trouverez également la version du SDK Windows 10 hello sous \Windows Kits\10\Lib.</span><span class="sxs-lookup"><span data-stu-id="184e9-118">You'll also find hello Windows 10 SDK version under \Windows Kits\10\Lib.</span></span> <span data-ttu-id="184e9-119">Si vous ne voyez pas ces dossiers, réinstallez Visual Studio et que tooselect hello SDK Windows 10 lors de l’installation de hello.</span><span class="sxs-lookup"><span data-stu-id="184e9-119">If you don’t see these folders, reinstall Visual Studio and be sure tooselect hello Windows 10 SDK during hello installation.</span></span> <span data-ttu-id="184e9-120">Si vous avez cela installé avec Visual Studio, compilateur local de hello U-SQL se trouve automatiquement.</span><span class="sxs-lookup"><span data-stu-id="184e9-120">If you have this installed with Visual Studio, hello U-SQL local compiler will find it automatically.</span></span>

    ![Data Lake Tools pour Visual Studio exécution locale Windows 10 SDK](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-windows-10-sdk.png)

    - <span data-ttu-id="184e9-122">Installez [Data Lake Tools for Visual Studio](http://aka.ms/adltoolsvs).</span><span class="sxs-lookup"><span data-stu-id="184e9-122">Install [Data Lake Tools for Visual Studio](http://aka.ms/adltoolsvs).</span></span> <span data-ttu-id="184e9-123">Vous pouvez trouver des fichiers Visual C++ et le Kit de développement à l’emplacement C:\Program Files (x86) \Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Microsoft\ADL Tools\X.X.XXXX.X\CppSDK en préemballages hello.</span><span class="sxs-lookup"><span data-stu-id="184e9-123">You can find hello prepackaged Visual C++ and Windows SDK files at C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Microsoft\ADL Tools\X.X.XXXX.X\CppSDK.</span></span> <span data-ttu-id="184e9-124">Dans ce cas, compilateur local de hello U-SQL ne peut pas rechercher des dépendances de hello automatiquement.</span><span class="sxs-lookup"><span data-stu-id="184e9-124">In this case, hello U-SQL local compiler cannot find hello dependencies automatically.</span></span> <span data-ttu-id="184e9-125">Vous devez le chemin d’accès CppSDK toospecify hello pour celle-ci.</span><span class="sxs-lookup"><span data-stu-id="184e9-125">You need toospecify hello CppSDK path for it.</span></span> <span data-ttu-id="184e9-126">Vous pouvez copier l’emplacement des fichiers de tooanother hello ou utiliser tel quel.</span><span class="sxs-lookup"><span data-stu-id="184e9-126">You can either copy hello files tooanother location or use it as is.</span></span>

## <a name="understand-basic-concepts"></a><span data-ttu-id="184e9-127">Comprendre les concepts de base</span><span class="sxs-lookup"><span data-stu-id="184e9-127">Understand basic concepts</span></span>

### <a name="data-root"></a><span data-ttu-id="184e9-128">Racine de données</span><span class="sxs-lookup"><span data-stu-id="184e9-128">Data root</span></span>

<span data-ttu-id="184e9-129">dossier de données racine de Hello est un « magasin local » pour le compte de calcul local hello.</span><span class="sxs-lookup"><span data-stu-id="184e9-129">hello data-root folder is a "local store" for hello local compute account.</span></span> <span data-ttu-id="184e9-130">Il est le compte d’Azure Data Lake Store toohello équivalent d’un compte Analytique lac de données.</span><span class="sxs-lookup"><span data-stu-id="184e9-130">It's equivalent toohello Azure Data Lake Store account of a Data Lake Analytics account.</span></span> <span data-ttu-id="184e9-131">Dossier de données-racine différent tooa de commutation est identique à commutation tooa autre banque de compte.</span><span class="sxs-lookup"><span data-stu-id="184e9-131">Switching tooa different data-root folder is just like switching tooa different store account.</span></span> <span data-ttu-id="184e9-132">Si vous souhaitez tooaccess fréquemment les données partagées avec des dossiers racine de données différents, vous devez utiliser des chemins d’accès absolus dans vos scripts.</span><span class="sxs-lookup"><span data-stu-id="184e9-132">If you want tooaccess commonly shared data with different data-root folders, you must use absolute paths in your scripts.</span></span> <span data-ttu-id="184e9-133">Ou bien, créez des liens symboliques de système de fichier (par exemple, **mklink** sur NTFS) sous hello racine de données dossier toopoint toohello les données partagées.</span><span class="sxs-lookup"><span data-stu-id="184e9-133">Or, create file system symbolic links (for example, **mklink** on NTFS) under hello data-root folder toopoint toohello shared data.</span></span>

<span data-ttu-id="184e9-134">dossier de données racine Hello est utilisé pour :</span><span class="sxs-lookup"><span data-stu-id="184e9-134">hello data-root folder is used to:</span></span>

- <span data-ttu-id="184e9-135">Stocker les métadonnées locales, notamment des bases de données, des tables, des fonctions table (TVF) et des assemblys.</span><span class="sxs-lookup"><span data-stu-id="184e9-135">Store local metadata, including databases, tables, table-valued functions (TVFs), and assemblies.</span></span>
- <span data-ttu-id="184e9-136">Rechercher hello d’entrée et les chemins d’accès de sortie sont définies comme des chemins d’accès relatifs dans U-SQL.</span><span class="sxs-lookup"><span data-stu-id="184e9-136">Look up hello input and output paths that are defined as relative paths in U-SQL.</span></span> <span data-ttu-id="184e9-137">À l’aide de chemins d’accès relatifs rend plus facile toodeploy votre tooAzure de projets U-SQL.</span><span class="sxs-lookup"><span data-stu-id="184e9-137">Using relative paths makes it easier toodeploy your U-SQL projects tooAzure.</span></span>

### <a name="file-path-in-u-sql"></a><span data-ttu-id="184e9-138">Chemin d’accès des fichiers dans U-SQL</span><span class="sxs-lookup"><span data-stu-id="184e9-138">File path in U-SQL</span></span>

<span data-ttu-id="184e9-139">Vous pouvez utiliser un chemin d’accès relatif et un chemin d’accès absolu local dans des scripts SQL-U.</span><span class="sxs-lookup"><span data-stu-id="184e9-139">You can use both a relative path and a local absolute path in U-SQL scripts.</span></span> <span data-ttu-id="184e9-140">chemin d’accès relatif de Hello est le chemin d’accès au dossier toohello relatif racine de données spécifié.</span><span class="sxs-lookup"><span data-stu-id="184e9-140">hello relative path is relative toohello specified data-root folder path.</span></span> <span data-ttu-id="184e9-141">Il est recommandé que vous utilisez « / » comme hello toomake de séparateur de chemin d’accès de vos scripts compatibles avec SSI hello.</span><span class="sxs-lookup"><span data-stu-id="184e9-141">We recommend that you use "/" as hello path separator toomake your scripts compatible with hello server side.</span></span> <span data-ttu-id="184e9-142">Voici quelques exemples de chemins relatifs, avec leurs chemins absolus équivalents.</span><span class="sxs-lookup"><span data-stu-id="184e9-142">Here are some examples of relative paths and their equivalent absolute paths.</span></span> <span data-ttu-id="184e9-143">Dans ces exemples, C:\LocalRunDataRoot est le dossier racine de données de hello.</span><span class="sxs-lookup"><span data-stu-id="184e9-143">In these examples, C:\LocalRunDataRoot is hello data-root folder.</span></span>

|<span data-ttu-id="184e9-144">Chemin relatif</span><span class="sxs-lookup"><span data-stu-id="184e9-144">Relative path</span></span>|<span data-ttu-id="184e9-145">Chemin absolu</span><span class="sxs-lookup"><span data-stu-id="184e9-145">Absolute path</span></span>|
|-------------|-------------|
|<span data-ttu-id="184e9-146">/abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="184e9-146">/abc/def/input.csv</span></span> |<span data-ttu-id="184e9-147">C:\LocalRunDataRoot\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="184e9-147">C:\LocalRunDataRoot\abc\def\input.csv</span></span>|
|<span data-ttu-id="184e9-148">abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="184e9-148">abc/def/input.csv</span></span>  |<span data-ttu-id="184e9-149">C:\LocalRunDataRoot\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="184e9-149">C:\LocalRunDataRoot\abc\def\input.csv</span></span>|
|<span data-ttu-id="184e9-150">D:/abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="184e9-150">D:/abc/def/input.csv</span></span> |<span data-ttu-id="184e9-151">D:\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="184e9-151">D:\abc\def\input.csv</span></span>|

### <a name="working-directory"></a><span data-ttu-id="184e9-152">Répertoire de travail</span><span class="sxs-lookup"><span data-stu-id="184e9-152">Working directory</span></span>

<span data-ttu-id="184e9-153">Lorsque vous exécutez le script de hello U-SQL localement, un répertoire de travail est créé lors de la compilation sous le répertoire en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="184e9-153">When running hello U-SQL script locally, a working directory is created during compilation under current running directory.</span></span> <span data-ttu-id="184e9-154">En outre toohello compilation génère, hello nécessitent des fichiers d’exécution pour une exécution locale sera répertoire de travail copié toothis de clichés instantanés.</span><span class="sxs-lookup"><span data-stu-id="184e9-154">In addition toohello compilation outputs, hello needed runtime files for local execution will be shadow copied toothis working directory.</span></span> <span data-ttu-id="184e9-155">Hello dossier racine de répertoire de travail est appelé « ScopeWorkDir » et les fichiers hello sous le répertoire de travail de hello sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="184e9-155">hello working directory root folder is called "ScopeWorkDir" and hello files under hello working directory are as follows:</span></span>

|<span data-ttu-id="184e9-156">Répertoire/fichier</span><span class="sxs-lookup"><span data-stu-id="184e9-156">Directory/file</span></span>|<span data-ttu-id="184e9-157">Répertoire/fichier</span><span class="sxs-lookup"><span data-stu-id="184e9-157">Directory/file</span></span>|<span data-ttu-id="184e9-158">Répertoire/fichier</span><span class="sxs-lookup"><span data-stu-id="184e9-158">Directory/file</span></span>|<span data-ttu-id="184e9-159">Définition</span><span class="sxs-lookup"><span data-stu-id="184e9-159">Definition</span></span>|<span data-ttu-id="184e9-160">Description</span><span class="sxs-lookup"><span data-stu-id="184e9-160">Description</span></span>|
|--------------|--------------|--------------|----------|-----------|
|<span data-ttu-id="184e9-161">C6A101DDCB470506</span><span class="sxs-lookup"><span data-stu-id="184e9-161">C6A101DDCB470506</span></span>| | |<span data-ttu-id="184e9-162">Chaîne de hachage de la version exécutable</span><span class="sxs-lookup"><span data-stu-id="184e9-162">Hash string of runtime version</span></span>|<span data-ttu-id="184e9-163">Cliché instantané des fichiers exécutables nécessaires à l'exécution locale</span><span class="sxs-lookup"><span data-stu-id="184e9-163">Shadow copy of runtime files needed for local execution</span></span>|
| |<span data-ttu-id="184e9-164">Script_66AE4909AA0ED06C</span><span class="sxs-lookup"><span data-stu-id="184e9-164">Script_66AE4909AA0ED06C</span></span>| |<span data-ttu-id="184e9-165">Nom de script + chaîne de hachage du chemin du script</span><span class="sxs-lookup"><span data-stu-id="184e9-165">Script name + hash string of script path</span></span>|<span data-ttu-id="184e9-166">Résultats de la compilation et journalisation des étapes d'exécution</span><span class="sxs-lookup"><span data-stu-id="184e9-166">Compilation outputs and execution step logging</span></span>|
| | |<span data-ttu-id="184e9-167">\_script\_.abr</span><span class="sxs-lookup"><span data-stu-id="184e9-167">\_script\_.abr</span></span>|<span data-ttu-id="184e9-168">Sortie du compilateur</span><span class="sxs-lookup"><span data-stu-id="184e9-168">Compiler output</span></span>|<span data-ttu-id="184e9-169">Fichier algèbre</span><span class="sxs-lookup"><span data-stu-id="184e9-169">Algebra file</span></span>|
| | |<span data-ttu-id="184e9-170">\_ScopeCodeGen\_.*</span><span class="sxs-lookup"><span data-stu-id="184e9-170">\_ScopeCodeGen\_.*</span></span>|<span data-ttu-id="184e9-171">Sortie du compilateur</span><span class="sxs-lookup"><span data-stu-id="184e9-171">Compiler output</span></span>|<span data-ttu-id="184e9-172">Code géré généré</span><span class="sxs-lookup"><span data-stu-id="184e9-172">Generated managed code</span></span>|
| | |<span data-ttu-id="184e9-173">\_ScopeCodeGenEngine\_.*</span><span class="sxs-lookup"><span data-stu-id="184e9-173">\_ScopeCodeGenEngine\_.*</span></span>|<span data-ttu-id="184e9-174">Sortie du compilateur</span><span class="sxs-lookup"><span data-stu-id="184e9-174">Compiler output</span></span>|<span data-ttu-id="184e9-175">Code natif généré</span><span class="sxs-lookup"><span data-stu-id="184e9-175">Generated native code</span></span>|
| | |<span data-ttu-id="184e9-176">referenced assemblies</span><span class="sxs-lookup"><span data-stu-id="184e9-176">referenced assemblies</span></span>|<span data-ttu-id="184e9-177">Référence d’assembly</span><span class="sxs-lookup"><span data-stu-id="184e9-177">Assembly reference</span></span>|<span data-ttu-id="184e9-178">Fichiers d’assemblys de référence</span><span class="sxs-lookup"><span data-stu-id="184e9-178">Referenced assembly files</span></span>|
| | |<span data-ttu-id="184e9-179">deployed_resources</span><span class="sxs-lookup"><span data-stu-id="184e9-179">deployed_resources</span></span>|<span data-ttu-id="184e9-180">Déploiement de ressources</span><span class="sxs-lookup"><span data-stu-id="184e9-180">Resource deployment</span></span>|<span data-ttu-id="184e9-181">Fichiers de déploiement de ressources</span><span class="sxs-lookup"><span data-stu-id="184e9-181">Resource deployment files</span></span>|
| | |<span data-ttu-id="184e9-182">xxxxxxxx.xxx[1..n]\_\*.*</span><span class="sxs-lookup"><span data-stu-id="184e9-182">xxxxxxxx.xxx[1..n]\_\*.*</span></span>|<span data-ttu-id="184e9-183">Journal d’exécution</span><span class="sxs-lookup"><span data-stu-id="184e9-183">Execution log</span></span>|<span data-ttu-id="184e9-184">Journal des étapes d'exécution</span><span class="sxs-lookup"><span data-stu-id="184e9-184">Log of execution steps</span></span>|


## <a name="use-hello-sdk-from-hello-command-line"></a><span data-ttu-id="184e9-185">Utilisez hello SDK à partir de la ligne de commande hello</span><span class="sxs-lookup"><span data-stu-id="184e9-185">Use hello SDK from hello command line</span></span>

### <a name="command-line-interface-of-hello-helper-application"></a><span data-ttu-id="184e9-186">Interface de ligne de commande de l’application d’assistance de hello</span><span class="sxs-lookup"><span data-stu-id="184e9-186">Command-line interface of hello helper application</span></span>

<span data-ttu-id="184e9-187">Sous directory\build\runtime du Kit de développement logiciel, LocalRunHelper.exe est hello d’assistance de ligne de commande qui fournit des fonctions de toomost Hello couramment utilisées et exécution locale d’interfaces.</span><span class="sxs-lookup"><span data-stu-id="184e9-187">Under SDK directory\build\runtime, LocalRunHelper.exe is hello command-line helper application that provides interfaces toomost of hello commonly used local-run functions.</span></span> <span data-ttu-id="184e9-188">Notez que les deux hello commande et les commutateurs d’arguments hello respectent la casse.</span><span class="sxs-lookup"><span data-stu-id="184e9-188">Note that both hello command and hello argument switches are case-sensitive.</span></span> <span data-ttu-id="184e9-189">tooinvoke il :</span><span class="sxs-lookup"><span data-stu-id="184e9-189">tooinvoke it:</span></span>

    LocalRunHelper.exe <command> <Required-Command-Arguments> [Optional-Command-Arguments]

<span data-ttu-id="184e9-190">Exécutez LocalRunHelper.exe sans argument ou avec hello **aide** passer les informations d’aide tooshow hello :</span><span class="sxs-lookup"><span data-stu-id="184e9-190">Run LocalRunHelper.exe without arguments or with hello **help** switch tooshow hello help information:</span></span>

    > LocalRunHelper.exe help

        Command 'help' :  Show usage information
        Command 'compile' :  Compile hello script
        Required Arguments :
            -Script param
                    Script File Path
        Optional Arguments :
            -Shallow [default value 'False']
                    Shallow compile

<span data-ttu-id="184e9-191">Informations d’aide dans hello :</span><span class="sxs-lookup"><span data-stu-id="184e9-191">In hello help information:</span></span>

-  <span data-ttu-id="184e9-192">**Commande** donne hello nom de la commande.</span><span class="sxs-lookup"><span data-stu-id="184e9-192">**Command** gives hello command’s name.</span></span>  
-  <span data-ttu-id="184e9-193">Le paramètre **Argument obligatoire** répertorie les arguments qui doivent être fournis.</span><span class="sxs-lookup"><span data-stu-id="184e9-193">**Required Argument** lists arguments that must be supplied.</span></span>  
-  <span data-ttu-id="184e9-194">Le paramètre **Argument facultatif** répertorie les arguments facultatifs, avec des valeurs par défaut.</span><span class="sxs-lookup"><span data-stu-id="184e9-194">**Optional Argument** lists arguments that are optional, with default values.</span></span>  <span data-ttu-id="184e9-195">Facultatif pour les arguments booléens n’ont pas les paramètres, et leur apparence signifie tootheir négatif par défaut.</span><span class="sxs-lookup"><span data-stu-id="184e9-195">Optional Boolean arguments don’t have parameters, and their appearances mean negative tootheir default value.</span></span>

### <a name="return-value-and-logging"></a><span data-ttu-id="184e9-196">Valeur de retour et journalisation</span><span class="sxs-lookup"><span data-stu-id="184e9-196">Return value and logging</span></span>

<span data-ttu-id="184e9-197">application d’assistance de Hello retourne **0** de réussite et **-1** de l’échec.</span><span class="sxs-lookup"><span data-stu-id="184e9-197">hello helper application returns **0** for success and **-1** for failure.</span></span> <span data-ttu-id="184e9-198">Par défaut, le programme d’assistance hello envoie console actuelle de tous les messages toohello.</span><span class="sxs-lookup"><span data-stu-id="184e9-198">By default, hello helper sends all messages toohello current console.</span></span> <span data-ttu-id="184e9-199">Toutefois, la plupart des commandes hello prennent en charge hello **-(messageout) chemin_vers_fichier_journal** argument facultatif qui redirige hello génère le fichier de journal tooa.</span><span class="sxs-lookup"><span data-stu-id="184e9-199">However, most of hello commands support hello **-MessageOut path_to_log_file** optional argument that redirects hello outputs tooa log file.</span></span>

### <a name="environment-variable-configuring"></a><span data-ttu-id="184e9-200">Configuration de la variable d’environnement</span><span class="sxs-lookup"><span data-stu-id="184e9-200">Environment variable configuring</span></span>

<span data-ttu-id="184e9-201">L’exécution U-SQL locale requiert une racine de données spécifiée comme compte de stockage local, ainsi qu’un chemin d’accès CppSDK spécifié pour les dépendances.</span><span class="sxs-lookup"><span data-stu-id="184e9-201">U-SQL local run needs a specified data root as local storage account, as well as a specified CppSDK path for dependencies.</span></span> <span data-ttu-id="184e9-202">Vous pouvez à la fois argument de hello défini dans la variable d’environnement de ligne de commande ou est définie pour eux.</span><span class="sxs-lookup"><span data-stu-id="184e9-202">You can both set hello argument in command-line or set environment variable for them.</span></span>

- <span data-ttu-id="184e9-203">Ensemble hello **SCOPE_CPP_SDK** variable d’environnement.</span><span class="sxs-lookup"><span data-stu-id="184e9-203">Set hello **SCOPE_CPP_SDK** environment variable.</span></span>

    <span data-ttu-id="184e9-204">Si vous obtenez Microsoft Visual C++ et hello Kit de développement logiciel Windows en installant Data Lake Tools pour Visual Studio, vérifiez que vous avez hello suivant du dossier :</span><span class="sxs-lookup"><span data-stu-id="184e9-204">If you get Microsoft Visual C++ and hello Windows SDK by installing Data Lake Tools for Visual Studio, verify that you have hello following folder:</span></span>

        C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Microsoft\Microsoft Azure Data Lake Tools for Visual Studio 2015\X.X.XXXX.X\CppSDK

    <span data-ttu-id="184e9-205">Définir une nouvelle variable d’environnement appelée **SCOPE_CPP_SDK** toopoint toothis active.</span><span class="sxs-lookup"><span data-stu-id="184e9-205">Define a new environment variable called **SCOPE_CPP_SDK** toopoint toothis directory.</span></span> <span data-ttu-id="184e9-206">Ou copiez hello dossier toohello autre emplacement et spécifier **SCOPE_CPP_SDK** que.</span><span class="sxs-lookup"><span data-stu-id="184e9-206">Or copy hello folder toohello other location and specify **SCOPE_CPP_SDK** as that.</span></span>

    <span data-ttu-id="184e9-207">Dans la variable d’environnement toosetting hello plus, vous pouvez spécifier hello **- CppSDK** argument lorsque vous utilisez la ligne de commande hello.</span><span class="sxs-lookup"><span data-stu-id="184e9-207">In addition toosetting hello environment variable, you can specify hello **-CppSDK** argument when you're using hello command line.</span></span> <span data-ttu-id="184e9-208">Cet argument remplace votre variable d’environnement CppSDK par défaut.</span><span class="sxs-lookup"><span data-stu-id="184e9-208">This argument overwrites your default CppSDK environment variable.</span></span>

- <span data-ttu-id="184e9-209">Ensemble hello **LOCALRUN_DATAROOT** variable d’environnement.</span><span class="sxs-lookup"><span data-stu-id="184e9-209">Set hello **LOCALRUN_DATAROOT** environment variable.</span></span>

    <span data-ttu-id="184e9-210">Définir une nouvelle variable d’environnement appelée **LOCALRUN_DATAROOT** qui pointe toohello la racine de données.</span><span class="sxs-lookup"><span data-stu-id="184e9-210">Define a new environment variable called **LOCALRUN_DATAROOT** that points toohello data root.</span></span>

    <span data-ttu-id="184e9-211">Dans la variable d’environnement toosetting hello plus, vous pouvez spécifier hello **- DataRoot** argument avec un chemin d’accès racine de données hello lorsque vous utilisez une ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="184e9-211">In addition toosetting hello environment variable, you can specify hello **-DataRoot** argument with hello data-root path when you're using a command line.</span></span> <span data-ttu-id="184e9-212">Cet argument remplace votre variable d’environnement de racine de données par défaut.</span><span class="sxs-lookup"><span data-stu-id="184e9-212">This argument overwrites your default data-root environment variable.</span></span> <span data-ttu-id="184e9-213">Vous devez tooadd cet argument de ligne de commande tooevery que vous êtes en cours d’exécution afin que vous pouvez remplacer la variable d’environnement racine de données hello par défaut pour toutes les opérations.</span><span class="sxs-lookup"><span data-stu-id="184e9-213">You need tooadd this argument tooevery command line you're running so that you can overwrite hello default data-root environment variable for all operations.</span></span>

### <a name="sdk-command-line-usage-samples"></a><span data-ttu-id="184e9-214">Exemples d’utilisation en ligne de commande du Kit SDK</span><span class="sxs-lookup"><span data-stu-id="184e9-214">SDK command line usage samples</span></span>

#### <a name="compile-and-run"></a><span data-ttu-id="184e9-215">Compilation et exécution</span><span class="sxs-lookup"><span data-stu-id="184e9-215">Compile and run</span></span>

<span data-ttu-id="184e9-216">Hello **exécuter** commande toocompile hello script et puis exécutez résultats compilés.</span><span class="sxs-lookup"><span data-stu-id="184e9-216">hello **run** command is used toocompile hello script and then execute compiled results.</span></span> <span data-ttu-id="184e9-217">Ses arguments de ligne de commande sont une combinaison des commandes **compile** et **execute**.</span><span class="sxs-lookup"><span data-stu-id="184e9-217">Its command-line arguments are a combination of those from **compile** and **execute**.</span></span>

    LocalRunHelper run -Script path_to_usql_script.usql [optional_arguments]

<span data-ttu-id="184e9-218">Hello Voici les arguments facultatifs pour **exécuter**:</span><span class="sxs-lookup"><span data-stu-id="184e9-218">hello following are optional arguments for **run**:</span></span>


|<span data-ttu-id="184e9-219">Argument</span><span class="sxs-lookup"><span data-stu-id="184e9-219">Argument</span></span>|<span data-ttu-id="184e9-220">Valeur par défaut</span><span class="sxs-lookup"><span data-stu-id="184e9-220">Default value</span></span>|<span data-ttu-id="184e9-221">Description</span><span class="sxs-lookup"><span data-stu-id="184e9-221">Description</span></span>|
|--------|-------------|-----------|
|<span data-ttu-id="184e9-222">-CodeBehind</span><span class="sxs-lookup"><span data-stu-id="184e9-222">-CodeBehind</span></span>|<span data-ttu-id="184e9-223">False</span><span class="sxs-lookup"><span data-stu-id="184e9-223">False</span></span>|<span data-ttu-id="184e9-224">script de Hello associé au code .cs</span><span class="sxs-lookup"><span data-stu-id="184e9-224">hello script has .cs code behind</span></span>|
|<span data-ttu-id="184e9-225">-CppSDK</span><span class="sxs-lookup"><span data-stu-id="184e9-225">-CppSDK</span></span>| |<span data-ttu-id="184e9-226">Répertoire CppSDK</span><span class="sxs-lookup"><span data-stu-id="184e9-226">CppSDK Directory</span></span>|
|<span data-ttu-id="184e9-227">-DataRoot</span><span class="sxs-lookup"><span data-stu-id="184e9-227">-DataRoot</span></span>| <span data-ttu-id="184e9-228">Variable d’environnement DataRoot</span><span class="sxs-lookup"><span data-stu-id="184e9-228">DataRoot environment variable</span></span>|<span data-ttu-id="184e9-229">DataRoot pour la série locale, par défaut trop variable d’environnement 'LOCALRUN_DATAROOT'</span><span class="sxs-lookup"><span data-stu-id="184e9-229">DataRoot for local run, default too'LOCALRUN_DATAROOT' environment variable</span></span>|
|<span data-ttu-id="184e9-230">-MessageOut</span><span class="sxs-lookup"><span data-stu-id="184e9-230">-MessageOut</span></span>| |<span data-ttu-id="184e9-231">Vider les messages sur le fichier de console tooa</span><span class="sxs-lookup"><span data-stu-id="184e9-231">Dump messages on console tooa file</span></span>|
|<span data-ttu-id="184e9-232">-Parallel</span><span class="sxs-lookup"><span data-stu-id="184e9-232">-Parallel</span></span>|<span data-ttu-id="184e9-233">1</span><span class="sxs-lookup"><span data-stu-id="184e9-233">1</span></span>|<span data-ttu-id="184e9-234">Exécutez hello plan avec hello spécifié de parallélisme</span><span class="sxs-lookup"><span data-stu-id="184e9-234">Run hello plan with hello specified parallelism</span></span>|
|<span data-ttu-id="184e9-235">-References</span><span class="sxs-lookup"><span data-stu-id="184e9-235">-References</span></span>| |<span data-ttu-id="184e9-236">Liste des assemblys de référence tooextra de chemins d’accès ou les fichiers de données de code-behind, séparé par ';'</span><span class="sxs-lookup"><span data-stu-id="184e9-236">List of paths tooextra reference assemblies or data files of code behind, separated by ';'</span></span>|
|<span data-ttu-id="184e9-237">-UdoRedirect</span><span class="sxs-lookup"><span data-stu-id="184e9-237">-UdoRedirect</span></span>|<span data-ttu-id="184e9-238">False</span><span class="sxs-lookup"><span data-stu-id="184e9-238">False</span></span>|<span data-ttu-id="184e9-239">Générer la configuration de redirection d’assembly Udo</span><span class="sxs-lookup"><span data-stu-id="184e9-239">Generate Udo assembly redirect config</span></span>|
|<span data-ttu-id="184e9-240">-UseDatabase</span><span class="sxs-lookup"><span data-stu-id="184e9-240">-UseDatabase</span></span>|<span data-ttu-id="184e9-241">master</span><span class="sxs-lookup"><span data-stu-id="184e9-241">master</span></span>|<span data-ttu-id="184e9-242">Toouse de base de données pour le code-behind d’inscription de l’assembly temporaire</span><span class="sxs-lookup"><span data-stu-id="184e9-242">Database toouse for code behind temporary assembly registration</span></span>|
|<span data-ttu-id="184e9-243">-Verbose</span><span class="sxs-lookup"><span data-stu-id="184e9-243">-Verbose</span></span>|<span data-ttu-id="184e9-244">False</span><span class="sxs-lookup"><span data-stu-id="184e9-244">False</span></span>|<span data-ttu-id="184e9-245">Afficher les sorties détaillées du runtime</span><span class="sxs-lookup"><span data-stu-id="184e9-245">Show detailed outputs from runtime</span></span>|
|<span data-ttu-id="184e9-246">-WorkDir</span><span class="sxs-lookup"><span data-stu-id="184e9-246">-WorkDir</span></span>|<span data-ttu-id="184e9-247">Répertoire actif</span><span class="sxs-lookup"><span data-stu-id="184e9-247">Current Directory</span></span>|<span data-ttu-id="184e9-248">Répertoire des sorties et de l’utilisation du compilateur</span><span class="sxs-lookup"><span data-stu-id="184e9-248">Directory for compiler usage and outputs</span></span>|
|<span data-ttu-id="184e9-249">-RunScopeCEP</span><span class="sxs-lookup"><span data-stu-id="184e9-249">-RunScopeCEP</span></span>|<span data-ttu-id="184e9-250">0</span><span class="sxs-lookup"><span data-stu-id="184e9-250">0</span></span>|<span data-ttu-id="184e9-251">ScopeCEP mode toouse</span><span class="sxs-lookup"><span data-stu-id="184e9-251">ScopeCEP mode toouse</span></span>|
|<span data-ttu-id="184e9-252">-ScopeCEPTempPath</span><span class="sxs-lookup"><span data-stu-id="184e9-252">-ScopeCEPTempPath</span></span>|<span data-ttu-id="184e9-253">temp</span><span class="sxs-lookup"><span data-stu-id="184e9-253">temp</span></span>|<span data-ttu-id="184e9-254">Toouse de chemin d’accès temporaire pour la diffusion en continu de données</span><span class="sxs-lookup"><span data-stu-id="184e9-254">Temp path toouse for streaming data</span></span>|
|<span data-ttu-id="184e9-255">-OptFlags</span><span class="sxs-lookup"><span data-stu-id="184e9-255">-OptFlags</span></span>| |<span data-ttu-id="184e9-256">Liste séparée par des virgules d’indicateurs d’optimiseur</span><span class="sxs-lookup"><span data-stu-id="184e9-256">Comma-separated list of optimizer flags</span></span>|


<span data-ttu-id="184e9-257">Voici un exemple :</span><span class="sxs-lookup"><span data-stu-id="184e9-257">Here's an example:</span></span>

    LocalRunHelper run -Script d:\test\test1.usql -WorkDir d:\test\bin -CodeBehind -References "d:\asm\ref1.dll;d:\asm\ref2.dll" -UseDatabase testDB –Parallel 5 -Verbose

<span data-ttu-id="184e9-258">Outre la combinaison **compiler** et **exécuter**, vous pouvez compiler et exécuter des exécutables de hello compilé séparément.</span><span class="sxs-lookup"><span data-stu-id="184e9-258">Besides combining **compile** and **execute**, you can compile and execute hello compiled executables separately.</span></span>

#### <a name="compile-a-u-sql-script"></a><span data-ttu-id="184e9-259">Compiler un script U-SQL</span><span class="sxs-lookup"><span data-stu-id="184e9-259">Compile a U-SQL script</span></span>

<span data-ttu-id="184e9-260">Hello **compiler** commande est utilisée toocompile U-SQL script tooexecutables.</span><span class="sxs-lookup"><span data-stu-id="184e9-260">hello **compile** command is used toocompile a U-SQL script tooexecutables.</span></span>

    LocalRunHelper compile -Script path_to_usql_script.usql [optional_arguments]

<span data-ttu-id="184e9-261">Hello Voici les arguments facultatifs pour **compiler**:</span><span class="sxs-lookup"><span data-stu-id="184e9-261">hello following are optional arguments for **compile**:</span></span>


|<span data-ttu-id="184e9-262">Argument</span><span class="sxs-lookup"><span data-stu-id="184e9-262">Argument</span></span>|<span data-ttu-id="184e9-263">Description</span><span class="sxs-lookup"><span data-stu-id="184e9-263">Description</span></span>|
|--------|-----------|
| <span data-ttu-id="184e9-264">-CodeBehind [valeur par défaut 'False']</span><span class="sxs-lookup"><span data-stu-id="184e9-264">-CodeBehind [default value 'False']</span></span>|<span data-ttu-id="184e9-265">script de Hello associé au code .cs</span><span class="sxs-lookup"><span data-stu-id="184e9-265">hello script has .cs code behind</span></span>|
| <span data-ttu-id="184e9-266">-CppSDK [valeur par défaut '']</span><span class="sxs-lookup"><span data-stu-id="184e9-266">-CppSDK [default value '']</span></span>|<span data-ttu-id="184e9-267">Répertoire CppSDK</span><span class="sxs-lookup"><span data-stu-id="184e9-267">CppSDK Directory</span></span>|
| <span data-ttu-id="184e9-268">-DataRoot [valeur par défaut ’DataRoot environment variable’]</span><span class="sxs-lookup"><span data-stu-id="184e9-268">-DataRoot [default value 'DataRoot environment variable']</span></span>|<span data-ttu-id="184e9-269">DataRoot pour la série locale, par défaut trop variable d’environnement 'LOCALRUN_DATAROOT'</span><span class="sxs-lookup"><span data-stu-id="184e9-269">DataRoot for local run, default too'LOCALRUN_DATAROOT' environment variable</span></span>|
| <span data-ttu-id="184e9-270">-MessageOut [valeur par défaut '']</span><span class="sxs-lookup"><span data-stu-id="184e9-270">-MessageOut [default value '']</span></span>|<span data-ttu-id="184e9-271">Vider les messages sur le fichier de console tooa</span><span class="sxs-lookup"><span data-stu-id="184e9-271">Dump messages on console tooa file</span></span>|
| <span data-ttu-id="184e9-272">-References [valeur par défaut '']</span><span class="sxs-lookup"><span data-stu-id="184e9-272">-References [default value '']</span></span>|<span data-ttu-id="184e9-273">Liste des assemblys de référence tooextra de chemins d’accès ou les fichiers de données de code-behind, séparé par ';'</span><span class="sxs-lookup"><span data-stu-id="184e9-273">List of paths tooextra reference assemblies or data files of code behind, separated by ';'</span></span>|
| <span data-ttu-id="184e9-274">-Shallow [valeur par défaut 'False']</span><span class="sxs-lookup"><span data-stu-id="184e9-274">-Shallow [default value 'False']</span></span>|<span data-ttu-id="184e9-275">Compilation superficielle</span><span class="sxs-lookup"><span data-stu-id="184e9-275">Shallow compile</span></span>|
| <span data-ttu-id="184e9-276">-UdoRedirect [valeur par défaut 'False']</span><span class="sxs-lookup"><span data-stu-id="184e9-276">-UdoRedirect [default value 'False']</span></span>|<span data-ttu-id="184e9-277">Générer la configuration de redirection d’assembly Udo</span><span class="sxs-lookup"><span data-stu-id="184e9-277">Generate Udo assembly redirect config</span></span>|
| <span data-ttu-id="184e9-278">-UseDatabase [valeur par défaut 'master']</span><span class="sxs-lookup"><span data-stu-id="184e9-278">-UseDatabase [default value 'master']</span></span>|<span data-ttu-id="184e9-279">Toouse de base de données pour le code-behind d’inscription de l’assembly temporaire</span><span class="sxs-lookup"><span data-stu-id="184e9-279">Database toouse for code behind temporary assembly registration</span></span>|
| <span data-ttu-id="184e9-280">-WorkDir [valeur par défaut ’Current Directory’]</span><span class="sxs-lookup"><span data-stu-id="184e9-280">-WorkDir [default value 'Current Directory']</span></span>|<span data-ttu-id="184e9-281">Répertoire des sorties et de l’utilisation du compilateur</span><span class="sxs-lookup"><span data-stu-id="184e9-281">Directory for compiler usage and outputs</span></span>|
| <span data-ttu-id="184e9-282">-RunScopeCEP [valeur par défaut ’0’]</span><span class="sxs-lookup"><span data-stu-id="184e9-282">-RunScopeCEP [default value '0']</span></span>|<span data-ttu-id="184e9-283">ScopeCEP mode toouse</span><span class="sxs-lookup"><span data-stu-id="184e9-283">ScopeCEP mode toouse</span></span>|
| <span data-ttu-id="184e9-284">-ScopeCEPTempPath [valeur par défaut ’temp’]</span><span class="sxs-lookup"><span data-stu-id="184e9-284">-ScopeCEPTempPath [default value 'temp']</span></span>|<span data-ttu-id="184e9-285">Toouse de chemin d’accès temporaire pour la diffusion en continu de données</span><span class="sxs-lookup"><span data-stu-id="184e9-285">Temp path toouse for streaming data</span></span>|
| <span data-ttu-id="184e9-286">-OptFlags [valeur par défaut ’’]</span><span class="sxs-lookup"><span data-stu-id="184e9-286">-OptFlags [default value '']</span></span>|<span data-ttu-id="184e9-287">Liste séparée par des virgules d’indicateurs d’optimiseur</span><span class="sxs-lookup"><span data-stu-id="184e9-287">Comma-separated list of optimizer flags</span></span>|


<span data-ttu-id="184e9-288">Voici quelques exemples d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="184e9-288">Here are some usage examples.</span></span>

<span data-ttu-id="184e9-289">Compilez un script U-SQL :</span><span class="sxs-lookup"><span data-stu-id="184e9-289">Compile a U-SQL script:</span></span>

    LocalRunHelper compile -Script d:\test\test1.usql

<span data-ttu-id="184e9-290">Compiler un script U-SQL et définir le dossier de données racine hello.</span><span class="sxs-lookup"><span data-stu-id="184e9-290">Compile a U-SQL script and set hello data-root folder.</span></span> <span data-ttu-id="184e9-291">Notez que cette opération va remplacer la variable d’environnement hello ensemble.</span><span class="sxs-lookup"><span data-stu-id="184e9-291">Note that this will overwrite hello set environment variable.</span></span>

    LocalRunHelper compile -Script d:\test\test1.usql –DataRoot c:\DataRoot

<span data-ttu-id="184e9-292">Compilez un script U-SQL et définissez un répertoire de travail, un assembly de référence et une base de données :</span><span class="sxs-lookup"><span data-stu-id="184e9-292">Compile a U-SQL script and set a working directory, reference assembly, and database:</span></span>

    LocalRunHelper compile -Script d:\test\test1.usql -WorkDir d:\test\bin -References "d:\asm\ref1.dll;d:\asm\ref2.dll" -UseDatabase testDB

#### <a name="execute-compiled-results"></a><span data-ttu-id="184e9-293">Exécuter les résultats compilés</span><span class="sxs-lookup"><span data-stu-id="184e9-293">Execute compiled results</span></span>

<span data-ttu-id="184e9-294">Hello **exécuter** commande est utilisée tooexecute compilé résultats.</span><span class="sxs-lookup"><span data-stu-id="184e9-294">hello **execute** command is used tooexecute compiled results.</span></span>   

    LocalRunHelper execute -Algebra path_to_compiled_algebra_file [optional_arguments]

<span data-ttu-id="184e9-295">Hello Voici les arguments facultatifs pour **exécuter**:</span><span class="sxs-lookup"><span data-stu-id="184e9-295">hello following are optional arguments for **execute**:</span></span>

|<span data-ttu-id="184e9-296">Argument</span><span class="sxs-lookup"><span data-stu-id="184e9-296">Argument</span></span>|<span data-ttu-id="184e9-297">Description</span><span class="sxs-lookup"><span data-stu-id="184e9-297">Description</span></span>|
|--------|-----------|
|<span data-ttu-id="184e9-298">-DataRoot [valeur par défaut '']</span><span class="sxs-lookup"><span data-stu-id="184e9-298">-DataRoot [default value '']</span></span>|<span data-ttu-id="184e9-299">Racine de données pour l’exécution des métadonnées.</span><span class="sxs-lookup"><span data-stu-id="184e9-299">Data root for metadata execution.</span></span> <span data-ttu-id="184e9-300">Sa valeur par défaut toohello **LOCALRUN_DATAROOT** variable d’environnement.</span><span class="sxs-lookup"><span data-stu-id="184e9-300">It defaults toohello **LOCALRUN_DATAROOT** environment variable.</span></span>|
|<span data-ttu-id="184e9-301">-MessageOut [valeur par défaut '']</span><span class="sxs-lookup"><span data-stu-id="184e9-301">-MessageOut [default value '']</span></span>|<span data-ttu-id="184e9-302">Vider les messages sur le fichier de tooa console hello.</span><span class="sxs-lookup"><span data-stu-id="184e9-302">Dump messages on hello console tooa file.</span></span>|
|<span data-ttu-id="184e9-303">-Parallel [valeur par défaut '1']</span><span class="sxs-lookup"><span data-stu-id="184e9-303">-Parallel [default value '1']</span></span>|<span data-ttu-id="184e9-304">Étapes d’exécution locale indicateur toorun hello généré par hello spécifié au niveau de parallélisme.</span><span class="sxs-lookup"><span data-stu-id="184e9-304">Indicator toorun hello generated local-run steps with hello specified parallelism level.</span></span>|
|<span data-ttu-id="184e9-305">-Verbose [valeur par défaut 'False']</span><span class="sxs-lookup"><span data-stu-id="184e9-305">-Verbose [default value 'False']</span></span>|<span data-ttu-id="184e9-306">Indicateur tooshow détaillées des sorties à partir de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="184e9-306">Indicator tooshow detailed outputs from runtime.</span></span>|

<span data-ttu-id="184e9-307">Voici un exemple d’utilisation :</span><span class="sxs-lookup"><span data-stu-id="184e9-307">Here's a usage example:</span></span>

    LocalRunHelper execute -Algebra d:\test\workdir\C6A101DDCB470506\Script_66AE4909AA0ED06C\__script__.abr –DataRoot c:\DataRoot –Parallel 5


## <a name="use-hello-sdk-with-programming-interfaces"></a><span data-ttu-id="184e9-308">Utilisez hello Kit de développement logiciel avec les interfaces de programmation</span><span class="sxs-lookup"><span data-stu-id="184e9-308">Use hello SDK with programming interfaces</span></span>

<span data-ttu-id="184e9-309">interfaces de programmation Hello se trouvent dans hello LocalRunHelper.exe.</span><span class="sxs-lookup"><span data-stu-id="184e9-309">hello programming interfaces are all located in hello LocalRunHelper.exe.</span></span> <span data-ttu-id="184e9-310">Vous pouvez utiliser les fonctionnalités de hello de toointegrate Hello U-SQL SDK et hello c# test framework tooscale votre test local du script U-SQL.</span><span class="sxs-lookup"><span data-stu-id="184e9-310">You can use them toointegrate hello functionality of hello U-SQL SDK and hello C# test framework tooscale your U-SQL script local test.</span></span> <span data-ttu-id="184e9-311">Dans cet article, je vais utiliser hello standard c# unité test projet tooshow toouse ces interfaces tootest votre script U-SQL.</span><span class="sxs-lookup"><span data-stu-id="184e9-311">In this article, I will use hello standard C# unit test project tooshow how toouse these interfaces tootest your U-SQL script.</span></span>

### <a name="step-1-create-c-unit-test-project-and-configuration"></a><span data-ttu-id="184e9-312">Étape 1 : Créer une configuration et un projet de test unitaire C#</span><span class="sxs-lookup"><span data-stu-id="184e9-312">Step 1: Create C# unit test project and configuration</span></span>

- <span data-ttu-id="184e9-313">Créez un projet de test unitaire C# dans Fichier > Nouveau > Projet > Visual C# > Test > Projet de test unitaire.</span><span class="sxs-lookup"><span data-stu-id="184e9-313">Create a C# unit test project through File > New > Project > Visual C# > Test > Unit Test Project.</span></span>
- <span data-ttu-id="184e9-314">Ajoutez LocalRunHelper.exe comme référence pour le projet de hello.</span><span class="sxs-lookup"><span data-stu-id="184e9-314">Add LocalRunHelper.exe as a reference for hello project.</span></span> <span data-ttu-id="184e9-315">Hello LocalRunHelper.exe se trouve dans \build\runtime\LocalRunHelper.exe dans le package Nuget.</span><span class="sxs-lookup"><span data-stu-id="184e9-315">hello LocalRunHelper.exe is located at \build\runtime\LocalRunHelper.exe in Nuget package.</span></span>

    ![Kit SDK Azure Data Lake U-SQL - Ajouter une référence](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-add-reference.png)

- <span data-ttu-id="184e9-317">Kit de développement logiciel U-SQL **uniquement** prise en charge x64, environnement, vérifiez que tooset build plateforme cible en tant que x64.</span><span class="sxs-lookup"><span data-stu-id="184e9-317">U-SQL SDK **only** support x64 environment, make sure tooset build platform target as x64.</span></span> <span data-ttu-id="184e9-318">Vous pouvez le faire dans Propriété du projet > Build > Plateforme cible.</span><span class="sxs-lookup"><span data-stu-id="184e9-318">You can set that through Project Property > Build > Platform target.</span></span>

    ![Kit SDK Azure Data Lake U-SQL - Configurer un projet x64](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-configure-x64.png)

- <span data-ttu-id="184e9-320">Assurez-vous que tooset votre environnement de test en tant que x64.</span><span class="sxs-lookup"><span data-stu-id="184e9-320">Make sure tooset your test environment as x64.</span></span> <span data-ttu-id="184e9-321">Dans Visual Studio, vous pouvez le faire dans Test > Paramètres de test > Architecture de processeur par défaut > x64.</span><span class="sxs-lookup"><span data-stu-id="184e9-321">In Visual Studio, you can set it through Test > Test Settings > Default Processor Architecture > x64.</span></span>

    ![Kit SDK Azure Data Lake U-SQL - Configurer un environnement de test x64](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-configure-test-x64.png)

- <span data-ttu-id="184e9-323">Assurez-vous que toocopy tous les fichiers de dépendance sous le répertoire de travail tooproject NugetPackage\build\runtime\ qui est habituellement sous ProjectFolder\bin\x64\Debug.</span><span class="sxs-lookup"><span data-stu-id="184e9-323">Make sure toocopy all dependency files under NugetPackage\build\runtime\ tooproject working directory which is usually under ProjectFolder\bin\x64\Debug.</span></span>

### <a name="step-2-create-u-sql-script-test-case"></a><span data-ttu-id="184e9-324">Étape 2 : Créer des cas de test du script U-SQL</span><span class="sxs-lookup"><span data-stu-id="184e9-324">Step 2: Create U-SQL script test case</span></span>

<span data-ttu-id="184e9-325">Voici un exemple de code hello pour le test de script U-SQL.</span><span class="sxs-lookup"><span data-stu-id="184e9-325">Below is hello sample code for U-SQL script test.</span></span> <span data-ttu-id="184e9-326">Pour le test, vous devez tooprepare, scripts, fichiers d’entrée et sortie attendue.</span><span class="sxs-lookup"><span data-stu-id="184e9-326">For testing, you need tooprepare scripts, input files and expected output files.</span></span>

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
                //Specify hello local run message output path
                StreamWriter MessageOutput = new StreamWriter("../../../log.txt");

                LocalRunHelper localrun = new LocalRunHelper(MessageOutput);

                //Configure hello DateRoot path, Script Path and CPPSDK path
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

                //Don't forget tooclose MessageOutput tooget logs into file
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


### <a name="programming-interfaces-in-localrunhelperexe"></a><span data-ttu-id="184e9-327">Interfaces de programmation dans LocalRunHelper.exe</span><span class="sxs-lookup"><span data-stu-id="184e9-327">Programming interfaces in LocalRunHelper.exe</span></span>

<span data-ttu-id="184e9-328">LocalRunHelper.exe fournit hello interfaces de programmation pour la compilation locale U-SQL, exécuter, les interfaces hello etc. sont répertoriés comme suit.</span><span class="sxs-lookup"><span data-stu-id="184e9-328">LocalRunHelper.exe provides hello programming interfaces for U-SQL local compile, run, etc. hello interfaces are listed as follows.</span></span>

<span data-ttu-id="184e9-329">**Constructeur**</span><span class="sxs-lookup"><span data-stu-id="184e9-329">**Constructor**</span></span>

<span data-ttu-id="184e9-330">public LocalRunHelper([System.IO.TextWriter messageOutput = null])</span><span class="sxs-lookup"><span data-stu-id="184e9-330">public LocalRunHelper([System.IO.TextWriter messageOutput = null])</span></span>

|<span data-ttu-id="184e9-331">Paramètre</span><span class="sxs-lookup"><span data-stu-id="184e9-331">Parameter</span></span>|<span data-ttu-id="184e9-332">Type</span><span class="sxs-lookup"><span data-stu-id="184e9-332">Type</span></span>|<span data-ttu-id="184e9-333">Description</span><span class="sxs-lookup"><span data-stu-id="184e9-333">Description</span></span>|
|---------|----|-----------|
|<span data-ttu-id="184e9-334">messageOutput</span><span class="sxs-lookup"><span data-stu-id="184e9-334">messageOutput</span></span>|<span data-ttu-id="184e9-335">System.IO.TextWriter</span><span class="sxs-lookup"><span data-stu-id="184e9-335">System.IO.TextWriter</span></span>|<span data-ttu-id="184e9-336">pour les messages de sortie, définissez toonull toouse Console</span><span class="sxs-lookup"><span data-stu-id="184e9-336">for output messages, set toonull toouse Console</span></span>|

<span data-ttu-id="184e9-337">**Propriétés**</span><span class="sxs-lookup"><span data-stu-id="184e9-337">**Properties**</span></span>

|<span data-ttu-id="184e9-338">Propriété</span><span class="sxs-lookup"><span data-stu-id="184e9-338">Property</span></span>|<span data-ttu-id="184e9-339">Type</span><span class="sxs-lookup"><span data-stu-id="184e9-339">Type</span></span>|<span data-ttu-id="184e9-340">Description</span><span class="sxs-lookup"><span data-stu-id="184e9-340">Description</span></span>|
|--------|----|-----------|
|<span data-ttu-id="184e9-341">AlgebraPath</span><span class="sxs-lookup"><span data-stu-id="184e9-341">AlgebraPath</span></span>|<span data-ttu-id="184e9-342">string</span><span class="sxs-lookup"><span data-stu-id="184e9-342">string</span></span>|<span data-ttu-id="184e9-343">Hello chemin d’accès tooalgebra fichier (fichier de l’algèbre est un des résultats de compilation hello)</span><span class="sxs-lookup"><span data-stu-id="184e9-343">hello path tooalgebra file (algebra file is one of hello compilation results)</span></span>|
|<span data-ttu-id="184e9-344">CodeBehindReferences</span><span class="sxs-lookup"><span data-stu-id="184e9-344">CodeBehindReferences</span></span>|<span data-ttu-id="184e9-345">string</span><span class="sxs-lookup"><span data-stu-id="184e9-345">string</span></span>|<span data-ttu-id="184e9-346">Si le script de hello possède des références de code supplémentaire, spécifier des chemins d’accès de hello séparées par ';'</span><span class="sxs-lookup"><span data-stu-id="184e9-346">If hello script has additional code behind references, specify hello paths separated with ';'</span></span>|
|<span data-ttu-id="184e9-347">CppSdkDir</span><span class="sxs-lookup"><span data-stu-id="184e9-347">CppSdkDir</span></span>|<span data-ttu-id="184e9-348">string</span><span class="sxs-lookup"><span data-stu-id="184e9-348">string</span></span>|<span data-ttu-id="184e9-349">Répertoire CppSDK</span><span class="sxs-lookup"><span data-stu-id="184e9-349">CppSDK directory</span></span>|
|<span data-ttu-id="184e9-350">CurrentDir</span><span class="sxs-lookup"><span data-stu-id="184e9-350">CurrentDir</span></span>|<span data-ttu-id="184e9-351">string</span><span class="sxs-lookup"><span data-stu-id="184e9-351">string</span></span>|<span data-ttu-id="184e9-352">Répertoire actif</span><span class="sxs-lookup"><span data-stu-id="184e9-352">Current directory</span></span>|
|<span data-ttu-id="184e9-353">DataRoot</span><span class="sxs-lookup"><span data-stu-id="184e9-353">DataRoot</span></span>|<span data-ttu-id="184e9-354">string</span><span class="sxs-lookup"><span data-stu-id="184e9-354">string</span></span>|<span data-ttu-id="184e9-355">Chemin d’accès de la racine de données</span><span class="sxs-lookup"><span data-stu-id="184e9-355">Data root path</span></span>|
|<span data-ttu-id="184e9-356">DebuggerMailPath</span><span class="sxs-lookup"><span data-stu-id="184e9-356">DebuggerMailPath</span></span>|<span data-ttu-id="184e9-357">string</span><span class="sxs-lookup"><span data-stu-id="184e9-357">string</span></span>|<span data-ttu-id="184e9-358">Hello chemin d’accès toodebugger mailslot</span><span class="sxs-lookup"><span data-stu-id="184e9-358">hello path toodebugger mailslot</span></span>|
|<span data-ttu-id="184e9-359">GenerateUdoRedirect</span><span class="sxs-lookup"><span data-stu-id="184e9-359">GenerateUdoRedirect</span></span>|<span data-ttu-id="184e9-360">bool</span><span class="sxs-lookup"><span data-stu-id="184e9-360">bool</span></span>|<span data-ttu-id="184e9-361">Si nous voulons que le chargement d’assemblys toogenerate la redirection de remplacer la configuration</span><span class="sxs-lookup"><span data-stu-id="184e9-361">If we want toogenerate assembly loading redirection override config</span></span>|
|<span data-ttu-id="184e9-362">HasCodeBehind</span><span class="sxs-lookup"><span data-stu-id="184e9-362">HasCodeBehind</span></span>|<span data-ttu-id="184e9-363">bool</span><span class="sxs-lookup"><span data-stu-id="184e9-363">bool</span></span>|<span data-ttu-id="184e9-364">Si le script de hello a code-behind</span><span class="sxs-lookup"><span data-stu-id="184e9-364">If hello script has code behind</span></span>|
|<span data-ttu-id="184e9-365">InputDir</span><span class="sxs-lookup"><span data-stu-id="184e9-365">InputDir</span></span>|<span data-ttu-id="184e9-366">string</span><span class="sxs-lookup"><span data-stu-id="184e9-366">string</span></span>|<span data-ttu-id="184e9-367">Répertoire des données d’entrée</span><span class="sxs-lookup"><span data-stu-id="184e9-367">Directory for input data</span></span>|
|<span data-ttu-id="184e9-368">MessagePath</span><span class="sxs-lookup"><span data-stu-id="184e9-368">MessagePath</span></span>|<span data-ttu-id="184e9-369">string</span><span class="sxs-lookup"><span data-stu-id="184e9-369">string</span></span>|<span data-ttu-id="184e9-370">Chemin d’accès du fichier de vidage des messages</span><span class="sxs-lookup"><span data-stu-id="184e9-370">Message dump file path</span></span>|
|<span data-ttu-id="184e9-371">OutputDir</span><span class="sxs-lookup"><span data-stu-id="184e9-371">OutputDir</span></span>|<span data-ttu-id="184e9-372">string</span><span class="sxs-lookup"><span data-stu-id="184e9-372">string</span></span>|<span data-ttu-id="184e9-373">Répertoire des données de sortie</span><span class="sxs-lookup"><span data-stu-id="184e9-373">Directory for output data</span></span>|
|<span data-ttu-id="184e9-374">Parallélisme</span><span class="sxs-lookup"><span data-stu-id="184e9-374">Parallelism</span></span>|<span data-ttu-id="184e9-375">int</span><span class="sxs-lookup"><span data-stu-id="184e9-375">int</span></span>|<span data-ttu-id="184e9-376">Algèbre de parallélisme toorun hello</span><span class="sxs-lookup"><span data-stu-id="184e9-376">Parallelism toorun hello algebra</span></span>|
|<span data-ttu-id="184e9-377">ParentPid</span><span class="sxs-lookup"><span data-stu-id="184e9-377">ParentPid</span></span>|<span data-ttu-id="184e9-378">int</span><span class="sxs-lookup"><span data-stu-id="184e9-378">int</span></span>|<span data-ttu-id="184e9-379">PID du parent hello sur quel hello service surveille tooexit, jeu too0 ou tooignore négatif</span><span class="sxs-lookup"><span data-stu-id="184e9-379">PID of hello parent on which hello service monitors tooexit, set too0 or negative tooignore</span></span>|
|<span data-ttu-id="184e9-380">ResultPath</span><span class="sxs-lookup"><span data-stu-id="184e9-380">ResultPath</span></span>|<span data-ttu-id="184e9-381">string</span><span class="sxs-lookup"><span data-stu-id="184e9-381">string</span></span>|<span data-ttu-id="184e9-382">Chemin d’accès du fichier de vidage des résultats</span><span class="sxs-lookup"><span data-stu-id="184e9-382">Result dump file path</span></span>|
|<span data-ttu-id="184e9-383">RuntimeDir</span><span class="sxs-lookup"><span data-stu-id="184e9-383">RuntimeDir</span></span>|<span data-ttu-id="184e9-384">string</span><span class="sxs-lookup"><span data-stu-id="184e9-384">string</span></span>|<span data-ttu-id="184e9-385">Répertoire du runtime</span><span class="sxs-lookup"><span data-stu-id="184e9-385">Runtime directory</span></span>|
|<span data-ttu-id="184e9-386">ScriptPath</span><span class="sxs-lookup"><span data-stu-id="184e9-386">ScriptPath</span></span>|<span data-ttu-id="184e9-387">string</span><span class="sxs-lookup"><span data-stu-id="184e9-387">string</span></span>|<span data-ttu-id="184e9-388">Où toofind hello script</span><span class="sxs-lookup"><span data-stu-id="184e9-388">Where toofind hello script</span></span>|
|<span data-ttu-id="184e9-389">Shallow</span><span class="sxs-lookup"><span data-stu-id="184e9-389">Shallow</span></span>|<span data-ttu-id="184e9-390">valeur booléenne</span><span class="sxs-lookup"><span data-stu-id="184e9-390">bool</span></span>|<span data-ttu-id="184e9-391">Compilation superficielle ou non</span><span class="sxs-lookup"><span data-stu-id="184e9-391">Shallow compile or not</span></span>|
|<span data-ttu-id="184e9-392">TempDir</span><span class="sxs-lookup"><span data-stu-id="184e9-392">TempDir</span></span>|<span data-ttu-id="184e9-393">string</span><span class="sxs-lookup"><span data-stu-id="184e9-393">string</span></span>|<span data-ttu-id="184e9-394">Répertoire Temp</span><span class="sxs-lookup"><span data-stu-id="184e9-394">Temp directory</span></span>|
|<span data-ttu-id="184e9-395">UseDataBase</span><span class="sxs-lookup"><span data-stu-id="184e9-395">UseDataBase</span></span>|<span data-ttu-id="184e9-396">string</span><span class="sxs-lookup"><span data-stu-id="184e9-396">string</span></span>|<span data-ttu-id="184e9-397">Spécifiez toouse de base de données hello pour le code-behind d’enregistrement de l’assembly temporaire, maître par défaut</span><span class="sxs-lookup"><span data-stu-id="184e9-397">Specify hello database toouse for code behind temporary assembly registration, master by default</span></span>|
|<span data-ttu-id="184e9-398">WorkDir</span><span class="sxs-lookup"><span data-stu-id="184e9-398">WorkDir</span></span>|<span data-ttu-id="184e9-399">string</span><span class="sxs-lookup"><span data-stu-id="184e9-399">string</span></span>|<span data-ttu-id="184e9-400">Répertoire de travail favori</span><span class="sxs-lookup"><span data-stu-id="184e9-400">Preferred working directory</span></span>|


<span data-ttu-id="184e9-401">**Méthode**</span><span class="sxs-lookup"><span data-stu-id="184e9-401">**Method**</span></span>

|<span data-ttu-id="184e9-402">Méthode</span><span class="sxs-lookup"><span data-stu-id="184e9-402">Method</span></span>|<span data-ttu-id="184e9-403">Description</span><span class="sxs-lookup"><span data-stu-id="184e9-403">Description</span></span>|<span data-ttu-id="184e9-404">Renvoie</span><span class="sxs-lookup"><span data-stu-id="184e9-404">Return</span></span>|<span data-ttu-id="184e9-405">Paramètre</span><span class="sxs-lookup"><span data-stu-id="184e9-405">Parameter</span></span>|
|------|-----------|------|---------|
|<span data-ttu-id="184e9-406">public bool DoCompile()</span><span class="sxs-lookup"><span data-stu-id="184e9-406">public bool DoCompile()</span></span>|<span data-ttu-id="184e9-407">Compiler hello U-SQL script</span><span class="sxs-lookup"><span data-stu-id="184e9-407">Compile hello U-SQL script</span></span>|<span data-ttu-id="184e9-408">True en cas de réussite</span><span class="sxs-lookup"><span data-stu-id="184e9-408">True on success</span></span>| |
|<span data-ttu-id="184e9-409">public bool DoExec()</span><span class="sxs-lookup"><span data-stu-id="184e9-409">public bool DoExec()</span></span>|<span data-ttu-id="184e9-410">Exécution du résultat de hello compilé</span><span class="sxs-lookup"><span data-stu-id="184e9-410">Execute hello compiled result</span></span>|<span data-ttu-id="184e9-411">True en cas de réussite</span><span class="sxs-lookup"><span data-stu-id="184e9-411">True on success</span></span>| |
|<span data-ttu-id="184e9-412">public bool DoRun()</span><span class="sxs-lookup"><span data-stu-id="184e9-412">public bool DoRun()</span></span>|<span data-ttu-id="184e9-413">Exécutez hello U-SQL script (compiler + exécuter)</span><span class="sxs-lookup"><span data-stu-id="184e9-413">Run hello U-SQL script (Compile + Execute)</span></span>|<span data-ttu-id="184e9-414">True en cas de réussite</span><span class="sxs-lookup"><span data-stu-id="184e9-414">True on success</span></span>| |
|<span data-ttu-id="184e9-415">public bool IsValidRuntimeDir(string chemin-d’accès)</span><span class="sxs-lookup"><span data-stu-id="184e9-415">public bool IsValidRuntimeDir(string path)</span></span>|<span data-ttu-id="184e9-416">Vérifier si hello chemin d’accès donné est le chemin d’accès d’exécution valide</span><span class="sxs-lookup"><span data-stu-id="184e9-416">Check if hello given path is valid runtime path</span></span>|<span data-ttu-id="184e9-417">True en cas de validité</span><span class="sxs-lookup"><span data-stu-id="184e9-417">True for valid</span></span>|<span data-ttu-id="184e9-418">chemin d’accès de Hello du répertoire du runtime</span><span class="sxs-lookup"><span data-stu-id="184e9-418">hello path of runtime directory</span></span>|


## <a name="faq-about-common-issue"></a><span data-ttu-id="184e9-419">FAQ sur les problèmes courants</span><span class="sxs-lookup"><span data-stu-id="184e9-419">FAQ about common issue</span></span>

### <a name="error-1"></a><span data-ttu-id="184e9-420">Erreur 1 :</span><span class="sxs-lookup"><span data-stu-id="184e9-420">Error 1:</span></span>
<span data-ttu-id="184e9-421">E_CSC_SYSTEM_INTERNAL : Erreur interne !</span><span class="sxs-lookup"><span data-stu-id="184e9-421">E_CSC_SYSTEM_INTERNAL: Internal error!</span></span> <span data-ttu-id="184e9-422">Impossible de charger le fichier ou l’assembly « ScopeEngineManaged.dll » ou une de ses dépendances.</span><span class="sxs-lookup"><span data-stu-id="184e9-422">Could not load file or assembly 'ScopeEngineManaged.dll' or one of its dependencies.</span></span> <span data-ttu-id="184e9-423">module de Hello spécifié est introuvable.</span><span class="sxs-lookup"><span data-stu-id="184e9-423">hello specified module could not be found.</span></span>

<span data-ttu-id="184e9-424">Vérifiez les suivant hello :</span><span class="sxs-lookup"><span data-stu-id="184e9-424">Please check hello following:</span></span>

- <span data-ttu-id="184e9-425">Assurez-vous que vous avez un environnement x64.</span><span class="sxs-lookup"><span data-stu-id="184e9-425">Make sure you have x64 environment.</span></span> <span data-ttu-id="184e9-426">plateforme cible de build Hello et environnement de test hello doit être x64, consultez trop**étape 1 : créer c# unité projet de test et configuration** ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="184e9-426">hello build target platform and hello test environment should be x64, refer too**Step 1: Create C# unit test project and configuration** above.</span></span>
- <span data-ttu-id="184e9-427">Assurez-vous que vous avez copié tous les fichiers de dépendance sous le répertoire de travail NugetPackage\build\runtime\ tooproject.</span><span class="sxs-lookup"><span data-stu-id="184e9-427">Make sure you have copied all dependency files under NugetPackage\build\runtime\ tooproject working directory.</span></span>


## <a name="next-steps"></a><span data-ttu-id="184e9-428">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="184e9-428">Next steps</span></span>

* <span data-ttu-id="184e9-429">toolearn U-SQL, consultez [prise en main langage lac de données Azure Analytique U-SQL](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="184e9-429">toolearn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
* <span data-ttu-id="184e9-430">toolog des informations de diagnostic, consultez [l’accès aux journaux de diagnostic pour l’Analytique de LAC de données Azure](data-lake-analytics-diagnostic-logs.md).</span><span class="sxs-lookup"><span data-stu-id="184e9-430">toolog diagnostics information, see [Accessing diagnostics logs for Azure Data Lake Analytics](data-lake-analytics-diagnostic-logs.md).</span></span>
* <span data-ttu-id="184e9-431">toosee une requête plus complexe, consultez [analyser les journaux du site Web à l’aide d’Analytique de LAC de données Azure](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="184e9-431">toosee a more complex query, see [Analyze website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="184e9-432">Détails de la tâche tooview, consultez [navigateur de travail d’utilisation et de la vue des travaux pour les travaux de l’Analytique de LAC de données Azure](data-lake-analytics-data-lake-tools-view-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="184e9-432">tooview job details, see [Use Job Browser and Job View for Azure Data Lake Analytics jobs](data-lake-analytics-data-lake-tools-view-jobs.md).</span></span>
* <span data-ttu-id="184e9-433">vue de l’exécution toouse hello vertex, consultez [hello d’utilisation vue de l’exécution de sommets dans Data Lake Tools pour Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).</span><span class="sxs-lookup"><span data-stu-id="184e9-433">toouse hello vertex execution view, see [Use hello Vertex Execution View in Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).</span></span>
