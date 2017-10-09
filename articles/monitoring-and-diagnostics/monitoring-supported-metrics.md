---
title: "métrique d’analyse - des métriques prises en charge par le type de ressource d’aaaAzure | Documents Microsoft"
description: Liste des mesures disponibles pour chaque type de ressource avec Azure Monitor.
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 63d4ac65-1688-40d1-85c8-7cd408285b0f
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/05/2017
ms.author: johnkem
ms.openlocfilehash: 66834238a1a4fcd7db1464cc023c18ee2563517a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="supported-metrics-with-azure-monitor"></a>Mesures prises en charge avec Azure Monitor
Moniteur Azure fournit plusieurs façons toointeract avec métriques, notamment les graphiques dans le portail de hello, y accéder via l’API REST de hello ou les requêtes à l’aide de PowerShell ou CLI. Voici une liste complète de toutes les mesures actuellement offertes par le pipeline de mesure d’Azure Monitor.

> [!NOTE]
> D’autres mesures peuvent être disponibles dans le portail de hello ou les API héritées. Cette liste inclut uniquement les métriques de la version préliminaire publique disponible à l’aide de la version préliminaire publique de hello du pipeline métrique du moniteur de Windows Azure hello consolidé.
>
>

## <a name="microsoftanalysisservicesservers"></a>Microsoft.AnalysisServices/servers

|Mesure|Nom d’affichage de la mesure|Unité|Type d’agrégation|Description|
|---|---|---|---|---|
|qpu_metric|QPU|Nombre|Moyenne|QPU. Plage de 0 à 100 pour S1, de 0 à 200 pour S2 et de 0 à 400 pour S4|
|memory_metric|Mémoire|Octets|Moyenne|Mémoire. Plage de 0 à 25 Go pour S1, de 0 à 50 Go pour S2 et de 0 à 100 Go pour S4|
|TotalConnectionRequests|Nombre total de demandes de connexion|Nombre|Moyenne|Nombre total de demandes de connexion. Il s’agit des arrivées.|
|SuccessfullConnectionsPerSec|Connexions réussies par seconde|CountPerSecond|Moyenne|Taux de connexions terminées réussies.|
|TotalConnectionFailures|Nombre total d’échecs de connexion|Nombre|Moyenne|Total des échecs de tentatives de connexion.|
|CurrentUserSessions|Sessions utilisateur actuelles|Nombre|Moyenne|Nombre actuel de sessions utilisateur établies.|
|QueryPoolBusyThreads|Threads occupés du pool de threads de requêtes|Nombre|Moyenne|Nombre de threads occupés dans le pool de threads de requête hello.|
|CommandPoolJobQueueLength|Longueur de la file d’attente des travaux du pool de commandes|Nombre|Moyenne|Nombre de travaux dans la file d’attente hello du pool de threads de commande hello.|
|ProcessingPoolJobQueueLength|Longueur de la file d’attente des travaux du pool de traitement|Nombre|Moyenne|Nombre de travaux de non-E/s dans la file d’attente hello Hello pool de threads de traitement.|
|CurrentConnections|Connexion : connexions actuelles|Nombre|Moyenne|Nombre actuel de connexions client établies.|
|CleanerCurrentPrice|Mémoire : prix actuel du nettoyage|Nombre|Moyenne|Prix actuel de la mémoire, $/ octet/temps, normalisé too1000.|
|CleanerMemoryShrinkable|Mémoire : mémoire de nettoyage réductible|Octets|Moyenne|Quantité de mémoire, en octets, toopurging objet par le nettoyeur d’arrière-plan hello.|
|CleanerMemoryNonshrinkable|Mémoire : mémoire de nettoyage non réductible|Octets|Moyenne|Quantité de mémoire, en octets, pas sujet toopurging par le nettoyeur d’arrière-plan hello.|
|MemoryUsage|Mémoire : utilisation de la mémoire|Octets|Moyenne|Utilisation de la mémoire de processus serveur hello dans le calcul du coût de la mémoire nettoyage. Égale toocounter process\\privatebytes et taille de hello de données mappé en mémoire, en ignorant toute mémoire mappée ou allouée par le moteur de mémoire analytique hello xVelocity (VertiPaq) dépassant le moteur xVelocity de hello limite de mémoire.|
|MemoryLimitHard|Mémoire : limite de mémoire physique|Octets|Moyenne|Limite de mémoire physique, du fichier de configuration.|
|MemoryLimitHigh|Mémoire : limite de mémoire élevée|Octets|Moyenne|Limite de mémoire élevée, du fichier de configuration.|
|MemoryLimitLow|Mémoire : limite de mémoire basse|Octets|Moyenne|Limite de mémoire basse, du fichier de configuration.|
|MemoryLimitVertiPaq|Mémoire : limite de mémoire VertiPaq|Octets|Moyenne|Limite en mémoire, du fichier de configuration.|
|Quota|Mémoire : quota|Octets|Moyenne|Quota de mémoire actuel, en octets. Le quota de mémoire est également appelé réserve de mémoire ou d’allocation.|
|QuotaBlocked|Mémoire : quota bloqué|Nombre|Moyenne|Nombre actuel de requêtes de quota qui sont bloquées en attendant la libération d’autres quotas de mémoire.|
|VertiPaqNonpaged|Mémoire : réserve non paginée VertiPaq|Octets|Moyenne|Octets de mémoire verrouillée dans le jeu de travail hello pour une utilisation par le moteur de hello en mémoire.|
|VertiPaqPaged|Mémoire : réserve paginée VertiPaq|Octets|Moyenne|Octets de mémoire paginée utilisée pour les données en mémoire.|
|RowsReadPerSec|Traitement : lignes lues par seconde|CountPerSecond|Moyenne|Taux de lignes lues à partir de toutes les bases de données relationnelles.|
|RowsConvertedPerSec|Traitement : lignes converties par seconde|CountPerSecond|Moyenne|Taux de lignes converties lors du traitement.|
|RowsWrittenPerSec|Traitement : lignes écrites par seconde|CountPerSecond|Moyenne|Taux de lignes écrites lors du traitement.|
|CommandPoolBusyThreads|Threads : threads occupés du pool commandes|Nombre|Moyenne|Nombre de threads occupés dans le pool de threads de commande hello.|
|CommandPoolIdleThreads|Threads : threads inactifs du pool commande|Nombre|Moyenne|Nombre de threads inactifs dans le pool de threads de commande hello.|
|LongParsingBusyThreads|Threads : threads d’analyse longue occupés|Nombre|Moyenne|Nombre de threads occupés dans hello pool de threads d’analyse longue.|
|LongParsingIdleThreads|Threads : threads d’analyse longue inactifs|Nombre|Moyenne|Nombre de threads inactifs dans hello pool de threads d’analyse longue.|
|LongParsingJobQueueLength|Threads : durée de file d’attente des travaux d’analyse longue|Nombre|Moyenne|Nombre de travaux dans la file d’attente hello Hello pool de threads d’analyse longue.|
|ProcessingPoolBusyIOJobThreads|Threads : traitement des threads de travail d’E/S occupés du pool|Nombre|Moyenne|Nombre de threads exécutant des travaux d’e/s dans le pool de threads de traitement de hello.|
|ProcessingPoolBusyNonIOThreads|Threads : traitement des threads de travail autres qu’E/S occupés du pool|Nombre|Moyenne|Nombre de threads exécutant des travaux de non-E/s dans le pool de threads de traitement de hello.|
|ProcessingPoolIOJobQueueLength|Threads : longueur de la file d’attente des travaux d’E/S du pool de traitement|Nombre|Moyenne|Nombre de travaux d’e/s dans la file d’attente hello Hello pool de threads de traitement.|
|ProcessingPoolIdleIOJobThreads|Threads : traitement des threads de travail d’E/S ignorés du pool|Nombre|Moyenne|Nombre de threads inactifs pour les travaux d’e/s dans le pool de threads de traitement de hello.|
|ProcessingPoolIdleNonIOThreads|Threads : traitement des threads de travail autres qu’E/S inactifs du pool|Nombre|Moyenne|Nombre de threads inactifs dans le pool de threads de traitement de hello dédié des travaux d’e/S toonon.|
|QueryPoolIdleThreads|Threads : threads inactifs du pool de requêtes|Nombre|Moyenne|Nombre de threads inactifs pour les travaux d’e/s dans le pool de threads de traitement de hello.|
|QueryPoolJobQueueLength|Threads : longueur de file d’attente de travaux du pool de requêtes|Nombre|Moyenne|Nombre de travaux dans la file d’attente hello du pool de threads de requête hello.|
|ShortParsingBusyThreads|Threads : threads d’analyse courte occupés|Nombre|Moyenne|Nombre de threads occupés dans hello court de pool de threads d’analyse.|
|ShortParsingIdleThreads|Threads : threads d’analyse courte inactifs|Nombre|Moyenne|Nombre de threads inactifs dans hello court de pool de threads d’analyse.|
|ShortParsingJobQueueLength|Threads : durée de file d’attente des travaux d’analyse courte|Nombre|Moyenne|Nombre de travaux dans la file d’attente hello Hello court de pool de threads d’analyse.|
|memory_thrashing_metric|Vidage de mémoire|Pourcentage|Moyenne|Vidage de mémoire moyenne.|

## <a name="microsoftapimanagementservice"></a>Microsoft.ApiManagement/service

|Mesure|Nom d’affichage de la mesure|Unité|Type d’agrégation|Description|
|---|---|---|---|---|
|TotalRequests|Nombre total de demandes de la passerelle|Nombre|Total|Nombre de demandes de la passerelle|
|SuccessfulRequests|Demandes de la passerelle ayant abouti|Nombre|Total|Nombre de demandes de la passerelle ayant abouti|
|UnauthorizedRequests|Demandes de la passerelle non autorisées|Nombre|Total|Nombre de demandes de la passerelle non autorisées|
|FailedRequests|Demandes de la passerelle ayant échoué|Nombre|Total|Nombre de défaillances des demandes de la passerelle|
|OtherRequests|Autres demandes de la passerelle|Nombre|Total|Nombre d’autres demandes de la passerelle|

## <a name="microsoftbatchbatchaccounts"></a>Microsoft.Batch/batchAccounts

