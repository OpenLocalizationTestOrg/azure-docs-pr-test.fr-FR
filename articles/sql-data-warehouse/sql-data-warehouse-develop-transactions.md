---
title: "aaaTransactions dans l’entrepôt de données SQL | Documents Microsoft"
description: "Conseils relatifs à l’implémentation de transactions dans Microsoft Azure SQL Data Warehouse, dans le cadre du développement de solutions."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: ae621788-e575-41f5-8bfe-fa04dc4b0b53
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 7c541648553238443b407666612561918096eb61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="transactions-in-sql-data-warehouse"></a>Transactions dans SQL Data Warehouse
Comme pour tout, l’entrepôt de données SQL prend en charge les transactions dans le cadre de la charge de travail entrepôt de données hello. Cependant, performances de hello tooensure d’entrepôt de données SQL sont conservées à l’échelle de que certaines fonctionnalités sont limitées quand comparé tooSQL Server. Cet article met en évidence les différences de hello et listes hello d’autres. 

## <a name="transaction-isolation-levels"></a>Niveaux d’isolation des transactions
SQL Data Warehouse implémente les transactions ACID. Toutefois, hello d’Isolation de la prise en charge transactionnelle de hello est limité trop`READ UNCOMMITTED` et il ne peut pas être modifié. Vous pouvez implémenter un nombre de méthodes de codage tooprevent dirty lit des données s’il s’agit d’un critère important pour vous. Hello méthodes les plus populaires exploitent SACT et le basculement de partition table (souvent appelé modèle de fenêtre glissante de hello) tooprevent les utilisateurs à partir de l’interrogation des données qui sont toujours en cours de préparation. Affichages que les données de filtre préliminaire hello sont également une approche courante.  

## <a name="transaction-size"></a>Taille de la transaction
Une transaction de modification de données unique est limitée en taille. limite de Hello aujourd'hui est appliqué « par distribution ». Par conséquent, l’allocation totale hello peut être calculée en multipliant la limite de hello par nombre de distribution hello. tooapproximate hello nombre de lignes dans une transaction de hello division cap de distribution hello par taille totale de hello de chaque ligne. Pour les colonnes de longueur variable envisagez prendre une longueur de colonne moyenne au lieu d’utiliser la taille maximale de hello.

Dans la table hello ci-dessous hello les hypothèses suivantes ont été apportées :

* Une distribution égale des données s’est produite 
* longueur de ligne moyenne Hello est 250 octets

| [DWU][DWU] | Limite par distribution (Go) | Nombre de distributions | Taille de transaction MAX (Go) | # Lignes par distribution | Nombre de lignes max par transaction |
| --- | --- | --- | --- | --- | --- |
| DW100 |1 |60 |60 |4 000 000 |240 000 000 |
| DW200 |1.5 |60 |90 |6 000 000 |360 000 000 |
| DW300 |2.25 |60 |135 |9 000 000 |540 000 000 |
| DW400 |3 |60 |180 |12 000 000 |720 000 000 |
| DW500 |3,75 |60 |225 |15 000 000 |900 000 000 |
| DW600 |4.5 |60 |270 |18 000 000 |1 080 000 000 |
| DW1000 |7.5 |60 |450 |30 000 000 |1 800 000 000 |
| DW1200 |9 |60 |540 |36 000 000 |2 160 000 000 |
| DW1500 |11,25 |60 |675 |45 000 000 |2 700 000 000 |
| DW2000 |15 |60 |900 |60 000 000 |3 600 000 000 |
| DW3000 |22,5 |60 |1 350 |90 000 000 |5 400 000 000 |
| DW6000 |45 |60 |2 700 |180 000 000 |10 800 000 000 |

limite de taille de transaction Hello est appliquée par la transaction ou l’opération. Elle n’est pas appliquée à toutes les transactions simultanées. Par conséquent, chaque transaction est autorisée toowrite cette quantité de données toohello journal. 

toooptimize et réduire les données écrites toohello journal hello reportez-vous toohello [Transactions meilleures pratiques] [ Transactions best practices] l’article.

> [!WARNING]
> Hello maximale de taille de la transaction ne peut être obtenue pour le hachage ou de tables ROUND_ROBIN distribués où hello propager de bienvenue des données est la même. Si la transaction de hello écrit les données de manière asymétrique toohello distributions, hello limite est probablement toobe atteint taille de transaction maximal toohello préalable.
> <!--REPLICATED_TABLE-->
> 
> 

## <a name="transaction-state"></a>État des transactions
SQL Data Warehouse utilise hello XACT_STATE() fonction tooreport Échec d’une transaction à l’aide de la valeur de hello -2. Cela signifie que les transactions hello a échoué et sont marquée pour la restauration uniquement

> [!NOTE]
> l’utilisation de -2 Hello par hello XACT_STATE fonction toodenote un ordinateur Échec de la transaction représente un comportement différent tooSQL Server. SQL Server utilise la valeur -1 de hello toorepresent une transaction non validable. SQL Server peut tolérer des erreurs à l’intérieur d’une transaction sans qu’il ait toobe marqué comme non validable. Par exemple, la valeur `SELECT 1/0` entraîne une erreur, mais ne fait pas passer une transaction à l’état non validable. SQL Server permet également de lectures de transaction non validable de hello. Mais SQL Data Warehouse ne vous le permet pas. Si une erreur se produit à l’intérieur d’une transaction de l’entrepôt de données SQL, il insère automatiquement les état hello -2, et vous ne serez pas en mesure de toomake les autres instructions select jusqu'à ce que l’instruction de hello a été annulée. Il est donc important toocheck que votre toosee de code d’application si elle utilise XACT_STATE() comme vous pouvez être amené à toomake de modifications de code.
> 
> 

