---
title: "les scripts aaaDevelop U-SQL à l’aide de Data Lake Tools pour Visual Studio | Documents Microsoft"
description: "Découvrez comment tooinstall Data Lake Tools pour Visual Studio et les scripts U-SQL toodevelop et de test."
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: jhubbard
editor: cgronlun
ms.assetid: ad8a6992-02c7-47d4-a108-62fc5a0777a3
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/28/2017
ms.author: saveenr, yanacai
ms.openlocfilehash: 7a0c02c275b8cefecbe784ba63969cbf24a150d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-u-sql-scripts-by-using-data-lake-tools-for-visual-studio"></a>Développer des scripts U-SQL à l’aide des outils Data Lake pour Visual Studio
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]


Découvrez comment toouse Visual Studio toocreate Analytique de LAC de données Azure des comptes, définir des travaux dans [U-SQL](data-lake-analytics-u-sql-get-started.md)et soumettre le service de données Lake Analytique toohello travaux. Pour plus d’informations sur Analytique Data Lake, consultez [Présentation d’Analytique Data Lake Azure](data-lake-analytics-overview.md).


## <a name="prerequisites"></a>Composants requis

* **Visual Studio** : toutes les éditions sauf Express sont prises en charge.
    * Visual Studio 2017
    * Visual Studio 2015
    * Visual Studio 2013
* **Kit SDK Microsoft Azure pour .NET** version 2.7.1 ou ultérieure.  Installez-le à l’aide de hello [le programme d’installation de Web platform](http://www.microsoft.com/web/downloads/platform.aspx).
* Un compte**Data Lake Analytics**. toocreate un compte, consultez [prise en main Analytique de LAC de données Azure à l’aide du portail Azure](data-lake-analytics-get-started-portal.md).

## <a name="install-azure-data-lake-tools-for-visual-studio"></a>Installer Azure Data Lake Tools pour Visual Studio 

Téléchargez et installez Azure Data Lake Tools pour Visual Studio [à partir du centre de téléchargement de hello](http://aka.ms/adltoolsvs). Après l’installation, notez les points suivants :
* Hello **l’Explorateur de serveurs** > **Azure** nœud contient un **Analytique lac de données** nœud. 
* Hello **outils** menu a un **Data Lake** élément.

## <a name="connect-tooan-azure-data-lake-analytics-account"></a>Tooan Analytique de LAC de données Azure compte de connexion

1. Ouvrez Visual Studio.
2. Ouvrez l’Explorateur de serveurs en sélectionnant **Afficher** > **Explorateur de serveurs**.
3. Cliquez avec le bouton droit sur **Azure**. Puis sélectionnez **connecter tooMicrosoft abonnement Azure** et suivez les instructions de hello.
4. Dans l’Explorateur de serveurs, sélectionnez **Azure** > **Data Lake Analytics**. Une liste des comptes Data Lake Analytics s’affiche.


## <a name="write-your-first-u-sql-script"></a>Rédiger son premier script U-SQL

Hello suivant le texte est un simple script U-SQL. Il définit un petit jeu de données et les écritures Data Lake Store dataset toohello par défaut comme un fichier appelé `/data.csv`.

```
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS 
              D( customer, amount );
OUTPUT @a
    too"/data.csv"
    USING Outputters.Csv();
```

### <a name="submit-a-data-lake-analytics-job"></a>Envoyer le travail Analytique Data Lake

1. Sélectionnez **Fichier** > **Nouveau** > **Projet**.

2. Sélectionnez hello **U-SQL projet** , puis tapez **OK**. Visual Studio crée une solution avec un fichier **Script.usql**.

3. Coller le script précédent de hello dans hello **Script.usql** fenêtre.

4. Dans le coin supérieur gauche de hello Hello **Script.usql** fenêtre, spécifiez hello Analytique lac de données compte.

    ![Soumettre un projet U-SQL Visual Studio](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-submit-job.png)

5. Dans le coin supérieur gauche de hello Hello **Script.usql** fenêtre, sélectionnez **Submit**.
6. Vérifiez que hello **Analytique compte**, puis sélectionnez **Submit**. Résultats de la soumission sont disponibles dans hello Data Lake Tools pour Visual Studio résultats après que l’envoi de hello est terminée.

    ![Soumettre un projet U-SQL Visual Studio](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-submit-job-advanced.png)
7. toosee hello dernier travail état et l’actualisation hello écran, cliquez sur **Actualiser**. Lors de la réussite du travail de hello, il affiche hello **travail graphique**, **des opérations de métadonnées**, **historique de l’état**, et **Diagnostics**:

    ![Graphique des performances du travail U-SQL Visual Studio Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-performance-graph.png)

   * **Résumé du travail** affiche hello résumé du travail de hello.   
   * **Détails de la tâche** affiche des informations plus spécifiques sur la tâche hello, y compris le script de hello, des ressources et des sommets.
   * **Graphique de travail** visualise progression hello de hello.
   * **Opérations de métadonnées** montre toutes les actions hello qui ont été effectuées sur le catalogue de hello U-SQL.
   * **Données** affiche toutes les entrées de hello et sorties.
   * **Diagnostics** fournit une analyse avancée pour l’optimisation des performances et de l’exécution des travaux.

### <a name="toocheck-job-state"></a>état de la tâche toocheck

1. Dans l’Explorateur de serveurs, sélectionnez **Azure** > **Data Lake Analytics**. 
2. Développez le nom du compte hello Analytique lac de données.
3. Double-cliquez sur **Travaux**.
4. Sélectionnez la tâche hello que vous avez déjà envoyé.

### <a name="toosee-hello-output-of-a-job"></a>sortie de hello toosee d’une tâche

1. Dans l’Explorateur de serveurs, parcourir le travail toohello que vous avez envoyé.
2. Cliquez sur hello **données** onglet.
3. Bonjour **de sorties de travail** onglet, sélectionnez hello `"/data.csv"` fichier.

## <a name="next-steps"></a>Étapes suivantes

* [Run U-SQL scripts on your own workstation for testing and debugging (Exécuter des scripts U-SQL sur votre station de travail pour les tests et le débogage)](data-lake-analytics-data-lake-tools-local-run.md)
* [Débogage de travaux U-SQL](data-lake-analytics-debug-u-sql-jobs.md)
* [Utilisez hello Azure Data Lake Tools pour Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md)
