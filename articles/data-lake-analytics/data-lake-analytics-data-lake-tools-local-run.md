---
title: "aaaTest et debug U-SQL travaux à l’aide locale exécuter et hello du Kit de développement logiciel Azure données Lake U-SQL | Documents Microsoft"
description: "Découvrez comment toouse Azure Data Lake Tools pour Visual Studio et tootest du Kit de développement logiciel Azure données Lake U-SQL hello et débogage U-SQL des travaux sur votre station de travail locale."
services: data-lake-analytics
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 66dd58b1-0b28-46d1-aaae-43ee2739ae0a
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 11/15/2016
ms.author: yanacai
ms.openlocfilehash: be04558a504acf6a088e207608ee2d4a011d3ffc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="test-and-debug-u-sql-jobs-by-using-local-run-and-hello-azure-data-lake-u-sql-sdk"></a><span data-ttu-id="1aada-103">Tester et déboguer des travaux U-SQL à l’aide locale exécuter et hello Kit de développement logiciel Azure données Lake U-SQL</span><span class="sxs-lookup"><span data-stu-id="1aada-103">Test and debug U-SQL jobs by using local run and hello Azure Data Lake U-SQL SDK</span></span>

<span data-ttu-id="1aada-104">Vous pouvez utiliser Azure Data Lake Tools pour Visual Studio et les travaux de hello SQL-U de LAC de données Azure SDK toorun U-SQL sur votre station de travail, comme vous le faites dans le service Azure Data Lake hello.</span><span class="sxs-lookup"><span data-stu-id="1aada-104">You can use Azure Data Lake Tools for Visual Studio and hello Azure Data Lake U-SQL SDK toorun U-SQL jobs on your workstation, just as you can in hello Azure Data Lake service.</span></span> <span data-ttu-id="1aada-105">Ces deux fonctionnalités d’exécution locale accélèrent les procédures de test et de débogage de vos travaux U-SQL.</span><span class="sxs-lookup"><span data-stu-id="1aada-105">These two local-run features save you time in testing and debugging your U-SQL jobs.</span></span>

## <a name="understand-hello-data-root-folder-and-hello-file-path"></a><span data-ttu-id="1aada-106">Comprendre le dossier de données racine hello et chemin d’accès du fichier hello</span><span class="sxs-lookup"><span data-stu-id="1aada-106">Understand hello data-root folder and hello file path</span></span>

<span data-ttu-id="1aada-107">Exécution locale et hello U-SQL SDK requièrent un dossier racine de données.</span><span class="sxs-lookup"><span data-stu-id="1aada-107">Both local run and hello U-SQL SDK require a data-root folder.</span></span> <span data-ttu-id="1aada-108">dossier de données racine de Hello est un « magasin local » pour le compte de calcul local hello.</span><span class="sxs-lookup"><span data-stu-id="1aada-108">hello data-root folder is a "local store" for hello local compute account.</span></span> <span data-ttu-id="1aada-109">Il est le compte d’Azure Data Lake Store toohello équivalent d’un compte Analytique lac de données.</span><span class="sxs-lookup"><span data-stu-id="1aada-109">It's equivalent toohello Azure Data Lake Store account of a Data Lake Analytics account.</span></span> <span data-ttu-id="1aada-110">Dossier de données-racine différent tooa de commutation est identique à commutation tooa autre banque de compte.</span><span class="sxs-lookup"><span data-stu-id="1aada-110">Switching tooa different data-root folder is just like switching tooa different store account.</span></span> <span data-ttu-id="1aada-111">Si vous souhaitez tooaccess fréquemment les données partagées avec des dossiers racine de données différents, vous devez utiliser des chemins d’accès absolus dans vos scripts.</span><span class="sxs-lookup"><span data-stu-id="1aada-111">If you want tooaccess commonly shared data with different data-root folders, you must use absolute paths in your scripts.</span></span> <span data-ttu-id="1aada-112">Ou bien, créez des liens symboliques de système de fichier (par exemple, **mklink** sur NTFS) sous hello racine de données dossier toopoint toohello les données partagées.</span><span class="sxs-lookup"><span data-stu-id="1aada-112">Or, create file system symbolic links (for example, **mklink** on NTFS) under hello data-root folder toopoint toohello shared data.</span></span>

