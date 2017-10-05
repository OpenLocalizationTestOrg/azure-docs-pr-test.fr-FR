---
title: "Tester et déboguer des travaux U-SQL à l’aide d’une exécution locale et du Kit de développement logiciel (SDK) Azure Data Lake U-SQL | Microsoft Docs"
description: "Découvrez comment utiliser Azure Data Lake Tools pour Visual Studio et le Kit de développement logiciel (SDK) Azure Data Lake U-SQL pour tester et déboguer des travaux U-SQL sur votre station de travail locale."
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
ms.openlocfilehash: 771a96df5cc66bac46e7144785be8cc072b57b31
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="test-and-debug-u-sql-jobs-by-using-local-run-and-the-azure-data-lake-u-sql-sdk"></a><span data-ttu-id="37ddf-103">Tester et déboguer des travaux U-SQL à l’aide d’une exécution locale et du Kit de développement logiciel (SDK) Azure Data Lake U-SQL</span><span class="sxs-lookup"><span data-stu-id="37ddf-103">Test and debug U-SQL jobs by using local run and the Azure Data Lake U-SQL SDK</span></span>

<span data-ttu-id="37ddf-104">Vous pouvez utiliser Azure Data Lake Tools pour Visual Studio et le Kit de développement logiciel (SDK) U-SQL pour exécuter des travaux U-SQL sur votre station de travail, comme vous pouvez le faire dans le service Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="37ddf-104">You can use Azure Data Lake Tools for Visual Studio and the Azure Data Lake U-SQL SDK to run U-SQL jobs on your workstation, just as you can in the Azure Data Lake service.</span></span> <span data-ttu-id="37ddf-105">Ces deux fonctionnalités d’exécution locale accélèrent les procédures de test et de débogage de vos travaux U-SQL.</span><span class="sxs-lookup"><span data-stu-id="37ddf-105">These two local-run features save you time in testing and debugging your U-SQL jobs.</span></span>

## <a name="understand-the-data-root-folder-and-the-file-path"></a><span data-ttu-id="37ddf-106">Comprendre le dossier racine de données et le chemin d’accès</span><span class="sxs-lookup"><span data-stu-id="37ddf-106">Understand the data-root folder and the file path</span></span>

<span data-ttu-id="37ddf-107">L’exécution locale et le Kit de développement logiciel (SDK) U-SQL nécessitent un dossier racine de données.</span><span class="sxs-lookup"><span data-stu-id="37ddf-107">Both local run and the U-SQL SDK require a data-root folder.</span></span> <span data-ttu-id="37ddf-108">Ce dossier est un « magasin local » pour le compte de calcul local.</span><span class="sxs-lookup"><span data-stu-id="37ddf-108">The data-root folder is a "local store" for the local compute account.</span></span> <span data-ttu-id="37ddf-109">Il est équivalent au compte Azure Data Lake Store d’un compte Data Lake Analytics dans Azure.</span><span class="sxs-lookup"><span data-stu-id="37ddf-109">It's equivalent to the Azure Data Lake Store account of a Data Lake Analytics account.</span></span> <span data-ttu-id="37ddf-110">Basculer vers un dossier racine de données différent revient à basculer vers un autre compte de magasin.</span><span class="sxs-lookup"><span data-stu-id="37ddf-110">Switching to a different data-root folder is just like switching to a different store account.</span></span> <span data-ttu-id="37ddf-111">Si vous souhaitez accéder aux données généralement partagées avec des dossiers racines de données différents, vous devez utiliser des chemins d’accès absolus dans vos scripts.</span><span class="sxs-lookup"><span data-stu-id="37ddf-111">If you want to access commonly shared data with different data-root folders, you must use absolute paths in your scripts.</span></span> <span data-ttu-id="37ddf-112">Vous pouvez aussi créer des liens symboliques de système de fichiers (par exemple, **mklink** sur NTFS) sous le dossier racine de données, afin de pointer vers les données partagées.</span><span class="sxs-lookup"><span data-stu-id="37ddf-112">Or, create file system symbolic links (for example, **mklink** on NTFS) under the data-root folder to point to the shared data.</span></span>

