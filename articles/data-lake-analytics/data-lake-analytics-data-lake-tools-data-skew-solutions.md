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
# <a name="resolve-data-skew-problems-by-using-azure-data-lake-tools-for-visual-studio"></a><span data-ttu-id="ca732-103">Résolution de problèmes d'asymétrie des données à l’aide d'Azure Data Lake Tools pour Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ca732-103">Resolve data-skew problems by using Azure Data Lake Tools for Visual Studio</span></span>

## <a name="what-is-data-skew"></a><span data-ttu-id="ca732-104">Qu’est-ce que l'asymétrie des données ?</span><span class="sxs-lookup"><span data-stu-id="ca732-104">What is data skew?</span></span>

<span data-ttu-id="ca732-105">en résumé, l'asymétrie des données correspond à une valeur surreprésentée.</span><span class="sxs-lookup"><span data-stu-id="ca732-105">Briefly stated, data skew is an over-represented value.</span></span> <span data-ttu-id="ca732-106">Imaginez que vous avez affectés à 50 examinateurs de taxe tooaudit de revenus, un examiner pour chaque état des États-Unis.</span><span class="sxs-lookup"><span data-stu-id="ca732-106">Imagine that you have assigned 50 tax examiners tooaudit tax returns, one examiner for each US state.</span></span> <span data-ttu-id="ca732-107">examiner du Wyoming Hello, car il population de hello est petite, a peu toodo.</span><span class="sxs-lookup"><span data-stu-id="ca732-107">hello Wyoming examiner, because hello population there is small, has little toodo.</span></span> <span data-ttu-id="ca732-108">En Californie, toutefois, les examiner hello est conservée très occupé en raison de la population de grande taille de l’état hello.</span><span class="sxs-lookup"><span data-stu-id="ca732-108">In California, however, hello examiner is kept very busy because of hello state's large population.</span></span>
    <span data-ttu-id="ca732-109">![Exemple de problème d'asymétrie des données](./media/data-lake-analytics-data-lake-tools-data-skew-solutions/data-skew-problem.png)</span><span class="sxs-lookup"><span data-stu-id="ca732-109">![Data-skew problem example](./media/data-lake-analytics-data-lake-tools-data-skew-solutions/data-skew-problem.png)</span></span>

<span data-ttu-id="ca732-110">Dans notre scénario, les données de salutation sont distribuées inégalement entre tous les examinateurs de taxes, ce qui signifie que certaines examinateurs doivent fonctionner plus que d’autres.</span><span class="sxs-lookup"><span data-stu-id="ca732-110">In our scenario, hello data is unevenly distributed across all tax examiners, which means that some examiners must work more than others.</span></span> <span data-ttu-id="ca732-111">Dans votre travail, vous rencontrez souvent situations comme exemple de taxe-examiner hello ici.</span><span class="sxs-lookup"><span data-stu-id="ca732-111">In your own job, you frequently experience situations like hello tax-examiner example here.</span></span> <span data-ttu-id="ca732-112">En termes plus techniques, un sommet obtient beaucoup plus de données à ses homologues, une situation qui rend les sommets hello plus que d’autres et qui finalement ralentit l’intégralité du travail de hello de travail.</span><span class="sxs-lookup"><span data-stu-id="ca732-112">In more technical terms, one vertex gets much more data than its peers, a situation that makes hello vertex work more than hello others and that eventually slows down an entire job.</span></span> <span data-ttu-id="ca732-113">Qui plus est, hello travail peut échouer, car les sommets doivent, par exemple, une limitation de l’exécution de 5 heures et une limitation de 6 Go de mémoire.</span><span class="sxs-lookup"><span data-stu-id="ca732-113">What's worse, hello job might fail, because vertices might have, for example, a 5-hour runtime limitation and a 6-GB memory limitation.</span></span>

## <a name="resolving-data-skew-problems"></a><span data-ttu-id="ca732-114">Résolution de problèmes liés à l'asymétrie des données</span><span class="sxs-lookup"><span data-stu-id="ca732-114">Resolving data-skew problems</span></span>

<span data-ttu-id="ca732-115">Azure Data Lake Tools pour Visual Studio peut aider à détecter un éventuel problème d'asymétrie des données dans votre tâche.</span><span class="sxs-lookup"><span data-stu-id="ca732-115">Azure Data Lake Tools for Visual Studio can help detect whether your job has a data-skew problem.</span></span> <span data-ttu-id="ca732-116">En cas de problème, vous pouvez le résoudre en essayant de solutions hello dans cette section.</span><span class="sxs-lookup"><span data-stu-id="ca732-116">If a problem exists, you can resolve it by trying hello solutions in this section.</span></span>

## <a name="solution-1-improve-table-partitioning"></a><span data-ttu-id="ca732-117">Solution 1 : Améliorer le partitionnement de tables</span><span class="sxs-lookup"><span data-stu-id="ca732-117">Solution 1: Improve table partitioning</span></span>

### <a name="option-1-filter-hello-skewed-key-value-in-advance"></a><span data-ttu-id="ca732-118">Option 1 : Hello de filtre valeur de clé asymétrique à l’avance</span><span class="sxs-lookup"><span data-stu-id="ca732-118">Option 1: Filter hello skewed key value in advance</span></span>

<span data-ttu-id="ca732-119">Si elle n’affecte pas votre logique métier, vous pouvez filtrer les valeurs de fréquence plus élevée hello à l’avance.</span><span class="sxs-lookup"><span data-stu-id="ca732-119">If it does not affect your business logic, you can filter hello higher-frequency values in advance.</span></span> <span data-ttu-id="ca732-120">Par exemple, s’il existe un grand nombre de 000 000-000 dans la colonne GUID, vous pouvez tooaggregate cette valeur.</span><span class="sxs-lookup"><span data-stu-id="ca732-120">For example, if there are a lot of 000-000-000 in column GUID, you might not want tooaggregate that value.</span></span> <span data-ttu-id="ca732-121">Avant d’agrégation, vous pouvez écrire « WHERE GUID ! = « 000-000 000 » « valeur de haute fréquence toofilter hello.</span><span class="sxs-lookup"><span data-stu-id="ca732-121">Before you aggregate, you can write “WHERE GUID != “000-000-000”” toofilter hello high-frequency value.</span></span>

### <a name="option-2-pick-a-different-partition-or-distribution-key"></a><span data-ttu-id="ca732-122">Option 2 : Sélectionner une clé de distribution ou de partition différente</span><span class="sxs-lookup"><span data-stu-id="ca732-122">Option 2: Pick a different partition or distribution key</span></span>

<span data-ttu-id="ca732-123">Bonjour précédent exemple, si vous souhaitez que la charge de travail uniquement toocheck hello-fiscaux tous sur hello pays, vous pouvez améliorer la distribution des données hello en sélectionnant le numéro d’identification hello comme clé.</span><span class="sxs-lookup"><span data-stu-id="ca732-123">In hello preceding example, if you want only toocheck hello tax-audit workload all over hello country, you can improve hello data distribution by selecting hello ID number as your key.</span></span> <span data-ttu-id="ca732-124">Sélection d’une autre partition ou une clé de distribution peut parfois distribuer hello données plus équitablement, mais vous devez toomake vraiment que ce choix n’affecte pas votre logique métier.</span><span class="sxs-lookup"><span data-stu-id="ca732-124">Picking a different partition or distribution key can sometimes distribute hello data more evenly, but you need toomake sure that this choice doesn’t affect your business logic.</span></span> <span data-ttu-id="ca732-125">Par exemple, des somme toocalculate hello taxe pour chaque état, vous pourriez toodesignate _état_ en tant que clé de partition hello.</span><span class="sxs-lookup"><span data-stu-id="ca732-125">For instance, toocalculate hello tax sum for each state, you might want toodesignate _State_ as hello partition key.</span></span> <span data-ttu-id="ca732-126">Si vous continuez à tooexperience ce problème, essayez d’utiliser l’Option 3.</span><span class="sxs-lookup"><span data-stu-id="ca732-126">If you continue tooexperience this problem, try using Option 3.</span></span>

### <a name="option-3-add-more-partition-or-distribution-keys"></a><span data-ttu-id="ca732-127">Option 3 : Ajouter plus de clés de distribution ou de partition</span><span class="sxs-lookup"><span data-stu-id="ca732-127">Option 3: Add more partition or distribution keys</span></span>

<span data-ttu-id="ca732-128">Au lieu d’utiliser uniquement _l'état_ comme clé de partition, vous pouvez utiliser plusieurs clés pour le partitionnement.</span><span class="sxs-lookup"><span data-stu-id="ca732-128">Instead of using only _State_ as a partition key, you can use more than one key for partitioning.</span></span> <span data-ttu-id="ca732-129">Par exemple, envisagez d’ajouter _Code postal_ comme une partition supplémentaire partition de données de clé tooreduce tailles et répartir plus équitablement les données de salutation.</span><span class="sxs-lookup"><span data-stu-id="ca732-129">For example, consider adding _ZIP Code_ as an additional partition key tooreduce data-partition sizes and distribute hello data more evenly.</span></span>

### <a name="option-4-use-round-robin-distribution"></a><span data-ttu-id="ca732-130">Option 4 : Utiliser la distribution par tourniquet (round robin)</span><span class="sxs-lookup"><span data-stu-id="ca732-130">Option 4: Use round-robin distribution</span></span>

<span data-ttu-id="ca732-131">Si vous ne peut pas trouver une clé appropriée pour la partition et la distribution, vous pouvez essayer de distribution de tourniquet toouse.</span><span class="sxs-lookup"><span data-stu-id="ca732-131">If you cannot find an appropriate key for partition and distribution, you can try toouse round-robin distribution.</span></span> <span data-ttu-id="ca732-132">La distribution par tourniquet (round robin) traite toutes les lignes de manière égale et les place au hasard dans des compartiments correspondants.</span><span class="sxs-lookup"><span data-stu-id="ca732-132">Round-robin distribution treats all rows equally and randomly puts them into corresponding buckets.</span></span> <span data-ttu-id="ca732-133">les données de salutation obtient distribuées uniformément, mais lors de la perte d’informations localité, un inconvénient qui peut également réduire les performances pour certaines opérations.</span><span class="sxs-lookup"><span data-stu-id="ca732-133">hello data gets evenly distributed, but it loses locality information, a drawback that can also reduce job performance for some operations.</span></span> <span data-ttu-id="ca732-134">En outre, si vous effectuez d’agrégation pour la clé asymétrique de hello malgré tout, hello inclinaison de données problème persiste.</span><span class="sxs-lookup"><span data-stu-id="ca732-134">Additionally, if you are doing aggregation for hello skewed key anyway, hello data-skew problem will persist.</span></span> <span data-ttu-id="ca732-135">toolearn savoir plus sur la distribution alternée, consultez hello U-SQL Table Distributions section [CREATE TABLE (U-SQL) : création d’une Table avec schéma](https://msdn.microsoft.com/en-us/library/mt706196.aspx#dis_sch).</span><span class="sxs-lookup"><span data-stu-id="ca732-135">toolearn more about round-robin distribution, see hello U-SQL Table Distributions section in [CREATE TABLE (U-SQL): Creating a Table with Schema](https://msdn.microsoft.com/en-us/library/mt706196.aspx#dis_sch).</span></span>

## <a name="solution-2-improve-hello-query-plan"></a><span data-ttu-id="ca732-136">Solution 2 : Améliorer le plan de requête hello</span><span class="sxs-lookup"><span data-stu-id="ca732-136">Solution 2: Improve hello query plan</span></span>

### <a name="option-1-use-hello-create-statistics-statement"></a><span data-ttu-id="ca732-137">Option 1 : Utilisez l’instruction CREATE STATISTICS hello</span><span class="sxs-lookup"><span data-stu-id="ca732-137">Option 1: Use hello CREATE STATISTICS statement</span></span>

<span data-ttu-id="ca732-138">U-SQL fournit l’instruction CREATE STATISTICS hello sur les tables.</span><span class="sxs-lookup"><span data-stu-id="ca732-138">U-SQL provides hello CREATE STATISTICS statement on tables.</span></span> <span data-ttu-id="ca732-139">Cette instruction donne l’optimiseur de requête plus d’informations toohello sur hello données caractéristiques, telles que la distribution de la valeur, qui sont stockées dans une table.</span><span class="sxs-lookup"><span data-stu-id="ca732-139">This statement gives more information toohello query optimizer about hello data characteristics, such as value distribution, that are stored in a table.</span></span> <span data-ttu-id="ca732-140">Pour la plupart des requêtes, optimiseur de requête hello génère déjà les statistiques nécessaires hello pour un plan de requête de haute qualité.</span><span class="sxs-lookup"><span data-stu-id="ca732-140">For most queries, hello query optimizer already generates hello necessary statistics for a high-quality query plan.</span></span> <span data-ttu-id="ca732-141">Parfois, vous devrez peut-être les performances des requêtes tooimprove en créant des statistiques supplémentaires avec CREATE STATISTICS ou en modifiant la conception de requête hello.</span><span class="sxs-lookup"><span data-stu-id="ca732-141">Occasionally, you might need tooimprove query performance by creating additional statistics with CREATE STATISTICS or by modifying hello query design.</span></span> <span data-ttu-id="ca732-142">Pour plus d’informations, consultez hello [CREATE STATISTICS (U-SQL)](https://msdn.microsoft.com/en-us/library/azure/mt771898.aspx) page.</span><span class="sxs-lookup"><span data-stu-id="ca732-142">For more information, see hello [CREATE STATISTICS (U-SQL)](https://msdn.microsoft.com/en-us/library/azure/mt771898.aspx) page.</span></span>

<span data-ttu-id="ca732-143">Exemple de code :</span><span class="sxs-lookup"><span data-stu-id="ca732-143">Code example:</span></span>

    CREATE STATISTICS IF NOT EXISTS stats_SampleTable_date ON SampleDB.dbo.SampleTable(date) WITH FULLSCAN;

>[!NOTE]
><span data-ttu-id="ca732-144">Les informations statistiques ne sont pas mises à jour automatiquement.</span><span class="sxs-lookup"><span data-stu-id="ca732-144">Statistics information is not updated automatically.</span></span> <span data-ttu-id="ca732-145">Si vous mettez à jour les données hello dans une table sans recréer des statistiques de hello, les performances des requêtes hello peuvent refuser.</span><span class="sxs-lookup"><span data-stu-id="ca732-145">If you update hello data in a table without re-creating hello statistics, hello query performance might decline.</span></span>

### <a name="option-2-use-skewfactor"></a><span data-ttu-id="ca732-146">Option 2 : Utiliser SKEWFACTOR</span><span class="sxs-lookup"><span data-stu-id="ca732-146">Option 2: Use SKEWFACTOR</span></span>

<span data-ttu-id="ca732-147">Si vous souhaitez que des taxes de hello toosum pour chaque état, vous devez utiliser Grouper par état, une approche qui ne d’éviter le problème de données-inclinaison hello.</span><span class="sxs-lookup"><span data-stu-id="ca732-147">If you want toosum hello tax for each state, you must use GROUP BY state, an approach that doesn't avoid hello data-skew problem.</span></span> <span data-ttu-id="ca732-148">Toutefois, vous pouvez fournir un indicateur de données dans votre tooidentify requête données biaiser clés afin de pouvoir les optimiseur hello préparer un plan d’exécution pour vous.</span><span class="sxs-lookup"><span data-stu-id="ca732-148">However, you can provide a data hint in your query tooidentify data skew in keys so that hello optimizer can prepare an execution plan for you.</span></span>

<span data-ttu-id="ca732-149">En règle générale, vous pouvez définir le paramètre hello comme 0,5 et 1, 0,5, ce qui signifie que peu inclinaison lourde signification inclinaison et 1.</span><span class="sxs-lookup"><span data-stu-id="ca732-149">Usually, you can set hello parameter as 0.5 and 1, with 0.5 meaning not much skew and 1 meaning heavy skew.</span></span> <span data-ttu-id="ca732-150">Comme indicateur de hello affecte l’optimisation du plan d’exécution de l’instruction en cours hello et toutes les instructions en aval, pour pouvoir qu’indicateur de hello tooadd hello potentiel rétrécie key-wise d’agrégation.</span><span class="sxs-lookup"><span data-stu-id="ca732-150">Because hello hint affects execution-plan optimization for hello current statement and all downstream statements, be sure tooadd hello hint before hello potential skewed key-wise aggregation.</span></span>

    SKEWFACTOR (columns) = x

    Provides a hint that hello given columns have a skew factor x from 0 (no skew) through 1 (very heavy skew).

<span data-ttu-id="ca732-151">Exemple de code :</span><span class="sxs-lookup"><span data-stu-id="ca732-151">Code example:</span></span>

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

### <a name="option-3-use-rowcount"></a><span data-ttu-id="ca732-152">Option 3 : Utiliser ROWCOUNT</span><span class="sxs-lookup"><span data-stu-id="ca732-152">Option 3: Use ROWCOUNT</span></span>  
<span data-ttu-id="ca732-153">En outre tooSKEWFACTOR, pour la clé asymétrique spécifique joindre des cas, si vous savez que hello autre ensemble de lignes jointes est petit, vous pouvez indiquer l’optimiseur de hello en ajoutant un indicateur du nombre de lignes dans l’instruction de U-SQL hello avant la jointure.</span><span class="sxs-lookup"><span data-stu-id="ca732-153">In addition tooSKEWFACTOR, for specific skewed-key join cases, if you know that hello other joined row set is small, you can tell hello optimizer by adding a ROWCOUNT hint in hello U-SQL statement before JOIN.</span></span> <span data-ttu-id="ca732-154">De cette manière, optimiseur peut choisir un toohelp de stratégie de jointure diffusion améliorer les performances.</span><span class="sxs-lookup"><span data-stu-id="ca732-154">This way, optimizer can choose a broadcast join strategy toohelp improve performance.</span></span> <span data-ttu-id="ca732-155">N’oubliez pas que nombre de lignes ne résout pas le problème de données-inclinaison hello, mais il peut proposer une assistance supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="ca732-155">Be aware that ROWCOUNT does not resolve hello data-skew problem, but it can offer some additional help.</span></span>

    OPTION(ROWCOUNT = n)

    Identify a small row set before JOIN by providing an estimated integer row count.

<span data-ttu-id="ca732-156">Exemple de code :</span><span class="sxs-lookup"><span data-stu-id="ca732-156">Code example:</span></span>

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

## <a name="solution-3-improve-hello-user-defined-reducer-and-combiner"></a><span data-ttu-id="ca732-157">Solution 3 : Améliorer COMBINATEUR et réducteur de hello défini par l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="ca732-157">Solution 3: Improve hello user-defined reducer and combiner</span></span>

<span data-ttu-id="ca732-158">Vous pouvez écrire parfois un toodeal opérateur défini par l’utilisateur avec une logique complexe de processus et un réducteur bien écrite et l’association peuvent atténuer un problème d’inclinaison de données dans certains cas.</span><span class="sxs-lookup"><span data-stu-id="ca732-158">You can sometimes write a user-defined operator toodeal with complicated process logic, and a well-written reducer and combiner might mitigate a data-skew problem in some cases.</span></span>

### <a name="option-1-use-a-recursive-reducer-if-possible"></a><span data-ttu-id="ca732-159">Option 1 : Utiliser un réducteur récursif si possible</span><span class="sxs-lookup"><span data-stu-id="ca732-159">Option 1: Use a recursive reducer, if possible</span></span>

<span data-ttu-id="ca732-160">Par défaut, le réducteur défini par l’utilisateur s’exécute en mode non récursif, ce qui signifie que le travail de réduction pour une clé est distribué dans un seul vertex.</span><span class="sxs-lookup"><span data-stu-id="ca732-160">By default, a user-defined reducer runs in non-recursive mode, which means that reduce work for a key is distributed into a single vertex.</span></span> <span data-ttu-id="ca732-161">Mais si vos données sont déformées, hello les jeux de données volumineux peuvent être traitées dans un sommet unique et exécuter pendant un certain temps.</span><span class="sxs-lookup"><span data-stu-id="ca732-161">But if your data is skewed, hello huge data sets might be processed in a single vertex and run for a long time.</span></span>

<span data-ttu-id="ca732-162">tooimprove des performances, vous pouvez ajouter un attribut dans votre toorun de réducteur toodefine code en mode de récursive.</span><span class="sxs-lookup"><span data-stu-id="ca732-162">tooimprove performance, you can add an attribute in your code toodefine reducer toorun in recursive mode.</span></span> <span data-ttu-id="ca732-163">Ensuite, hello les jeux de données volumineux peut être distribuée toomultiple sommets et s’exécuter en parallèle, ce qui accélère votre travail.</span><span class="sxs-lookup"><span data-stu-id="ca732-163">Then, hello huge data sets can be distributed toomultiple vertices and run in parallel, which speeds up your job.</span></span>

<span data-ttu-id="ca732-164">toochange un toorecursive du réducteur non récursive, vous devez toomake assurer que votre algorithme est associatif.</span><span class="sxs-lookup"><span data-stu-id="ca732-164">toochange a non-recursive reducer toorecursive, you need toomake sure that your algorithm is associative.</span></span> <span data-ttu-id="ca732-165">Par exemple, somme de hello est associative et hello median n’est pas.</span><span class="sxs-lookup"><span data-stu-id="ca732-165">For example, hello sum is associative, and hello median is not.</span></span> <span data-ttu-id="ca732-166">Vous devez également toomake vraiment que hello d’entrée et sortie pour le réducteur conservent hello même schéma.</span><span class="sxs-lookup"><span data-stu-id="ca732-166">You also need toomake sure that hello input and output for reducer keep hello same schema.</span></span>

<span data-ttu-id="ca732-167">Attribut d'un réducteur récursif :</span><span class="sxs-lookup"><span data-stu-id="ca732-167">Attribute of recursive reducer:</span></span>

    [SqlUserDefinedReducer(IsRecursive = true)]

<span data-ttu-id="ca732-168">Exemple de code :</span><span class="sxs-lookup"><span data-stu-id="ca732-168">Code example:</span></span>

    [SqlUserDefinedReducer(IsRecursive = true)]
    public class TopNReducer : IReducer
    {
        public override IEnumerable<IRow>
            Reduce(IRowset input, IUpdatableRow output)
        {
            //Your reducer code goes here.
        }
    }

### <a name="option-2-use-row-level-combiner-mode-if-possible"></a><span data-ttu-id="ca732-169">Option 2 : Utiliser le mode de combinateur au niveau des lignes si possible</span><span class="sxs-lookup"><span data-stu-id="ca732-169">Option 2: Use row-level combiner mode, if possible</span></span>

<span data-ttu-id="ca732-170">Indicateur de nombre de lignes toohello similaires pour les cas de jointure de clé asymétrique spécifique, en mode d’association tente toodistribute énorme valeur de clé asymétrique jeux toomultiple sommets afin que le travail de hello pouvant être exécuté simultanément.</span><span class="sxs-lookup"><span data-stu-id="ca732-170">Similar toohello ROWCOUNT hint for specific skewed-key join cases, combiner mode tries toodistribute huge skewed-key value sets toomultiple vertices so that hello work can be executed concurrently.</span></span> <span data-ttu-id="ca732-171">Le mode de combinateur ne permet pas de résoudre le problème d'asymétrie des données, mais peut être utile pour traiter les ensembles de valeurs de clés de décalage volumineux.</span><span class="sxs-lookup"><span data-stu-id="ca732-171">Combiner mode can’t resolve data-skew issues, but it can offer some additional help for huge skewed-key value sets.</span></span>

<span data-ttu-id="ca732-172">Par défaut, le mode d’association hello est complet, ce qui signifie que hello gauche ensemble de lignes, et ensemble de lignes à droite ne peut pas être séparées par des.</span><span class="sxs-lookup"><span data-stu-id="ca732-172">By default, hello combiner mode is Full, which means that hello left row set and right row set cannot be separated.</span></span> <span data-ttu-id="ca732-173">Définition du mode hello comme gauche/droite/interne permet au niveau de la ligne de jointure.</span><span class="sxs-lookup"><span data-stu-id="ca732-173">Setting hello mode as Left/Right/Inner enables row-level join.</span></span> <span data-ttu-id="ca732-174">système de Hello sépare les ensembles de lignes correspondantes hello et comment les répartit dans plusieurs sommets qui s’exécutent en parallèle.</span><span class="sxs-lookup"><span data-stu-id="ca732-174">hello system separates hello corresponding row sets and distributes them into multiple vertices that run in parallel.</span></span> <span data-ttu-id="ca732-175">Toutefois, avant de configurer le mode COMBINATEUR hello, veillez à tooensure qui hello correspondante des ensembles de lignes peut être séparé.</span><span class="sxs-lookup"><span data-stu-id="ca732-175">However, before you configure hello combiner mode, be careful tooensure that hello corresponding row sets can be separated.</span></span>

<span data-ttu-id="ca732-176">exemple Hello qui suit montre un ensemble de valeurs séparées par des lignes de gauche.</span><span class="sxs-lookup"><span data-stu-id="ca732-176">hello example that follows shows a separated left row set.</span></span> <span data-ttu-id="ca732-177">Chaque ligne de sortie dépend d’une seule ligne d’entrée de hello gauche, et potentiellement dépend de toutes les lignes de hello droite avec hello même valeur de clé.</span><span class="sxs-lookup"><span data-stu-id="ca732-177">Each output row depends on a single input row from hello left, and it potentially depends on all rows from hello right with hello same key value.</span></span> <span data-ttu-id="ca732-178">Si vous définissez le mode d’association hello de gauche, système de hello sépare hello énorme gauche-ensemble de lignes dans les petits et les affecte toomultiple sommets.</span><span class="sxs-lookup"><span data-stu-id="ca732-178">If you set hello combiner mode as left, hello system separates hello huge left-row set into small ones and assigns them toomultiple vertices.</span></span>

![Illustration du mode de combinateur](./media/data-lake-analytics-data-lake-tools-data-skew-solutions/combiner-mode-illustration.png)

>[!NOTE]
><span data-ttu-id="ca732-180">Si vous définissez le mode d’association incorrect hello, combinaison de hello est moins efficace, et les résultats de hello sont peut-être erronés.</span><span class="sxs-lookup"><span data-stu-id="ca732-180">If you set hello wrong combiner mode, hello combination is less efficient, and hello results might be wrong.</span></span>

<span data-ttu-id="ca732-181">Attributs du mode de combinateur :</span><span class="sxs-lookup"><span data-stu-id="ca732-181">Attributes of combiner mode:</span></span>

- [SqlUserDefinedCombiner(Mode=CombinerMode.Full)]: Every output row potentially depends on all hello input rows from left and right with hello same key value.

- <span data-ttu-id="ca732-182">SqlUserDefinedCombiner(Mode=CombinerMode.Left) : Chaque ligne de sortie dépend d’une seule ligne d’entrée de hello gauche (et potentiellement toutes les lignes de hello droite avec hello même valeur de clé).</span><span class="sxs-lookup"><span data-stu-id="ca732-182">SqlUserDefinedCombiner(Mode=CombinerMode.Left): Every output row depends on a single input row from hello left (and potentially all rows from hello right with hello same key value).</span></span>

- <span data-ttu-id="ca732-183">qlUserDefinedCombiner(Mode=CombinerMode.Right) : chaque ligne de sortie dépend d’une ligne d’entrée de hello droit (et potentiellement toutes les lignes de gauche hello avec hello même valeur de clé).</span><span class="sxs-lookup"><span data-stu-id="ca732-183">qlUserDefinedCombiner(Mode=CombinerMode.Right): Every output row depends on a single input row from hello right (and potentially all rows from hello left with hello same key value).</span></span>

- <span data-ttu-id="ca732-184">SqlUserDefinedCombiner(Mode=CombinerMode.Inner) : Chaque ligne de sortie dépend une ligne d’entrée de hello gauche et hello droite avec hello même valeur.</span><span class="sxs-lookup"><span data-stu-id="ca732-184">SqlUserDefinedCombiner(Mode=CombinerMode.Inner): Every output row depends on a single input row from hello left and hello right with hello same value.</span></span>

<span data-ttu-id="ca732-185">Exemple de code :</span><span class="sxs-lookup"><span data-stu-id="ca732-185">Code example:</span></span>

    [SqlUserDefinedCombiner(Mode = CombinerMode.Right)]
    public class WatsonDedupCombiner : ICombiner
    {
        public override IEnumerable<IRow>
            Combine(IRowset left, IRowset right, IUpdatableRow output)
        {
        //Your combiner code goes here.
        }
    }