<span data-ttu-id="1aada-113">dossier de données racine Hello est utilisé pour :</span><span class="sxs-lookup"><span data-stu-id="1aada-113">hello data-root folder is used to:</span></span>

- <span data-ttu-id="1aada-114">Stocker les métadonnées, notamment des bases de données, des tables, des fonctions table (TVF) et des assemblys.</span><span class="sxs-lookup"><span data-stu-id="1aada-114">Store metadata, including databases, tables, table-valued functions (TVFs), and assemblies.</span></span>
- <span data-ttu-id="1aada-115">Rechercher hello d’entrée et les chemins d’accès de sortie sont définies comme des chemins d’accès relatifs dans U-SQL.</span><span class="sxs-lookup"><span data-stu-id="1aada-115">Look up hello input and output paths that are defined as relative paths in U-SQL.</span></span> <span data-ttu-id="1aada-116">À l’aide de chemins d’accès relatifs rend plus facile toodeploy votre tooAzure de projets U-SQL.</span><span class="sxs-lookup"><span data-stu-id="1aada-116">Using relative paths makes it easier toodeploy your U-SQL projects tooAzure.</span></span>

<span data-ttu-id="1aada-117">Vous pouvez utiliser un chemin d’accès relatif et un chemin d’accès absolu local dans des scripts SQL-U.</span><span class="sxs-lookup"><span data-stu-id="1aada-117">You can use both a relative path and a local absolute path in U-SQL scripts.</span></span> <span data-ttu-id="1aada-118">chemin d’accès relatif de Hello est le chemin d’accès au dossier toohello relatif racine de données spécifié.</span><span class="sxs-lookup"><span data-stu-id="1aada-118">hello relative path is relative toohello specified data-root folder path.</span></span> <span data-ttu-id="1aada-119">Il est recommandé que vous utilisez « / » comme hello toomake de séparateur de chemin d’accès de vos scripts compatibles avec SSI hello.</span><span class="sxs-lookup"><span data-stu-id="1aada-119">We recommend that you use "/" as hello path separator toomake your scripts compatible with hello server side.</span></span> <span data-ttu-id="1aada-120">Voici quelques exemples de chemins relatifs, avec leurs chemins absolus équivalents.</span><span class="sxs-lookup"><span data-stu-id="1aada-120">Here are some examples of relative paths and their equivalent absolute paths.</span></span> <span data-ttu-id="1aada-121">Dans ces exemples, C:\LocalRunDataRoot est le dossier racine de données de hello.</span><span class="sxs-lookup"><span data-stu-id="1aada-121">In these examples, C:\LocalRunDataRoot is hello data-root folder.</span></span>

|<span data-ttu-id="1aada-122">Chemin relatif</span><span class="sxs-lookup"><span data-stu-id="1aada-122">Relative path</span></span>|<span data-ttu-id="1aada-123">Chemin absolu</span><span class="sxs-lookup"><span data-stu-id="1aada-123">Absolute path</span></span>|
|-------------|-------------|
|<span data-ttu-id="1aada-124">/abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="1aada-124">/abc/def/input.csv</span></span> |<span data-ttu-id="1aada-125">C:\LocalRunDataRoot\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="1aada-125">C:\LocalRunDataRoot\abc\def\input.csv</span></span>|
|<span data-ttu-id="1aada-126">abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="1aada-126">abc/def/input.csv</span></span>  |<span data-ttu-id="1aada-127">C:\LocalRunDataRoot\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="1aada-127">C:\LocalRunDataRoot\abc\def\input.csv</span></span>|
|<span data-ttu-id="1aada-128">D:/abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="1aada-128">D:/abc/def/input.csv</span></span> |<span data-ttu-id="1aada-129">D:\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="1aada-129">D:\abc\def\input.csv</span></span>|

