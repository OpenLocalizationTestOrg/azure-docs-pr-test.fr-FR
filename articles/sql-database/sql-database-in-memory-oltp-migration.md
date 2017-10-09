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
# <a name="use-in-memory-oltp-tooimprove-your-application-performance-in-sql-database"></a><span data-ttu-id="595de-103">Utilisez l’OLTP en mémoire tooimprove les performances de votre application de base de données SQL</span><span class="sxs-lookup"><span data-stu-id="595de-103">Use In-Memory OLTP tooimprove your application performance in SQL Database</span></span>
<span data-ttu-id="595de-104">[OLTP en mémoire](sql-database-in-memory.md) peut être utilisé tooimprove les performances de hello de traitement des transactions, intégrer les données et les scénarios de données temporaires dans [Premium](sql-database-service-tiers.md) bases de données SQL Azure sans augmenter hello niveau tarifaire.</span><span class="sxs-lookup"><span data-stu-id="595de-104">[In-Memory OLTP](sql-database-in-memory.md) can be used tooimprove hello performance of transaction processing, data ingestion, and transient data scenarios, in  [Premium](sql-database-service-tiers.md) Azure SQL Databases without increasing hello pricing tier.</span></span> 

> [!NOTE] 
> <span data-ttu-id="595de-105">Découvrez comment le [Quorum double la charge de travail de la base de données clé tout en réduisant les DTU de 70 % avec la SQL Database](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database)</span><span class="sxs-lookup"><span data-stu-id="595de-105">Learn how [Quorum doubles key database’s workload while lowering DTU by 70% with SQL Database](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database)</span></span>


<span data-ttu-id="595de-106">Suivez ces étapes de tooadopt OLTP en mémoire dans votre base de données existante.</span><span class="sxs-lookup"><span data-stu-id="595de-106">Follow these steps tooadopt In-Memory OLTP in your existing database.</span></span>

## <a name="step-1-ensure-you-are-using-a-premium-database"></a><span data-ttu-id="595de-107">Étape 1 : vérifiez que vous utilisez une base de données Premium</span><span class="sxs-lookup"><span data-stu-id="595de-107">Step 1: Ensure you are using a Premium database</span></span>
<span data-ttu-id="595de-108">OLTP en mémoire est pris en charge uniquement dans les bases de données Premium.</span><span class="sxs-lookup"><span data-stu-id="595de-108">In-Memory OLTP is supported only in Premium databases.</span></span> <span data-ttu-id="595de-109">En mémoire est prise en charge si hello renvoyé de résultat est 1 (pas 0) :</span><span class="sxs-lookup"><span data-stu-id="595de-109">In-Memory is supported if hello returned result is 1 (not 0):</span></span>

```
SELECT DatabasePropertyEx(Db_Name(), 'IsXTPSupported');
```

<span data-ttu-id="595de-110">L’acronyme *XTP* signifie *Extreme Transaction Processing (Traitement de transactions extrêmes)*</span><span class="sxs-lookup"><span data-stu-id="595de-110">*XTP* stands for *Extreme Transaction Processing*</span></span>



## <a name="step-2-identify-objects-toomigrate-tooin-memory-oltp"></a><span data-ttu-id="595de-111">Étape 2 : Identifier les objets toomigrate tooIn-mémoire OLTP</span><span class="sxs-lookup"><span data-stu-id="595de-111">Step 2: Identify objects toomigrate tooIn-Memory OLTP</span></span>
<span data-ttu-id="595de-112">SSMS inclut un rapport de **présentation d’analyse des performances des transactions** que vous pouvez exécuter sur une base de données avec une charge de travail active.</span><span class="sxs-lookup"><span data-stu-id="595de-112">SSMS includes a **Transaction Performance Analysis Overview** report that you can run against a database with an active workload.</span></span> <span data-ttu-id="595de-113">rapport de Hello identifie les tables et procédures stockées qui sont candidates pour la migration OLTP en mémoire tooIn.</span><span class="sxs-lookup"><span data-stu-id="595de-113">hello report identifies tables and stored procedures that are candidates for migration tooIn-Memory OLTP.</span></span>

