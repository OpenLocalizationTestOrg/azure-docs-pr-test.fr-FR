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
# <a name="getting-started-with-elastic-database-jobs"></a>Prise en main de Tâches de bases de données élastiques
Travaux de base de données élastique (version préliminaire) pour base de données SQL Azure vous permet de tooreliability exécuter des scripts T-SQL qui s’étendent sur plusieurs bases de données lors de la tentative automatique et en fournissant son achèvement éventuel de garantie. Pour plus d’informations sur la fonctionnalité de travail de base de données élastique hello, consultez hello [page de vue d’ensemble de fonctionnalités](sql-database-elastic-jobs-overview.md).

Cette rubrique étend l’exemple hello trouvé dans [prise en main des outils de base de données élastique](sql-database-elastic-scale-get-started.md). Issue, vous allez : Découvrez comment toocreate et gérer les travaux de gérer un groupe de bases de données associées. Il n’est pas requis toouse hello élastique outils dans bénéficiant de tootake d’ordre de hello travaux élastique.

## <a name="prerequisites"></a>Composants requis
Téléchargez et exécutez hello [mise en route avec l’exemple des outils de base de données élastique](sql-database-elastic-scale-get-started.md).

## <a name="create-a-shard-map-manager-using-hello-sample-app"></a>Créer une carte de partitions manager à l’aide de hello, exemple d’application
Ici vous allez créer une carte de partitions manager ainsi que plusieurs partitions, suivie de l’insertion de données dans les partitions hello. Si vous avez déjà configuré avec des données partitionnées de partitions, vous pouvez ignorer hello comme suit et déplacer la section suivante de toohello.

1. Générez et exécutez hello **prise en main des outils de base de données élastique** exemple d’application. Hello comme suit avant l’étape 7 de la section de hello [télécharger et exécuter l’exemple d’application hello](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app). Extrémité hello de l’étape 7, vous verrez hello après l’invite de commandes :

   ![invite de commande](./media/sql-database-elastic-query-getting-started/cmd-prompt.png)