## <a name="use-local-run-from-visual-studio"></a><span data-ttu-id="1aada-130">Utiliser l’exécution locale depuis Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1aada-130">Use local run from Visual Studio</span></span>

<span data-ttu-id="1aada-131">Data Lake Tools pour Visual Studio fournit une expérience d’exécution locale U-SQL dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1aada-131">Data Lake Tools for Visual Studio provides a U-SQL local-run experience in Visual Studio.</span></span> <span data-ttu-id="1aada-132">À l’aide de cette fonctionnalité, vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="1aada-132">By using this feature, you can:</span></span>

- <span data-ttu-id="1aada-133">Exécuter des scripts U-SQL en local, ainsi que des assemblys C#.</span><span class="sxs-lookup"><span data-stu-id="1aada-133">Run a U-SQL script locally, along with C# assemblies.</span></span>
- <span data-ttu-id="1aada-134">Déboguer un assembly C# en local.</span><span class="sxs-lookup"><span data-stu-id="1aada-134">Debug a C# assembly locally.</span></span>
- <span data-ttu-id="1aada-135">Créer, afficher et supprimer des catalogues U-SQL (bases de données locales, assemblys, schémas et tables) de l’Explorateur de serveurs.</span><span class="sxs-lookup"><span data-stu-id="1aada-135">Create, view, and delete U-SQL catalogs (local databases, assemblies, schemas, and tables) from Server Explorer.</span></span> <span data-ttu-id="1aada-136">Vous trouverez également les catalogue local hello également à partir de l’Explorateur de serveurs.</span><span class="sxs-lookup"><span data-stu-id="1aada-136">You can also find hello local catalog also from Server Explorer.</span></span>

    ![Data Lake Tools pour Visual Studio exécution locale catalogue local](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-local-catalog.png)

<span data-ttu-id="1aada-138">programme d’installation de Data Lake Tools Hello crée un toobe du dossier C:\LocalRunRoot utilisé comme dossier de données racine par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="1aada-138">hello Data Lake Tools installer creates a C:\LocalRunRoot folder toobe used as hello default data-root folder.</span></span> <span data-ttu-id="1aada-139">parallélisme de local-exécuter Hello par défaut est 1.</span><span class="sxs-lookup"><span data-stu-id="1aada-139">hello default local-run parallelism is 1.</span></span>

### <a name="tooconfigure-local-run-in-visual-studio"></a><span data-ttu-id="1aada-140">tooconfigure local s’exécutent dans Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1aada-140">tooconfigure local run in Visual Studio</span></span>

1. <span data-ttu-id="1aada-141">Ouvrez Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1aada-141">Open Visual Studio.</span></span>
2. <span data-ttu-id="1aada-142">Ouvrez l’**Explorateur de serveurs**.</span><span class="sxs-lookup"><span data-stu-id="1aada-142">Open **Server Explorer**.</span></span>
3. <span data-ttu-id="1aada-143">Développez **Azure** > **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="1aada-143">Expand **Azure** > **Data Lake Analytics**.</span></span>
4. <span data-ttu-id="1aada-144">Cliquez sur hello **Data Lake** menu, puis sur **Options et paramètres**.</span><span class="sxs-lookup"><span data-stu-id="1aada-144">Click hello **Data Lake** menu, and then click **Options and Settings**.</span></span>
5. <span data-ttu-id="1aada-145">Dans l’arborescence de hello gauche, développez **Azure Data Lake**, puis développez **général**.</span><span class="sxs-lookup"><span data-stu-id="1aada-145">In hello left tree, expand **Azure Data Lake**, and then expand **General**.</span></span>

    ![Data Lake Tools pour Visual Studio exécution locale configurer paramètres](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-configure.png)