<span data-ttu-id="595de-114">Dans SSMS, rapport de hello toogenerate :</span><span class="sxs-lookup"><span data-stu-id="595de-114">In SSMS, toogenerate hello report:</span></span>

* <span data-ttu-id="595de-115">Bonjour **l’Explorateur d’objets**, cliquez sur le nœud de votre base de données.</span><span class="sxs-lookup"><span data-stu-id="595de-115">In hello **Object Explorer**, right-click your database node.</span></span>
* <span data-ttu-id="595de-116">Cliquez sur **Rapports** > **Rapports Standard** > **Présentation de l’analyse des performances des transactions**.</span><span class="sxs-lookup"><span data-stu-id="595de-116">Click **Reports** > **Standard Reports** > **Transaction Performance Analysis Overview**.</span></span>

<span data-ttu-id="595de-117">Pour plus d’informations, consultez [déterminer si une Table ou une procédure stockée doit être déplacée tooIn l’OLTP en mémoire](http://msdn.microsoft.com/library/dn205133.aspx).</span><span class="sxs-lookup"><span data-stu-id="595de-117">For more information, see [Determining if a Table or Stored Procedure Should Be Ported tooIn-Memory OLTP](http://msdn.microsoft.com/library/dn205133.aspx).</span></span>

## <a name="step-3-create-a-comparable-test-database"></a><span data-ttu-id="595de-118">Étape 3 : Créer une base de données de test comparable</span><span class="sxs-lookup"><span data-stu-id="595de-118">Step 3: Create a comparable test database</span></span>
<span data-ttu-id="595de-119">Supposons que le rapport de hello indique votre base de données a une table qui tirent parti d’être convertie table mémoire optimisée de tooa.</span><span class="sxs-lookup"><span data-stu-id="595de-119">Suppose hello report indicates your database has a table that would benefit from being converted tooa memory-optimized table.</span></span> <span data-ttu-id="595de-120">Nous vous recommandons de commencer par tester indication de hello tooconfirm en testant.</span><span class="sxs-lookup"><span data-stu-id="595de-120">We recommend that you first test tooconfirm hello indication by testing.</span></span>

<span data-ttu-id="595de-121">Vous avez besoin d’une copie de test de votre base de données de production.</span><span class="sxs-lookup"><span data-stu-id="595de-121">You need a test copy of your production database.</span></span> <span data-ttu-id="595de-122">Hello base de données de test doit être à hello même niveau de la couche de service en tant que votre base de données de production.</span><span class="sxs-lookup"><span data-stu-id="595de-122">hello test database should be at hello same service tier level as your production database.</span></span>

<span data-ttu-id="595de-123">tooease tester, optimiser votre base de données de test comme suit :</span><span class="sxs-lookup"><span data-stu-id="595de-123">tooease testing, tweak your test database as follows:</span></span>

1. <span data-ttu-id="595de-124">Se connecter à base de données de test toohello à l’aide de SSMS.</span><span class="sxs-lookup"><span data-stu-id="595de-124">Connect toohello test database by using SSMS.</span></span>
2. <span data-ttu-id="595de-125">tooavoid avoir hello option WITH (SNAPSHOT) dans les requêtes, attribuez une option de base de données hello comme Bonjour instruction T-SQL suivante :</span><span class="sxs-lookup"><span data-stu-id="595de-125">tooavoid needing hello WITH (SNAPSHOT) option in queries, set hello database option as shown in hello following T-SQL statement:</span></span>
   
   ```
   ALTER DATABASE CURRENT
    SET
        MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT = ON;
   ```

## <a name="step-4-migrate-tables"></a><span data-ttu-id="595de-126">Étape 4 : Migrer les tables</span><span class="sxs-lookup"><span data-stu-id="595de-126">Step 4: Migrate tables</span></span>
<span data-ttu-id="595de-127">Vous devez créer et remplir une copie mémoire optimisée de la table de hello souhaité tootest.</span><span class="sxs-lookup"><span data-stu-id="595de-127">You must create and populate a memory-optimized copy of hello table you want tootest.</span></span> <span data-ttu-id="595de-128">Vous pouvez le créer en utilisant soit :</span><span class="sxs-lookup"><span data-stu-id="595de-128">You can create it by using either:</span></span>

* <span data-ttu-id="595de-129">Hello pratique Assistant Optimisation de mémoire dans SSMS.</span><span class="sxs-lookup"><span data-stu-id="595de-129">hello handy Memory Optimization Wizard in SSMS.</span></span>
* <span data-ttu-id="595de-130">T-SQL manuel.</span><span class="sxs-lookup"><span data-stu-id="595de-130">Manual T-SQL.</span></span>

#### <a name="memory-optimization-wizard-in-ssms"></a><span data-ttu-id="595de-131">Assistant Optimisation de mémoire en SSMS</span><span class="sxs-lookup"><span data-stu-id="595de-131">Memory Optimization Wizard in SSMS</span></span>
<span data-ttu-id="595de-132">toouse cette option de migration :</span><span class="sxs-lookup"><span data-stu-id="595de-132">toouse this migration option:</span></span>

1. <span data-ttu-id="595de-133">Se connecter à base de données de test toohello avec SSMS.</span><span class="sxs-lookup"><span data-stu-id="595de-133">Connect toohello test database with SSMS.</span></span>
2. <span data-ttu-id="595de-134">Bonjour **l’Explorateur d’objets**, avec le bouton droit sur la table de hello, puis cliquez sur **conseiller d’optimisation de mémoire**.</span><span class="sxs-lookup"><span data-stu-id="595de-134">In hello **Object Explorer**, right-click on hello table, and then click **Memory Optimization Advisor**.</span></span>
   
   * <span data-ttu-id="595de-135">Hello **Table mémoire optimiseur Advisor** Assistant s’affiche.</span><span class="sxs-lookup"><span data-stu-id="595de-135">hello **Table Memory Optimizer Advisor** wizard is displayed.</span></span>
3. <span data-ttu-id="595de-136">Dans l’Assistant de hello, cliquez sur **validation de la Migration** (ou hello **suivant** bouton) toosee si hello table a des non pris en charge les fonctionnalités qui sont prises en charge dans les tables optimisées en mémoire.</span><span class="sxs-lookup"><span data-stu-id="595de-136">In hello wizard, click **Migration validation** (or hello **Next** button) toosee if hello table has any unsupported features that are unsupported in memory-optimized tables.</span></span> <span data-ttu-id="595de-137">Pour plus d'informations, consultez les pages suivantes :</span><span class="sxs-lookup"><span data-stu-id="595de-137">For more information, see:</span></span>
   
   * <span data-ttu-id="595de-138">Hello *liste de vérification de l’optimisation mémoire* dans [conseiller d’optimisation de mémoire](http://msdn.microsoft.com/library/dn284308.aspx).</span><span class="sxs-lookup"><span data-stu-id="595de-138">hello *memory optimization checklist* in [Memory Optimization Advisor](http://msdn.microsoft.com/library/dn284308.aspx).</span></span>
   * <span data-ttu-id="595de-139">[Constructions Transact-SQL non prises en charge par In-Memory OLTP](http://msdn.microsoft.com/library/dn246937.aspx).</span><span class="sxs-lookup"><span data-stu-id="595de-139">[Transact-SQL Constructs Not Supported by In-Memory OLTP](http://msdn.microsoft.com/library/dn246937.aspx).</span></span>
   * <span data-ttu-id="595de-140">[L’OLTP en mémoire tooIn migration](http://msdn.microsoft.com/library/dn247639.aspx).</span><span class="sxs-lookup"><span data-stu-id="595de-140">[Migrating tooIn-Memory OLTP](http://msdn.microsoft.com/library/dn247639.aspx).</span></span>
4. <span data-ttu-id="595de-141">Si la table de hello n’a aucune fonctionnalité non prise en charge, le conseiller hello peut effectuer schéma hello et migration des données pour vous.</span><span class="sxs-lookup"><span data-stu-id="595de-141">If hello table has no unsupported features, hello advisor can perform hello actual schema and data migration for you.</span></span>

#### <a name="manual-t-sql"></a><span data-ttu-id="595de-142">T-SQL manuel</span><span class="sxs-lookup"><span data-stu-id="595de-142">Manual T-SQL</span></span>
<span data-ttu-id="595de-143">toouse cette option de migration :</span><span class="sxs-lookup"><span data-stu-id="595de-143">toouse this migration option:</span></span>

1. <span data-ttu-id="595de-144">Se connecter à base de données de test tooyour à l’aide de SSMS (ou un utilitaire similaire).</span><span class="sxs-lookup"><span data-stu-id="595de-144">Connect tooyour test database by using SSMS (or a similar utility).</span></span>
2. <span data-ttu-id="595de-145">Obtenir le script T-SQL complet de hello pour votre table et ses index.</span><span class="sxs-lookup"><span data-stu-id="595de-145">Obtain hello complete T-SQL script for your table and its indexes.</span></span>
   
   * <span data-ttu-id="595de-146">Dans SSMS, cliquez avec le bouton droit sur le nœud de votre table.</span><span class="sxs-lookup"><span data-stu-id="595de-146">In SSMS, right-click your table node.</span></span>
   * <span data-ttu-id="595de-147">Cliquez sur **Générer un script de la table en tant que** > **CREATE To** > **Fenêtre de nouvelle requête**.</span><span class="sxs-lookup"><span data-stu-id="595de-147">Click **Script Table As** > **CREATE To** > **New Query Window**.</span></span>
3. <span data-ttu-id="595de-148">Dans la fenêtre de script hello, ajoutez WITH (MEMORY_OPTIMIZED = ON) toohello l’instruction CREATE TABLE.</span><span class="sxs-lookup"><span data-stu-id="595de-148">In hello script window, add WITH (MEMORY_OPTIMIZED = ON) toohello CREATE TABLE statement.</span></span>
4. <span data-ttu-id="595de-149">En l’absence d’un index ordonné en clusters, modifiez-le tooNONCLUSTERED.</span><span class="sxs-lookup"><span data-stu-id="595de-149">If there is a CLUSTERED index, change it tooNONCLUSTERED.</span></span>
5. <span data-ttu-id="595de-150">Renommer la table existante de hello à l’aide de SP_RENAME.</span><span class="sxs-lookup"><span data-stu-id="595de-150">Rename hello existing table by using SP_RENAME.</span></span>
6. <span data-ttu-id="595de-151">Créer hello optimisées en mémoire copie de la table de hello en exécutant le script CREATE TABLE modifié.</span><span class="sxs-lookup"><span data-stu-id="595de-151">Create hello new memory-optimized copy of hello table by running your edited CREATE TABLE script.</span></span>
7. <span data-ttu-id="595de-152">Copier la table mémoire optimisée de hello données tooyour à l’aide de INSERT... SÉLECTIONNEZ * DANS :</span><span class="sxs-lookup"><span data-stu-id="595de-152">Copy hello data tooyour memory-optimized table by using INSERT...SELECT * INTO:</span></span>

```
INSERT INTO <new_memory_optimized_table>
        SELECT * FROM <old_disk_based_table>;
```


## <a name="step-5-optional-migrate-stored-procedures"></a><span data-ttu-id="595de-153">Étape 5 (facultative) : migrer les procédures stockées</span><span class="sxs-lookup"><span data-stu-id="595de-153">Step 5 (optional): Migrate stored procedures</span></span>
<span data-ttu-id="595de-154">fonctionnalité de mémoire Hello permettre également modifier une procédure stockée pour améliorer les performances.</span><span class="sxs-lookup"><span data-stu-id="595de-154">hello In-Memory feature can also modify a stored procedure for improved performance.</span></span>

### <a name="considerations-with-natively-compiled-stored-procedures"></a><span data-ttu-id="595de-155">Considérations relatives à des procédures stockées compilées en mode natif</span><span class="sxs-lookup"><span data-stu-id="595de-155">Considerations with natively compiled stored procedures</span></span>
<span data-ttu-id="595de-156">Une procédure stockée compilée en mode natif doit avoir hello options sur sa clause avec T-SQL suivantes :</span><span class="sxs-lookup"><span data-stu-id="595de-156">A natively compiled stored procedure must have hello following options on its T-SQL WITH clause:</span></span>

* <span data-ttu-id="595de-157">NATIVE_COMPILATION</span><span class="sxs-lookup"><span data-stu-id="595de-157">NATIVE_COMPILATION</span></span>
* <span data-ttu-id="595de-158">SCHEMABINDING : tables signification hello de procédure stockée ne peut pas avoir leurs définitions de colonne modifiées de quelque manière qui affecterait la procédure stockée hello, sauf si vous supprimez la procédure stockée hello.</span><span class="sxs-lookup"><span data-stu-id="595de-158">SCHEMABINDING: meaning tables that hello stored procedure cannot have their column definitions changed in any way that would affect hello stored procedure, unless you drop hello stored procedure.</span></span>

<span data-ttu-id="595de-159">Un module natif doit utiliser un grand [bloc ATOMIC](http://msdn.microsoft.com/library/dn452281.aspx) pour la gestion de transaction.</span><span class="sxs-lookup"><span data-stu-id="595de-159">A native module must use one big [ATOMIC blocks](http://msdn.microsoft.com/library/dn452281.aspx) for transaction management.</span></span> <span data-ttu-id="595de-160">Il n’existe aucun rôle pour une instruction BEGIN TRANSACTION ou ROLLBACK TRANSACTION explicite.</span><span class="sxs-lookup"><span data-stu-id="595de-160">There is no role for an explicit BEGIN TRANSACTION, or for ROLLBACK TRANSACTION.</span></span> <span data-ttu-id="595de-161">Si votre code détecte une violation d’une règle d’entreprise, il peut s’arrêter bloc atomique de hello avec un [lever](http://msdn.microsoft.com/library/ee677615.aspx) instruction.</span><span class="sxs-lookup"><span data-stu-id="595de-161">If your code detects a violation of a business rule, it can terminate hello atomic block with a [THROW](http://msdn.microsoft.com/library/ee677615.aspx) statement.</span></span>

### <a name="typical-create-procedure-for-natively-compiled"></a><span data-ttu-id="595de-162">En général, CREATE PROCEDURE compilée en mode natif</span><span class="sxs-lookup"><span data-stu-id="595de-162">Typical CREATE PROCEDURE for natively compiled</span></span>
<span data-ttu-id="595de-163">En règle générale, hello T-SQL toocreate une procédure stockée compilée en mode natif est similaire toohello suivant le modèle :</span><span class="sxs-lookup"><span data-stu-id="595de-163">Typically hello T-SQL toocreate a natively compiled stored procedure is similar toohello following template:</span></span>

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

* <span data-ttu-id="595de-164">Pour hello TRANSACTION_ISOLATION_LEVEL, instantané est la procédure la valeur pour hello compilée stockée hello plus courante.</span><span class="sxs-lookup"><span data-stu-id="595de-164">For hello TRANSACTION_ISOLATION_LEVEL, SNAPSHOT is hello most common value for hello natively compiled stored procedure.</span></span> <span data-ttu-id="595de-165">Toutefois, un sous-ensemble de hello autres valeurs sont également pris en charge :</span><span class="sxs-lookup"><span data-stu-id="595de-165">However,  a subset of hello other values are also supported:</span></span>
  
  * <span data-ttu-id="595de-166">REPEATABLE READ</span><span class="sxs-lookup"><span data-stu-id="595de-166">REPEATABLE READ</span></span>
  * <span data-ttu-id="595de-167">SERIALIZABLE</span><span class="sxs-lookup"><span data-stu-id="595de-167">SERIALIZABLE</span></span>
* <span data-ttu-id="595de-168">Hello valeur langue doit être présent dans la vue de sys.languages hello.</span><span class="sxs-lookup"><span data-stu-id="595de-168">hello LANGUAGE value must be present in hello sys.languages view.</span></span>

### <a name="how-toomigrate-a-stored-procedure"></a><span data-ttu-id="595de-169">Comment toomigrate une procédure stockée</span><span class="sxs-lookup"><span data-stu-id="595de-169">How toomigrate a stored procedure</span></span>
<span data-ttu-id="595de-170">les étapes de migration de Hello sont :</span><span class="sxs-lookup"><span data-stu-id="595de-170">hello migration steps are:</span></span>

1. <span data-ttu-id="595de-171">Obtenir hello CREATE PROCEDURE script toohello procédure stockée interprétée normale.</span><span class="sxs-lookup"><span data-stu-id="595de-171">Obtain hello CREATE PROCEDURE script toohello regular interpreted stored procedure.</span></span>
2. <span data-ttu-id="595de-172">Réécrire son en-tête toomatch hello précédent modèle.</span><span class="sxs-lookup"><span data-stu-id="595de-172">Rewrite its header toomatch hello previous template.</span></span>
3. <span data-ttu-id="595de-173">Vérifier si le procédure stockée hello code T-SQL utilise des fonctionnalités qui ne sont pas pris en charge pour les procédures stockées compilées en mode natif.</span><span class="sxs-lookup"><span data-stu-id="595de-173">Ascertain whether hello stored procedure T-SQL code uses any features that are not supported for natively compiled stored procedures.</span></span> <span data-ttu-id="595de-174">Mettre en œuvre des solutions de contournement si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="595de-174">Implement workarounds if necessary.</span></span>
   
   * <span data-ttu-id="595de-175">Pour plus d’informations, voir [Problèmes de migration pour les procédures stockées compilées natives](http://msdn.microsoft.com/library/dn296678.aspx).</span><span class="sxs-lookup"><span data-stu-id="595de-175">For details see [Migration Issues for Natively Compiled Stored Procedures](http://msdn.microsoft.com/library/dn296678.aspx).</span></span>
4. <span data-ttu-id="595de-176">Renommer une procédure stockée hello ancien à l’aide de SP_RENAME.</span><span class="sxs-lookup"><span data-stu-id="595de-176">Rename hello old stored procedure by using SP_RENAME.</span></span> <span data-ttu-id="595de-177">Ou FAITES-LE SIMPLEMENT GLISSER (DROP).</span><span class="sxs-lookup"><span data-stu-id="595de-177">Or simply DROP it.</span></span>
5. <span data-ttu-id="595de-178">Exécutez le script CREATE PROCEDURE T-SQL modifié.</span><span class="sxs-lookup"><span data-stu-id="595de-178">Run your edited CREATE PROCEDURE T-SQL script.</span></span>

## <a name="step-6-run-your-workload-in-test"></a><span data-ttu-id="595de-179">Étape 6 : exécuter votre charge de travail dans un test</span><span class="sxs-lookup"><span data-stu-id="595de-179">Step 6: Run your workload in test</span></span>
<span data-ttu-id="595de-180">Exécutez une charge de travail dans votre base de données de test est similaire toohello la charge de travail qui s’exécute dans votre base de données de production.</span><span class="sxs-lookup"><span data-stu-id="595de-180">Run a workload in your test database that is similar toohello workload that runs in your production database.</span></span> <span data-ttu-id="595de-181">Cela doit faire apparaître les gains de performances hello atteints par votre utilisation des fonctionnalités de In-Memory hello pour les tables et procédures stockées.</span><span class="sxs-lookup"><span data-stu-id="595de-181">This should reveal hello performance gain achieved by your use of hello In-Memory feature for tables and stored procedures.</span></span>

<span data-ttu-id="595de-182">Les attributs principaux de la charge de travail hello sont :</span><span class="sxs-lookup"><span data-stu-id="595de-182">Major attributes of hello workload are:</span></span>

* <span data-ttu-id="595de-183">Nombre de connexions simultanées.</span><span class="sxs-lookup"><span data-stu-id="595de-183">Number of concurrent connections.</span></span>
* <span data-ttu-id="595de-184">Rapport Lecture/Écriture</span><span class="sxs-lookup"><span data-stu-id="595de-184">Read/write ratio.</span></span>

<span data-ttu-id="595de-185">tootailor et test de charge de travail exécution hello, envisagez d’utiliser l’outil pratique ostress.exe hello, notamment [ici](sql-database-in-memory.md).</span><span class="sxs-lookup"><span data-stu-id="595de-185">tootailor and run hello test workload, consider using hello handy ostress.exe tool, which illustrated in [here](sql-database-in-memory.md).</span></span>

<span data-ttu-id="595de-186">latence du réseau toominimize, exécutez votre test Bonjour même région géographique Azure où la base de données hello existe.</span><span class="sxs-lookup"><span data-stu-id="595de-186">toominimize network latency, run your test in hello same Azure geographic region where hello database exists.</span></span>

## <a name="step-7-post-implementation-monitoring"></a><span data-ttu-id="595de-187">Étape 7 : surveillance post exécution</span><span class="sxs-lookup"><span data-stu-id="595de-187">Step 7: Post-implementation monitoring</span></span>
<span data-ttu-id="595de-188">Tenez compte des effets des performances hello de vos implémentations de mémoire en production d’analyse :</span><span class="sxs-lookup"><span data-stu-id="595de-188">Consider monitoring hello performance effects of your In-Memory implementations in production:</span></span>

* <span data-ttu-id="595de-189">[Surveiller le stockage en mémoire](sql-database-in-memory-oltp-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="595de-189">[Monitor In-Memory Storage](sql-database-in-memory-oltp-monitoring.md).</span></span>
* [<span data-ttu-id="595de-190">Analyse d’une base de données SQL Azure à l’aide de vues de gestion dynamique</span><span class="sxs-lookup"><span data-stu-id="595de-190">Monitoring Azure SQL Database using dynamic management views</span></span>](sql-database-monitoring-with-dmvs.md)

## <a name="related-links"></a><span data-ttu-id="595de-191">Liens connexes</span><span class="sxs-lookup"><span data-stu-id="595de-191">Related links</span></span>
* [<span data-ttu-id="595de-192">In-Memory OLTP (optimisation en mémoire)</span><span class="sxs-lookup"><span data-stu-id="595de-192">In-Memory OLTP (In-Memory Optimization)</span></span>](http://msdn.microsoft.com/library/dn133186.aspx)
* [<span data-ttu-id="595de-193">Introduction tooNatively de procédures stockées compilées</span><span class="sxs-lookup"><span data-stu-id="595de-193">Introduction tooNatively Compiled Stored Procedures</span></span>](http://msdn.microsoft.com/library/dn133184.aspx)
* [<span data-ttu-id="595de-194">Conseil d’optimisation par mémoire</span><span class="sxs-lookup"><span data-stu-id="595de-194">Memory Optimization Advisor</span></span>](http://msdn.microsoft.com/library/dn284308.aspx)

