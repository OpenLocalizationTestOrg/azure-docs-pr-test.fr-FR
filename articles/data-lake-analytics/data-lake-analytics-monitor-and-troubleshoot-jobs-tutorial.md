---
title: "travaux d’Analytique de LAC de données Azure aaaTroubleshoot à l’aide du portail Azure | Documents Microsoft"
description: "Découvrez comment toouse hello travaux de portail Azure tootroubleshoot Analytique lac de données. "
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: b7066d81-3142-474f-8a34-32b0b39656dc
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: e810d56bab8f1a8254721ec9906bb6a4508dc22a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-data-lake-analytics-jobs-using-azure-portal"></a>Dépanner les travaux Azure Data Lake Analytics à l’aide du portail Azure
Découvrez comment toouse hello travaux de portail Azure tootroubleshoot Analytique lac de données.

Dans ce didacticiel, vous le programme d’installation d’un problème de fichier source manquant et utiliser hello Azure Portal tootroubleshoot hello problème.

## <a name="submit-a-data-lake-analytics-job"></a>Envoyer le travail Analytique Data Lake

Soumettre hello suivant travail U-SQL :

```
@searchlog =
   EXTRACT UserId          int,
           Start           DateTime,
           Region          string,
           Query           string,
           Duration        int?,
           Urls            string,
           ClickedUrls     string
   FROM "/Samples/Data/SearchLog.tsv1"
   USING Extractors.Tsv();

OUTPUT @searchlog   
   too"/output/SearchLog-from-adls.csv"
   USING Outputters.Csv();
```
    
Bonjour fichier source défini dans le script de hello est **/Samples/Data/SearchLog.tsv1**, où il doit être **/Samples/Data/SearchLog.tsv**.


## <a name="troubleshoot-hello-job"></a>Résoudre les problèmes des travaux de hello

**toosee tous hello travaux**

1. À partir de hello portail Azure, cliquez sur **Microsoft Azure** dans le coin supérieur gauche de hello.
2. Cliquez sur mosaïque hello avec le nom de votre compte Analytique lac de données.  Résumé des tâches Hello sont indiquée sur hello **gestion des travaux** vignette.

    ![Gestion du travail Analytique Data Lake Azure](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-job-management.png)

    le travail Hello gestion vous donne un aperçu de l’état de la tâche hello. Notez qu’il s’agit d’une tâche ayant échoué.
3. Cliquez sur hello **gestion des travaux** vignette des travaux de hello toosee. travaux de Hello est classées en **en cours d’exécution**, **en file d’attente**, et **terminé**. Vous allez voir votre travail ayant échoué Bonjour **terminé** section. Il doit être dans la liste de hello. Lorsque vous avez un grand nombre de travaux, vous pouvez cliquer sur **filtre** toohelp vous toolocate travaux.

    ![Travail de filtre d’Analytique Data Lake Azure](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-filter-jobs.png)
4. Cliquez sur hello le travail ayant échoué à partir de hello liste tooopen hello détails d’une tâche dans un nouveau panneau :

    ![Travail d’échec d’Analytique Data Lake Azure](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-failed-job.png)

    Hello d’avis **renvoyer** bouton. Après avoir corrigé le problème de hello, vous pouvez renvoyer le travail de hello.
5. Cliquez sur la partie en surbrillance de hello précédente capture d’écran tooopen hello détails de l’erreur.  Le résultat suivant doit s’afficher :

    ![Détails sur le travail d’échec d’Analytique Data Lake Azure](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-failed-job-details.png)

    Il indique le dossier source de hello est introuvable.
6. Cliquez sur **Dupliquer le Script**.
7. Hello de mise à jour **FROM** toohello chemin qui suit :

    « Samples/Data/SearchLog.tsv »
8. Cliquez sur **Envoyer le travail**.

## <a name="see-also"></a>Voir aussi
* [Présentation d’Analytique Data Lake Azure](data-lake-analytics-overview.md)
* [Prise en main d’Analytique Data Lake à l’aide d’Azure PowerShell](data-lake-analytics-get-started-powershell.md)
* [Prise en main d’Analytique Data Lake Azure et U-SQL à l’aide de Visual Studio.](data-lake-analytics-u-sql-get-started.md)
* [Gestion d'Azure Data Lake Analytics à l'aide du portail Azure](data-lake-analytics-manage-use-portal.md)
