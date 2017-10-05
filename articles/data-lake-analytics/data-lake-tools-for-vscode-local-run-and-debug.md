---
title: "Azure Data Lake Tools : exécution locale et débogage local U-SQL avec Visual Studio Code | Microsoft Docs"
description: "Découvrez comment utiliser Azure Data Lake Tools pour Visual Studio Code pour l’exécution locale et le débogage local."
Keywords: "VScode,Azure Data Lake Tools,exécution locale,débogage local,Débogage local,aperçu du fichier de stockage,charger vers le chemin de stockage"
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
ms.openlocfilehash: 367e4ba792f83d6ee246208306e4c09b69cb49ef
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="u-sql-local-run-and-local-debug-with-visual-studio-code"></a><span data-ttu-id="b159d-104">Exécution locale et débogage local U-SQL avec Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="b159d-104">U-SQL local run and local debug with Visual Studio Code</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b159d-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="b159d-105">Prerequisites</span></span>
<span data-ttu-id="b159d-106">Vérifiez que les prérequis suivants sont remplis avant de démarrer ces procédures :</span><span class="sxs-lookup"><span data-stu-id="b159d-106">Make sure you have the following prerequisites in place before you start these procedures:</span></span>
- <span data-ttu-id="b159d-107">Azure Data Lake Tools pour Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="b159d-107">Azure Data Lake Tool for Visual Studio Code.</span></span> <span data-ttu-id="b159d-108">Pour les instructions, consultez [Utilisation d’Azure Data Lake Tools pour Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="b159d-108">For instructions, see [Use Azure Data Lake Tools for Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span></span>
- <span data-ttu-id="b159d-109">C# pour Visual Studio Code (si vous souhaitez effectuer un débogage local U-SQL).</span><span class="sxs-lookup"><span data-stu-id="b159d-109">C# for Visual Studio Code (if you want to perform a U-SQL local debug).</span></span>

   ![Installer C# dans Data Lake Tools pour Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-install-ms-vscodecsharp.png)
   
   > [!NOTE]
   > <span data-ttu-id="b159d-111">Les fonctionnalités d’exécution et de débogage U-SQL en local ne prennent en charge que les utilisateurs Windows.</span><span class="sxs-lookup"><span data-stu-id="b159d-111">The U-SQL local run and debug features currently only support Windows users.</span></span> 


## <a name="set-up-the-u-sql-local-run-environment"></a><span data-ttu-id="b159d-112">Configurer l’environnement d’exécution locale U-SQL</span><span class="sxs-lookup"><span data-stu-id="b159d-112">Set up the U-SQL local run environment</span></span>

1. <span data-ttu-id="b159d-113">Sélectionnez Ctrl+Maj+P pour ouvrir la palette de commandes, puis entrez **ADL: Download LocalRun Dependency** pour télécharger les packages.</span><span class="sxs-lookup"><span data-stu-id="b159d-113">Select Ctrl+Shift+P to open the command palette, and then enter **ADL: Download LocalRun Dependency** to download the packages.</span></span>  

   ![Télécharger les packages ADL LocalRun Dependency](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/DownloadLocalRun.png)

2. <span data-ttu-id="b159d-115">Recherchez les packages de dépendance à partir du chemin indiqué dans le volet **Sortie**, puis installez BuildTools et Win10SDK 10240.</span><span class="sxs-lookup"><span data-stu-id="b159d-115">Locate the dependency packages from the path shown in the **Output** pane, and then install BuildTools and Win10SDK 10240.</span></span> <span data-ttu-id="b159d-116">Voici un exemple de chemin :</span><span class="sxs-lookup"><span data-stu-id="b159d-116">Here is an example path:</span></span>  
`C:\Users\xxx\.vscode\extensions\usqlextpublisher.usql-vscode-ext-x.x.x\LocalRunDependency
`  
  <span data-ttu-id="b159d-117">![Rechercher les packages de dépendance](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/LocateDependencyPath.png)</span><span class="sxs-lookup"><span data-stu-id="b159d-117">![Locate the dependency packages](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/LocateDependencyPath.png)</span></span>

   <span data-ttu-id="b159d-118">a.</span><span class="sxs-lookup"><span data-stu-id="b159d-118">a.</span></span> <span data-ttu-id="b159d-119">Pour installer BuildTools, suivez les instructions de l’assistant.</span><span class="sxs-lookup"><span data-stu-id="b159d-119">To install BuildTools, follow the wizard instructions.</span></span>   

  ![Installer BuildTools](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/InstallBuildTools.png)

   <span data-ttu-id="b159d-121">b.</span><span class="sxs-lookup"><span data-stu-id="b159d-121">b.</span></span> <span data-ttu-id="b159d-122">Pour installer Win10SDK 10240, suivez les instructions de l’assistant.</span><span class="sxs-lookup"><span data-stu-id="b159d-122">To install Win10SDK 10240, follow the wizard instructions.</span></span>  

  ![Installer Win10SDK 10240](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/InstallWin10SDK.png)

3. <span data-ttu-id="b159d-124">Définissez la variable d’environnement.</span><span class="sxs-lookup"><span data-stu-id="b159d-124">Set up the environment variable.</span></span> <span data-ttu-id="b159d-125">Définissez la variable d’environnement **SCOPE_CPP_SDK** sur :</span><span class="sxs-lookup"><span data-stu-id="b159d-125">Set the **SCOPE_CPP_SDK** environment variable to:</span></span>  
`C:\Users\xxx\.vscode\extensions\usqlextpublisher.usql-vscode-ext-x.x.x\LocalRunDependency\CppSDK_3rdparty
`  
4. <span data-ttu-id="b159d-126">Redémarrez le système d’exploitation pour que les paramètres de la variable d’environnement prennent effet.</span><span class="sxs-lookup"><span data-stu-id="b159d-126">Restart the OS to make sure that the environment variable settings take effect.</span></span>  

   ![Vérifier que la variable d’environnement SCOPE_CPP_SDK est installée](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/ConfigScopeCppSDk.png)

## <a name="start-the-local-run-service-and-submit-the-u-sql-job-to-a-local-account"></a><span data-ttu-id="b159d-128">Démarrer le service d’exécution locale et envoyer le travail U-SQL à un compte local</span><span class="sxs-lookup"><span data-stu-id="b159d-128">Start the local run service and submit the U-SQL job to a local account</span></span> 
<span data-ttu-id="b159d-129">Les nouveaux utilisateurs sont invités à télécharger les packages ADL: Download LocalRun Dependency s’ils ne sont pas déjà installés.</span><span class="sxs-lookup"><span data-stu-id="b159d-129">For the first-time user, you are prompted to download the ADL: Download LocalRun Dependency packages if they are not already installed.</span></span>
1. <span data-ttu-id="b159d-130">Sélectionnez Ctrl+Maj+P pour ouvrir la palette de commandes, puis entrez **ADL: Start Local Run Service**.</span><span class="sxs-lookup"><span data-stu-id="b159d-130">Select Ctrl+Shift+P to open the command palette, and then enter **ADL: Start Local Run Service**.</span></span>
2. <span data-ttu-id="b159d-131">Sélectionnez **Accepter** pour accepter les termes du contrat de licence du logiciel Microsoft pour la première fois.</span><span class="sxs-lookup"><span data-stu-id="b159d-131">Select **Accept** to accept the Microsoft Software License Terms for the first time.</span></span> 

   ![Accepter les termes du contrat de licence du logiciel Microsoft](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/AcceptEULA.png)   
3. <span data-ttu-id="b159d-133">La console cmd s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="b159d-133">The cmd console opens.</span></span> <span data-ttu-id="b159d-134">Les nouveaux utilisateurs doivent entrer **3**, puis rechercher le chemin de dossier local pour l’entrée et la sortie des données.</span><span class="sxs-lookup"><span data-stu-id="b159d-134">For first-time users, you need to enter **3**, and then locate the local folder path for your data input and output.</span></span> <span data-ttu-id="b159d-135">Pour les autres options, vous pouvez utiliser les valeurs par défaut.</span><span class="sxs-lookup"><span data-stu-id="b159d-135">For other options, you can use the default values.</span></span> 

   ![Data Lake Tools pour Visual Studio Code - cmd exécution locale](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-run-cmd.png)
4. <span data-ttu-id="b159d-137">Sélectionnez Ctrl+Maj+P pour ouvrir la palette de commandes et entrez **ADL: Submit Job**, puis sélectionnez **Local** pour envoyer le travail à votre compte local.</span><span class="sxs-lookup"><span data-stu-id="b159d-137">Select Ctrl+Shift+P to open the command palette, enter **ADL: Submit Job**, and then select **Local** to submit the job to your local account.</span></span>

   ![Data Lake Tools pour Visual Studio Code - Sélectionner Local](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-select-local.png)
5. <span data-ttu-id="b159d-139">Après avoir envoyé le travail, vous pouvez afficher les détails de l’envoi.</span><span class="sxs-lookup"><span data-stu-id="b159d-139">After you submit the job, you can view the submission details.</span></span> <span data-ttu-id="b159d-140">Pour afficher les détails de l’envoi, sélectionnez **jobUrl** dans la fenêtre **Sortie**.</span><span class="sxs-lookup"><span data-stu-id="b159d-140">To view the submission details select **jobUrl** in the **Output** window.</span></span> <span data-ttu-id="b159d-141">Vous pouvez également afficher l’état de l’envoi du travail à partir de la console cmd.</span><span class="sxs-lookup"><span data-stu-id="b159d-141">You can also view the job submission status from the cmd console.</span></span> <span data-ttu-id="b159d-142">Entrez **7** dans la console cmd si vous souhaitez connaître plus de détails sur le travail.</span><span class="sxs-lookup"><span data-stu-id="b159d-142">Enter **7** in the cmd console if you want to know more job details.</span></span>

   <span data-ttu-id="b159d-143">![Data Lake Tools pour Visual Studio Code - Sortie exécution locale](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-run-result.png)
   ![Data Lake Tools pour Visual Studio Code - État cmd exécution locale](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-localrun-cmd-status.png)</span><span class="sxs-lookup"><span data-stu-id="b159d-143">![Data Lake Tools for Visual Studio Code local run output](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-run-result.png)
![Data Lake Tools for Visual Studio Code local run cmd status](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-localrun-cmd-status.png)</span></span> 


## <a name="start-a-local-debug-for-the-u-sql-job"></a><span data-ttu-id="b159d-144">Démarrer un débogage local pour le travail U-SQL</span><span class="sxs-lookup"><span data-stu-id="b159d-144">Start a local debug for the U-SQL job</span></span>  
<span data-ttu-id="b159d-145">Les nouveaux utilisateurs sont invités à télécharger les packages ADL: Download LocalRun Dependency s’ils ne sont pas déjà installés.</span><span class="sxs-lookup"><span data-stu-id="b159d-145">For the first-time user, you are prompted to download the ADL: Download LocalRun Dependency packages if they are not already installed.</span></span>
  
1. <span data-ttu-id="b159d-146">Sélectionnez Ctrl+Maj+P pour ouvrir la palette de commandes, puis entrez **ADL: Start Local Run Service**.</span><span class="sxs-lookup"><span data-stu-id="b159d-146">Select Ctrl+Shift+P to open the command palette, and then enter **ADL: Start Local Run Service**.</span></span> <span data-ttu-id="b159d-147">La console cmd s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="b159d-147">The cmd console opens.</span></span> <span data-ttu-id="b159d-148">Vérifiez que la valeur **DataRoot** est définie.</span><span class="sxs-lookup"><span data-stu-id="b159d-148">Make sure that the **DataRoot** is set.</span></span>
3. <span data-ttu-id="b159d-149">Définissez un point d’arrêt dans votre code C# code-behind.</span><span class="sxs-lookup"><span data-stu-id="b159d-149">Set a breakpoint in your C# code-behind.</span></span>
4. <span data-ttu-id="b159d-150">Dans l’éditeur de script, sélectionnez Ctrl+Maj+P pour ouvrir la console de commandes, puis entrez **Local Debug** pour démarrer votre service de débogage local.</span><span class="sxs-lookup"><span data-stu-id="b159d-150">Back in the script editor, select Ctrl+Shift+P to open the command console, and then enter **Local Debug** to start your local debug service.</span></span>

![Data Lake Tools pour Visual Studio Code - Résultat débogage local](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-debug-result.png)


## <a name="next-steps"></a><span data-ttu-id="b159d-152">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b159d-152">Next steps</span></span>
- <span data-ttu-id="b159d-153">Pour utiliser Azure Data Lake Tools pour Visual Studio Code, consultez [Utilisation d’Azure Data Lake Tools pour Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="b159d-153">For using Azure Data Lake Tools for Visual Studio Code, see [Use Azure Data Lake Tools for Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span></span>
- <span data-ttu-id="b159d-154">Consultez [Didacticiel : Bien démarrer avec Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md) pour obtenir des informations sur la prise en main de Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="b159d-154">For getting started information on Data Lake Analytics, see [Tutorial: Get started with Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).</span></span>
- <span data-ttu-id="b159d-155">Pour obtenir des informations sur l’utilisation de Data Lake Tools pour Visual Studio, consultez [Didacticiel : développer des scripts U-SQL avec Data Lake Tools pour Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="b159d-155">For information about Data Lake Tools for Visual Studio, see [Tutorial: Develop U-SQL scripts by using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
- <span data-ttu-id="b159d-156">Pour plus d’informations sur le développement d’assemblys, consultez [Développement d’assemblys U-SQL pour les tâches d’Azure Data Lake Analytics](data-lake-analytics-u-sql-develop-assemblies.md).</span><span class="sxs-lookup"><span data-stu-id="b159d-156">For the information on developing assemblies, see [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md).</span></span>
