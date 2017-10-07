---
title: "Azure Data Lake Tools : exécution locale et débogage local U-SQL avec Visual Studio Code | Microsoft Docs"
description: "Découvrez comment déboguer les toouse Azure Data Lake Tools pour Visual Studio Code toolocal local et exécution."
Keywords: "Chemin d’accès de le toostorage de téléchargement VScode, Azure Data Lake Tools, exécution, le fichier de stockage débogage Local, le débogage Local, version d’évaluation locale"
services: data-lake-analytics
documentationcenter: 
author: jejiang
manager: DJ
editor: jejiang
tags: azure-portal
ms.assetid: dc9b21d8-c5f4-4f77-bcbc-eff458f48de2
ms.service: data-lake-analytics
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: big-data
ms.date: 07/14/2017
ms.author: jejiang
ms.openlocfilehash: fb152f07fe8c4b03dde8fb8e62c7475eccda0578
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="u-sql-local-run-and-local-debug-with-visual-studio-code"></a><span data-ttu-id="9d12b-104">Exécution locale et débogage local U-SQL avec Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="9d12b-104">U-SQL local run and local debug with Visual Studio Code</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9d12b-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="9d12b-105">Prerequisites</span></span>
<span data-ttu-id="9d12b-106">Vérifiez que vous avez hello suivant des conditions préalables en place avant de commencer ces procédures :</span><span class="sxs-lookup"><span data-stu-id="9d12b-106">Make sure you have hello following prerequisites in place before you start these procedures:</span></span>
- <span data-ttu-id="9d12b-107">Azure Data Lake Tools pour Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="9d12b-107">Azure Data Lake Tool for Visual Studio Code.</span></span> <span data-ttu-id="9d12b-108">Pour les instructions, consultez [Utilisation d’Azure Data Lake Tools pour Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="9d12b-108">For instructions, see [Use Azure Data Lake Tools for Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span></span>
- <span data-ttu-id="9d12b-109">C# pour Visual Studio Code (si vous voulez le débogage local de tooperform U-SQL).</span><span class="sxs-lookup"><span data-stu-id="9d12b-109">C# for Visual Studio Code (if you want tooperform a U-SQL local debug).</span></span>

   ![Installer C# dans Data Lake Tools pour Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-install-ms-vscodecsharp.png)
   
   > [!NOTE]
   > <span data-ttu-id="9d12b-111">Hello série locale d’U-SQL et les fonctionnalités de débogage actuellement prennent uniquement en charge les utilisateurs Windows.</span><span class="sxs-lookup"><span data-stu-id="9d12b-111">hello U-SQL local run and debug features currently only support Windows users.</span></span> 


## <a name="set-up-hello-u-sql-local-run-environment"></a><span data-ttu-id="9d12b-112">Installer l’environnement d’exécution local hello U-SQL</span><span class="sxs-lookup"><span data-stu-id="9d12b-112">Set up hello U-SQL local run environment</span></span>

1. <span data-ttu-id="9d12b-113">Sélectionnez la palette de commandes Ctrl + Maj + P tooopen hello et entrez **ADL : Téléchargez la dépendance de LocalRun** packages de hello toodownload.</span><span class="sxs-lookup"><span data-stu-id="9d12b-113">Select Ctrl+Shift+P tooopen hello command palette, and then enter **ADL: Download LocalRun Dependency** toodownload hello packages.</span></span>  

   ![Télécharger les packages de dépendance de LocalRun ADL hello](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/DownloadLocalRun.png)

2. <span data-ttu-id="9d12b-115">Recherchez des packages de dépendance hello du chemin d’accès hello illustré hello **sortie** volet, puis installez BuildTools et Win10SDK 10240.</span><span class="sxs-lookup"><span data-stu-id="9d12b-115">Locate hello dependency packages from hello path shown in hello **Output** pane, and then install BuildTools and Win10SDK 10240.</span></span> <span data-ttu-id="9d12b-116">Voici un exemple de chemin :</span><span class="sxs-lookup"><span data-stu-id="9d12b-116">Here is an example path:</span></span>  
`C:\Users\xxx\.vscode\extensions\usqlextpublisher.usql-vscode-ext-x.x.x\LocalRunDependency
`  
  <span data-ttu-id="9d12b-117">![Recherchez des packages de dépendance hello](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/LocateDependencyPath.png)</span><span class="sxs-lookup"><span data-stu-id="9d12b-117">![Locate hello dependency packages](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/LocateDependencyPath.png)</span></span>

   <span data-ttu-id="9d12b-118">a.</span><span class="sxs-lookup"><span data-stu-id="9d12b-118">a.</span></span> <span data-ttu-id="9d12b-119">tooinstall BuildTools, suivez les instructions de l’Assistant hello.</span><span class="sxs-lookup"><span data-stu-id="9d12b-119">tooinstall BuildTools, follow hello wizard instructions.</span></span>   

  ![Installer BuildTools](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/InstallBuildTools.png)

   <span data-ttu-id="9d12b-121">b.</span><span class="sxs-lookup"><span data-stu-id="9d12b-121">b.</span></span> <span data-ttu-id="9d12b-122">tooinstall Win10SDK 10240, suivez les instructions de l’Assistant hello.</span><span class="sxs-lookup"><span data-stu-id="9d12b-122">tooinstall Win10SDK 10240, follow hello wizard instructions.</span></span>  

  ![Installer Win10SDK 10240](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/InstallWin10SDK.png)

3. <span data-ttu-id="9d12b-124">Configurer la variable d’environnement hello.</span><span class="sxs-lookup"><span data-stu-id="9d12b-124">Set up hello environment variable.</span></span> <span data-ttu-id="9d12b-125">Ensemble hello **SCOPE_CPP_SDK** variable d’environnement :</span><span class="sxs-lookup"><span data-stu-id="9d12b-125">Set hello **SCOPE_CPP_SDK** environment variable to:</span></span>  
`C:\Users\xxx\.vscode\extensions\usqlextpublisher.usql-vscode-ext-x.x.x\LocalRunDependency\CppSDK_3rdparty
`  
4. <span data-ttu-id="9d12b-126">Redémarrez toomake hello du système d’exploitation sûr que les paramètres de variable d’environnement hello prennent effet.</span><span class="sxs-lookup"><span data-stu-id="9d12b-126">Restart hello OS toomake sure that hello environment variable settings take effect.</span></span>  

   ![Vérifiez la variable d’environnement SCOPE_CPP_SDK hello est installé.](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/ConfigScopeCppSDk.png)

## <a name="start-hello-local-run-service-and-submit-hello-u-sql-job-tooa-local-account"></a><span data-ttu-id="9d12b-128">Démarrer le service d’exécution local hello et soumettre hello U-SQL travail tooa local compte</span><span class="sxs-lookup"><span data-stu-id="9d12b-128">Start hello local run service and submit hello U-SQL job tooa local account</span></span> 
<span data-ttu-id="9d12b-129">Hello utilisateur, vous êtes hello de toodownload demandées ADL : Téléchargez la dépendance de LocalRun packages s’ils ne sont pas déjà installés.</span><span class="sxs-lookup"><span data-stu-id="9d12b-129">For hello first-time user, you are prompted toodownload hello ADL: Download LocalRun Dependency packages if they are not already installed.</span></span>
1. <span data-ttu-id="9d12b-130">Sélectionnez la palette de commandes Ctrl + Maj + P tooopen hello et entrez **ADL : démarrer le Service d’exécution Local**.</span><span class="sxs-lookup"><span data-stu-id="9d12b-130">Select Ctrl+Shift+P tooopen hello command palette, and then enter **ADL: Start Local Run Service**.</span></span>
2. <span data-ttu-id="9d12b-131">Sélectionnez **accepter** tooaccept hello contrat de licence logiciel Microsoft hello première fois.</span><span class="sxs-lookup"><span data-stu-id="9d12b-131">Select **Accept** tooaccept hello Microsoft Software License Terms for hello first time.</span></span> 

   ![Acceptez le contrat de licence logiciel Microsoft hello](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/AcceptEULA.png)   
3. <span data-ttu-id="9d12b-133">Hello cmd console s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="9d12b-133">hello cmd console opens.</span></span> <span data-ttu-id="9d12b-134">Pour les utilisateurs de la première fois, vous devez tooenter **3**, puis recherchez le chemin d’accès du dossier local hello pour vos données d’entrée et sortie.</span><span class="sxs-lookup"><span data-stu-id="9d12b-134">For first-time users, you need tooenter **3**, and then locate hello local folder path for your data input and output.</span></span> <span data-ttu-id="9d12b-135">Pour les autres options, vous pouvez utiliser les valeurs par défaut de hello.</span><span class="sxs-lookup"><span data-stu-id="9d12b-135">For other options, you can use hello default values.</span></span> 

   ![Data Lake Tools pour Visual Studio Code - cmd exécution locale](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-run-cmd.png)
4. <span data-ttu-id="9d12b-137">Sélectionnez la palette de commandes hello Ctrl + Maj + P tooopen, entrez **ADL : soumettre un travail**, puis sélectionnez **Local** compte local de toosubmit hello travail tooyour.</span><span class="sxs-lookup"><span data-stu-id="9d12b-137">Select Ctrl+Shift+P tooopen hello command palette, enter **ADL: Submit Job**, and then select **Local** toosubmit hello job tooyour local account.</span></span>

   ![Data Lake Tools pour Visual Studio Code - Sélectionner Local](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-select-local.png)
5. <span data-ttu-id="9d12b-139">Après avoir soumis le travail de hello, vous pouvez afficher les détails de l’envoi hello.</span><span class="sxs-lookup"><span data-stu-id="9d12b-139">After you submit hello job, you can view hello submission details.</span></span> <span data-ttu-id="9d12b-140">Sélectionnez des détails de soumission de hello tooview **jobUrl** Bonjour **sortie** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="9d12b-140">tooview hello submission details select **jobUrl** in hello **Output** window.</span></span> <span data-ttu-id="9d12b-141">Vous pouvez également afficher le statut de la soumission tâche hello à partir de la console de cmd hello.</span><span class="sxs-lookup"><span data-stu-id="9d12b-141">You can also view hello job submission status from hello cmd console.</span></span> <span data-ttu-id="9d12b-142">Entrez **7** dans la console hello cmd si vous souhaitez tooknow plus de travail plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="9d12b-142">Enter **7** in hello cmd console if you want tooknow more job details.</span></span>

   <span data-ttu-id="9d12b-143">![Data Lake Tools pour Visual Studio Code - Sortie exécution locale](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-run-result.png)
   ![Data Lake Tools pour Visual Studio Code - État cmd exécution locale](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-localrun-cmd-status.png)</span><span class="sxs-lookup"><span data-stu-id="9d12b-143">![Data Lake Tools for Visual Studio Code local run output](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-run-result.png)
![Data Lake Tools for Visual Studio Code local run cmd status](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-localrun-cmd-status.png)</span></span> 


## <a name="start-a-local-debug-for-hello-u-sql-job"></a><span data-ttu-id="9d12b-144">Démarrer un débogage local pour le travail de U-SQL hello</span><span class="sxs-lookup"><span data-stu-id="9d12b-144">Start a local debug for hello U-SQL job</span></span>  
<span data-ttu-id="9d12b-145">Hello utilisateur, vous êtes hello de toodownload demandées ADL : Téléchargez la dépendance de LocalRun packages s’ils ne sont pas déjà installés.</span><span class="sxs-lookup"><span data-stu-id="9d12b-145">For hello first-time user, you are prompted toodownload hello ADL: Download LocalRun Dependency packages if they are not already installed.</span></span>
  
1. <span data-ttu-id="9d12b-146">Sélectionnez la palette de commandes Ctrl + Maj + P tooopen hello et entrez **ADL : démarrer le Service d’exécution Local**.</span><span class="sxs-lookup"><span data-stu-id="9d12b-146">Select Ctrl+Shift+P tooopen hello command palette, and then enter **ADL: Start Local Run Service**.</span></span> <span data-ttu-id="9d12b-147">Hello cmd console s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="9d12b-147">hello cmd console opens.</span></span> <span data-ttu-id="9d12b-148">Vérifiez que hello **DataRoot** est définie.</span><span class="sxs-lookup"><span data-stu-id="9d12b-148">Make sure that hello **DataRoot** is set.</span></span>
3. <span data-ttu-id="9d12b-149">Définissez un point d’arrêt dans votre code C# code-behind.</span><span class="sxs-lookup"><span data-stu-id="9d12b-149">Set a breakpoint in your C# code-behind.</span></span>
4. <span data-ttu-id="9d12b-150">Dans l’éditeur de script hello, sélectionnez console de commande Ctrl + Maj + P tooopen hello et puis entrez **débogage Local** toostart votre service de débogage local.</span><span class="sxs-lookup"><span data-stu-id="9d12b-150">Back in hello script editor, select Ctrl+Shift+P tooopen hello command console, and then enter **Local Debug** toostart your local debug service.</span></span>

![Data Lake Tools pour Visual Studio Code - Résultat débogage local](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-debug-result.png)


## <a name="next-steps"></a><span data-ttu-id="9d12b-152">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9d12b-152">Next steps</span></span>
- <span data-ttu-id="9d12b-153">Pour utiliser Azure Data Lake Tools pour Visual Studio Code, consultez [Utilisation d’Azure Data Lake Tools pour Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="9d12b-153">For using Azure Data Lake Tools for Visual Studio Code, see [Use Azure Data Lake Tools for Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span></span>
- <span data-ttu-id="9d12b-154">Consultez [Didacticiel : Bien démarrer avec Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md) pour obtenir des informations sur la prise en main de Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="9d12b-154">For getting started information on Data Lake Analytics, see [Tutorial: Get started with Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).</span></span>
- <span data-ttu-id="9d12b-155">Pour obtenir des informations sur l’utilisation de Data Lake Tools pour Visual Studio, consultez [Didacticiel : développer des scripts U-SQL avec Data Lake Tools pour Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="9d12b-155">For information about Data Lake Tools for Visual Studio, see [Tutorial: Develop U-SQL scripts by using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
- <span data-ttu-id="9d12b-156">Pour plus d’informations hello sur le développement des assemblys, consultez [assemblys développer U-SQL pour les travaux de l’Analytique de LAC de données Azure](data-lake-analytics-u-sql-develop-assemblies.md).</span><span class="sxs-lookup"><span data-stu-id="9d12b-156">For hello information on developing assemblies, see [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md).</span></span>
