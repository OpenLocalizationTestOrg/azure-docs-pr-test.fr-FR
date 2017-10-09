---
title: "groupes aaaManage de bases de données SQL Azure | Documents Microsoft"
description: "Passez en revue la création et la gestion d’une tâche élastique."
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: f858344d-085b-4022-935e-1b5fa20adbac
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: a73c4fb24c332fae0e917c18272724cccd56f29a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-scaled-out-azure-sql-databases-using-elastic-jobs-preview"></a>Créer et gérer des bases de données SQL Azure avec montée en charge à l’aide de tâches élastiques (version préliminaire)


**tâches de bases de données élastiques** simplifient la gestion des groupes de bases de données en exécutant des opérations administratives telles que les modifications de schéma, la gestion des informations d’identification, les mises à jour de données de référence, la collecte des données de performances ou la collecte de données de télémétrie du locataire (client). Les travaux de base de données élastiques est actuellement disponible via hello portail Azure et les applets de commande PowerShell. Toutefois, hello surfaces du portail Azure des fonctionnalités réduites limité tooexecution sur toutes les bases de données dans un [pool élastique (version préliminaire)](sql-database-elastic-pool.md). tooaccess des fonctionnalités supplémentaires et l’exécution de scripts sur un groupe de bases de données, notamment une collection personnalisée ou une partition définie (créé à l’aide de [bibliothèque cliente de base de données élastique](sql-database-elastic-scale-introduction.md)), consultez [création et gestion travaux à l’aide de PowerShell](sql-database-elastic-jobs-powershell.md). Pour en savoir plus sur les tâches, consultez la rubrique [Vue d'ensemble des tâches de bases de données élastiques](sql-database-elastic-jobs-overview.md). 

## <a name="prerequisites"></a>Composants requis
* Un abonnement Azure. Pour un essai gratuit, consultez [Version d'évaluation gratuite](https://azure.microsoft.com/pricing/free-trial/).
* Un pool élastique. Voir [À propos des pools élastiques](sql-database-elastic-pool.md).
* Installation des composants du service de tâches de bases de données élastiques. Consultez [installation du service de travail de base de données élastique hello](sql-database-elastic-jobs-service-installation.md).

## <a name="creating-jobs"></a>Création de travaux
1. À l’aide de hello [portail Azure](https://portal.azure.com), à partir d’un pool de travail élastique de base de données existant, cliquez sur **travail de création de**.
2. Tapez dans le nom d’utilisateur hello et un mot de passe d’administrateur de base de données hello (créé à l’installation de travaux) de base de données de contrôle hello travaux (stockage des métadonnées pour les travaux).
   
    ![Nom du travail hello, tapez ou collez dans le code, puis cliquez sur Exécuter][1]
3. Bonjour **créer une tâche** panneau, tapez un nom pour le travail de hello.
4. Tapez hello nom et mot de passe tooconnect toohello cible bases de données utilisateur disposant d’autorisations suffisantes pour toosucceed de l’exécution du script.
5. Collez ou tapez dans le script de hello T-SQL.
6. Cliquez sur **Enregistrer**, puis sur **Exécuter**.
   
    ![Créez des tâches et exécutez-les.][5]

## <a name="run-idempotent-jobs"></a>Exécution de tâches idempotent
Lorsque vous exécutez un script sur un ensemble de bases de données, vous devez être sûr que le script de hello est idempotente. Autrement dit, hello script doit être en mesure de toorun plusieurs fois, même si elle a échoué avant dans un état incomplet. Par exemple, lorsqu’un script échoue, le travail de hello sera automatiquement retentée jusqu'à ce qu’il réussisse (dans les limites, en tant que nouvelle tentative de hello logique finalement cessera hello une nouvelle tentative). toodo de façon Hello est toouse hello une clause « IF EXISTS » et supprimez toute instance trouvée avant de créer un nouvel objet. Voici un exemple :

    IF EXISTS (SELECT name FROM sys.indexes
            WHERE name = N'IX_ProductVendor_VendorID')
    DROP INDEX IX_ProductVendor_VendorID ON Purchasing.ProductVendor;
    GO
    CREATE INDEX IX_ProductVendor_VendorID
    ON Purchasing.ProductVendor (VendorID);

Vous pouvez également utiliser une clause « IF NOT EXISTS » avant de créer une instance :

    IF NOT EXISTS (SELECT name FROM sys.tables WHERE name = 'TestTable')
    BEGIN
     CREATE TABLE TestTable(
      TestTableId INT PRIMARY KEY IDENTITY,
      InsertionTime DATETIME2
     );
    END
    GO

    INSERT INTO TestTable(InsertionTime) VALUES (sysutcdatetime());
    GO

Ce script met ensuite à jour la table hello créé précédemment.

    IF NOT EXISTS (SELECT columns.name FROM sys.columns INNER JOIN sys.tables on columns.object_id = tables.object_id WHERE tables.name = 'TestTable' AND columns.name = 'AdditionalInformation')
    BEGIN

    ALTER TABLE TestTable

    ADD AdditionalInformation NVARCHAR(400);
    END
    GO

    INSERT INTO TestTable(InsertionTime, AdditionalInformation) VALUES (sysutcdatetime(), 'test');
    GO


## <a name="checking-job-status"></a>Vérification du statut de la tâche
Une fois la tâche lancée, vous pouvez vérifier son statut.

1. Dans la page de pool élastique hello, cliquez sur **gérer les travaux**.
   
    ![Cliquez sur « Gérer les tâches ».][2]
2. Cliquez sur hello nom (a) d’une tâche. Hello **état** peut être « Completed » ou « Échec ». Détails de la tâche Hello apparaissent (b) avec la date et l’heure de création et l’exécution. liste de Hello (c) ci-dessous hello qui affiche la progression de hello du script hello sur chaque base de données dans le pool de hello, précisant la date et l’heure.
   
    ![Vérification d'une tâche terminée][3]

## <a name="checking-failed-jobs"></a>Vérification des tâches ayant échoué
Si une tâche échoue, un journal détaillant son exécution est créé. Cliquez sur nom hello hello échoué de la tâche toosee ses détails.

![Vérifier une tâche ayant échoué][4]

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-create-and-manage/screen-1.png
[2]: ./media/sql-database-elastic-jobs-create-and-manage/click-manage-jobs.png
[3]: ./media/sql-database-elastic-jobs-create-and-manage/running-jobs.png
[4]: ./media/sql-database-elastic-jobs-create-and-manage/failed.png
[5]: ./media/sql-database-elastic-jobs-create-and-manage/screen-2.png


