---
title: "aaaGuide pour l’utilisation de PolyBase dans SQL Data Warehouse | Documents Microsoft"
description: "Instructions et recommandations relatives à l'utilisation de PolyBase dans les scénarios SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: 4757fce1-96b3-48ea-8a51-be1385705f9f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 6/5/2016
ms.custom: loading
ms.author: cakarst;barbkess
ms.openlocfilehash: b05e4c5d528f2fe1c60d6855b5333065f0c908ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="guide-for-using-polybase-in-sql-data-warehouse"></a>Guide d'utilisation de PolyBase dans SQL Data Warehouse
Ce guide fournit des informations pratiques pour l'utilisation de PolyBase dans SQL Data Warehouse.

tooget démarré, consultez hello [charger des données avec PolyBase] [ Load data with PolyBase] didacticiel.

## <a name="rotating-storage-keys"></a>Rotation des clés de stockage
À partir de tootime de temps, vous devez le stockage blob tooyour clé toochange hello accès pour des raisons de sécurité.

Bonjour tooperform de façon plus élégante que cette tâche est toofollow un processus appelé « rotation des clés de hello ». Vous avez peut-être remarqué que vous disposez de deux clés de stockage pour votre compte de stockage d'objets blob. Cela permet une transition.

La rotation de vos clés de compte de stockage Azure est un processus simple en trois étapes.

1. Créer le deuxième information d’identification de la portée de la base de données en fonction de la clé d’accès de stockage secondaire de hello
2. Créez la deuxième source de données externe en fonction de ces nouvelles informations d'identification.
3. Supprimez et recréez les tables externes hello pointant vers la nouvelle source de données externe toohello

Lorsque vous avez migré toutes les tables externes toohello nouvelle source de données externe que vous pouvez effectuer hello nettoyer des tâches :

1. suppression de la première source de données externe ;
2. Première base de données de la suppression d’une étendue d’informations d’identification en fonction de la clé d’accès de stockage principal de hello
3. Connectez-vous à Azure et régénérer la clé d’accès primaire hello prête pour hello prochaine

## <a name="query-azure-blob-storage-data"></a>Interroger des données de l’espace de stockage d’objets Blob Microsoft Azure
Requêtes sur des tables externes utilisent simplement le nom de la table hello comme s’il s’agissait d’une table relationnelle.

```sql
-- Query Azure storage resident data via external table.
SELECT * FROM [ext].[CarSensor_Data]
;
```

> [!NOTE]
> Une requête sur une table externe peut échouer avec l’erreur de hello *« requête abandonnée : seuil de rejet maximal hello a été atteinte lors de la lecture à partir d’une source externe »*. Cela indique que vos données externes contiennent des enregistrements *à l’intégrité compromise* . Un enregistrement de données est considérée comme « dirty » si les types de données réelles hello/nombre de colonnes ne correspondent pas les définitions des colonnes d’une table externe hello hello ou si les données de salutation n’est pas conforme toohello externe format spécifiés. toofix, assurez-vous que votre table externe et les définitions de format de fichier externe sont correctes et que vos données externes est conforme à des définitions de toothese. Au cas où un sous-ensemble d’enregistrements de données externes sont incorrectes, vous pouvez choisir tooreject ces enregistrements de vos requêtes à l’aide des options de rejet hello dans DDL créer la TABLE externe.
> 
> 

## <a name="load-data-from-azure-blob-storage"></a>Charger des données à partir d’objets Blob Microsoft Azure Storage
Cet exemple charge des données à partir de la base de données du Data Warehouse tooSQL stockage blob Azure.

Le stockage des données directement supprime les temps de transfert de données hello pour les requêtes. Le stockage des données avec un index columnstore améliore les performances des requêtes d’analyse par des too10x.

Cet exemple utilise des données de tooload instruction CREATE TABLE AS SELECT hello. nouvelle table de Hello hérite des colonnes hello nommées dans la requête de hello. Il hérite des types de données hello de ces colonnes de définition de la table externe hello.

CREATE TABLE AS SELECT est une très performantes instruction Transact-SQL qui charge des données hello tooall parallèle Bonjour les nœuds de votre entrepôt de données SQL.  Il a été développé pour le moteur de traitement parallèle massif (MPP) hello dans le système de plateforme Analytique et est désormais dans l’entrepôt de données SQL.

```sql
-- Load data from Azure blob storage tooSQL Data Warehouse

CREATE TABLE [dbo].[Customer_Speed]
WITH
(   
    CLUSTERED COLUMNSTORE INDEX
,    DISTRIBUTION = HASH([CarSensor_Data].[CustomerKey])
)
AS
SELECT *
FROM   [ext].[CarSensor_Data]
;
```

Consultez [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)].

## <a name="create-statistics-on-newly-loaded-data"></a>Créer des statistiques sur des données nouvellement chargées
Azure SQL Data Warehouse ne prend pas encore en charge les statistiques à création ou mise à jour automatique.  Dans l’ordre tooget hello optimiser les performances de vos requêtes, il est important que créer des statistiques sur toutes les colonnes de toutes les tables après le premier chargement de hello ou toutes les modifications importantes se produisent dans les données de salutation.  Pour obtenir une explication détaillée des statistiques, consultez hello [statistiques] [ Statistics] rubrique dans le groupe de développement hello de rubriques.  Voici un exemple rapide de la façon dont les statistiques toocreate sur hello déposée chargement dans cet exemple.

