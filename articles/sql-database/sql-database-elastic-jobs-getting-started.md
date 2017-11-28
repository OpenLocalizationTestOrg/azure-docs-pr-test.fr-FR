---
title: "aaaGetting a démarré avec des tâches de base de données élastique | Documents Microsoft"
description: "comment les tâches de base de données élastique toouse"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
ms.assetid: 2540de0e-2235-4cdd-9b6a-b841adba00e5
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/06/2016
ms.author: ddove
ms.openlocfilehash: bc5894d2df4235738ab961db4f69c11cdf786cc6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-elastic-database-jobs"></a><span data-ttu-id="83e58-103">Prise en main de Tâches de bases de données élastiques</span><span class="sxs-lookup"><span data-stu-id="83e58-103">Getting started with Elastic Database jobs</span></span>
<span data-ttu-id="83e58-104">Travaux de base de données élastique (version préliminaire) pour base de données SQL Azure vous permet de tooreliability exécuter des scripts T-SQL qui s’étendent sur plusieurs bases de données lors de la tentative automatique et en fournissant son achèvement éventuel de garantie.</span><span class="sxs-lookup"><span data-stu-id="83e58-104">Elastic Database jobs (preview) for Azure SQL Database allows you tooreliability execute T-SQL scripts that span multiple databases while automatically retrying and providing eventual completion guarantees.</span></span> <span data-ttu-id="83e58-105">Pour plus d’informations sur la fonctionnalité de travail de base de données élastique hello, consultez hello [page de vue d’ensemble de fonctionnalités](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="83e58-105">For more information about hello Elastic Database job feature, please see hello [feature overview page](sql-database-elastic-jobs-overview.md).</span></span>

<span data-ttu-id="83e58-106">Cette rubrique étend l’exemple hello trouvé dans [prise en main des outils de base de données élastique](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="83e58-106">This topic extends hello sample found in [Getting started with Elastic Database tools](sql-database-elastic-scale-get-started.md).</span></span> <span data-ttu-id="83e58-107">Issue, vous allez : Découvrez comment toocreate et gérer les travaux de gérer un groupe de bases de données associées.</span><span class="sxs-lookup"><span data-stu-id="83e58-107">When completed, you will: learn how toocreate and manage jobs that manage a group of related databases.</span></span> <span data-ttu-id="83e58-108">Il n’est pas requis toouse hello élastique outils dans bénéficiant de tootake d’ordre de hello travaux élastique.</span><span class="sxs-lookup"><span data-stu-id="83e58-108">It is not required toouse hello Elastic Scale tools in order tootake advantage of hello benefits of Elastic jobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="83e58-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="83e58-109">Prerequisites</span></span>
<span data-ttu-id="83e58-110">Téléchargez et exécutez hello [mise en route avec l’exemple des outils de base de données élastique](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="83e58-110">Download and run hello [Getting started with Elastic Database tools sample](sql-database-elastic-scale-get-started.md).</span></span>

## <a name="create-a-shard-map-manager-using-hello-sample-app"></a><span data-ttu-id="83e58-111">Créer une carte de partitions manager à l’aide de hello, exemple d’application</span><span class="sxs-lookup"><span data-stu-id="83e58-111">Create a shard map manager using hello sample app</span></span>
<span data-ttu-id="83e58-112">Ici vous allez créer une carte de partitions manager ainsi que plusieurs partitions, suivie de l’insertion de données dans les partitions hello.</span><span class="sxs-lookup"><span data-stu-id="83e58-112">Here you will create a shard map manager along with several shards, followed by insertion of data into hello shards.</span></span> <span data-ttu-id="83e58-113">Si vous avez déjà configuré avec des données partitionnées de partitions, vous pouvez ignorer hello comme suit et déplacer la section suivante de toohello.</span><span class="sxs-lookup"><span data-stu-id="83e58-113">If you already have shards set up with sharded data in them, you can skip hello following steps and move toohello next section.</span></span>

1. <span data-ttu-id="83e58-114">Générez et exécutez hello **prise en main des outils de base de données élastique** exemple d’application.</span><span class="sxs-lookup"><span data-stu-id="83e58-114">Build and run hello **Getting started with Elastic Database tools** sample application.</span></span> <span data-ttu-id="83e58-115">Hello comme suit avant l’étape 7 de la section de hello [télécharger et exécuter l’exemple d’application hello](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app).</span><span class="sxs-lookup"><span data-stu-id="83e58-115">Follow hello steps until step 7 in hello section [Download and run hello sample app](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app).</span></span> <span data-ttu-id="83e58-116">Extrémité hello de l’étape 7, vous verrez hello après l’invite de commandes :</span><span class="sxs-lookup"><span data-stu-id="83e58-116">At hello end of Step 7, you will see hello following command prompt:</span></span>

   ![invite de commande](./media/sql-database-elastic-query-getting-started/cmd-prompt.png)

2. <span data-ttu-id="83e58-118">Dans la fenêtre de commande hello, tapez « 1 » et appuyez sur **entrée**.</span><span class="sxs-lookup"><span data-stu-id="83e58-118">In hello command window, type "1" and press **Enter**.</span></span> <span data-ttu-id="83e58-119">Cela crée le Gestionnaire de carte de partitions hello et ajoute le serveur de toohello deux partitions.</span><span class="sxs-lookup"><span data-stu-id="83e58-119">This creates hello shard map manager, and adds two shards toohello server.</span></span> <span data-ttu-id="83e58-120">Entrez « 3 », puis appuyez sur **Entrée**. Répétez cette action quatre fois.</span><span class="sxs-lookup"><span data-stu-id="83e58-120">Then type "3" and press **Enter**; repeat this action four times.</span></span> <span data-ttu-id="83e58-121">Cela permet d’insérer des lignes d’exemples de données dans vos partitions.</span><span class="sxs-lookup"><span data-stu-id="83e58-121">This inserts sample data rows in your shards.</span></span>
3. <span data-ttu-id="83e58-122">Hello [portail Azure](https://portal.azure.com) doit afficher trois nouvelles bases de données :</span><span class="sxs-lookup"><span data-stu-id="83e58-122">hello [Azure Portal](https://portal.azure.com) should show three new databases:</span></span>

   ![Confirmation Visual Studio](./media/sql-database-elastic-query-getting-started/portal.png)

   <span data-ttu-id="83e58-124">À ce stade, nous allons créer une collection de base de données personnalisée qui reflète toutes les bases de données hello dans la carte de partitions hello.</span><span class="sxs-lookup"><span data-stu-id="83e58-124">At this point, we will create a custom database collection that reflects all hello databases in hello shard map.</span></span> <span data-ttu-id="83e58-125">Cela nous permet toocreate et exécuter un travail qui ajouter une nouvelle table entre les partitions.</span><span class="sxs-lookup"><span data-stu-id="83e58-125">This will allow us toocreate and execute a job that add a new table across shards.</span></span>

<span data-ttu-id="83e58-126">Ici nous généralement créerait une cible de carte de partitions, à l’aide de hello **New-AzureSqlJobTarget** applet de commande.</span><span class="sxs-lookup"><span data-stu-id="83e58-126">Here we would usually create a shard map target, using hello **New-AzureSqlJobTarget** cmdlet.</span></span> <span data-ttu-id="83e58-127">base de données du gestionnaire Hello partition carte doit être défini en tant que base de données cible et ensuite la carte de partitions spécifiques de hello est spécifié en tant que cible.</span><span class="sxs-lookup"><span data-stu-id="83e58-127">hello shard map manager database must be set as a database target and then hello specific shard map is specified as a target.</span></span> <span data-ttu-id="83e58-128">Au lieu de cela, nous continu tooenumerate toutes les bases de données hello dans le serveur de hello et ajouter hello bases de données toohello nouveau regroupement personnalisé avec l’exception hello de base de données master.</span><span class="sxs-lookup"><span data-stu-id="83e58-128">Instead, we are going tooenumerate all hello databases in hello server and add hello databases toohello new custom collection with hello exception of master database.</span></span>

## <a name="creates-a-custom-collection-and-add-all-databases-in-hello-server-toohello-custom-collection-target-with-hello-exception-of-master"></a><span data-ttu-id="83e58-129">Crée une collection personnalisée et ajoutez toutes les bases de données dans la cible de collection personnalisée hello serveur toohello avec l’exception hello du maître.</span><span class="sxs-lookup"><span data-stu-id="83e58-129">Creates a custom collection and add all databases in hello server toohello custom collection target with hello exception of master.</span></span>
   ```
    $customCollectionName = "dbs_in_server"
    New-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $ResourceGroupName = "ddove_samples"
    $ServerName = "samples"
    $dbsinserver = Get-AzureRMSqlDatabase -ResourceGroupName $ResourceGroupName -ServerName $ServerName
    $dbsinserver | %{
    $currentdb = $_.DatabaseName
    $ErrorActionPreference = "Stop"
    Write-Output ""

    Try
    {
       New-AzureSqlJobTarget -ServerName $ServerName -DatabaseName $currentdb | Write-Output
    }
    Catch
    {
        $ErrorMessage = $_.Exception.Message
        $ErrorCategory = $_.CategoryInfo.Reason

        if ($ErrorCategory -eq 'UniqueConstraintViolatedException')
        {
             Write-Host $currentdb "is already a database target."
        }

        else
        {
            throw $_
        }

    }

    Try
    {
        if ($currentdb -eq "master")
        {
            Write-Host $currentdb "will not be added custom collection target" $CustomCollectionName "."
        }

        else
        {
            Add-AzureSqlJobChildTarget -CustomCollectionName $CustomCollectionName -ServerName $ServerName -DatabaseName $currentdb
            Write-Host $currentdb "was added to" $CustomCollectionName "."
        }

    }
    Catch
    {
        $ErrorMessage = $_.Exception.Message
        $ErrorCategory = $_.CategoryInfo.Reason

        if ($ErrorCategory -eq 'UniqueConstraintViolatedException')
        {
             Write-Host $currentdb "is already in hello custom collection target" $CustomCollectionName"."
        }

        else
        {
            throw $_
        }
    }
    $ErrorActionPreference = "Continue"
   }
   ```
## <a name="create-a-t-sql-script-for-execution-across-databases"></a><span data-ttu-id="83e58-130">Créez un script T-SQL pour l’exécuter sur des bases de données</span><span class="sxs-lookup"><span data-stu-id="83e58-130">Create a T-SQL Script for execution across databases</span></span>
   ```
    $scriptName = "NewTable"
    $scriptCommandText = "
    IF NOT EXISTS (SELECT name FROM sys.tables WHERE name = 'Test')
    BEGIN
        CREATE TABLE Test(
            TestId INT PRIMARY KEY IDENTITY,
            InsertionTime DATETIME2
        );
    END
    GO
    INSERT INTO Test(InsertionTime) VALUES (sysutcdatetime());
    GO"

    $script = New-AzureSqlJobContent -ContentName $scriptName -CommandText $scriptCommandText
    Write-Output $script
   ```

## <a name="create-hello-job-tooexecute-a-script-across-hello-custom-group-of-databases"></a><span data-ttu-id="83e58-131">Création d’un script hello travail tooexecute entre le groupe personnalisé de hello des bases de données</span><span class="sxs-lookup"><span data-stu-id="83e58-131">Create hello job tooexecute a script across hello custom group of databases</span></span>

   ```
    $jobName = "create on server dbs"
    $scriptName = "NewTable"
    $customCollectionName = "dbs_in_server"
    $credentialName = "ddove66"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job
   ```

## <a name="execute-hello-job"></a><span data-ttu-id="83e58-132">Exécuter le travail de hello</span><span class="sxs-lookup"><span data-stu-id="83e58-132">Execute hello job</span></span>
<span data-ttu-id="83e58-133">Hello PowerShell script suivant peut être utilisé tooexecute un travail existant :</span><span class="sxs-lookup"><span data-stu-id="83e58-133">hello following PowerShell script can be used tooexecute an existing job:</span></span>

<span data-ttu-id="83e58-134">Mettre à jour hello suivant tooreflect variable hello souhaité travail nom toohave exécutée :</span><span class="sxs-lookup"><span data-stu-id="83e58-134">Update hello following variable tooreflect hello desired job name toohave executed:</span></span>

   ```
    $jobName = "create on server dbs"
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName
    Write-Output $jobExecution
   ```

## <a name="retrieve-hello-state-of-a-single-job-execution"></a><span data-ttu-id="83e58-135">Récupérer l’état de l’exécution d’une seule tâche hello</span><span class="sxs-lookup"><span data-stu-id="83e58-135">Retrieve hello state of a single job execution</span></span>
<span data-ttu-id="83e58-136">Utilisez hello même **Get-AzureSqlJobExecution** applet de commande avec hello **IncludeChildren** état de hello tooview paramètre d’exécutions de travail enfant, hello à savoir un état spécifique pour chaque exécution du travail sur chaque base de données ciblée par le travail de hello.</span><span class="sxs-lookup"><span data-stu-id="83e58-136">Use hello same **Get-AzureSqlJobExecution** cmdlet with hello **IncludeChildren** parameter tooview hello state of child job executions, namely hello specific state for each job execution against each database targeted by hello job.</span></span>

   ```
    $jobExecutionId = "{Job Execution Id}"
    $jobExecutions = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId -IncludeChildren
    Write-Output $jobExecutions
   ```

## <a name="view-hello-state-across-multiple-job-executions"></a><span data-ttu-id="83e58-137">Afficher l’état hello sur plusieurs exécutions du travail</span><span class="sxs-lookup"><span data-stu-id="83e58-137">View hello state across multiple job executions</span></span>
<span data-ttu-id="83e58-138">Hello **Get-AzureSqlJobExecution** applet de commande a plusieurs paramètres facultatifs qui peuvent être utilisé toodisplay plusieurs exécutions du travail, filtrées par le biais des paramètres de hello fourni.</span><span class="sxs-lookup"><span data-stu-id="83e58-138">hello **Get-AzureSqlJobExecution** cmdlet has multiple optional parameters that can be used toodisplay multiple job executions, filtered through hello provided parameters.</span></span> <span data-ttu-id="83e58-139">suivant de Hello présente quelques-unes des façons possibles de hello toouse Get-AzureSqlJobExecution :</span><span class="sxs-lookup"><span data-stu-id="83e58-139">hello following demonstrates some of hello possible ways toouse Get-AzureSqlJobExecution:</span></span>

<span data-ttu-id="83e58-140">Récupérez toutes les exécutions de tâches de niveau supérieur actives :</span><span class="sxs-lookup"><span data-stu-id="83e58-140">Retrieve all active top level job executions:</span></span>

   ```
    Get-AzureSqlJobExecution
   ```

<span data-ttu-id="83e58-141">Récupérez toutes les exécutions de tâches de niveau supérieur, y compris les exécutions de tâches inactives :</span><span class="sxs-lookup"><span data-stu-id="83e58-141">Retrieve all top level job executions, including inactive job executions:</span></span>

   ```
    Get-AzureSqlJobExecution -IncludeInactive
   ```

<span data-ttu-id="83e58-142">Récupérez toutes les exécutions de tâches enfants d'un ID d'exécution de tâches fourni, y compris les exécutions de tâches inactives :</span><span class="sxs-lookup"><span data-stu-id="83e58-142">Retrieve all child job executions of a provided job execution ID, including inactive job executions:</span></span>

   ```
    $parentJobExecutionId = "{Job Execution Id}"
    Get-AzureSqlJobExecution -AzureSqlJobExecution -JobExecutionId $parentJobExecutionId -IncludeInactive -IncludeChildren
   ```

<span data-ttu-id="83e58-143">Récupérez toutes les exécutions de tâches créées à l'aide d'une planification/combinaison de tâches, y compris les tâches inactives :</span><span class="sxs-lookup"><span data-stu-id="83e58-143">Retrieve all job executions created using a schedule / job combination, including inactive jobs:</span></span>

   ```
    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Get-AzureSqlJobExecution -JobName $jobName -ScheduleName $scheduleName -IncludeInactive
   ```

<span data-ttu-id="83e58-144">Récupérez toutes les tâches ciblant une carte de partitions spécifiée, y compris les tâches inactives :</span><span class="sxs-lookup"><span data-stu-id="83e58-144">Retrieve all jobs targeting a specified shard map, including inactive jobs:</span></span>

   ```
    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $target = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive
   ```

<span data-ttu-id="83e58-145">Récupérez toutes les tâches ciblant une collecte personnalisée spécifiée, y compris les tâches inactives :</span><span class="sxs-lookup"><span data-stu-id="83e58-145">Retrieve all jobs targeting a specified custom collection, including inactive jobs:</span></span>

   ```
    $customCollectionName = "{Custom Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive
   ```

<span data-ttu-id="83e58-146">Récupérer la liste de hello d’exécutions de tâches de travail au sein de l’exécution d’une tâche spécifique :</span><span class="sxs-lookup"><span data-stu-id="83e58-146">Retrieve hello list of job task executions within a specific job execution:</span></span>

   ```
    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Write-Output $jobTaskExecutions
   ```

<span data-ttu-id="83e58-147">Récupérez les détails d’exécution de tâches de travail :</span><span class="sxs-lookup"><span data-stu-id="83e58-147">Retrieve job task execution details:</span></span>

<span data-ttu-id="83e58-148">Hello PowerShell script suivant peut être utilisé tooview les détails de hello une tâche d’exécution des tâches, qui est particulièrement utile lors du débogage des erreurs d’exécution.</span><span class="sxs-lookup"><span data-stu-id="83e58-148">hello following PowerShell script can be used tooview hello details of a job task execution, which is particularly useful when debugging execution failures.</span></span>
   ```
    $jobTaskExecutionId = "{Job Task Execution Id}"
    $jobTaskExecution = Get-AzureSqlJobTaskExecution -JobTaskExecutionId $jobTaskExecutionId
    Write-Output $jobTaskExecution
   ```

## <a name="retrieve-failures-within-job-task-executions"></a><span data-ttu-id="83e58-149">Récupérez des échecs dans les exécutions de tâches de travail</span><span class="sxs-lookup"><span data-stu-id="83e58-149">Retrieve failures within job task executions</span></span>
<span data-ttu-id="83e58-150">objet de JobTaskExecution Hello inclut une propriété pour hello du cycle de vie de la tâche hello avec une propriété de Message.</span><span class="sxs-lookup"><span data-stu-id="83e58-150">hello JobTaskExecution object includes a property for hello Lifecycle of hello task along with a Message property.</span></span> <span data-ttu-id="83e58-151">Si une exécution de tâches de travail a échoué, hello du cycle de vie propriété sera définie trop*n’a pas pu* et propriété de Message de salutation sera définie message d’exception résultant toohello et sa pile.</span><span class="sxs-lookup"><span data-stu-id="83e58-151">If a job task execution failed, hello Lifecycle property will be set too*Failed* and hello Message property will be set toohello resulting exception message and its stack.</span></span> <span data-ttu-id="83e58-152">Si une tâche n’a pas réussi, il est important tooview les détails de hello des tâches de travail qui n’a pas réussi pour un travail donné.</span><span class="sxs-lookup"><span data-stu-id="83e58-152">If a job did not succeed, it is important tooview hello details of job tasks that did not succeed for a given job.</span></span>

   ```
    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Foreach($jobTaskExecution in $jobTaskExecutions)
        {
        if($jobTaskExecution.Lifecycle -ne 'Succeeded')
            {
            Write-Output $jobTaskExecution
            }
        }
   ```

## <a name="waiting-for-a-job-execution-toocomplete"></a><span data-ttu-id="83e58-153">En attente pour un toocomplete de l’exécution du travail</span><span class="sxs-lookup"><span data-stu-id="83e58-153">Waiting for a job execution toocomplete</span></span>
<span data-ttu-id="83e58-154">Hello PowerShell script suivant peut être utilisé toowait pour un toocomplete de tâche de travail :</span><span class="sxs-lookup"><span data-stu-id="83e58-154">hello following PowerShell script can be used toowait for a job task toocomplete:</span></span>

   ```
    $jobExecutionId = "{Job Execution Id}"
    Wait-AzureSqlJobExecution -JobExecutionId $jobExecutionId
   ```

## <a name="create-a-custom-execution-policy"></a><span data-ttu-id="83e58-155">Créez une stratégie d'exécution personnalisée</span><span class="sxs-lookup"><span data-stu-id="83e58-155">Create a custom execution policy</span></span>
<span data-ttu-id="83e58-156">Tâches de bases de données prend en charge la création de stratégies d'exécution personnalisées qui peuvent être appliquées lors du démarrage des tâches.</span><span class="sxs-lookup"><span data-stu-id="83e58-156">Elastic Database jobs supports creating custom execution policies that can be applied when starting jobs.</span></span>

<span data-ttu-id="83e58-157">Les stratégies d'exécution permettent de définir :</span><span class="sxs-lookup"><span data-stu-id="83e58-157">Execution policies currently allow for defining:</span></span>

* <span data-ttu-id="83e58-158">Nom : L’identificateur de la stratégie d’exécution hello.</span><span class="sxs-lookup"><span data-stu-id="83e58-158">Name: Identifier for hello execution policy.</span></span>
* <span data-ttu-id="83e58-159">Délai d’attente de la tâche : délai avant l’annulation d’une tâche par Tâches de bases de données élastiques.</span><span class="sxs-lookup"><span data-stu-id="83e58-159">Job Timeout: Total time before a job will be canceled by Elastic Database Jobs.</span></span>
* <span data-ttu-id="83e58-160">Intervalle de nouvelle tentative initial : Toowait d’intervalle avant la première nouvelle tentative.</span><span class="sxs-lookup"><span data-stu-id="83e58-160">Initial Retry Interval: Interval toowait before first retry.</span></span>
* <span data-ttu-id="83e58-161">Intervalle maximal de tentatives : L’extrémité de toouse des intervalles de nouvelle tentative.</span><span class="sxs-lookup"><span data-stu-id="83e58-161">Maximum Retry Interval: Cap of retry intervals toouse.</span></span>
* <span data-ttu-id="83e58-162">Coefficient d’interruption d’intervalle de nouvelle tentative : Coefficient utilisé toocalculate hello prochain intervalle entre les nouvelles tentatives.</span><span class="sxs-lookup"><span data-stu-id="83e58-162">Retry Interval Backoff Coefficient: Coefficient used toocalculate hello next interval between retries.</span></span>  <span data-ttu-id="83e58-163">Hello formule suivante est utilisée : (intervalle avant nouvelle tentative initiale) * Math.pow (intervalle interruption Coefficient (), (nombre de tentatives de) - 2).</span><span class="sxs-lookup"><span data-stu-id="83e58-163">hello following formula is used: (Initial Retry Interval) * Math.pow((Interval Backoff Coefficient), (Number of Retries) - 2).</span></span>
* <span data-ttu-id="83e58-164">Nombre maximal de tentatives : hello nombre maximal de tooperform de tentatives de nouvelle tentative au sein d’un travail.</span><span class="sxs-lookup"><span data-stu-id="83e58-164">Maximum Attempts: hello maximum number of retry attempts tooperform within a job.</span></span>

<span data-ttu-id="83e58-165">stratégie d’exécution par défaut Hello utilise hello valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="83e58-165">hello default execution policy uses hello following values:</span></span>

* <span data-ttu-id="83e58-166">Le nom : la stratégie d'exécution par défaut</span><span class="sxs-lookup"><span data-stu-id="83e58-166">Name: Default execution policy</span></span>
* <span data-ttu-id="83e58-167">Délai d’attente de la tâche : 1 semaine</span><span class="sxs-lookup"><span data-stu-id="83e58-167">Job Timeout: 1 week</span></span>
* <span data-ttu-id="83e58-168">Intervalle avant nouvelle tentative initiale : 100 millisecondes</span><span class="sxs-lookup"><span data-stu-id="83e58-168">Initial Retry Interval:  100 milliseconds</span></span>
* <span data-ttu-id="83e58-169">Intervalle maximal avant nouvelle tentative : 30 minutes</span><span class="sxs-lookup"><span data-stu-id="83e58-169">Maximum Retry Interval: 30 minutes</span></span>
* <span data-ttu-id="83e58-170">Coefficient de l'intervalle avant nouvelle tentative : 2</span><span class="sxs-lookup"><span data-stu-id="83e58-170">Retry Interval Coefficient: 2</span></span>
* <span data-ttu-id="83e58-171">Nombre maximal de tentatives : 2 147 483 647</span><span class="sxs-lookup"><span data-stu-id="83e58-171">Maximum Attempts: 2,147,483,647</span></span>

<span data-ttu-id="83e58-172">Créer la stratégie d’exécution hello souhaité :</span><span class="sxs-lookup"><span data-stu-id="83e58-172">Create hello desired execution policy:</span></span>

   ```
    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 10
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $executionPolicy = New-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $executionPolicy
   ```

### <a name="update-a-custom-execution-policy"></a><span data-ttu-id="83e58-173">Mettez à jour une stratégie d'exécution personnalisée</span><span class="sxs-lookup"><span data-stu-id="83e58-173">Update a custom execution policy</span></span>
<span data-ttu-id="83e58-174">Hello de mise à jour souhaitée tooupdate de stratégie d’exécution :</span><span class="sxs-lookup"><span data-stu-id="83e58-174">Update hello desired execution policy tooupdate:</span></span>

   ```
    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 15
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $updatedExecutionPolicy = Set-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $updatedExecutionPolicy
   ```

## <a name="cancel-a-job"></a><span data-ttu-id="83e58-175">Annulation d’une tâche</span><span class="sxs-lookup"><span data-stu-id="83e58-175">Cancel a job</span></span>
<span data-ttu-id="83e58-176">La fonctionnalité Tâches de bases de données élastiques prend en charge les demandes d’annulation de tâches.</span><span class="sxs-lookup"><span data-stu-id="83e58-176">Elastic Database Jobs supports jobs cancellation requests.</span></span>  <span data-ttu-id="83e58-177">Si les travaux de base de données élastique détecte une demande d’annulation d’une tâche en cours d’exécution, il tentera de travail de hello toostop.</span><span class="sxs-lookup"><span data-stu-id="83e58-177">If Elastic Database Jobs detects a cancellation request for a job currently being executed, it will attempt toostop hello job.</span></span>

<span data-ttu-id="83e58-178">La fonctionnalité Tâches de bases de données élastiques peut effectuer une annulation de deux manières différentes :</span><span class="sxs-lookup"><span data-stu-id="83e58-178">There are two different ways that Elastic Database Jobs can perform a cancellation:</span></span>

1. <span data-ttu-id="83e58-179">L’annulation en cours d’exécution des tâches : si une annulation est détectée pendant une tâche est en cours d’exécution, l’annulation sera tentée dans hello aspect de la tâche hello en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="83e58-179">Canceling Currently Executing Tasks: If a cancellation is detected while a task is currently running, a cancellation will be attempted within hello currently executing aspect of hello task.</span></span>  <span data-ttu-id="83e58-180">Par exemple : en l’absence d’une requête longue en cours d’exécution lorsqu’une annulation est tentée, il y aura une requête de hello toocancel tentative.</span><span class="sxs-lookup"><span data-stu-id="83e58-180">For example: If there is a long running query currently being performed when a cancellation is attempted, there will be an attempt toocancel hello query.</span></span>
2. <span data-ttu-id="83e58-181">Nouvelles tentatives annulation de tâche : Si une annulation est détectée par le thread de contrôle hello avant de lancer une tâche pour l’exécution, thread de contrôle hello éviter de lancer la tâche hello et déclarer la demande de hello comme annulée.</span><span class="sxs-lookup"><span data-stu-id="83e58-181">Canceling Task Retries: If a cancellation is detected by hello control thread before a task is launched for execution, hello control thread will avoid launching hello task and declare hello request as canceled.</span></span>

<span data-ttu-id="83e58-182">Si une annulation de tâche est demandée pour un travail parent, demande d’annulation hello sera respectée pour la tâche parente de hello et pour toutes ses tâches enfants.</span><span class="sxs-lookup"><span data-stu-id="83e58-182">If a job cancellation is requested for a parent job, hello cancellation request will be honored for hello parent job and for all of its child jobs.</span></span>

<span data-ttu-id="83e58-183">toosubmit une demande d’annulation, utilisez hello **Stop-AzureSqlJobExecution** applet de commande et ensemble hello **JobExecutionId** paramètre.</span><span class="sxs-lookup"><span data-stu-id="83e58-183">toosubmit a cancellation request, use hello **Stop-AzureSqlJobExecution** cmdlet and set hello **JobExecutionId** parameter.</span></span>

   ```
    $jobExecutionId = "{Job Execution Id}"
    Stop-AzureSqlJobExecution -JobExecutionId $jobExecutionId
   ```

## <a name="delete-a-job-by-name-and-hello-jobs-history"></a><span data-ttu-id="83e58-184">Supprimer un travail par nom et l’historique du travail hello</span><span class="sxs-lookup"><span data-stu-id="83e58-184">Delete a job by name and hello job's history</span></span>
<span data-ttu-id="83e58-185">Tâches de bases de données élastiques prend en charge la suppression des tâches asynchrone.</span><span class="sxs-lookup"><span data-stu-id="83e58-185">Elastic Database jobs supports asynchronous deletion of jobs.</span></span> <span data-ttu-id="83e58-186">Un travail peut être marqué pour suppression et hello système supprime le travail de hello et son historique une fois que toutes les exécutions de la tâche s’est terminé pour le travail de hello.</span><span class="sxs-lookup"><span data-stu-id="83e58-186">A job can be marked for deletion and hello system will delete hello job and all its job history after all job executions have completed for hello job.</span></span> <span data-ttu-id="83e58-187">système de Hello n’est pas automatiquement annulé exécutions de travail actif.</span><span class="sxs-lookup"><span data-stu-id="83e58-187">hello system will not automatically cancel active job executions.</span></span>  

<span data-ttu-id="83e58-188">Au lieu de cela, Stop-AzureSqlJobExecution doit être appelée toocancel les exécutions de travail actif.</span><span class="sxs-lookup"><span data-stu-id="83e58-188">Instead, Stop-AzureSqlJobExecution must be invoked toocancel active job executions.</span></span>

<span data-ttu-id="83e58-189">suppression du travail tootrigger, utilisez hello **Remove-AzureSqlJob** applet de commande et ensemble hello **JobName** paramètre.</span><span class="sxs-lookup"><span data-stu-id="83e58-189">tootrigger job deletion, use hello **Remove-AzureSqlJob** cmdlet and set hello **JobName** parameter.</span></span>

   ```
    $jobName = "{Job Name}"
    Remove-AzureSqlJob -JobName $jobName
   ```

## <a name="create-a-custom-database-target"></a><span data-ttu-id="83e58-190">Création d’une cible de base de données personnalisée</span><span class="sxs-lookup"><span data-stu-id="83e58-190">Create a custom database target</span></span>
<span data-ttu-id="83e58-191">Les cibles de base de données personnalisées peuvent être définies dans Tâches de bases de données élastiques, qui peut être utilisé directement pour l'exécution ou l’inclusion dans un groupe de base de données personnalisé.</span><span class="sxs-lookup"><span data-stu-id="83e58-191">Custom database targets can be defined in Elastic Database jobs which can be used either for execution directly or for inclusion within a custom database group.</span></span> <span data-ttu-id="83e58-192">Étant donné que **pools élastiques** sont pas encore directement pris en charge via hello APIs PowerShell, vous créez simplement une cible de la base de données personnalisée et la cible de collection de base de données personnalisée qui englobe toutes les bases de données hello dans le pool de hello.</span><span class="sxs-lookup"><span data-stu-id="83e58-192">Since **elastic pools** are not yet directly supported via hello PowerShell APIs, you simply create a custom database target and custom database collection target which encompasses all hello databases in hello pool.</span></span>

<span data-ttu-id="83e58-193">Définissez hello suit les informations de base de données de variables tooreflect hello souhaité :</span><span class="sxs-lookup"><span data-stu-id="83e58-193">Set hello following variables tooreflect hello desired database information:</span></span>

   ```
    $databaseName = "{Database Name}"
    $databaseServerName = "{Server Name}"
    New-AzureSqlJobDatabaseTarget -DatabaseName $databaseName -ServerName $databaseServerName
   ```

## <a name="create-a-custom-database-collection-target"></a><span data-ttu-id="83e58-194">Créez une cible de collecte de base de données personnalisée</span><span class="sxs-lookup"><span data-stu-id="83e58-194">Create a custom database collection target</span></span>
<span data-ttu-id="83e58-195">Une cible de collection de base de données personnalisée peut être l’exécution de tooenable définie sur plusieurs cibles de base de données.</span><span class="sxs-lookup"><span data-stu-id="83e58-195">A custom database collection target can be defined tooenable execution across multiple defined database targets.</span></span> <span data-ttu-id="83e58-196">Après la création d’un groupe de la base de données, les bases de données peuvent être cible de collection personnalisée toohello associé.</span><span class="sxs-lookup"><span data-stu-id="83e58-196">After a database group is created, databases can be associated toohello custom collection target.</span></span>

<span data-ttu-id="83e58-197">Définissez hello variables tooreflect hello collection personnalisée souhaitée cible configuration suivante :</span><span class="sxs-lookup"><span data-stu-id="83e58-197">Set hello following variables tooreflect hello desired custom collection target configuration:</span></span>

   ```
    $customCollectionName = "{Custom Database Collection Name}"
    New-AzureSqlJobTarget -CustomCollectionName $customCollectionName
   ```

### <a name="add-databases-tooa-custom-database-collection-target"></a><span data-ttu-id="83e58-198">Ajouter la cible de collecte des bases de données tooa base de données personnalisée</span><span class="sxs-lookup"><span data-stu-id="83e58-198">Add databases tooa custom database collection target</span></span>
<span data-ttu-id="83e58-199">Cibles de la base de données peuvent être associés à la base de données personnalisée collection cibles toocreate un groupe de bases de données.</span><span class="sxs-lookup"><span data-stu-id="83e58-199">Database targets can be associated with custom database collection targets toocreate a group of databases.</span></span> <span data-ttu-id="83e58-200">Chaque fois qu’un travail est créé qui pointe vers une cible de collection de base de données personnalisée, il sera groupe toohello associé de développé tootarget hello bases de données au moment de l’exécution de hello.</span><span class="sxs-lookup"><span data-stu-id="83e58-200">Whenever a job is created that targets a custom database collection target, it will be expanded tootarget hello databases associated toohello group at hello time of execution.</span></span>

<span data-ttu-id="83e58-201">Ajouter la collecte personnalisée spécifique de base de données tooa hello souhaité :</span><span class="sxs-lookup"><span data-stu-id="83e58-201">Add hello desired database tooa specific custom collection:</span></span>

   ```
    $serverName = "{Database Server Name}"
    $databaseName = "{Database Name}"
    $customCollectionName = "{Custom Database Collection Name}"
    Add-AzureSqlJobChildTarget -CustomCollectionName $customCollectionName -DatabaseName $databaseName -ServerName $databaseServerName
   ```

#### <a name="review-hello-databases-within-a-custom-database-collection-target"></a><span data-ttu-id="83e58-202">Passez en revue les bases de données hello dans une cible de collection de base de données personnalisée</span><span class="sxs-lookup"><span data-stu-id="83e58-202">Review hello databases within a custom database collection target</span></span>
<span data-ttu-id="83e58-203">Hello d’utilisation **Get-AzureSqlJobTarget** applet de commande tooretrieve hello enfant bases de données d’une cible de collection de base de données personnalisée.</span><span class="sxs-lookup"><span data-stu-id="83e58-203">Use hello **Get-AzureSqlJobTarget** cmdlet tooretrieve hello child databases within a custom database collection target.</span></span>

   ```
    $customCollectionName = "{Custom Database Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $childTargets = Get-AzureSqlJobTarget -ParentTargetId $target.TargetId
    Write-Output $childTargets
   ```

### <a name="create-a-job-tooexecute-a-script-across-a-custom-database-collection-target"></a><span data-ttu-id="83e58-204">Créer un travail tooexecute un script sur une cible de collection personnalisé de la base de données</span><span class="sxs-lookup"><span data-stu-id="83e58-204">Create a job tooexecute a script across a custom database collection target</span></span>
<span data-ttu-id="83e58-205">Hello d’utilisation **New-AzureSqlJob** toocreate de l’applet de commande un travail par rapport à un groupe de bases de données définies par une cible de collection de base de données personnalisée.</span><span class="sxs-lookup"><span data-stu-id="83e58-205">Use hello **New-AzureSqlJob** cmdlet toocreate a job against a group of databases defined by a custom database collection target.</span></span> <span data-ttu-id="83e58-206">Les travaux de base de données élastiques développera les travaux hello en plusieurs tâches enfants chaque base de données tooa correspondante associée cible de collecte de base de données personnalisée hello et assurez-vous que le script de hello est exécutée sur chaque base de données.</span><span class="sxs-lookup"><span data-stu-id="83e58-206">Elastic Database jobs will expand hello job into multiple child jobs each corresponding tooa database associated with hello custom database collection target and ensure that hello script is executed against each database.</span></span> <span data-ttu-id="83e58-207">Là encore, il est important que les scripts sont tooretries résilient de toobe idempotent.</span><span class="sxs-lookup"><span data-stu-id="83e58-207">Again, it is important that scripts are idempotent toobe resilient tooretries.</span></span>

   ```
    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $customCollectionName = "{Custom Collection Name}"
    $credentialName = "{Credential Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job
   ```

## <a name="data-collection-across-databases"></a><span data-ttu-id="83e58-208">Collecte de données sur les bases de données</span><span class="sxs-lookup"><span data-stu-id="83e58-208">Data collection across databases</span></span>
<span data-ttu-id="83e58-209">**Les travaux de base de données élastiques** prend en charge l’exécution d’une requête sur un groupe de bases de données et envoie les table hello résultats tooa spécifié de base de données.</span><span class="sxs-lookup"><span data-stu-id="83e58-209">**Elastic Database jobs** supports executing a query across a group of databases and sends hello results tooa specified database’s table.</span></span> <span data-ttu-id="83e58-210">table de Hello peut être interrogée après les résultats de la requête hello hello faits toosee à partir de chaque base de données.</span><span class="sxs-lookup"><span data-stu-id="83e58-210">hello table can be queried after hello fact toosee hello query’s results from each database.</span></span> <span data-ttu-id="83e58-211">Cela fournit un tooexecute mécanisme asynchrone d’une requête entre plusieurs bases de données.</span><span class="sxs-lookup"><span data-stu-id="83e58-211">This provides an asynchronous mechanism tooexecute a query across many databases.</span></span> <span data-ttu-id="83e58-212">Cas d’échec comme l’une des bases de données hello est temporairement indisponible sont gérées automatiquement par nouvelles tentatives.</span><span class="sxs-lookup"><span data-stu-id="83e58-212">Failure cases such as one of hello databases being temporarily unavailable are handled automatically via retries.</span></span>

<span data-ttu-id="83e58-213">table de destination spécifiée Hello sera automatiquement créée si elle n’existe pas encore, schéma hello correspondant de hello retourné de jeu de résultats.</span><span class="sxs-lookup"><span data-stu-id="83e58-213">hello specified destination table will be automatically created if it does not yet exist, matching hello schema of hello returned result set.</span></span> <span data-ttu-id="83e58-214">Si l’exécution du script retourne plusieurs jeux de résultats, les tâches de base de données élastique n’envoie hello première table de destination un toohello fourni.</span><span class="sxs-lookup"><span data-stu-id="83e58-214">If a script execution returns multiple result sets, Elastic Database jobs will only send hello first one toohello provided destination table.</span></span>

<span data-ttu-id="83e58-215">Hello PowerShell script suivant peut être utilisé tooexecute un script qui collecte ses résultats dans une table spécifiée.</span><span class="sxs-lookup"><span data-stu-id="83e58-215">hello following PowerShell script can be used tooexecute a script collecting its results into a specified table.</span></span> <span data-ttu-id="83e58-216">Ce script part du principe qu'un script T-SQL, qui génère un jeu de résultats unique, et une cible de collecte de base de données personnalisée ont été créés.</span><span class="sxs-lookup"><span data-stu-id="83e58-216">This script assumes that a T-SQL script has been created which outputs a single result set and a custom database collection target has been created.</span></span>

<span data-ttu-id="83e58-217">Hello ensemble suivant tooreflect hello souhaitée script, informations d’identification et la cible de l’exécution :</span><span class="sxs-lookup"><span data-stu-id="83e58-217">Set hello following tooreflect hello desired script, credentials, and execution target:</span></span>

   ```
    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $executionCredentialName = "{Execution Credential Name}"
    $customCollectionName = "{Custom Collection Name}"
    $destinationCredentialName = "{Destination Credential Name}"
    $destinationServerName = "{Destination Server Name}"
    $destinationDatabaseName = "{Destination Database Name}"
    $destinationSchemaName = "{Destination Schema Name}"
    $destinationTableName = "{Destination Table Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
   ```

### <a name="create-and-start-a-job-for-data-collection-scenarios"></a><span data-ttu-id="83e58-218">Créez et démarrez une tâche pour les scénarios de collecte de données</span><span class="sxs-lookup"><span data-stu-id="83e58-218">Create and start a job for data collection scenarios</span></span>
   ```
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $executionCredentialName -ContentName $scriptName -ResultSetDestinationServerName $destinationServerName -ResultSetDestinationDatabaseName $destinationDatabaseName -ResultSetDestinationSchemaName $destinationSchemaName -ResultSetDestinationTableName $destinationTableName -ResultSetDestinationCredentialName $destinationCredentialName -TargetId $target.TargetId
    Write-Output $job
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName
    Write-Output $jobExecution
   ```

## <a name="create-a-schedule-for-job-execution-using-a-job-trigger"></a><span data-ttu-id="83e58-219">Créez une planification pour l'exécution de tâches à l'aide d'un déclencheur de tâches</span><span class="sxs-lookup"><span data-stu-id="83e58-219">Create a schedule for job execution using a job trigger</span></span>
<span data-ttu-id="83e58-220">Hello PowerShell script suivant peut être utilisé toocreate un calendrier récurrent.</span><span class="sxs-lookup"><span data-stu-id="83e58-220">hello following PowerShell script can be used toocreate a reoccurring schedule.</span></span> <span data-ttu-id="83e58-221">Ce script utilise un intervalle d’une minute, mais New-AzureSqlJobSchedule prend également en charge les paramètres -DayInterval, - HourInterval, - MonthInterval et - WeekInterval.</span><span class="sxs-lookup"><span data-stu-id="83e58-221">This script uses a one minute interval, but New-AzureSqlJobSchedule also supports -DayInterval, -HourInterval, -MonthInterval, and -WeekInterval parameters.</span></span> <span data-ttu-id="83e58-222">Les planifications qui ne s'exécutent qu'une seule fois peuvent être créées en transmettant  - OneTime.</span><span class="sxs-lookup"><span data-stu-id="83e58-222">Schedules that execute only once can be created by passing -OneTime.</span></span>

<span data-ttu-id="83e58-223">Créez une nouvelle planification :</span><span class="sxs-lookup"><span data-stu-id="83e58-223">Create a new schedule:</span></span>
   ```
    $scheduleName = "Every one minute"
    $minuteInterval = 1
    $startTime = (Get-Date).ToUniversalTime()
    $schedule = New-AzureSqlJobSchedule -MinuteInterval $minuteInterval -ScheduleName $scheduleName -StartTime $startTime
    Write-Output $schedule
   ```

### <a name="create-a-job-trigger-toohave-a-job-executed-on-a-time-schedule"></a><span data-ttu-id="83e58-224">Créer un toohave de déclencheur de tâche à une tâche s’exécutée selon une planification</span><span class="sxs-lookup"><span data-stu-id="83e58-224">Create a job trigger toohave a job executed on a time schedule</span></span>
<span data-ttu-id="83e58-225">Un déclencheur de tâche peut être défini toohave un travail exécuté conformément tooa Calendrier.</span><span class="sxs-lookup"><span data-stu-id="83e58-225">A job trigger can be defined toohave a job executed according tooa time schedule.</span></span> <span data-ttu-id="83e58-226">Hello PowerShell script suivant peut être utilisé toocreate un déclencheur de tâche.</span><span class="sxs-lookup"><span data-stu-id="83e58-226">hello following PowerShell script can be used toocreate a job trigger.</span></span>

<span data-ttu-id="83e58-227">Hello ensemble suivant de variables toocorrespond toohello souhaitée de travail et une planification :</span><span class="sxs-lookup"><span data-stu-id="83e58-227">Set hello following variables toocorrespond toohello desired job and schedule:</span></span>

   ```
    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    $jobTrigger = New-AzureSqlJobTrigger -ScheduleName $scheduleName -JobName $jobName
    Write-Output $jobTrigger
   ```

### <a name="remove-a-scheduled-association-toostop-job-from-executing-on-schedule"></a><span data-ttu-id="83e58-228">Supprimer une tâche de toostop association planifiée l’exécution de la planification</span><span class="sxs-lookup"><span data-stu-id="83e58-228">Remove a scheduled association toostop job from executing on schedule</span></span>
<span data-ttu-id="83e58-229">toodiscontinue qui se reproduit l’exécution du travail via un déclencheur de tâche, le déclencheur de tâche hello peut être supprimée.</span><span class="sxs-lookup"><span data-stu-id="83e58-229">toodiscontinue reoccurring job execution through a job trigger, hello job trigger can be removed.</span></span>
<span data-ttu-id="83e58-230">Supprimer un toostop de déclencheur de tâche un travail à partir d’en cours d’exécution en fonction tooa planification, à l’aide de hello **Remove-AzureSqlJobTrigger** applet de commande.</span><span class="sxs-lookup"><span data-stu-id="83e58-230">Remove a job trigger toostop a job from being executed according tooa schedule using hello **Remove-AzureSqlJobTrigger** cmdlet.</span></span>

   ```
    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Remove-AzureSqlJobTrigger -ScheduleName $scheduleName -JobName $jobName
   ```

## <a name="import-elastic-database-query-results-tooexcel"></a><span data-ttu-id="83e58-231">Importer tooExcel de résultats de requête de base de données élastique</span><span class="sxs-lookup"><span data-stu-id="83e58-231">Import elastic database query results tooExcel</span></span>
 <span data-ttu-id="83e58-232">Vous pouvez importer les résultats hello à partir d’un fichier Excel de tooan requête.</span><span class="sxs-lookup"><span data-stu-id="83e58-232">You can import hello results from of a query tooan Excel file.</span></span>

1. <span data-ttu-id="83e58-233">Lancez Excel 2013.</span><span class="sxs-lookup"><span data-stu-id="83e58-233">Launch Excel 2013.</span></span>
2. <span data-ttu-id="83e58-234">Accédez toohello **données** ruban.</span><span class="sxs-lookup"><span data-stu-id="83e58-234">Navigate toohello **Data** ribbon.</span></span>
3. <span data-ttu-id="83e58-235">Cliquez sur **À partir d’autres sources** et sur **À partir de SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="83e58-235">Click **From Other Sources** and click **From SQL Server**.</span></span>

   ![Importation au format Excel à partir d’autres sources](./media/sql-database-elastic-query-getting-started/exel-sources.png)

4. <span data-ttu-id="83e58-237">Bonjour **Assistant connexion de données** tapez hello des informations d’identification nom et la connexion de serveur.</span><span class="sxs-lookup"><span data-stu-id="83e58-237">In hello **Data Connection Wizard** type hello server name and login credentials.</span></span> <span data-ttu-id="83e58-238">Cliquez ensuite sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="83e58-238">Then click **Next**.</span></span>
5. <span data-ttu-id="83e58-239">Dans la boîte de dialogue hello **base de données hello Select qui contient les données hello**, sélectionnez hello **ElasticDBQuery** base de données.</span><span class="sxs-lookup"><span data-stu-id="83e58-239">In hello dialog box **Select hello database that contains hello data you want**, select hello **ElasticDBQuery** database.</span></span>
6. <span data-ttu-id="83e58-240">Sélectionnez hello **clients** de table dans la vue de liste hello et cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="83e58-240">Select hello **Customers** table in hello list view and click **Next**.</span></span> <span data-ttu-id="83e58-241">Puis, cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="83e58-241">Then click **Finish**.</span></span>
7. <span data-ttu-id="83e58-242">Bonjour **importer des données** formulaire sous **Choisissez comment vous voulez que tooview ces données dans votre classeur**, sélectionnez **Table** et cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="83e58-242">In hello **Import Data** form, under **Select how you want tooview this data in your workbook**, select **Table** and click **OK**.</span></span>

<span data-ttu-id="83e58-243">Tous les hello des lignes à partir de **clients** table, stockée dans des partitions différentes remplir la feuille de calcul Excel hello.</span><span class="sxs-lookup"><span data-stu-id="83e58-243">All hello rows from **Customers** table, stored in different shards populate hello Excel sheet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="83e58-244">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="83e58-244">Next steps</span></span>
<span data-ttu-id="83e58-245">Vous pouvez maintenant utiliser les fonctions de données Excel.</span><span class="sxs-lookup"><span data-stu-id="83e58-245">You can now use Excel’s data functions.</span></span> <span data-ttu-id="83e58-246">Utilisez la chaîne de connexion hello avec le nom de votre serveur, nom de la base de données et les informations d’identification tooconnect votre BI et données intégration outils toohello requête élastique de base de données.</span><span class="sxs-lookup"><span data-stu-id="83e58-246">Use hello connection string with your server name, database name and credentials tooconnect your BI and data integration tools toohello elastic query database.</span></span> <span data-ttu-id="83e58-247">Assurez-vous que SQL Server est pris en charge comme source de données pour votre outil.</span><span class="sxs-lookup"><span data-stu-id="83e58-247">Make sure that SQL Server is supported as a data source for your tool.</span></span> <span data-ttu-id="83e58-248">Consultez la base de données de requête élastique toohello et des tables externes comme toute autre base de données SQL Server et des tables SQL Server que vous devez vous connecter toowith votre outil.</span><span class="sxs-lookup"><span data-stu-id="83e58-248">Refer toohello elastic query database and external tables just like any other SQL Server database and SQL Server tables that you would connect toowith your tool.</span></span>

### <a name="cost"></a><span data-ttu-id="83e58-249">Coût</span><span class="sxs-lookup"><span data-stu-id="83e58-249">Cost</span></span>
<span data-ttu-id="83e58-250">Il n’existe aucun frais supplémentaire pour à l’aide de la fonctionnalité de requête de base de données élastique hello.</span><span class="sxs-lookup"><span data-stu-id="83e58-250">There is no additional charge for using hello Elastic Database query feature.</span></span> <span data-ttu-id="83e58-251">Toutefois, pour l’instant cette fonctionnalité est disponible uniquement sur les bases de données premium, comme un point de terminaison, les partitions hello peuvent être de n’importe quel niveau de service.</span><span class="sxs-lookup"><span data-stu-id="83e58-251">However, at this time this feature is available only on premium databases as an end point, but hello shards can be of any service tier.</span></span>

<span data-ttu-id="83e58-252">Pour plus d’informations sur la tarification, consultez la page [Tarification - Base de données SQL](https://azure.microsoft.com/pricing/details/sql-database/).</span><span class="sxs-lookup"><span data-stu-id="83e58-252">For pricing information see [SQL Database Pricing Details](https://azure.microsoft.com/pricing/details/sql-database/).</span></span>

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-query-getting-started/cmd-prompt.png
[2]: ./media/sql-database-elastic-query-getting-started/portal.png
[3]: ./media/sql-database-elastic-query-getting-started/tiers.png
[4]: ./media/sql-database-elastic-query-getting-started/details.png
[5]: ./media/sql-database-elastic-query-getting-started/exel-sources.png
<!--anchors-->
