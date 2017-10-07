---
title: "code du fichier d’événements pour la base de données SQL d’aaaXEvent | Documents Microsoft"
description: "Fournit de PowerShell et Transact-SQL pour obtenir un exemple de code en deux phases qui montre la cible de fichier d’événements hello dans un événement étendu sur la base de données SQL Azure. Le service Azure Storage est nécessaire pour ce scénario."
services: sql-database
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
tags: 
ms.assetid: bbb10ecc-739f-4159-b844-12b4be161231
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: genemi
ms.openlocfilehash: 4457bd3250f4644b54da2f7daddb9da12070e93a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="event-file-target-code-for-extended-events-in-sql-database"></a><span data-ttu-id="0c4cd-104">Code cible du fichier d’événements pour les événements étendus dans SQL Database</span><span class="sxs-lookup"><span data-stu-id="0c4cd-104">Event File target code for extended events in SQL Database</span></span>

[!INCLUDE [sql-database-xevents-selectors-1-include](../../includes/sql-database-xevents-selectors-1-include.md)]

<span data-ttu-id="0c4cd-105">Vous souhaitez un exemple de code complet pour une façon fiable toocapture et fournir les informations pour un événement étendu.</span><span class="sxs-lookup"><span data-stu-id="0c4cd-105">You want a complete code sample for a robust way toocapture and report information for an extended event.</span></span>