<span data-ttu-id="1aada-147">Un projet U-SQL Visual Studio est requis pour exécuter l’exécution locale.</span><span class="sxs-lookup"><span data-stu-id="1aada-147">A Visual Studio U-SQL project is required for performing local run.</span></span> <span data-ttu-id="1aada-148">Cette partie diffère de l'exécution de scripts U-SQL à partir d'Azure.</span><span class="sxs-lookup"><span data-stu-id="1aada-148">This part is different from running U-SQL scripts from Azure.</span></span>

### <a name="toorun-a-u-sql-script-locally"></a><span data-ttu-id="1aada-149">script toorun U-SQL localement</span><span class="sxs-lookup"><span data-stu-id="1aada-149">toorun a U-SQL script locally</span></span>
1. <span data-ttu-id="1aada-150">Dans Visual Studio, ouvrez votre projet U-SQL.</span><span class="sxs-lookup"><span data-stu-id="1aada-150">From Visual Studio, open your U-SQL project.</span></span>   
2. <span data-ttu-id="1aada-151">Cliquez avec le bouton droit sur un script U-SQL dans l'Explorateur de solutions, puis cliquez sur **Soumettre le script**.</span><span class="sxs-lookup"><span data-stu-id="1aada-151">Right-click a U-SQL script in Solution Explorer, and then click **Submit Script**.</span></span>
3. <span data-ttu-id="1aada-152">Sélectionnez **(Local)** compte d’identification hello Analytique toorun localement votre script.</span><span class="sxs-lookup"><span data-stu-id="1aada-152">Select **(Local)** as hello Analytics account toorun your script locally.</span></span>
<span data-ttu-id="1aada-153">Vous pouvez également cliquer sur hello **(Local)** compte haut hello de fenêtre de script, puis cliquez sur **Submit** (ou utilisez Bonjour Ctrl + F5 raccourci).</span><span class="sxs-lookup"><span data-stu-id="1aada-153">You can also click hello **(Local)** account on hello top of script window, and then click **Submit** (or use hello Ctrl + F5 keyboard shortcut).</span></span>

    ![Data Lake Tools pour Visual Studio exécution locale soumettre travaux](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-submit-job.png)

### <a name="debug-scripts-and-c-assemblies-locally"></a><span data-ttu-id="1aada-155">Déboguer localement des scripts et des assemblys C#</span><span class="sxs-lookup"><span data-stu-id="1aada-155">Debug scripts and C# assemblies locally</span></span>

<span data-ttu-id="1aada-156">Vous pouvez déboguer des assemblys c# sans l’envoi et de son inscription tooAzure Service Analytique de LAC de données.</span><span class="sxs-lookup"><span data-stu-id="1aada-156">You can debug C# assemblies without submitting and registering it tooAzure Data Lake Analytics Service.</span></span> <span data-ttu-id="1aada-157">Vous pouvez définir des points d’arrêt dans les deux hello fichier code-behind et dans un projet c# référencé.</span><span class="sxs-lookup"><span data-stu-id="1aada-157">You can set breakpoints in both hello code behind file and in a referenced C# project.</span></span>

#### <a name="toodebug-local-code-in-code-behind-file"></a><span data-ttu-id="1aada-158">toodebug de codes locale dans le fichier code-behind</span><span class="sxs-lookup"><span data-stu-id="1aada-158">toodebug local code in code behind file</span></span>

1. <span data-ttu-id="1aada-159">Définir des points d’arrêt dans hello fichier code-behind.</span><span class="sxs-lookup"><span data-stu-id="1aada-159">Set breakpoints in hello code behind file.</span></span>
2. <span data-ttu-id="1aada-160">Appuyez sur F5 toodebug script hello localement.</span><span class="sxs-lookup"><span data-stu-id="1aada-160">Press F5 toodebug hello script locally.</span></span>

> [!NOTE]
   > <span data-ttu-id="1aada-161">Hello suivant la procédure ne fonctionne que dans Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="1aada-161">hello following procedure only works in Visual Studio 2015.</span></span> <span data-ttu-id="1aada-162">Dans les plus anciennes de Visual Studio, vous devrez peut-être ajouter des fichiers pdb de hello toomanually.</span><span class="sxs-lookup"><span data-stu-id="1aada-162">In older Visual Studio you may need toomanually add hello pdb files.</span></span>  
   >
   >