|Mesure|Nom d’affichage de la mesure|Unité|Type d’agrégation|Description|
|---|---|---|---|---|
|CoreCount|Nombre de cœurs dédiés|Nombre|Total|Nombre total de cœurs dédiés dans le compte de traitement par lots hello|
|TotalNodeCount|Nombre de nœuds dédiés|Nombre|Total|Nombre total de nœuds dédiés dans le compte de traitement par lots hello|
|LowPriorityCoreCount|Nombre de cœurs à priorité basse|Nombre|Total|Nombre total de cœurs de faible priorité dans le compte de traitement par lots hello|
|TotalLowPriorityNodeCount|Nombre de nœuds à priorité basse|Nombre|Total|Nombre total de nœuds de faible priorité dans le compte de traitement par lots hello|
|CreatingNodeCount|Nombre de nœuds créés|Nombre|Total|Nombre de nœuds en cours de création|
|StartingNodeCount|Nombre de nœuds de départ|Nombre|Total|Nœuds de nœuds de départ|
|WaitingForStartTaskNodeCount|Nombre de nœuds en attente de démarrage de tâche|Nombre|Total|Nombre de nœuds en attente de toocomplete de démarrer la tâche hello|
|StartTaskFailedNodeCount|Nombre de nœuds pour lesquels le démarrage d’une tâche a échoué|Nombre|Total|Nombre de nœuds où hello démarrer la tâche a échoué|
|IdleNodeCount|Nombre de nœuds inactifs|Nombre|Total|Le nombre de nœuds inactifs|
|OfflineNodeCount|Nombre de nœuds hors ligne|Nombre|Total|Le nombre de nœuds hors ligne|
|RebootingNodeCount|Nombre de nœuds en cours de redémarrage|Nombre|Total|Le nombre de nœuds en cours de redémarrage|
|ReimagingNodeCount|Nombre de nœuds en cours de réimageage|Nombre|Total|Le nombre de nœuds en cours de réimageage|
|RunningNodeCount|Nombre de nœuds en cours d’exécution|Nombre|Total|Le nombre de nœuds en cours d’exécution|
|LeavingPoolNodeCount|Nombre de nœuds quittant le pool|Nombre|Total|Nombre de nœuds en laissant hello Pool|
|UnusableNodeCount|Nombre de nœuds inutilisables|Nombre|Total|Le nombre de nœuds inutilisables|
|PreemptedNodeCount|Nombre de nœuds reportés|Nombre|Total|Nombre de nœuds reportés|
|TaskStartEvent|Événements de lancement de tâche|Nombre|Total|Nombre total de tâches ayant démarré|
|TaskCompleteEvent|Événements de fin de tâche|Nombre|Total|Le nombre total de tâches terminées|
|TaskFailEvent|Événements d’échec de tâches|Nombre|Total|Le nombre total de tâches terminées dans un état d’échec|
|PoolCreateEvent|Événements de création de pool|Nombre|Total|Nombre total de pools créés|
|PoolResizeStartEvent|Événements de démarrage de redimensionnement de pool|Nombre|Total|Nombre total de redimensionnements de pool ayant démarré|
|PoolResizeCompleteEvent|Événements de fin de redimensionnement de pool|Nombre|Total|Nombre total de redimensionnements de pool terminés|
|PoolDeleteStartEvent|Événements de démarrage de suppression de pool|Nombre|Total|Nombre total de suppressions de pool ayant démarré|
|PoolDeleteCompleteEvent|Événements de suppression de pool terminés|Nombre|Total|Nombre total de suppressions de pool terminées|

## <a name="microsoftcacheredis"></a>Microsoft.Cache/redis

|Mesure|Nom d’affichage de la mesure|Unité|Type d’agrégation|Description|
|---|---|---|---|---|
|connectedclients|Clients connectés|Nombre|Maximale||
|totalcommandsprocessed|Total des opérations|Nombre|Total||
|cachehits|Présences dans le cache|Nombre|Total||
|cachemisses|Absences dans le cache|Nombre|Total||
|getcommands|Gets|Nombre|Total||
|setcommands|Sets|Nombre|Total||
|evictedkeys|Clés exclues|Nombre|Total||
|totalkeys|Nombre total de clés|Nombre|Maximale||
|expiredkeys|Clés expirées|Nombre|Total||
|usedmemory|Mémoire utilisée|Octets|Maximale||
|usedmemoryRss|Taille de la mémoire résidente utilisée|Octets|Maximale||
|serverLoad|Charge du serveur|Pourcentage|Maximale||
|cacheWrite|Cache d’écriture|BytesPerSecond|Maximale||
|cacheRead|Lecture du cache|BytesPerSecond|Maximale||
|percentProcessorTime|UC|Pourcentage|Maximale||
|connectedclients0|Clients connectés (Shard 0)|Nombre|Maximale||
|totalcommandsprocessed0|Total des opérations (Shard 0)|Nombre|Total||
|cachehits0|Présences dans le cache (Shard 0)|Nombre|Total||
|cachemisses0|Absences dans le cache (Shard 0)|Nombre|Total||
|getcommands0|Gets (Shard 0)|Nombre|Total||
|setcommands0|Sets (Shard 0)|Nombre|Total||
|evictedkeys0|Clés exclues (Shard 0)|Nombre|Total||
|totalkeys0|Nombre total de clés (Shard 0)|Nombre|Maximale||
|expiredkeys0|Clés expirées (Shard 0)|Nombre|Total||
|usedmemory0|Mémoire utilisée (Shard 0)|Octets|Maximale||
|usedmemoryRss0|Mémoire résidente utilisée (Shard 0)|Octets|Maximale||
|serverLoad0|Charge du serveur (Shard 0)|Pourcentage|Maximale||
|cacheWrite0|Cache d’écriture (Shard 0)|BytesPerSecond|Maximale||
|cacheRead0|Cache de lecture (Shard 0)|BytesPerSecond|Maximale||
|percentProcessorTime0|UC (Shard 0)|Pourcentage|Maximale||
|connectedclients1|Clients connectés (Shard 1)|Nombre|Maximale||
|totalcommandsprocessed1|Total des opérations (Shard 1)|Nombre|Total||
|cachehits1|Présences dans le cache (Shard 1)|Nombre|Total||
|cachemisses1|Absences dans le cache (Shard 1)|Nombre|Total||
|getcommands1|Gets (Shard 1)|Nombre|Total||
|setcommands1|Sets (Shard 1)|Nombre|Total||
|evictedkeys1|Clés exclues (Shard 1)|Nombre|Total||
|totalkeys1|Nombre total de clés (Shard 1)|Nombre|Maximale||
|expiredkeys1|Clés expirées (Shard 1)|Nombre|Total||
|usedmemory1|Mémoire utilisée (Shard 1)|Octets|Maximale||
|usedmemoryRss1|Mémoire résidente utilisée (Shard 1)|Octets|Maximale||
|serverLoad1|Charge du serveur (Shard 1)|Pourcentage|Maximale||
|cacheWrite1|Cache d’écriture (Shard 1)|BytesPerSecond|Maximale||
|cacheRead1|Lecture du cache (Shard 1)|BytesPerSecond|Maximale||
|percentProcessorTime1|UC (Shard 1)|Pourcentage|Maximale||
|connectedclients2|Clients connectés (Shard 2)|Nombre|Maximale||
|totalcommandsprocessed2|Total des opérations (Shard 2)|Nombre|Total||
|cachehits2|Présences dans le cache (Shard 2)|Nombre|Total||
|cachemisses2|Absences dans le cache (Shard 2)|Nombre|Total||
|getcommands2|Gets (Shard 2)|Nombre|Total||
|setcommands2|Sets (Shard 2)|Nombre|Total||
|evictedkeys2|Clés exclues (Shard 2)|Nombre|Total||
|totalkeys2|Nombre total de clés (Shard 2)|Nombre|Maximale||
|expiredkeys2|Clés expirées (Shard 2)|Nombre|Total||
|usedmemory2|Mémoire utilisée (Shard 2)|Octets|Maximale||
|usedmemoryRss2|Mémoire résidente utilisée (Shard 2)|Octets|Maximale||
|serverLoad2|Charge du serveur (Shard 2)|Pourcentage|Maximale||
|cacheWrite2|Cache d’écriture (Shard 2)|BytesPerSecond|Maximale||
|cacheRead2|Lecture du cache (Shard 2)|BytesPerSecond|Maximale||
|percentProcessorTime2|UC (Shard 2)|Pourcentage|Maximale||
|connectedclients3|Clients connectés (Shard 3)|Nombre|Maximale||
|totalcommandsprocessed3|Total des opérations (Shard 3)|Nombre|Total||
|cachehits3|Présences dans le cache (Shard 3)|Nombre|Total||
|cachemisses3|Absences dans le cache (Shard 3)|Nombre|Total||
|getcommands3|Gets (Shard 3)|Nombre|Total||
|setcommands3|Sets (Shard 3)|Nombre|Total||
|evictedkeys3|Clés exclues (Shard 3)|Nombre|Total||
|totalkeys3|Nombre total de clés (Shard 3)|Nombre|Maximale||
|expiredkeys3|Clés expirées (Shard 3)|Nombre|Total||
|usedmemory3|Mémoire utilisée (Shard 3)|Octets|Maximale||
|usedmemoryRss3|Mémoire résidente utilisée (Shard 3)|Octets|Maximale||
|serverLoad3|Charge du serveur (Shard 3)|Pourcentage|Maximale||
|cacheWrite3|Cache d’écriture (Shard 3)|BytesPerSecond|Maximale||
|cacheRead3|Lecture du cache (Shard 3)|BytesPerSecond|Maximale||
|percentProcessorTime3|UC (Shard 3)|Pourcentage|Maximale||
|connectedclients4|Clients connectés (Shard 4)|Nombre|Maximale||
|totalcommandsprocessed4|Total des opérations (Shard 4)|Nombre|Total||
|cachehits4|Présences dans le cache (Shard 4)|Nombre|Total||
|cachemisses4|Absences dans le cache (Shard 4)|Nombre|Total||
|getcommands4|Gets (Shard 4)|Nombre|Total||
|setcommands4|Sets (Shard 4)|Nombre|Total||
|evictedkeys4|Clés exclues (Shard 4)|Nombre|Total||
|totalkeys4|Nombre total de clés (Shard 4)|Nombre|Maximale||
|expiredkeys4|Clés expirées (Shard 4)|Nombre|Total||
|usedmemory4|Mémoire utilisée (Shard 4)|Octets|Maximale||
|usedmemoryRss4|Mémoire résidente utilisée (Shard 4)|Octets|Maximale||
|serverLoad4|Charge du serveur (Shard 4)|Pourcentage|Maximale||
|cacheWrite4|Cache d’écriture (Shard 4)|BytesPerSecond|Maximale||
|cacheRead4|Lecture du cache (Shard 4)|BytesPerSecond|Maximale||
|percentProcessorTime4|UC (Shard 4)|Pourcentage|Maximale||
|connectedclients5|Clients connectés (Shard 5)|Nombre|Maximale||
|totalcommandsprocessed5|Total des opérations (Shard 5)|Nombre|Total||
|cachehits5|Présences dans le cache (Shard 5)|Nombre|Total||
|cachemisses5|Absences dans le cache (Shard 5)|Nombre|Total||
|getcommands5|Gets (Shard 5)|Nombre|Total||
|setcommands5|Sets (Shard 5)|Nombre|Total||
|evictedkeys5|Clés exclues (Shard 5)|Nombre|Total||
|totalkeys5|Nombre total de clés (Shard 5)|Nombre|Maximale||
|expiredkeys5|Clés expirées (Shard 5)|Nombre|Total||
|usedmemory5|Mémoire utilisée (Shard 5)|Octets|Maximale||
|usedmemoryRss5|Mémoire résidente utilisée (Shard 5)|Octets|Maximale||
|serverLoad5|Charge du serveur (Shard 5)|Pourcentage|Maximale||
|cacheWrite5|Cache d’écriture (Shard 5)|BytesPerSecond|Maximale||
|cacheRead5|Lecture du cache (Shard 5)|BytesPerSecond|Maximale||
|percentProcessorTime5|UC (Shard 5)|Pourcentage|Maximale||
|connectedclients6|Clients connectés (Shard 6)|Nombre|Maximale||
|totalcommandsprocessed6|Total des opérations (Shard 6)|Nombre|Total||
|cachehits6|Présences dans le cache (Shard 6)|Nombre|Total||
|cachemisses6|Absences dans le cache (Shard 6)|Nombre|Total||
|getcommands6|Gets (Shard 6)|Nombre|Total||
|setcommands6|Sets (Shard 6)|Nombre|Total||
|evictedkeys6|Clés exclues (Shard 6)|Nombre|Total||
|totalkeys6|Nombre total de clés (Shard 6)|Nombre|Maximale||
|expiredkeys6|Clés expirées (Shard 6)|Nombre|Total||
|usedmemory6|Mémoire utilisée (Shard 6)|Octets|Maximale||
|usedmemoryRss6|Mémoire résidente utilisée (Shard 6)|Octets|Maximale||
|serverLoad6|Charge du serveur (Shard 6)|Pourcentage|Maximale||
|cacheWrite6|Cache d’écriture (Shard 6)|BytesPerSecond|Maximale||
|cacheRead6|Lecture du cache (Shard 6)|BytesPerSecond|Maximale||
|percentProcessorTime6|UC (Shard 6)|Pourcentage|Maximale||
|connectedclients7|Clients connectés (Shard 7)|Nombre|Maximale||
|totalcommandsprocessed7|Total des opérations (Shard 7)|Nombre|Total||
|cachehits7|Présences dans le cache (Shard 7)|Nombre|Total||
|cachemisses7|Absences dans le cache (Shard 7)|Nombre|Total||
|getcommands7|Gets (Shard 7)|Nombre|Total||
|setcommands7|Sets (Shard 7)|Nombre|Total||
|evictedkeys7|Clés exclues (Shard 7)|Nombre|Total||
|totalkeys7|Nombre total de clés (Shard 7)|Nombre|Maximale||
|expiredkeys7|Clés expirées (Shard 7)|Nombre|Total||
|usedmemory7|Mémoire utilisée (Shard 7)|Octets|Maximale||
|usedmemoryRss7|Mémoire résidente utilisée (Shard 7)|Octets|Maximale||
|serverLoad7|Charge du serveur (Shard 7)|Pourcentage|Maximale||
|cacheWrite7|Cache d’écriture (Shard 7)|BytesPerSecond|Maximale||
|cacheRead7|Lecture du cache (Shard 7)|BytesPerSecond|Maximale||
|percentProcessorTime7|UC (Shard 7)|Pourcentage|Maximale||
|connectedclients8|Clients connectés (Shard 8)|Nombre|Maximale||
|totalcommandsprocessed8|Total des opérations (Shard 8)|Nombre|Total||
|cachehits8|Présences dans le cache (Shard 8)|Nombre|Total||
|cachemisses8|Absences dans le cache (Shard 8)|Nombre|Total||
|getcommands8|Gets (Shard 8)|Nombre|Total||
|setcommands8|Sets (Shard 8)|Nombre|Total||
|evictedkeys8|Clés exclues (Shard 8)|Nombre|Total||
|totalkeys8|Nombre total de clés (Shard 8)|Nombre|Maximale||
|expiredkeys8|Clés expirées (Shard 8)|Nombre|Total||
|usedmemory8|Mémoire utilisée (Shard 8)|Octets|Maximale||
|usedmemoryRss8|Mémoire résidente utilisée (Shard 8)|Octets|Maximale||
|serverLoad8|Charge du serveur (Shard 8)|Pourcentage|Maximale||
|cacheWrite8|Cache d’écriture (Shard 8)|BytesPerSecond|Maximale||
|cacheRead8|Lecture du cache (Shard 8)|BytesPerSecond|Maximale||
|percentProcessorTime8|UC (Shard 8)|Pourcentage|Maximale||
|connectedclients9|Clients connectés (Shard 9)|Nombre|Maximale||
|totalcommandsprocessed9|Total des opérations (Shard 9)|Nombre|Total||
|cachehits9|Présences dans le cache (Shard 9)|Nombre|Total||
|cachemisses9|Absences dans le cache (Shard 9)|Nombre|Total||
|getcommands9|Gets (Shard 9)|Nombre|Total||
|setcommands9|Sets (Shard 9)|Nombre|Total||
|evictedkeys9|Clés exclues (Shard 9)|Nombre|Total||
|totalkeys9|Nombre total de clés (Shard 9)|Nombre|Maximale||
|expiredkeys9|Clés expirées (Shard 9)|Nombre|Total||
|usedmemory9|Mémoire utilisée (Shard 9)|Octets|Maximale||
|usedmemoryRss9|Mémoire résidente utilisée (Shard 9)|Octets|Maximale||
|serverLoad9|Charge du serveur (Shard 9)|Pourcentage|Maximale||
|cacheWrite9|Cache d’écriture (Shard 9)|BytesPerSecond|Maximale||
|cacheRead9|Cache de lecture (Shard 9)|BytesPerSecond|Maximale||
|percentProcessorTime9|UC (Shard 9)|Pourcentage|Maximale||

