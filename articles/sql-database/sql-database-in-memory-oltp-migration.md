---
title: "OLTP en mémoire aaaIn améliore les performances des transactions-dépassement SQL | Documents Microsoft"
description: "Adopter l’OLTP en mémoire tooimprove transactionnelle des performances dans une base de données SQL existante."
services: sql-database
documentationcenter: 
author: jodebrui
manager: jhubbard
editor: MightyPen
ms.assetid: c2bf14a0-905b-47b4-afb6-efe9a61147d5
ms.service: sql-database
ms.custom: develop databases
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/22/2016
ms.author: jodebrui
ms.openlocfilehash: 1bed796069565eb6741953837cf0477c2ddd8519
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-in-memory-oltp-tooimprove-your-application-performance-in-sql-database"></a>Utilisez l’OLTP en mémoire tooimprove les performances de votre application de base de données SQL
[OLTP en mémoire](sql-database-in-memory.md) peut être utilisé tooimprove les performances de hello de traitement des transactions, intégrer les données et les scénarios de données temporaires dans [Premium](sql-database-service-tiers.md) bases de données SQL Azure sans augmenter hello niveau tarifaire. 

> [!NOTE] 
> Découvrez comment le [Quorum double la charge de travail de la base de données clé tout en réduisant les DTU de 70 % avec la SQL Database](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database)


Suivez ces étapes de tooadopt OLTP en mémoire dans votre base de données existante.

## <a name="step-1-ensure-you-are-using-a-premium-database"></a>Étape 1 : vérifiez que vous utilisez une base de données Premium
OLTP en mémoire est pris en charge uniquement dans les bases de données Premium. En mémoire est prise en charge si hello renvoyé de résultat est 1 (pas 0) :

```
SELECT DatabasePropertyEx(Db_Name(), 'IsXTPSupported');
```

L’acronyme *XTP* signifie *Extreme Transaction Processing (Traitement de transactions extrêmes)*



## <a name="step-2-identify-objects-toomigrate-tooin-memory-oltp"></a>Étape 2 : Identifier les objets toomigrate tooIn-mémoire OLTP
SSMS inclut un rapport de **présentation d’analyse des performances des transactions** que vous pouvez exécuter sur une base de données avec une charge de travail active. rapport de Hello identifie les tables et procédures stockées qui sont candidates pour la migration OLTP en mémoire tooIn.

Dans SSMS, rapport de hello toogenerate :

* Bonjour **l’Explorateur d’objets**, cliquez sur le nœud de votre base de données.
* Cliquez sur **Rapports** > **Rapports Standard** > **Présentation de l’analyse des performances des transactions**.

