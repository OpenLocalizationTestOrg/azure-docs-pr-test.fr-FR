---
title: "événements aaaExtended dans la base de données SQL | Documents Microsoft"
description: "Décrit les événements étendus (XEvents) dans la base de données SQL Azure et les différences entre les sessions d’événements dans la base de données SQL Azure et dans Microsoft SQL Server."
services: sql-database
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
tags: 
ms.assetid: 3b28cf15-f820-4b3c-8310-908d6d5b9d0c
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: genemi
ms.openlocfilehash: 8c966a84412aa561c92b16e5c6902102483eb1bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="extended-events-in-sql-database"></a>Événement étendus dans la base de données SQL
[!INCLUDE [sql-database-xevents-selectors-1-include](../../includes/sql-database-xevents-selectors-1-include.md)]

Cette rubrique explique comment implémentation hello des événements étendus dans la base de données SQL Azure est légèrement différent tooextended comparés dans Microsoft SQL Server.

- Base de données SQL V12 acquise fonctionnalité événements étendus hello hello deuxième semestre calendrier 2015.
- Cette fonctionnalité est présente dans SQL Server depuis 2008.
- ensemble de fonctionnalités Hello des événements étendus sur la base de données SQL est un sous-ensemble robust de fonctionnalités hello sur SQL Server.

*XEvents* est un surnom informel parfois utilisé pour désigne les « événements étendus » dans les blogs et autres emplacements informels.

Des informations complémentaires sur les événements étendus, pour Base de données SQL Azure et Microsoft SQL Server, sont disponibles dans :

