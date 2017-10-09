---
title: "problèmes de données-inclinaison aaaResolve à l’aide d’Azure Data Lake Tools pour Visual Studio | Documents Microsoft"
description: "Solutions de dépannage potentielles pour les problèmes d'asymétrie des données à l’aide d’Azure Data Lake Tools pour Visual Studio."
services: data-lake-analytics
documentationcenter: 
author: yanancai
manager: 
editor: 
ms.assetid: 
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/16/2016
ms.author: yanacai
ms.openlocfilehash: 3909fbd89eb40f061268cb7128f7fa84a3c33de7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="resolve-data-skew-problems-by-using-azure-data-lake-tools-for-visual-studio"></a>Résolution de problèmes d'asymétrie des données à l’aide d'Azure Data Lake Tools pour Visual Studio

## <a name="what-is-data-skew"></a>Qu’est-ce que l'asymétrie des données ?

en résumé, l'asymétrie des données correspond à une valeur surreprésentée. Imaginez que vous avez affectés à 50 examinateurs de taxe tooaudit de revenus, un examiner pour chaque état des États-Unis. examiner du Wyoming Hello, car il population de hello est petite, a peu toodo. En Californie, toutefois, les examiner hello est conservée très occupé en raison de la population de grande taille de l’état hello.
    ![Exemple de problème d'asymétrie des données](./media/data-lake-analytics-data-lake-tools-data-skew-solutions/data-skew-problem.png)

Dans notre scénario, les données de salutation sont distribuées inégalement entre tous les examinateurs de taxes, ce qui signifie que certaines examinateurs doivent fonctionner plus que d’autres. Dans votre travail, vous rencontrez souvent situations comme exemple de taxe-examiner hello ici. En termes plus techniques, un sommet obtient beaucoup plus de données à ses homologues, une situation qui rend les sommets hello plus que d’autres et qui finalement ralentit l’intégralité du travail de hello de travail. Qui plus est, hello travail peut échouer, car les sommets doivent, par exemple, une limitation de l’exécution de 5 heures et une limitation de 6 Go de mémoire.

## <a name="resolving-data-skew-problems"></a>Résolution de problèmes liés à l'asymétrie des données

Azure Data Lake Tools pour Visual Studio peut aider à détecter un éventuel problème d'asymétrie des données dans votre tâche. En cas de problème, vous pouvez le résoudre en essayant de solutions hello dans cette section.

## <a name="solution-1-improve-table-partitioning"></a>Solution 1 : Améliorer le partitionnement de tables

### <a name="option-1-filter-hello-skewed-key-value-in-advance"></a>Option 1 : Hello de filtre valeur de clé asymétrique à l’avance

Si elle n’affecte pas votre logique métier, vous pouvez filtrer les valeurs de fréquence plus élevée hello à l’avance. Par exemple, s’il existe un grand nombre de 000 000-000 dans la colonne GUID, vous pouvez tooaggregate cette valeur. Avant d’agrégation, vous pouvez écrire « WHERE GUID ! = « 000-000 000 » « valeur de haute fréquence toofilter hello.

### <a name="option-2-pick-a-different-partition-or-distribution-key"></a>Option 2 : Sélectionner une clé de distribution ou de partition différente

Bonjour précédent exemple, si vous souhaitez que la charge de travail uniquement toocheck hello-fiscaux tous sur hello pays, vous pouvez améliorer la distribution des données hello en sélectionnant le numéro d’identification hello comme clé. Sélection d’une autre partition ou une clé de distribution peut parfois distribuer hello données plus équitablement, mais vous devez toomake vraiment que ce choix n’affecte pas votre logique métier. Par exemple, des somme toocalculate hello taxe pour chaque état, vous pourriez toodesignate _état_ en tant que clé de partition hello. Si vous continuez à tooexperience ce problème, essayez d’utiliser l’Option 3.

### <a name="option-3-add-more-partition-or-distribution-keys"></a>Option 3 : Ajouter plus de clés de distribution ou de partition

Au lieu d’utiliser uniquement _l'état_ comme clé de partition, vous pouvez utiliser plusieurs clés pour le partitionnement. Par exemple, envisagez d’ajouter _Code postal_ comme une partition supplémentaire partition de données de clé tooreduce tailles et répartir plus équitablement les données de salutation.

### <a name="option-4-use-round-robin-distribution"></a>Option 4 : Utiliser la distribution par tourniquet (round robin)

Si vous ne peut pas trouver une clé appropriée pour la partition et la distribution, vous pouvez essayer de distribution de tourniquet toouse. La distribution par tourniquet (round robin) traite toutes les lignes de manière égale et les place au hasard dans des compartiments correspondants. les données de salutation obtient distribuées uniformément, mais lors de la perte d’informations localité, un inconvénient qui peut également réduire les performances pour certaines opérations. En outre, si vous effectuez d’agrégation pour la clé asymétrique de hello malgré tout, hello inclinaison de données problème persiste. toolearn savoir plus sur la distribution alternée, consultez hello U-SQL Table Distributions section [CREATE TABLE (U-SQL) : création d’une Table avec schéma](https://msdn.microsoft.com/en-us/library/mt706196.aspx#dis_sch).

## <a name="solution-2-improve-hello-query-plan"></a>Solution 2 : Améliorer le plan de requête hello

### <a name="option-1-use-hello-create-statistics-statement"></a>Option 1 : Utilisez l’instruction CREATE STATISTICS hello

U-SQL fournit l’instruction CREATE STATISTICS hello sur les tables. Cette instruction donne l’optimiseur de requête plus d’informations toohello sur hello données caractéristiques, telles que la distribution de la valeur, qui sont stockées dans une table. Pour la plupart des requêtes, optimiseur de requête hello génère déjà les statistiques nécessaires hello pour un plan de requête de haute qualité. Parfois, vous devrez peut-être les performances des requêtes tooimprove en créant des statistiques supplémentaires avec CREATE STATISTICS ou en modifiant la conception de requête hello. Pour plus d’informations, consultez hello [CREATE STATISTICS (U-SQL)](https://msdn.microsoft.com/en-us/library/azure/mt771898.aspx) page.

Exemple de code :

    CREATE STATISTICS IF NOT EXISTS stats_SampleTable_date ON SampleDB.dbo.SampleTable(date) WITH FULLSCAN;

>[!NOTE]
>Les informations statistiques ne sont pas mises à jour automatiquement. Si vous mettez à jour les données hello dans une table sans recréer des statistiques de hello, les performances des requêtes hello peuvent refuser.

### <a name="option-2-use-skewfactor"></a>Option 2 : Utiliser SKEWFACTOR

Si vous souhaitez que des taxes de hello toosum pour chaque état, vous devez utiliser Grouper par état, une approche qui ne d’éviter le problème de données-inclinaison hello. Toutefois, vous pouvez fournir un indicateur de données dans votre tooidentify requête données biaiser clés afin de pouvoir les optimiseur hello préparer un plan d’exécution pour vous.

En règle générale, vous pouvez définir le paramètre hello comme 0,5 et 1, 0,5, ce qui signifie que peu inclinaison lourde signification inclinaison et 1. Comme indicateur de hello affecte l’optimisation du plan d’exécution de l’instruction en cours hello et toutes les instructions en aval, pour pouvoir qu’indicateur de hello tooadd hello potentiel rétrécie key-wise d’agrégation.

    SKEWFACTOR (columns) = x

    Provides a hint that hello given columns have a skew factor x from 0 (no skew) through 1 (very heavy skew).

Exemple de code :

    //Add a SKEWFACTOR hint.
    @Impressions =
        SELECT * FROM
        searchDM.SML.PageView(@start, @end) AS PageView
        OPTION(SKEWFACTOR(Query)=0.5)
        ;

    //Query 1 for key: Query, ClientId
    @Sessions =
        SELECT
            ClientId,
            Query,
            SUM(PageClicks) AS Clicks
        FROM
            @Impressions
        GROUP BY
            Query, ClientId
        ;

    //Query 2 for Key: Query
    @Display =
        SELECT * FROM @Sessions
            INNER JOIN @Campaigns
                ON @Sessions.Query == @Campaigns.Query
        ;   

### <a name="option-3-use-rowcount"></a>Option 3 : Utiliser ROWCOUNT  
En outre tooSKEWFACTOR, pour la clé asymétrique spécifique joindre des cas, si vous savez que hello autre ensemble de lignes jointes est petit, vous pouvez indiquer l’optimiseur de hello en ajoutant un indicateur du nombre de lignes dans l’instruction de U-SQL hello avant la jointure. De cette manière, optimiseur peut choisir un toohelp de stratégie de jointure diffusion améliorer les performances. N’oubliez pas que nombre de lignes ne résout pas le problème de données-inclinaison hello, mais il peut proposer une assistance supplémentaire.

    OPTION(ROWCOUNT = n)

    Identify a small row set before JOIN by providing an estimated integer row count.

Exemple de code :

    //Unstructured (24-hour daily log impressions)
    @Huge   = EXTRACT ClientId int, ...
                FROM @"wasb://ads@wcentralus/2015/10/30/{*}.nif"
                ;

    //Small subset (that is, ForgetMe opt out)
    @Small  = SELECT * FROM @Huge
                WHERE Bing.ForgetMe(x,y,z)
                OPTION(ROWCOUNT=500)
                ;

    //Result (not enough information toodetermine simple broadcast JOIN)
    @Remove = SELECT * FROM Bing.Sessions
                INNER JOIN @Small ON Sessions.Client == @Small.Client
                ;

## <a name="solution-3-improve-hello-user-defined-reducer-and-combiner"></a>Solution 3 : Améliorer COMBINATEUR et réducteur de hello défini par l’utilisateur

Vous pouvez écrire parfois un toodeal opérateur défini par l’utilisateur avec une logique complexe de processus et un réducteur bien écrite et l’association peuvent atténuer un problème d’inclinaison de données dans certains cas.

### <a name="option-1-use-a-recursive-reducer-if-possible"></a>Option 1 : Utiliser un réducteur récursif si possible

Par défaut, le réducteur défini par l’utilisateur s’exécute en mode non récursif, ce qui signifie que le travail de réduction pour une clé est distribué dans un seul vertex. Mais si vos données sont déformées, hello les jeux de données volumineux peuvent être traitées dans un sommet unique et exécuter pendant un certain temps.

tooimprove des performances, vous pouvez ajouter un attribut dans votre toorun de réducteur toodefine code en mode de récursive. Ensuite, hello les jeux de données volumineux peut être distribuée toomultiple sommets et s’exécuter en parallèle, ce qui accélère votre travail.

toochange un toorecursive du réducteur non récursive, vous devez toomake assurer que votre algorithme est associatif. Par exemple, somme de hello est associative et hello median n’est pas. Vous devez également toomake vraiment que hello d’entrée et sortie pour le réducteur conservent hello même schéma.

Attribut d'un réducteur récursif :

    [SqlUserDefinedReducer(IsRecursive = true)]

Exemple de code :

    [SqlUserDefinedReducer(IsRecursive = true)]
    public class TopNReducer : IReducer
    {
        public override IEnumerable<IRow>
            Reduce(IRowset input, IUpdatableRow output)
        {
            //Your reducer code goes here.
        }
    }

### <a name="option-2-use-row-level-combiner-mode-if-possible"></a>Option 2 : Utiliser le mode de combinateur au niveau des lignes si possible

Indicateur de nombre de lignes toohello similaires pour les cas de jointure de clé asymétrique spécifique, en mode d’association tente toodistribute énorme valeur de clé asymétrique jeux toomultiple sommets afin que le travail de hello pouvant être exécuté simultanément. Le mode de combinateur ne permet pas de résoudre le problème d'asymétrie des données, mais peut être utile pour traiter les ensembles de valeurs de clés de décalage volumineux.

Par défaut, le mode d’association hello est complet, ce qui signifie que hello gauche ensemble de lignes, et ensemble de lignes à droite ne peut pas être séparées par des. Définition du mode hello comme gauche/droite/interne permet au niveau de la ligne de jointure. système de Hello sépare les ensembles de lignes correspondantes hello et comment les répartit dans plusieurs sommets qui s’exécutent en parallèle. Toutefois, avant de configurer le mode COMBINATEUR hello, veillez à tooensure qui hello correspondante des ensembles de lignes peut être séparé.

exemple Hello qui suit montre un ensemble de valeurs séparées par des lignes de gauche. Chaque ligne de sortie dépend d’une seule ligne d’entrée de hello gauche, et potentiellement dépend de toutes les lignes de hello droite avec hello même valeur de clé. Si vous définissez le mode d’association hello de gauche, système de hello sépare hello énorme gauche-ensemble de lignes dans les petits et les affecte toomultiple sommets.

![Illustration du mode de combinateur](./media/data-lake-analytics-data-lake-tools-data-skew-solutions/combiner-mode-illustration.png)

>[!NOTE]
>Si vous définissez le mode d’association incorrect hello, combinaison de hello est moins efficace, et les résultats de hello sont peut-être erronés.

Attributs du mode de combinateur :

- [SqlUserDefinedCombiner(Mode=CombinerMode.Full)]: Every output row potentially depends on all hello input rows from left and right with hello same key value.

- SqlUserDefinedCombiner(Mode=CombinerMode.Left) : Chaque ligne de sortie dépend d’une seule ligne d’entrée de hello gauche (et potentiellement toutes les lignes de hello droite avec hello même valeur de clé).

- qlUserDefinedCombiner(Mode=CombinerMode.Right) : chaque ligne de sortie dépend d’une ligne d’entrée de hello droit (et potentiellement toutes les lignes de gauche hello avec hello même valeur de clé).

- SqlUserDefinedCombiner(Mode=CombinerMode.Inner) : Chaque ligne de sortie dépend une ligne d’entrée de hello gauche et hello droite avec hello même valeur.

Exemple de code :

    [SqlUserDefinedCombiner(Mode = CombinerMode.Right)]
    public class WatsonDedupCombiner : ICombiner
    {
        public override IEnumerable<IRow>
            Combine(IRowset left, IRowset right, IUpdatableRow output)
        {
        //Your combiner code goes here.
        }
    }
