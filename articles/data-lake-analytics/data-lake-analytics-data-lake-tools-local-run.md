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
# <a name="test-and-debug-u-sql-jobs-by-using-local-run-and-hello-azure-data-lake-u-sql-sdk"></a>Tester et déboguer des travaux U-SQL à l’aide locale exécuter et hello Kit de développement logiciel Azure données Lake U-SQL

Vous pouvez utiliser Azure Data Lake Tools pour Visual Studio et les travaux de hello SQL-U de LAC de données Azure SDK toorun U-SQL sur votre station de travail, comme vous le faites dans le service Azure Data Lake hello. Ces deux fonctionnalités d’exécution locale accélèrent les procédures de test et de débogage de vos travaux U-SQL.

## <a name="understand-hello-data-root-folder-and-hello-file-path"></a>Comprendre le dossier de données racine hello et chemin d’accès du fichier hello

Exécution locale et hello U-SQL SDK requièrent un dossier racine de données. dossier de données racine de Hello est un « magasin local » pour le compte de calcul local hello. Il est le compte d’Azure Data Lake Store toohello équivalent d’un compte Analytique lac de données. Dossier de données-racine différent tooa de commutation est identique à commutation tooa autre banque de compte. Si vous souhaitez tooaccess fréquemment les données partagées avec des dossiers racine de données différents, vous devez utiliser des chemins d’accès absolus dans vos scripts. Ou bien, créez des liens symboliques de système de fichier (par exemple, **mklink** sur NTFS) sous hello racine de données dossier toopoint toohello les données partagées.

dossier de données racine Hello est utilisé pour :

- Stocker les métadonnées, notamment des bases de données, des tables, des fonctions table (TVF) et des assemblys.
- Rechercher hello d’entrée et les chemins d’accès de sortie sont définies comme des chemins d’accès relatifs dans U-SQL. À l’aide de chemins d’accès relatifs rend plus facile toodeploy votre tooAzure de projets U-SQL.

Vous pouvez utiliser un chemin d’accès relatif et un chemin d’accès absolu local dans des scripts SQL-U. chemin d’accès relatif de Hello est le chemin d’accès au dossier toohello relatif racine de données spécifié. Il est recommandé que vous utilisez « / » comme hello toomake de séparateur de chemin d’accès de vos scripts compatibles avec SSI hello. Voici quelques exemples de chemins relatifs, avec leurs chemins absolus équivalents. Dans ces exemples, C:\LocalRunDataRoot est le dossier racine de données de hello.

|Chemin relatif|Chemin absolu|
|-------------|-------------|
|/abc/def/input.csv |C:\LocalRunDataRoot\abc\def\input.csv|
|abc/def/input.csv  |C:\LocalRunDataRoot\abc\def\input.csv|
|D:/abc/def/input.csv |D:\abc\def\input.csv|

## <a name="use-local-run-from-visual-studio"></a>Utiliser l’exécution locale depuis Visual Studio

Data Lake Tools pour Visual Studio fournit une expérience d’exécution locale U-SQL dans Visual Studio. À l’aide de cette fonctionnalité, vous pouvez :

- Exécuter des scripts U-SQL en local, ainsi que des assemblys C#.
- Déboguer un assembly C# en local.
- Créer, afficher et supprimer des catalogues U-SQL (bases de données locales, assemblys, schémas et tables) de l’Explorateur de serveurs. Vous trouverez également les catalogue local hello également à partir de l’Explorateur de serveurs.

    ![Data Lake Tools pour Visual Studio exécution locale catalogue local](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-local-catalog.png)

programme d’installation de Data Lake Tools Hello crée un toobe du dossier C:\LocalRunRoot utilisé comme dossier de données racine par défaut hello. parallélisme de local-exécuter Hello par défaut est 1.

### <a name="tooconfigure-local-run-in-visual-studio"></a>tooconfigure local s’exécutent dans Visual Studio

