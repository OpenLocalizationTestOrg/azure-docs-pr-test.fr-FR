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
# <a name="debug-user-defined-c-code-for-failed-u-sql-jobs"></a>Débogage de code C# défini par l’utilisateur pour des travaux U-SQL ayant échoué

U-SQL fournit un modèle d’extensibilité en c#, donc vous pouvez écrire vos fonctionnalités de tooadd code tel qu’un extracteur personnalisé ou un réducteur. toolearn, voir [guide de programmation U-SQL](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-u-sql-programmability-guide#use-user-defined-functions-udf). Dans la pratique, tout code peut nécessiter un débogage, et les systèmes de Big Data ne peuvent fournir, pour le débogage du runtime, que des informations limitées, telles que des fichiers journaux.

Azure Data Lake Tools pour Visual Studio fournit une fonctionnalité appelée **Échec de la déboguer de sommets**, ce qui vous permet de cloner une tâche ayant échoué à partir de l’ordinateur local tooyour cloud hello pour le débogage. clone de local Hello capture hello entière environnement cloud, y compris les données d’entrée et le code utilisateur.

Hello vidéo suivante montre échec sommets déboguer dans Azure Data Lake Tools pour Visual Studio.

> [!VIDEO https://e0d1.wpc.azureedge.net/80E0D1/OfficeMixProdMediaBlobStorage/asset-d3aeab42-6149-4ecc-b044-aa624901ab32/b0fc0373c8f94f1bb8cd39da1310adb8.mp4?sv=2012-02-12&sr=c&si=a91fad76-cfdd-4513-9668-483de39e739c&sig=K%2FR%2FdnIi9S6P%2FBlB3iLAEV5pYu6OJFBDlQy%2FQtZ7E7M%3D&se=2116-07-19T09:27:30Z&rscd=attachment%3B%20filename%3DDebugyourcustomcodeinUSQLADLA.mp4]
>

> [!NOTE]
> Visual Studio requiert hello suivant deux mises à jour, s’ils ne sont pas déjà installés : [Microsoft Visual C++ 2015 Redistributable Update 3](https://www.microsoft.com/en-us/download/details.aspx?id=53840) et [Universal Runtime C pour Windows](https://www.microsoft.com/download/details.aspx?id=50410).

## <a name="download-failed-vertex-toolocal-machine"></a>Échec du téléchargement du sommet toolocal machine

Lorsque vous ouvrez une tâche ayant échoué dans Azure Data Lake Tools pour Visual Studio, vous voyez une barre jaune alerte avec des messages d’erreur détaillés dans l’onglet d’erreur hello.

1. Cliquez sur **télécharger** toodownload tous hello requis des ressources et les flux d’entrée. Si le téléchargement de hello ne se termine, cliquez sur **réessayer**.

2. Cliquez sur **ouvrir** après le téléchargement de hello terminé toogenerate un environnement de débogage local. Une nouvelle instance Visual Studio avec une solution de débogage est automatiquement créée et ouverte.

![Télécharger le vertex Visual Studio pour le débogage U-SQL Azure Data Lake Analytics](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-download-vertex.png)

Les travaux peuvent inclure des fichiers sources code-behind ou des assemblys inscrits, et les scénarios de débogage diffèrent pour ces deux types.

- [Débogage de tâches ayant échoué avec code-behind](#debug-job-failed-with-code-behind)
- [Débogage de tâches ayant échoué avec des assemblys](#debug-job-failed-with-assemblies)


## <a name="debug-job-failed-with-code-behind"></a>Débogage de tâches ayant échoué avec code-behind

Si un travail U-SQL échoue et que le travail de hello inclut le code utilisateur (généralement nommé `Script.usql.cs` dans un projet U-SQL), que code source est importé dans hello déboguer la solution.  À partir de là, vous pouvez utiliser problème de hello Visual Studio débogage outils (espion, variables, etc.) tootroubleshoot hello.

> [!NOTE]
> Avant le débogage, être vraiment toocheck **Exceptions Common Language Runtime** dans la fenêtre de paramètres d’Exception hello (**Ctrl + Alt + E**).

![Configuration de Visual Studio pour le débogage U-SQL Azure Data Lake Analytics](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-clr-exception-setting.png)

1. Appuyez sur **F5** code de code-behind toorun hello. Celui-ci s’exécute jusqu'à ce qu’il soit arrêté par une exception.

2. Ouvrez hello `ADLTool_Codebehind.usql.cs` de fichiers et de définir des points d’arrêt, puis appuyez sur **F5** code de hello toodebug étape par étape.

    ![Exception de débogage U-SQL Azure Data Lake Analytics](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-debug-exception.png)

## <a name="debug-job-failed-with-assemblies"></a>Débogage de tâches ayant échoué avec des assemblys

Si vous utilisez des assemblys inscrits dans votre script U-SQL, système de hello Impossible d’obtenir hello source code automatiquement. Dans ce cas, ajouter manuellement source code fichiers toohello la solution les assemblys hello.

### <a name="configure-hello-solution"></a>Configurer une solution de hello

1. Avec le bouton droit **Solution 'VertexDebug' > Ajouter > projet existant...**  toofind hello de code source d’assemblys et ajouter toohello de projet hello déboguer la solution.

    ![Projet d’ajout de débogage U-SQL Azure Data Lake Analytics](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-add-project-to-debug-solution.png)

2. Avec le bouton droit **LocalVertexHost > Propriétés** Bonjour de solution et copie hello **du répertoire de travail** chemin d’accès.

3. Avec le bouton droit **projet de code source assembly > Propriétés**, sélectionnez hello **générer** onglet située à gauche et collez le chemin d’accès de hello copié en tant que **sortie > chemin de sortie**.

    ![Chemin d’accès de pdb de définition de débogage U-SQL Azure Data Lake Analytics](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-set-pdb-path.png)

4. Appuyez sur **Ctrl + Alt + E**, vérifiez les **exceptions Common Language Runtime** dans la fenêtre des paramètres d’exception.

### <a name="start-debug"></a>Début du débogage

1. Avec le bouton droit **projet de code source assembly > reconstruire** toohello les fichiers .pdb de toooutput `LocalVertexHost` répertoire de travail.

2. Appuyez sur **F5** et projet de hello s’exécute jusqu'à ce qu’elle soit arrêtée par une exception. Vous pouvez voir hello après le message d’avertissement, vous pouvez ignorer en toute sécurité. Peut prendre jusqu'à l’écran de débogage toohello tooa tooget minute.

    ![Avertissement Visual Studio pour le débogage U-SQL Azure Data Lake Analytics](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-visual-studio-u-sql-debug-warning.png)

3. Ouvrez votre code source et de définir des points d’arrêt, puis appuyez sur **F5** code de hello toodebug étape par étape.

Vous pouvez également utiliser le problème de hello Visual Studio débogage outils (espion, variables, etc.) tootroubleshoot hello.

> [!NOTE]
> Régénérez le projet de code source assembly hello chaque fois après avoir modifié les fichiers .pdb de hello code toogenerate mis à jour.

Après le débogage, si le projet de hello se termine correctement fenêtre de sortie de hello affiche hello message suivant :

```
hello Program 'LocalVertexHost.exe' has exited with code 0 (0x0).
```

![Débogage U-SQL Azure Data Lake Analytics réussi](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-debug-succeed.png)

## <a name="resubmit-hello-job"></a>Soumettez à nouveau le travail de hello

Une fois que vous avez terminé le débogage, soumettez à nouveau hello du travail ayant échoué.

1. Pour les travaux avec les solutions de code-behind, copier votre code c# dans le fichier de source de code-behind hello (généralement `Script.usql.cs`).
2. Pour les travaux avec les assemblys, inscrire hello mis à jour d’assemblys .dll dans votre base de données ADLA :
    1. À partir de l’Explorateur de serveurs ou Cloud Explorer, développez hello **compte ADLA > bases de données** nœud.
    2. Avec le bouton droit **assemblys** et enregistrer vos nouveaux assemblys .dll avec la base de données ADLA hello : ![débogage de LAC de données Azure Analytique U-SQL inscrire l’assembly](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-register-assembly.png)
3. Renvoyez le travail.

## <a name="next-steps"></a>Étapes suivantes

- [Guide de programmabilité U-SQL](data-lake-analytics-u-sql-programmability-guide.md)
- [Développer des opérateurs U-SQL définis par l’utilisateur pour des travaux Azure Data Lake Analytics](data-lake-analytics-u-sql-develop-user-defined-operators.md)
- [Didacticiel : Développer des scripts U-SQL avec Data Lake Tools pour Visual Studio](data-lake-analytics-data-lake-tools-get-started.md)