Dans SQL Server par exemple, vous pouvez voir une transaction ressemblant à ce qui suit :

```sql
SET NOCOUNT ON;
DECLARE @xact_state smallint = 0;

BEGIN TRAN
    BEGIN TRY
        DECLARE @i INT;
        SET     @i = CONVERT(INT,'ABC');
    END TRY
    BEGIN CATCH
        SET @xact_state = XACT_STATE();

        SELECT  ERROR_NUMBER()    AS ErrNumber
        ,       ERROR_SEVERITY()  AS ErrSeverity
        ,       ERROR_STATE()     AS ErrState
        ,       ERROR_PROCEDURE() AS ErrProcedure
        ,       ERROR_MESSAGE()   AS ErrMessage
        ;

        IF @@TRANCOUNT > 0
        BEGIN
            PRINT 'ROLLBACK';
            ROLLBACK TRAN;
        END

    END CATCH;

IF @@TRANCOUNT >0
BEGIN
    PRINT 'COMMIT';
    COMMIT TRAN;
END

SELECT @xact_state AS TransactionState;
```

Si vous laissez votre code, car il est au-dessus de vous obtiendrez hello message d’erreur suivant :

Msg 111233, niveau 16, état 1, ligne 1 111233 ; hello en cours a été annulée, et les modifications en attente ont été restaurées. Cause : une transaction à un état de restauration uniquement n’a été pas explicitement restaurée avant une instruction DDL, DML ou SELECT.

Vous obtiendrez également pas les résultats de hello de hello erreur_ * fonctions.

Dans l’entrepôt de données SQL, code de hello doit toobe légèrement modifié :

```sql
SET NOCOUNT ON;
DECLARE @xact_state smallint = 0;

BEGIN TRAN
    BEGIN TRY
        DECLARE @i INT;
        SET     @i = CONVERT(INT,'ABC');
    END TRY
    BEGIN CATCH
        SET @xact_state = XACT_STATE();

        IF @@TRANCOUNT > 0
        BEGIN
            PRINT 'ROLLBACK';
            ROLLBACK TRAN;
        END

        SELECT  ERROR_NUMBER()    AS ErrNumber
        ,       ERROR_SEVERITY()  AS ErrSeverity
        ,       ERROR_STATE()     AS ErrState
        ,       ERROR_PROCEDURE() AS ErrProcedure
        ,       ERROR_MESSAGE()   AS ErrMessage
        ;
    END CATCH;

IF @@TRANCOUNT >0
BEGIN
    PRINT 'COMMIT';
    COMMIT TRAN;
END

SELECT @xact_state AS TransactionState;
```

Hello attendu comportement est désormais prise en charge. erreur Hello dans les transactions hello est géré et hello erreur_ * fonctions fournissent des valeurs comme prévu.

Tout ce qui a changé est que hello `ROLLBACK` Hello transaction avait toohappen avant hello lire des informations d’erreur hello Bonjour `CATCH` bloc.

## <a name="errorline-function"></a>Fonction Error_Line()
Il est également important de noter que SQL Data Warehouse ne pas implémenter ou prend en charge la fonction ERROR_LINE() hello. Si vous avez cela dans votre code, vous devez tooremove il toobe compatible avec l’entrepôt de données SQL. Utilisez à la place des étiquettes de requête dans votre code à tooimplement des fonctionnalités équivalentes. Reportez-vous toohello [étiquette] [ LABEL] article pour plus d’informations sur cette fonctionnalité.

## <a name="using-throw-and-raiserror"></a>Utilisation des paramètres THROW et RAISERROR
THROW est hello implémentation plus moderne pour le déclenchement d’exceptions dans l’entrepôt de données SQL mais RAISERROR est également. Il existe quelques différences qui méritent notre attention toohowever.

* Messages d’erreur ne doit pas être Bonjour plage de 100 000 à 150 000 pour THROW défini par l’utilisateur
* Les messages d’erreurs associés au paramètre RAISERROR sont définis sur la valeur fixe de 50 000.
* L’utilisation de l’élément sys.messages n’est pas prise en charge.

## <a name="limitiations"></a>Limitations
SQL Data Warehouse a quelques autres restrictions qui se rapportent tootransactions.

Les voici :

* Les transactions distribuées ne sont pas acceptées.
* Les transactions imbriquées ne sont pas autorisées.
* Les points de sauvegarde ne sont pas acceptés.
* Transactions sans nom
* Transactions sans marquage
* Aucune prise en charge de DDL comme `CREATE TABLE` dans une transaction définie par l’utilisateur

## <a name="next-steps"></a>Étapes suivantes
toolearn plus sur l’optimisation des transactions, consultez [Transactions meilleures pratiques][Transactions best practices].  toolearn sur les autres pratiques recommandées SQL Data Warehouse, consultez [SQL Data Warehouse meilleures pratiques][SQL Data Warehouse best practices].

<!--Image references-->

<!--Article references-->
[DWU]: ./sql-data-warehouse-overview-what-is.md
[development overview]: ./sql-data-warehouse-overview-develop.md
[Transactions best practices]: ./sql-data-warehouse-develop-best-practices-transactions.md
[SQL Data Warehouse best practices]: ./sql-data-warehouse-best-practices.md
[LABEL]: ./sql-data-warehouse-develop-label.md

<!--MSDN references-->

<!--Other Web references-->