<span data-ttu-id="37ddf-113">Le dossier racine de données est utilisé pour :</span><span class="sxs-lookup"><span data-stu-id="37ddf-113">The data-root folder is used to:</span></span>

- <span data-ttu-id="37ddf-114">Stocker les métadonnées, notamment des bases de données, des tables, des fonctions table (TVF) et des assemblys.</span><span class="sxs-lookup"><span data-stu-id="37ddf-114">Store metadata, including databases, tables, table-valued functions (TVFs), and assemblies.</span></span>
- <span data-ttu-id="37ddf-115">Rechercher les chemins d’entrée et de sortie qui sont définis comme des chemins relatifs dans U-SQL.</span><span class="sxs-lookup"><span data-stu-id="37ddf-115">Look up the input and output paths that are defined as relative paths in U-SQL.</span></span> <span data-ttu-id="37ddf-116">Les chemins relatifs facilitent le déploiement de vos projets U-SQL dans Azure.</span><span class="sxs-lookup"><span data-stu-id="37ddf-116">Using relative paths makes it easier to deploy your U-SQL projects to Azure.</span></span>

<span data-ttu-id="37ddf-117">Vous pouvez utiliser un chemin d’accès relatif et un chemin d’accès absolu local dans des scripts SQL-U.</span><span class="sxs-lookup"><span data-stu-id="37ddf-117">You can use both a relative path and a local absolute path in U-SQL scripts.</span></span> <span data-ttu-id="37ddf-118">Le chemin d’accès relatif dépend du chemin d’accès au dossier racine de données spécifié.</span><span class="sxs-lookup"><span data-stu-id="37ddf-118">The relative path is relative to the specified data-root folder path.</span></span> <span data-ttu-id="37ddf-119">Il est recommandé d’utiliser « / » en tant que séparateur de chemin afin de rendre vos scripts compatibles avec le côté serveur.</span><span class="sxs-lookup"><span data-stu-id="37ddf-119">We recommend that you use "/" as the path separator to make your scripts compatible with the server side.</span></span> <span data-ttu-id="37ddf-120">Voici quelques exemples de chemins relatifs, avec leurs chemins absolus équivalents.</span><span class="sxs-lookup"><span data-stu-id="37ddf-120">Here are some examples of relative paths and their equivalent absolute paths.</span></span> <span data-ttu-id="37ddf-121">Dans ces exemples, le chemin C:\LocalRunDataRoot correspond à la racine de données.</span><span class="sxs-lookup"><span data-stu-id="37ddf-121">In these examples, C:\LocalRunDataRoot is the data-root folder.</span></span>

|<span data-ttu-id="37ddf-122">Chemin relatif</span><span class="sxs-lookup"><span data-stu-id="37ddf-122">Relative path</span></span>|<span data-ttu-id="37ddf-123">Chemin absolu</span><span class="sxs-lookup"><span data-stu-id="37ddf-123">Absolute path</span></span>|
|-------------|-------------|
|<span data-ttu-id="37ddf-124">/abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="37ddf-124">/abc/def/input.csv</span></span> |<span data-ttu-id="37ddf-125">C:\LocalRunDataRoot\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="37ddf-125">C:\LocalRunDataRoot\abc\def\input.csv</span></span>|
|<span data-ttu-id="37ddf-126">abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="37ddf-126">abc/def/input.csv</span></span>  |<span data-ttu-id="37ddf-127">C:\LocalRunDataRoot\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="37ddf-127">C:\LocalRunDataRoot\abc\def\input.csv</span></span>|
|<span data-ttu-id="37ddf-128">D:/abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="37ddf-128">D:/abc/def/input.csv</span></span> |<span data-ttu-id="37ddf-129">D:\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="37ddf-129">D:\abc\def\input.csv</span></span>|