## <a name="microsoftcognitiveservicesaccounts"></a>Microsoft.CognitiveServices/accounts

|Mesure|Nom d’affichage de la mesure|Unité|Type d’agrégation|Description|
|---|---|---|---|---|
|TotalCalls|Nombre total d’appels|Nombre|Total|Nombre total d’appels.|
|SuccessfulCalls|Appels réussis|Nombre|Total|Nombre d’appels réussis.|
|TotalErrors|Nombre total d’erreurs|Nombre|Total|Nombre total d’appels avec réponse d’erreur (code de réponse HTTP : 4xx ou 5xx).|
|BlockedCalls|Appels bloqués|Nombre|Total|Nombre d’appels ayant dépassé la limite de débit ou de quota.|
|ServerErrors|Erreurs de serveur|Nombre|Total|Nombre d’appels avec erreur interne du service (code de réponse HTTP : 5xx).|
|ClientErrors|Erreurs de client|Nombre|Total|Nombre d’appels avec erreur côté client (code de réponse HTTP : 4xx).|
|DataIn|Données entrantes|Octets|Total|Taille des données entrantes en octets.|
|DataOut|Données sortantes|Octets|Total|Taille des données sortantes en octets.|
|Latency|Latency|Millisecondes|Moyenne|Latence en millisecondes.|

## <a name="microsoftcomputevirtualmachines"></a>Microsoft.Compute/virtualMachines

|Mesure|Nom d’affichage de la mesure|Unité|Type d’agrégation|Description|
|---|---|---|---|---|
|Percentage CPU|Percentage CPU|Pourcentage|Moyenne|pourcentage de Hello d’unités de calcul alloués qui sont actuellement en cours d’utilisation par hello ou les machines virtuelles|
|Network In|Network In|Octets|Total|nombre de Hello d’octets reçus sur toutes les interfaces réseau par hello (trafic entrant) ou les machines virtuelles|
|Network Out|Network Out|Octets|Total|nombre de Hello d’octets sur toutes les interfaces réseau par hello ou les machines virtuelles (trafic sortant)|
|Disk Read Bytes|Disk Read Bytes|Octets|Total|Total d’octets lus à partir du disque pendant la période d’analyse|
|Disk Write Bytes|Disk Write Bytes|Octets|Total|Nombre total d’octets écrit toodisk pendant la période d’analyse|
|Disk Read Operations/Sec|Disk Read Operations/Sec|CountPerSecond|Moyenne|E/S de lecture disque par seconde|
|Disk Write Operations/Sec|Disk Write Operations/Sec|CountPerSecond|Moyenne|E/S d’écriture disque par seconde|

## <a name="microsoftcomputevirtualmachinescalesets"></a>Microsoft.Compute/virtualMachineScaleSets

|Mesure|Nom d’affichage de la mesure|Unité|Type d’agrégation|Description|
|---|---|---|---|---|
|Percentage CPU|Percentage CPU|Pourcentage|Moyenne|pourcentage de Hello d’unités de calcul alloués qui sont actuellement en cours d’utilisation par hello ou les machines virtuelles|
|Network In|Network In|Octets|Total|nombre de Hello d’octets reçus sur toutes les interfaces réseau par hello (trafic entrant) ou les machines virtuelles|
|Network Out|Network Out|Octets|Total|nombre de Hello d’octets sur toutes les interfaces réseau par hello ou les machines virtuelles (trafic sortant)|
|Disk Read Bytes|Disk Read Bytes|Octets|Total|Total d’octets lus à partir du disque pendant la période d’analyse|
|Disk Write Bytes|Disk Write Bytes|Octets|Total|Nombre total d’octets écrit toodisk pendant la période d’analyse|
|Disk Read Operations/Sec|Disk Read Operations/Sec|CountPerSecond|Moyenne|E/S de lecture disque par seconde|
|Disk Write Operations/Sec|Disk Write Operations/Sec|CountPerSecond|Moyenne|E/S d’écriture disque par seconde|

## <a name="microsoftcomputevirtualmachinescalesetsvirtualmachines"></a>Microsoft.Compute/virtualMachineScaleSets/virtualMachines

|Mesure|Nom d’affichage de la mesure|Unité|Type d’agrégation|Description|
|---|---|---|---|---|
|Percentage CPU|Percentage CPU|Pourcentage|Moyenne|pourcentage de Hello d’unités de calcul alloués qui sont actuellement en cours d’utilisation par hello ou les machines virtuelles|
|Network In|Network In|Octets|Total|nombre de Hello d’octets reçus sur toutes les interfaces réseau par hello (trafic entrant) ou les machines virtuelles|
|Network Out|Network Out|Octets|Total|nombre de Hello d’octets sur toutes les interfaces réseau par hello ou les machines virtuelles (trafic sortant)|
|Disk Read Bytes|Disk Read Bytes|Octets|Total|Total d’octets lus à partir du disque pendant la période d’analyse|
|Disk Write Bytes|Disk Write Bytes|Octets|Total|Nombre total d’octets écrit toodisk pendant la période d’analyse|
|Disk Read Operations/Sec|Disk Read Operations/Sec|CountPerSecond|Moyenne|E/S de lecture disque par seconde|
|Disk Write Operations/Sec|Disk Write Operations/Sec|CountPerSecond|Moyenne|E/S d’écriture disque par seconde|

## <a name="microsoftcustomerinsightshubs"></a>Microsoft.CustomerInsights/hubs

