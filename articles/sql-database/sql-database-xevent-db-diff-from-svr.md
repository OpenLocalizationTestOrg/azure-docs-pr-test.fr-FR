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
# <a name="extended-events-in-sql-database"></a><span data-ttu-id="57fc3-103">Événement étendus dans la base de données SQL</span><span class="sxs-lookup"><span data-stu-id="57fc3-103">Extended events in SQL Database</span></span>
[!INCLUDE [sql-database-xevents-selectors-1-include](../../includes/sql-database-xevents-selectors-1-include.md)]

<span data-ttu-id="57fc3-104">Cette rubrique explique comment implémentation hello des événements étendus dans la base de données SQL Azure est légèrement différent tooextended comparés dans Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="57fc3-104">This topic explains how hello implementation of extended events in Azure SQL Database is slightly different compared tooextended events in Microsoft SQL Server.</span></span>

- <span data-ttu-id="57fc3-105">Base de données SQL V12 acquise fonctionnalité événements étendus hello hello deuxième semestre calendrier 2015.</span><span class="sxs-lookup"><span data-stu-id="57fc3-105">SQL Database V12 gained hello extended events feature in hello second half of calendar 2015.</span></span>
- <span data-ttu-id="57fc3-106">Cette fonctionnalité est présente dans SQL Server depuis 2008.</span><span class="sxs-lookup"><span data-stu-id="57fc3-106">SQL Server has had extended events since 2008.</span></span>
- <span data-ttu-id="57fc3-107">ensemble de fonctionnalités Hello des événements étendus sur la base de données SQL est un sous-ensemble robust de fonctionnalités hello sur SQL Server.</span><span class="sxs-lookup"><span data-stu-id="57fc3-107">hello feature set of extended events on SQL Database is a robust subset of hello features on SQL Server.</span></span>

<span data-ttu-id="57fc3-108">*XEvents* est un surnom informel parfois utilisé pour désigne les « événements étendus » dans les blogs et autres emplacements informels.</span><span class="sxs-lookup"><span data-stu-id="57fc3-108">*XEvents* is an informal nickname that is sometimes used for 'extended events' in blogs and other informal locations.</span></span>

<span data-ttu-id="57fc3-109">Des informations complémentaires sur les événements étendus, pour Base de données SQL Azure et Microsoft SQL Server, sont disponibles dans :</span><span class="sxs-lookup"><span data-stu-id="57fc3-109">Additional information about extended events, for Azure SQL Database and Microsoft SQL Server, is available at:</span></span>