<span data-ttu-id="0c4cd-106">Dans Microsoft SQL Server, hello [cible du fichier de l’événement](http://msdn.microsoft.com/library/ff878115.aspx) est sorties d’événement toostore utilisé dans un fichier de disque dur local.</span><span class="sxs-lookup"><span data-stu-id="0c4cd-106">In Microsoft SQL Server, hello [Event File target](http://msdn.microsoft.com/library/ff878115.aspx) is used toostore event outputs into a local hard drive file.</span></span> <span data-ttu-id="0c4cd-107">Mais ces fichiers ne sont pas disponible tooAzure de base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="0c4cd-107">But such files are not available tooAzure SQL Database.</span></span> <span data-ttu-id="0c4cd-108">Au lieu de cela, nous utilisons cible de fichier d’événements du service toosupport hello hello le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="0c4cd-108">Instead we use hello Azure Storage service toosupport hello Event File target.</span></span>

<span data-ttu-id="0c4cd-109">Cette rubrique présente un exemple de code en deux phases :</span><span class="sxs-lookup"><span data-stu-id="0c4cd-109">This topic presents a two-phase code sample:</span></span>

* <span data-ttu-id="0c4cd-110">PowerShell, toocreate un conteneur de stockage Azure dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="0c4cd-110">PowerShell, toocreate an Azure Storage container in hello cloud.</span></span>
* <span data-ttu-id="0c4cd-111">Transact-SQL :</span><span class="sxs-lookup"><span data-stu-id="0c4cd-111">Transact-SQL:</span></span>
  
  * <span data-ttu-id="0c4cd-112">tooassign hello Azure Storage conteneur tooan événement cible du fichier.</span><span class="sxs-lookup"><span data-stu-id="0c4cd-112">tooassign hello Azure Storage container tooan Event File target.</span></span>
  * <span data-ttu-id="0c4cd-113">session d’événements hello toocreate et démarrer et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="0c4cd-113">toocreate and start hello event session, and so on.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0c4cd-114">Composants requis</span><span class="sxs-lookup"><span data-stu-id="0c4cd-114">Prerequisites</span></span>

* <span data-ttu-id="0c4cd-115">Un compte et un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="0c4cd-115">An Azure account and subscription.</span></span> <span data-ttu-id="0c4cd-116">Vous pouvez vous inscrire à un [essai gratuit](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0c4cd-116">You can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="0c4cd-117">Une base de données dans laquelle vous pouvez créer une table.</span><span class="sxs-lookup"><span data-stu-id="0c4cd-117">Any database you can create a table in.</span></span>
  
  * <span data-ttu-id="0c4cd-118">Vous pouvez aussi [créer une base de données de démonstration **AdventureWorksLT**](sql-database-get-started.md) en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="0c4cd-118">Optionally you can [create an **AdventureWorksLT** demonstration database](sql-database-get-started.md) in minutes.</span></span>
* <span data-ttu-id="0c4cd-119">SQL Server Management Studio (ssms.exe), dans l’idéal, la version de sa dernière mise à jour mensuelle.</span><span class="sxs-lookup"><span data-stu-id="0c4cd-119">SQL Server Management Studio (ssms.exe), ideally its latest monthly update version.</span></span> 
  <span data-ttu-id="0c4cd-120">Vous pouvez télécharger hello ssms.exe plus récentes à partir de :</span><span class="sxs-lookup"><span data-stu-id="0c4cd-120">You can download hello latest ssms.exe from:</span></span>
  
  * <span data-ttu-id="0c4cd-121">À partir de la rubrique [Télécharger SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="0c4cd-121">Topic titled [Download SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).</span></span>
  * [<span data-ttu-id="0c4cd-122">Un téléchargement de toohello lien direct.</span><span class="sxs-lookup"><span data-stu-id="0c4cd-122">A direct link toohello download.</span></span>](http://go.microsoft.com/fwlink/?linkid=616025)
* <span data-ttu-id="0c4cd-123">Vous devez avoir hello [modules Azure PowerShell](http://go.microsoft.com/?linkid=9811175) installé.</span><span class="sxs-lookup"><span data-stu-id="0c4cd-123">You must have hello [Azure PowerShell modules](http://go.microsoft.com/?linkid=9811175) installed.</span></span>
  
  * <span data-ttu-id="0c4cd-124">modules de Hello fournissent des commandes telles que - **New-AzureStorageAccount**.</span><span class="sxs-lookup"><span data-stu-id="0c4cd-124">hello modules provide commands such as - **New-AzureStorageAccount**.</span></span>

## <a name="phase-1-powershell-code-for-azure-storage-container"></a><span data-ttu-id="0c4cd-125">Phase 1 : code PowerShell pour le conteneur Azure Storage</span><span class="sxs-lookup"><span data-stu-id="0c4cd-125">Phase 1: PowerShell code for Azure Storage container</span></span>

<span data-ttu-id="0c4cd-126">Cette PowerShell est la phase 1 de l’exemple de code en deux phases hello.</span><span class="sxs-lookup"><span data-stu-id="0c4cd-126">This PowerShell is phase 1 of hello two-phase code sample.</span></span>

<span data-ttu-id="0c4cd-127">script de Hello démarre avec les commandes tooclean après un éventuel précédent est rerunnable.</span><span class="sxs-lookup"><span data-stu-id="0c4cd-127">hello script starts with commands tooclean up after a possible previous run, and is rerunnable.</span></span>

1. <span data-ttu-id="0c4cd-128">Collez le script PowerShell de hello dans un simple éditeur de texte tel que Notepad.exe, enregistrez le script de hello en tant que fichier avec l’extension de hello **.ps1**.</span><span class="sxs-lookup"><span data-stu-id="0c4cd-128">Paste hello PowerShell script into a simple text editor such as Notepad.exe, and save hello script as a file with hello extension **.ps1**.</span></span>
2. <span data-ttu-id="0c4cd-129">Démarrez PowerShell ISE en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="0c4cd-129">Start PowerShell ISE as an Administrator.</span></span>
3. <span data-ttu-id="0c4cd-130">À l’invite de hello, tapez</span><span class="sxs-lookup"><span data-stu-id="0c4cd-130">At hello prompt, type</span></span><br/>`Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Scope CurrentUser`<br/><span data-ttu-id="0c4cd-131">et appuyez sur Entrée.</span><span class="sxs-lookup"><span data-stu-id="0c4cd-131">and then press Enter.</span></span>
4. <span data-ttu-id="0c4cd-132">Dans PowerShell ISE, ouvrez votre fichier **.ps1** .</span><span class="sxs-lookup"><span data-stu-id="0c4cd-132">In PowerShell ISE, open your **.ps1** file.</span></span> <span data-ttu-id="0c4cd-133">Exécutez le script de hello.</span><span class="sxs-lookup"><span data-stu-id="0c4cd-133">Run hello script.</span></span>
5. <span data-ttu-id="0c4cd-134">script de Hello commence une nouvelle fenêtre dans laquelle vous vous connectez tooAzure.</span><span class="sxs-lookup"><span data-stu-id="0c4cd-134">hello script first starts a new window in which you log in tooAzure.</span></span>
   
   * <span data-ttu-id="0c4cd-135">Si vous réexécutez le script de hello sans interrompre votre session, vous pouvez hello pratique commenté hello **Add-AzureAccount** commande.</span><span class="sxs-lookup"><span data-stu-id="0c4cd-135">If you rerun hello script without disrupting your session, you have hello convenient option of commenting out hello **Add-AzureAccount** command.</span></span>

![PowerShell ISE, avec le module Windows Azure installé, prêt toorun script.][30_powershell_ise]


### <a name="powershell-code"></a><span data-ttu-id="0c4cd-137">Code PowerShell</span><span class="sxs-lookup"><span data-stu-id="0c4cd-137">PowerShell code</span></span>

```powershell
## TODO: Before running, find all 'TODO' and make each edit!!

#--------------- 1 -----------------------


# You can comment out or skip this Add-AzureAccount
# command after hello first run.
# Current PowerShell environment retains hello successful outcome.

'Expect a pop-up window in which you log in tooAzure.'


Add-AzureAccount

#-------------- 2 ------------------------


'
TODO: Edit hello values assigned toothese variables, especially hello first few!
'

# Ensure hello current date is between
# hello Expiry and Start time values that you edit here.

$subscriptionName    = 'YOUR_SUBSCRIPTION_NAME'
$policySasExpiryTime = '2016-01-28T23:44:56Z'
$policySasStartTime  = '2015-08-01'


$storageAccountName     = 'gmstorageaccountxevent'
$storageAccountLocation = 'West US'
$contextName            = 'gmcontext'
$containerName          = 'gmcontainerxevent'
$policySasToken         = 'gmpolicysastoken'


# Leave this value alone, as 'rwl'.
$policySasPermission = 'rwl'

#--------------- 3 -----------------------


# hello ending display lists your Azure subscriptions.
# One should match hello $subscriptionName value you assigned
#   earlier in this PowerShell script. 

'Choose an existing subscription for hello current PowerShell environment.'


Select-AzureSubscription -SubscriptionName $subscriptionName


#-------------- 4 ------------------------


'
Clean up hello old Azure Storage Account after any previous run, 
before continuing this new run.'


If ($storageAccountName)
{
    Remove-AzureStorageAccount -StorageAccountName $storageAccountName
}

#--------------- 5 -----------------------

[System.DateTime]::Now.ToString()

'
Create a storage account. 
This might take several minutes, will beep when ready.
  ...PLEASE WAIT...'

New-AzureStorageAccount `
    -StorageAccountName $storageAccountName `
    -Location           $storageAccountLocation

[System.DateTime]::Now.ToString()

[System.Media.SystemSounds]::Beep.Play()


'
Get hello primary access key for your storage account.
'


$primaryAccessKey_ForStorageAccount = `
    (Get-AzureStorageKey `
        -StorageAccountName $storageAccountName).Primary

"`$primaryAccessKey_ForStorageAccount = $primaryAccessKey_ForStorageAccount"

'Azure Storage Account cmdlet completed.
Remainder of PowerShell .ps1 script continues.
'

#--------------- 6 -----------------------


# hello context will be needed toocreate a container within hello storage account.

'Create a context object from hello storage account and its primary access key.
'

$context = New-AzureStorageContext `
    -StorageAccountName $storageAccountName `
    -StorageAccountKey  $primaryAccessKey_ForStorageAccount


'Create a container within hello storage account.
'


$containerObjectInStorageAccount = New-AzureStorageContainer `
    -Name    $containerName `
    -Context $context


'Create a security policy toobe applied toohello SAS token.
'

New-AzureStorageContainerStoredAccessPolicy `
    -Container  $containerName `
    -Context    $context `
    -Policy     $policySasToken `
    -Permission $policySasPermission `
    -ExpiryTime $policySasExpiryTime `
    -StartTime  $policySasStartTime 

'
Generate a SAS token for hello container.
'
Try
{
    $sasTokenWithPolicy = New-AzureStorageContainerSASToken `
        -Name    $containerName `
        -Context $context `
        -Policy  $policySasToken
}
Catch 
{
    $Error[0].Exception.ToString()
}

#-------------- 7 ------------------------


'Display hello values that YOU must edit into hello Transact-SQL script next!:
'

"storageAccountName: $storageAccountName"
"containerName:      $containerName"
"sasTokenWithPolicy: $sasTokenWithPolicy"

'
REMINDER: sasTokenWithPolicy here might start with "?" character, which you must exclude from Transact-SQL.
'

'
(Later, return here toodelete your Azure Storage account. See hello preceding - Remove-AzureStorageAccount -StorageAccountName $storageAccountName)'

'
Now shift toohello Transact-SQL portion of hello two-part code sample!'

# EOFile
```


<span data-ttu-id="0c4cd-138">Prenez note de hello peu de valeurs nommées qui imprime de script PowerShell de hello lorsqu’elle se termine.</span><span class="sxs-lookup"><span data-stu-id="0c4cd-138">Take note of hello few named values that hello PowerShell script prints when it ends.</span></span> <span data-ttu-id="0c4cd-139">Vous devez modifier ces valeurs dans le script Transact-SQL qui suit en tant que la phase 2 de hello.</span><span class="sxs-lookup"><span data-stu-id="0c4cd-139">You must edit those values into hello Transact-SQL script that follows as phase 2.</span></span>

## <a name="phase-2-transact-sql-code-that-uses-azure-storage-container"></a><span data-ttu-id="0c4cd-140">Phase 2 : code Transact-SQL utilisant le conteneur Azure Storage</span><span class="sxs-lookup"><span data-stu-id="0c4cd-140">Phase 2: Transact-SQL code that uses Azure Storage container</span></span>

* <span data-ttu-id="0c4cd-141">Dans la phase 1 de cet exemple de code, vous avez exécuté une toocreate de script PowerShell un conteneur de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="0c4cd-141">In phase 1 of this code sample, you ran a PowerShell script toocreate an Azure Storage container.</span></span>
* <span data-ttu-id="0c4cd-142">Ensuite dans la phase 2, hello script Transact-SQL suivant doit utiliser le conteneur de hello.</span><span class="sxs-lookup"><span data-stu-id="0c4cd-142">Next in phase 2, hello following Transact-SQL script must use hello container.</span></span>

<span data-ttu-id="0c4cd-143">script de Hello démarre avec les commandes tooclean après un éventuel précédent est rerunnable.</span><span class="sxs-lookup"><span data-stu-id="0c4cd-143">hello script starts with commands tooclean up after a possible previous run, and is rerunnable.</span></span>

<span data-ttu-id="0c4cd-144">Hello script PowerShell imprime quelques valeurs nommées s’il est terminé.</span><span class="sxs-lookup"><span data-stu-id="0c4cd-144">hello PowerShell script printed a few named values when it ended.</span></span> <span data-ttu-id="0c4cd-145">Vous devez modifier hello Transact-SQL script toouse ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="0c4cd-145">You must edit hello Transact-SQL script toouse those values.</span></span> <span data-ttu-id="0c4cd-146">Rechercher **TODO** Bonjour de hello Transact-SQL script toolocate des points d’édition.</span><span class="sxs-lookup"><span data-stu-id="0c4cd-146">Find **TODO** in hello Transact-SQL script toolocate hello edit points.</span></span>

1. <span data-ttu-id="0c4cd-147">Ouvrez SQL Server Management Studio (ssms.exe).</span><span class="sxs-lookup"><span data-stu-id="0c4cd-147">Open SQL Server Management Studio (ssms.exe).</span></span>
2. <span data-ttu-id="0c4cd-148">Connecter la base de données de base de données SQL Azure tooyour.</span><span class="sxs-lookup"><span data-stu-id="0c4cd-148">Connect tooyour Azure SQL Database database.</span></span>
3. <span data-ttu-id="0c4cd-149">Cliquez sur tooopen un nouveau volet de requête.</span><span class="sxs-lookup"><span data-stu-id="0c4cd-149">Click tooopen a new query pane.</span></span>
4. <span data-ttu-id="0c4cd-150">Collez hello suivant le script Transact-SQL dans le volet de requête hello.</span><span class="sxs-lookup"><span data-stu-id="0c4cd-150">Paste hello following Transact-SQL script into hello query pane.</span></span>
5. <span data-ttu-id="0c4cd-151">Trouver toutes **TODO** hello script et apportez les modifications appropriées hello.</span><span class="sxs-lookup"><span data-stu-id="0c4cd-151">Find every **TODO** in hello script and make hello appropriate edits.</span></span>
6. <span data-ttu-id="0c4cd-152">Enregistrez et exécutez ensuite le script de hello.</span><span class="sxs-lookup"><span data-stu-id="0c4cd-152">Save, and then run hello script.</span></span>


> [!WARNING]
> <span data-ttu-id="0c4cd-153">valeur de la clé SAS généré par hello précédant le script PowerShell de Hello pourrait commencer par un ' ?' (point d’interrogation).</span><span class="sxs-lookup"><span data-stu-id="0c4cd-153">hello SAS key value generated by hello preceding PowerShell script might begin with a '?' (question mark).</span></span> <span data-ttu-id="0c4cd-154">Lorsque vous utilisez la clé SAS hello Bonjour script T-SQL suivant, vous devez *suppriment hello ' ?'* .</span><span class="sxs-lookup"><span data-stu-id="0c4cd-154">When you use hello SAS key in hello following T-SQL script, you must *remove hello leading '?'*.</span></span> <span data-ttu-id="0c4cd-155">Dans le cas contraire, vos efforts peuvent être bloqués par la sécurité.</span><span class="sxs-lookup"><span data-stu-id="0c4cd-155">Otherwise your efforts might be blocked by security.</span></span>


### <a name="transact-sql-code"></a><span data-ttu-id="0c4cd-156">Code Transact-SQL</span><span class="sxs-lookup"><span data-stu-id="0c4cd-156">Transact-SQL code</span></span>

```sql
---- TODO: First, run hello PowerShell portion of this two-part code sample.
---- TODO: Second, find every 'TODO' in this Transact-SQL file, and edit each.

---- Transact-SQL code for Event File target on Azure SQL Database.


SET NOCOUNT ON;
GO


----  Step 1.  Establish one little table, and  ---------
----  insert one row of data.


IF EXISTS
    (SELECT * FROM sys.objects
        WHERE type = 'U' and name = 'gmTabEmployee')
BEGIN
    DROP TABLE gmTabEmployee;
END
GO


CREATE TABLE gmTabEmployee
(
    EmployeeGuid         uniqueIdentifier   not null  default newid()  primary key,
    EmployeeId           int                not null  identity(1,1),
    EmployeeKudosCount   int                not null  default 0,
    EmployeeDescr        nvarchar(256)          null
);
GO


INSERT INTO gmTabEmployee ( EmployeeDescr )
    VALUES ( 'Jane Doe' );
GO


------  Step 2.  Create key, and  ------------
------  Create credential (your Azure Storage container must already exist).


IF NOT EXISTS
    (SELECT * FROM sys.symmetric_keys
        WHERE symmetric_key_id = 101)
BEGIN
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '0C34C960-6621-4682-A123-C7EA08E3FC46' -- Or any newid().
END
GO


IF EXISTS
    (SELECT * FROM sys.database_scoped_credentials
        -- TODO: Assign AzureStorageAccount name, and hello associated Container name.
        WHERE name = 'https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent')
BEGIN
    DROP DATABASE SCOPED CREDENTIAL
        -- TODO: Assign AzureStorageAccount name, and hello associated Container name.
        [https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent] ;
END
GO


CREATE
    DATABASE SCOPED
    CREDENTIAL
        -- use '.blob.',   and not '.queue.' or '.table.' etc.
        -- TODO: Assign AzureStorageAccount name, and hello associated Container name.
        [https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent]
    WITH
        IDENTITY = 'SHARED ACCESS SIGNATURE',  -- "SAS" token.
        -- TODO: Paste in hello long SasToken string here for Secret, but exclude any leading '?'.
        SECRET = 'sv=2014-02-14&sr=c&si=gmpolicysastoken&sig=EjAqjo6Nu5xMLEZEkMkLbeF7TD9v1J8DNB2t8gOKTts%3D'
    ;
GO


------  Step 3.  Create (define) an event session.  --------
------  hello event session has an event with an action,
------  and a has a target.

IF EXISTS
    (SELECT * from sys.database_event_sessions
        WHERE name = 'gmeventsessionname240b')
BEGIN
    DROP
        EVENT SESSION
            gmeventsessionname240b
        ON DATABASE;
END
GO


CREATE
    EVENT SESSION
        gmeventsessionname240b
    ON DATABASE

    ADD EVENT
        sqlserver.sql_statement_starting
            (
            ACTION (sqlserver.sql_text)
            WHERE statement LIKE 'UPDATE gmTabEmployee%'
            )
    ADD TARGET
        package0.event_file
            (
            -- TODO: Assign AzureStorageAccount name, and hello associated Container name.
            -- Also, tweak hello .xel file name at end, if you like.
            SET filename =
                'https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent/anyfilenamexel242b.xel'
            )
    WITH
        (MAX_MEMORY = 10 MB,
        MAX_DISPATCH_LATENCY = 3 SECONDS)
    ;
GO


------  Step 4.  Start hello event session.  ----------------
------  Issue hello SQL Update statements that will be traced.
------  Then stop hello session.

------  Note: If hello target fails tooattach,
------  hello session must be stopped and restarted.

ALTER
    EVENT SESSION
        gmeventsessionname240b
    ON DATABASE
    STATE = START;
GO


SELECT 'BEFORE_Updates', EmployeeKudosCount, * FROM gmTabEmployee;

UPDATE gmTabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 2
    WHERE EmployeeDescr = 'Jane Doe';

UPDATE gmTabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 13
    WHERE EmployeeDescr = 'Jane Doe';

SELECT 'AFTER__Updates', EmployeeKudosCount, * FROM gmTabEmployee;
GO


ALTER
    EVENT SESSION
        gmeventsessionname240b
    ON DATABASE
    STATE = STOP;
GO


-------------- Step 5.  Select hello results. ----------

SELECT
        *, 'CLICK_NEXT_CELL_TO_BROWSE_ITS_RESULTS!' as [CLICK_NEXT_CELL_TO_BROWSE_ITS_RESULTS],
        CAST(event_data AS XML) AS [event_data_XML]  -- TODO: In ssms.exe results grid, double-click this cell!
    FROM
        sys.fn_xe_file_target_read_file
            (
                -- TODO: Fill in Storage Account name, and hello associated Container name.
                'https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent/anyfilenamexel242b',
                null, null, null
            );
GO


-------------- Step 6.  Clean up. ----------

DROP
    EVENT SESSION
        gmeventsessionname240b
    ON DATABASE;
GO

DROP DATABASE SCOPED CREDENTIAL
    -- TODO: Assign AzureStorageAccount name, and hello associated Container name.
    [https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent]
    ;
GO

DROP TABLE gmTabEmployee;
GO

PRINT 'Use PowerShell Remove-AzureStorageAccount toodelete your Azure Storage account!';
GO
```


<span data-ttu-id="0c4cd-157">En cas de cible de hello tooattach lorsque vous exécutez, vous devez arrêter et redémarrer la session d’événements hello :</span><span class="sxs-lookup"><span data-stu-id="0c4cd-157">If hello target fails tooattach when you run, you must stop and restart hello event session:</span></span>

```sql
ALTER EVENT SESSION ... STATE = STOP;
GO
ALTER EVENT SESSION ... STATE = START;
GO
```


## <a name="output"></a><span data-ttu-id="0c4cd-158">Sortie</span><span class="sxs-lookup"><span data-stu-id="0c4cd-158">Output</span></span>

<span data-ttu-id="0c4cd-159">Lorsque hello script Transact-SQL est terminée, cliquez sur une cellule sous hello **event_data_XML** en-tête de colonne.</span><span class="sxs-lookup"><span data-stu-id="0c4cd-159">When hello Transact-SQL script completes, click a cell under hello **event_data_XML** column header.</span></span> <span data-ttu-id="0c4cd-160">Un élément **<event>** s’affiche, avec une instruction UPDATE.</span><span class="sxs-lookup"><span data-stu-id="0c4cd-160">One **<event>** element is displayed which shows one UPDATE statement.</span></span>

<span data-ttu-id="0c4cd-161">Voici un élément **<event>** généré pendant le test :</span><span class="sxs-lookup"><span data-stu-id="0c4cd-161">Here is one **<event>** element that was generated during testing:</span></span>


```xml
<event name="sql_statement_starting" package="sqlserver" timestamp="2015-09-22T19:18:45.420Z">
  <data name="state">
    <value>0</value>
    <text>Normal</text>
  </data>
  <data name="line_number">
    <value>5</value>
  </data>
  <data name="offset">
    <value>148</value>
  </data>
  <data name="offset_end">
    <value>368</value>
  </data>
  <data name="statement">
    <value>UPDATE gmTabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 2
    WHERE EmployeeDescr = 'Jane Doe'</value>
  </data>
  <action name="sql_text" package="sqlserver">
    <value>

SELECT 'BEFORE_Updates', EmployeeKudosCount, * FROM gmTabEmployee;

UPDATE gmTabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 2
    WHERE EmployeeDescr = 'Jane Doe';

UPDATE gmTabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 13
    WHERE EmployeeDescr = 'Jane Doe';

SELECT 'AFTER__Updates', EmployeeKudosCount, * FROM gmTabEmployee;
</value>
  </action>
</event>
```


<span data-ttu-id="0c4cd-162">Hello précédent hello de script utilisé Transact-SQL suivant système fonction tooread hello event_file :</span><span class="sxs-lookup"><span data-stu-id="0c4cd-162">hello preceding Transact-SQL script used hello following system function tooread hello event_file:</span></span>

* [<span data-ttu-id="0c4cd-163">sys.fn_xe_file_target_read_file (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="0c4cd-163">sys.fn_xe_file_target_read_file (Transact-SQL)</span></span>](http://msdn.microsoft.com/library/cc280743.aspx)

<span data-ttu-id="0c4cd-164">Une explication des options avancées pour l’affichage de hello des données d’événements étendus est disponible à l’adresse :</span><span class="sxs-lookup"><span data-stu-id="0c4cd-164">An explanation of advanced options for hello viewing of data from extended events is available at:</span></span>

* [<span data-ttu-id="0c4cd-165">Affichage avancée des données cibles à partir d’événements étendus</span><span class="sxs-lookup"><span data-stu-id="0c4cd-165">Advanced Viewing of Target Data from Extended Events</span></span>](http://msdn.microsoft.com/library/mt752502.aspx)


## <a name="converting-hello-code-sample-toorun-on-sql-server"></a><span data-ttu-id="0c4cd-166">Lors de la conversion toorun exemple de code hello sur SQL Server</span><span class="sxs-lookup"><span data-stu-id="0c4cd-166">Converting hello code sample toorun on SQL Server</span></span>

<span data-ttu-id="0c4cd-167">Supposons que vous souhaitiez hello toorun précédent exemple Transact-SQL de Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="0c4cd-167">Suppose you wanted toorun hello preceding Transact-SQL sample on Microsoft SQL Server.</span></span>

* <span data-ttu-id="0c4cd-168">Par souci de simplicité, vous pouvez utiliser replace toocompletely conteneur de stockage Azure hello avec un simple fichier tel que **C:\myeventdata.xel**.</span><span class="sxs-lookup"><span data-stu-id="0c4cd-168">For simplicity, you would want toocompletely replace use of hello Azure Storage container with a simple file such as **C:\myeventdata.xel**.</span></span> <span data-ttu-id="0c4cd-169">fichier de Hello serait écrite toohello un disque dur local de l’ordinateur hello qui héberge SQL Server.</span><span class="sxs-lookup"><span data-stu-id="0c4cd-169">hello file would be written toohello local hard drive of hello computer that hosts SQL Server.</span></span>
* <span data-ttu-id="0c4cd-170">Vous n’avez pas besoin d’instructions Transact-SQL de type **CREATE MASTER KEY** et **CREATE CREDENTIAL**.</span><span class="sxs-lookup"><span data-stu-id="0c4cd-170">You would not need any kind of Transact-SQL statements for **CREATE MASTER KEY** and **CREATE CREDENTIAL**.</span></span>
* <span data-ttu-id="0c4cd-171">Bonjour **CREATE EVENT SESSION** instruction, dans son **ajouter une cible** clause, vous devez remplacer la valeur de Http hello affecté apportées trop**filename =** avec une chaîne de chemin d’accès complet comme  **C:\myfile.xel**.</span><span class="sxs-lookup"><span data-stu-id="0c4cd-171">In hello **CREATE EVENT SESSION** statement, in its **ADD TARGET** clause, you would replace hello Http value assigned made too**filename=** with a full path string like **C:\myfile.xel**.</span></span>
  
  * <span data-ttu-id="0c4cd-172">Vous n’avez pas besoin de compte Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="0c4cd-172">No Azure Storage account need be involved.</span></span>

## <a name="more-information"></a><span data-ttu-id="0c4cd-173">Plus d’informations</span><span class="sxs-lookup"><span data-stu-id="0c4cd-173">More information</span></span>

<span data-ttu-id="0c4cd-174">Pour plus d’informations sur les comptes et les conteneurs hello service de stockage Azure, consultez :</span><span class="sxs-lookup"><span data-stu-id="0c4cd-174">For more info about accounts and containers in hello Azure Storage service, see:</span></span>

* [<span data-ttu-id="0c4cd-175">Comment toouse stockage d’objets Blob à partir de .NET</span><span class="sxs-lookup"><span data-stu-id="0c4cd-175">How toouse Blob storage from .NET</span></span>](../storage/blobs/storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="0c4cd-176">Désignation et référencement des conteneurs, des objets BLOB et des métadonnées</span><span class="sxs-lookup"><span data-stu-id="0c4cd-176">Naming and Referencing Containers, Blobs, and Metadata</span></span>](http://msdn.microsoft.com/library/azure/dd135715.aspx)
* [<span data-ttu-id="0c4cd-177">Utilisation de hello conteneur racine</span><span class="sxs-lookup"><span data-stu-id="0c4cd-177">Working with hello Root Container</span></span>](http://msdn.microsoft.com/library/azure/ee395424.aspx)
* [<span data-ttu-id="0c4cd-178">Leçon 1 : Créer une stratégie d’accès stockée et une signature d’accès partagé sur un conteneur Azure</span><span class="sxs-lookup"><span data-stu-id="0c4cd-178">Lesson 1: Create a stored access policy and a shared access signature on an Azure container</span></span>](http://msdn.microsoft.com/library/dn466430.aspx)
  * [<span data-ttu-id="0c4cd-179">Leçon 2 : Créer des informations d’identification SQL Server à l’aide d’une signature d’accès partagé</span><span class="sxs-lookup"><span data-stu-id="0c4cd-179">Lesson 2: Create a SQL Server credential using a shared access signature</span></span>](http://msdn.microsoft.com/library/dn466435.aspx)

<!--
Image references.
-->

[30_powershell_ise]: ./media/sql-database-xevent-code-event-file/event-file-powershell-ise-b30.png