|Mesure|Nom d’affichage de la mesure|Unité|Type d’agrégation|Description|
|---|---|---|---|---|
|DCIApiCalls|Appels de l’API Insights client|Nombre|Total||
|DCIMappingImportOperationSuccessfulLines|Mappage des lignes de réussite d’opération d’importation|Nombre|Total||
|DCIMappingImportOperationFailedLines|Mappage des lignes en échec d’opération d’importation|Nombre|Total||
|DCIMappingImportOperationTotalLines|Mappage du total des lignes d’opération d’importation|Nombre|Total||
|DCIMappingImportOperationRuntimeInSeconds|Mappage d’exécution d’opération d’importation en secondes|Secondes|Total||
|DCIOutboundProfileExportSucceeded|Exportation réussie de profil de sortie|Nombre|Total||
|DCIOutboundProfileExportFailed|Échec de l’exportation de profil de sortie|Nombre|Total||
|DCIOutboundProfileExportDuration|Durée d’exportation de profil de sortie|Secondes|Total||
|DCIOutboundKpiExportSucceeded|Exportation réussie de l’indicateur KPI sortant|Nombre|Total||
|DCIOutboundKpiExportFailed|Échec de l’exportation de l’indicateur KPI sortant|Nombre|Total||
|DCIOutboundKpiExportDuration|Durée de l’exportation de l’indicateur KPI sortant|Secondes|Total||
|DCIOutboundKpiExportStarted|Exportation démarrée de l’indicateur KPI sortant|Secondes|Total||
|DCIOutboundKpiRecordCount|Nombre d’enregistrements KPI sortants|Secondes|Total||
|DCIOutboundProfileExportCount|Nombre d’exportations de profils de sortie|Secondes|Total||
|DCIOutboundInitialProfileExportFailed|Échec de l’exportation de profil initial de sortie|Secondes|Total||
|DCIOutboundInitialProfileExportSucceeded|Réussite de l’exportation de profil initial de sortie|Secondes|Total||
|DCIOutboundInitialKpiExportFailed|Échec de l’exportation de l’indicateur KPI initial sortant|Secondes|Total||
|DCIOutboundInitialKpiExportSucceeded|Réussite de l’exportation de l’indicateur KPI initial sortant|Secondes|Total||
|DCIOutboundInitialProfileExportDurationInSeconds|Durée d’exportation de profil initial de sortie en secondes|Secondes|Total||
|AdlaJobForStandardKpiFailed|Échec du travail ADLA pour l’indicateur KPI standard en secondes|Secondes|Total||
|AdlaJobForStandardKpiTimeOut|Délai d’expiration du travail ADLA pour l’indicateur KPI standard en secondes|Secondes|Total||
|AdlaJobForStandardKpiCompleted|Achèvement du travail ADLA pour l’indicateur KPI standard en secondes|Secondes|Total||
|ImportASAValuesFailed|Nombre d’importations de valeurs ASA en échec|Nombre|Total||
|ImportASAValuesSucceeded|Nombre d’importations de valeurs ASA réussies|Nombre|Total||

## <a name="microsoftdatalakeanalyticsaccounts"></a>Microsoft.DataLakeAnalytics/accounts

|Mesure|Nom d’affichage de la mesure|Unité|Type d’agrégation|Description|
|---|---|---|---|---|
|JobEndedSuccess|Travaux réussis|Nombre|Total|Nombre de travaux réussis|
|JobEndedFailure|Travaux en échec|Nombre|Total|Nombre de travaux en échec|
|JobEndedCancelled|Travaux annulés|Nombre|Total|Nombre de travaux annulés|
|JobAUEndedSuccess|Durée AU de réussite|Secondes|Total|Durée AU totale des travaux réussis.|
|JobAUEndedFailure|Durée AU d’échec|Secondes|Total|Durée AU totale des travaux en échec|
|JobAUEndedCancelled|Durée AU d’annulation|Secondes|Total|Durée AU totale des travaux annulés|

## <a name="microsoftdbformysqlservers"></a>Microsoft.DBforMySQL/servers

|Mesure|Nom d’affichage de la mesure|Unité|Type d’agrégation|Description|
|---|---|---|---|---|
|cpu_percent|Pourcentage d’UC|Pourcentage|Moyenne|Pourcentage d’UC|
|compute_limit|Limite d’unités de calcul|Nombre|Moyenne|Limite d’unités de calcul|
|compute_consumption_percent|Pourcentage d’unités de calcul|Pourcentage|Moyenne|Pourcentage d’unités de calcul|
|memory_percent|Pourcentage de mémoire|Pourcentage|Moyenne|Pourcentage de mémoire|
|io_consumption_percent|Pourcentage d’E/S|Pourcentage|Moyenne|Pourcentage d’E/S|
|storage_percent|Pourcentage de stockage|Pourcentage|Moyenne|Pourcentage de stockage|
|storage_used|Stockage utilisé|Octets|Moyenne|Stockage utilisé|
|storage_limit|Limite de stockage|Octets|Moyenne|Limite de stockage|
|active_connections|Nombre total de connexions actif|Nombre|Moyenne|Nombre total de connexions actif|
|connections_failed|Total de connexions ayant échoué|Nombre|Moyenne|Total de connexions ayant échoué|

## <a name="microsoftdbforpostgresqlservers"></a>Microsoft.DBforPostgreSQL/servers

|Mesure|Nom d’affichage de la mesure|Unité|Type d’agrégation|Description|
|---|---|---|---|---|
|cpu_percent|Pourcentage d’UC|Pourcentage|Moyenne|Pourcentage d’UC|
|compute_limit|Limite d’unités de calcul|Nombre|Moyenne|Limite d’unités de calcul|
|compute_consumption_percent|Pourcentage d’unités de calcul|Pourcentage|Moyenne|Pourcentage d’unités de calcul|
|memory_percent|Pourcentage de mémoire|Pourcentage|Moyenne|Pourcentage de mémoire|
|io_consumption_percent|Pourcentage d’E/S|Pourcentage|Moyenne|Pourcentage d’E/S|
|storage_percent|Pourcentage de stockage|Pourcentage|Moyenne|Pourcentage de stockage|
|storage_used|Stockage utilisé|Octets|Moyenne|Stockage utilisé|
|storage_limit|Limite de stockage|Octets|Moyenne|Limite de stockage|
|active_connections|Nombre total de connexions actif|Nombre|Moyenne|Nombre total de connexions actif|
|connections_failed|Total de connexions ayant échoué|Nombre|Moyenne|Total de connexions ayant échoué|

## <a name="microsoftdevicesiothubs"></a>Microsoft.Devices/IotHubs

|Mesure|Nom d’affichage de la mesure|Unité|Type d’agrégation|Description|
|---|---|---|---|---|
|d2c.telemetry.ingress.allProtocol|Tentatives d’envoi de message de télémétrie|Nombre|Total|Nombre de toobe de tentative de messages appareil-à-cloud télémétrie envoyé tooyour IoT hub|
|d2c.telemetry.ingress.success|Messages de télémétrie envoyés|Nombre|Total|Nombre de messages de l’appareil-à-cloud télémétrie envoyé tooyour IoT hub|
|c2d.commands.egress.complete.success|Commandes terminées|Nombre|Total|Nombre de commandes cloud-à-appareil effectués par l’appareil de hello|
|c2d.commands.egress.abandon.success|Commandes abandonnées|Nombre|Total|Nombre de commandes cloud-à-appareil abandonnées par le périphérique de hello|
|c2d.commands.egress.reject.success|Commandes rejetées|Nombre|Total|Nombre de commandes cloud-à-appareil rejetés par le périphérique de hello|
|devices.totalDevices|Nombre total d’appareils|Nombre|Total|Nombre de périphériques inscrits tooyour IoT hub|
|devices.connectedDevices.allProtocol|Appareils connectés|Nombre|Total|Nombre d’unités connectées tooyour IoT hub|
|d2c.telemetry.egress.success|Messages de télémétrie remis|Nombre|Total|Nombre de fois où les messages ont été correctement écrites tooendpoints (total)|
|d2c.telemetry.egress.dropped|Messages supprimés|Nombre|Total|Nombre de messages ignorés, car le point de terminaison de remise hello a été inactif|
|d2c.telemetry.egress.orphaned|Messages orphelins|Nombre|Total|nombre de Hello de messages ne correspond ne pas à tous les itinéraires, y compris la gamme de secours hello|
|d2c.telemetry.egress.invalid|Messages non valides|Nombre|Total|Hello nombre de messages non remis en raison tooincompatibility avec point de terminaison hello|
|d2c.telemetry.egress.fallback|Messages correspondant à une condition de secours|Nombre|Total|Nombre de messages écrits de point de terminaison de secours toohello|
|d2c.endpoints.egress.eventHubs|Messages remis tooEvent points de terminaison de Hub|Nombre|Total|Nombre de messages ont des points de terminaison de Hub tooEvent écrit avec succès|
|d2c.endpoints.latency.eventHubs|Latence des messages des points de terminaison Event Hub|Millisecondes|Moyenne|latence de Hello moyenne entre toohello IoT hub message en entrée et d’entrée de message dans un point de terminaison de Hub d’événements, en millisecondes|
|d2c.endpoints.egress.serviceBusQueues|Messages remis tooService points de terminaison de file d’attente du Bus|Nombre|Total|Nombre de messages ont des points de terminaison de file d’attente du Bus tooService écrit avec succès|
|d2c.endpoints.latency.serviceBusQueues|Latence des messages des points de terminaison de files d’attente Service Bus|Millisecondes|Moyenne|latence de Hello moyenne entre toohello IoT hub message en entrée et d’entrée de message dans un point de terminaison de file d’attente du Bus de Service, en millisecondes|
|d2c.endpoints.egress.serviceBusTopics|Messages remis tooService points de terminaison de la rubrique Bus|Nombre|Total|Nombre de fois où les messages ont été correctement écrit tooService rubrique Bus points de terminaison|
|d2c.endpoints.latency.serviceBusTopics|Latence des messages des points de terminaison de rubriques Service Bus|Millisecondes|Moyenne|latence de Hello moyenne entre toohello IoT hub message en entrée et d’entrée de message dans un point de terminaison de la rubrique Service Bus, en millisecondes|
|d2c.endpoints.egress.builtIn.events|Messages remis du point de terminaison toohello intégrés (messages/événements)|Nombre|Total|Nombre de fois où les messages ont été le point de terminaison a été écrite toohello intégrés (messages/événements)|
|d2c.endpoints.latency.builtIn.events|Latence des messages pour point de terminaison hello intégrés (messages/événements)|Millisecondes|Moyenne|latence de Hello moyenne entre toohello IoT hub message en entrée et d’entrée de message dans hello intégrés point de terminaison (événements/messages), en millisecondes |
|d2c.twin.read.success|Lectures de représentations réussies d’appareils|Nombre|Total|nombre de Hello de toutes les lectures de double d’initiée par l’appareil.|
|d2c.twin.read.failure|Lectures de représentations d’appareils en échec|Nombre|Total|nombre de Hello de tous les échecs d’initiés par le périphérique de double lectures.|
|d2c.twin.read.size|Taille de la réponse des lectures de représentations des appareils|Octets|Moyenne|moyenne de Hello, min et max de réussite initiée par l’appareil à deux lectures.|
|d2c.twin.update.success|Mises à jour de représentations réussies d’appareils|Nombre|Total|nombre de Hello de toutes les mises à jour de double d’initiée par l’appareil.|
|d2c.twin.update.failure|Mises à jour de représentations d’appareils en échec|Nombre|Total|nombre de Hello de tous les échecs d’initiés par le périphérique de double les mises à jour.|
|d2c.twin.update.size|Taille des mises à jour de représentations d’appareils|Octets|Moyenne|moyenne de Hello, min et taille maximale de tous les initiés par le périphérique à deux mises à jour.|
|c2d.methods.success|Appels de méthode directe réussis|Nombre|Total|nombre de Hello réussite directe d’appels de méthode.|
|c2d.methods.failure|Appels de méthode directe en échec|Nombre|Total|nombre de Hello de tous les échecs d’appels de méthode directe.|
|c2d.methods.requestSize|Taille de demande des appels de méthode directe|Octets|Moyenne|moyenne de Hello, min et max de toutes les demandes de méthode directe.|
|c2d.methods.responseSize|Taille de réponse des appels de méthode directe|Octets|Moyenne|moyenne de Hello, min et max de toutes les réponses de réussite méthode directe.|
|c2d.twin.read.success|Lectures de représentations réussies de serveur principal|Nombre|Total|nombre de Hello de toutes les lectures de double d’initiée par back-end.|
|c2d.twin.read.failure|Lectures de représentations de serveur principal en échec|Nombre|Total|nombre de Hello de tous les échecs initiée par back-end de double lectures.|
|c2d.twin.read.size|Taille de la réponse des lectures de représentations de serveur principal|Octets|Moyenne|moyenne de Hello, min et max de réussite initiée par back-end à deux lectures.|
|c2d.twin.update.success|Mises à jour de représentations réussies de serveur principal|Nombre|Total|nombre de Hello de toutes les mises à jour de double d’initiée par back-end.|
|c2d.twin.update.failure|Mises à jour de représentations de serveur principal en échec|Nombre|Total|nombre de Hello de tous les échecs initiée par back-end de double les mises à jour.|
|c2d.twin.update.size|Taille des mises à jour de représentations de serveur principal|Octets|Moyenne|moyenne de Hello, min et max taille de tous les initiée par back-end à deux mises à jour.|
|twinQueries.success|Requêtes de représentations réussies|Nombre|Total|nombre de Hello de toutes les requêtes de double réussie.|
|twinQueries.failure|Requêtes de représentations en échec|Nombre|Total|nombre de Hello de toutes les requêtes ayant échoué double.|
|twinQueries.resultSize|Taille du résultat des requêtes de représentations|Octets|Moyenne|moyenne de Hello, min et max de la taille des résultats de toutes les requêtes réussies double hello.|
|jobs.createTwinUpdateJob.success|Créations réussies des travaux de mises à jour de représentations|Nombre|Total|nombre de Hello de tous les travaux de mise à jour de double réussie.|
|jobs.createTwinUpdateJob.failure|Créations des travaux de mises à jour de représentations en échec|Nombre|Total|nombre de Hello de tout échec de la création de travaux de mise à jour de double.|
|jobs.createDirectMethodJob.success|Créations réussies des travaux d’appel de méthode|Nombre|Total|nombre de Hello de tous les travaux d’appel de méthode directe réussie.|
|jobs.createDirectMethodJob.failure|Créations des travaux d’appel de méthode en échec|Nombre|Total|nombre de Hello de tout échec de la création de travaux d’appel de méthode directe.|
|jobs.listJobs.success|Travaux de toolist appels réussis|Nombre|Total|nombre de Hello de tous les travaux de toolist appels réussis.|
|jobs.listJobs.failure|Échecs des appels toolist travaux|Nombre|Total|nombre de Hello de tous les travaux de toolist d’appels ayant échoué.|
|jobs.cancelJob.success|Annulations de travaux réussies|Nombre|Total|nombre de Hello de réussite appelle toocancel un travail.|
|jobs.cancelJob.failure|Annulations de travaux en échec|Nombre|Total|nombre de Hello de tous les appels ayant échoué toocancel un travail.|
|jobs.queryJobs.success|Requêtes de travaux réussies|Nombre|Total|nombre de Hello de tous les travaux de tooquery appels réussis.|
|jobs.queryJobs.failure|Requêtes de travaux en échec|Nombre|Total|nombre de Hello de tous les travaux de tooquery d’appels ayant échoué.|
|jobs.completed|Travaux terminés|Nombre|Total|nombre de Hello de toutes les tâches terminées.|
|jobs.failed|Travaux en échec|Nombre|Total|nombre de Hello de toutes les tâches ayant échoué.|
|d2c.telemetry.ingress.sendThrottle|Nombre d’erreurs de limitation|Nombre|Total|Nombre d’erreurs de limitation en raison des limitations de débit toodevice|
|dailyMessageQuotaUsed|Nombre total de messages utilisés|Nombre|Moyenne|Nombre total de messages utilisés aujourd'hui|

