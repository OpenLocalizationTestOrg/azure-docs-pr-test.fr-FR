---
title: "Prise en main des tâches de base de données élastiques | Microsoft Docs"
description: "Utilisation des tâches de bases de données élastiques"
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
ms.openlocfilehash: 05c20e880d4eb1eacdecc0c4c7e7491dfe1e6a89
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-elastic-database-jobs"></a><span data-ttu-id="dcf4e-103">Prise en main de Tâches de bases de données élastiques</span><span class="sxs-lookup"><span data-stu-id="dcf4e-103">Getting started with Elastic Database jobs</span></span>
<span data-ttu-id="dcf4e-104">Tâches de bases de données élastiques (version préliminaire) pour la base de données SQL Azure vous permet d’exécuter, de manière efficace, des scripts T-SQL qui s'étendent sur plusieurs bases de données, tout en apportant automatiquement de nouvelles tentatives et des garanties d’achèvement éventuel.</span><span class="sxs-lookup"><span data-stu-id="dcf4e-104">Elastic Database jobs (preview) for Azure SQL Database allows you to reliability execute T-SQL scripts that span multiple databases while automatically retrying and providing eventual completion guarantees.</span></span> <span data-ttu-id="dcf4e-105">Pour plus d’informations sur la fonctionnalité Tâches de bases de données élastiques, veuillez consulter la [page de vue d’ensemble des fonctionnalités](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="dcf4e-105">For more information about the Elastic Database job feature, please see the [feature overview page](sql-database-elastic-jobs-overview.md).</span></span>

