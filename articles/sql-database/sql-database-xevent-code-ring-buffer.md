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
# <a name="ring-buffer-target-code-for-extended-events-in-sql-database"></a>Code cible de la mémoire tampon en anneau pour les événements étendus dans SQL Database

[!INCLUDE [sql-database-xevents-selectors-1-include](../../includes/sql-database-xevents-selectors-1-include.md)]

Vous souhaitez un exemple de code complet pour hello plus simple rapidement toocapture et fournir les informations pour un événement étendu pendant un test. Hello plus simple pour les données d’événements étendus est hello [cible de mémoire tampon en anneau](http://msdn.microsoft.com/library/ff878182.aspx).

Cette rubrique présente un exemple de code Transact-SQL qui :

1. Crée une table avec toodemonstrate de données avec.
2. Crée une session pour un événement étendu existant, à savoir **sqlserver.sql_statement_starting**.
   
   * événement Hello est limitée tooSQL les instructions qui contiennent une chaîne particulière de la mise à jour : **instruction comme '% mise à jour tabEmployee %'**.
   * Choisit de sortie de hello toosend de cible de tooa d’événement hello du type de mémoire tampon en anneau, à savoir **package0.ring_buffer**.
3. Démarre la session d’événements hello.
4. Émet un ensemble d’instructions SQL UPDATE simples.
5. Émet une sortie des événements SQL SELECT instruction tooretrieve à partir de la mémoire tampon en anneau de hello.
   
   * **sys.dm_xe_database_session_targets** et d’autres vues de gestion dynamique (DMV) sont incluses.
6. Arrête la session d’événements hello.
7. Suppressions hello cible de mémoire tampon en anneau, toorelease ses ressources.
8. Supprime la session d’événements hello et tableau de démonstration hello.

## <a name="prerequisites"></a>Composants requis

* Un compte et un abonnement Azure. Vous pouvez vous inscrire à un [essai gratuit](https://azure.microsoft.com/pricing/free-trial/).
* Une base de données dans laquelle vous pouvez créer une table.
  
  * Vous pouvez aussi [créer une base de données de démonstration **AdventureWorksLT**](sql-database-get-started.md) en quelques minutes.
* SQL Server Management Studio (ssms.exe), dans l’idéal, la version de sa dernière mise à jour mensuelle. 
  Vous pouvez télécharger hello ssms.exe plus récentes à partir de :
  
  * À partir de la rubrique [Télécharger SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).
  * [Un téléchargement de toohello lien direct.](http://go.microsoft.com/fwlink/?linkid=616025)

## <a name="code-sample"></a>Exemple de code

Avec très peu de modifications, hello exemple de code suivant mémoire tampon en anneau peut être exécuté sur la base de données SQL Azure ou Microsoft SQL Server. différence de Hello est présence hello du nœud de hello 'base de _données' dans le nom hello de certaines vues de gestion dynamique (DMV), utilisée dans la clause FROM de hello à l’étape 5. Par exemple :

* sys.dm_xe**_database**_session_targets
* sys.dm_xe_session_targets

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

## <a name="ring-buffer-contents"></a>Contenu de la mémoire tampon en anneau

Nous avons utilisé les exemples de code hello ssms.exe toorun.

résultats de hello tooview, nous avez cliqué sur hello cellule sous l’en-tête de colonne hello **target_data_XML**.

Ensuite, dans le volet de résultats hello nous avez cliqué sur hello cellule sous l’en-tête de colonne hello **target_data_XML**. Cliquez sur créé un autre onglet fichier dans ssms.exe affiché dans le hello contenu de la cellule de résultat hello au format XML.

Hello est affiché dans le bloc de hello. Elle semble longue, mais ne comprend que deux éléments **<event>** .

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


#### <a name="release-resources-held-by-your-ring-buffer"></a>Libérer les ressources détenues par votre mémoire tampon en anneau

Lorsque vous avez terminé avec votre mémoire tampon en anneau, vous pouvez le supprimer et libérer ses ressources émettant un **ALTER** à hello qui suit :

```sql
ALTER EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    DROP TARGET package0.ring_buffer;
GO
```


définition de Hello de votre session d’événements est mis à jour, mais pas supprimée. Ultérieurement, vous pouvez ajouter une autre instance de la session d’événements tooyour hello mémoire tampon en anneau :

```sql
ALTER EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    ADD TARGET
        package0.ring_buffer
            (SET
                max_memory = 500   -- Units of KB.
            );
```


## <a name="more-information"></a>Plus d’informations

rubrique de principal Hello pour les événements étendus sur la base de données SQL Azure est :

* La rubrique [Considérations relatives aux événements étendus dans Azure SQL Database](sql-database-xevent-db-diff-from-svr.md) décrit les différences à prendre en compte entre les événements étendus dans Azure SQL Database et ceux dans Microsoft SQL Server.

Autres rubriques d’exemples de code pour les événements étendus sont disponibles au hello suivant liens. Toutefois, vous devez vérifier régulièrement les tout toosee exemple qu’exemple hello cible Microsoft SQL Server par rapport à la base de données SQL Azure. Vous pouvez décider si des modifications mineures sont nécessaires toorun hello exemple.

* Exemple de code pour Azure SQL Database : [Code cible du fichier d’événements pour les événements étendus dans SQL Database](sql-database-xevent-code-event-file.md)

<!--
('lock_acquired' event.)

- Code sample for SQL Server: [Determine Which Queries Are Holding Locks](http://msdn.microsoft.com/library/bb677357.aspx)
- Code sample for SQL Server: [Find hello Objects That Have hello Most Locks Taken on Them](http://msdn.microsoft.com/library/bb630355.aspx)
-->