## <a name="microsofteventhubnamespaces"></a>Microsoft.EventHub/namespaces

|Mesure|Nom d’affichage de la mesure|Unité|Type d’agrégation|Description|
|---|---|---|---|---|
|INREQS|Demandes d’envoi entrantes|Nombre|Total|Nombre total des demandes d’envoi entrantes pour un hub de notification|
|SUCCREQ|Requêtes ayant réussi|Nombre|Total|Nombre total de demandes ayant réussi pour un espace de noms|
|FAILREQ|Demandes ayant échoué|Nombre|Total|Nombre total de demandes ayant échoué pour un espace de noms|
|SVRBSY|Erreurs de serveur occupé|Nombre|Total|Nombre total d’erreurs de serveur occupé pour un espace de noms|
|INTERR|Erreurs internes du serveur|Nombre|Total|Nombre total d’erreurs de serveur internes pour un espace de noms|
|MISCERR|Autres erreurs|Nombre|Total|Nombre total de demandes ayant échoué pour un espace de noms|
|INMSGS|Messages entrants|Nombre|Total|Nombre total de messages entrants pour un espace de noms|
|OUTMSGS|Messages sortants|Nombre|Total|Nombre total de messages sortants pour un espace de noms|
|EHINMBS|Octets entrants|Octets|Total|Débit de messages entrants Event Hub pour un espace de noms|
|EHOUTMBS|Octets sortants|Octets|Total|Nombre total de messages sortants pour un espace de noms|
|EHABL|Archiver les messages de file d’attente|Nombre|Total|Messages d’archive Event Hub dans le backlog pour un espace de noms|
|EHAMSGS|Archiver les messages|Nombre|Total|Messages archivés Event Hub dans un espace de noms|
|EHAMBS|Débit message archive|Octets|Total|Débit de messages archivés Event Hub dans un espace de noms|

## <a name="microsoftlogicworkflows"></a>Microsoft.Logic/workflows

|Mesure|Nom d’affichage de la mesure|Unité|Type d’agrégation|Description|
|---|---|---|---|---|
|RunsStarted|Exécutions démarrées|Nombre|Total|Nombre d’exécutions de flux de travail démarrées.|
|RunsCompleted|Exécutions terminées|Nombre|Total|Nombre d’exécutions de flux de travail terminées.|
|RunsSucceeded|Exécutions réussies|Nombre|Total|Nombre d’exécutions de flux de travail ayant réussi.|
|RunsFailed|Exécutions ayant échoué|Nombre|Total|Nombre d’exécutions de flux de travail ayant échoué.|
|RunsCancelled|Exécutions annulées|Nombre|Total|Nombre d’exécutions de flux de travail annulées.|
|RunLatency|Latence d’exécution|Secondes|Moyenne|Latence des exécutions de flux de travail terminées.|
|RunSuccessLatency|Latence d’exécution ayant réussi|Secondes|Moyenne|Latence des exécutions de flux de travail ayant réussi.|
|RunThrottledEvents|Exécuter événements limités|Nombre|Total|Nombre d’actions de flux de travail ou d’événements limités par déclencheur.|
|RunFailurePercentage|Pourcentage d’échec des exécutions|Pourcentage|Total|Pourcentage d’exécutions de flux de travail ayant échoué.|
|ActionsStarted|Actions démarrées |Nombre|Total|Nombre d’actions de flux de travail démarrées.|
|ActionsCompleted|Actions terminées |Nombre|Total|Nombre d’actions de flux de travail terminées.|
|ActionsSucceeded|Actions ayant réussi |Nombre|Total|Nombre d’actions de flux de travail ayant réussi.|
|ActionsFailed|Actions ayant échoué|Nombre|Total|Nombre d’actions de flux de travail ayant échoué.|
|ActionsSkipped|Actions ignorées |Nombre|Total|Nombre d’actions de flux de travail ignorées.|
|ActionLatency|Latence de l’action |Secondes|Moyenne|Latence des actions de flux de travail terminés.|
|ActionSuccessLatency|Latence de réussite d’action |Secondes|Moyenne|Latence des actions de flux de travail ayant réussi.|
|ActionThrottledEvents|Événements d’action limitée|Nombre|Total|Nombre d’événements limités d’action de flux de travail.|
|TriggersStarted|Déclenchements lancés |Nombre|Total|Nombre de déclencheurs de flux de travail démarrés.|
|TriggersCompleted|Déclenchements terminés |Nombre|Total|Nombre de déclencheurs de flux de travail terminés.|
|TriggersSucceeded|Déclenchements ayant réussi |Nombre|Total|Nombre de déclencheurs de flux de travail ayant réussi.|
|TriggersFailed|Déclenchements ayant échoué |Nombre|Total|Nombre de déclencheurs de flux de travail ayant échoué.|
|TriggersSkipped|Déclenchements ignorés|Nombre|Total|Nombre de déclencheurs de flux de travail ignorés.|
|TriggersFired|Déclenchements activés |Nombre|Total|Nombre de déclencheurs de flux de travail activés.|
|TriggerLatency|Latence de déclencheur |Secondes|Moyenne|Latence des déclenchements de flux de travail terminés.|
|TriggerFireLatency|Latence d’activation de déclencheur |Secondes|Moyenne|Latence des déclencheurs de flux de travail activés.|
|TriggerSuccessLatency|Latence déclencheur ayant réussi |Secondes|Moyenne|Latence des déclencheurs de flux de travail ayant réussi.|
|TriggerThrottledEvents|Événements limités par déclencheur|Nombre|Total|Nombre d’événements de flux de travail limités par déclencheur.|
|BillableActionExecutions|Exécutions d’actions facturables|Nombre|Total|Nombre d’exécutions d’actions de flux de travail facturées.|
|BillableTriggerExecutions|Exécutions de déclencheurs facturables|Nombre|Total|Nombre d’exécutions de déclencheurs de flux de travail facturées.|
|TotalBillableExecutions|Nombre total d’exécutions facturables|Nombre|Total|Nombre d’exécutions de flux de travail facturées.|

## <a name="microsoftnetworkapplicationgateways"></a>Microsoft.Network/applicationGateways

|Mesure|Nom d’affichage de la mesure|Unité|Type d’agrégation|Description|
|---|---|---|---|---|
|Throughput|Throughput|BytesPerSecond|Moyenne||

## <a name="microsoftnetworkexpressroutecircuits"></a>Microsoft.Network/expressRouteCircuits

|Mesure|Nom d’affichage de la mesure|Unité|Type d’agrégation|Description|
|---|---|---|---|---|
|BytesIn|BytesIn|Nombre|Total||
|BytesOut|BytesOut|Nombre|Total||

## <a name="microsoftnotificationhubsnamespacesnotificationhubs"></a>Microsoft.NotificationHubs/Namespaces/NotificationHubs

