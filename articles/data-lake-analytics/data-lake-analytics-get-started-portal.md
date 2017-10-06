---
title: "aaaGet démarré avec Analytique de LAC de données Azure à l’aide du portail Azure | Documents Microsoft"
description: "Découvrez comment toouse hello toocreate portail Azure un compte Analytique lac de données, créez une tâche Analytique lac de données à l’aide de U-SQL et envoi de la tâche de hello. "
services: data-lake-analytics
documentationcenter: 
author: edmacauley
manager: jhubbard
editor: cgronlun
ms.assetid: b1584d16-e0d2-4019-ad1f-f04be8c5b430
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/21/2017
ms.author: edmaca
ms.openlocfilehash: 6bb54404fa42cfed25b18bc2bfb7c72e6c361149
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-azure-portal"></a>Prise en main d’Azure Data Lake Analytics à l’aide du Portail Azure
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

Découvrez comment toouse hello Azure toocreate portail des comptes Analytique de LAC de données Azure, définir des travaux dans [U-SQL](data-lake-analytics-u-sql-get-started.md)et soumettre le service de données Lake Analytique toohello travaux. Pour plus d’informations sur Analytique Data Lake, consultez [Présentation d’Analytique Data Lake Azure](data-lake-analytics-overview.md).

## <a name="prerequisites"></a>Composants requis

Avant de commencer ce didacticiel, vous devez disposer d’un **abonnement Azure**. Consultez la rubrique [Obtenir une version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/).

## <a name="create-a-data-lake-analytics-account"></a>Créer un compte Data Lake Analytics

Maintenant, vous allez créer un Analytique lac de données et un magasin Data Lake Store compte hello même temps.  Cette étape est simple et seulement prend environ 60 secondes toofinish.

1. Ouverture de session toohello [portail Azure](https://portal.azure.com).
2. Cliquez sur **Nouveau** >  **Données + analyse** > **Data Lake Analytics**.
3. Sélectionnez les valeurs de hello éléments suivants :
   * **Nom** : donnez un nom à votre compte Data Lake Analytics (utilisez uniquement des lettres minuscules et des chiffres).
   * **Abonnement**: choisissez hello abonnement Azure utilisé pour le compte de l’Analytique de hello.
   * **Groupe de ressources**. Sélectionnez un groupe de ressources Azure existant ou créez-en un.
   * **Emplacement**. Sélectionnez un centre de données Azure pour compte Analytique lac de données de hello.
   * **Data Lake Store**: suivez hello instruction toocreate un nouveau compte Data Lake Store, ou sélectionnez-en un existant. 
4. Si vous le souhaitez, sélectionnez un niveau tarifaire pour votre compte Data Lake Analytics.
5. Cliquez sur **Create**. 


## <a name="your-first-u-sql-script"></a>Votre premier script U-SQL

Hello suivant le texte est un script U-SQL très simple. Il se définissent un jeu de données petit script de hello, puis écrivez ce jeu de données sortantes Data Lake Store toohello par défaut comme un fichier appelé `/data.csv`.

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

## <a name="submit-a-u-sql-job"></a>Envoyer un travail U-SQL

1. À partir de hello compte d’Analytique lac de données, cliquez sur **nouveau travail**.
2. Collez le texte hello Hello script U-SQL ci-dessus. 
3. Cliquez sur **Envoyer le travail**.   
4. Patientez jusqu'à ce que les changements d’état de tâche de hello trop**Succeeded**.
5. En cas d’échec de la tâche de hello, consultez [moniteur et résoudre les problèmes de travaux d’Analytique lac de données](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md).
6. Cliquez sur hello **sortie** onglet, puis cliquez sur `data.csv`. 

## <a name="see-also"></a>Voir aussi

* tooget en main le développement d’applications SQL-U, consultez [scripts développer U-SQL à l’aide de Data Lake Tools pour Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).
* toolearn U-SQL, consultez [prise en main langage lac de données Azure Analytique U-SQL](data-lake-analytics-u-sql-get-started.md).
* Pour les tâches de gestion, consultez [Gestion d’Azure Data Lake Analytics à l’aide du portail Azure](data-lake-analytics-manage-use-portal.md).