Pour plus d’informations, consultez [déterminer si une Table ou une procédure stockée doit être déplacée tooIn l’OLTP en mémoire](http://msdn.microsoft.com/library/dn205133.aspx).

## <a name="step-3-create-a-comparable-test-database"></a>Étape 3 : Créer une base de données de test comparable
Supposons que le rapport de hello indique votre base de données a une table qui tirent parti d’être convertie table mémoire optimisée de tooa. Nous vous recommandons de commencer par tester indication de hello tooconfirm en testant.

Vous avez besoin d’une copie de test de votre base de données de production. Hello base de données de test doit être à hello même niveau de la couche de service en tant que votre base de données de production.

tooease tester, optimiser votre base de données de test comme suit :

1. Se connecter à base de données de test toohello à l’aide de SSMS.
2. tooavoid avoir hello option WITH (SNAPSHOT) dans les requêtes, attribuez une option de base de données hello comme Bonjour instruction T-SQL suivante :
   
   ```
   ALTER DATABASE CURRENT
    SET
        MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT = ON;
   ```

## <a name="step-4-migrate-tables"></a>Étape 4 : Migrer les tables
Vous devez créer et remplir une copie mémoire optimisée de la table de hello souhaité tootest. Vous pouvez le créer en utilisant soit :

* Hello pratique Assistant Optimisation de mémoire dans SSMS.
* T-SQL manuel.

#### <a name="memory-optimization-wizard-in-ssms"></a>Assistant Optimisation de mémoire en SSMS
toouse cette option de migration :

1. Se connecter à base de données de test toohello avec SSMS.
2. Bonjour **l’Explorateur d’objets**, avec le bouton droit sur la table de hello, puis cliquez sur **conseiller d’optimisation de mémoire**.
   
   * Hello **Table mémoire optimiseur Advisor** Assistant s’affiche.
3. Dans l’Assistant de hello, cliquez sur **validation de la Migration** (ou hello **suivant** bouton) toosee si hello table a des non pris en charge les fonctionnalités qui sont prises en charge dans les tables optimisées en mémoire. Pour plus d'informations, consultez les pages suivantes :
   
   * Hello *liste de vérification de l’optimisation mémoire* dans [conseiller d’optimisation de mémoire](http://msdn.microsoft.com/library/dn284308.aspx).
   * [Constructions Transact-SQL non prises en charge par In-Memory OLTP](http://msdn.microsoft.com/library/dn246937.aspx).
   * [L’OLTP en mémoire tooIn migration](http://msdn.microsoft.com/library/dn247639.aspx).
4. Si la table de hello n’a aucune fonctionnalité non prise en charge, le conseiller hello peut effectuer schéma hello et migration des données pour vous.

#### <a name="manual-t-sql"></a>T-SQL manuel
toouse cette option de migration :

1. Se connecter à base de données de test tooyour à l’aide de SSMS (ou un utilitaire similaire).
2. Obtenir le script T-SQL complet de hello pour votre table et ses index.
   
   * Dans SSMS, cliquez avec le bouton droit sur le nœud de votre table.
   * Cliquez sur **Générer un script de la table en tant que** > **CREATE To** > **Fenêtre de nouvelle requête**.
3. Dans la fenêtre de script hello, ajoutez WITH (MEMORY_OPTIMIZED = ON) toohello l’instruction CREATE TABLE.
4. En l’absence d’un index ordonné en clusters, modifiez-le tooNONCLUSTERED.
5. Renommer la table existante de hello à l’aide de SP_RENAME.
6. Créer hello optimisées en mémoire copie de la table de hello en exécutant le script CREATE TABLE modifié.
7. Copier la table mémoire optimisée de hello données tooyour à l’aide de INSERT... SÉLECTIONNEZ * DANS :

```
INSERT INTO <new_memory_optimized_table>
        SELECT * FROM <old_disk_based_table>;
```


## <a name="step-5-optional-migrate-stored-procedures"></a>Étape 5 (facultative) : migrer les procédures stockées
fonctionnalité de mémoire Hello permettre également modifier une procédure stockée pour améliorer les performances.

### <a name="considerations-with-natively-compiled-stored-procedures"></a>Considérations relatives à des procédures stockées compilées en mode natif
Une procédure stockée compilée en mode natif doit avoir hello options sur sa clause avec T-SQL suivantes :

* NATIVE_COMPILATION
* SCHEMABINDING : tables signification hello de procédure stockée ne peut pas avoir leurs définitions de colonne modifiées de quelque manière qui affecterait la procédure stockée hello, sauf si vous supprimez la procédure stockée hello.

Un module natif doit utiliser un grand [bloc ATOMIC](http://msdn.microsoft.com/library/dn452281.aspx) pour la gestion de transaction. Il n’existe aucun rôle pour une instruction BEGIN TRANSACTION ou ROLLBACK TRANSACTION explicite. Si votre code détecte une violation d’une règle d’entreprise, il peut s’arrêter bloc atomique de hello avec un [lever](http://msdn.microsoft.com/library/ee677615.aspx) instruction.

### <a name="typical-create-procedure-for-natively-compiled"></a>En général, CREATE PROCEDURE compilée en mode natif
En règle générale, hello T-SQL toocreate une procédure stockée compilée en mode natif est similaire toohello suivant le modèle :

```
CREATE PROCEDURE schemaname.procedurename
    @param1 type1, …
    WITH NATIVE_COMPILATION, SCHEMABINDING
    AS
        BEGIN ATOMIC WITH
            (TRANSACTION ISOLATION LEVEL = SNAPSHOT,
            LANGUAGE = N'your_language__see_sys.languages'
            )
        …
        END;
```

* Pour hello TRANSACTION_ISOLATION_LEVEL, instantané est la procédure la valeur pour hello compilée stockée hello plus courante. Toutefois, un sous-ensemble de hello autres valeurs sont également pris en charge :
  
  * REPEATABLE READ
  * SERIALIZABLE
* Hello valeur langue doit être présent dans la vue de sys.languages hello.

### <a name="how-toomigrate-a-stored-procedure"></a>Comment toomigrate une procédure stockée
les étapes de migration de Hello sont :

1. Obtenir hello CREATE PROCEDURE script toohello procédure stockée interprétée normale.
2. Réécrire son en-tête toomatch hello précédent modèle.
3. Vérifier si le procédure stockée hello code T-SQL utilise des fonctionnalités qui ne sont pas pris en charge pour les procédures stockées compilées en mode natif. Mettre en œuvre des solutions de contournement si nécessaire.
   
   * Pour plus d’informations, voir [Problèmes de migration pour les procédures stockées compilées natives](http://msdn.microsoft.com/library/dn296678.aspx).
4. Renommer une procédure stockée hello ancien à l’aide de SP_RENAME. Ou FAITES-LE SIMPLEMENT GLISSER (DROP).
5. Exécutez le script CREATE PROCEDURE T-SQL modifié.

## <a name="step-6-run-your-workload-in-test"></a>Étape 6 : exécuter votre charge de travail dans un test
Exécutez une charge de travail dans votre base de données de test est similaire toohello la charge de travail qui s’exécute dans votre base de données de production. Cela doit faire apparaître les gains de performances hello atteints par votre utilisation des fonctionnalités de In-Memory hello pour les tables et procédures stockées.

Les attributs principaux de la charge de travail hello sont :

* Nombre de connexions simultanées.
* Rapport Lecture/Écriture

tootailor et test de charge de travail exécution hello, envisagez d’utiliser l’outil pratique ostress.exe hello, notamment [ici](sql-database-in-memory.md).

latence du réseau toominimize, exécutez votre test Bonjour même région géographique Azure où la base de données hello existe.

## <a name="step-7-post-implementation-monitoring"></a>Étape 7 : surveillance post exécution
Tenez compte des effets des performances hello de vos implémentations de mémoire en production d’analyse :

* [Surveiller le stockage en mémoire](sql-database-in-memory-oltp-monitoring.md).
* [Analyse d’une base de données SQL Azure à l’aide de vues de gestion dynamique](sql-database-monitoring-with-dmvs.md)

## <a name="related-links"></a>Liens connexes
* [In-Memory OLTP (optimisation en mémoire)](http://msdn.microsoft.com/library/dn133186.aspx)
* [Introduction tooNatively de procédures stockées compilées](http://msdn.microsoft.com/library/dn133184.aspx)
* [Conseil d’optimisation par mémoire](http://msdn.microsoft.com/library/dn284308.aspx)

