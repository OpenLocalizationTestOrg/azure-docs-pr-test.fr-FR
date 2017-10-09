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
# <a name="create-and-manage-scaled-out-azure-sql-databases-using-elastic-jobs-preview"></a><span data-ttu-id="063fb-103">Créer et gérer des bases de données SQL Azure avec montée en charge à l’aide de tâches élastiques (version préliminaire)</span><span class="sxs-lookup"><span data-stu-id="063fb-103">Create and manage scaled out Azure SQL Databases using elastic jobs (preview)</span></span>


<span data-ttu-id="063fb-104">**tâches de bases de données élastiques** simplifient la gestion des groupes de bases de données en exécutant des opérations administratives telles que les modifications de schéma, la gestion des informations d’identification, les mises à jour de données de référence, la collecte des données de performances ou la collecte de données de télémétrie du locataire (client).</span><span class="sxs-lookup"><span data-stu-id="063fb-104">**Elastic Database jobs** simplify management of groups of databases by executing administrative operations such as schema changes, credentials management, reference data updates, performance data collection or tenant (customer) telemetry collection.</span></span> <span data-ttu-id="063fb-105">Les travaux de base de données élastiques est actuellement disponible via hello portail Azure et les applets de commande PowerShell.</span><span class="sxs-lookup"><span data-stu-id="063fb-105">Elastic Database jobs is currently available through hello Azure portal and PowerShell cmdlets.</span></span> <span data-ttu-id="063fb-106">Toutefois, hello surfaces du portail Azure des fonctionnalités réduites limité tooexecution sur toutes les bases de données dans un [pool élastique (version préliminaire)](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="063fb-106">However, hello Azure portal surfaces reduced functionality limited tooexecution across all databases in an [elastic pool (preview)](sql-database-elastic-pool.md).</span></span> <span data-ttu-id="063fb-107">tooaccess des fonctionnalités supplémentaires et l’exécution de scripts sur un groupe de bases de données, notamment une collection personnalisée ou une partition définie (créé à l’aide de [bibliothèque cliente de base de données élastique](sql-database-elastic-scale-introduction.md)), consultez [création et gestion travaux à l’aide de PowerShell](sql-database-elastic-jobs-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="063fb-107">tooaccess additional features and execution of scripts across a group of databases including a custom-defined collection or a shard set (created using [Elastic Database client library](sql-database-elastic-scale-introduction.md)), see [Creating and managing jobs using PowerShell](sql-database-elastic-jobs-powershell.md).</span></span> <span data-ttu-id="063fb-108">Pour en savoir plus sur les tâches, consultez la rubrique [Vue d'ensemble des tâches de bases de données élastiques](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="063fb-108">For more information about jobs, see [Elastic Database jobs overview](sql-database-elastic-jobs-overview.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="063fb-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="063fb-109">Prerequisites</span></span>
* <span data-ttu-id="063fb-110">Un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="063fb-110">An Azure subscription.</span></span> <span data-ttu-id="063fb-111">Pour un essai gratuit, consultez [Version d'évaluation gratuite](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="063fb-111">For a free trial, see [Free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="063fb-112">Un pool élastique.</span><span class="sxs-lookup"><span data-stu-id="063fb-112">An elastic pool.</span></span> <span data-ttu-id="063fb-113">Voir [À propos des pools élastiques](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="063fb-113">See [About elastic pools](sql-database-elastic-pool.md).</span></span>
* <span data-ttu-id="063fb-114">Installation des composants du service de tâches de bases de données élastiques.</span><span class="sxs-lookup"><span data-stu-id="063fb-114">Installation of elastic database job service components.</span></span> <span data-ttu-id="063fb-115">Consultez [installation du service de travail de base de données élastique hello](sql-database-elastic-jobs-service-installation.md).</span><span class="sxs-lookup"><span data-stu-id="063fb-115">See [Installing hello elastic database job service](sql-database-elastic-jobs-service-installation.md).</span></span>

## <a name="creating-jobs"></a><span data-ttu-id="063fb-116">Création de travaux</span><span class="sxs-lookup"><span data-stu-id="063fb-116">Creating jobs</span></span>
1. <span data-ttu-id="063fb-117">À l’aide de hello [portail Azure](https://portal.azure.com), à partir d’un pool de travail élastique de base de données existant, cliquez sur **travail de création de**.</span><span class="sxs-lookup"><span data-stu-id="063fb-117">Using hello [Azure portal](https://portal.azure.com), from an existing elastic database job pool, click **Create job**.</span></span>
2. <span data-ttu-id="063fb-118">Tapez dans le nom d’utilisateur hello et un mot de passe d’administrateur de base de données hello (créé à l’installation de travaux) de base de données de contrôle hello travaux (stockage des métadonnées pour les travaux).</span><span class="sxs-lookup"><span data-stu-id="063fb-118">Type in hello username and password of hello database administrator (created at installation of Jobs) for hello jobs control database (metadata storage for jobs).</span></span>
   
    ![Nom du travail hello, tapez ou collez dans le code, puis cliquez sur Exécuter][1]
3. <span data-ttu-id="063fb-120">Bonjour **créer une tâche** panneau, tapez un nom pour le travail de hello.</span><span class="sxs-lookup"><span data-stu-id="063fb-120">In hello **Create Job** blade, type a name for hello job.</span></span>
4. <span data-ttu-id="063fb-121">Tapez hello nom et mot de passe tooconnect toohello cible bases de données utilisateur disposant d’autorisations suffisantes pour toosucceed de l’exécution du script.</span><span class="sxs-lookup"><span data-stu-id="063fb-121">Type hello user name and password tooconnect toohello target databases with sufficient permissions for script execution toosucceed.</span></span>
5. <span data-ttu-id="063fb-122">Collez ou tapez dans le script de hello T-SQL.</span><span class="sxs-lookup"><span data-stu-id="063fb-122">Paste or type in hello T-SQL script.</span></span>
6. <span data-ttu-id="063fb-123">Cliquez sur **Enregistrer**, puis sur **Exécuter**.</span><span class="sxs-lookup"><span data-stu-id="063fb-123">Click **Save** and then click **Run**.</span></span>
   
    ![Créez des tâches et exécutez-les.][5]

## <a name="run-idempotent-jobs"></a><span data-ttu-id="063fb-125">Exécution de tâches idempotent</span><span class="sxs-lookup"><span data-stu-id="063fb-125">Run idempotent jobs</span></span>
<span data-ttu-id="063fb-126">Lorsque vous exécutez un script sur un ensemble de bases de données, vous devez être sûr que le script de hello est idempotente.</span><span class="sxs-lookup"><span data-stu-id="063fb-126">When you run a script against a set of databases, you must be sure that hello script is idempotent.</span></span> <span data-ttu-id="063fb-127">Autrement dit, hello script doit être en mesure de toorun plusieurs fois, même si elle a échoué avant dans un état incomplet.</span><span class="sxs-lookup"><span data-stu-id="063fb-127">That is, hello script must be able toorun multiple times, even if it has failed before in an incomplete state.</span></span> <span data-ttu-id="063fb-128">Par exemple, lorsqu’un script échoue, le travail de hello sera automatiquement retentée jusqu'à ce qu’il réussisse (dans les limites, en tant que nouvelle tentative de hello logique finalement cessera hello une nouvelle tentative).</span><span class="sxs-lookup"><span data-stu-id="063fb-128">For example, when a script fails, hello job will be automatically retried until it succeeds (within limits, as hello retry logic will eventually cease hello retrying).</span></span> <span data-ttu-id="063fb-129">toodo de façon Hello est toouse hello une clause « IF EXISTS » et supprimez toute instance trouvée avant de créer un nouvel objet.</span><span class="sxs-lookup"><span data-stu-id="063fb-129">hello way toodo this is toouse hello an "IF EXISTS" clause and delete any found instance before creating a new object.</span></span> <span data-ttu-id="063fb-130">Voici un exemple :</span><span class="sxs-lookup"><span data-stu-id="063fb-130">An example is shown here:</span></span>

    IF EXISTS (SELECT name FROM sys.indexes
            WHERE name = N'IX_ProductVendor_VendorID')
    DROP INDEX IX_ProductVendor_VendorID ON Purchasing.ProductVendor;
    GO
    CREATE INDEX IX_ProductVendor_VendorID
    ON Purchasing.ProductVendor (VendorID);

<span data-ttu-id="063fb-131">Vous pouvez également utiliser une clause « IF NOT EXISTS » avant de créer une instance :</span><span class="sxs-lookup"><span data-stu-id="063fb-131">Alternatively, use an "IF NOT EXISTS" clause before creating a new instance:</span></span>

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

<span data-ttu-id="063fb-132">Ce script met ensuite à jour la table hello créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="063fb-132">This script then updates hello table created previously.</span></span>

    IF NOT EXISTS (SELECT columns.name FROM sys.columns INNER JOIN sys.tables on columns.object_id = tables.object_id WHERE tables.name = 'TestTable' AND columns.name = 'AdditionalInformation')
    BEGIN

    ALTER TABLE TestTable

    ADD AdditionalInformation NVARCHAR(400);
    END
    GO

    INSERT INTO TestTable(InsertionTime, AdditionalInformation) VALUES (sysutcdatetime(), 'test');
    GO


## <a name="checking-job-status"></a><span data-ttu-id="063fb-133">Vérification du statut de la tâche</span><span class="sxs-lookup"><span data-stu-id="063fb-133">Checking job status</span></span>
<span data-ttu-id="063fb-134">Une fois la tâche lancée, vous pouvez vérifier son statut.</span><span class="sxs-lookup"><span data-stu-id="063fb-134">After a job has begun, you can check on its progress.</span></span>

1. <span data-ttu-id="063fb-135">Dans la page de pool élastique hello, cliquez sur **gérer les travaux**.</span><span class="sxs-lookup"><span data-stu-id="063fb-135">From hello elastic pool page, click **Manage jobs**.</span></span>
   
    ![Cliquez sur « Gérer les tâches ».][2]
2. <span data-ttu-id="063fb-137">Cliquez sur hello nom (a) d’une tâche.</span><span class="sxs-lookup"><span data-stu-id="063fb-137">Click on hello name (a) of a job.</span></span> <span data-ttu-id="063fb-138">Hello **état** peut être « Completed » ou « Échec ».</span><span class="sxs-lookup"><span data-stu-id="063fb-138">hello **STATUS** can be "Completed" or "Failed."</span></span> <span data-ttu-id="063fb-139">Détails de la tâche Hello apparaissent (b) avec la date et l’heure de création et l’exécution.</span><span class="sxs-lookup"><span data-stu-id="063fb-139">hello job's details appear (b) with its date and time of creation and running.</span></span> <span data-ttu-id="063fb-140">liste de Hello (c) ci-dessous hello qui affiche la progression de hello du script hello sur chaque base de données dans le pool de hello, précisant la date et l’heure.</span><span class="sxs-lookup"><span data-stu-id="063fb-140">hello list (c) below hello that shows hello progress of hello script against each database in hello pool, giving its date and time details.</span></span>
   
    ![Vérification d'une tâche terminée][3]

## <a name="checking-failed-jobs"></a><span data-ttu-id="063fb-142">Vérification des tâches ayant échoué</span><span class="sxs-lookup"><span data-stu-id="063fb-142">Checking failed jobs</span></span>
<span data-ttu-id="063fb-143">Si une tâche échoue, un journal détaillant son exécution est créé.</span><span class="sxs-lookup"><span data-stu-id="063fb-143">If a job fails, a log of its execution can found.</span></span> <span data-ttu-id="063fb-144">Cliquez sur nom hello hello échoué de la tâche toosee ses détails.</span><span class="sxs-lookup"><span data-stu-id="063fb-144">Click hello name of hello failed job toosee its details.</span></span>

![Vérifier une tâche ayant échoué][4]

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-create-and-manage/screen-1.png
[2]: ./media/sql-database-elastic-jobs-create-and-manage/click-manage-jobs.png
[3]: ./media/sql-database-elastic-jobs-create-and-manage/running-jobs.png
[4]: ./media/sql-database-elastic-jobs-create-and-manage/failed.png
[5]: ./media/sql-database-elastic-jobs-create-and-manage/screen-2.png


