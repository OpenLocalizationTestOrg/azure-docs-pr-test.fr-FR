---
title: "Événement étendus dans SQL Database | Microsoft Docs"
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
ms.openlocfilehash: 7e5da1c32484b0b94d2ad32ead6bb7c28f9744aa
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="extended-events-in-sql-database"></a><span data-ttu-id="921b5-103">Événement étendus dans la base de données SQL</span><span class="sxs-lookup"><span data-stu-id="921b5-103">Extended events in SQL Database</span></span>
[!INCLUDE [sql-database-xevents-selectors-1-include](../../includes/sql-database-xevents-selectors-1-include.md)]

<span data-ttu-id="921b5-104">Cette rubrique explique les quelques différences entre l’implémentation d’événements étendus dans la base de données SQL Azure et dans Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="921b5-104">This topic explains how the implementation of extended events in Azure SQL Database is slightly different compared to extended events in Microsoft SQL Server.</span></span>

- <span data-ttu-id="921b5-105">La base de données SQL V12 a intégré la fonctionnalité d’événements étendus au cours de la seconde moitié du calendrier 2015.</span><span class="sxs-lookup"><span data-stu-id="921b5-105">SQL Database V12 gained the extended events feature in the second half of calendar 2015.</span></span>
- <span data-ttu-id="921b5-106">Cette fonctionnalité est présente dans SQL Server depuis 2008.</span><span class="sxs-lookup"><span data-stu-id="921b5-106">SQL Server has had extended events since 2008.</span></span>
- <span data-ttu-id="921b5-107">L’ensemble de fonctionnalités des événements étendus sur la base de données SQL est un sous-ensemble robuste des fonctionnalités de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="921b5-107">The feature set of extended events on SQL Database is a robust subset of the features on SQL Server.</span></span>

<span data-ttu-id="921b5-108">*XEvents* est un surnom informel parfois utilisé pour désigne les « événements étendus » dans les blogs et autres emplacements informels.</span><span class="sxs-lookup"><span data-stu-id="921b5-108">*XEvents* is an informal nickname that is sometimes used for 'extended events' in blogs and other informal locations.</span></span>

<span data-ttu-id="921b5-109">Des informations complémentaires sur les événements étendus, pour Base de données SQL Azure et Microsoft SQL Server, sont disponibles dans :</span><span class="sxs-lookup"><span data-stu-id="921b5-109">Additional information about extended events, for Azure SQL Database and Microsoft SQL Server, is available at:</span></span>