<span data-ttu-id="dcf4e-106">Cette rubrique étend l’exemple de la rubrique [Prise en main des outils de base de données élastique](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="dcf4e-106">This topic extends the sample found in [Getting started with Elastic Database tools](sql-database-elastic-scale-get-started.md).</span></span> <span data-ttu-id="dcf4e-107">Une fois l’opération terminée, vous apprendrez à créer et à gérer des tâches qui gèrent un groupe de bases de données associées.</span><span class="sxs-lookup"><span data-stu-id="dcf4e-107">When completed, you will: learn how to create and manage jobs that manage a group of related databases.</span></span> <span data-ttu-id="dcf4e-108">Il n’est pas nécessaire d’utiliser les outils de mise à l’échelle élastique pour tirer parti des avantages des tâches élastiques.</span><span class="sxs-lookup"><span data-stu-id="dcf4e-108">It is not required to use the Elastic Scale tools in order to take advantage of the benefits of Elastic jobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dcf4e-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="dcf4e-109">Prerequisites</span></span>
<span data-ttu-id="dcf4e-110">Téléchargez et exécutez l’exemple de la rubrique [Prise en main des outils de base de données élastique](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="dcf4e-110">Download and run the [Getting started with Elastic Database tools sample](sql-database-elastic-scale-get-started.md).</span></span>

## <a name="create-a-shard-map-manager-using-the-sample-app"></a><span data-ttu-id="dcf4e-111">Créez un gestionnaire des cartes de partitions à l’aide de l’exemple d’application</span><span class="sxs-lookup"><span data-stu-id="dcf4e-111">Create a shard map manager using the sample app</span></span>
<span data-ttu-id="dcf4e-112">Ici vous allez créer un gestionnaire des cartes de partitions avec plusieurs partitions, puis insérer des données dans les partitions.</span><span class="sxs-lookup"><span data-stu-id="dcf4e-112">Here you will create a shard map manager along with several shards, followed by insertion of data into the shards.</span></span> <span data-ttu-id="dcf4e-113">Si vos partitions comportent déjà des données partitionnées, vous pouvez ignorer ces étapes et passer à la section suivante.</span><span class="sxs-lookup"><span data-stu-id="dcf4e-113">If you already have shards set up with sharded data in them, you can skip the following steps and move to the next section.</span></span>

1. <span data-ttu-id="dcf4e-114">Créez et exécutez l’exemple d’application de la rubrique **Prise en main des outils de base de données élastique** .</span><span class="sxs-lookup"><span data-stu-id="dcf4e-114">Build and run the **Getting started with Elastic Database tools** sample application.</span></span> <span data-ttu-id="dcf4e-115">Suivez la procédure jusqu’à l’étape 7 dans la section [Télécharger et exécuter l’exemple d’application](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app).</span><span class="sxs-lookup"><span data-stu-id="dcf4e-115">Follow the steps until step 7 in the section [Download and run the sample app](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app).</span></span> <span data-ttu-id="dcf4e-116">À la fin de l’étape 7, vous verrez l’invite de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="dcf4e-116">At the end of Step 7, you will see the following command prompt:</span></span>

   ![invite de commande](./media/sql-database-elastic-query-getting-started/cmd-prompt.png)

2. <span data-ttu-id="dcf4e-118">Dans la fenêtre de commande, entrez « 1 » et appuyez sur **Entrée**.</span><span class="sxs-lookup"><span data-stu-id="dcf4e-118">In the command window, type "1" and press **Enter**.</span></span> <span data-ttu-id="dcf4e-119">Cela crée le gestionnaire des cartes de partitions et ajoute deux partitions sur le serveur.</span><span class="sxs-lookup"><span data-stu-id="dcf4e-119">This creates the shard map manager, and adds two shards to the server.</span></span> <span data-ttu-id="dcf4e-120">Entrez « 3 », puis appuyez sur **Entrée**. Répétez cette action quatre fois.</span><span class="sxs-lookup"><span data-stu-id="dcf4e-120">Then type "3" and press **Enter**; repeat this action four times.</span></span> <span data-ttu-id="dcf4e-121">Cela permet d’insérer des lignes d’exemples de données dans vos partitions.</span><span class="sxs-lookup"><span data-stu-id="dcf4e-121">This inserts sample data rows in your shards.</span></span>
3. <span data-ttu-id="dcf4e-122">Le [portail Azure](https://portal.azure.com) doit alors montrer trois nouvelles bases de données :</span><span class="sxs-lookup"><span data-stu-id="dcf4e-122">The [Azure Portal](https://portal.azure.com) should show three new databases:</span></span>

   ![Confirmation Visual Studio](./media/sql-database-elastic-query-getting-started/portal.png)

   <span data-ttu-id="dcf4e-124">À ce stade, nous créerons une collecte de base de données personnalisée qui reflétera toutes les bases de données dans la carte de partitions.</span><span class="sxs-lookup"><span data-stu-id="dcf4e-124">At this point, we will create a custom database collection that reflects all the databases in the shard map.</span></span> <span data-ttu-id="dcf4e-125">Ceci nous permettra de créer et d’exécuter une tâche qui ajoutera une nouvelle table aux partitions.</span><span class="sxs-lookup"><span data-stu-id="dcf4e-125">This will allow us to create and execute a job that add a new table across shards.</span></span>

<span data-ttu-id="dcf4e-126">Dans ce cas précis, nous créons généralement une cible de carte de partitions, à l’aide de l’applet de commande **New-AzureSqlJobTarget** .</span><span class="sxs-lookup"><span data-stu-id="dcf4e-126">Here we would usually create a shard map target, using the **New-AzureSqlJobTarget** cmdlet.</span></span> <span data-ttu-id="dcf4e-127">La base de données du gestionnaire de cartes de partitions doit être définie en tant que base de données cible et la carte de partitions spécifique doit être spécifiée en tant que cible.</span><span class="sxs-lookup"><span data-stu-id="dcf4e-127">The shard map manager database must be set as a database target and then the specific shard map is specified as a target.</span></span> <span data-ttu-id="dcf4e-128">Au lieu de cela, nous énumérerons toutes les bases de données du serveur et nous ajouterons les bases de données à la nouvelle collecte personnalisée, à l'exception de la base de données principale.</span><span class="sxs-lookup"><span data-stu-id="dcf4e-128">Instead, we are going to enumerate all the databases in the server and add the databases to the new custom collection with the exception of master database.</span></span>

## <a name="creates-a-custom-collection-and-add-all-databases-in-the-server-to-the-custom-collection-target-with-the-exception-of-master"></a><span data-ttu-id="dcf4e-129">Crée une collecte personnalisée et ajoute toutes les bases de données du serveur à la cible de la collecte personnalisée, à l’exception de la base de données principale.</span><span class="sxs-lookup"><span data-stu-id="dcf4e-129">Creates a custom collection and add all databases in the server to the custom collection target with the exception of master.</span></span>
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
             Write-Host $currentdb "is already in the custom collection target" $CustomCollectionName"."
        }

        else
        {
            throw $_
        }
    }
    $ErrorActionPreference = "Continue"
   }
   ```
## <a name="create-a-t-sql-script-for-execution-across-databases"></a><span data-ttu-id="dcf4e-130">Créez un script T-SQL pour l’exécuter sur des bases de données</span><span class="sxs-lookup"><span data-stu-id="dcf4e-130">Create a T-SQL Script for execution across databases</span></span>
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

## <a name="create-the-job-to-execute-a-script-across-the-custom-group-of-databases"></a><span data-ttu-id="dcf4e-131">Créez la tâche pour exécuter un script sur le groupe de bases de données personnalisé</span><span class="sxs-lookup"><span data-stu-id="dcf4e-131">Create the job to execute a script across the custom group of databases</span></span>

   ```
    $jobName = "create on server dbs"
    $scriptName = "NewTable"
    $customCollectionName = "dbs_in_server"
    $credentialName = "ddove66"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job
   ```

## <a name="execute-the-job"></a><span data-ttu-id="dcf4e-132">Exécutez la tâche</span><span class="sxs-lookup"><span data-stu-id="dcf4e-132">Execute the job</span></span>
<span data-ttu-id="dcf4e-133">Le script PowerShell suivant peut être utilisé pour exécuter une tâche existante :</span><span class="sxs-lookup"><span data-stu-id="dcf4e-133">The following PowerShell script can be used to execute an existing job:</span></span>

<span data-ttu-id="dcf4e-134">Mettez à jour la variable suivante pour refléter le nom de la tâche souhaitée à exécuter :</span><span class="sxs-lookup"><span data-stu-id="dcf4e-134">Update the following variable to reflect the desired job name to have executed:</span></span>

   ```
    $jobName = "create on server dbs"
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName
    Write-Output $jobExecution
   ```

## <a name="retrieve-the-state-of-a-single-job-execution"></a><span data-ttu-id="dcf4e-135">Récupérez l'état de l'exécution d'une tâche unique</span><span class="sxs-lookup"><span data-stu-id="dcf4e-135">Retrieve the state of a single job execution</span></span>
<span data-ttu-id="dcf4e-136">Utilisez la même applet de commande **Get-AzureSqlJobExecution** avec le paramètre **IncludeChildren** pour afficher l’état de l’exécution des tâches enfants, à savoir l’état spécifique à chaque exécution de tâche sur chaque base de données ciblée par la tâche.</span><span class="sxs-lookup"><span data-stu-id="dcf4e-136">Use the same **Get-AzureSqlJobExecution** cmdlet with the **IncludeChildren** parameter to view the state of child job executions, namely the specific state for each job execution against each database targeted by the job.</span></span>

   ```
    $jobExecutionId = "{Job Execution Id}"
    $jobExecutions = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId -IncludeChildren
    Write-Output $jobExecutions
   ```

## <a name="view-the-state-across-multiple-job-executions"></a><span data-ttu-id="dcf4e-137">Afficher l’état sur plusieurs exécutions de tâches</span><span class="sxs-lookup"><span data-stu-id="dcf4e-137">View the state across multiple job executions</span></span>
<span data-ttu-id="dcf4e-138">L’applet de commande **Get-AzureSqlJobExecution** dispose de plusieurs paramètres facultatifs qui peuvent être utilisés pour afficher plusieurs exécutions de tâches, filtrées selon les paramètres fournis.</span><span class="sxs-lookup"><span data-stu-id="dcf4e-138">The **Get-AzureSqlJobExecution** cmdlet has multiple optional parameters that can be used to display multiple job executions, filtered through the provided parameters.</span></span> <span data-ttu-id="dcf4e-139">L'exemple suivant présente certaines façons d'utiliser Get-AzureSqlJobExecution :</span><span class="sxs-lookup"><span data-stu-id="dcf4e-139">The following demonstrates some of the possible ways to use Get-AzureSqlJobExecution:</span></span>

<span data-ttu-id="dcf4e-140">Récupérez toutes les exécutions de tâches de niveau supérieur actives :</span><span class="sxs-lookup"><span data-stu-id="dcf4e-140">Retrieve all active top level job executions:</span></span>

   ```
    Get-AzureSqlJobExecution
   ```

<span data-ttu-id="dcf4e-141">Récupérez toutes les exécutions de tâches de niveau supérieur, y compris les exécutions de tâches inactives :</span><span class="sxs-lookup"><span data-stu-id="dcf4e-141">Retrieve all top level job executions, including inactive job executions:</span></span>

   ```
    Get-AzureSqlJobExecution -IncludeInactive
   ```

<span data-ttu-id="dcf4e-142">Récupérez toutes les exécutions de tâches enfants d'un ID d'exécution de tâches fourni, y compris les exécutions de tâches inactives :</span><span class="sxs-lookup"><span data-stu-id="dcf4e-142">Retrieve all child job executions of a provided job execution ID, including inactive job executions:</span></span>

   ```
    $parentJobExecutionId = "{Job Execution Id}"
    Get-AzureSqlJobExecution -AzureSqlJobExecution -JobExecutionId $parentJobExecutionId -IncludeInactive -IncludeChildren
   ```

<span data-ttu-id="dcf4e-143">Récupérez toutes les exécutions de tâches créées à l'aide d'une planification/combinaison de tâches, y compris les tâches inactives :</span><span class="sxs-lookup"><span data-stu-id="dcf4e-143">Retrieve all job executions created using a schedule / job combination, including inactive jobs:</span></span>

   ```
    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Get-AzureSqlJobExecution -JobName $jobName -ScheduleName $scheduleName -IncludeInactive
   ```

<span data-ttu-id="dcf4e-144">Récupérez toutes les tâches ciblant une carte de partitions spécifiée, y compris les tâches inactives :</span><span class="sxs-lookup"><span data-stu-id="dcf4e-144">Retrieve all jobs targeting a specified shard map, including inactive jobs:</span></span>

   ```
    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $target = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive
   ```

<span data-ttu-id="dcf4e-145">Récupérez toutes les tâches ciblant une collecte personnalisée spécifiée, y compris les tâches inactives :</span><span class="sxs-lookup"><span data-stu-id="dcf4e-145">Retrieve all jobs targeting a specified custom collection, including inactive jobs:</span></span>

   ```
    $customCollectionName = "{Custom Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive
   ```

<span data-ttu-id="dcf4e-146">Récupérez la liste des exécutions de tâches de travail dans l'exécution d'une tâche spécifique :</span><span class="sxs-lookup"><span data-stu-id="dcf4e-146">Retrieve the list of job task executions within a specific job execution:</span></span>

   ```
    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Write-Output $jobTaskExecutions
   ```

<span data-ttu-id="dcf4e-147">Récupérez les détails d’exécution de tâches de travail :</span><span class="sxs-lookup"><span data-stu-id="dcf4e-147">Retrieve job task execution details:</span></span>

<span data-ttu-id="dcf4e-148">Le script PowerShell suivant peut être utilisé pour afficher les détails d'une exécution de tâches de travail, qui est particulièrement utile lors du débogage des échecs d'exécution.</span><span class="sxs-lookup"><span data-stu-id="dcf4e-148">The following PowerShell script can be used to view the details of a job task execution, which is particularly useful when debugging execution failures.</span></span>
   ```
    $jobTaskExecutionId = "{Job Task Execution Id}"
    $jobTaskExecution = Get-AzureSqlJobTaskExecution -JobTaskExecutionId $jobTaskExecutionId
    Write-Output $jobTaskExecution
   ```

## <a name="retrieve-failures-within-job-task-executions"></a><span data-ttu-id="dcf4e-149">Récupérez des échecs dans les exécutions de tâches de travail</span><span class="sxs-lookup"><span data-stu-id="dcf4e-149">Retrieve failures within job task executions</span></span>
<span data-ttu-id="dcf4e-150">L'objet JobTaskExecution inclut une propriété pour le cycle de vie de la tâche, ainsi qu’une propriété Message.</span><span class="sxs-lookup"><span data-stu-id="dcf4e-150">The JobTaskExecution object includes a property for the Lifecycle of the task along with a Message property.</span></span> <span data-ttu-id="dcf4e-151">Si une exécution de tâches de travail a échoué, la propriété du cycle de vie est définie sur *Échec* et la propriété Message est définie sur le message d'exception résultant et sa pile.</span><span class="sxs-lookup"><span data-stu-id="dcf4e-151">If a job task execution failed, the Lifecycle property will be set to *Failed* and the Message property will be set to the resulting exception message and its stack.</span></span> <span data-ttu-id="dcf4e-152">Si une tâche a échoué, il est important d’afficher les détails des tâches de travail qui n'ont pas abouti pour une tâche donnée.</span><span class="sxs-lookup"><span data-stu-id="dcf4e-152">If a job did not succeed, it is important to view the details of job tasks that did not succeed for a given job.</span></span>

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

## <a name="waiting-for-a-job-execution-to-complete"></a><span data-ttu-id="dcf4e-153">En attente d’une exécution de tâche à effectuer</span><span class="sxs-lookup"><span data-stu-id="dcf4e-153">Waiting for a job execution to complete</span></span>
<span data-ttu-id="dcf4e-154">Le script PowerShell suivant peut être utilisé pour attendre l’exécution d’une tâche :</span><span class="sxs-lookup"><span data-stu-id="dcf4e-154">The following PowerShell script can be used to wait for a job task to complete:</span></span>

   ```
    $jobExecutionId = "{Job Execution Id}"
    Wait-AzureSqlJobExecution -JobExecutionId $jobExecutionId
   ```

## <a name="create-a-custom-execution-policy"></a><span data-ttu-id="dcf4e-155">Créez une stratégie d'exécution personnalisée</span><span class="sxs-lookup"><span data-stu-id="dcf4e-155">Create a custom execution policy</span></span>
<span data-ttu-id="dcf4e-156">Tâches de bases de données prend en charge la création de stratégies d'exécution personnalisées qui peuvent être appliquées lors du démarrage des tâches.</span><span class="sxs-lookup"><span data-stu-id="dcf4e-156">Elastic Database jobs supports creating custom execution policies that can be applied when starting jobs.</span></span>

<span data-ttu-id="dcf4e-157">Les stratégies d'exécution permettent de définir :</span><span class="sxs-lookup"><span data-stu-id="dcf4e-157">Execution policies currently allow for defining:</span></span>

* <span data-ttu-id="dcf4e-158">Le nom : l'identificateur de la stratégie d'exécution.</span><span class="sxs-lookup"><span data-stu-id="dcf4e-158">Name: Identifier for the execution policy.</span></span>
* <span data-ttu-id="dcf4e-159">Délai d’attente de la tâche : délai avant l’annulation d’une tâche par Tâches de bases de données élastiques.</span><span class="sxs-lookup"><span data-stu-id="dcf4e-159">Job Timeout: Total time before a job will be canceled by Elastic Database Jobs.</span></span>
* <span data-ttu-id="dcf4e-160">Intervalle avant nouvelle tentative initiale : l'intervalle d'attente avant la première nouvelle tentative.</span><span class="sxs-lookup"><span data-stu-id="dcf4e-160">Initial Retry Interval: Interval to wait before first retry.</span></span>
* <span data-ttu-id="dcf4e-161">Intervalle maximal avant nouvelle tentative : plafond des intervalles avant nouvelle tentative à utiliser.</span><span class="sxs-lookup"><span data-stu-id="dcf4e-161">Maximum Retry Interval: Cap of retry intervals to use.</span></span>
* <span data-ttu-id="dcf4e-162">Coefficient d'interruption de l’intervalle avant nouvelle tentative : ce coefficient permet de calculer le prochain intervalle entre les tentatives.</span><span class="sxs-lookup"><span data-stu-id="dcf4e-162">Retry Interval Backoff Coefficient: Coefficient used to calculate the next interval between retries.</span></span>  <span data-ttu-id="dcf4e-163">La formule suivante est utilisée : (intervalle avant nouvelle tentative initiale) * Math.pow (coefficient d’interruption de l’intervalle), (nombre de tentatives) - 2).</span><span class="sxs-lookup"><span data-stu-id="dcf4e-163">The following formula is used: (Initial Retry Interval) * Math.pow((Interval Backoff Coefficient), (Number of Retries) - 2).</span></span>
* <span data-ttu-id="dcf4e-164">Nombre maximal de tentatives : le nombre maximal de nouvelles tentatives effectuées dans une tâche.</span><span class="sxs-lookup"><span data-stu-id="dcf4e-164">Maximum Attempts: The maximum number of retry attempts to perform within a job.</span></span>

<span data-ttu-id="dcf4e-165">La stratégie d'exécution par défaut utilise les valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="dcf4e-165">The default execution policy uses the following values:</span></span>

* <span data-ttu-id="dcf4e-166">Le nom : la stratégie d'exécution par défaut</span><span class="sxs-lookup"><span data-stu-id="dcf4e-166">Name: Default execution policy</span></span>
* <span data-ttu-id="dcf4e-167">Délai d’attente de la tâche : 1 semaine</span><span class="sxs-lookup"><span data-stu-id="dcf4e-167">Job Timeout: 1 week</span></span>
* <span data-ttu-id="dcf4e-168">Intervalle avant nouvelle tentative initiale : 100 millisecondes</span><span class="sxs-lookup"><span data-stu-id="dcf4e-168">Initial Retry Interval:  100 milliseconds</span></span>
* <span data-ttu-id="dcf4e-169">Intervalle maximal avant nouvelle tentative : 30 minutes</span><span class="sxs-lookup"><span data-stu-id="dcf4e-169">Maximum Retry Interval: 30 minutes</span></span>
* <span data-ttu-id="dcf4e-170">Coefficient de l'intervalle avant nouvelle tentative : 2</span><span class="sxs-lookup"><span data-stu-id="dcf4e-170">Retry Interval Coefficient: 2</span></span>
* <span data-ttu-id="dcf4e-171">Nombre maximal de tentatives : 2 147 483 647</span><span class="sxs-lookup"><span data-stu-id="dcf4e-171">Maximum Attempts: 2,147,483,647</span></span>

<span data-ttu-id="dcf4e-172">Créez la stratégie d'exécution souhaitée :</span><span class="sxs-lookup"><span data-stu-id="dcf4e-172">Create the desired execution policy:</span></span>

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

### <a name="update-a-custom-execution-policy"></a><span data-ttu-id="dcf4e-173">Mettez à jour une stratégie d'exécution personnalisée</span><span class="sxs-lookup"><span data-stu-id="dcf4e-173">Update a custom execution policy</span></span>
<span data-ttu-id="dcf4e-174">Mettez à jour la stratégie d'exécution souhaitée :</span><span class="sxs-lookup"><span data-stu-id="dcf4e-174">Update the desired execution policy to update:</span></span>

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

## <a name="cancel-a-job"></a><span data-ttu-id="dcf4e-175">Annulation d’une tâche</span><span class="sxs-lookup"><span data-stu-id="dcf4e-175">Cancel a job</span></span>
<span data-ttu-id="dcf4e-176">La fonctionnalité Tâches de bases de données élastiques prend en charge les demandes d’annulation de tâches.</span><span class="sxs-lookup"><span data-stu-id="dcf4e-176">Elastic Database Jobs supports jobs cancellation requests.</span></span>  <span data-ttu-id="dcf4e-177">Si la fonctionnalité Tâches de bases de données élastiques détecte une demande d'annulation d'une tâche en cours d'exécution, il tente d'arrêter la tâche.</span><span class="sxs-lookup"><span data-stu-id="dcf4e-177">If Elastic Database Jobs detects a cancellation request for a job currently being executed, it will attempt to stop the job.</span></span>

<span data-ttu-id="dcf4e-178">La fonctionnalité Tâches de bases de données élastiques peut effectuer une annulation de deux manières différentes :</span><span class="sxs-lookup"><span data-stu-id="dcf4e-178">There are two different ways that Elastic Database Jobs can perform a cancellation:</span></span>

1. <span data-ttu-id="dcf4e-179">Annulation des tâches en cours d'exécution : si une annulation est détectée pendant qu’une tâche est en cours d'exécution, l'annulation sera tentée au sein de l'aspect de la tâche en cours d'exécution.</span><span class="sxs-lookup"><span data-stu-id="dcf4e-179">Canceling Currently Executing Tasks: If a cancellation is detected while a task is currently running, a cancellation will be attempted within the currently executing aspect of the task.</span></span>  <span data-ttu-id="dcf4e-180">Par exemple : si une requête de longue durée s’exécute lorsqu'une annulation est tentée, une tentative d'annulation de la requête sera effectuée.</span><span class="sxs-lookup"><span data-stu-id="dcf4e-180">For example: If there is a long running query currently being performed when a cancellation is attempted, there will be an attempt to cancel the query.</span></span>
2. <span data-ttu-id="dcf4e-181">Annulation des tentatives de tâches : si une annulation est détectée par le thread de contrôle avant de lancer l'exécution d'une tâche, le thread de contrôle permettra d’éviter le lancement de la tâche et de déclarer la requête comme étant annulée.</span><span class="sxs-lookup"><span data-stu-id="dcf4e-181">Canceling Task Retries: If a cancellation is detected by the control thread before a task is launched for execution, the control thread will avoid launching the task and declare the request as canceled.</span></span>

<span data-ttu-id="dcf4e-182">Si une annulation de tâche est demandée pour une tâche parente, la demande d'annulation sera respectée pour la tâche parente et toutes ses tâches enfants.</span><span class="sxs-lookup"><span data-stu-id="dcf4e-182">If a job cancellation is requested for a parent job, the cancellation request will be honored for the parent job and for all of its child jobs.</span></span>

<span data-ttu-id="dcf4e-183">Pour envoyer une demande d’annulation, utilisez l’applet de commande **Stop-AzureSqlJobExecution** et définissez le paramètre **JobExecutionId**.</span><span class="sxs-lookup"><span data-stu-id="dcf4e-183">To submit a cancellation request, use the **Stop-AzureSqlJobExecution** cmdlet and set the **JobExecutionId** parameter.</span></span>

   ```
    $jobExecutionId = "{Job Execution Id}"
    Stop-AzureSqlJobExecution -JobExecutionId $jobExecutionId
   ```

## <a name="delete-a-job-by-name-and-the-jobs-history"></a><span data-ttu-id="dcf4e-184">Supprimez une tâche via son nom et l'historique de la tâche</span><span class="sxs-lookup"><span data-stu-id="dcf4e-184">Delete a job by name and the job's history</span></span>
<span data-ttu-id="dcf4e-185">Tâches de bases de données élastiques prend en charge la suppression des tâches asynchrone.</span><span class="sxs-lookup"><span data-stu-id="dcf4e-185">Elastic Database jobs supports asynchronous deletion of jobs.</span></span> <span data-ttu-id="dcf4e-186">La suppression d’une tâche peut être signalée et le système supprime la tâche et son historique une fois que toutes les exécutions de tâches auront été effectuées.</span><span class="sxs-lookup"><span data-stu-id="dcf4e-186">A job can be marked for deletion and the system will delete the job and all its job history after all job executions have completed for the job.</span></span> <span data-ttu-id="dcf4e-187">Le système n'annule pas automatiquement les exécutions de tâches actives.</span><span class="sxs-lookup"><span data-stu-id="dcf4e-187">The system will not automatically cancel active job executions.</span></span>  

<span data-ttu-id="dcf4e-188">Au lieu de cela, Stop-AzureSqlJobExecution doit être appelé pour annuler les exécutions de tâches actives.</span><span class="sxs-lookup"><span data-stu-id="dcf4e-188">Instead, Stop-AzureSqlJobExecution must be invoked to cancel active job executions.</span></span>

<span data-ttu-id="dcf4e-189">Pour déclencher la suppression de tâches, utilisez l’applet de commande **Remove-AzureSqlJob** et définissez le paramètre **JobName**.</span><span class="sxs-lookup"><span data-stu-id="dcf4e-189">To trigger job deletion, use the **Remove-AzureSqlJob** cmdlet and set the **JobName** parameter.</span></span>

   ```
    $jobName = "{Job Name}"
    Remove-AzureSqlJob -JobName $jobName
   ```

## <a name="create-a-custom-database-target"></a><span data-ttu-id="dcf4e-190">Création d’une cible de base de données personnalisée</span><span class="sxs-lookup"><span data-stu-id="dcf4e-190">Create a custom database target</span></span>
<span data-ttu-id="dcf4e-191">Les cibles de base de données personnalisées peuvent être définies dans Tâches de bases de données élastiques, qui peut être utilisé directement pour l'exécution ou l’inclusion dans un groupe de base de données personnalisé.</span><span class="sxs-lookup"><span data-stu-id="dcf4e-191">Custom database targets can be defined in Elastic Database jobs which can be used either for execution directly or for inclusion within a custom database group.</span></span> <span data-ttu-id="dcf4e-192">Dans la mesure où les **pools élastiques** ne sont pas encore pris en charge directement via les API PowerShell, vous créez simplement une cible de base de données personnalisée et une cible de collecte de base de données personnalisée qui englobe toutes les bases de données dans le pool.</span><span class="sxs-lookup"><span data-stu-id="dcf4e-192">Since **elastic pools** are not yet directly supported via the PowerShell APIs, you simply create a custom database target and custom database collection target which encompasses all the databases in the pool.</span></span>

<span data-ttu-id="dcf4e-193">Définissez les variables suivantes pour refléter les informations de base de données souhaitées :</span><span class="sxs-lookup"><span data-stu-id="dcf4e-193">Set the following variables to reflect the desired database information:</span></span>

   ```
    $databaseName = "{Database Name}"
    $databaseServerName = "{Server Name}"
    New-AzureSqlJobDatabaseTarget -DatabaseName $databaseName -ServerName $databaseServerName
   ```

## <a name="create-a-custom-database-collection-target"></a><span data-ttu-id="dcf4e-194">Créez une cible de collecte de base de données personnalisée</span><span class="sxs-lookup"><span data-stu-id="dcf4e-194">Create a custom database collection target</span></span>
<span data-ttu-id="dcf4e-195">Une cible de collecte de base de données personnalisée peut être définie pour permettre l'exécution sur plusieurs cibles de base de données définies.</span><span class="sxs-lookup"><span data-stu-id="dcf4e-195">A custom database collection target can be defined to enable execution across multiple defined database targets.</span></span> <span data-ttu-id="dcf4e-196">Une fois le groupe de base de données créé, les bases de données peuvent être associées à la cible de collecte personnalisée.</span><span class="sxs-lookup"><span data-stu-id="dcf4e-196">After a database group is created, databases can be associated to the custom collection target.</span></span>

<span data-ttu-id="dcf4e-197">Définissez les variables suivantes pour refléter la configuration de la cible de collecte personnalisée souhaitée :</span><span class="sxs-lookup"><span data-stu-id="dcf4e-197">Set the following variables to reflect the desired custom collection target configuration:</span></span>

   ```
    $customCollectionName = "{Custom Database Collection Name}"
    New-AzureSqlJobTarget -CustomCollectionName $customCollectionName
   ```

### <a name="add-databases-to-a-custom-database-collection-target"></a><span data-ttu-id="dcf4e-198">Ajoutez des bases de données pour une cible de collecte de base de données personnalisée</span><span class="sxs-lookup"><span data-stu-id="dcf4e-198">Add databases to a custom database collection target</span></span>
<span data-ttu-id="dcf4e-199">Les cibles de base de données peuvent être associées à des cibles de collecte de base de données personnalisées pour créer un groupe de bases de données.</span><span class="sxs-lookup"><span data-stu-id="dcf4e-199">Database targets can be associated with custom database collection targets to create a group of databases.</span></span> <span data-ttu-id="dcf4e-200">Chaque fois qu’une tâche, visant une cible de collecte de base de données personnalisée, est créée, celle-ci est développée afin de cibler les bases de données associées au groupe durant l'exécution.</span><span class="sxs-lookup"><span data-stu-id="dcf4e-200">Whenever a job is created that targets a custom database collection target, it will be expanded to target the databases associated to the group at the time of execution.</span></span>

<span data-ttu-id="dcf4e-201">Ajoutez la base de données souhaitée pour une collecte personnalisée :</span><span class="sxs-lookup"><span data-stu-id="dcf4e-201">Add the desired database to a specific custom collection:</span></span>

   ```
    $serverName = "{Database Server Name}"
    $databaseName = "{Database Name}"
    $customCollectionName = "{Custom Database Collection Name}"
    Add-AzureSqlJobChildTarget -CustomCollectionName $customCollectionName -DatabaseName $databaseName -ServerName $databaseServerName
   ```

#### <a name="review-the-databases-within-a-custom-database-collection-target"></a><span data-ttu-id="dcf4e-202">Examinez les bases de données dans une cible de collecte de base de données personnalisée</span><span class="sxs-lookup"><span data-stu-id="dcf4e-202">Review the databases within a custom database collection target</span></span>
<span data-ttu-id="dcf4e-203">Utilisez l’applet de commande **Get-AzureSqlJobTarget** pour récupérer les bases de données enfants dans une cible de collecte de base de données personnalisée.</span><span class="sxs-lookup"><span data-stu-id="dcf4e-203">Use the **Get-AzureSqlJobTarget** cmdlet to retrieve the child databases within a custom database collection target.</span></span>

   ```
    $customCollectionName = "{Custom Database Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $childTargets = Get-AzureSqlJobTarget -ParentTargetId $target.TargetId
    Write-Output $childTargets
   ```

### <a name="create-a-job-to-execute-a-script-across-a-custom-database-collection-target"></a><span data-ttu-id="dcf4e-204">Créez une tâche pour exécuter un script sur une cible de collecte de base de données personnalisée</span><span class="sxs-lookup"><span data-stu-id="dcf4e-204">Create a job to execute a script across a custom database collection target</span></span>
<span data-ttu-id="dcf4e-205">Utilisez l’applet de commande **New-AzureSqlJob** pour créer une tâche sur un groupe de bases de données défini par une cible de collecte de base de données.</span><span class="sxs-lookup"><span data-stu-id="dcf4e-205">Use the **New-AzureSqlJob** cmdlet to create a job against a group of databases defined by a custom database collection target.</span></span> <span data-ttu-id="dcf4e-206">La fonctionnalité Tâches de bases de données élastiques étendra la tâche en plusieurs tâches enfants correspondant chacune à une base de données associée à la cible de la collecte de base de données personnalisée et s’assurera que le script est exécuté sur chaque base de données.</span><span class="sxs-lookup"><span data-stu-id="dcf4e-206">Elastic Database jobs will expand the job into multiple child jobs each corresponding to a database associated with the custom database collection target and ensure that the script is executed against each database.</span></span> <span data-ttu-id="dcf4e-207">Encore une fois, il est important que les scripts soient idempotents pour résister à de nouvelles tentatives.</span><span class="sxs-lookup"><span data-stu-id="dcf4e-207">Again, it is important that scripts are idempotent to be resilient to retries.</span></span>

   ```
    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $customCollectionName = "{Custom Collection Name}"
    $credentialName = "{Credential Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job
   ```

## <a name="data-collection-across-databases"></a><span data-ttu-id="dcf4e-208">Collecte de données sur les bases de données</span><span class="sxs-lookup"><span data-stu-id="dcf4e-208">Data collection across databases</span></span>
<span data-ttu-id="dcf4e-209">**Tâches de bases de données élastiques** prend en charge l'exécution d'une requête sur un groupe de bases de données et envoie les résultats de la table d’une base de données spécifiée.</span><span class="sxs-lookup"><span data-stu-id="dcf4e-209">**Elastic Database jobs** supports executing a query across a group of databases and sends the results to a specified database’s table.</span></span> <span data-ttu-id="dcf4e-210">Le tableau peut être interrogé une fois les résultats de la requête affichés à partir de chaque base de données.</span><span class="sxs-lookup"><span data-stu-id="dcf4e-210">The table can be queried after the fact to see the query’s results from each database.</span></span> <span data-ttu-id="dcf4e-211">Ceci fournit un mécanisme asynchrone, permettant d’exécuter une requête sur plusieurs bases de données.</span><span class="sxs-lookup"><span data-stu-id="dcf4e-211">This provides an asynchronous mechanism to execute a query across many databases.</span></span> <span data-ttu-id="dcf4e-212">Les cas d'échec, notamment l’indisponibilité temporaire d’une des bases de données, sont gérés automatiquement par le biais de tentatives.</span><span class="sxs-lookup"><span data-stu-id="dcf4e-212">Failure cases such as one of the databases being temporarily unavailable are handled automatically via retries.</span></span>

<span data-ttu-id="dcf4e-213">La table de destination spécifiée sera automatiquement créée s’il n’existe pas encore de table correspondant au schéma du jeu de résultats retourné.</span><span class="sxs-lookup"><span data-stu-id="dcf4e-213">The specified destination table will be automatically created if it does not yet exist, matching the schema of the returned result set.</span></span> <span data-ttu-id="dcf4e-214">Si l'exécution d'un script retourne plusieurs jeux de résultats, la fonctionnalité Tâches de bases de données élastiques enverra uniquement le premier vers la table de destination fournie.</span><span class="sxs-lookup"><span data-stu-id="dcf4e-214">If a script execution returns multiple result sets, Elastic Database jobs will only send the first one to the provided destination table.</span></span>

<span data-ttu-id="dcf4e-215">Le script PowerShell suivant peut être utilisé pour exécuter un script qui collecte ses résultats dans une table spécifiée.</span><span class="sxs-lookup"><span data-stu-id="dcf4e-215">The following PowerShell script can be used to execute a script collecting its results into a specified table.</span></span> <span data-ttu-id="dcf4e-216">Ce script part du principe qu'un script T-SQL, qui génère un jeu de résultats unique, et une cible de collecte de base de données personnalisée ont été créés.</span><span class="sxs-lookup"><span data-stu-id="dcf4e-216">This script assumes that a T-SQL script has been created which outputs a single result set and a custom database collection target has been created.</span></span>

<span data-ttu-id="dcf4e-217">Définissez les valeurs suivantes pour refléter le script, les informations d'identification et les cibles d'exécution souhaités :</span><span class="sxs-lookup"><span data-stu-id="dcf4e-217">Set the following to reflect the desired script, credentials, and execution target:</span></span>

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

### <a name="create-and-start-a-job-for-data-collection-scenarios"></a><span data-ttu-id="dcf4e-218">Créez et démarrez une tâche pour les scénarios de collecte de données</span><span class="sxs-lookup"><span data-stu-id="dcf4e-218">Create and start a job for data collection scenarios</span></span>
   ```
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $executionCredentialName -ContentName $scriptName -ResultSetDestinationServerName $destinationServerName -ResultSetDestinationDatabaseName $destinationDatabaseName -ResultSetDestinationSchemaName $destinationSchemaName -ResultSetDestinationTableName $destinationTableName -ResultSetDestinationCredentialName $destinationCredentialName -TargetId $target.TargetId
    Write-Output $job
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName
    Write-Output $jobExecution
   ```

## <a name="create-a-schedule-for-job-execution-using-a-job-trigger"></a><span data-ttu-id="dcf4e-219">Créez une planification pour l'exécution de tâches à l'aide d'un déclencheur de tâches</span><span class="sxs-lookup"><span data-stu-id="dcf4e-219">Create a schedule for job execution using a job trigger</span></span>
<span data-ttu-id="dcf4e-220">Le script PowerShell suivant peut être utilisé pour créer une planification récurrente.</span><span class="sxs-lookup"><span data-stu-id="dcf4e-220">The following PowerShell script can be used to create a reoccurring schedule.</span></span> <span data-ttu-id="dcf4e-221">Ce script utilise un intervalle d’une minute, mais New-AzureSqlJobSchedule prend également en charge les paramètres -DayInterval, - HourInterval, - MonthInterval et - WeekInterval.</span><span class="sxs-lookup"><span data-stu-id="dcf4e-221">This script uses a one minute interval, but New-AzureSqlJobSchedule also supports -DayInterval, -HourInterval, -MonthInterval, and -WeekInterval parameters.</span></span> <span data-ttu-id="dcf4e-222">Les planifications qui ne s'exécutent qu'une seule fois peuvent être créées en transmettant  - OneTime.</span><span class="sxs-lookup"><span data-stu-id="dcf4e-222">Schedules that execute only once can be created by passing -OneTime.</span></span>

<span data-ttu-id="dcf4e-223">Créez une nouvelle planification :</span><span class="sxs-lookup"><span data-stu-id="dcf4e-223">Create a new schedule:</span></span>
   ```
    $scheduleName = "Every one minute"
    $minuteInterval = 1
    $startTime = (Get-Date).ToUniversalTime()
    $schedule = New-AzureSqlJobSchedule -MinuteInterval $minuteInterval -ScheduleName $scheduleName -StartTime $startTime
    Write-Output $schedule
   ```

### <a name="create-a-job-trigger-to-have-a-job-executed-on-a-time-schedule"></a><span data-ttu-id="dcf4e-224">Créez un déclencheur de tâches pour une tâche exécutée selon un calendrier</span><span class="sxs-lookup"><span data-stu-id="dcf4e-224">Create a job trigger to have a job executed on a time schedule</span></span>
<span data-ttu-id="dcf4e-225">Un déclencheur de tâches peut être défini pour un travail exécuté selon un calendrier.</span><span class="sxs-lookup"><span data-stu-id="dcf4e-225">A job trigger can be defined to have a job executed according to a time schedule.</span></span> <span data-ttu-id="dcf4e-226">Le script PowerShell suivant peut être utilisé pour créer un déclencheur de tâches.</span><span class="sxs-lookup"><span data-stu-id="dcf4e-226">The following PowerShell script can be used to create a job trigger.</span></span>

<span data-ttu-id="dcf4e-227">Définissez les variables suivantes pour qu’elles correspondent à la tâche et à la planification souhaitées :</span><span class="sxs-lookup"><span data-stu-id="dcf4e-227">Set the following variables to correspond to the desired job and schedule:</span></span>

   ```
    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    $jobTrigger = New-AzureSqlJobTrigger -ScheduleName $scheduleName -JobName $jobName
    Write-Output $jobTrigger
   ```

### <a name="remove-a-scheduled-association-to-stop-job-from-executing-on-schedule"></a><span data-ttu-id="dcf4e-228">Supprimez une association planifiée pour arrêter une tâche depuis l'exécution de la planification</span><span class="sxs-lookup"><span data-stu-id="dcf4e-228">Remove a scheduled association to stop job from executing on schedule</span></span>
<span data-ttu-id="dcf4e-229">Pour interrompre l'exécution d’une tâche récurrente via un déclencheur de tâches, le déclencheur de tâches peut être supprimé.</span><span class="sxs-lookup"><span data-stu-id="dcf4e-229">To discontinue reoccurring job execution through a job trigger, the job trigger can be removed.</span></span>
<span data-ttu-id="dcf4e-230">Supprimez un déclencheur de tâches pour arrêter une tâche qui s'exécute selon une planification à l'aide de l’applet de commande **Remove-AzureSqlJobTrigger** .</span><span class="sxs-lookup"><span data-stu-id="dcf4e-230">Remove a job trigger to stop a job from being executed according to a schedule using the **Remove-AzureSqlJobTrigger** cmdlet.</span></span>

   ```
    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Remove-AzureSqlJobTrigger -ScheduleName $scheduleName -JobName $jobName
   ```

## <a name="import-elastic-database-query-results-to-excel"></a><span data-ttu-id="dcf4e-231">Importez les résultats de la requête de base de données élastique dans Excel</span><span class="sxs-lookup"><span data-stu-id="dcf4e-231">Import elastic database query results to Excel</span></span>
 <span data-ttu-id="dcf4e-232">Vous pouvez importer les résultats d’une requête vers un fichier Excel.</span><span class="sxs-lookup"><span data-stu-id="dcf4e-232">You can import the results from of a query to an Excel file.</span></span>

1. <span data-ttu-id="dcf4e-233">Lancez Excel 2013.</span><span class="sxs-lookup"><span data-stu-id="dcf4e-233">Launch Excel 2013.</span></span>
2. <span data-ttu-id="dcf4e-234">Accédez au ruban **Données** .</span><span class="sxs-lookup"><span data-stu-id="dcf4e-234">Navigate to the **Data** ribbon.</span></span>
3. <span data-ttu-id="dcf4e-235">Cliquez sur **À partir d’autres sources** et sur **À partir de SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="dcf4e-235">Click **From Other Sources** and click **From SQL Server**.</span></span>

   ![Importation au format Excel à partir d’autres sources](./media/sql-database-elastic-query-getting-started/exel-sources.png)

4. <span data-ttu-id="dcf4e-237">Dans l’ **Assistant de connexion de données** saisissez le nom du serveur et les informations de connexion.</span><span class="sxs-lookup"><span data-stu-id="dcf4e-237">In the **Data Connection Wizard** type the server name and login credentials.</span></span> <span data-ttu-id="dcf4e-238">Cliquez ensuite sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="dcf4e-238">Then click **Next**.</span></span>
5. <span data-ttu-id="dcf4e-239">Dans la boîte de dialogue **Sélectionner la base de données qui contient les données que vous souhaitez**, sélectionnez la base de données **ElasticDBQuery**.</span><span class="sxs-lookup"><span data-stu-id="dcf4e-239">In the dialog box **Select the database that contains the data you want**, select the **ElasticDBQuery** database.</span></span>
6. <span data-ttu-id="dcf4e-240">Sélectionnez la table **Clients** dans la liste et cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="dcf4e-240">Select the **Customers** table in the list view and click **Next**.</span></span> <span data-ttu-id="dcf4e-241">Puis, cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="dcf4e-241">Then click **Finish**.</span></span>
7. <span data-ttu-id="dcf4e-242">Dans le formulaire **Importer des données**, sous **Sélectionner le mode d’affichage des données dans votre classeur**, sélectionnez **Table** et cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="dcf4e-242">In the **Import Data** form, under **Select how you want to view this data in your workbook**, select **Table** and click **OK**.</span></span>

<span data-ttu-id="dcf4e-243">Toutes les lignes de la table **Clients** , stockées dans des partitions différentes, remplissent la feuille Excel.</span><span class="sxs-lookup"><span data-stu-id="dcf4e-243">All the rows from **Customers** table, stored in different shards populate the Excel sheet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dcf4e-244">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="dcf4e-244">Next steps</span></span>
<span data-ttu-id="dcf4e-245">Vous pouvez maintenant utiliser les fonctions de données Excel.</span><span class="sxs-lookup"><span data-stu-id="dcf4e-245">You can now use Excel’s data functions.</span></span> <span data-ttu-id="dcf4e-246">Utilisez la chaîne de connexion avec votre nom de serveur, votre nom de base de données et les informations d’identification pour connecter vos outils d’intégration BI et de données à la base de données de requête élastique.</span><span class="sxs-lookup"><span data-stu-id="dcf4e-246">Use the connection string with your server name, database name and credentials to connect your BI and data integration tools to the elastic query database.</span></span> <span data-ttu-id="dcf4e-247">Assurez-vous que SQL Server est pris en charge comme source de données pour votre outil.</span><span class="sxs-lookup"><span data-stu-id="dcf4e-247">Make sure that SQL Server is supported as a data source for your tool.</span></span> <span data-ttu-id="dcf4e-248">Traitez la base de données de requête élastique et les tables externes comme n’importe quelles bases de données SQL Server et tables SQL Server auxquelles vous vous connectez avec votre outil.</span><span class="sxs-lookup"><span data-stu-id="dcf4e-248">Refer to the elastic query database and external tables just like any other SQL Server database and SQL Server tables that you would connect to with your tool.</span></span>

### <a name="cost"></a><span data-ttu-id="dcf4e-249">Coût</span><span class="sxs-lookup"><span data-stu-id="dcf4e-249">Cost</span></span>
<span data-ttu-id="dcf4e-250">La fonction de requête de base de données élastique n’entraîne pas de frais supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="dcf4e-250">There is no additional charge for using the Elastic Database query feature.</span></span> <span data-ttu-id="dcf4e-251">Toutefois, pour l’instant, cette fonctionnalité n’est disponible que sur les bases de données premium comme point de terminaison, mais les partitions peuvent provenir de n’importe quel niveau de service.</span><span class="sxs-lookup"><span data-stu-id="dcf4e-251">However, at this time this feature is available only on premium databases as an end point, but the shards can be of any service tier.</span></span>

<span data-ttu-id="dcf4e-252">Pour plus d’informations sur la tarification, consultez la page [Tarification - Base de données SQL](https://azure.microsoft.com/pricing/details/sql-database/).</span><span class="sxs-lookup"><span data-stu-id="dcf4e-252">For pricing information see [SQL Database Pricing Details](https://azure.microsoft.com/pricing/details/sql-database/).</span></span>

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-query-getting-started/cmd-prompt.png
[2]: ./media/sql-database-elastic-query-getting-started/portal.png
[3]: ./media/sql-database-elastic-query-getting-started/tiers.png
[4]: ./media/sql-database-elastic-query-getting-started/details.png
[5]: ./media/sql-database-elastic-query-getting-started/exel-sources.png
<!--anchors-->