## <a name="use-local-run-from-visual-studio"></a><span data-ttu-id="37ddf-130">Utiliser l’exécution locale depuis Visual Studio</span><span class="sxs-lookup"><span data-stu-id="37ddf-130">Use local run from Visual Studio</span></span>

<span data-ttu-id="37ddf-131">Data Lake Tools pour Visual Studio fournit une expérience d’exécution locale U-SQL dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="37ddf-131">Data Lake Tools for Visual Studio provides a U-SQL local-run experience in Visual Studio.</span></span> <span data-ttu-id="37ddf-132">À l’aide de cette fonctionnalité, vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="37ddf-132">By using this feature, you can:</span></span>

- <span data-ttu-id="37ddf-133">Exécuter des scripts U-SQL en local, ainsi que des assemblys C#.</span><span class="sxs-lookup"><span data-stu-id="37ddf-133">Run a U-SQL script locally, along with C# assemblies.</span></span>
- <span data-ttu-id="37ddf-134">Déboguer un assembly C# en local.</span><span class="sxs-lookup"><span data-stu-id="37ddf-134">Debug a C# assembly locally.</span></span>
- <span data-ttu-id="37ddf-135">Créer, afficher et supprimer des catalogues U-SQL (bases de données locales, assemblys, schémas et tables) de l’Explorateur de serveurs.</span><span class="sxs-lookup"><span data-stu-id="37ddf-135">Create, view, and delete U-SQL catalogs (local databases, assemblies, schemas, and tables) from Server Explorer.</span></span> <span data-ttu-id="37ddf-136">Le catalogue local est également accessible depuis l’Explorateur de serveurs.</span><span class="sxs-lookup"><span data-stu-id="37ddf-136">You can also find the local catalog also from Server Explorer.</span></span>

    ![Data Lake Tools pour Visual Studio exécution locale catalogue local](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-local-catalog.png)

<span data-ttu-id="37ddf-138">Le programme d’installation de Data Lake Tools crée un dossier C:\LocalRunRoot, qui est utilisé en tant que dossier racine de données par défaut.</span><span class="sxs-lookup"><span data-stu-id="37ddf-138">The Data Lake Tools installer creates a C:\LocalRunRoot folder to be used as the default data-root folder.</span></span> <span data-ttu-id="37ddf-139">Le parallélisme d’exécution locale par défaut est 1.</span><span class="sxs-lookup"><span data-stu-id="37ddf-139">The default local-run parallelism is 1.</span></span>

### <a name="to-configure-local-run-in-visual-studio"></a><span data-ttu-id="37ddf-140">Pour configurer l’exécution locale dans Visual Studio</span><span class="sxs-lookup"><span data-stu-id="37ddf-140">To configure local run in Visual Studio</span></span>

1. <span data-ttu-id="37ddf-141">Ouvrez Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="37ddf-141">Open Visual Studio.</span></span>
2. <span data-ttu-id="37ddf-142">Ouvrez l’**Explorateur de serveurs**.</span><span class="sxs-lookup"><span data-stu-id="37ddf-142">Open **Server Explorer**.</span></span>
3. <span data-ttu-id="37ddf-143">Développez **Azure** > **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="37ddf-143">Expand **Azure** > **Data Lake Analytics**.</span></span>
4. <span data-ttu-id="37ddf-144">Cliquez sur le menu **Data Lake**, puis sur **Options et paramètres**.</span><span class="sxs-lookup"><span data-stu-id="37ddf-144">Click the **Data Lake** menu, and then click **Options and Settings**.</span></span>
5. <span data-ttu-id="37ddf-145">Dans l’arborescence de gauche, développez **Azure Data Lake**, puis **Général**.</span><span class="sxs-lookup"><span data-stu-id="37ddf-145">In the left tree, expand **Azure Data Lake**, and then expand **General**.</span></span>

    ![Data Lake Tools pour Visual Studio exécution locale configurer paramètres](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-configure.png)

