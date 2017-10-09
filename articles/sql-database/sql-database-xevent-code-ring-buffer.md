---
title: "aaaXEvent code de mémoire tampon en anneau pour la base de données SQL | Documents Microsoft"
description: "Fournit un exemple de code Transact-SQL qui est effectué facile et rapide à l’aide de la cible de mémoire tampon en anneau hello, dans la base de données SQL Azure."
services: sql-database
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
tags: 
ms.assetid: 2510fb3f-c8f2-437a-8f49-9d5f6c96e75b
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: genemi
ms.openlocfilehash: 21df748d9999d6837d2b5bbe4a3f47fb351b4633
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="ring-buffer-target-code-for-extended-events-in-sql-database"></a><span data-ttu-id="787ef-103">Code cible de la mémoire tampon en anneau pour les événements étendus dans SQL Database</span><span class="sxs-lookup"><span data-stu-id="787ef-103">Ring Buffer target code for extended events in SQL Database</span></span>

[!INCLUDE [sql-database-xevents-selectors-1-include](../../includes/sql-database-xevents-selectors-1-include.md)]

<span data-ttu-id="787ef-104">Vous souhaitez un exemple de code complet pour hello plus simple rapidement toocapture et fournir les informations pour un événement étendu pendant un test.</span><span class="sxs-lookup"><span data-stu-id="787ef-104">You want a complete code sample for hello easiest quick way toocapture and report information for an extended event during a test.</span></span> <span data-ttu-id="787ef-105">Hello plus simple pour les données d’événements étendus est hello [cible de mémoire tampon en anneau](http://msdn.microsoft.com/library/ff878182.aspx).</span><span class="sxs-lookup"><span data-stu-id="787ef-105">hello easiest target for extended event data is hello [Ring Buffer target](http://msdn.microsoft.com/library/ff878182.aspx).</span></span>

<span data-ttu-id="787ef-106">Cette rubrique présente un exemple de code Transact-SQL qui :</span><span class="sxs-lookup"><span data-stu-id="787ef-106">This topic presents a Transact-SQL code sample that:</span></span>

1. <span data-ttu-id="787ef-107">Crée une table avec toodemonstrate de données avec.</span><span class="sxs-lookup"><span data-stu-id="787ef-107">Creates a table with data toodemonstrate with.</span></span>
2. <span data-ttu-id="787ef-108">Crée une session pour un événement étendu existant, à savoir **sqlserver.sql_statement_starting**.</span><span class="sxs-lookup"><span data-stu-id="787ef-108">Creates a session for an existing extended event, namely **sqlserver.sql_statement_starting**.</span></span>
   
   * <span data-ttu-id="787ef-109">événement Hello est limitée tooSQL les instructions qui contiennent une chaîne particulière de la mise à jour : **instruction comme '% mise à jour tabEmployee %'**.</span><span class="sxs-lookup"><span data-stu-id="787ef-109">hello event is limited tooSQL statements that contain a particular Update string: **statement LIKE '%UPDATE tabEmployee%'**.</span></span>
   * <span data-ttu-id="787ef-110">Choisit de sortie de hello toosend de cible de tooa d’événement hello du type de mémoire tampon en anneau, à savoir **package0.ring_buffer**.</span><span class="sxs-lookup"><span data-stu-id="787ef-110">Chooses toosend hello output of hello event tooa target of type Ring Buffer, namely  **package0.ring_buffer**.</span></span>
3. <span data-ttu-id="787ef-111">Démarre la session d’événements hello.</span><span class="sxs-lookup"><span data-stu-id="787ef-111">Starts hello event session.</span></span>
4. <span data-ttu-id="787ef-112">Émet un ensemble d’instructions SQL UPDATE simples.</span><span class="sxs-lookup"><span data-stu-id="787ef-112">Issues a couple of simple SQL UPDATE statements.</span></span>
5. <span data-ttu-id="787ef-113">Émet une sortie des événements SQL SELECT instruction tooretrieve à partir de la mémoire tampon en anneau de hello.</span><span class="sxs-lookup"><span data-stu-id="787ef-113">Issues a SQL SELECT statement tooretrieve event output from hello Ring Buffer.</span></span>
   
   * <span data-ttu-id="787ef-114">**sys.dm_xe_database_session_targets** et d’autres vues de gestion dynamique (DMV) sont incluses.</span><span class="sxs-lookup"><span data-stu-id="787ef-114">**sys.dm_xe_database_session_targets** and other dynamic management views (DMVs) are joined.</span></span>
6. <span data-ttu-id="787ef-115">Arrête la session d’événements hello.</span><span class="sxs-lookup"><span data-stu-id="787ef-115">Stops hello event session.</span></span>
7. <span data-ttu-id="787ef-116">Suppressions hello cible de mémoire tampon en anneau, toorelease ses ressources.</span><span class="sxs-lookup"><span data-stu-id="787ef-116">Drops hello Ring Buffer target, toorelease its resources.</span></span>
8. <span data-ttu-id="787ef-117">Supprime la session d’événements hello et tableau de démonstration hello.</span><span class="sxs-lookup"><span data-stu-id="787ef-117">Drops hello event session and hello demo table.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="787ef-118">Composants requis</span><span class="sxs-lookup"><span data-stu-id="787ef-118">Prerequisites</span></span>

* <span data-ttu-id="787ef-119">Un compte et un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="787ef-119">An Azure account and subscription.</span></span> <span data-ttu-id="787ef-120">Vous pouvez vous inscrire à un [essai gratuit](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="787ef-120">You can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="787ef-121">Une base de données dans laquelle vous pouvez créer une table.</span><span class="sxs-lookup"><span data-stu-id="787ef-121">Any database you can create a table in.</span></span>
  
  * <span data-ttu-id="787ef-122">Vous pouvez aussi [créer une base de données de démonstration **AdventureWorksLT**](sql-database-get-started.md) en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="787ef-122">Optionally you can [create an **AdventureWorksLT** demonstration database](sql-database-get-started.md) in minutes.</span></span>
* <span data-ttu-id="787ef-123">SQL Server Management Studio (ssms.exe), dans l’idéal, la version de sa dernière mise à jour mensuelle.</span><span class="sxs-lookup"><span data-stu-id="787ef-123">SQL Server Management Studio (ssms.exe), ideally its latest monthly update version.</span></span> 
  <span data-ttu-id="787ef-124">Vous pouvez télécharger hello ssms.exe plus récentes à partir de :</span><span class="sxs-lookup"><span data-stu-id="787ef-124">You can download hello latest ssms.exe from:</span></span>
  
  * <span data-ttu-id="787ef-125">À partir de la rubrique [Télécharger SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="787ef-125">Topic titled [Download SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).</span></span>
  * [<span data-ttu-id="787ef-126">Un téléchargement de toohello lien direct.</span><span class="sxs-lookup"><span data-stu-id="787ef-126">A direct link toohello download.</span></span>](http://go.microsoft.com/fwlink/?linkid=616025)

## <a name="code-sample"></a><span data-ttu-id="787ef-127">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="787ef-127">Code sample</span></span>

<span data-ttu-id="787ef-128">Avec très peu de modifications, hello exemple de code suivant mémoire tampon en anneau peut être exécuté sur la base de données SQL Azure ou Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="787ef-128">With very minor modification, hello following Ring Buffer code sample can be run on either Azure SQL Database or Microsoft SQL Server.</span></span> <span data-ttu-id="787ef-129">différence de Hello est présence hello du nœud de hello 'base de _données' dans le nom hello de certaines vues de gestion dynamique (DMV), utilisée dans la clause FROM de hello à l’étape 5.</span><span class="sxs-lookup"><span data-stu-id="787ef-129">hello difference is hello presence of hello node '_database' in hello name of some dynamic management views (DMVs), used in hello FROM clause in Step 5.</span></span> <span data-ttu-id="787ef-130">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="787ef-130">For example:</span></span>

* <span data-ttu-id="787ef-131">sys.dm_xe**_database**_session_targets</span><span class="sxs-lookup"><span data-stu-id="787ef-131">sys.dm_xe**_database**_session_targets</span></span>
* <span data-ttu-id="787ef-132">sys.dm_xe_session_targets</span><span class="sxs-lookup"><span data-stu-id="787ef-132">sys.dm_xe_session_targets</span></span>

&nbsp;

```sql
GO
----  Transact-SQL.
---- Step set 1.

SET NOCOUNT ON;
GO


IF EXISTS
    (SELECT * FROM sys.objects
        WHERE type = 'U' and name = 'tabEmployee')
BEGIN
    DROP TABLE tabEmployee;
END
GO


CREATE TABLE tabEmployee
(
    EmployeeGuid         uniqueIdentifier   not null  default newid()  primary key,
    EmployeeId           int                not null  identity(1,1),
    EmployeeKudosCount   int                not null  default 0,
    EmployeeDescr        nvarchar(256)          null
);
GO


INSERT INTO tabEmployee ( EmployeeDescr )
    VALUES ( 'Jane Doe' );
GO

---- Step set 2.


IF EXISTS
    (SELECT * from sys.database_event_sessions
        WHERE name = 'eventsession_gm_azuresqldb51')
BEGIN
    DROP EVENT SESSION eventsession_gm_azuresqldb51
        ON DATABASE;
END
GO


CREATE
    EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    ADD EVENT
        sqlserver.sql_statement_starting
            (
            ACTION (sqlserver.sql_text)
            WHERE statement LIKE '%UPDATE tabEmployee%'
            )
    ADD TARGET
        package0.ring_buffer
            (SET
                max_memory = 500   -- Units of KB.
            );
GO

---- Step set 3.


ALTER EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    STATE = START;
GO

---- Step set 4.


SELECT 'BEFORE_Updates', EmployeeKudosCount, * FROM tabEmployee;

UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 102;

UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 1015;

SELECT 'AFTER__Updates', EmployeeKudosCount, * FROM tabEmployee;
GO

---- Step set 5.


SELECT
    se.name                      AS [session-name],
    ev.event_name,
    ac.action_name,
    st.target_name,
    se.session_source,
    st.target_data,
    CAST(st.target_data AS XML)  AS [target_data_XML]
FROM
               sys.dm_xe_database_session_event_actions  AS ac

    INNER JOIN sys.dm_xe_database_session_events         AS ev  ON ev.event_name = ac.event_name
        AND CAST(ev.event_session_address AS BINARY(8)) = CAST(ac.event_session_address AS BINARY(8))

    INNER JOIN sys.dm_xe_database_session_object_columns AS oc
         ON CAST(oc.event_session_address AS BINARY(8)) = CAST(ac.event_session_address AS BINARY(8))

    INNER JOIN sys.dm_xe_database_session_targets        AS st
         ON CAST(st.event_session_address AS BINARY(8)) = CAST(ac.event_session_address AS BINARY(8))

    INNER JOIN sys.dm_xe_database_sessions               AS se
         ON CAST(ac.event_session_address AS BINARY(8)) = CAST(se.address AS BINARY(8))
WHERE
        oc.column_name = 'occurrence_number'
    AND
        se.name        = 'eventsession_gm_azuresqldb51'
    AND
        ac.action_name = 'sql_text'
ORDER BY
    se.name,
    ev.event_name,
    ac.action_name,
    st.target_name,
    se.session_source
;
GO

---- Step set 6.


ALTER EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    STATE = STOP;
GO

---- Step set 7.


ALTER EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    DROP TARGET package0.ring_buffer;
GO

---- Step set 8.


DROP EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE;
GO

DROP TABLE tabEmployee;
GO
```


&nbsp;

## <a name="ring-buffer-contents"></a><span data-ttu-id="787ef-133">Contenu de la mémoire tampon en anneau</span><span class="sxs-lookup"><span data-stu-id="787ef-133">Ring Buffer contents</span></span>

<span data-ttu-id="787ef-134">Nous avons utilisé les exemples de code hello ssms.exe toorun.</span><span class="sxs-lookup"><span data-stu-id="787ef-134">We used ssms.exe toorun hello code sample.</span></span>

<span data-ttu-id="787ef-135">résultats de hello tooview, nous avez cliqué sur hello cellule sous l’en-tête de colonne hello **target_data_XML**.</span><span class="sxs-lookup"><span data-stu-id="787ef-135">tooview hello results, we clicked hello cell under hello column header **target_data_XML**.</span></span>

<span data-ttu-id="787ef-136">Ensuite, dans le volet de résultats hello nous avez cliqué sur hello cellule sous l’en-tête de colonne hello **target_data_XML**.</span><span class="sxs-lookup"><span data-stu-id="787ef-136">Then in hello results pane we clicked hello cell under hello column header **target_data_XML**.</span></span> <span data-ttu-id="787ef-137">Cliquez sur créé un autre onglet fichier dans ssms.exe affiché dans le hello contenu de la cellule de résultat hello au format XML.</span><span class="sxs-lookup"><span data-stu-id="787ef-137">This click created another file tab in ssms.exe in which hello content of hello result cell was displayed, as XML.</span></span>

<span data-ttu-id="787ef-138">Hello est affiché dans le bloc de hello.</span><span class="sxs-lookup"><span data-stu-id="787ef-138">hello output is shown in hello following block.</span></span> <span data-ttu-id="787ef-139">Elle semble longue, mais ne comprend que deux éléments **<event>** .</span><span class="sxs-lookup"><span data-stu-id="787ef-139">It looks long, but it is just two **<event>** elements.</span></span>

&nbsp;

```
<RingBufferTarget truncated="0" processingTime="0" totalEventsProcessed="2" eventCount="2" droppedCount="0" memoryUsed="1728">
  <event name="sql_statement_starting" package="sqlserver" timestamp="2015-09-22T15:29:31.317Z">
    <data name="state">
      <type name="statement_starting_state" package="sqlserver" />
      <value>0</value>
      <text>Normal</text>
    </data>
    <data name="line_number">
      <type name="int32" package="package0" />
      <value>7</value>
    </data>
    <data name="offset">
      <type name="int32" package="package0" />
      <value>184</value>
    </data>
    <data name="offset_end">
      <type name="int32" package="package0" />
      <value>328</value>
    </data>
    <data name="statement">
      <type name="unicode_string" package="package0" />
      <value>UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 102</value>
    </data>
    <action name="sql_text" package="sqlserver">
      <type name="unicode_string" package="package0" />
      <value>
---- Step set 4.


SELECT 'BEFORE_Updates', EmployeeKudosCount, * FROM tabEmployee;

UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 102;

UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 1015;

SELECT 'AFTER__Updates', EmployeeKudosCount, * FROM tabEmployee;
</value>
    </action>
  </event>
  <event name="sql_statement_starting" package="sqlserver" timestamp="2015-09-22T15:29:31.327Z">
    <data name="state">
      <type name="statement_starting_state" package="sqlserver" />
      <value>0</value>
      <text>Normal</text>
    </data>
    <data name="line_number">
      <type name="int32" package="package0" />
      <value>10</value>
    </data>
    <data name="offset">
      <type name="int32" package="package0" />
      <value>340</value>
    </data>
    <data name="offset_end">
      <type name="int32" package="package0" />
      <value>486</value>
    </data>
    <data name="statement">
      <type name="unicode_string" package="package0" />
      <value>UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 1015</value>
    </data>
    <action name="sql_text" package="sqlserver">
      <type name="unicode_string" package="package0" />
      <value>
---- Step set 4.


SELECT 'BEFORE_Updates', EmployeeKudosCount, * FROM tabEmployee;

UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 102;

UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 1015;

SELECT 'AFTER__Updates', EmployeeKudosCount, * FROM tabEmployee;
</value>
    </action>
  </event>
</RingBufferTarget>
```


#### <a name="release-resources-held-by-your-ring-buffer"></a><span data-ttu-id="787ef-140">Libérer les ressources détenues par votre mémoire tampon en anneau</span><span class="sxs-lookup"><span data-stu-id="787ef-140">Release resources held by your Ring Buffer</span></span>

<span data-ttu-id="787ef-141">Lorsque vous avez terminé avec votre mémoire tampon en anneau, vous pouvez le supprimer et libérer ses ressources émettant un **ALTER** à hello qui suit :</span><span class="sxs-lookup"><span data-stu-id="787ef-141">When you are done with your Ring Buffer, you can remove it and release its resources issuing an **ALTER** like hello following:</span></span>

```sql
ALTER EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    DROP TARGET package0.ring_buffer;
GO
```


<span data-ttu-id="787ef-142">définition de Hello de votre session d’événements est mis à jour, mais pas supprimée.</span><span class="sxs-lookup"><span data-stu-id="787ef-142">hello definition of your event session is updated, but not dropped.</span></span> <span data-ttu-id="787ef-143">Ultérieurement, vous pouvez ajouter une autre instance de la session d’événements tooyour hello mémoire tampon en anneau :</span><span class="sxs-lookup"><span data-stu-id="787ef-143">Later you can add another instance of hello Ring Buffer tooyour event session:</span></span>

```sql
ALTER EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    ADD TARGET
        package0.ring_buffer
            (SET
                max_memory = 500   -- Units of KB.
            );
```


## <a name="more-information"></a><span data-ttu-id="787ef-144">Plus d’informations</span><span class="sxs-lookup"><span data-stu-id="787ef-144">More information</span></span>

<span data-ttu-id="787ef-145">rubrique de principal Hello pour les événements étendus sur la base de données SQL Azure est :</span><span class="sxs-lookup"><span data-stu-id="787ef-145">hello primary topic for extended events on Azure SQL Database is:</span></span>

* <span data-ttu-id="787ef-146">La rubrique [Considérations relatives aux événements étendus dans Azure SQL Database](sql-database-xevent-db-diff-from-svr.md) décrit les différences à prendre en compte entre les événements étendus dans Azure SQL Database et ceux dans Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="787ef-146">[Extended event considerations in SQL Database](sql-database-xevent-db-diff-from-svr.md), which contrasts some aspects of extended events that differ between Azure SQL Database versus Microsoft SQL Server.</span></span>

<span data-ttu-id="787ef-147">Autres rubriques d’exemples de code pour les événements étendus sont disponibles au hello suivant liens.</span><span class="sxs-lookup"><span data-stu-id="787ef-147">Other code sample topics for extended events are available at hello following links.</span></span> <span data-ttu-id="787ef-148">Toutefois, vous devez vérifier régulièrement les tout toosee exemple qu’exemple hello cible Microsoft SQL Server par rapport à la base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="787ef-148">However, you must routinely check any sample toosee whether hello sample targets Microsoft SQL Server versus Azure SQL Database.</span></span> <span data-ttu-id="787ef-149">Vous pouvez décider si des modifications mineures sont nécessaires toorun hello exemple.</span><span class="sxs-lookup"><span data-stu-id="787ef-149">Then you can decide whether minor changes are needed toorun hello sample.</span></span>

* <span data-ttu-id="787ef-150">Exemple de code pour Azure SQL Database : [Code cible du fichier d’événements pour les événements étendus dans SQL Database](sql-database-xevent-code-event-file.md)</span><span class="sxs-lookup"><span data-stu-id="787ef-150">Code sample for Azure SQL Database: [Event File target code for extended events in SQL Database](sql-database-xevent-code-event-file.md)</span></span>

<!--
('lock_acquired' event.)

- Code sample for SQL Server: [Determine Which Queries Are Holding Locks](http://msdn.microsoft.com/library/bb677357.aspx)
- Code sample for SQL Server: [Find hello Objects That Have hello Most Locks Taken on Them](http://msdn.microsoft.com/library/bb630355.aspx)
-->
