---
title: les travaux aaaDebug U-SQL | Documents Microsoft
description: "Découvrez comment toodebug U-SQL a échoué à l’aide de Visual Studio de sommets."
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: jhubbard
editor: cgronlun
ms.assetid: bcd0b01e-1755-4112-8e8a-a5cabdca4df2
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 09/02/2016
ms.author: saveenr
ms.openlocfilehash: 092bffa1a59ed91c5837402d0276447480b923fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="debug-user-defined-c-code-for-failed-u-sql-jobs"></a><span data-ttu-id="ea898-103">Débogage de code C# défini par l’utilisateur pour des travaux U-SQL ayant échoué</span><span class="sxs-lookup"><span data-stu-id="ea898-103">Debug user-defined C# code for failed U-SQL jobs</span></span>

<span data-ttu-id="ea898-104">U-SQL fournit un modèle d’extensibilité en c#, donc vous pouvez écrire vos fonctionnalités de tooadd code tel qu’un extracteur personnalisé ou un réducteur.</span><span class="sxs-lookup"><span data-stu-id="ea898-104">U-SQL provides an extensibility model using C#, so you can write your code tooadd functionality such as a custom extractor or reducer.</span></span> <span data-ttu-id="ea898-105">toolearn, voir [guide de programmation U-SQL](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-u-sql-programmability-guide#use-user-defined-functions-udf).</span><span class="sxs-lookup"><span data-stu-id="ea898-105">toolearn more, see [U-SQL programmability guide](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-u-sql-programmability-guide#use-user-defined-functions-udf).</span></span> <span data-ttu-id="ea898-106">Dans la pratique, tout code peut nécessiter un débogage, et les systèmes de Big Data ne peuvent fournir, pour le débogage du runtime, que des informations limitées, telles que des fichiers journaux.</span><span class="sxs-lookup"><span data-stu-id="ea898-106">In practice any code may need debugging, and big data systems may only provide limited runtime debugging information such as log files.</span></span>

<span data-ttu-id="ea898-107">Azure Data Lake Tools pour Visual Studio fournit une fonctionnalité appelée **Échec de la déboguer de sommets**, ce qui vous permet de cloner une tâche ayant échoué à partir de l’ordinateur local tooyour cloud hello pour le débogage.</span><span class="sxs-lookup"><span data-stu-id="ea898-107">Azure Data Lake Tools for Visual Studio provides a feature called **Failed Vertex Debug**, which lets you clone a failed job from hello cloud tooyour local machine for debugging.</span></span> <span data-ttu-id="ea898-108">clone de local Hello capture hello entière environnement cloud, y compris les données d’entrée et le code utilisateur.</span><span class="sxs-lookup"><span data-stu-id="ea898-108">hello local clone captures hello entire cloud environment, including any input data and user code.</span></span>

<span data-ttu-id="ea898-109">Hello vidéo suivante montre échec sommets déboguer dans Azure Data Lake Tools pour Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ea898-109">hello following video demonstrates Failed Vertex Debug in Azure Data Lake Tools for Visual Studio.</span></span>