<span data-ttu-id="37ddf-147">Un projet U-SQL Visual Studio est requis pour exécuter l’exécution locale.</span><span class="sxs-lookup"><span data-stu-id="37ddf-147">A Visual Studio U-SQL project is required for performing local run.</span></span> <span data-ttu-id="37ddf-148">Cette partie diffère de l'exécution de scripts U-SQL à partir d'Azure.</span><span class="sxs-lookup"><span data-stu-id="37ddf-148">This part is different from running U-SQL scripts from Azure.</span></span>

### <a name="to-run-a-u-sql-script-locally"></a><span data-ttu-id="37ddf-149">Pour exécuter un script U-SQL localement</span><span class="sxs-lookup"><span data-stu-id="37ddf-149">To run a U-SQL script locally</span></span>
1. <span data-ttu-id="37ddf-150">Dans Visual Studio, ouvrez votre projet U-SQL.</span><span class="sxs-lookup"><span data-stu-id="37ddf-150">From Visual Studio, open your U-SQL project.</span></span>   
2. <span data-ttu-id="37ddf-151">Cliquez avec le bouton droit sur un script U-SQL dans l'Explorateur de solutions, puis cliquez sur **Soumettre le script**.</span><span class="sxs-lookup"><span data-stu-id="37ddf-151">Right-click a U-SQL script in Solution Explorer, and then click **Submit Script**.</span></span>
3. <span data-ttu-id="37ddf-152">Sélectionnez **(Local)** en tant que compte Analytics pour exécuter votre script en local.</span><span class="sxs-lookup"><span data-stu-id="37ddf-152">Select **(Local)** as the Analytics account to run your script locally.</span></span>
<span data-ttu-id="37ddf-153">Vous pouvez également cliquer sur le compte **(Local)** en haut de la fenêtre de script, puis sur **Envoyer** (ou utiliser le raccourci clavier Ctrl + F5).</span><span class="sxs-lookup"><span data-stu-id="37ddf-153">You can also click the **(Local)** account on the top of script window, and then click **Submit** (or use the Ctrl + F5 keyboard shortcut).</span></span>

    ![Data Lake Tools pour Visual Studio exécution locale soumettre travaux](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-submit-job.png)

### <a name="debug-scripts-and-c-assemblies-locally"></a><span data-ttu-id="37ddf-155">Déboguer localement des scripts et des assemblys C#</span><span class="sxs-lookup"><span data-stu-id="37ddf-155">Debug scripts and C# assemblies locally</span></span>

<span data-ttu-id="37ddf-156">Vous pouvez déboguer des assemblys C# sans les envoyer ni les inscrire auprès du service Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="37ddf-156">You can debug C# assemblies without submitting and registering it to Azure Data Lake Analytics Service.</span></span> <span data-ttu-id="37ddf-157">Vous pouvez définir des points d'arrêt à la fois dans les fichier code-behind et dans un projet C# référencé.</span><span class="sxs-lookup"><span data-stu-id="37ddf-157">You can set breakpoints in both the code behind file and in a referenced C# project.</span></span>

#### <a name="to-debug-local-code-in-code-behind-file"></a><span data-ttu-id="37ddf-158">Pour déboguer le code local dans le fichier code-behind</span><span class="sxs-lookup"><span data-stu-id="37ddf-158">To debug local code in code behind file</span></span>

1. <span data-ttu-id="37ddf-159">Définissez des points d'arrêt dans le fichier code-behind.</span><span class="sxs-lookup"><span data-stu-id="37ddf-159">Set breakpoints in the code behind file.</span></span>
2. <span data-ttu-id="37ddf-160">Appuyez sur F5 pour déboguer le script localement.</span><span class="sxs-lookup"><span data-stu-id="37ddf-160">Press F5 to debug the script locally.</span></span>

> [!NOTE]
   > <span data-ttu-id="37ddf-161">La procédure suivante fonctionne uniquement dans Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="37ddf-161">The following procedure only works in Visual Studio 2015.</span></span> <span data-ttu-id="37ddf-162">Dans les versions Visual Studio plus anciennes, vous devrez peut-être ajouter manuellement les fichiers pdb.</span><span class="sxs-lookup"><span data-stu-id="37ddf-162">In older Visual Studio you may need to manually add the pdb files.</span></span>  
   >
   >