|Mesure|Nom d’affichage de la mesure|Unité|Type d’agrégation|Description|
|---|---|---|---|---|
|registration.all|Opération d’inscription|Nombre|Total|nombre de Hello de toutes les opérations d’inscription réussie (requêtes de mises à jour de créations et suppressions). |
|registration.create|Opérations de création d’inscription|Nombre|Total|nombre de Hello de toutes les créations d’une inscription réussie.|
|registration.update|Opérations de mise à jour d’inscription|Nombre|Total|nombre de Hello de toutes les mises à jour de l’enregistrement est effectué.|
|registration.get|Opérations de lecture d’inscription|Nombre|Total|nombre de Hello de toutes les requêtes d’inscription réussie.|
|registration.delete|Opérations de suppression d’inscription|Nombre|Total|nombre de Hello de toutes les suppressions d’une inscription réussie.|
|incoming|Messages entrants|Nombre|Total|nombre Hello de tous les appels d’API d’envoi. |
|incoming.scheduled|Notifications Push planifiées envoyées|Nombre|Total|Notifications Push planifiées annulées|
|incoming.scheduled.cancel|Notifications Push planifiées annulées|Nombre|Total|Notifications Push planifiées annulées|
|scheduled.pending|Notifications planifiées en attente|Nombre|Total|Notifications planifiées en attente|
|installation.all|Opérations de gestion de l’installation|Nombre|Total|Opérations de gestion de l’installation|
|installation.get|Opérations d’obtention d’installation|Nombre|Total|Opérations d’obtention d’installation|
|installation.upsert|Opérations de création ou de mise à jour d’installation|Nombre|Total|Opérations de création ou de mise à jour d’installation|
|installation.patch|Opérations d’installation de correctif|Nombre|Total|Opérations d’installation de correctif|
|installation.delete|Opérations de suppression d’installation|Nombre|Total|Opérations de suppression d’installation|
|outgoing.allpns.success|Notifications réussies|Nombre|Total|nombre de Hello de toutes les notifications.|
|outgoing.allpns.invalidpayload|Erreurs de charge utile|Nombre|Total|nombre de Hello de Push a échoué, car hello PNS a retourné une erreur de la charge utile incorrect.|
|outgoing.allpns.pnserror|Erreurs système de notification externe|Nombre|Total|nombre de Hello de Push a échoué en raison d’un problème de communication avec hello PNS (exclut les problèmes d’authentification).|
|outgoing.allpns.channelerror|Erreurs de canal|Nombre|Total|nombre de Hello d’exécute un push qui a échoué, car le canal de hello n’est pas valide non associé hello correct application accélérée ou a expiré.|
|outgoing.allpns.badorexpiredchannel|Erreurs de canal incorrect ou arrivé à expiration|Nombre|Total|nombre de Hello d’exécute un push qui a échoué, car le canal/jeton/registrationId hello dans l’enregistrement de hello a expiré ou non valide.|
|outgoing.wns.success|Notifications WNS réussies|Nombre|Total|nombre de Hello de toutes les notifications.|
|outgoing.wns.invalidcredentials|Erreurs d’autorisation WNS (informations d’identification non valides)|Nombre|Total|nombre de Hello d’exécute un push qui a échoué, car hello PNS n’a pas accepté hello fourni d’informations d’identification ou hello sont bloqués. (Windows Live ne reconnaît pas les informations d’identification de hello).|
|outgoing.wns.badchannel|Erreur de canal WNS incorrect|Nombre|Total|Hello nombre de Push a échoué car hello ChannelURI dans l’enregistrement de hello n’est pas reconnu (état WNS : 404 introuvable).|
|outgoing.wns.expiredchannel|Erreur de canal WNS arrivé à expiration|Nombre|Total|Hello nombre de Push a échoué car hello ChannelURI est expiré (état WNS : 410 Gone).|
|outgoing.wns.throttled|Notifications WNS limitées|Nombre|Total|Hello nombre de Push a échoué, car cette application est la limitation de WNS (état WNS : 406 non Acceptable).|
|outgoing.wns.tokenproviderunreachable|Erreurs d’autorisation WNS (inaccessible)|Nombre|Total|Windows Live n’est pas accessible.|
|outgoing.wns.invalidtoken|Erreurs d’autorisation WNS (jeton non valide)|Nombre|Total|Hello jeton fourni tooWNS n’est pas valide (état WNS : 401 non autorisé).|
|outgoing.wns.wrongtoken|Erreurs d’autorisation WNS (jeton incorrect)|Nombre|Total|Hello jeton fourni tooWNS est valide, mais pour une autre application (état WNS : 403 Interdit). Cela peut se produire si hello ChannelURI dans l’enregistrement de hello est associé à une autre application. Vérifiez cette application de client hello est associée à hello même application dont informations d’identification sont dans le hub de notification hello.|
|outgoing.wns.invalidnotificationformat|Format de notification WNS non valide|Nombre|Total|format Hello de notification de hello n’est pas valide (état WNS : 400). Notez que WNS ne rejette pas toutes les charges utiles non valides.|
|outgoing.wns.invalidnotificationsize|Erreur de taille de notification WNS non valide|Nombre|Total|charge utile de notification Hello est trop grande (état WNS : 413).|
|outgoing.wns.channelthrottled|Canal WNS limité|Nombre|Total|notification de Hello a été supprimée, car hello ChannelURI dans l’enregistrement de hello est limitée (en-tête de réponse WNS : X-WNS-NotificationStatus:channelThrottled).|
|outgoing.wns.channeldisconnected|Canal WNS déconnecté|Nombre|Total|notification de Hello a été supprimée, car hello ChannelURI dans l’enregistrement de hello est limitée (en-tête de réponse WNS : X-WNS-DeviceConnectionStatus : déconnecté).|
|outgoing.wns.dropped|Notifications WNS supprimées|Nombre|Total|notification de Hello a été supprimée, car hello ChannelURI dans l’enregistrement de hello est limitée (X-WNS-NotificationStatus : supprimée mais pas X-WNS-DeviceConnectionStatus : déconnecté).|
|outgoing.wns.pnserror|Erreurs WNS|Nombre|Total|La notification n’a pas été remise en raison d’erreurs de communication avec WNS.|
|outgoing.wns.authenticationerror|Erreurs d’authentification WNS|Nombre|Total|La notification n’a pas été remise en raison d’erreurs de communication avec Windows Live, d’informations d’identification non valides ou d’un jeton incorrect.|
|outgoing.apns.success|Notifications APNS réussies|Nombre|Total|nombre de Hello de toutes les notifications.|
|outgoing.apns.invalidcredentials|Erreurs d’autorisation APNS|Nombre|Total|nombre de Hello d’exécute un push qui a échoué, car hello PNS n’a pas accepté hello fourni d’informations d’identification ou hello sont bloqués.|
|outgoing.apns.badchannel|Erreur de canal APNS incorrect|Nombre|Total|Hello nombre de Push a échoué, car le jeton de hello n’est pas valide (code d’état APNS : 8).|
|outgoing.apns.expiredchannel|Erreur de canal APNS arrivé à expiration|Nombre|Total|nombre de Hello du jeton qui ont été invalidés par canal de commentaires d’APNS hello.|
|outgoing.apns.invalidnotificationsize|Erreur de taille de notification APNS non valide|Nombre|Total|Hello nombre de Push a échoué, car la charge utile de hello était trop volumineuse (code d’état APNS : 7).|
|outgoing.apns.pnserror|Erreurs APNS|Nombre|Total|nombre de Hello d’exécute un push qui a échoué en raison d’erreurs de communication avec APNS.|
|outgoing.gcm.success|Notifications GCM réussies|Nombre|Total|nombre de Hello de toutes les notifications.|
|outgoing.gcm.invalidcredentials|Erreurs d’autorisation GCM (informations d’identification non valides)|Nombre|Total|nombre de Hello d’exécute un push qui a échoué, car hello PNS n’a pas accepté hello fourni d’informations d’identification ou hello sont bloqués.|
|outgoing.gcm.badchannel|Erreur de canal GCM incorrect|Nombre|Total|Hello nombre de Push a échoué car registrationId hello dans l’enregistrement de hello n’est pas reconnu (résultats GCM : enregistrement non valide).|
|outgoing.gcm.expiredchannel|Erreur de canal GCM arrivé à expiration|Nombre|Total|Hello nombre de Push a échoué car registrationId hello dans l’enregistrement de hello a expiré (résultats GCM : NotRegistered).|
|outgoing.gcm.throttled|Notifications GCM limitées|Nombre|Total|Hello nombre de Push a échoué, car le GCM limitées à cette application (code d’état GCM : 501-599 ou résultat : non disponible).|
|outgoing.gcm.invalidnotificationformat|Format de notification GCM non valide|Nombre|Total|Hello nombre de Push a échoué, car la charge utile de hello n’a pas été formaté correctement (les résultats GCM : InvalidDataKey ou InvalidTtl).|
|outgoing.gcm.invalidnotificationsize|Erreur de taille de notification GCM non valide|Nombre|Total|Hello nombre de Push a échoué, car la charge utile de hello était trop volumineuse (résultats GCM : MessageTooBig).|
|outgoing.gcm.wrongchannel|Erreur de canal GCM incorrect|Nombre|Total|nombre de Hello de Push a échoué car registrationId hello dans l’enregistrement de hello n’est pas associé application en cours de toohello (résultats GCM : InvalidPackageName).|
|outgoing.gcm.pnserror|Erreurs GCM|Nombre|Total|nombre de Hello d’exécute un push qui a échoué en raison d’erreurs de communication avec GCM.|
|outgoing.gcm.authenticationerror|Erreurs d’authentification GCM|Nombre|Total|Hello nombre de Push a échoué car hello PNS n’a pas accepté hello fourni d’informations d’identification de hello informations d’identification sont bloquées ou hello ID d’expéditeur n’est pas configuré correctement dans l’application hello (résultats GCM : MismatchedSenderId).|
|outgoing.mpns.success|Notifications MPNS réussies|Nombre|Total|nombre de Hello de toutes les notifications.|
|outgoing.mpns.invalidcredentials|Informations d’identification MPNS non valides|Nombre|Total|nombre de Hello d’exécute un push qui a échoué, car hello PNS n’a pas accepté hello fourni d’informations d’identification ou hello sont bloqués.|
|outgoing.mpns.badchannel|Erreur de canal incorrect MPNS|Nombre|Total|Hello nombre de Push a échoué car hello ChannelURI dans l’enregistrement de hello n’est pas reconnu (état MPNS : 404 introuvable).|
|outgoing.mpns.throttled|Notifications MPNS limitées|Nombre|Total|Hello nombre de Push a échoué, car cette application est la limitation de MPNS (WNS MPNS : 406 non Acceptable).|
|outgoing.mpns.invalidnotificationformat|Format de notification MPNS non valide|Nombre|Total|nombre de Hello d’exécute un push qui a échoué, car la charge utile de hello de notification de hello était trop volumineuse.|
|outgoing.mpns.channeldisconnected|Canal MPNS déconnecté|Nombre|Total|nombre de Push a échoué car hello ChannelURI dans l’enregistrement de hello a été déconnectée de Hello (état MPNS : 412 introuvable).|
|outgoing.mpns.dropped|Notifications MPNS supprimées|Nombre|Total|Hello nombre de push qui ont été supprimés par MPNS (en-tête de réponse MPNS : X-NotificationStatus : QueueFull ou Suppressed).|
|outgoing.mpns.pnserror|Erreurs MPNS|Nombre|Total|nombre de Hello d’exécute un push qui a échoué en raison d’erreurs de communication avec MPNS.|
|outgoing.mpns.authenticationerror|Erreurs d’authentification MPNS|Nombre|Total|nombre de Hello d’exécute un push qui a échoué, car hello PNS n’a pas accepté hello fourni d’informations d’identification ou hello sont bloqués.|
|notificationhub.pushes|Toutes les notifications sortantes|Nombre|Total|Toutes les notifications sortantes du hub de notification hello|
|incoming.all.requests|Toutes les demandes entrantes|Nombre|Total|Nombre total des demandes entrantes pour un hub de notification|
|incoming.all.failedrequests|Toutes les requêtes entrantes ayant échoué|Nombre|Total|Nombre total des demandes entrantes ayant échoué pour un hub de notification|