> [!VIDEO https://e0d1.wpc.azureedge.net/80E0D1/OfficeMixProdMediaBlobStorage/asset-d3aeab42-6149-4ecc-b044-aa624901ab32/b0fc0373c8f94f1bb8cd39da1310adb8.mp4?sv=2012-02-12&sr=c&si=a91fad76-cfdd-4513-9668-483de39e739c&sig=K%2FR%2FdnIi9S6P%2FBlB3iLAEV5pYu6OJFBDlQy%2FQtZ7E7M%3D&se=2116-07-19T09:27:30Z&rscd=attachment%3B%20filename%3DDebugyourcustomcodeinUSQLADLA.mp4]
>

> [!NOTE]
> <span data-ttu-id="ea898-110">Visual Studio requiert hello suivant deux mises à jour, s’ils ne sont pas déjà installés : [Microsoft Visual C++ 2015 Redistributable Update 3](https://www.microsoft.com/en-us/download/details.aspx?id=53840) et [Universal Runtime C pour Windows](https://www.microsoft.com/download/details.aspx?id=50410).</span><span class="sxs-lookup"><span data-stu-id="ea898-110">Visual Studio requires hello following two updates, if they are not already installed: [Microsoft Visual C++ 2015 Redistributable Update 3](https://www.microsoft.com/en-us/download/details.aspx?id=53840) and the [Universal C Runtime for Windows](https://www.microsoft.com/download/details.aspx?id=50410).</span></span>

## <a name="download-failed-vertex-toolocal-machine"></a><span data-ttu-id="ea898-111">Échec du téléchargement du sommet toolocal machine</span><span class="sxs-lookup"><span data-stu-id="ea898-111">Download failed vertex toolocal machine</span></span>

<span data-ttu-id="ea898-112">Lorsque vous ouvrez une tâche ayant échoué dans Azure Data Lake Tools pour Visual Studio, vous voyez une barre jaune alerte avec des messages d’erreur détaillés dans l’onglet d’erreur hello.</span><span class="sxs-lookup"><span data-stu-id="ea898-112">When you open a failed job in Azure Data Lake Tools for Visual Studio, you see a yellow alert bar with detailed error messages in hello error tab.</span></span>

1. <span data-ttu-id="ea898-113">Cliquez sur **télécharger** toodownload tous hello requis des ressources et les flux d’entrée.</span><span class="sxs-lookup"><span data-stu-id="ea898-113">Click **Download** toodownload all hello required resources and input streams.</span></span> <span data-ttu-id="ea898-114">Si le téléchargement de hello ne se termine, cliquez sur **réessayer**.</span><span class="sxs-lookup"><span data-stu-id="ea898-114">If hello download doesn't complete, click **Retry**.</span></span>

2. <span data-ttu-id="ea898-115">Cliquez sur **ouvrir** après le téléchargement de hello terminé toogenerate un environnement de débogage local.</span><span class="sxs-lookup"><span data-stu-id="ea898-115">Click **Open** after hello download completes toogenerate a local debugging environment.</span></span> <span data-ttu-id="ea898-116">Une nouvelle instance Visual Studio avec une solution de débogage est automatiquement créée et ouverte.</span><span class="sxs-lookup"><span data-stu-id="ea898-116">A new Visual Studio instance with a debugging solution is automatically created and opened.</span></span>

![Télécharger le vertex Visual Studio pour le débogage U-SQL Azure Data Lake Analytics](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-download-vertex.png)

<span data-ttu-id="ea898-118">Les travaux peuvent inclure des fichiers sources code-behind ou des assemblys inscrits, et les scénarios de débogage diffèrent pour ces deux types.</span><span class="sxs-lookup"><span data-stu-id="ea898-118">Jobs may include code-behind source files or registered assemblies, and these two types have different debugging scenarios.</span></span>

- [<span data-ttu-id="ea898-119">Débogage de tâches ayant échoué avec code-behind</span><span class="sxs-lookup"><span data-stu-id="ea898-119">Debug a failed job with code-behind</span></span>](#debug-job-failed-with-code-behind)
- [<span data-ttu-id="ea898-120">Débogage de tâches ayant échoué avec des assemblys</span><span class="sxs-lookup"><span data-stu-id="ea898-120">Debug a failed job with assemblies</span></span>](#debug-job-failed-with-assemblies)


## <a name="debug-job-failed-with-code-behind"></a><span data-ttu-id="ea898-121">Débogage de tâches ayant échoué avec code-behind</span><span class="sxs-lookup"><span data-stu-id="ea898-121">Debug job failed with code-behind</span></span>

<span data-ttu-id="ea898-122">Si un travail U-SQL échoue et que le travail de hello inclut le code utilisateur (généralement nommé `Script.usql.cs` dans un projet U-SQL), que code source est importé dans hello déboguer la solution.</span><span class="sxs-lookup"><span data-stu-id="ea898-122">If a U-SQL job fails, and hello job includes user code (typically named `Script.usql.cs` in a U-SQL project), that source code is imported into hello debugging solution.</span></span>  <span data-ttu-id="ea898-123">À partir de là, vous pouvez utiliser problème de hello Visual Studio débogage outils (espion, variables, etc.) tootroubleshoot hello.</span><span class="sxs-lookup"><span data-stu-id="ea898-123">From there you can use hello Visual Studio debugging tools (watch, variables, etc.) tootroubleshoot hello problem.</span></span>

> [!NOTE]
> <span data-ttu-id="ea898-124">Avant le débogage, être vraiment toocheck **Exceptions Common Language Runtime** dans la fenêtre de paramètres d’Exception hello (**Ctrl + Alt + E**).</span><span class="sxs-lookup"><span data-stu-id="ea898-124">Before debugging, be sure toocheck **Common Language Runtime Exceptions** in hello Exception Settings window (**Ctrl + Alt + E**).</span></span>

![Configuration de Visual Studio pour le débogage U-SQL Azure Data Lake Analytics](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-clr-exception-setting.png)

1. <span data-ttu-id="ea898-126">Appuyez sur **F5** code de code-behind toorun hello.</span><span class="sxs-lookup"><span data-stu-id="ea898-126">Press **F5** toorun hello code-behind code.</span></span> <span data-ttu-id="ea898-127">Celui-ci s’exécute jusqu'à ce qu’il soit arrêté par une exception.</span><span class="sxs-lookup"><span data-stu-id="ea898-127">It will run until it is stopped by an exception.</span></span>

2. <span data-ttu-id="ea898-128">Ouvrez hello `ADLTool_Codebehind.usql.cs` de fichiers et de définir des points d’arrêt, puis appuyez sur **F5** code de hello toodebug étape par étape.</span><span class="sxs-lookup"><span data-stu-id="ea898-128">Open hello `ADLTool_Codebehind.usql.cs` file and set breakpoints, then press **F5** toodebug hello code step by step.</span></span>

    ![Exception de débogage U-SQL Azure Data Lake Analytics](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-debug-exception.png)

## <a name="debug-job-failed-with-assemblies"></a><span data-ttu-id="ea898-130">Débogage de tâches ayant échoué avec des assemblys</span><span class="sxs-lookup"><span data-stu-id="ea898-130">Debug job failed with assemblies</span></span>

<span data-ttu-id="ea898-131">Si vous utilisez des assemblys inscrits dans votre script U-SQL, système de hello Impossible d’obtenir hello source code automatiquement.</span><span class="sxs-lookup"><span data-stu-id="ea898-131">If you use registered assemblies in your U-SQL script, hello system can't get hello source code automatically.</span></span> <span data-ttu-id="ea898-132">Dans ce cas, ajouter manuellement source code fichiers toohello la solution les assemblys hello.</span><span class="sxs-lookup"><span data-stu-id="ea898-132">In this case, manually add hello assemblies' source code files toohello solution.</span></span>

### <a name="configure-hello-solution"></a><span data-ttu-id="ea898-133">Configurer une solution de hello</span><span class="sxs-lookup"><span data-stu-id="ea898-133">Configure hello solution</span></span>

1. <span data-ttu-id="ea898-134">Avec le bouton droit **Solution 'VertexDebug' > Ajouter > projet existant...**  toofind hello de code source d’assemblys et ajouter toohello de projet hello déboguer la solution.</span><span class="sxs-lookup"><span data-stu-id="ea898-134">Right-click **Solution 'VertexDebug' > Add > Existing Project...** toofind hello assemblies' source code and add hello project toohello debugging solution.</span></span>

    ![Projet d’ajout de débogage U-SQL Azure Data Lake Analytics](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-add-project-to-debug-solution.png)

2. <span data-ttu-id="ea898-136">Avec le bouton droit **LocalVertexHost > Propriétés** Bonjour de solution et copie hello **du répertoire de travail** chemin d’accès.</span><span class="sxs-lookup"><span data-stu-id="ea898-136">Right-click **LocalVertexHost > Properties** in hello solution and copy hello **Working Directory** path.</span></span>

3. <span data-ttu-id="ea898-137">Avec le bouton droit **projet de code source assembly > Propriétés**, sélectionnez hello **générer** onglet située à gauche et collez le chemin d’accès de hello copié en tant que **sortie > chemin de sortie**.</span><span class="sxs-lookup"><span data-stu-id="ea898-137">Right-Click **assembly source code project > Properties**, select hello **Build** tab at left, and paste hello copied path as **Output > Output path**.</span></span>

    ![Chemin d’accès de pdb de définition de débogage U-SQL Azure Data Lake Analytics](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-set-pdb-path.png)

4. <span data-ttu-id="ea898-139">Appuyez sur **Ctrl + Alt + E**, vérifiez les **exceptions Common Language Runtime** dans la fenêtre des paramètres d’exception.</span><span class="sxs-lookup"><span data-stu-id="ea898-139">Press **Ctrl + Alt + E**, check **Common Language Runtime Exceptions** in Exception Settings window.</span></span>

### <a name="start-debug"></a><span data-ttu-id="ea898-140">Début du débogage</span><span class="sxs-lookup"><span data-stu-id="ea898-140">Start debug</span></span>

1. <span data-ttu-id="ea898-141">Avec le bouton droit **projet de code source assembly > reconstruire** toohello les fichiers .pdb de toooutput `LocalVertexHost` répertoire de travail.</span><span class="sxs-lookup"><span data-stu-id="ea898-141">Right-click **assembly source code project > Rebuild** toooutput .pdb files toohello `LocalVertexHost` working directory.</span></span>

2. <span data-ttu-id="ea898-142">Appuyez sur **F5** et projet de hello s’exécute jusqu'à ce qu’elle soit arrêtée par une exception.</span><span class="sxs-lookup"><span data-stu-id="ea898-142">Press **F5** and hello project will run until it is stopped by an exception.</span></span> <span data-ttu-id="ea898-143">Vous pouvez voir hello après le message d’avertissement, vous pouvez ignorer en toute sécurité.</span><span class="sxs-lookup"><span data-stu-id="ea898-143">You may see hello following warning message, which you can safely ignore.</span></span> <span data-ttu-id="ea898-144">Peut prendre jusqu'à l’écran de débogage toohello tooa tooget minute.</span><span class="sxs-lookup"><span data-stu-id="ea898-144">It can take up tooa minute tooget toohello debug screen.</span></span>

    ![Avertissement Visual Studio pour le débogage U-SQL Azure Data Lake Analytics](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-visual-studio-u-sql-debug-warning.png)

3. <span data-ttu-id="ea898-146">Ouvrez votre code source et de définir des points d’arrêt, puis appuyez sur **F5** code de hello toodebug étape par étape.</span><span class="sxs-lookup"><span data-stu-id="ea898-146">Open your source code and set breakpoints, then press **F5** toodebug hello code step by step.</span></span>

<span data-ttu-id="ea898-147">Vous pouvez également utiliser le problème de hello Visual Studio débogage outils (espion, variables, etc.) tootroubleshoot hello.</span><span class="sxs-lookup"><span data-stu-id="ea898-147">You can also use hello Visual Studio debugging tools (watch, variables, etc.) tootroubleshoot hello problem.</span></span>

> [!NOTE]
> <span data-ttu-id="ea898-148">Régénérez le projet de code source assembly hello chaque fois après avoir modifié les fichiers .pdb de hello code toogenerate mis à jour.</span><span class="sxs-lookup"><span data-stu-id="ea898-148">Rebuild hello assembly source code project each time after you modify hello code toogenerate updated .pdb files.</span></span>

<span data-ttu-id="ea898-149">Après le débogage, si le projet de hello se termine correctement fenêtre de sortie de hello affiche hello message suivant :</span><span class="sxs-lookup"><span data-stu-id="ea898-149">After debugging, if hello project completes successfully hello output window shows hello following message:</span></span>

```
hello Program 'LocalVertexHost.exe' has exited with code 0 (0x0).
```

![Débogage U-SQL Azure Data Lake Analytics réussi](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-debug-succeed.png)

## <a name="resubmit-hello-job"></a><span data-ttu-id="ea898-151">Soumettez à nouveau le travail de hello</span><span class="sxs-lookup"><span data-stu-id="ea898-151">Resubmit hello job</span></span>

<span data-ttu-id="ea898-152">Une fois que vous avez terminé le débogage, soumettez à nouveau hello du travail ayant échoué.</span><span class="sxs-lookup"><span data-stu-id="ea898-152">Once you have completed debugging, resubmit hello failed job.</span></span>

1. <span data-ttu-id="ea898-153">Pour les travaux avec les solutions de code-behind, copier votre code c# dans le fichier de source de code-behind hello (généralement `Script.usql.cs`).</span><span class="sxs-lookup"><span data-stu-id="ea898-153">For jobs with code-behind solutions, copy your C# code into hello code-behind source file (typically `Script.usql.cs`).</span></span>
2. <span data-ttu-id="ea898-154">Pour les travaux avec les assemblys, inscrire hello mis à jour d’assemblys .dll dans votre base de données ADLA :</span><span class="sxs-lookup"><span data-stu-id="ea898-154">For jobs with assemblies, register hello updated .dll assemblies into your ADLA database:</span></span>
    1. <span data-ttu-id="ea898-155">À partir de l’Explorateur de serveurs ou Cloud Explorer, développez hello **compte ADLA > bases de données** nœud.</span><span class="sxs-lookup"><span data-stu-id="ea898-155">From Server Explorer or Cloud Explorer, expand hello **ADLA account > Databases** node.</span></span>
    2. <span data-ttu-id="ea898-156">Avec le bouton droit **assemblys** et enregistrer vos nouveaux assemblys .dll avec la base de données ADLA hello : ![débogage de LAC de données Azure Analytique U-SQL inscrire l’assembly](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-register-assembly.png)</span><span class="sxs-lookup"><span data-stu-id="ea898-156">Right-click **Assemblies** and register your new .dll assemblies with hello ADLA database: ![Azure Data Lake Analytics U-SQL debug register assembly](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-register-assembly.png)</span></span>
3. <span data-ttu-id="ea898-157">Renvoyez le travail.</span><span class="sxs-lookup"><span data-stu-id="ea898-157">Resubmit your job.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ea898-158">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ea898-158">Next steps</span></span>

- [<span data-ttu-id="ea898-159">Guide de programmabilité U-SQL</span><span class="sxs-lookup"><span data-stu-id="ea898-159">U-SQL programmability guide</span></span>](data-lake-analytics-u-sql-programmability-guide.md)
- [<span data-ttu-id="ea898-160">Développer des opérateurs U-SQL définis par l’utilisateur pour des travaux Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="ea898-160">Develop U-SQL User-defined operators for Azure Data Lake Analytics jobs</span></span>](data-lake-analytics-u-sql-develop-user-defined-operators.md)
- [<span data-ttu-id="ea898-161">Didacticiel : Développer des scripts U-SQL avec Data Lake Tools pour Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ea898-161">Tutorial: develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
