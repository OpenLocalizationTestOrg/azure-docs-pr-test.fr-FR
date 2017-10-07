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
# <a name="u-sql-local-run-and-local-debug-with-visual-studio-code"></a>Exécution locale et débogage local U-SQL avec Visual Studio Code

## <a name="prerequisites"></a>Composants requis
Vérifiez que vous avez hello suivant des conditions préalables en place avant de commencer ces procédures :
- Azure Data Lake Tools pour Visual Studio Code. Pour les instructions, consultez [Utilisation d’Azure Data Lake Tools pour Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).
- C# pour Visual Studio Code (si vous voulez le débogage local de tooperform U-SQL).

   ![Installer C# dans Data Lake Tools pour Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-install-ms-vscodecsharp.png)
   
   > [!NOTE]
   > Hello série locale d’U-SQL et les fonctionnalités de débogage actuellement prennent uniquement en charge les utilisateurs Windows. 


## <a name="set-up-hello-u-sql-local-run-environment"></a>Installer l’environnement d’exécution local hello U-SQL

1. Sélectionnez la palette de commandes Ctrl + Maj + P tooopen hello et entrez **ADL : Téléchargez la dépendance de LocalRun** packages de hello toodownload.  

   ![Télécharger les packages de dépendance de LocalRun ADL hello](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/DownloadLocalRun.png)

2. Recherchez des packages de dépendance hello du chemin d’accès hello illustré hello **sortie** volet, puis installez BuildTools et Win10SDK 10240. Voici un exemple de chemin :  
`C:\Users\xxx\.vscode\extensions\usqlextpublisher.usql-vscode-ext-x.x.x\LocalRunDependency
`  
  ![Recherchez des packages de dépendance hello](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/LocateDependencyPath.png)

   a. tooinstall BuildTools, suivez les instructions de l’Assistant hello.   

  ![Installer BuildTools](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/InstallBuildTools.png)

   b. tooinstall Win10SDK 10240, suivez les instructions de l’Assistant hello.  

  ![Installer Win10SDK 10240](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/InstallWin10SDK.png)

3. Configurer la variable d’environnement hello. Ensemble hello **SCOPE_CPP_SDK** variable d’environnement :  
`C:\Users\xxx\.vscode\extensions\usqlextpublisher.usql-vscode-ext-x.x.x\LocalRunDependency\CppSDK_3rdparty
`  
4. Redémarrez toomake hello du système d’exploitation sûr que les paramètres de variable d’environnement hello prennent effet.  

   ![Vérifiez la variable d’environnement SCOPE_CPP_SDK hello est installé.](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/ConfigScopeCppSDk.png)

## <a name="start-hello-local-run-service-and-submit-hello-u-sql-job-tooa-local-account"></a>Démarrer le service d’exécution local hello et soumettre hello U-SQL travail tooa local compte 
Hello utilisateur, vous êtes hello de toodownload demandées ADL : Téléchargez la dépendance de LocalRun packages s’ils ne sont pas déjà installés.
1. Sélectionnez la palette de commandes Ctrl + Maj + P tooopen hello et entrez **ADL : démarrer le Service d’exécution Local**.
2. Sélectionnez **accepter** tooaccept hello contrat de licence logiciel Microsoft hello première fois. 

   ![Acceptez le contrat de licence logiciel Microsoft hello](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/AcceptEULA.png)   
3. Hello cmd console s’ouvre. Pour les utilisateurs de la première fois, vous devez tooenter **3**, puis recherchez le chemin d’accès du dossier local hello pour vos données d’entrée et sortie. Pour les autres options, vous pouvez utiliser les valeurs par défaut de hello. 

   ![Data Lake Tools pour Visual Studio Code - cmd exécution locale](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-run-cmd.png)
4. Sélectionnez la palette de commandes hello Ctrl + Maj + P tooopen, entrez **ADL : soumettre un travail**, puis sélectionnez **Local** compte local de toosubmit hello travail tooyour.

   ![Data Lake Tools pour Visual Studio Code - Sélectionner Local](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-select-local.png)
5. Après avoir soumis le travail de hello, vous pouvez afficher les détails de l’envoi hello. Sélectionnez des détails de soumission de hello tooview **jobUrl** Bonjour **sortie** fenêtre. Vous pouvez également afficher le statut de la soumission tâche hello à partir de la console de cmd hello. Entrez **7** dans la console hello cmd si vous souhaitez tooknow plus de travail plus d’informations.

   ![Data Lake Tools pour Visual Studio Code - Sortie exécution locale](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-run-result.png)
   ![Data Lake Tools pour Visual Studio Code - État cmd exécution locale](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-localrun-cmd-status.png) 


## <a name="start-a-local-debug-for-hello-u-sql-job"></a>Démarrer un débogage local pour le travail de U-SQL hello  
Hello utilisateur, vous êtes hello de toodownload demandées ADL : Téléchargez la dépendance de LocalRun packages s’ils ne sont pas déjà installés.
  
1. Sélectionnez la palette de commandes Ctrl + Maj + P tooopen hello et entrez **ADL : démarrer le Service d’exécution Local**. Hello cmd console s’ouvre. Vérifiez que hello **DataRoot** est définie.
3. Définissez un point d’arrêt dans votre code C# code-behind.
4. Dans l’éditeur de script hello, sélectionnez console de commande Ctrl + Maj + P tooopen hello et puis entrez **débogage Local** toostart votre service de débogage local.

![Data Lake Tools pour Visual Studio Code - Résultat débogage local](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-debug-result.png)


## <a name="next-steps"></a>Étapes suivantes
- Pour utiliser Azure Data Lake Tools pour Visual Studio Code, consultez [Utilisation d’Azure Data Lake Tools pour Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).
- Consultez [Didacticiel : Bien démarrer avec Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md) pour obtenir des informations sur la prise en main de Data Lake Analytics.
- Pour obtenir des informations sur l’utilisation de Data Lake Tools pour Visual Studio, consultez [Didacticiel : développer des scripts U-SQL avec Data Lake Tools pour Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).
- Pour plus d’informations hello sur le développement des assemblys, consultez [assemblys développer U-SQL pour les travaux de l’Analytique de LAC de données Azure](data-lake-analytics-u-sql-develop-assemblies.md).