## <a name="microsoftpowerbidedicatedcapacities"></a>Microsoft.PowerBIDedicated/capacities

|Mesure|Nom d’affichage de la mesure|Unité|Type d’agrégation|Description|
|---|---|---|---|---|
|qpu_metric|QPU|Nombre|Moyenne|QPU. Plage de 0 à 100 pour S1, de 0 à 200 pour S2 et de 0 à 400 pour S4|
|memory_metric|Mémoire|Octets|Moyenne|Mémoire. Plage de 0 à 25 Go pour S1, de 0 à 50 Go pour S2 et de 0 à 100 Go pour S4|
|TotalConnectionRequests|Nombre total de demandes de connexion|Nombre|Moyenne|Nombre total de demandes de connexion. Il s’agit des arrivées.|
|SuccessfullConnectionsPerSec|Connexions réussies par seconde|CountPerSecond|Moyenne|Taux de connexions terminées réussies.|
|TotalConnectionFailures|Nombre total d’échecs de connexion|Nombre|Moyenne|Total des échecs de tentatives de connexion.|
|CurrentUserSessions|Sessions utilisateur actuelles|Nombre|Moyenne|Nombre actuel de sessions utilisateur établies.|
|QueryPoolBusyThreads|Threads occupés du pool de threads de requêtes|Nombre|Moyenne|Nombre de threads occupés dans le pool de threads de requête hello.|
|CommandPoolJobQueueLength|Longueur de la file d’attente des travaux du pool de commandes|Nombre|Moyenne|Nombre de travaux dans la file d’attente hello du pool de threads de commande hello.|
|ProcessingPoolJobQueueLength|Longueur de la file d’attente des travaux du pool de traitement|Nombre|Moyenne|Nombre de travaux de non-E/s dans la file d’attente hello Hello pool de threads de traitement.|
|CurrentConnections|Connexion : connexions actuelles|Nombre|Moyenne|Nombre actuel de connexions client établies.|
|CleanerCurrentPrice|Mémoire : prix actuel du nettoyage|Nombre|Moyenne|Prix actuel de la mémoire, $/ octet/temps, normalisé too1000.|
|CleanerMemoryShrinkable|Mémoire : mémoire de nettoyage réductible|Octets|Moyenne|Quantité de mémoire, en octets, toopurging objet par le nettoyeur d’arrière-plan hello.|
|CleanerMemoryNonshrinkable|Mémoire : mémoire de nettoyage non réductible|Octets|Moyenne|Quantité de mémoire, en octets, pas sujet toopurging par le nettoyeur d’arrière-plan hello.|
|MemoryUsage|Mémoire : utilisation de la mémoire|Octets|Moyenne|Utilisation de la mémoire de processus serveur hello dans le calcul du coût de la mémoire nettoyage. Égale toocounter process\\privatebytes et taille de hello de données mappé en mémoire, en ignorant toute mémoire mappée ou allouée par le moteur de mémoire analytique hello xVelocity (VertiPaq) dépassant le moteur xVelocity de hello limite de mémoire.|
|MemoryLimitHard|Mémoire : limite de mémoire physique|Octets|Moyenne|Limite de mémoire physique, du fichier de configuration.|
|MemoryLimitHigh|Mémoire : limite de mémoire élevée|Octets|Moyenne|Limite de mémoire élevée, du fichier de configuration.|
|MemoryLimitLow|Mémoire : limite de mémoire basse|Octets|Moyenne|Limite de mémoire basse, du fichier de configuration.|
|MemoryLimitVertiPaq|Mémoire : limite de mémoire VertiPaq|Octets|Moyenne|Limite en mémoire, du fichier de configuration.|
|Quota|Mémoire : quota|Octets|Moyenne|Quota de mémoire actuel, en octets. Le quota de mémoire est également appelé réserve de mémoire ou d’allocation.|
|QuotaBlocked|Mémoire : quota bloqué|Nombre|Moyenne|Nombre actuel de requêtes de quota qui sont bloquées en attendant la libération d’autres quotas de mémoire.|
|VertiPaqNonpaged|Mémoire : réserve non paginée VertiPaq|Octets|Moyenne|Octets de mémoire verrouillée dans le jeu de travail hello pour une utilisation par le moteur de hello en mémoire.|
|VertiPaqPaged|Mémoire : réserve paginée VertiPaq|Octets|Moyenne|Octets de mémoire paginée utilisée pour les données en mémoire.|
|RowsReadPerSec|Traitement : lignes lues par seconde|CountPerSecond|Moyenne|Taux de lignes lues à partir de toutes les bases de données relationnelles.|
|RowsConvertedPerSec|Traitement : lignes converties par seconde|CountPerSecond|Moyenne|Taux de lignes converties lors du traitement.|
|RowsWrittenPerSec|Traitement : lignes écrites par seconde|CountPerSecond|Moyenne|Taux de lignes écrites lors du traitement.|
|CommandPoolBusyThreads|Threads : threads occupés du pool commandes|Nombre|Moyenne|Nombre de threads occupés dans le pool de threads de commande hello.|
|CommandPoolIdleThreads|Threads : threads inactifs du pool commande|Nombre|Moyenne|Nombre de threads inactifs dans le pool de threads de commande hello.|
|LongParsingBusyThreads|Threads : threads d’analyse longue occupés|Nombre|Moyenne|Nombre de threads occupés dans hello pool de threads d’analyse longue.|
|LongParsingIdleThreads|Threads : threads d’analyse longue inactifs|Nombre|Moyenne|Nombre de threads inactifs dans hello pool de threads d’analyse longue.|
|LongParsingJobQueueLength|Threads : durée de file d’attente des travaux d’analyse longue|Nombre|Moyenne|Nombre de travaux dans la file d’attente hello Hello pool de threads d’analyse longue.|
|ProcessingPoolBusyIOJobThreads|Threads : traitement des threads de travail d’E/S occupés du pool|Nombre|Moyenne|Nombre de threads exécutant des travaux d’e/s dans le pool de threads de traitement de hello.|
|ProcessingPoolBusyNonIOThreads|Threads : traitement des threads de travail autres qu’E/S occupés du pool|Nombre|Moyenne|Nombre de threads exécutant des travaux de non-E/s dans le pool de threads de traitement de hello.|
|ProcessingPoolIOJobQueueLength|Threads : longueur de la file d’attente des travaux d’E/S du pool de traitement|Nombre|Moyenne|Nombre de travaux d’e/s dans la file d’attente hello Hello pool de threads de traitement.|
|ProcessingPoolIdleIOJobThreads|Threads : traitement des threads de travail d’E/S ignorés du pool|Nombre|Moyenne|Nombre de threads inactifs pour les travaux d’e/s dans le pool de threads de traitement de hello.|
|ProcessingPoolIdleNonIOThreads|Threads : traitement des threads de travail autres qu’E/S inactifs du pool|Nombre|Moyenne|Nombre de threads inactifs dans le pool de threads de traitement de hello dédié des travaux d’e/S toonon.|
|QueryPoolIdleThreads|Threads : threads inactifs du pool de requêtes|Nombre|Moyenne|Nombre de threads inactifs pour les travaux d’e/s dans le pool de threads de traitement de hello.|
|QueryPoolJobQueueLength|Threads : longueur de file d’attente de travaux du pool de requêtes|Nombre|Moyenne|Nombre de travaux dans la file d’attente hello du pool de threads de requête hello.|
|ShortParsingBusyThreads|Threads : threads d’analyse courte occupés|Nombre|Moyenne|Nombre de threads occupés dans hello court de pool de threads d’analyse.|
|ShortParsingIdleThreads|Threads : threads d’analyse courte inactifs|Nombre|Moyenne|Nombre de threads inactifs dans hello court de pool de threads d’analyse.|
|ShortParsingJobQueueLength|Threads : durée de file d’attente des travaux d’analyse courte|Nombre|Moyenne|Nombre de travaux dans la file d’attente hello Hello court de pool de threads d’analyse.|
|memory_thrashing_metric|Vidage de mémoire|Pourcentage|Moyenne|Vidage de mémoire moyenne.|

## <a name="microsoftsearchsearchservices"></a>Microsoft.Search/searchServices

|Mesure|Nom d’affichage de la mesure|Unité|Type d’agrégation|Description|
|---|---|---|---|---|
|SearchLatency|Latence de recherche|Secondes|Moyenne|Latence moyenne recherche hello service de recherche|
|SearchQueriesPerSecond|Requêtes de recherche par seconde|CountPerSecond|Moyenne|Requêtes de recherche par seconde pour le service de recherche hello|
|ThrottledSearchQueriesPercentage|Pourcentage de requêtes de recherche limitées|Pourcentage|Moyenne|Pourcentage de requêtes de recherche qui ont été limitée pour le service de recherche hello|

## <a name="microsoftservicebusnamespaces"></a>Microsoft.ServiceBus/namespaces

|Mesure|Nom d’affichage de la mesure|Unité|Type d’agrégation|Description|
|---|---|---|---|---|
|CPUXNS|Utilisation du processeur par espace de noms|Pourcentage|Maximale|Mesure d’utilisation du processeur de l’espace de noms Service Bus Premium|
|WSXNS|Utilisation de la taille mémoire par espace de noms|Pourcentage|Maximale|Mesure d’utilisation de la mémoire de l’espace de noms Service Bus Premium|

## <a name="microsoftsqlserversdatabases"></a>Microsoft.Sql/servers/databases