2. Dans la fenêtre de commande hello, tapez « 1 » et appuyez sur **entrée**. Cela crée le Gestionnaire de carte de partitions hello et ajoute le serveur de toohello deux partitions. Entrez « 3 », puis appuyez sur **Entrée**. Répétez cette action quatre fois. Cela permet d’insérer des lignes d’exemples de données dans vos partitions.
3. Hello [portail Azure](https://portal.azure.com) doit afficher trois nouvelles bases de données :

   ![Confirmation Visual Studio](./media/sql-database-elastic-query-getting-started/portal.png)

   À ce stade, nous allons créer une collection de base de données personnalisée qui reflète toutes les bases de données hello dans la carte de partitions hello. Cela nous permet toocreate et exécuter un travail qui ajouter une nouvelle table entre les partitions.

Ici nous généralement créerait une cible de carte de partitions, à l’aide de hello **New-AzureSqlJobTarget** applet de commande. base de données du gestionnaire Hello partition carte doit être défini en tant que base de données cible et ensuite la carte de partitions spécifiques de hello est spécifié en tant que cible. Au lieu de cela, nous continu tooenumerate toutes les bases de données hello dans le serveur de hello et ajouter hello bases de données toohello nouveau regroupement personnalisé avec l’exception hello de base de données master.

## <a name="creates-a-custom-collection-and-add-all-databases-in-hello-server-toohello-custom-collection-target-with-hello-exception-of-master"></a>Crée une collection personnalisée et ajoutez toutes les bases de données dans la cible de collection personnalisée hello serveur toohello avec l’exception hello du maître.
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
## <a name="create-a-t-sql-script-for-execution-across-databases"></a>Créez un script T-SQL pour l’exécuter sur des bases de données
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

## <a name="create-hello-job-tooexecute-a-script-across-hello-custom-group-of-databases"></a>Création d’un script hello travail tooexecute entre le groupe personnalisé de hello des bases de données

   ```
    $jobName = "create on server dbs"
    $scriptName = "NewTable"
    $customCollectionName = "dbs_in_server"
    $credentialName = "ddove66"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job
   ```

## <a name="execute-hello-job"></a>Exécuter le travail de hello
Hello PowerShell script suivant peut être utilisé tooexecute un travail existant :

Mettre à jour hello suivant tooreflect variable hello souhaité travail nom toohave exécutée :

   ```
    $jobName = "create on server dbs"
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName
    Write-Output $jobExecution
   ```

## <a name="retrieve-hello-state-of-a-single-job-execution"></a>Récupérer l’état de l’exécution d’une seule tâche hello
Utilisez hello même **Get-AzureSqlJobExecution** applet de commande avec hello **IncludeChildren** état de hello tooview paramètre d’exécutions de travail enfant, hello à savoir un état spécifique pour chaque exécution du travail sur chaque base de données ciblée par le travail de hello.

   ```
    $jobExecutionId = "{Job Execution Id}"
    $jobExecutions = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId -IncludeChildren
    Write-Output $jobExecutions
   ```

## <a name="view-hello-state-across-multiple-job-executions"></a>Afficher l’état hello sur plusieurs exécutions du travail
Hello **Get-AzureSqlJobExecution** applet de commande a plusieurs paramètres facultatifs qui peuvent être utilisé toodisplay plusieurs exécutions du travail, filtrées par le biais des paramètres de hello fourni. suivant de Hello présente quelques-unes des façons possibles de hello toouse Get-AzureSqlJobExecution :

Récupérez toutes les exécutions de tâches de niveau supérieur actives :

   ```
    Get-AzureSqlJobExecution
   ```

Récupérez toutes les exécutions de tâches de niveau supérieur, y compris les exécutions de tâches inactives :

   ```
    Get-AzureSqlJobExecution -IncludeInactive
   ```

Récupérez toutes les exécutions de tâches enfants d'un ID d'exécution de tâches fourni, y compris les exécutions de tâches inactives :

   ```
    $parentJobExecutionId = "{Job Execution Id}"
    Get-AzureSqlJobExecution -AzureSqlJobExecution -JobExecutionId $parentJobExecutionId -IncludeInactive -IncludeChildren
   ```

Récupérez toutes les exécutions de tâches créées à l'aide d'une planification/combinaison de tâches, y compris les tâches inactives :

   ```
    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Get-AzureSqlJobExecution -JobName $jobName -ScheduleName $scheduleName -IncludeInactive
   ```

Récupérez toutes les tâches ciblant une carte de partitions spécifiée, y compris les tâches inactives :

   ```
    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $target = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive
   ```

Récupérez toutes les tâches ciblant une collecte personnalisée spécifiée, y compris les tâches inactives :

   ```
    $customCollectionName = "{Custom Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive
   ```

Récupérer la liste de hello d’exécutions de tâches de travail au sein de l’exécution d’une tâche spécifique :

   ```
    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Write-Output $jobTaskExecutions
   ```

Récupérez les détails d’exécution de tâches de travail :

Hello PowerShell script suivant peut être utilisé tooview les détails de hello une tâche d’exécution des tâches, qui est particulièrement utile lors du débogage des erreurs d’exécution.
   ```
    $jobTaskExecutionId = "{Job Task Execution Id}"
    $jobTaskExecution = Get-AzureSqlJobTaskExecution -JobTaskExecutionId $jobTaskExecutionId
    Write-Output $jobTaskExecution
   ```

## <a name="retrieve-failures-within-job-task-executions"></a>Récupérez des échecs dans les exécutions de tâches de travail
objet de JobTaskExecution Hello inclut une propriété pour hello du cycle de vie de la tâche hello avec une propriété de Message. Si une exécution de tâches de travail a échoué, hello du cycle de vie propriété sera définie trop*n’a pas pu* et propriété de Message de salutation sera définie message d’exception résultant toohello et sa pile. Si une tâche n’a pas réussi, il est important tooview les détails de hello des tâches de travail qui n’a pas réussi pour un travail donné.

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

## <a name="waiting-for-a-job-execution-toocomplete"></a>En attente pour un toocomplete de l’exécution du travail
Hello PowerShell script suivant peut être utilisé toowait pour un toocomplete de tâche de travail :

   ```
    $jobExecutionId = "{Job Execution Id}"
    Wait-AzureSqlJobExecution -JobExecutionId $jobExecutionId
   ```

## <a name="create-a-custom-execution-policy"></a>Créez une stratégie d'exécution personnalisée
Tâches de bases de données prend en charge la création de stratégies d'exécution personnalisées qui peuvent être appliquées lors du démarrage des tâches.

Les stratégies d'exécution permettent de définir :

* Nom : L’identificateur de la stratégie d’exécution hello.
* Délai d’attente de la tâche : délai avant l’annulation d’une tâche par Tâches de bases de données élastiques.
* Intervalle de nouvelle tentative initial : Toowait d’intervalle avant la première nouvelle tentative.
* Intervalle maximal de tentatives : L’extrémité de toouse des intervalles de nouvelle tentative.
* Coefficient d’interruption d’intervalle de nouvelle tentative : Coefficient utilisé toocalculate hello prochain intervalle entre les nouvelles tentatives.  Hello formule suivante est utilisée : (intervalle avant nouvelle tentative initiale) * Math.pow (intervalle interruption Coefficient (), (nombre de tentatives de) - 2).
* Nombre maximal de tentatives : hello nombre maximal de tooperform de tentatives de nouvelle tentative au sein d’un travail.

stratégie d’exécution par défaut Hello utilise hello valeurs suivantes :

* Le nom : la stratégie d'exécution par défaut
* Délai d’attente de la tâche : 1 semaine
* Intervalle avant nouvelle tentative initiale : 100 millisecondes
* Intervalle maximal avant nouvelle tentative : 30 minutes
* Coefficient de l'intervalle avant nouvelle tentative : 2
* Nombre maximal de tentatives : 2 147 483 647

Créer la stratégie d’exécution hello souhaité :

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

### <a name="update-a-custom-execution-policy"></a>Mettez à jour une stratégie d'exécution personnalisée
Hello de mise à jour souhaitée tooupdate de stratégie d’exécution :

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

## <a name="cancel-a-job"></a>Annulation d’une tâche
La fonctionnalité Tâches de bases de données élastiques prend en charge les demandes d’annulation de tâches.  Si les travaux de base de données élastique détecte une demande d’annulation d’une tâche en cours d’exécution, il tentera de travail de hello toostop.

La fonctionnalité Tâches de bases de données élastiques peut effectuer une annulation de deux manières différentes :

1. L’annulation en cours d’exécution des tâches : si une annulation est détectée pendant une tâche est en cours d’exécution, l’annulation sera tentée dans hello aspect de la tâche hello en cours d’exécution.  Par exemple : en l’absence d’une requête longue en cours d’exécution lorsqu’une annulation est tentée, il y aura une requête de hello toocancel tentative.
2. Nouvelles tentatives annulation de tâche : Si une annulation est détectée par le thread de contrôle hello avant de lancer une tâche pour l’exécution, thread de contrôle hello éviter de lancer la tâche hello et déclarer la demande de hello comme annulée.

Si une annulation de tâche est demandée pour un travail parent, demande d’annulation hello sera respectée pour la tâche parente de hello et pour toutes ses tâches enfants.

toosubmit une demande d’annulation, utilisez hello **Stop-AzureSqlJobExecution** applet de commande et ensemble hello **JobExecutionId** paramètre.

   ```
    $jobExecutionId = "{Job Execution Id}"
    Stop-AzureSqlJobExecution -JobExecutionId $jobExecutionId
   ```

## <a name="delete-a-job-by-name-and-hello-jobs-history"></a>Supprimer un travail par nom et l’historique du travail hello
Tâches de bases de données élastiques prend en charge la suppression des tâches asynchrone. Un travail peut être marqué pour suppression et hello système supprime le travail de hello et son historique une fois que toutes les exécutions de la tâche s’est terminé pour le travail de hello. système de Hello n’est pas automatiquement annulé exécutions de travail actif.  

Au lieu de cela, Stop-AzureSqlJobExecution doit être appelée toocancel les exécutions de travail actif.

suppression du travail tootrigger, utilisez hello **Remove-AzureSqlJob** applet de commande et ensemble hello **JobName** paramètre.

   ```
    $jobName = "{Job Name}"
    Remove-AzureSqlJob -JobName $jobName
   ```

## <a name="create-a-custom-database-target"></a>Création d’une cible de base de données personnalisée
Les cibles de base de données personnalisées peuvent être définies dans Tâches de bases de données élastiques, qui peut être utilisé directement pour l'exécution ou l’inclusion dans un groupe de base de données personnalisé. Étant donné que **pools élastiques** sont pas encore directement pris en charge via hello APIs PowerShell, vous créez simplement une cible de la base de données personnalisée et la cible de collection de base de données personnalisée qui englobe toutes les bases de données hello dans le pool de hello.

Définissez hello suit les informations de base de données de variables tooreflect hello souhaité :

   ```
    $databaseName = "{Database Name}"
    $databaseServerName = "{Server Name}"
    New-AzureSqlJobDatabaseTarget -DatabaseName $databaseName -ServerName $databaseServerName
   ```

## <a name="create-a-custom-database-collection-target"></a>Créez une cible de collecte de base de données personnalisée
Une cible de collection de base de données personnalisée peut être l’exécution de tooenable définie sur plusieurs cibles de base de données. Après la création d’un groupe de la base de données, les bases de données peuvent être cible de collection personnalisée toohello associé.

Définissez hello variables tooreflect hello collection personnalisée souhaitée cible configuration suivante :

   ```
    $customCollectionName = "{Custom Database Collection Name}"
    New-AzureSqlJobTarget -CustomCollectionName $customCollectionName
   ```

### <a name="add-databases-tooa-custom-database-collection-target"></a>Ajouter la cible de collecte des bases de données tooa base de données personnalisée
Cibles de la base de données peuvent être associés à la base de données personnalisée collection cibles toocreate un groupe de bases de données. Chaque fois qu’un travail est créé qui pointe vers une cible de collection de base de données personnalisée, il sera groupe toohello associé de développé tootarget hello bases de données au moment de l’exécution de hello.

Ajouter la collecte personnalisée spécifique de base de données tooa hello souhaité :

   ```
    $serverName = "{Database Server Name}"
    $databaseName = "{Database Name}"
    $customCollectionName = "{Custom Database Collection Name}"
    Add-AzureSqlJobChildTarget -CustomCollectionName $customCollectionName -DatabaseName $databaseName -ServerName $databaseServerName
   ```

#### <a name="review-hello-databases-within-a-custom-database-collection-target"></a>Passez en revue les bases de données hello dans une cible de collection de base de données personnalisée
Hello d’utilisation **Get-AzureSqlJobTarget** applet de commande tooretrieve hello enfant bases de données d’une cible de collection de base de données personnalisée.

   ```
    $customCollectionName = "{Custom Database Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $childTargets = Get-AzureSqlJobTarget -ParentTargetId $target.TargetId
    Write-Output $childTargets
   ```

### <a name="create-a-job-tooexecute-a-script-across-a-custom-database-collection-target"></a>Créer un travail tooexecute un script sur une cible de collection personnalisé de la base de données
Hello d’utilisation **New-AzureSqlJob** toocreate de l’applet de commande un travail par rapport à un groupe de bases de données définies par une cible de collection de base de données personnalisée. Les travaux de base de données élastiques développera les travaux hello en plusieurs tâches enfants chaque base de données tooa correspondante associée cible de collecte de base de données personnalisée hello et assurez-vous que le script de hello est exécutée sur chaque base de données. Là encore, il est important que les scripts sont tooretries résilient de toobe idempotent.

   ```
    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $customCollectionName = "{Custom Collection Name}"
    $credentialName = "{Credential Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job
   ```

## <a name="data-collection-across-databases"></a>Collecte de données sur les bases de données
**Les travaux de base de données élastiques** prend en charge l’exécution d’une requête sur un groupe de bases de données et envoie les table hello résultats tooa spécifié de base de données. table de Hello peut être interrogée après les résultats de la requête hello hello faits toosee à partir de chaque base de données. Cela fournit un tooexecute mécanisme asynchrone d’une requête entre plusieurs bases de données. Cas d’échec comme l’une des bases de données hello est temporairement indisponible sont gérées automatiquement par nouvelles tentatives.

table de destination spécifiée Hello sera automatiquement créée si elle n’existe pas encore, schéma hello correspondant de hello retourné de jeu de résultats. Si l’exécution du script retourne plusieurs jeux de résultats, les tâches de base de données élastique n’envoie hello première table de destination un toohello fourni.

Hello PowerShell script suivant peut être utilisé tooexecute un script qui collecte ses résultats dans une table spécifiée. Ce script part du principe qu'un script T-SQL, qui génère un jeu de résultats unique, et une cible de collecte de base de données personnalisée ont été créés.

Hello ensemble suivant tooreflect hello souhaitée script, informations d’identification et la cible de l’exécution :

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

### <a name="create-and-start-a-job-for-data-collection-scenarios"></a>Créez et démarrez une tâche pour les scénarios de collecte de données
   ```
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $executionCredentialName -ContentName $scriptName -ResultSetDestinationServerName $destinationServerName -ResultSetDestinationDatabaseName $destinationDatabaseName -ResultSetDestinationSchemaName $destinationSchemaName -ResultSetDestinationTableName $destinationTableName -ResultSetDestinationCredentialName $destinationCredentialName -TargetId $target.TargetId
    Write-Output $job
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName
    Write-Output $jobExecution
   ```

## <a name="create-a-schedule-for-job-execution-using-a-job-trigger"></a>Créez une planification pour l'exécution de tâches à l'aide d'un déclencheur de tâches
Hello PowerShell script suivant peut être utilisé toocreate un calendrier récurrent. Ce script utilise un intervalle d’une minute, mais New-AzureSqlJobSchedule prend également en charge les paramètres -DayInterval, - HourInterval, - MonthInterval et - WeekInterval. Les planifications qui ne s'exécutent qu'une seule fois peuvent être créées en transmettant  - OneTime.

Créez une nouvelle planification :
   ```
    $scheduleName = "Every one minute"
    $minuteInterval = 1
    $startTime = (Get-Date).ToUniversalTime()
    $schedule = New-AzureSqlJobSchedule -MinuteInterval $minuteInterval -ScheduleName $scheduleName -StartTime $startTime
    Write-Output $schedule
   ```

### <a name="create-a-job-trigger-toohave-a-job-executed-on-a-time-schedule"></a>Créer un toohave de déclencheur de tâche à une tâche s’exécutée selon une planification
Un déclencheur de tâche peut être défini toohave un travail exécuté conformément tooa Calendrier. Hello PowerShell script suivant peut être utilisé toocreate un déclencheur de tâche.

Hello ensemble suivant de variables toocorrespond toohello souhaitée de travail et une planification :

   ```
    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    $jobTrigger = New-AzureSqlJobTrigger -ScheduleName $scheduleName -JobName $jobName
    Write-Output $jobTrigger
   ```

### <a name="remove-a-scheduled-association-toostop-job-from-executing-on-schedule"></a>Supprimer une tâche de toostop association planifiée l’exécution de la planification
toodiscontinue qui se reproduit l’exécution du travail via un déclencheur de tâche, le déclencheur de tâche hello peut être supprimée.
Supprimer un toostop de déclencheur de tâche un travail à partir d’en cours d’exécution en fonction tooa planification, à l’aide de hello **Remove-AzureSqlJobTrigger** applet de commande.

   ```
    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Remove-AzureSqlJobTrigger -ScheduleName $scheduleName -JobName $jobName
   ```

## <a name="import-elastic-database-query-results-tooexcel"></a>Importer tooExcel de résultats de requête de base de données élastique
 Vous pouvez importer les résultats hello à partir d’un fichier Excel de tooan requête.

1. Lancez Excel 2013.
2. Accédez toohello **données** ruban.
3. Cliquez sur **À partir d’autres sources** et sur **À partir de SQL Server**.

   ![Importation au format Excel à partir d’autres sources](./media/sql-database-elastic-query-getting-started/exel-sources.png)

4. Bonjour **Assistant connexion de données** tapez hello des informations d’identification nom et la connexion de serveur. Cliquez ensuite sur **Suivant**.
5. Dans la boîte de dialogue hello **base de données hello Select qui contient les données hello**, sélectionnez hello **ElasticDBQuery** base de données.
6. Sélectionnez hello **clients** de table dans la vue de liste hello et cliquez sur **suivant**. Puis, cliquez sur **Terminer**.
7. Bonjour **importer des données** formulaire sous **Choisissez comment vous voulez que tooview ces données dans votre classeur**, sélectionnez **Table** et cliquez sur **OK**.

Tous les hello des lignes à partir de **clients** table, stockée dans des partitions différentes remplir la feuille de calcul Excel hello.

## <a name="next-steps"></a>Étapes suivantes
Vous pouvez maintenant utiliser les fonctions de données Excel. Utilisez la chaîne de connexion hello avec le nom de votre serveur, nom de la base de données et les informations d’identification tooconnect votre BI et données intégration outils toohello requête élastique de base de données. Assurez-vous que SQL Server est pris en charge comme source de données pour votre outil. Consultez la base de données de requête élastique toohello et des tables externes comme toute autre base de données SQL Server et des tables SQL Server que vous devez vous connecter toowith votre outil.

### <a name="cost"></a>Coût
Il n’existe aucun frais supplémentaire pour à l’aide de la fonctionnalité de requête de base de données élastique hello. Toutefois, pour l’instant cette fonctionnalité est disponible uniquement sur les bases de données premium, comme un point de terminaison, les partitions hello peuvent être de n’importe quel niveau de service.

Pour plus d’informations sur la tarification, consultez la page [Tarification - Base de données SQL](https://azure.microsoft.com/pricing/details/sql-database/).

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-query-getting-started/cmd-prompt.png
[2]: ./media/sql-database-elastic-query-getting-started/portal.png
[3]: ./media/sql-database-elastic-query-getting-started/tiers.png
[4]: ./media/sql-database-elastic-query-getting-started/details.png
[5]: ./media/sql-database-elastic-query-getting-started/exel-sources.png
<!--anchors-->