#### <a name="to-debug-local-code-in-a-referenced-c-project"></a><span data-ttu-id="37ddf-163">Pour déboguer le code local dans un projet C# référencé</span><span class="sxs-lookup"><span data-stu-id="37ddf-163">To debug local code in a referenced C# project</span></span>

1. <span data-ttu-id="37ddf-164">Créez un projet d'assembly C# et générez-le pour obtenir la dll de sortie.</span><span class="sxs-lookup"><span data-stu-id="37ddf-164">Create a C# Assembly project, and build it to generate the output dll.</span></span>
2. <span data-ttu-id="37ddf-165">Inscrivez la dll à l'aide d'une instruction SQL-U :</span><span class="sxs-lookup"><span data-stu-id="37ddf-165">Register the dll using a U-SQL statement:</span></span>

        CREATE ASSEMBLY assemblyname FROM @"..\..\path\to\output\.dll";
        
3. <span data-ttu-id="37ddf-166">Définissez des points d'arrêt dans le code C#.</span><span class="sxs-lookup"><span data-stu-id="37ddf-166">Set breakpoints in the C# code.</span></span>
4. <span data-ttu-id="37ddf-167">Appuyez sur F5 pour déboguer le script en faisant référence à la DLL C# localement.</span><span class="sxs-lookup"><span data-stu-id="37ddf-167">Press F5 to debug the script with referencing the C# dll locally.</span></span>

## <a name="use-local-run-from-the-data-lake-u-sql-sdk"></a><span data-ttu-id="37ddf-168">Utiliser une exécution locale à partir du Kit de développement logiciel (SDK) U-SQL Data Lake</span><span class="sxs-lookup"><span data-stu-id="37ddf-168">Use local run from the Data Lake U-SQL SDK</span></span>

<span data-ttu-id="37ddf-169">Outre l’exécution locale de scripts U-SQL à l’aide de Visual Studio, vous pouvez également utiliser le Kit de développement logiciel (SDK) U-SQL Azure Data Lake pour exécuter les scripts U-SQL en local, avec la ligne de commande et les interfaces de programmation.</span><span class="sxs-lookup"><span data-stu-id="37ddf-169">In addition to running U-SQL scripts locally by using Visual Studio, you can use the Azure Data Lake U-SQL SDK to run U-SQL scripts locally with command-line and programming interfaces.</span></span> <span data-ttu-id="37ddf-170">Par ce biais, vous pouvez mettre votre test local U-SQL à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="37ddf-170">Through these, you can scale your U-SQL local test.</span></span>

<span data-ttu-id="37ddf-171">En savoir plus sur le [Kit de développement logiciel (SDK) U-SQL Azure Data Lake](data-lake-analytics-u-sql-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="37ddf-171">Learn more about [Azure Data Lake U-SQL SDK](data-lake-analytics-u-sql-sdk.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="37ddf-172">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="37ddf-172">Next steps</span></span>

* <span data-ttu-id="37ddf-173">Pour consulter une requête plus complexe, voir [Analyse de journaux des sites web à l’aide d’Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="37ddf-173">To see a more complex query, see [Analyze website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="37ddf-174">Pour afficher les détails d’un travail, voir [Utilisation de l’Explorateur de travaux et de la Vue des travaux pour les travaux Azure Data Lake Analytics](data-lake-analytics-data-lake-tools-view-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="37ddf-174">To view job details, see [Use Job Browser and Job View for Azure Data Lake Analytics jobs](data-lake-analytics-data-lake-tools-view-jobs.md).</span></span>
* <span data-ttu-id="37ddf-175">Pour utiliser la vue d’exécution du vertex, voir [Utilisation de la vue d’exécution du vertex dans Data Lake Tools pour Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).</span><span class="sxs-lookup"><span data-stu-id="37ddf-175">To use the vertex execution view, see [Use the Vertex Execution View in Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).</span></span>