|Mesure|Nom d’affichage de la mesure|Unité|Type d’agrégation|Description|
|---|---|---|---|---|
|cpu_percent|Pourcentage UC|Pourcentage|Moyenne|Pourcentage UC|
|physical_data_read_percent|Pourcentage E/S des données|Pourcentage|Moyenne|Pourcentage E/S des données|
|log_write_percent|Pourcentage E/S du journal|Pourcentage|Moyenne|Pourcentage E/S du journal|
|dtu_consumption_percent|Pourcentage DTU|Pourcentage|Moyenne|Pourcentage DTU|
|storage|Taille de base de données totale|Octets|Maximale|Taille de base de données totale|
|connection_successful|Connexions réussies|Nombre|Total|Connexions réussies|
|connection_failed|Connexions ayant échoué|Nombre|Total|Connexions ayant échoué|
|blocked_by_firewall|Bloqué par le pare-feu|Nombre|Total|Bloqué par le pare-feu|
|deadlock|Blocages|Nombre|Total|Blocages|
|storage_percent|Pourcentage de la taille de la base de données|Pourcentage|Maximale|Pourcentage de la taille de la base de données|
|xtp_storage_percent|Pourcentage de stockage OLTP en mémoire|Pourcentage|Moyenne|Pourcentage de stockage OLTP en mémoire|
|workers_percent|Pourcentage de travaux|Pourcentage|Moyenne|Pourcentage de travaux|
|sessions_percent|Pourcentage de sessions|Pourcentage|Moyenne|Pourcentage de sessions|
|dtu_limit|Limite DTU|Nombre|Moyenne|Limite DTU|
|dtu_used|DTU utilisé|Nombre|Moyenne|DTU utilisé|
|dwu_limit|Limite DWU|Nombre|Maximale|Limite DWU|
|dwu_consumption_percent|Pourcentage DWU|Pourcentage|Maximale|Pourcentage DWU|
|dwu_used|DWU utilisé|Nombre|Maximale|DWU utilisé|

## <a name="microsoftsqlserverselasticpools"></a>Microsoft.Sql/servers/elasticPools

|Mesure|Nom d’affichage de la mesure|Unité|Type d’agrégation|Description|
|---|---|---|---|---|
|cpu_percent|Pourcentage UC|Pourcentage|Moyenne|Pourcentage UC|
|database_cpu_percent|Pourcentage UC|Pourcentage|Moyenne|Pourcentage UC|
|physical_data_read_percent|Pourcentage E/S des données|Pourcentage|Moyenne|Pourcentage E/S des données|
|database_physical_data_read_percent|Pourcentage E/S des données|Pourcentage|Moyenne|Pourcentage E/S des données|
|log_write_percent|Pourcentage E/S du journal|Pourcentage|Moyenne|Pourcentage E/S du journal|
|database_log_write_percent|Pourcentage E/S du journal|Pourcentage|Moyenne|Pourcentage E/S du journal|
|dtu_consumption_percent|Pourcentage DTU|Pourcentage|Moyenne|Pourcentage DTU|
|database_dtu_consumption_percent|Pourcentage DTU|Pourcentage|Moyenne|Pourcentage DTU|
|storage_percent|Pourcentage de stockage|Pourcentage|Moyenne|Pourcentage de stockage|
|workers_percent|Pourcentage de travaux|Pourcentage|Moyenne|Pourcentage de travaux|
|database_workers_percent|Pourcentage de travaux|Pourcentage|Moyenne|Pourcentage de travaux|
|sessions_percent|Pourcentage de sessions|Pourcentage|Moyenne|Pourcentage de sessions|
|database_sessions_percent|Pourcentage de sessions|Pourcentage|Moyenne|Pourcentage de sessions|
|eDTU_limit|Limite eDTU|Nombre|Moyenne|Limite eDTU|
|storage_limit|Limite de stockage|Octets|Moyenne|Limite de stockage|
|eDTU_used|eDTU utilisé|Nombre|Moyenne|eDTU utilisé|
|storage_used|Stockage utilisé|Octets|Moyenne|Stockage utilisé|
|database_storage_used|Stockage utilisé|Octets|Moyenne|Stockage utilisé|
|xtp_storage_percent|Pourcentage de stockage OLTP en mémoire|Pourcentage|Moyenne|Pourcentage de stockage OLTP en mémoire|

## <a name="microsoftsqlservers"></a>Microsoft.Sql/servers

|Mesure|Nom d’affichage de la mesure|Unité|Type d’agrégation|Description|
|---|---|---|---|---|
|dtu_consumption_percent|Pourcentage DTU|Pourcentage|Moyenne|Pourcentage DTU|
|database_dtu_consumption_percent|Pourcentage DTU|Pourcentage|Moyenne|Pourcentage DTU|
|storage_used|Stockage utilisé|Octets|Moyenne|Stockage utilisé|
|database_storage_used|Stockage utilisé|Octets|Moyenne|Stockage utilisé|

## <a name="microsoftstreamanalyticsstreamingjobs"></a>Microsoft.StreamAnalytics/streamingjobs

|Mesure|Nom d’affichage de la mesure|Unité|Type d’agrégation|Description|
|---|---|---|---|---|
|ResourceUtilization|Utilisation de % d’unités de diffusion|Pourcentage|Maximale|Utilisation de % d’unités de diffusion|
|InputEvents|Événements d’entrée|Nombre|Total|Événements d’entrée|
|InputEventBytes|Octets des événements d’entrée|Octets|Total|Octets des événements d’entrée|
|LateInputEvents|Événements d’entrée tardifs|Nombre|Total|Événements d’entrée tardifs|
|OutputEvents|Événements de sortie|Nombre|Total|Événements de sortie|
|ConversionErrors|Erreurs de conversion de données|Nombre|Total|Erreurs de conversion de données|
|Errors|Erreurs d’exécution|Nombre|Total|Erreurs d’exécution|
|DroppedOrAdjustedEvents|Événements en désordre|Nombre|Total|Événements en désordre|
|AMLCalloutRequests|Requêtes de fonction|Nombre|Total|Requêtes de fonction|
|AMLCalloutFailedRequests|Requêtes de fonction ayant échoué|Nombre|Total|Requêtes de fonction ayant échoué|
|AMLCalloutInputEvents|Événements de fonction|Nombre|Total|Événements de fonction|

## <a name="microsoftwebserverfarms"></a>Microsoft.Web/serverfarms

|Mesure|Nom d’affichage de la mesure|Unité|Type d’agrégation|Description|
|---|---|---|---|---|
|CpuPercentage|Pourcentage UC|Pourcentage|Moyenne|Pourcentage UC|
|MemoryPercentage|Pourcentage de mémoire|Pourcentage|Moyenne|Pourcentage de mémoire|
|DiskQueueLength|Longueur de file d'attente de disque|Nombre|Total|Longueur de file d'attente de disque|
|HttpQueueLength|Longueur de la file d’attente HTTP|Nombre|Total|Longueur de la file d’attente HTTP|
|BytesReceived|Données entrantes|Octets|Total|Données entrantes|
|BytesSent|Données sortantes|Octets|Total|Données sortantes|

## <a name="microsoftwebsites-excluding-functions"></a>Microsoft.Web/sites (à l’exclusion de Functions)

|Mesure|Nom d’affichage de la mesure|Unité|Type d’agrégation|Description|
|---|---|---|---|---|
|CpuTime|Temps processeur|Secondes|Total|Temps processeur|
|Requests|Requests|Nombre|Total|Requests|
|BytesReceived|Données entrantes|Octets|Total|Données entrantes|
|BytesSent|Données sortantes|Octets|Total|Données sortantes|
|Http101|HTTP 101|Nombre|Total|HTTP 101|
|Http2xx|Http 2xx|Nombre|Total|Http 2xx|
|Http3xx|Http 3xx|Nombre|Total|Http 3xx|
|Http401|Http 401|Nombre|Total|Http 401|
|Http403|Http 403|Nombre|Total|Http 403|
|Http404|Http 404|Nombre|Total|Http 404|
|Http406|Http 406|Nombre|Total|Http 406|
|Http4xx|Http 4xx|Nombre|Total|Http 4xx|
|Http5xx|Erreurs de serveur http|Nombre|Total|Erreurs de serveur http|
|MemoryWorkingSet|Plage de travail de la mémoire|Octets|Moyenne|Plage de travail de la mémoire|
|AverageMemoryWorkingSet|Plage de travail moyenne de la mémoire|Octets|Moyenne|Plage de travail moyenne de la mémoire|
|AverageResponseTime|Temps de réponse moyen|Secondes|Moyenne|Temps de réponse moyen|

## <a name="microsoftwebsites-functions"></a>Microsoft.Web/sites (Functions)

|Mesure|Nom d’affichage de la mesure|Unité|Type d’agrégation|Description|
|---|---|---|---|---|
|BytesReceived|Données entrantes|Octets|Total|Données entrantes|
|BytesSent|Données sortantes|Octets|Total|Données sortantes|
|Http5xx|Erreurs de serveur http|Nombre|Total|Erreurs de serveur http|
|MemoryWorkingSet|Plage de travail de la mémoire|Octets|Moyenne|Plage de travail de la mémoire|
|AverageMemoryWorkingSet|Plage de travail moyenne de la mémoire|Octets|Moyenne|Plage de travail moyenne de la mémoire|
|FunctionExecutionUnits|Unités d’exécution de fonctions|Nombre|Moyenne|Unités d’exécution de fonctions|
|FunctionExecutionCount|Nombre d’exécutions de fonctions|Nombre|Moyenne|Nombre d’exécutions de fonctions|

## <a name="microsoftwebsitesslots"></a>Microsoft.Web/sites/slots

|Mesure|Nom d’affichage de la mesure|Unité|Type d’agrégation|Description|
|---|---|---|---|---|
|CpuTime|Temps processeur|Secondes|Total|Temps processeur|
|Requests|Requests|Nombre|Total|Requests|
|BytesReceived|Données entrantes|Octets|Total|Données entrantes|
|BytesSent|Données sortantes|Octets|Total|Données sortantes|
|Http101|HTTP 101|Nombre|Total|HTTP 101|
|Http2xx|Http 2xx|Nombre|Total|Http 2xx|
|Http3xx|Http 3xx|Nombre|Total|Http 3xx|
|Http401|Http 401|Nombre|Total|Http 401|
|Http403|Http 403|Nombre|Total|Http 403|
|Http404|Http 404|Nombre|Total|Http 404|
|Http406|Http 406|Nombre|Total|Http 406|
|Http4xx|Http 4xx|Nombre|Total|Http 4xx|
|Http5xx|Erreurs de serveur http|Nombre|Total|Erreurs de serveur http|
|MemoryWorkingSet|Plage de travail de la mémoire|Octets|Moyenne|Plage de travail de la mémoire|
|AverageMemoryWorkingSet|Plage de travail moyenne de la mémoire|Octets|Moyenne|Plage de travail moyenne de la mémoire|
|AverageResponseTime|Temps de réponse moyen|Secondes|Moyenne|Temps de réponse moyen|
|FunctionExecutionUnits|Unités d’exécution de fonctions|Nombre|Moyenne|Unités d’exécution de fonctions|
|FunctionExecutionCount|Nombre d’exécutions de fonctions|Nombre|Moyenne|Nombre d’exécutions de fonctions|

## <a name="next-steps"></a>Étapes suivantes
* [En savoir plus sur les mesures dans Azure Monitor](monitoring-overview-metrics.md)
* [Créer des alertes sur les mesures](insights-receive-alert-notifications.md)
* [Exportation des métriques toostorage, concentrateur d’événements ou Analytique de journal](monitoring-overview-of-diagnostic-logs.md)
