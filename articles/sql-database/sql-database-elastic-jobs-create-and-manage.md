---
title: "Gérer des groupes de bases de données Azure SQL | Microsoft Docs"
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
ms.openlocfilehash: d30cc74778e0b36dd632c2f040ce80d1ca8af5a5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-scaled-out-azure-sql-databases-using-elastic-jobs-preview"></a><span data-ttu-id="ea9bc-103">Créer et gérer des bases de données SQL Azure avec montée en charge à l’aide de tâches élastiques (version préliminaire)</span><span class="sxs-lookup"><span data-stu-id="ea9bc-103">Create and manage scaled out Azure SQL Databases using elastic jobs (preview)</span></span>


<span data-ttu-id="ea9bc-104">**tâches de bases de données élastiques** simplifient la gestion des groupes de bases de données en exécutant des opérations administratives telles que les modifications de schéma, la gestion des informations d’identification, les mises à jour de données de référence, la collecte des données de performances ou la collecte de données de télémétrie du locataire (client).</span><span class="sxs-lookup"><span data-stu-id="ea9bc-104">**Elastic Database jobs** simplify management of groups of databases by executing administrative operations such as schema changes, credentials management, reference data updates, performance data collection or tenant (customer) telemetry collection.</span></span> <span data-ttu-id="ea9bc-105">Tâches de bases de données élastiques est actuellement disponible via le portail Azure et les applets de commande PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ea9bc-105">Elastic Database jobs is currently available through the Azure portal and PowerShell cmdlets.</span></span> <span data-ttu-id="ea9bc-106">Le Portail Azure propose toutefois une fonctionnalité réduite, qui se limite à une exécution sur toutes les bases de données d’un [pool élastique (version préliminaire)](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="ea9bc-106">However, the Azure portal surfaces reduced functionality limited to execution across all databases in an [elastic pool (preview)](sql-database-elastic-pool.md).</span></span> <span data-ttu-id="ea9bc-107">Pour accéder à des fonctionnalités supplémentaires et à l’exécution des scripts sur un groupe de bases de données, notamment une collection personnalisée ou un ensemble de partitions (créé à l’aide de la [bibliothèque cliente de la base de données élastique](sql-database-elastic-scale-introduction.md)), consultez l’article [Créer et gérer des tâches avec PowerShell](sql-database-elastic-jobs-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="ea9bc-107">To access additional features and execution of scripts across a group of databases including a custom-defined collection or a shard set (created using [Elastic Database client library](sql-database-elastic-scale-introduction.md)), see [Creating and managing jobs using PowerShell](sql-database-elastic-jobs-powershell.md).</span></span> <span data-ttu-id="ea9bc-108">Pour en savoir plus sur les tâches, consultez la rubrique [Vue d'ensemble des tâches de bases de données élastiques](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ea9bc-108">For more information about jobs, see [Elastic Database jobs overview](sql-database-elastic-jobs-overview.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="ea9bc-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="ea9bc-109">Prerequisites</span></span>
* <span data-ttu-id="ea9bc-110">Un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="ea9bc-110">An Azure subscription.</span></span> <span data-ttu-id="ea9bc-111">Pour un essai gratuit, consultez [Version d'évaluation gratuite](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ea9bc-111">For a free trial, see [Free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="ea9bc-112">Un pool élastique.</span><span class="sxs-lookup"><span data-stu-id="ea9bc-112">An elastic pool.</span></span> <span data-ttu-id="ea9bc-113">Voir [À propos des pools élastiques](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="ea9bc-113">See [About elastic pools](sql-database-elastic-pool.md).</span></span>
* <span data-ttu-id="ea9bc-114">Installation des composants du service de tâches de bases de données élastiques.</span><span class="sxs-lookup"><span data-stu-id="ea9bc-114">Installation of elastic database job service components.</span></span> <span data-ttu-id="ea9bc-115">Voir [Installation du service de tâches de bases de données élastiques](sql-database-elastic-jobs-service-installation.md).</span><span class="sxs-lookup"><span data-stu-id="ea9bc-115">See [Installing the elastic database job service](sql-database-elastic-jobs-service-installation.md).</span></span>

## <a name="creating-jobs"></a><span data-ttu-id="ea9bc-116">Création de travaux</span><span class="sxs-lookup"><span data-stu-id="ea9bc-116">Creating jobs</span></span>
1. <span data-ttu-id="ea9bc-117">À l'aide du [portail Azure](https://portal.azure.com), à partir d'un pool élastique de tâches de bases de données existant, cliquez sur **Créer une tâche**.</span><span class="sxs-lookup"><span data-stu-id="ea9bc-117">Using the [Azure portal](https://portal.azure.com), from an existing elastic database job pool, click **Create job**.</span></span>
2. <span data-ttu-id="ea9bc-118">Tapez le nom d’utilisateur et le mot de passe de l’administrateur (créé à l’installation de Jobs) de la base de données de contrôle des tâches (stockage des métadonnées pour les tâches).</span><span class="sxs-lookup"><span data-stu-id="ea9bc-118">Type in the username and password of the database administrator (created at installation of Jobs) for the jobs control database (metadata storage for jobs).</span></span>
   
    ![Nommez la tâche, saisissez ou collez le code puis cliquez sur Exécuter][1]
3. <span data-ttu-id="ea9bc-120">Dans le volet **Créer une tâche** , nommez la tâche.</span><span class="sxs-lookup"><span data-stu-id="ea9bc-120">In the **Create Job** blade, type a name for the job.</span></span>
4. <span data-ttu-id="ea9bc-121">Tapez le nom d’utilisateur et le mot de passe pour vous connecter aux bases de données cibles avec les autorisations suffisantes pour l’exécution du script.</span><span class="sxs-lookup"><span data-stu-id="ea9bc-121">Type the user name and password to connect to the target databases with sufficient permissions for script execution to succeed.</span></span>
5. <span data-ttu-id="ea9bc-122">Collez ou saisissez le script T-SQL.</span><span class="sxs-lookup"><span data-stu-id="ea9bc-122">Paste or type in the T-SQL script.</span></span>
6. <span data-ttu-id="ea9bc-123">Cliquez sur **Enregistrer**, puis sur **Exécuter**.</span><span class="sxs-lookup"><span data-stu-id="ea9bc-123">Click **Save** and then click **Run**.</span></span>
   
    ![Créez des tâches et exécutez-les.][5]

## <a name="run-idempotent-jobs"></a><span data-ttu-id="ea9bc-125">Exécution de tâches idempotent</span><span class="sxs-lookup"><span data-stu-id="ea9bc-125">Run idempotent jobs</span></span>
<span data-ttu-id="ea9bc-126">Lorsque vous exécutez un script sur un ensemble de bases de données, vous devez être sûr que le script est idempotent.</span><span class="sxs-lookup"><span data-stu-id="ea9bc-126">When you run a script against a set of databases, you must be sure that the script is idempotent.</span></span> <span data-ttu-id="ea9bc-127">Autrement dit, le script doit pouvoir être exécuté plusieurs fois, même s'il a échoué avec un état incomplet auparavant.</span><span class="sxs-lookup"><span data-stu-id="ea9bc-127">That is, the script must be able to run multiple times, even if it has failed before in an incomplete state.</span></span> <span data-ttu-id="ea9bc-128">Par exemple, lorsqu'un script échoue, la tâche sera automatiquement relancée jusqu'à ce qu'elle  aboutisse (jusqu'à une certaine limite car la logique de relance finira par s'arrêter).</span><span class="sxs-lookup"><span data-stu-id="ea9bc-128">For example, when a script fails, the job will be automatically retried until it succeeds (within limits, as the retry logic will eventually cease the retrying).</span></span> <span data-ttu-id="ea9bc-129">La solution consiste à utiliser la clause « IF EXISTS » et à supprimer toutes les instances trouvées avant de créer un objet.</span><span class="sxs-lookup"><span data-stu-id="ea9bc-129">The way to do this is to use the an "IF EXISTS" clause and delete any found instance before creating a new object.</span></span> <span data-ttu-id="ea9bc-130">Voici un exemple :</span><span class="sxs-lookup"><span data-stu-id="ea9bc-130">An example is shown here:</span></span>

    IF EXISTS (SELECT name FROM sys.indexes
            WHERE name = N'IX_ProductVendor_VendorID')
    DROP INDEX IX_ProductVendor_VendorID ON Purchasing.ProductVendor;
    GO
    CREATE INDEX IX_ProductVendor_VendorID
    ON Purchasing.ProductVendor (VendorID);

<span data-ttu-id="ea9bc-131">Vous pouvez également utiliser une clause « IF NOT EXISTS » avant de créer une instance :</span><span class="sxs-lookup"><span data-stu-id="ea9bc-131">Alternatively, use an "IF NOT EXISTS" clause before creating a new instance:</span></span>

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

<span data-ttu-id="ea9bc-132">ce script met alors à jour la table créée précédemment.</span><span class="sxs-lookup"><span data-stu-id="ea9bc-132">This script then updates the table created previously.</span></span>

    IF NOT EXISTS (SELECT columns.name FROM sys.columns INNER JOIN sys.tables on columns.object_id = tables.object_id WHERE tables.name = 'TestTable' AND columns.name = 'AdditionalInformation')
    BEGIN

    ALTER TABLE TestTable

    ADD AdditionalInformation NVARCHAR(400);
    END
    GO

    INSERT INTO TestTable(InsertionTime, AdditionalInformation) VALUES (sysutcdatetime(), 'test');
    GO


## <a name="checking-job-status"></a><span data-ttu-id="ea9bc-133">Vérification du statut de la tâche</span><span class="sxs-lookup"><span data-stu-id="ea9bc-133">Checking job status</span></span>
<span data-ttu-id="ea9bc-134">Une fois la tâche lancée, vous pouvez vérifier son statut.</span><span class="sxs-lookup"><span data-stu-id="ea9bc-134">After a job has begun, you can check on its progress.</span></span>

1. <span data-ttu-id="ea9bc-135">Sur la page du pool élastique, cliquez sur **Gérer les travaux**.</span><span class="sxs-lookup"><span data-stu-id="ea9bc-135">From the elastic pool page, click **Manage jobs**.</span></span>
   
    ![Cliquez sur « Gérer les tâches ».][2]
2. <span data-ttu-id="ea9bc-137">Cliquez sur le nom (a) d'une tâche.</span><span class="sxs-lookup"><span data-stu-id="ea9bc-137">Click on the name (a) of a job.</span></span> <span data-ttu-id="ea9bc-138">Le champ **STATUS** peut afficher la valeur « Completed » (Terminé) ou « Failed » (Échec).</span><span class="sxs-lookup"><span data-stu-id="ea9bc-138">The **STATUS** can be "Completed" or "Failed."</span></span> <span data-ttu-id="ea9bc-139">Les détails de la tâche (b) incluent la date et l'heure de création et d'exécution.</span><span class="sxs-lookup"><span data-stu-id="ea9bc-139">The job's details appear (b) with its date and time of creation and running.</span></span> <span data-ttu-id="ea9bc-140">La liste (c) ci-dessous indique la progression du script sur chaque base de données du pool, en précisant la date et l'heure.</span><span class="sxs-lookup"><span data-stu-id="ea9bc-140">The list (c) below the that shows the progress of the script against each database in the pool, giving its date and time details.</span></span>
   
    ![Vérification d'une tâche terminée][3]

## <a name="checking-failed-jobs"></a><span data-ttu-id="ea9bc-142">Vérification des tâches ayant échoué</span><span class="sxs-lookup"><span data-stu-id="ea9bc-142">Checking failed jobs</span></span>
<span data-ttu-id="ea9bc-143">Si une tâche échoue, un journal détaillant son exécution est créé.</span><span class="sxs-lookup"><span data-stu-id="ea9bc-143">If a job fails, a log of its execution can found.</span></span> <span data-ttu-id="ea9bc-144">Cliquez sur le nom de la tâche ayant échoué pour afficher ses détails.</span><span class="sxs-lookup"><span data-stu-id="ea9bc-144">Click the name of the failed job to see its details.</span></span>

![Vérifier une tâche ayant échoué][4]

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-create-and-manage/screen-1.png
[2]: ./media/sql-database-elastic-jobs-create-and-manage/click-manage-jobs.png
[3]: ./media/sql-database-elastic-jobs-create-and-manage/running-jobs.png
[4]: ./media/sql-database-elastic-jobs-create-and-manage/failed.png
[5]: ./media/sql-database-elastic-jobs-create-and-manage/screen-2.png