1. Ouvrez Visual Studio.
2. Ouvrez l’**Explorateur de serveurs**.
3. Développez **Azure** > **Data Lake Analytics**.
4. Cliquez sur hello **Data Lake** menu, puis sur **Options et paramètres**.
5. Dans l’arborescence de hello gauche, développez **Azure Data Lake**, puis développez **général**.

    ![Data Lake Tools pour Visual Studio exécution locale configurer paramètres](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-configure.png)

Un projet U-SQL Visual Studio est requis pour exécuter l’exécution locale. Cette partie diffère de l'exécution de scripts U-SQL à partir d'Azure.

### <a name="toorun-a-u-sql-script-locally"></a>script toorun U-SQL localement
1. Dans Visual Studio, ouvrez votre projet U-SQL.   
2. Cliquez avec le bouton droit sur un script U-SQL dans l'Explorateur de solutions, puis cliquez sur **Soumettre le script**.
3. Sélectionnez **(Local)** compte d’identification hello Analytique toorun localement votre script.
Vous pouvez également cliquer sur hello **(Local)** compte haut hello de fenêtre de script, puis cliquez sur **Submit** (ou utilisez Bonjour Ctrl + F5 raccourci).

    ![Data Lake Tools pour Visual Studio exécution locale soumettre travaux](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-submit-job.png)

### <a name="debug-scripts-and-c-assemblies-locally"></a>Déboguer localement des scripts et des assemblys C#

Vous pouvez déboguer des assemblys c# sans l’envoi et de son inscription tooAzure Service Analytique de LAC de données. Vous pouvez définir des points d’arrêt dans les deux hello fichier code-behind et dans un projet c# référencé.

#### <a name="toodebug-local-code-in-code-behind-file"></a>toodebug de codes locale dans le fichier code-behind

1. Définir des points d’arrêt dans hello fichier code-behind.
2. Appuyez sur F5 toodebug script hello localement.

> [!NOTE]
   > Hello suivant la procédure ne fonctionne que dans Visual Studio 2015. Dans les plus anciennes de Visual Studio, vous devrez peut-être ajouter des fichiers pdb de hello toomanually.  
   >
   >

#### <a name="toodebug-local-code-in-a-referenced-c-project"></a>toodebug le code local dans un projet c# référencé

1. Créer un projet d’Assembly c# et le générer toogenerate hello sortie dll.
2. Inscrire la dll hello à l’aide d’une instruction U-SQL :

        CREATE ASSEMBLY assemblyname FROM @"..\..\path\to\output\.dll";
        
3. Définir des points d’arrêt dans le code c# de hello.
4. Appuyez sur F5 script de hello toodebug avec faisant référence à la dll hello c# localement.

## <a name="use-local-run-from-hello-data-lake-u-sql-sdk"></a>Utilisez local, exécutez à partir de hello SDK de données Lake U-SQL

En outre toorunning U-SQL scripts localement à l’aide de Visual Studio, vous pouvez utiliser des scripts de hello SQL-U de LAC de données Azure SDK toorun U-SQL localement avec les interfaces de ligne de commande et de programmation. Par ce biais, vous pouvez mettre votre test local U-SQL à l’échelle.

En savoir plus sur le [Kit de développement logiciel (SDK) U-SQL Azure Data Lake](data-lake-analytics-u-sql-sdk.md).


## <a name="next-steps"></a>Étapes suivantes

* toosee une requête plus complexe, consultez [analyser les journaux du site Web à l’aide d’Analytique de LAC de données Azure](data-lake-analytics-analyze-weblogs.md).
* Détails de la tâche tooview, consultez [navigateur de travail d’utilisation et de la vue des travaux pour les travaux de l’Analytique de LAC de données Azure](data-lake-analytics-data-lake-tools-view-jobs.md).
* vue de l’exécution toouse hello vertex, consultez [hello d’utilisation vue de l’exécution de sommets dans Data Lake Tools pour Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).