#### <a name="toodebug-local-code-in-a-referenced-c-project"></a><span data-ttu-id="1aada-163">toodebug le code local dans un projet c# référencé</span><span class="sxs-lookup"><span data-stu-id="1aada-163">toodebug local code in a referenced C# project</span></span>

1. <span data-ttu-id="1aada-164">Créer un projet d’Assembly c# et le générer toogenerate hello sortie dll.</span><span class="sxs-lookup"><span data-stu-id="1aada-164">Create a C# Assembly project, and build it toogenerate hello output dll.</span></span>
2. <span data-ttu-id="1aada-165">Inscrire la dll hello à l’aide d’une instruction U-SQL :</span><span class="sxs-lookup"><span data-stu-id="1aada-165">Register hello dll using a U-SQL statement:</span></span>

        CREATE ASSEMBLY assemblyname FROM @"..\..\path\to\output\.dll";
        
3. <span data-ttu-id="1aada-166">Définir des points d’arrêt dans le code c# de hello.</span><span class="sxs-lookup"><span data-stu-id="1aada-166">Set breakpoints in hello C# code.</span></span>
4. <span data-ttu-id="1aada-167">Appuyez sur F5 script de hello toodebug avec faisant référence à la dll hello c# localement.</span><span class="sxs-lookup"><span data-stu-id="1aada-167">Press F5 toodebug hello script with referencing hello C# dll locally.</span></span>

## <a name="use-local-run-from-hello-data-lake-u-sql-sdk"></a><span data-ttu-id="1aada-168">Utilisez local, exécutez à partir de hello SDK de données Lake U-SQL</span><span class="sxs-lookup"><span data-stu-id="1aada-168">Use local run from hello Data Lake U-SQL SDK</span></span>

<span data-ttu-id="1aada-169">En outre toorunning U-SQL scripts localement à l’aide de Visual Studio, vous pouvez utiliser des scripts de hello SQL-U de LAC de données Azure SDK toorun U-SQL localement avec les interfaces de ligne de commande et de programmation.</span><span class="sxs-lookup"><span data-stu-id="1aada-169">In addition toorunning U-SQL scripts locally by using Visual Studio, you can use hello Azure Data Lake U-SQL SDK toorun U-SQL scripts locally with command-line and programming interfaces.</span></span> <span data-ttu-id="1aada-170">Par ce biais, vous pouvez mettre votre test local U-SQL à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="1aada-170">Through these, you can scale your U-SQL local test.</span></span>

<span data-ttu-id="1aada-171">En savoir plus sur le [Kit de développement logiciel (SDK) U-SQL Azure Data Lake](data-lake-analytics-u-sql-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="1aada-171">Learn more about [Azure Data Lake U-SQL SDK](data-lake-analytics-u-sql-sdk.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="1aada-172">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1aada-172">Next steps</span></span>

* <span data-ttu-id="1aada-173">toosee une requête plus complexe, consultez [analyser les journaux du site Web à l’aide d’Analytique de LAC de données Azure](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="1aada-173">toosee a more complex query, see [Analyze website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="1aada-174">Détails de la tâche tooview, consultez [navigateur de travail d’utilisation et de la vue des travaux pour les travaux de l’Analytique de LAC de données Azure](data-lake-analytics-data-lake-tools-view-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="1aada-174">tooview job details, see [Use Job Browser and Job View for Azure Data Lake Analytics jobs](data-lake-analytics-data-lake-tools-view-jobs.md).</span></span>
* <span data-ttu-id="1aada-175">vue de l’exécution toouse hello vertex, consultez [hello d’utilisation vue de l’exécution de sommets dans Data Lake Tools pour Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).</span><span class="sxs-lookup"><span data-stu-id="1aada-175">toouse hello vertex execution view, see [Use hello Vertex Execution View in Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).</span></span>