- [<span data-ttu-id="921b5-110">Démarrage rapide : Événements étendus dans SQL Server</span><span class="sxs-lookup"><span data-stu-id="921b5-110">Quick Start: Extended events in SQL Server</span></span>](http://msdn.microsoft.com/library/mt733217.aspx)
- [<span data-ttu-id="921b5-111">Événements étendus</span><span class="sxs-lookup"><span data-stu-id="921b5-111">Extended Events</span></span>](http://msdn.microsoft.com/library/bb630282.aspx)

## <a name="prerequisites"></a><span data-ttu-id="921b5-112">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="921b5-112">Prerequisites</span></span>

<span data-ttu-id="921b5-113">Cette rubrique part du principe que vous connaissez déjà les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="921b5-113">This topic assumes you already have some knowledge of:</span></span>

- <span data-ttu-id="921b5-114">[Service Base de données SQL Azure](https://azure.microsoft.com/services/sql-database/)</span><span class="sxs-lookup"><span data-stu-id="921b5-114">[Azure SQL Database service](https://azure.microsoft.com/services/sql-database/).</span></span>
- <span data-ttu-id="921b5-115">[Événements étendus](http://msdn.microsoft.com/library/bb630282.aspx) dans Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="921b5-115">[Extended events](http://msdn.microsoft.com/library/bb630282.aspx) in Microsoft SQL Server.</span></span>

- <span data-ttu-id="921b5-116">La majeure partie de notre documentation sur les événements étendus s’applique à SQL Server et au service Base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="921b5-116">The bulk of our documentation about extended events applies to both SQL Server and SQL Database.</span></span>

<span data-ttu-id="921b5-117">Il est utile d’avoir une connaissance préalable des éléments suivants lorsque vous choisissez le fichier d’événements comme [cible](#AzureXEventsTargets):</span><span class="sxs-lookup"><span data-stu-id="921b5-117">Prior exposure to the following items is helpful when choosing the Event File as the [target](#AzureXEventsTargets):</span></span>

- [<span data-ttu-id="921b5-118">Service Azure Storage</span><span class="sxs-lookup"><span data-stu-id="921b5-118">Azure Storage service</span></span>](https://azure.microsoft.com/services/storage/)


- <span data-ttu-id="921b5-119">PowerShell</span><span class="sxs-lookup"><span data-stu-id="921b5-119">PowerShell</span></span>
    - <span data-ttu-id="921b5-120">[Utilisation d’Azure PowerShell avec Azure Storage](../storage/common/storage-powershell-guide-full.md) - Cette rubrique fournit des informations complètes sur PowerShell et le service Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="921b5-120">[Using Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md) - Provides comprehensive information about PowerShell and the Azure Storage service.</span></span>

## <a name="code-samples"></a><span data-ttu-id="921b5-121">Exemples de code</span><span class="sxs-lookup"><span data-stu-id="921b5-121">Code samples</span></span>

<span data-ttu-id="921b5-122">Des rubriques connexes fournissent deux exemples de code :</span><span class="sxs-lookup"><span data-stu-id="921b5-122">Related topics provide two code samples:</span></span>


- [<span data-ttu-id="921b5-123">Code cible de la mémoire tampon en anneau pour les événements étendus dans la base de données SQL</span><span class="sxs-lookup"><span data-stu-id="921b5-123">Ring Buffer target code for extended events in SQL Database</span></span>](sql-database-xevent-code-ring-buffer.md)
    - <span data-ttu-id="921b5-124">Script Transact-SQL simple court.</span><span class="sxs-lookup"><span data-stu-id="921b5-124">Short simple Transact-SQL script.</span></span>
    - <span data-ttu-id="921b5-125">Dans la rubrique concernant l’exemple de code, nous insistons sur le fait que, lorsque vous avez fini de traiter une cible de la mémoire tampon en anneau, vous devez en libérer les ressources en exécutant une instruction `ALTER EVENT SESSION ... ON DATABASE DROP TARGET ...;` alter-drop.</span><span class="sxs-lookup"><span data-stu-id="921b5-125">We emphasize in the code sample topic that, when you are done with a Ring Buffer target, you should release its resources by executing an alter-drop `ALTER EVENT SESSION ... ON DATABASE DROP TARGET ...;` statement.</span></span> <span data-ttu-id="921b5-126">Vous pouvez ensuite ajouter une autre instance de mémoire tampon en anneau avec l’instruction `ALTER EVENT SESSION ... ON DATABASE ADD TARGET ...`.</span><span class="sxs-lookup"><span data-stu-id="921b5-126">Later you can add another instance of Ring Buffer by `ALTER EVENT SESSION ... ON DATABASE ADD TARGET ...`.</span></span>


- [<span data-ttu-id="921b5-127">Code cible du fichier d’événements pour les événements étendus dans la base de données SQL</span><span class="sxs-lookup"><span data-stu-id="921b5-127">Event File target code for extended events in SQL Database</span></span>](sql-database-xevent-code-event-file.md)
    - <span data-ttu-id="921b5-128">La Phase 1 est PowerShell pour créer un conteneur Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="921b5-128">Phase 1 is PowerShell to create an Azure Storage container.</span></span>
    - <span data-ttu-id="921b5-129">La Phase 2 est Transact-SQL qui utilise le conteneur Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="921b5-129">Phase 2 is Transact-SQL that uses the Azure Storage container.</span></span>

## <a name="transact-sql-differences"></a><span data-ttu-id="921b5-130">Différences Transact-SQL</span><span class="sxs-lookup"><span data-stu-id="921b5-130">Transact-SQL differences</span></span>


- <span data-ttu-id="921b5-131">Lorsque vous exécutez la commande [CREATE EVENT SESSION](http://msdn.microsoft.com/library/bb677289.aspx) sur SQL Server, vous pouvez utiliser la clause **ON SERVER** .</span><span class="sxs-lookup"><span data-stu-id="921b5-131">When you execute the [CREATE EVENT SESSION](http://msdn.microsoft.com/library/bb677289.aspx) command on SQL Server, you use the **ON SERVER** clause.</span></span> <span data-ttu-id="921b5-132">Mais sur la base de données SQL vous utilisez la clause **ON DATABASE** à la place.</span><span class="sxs-lookup"><span data-stu-id="921b5-132">But on SQL Database you use the **ON DATABASE** clause instead.</span></span>


- <span data-ttu-id="921b5-133">La clause **ON DATABASE** s’applique également aux commandes Transact-SQL [ALTER EVENT SESSION](http://msdn.microsoft.com/library/bb630368.aspx) et [DROP EVENT SESSION](http://msdn.microsoft.com/library/bb630257.aspx).</span><span class="sxs-lookup"><span data-stu-id="921b5-133">The **ON DATABASE** clause also applies to the [ALTER EVENT SESSION](http://msdn.microsoft.com/library/bb630368.aspx) and [DROP EVENT SESSION](http://msdn.microsoft.com/library/bb630257.aspx) Transact-SQL commands.</span></span>


- <span data-ttu-id="921b5-134">Il est recommandé d’inclure l’option de session d’événement de **STARTUP_STATE = ON** dans vos instructions **CREATE EVENT SESSION** ou **ALTER EVENT SESSION**.</span><span class="sxs-lookup"><span data-stu-id="921b5-134">A best practice is to include the event session option of **STARTUP_STATE = ON** in your **CREATE EVENT SESSION**  or **ALTER EVENT SESSION** statements.</span></span>
    - <span data-ttu-id="921b5-135">La valeur **= ON** prend en charge le redémarrage automatique après la reconfiguration de la base de données logique en raison d’un basculement.</span><span class="sxs-lookup"><span data-stu-id="921b5-135">The **= ON** value supports an automatic restart after a reconfiguration of the logical database due to a failover.</span></span>

## <a name="new-catalog-views"></a><span data-ttu-id="921b5-136">Nouvelles vues catalogue</span><span class="sxs-lookup"><span data-stu-id="921b5-136">New catalog views</span></span>

<span data-ttu-id="921b5-137">La fonctionnalité des événements étendus est prise en charge par plusieurs [vues catalogue](http://msdn.microsoft.com/library/ms174365.aspx).</span><span class="sxs-lookup"><span data-stu-id="921b5-137">The extended events feature is supported by several [catalog views](http://msdn.microsoft.com/library/ms174365.aspx).</span></span> <span data-ttu-id="921b5-138">Les vues catalogue vous indiquent les *métadonnées ou définitions* des sessions d’événements créées par l’utilisateur dans la base de données actuelle.</span><span class="sxs-lookup"><span data-stu-id="921b5-138">Catalog views tell you about *metadata or definitions* of user-created event sessions in the current database.</span></span> <span data-ttu-id="921b5-139">Les affichages ne renvoient pas d’informations sur les instances des sessions d’événements actives.</span><span class="sxs-lookup"><span data-stu-id="921b5-139">The views do not return information about instances of active event sessions.</span></span>

| <span data-ttu-id="921b5-140">Nom de</span><span class="sxs-lookup"><span data-stu-id="921b5-140">Name of</span></span><br/><span data-ttu-id="921b5-141">la vue catalogue</span><span class="sxs-lookup"><span data-stu-id="921b5-141">catalog view</span></span> | <span data-ttu-id="921b5-142">Description</span><span class="sxs-lookup"><span data-stu-id="921b5-142">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="921b5-143">**sys.database_event_session_actions**</span><span class="sxs-lookup"><span data-stu-id="921b5-143">**sys.database_event_session_actions**</span></span> |<span data-ttu-id="921b5-144">Renvoie une ligne pour chaque action sur chaque événement d’une session d’événements.</span><span class="sxs-lookup"><span data-stu-id="921b5-144">Returns a row for each action on each event of an event session.</span></span> |
| <span data-ttu-id="921b5-145">**sys.database_event_session_events**</span><span class="sxs-lookup"><span data-stu-id="921b5-145">**sys.database_event_session_events**</span></span> |<span data-ttu-id="921b5-146">Renvoie une ligne pour chaque événement d’une session d’événements.</span><span class="sxs-lookup"><span data-stu-id="921b5-146">Returns a row for each event in an event session.</span></span> |
| <span data-ttu-id="921b5-147">**sys.database_event_session_fields**</span><span class="sxs-lookup"><span data-stu-id="921b5-147">**sys.database_event_session_fields**</span></span> |<span data-ttu-id="921b5-148">Renvoie une ligne pour chaque colonne pouvant être personnalisée définie explicitement sur les événements et les cibles.</span><span class="sxs-lookup"><span data-stu-id="921b5-148">Returns a row for each customize-able column that was explicitly set on events and targets.</span></span> |
| <span data-ttu-id="921b5-149">**sys.database_event_session_targets**</span><span class="sxs-lookup"><span data-stu-id="921b5-149">**sys.database_event_session_targets**</span></span> |<span data-ttu-id="921b5-150">Renvoie une ligne pour chaque cible d’événement pour une session d’événements.</span><span class="sxs-lookup"><span data-stu-id="921b5-150">Returns a row for each event target for an event session.</span></span> |
| <span data-ttu-id="921b5-151">**sys.database_event_sessions**</span><span class="sxs-lookup"><span data-stu-id="921b5-151">**sys.database_event_sessions**</span></span> |<span data-ttu-id="921b5-152">Renvoie une ligne pour chaque session d’événements dans la base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="921b5-152">Returns a row for each event session in the SQL Database database.</span></span> |

<span data-ttu-id="921b5-153">Dans Microsoft SQL Server, les noms des vues catalogue similaires contiennent *.server\_* au lieu de *.database\_*.</span><span class="sxs-lookup"><span data-stu-id="921b5-153">In Microsoft SQL Server, similar catalog views have names that include *.server\_* instead of *.database\_*.</span></span> <span data-ttu-id="921b5-154">Les noms suivent le modèle **sys.server_event_%**.</span><span class="sxs-lookup"><span data-stu-id="921b5-154">The name pattern is like **sys.server_event_%**.</span></span>

## <a name="new-dynamic-management-views-dmvshttpmsdnmicrosoftcomlibraryms188754aspx"></a><span data-ttu-id="921b5-155">Nouvelles vues de gestion dynamique [(DMV)](http://msdn.microsoft.com/library/ms188754.aspx)</span><span class="sxs-lookup"><span data-stu-id="921b5-155">New dynamic management views [(DMVs)](http://msdn.microsoft.com/library/ms188754.aspx)</span></span>

<span data-ttu-id="921b5-156">La base de données SQL Azure comporte des [vues de gestion dynamique (DMV)](http://msdn.microsoft.com/library/bb677293.aspx) qui prennent en charge les événements étendus.</span><span class="sxs-lookup"><span data-stu-id="921b5-156">Azure SQL Database has [dynamic management views (DMVs)](http://msdn.microsoft.com/library/bb677293.aspx) that support extended events.</span></span> <span data-ttu-id="921b5-157">Les vues de gestion dynamique vous renseignent sur les sessions d’événements *actives* .</span><span class="sxs-lookup"><span data-stu-id="921b5-157">DMVs tell you about *active* event sessions.</span></span>

| <span data-ttu-id="921b5-158">Nom de la vue de gestion dynamique</span><span class="sxs-lookup"><span data-stu-id="921b5-158">Name of DMV</span></span> | <span data-ttu-id="921b5-159">Description</span><span class="sxs-lookup"><span data-stu-id="921b5-159">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="921b5-160">**sys.dm_xe_database_session_event_actions**</span><span class="sxs-lookup"><span data-stu-id="921b5-160">**sys.dm_xe_database_session_event_actions**</span></span> |<span data-ttu-id="921b5-161">Renvoie des informations sur les actions d’une session d’événements.</span><span class="sxs-lookup"><span data-stu-id="921b5-161">Returns information about event session actions.</span></span> |
| <span data-ttu-id="921b5-162">**sys.dm_xe_database_session_events**</span><span class="sxs-lookup"><span data-stu-id="921b5-162">**sys.dm_xe_database_session_events**</span></span> |<span data-ttu-id="921b5-163">Renvoie des informations sur les sessions d’événements.</span><span class="sxs-lookup"><span data-stu-id="921b5-163">Returns information about session events.</span></span> |
| <span data-ttu-id="921b5-164">**sys.dm_xe_database_session_object_columns**</span><span class="sxs-lookup"><span data-stu-id="921b5-164">**sys.dm_xe_database_session_object_columns**</span></span> |<span data-ttu-id="921b5-165">Montre les valeurs de configuration pour les objets liés à une session.</span><span class="sxs-lookup"><span data-stu-id="921b5-165">Shows the configuration values for objects that are bound to a session.</span></span> |
| <span data-ttu-id="921b5-166">**sys.dm_xe_database_session_targets**</span><span class="sxs-lookup"><span data-stu-id="921b5-166">**sys.dm_xe_database_session_targets**</span></span> |<span data-ttu-id="921b5-167">Renvoie des informations sur les cibles d’une session d’événements.</span><span class="sxs-lookup"><span data-stu-id="921b5-167">Returns information about session targets.</span></span> |
| <span data-ttu-id="921b5-168">**sys.dm_xe_database_sessions**</span><span class="sxs-lookup"><span data-stu-id="921b5-168">**sys.dm_xe_database_sessions**</span></span> |<span data-ttu-id="921b5-169">Renvoie une ligne pour chaque session d’événements incluse dans la base de données actuelle.</span><span class="sxs-lookup"><span data-stu-id="921b5-169">Returns a row for each event session that is scoped to the current database.</span></span> |

<span data-ttu-id="921b5-170">Dans Microsoft SQL Server, les noms des vues catalogue similaires ne contiennent pas la partie *\_database*, par exemple :</span><span class="sxs-lookup"><span data-stu-id="921b5-170">In Microsoft SQL Server, similar catalog views are named without the *\_database* portion of the name, such as:</span></span>

- <span data-ttu-id="921b5-171">**sys.dm_xe_sessions**, au lieu de name</span><span class="sxs-lookup"><span data-stu-id="921b5-171">**sys.dm_xe_sessions**, instead of name</span></span><br/><span data-ttu-id="921b5-172">**sys.dm_xe_database_sessions**.</span><span class="sxs-lookup"><span data-stu-id="921b5-172">**sys.dm_xe_database_sessions**.</span></span>

### <a name="dmvs-common-to-both"></a><span data-ttu-id="921b5-173">Vues de gestion dynamique communes aux deux produits</span><span class="sxs-lookup"><span data-stu-id="921b5-173">DMVs common to both</span></span>
<span data-ttu-id="921b5-174">Pour les événements étendus, il existe des vues de gestion dynamique supplémentaires qui sont communes à la base de données SQL Azure et Microsoft SQL Server :</span><span class="sxs-lookup"><span data-stu-id="921b5-174">For extended events there are additional DMVs that are common to both Azure SQL Database and Microsoft SQL Server:</span></span>

- <span data-ttu-id="921b5-175">**sys.dm_xe_map_values**</span><span class="sxs-lookup"><span data-stu-id="921b5-175">**sys.dm_xe_map_values**</span></span>
- <span data-ttu-id="921b5-176">**sys.dm_xe_object_columns**</span><span class="sxs-lookup"><span data-stu-id="921b5-176">**sys.dm_xe_object_columns**</span></span>
- <span data-ttu-id="921b5-177">**sys.dm_xe_objects**</span><span class="sxs-lookup"><span data-stu-id="921b5-177">**sys.dm_xe_objects**</span></span>
- <span data-ttu-id="921b5-178">**sys.dm_xe_packages**</span><span class="sxs-lookup"><span data-stu-id="921b5-178">**sys.dm_xe_packages**</span></span>

 <a name="sqlfindseventsactionstargets" id="sqlfindseventsactionstargets"></a>

## <a name="find-the-available-extended-events-actions-and-targets"></a><span data-ttu-id="921b5-179">Rechercher les actions, cibles et événements étendus disponibles</span><span class="sxs-lookup"><span data-stu-id="921b5-179">Find the available extended events, actions, and targets</span></span>

<span data-ttu-id="921b5-180">Vous pouvez exécuter une simple instruction SQL **SELECT** pour obtenir une liste des événements, actions et cibles disponibles.</span><span class="sxs-lookup"><span data-stu-id="921b5-180">You can run a simple SQL **SELECT** to obtain a list of the available events, actions, and target.</span></span>

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


<span data-ttu-id="921b5-181"><a name="AzureXEventsTargets" id="AzureXEventsTargets"></a> &nbsp;</span><span class="sxs-lookup"><span data-stu-id="921b5-181"><a name="AzureXEventsTargets" id="AzureXEventsTargets"></a> &nbsp;</span></span>

## <a name="targets-for-your-sql-database-event-sessions"></a><span data-ttu-id="921b5-182">Cibles de vos sessions d’événements de Base de données SQL</span><span class="sxs-lookup"><span data-stu-id="921b5-182">Targets for your SQL Database event sessions</span></span>

<span data-ttu-id="921b5-183">Voici les cibles capables de capturer des résultats à partir de vos sessions d’événements sur la base de données SQL :</span><span class="sxs-lookup"><span data-stu-id="921b5-183">Here are targets that can capture results from your event sessions on SQL Database:</span></span>

- <span data-ttu-id="921b5-184">[Cible de mémoire tampon en anneau](http://msdn.microsoft.com/library/ff878182.aspx) -Maintient brièvement les données d’événements en mémoire.</span><span class="sxs-lookup"><span data-stu-id="921b5-184">[Ring Buffer target](http://msdn.microsoft.com/library/ff878182.aspx) - Briefly holds event data in memory.</span></span>
- <span data-ttu-id="921b5-185">[Cible de compteur d’événements](http://msdn.microsoft.com/library/ff878025.aspx) - Compte tous les événements qui se produisent pendant une session d’événements étendus.</span><span class="sxs-lookup"><span data-stu-id="921b5-185">[Event Counter target](http://msdn.microsoft.com/library/ff878025.aspx) - Counts all events that occur during an extended events session.</span></span>
- <span data-ttu-id="921b5-186">[Cible du fichier d’événements](http://msdn.microsoft.com/library/ff878115.aspx) - Écrit les mémoires tampons complètes dans un conteneur Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="921b5-186">[Event File target](http://msdn.microsoft.com/library/ff878115.aspx) - Writes complete buffers to an Azure Storage container.</span></span>

<span data-ttu-id="921b5-187">L’API [Suivi d’événements pour Windows](http://msdn.microsoft.com/library/ms751538.aspx) n’est pas disponible pour les événements étendus sur la base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="921b5-187">The [Event Tracing for Windows (ETW)](http://msdn.microsoft.com/library/ms751538.aspx) API is not available for extended events on SQL Database.</span></span>

## <a name="restrictions"></a><span data-ttu-id="921b5-188">Restrictions</span><span class="sxs-lookup"><span data-stu-id="921b5-188">Restrictions</span></span>

<span data-ttu-id="921b5-189">Il existe certaines différences liées à la sécurité qui conviennent à l’environnement cloud de Base de données SQL :</span><span class="sxs-lookup"><span data-stu-id="921b5-189">There are a couple of security-related differences befitting the cloud environment of SQL Database:</span></span>

- <span data-ttu-id="921b5-190">Les événements étendus sont fondés sur le modèle d’isolement à locataire unique.</span><span class="sxs-lookup"><span data-stu-id="921b5-190">Extended events are founded on the single-tenant isolation model.</span></span> <span data-ttu-id="921b5-191">Une session d’événements dans une base de données ne peut pas accéder aux données ou événements d’une autre base de données.</span><span class="sxs-lookup"><span data-stu-id="921b5-191">An event session in one database cannot access data or events from another database.</span></span>
- <span data-ttu-id="921b5-192">Vous ne pouvez pas émettre une instruction **CREATE EVENT SESSION** dans le contexte de la base de données **master**.</span><span class="sxs-lookup"><span data-stu-id="921b5-192">You cannot issue a **CREATE EVENT SESSION** statement in the context of the **master** database.</span></span>

## <a name="permission-model"></a><span data-ttu-id="921b5-193">Modèle d’autorisation</span><span class="sxs-lookup"><span data-stu-id="921b5-193">Permission model</span></span>

<span data-ttu-id="921b5-194">Vous devez disposer de l’autorisation **Contrôle** sur la base de données pour émettre une instruction **CREATE EVENT SESSION**.</span><span class="sxs-lookup"><span data-stu-id="921b5-194">You must have **Control** permission on the database to issue a **CREATE EVENT SESSION** statement.</span></span> <span data-ttu-id="921b5-195">Le propriétaire de la base de données (dbo) possède l’autorisation **Contrôle** .</span><span class="sxs-lookup"><span data-stu-id="921b5-195">The database owner (dbo) has **Control** permission.</span></span>

### <a name="storage-container-authorizations"></a><span data-ttu-id="921b5-196">Autorisations de conteneur de stockage</span><span class="sxs-lookup"><span data-stu-id="921b5-196">Storage container authorizations</span></span>

<span data-ttu-id="921b5-197">Le jeton SAP que vous générez pour votre conteneur Azure Storage doit spécifier **rwl** pour les autorisations.</span><span class="sxs-lookup"><span data-stu-id="921b5-197">The SAS token you generate for your Azure Storage container must specify **rwl** for the permissions.</span></span> <span data-ttu-id="921b5-198">La valeur **rwl** fournit les autorisations suivantes :</span><span class="sxs-lookup"><span data-stu-id="921b5-198">The **rwl** value provides the following permissions:</span></span>

- <span data-ttu-id="921b5-199">Lire</span><span class="sxs-lookup"><span data-stu-id="921b5-199">Read</span></span>
- <span data-ttu-id="921b5-200">Écrire</span><span class="sxs-lookup"><span data-stu-id="921b5-200">Write</span></span>
- <span data-ttu-id="921b5-201">Énumérer</span><span class="sxs-lookup"><span data-stu-id="921b5-201">List</span></span>

## <a name="performance-considerations"></a><span data-ttu-id="921b5-202">Considérations relatives aux performances</span><span class="sxs-lookup"><span data-stu-id="921b5-202">Performance considerations</span></span>

<span data-ttu-id="921b5-203">Il existe des scénarios où l’utilisation intensive des événements étendus peut accumuler plus de mémoire active qu’il n’en faut pour l’intégrité de l’ensemble du système.</span><span class="sxs-lookup"><span data-stu-id="921b5-203">There are scenarios where intensive use of extended events can accumulate more active memory than is healthy for the overall system.</span></span> <span data-ttu-id="921b5-204">Par conséquent, le système de la base de données SQL Azure définit et ajuste dynamiquement les limites de quantité de mémoire active pouvant être accumulée par une session d’événements.</span><span class="sxs-lookup"><span data-stu-id="921b5-204">Therefore the Azure SQL Database system dynamically sets and adjusts limits on the amount of active memory that can be accumulated by an event session.</span></span> <span data-ttu-id="921b5-205">De nombreux facteurs entrent dans le calcul dynamique.</span><span class="sxs-lookup"><span data-stu-id="921b5-205">Many factors go into the dynamic calculation.</span></span>

<span data-ttu-id="921b5-206">Si vous recevez un message d’erreur indiquant qu’une quantité maximale de mémoire a été appliquée, vous pouvez envisager certaines actions correctives, notamment :</span><span class="sxs-lookup"><span data-stu-id="921b5-206">If you receive an error message that says a memory maximum was enforced, some corrective actions you can take are:</span></span>

- <span data-ttu-id="921b5-207">Exécuter moins de sessions d’événement simultanées.</span><span class="sxs-lookup"><span data-stu-id="921b5-207">Run fewer concurrent event sessions.</span></span>
- <span data-ttu-id="921b5-208">À l’aide des instructions **CREATE** et **ALTER** pour les sessions d’événements, réduisez la quantité de mémoire spécifiée dans la clause **MAX\_MEMORY**.</span><span class="sxs-lookup"><span data-stu-id="921b5-208">Through your **CREATE** and **ALTER** statements for event sessions, reduce the amount of memory you specify on the **MAX\_MEMORY** clause.</span></span>

### <a name="network-latency"></a><span data-ttu-id="921b5-209">Latence du réseau</span><span class="sxs-lookup"><span data-stu-id="921b5-209">Network latency</span></span>

<span data-ttu-id="921b5-210">La cible **Fichier d’événement** peut rencontrer une latence ou des problèmes de réseau lors de la persistance de données sur des objets blob Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="921b5-210">The **Event File** target might experience network latency or failures while persisting data to Azure Storage blobs.</span></span> <span data-ttu-id="921b5-211">D’autres événements de la base de données SQL peuvent être retardés en attendant la fin de la communication réseau.</span><span class="sxs-lookup"><span data-stu-id="921b5-211">Other events in SQL Database might be delayed while they wait for the network communication to complete.</span></span> <span data-ttu-id="921b5-212">Ce délai peut ralentir votre charge de travail.</span><span class="sxs-lookup"><span data-stu-id="921b5-212">This delay can slow your workload.</span></span>

- <span data-ttu-id="921b5-213">Pour atténuer ce risque de baisse des performances, évitez de définir l’option **EVENT_RETENTION_MODE** sur **NO_EVENT_LOSS** dans vos définitions de session d’événements.</span><span class="sxs-lookup"><span data-stu-id="921b5-213">To mitigate this performance risk, avoid setting the **EVENT_RETENTION_MODE** option to **NO_EVENT_LOSS** in your event session definitions.</span></span>

## <a name="related-links"></a><span data-ttu-id="921b5-214">Liens connexes</span><span class="sxs-lookup"><span data-stu-id="921b5-214">Related links</span></span>

- <span data-ttu-id="921b5-215">[Utilisation d’Azure PowerShell avec Azure Storage](../storage/common/storage-powershell-guide-full.md)</span><span class="sxs-lookup"><span data-stu-id="921b5-215">[Using Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md).</span></span>
- [<span data-ttu-id="921b5-216">Applets de commande Azure Storage</span><span class="sxs-lookup"><span data-stu-id="921b5-216">Azure Storage Cmdlets</span></span>](http://msdn.microsoft.com/library/dn806401.aspx)
- <span data-ttu-id="921b5-217">[Utilisation d’Azure PowerShell avec Azure Storage](../storage/common/storage-powershell-guide-full.md) - Cette rubrique fournit des informations complètes sur PowerShell et le service Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="921b5-217">[Using Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md) - Provides comprehensive information about PowerShell and the Azure Storage service.</span></span>
- [<span data-ttu-id="921b5-218">Utilisation du stockage d’objets blob à partir de .NET</span><span class="sxs-lookup"><span data-stu-id="921b5-218">How to use Blob storage from .NET</span></span>](../storage/blobs/storage-dotnet-how-to-use-blobs.md)
- [<span data-ttu-id="921b5-219">CREATE CREDENTIAL (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="921b5-219">CREATE CREDENTIAL (Transact-SQL)</span></span>](http://msdn.microsoft.com/library/ms189522.aspx)
- [<span data-ttu-id="921b5-220">CREATE EVENT SESSION (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="921b5-220">CREATE EVENT SESSION (Transact-SQL)</span></span>](http://msdn.microsoft.com/library/bb677289.aspx)
- [<span data-ttu-id="921b5-221">Billets de blog de Jonathan Kehayias sur les événements étendus dans Microsoft SQL Server</span><span class="sxs-lookup"><span data-stu-id="921b5-221">Jonathan Kehayias' blog posts about extended events in Microsoft SQL Server</span></span>](http://www.sqlskills.com/blogs/jonathan/category/extended-events/)


- <span data-ttu-id="921b5-222">La page web *Mises à jour de service* Azure, restreinte par paramètre à Azure SQL Database :</span><span class="sxs-lookup"><span data-stu-id="921b5-222">The Azure *Service Updates* webpage, narrowed by parameter to Azure SQL Database:</span></span>
    - [<span data-ttu-id="921b5-223">https://azure.microsoft.com/updates/?service=sql-database</span><span class="sxs-lookup"><span data-stu-id="921b5-223">https://azure.microsoft.com/updates/?service=sql-database</span></span>](https://azure.microsoft.com/updates/?service=sql-database)


<span data-ttu-id="921b5-224">Vous trouverez d’autres rubriques d’exemples de code pour les événements étendus en suivant le lien ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="921b5-224">Other code sample topics for extended events are available at the following links.</span></span> <span data-ttu-id="921b5-225">Toutefois, vous devez vérifier régulièrement les exemples pour voir s’ils ciblent Microsoft SQL Server ou la base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="921b5-225">However, you must routinely check any sample to see whether the sample targets Microsoft SQL Server versus Azure SQL Database.</span></span> <span data-ttu-id="921b5-226">Vous pouvez ensuite déterminer si vous devez apporter quelques modifications mineures avant d’exécuter un exemple.</span><span class="sxs-lookup"><span data-stu-id="921b5-226">Then you can decide whether minor changes are needed to run the sample.</span></span>

<!--
('lock_acquired' event.)

- Code sample for SQL Server: [Determine Which Queries Are Holding Locks](http://msdn.microsoft.com/library/bb677357.aspx)
- Code sample for SQL Server: [Find the Objects That Have the Most Locks Taken on Them](http://msdn.microsoft.com/library/bb630355.aspx)
-->
