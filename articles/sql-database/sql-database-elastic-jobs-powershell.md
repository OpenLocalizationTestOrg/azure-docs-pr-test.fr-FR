---
title: "aaaCreate et gérer des tâches élastiques à l’aide de PowerShell | Documents Microsoft"
description: "PowerShell utilisé toomanage les pools de base de données SQL Azure"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
ms.assetid: 737d8d13-5632-4e18-9cb0-4d3b8a19e495
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: f6c18aecfa7e8c0b102a3b7cd2f266f5542ae400
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-sql-database-elastic-jobs-using-powershell-preview"></a>Création et gestion de tâches de bases de données SQL élastiques à l’aide de PowerShell (version préliminaire)

Hello PowerShell APIs pour **des travaux de base de données élastique** (en version préliminaire) vous permettent de définir un groupe de bases de données par rapport à laquelle les scripts sont exécutés. Cet article explique comment toocreate et gérer **des travaux de base de données élastique** à l’aide des applets de commande PowerShell. Voir [Vue d’ensemble des tâches de base de données élastiques](sql-database-elastic-jobs-overview.md). 

## <a name="prerequisites"></a>Composants requis
* Un abonnement Azure. Pour obtenir un essai gratuit, voir [Version d'évaluation d'un mois gratuite](https://azure.microsoft.com/pricing/free-trial/).
* Un ensemble de bases de données créées avec les outils de base de données élastique hello. Voir [Prise en main des outils de base de données élastiques](sql-database-elastic-scale-get-started.md).
* Azure PowerShell. Pour plus d’informations, consultez [comment tooinstall et configurer Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).
* **tâches de bases de données élastiques** : voir [Installing tâches de bases de données élastiques](sql-database-elastic-jobs-service-installation.md)

### <a name="select-your-azure-subscription"></a>Sélectionner votre abonnement Azure
abonnement de hello tooselect vous avez besoin de votre Id d’abonnement (**- SubscriptionId**) ou le nom de l’abonnement (**- SubscriptionName**). Si vous avez plusieurs abonnements, vous pouvez exécuter hello **Get-AzureRmSubscription** hello applet de commande et copie souhaité des informations d’abonnement à partir du jeu de résultats hello. Une fois vos informations d’abonnement, exécutez hello suivant l’applet de commande tooset cet abonnement comme valeur par défaut de hello, à savoir hello cible pour la création et la gestion des travaux :

    Select-AzureRmSubscription -SubscriptionId {SubscriptionID}

Hello [PowerShell ISE](https://technet.microsoft.com/library/dd315244.aspx) est recommandée pour l’utilisation toodevelop et exécuter des scripts PowerShell sur des tâches de base de données élastique hello.

## <a name="elastic-database-jobs-objects"></a>Objets des tâches de bases de données élastiques
Hello après le tableau répertorie tous les types d’objet hello de **des travaux de base de données élastique** , ainsi que sa description et ses APIs PowerShell correspondantes.

<table style="width:100%">
  <tr>
    <th>Type d'objet</th>
    <th>Description</th>
    <th>API PowerShell correspondantes</th>
  </tr>
  <tr>
    <td>Informations d'identification</td>
    <td>Nom d’utilisateur et mot de passe toouse lors de la connexion toodatabases pour l’exécution de scripts ou l’application de dacpac. <p>mot de passe Hello est chiffré avant d’envoyer tooand le stockage de base de données des travaux de base de données élastique hello.  mot de passe Hello est déchiffrée par hello service élastique travaux de base de données via les informations d’identification hello créé et téléchargé à partir du script d’installation hello.</td>
    <td><p>Get-AzureSqlJobCredential</p>
    <p>New-AzureSqlJobCredential</p><p>Set-AzureSqlJobCredential</p></td></td>
  </tr>

  <tr>
    <td>Script</td>
    <td>Toobe de script Transact-SQL utilisée pour l’exécution entre bases de données.  script de Hello doit être créé toobe idempotent, car le service de hello va tenter de l’exécution du script hello lors de défaillances.
    </td>
    <td>
    <p>Get-AzureSqlJobContent</p>
    <p>Get-AzureSqlJobContentDefinition</p>
    <p>New-AzureSqlJobContent</p>
    <p>Set-AzureSqlJobContentDefinition</p>
    </td>
  </tr>

  <tr>
    <td>DACPAC</td>
    <td><a href="https://msdn.microsoft.com/library/ee210546.aspx">Application de couche données </a> toobe appliquée sur des bases de données du package.

    </td>
    <td>
    <p>Get-AzureSqlJobContent</p>
    <p>New-AzureSqlJobContent</p>
    <p>Set-AzureSqlJobContentDefinition</p>
    </td>
  </tr>
  <tr>
    <td>Base de données cible</td>
    <td>Base de données et serveur nom pointage tooan base de données SQL Azure.

    </td>
    <td>
    <p>Get-AzureSqlJobTarget</p>
    <p>New-AzureSqlJobTarget</p>
    </td>
  </tr>
  <tr>
    <td>Carte de partitions cible</td>
    <td>Combinaison d’une cible de la base de données et un toobe d’informations d’identification utilisée toodetermine les informations stockées dans une carte de partitions de base de données élastique.
    </td>
    <td>
    <p>Get-AzureSqlJobTarget</p>
    <p>New-AzureSqlJobTarget</p>
    <p>Set-AzureSqlJobTarget</p>
    </td>
  </tr>
<tr>
    <td>Cible de la collection personnalisée</td>
    <td>Un groupe défini de bases de données toocollectively utiliser pour l’exécution.</td>
    <td>
    <p>Get-AzureSqlJobTarget</p>
    <p>New-AzureSqlJobTarget</p>
    </td>
  </tr>
<tr>
    <td>Cible enfant de la collection personnalisée</td>
    <td>Cible de la base de données qui est référencée à partir d'une collection personnalisée.</td>
    <td>
    <p>Add-AzureSqlJobChildTarget</p>
    <p>Remove-AzureSqlJobChildTarget</p>
    </td>
  </tr>

<tr>
    <td>Travail</td>
    <td>
    <p>Définition des paramètres d’une tâche qui peut être utilisé tootrigger exécution ou toofulfill une planification.</p>
    </td>
    <td>
    <p>Get-AzureSqlJob</p>
    <p>New-AzureSqlJob</p>
    <p>Set-AzureSqlJob</p>
    </td>
  </tr>

<tr>
    <td>Exécution des tâches</td>
    <td>
    <p>Conteneur de toofulfill nécessaire de tâches soit exécuter un script ou de l’application d’une cible de tooa DACPAC à l’aide des informations d’identification pour les connexions de base de données avec des erreurs gérées dans la stratégie d’exécution tooan conformément.</p>
    </td>
    <td>
    <p>Get-AzureSqlJobExecution</p>
    <p>Start-AzureSqlJobExecution</p>
    <p>Stop-AzureSqlJobExecution</p>
    <p>Wait-AzureSqlJobExecution</p>
  </tr>

<tr>
    <td>Exécution d’une tâche</td>
    <td>
    <p>Unité de travail toofulfill un travail.</p>
    <p>Si une tâche n’est pas en mesure de toosuccessfully exécuter, message d’exception résultant hello est consignée et une nouvelle tâche de travail correspondant est créée et exécutée dans toohello conformément spécifié stratégie d’exécution.</p></p>
    </td>
    <td>
    <p>Get-AzureSqlJobExecution</p>
    <p>Start-AzureSqlJobExecution</p>
    <p>Stop-AzureSqlJobExecution</p>
    <p>Wait-AzureSqlJobExecution</p>
  </tr>

<tr>
    <td>Stratégie d’exécution des tâches</td>
    <td>
    <p>Contrôle les délais d’expiration d’une tâche, les limites du nombre de tentatives et les intervalles entre les tentatives.</p>
    <p>Les tâches de bases de données incluent une stratégie d’exécution de tâche par défaut qui entraîne essentiellement un nombre infini de nouvelles tentatives de défaillances de tâches avec une interruption exponentielle des intervalles entre chaque tentative.</p>
    </td>
    <td>
    <p>Get-AzureSqlJobExecutionPolicy</p>
    <p>New-AzureSqlJobExecutionPolicy</p>
    <p>Set-AzureSqlJobExecutionPolicy</p>
    </td>
  </tr>

<tr>
    <td>Planification</td>
    <td>
    <p>Heure de base relatives à la place de tootake d’exécution sur un intervalle de récurrent ou à une seule fois.</p>
    </td>
    <td>
    <p>Get-AzureSqlJobSchedule</p>
    <p>New-AzureSqlJobSchedule</p>
    <p>Set-AzureSqlJobSchedule</p>
    </td>
  </tr>

<tr>
    <td>Déclencheur de tâches</td>
    <td>
    <p>Un mappage entre une tâche et une planification tootrigger l’exécution du travail en fonction de la planification de toohello.</p>
    </td>
    <td>
    <p>New-AzureSqlJobTrigger</p>
    <p>Remove-AzureSqlJobTrigger</p>
    </td>
  </tr>
</table>

## <a name="supported-elastic-database-jobs-group-types"></a>Types de groupe des tâches de bases de données élastiques prises en charge
Hello s’exécute des scripts Transact-SQL (T-SQL) ou l’application de dacpac sur un groupe de bases de données. Lorsqu’une tâche est soumis toobe exécutée dans un groupe de bases de données, les travaux hello » développe « hello en tâches enfants effectuent hello où chacun a demandé l’exécution par rapport à une base de données dans le groupe de hello. 

Vous pouvez créer deux types de groupes : 

* [Carte de partitions](sql-database-elastic-scale-shard-map-management.md) groupe : lorsqu’une tâche est soumis tootarget une carte de partitions, les travaux hello interroge toodetermine de carte de partitions hello son ensemble de partitions et qu’il crée ensuite des travaux pour chaque partition enfant dans la carte de partitions hello.
* Groupe Collection personnalisée : un ensemble défini de bases de données personnalisées. Lorsqu’un projet cible une collection personnalisée, il crée enfant travaux pour chaque base de données actuellement dans un regroupement personnalisé de hello.

## <a name="tooset-hello-elastic-database-jobs-connection"></a>tooset hello connexion des travaux de base de données élastique
Une connexion a besoin de définir des travaux de toohello toobe *base de données de contrôle* toousing préalable hello travaux API. Cette applet de commande en cours d’exécution déclenche un toopop de la fenêtre d’informations d’identification de la demande de nom d’utilisateur hello et le mot de passe créé lors de l’installation des travaux de base de données élastique. Tous les exemples fournis dans cette rubrique partent du principe que cette première étape a déjà été effectuée.

Ouvrir une base de données élastique toohello connexion :

    Use-AzureSqlJobConnection -CurrentAzureSubscription 

## <a name="encrypted-credentials-within-hello-elastic-database-jobs"></a>Informations d’identification chiffrées dans les travaux de base de données élastique hello
Informations d’identification de la base de données peuvent être insérées dans les travaux de hello *base de données contrôle* avec son mot de passe chiffré. Il est nécessaire de toostore informations d’identification tooenable travaux toobe exécutée ultérieurement, (à l’aide de planifications de travaux).

Le chiffrement fonctionne via un certificat créé dans le cadre du script d’installation hello. script d’installation Hello crée et téléchargements hello certificat hello Azure Cloud Service pour le déchiffrement de hello stockée mots de passe chiffrés. Bonjour Azure Cloud Service ultérieurement stocke la clé publique de hello dans les travaux de hello *base de données contrôle* qui permet l’interface de PowerShell API ou le portail classique Azure hello tooencrypt un mot de passe fourni sans nécessiter le certificat de hello toobe installé localement.

les mots de passe Hello d’informations d’identification sont chiffrées et sécurisée des utilisateurs avec accès en lecture seule tooElastic de base de données travaux des objets. Mais il est possible pour un utilisateur malveillant avec accès en lecture-écriture tooElastic travaux de base de données objets tooextract un mot de passe. Informations d’identification sont conçu toobe réutilisée dans les exécutions de travaux. Informations d’identification sont passées des bases de données tootarget lors de l’établissement de connexions. Il n’existe actuellement aucune restriction sur les bases de données cibles hello utilisés pour chaque information d’identification, l’utilisateur malveillant pourrait ajouter une cible de la base de données pour une base de données sous contrôle de l’utilisateur malveillant hello. utilisateur de Hello par la suite a pu démarrer un travail de ciblage de mot de passe de cette base de données toogain hello informations d’identification.

Voici quelques bonnes pratiques de sécurité pour les tâches de bases de données élastiques :

* Limiter l’utilisation de personnes de tootrusted API hello.
* Informations d’identification doivent avoir hello moins tâche hello tooperform nécessaire des privilèges.  Pour plus d’informations, consultez l’article MSDN [Autorisations](https://msdn.microsoft.com/library/bb669084.aspx) sur SQL Server.

### <a name="toocreate-an-encrypted-credential-for-job-execution-across-databases"></a>toocreate informations d’identification chiffrées pour l’exécution du travail entre les bases de données
toocreate une nouvelle chiffrée des informations d’identification, hello [ **applet de commande Get-Credential** ](https://technet.microsoft.com/library/hh849815.aspx) vous invite à spécifier un nom d’utilisateur et un mot de passe qui peut être passée toohello [ **AzureSqlJobCredential de nouveau applet de commande**](/powershell/module/elasticdatabasejobs/new-azuresqljobcredential).

    $credentialName = "{Credential Name}"
    $databaseCredential = Get-Credential
    $credential = New-AzureSqlJobCredential -Credential $databaseCredential -CredentialName $credentialName
    Write-Output $credential

### <a name="tooupdate-credentials"></a>informations d’identification tooupdate
Lors de la modification de mots de passe, utilisez hello [ **applet de commande Set-AzureSqlJobCredential** ](/powershell/module/elasticdatabasejobs/set-azuresqljobcredential) et ensemble hello **CredentialName** paramètre.

    $credentialName = "{Credential Name}"
    Set-AzureSqlJobCredential -CredentialName $credentialName -Credential $credential 

## <a name="toodefine-an-elastic-database-shard-map-target"></a>toodefine une cible de carte de partitions de base de données élastique
tooexecute une tâche sur toutes les bases de données dans un ensemble de partitions (créé à l’aide de [bibliothèque cliente de base de données élastique](sql-database-elastic-database-client-library.md)), utilisez une carte de partitions en tant que cible de base de données hello. Cet exemple requiert une application partitionnée créée à l’aide de la bibliothèque cliente de base de données élastique hello. Voir [Prise en main des outils de base de données élastique](sql-database-elastic-scale-get-started.md).

base de données du gestionnaire Hello partition carte doit être défini en tant que base de données cible et puis carte de partitions spécifiques de hello doit être spécifié en tant que cible.

    $shardMapCredentialName = "{Credential Name}"
    $shardMapDatabaseName = "{ShardMapDatabaseName}" #example: ElasticScaleStarterKit_ShardMapManagerDb
    $shardMapDatabaseServerName = "{ShardMapServerName}"
    $shardMapName = "{MyShardMap}" #example: CustomerIDShardMap
    $shardMapDatabaseTarget = New-AzureSqlJobTarget -DatabaseName $shardMapDatabaseName -ServerName $shardMapDatabaseServerName
    $shardMapTarget = New-AzureSqlJobTarget -ShardMapManagerCredentialName $shardMapCredentialName -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapDatabaseServerName -ShardMapName $shardMapName
    Write-Output $shardMapTarget

## <a name="create-a-t-sql-script-for-execution-across-databases"></a>Créez un script T-SQL pour l’exécuter sur des bases de données
Lorsque vous créez des scripts T-SQL pour l’exécution, il est vivement recommandé de toobuild les toobe [idempotent](https://en.wikipedia.org/wiki/Idempotence) et résilientes contre les défaillances. Les travaux de base de données élastiques effectuera une nouvelle tentative d’exécution d’un script chaque fois que l’exécution rencontre une défaillance, quelle que soit la classification hello de défaillance de hello.

Hello d’utilisation [ **applet de commande New-AzureSqlJobContent** ](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent) toocreate et enregistrer un script pour l’exécution et définir hello **- ContentName** et **- CommandText**paramètres.

    $scriptName = "Create a TestTable"

    $scriptCommandText = "
    IF NOT EXISTS (SELECT name FROM sys.tables WHERE name = 'TestTable')
    BEGIN
        CREATE TABLE TestTable(
            TestTableId INT PRIMARY KEY IDENTITY,
            InsertionTime DATETIME2
        );
    END
    GO
    INSERT INTO TestTable(InsertionTime) VALUES (sysutcdatetime());
    GO"

    $script = New-AzureSqlJobContent -ContentName $scriptName -CommandText $scriptCommandText
    Write-Output $script

### <a name="create-a-new-script-from-a-file"></a>Créer un script à partir d'un fichier
Si hello script T-SQL est définie dans un fichier, utilisez ce script de hello tooimport :

    $scriptName = "My Script Imported from a File"
    $scriptPath = "{Path tooSQL File}"
    $scriptCommandText = Get-Content -Path $scriptPath
    $script = New-AzureSqlJobContent -ContentName $scriptName -CommandText $scriptCommandText
    Write-Output $script

### <a name="tooupdate-a-t-sql-script-for-execution-across-databases"></a>script tooupdate T-SQL pour l’exécution entre bases de données
Cette mise à jour du script PowerShell hello texte de la commande T-SQL pour un script existant.

Hello ensemble définition toobe ensemble de variables tooreflect hello souhaité script suivant :

    $scriptName = "Create a TestTable"
    $scriptUpdateComment = "Adding AdditionalInformation column tooTestTable"
    $scriptCommandText = "
    IF NOT EXISTS (SELECT name FROM sys.tables WHERE name = 'TestTable')
    BEGIN
    CREATE TABLE TestTable(
        TestTableId INT PRIMARY KEY IDENTITY,
        InsertionTime DATETIME2
    );
    END
    GO

    IF NOT EXISTS (SELECT columns.name FROM sys.columns INNER JOIN sys.tables on columns.object_id = tables.object_id WHERE tables.name = 'TestTable' AND columns.name = 'AdditionalInformation')
    BEGIN
    ALTER TABLE TestTable
    ADD AdditionalInformation NVARCHAR(400);
    END
    GO

    INSERT INTO TestTable(InsertionTime, AdditionalInformation) VALUES (sysutcdatetime(), 'test');
    GO"

### <a name="tooupdate-hello-definition-tooan-existing-script"></a>script de tooan de définition hello tooupdate existant
    Set-AzureSqlJobContentDefinition -ContentName $scriptName -CommandText $scriptCommandText -Comment $scriptUpdateComment 

## <a name="toocreate-a-job-tooexecute-a-script-across-a-shard-map"></a>toocreate un tooexecute de travail un script sur une carte de partitions
Ce script PowerShell démarre une tâche pour l’exécution d’un script sur chaque partition dans la carte de partitions d’une infrastructure élastique.

Hello ensemble suivant hello tooreflect de variables souhaitée de script et la cible :

    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $credentialName = "{Credential Name}"
    $shardMapTarget = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName 
    $job = New-AzureSqlJob -ContentName $scriptName -CredentialName $credentialName -JobName $jobName -TargetId $shardMapTarget.TargetId
    Write-Output $job

## <a name="tooexecute-a-job"></a>tooexecute un travail
Ce script PowerShell exécute une tâche existante :

Mettre à jour hello suivant tooreflect variable hello souhaité travail nom toohave exécutée :

    $jobName = "{Job Name}"
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName 
    Write-Output $jobExecution

## <a name="tooretrieve-hello-state-of-a-single-job-execution"></a>état de hello tooretrieve de l’exécution d’une tâche unique
Hello d’utilisation [ **applet de commande Get-AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/get-azuresqljobexecution) et ensemble hello **JobExecutionId** état de hello tooview de paramètre de l’exécution du travail.

    $jobExecutionId = "{Job Execution Id}"
    $jobExecution = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId
    Write-Output $jobExecution

Utilisez hello même **Get-AzureSqlJobExecution** applet de commande avec hello **IncludeChildren** état de hello tooview paramètre d’exécutions de travail enfant, hello à savoir un état spécifique pour chaque exécution du travail sur chaque base de données ciblée par le travail de hello.

    $jobExecutionId = "{Job Execution Id}"
    $jobExecutions = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId -IncludeChildren
    Write-Output $jobExecutions 

## <a name="tooview-hello-state-across-multiple-job-executions"></a>état de hello tooview sur plusieurs exécutions du travail
Hello [ **applet de commande Get-AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/new-azuresqljob) ayant plusieurs paramètres facultatifs qui peuvent être utilisé toodisplay plusieurs exécutions du travail, filtrées par le biais des paramètres de hello fourni. suivant de Hello présente quelques-unes des façons possibles de hello toouse Get-AzureSqlJobExecution :

Récupérez toutes les exécutions de tâches de niveau supérieur actives :

    Get-AzureSqlJobExecution

Récupérez toutes les exécutions de tâches de niveau supérieur, y compris les exécutions de tâches inactives :

    Get-AzureSqlJobExecution -IncludeInactive

Récupérez toutes les exécutions de tâches enfants d'un ID d'exécution de tâches fourni, y compris les exécutions de tâches inactives :

    $parentJobExecutionId = "{Job Execution Id}"
    Get-AzureSqlJobExecution -AzureSqlJobExecution -JobExecutionId $parentJobExecutionId -IncludeInactive -IncludeChildren

Récupérez toutes les exécutions de tâches créées à l'aide d'une planification/combinaison de tâches, y compris les tâches inactives :

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Get-AzureSqlJobExecution -JobName $jobName -ScheduleName $scheduleName -IncludeInactive

Récupérez toutes les tâches ciblant une carte de partitions spécifiée, y compris les tâches inactives :

    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $target = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive

Récupérez toutes les tâches ciblant une collecte personnalisée spécifiée, y compris les tâches inactives :

    $customCollectionName = "{Custom Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive

Récupérer la liste de hello d’exécutions de tâches de travail au sein de l’exécution d’une tâche spécifique :

    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Write-Output $jobTaskExecutions 

Récupérez les détails d’exécution de tâches de travail :

Hello PowerShell script suivant peut être utilisé tooview les détails de hello une tâche d’exécution des tâches, qui est particulièrement utile lors du débogage des erreurs d’exécution.

    $jobTaskExecutionId = "{Job Task Execution Id}"
    $jobTaskExecution = Get-AzureSqlJobTaskExecution -JobTaskExecutionId $jobTaskExecutionId
    Write-Output $jobTaskExecution

## <a name="tooretrieve-failures-within-job-task-executions"></a>échecs de tooretrieve dans les exécutions de tâches de travail
Hello **JobTaskExecution objet** inclut une propriété pour hello du cycle de vie de la tâche hello avec une propriété de message. Si une exécution de tâches de travail a échoué, propriété de cycle de vie hello sera définie trop*n’a pas pu* et propriété de message hello sera définie message d’exception résultant toohello et sa pile. Si une tâche n’a pas réussi, il est important tooview les détails de hello des tâches de travail qui n’a pas réussi pour un travail donné.

    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Foreach($jobTaskExecution in $jobTaskExecutions) 
        {
        if($jobTaskExecution.Lifecycle -ne 'Succeeded')
            {
            Write-Output $jobTaskExecution
            }
        }

## <a name="toowait-for-a-job-execution-toocomplete"></a>toowait pour un toocomplete de l’exécution du travail
Hello PowerShell script suivant peut être utilisé toowait pour un toocomplete de tâche de travail :

    $jobExecutionId = "{Job Execution Id}"
    Wait-AzureSqlJobExecution -JobExecutionId $jobExecutionId 

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

    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 10
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $executionPolicy = New-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval 
    -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $executionPolicy

### <a name="update-a-custom-execution-policy"></a>Mettez à jour une stratégie d'exécution personnalisée
Hello de mise à jour souhaitée tooupdate de stratégie d’exécution :

    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 15
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $updatedExecutionPolicy = Set-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $updatedExecutionPolicy

## <a name="cancel-a-job"></a>Annulation d’une tâche
La fonctionnalité Tâches de bases de données élastiques prend en charge les demandes d'annulation de tâches.  Si les travaux de base de données élastique détecte une demande d’annulation d’une tâche en cours d’exécution, il tentera de travail de hello toostop.

La fonctionnalité Tâches de bases de données élastiques peut effectuer une annulation de deux manières différentes :

1. Annuler les tâches en cours d’exécution : si une annulation est détectée pendant une tâche est en cours d’exécution, l’annulation sera tentée dans hello aspect de la tâche hello en cours d’exécution.  Par exemple : en l’absence d’une requête longue en cours d’exécution lorsqu’une annulation est tentée, il y aura une requête de hello toocancel tentative.
2. L’annulation de nouvelles tentatives de tâche : si une annulation est détectée par le thread de contrôle hello avant de lancer une tâche pour l’exécution, thread de contrôle hello éviter de lancer la tâche hello et déclarer la demande de hello comme annulée.

Si une annulation de tâche est demandée pour un travail parent, demande d’annulation hello sera respectée pour la tâche parente de hello et pour toutes ses tâches enfants.

toosubmit une demande d’annulation, utilisez hello [ **applet de commande Stop-AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) et ensemble hello **JobExecutionId** paramètre.

    $jobExecutionId = "{Job Execution Id}"
    Stop-AzureSqlJobExecution -JobExecutionId $jobExecutionId

## <a name="toodelete-a-job-and-job-history-asynchronously"></a>toodelete une tâche et l’historique des travaux en mode asynchrone
Tâches de bases de données élastiques prend en charge la suppression des tâches asynchrone. Un travail peut être marqué pour suppression et hello système supprime le travail de hello et son historique une fois que toutes les exécutions de la tâche s’est terminé pour le travail de hello. système de Hello n’est pas automatiquement annulé exécutions de travail actif.  

Appeler [ **Stop-AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) toocancel les exécutions de travail actif.

suppression du travail tootrigger, utilisez hello [ **applet de commande Remove-AzureSqlJob** ](/powershell/module/elasticdatabasejobs/remove-azuresqljob) et ensemble hello **JobName** paramètre.

    $jobName = "{Job Name}"
    Remove-AzureSqlJob -JobName $jobName

## <a name="toocreate-a-custom-database-target"></a>toocreate une cible de la base de données personnalisée
Vous pouvez définir des cibles de bases de données personnalisées pour une exécution directe ou pour une inclusion dans un groupe de bases de données personnalisées. Par exemple, étant donné que **pools élastiques** sont pas encore directement pris en charge à l’aide de PowerShell APIs, vous pouvez créer une cible de la base de données personnalisée et la cible de collection de base de données personnalisée qui englobe toutes les bases de données hello dans le pool de hello.

Définissez hello suit les informations de base de données de variables tooreflect hello souhaité :

    $databaseName = "{Database Name}"
    $databaseServerName = "{Server Name}"
    New-AzureSqlJobDatabaseTarget -DatabaseName $databaseName -ServerName $databaseServerName 

## <a name="toocreate-a-custom-database-collection-target"></a>toocreate une cible de collection de base de données personnalisée
Hello d’utilisation [ **New-AzureSqlJobTarget** ](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) toodefine de l’applet de commande de base de données personnalisée collection cible tooenable l’exécution d’une sur plusieurs cibles de base de données. Après avoir créé un groupe de la base de données, les bases de données peuvent être associés à la cible de collection personnalisée hello.

Définissez hello variables tooreflect hello collection personnalisée souhaitée cible configuration suivante :

    $customCollectionName = "{Custom Database Collection Name}"
    New-AzureSqlJobTarget -CustomCollectionName $customCollectionName 

### <a name="tooadd-databases-tooa-custom-database-collection-target"></a>cible de collecte des base de données personnalisée tooa tooadd bases de données
tooadd un regroupement personnalisé spécifique de base de données tooa utiliser hello [ **Add-AzureSqlJobChildTarget** ](/powershell/module/elasticdatabasejobs/add-azuresqljobchildtarget) applet de commande.

    $databaseServerName = "{Database Server Name}"
    $databaseName = "{Database Name}"
    $customCollectionName = "{Custom Database Collection Name}"
    Add-AzureSqlJobChildTarget -CustomCollectionName $customCollectionName -DatabaseName $databaseName -ServerName $databaseServerName 

#### <a name="review-hello-databases-within-a-custom-database-collection-target"></a>Passez en revue les bases de données hello dans une cible de collection de base de données personnalisée
Hello d’utilisation [ **Get-AzureSqlJobTarget** ](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) applet de commande tooretrieve hello enfant bases de données d’une cible de collection de base de données personnalisée. 

    $customCollectionName = "{Custom Database Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $childTargets = Get-AzureSqlJobTarget -ParentTargetId $target.TargetId
    Write-Output $childTargets

### <a name="create-a-job-tooexecute-a-script-across-a-custom-database-collection-target"></a>Créer un travail tooexecute un script sur une cible de collection personnalisé de la base de données
Hello d’utilisation [ **New-AzureSqlJob** ](/powershell/module/elasticdatabasejobs/new-azuresqljob) toocreate de l’applet de commande un travail par rapport à un groupe de bases de données définies par une cible de collection de base de données personnalisée. Les travaux de base de données élastiques développera les travaux hello en plusieurs tâches enfants chaque base de données tooa correspondante associée cible de collecte de base de données personnalisée hello et assurez-vous que le script de hello est exécutée sur chaque base de données. Là encore, il est important que les scripts sont tooretries résilient de toobe idempotent.

    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $customCollectionName = "{Custom Collection Name}"
    $credentialName = "{Credential Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job

## <a name="data-collection-across-databases"></a>Collecte de données sur les bases de données
Vous pouvez utiliser un travail de tooexecute une requête sur un groupe de bases de données et envoyer hello tooa spécifiques résultant. table de Hello peut être interrogée après les résultats de la requête hello hello faits toosee à partir de chaque base de données. Cela fournit une méthode asynchrone de tooexecute d’une requête entre plusieurs bases de données. Les tentatives ayant échoué sont gérées automatiquement par l’exécution de nouvelles tentatives.

table de destination spécifiée Hello sera automatiquement créée si elle n’existe pas encore. nouvelle table de Hello correspond au schéma hello Hello retourné de jeu de résultats. Si un script retourne plusieurs jeux de résultats, les tâches de base de données élastique n’envoie première table de destination toohello hello.

Bonjour script PowerShell suivant exécute un script et collecte ses résultats dans une table spécifiée. Ce script part du principe qu’un script T-SQL, qui génère un jeu de résultats unique, et une cible de collecte de base de données personnalisée ont été créés.

Ce script utilise hello [ **Get-AzureSqlJobTarget** ](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) applet de commande. Définir les paramètres de hello pour le script, informations d’identification et la cible de l’exécution :

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

### <a name="toocreate-and-start-a-job-for-data-collection-scenarios"></a>toocreate et démarrer un travail pour les scénarios de collecte de données
Ce script utilise hello [ **Start-AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/start-azuresqljobexecution) applet de commande.

    $job = New-AzureSqlJob -JobName $jobName 
    -CredentialName $executionCredentialName 
    -ContentName $scriptName 
    -ResultSetDestinationServerName $destinationServerName 
    -ResultSetDestinationDatabaseName $destinationDatabaseName 
    -ResultSetDestinationSchemaName $destinationSchemaName 
    -ResultSetDestinationTableName $destinationTableName 
    -ResultSetDestinationCredentialName $destinationCredentialName 
    -TargetId $target.TargetId
    Write-Output $job
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName
    Write-Output $jobExecution

## <a name="tooschedule-a-job-execution-trigger"></a>tooschedule un déclencheur de l’exécution du travail
Hello PowerShell script suivant peut être utilisé toocreate une planification périodique. Ce script utilise un intervalle de minutes, mais [**New-AzureSqlJobSchedule**](/powershell/module/elasticdatabasejobs/new-azuresqljobschedule) prend également en charge les paramètres -DayInterval, - HourInterval, - MonthInterval et - WeekInterval. Les planifications qui ne s'exécutent qu'une seule fois peuvent être créées en transmettant  - OneTime.

Créez une nouvelle planification :

    $scheduleName = "Every one minute"
    $minuteInterval = 1
    $startTime = (Get-Date).ToUniversalTime()
    $schedule = New-AzureSqlJobSchedule 
    -MinuteInterval $minuteInterval 
    -ScheduleName $scheduleName 
    -StartTime $startTime 
    Write-Output $schedule

### <a name="tootrigger-a-job-executed-on-a-time-schedule"></a>tootrigger une tâche s’exécutée selon une planification
Un déclencheur de tâche peut être défini toohave un travail exécuté conformément tooa Calendrier. Hello PowerShell script suivant peut être utilisé toocreate un déclencheur de tâche.

Utilisez [New-AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/new-azuresqljobtrigger) et en jeu hello suivant variables toocorrespond toohello souhaitée travail et planification :

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    $jobTrigger = New-AzureSqlJobTrigger
    -ScheduleName $scheduleName
    -JobName $jobName
    Write-Output $jobTrigger

### <a name="tooremove-a-scheduled-association-toostop-job-from-executing-on-schedule"></a>tooremove un travail de toostop association planifiée à partir de l’exécution de la planification
toodiscontinue qui se reproduit l’exécution du travail via un déclencheur de tâche, le déclencheur de tâche hello peut être supprimée. Supprimer un toostop de déclencheur de tâche un travail à partir d’en cours d’exécution en fonction tooa planification, à l’aide de hello [ **applet de commande Remove-AzureSqlJobTrigger**](/powershell/module/elasticdatabasejobs/remove-azuresqljobtrigger).

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Remove-AzureSqlJobTrigger 
    -ScheduleName $scheduleName 
    -JobName $jobName

### <a name="retrieve-job-triggers-bound-tooa-time-schedule"></a>Récupérer la planification de temps de travail déclencheurs tooa liée
Hello PowerShell script suivant peut être tooobtain utilisé et afficher les hello planning déclencheurs tooa inscrits moment donné.

    $scheduleName = "{Schedule Name}"
    $jobTriggers = Get-AzureSqlJobTrigger -ScheduleName $scheduleName
    Write-Output $jobTriggers

### <a name="tooretrieve-job-triggers-bound-tooa-job"></a>les déclencheurs de tâche tooretrieve lié tooa travail
Utilisez [Get-AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/get-azuresqljobtrigger) tooobtain et affichage des planifications contenant un travail inscrit.

    $jobName = "{Job Name}"
    $jobTriggers = Get-AzureSqlJobTrigger -JobName $jobName
    Write-Output $jobTriggers

## <a name="toocreate-a-data-tier-application-dacpac-for-execution-across-databases"></a>toocreate une application de couche données (DACPAC) pour l’exécution entre bases de données
toocreate un DACPAC, consultez [applications de couche données](https://msdn.microsoft.com/library/ee210546.aspx). toodeploy un DACPAC, utilisez hello [applet de commande New-AzureSqlJobContent](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent). Hello DACPAC doit être accessible toohello service. Il est recommandé tooupload un tooAzure DACPAC créé stockage et de créer un [Signature d’accès partagé](../storage/common/storage-dotnet-shared-access-signature-part-1.md) pour hello DACPAC.

    $dacpacUri = "{Uri}"
    $dacpacName = "{Dacpac Name}"
    $dacpac = New-AzureSqlJobContent -DacpacUri $dacpacUri -ContentName $dacpacName 
    Write-Output $dacpac

### <a name="tooupdate-a-data-tier-application-dacpac-for-execution-across-databases"></a>tooupdate une application de couche données (DACPAC) pour l’exécution entre bases de données
Dacpac existantes, enregistrées dans les travaux de base de données élastique peut être mis à jour toopoint toonew URI. Hello d’utilisation [ **applet de commande Set-AzureSqlJobContentDefinition** ](/powershell/module/elasticdatabasejobs/set-azuresqljobcontentdefinition) tooupdate hello DACPAC URI sur existant enregistré DACPAC :

    $dacpacName = "{Dacpac Name}"
    $newDacpacUri = "{Uri}"
    $updatedDacpac = Set-AzureSqlJobDacpacDefinition -ContentName $dacpacName -DacpacUri $newDacpacUri
    Write-Output $updatedDacpac

## <a name="toocreate-a-job-tooapply-a-data-tier-application-dacpac-across-databases"></a>toocreate un tooapply de travail une application de couche données (DACPAC) sur les bases de données
Une fois un DACPAC a été créé dans les tâches de base de données élastique, un travail peut être créé tooapply hello DACPAC sur un groupe de bases de données. Hello PowerShell script suivant peut être utilisé toocreate un travail DACPAC sur un regroupement personnalisé des bases de données :

    $jobName = "{Job Name}"
    $dacpacName = "{Dacpac Name}"
    $customCollectionName = "{Custom Collection Name}"
    $credentialName = "{Credential Name}"
    $target = Get-AzureSqlJobTarget 
    -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob 
    -JobName $jobName 
    -CredentialName $credentialName 
    -ContentName $dacpacName -TargetId $target.TargetId
    Write-Output $job 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-powershell/cmd-prompt.png
[2]: ./media/sql-database-elastic-jobs-powershell/portal.png
<!--anchors-->