- [Démarrage rapide : Événements étendus dans SQL Server](http://msdn.microsoft.com/library/mt733217.aspx)
- [Événements étendus](http://msdn.microsoft.com/library/bb630282.aspx)

## <a name="prerequisites"></a>Conditions préalables

Cette rubrique part du principe que vous connaissez déjà les éléments suivants :

- [Service Base de données SQL Azure](https://azure.microsoft.com/services/sql-database/)
- [Événements étendus](http://msdn.microsoft.com/library/bb630282.aspx) dans Microsoft SQL Server.

- bloc Hello de notre documentation sur les événements étendus s’applique tooboth SQL Server et la base de données SQL.

Toohello préalable exposition éléments suivants est utile lorsque vous choisissez hello fichier d’événements en tant que hello [cible](#AzureXEventsTargets):

- [Service Azure Storage](https://azure.microsoft.com/services/storage/)


- PowerShell
    - [À l’aide d’Azure PowerShell avec le stockage Azure](../storage/common/storage-powershell-guide-full.md) -fournit des informations complètes sur PowerShell et hello service de stockage Azure.

## <a name="code-samples"></a>Exemples de code

Des rubriques connexes fournissent deux exemples de code :


- [Code cible de la mémoire tampon en anneau pour les événements étendus dans la base de données SQL](sql-database-xevent-code-ring-buffer.md)
    - Script Transact-SQL simple court.
    - Nous mettre en évidence dans la rubrique d’exemple de code hello que, lorsque vous avez terminé avec une cible de mémoire tampon en anneau, vous devez libérer ses ressources en exécutant alter déroulante `ALTER EVENT SESSION ... ON DATABASE DROP TARGET ...;` instruction. Vous pouvez ensuite ajouter une autre instance de mémoire tampon en anneau avec l’instruction `ALTER EVENT SESSION ... ON DATABASE ADD TARGET ...`.


- [Code cible du fichier d’événements pour les événements étendus dans la base de données SQL](sql-database-xevent-code-event-file.md)
    - Phase 1 : PowerShell toocreate un conteneur de stockage Azure.
    - Phase 2 est Transact-SQL qui utilise le conteneur de stockage Azure hello.

## <a name="transact-sql-differences"></a>Différences Transact-SQL


- Lorsque vous exécutez hello [CREATE EVENT SESSION](http://msdn.microsoft.com/library/bb677289.aspx) commande sur le serveur SQL Server, vous utilisez hello **ON SERVER** clause. Toutefois, sur la base de données SQL vous utiliser hello **ON DATABASE** clause à la place.


- Hello **ON DATABASE** clause s’applique également toohello [ALTER EVENT SESSION](http://msdn.microsoft.com/library/bb630368.aspx) et [DROP EVENT SESSION](http://msdn.microsoft.com/library/bb630257.aspx) commandes Transact-SQL.


- Une meilleure pratique est l’option de session d’événement tooinclude hello de **STARTUP_STATE = ON** dans votre **CREATE EVENT SESSION** ou **ALTER EVENT SESSION** instructions.
    - Hello **= ON** valeur prend en charge un redémarrage automatique après une reconfiguration de base de données logique hello en raison du basculement de tooa.

## <a name="new-catalog-views"></a>Nouvelles vues catalogue

Hello événements étendus est prise en charge par plusieurs [affichages catalogue](http://msdn.microsoft.com/library/ms174365.aspx). Affichages catalogue vous dire *métadonnées ou des définitions* des sessions d’événements de créés par l’utilisateur dans la base de données actuelle hello. vues de Hello ne retournent pas d’informations sur les instances de sessions d’événements active.

| Nom de<br/>la vue catalogue | Description |
|:--- |:--- |
| **sys.database_event_session_actions** |Renvoie une ligne pour chaque action sur chaque événement d’une session d’événements. |
| **sys.database_event_session_events** |Renvoie une ligne pour chaque événement d’une session d’événements. |
| **sys.database_event_session_fields** |Renvoie une ligne pour chaque colonne pouvant être personnalisée définie explicitement sur les événements et les cibles. |
| **sys.database_event_session_targets** |Renvoie une ligne pour chaque cible d’événement pour une session d’événements. |
| **sys.database_event_sessions** |Retourne une ligne pour chaque session d’événements dans la base de données de la base de données SQL hello. |

Dans Microsoft SQL Server, les noms des vues catalogue similaires contiennent *.server\_* au lieu de *.database\_*. modèle de nom Hello est similaire à **sys.server_event_%**.

## <a name="new-dynamic-management-views-dmvshttpmsdnmicrosoftcomlibraryms188754aspx"></a>Nouvelles vues de gestion dynamique [(DMV)](http://msdn.microsoft.com/library/ms188754.aspx)

La base de données SQL Azure comporte des [vues de gestion dynamique (DMV)](http://msdn.microsoft.com/library/bb677293.aspx) qui prennent en charge les événements étendus. Les vues de gestion dynamique vous renseignent sur les sessions d’événements *actives* .

| Nom de la vue de gestion dynamique | Description |
|:--- |:--- |
| **sys.dm_xe_database_session_event_actions** |Renvoie des informations sur les actions d’une session d’événements. |
| **sys.dm_xe_database_session_events** |Renvoie des informations sur les sessions d’événements. |
| **sys.dm_xe_database_session_object_columns** |Indique les valeurs de configuration de hello pour les objets qui sont liées tooa session. |
| **sys.dm_xe_database_session_targets** |Renvoie des informations sur les cibles d’une session d’événements. |
| **sys.dm_xe_database_sessions** |Retourne une ligne pour chaque session d’événements est étendue toohello de base de données actuelle. |

Dans Microsoft SQL Server, les vues de catalogue similaires sont nommés sans hello  *\_base de données* nom de la partie de hello, tel que :

- **sys.dm_xe_sessions**, au lieu de name<br/>**sys.dm_xe_database_sessions**.

### <a name="dmvs-common-tooboth"></a>Tooboth commune de vues de gestion dynamique
Il existe des vues DMV supplémentaires qui sont commune tooboth de base de données SQL Azure et Microsoft SQL Server pour les événements étendus :

- **sys.dm_xe_map_values**
- **sys.dm_xe_object_columns**
- **sys.dm_xe_objects**
- **sys.dm_xe_packages**

 <a name="sqlfindseventsactionstargets" id="sqlfindseventsactionstargets"></a>

## <a name="find-hello-available-extended-events-actions-and-targets"></a>Rechercher les cibles, les actions et les événements étendus disponible hello

Vous pouvez exécuter une simple SQL **sélectionnez** tooobtain une liste des événements disponibles de hello, actions et cibles.

```sql
SELECT
        o.object_type,
        p.name         AS [package_name],
        o.name         AS [db_object_name],
        o.description  AS [db_obj_description]
    FROM
                   sys.dm_xe_objects  AS o
        INNER JOIN sys.dm_xe_packages AS p  ON p.guid = o.package_guid
    WHERE
        o.object_type in
            (
            'action',  'event',  'target'
            )
    ORDER BY
        o.object_type,
        p.name,
        o.name;
```


<a name="AzureXEventsTargets" id="AzureXEventsTargets"></a>&nbsp;

## <a name="targets-for-your-sql-database-event-sessions"></a>Cibles de vos sessions d’événements de Base de données SQL

Voici les cibles capables de capturer des résultats à partir de vos sessions d’événements sur la base de données SQL :

- [Cible de mémoire tampon en anneau](http://msdn.microsoft.com/library/ff878182.aspx) -Maintient brièvement les données d’événements en mémoire.
- [Cible de compteur d’événements](http://msdn.microsoft.com/library/ff878025.aspx) - Compte tous les événements qui se produisent pendant une session d’événements étendus.
- [Cible de fichier](http://msdn.microsoft.com/library/ff878115.aspx) -conteneur de stockage Azure tooan écritures tampons complets.

Hello [suivi d’événements pour Windows (ETW)](http://msdn.microsoft.com/library/ms751538.aspx) API n’est pas disponible pour les événements étendus sur la base de données SQL.

## <a name="restrictions"></a>Restrictions

Il existe quelques différences en matière de sécurité befitting environnement en nuage hello de base de données SQL :

- Événements étendus sont fondées sur le modèle d’isolation du locataire unique hello. Une session d’événements dans une base de données ne peut pas accéder aux données ou événements d’une autre base de données.
- Impossible d’émettre un **CREATE EVENT SESSION** instruction dans le contexte de hello Hello **master** base de données.

## <a name="permission-model"></a>Modèle d’autorisation

Vous devez avoir **contrôle** autorisation sur hello de base de données tooissue un **CREATE EVENT SESSION** instruction. Hello propriétaire de base de données (dbo) a **contrôle** autorisation.

### <a name="storage-container-authorizations"></a>Autorisations de conteneur de stockage

vous générez pour votre conteneur de stockage Azure doit spécifier un jeton SAS Hello **rwl** pour les autorisations de hello. Hello **rwl** valeur fournit hello les autorisations suivantes :

- Lire
- Écrire
- Énumérer

## <a name="performance-considerations"></a>Considérations relatives aux performances

Il existe des scénarios où une utilisation intensive des événements étendus peut s’accumuler au active plus de mémoire qu’est sain pour hello globales du système. Par conséquent hello système de base de données SQL Azure définit dynamiquement et ajuste les limites de quantité hello de la mémoire active qui peut être regroupée par une session d’événements. Plusieurs facteurs entrent dans le calcul de dynamique hello.

Si vous recevez un message d’erreur indiquant qu’une quantité maximale de mémoire a été appliquée, vous pouvez envisager certaines actions correctives, notamment :

- Exécuter moins de sessions d’événement simultanées.
- Via votre **créer** et **ALTER** instructions pour les sessions d’événements, réduire hello de mémoire que vous spécifiez sur hello **MAX\_mémoire** clause.

### <a name="network-latency"></a>Latence du réseau

Hello **fichier d’événements** cible peut rencontrer latence du réseau ou des échecs lors de la persistance tooAzure de données des objets BLOB de stockage. Autres événements dans la base de données SQL peuvent être retardées et en attente pour toocomplete de communication réseau hello. Ce délai peut ralentir votre charge de travail.

- toomitigate ces performances risques, évitez d’utiliser hello **EVENT_RETENTION_MODE** option trop**NO_EVENT_LOSS** dans vos définitions de session d’événements.

## <a name="related-links"></a>Liens connexes

- [Utilisation d’Azure PowerShell avec Azure Storage](../storage/common/storage-powershell-guide-full.md)
- [Applets de commande Azure Storage](http://msdn.microsoft.com/library/dn806401.aspx)
- [À l’aide d’Azure PowerShell avec le stockage Azure](../storage/common/storage-powershell-guide-full.md) -fournit des informations complètes sur PowerShell et hello service de stockage Azure.
- [Comment toouse stockage d’objets Blob à partir de .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md)
- [CREATE CREDENTIAL (Transact-SQL)](http://msdn.microsoft.com/library/ms189522.aspx)
- [CREATE EVENT SESSION (Transact-SQL)](http://msdn.microsoft.com/library/bb677289.aspx)
- [Billets de blog de Jonathan Kehayias sur les événements étendus dans Microsoft SQL Server](http://www.sqlskills.com/blogs/jonathan/category/extended-events/)


- Bonjour Azure *mises à jour de Service* page Web, limitée par le paramètre tooAzure de la base de données SQL :
    - [https://azure.microsoft.com/updates/?service=sql-database](https://azure.microsoft.com/updates/?service=sql-database)


Autres rubriques d’exemples de code pour les événements étendus sont disponibles au hello suivant liens. Toutefois, vous devez vérifier régulièrement les tout toosee exemple qu’exemple hello cible Microsoft SQL Server par rapport à la base de données SQL Azure. Vous pouvez décider si des modifications mineures sont nécessaires toorun hello exemple.

<!--
('lock_acquired' event.)

- Code sample for SQL Server: [Determine Which Queries Are Holding Locks](http://msdn.microsoft.com/library/bb677357.aspx)
- Code sample for SQL Server: [Find hello Objects That Have hello Most Locks Taken on Them](http://msdn.microsoft.com/library/bb630355.aspx)
-->
