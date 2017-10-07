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
# <a name="event-file-target-code-for-extended-events-in-sql-database"></a>Code cible du fichier d’événements pour les événements étendus dans SQL Database

[!INCLUDE [sql-database-xevents-selectors-1-include](../../includes/sql-database-xevents-selectors-1-include.md)]

Vous souhaitez un exemple de code complet pour une façon fiable toocapture et fournir les informations pour un événement étendu.

Dans Microsoft SQL Server, hello [cible du fichier de l’événement](http://msdn.microsoft.com/library/ff878115.aspx) est sorties d’événement toostore utilisé dans un fichier de disque dur local. Mais ces fichiers ne sont pas disponible tooAzure de base de données SQL. Au lieu de cela, nous utilisons cible de fichier d’événements du service toosupport hello hello le stockage Azure.

Cette rubrique présente un exemple de code en deux phases :

* PowerShell, toocreate un conteneur de stockage Azure dans le cloud de hello.
* Transact-SQL :
  
  * tooassign hello Azure Storage conteneur tooan événement cible du fichier.
  * session d’événements hello toocreate et démarrer et ainsi de suite.

## <a name="prerequisites"></a>Composants requis

* Un compte et un abonnement Azure. Vous pouvez vous inscrire à un [essai gratuit](https://azure.microsoft.com/pricing/free-trial/).
* Une base de données dans laquelle vous pouvez créer une table.
  
  * Vous pouvez aussi [créer une base de données de démonstration **AdventureWorksLT**](sql-database-get-started.md) en quelques minutes.
* SQL Server Management Studio (ssms.exe), dans l’idéal, la version de sa dernière mise à jour mensuelle. 
  Vous pouvez télécharger hello ssms.exe plus récentes à partir de :
  
  * À partir de la rubrique [Télécharger SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).
  * [Un téléchargement de toohello lien direct.](http://go.microsoft.com/fwlink/?linkid=616025)
* Vous devez avoir hello [modules Azure PowerShell](http://go.microsoft.com/?linkid=9811175) installé.
  
  * modules de Hello fournissent des commandes telles que - **New-AzureStorageAccount**.

## <a name="phase-1-powershell-code-for-azure-storage-container"></a>Phase 1 : code PowerShell pour le conteneur Azure Storage

Cette PowerShell est la phase 1 de l’exemple de code en deux phases hello.

script de Hello démarre avec les commandes tooclean après un éventuel précédent est rerunnable.

1. Collez le script PowerShell de hello dans un simple éditeur de texte tel que Notepad.exe, enregistrez le script de hello en tant que fichier avec l’extension de hello **.ps1**.
2. Démarrez PowerShell ISE en tant qu’administrateur.
3. À l’invite de hello, tapez<br/>`Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Scope CurrentUser`<br/>et appuyez sur Entrée.
4. Dans PowerShell ISE, ouvrez votre fichier **.ps1** . Exécutez le script de hello.
5. script de Hello commence une nouvelle fenêtre dans laquelle vous vous connectez tooAzure.
   
   * Si vous réexécutez le script de hello sans interrompre votre session, vous pouvez hello pratique commenté hello **Add-AzureAccount** commande.

![PowerShell ISE, avec le module Windows Azure installé, prêt toorun script.][30_powershell_ise]


### <a name="powershell-code"></a>Code PowerShell

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


Prenez note de hello peu de valeurs nommées qui imprime de script PowerShell de hello lorsqu’elle se termine. Vous devez modifier ces valeurs dans le script Transact-SQL qui suit en tant que la phase 2 de hello.

## <a name="phase-2-transact-sql-code-that-uses-azure-storage-container"></a>Phase 2 : code Transact-SQL utilisant le conteneur Azure Storage

* Dans la phase 1 de cet exemple de code, vous avez exécuté une toocreate de script PowerShell un conteneur de stockage Azure.
* Ensuite dans la phase 2, hello script Transact-SQL suivant doit utiliser le conteneur de hello.

script de Hello démarre avec les commandes tooclean après un éventuel précédent est rerunnable.

Hello script PowerShell imprime quelques valeurs nommées s’il est terminé. Vous devez modifier hello Transact-SQL script toouse ces valeurs. Rechercher **TODO** Bonjour de hello Transact-SQL script toolocate des points d’édition.

1. Ouvrez SQL Server Management Studio (ssms.exe).
2. Connecter la base de données de base de données SQL Azure tooyour.
3. Cliquez sur tooopen un nouveau volet de requête.
4. Collez hello suivant le script Transact-SQL dans le volet de requête hello.
5. Trouver toutes **TODO** hello script et apportez les modifications appropriées hello.
6. Enregistrez et exécutez ensuite le script de hello.


> [!WARNING]
> valeur de la clé SAS généré par hello précédant le script PowerShell de Hello pourrait commencer par un ' ?' (point d’interrogation). Lorsque vous utilisez la clé SAS hello Bonjour script T-SQL suivant, vous devez *suppriment hello ' ?'* . Dans le cas contraire, vos efforts peuvent être bloqués par la sécurité.


### <a name="transact-sql-code"></a>Code Transact-SQL

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


En cas de cible de hello tooattach lorsque vous exécutez, vous devez arrêter et redémarrer la session d’événements hello :

```sql
ALTER EVENT SESSION ... STATE = STOP;
GO
ALTER EVENT SESSION ... STATE = START;
GO
```


## <a name="output"></a>Sortie

Lorsque hello script Transact-SQL est terminée, cliquez sur une cellule sous hello **event_data_XML** en-tête de colonne. Un élément **<event>** s’affiche, avec une instruction UPDATE.

Voici un élément **<event>** généré pendant le test :


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


Hello précédent hello de script utilisé Transact-SQL suivant système fonction tooread hello event_file :

* [sys.fn_xe_file_target_read_file (Transact-SQL)](http://msdn.microsoft.com/library/cc280743.aspx)

Une explication des options avancées pour l’affichage de hello des données d’événements étendus est disponible à l’adresse :

* [Affichage avancée des données cibles à partir d’événements étendus](http://msdn.microsoft.com/library/mt752502.aspx)


## <a name="converting-hello-code-sample-toorun-on-sql-server"></a>Lors de la conversion toorun exemple de code hello sur SQL Server

Supposons que vous souhaitiez hello toorun précédent exemple Transact-SQL de Microsoft SQL Server.

* Par souci de simplicité, vous pouvez utiliser replace toocompletely conteneur de stockage Azure hello avec un simple fichier tel que **C:\myeventdata.xel**. fichier de Hello serait écrite toohello un disque dur local de l’ordinateur hello qui héberge SQL Server.
* Vous n’avez pas besoin d’instructions Transact-SQL de type **CREATE MASTER KEY** et **CREATE CREDENTIAL**.
* Bonjour **CREATE EVENT SESSION** instruction, dans son **ajouter une cible** clause, vous devez remplacer la valeur de Http hello affecté apportées trop**filename =** avec une chaîne de chemin d’accès complet comme  **C:\myfile.xel**.
  
  * Vous n’avez pas besoin de compte Azure Storage.

## <a name="more-information"></a>Plus d’informations

Pour plus d’informations sur les comptes et les conteneurs hello service de stockage Azure, consultez :

* [Comment toouse stockage d’objets Blob à partir de .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md)
* [Désignation et référencement des conteneurs, des objets BLOB et des métadonnées](http://msdn.microsoft.com/library/azure/dd135715.aspx)
* [Utilisation de hello conteneur racine](http://msdn.microsoft.com/library/azure/ee395424.aspx)
* [Leçon 1 : Créer une stratégie d’accès stockée et une signature d’accès partagé sur un conteneur Azure](http://msdn.microsoft.com/library/dn466430.aspx)
  * [Leçon 2 : Créer des informations d’identification SQL Server à l’aide d’une signature d’accès partagé](http://msdn.microsoft.com/library/dn466435.aspx)

<!--
Image references.
-->

[30_powershell_ise]: ./media/sql-database-xevent-code-event-file/event-file-powershell-ise-b30.png