- [<span data-ttu-id="57fc3-110">Démarrage rapide : Événements étendus dans SQL Server</span><span class="sxs-lookup"><span data-stu-id="57fc3-110">Quick Start: Extended events in SQL Server</span></span>](http://msdn.microsoft.com/library/mt733217.aspx)
- [<span data-ttu-id="57fc3-111">Événements étendus</span><span class="sxs-lookup"><span data-stu-id="57fc3-111">Extended Events</span></span>](http://msdn.microsoft.com/library/bb630282.aspx)

## <a name="prerequisites"></a><span data-ttu-id="57fc3-112">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="57fc3-112">Prerequisites</span></span>

<span data-ttu-id="57fc3-113">Cette rubrique part du principe que vous connaissez déjà les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="57fc3-113">This topic assumes you already have some knowledge of:</span></span>

- <span data-ttu-id="57fc3-114">[Service Base de données SQL Azure](https://azure.microsoft.com/services/sql-database/)</span><span class="sxs-lookup"><span data-stu-id="57fc3-114">[Azure SQL Database service](https://azure.microsoft.com/services/sql-database/).</span></span>
- <span data-ttu-id="57fc3-115">[Événements étendus](http://msdn.microsoft.com/library/bb630282.aspx) dans Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="57fc3-115">[Extended events](http://msdn.microsoft.com/library/bb630282.aspx) in Microsoft SQL Server.</span></span>

- <span data-ttu-id="57fc3-116">bloc Hello de notre documentation sur les événements étendus s’applique tooboth SQL Server et la base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="57fc3-116">hello bulk of our documentation about extended events applies tooboth SQL Server and SQL Database.</span></span>

<span data-ttu-id="57fc3-117">Toohello préalable exposition éléments suivants est utile lorsque vous choisissez hello fichier d’événements en tant que hello [cible](#AzureXEventsTargets):</span><span class="sxs-lookup"><span data-stu-id="57fc3-117">Prior exposure toohello following items is helpful when choosing hello Event File as hello [target](#AzureXEventsTargets):</span></span>

- [<span data-ttu-id="57fc3-118">Service Azure Storage</span><span class="sxs-lookup"><span data-stu-id="57fc3-118">Azure Storage service</span></span>](https://azure.microsoft.com/services/storage/)


- <span data-ttu-id="57fc3-119">PowerShell</span><span class="sxs-lookup"><span data-stu-id="57fc3-119">PowerShell</span></span>
    - <span data-ttu-id="57fc3-120">[À l’aide d’Azure PowerShell avec le stockage Azure](../storage/common/storage-powershell-guide-full.md) -fournit des informations complètes sur PowerShell et hello service de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="57fc3-120">[Using Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md) - Provides comprehensive information about PowerShell and hello Azure Storage service.</span></span>

## <a name="code-samples"></a><span data-ttu-id="57fc3-121">Exemples de code</span><span class="sxs-lookup"><span data-stu-id="57fc3-121">Code samples</span></span>

<span data-ttu-id="57fc3-122">Des rubriques connexes fournissent deux exemples de code :</span><span class="sxs-lookup"><span data-stu-id="57fc3-122">Related topics provide two code samples:</span></span>


- [<span data-ttu-id="57fc3-123">Code cible de la mémoire tampon en anneau pour les événements étendus dans la base de données SQL</span><span class="sxs-lookup"><span data-stu-id="57fc3-123">Ring Buffer target code for extended events in SQL Database</span></span>](sql-database-xevent-code-ring-buffer.md)
    - <span data-ttu-id="57fc3-124">Script Transact-SQL simple court.</span><span class="sxs-lookup"><span data-stu-id="57fc3-124">Short simple Transact-SQL script.</span></span>
    - <span data-ttu-id="57fc3-125">Nous mettre en évidence dans la rubrique d’exemple de code hello que, lorsque vous avez terminé avec une cible de mémoire tampon en anneau, vous devez libérer ses ressources en exécutant alter déroulante `ALTER EVENT SESSION ... ON DATABASE DROP TARGET ...;` instruction.</span><span class="sxs-lookup"><span data-stu-id="57fc3-125">We emphasize in hello code sample topic that, when you are done with a Ring Buffer target, you should release its resources by executing an alter-drop `ALTER EVENT SESSION ... ON DATABASE DROP TARGET ...;` statement.</span></span> <span data-ttu-id="57fc3-126">Vous pouvez ensuite ajouter une autre instance de mémoire tampon en anneau avec l’instruction `ALTER EVENT SESSION ... ON DATABASE ADD TARGET ...`.</span><span class="sxs-lookup"><span data-stu-id="57fc3-126">Later you can add another instance of Ring Buffer by `ALTER EVENT SESSION ... ON DATABASE ADD TARGET ...`.</span></span>


- [<span data-ttu-id="57fc3-127">Code cible du fichier d’événements pour les événements étendus dans la base de données SQL</span><span class="sxs-lookup"><span data-stu-id="57fc3-127">Event File target code for extended events in SQL Database</span></span>](sql-database-xevent-code-event-file.md)
    - <span data-ttu-id="57fc3-128">Phase 1 : PowerShell toocreate un conteneur de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="57fc3-128">Phase 1 is PowerShell toocreate an Azure Storage container.</span></span>
    - <span data-ttu-id="57fc3-129">Phase 2 est Transact-SQL qui utilise le conteneur de stockage Azure hello.</span><span class="sxs-lookup"><span data-stu-id="57fc3-129">Phase 2 is Transact-SQL that uses hello Azure Storage container.</span></span>

## <a name="transact-sql-differences"></a><span data-ttu-id="57fc3-130">Différences Transact-SQL</span><span class="sxs-lookup"><span data-stu-id="57fc3-130">Transact-SQL differences</span></span>


- <span data-ttu-id="57fc3-131">Lorsque vous exécutez hello [CREATE EVENT SESSION](http://msdn.microsoft.com/library/bb677289.aspx) commande sur le serveur SQL Server, vous utilisez hello **ON SERVER** clause.</span><span class="sxs-lookup"><span data-stu-id="57fc3-131">When you execute hello [CREATE EVENT SESSION](http://msdn.microsoft.com/library/bb677289.aspx) command on SQL Server, you use hello **ON SERVER** clause.</span></span> <span data-ttu-id="57fc3-132">Toutefois, sur la base de données SQL vous utiliser hello **ON DATABASE** clause à la place.</span><span class="sxs-lookup"><span data-stu-id="57fc3-132">But on SQL Database you use hello **ON DATABASE** clause instead.</span></span>


- <span data-ttu-id="57fc3-133">Hello **ON DATABASE** clause s’applique également toohello [ALTER EVENT SESSION](http://msdn.microsoft.com/library/bb630368.aspx) et [DROP EVENT SESSION](http://msdn.microsoft.com/library/bb630257.aspx) commandes Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="57fc3-133">hello **ON DATABASE** clause also applies toohello [ALTER EVENT SESSION](http://msdn.microsoft.com/library/bb630368.aspx) and [DROP EVENT SESSION](http://msdn.microsoft.com/library/bb630257.aspx) Transact-SQL commands.</span></span>


- <span data-ttu-id="57fc3-134">Une meilleure pratique est l’option de session d’événement tooinclude hello de **STARTUP_STATE = ON** dans votre **CREATE EVENT SESSION** ou **ALTER EVENT SESSION** instructions.</span><span class="sxs-lookup"><span data-stu-id="57fc3-134">A best practice is tooinclude hello event session option of **STARTUP_STATE = ON** in your **CREATE EVENT SESSION**  or **ALTER EVENT SESSION** statements.</span></span>
    - <span data-ttu-id="57fc3-135">Hello **= ON** valeur prend en charge un redémarrage automatique après une reconfiguration de base de données logique hello en raison du basculement de tooa.</span><span class="sxs-lookup"><span data-stu-id="57fc3-135">hello **= ON** value supports an automatic restart after a reconfiguration of hello logical database due tooa failover.</span></span>

## <a name="new-catalog-views"></a><span data-ttu-id="57fc3-136">Nouvelles vues catalogue</span><span class="sxs-lookup"><span data-stu-id="57fc3-136">New catalog views</span></span>

<span data-ttu-id="57fc3-137">Hello événements étendus est prise en charge par plusieurs [affichages catalogue](http://msdn.microsoft.com/library/ms174365.aspx).</span><span class="sxs-lookup"><span data-stu-id="57fc3-137">hello extended events feature is supported by several [catalog views](http://msdn.microsoft.com/library/ms174365.aspx).</span></span> <span data-ttu-id="57fc3-138">Affichages catalogue vous dire *métadonnées ou des définitions* des sessions d’événements de créés par l’utilisateur dans la base de données actuelle hello.</span><span class="sxs-lookup"><span data-stu-id="57fc3-138">Catalog views tell you about *metadata or definitions* of user-created event sessions in hello current database.</span></span> <span data-ttu-id="57fc3-139">vues de Hello ne retournent pas d’informations sur les instances de sessions d’événements active.</span><span class="sxs-lookup"><span data-stu-id="57fc3-139">hello views do not return information about instances of active event sessions.</span></span>

| <span data-ttu-id="57fc3-140">Nom de</span><span class="sxs-lookup"><span data-stu-id="57fc3-140">Name of</span></span><br/><span data-ttu-id="57fc3-141">la vue catalogue</span><span class="sxs-lookup"><span data-stu-id="57fc3-141">catalog view</span></span> | <span data-ttu-id="57fc3-142">Description</span><span class="sxs-lookup"><span data-stu-id="57fc3-142">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="57fc3-143">**sys.database_event_session_actions**</span><span class="sxs-lookup"><span data-stu-id="57fc3-143">**sys.database_event_session_actions**</span></span> |<span data-ttu-id="57fc3-144">Renvoie une ligne pour chaque action sur chaque événement d’une session d’événements.</span><span class="sxs-lookup"><span data-stu-id="57fc3-144">Returns a row for each action on each event of an event session.</span></span> |
| <span data-ttu-id="57fc3-145">**sys.database_event_session_events**</span><span class="sxs-lookup"><span data-stu-id="57fc3-145">**sys.database_event_session_events**</span></span> |<span data-ttu-id="57fc3-146">Renvoie une ligne pour chaque événement d’une session d’événements.</span><span class="sxs-lookup"><span data-stu-id="57fc3-146">Returns a row for each event in an event session.</span></span> |
| <span data-ttu-id="57fc3-147">**sys.database_event_session_fields**</span><span class="sxs-lookup"><span data-stu-id="57fc3-147">**sys.database_event_session_fields**</span></span> |<span data-ttu-id="57fc3-148">Renvoie une ligne pour chaque colonne pouvant être personnalisée définie explicitement sur les événements et les cibles.</span><span class="sxs-lookup"><span data-stu-id="57fc3-148">Returns a row for each customize-able column that was explicitly set on events and targets.</span></span> |
| <span data-ttu-id="57fc3-149">**sys.database_event_session_targets**</span><span class="sxs-lookup"><span data-stu-id="57fc3-149">**sys.database_event_session_targets**</span></span> |<span data-ttu-id="57fc3-150">Renvoie une ligne pour chaque cible d’événement pour une session d’événements.</span><span class="sxs-lookup"><span data-stu-id="57fc3-150">Returns a row for each event target for an event session.</span></span> |
| <span data-ttu-id="57fc3-151">**sys.database_event_sessions**</span><span class="sxs-lookup"><span data-stu-id="57fc3-151">**sys.database_event_sessions**</span></span> |<span data-ttu-id="57fc3-152">Retourne une ligne pour chaque session d’événements dans la base de données de la base de données SQL hello.</span><span class="sxs-lookup"><span data-stu-id="57fc3-152">Returns a row for each event session in hello SQL Database database.</span></span> |

<span data-ttu-id="57fc3-153">Dans Microsoft SQL Server, les noms des vues catalogue similaires contiennent *.server\_* au lieu de *.database\_*.</span><span class="sxs-lookup"><span data-stu-id="57fc3-153">In Microsoft SQL Server, similar catalog views have names that include *.server\_* instead of *.database\_*.</span></span> <span data-ttu-id="57fc3-154">modèle de nom Hello est similaire à **sys.server_event_%**.</span><span class="sxs-lookup"><span data-stu-id="57fc3-154">hello name pattern is like **sys.server_event_%**.</span></span>

## <a name="new-dynamic-management-views-dmvshttpmsdnmicrosoftcomlibraryms188754aspx"></a><span data-ttu-id="57fc3-155">Nouvelles vues de gestion dynamique [(DMV)](http://msdn.microsoft.com/library/ms188754.aspx)</span><span class="sxs-lookup"><span data-stu-id="57fc3-155">New dynamic management views [(DMVs)](http://msdn.microsoft.com/library/ms188754.aspx)</span></span>

<span data-ttu-id="57fc3-156">La base de données SQL Azure comporte des [vues de gestion dynamique (DMV)](http://msdn.microsoft.com/library/bb677293.aspx) qui prennent en charge les événements étendus.</span><span class="sxs-lookup"><span data-stu-id="57fc3-156">Azure SQL Database has [dynamic management views (DMVs)](http://msdn.microsoft.com/library/bb677293.aspx) that support extended events.</span></span> <span data-ttu-id="57fc3-157">Les vues de gestion dynamique vous renseignent sur les sessions d’événements *actives* .</span><span class="sxs-lookup"><span data-stu-id="57fc3-157">DMVs tell you about *active* event sessions.</span></span>

| <span data-ttu-id="57fc3-158">Nom de la vue de gestion dynamique</span><span class="sxs-lookup"><span data-stu-id="57fc3-158">Name of DMV</span></span> | <span data-ttu-id="57fc3-159">Description</span><span class="sxs-lookup"><span data-stu-id="57fc3-159">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="57fc3-160">**sys.dm_xe_database_session_event_actions**</span><span class="sxs-lookup"><span data-stu-id="57fc3-160">**sys.dm_xe_database_session_event_actions**</span></span> |<span data-ttu-id="57fc3-161">Renvoie des informations sur les actions d’une session d’événements.</span><span class="sxs-lookup"><span data-stu-id="57fc3-161">Returns information about event session actions.</span></span> |
| <span data-ttu-id="57fc3-162">**sys.dm_xe_database_session_events**</span><span class="sxs-lookup"><span data-stu-id="57fc3-162">**sys.dm_xe_database_session_events**</span></span> |<span data-ttu-id="57fc3-163">Renvoie des informations sur les sessions d’événements.</span><span class="sxs-lookup"><span data-stu-id="57fc3-163">Returns information about session events.</span></span> |
| <span data-ttu-id="57fc3-164">**sys.dm_xe_database_session_object_columns**</span><span class="sxs-lookup"><span data-stu-id="57fc3-164">**sys.dm_xe_database_session_object_columns**</span></span> |<span data-ttu-id="57fc3-165">Indique les valeurs de configuration de hello pour les objets qui sont liées tooa session.</span><span class="sxs-lookup"><span data-stu-id="57fc3-165">Shows hello configuration values for objects that are bound tooa session.</span></span> |
| <span data-ttu-id="57fc3-166">**sys.dm_xe_database_session_targets**</span><span class="sxs-lookup"><span data-stu-id="57fc3-166">**sys.dm_xe_database_session_targets**</span></span> |<span data-ttu-id="57fc3-167">Renvoie des informations sur les cibles d’une session d’événements.</span><span class="sxs-lookup"><span data-stu-id="57fc3-167">Returns information about session targets.</span></span> |
| <span data-ttu-id="57fc3-168">**sys.dm_xe_database_sessions**</span><span class="sxs-lookup"><span data-stu-id="57fc3-168">**sys.dm_xe_database_sessions**</span></span> |<span data-ttu-id="57fc3-169">Retourne une ligne pour chaque session d’événements est étendue toohello de base de données actuelle.</span><span class="sxs-lookup"><span data-stu-id="57fc3-169">Returns a row for each event session that is scoped toohello current database.</span></span> |

<span data-ttu-id="57fc3-170">Dans Microsoft SQL Server, les vues de catalogue similaires sont nommés sans hello  *\_base de données* nom de la partie de hello, tel que :</span><span class="sxs-lookup"><span data-stu-id="57fc3-170">In Microsoft SQL Server, similar catalog views are named without hello *\_database* portion of hello name, such as:</span></span>

- <span data-ttu-id="57fc3-171">**sys.dm_xe_sessions**, au lieu de name</span><span class="sxs-lookup"><span data-stu-id="57fc3-171">**sys.dm_xe_sessions**, instead of name</span></span><br/><span data-ttu-id="57fc3-172">**sys.dm_xe_database_sessions**.</span><span class="sxs-lookup"><span data-stu-id="57fc3-172">**sys.dm_xe_database_sessions**.</span></span>

### <a name="dmvs-common-tooboth"></a><span data-ttu-id="57fc3-173">Tooboth commune de vues de gestion dynamique</span><span class="sxs-lookup"><span data-stu-id="57fc3-173">DMVs common tooboth</span></span>
<span data-ttu-id="57fc3-174">Il existe des vues DMV supplémentaires qui sont commune tooboth de base de données SQL Azure et Microsoft SQL Server pour les événements étendus :</span><span class="sxs-lookup"><span data-stu-id="57fc3-174">For extended events there are additional DMVs that are common tooboth Azure SQL Database and Microsoft SQL Server:</span></span>

- <span data-ttu-id="57fc3-175">**sys.dm_xe_map_values**</span><span class="sxs-lookup"><span data-stu-id="57fc3-175">**sys.dm_xe_map_values**</span></span>
- <span data-ttu-id="57fc3-176">**sys.dm_xe_object_columns**</span><span class="sxs-lookup"><span data-stu-id="57fc3-176">**sys.dm_xe_object_columns**</span></span>
- <span data-ttu-id="57fc3-177">**sys.dm_xe_objects**</span><span class="sxs-lookup"><span data-stu-id="57fc3-177">**sys.dm_xe_objects**</span></span>
- <span data-ttu-id="57fc3-178">**sys.dm_xe_packages**</span><span class="sxs-lookup"><span data-stu-id="57fc3-178">**sys.dm_xe_packages**</span></span>

 <a name="sqlfindseventsactionstargets" id="sqlfindseventsactionstargets"></a>

## <a name="find-hello-available-extended-events-actions-and-targets"></a><span data-ttu-id="57fc3-179">Rechercher les cibles, les actions et les événements étendus disponible hello</span><span class="sxs-lookup"><span data-stu-id="57fc3-179">Find hello available extended events, actions, and targets</span></span>

<span data-ttu-id="57fc3-180">Vous pouvez exécuter une simple SQL **sélectionnez** tooobtain une liste des événements disponibles de hello, actions et cibles.</span><span class="sxs-lookup"><span data-stu-id="57fc3-180">You can run a simple SQL **SELECT** tooobtain a list of hello available events, actions, and target.</span></span>

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


<span data-ttu-id="57fc3-181"><a name="AzureXEventsTargets" id="AzureXEventsTargets"></a>&nbsp;</span><span class="sxs-lookup"><span data-stu-id="57fc3-181"><a name="AzureXEventsTargets" id="AzureXEventsTargets"></a> &nbsp;</span></span>

## <a name="targets-for-your-sql-database-event-sessions"></a><span data-ttu-id="57fc3-182">Cibles de vos sessions d’événements de Base de données SQL</span><span class="sxs-lookup"><span data-stu-id="57fc3-182">Targets for your SQL Database event sessions</span></span>

<span data-ttu-id="57fc3-183">Voici les cibles capables de capturer des résultats à partir de vos sessions d’événements sur la base de données SQL :</span><span class="sxs-lookup"><span data-stu-id="57fc3-183">Here are targets that can capture results from your event sessions on SQL Database:</span></span>

- <span data-ttu-id="57fc3-184">[Cible de mémoire tampon en anneau](http://msdn.microsoft.com/library/ff878182.aspx) -Maintient brièvement les données d’événements en mémoire.</span><span class="sxs-lookup"><span data-stu-id="57fc3-184">[Ring Buffer target](http://msdn.microsoft.com/library/ff878182.aspx) - Briefly holds event data in memory.</span></span>
- <span data-ttu-id="57fc3-185">[Cible de compteur d’événements](http://msdn.microsoft.com/library/ff878025.aspx) - Compte tous les événements qui se produisent pendant une session d’événements étendus.</span><span class="sxs-lookup"><span data-stu-id="57fc3-185">[Event Counter target](http://msdn.microsoft.com/library/ff878025.aspx) - Counts all events that occur during an extended events session.</span></span>
- <span data-ttu-id="57fc3-186">[Cible de fichier](http://msdn.microsoft.com/library/ff878115.aspx) -conteneur de stockage Azure tooan écritures tampons complets.</span><span class="sxs-lookup"><span data-stu-id="57fc3-186">[Event File target](http://msdn.microsoft.com/library/ff878115.aspx) - Writes complete buffers tooan Azure Storage container.</span></span>

<span data-ttu-id="57fc3-187">Hello [suivi d’événements pour Windows (ETW)](http://msdn.microsoft.com/library/ms751538.aspx) API n’est pas disponible pour les événements étendus sur la base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="57fc3-187">hello [Event Tracing for Windows (ETW)](http://msdn.microsoft.com/library/ms751538.aspx) API is not available for extended events on SQL Database.</span></span>

## <a name="restrictions"></a><span data-ttu-id="57fc3-188">Restrictions</span><span class="sxs-lookup"><span data-stu-id="57fc3-188">Restrictions</span></span>

<span data-ttu-id="57fc3-189">Il existe quelques différences en matière de sécurité befitting environnement en nuage hello de base de données SQL :</span><span class="sxs-lookup"><span data-stu-id="57fc3-189">There are a couple of security-related differences befitting hello cloud environment of SQL Database:</span></span>

- <span data-ttu-id="57fc3-190">Événements étendus sont fondées sur le modèle d’isolation du locataire unique hello.</span><span class="sxs-lookup"><span data-stu-id="57fc3-190">Extended events are founded on hello single-tenant isolation model.</span></span> <span data-ttu-id="57fc3-191">Une session d’événements dans une base de données ne peut pas accéder aux données ou événements d’une autre base de données.</span><span class="sxs-lookup"><span data-stu-id="57fc3-191">An event session in one database cannot access data or events from another database.</span></span>
- <span data-ttu-id="57fc3-192">Impossible d’émettre un **CREATE EVENT SESSION** instruction dans le contexte de hello Hello **master** base de données.</span><span class="sxs-lookup"><span data-stu-id="57fc3-192">You cannot issue a **CREATE EVENT SESSION** statement in hello context of hello **master** database.</span></span>

## <a name="permission-model"></a><span data-ttu-id="57fc3-193">Modèle d’autorisation</span><span class="sxs-lookup"><span data-stu-id="57fc3-193">Permission model</span></span>

<span data-ttu-id="57fc3-194">Vous devez avoir **contrôle** autorisation sur hello de base de données tooissue un **CREATE EVENT SESSION** instruction.</span><span class="sxs-lookup"><span data-stu-id="57fc3-194">You must have **Control** permission on hello database tooissue a **CREATE EVENT SESSION** statement.</span></span> <span data-ttu-id="57fc3-195">Hello propriétaire de base de données (dbo) a **contrôle** autorisation.</span><span class="sxs-lookup"><span data-stu-id="57fc3-195">hello database owner (dbo) has **Control** permission.</span></span>

### <a name="storage-container-authorizations"></a><span data-ttu-id="57fc3-196">Autorisations de conteneur de stockage</span><span class="sxs-lookup"><span data-stu-id="57fc3-196">Storage container authorizations</span></span>

<span data-ttu-id="57fc3-197">vous générez pour votre conteneur de stockage Azure doit spécifier un jeton SAS Hello **rwl** pour les autorisations de hello.</span><span class="sxs-lookup"><span data-stu-id="57fc3-197">hello SAS token you generate for your Azure Storage container must specify **rwl** for hello permissions.</span></span> <span data-ttu-id="57fc3-198">Hello **rwl** valeur fournit hello les autorisations suivantes :</span><span class="sxs-lookup"><span data-stu-id="57fc3-198">hello **rwl** value provides hello following permissions:</span></span>

- <span data-ttu-id="57fc3-199">Lire</span><span class="sxs-lookup"><span data-stu-id="57fc3-199">Read</span></span>
- <span data-ttu-id="57fc3-200">Écrire</span><span class="sxs-lookup"><span data-stu-id="57fc3-200">Write</span></span>
- <span data-ttu-id="57fc3-201">Énumérer</span><span class="sxs-lookup"><span data-stu-id="57fc3-201">List</span></span>

## <a name="performance-considerations"></a><span data-ttu-id="57fc3-202">Considérations relatives aux performances</span><span class="sxs-lookup"><span data-stu-id="57fc3-202">Performance considerations</span></span>

<span data-ttu-id="57fc3-203">Il existe des scénarios où une utilisation intensive des événements étendus peut s’accumuler au active plus de mémoire qu’est sain pour hello globales du système.</span><span class="sxs-lookup"><span data-stu-id="57fc3-203">There are scenarios where intensive use of extended events can accumulate more active memory than is healthy for hello overall system.</span></span> <span data-ttu-id="57fc3-204">Par conséquent hello système de base de données SQL Azure définit dynamiquement et ajuste les limites de quantité hello de la mémoire active qui peut être regroupée par une session d’événements.</span><span class="sxs-lookup"><span data-stu-id="57fc3-204">Therefore hello Azure SQL Database system dynamically sets and adjusts limits on hello amount of active memory that can be accumulated by an event session.</span></span> <span data-ttu-id="57fc3-205">Plusieurs facteurs entrent dans le calcul de dynamique hello.</span><span class="sxs-lookup"><span data-stu-id="57fc3-205">Many factors go into hello dynamic calculation.</span></span>

<span data-ttu-id="57fc3-206">Si vous recevez un message d’erreur indiquant qu’une quantité maximale de mémoire a été appliquée, vous pouvez envisager certaines actions correctives, notamment :</span><span class="sxs-lookup"><span data-stu-id="57fc3-206">If you receive an error message that says a memory maximum was enforced, some corrective actions you can take are:</span></span>

- <span data-ttu-id="57fc3-207">Exécuter moins de sessions d’événement simultanées.</span><span class="sxs-lookup"><span data-stu-id="57fc3-207">Run fewer concurrent event sessions.</span></span>
- <span data-ttu-id="57fc3-208">Via votre **créer** et **ALTER** instructions pour les sessions d’événements, réduire hello de mémoire que vous spécifiez sur hello **MAX\_mémoire** clause.</span><span class="sxs-lookup"><span data-stu-id="57fc3-208">Through your **CREATE** and **ALTER** statements for event sessions, reduce hello amount of memory you specify on hello **MAX\_MEMORY** clause.</span></span>

### <a name="network-latency"></a><span data-ttu-id="57fc3-209">Latence du réseau</span><span class="sxs-lookup"><span data-stu-id="57fc3-209">Network latency</span></span>

<span data-ttu-id="57fc3-210">Hello **fichier d’événements** cible peut rencontrer latence du réseau ou des échecs lors de la persistance tooAzure de données des objets BLOB de stockage.</span><span class="sxs-lookup"><span data-stu-id="57fc3-210">hello **Event File** target might experience network latency or failures while persisting data tooAzure Storage blobs.</span></span> <span data-ttu-id="57fc3-211">Autres événements dans la base de données SQL peuvent être retardées et en attente pour toocomplete de communication réseau hello.</span><span class="sxs-lookup"><span data-stu-id="57fc3-211">Other events in SQL Database might be delayed while they wait for hello network communication toocomplete.</span></span> <span data-ttu-id="57fc3-212">Ce délai peut ralentir votre charge de travail.</span><span class="sxs-lookup"><span data-stu-id="57fc3-212">This delay can slow your workload.</span></span>

- <span data-ttu-id="57fc3-213">toomitigate ces performances risques, évitez d’utiliser hello **EVENT_RETENTION_MODE** option trop**NO_EVENT_LOSS** dans vos définitions de session d’événements.</span><span class="sxs-lookup"><span data-stu-id="57fc3-213">toomitigate this performance risk, avoid setting hello **EVENT_RETENTION_MODE** option too**NO_EVENT_LOSS** in your event session definitions.</span></span>

## <a name="related-links"></a><span data-ttu-id="57fc3-214">Liens connexes</span><span class="sxs-lookup"><span data-stu-id="57fc3-214">Related links</span></span>

- <span data-ttu-id="57fc3-215">[Utilisation d’Azure PowerShell avec Azure Storage](../storage/common/storage-powershell-guide-full.md)</span><span class="sxs-lookup"><span data-stu-id="57fc3-215">[Using Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md).</span></span>
- [<span data-ttu-id="57fc3-216">Applets de commande Azure Storage</span><span class="sxs-lookup"><span data-stu-id="57fc3-216">Azure Storage Cmdlets</span></span>](http://msdn.microsoft.com/library/dn806401.aspx)
- <span data-ttu-id="57fc3-217">[À l’aide d’Azure PowerShell avec le stockage Azure](../storage/common/storage-powershell-guide-full.md) -fournit des informations complètes sur PowerShell et hello service de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="57fc3-217">[Using Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md) - Provides comprehensive information about PowerShell and hello Azure Storage service.</span></span>
- [<span data-ttu-id="57fc3-218">Comment toouse stockage d’objets Blob à partir de .NET</span><span class="sxs-lookup"><span data-stu-id="57fc3-218">How toouse Blob storage from .NET</span></span>](../storage/blobs/storage-dotnet-how-to-use-blobs.md)
- [<span data-ttu-id="57fc3-219">CREATE CREDENTIAL (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="57fc3-219">CREATE CREDENTIAL (Transact-SQL)</span></span>](http://msdn.microsoft.com/library/ms189522.aspx)
- [<span data-ttu-id="57fc3-220">CREATE EVENT SESSION (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="57fc3-220">CREATE EVENT SESSION (Transact-SQL)</span></span>](http://msdn.microsoft.com/library/bb677289.aspx)
- [<span data-ttu-id="57fc3-221">Billets de blog de Jonathan Kehayias sur les événements étendus dans Microsoft SQL Server</span><span class="sxs-lookup"><span data-stu-id="57fc3-221">Jonathan Kehayias' blog posts about extended events in Microsoft SQL Server</span></span>](http://www.sqlskills.com/blogs/jonathan/category/extended-events/)


- <span data-ttu-id="57fc3-222">Bonjour Azure *mises à jour de Service* page Web, limitée par le paramètre tooAzure de la base de données SQL :</span><span class="sxs-lookup"><span data-stu-id="57fc3-222">hello Azure *Service Updates* webpage, narrowed by parameter tooAzure SQL Database:</span></span>
    - [<span data-ttu-id="57fc3-223">https://azure.microsoft.com/updates/?service=sql-database</span><span class="sxs-lookup"><span data-stu-id="57fc3-223">https://azure.microsoft.com/updates/?service=sql-database</span></span>](https://azure.microsoft.com/updates/?service=sql-database)


<span data-ttu-id="57fc3-224">Autres rubriques d’exemples de code pour les événements étendus sont disponibles au hello suivant liens.</span><span class="sxs-lookup"><span data-stu-id="57fc3-224">Other code sample topics for extended events are available at hello following links.</span></span> <span data-ttu-id="57fc3-225">Toutefois, vous devez vérifier régulièrement les tout toosee exemple qu’exemple hello cible Microsoft SQL Server par rapport à la base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="57fc3-225">However, you must routinely check any sample toosee whether hello sample targets Microsoft SQL Server versus Azure SQL Database.</span></span> <span data-ttu-id="57fc3-226">Vous pouvez décider si des modifications mineures sont nécessaires toorun hello exemple.</span><span class="sxs-lookup"><span data-stu-id="57fc3-226">Then you can decide whether minor changes are needed toorun hello sample.</span></span>

<!--
('lock_acquired' event.)

- Code sample for SQL Server: [Determine Which Queries Are Holding Locks](http://msdn.microsoft.com/library/bb677357.aspx)
- Code sample for SQL Server: [Find hello Objects That Have hello Most Locks Taken on Them](http://msdn.microsoft.com/library/bb630355.aspx)
-->