```sql
create statistics [SensorKey] on [Customer_Speed] ([SensorKey]);
create statistics [CustomerKey] on [Customer_Speed] ([CustomerKey]);
create statistics [GeographyKey] on [Customer_Speed] ([GeographyKey]);
create statistics [Speed] on [Customer_Speed] ([Speed]);
create statistics [YearMeasured] on [Customer_Speed] ([YearMeasured]);
```

## <a name="export-data-tooazure-blob-storage"></a>Exporter le stockage d’objets blob de données tooAzure
Cette section montre comment tooexport des données à partir de l’entrepôt de données SQL tooAzure stockage d’objets blob. Cet exemple utilise CREATE EXTERNAL TABLE AS SELECT qui est un hautement performant Transact-SQL instruction tooexport hello de données en parallèle à partir de tous les nœuds de calcul hello.

Hello exemple suivant crée une table externe Weblogs2014 à l’aide des définitions de colonne et les données à partir de dbo. Table des blogs. définition de la table externe Hello est stockée dans l’entrepôt de données SQL et les résultats de hello d’instruction SELECT de hello sont exportée toohello répertoire « / archive/log2014 / » sous le conteneur d’objets blob hello spécifié par la source de données hello. les données de Hello sont exportées au format de fichier texte hello.

```sql
CREATE EXTERNAL TABLE Weblogs2014 WITH
(
    LOCATION='/archive/log2014/',
    DATA_SOURCE=azure_storage,
    FILE_FORMAT=text_file_format
)
AS
SELECT
    Uri,
    DateRequested
FROM
    dbo.Weblogs
WHERE
    1=1
    AND DateRequested > '12/31/2013'
    AND DateRequested < '01/01/2015';
```
## <a name="isolate-loading-users"></a>Isoler les utilisateurs du chargement
Il existe souvent un toohave besoin de plusieurs utilisateurs qui peuvent charger des données dans un entrepôt de données SQL. Étant donné que hello [CREATE TABLE AS SELECT (Transact-SQL)] [ CREATE TABLE AS SELECT (Transact-SQL)] nécessite des autorisations de contrôle de base de données hello, vous obtiendrez avec plusieurs utilisateurs à contrôler l’accès sur tous les schémas. toolimit, vous pouvez utiliser d’instruction de contrôle de refuser hello.

Par exemple, les schémas de base de données schema_A pour le service A et schema_B pour le service B laissent les utilisateurs de base de données user_A et user_B être utilisateurs du chargement PolyBase dans les services A et B, respectivement. Ils ont tous deux reçu des autorisations de base de données CONTROL.
créateurs Hello du schéma A et B désormais verrouiller leurs schémas à l’aide de refus :

```sql
   DENY CONTROL ON SCHEMA :: schema_A toouser_B;
   DENY CONTROL ON SCHEMA :: schema_B toouser_A;
```   
 Avec cette option, ce dernier et user_B doivent maintenant être verrouillée de hello les schémas d’autres sociétés.
 


## <a name="next-steps"></a>Étapes suivantes
toolearn en savoir plus sur mobile tooSQL données entrepôt de données, consultez hello [vue d’ensemble de la migration de données][data migration overview].

<!--Image references-->

<!--Article references-->
[Load data with bcp]: ./sql-data-warehouse-load-with-bcp.md
[Load data with PolyBase]: ./sql-data-warehouse-get-started-load-with-polybase.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[data migration overview]: ./sql-data-warehouse-overview-migrate.md

<!--MSDN references-->
[supported source/sink]: https://msdn.microsoft.com/library/dn894007.aspx
[copy activity]: https://msdn.microsoft.com/library/dn835035.aspx
[SQL Server destination adapter]: https://msdn.microsoft.com/library/ms141095.aspx
[SSIS]: https://msdn.microsoft.com/library/ms141026.aspx

[CREATE EXTERNAL DATA SOURCE (Transact-SQL)]: https://msdn.microsoft.com/library/dn935022.aspx
[CREATE EXTERNAL FILE FORMAT (Transact-SQL)]: https://msdn.microsoft.com/library/dn935026.aspx
[CREATE EXTERNAL TABLE (Transact-SQL)]: https://msdn.microsoft.com/library/dn935021.aspx

[DROP EXTERNAL DATA SOURCE (Transact-SQL)]: https://msdn.microsoft.com/library/mt146367.aspx
[DROP EXTERNAL FILE FORMAT (Transact-SQL)]: https://msdn.microsoft.com/library/mt146379.aspx
[DROP EXTERNAL TABLE (Transact-SQL)]: https://msdn.microsoft.com/library/mt130698.aspx

[CREATE TABLE AS SELECT (Transact-SQL)]: https://msdn.microsoft.com/library/mt204041.aspx
[INSERT...SELECT (Transact-SQL)]: https://msdn.microsoft.com/library/ms174335.aspx
[CREATE MASTER KEY (Transact-SQL)]: https://msdn.microsoft.com/library/ms174382.aspx
[CREATE CREDENTIAL (Transact-SQL)]: https://msdn.microsoft.com/library/ms189522.aspx
[CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)]: https://msdn.microsoft.com/library/mt270260.aspx
[DROP CREDENTIAL (Transact-SQL)]: https://msdn.microsoft.com/library/ms189450.aspx

<!-- External Links -->
