---
title: "aaaMonitor, diagnostiquer et résoudre les problèmes de stockage Azure | Documents Microsoft"
description: "Utiliser les fonctionnalités, comme analytique de stockage, journalisation, côté client et les autres outils tiers tooidentify, diagnostiquer et résoudre les problèmes liés au stockage Azure."
services: storage
documentationcenter: 
author: fhryo-msft
manager: jahogg
editor: tysonn
ms.assetid: d1e87d98-c763-4caa-ba20-2cf85f853303
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: fhryo-msft
ms.openlocfilehash: 43f34a4ccbc3071cdb489958252498a1f88e1a34
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-diagnose-and-troubleshoot-microsoft-azure-storage"></a>Surveiller, diagnostiquer et résoudre les problèmes liés à Microsoft Azure Storage
[!INCLUDE [storage-selector-portal-monitoring-diagnosing-troubleshooting](../../../includes/storage-selector-portal-monitoring-diagnosing-troubleshooting.md)]

## <a name="overview"></a>Vue d'ensemble
Le diagnostic et la résolution des problèmes dans une application distribuée hébergée dans un environnement cloud peuvent s'avérer plus complexes que dans des environnements traditionnels. Les applications peuvent être déployées dans une infrastructure PaaS ou IaaS, localement, sur un appareil mobile ou selon une formule combinée. En règle générale, le trafic du réseau de votre application peut traverser les réseaux publics et privés et votre application peut utiliser plusieurs technologies de stockage tels que les Tables de stockage Microsoft Azure, les objets BLOB, les files d’attente, ou stocke les fichiers de données tooother tels que relationnelle et les bases de données de document.

toomanage de telles applications correctement vous devez surveiller de manière proactive et comprendre comment toodiagnose et résoudre les problèmes de tous les aspects de ces derniers, leurs technologies connexes. En tant qu’utilisateur des services de stockage Azure, vous devez en permanence surveiller les services de stockage hello votre application utilise des modifications inattendues de comportement (par exemple, la plus lente que le temps de réponse habituel) et utiliser toocollect de journalisation plus détaillées des données et tooanalyze un problème de profondeur. vous obtenez à partir de la surveillance et la journalisation des informations de diagnostic Hello aidera à vous toodetermine hello cause première de hello émettre votre application a rencontré. Vous pouvez résoudre les problème de hello et déterminer les étapes appropriées à hello suivre tooremediate il. Le stockage Azure est un service Azure et constitue une partie importante de la plupart de hello des solutions aux clients de déployer toohello infrastructure Azure. Le stockage Azure inclut des fonctionnalités d’analyse toosimplify, diagnostiquer et résoudre les problèmes de stockage dans vos applications basées sur le cloud.

> [!NOTE]
> Hello stockage Azure ne prend pas en charge la journalisation pour l’instant.
> 

Pour un guide pratique tooend bout en bout résolution des problèmes dans les applications de stockage Azure, consultez [dépannage à l’aide d’Azure Storage Metrics et journalisation, AzCopy et l’Analyseur de Message de bout en bout](../storage-e2e-troubleshooting.md).

* [Introduction]
  * [Organisation de ce guide]
* [votre service de stockage de surveillance]
  * [Analyse de l’état d’intégrité du service]
  * [Analyse de la capacité]
  * [Analyse de la disponibilité]
  * [Analyse des performances]
* [diagnostiquer les problèmes de stockage]
  * [Problèmes d’état d’intégrité du service]
  * [Problèmes de performances]
  * [Erreurs de diagnostic]
  * [Problèmes d’émulateur de stockage]
  * [Outils de journalisation du stockage]
  * [Utilisation des outils de journalisation réseau]
* [le suivi de bout en bout]
  * [Corrélation des données de journalisation]
  * [ID de la demande client]
  * [ID demande serveur]
  * [Horodatages]
* [conseils de dépannage]
  * [mesures affichent AverageE2ELatency haute et basse AverageServerLatency]
  * [Affichent les métriques AverageE2ELatency basse et AverageServerLatency basse mais hello client rencontre une latence élevée]
  * [Les métriques indiquent une valeur AverageServerLatency élevée]
  * [Vous constatez des retards inattendus dans la livraison des messages d’une file d’attente]
  * [métriques indiquent une augmentation dans PercentThrottlingError]
  * [métriques indiquent une augmentation dans PercentTimeoutError]
  * [Les métriques indiquent une augmentation de la valeur PercentNetworkError]
  * [Hello client reçoit les messages HTTP 403 (interdit)]
  * [Hello client reçoit les messages HTTP 404 (introuvable)]
  * [Hello client reçoit les messages HTTP 409 (conflit)]
  * [PercentSuccess basse affichent les métriques ou les entrées de journal analytique ont des opérations avec état de la transaction de ClientOtherErrors]
  * [Les métriques de capacité indiquent une augmentation inattendue de l’utilisation de la capacité de stockage]
  * [Vous constatez des redémarrages inattendus des machines virtuelles associées à un grand nombre de disques durs virtuels]
  * [Votre problème survient à l’aide de l’émulateur de stockage hello pour le développement ou de test]
  * [Vous rencontrez des problèmes d’installation Bonjour Azure SDK pour .NET]
  * [Vous rencontrez un autre problème avec un service de stockage]
  * [Résolution des problèmes de stockage de fichiers Azure dans Windows](../files/storage-troubleshoot-windows-file-connection-problems.md)   
  * [Résolution des problèmes de stockage de fichiers Azure dans Linux](../files/storage-troubleshoot-linux-file-connection-problems.md)
* [annexes]
  * [annexe 1 : à l’aide du trafic HTTP et HTTPS du toocapture Fiddler]
  * [annexe 2 : à l’aide d’un trafic réseau Wireshark toocapture]
  * [annexe 3 : à l’aide de trafic de réseau Microsoft Message Analyzer toocapture]
  * [Annexe 4 : À l’aide de données de journaux et de métriques tooview Excel]
  * [Annexe 5 : analyse avec Application Insights pour Visual Studio Team Services]

## <a name="introduction"></a>Introduction
Problèmes de ce indique guide vous comment toouse des fonctionnalités telles qu’Analytique de stockage Azure, de journalisation côté client de hello bibliothèque cliente de stockage Azure et autres tooidentify des outils tiers, diagnostiquez et résoudre les problèmes de stockage Azure.

![][1]

Ce guide est prévu toobe lecture principalement par les développeurs de services en ligne qui utilisent des Services de stockage Azure et les professionnels de l’informatique chargés de gérer ces services en ligne. Ce guide vise Hello est :

* toohelp vous conservez le contrôle d’intégrité hello et les performances de vos comptes de stockage Azure.
* tooprovide des processus nécessaires de hello et toohelp outils vous décidez si un problème dans une application ou un problème est lié tooAzure stockage.
* tooprovide vous avec des instructions pour résoudre les problèmes liés à tooAzure stockage.

### <a name="how-this-guide-is-organized"></a>Organisation de ce guide
Hello la section «[votre service de stockage de surveillance]» décrit comment toomonitor hello intégrité et les performances de vos services de stockage Azure à l’aide d’Azure Storage Analytique Metrics (Storage Metrics).

Hello la section «[diagnostiquer les problèmes de stockage]» décrit comment toodiagnose problèmes à l’aide d’Azure Storage Analytique Logging (Storage Logging). Il décrit également comment tooenable à l’aide de journalisation côté client hello des fonctionnalités de l’une des bibliothèques clientes de hello telles que hello bibliothèque cliente de stockage pour .NET ou d’un hello SDK Azure pour Java.

Hello la section «[le suivi de bout en bout]» décrit comment vous pouvez mettre en corrélation les informations hello contenues dans les différents fichiers journaux et les données de métriques.

Hello la section «[conseils de dépannage]» fournit des conseils de dépannage pour les hello problèmes liés au stockage courants que vous pouvez rencontrer.

Hello »[annexes]» incluent des informations sur l’utilisation d’autres outils tels que Wireshark et Netmon pour l’analyse de réseau des données du paquet, Fiddler pour analyser les messages HTTP/HTTPS, et Microsoft Message Analyzer pour mettre en corrélation les données du journal.

## <a name="monitoring-your-storage-service"></a>Analyse de votre service de stockage
Si vous connaissez les outils d’analyse de performances Windows, vous pouvez considérer les métriques de stockage comme l’équivalent, dans Azure Storage, des compteurs de l’Analyseur de performances Windows. Dans les mesures de stockage, vous trouverez un ensemble complet de métriques (compteurs dans la terminologie de l’Analyseur de performances Windows), telles que la disponibilité du service, le nombre total de demandes tooservice, ou le pourcentage de demandes réussies tooservice. Pour obtenir une liste complète des métriques disponibles de hello, consultez [schéma de Table de métriques Storage Analytique](http://msdn.microsoft.com/library/azure/hh343264.aspx). Vous pouvez spécifier si vous souhaitez toocollect de service de stockage hello et des mesures agrégées toutes les heures ou toutes les minutes. Pour plus d’informations sur les métriques de tooenable et analyse vos comptes de stockage, voir [l’activation des métriques de stockage et l’affichage des données de métriques](http://go.microsoft.com/fwlink/?LinkId=510865).

Vous pouvez choisir les métriques toutes les heures souhaitées toodisplay Bonjour [portail Azure](https://portal.azure.com) et configurer des règles pour avertir les administrateurs par courrier électronique chaque fois qu’une mesure horaire dépasse un seuil spécifique. Pour plus d’informations, consultez [Réception de notifications d’alerte](/azure/monitoring-and-diagnostics/monitoring-overview-alerts.md). 

service de stockage Hello collecte les mesures à l’aide de son mieux, mais ne peut pas enregistrer chaque opération de stockage.

Bonjour portail Azure, vous pouvez afficher les métriques, telles que la disponibilité, nombre total de demandes et les numéros de latence moyenne pour un compte de stockage. Une règle de notification a également été configurée tooalert administrateur si disponibilité tombe sous un certain niveau. À partir de l’affichage de ces données, une zone possible pour un examen est le pourcentage de réussite de service table hello est inférieure à 100 % (pour plus d’informations, consultez la section de hello »[PercentSuccess basse affichent les métriques ou les entrées de journal analytique ont des opérations avec état de la transaction de ClientOtherErrors]»).

Vous devez surveiller en continu votre tooensure d’applications Azure qu’ils sont sains et performant que celui attendu par :

* L’établissement des métriques de ligne de base de l’application qui sera vous toocompare les données actuelles et identifier les modifications importantes de comportement hello du stockage Azure et votre application. les valeurs Hello vos métriques de ligne de base sera, dans de nombreux cas, spécifiques à l’application et vous devez les définir lorsque vous testez les performances de votre application.
* L’enregistrement des métriques par minute et leur utilisation toomonitor activement pour des erreurs inattendues et les anomalies telles que des pics du nombre d’erreurs ou des taux de demandes.
* Les métriques par heure de l’enregistrement à l’aide les valeurs moyennes de toomonitor comme moyen de nombre d’erreurs et taux de demandes.
* Examen des problèmes potentiels à l’aide des outils de diagnostic comme décrit plus loin dans la section de hello »[diagnostiquer les problèmes de stockage]. »

graphiques Hello Bonjour suivant image illustrent comment hello moyenne qui se produit pour les métriques permettre masquer des pics dans l’activité. les métriques de Hello apparaissent tooshow un taux stable de demandes, lors de la minute hello métriques révèlent fluctuations hello qui sont réellement en cours.

![][3]

Hello reste de cette section décrit les mesures que vous devez surveiller et pourquoi.

### <a name="monitoring-service-health"></a>Analyse de l’état d’intégrité du service
Vous pouvez utiliser hello [portail Azure](https://portal.azure.com) tooview hello intégrité hello stockage service (et autres services Azure) dans tous les hello régions Azure monde hello. Cela vous permet toosee immédiatement si un problème en dehors de votre contrôle affecte hello service de stockage dans la région de hello que vous utilisez pour votre application.

Hello [portail Azure](https://portal.azure.com) peut également fournir des notifications d’incidents affectant hello divers services Azure.
Remarque : Ces informations n’étaient précédemment disponibles, ainsi que des données historiques sur hello [tableau de bord de Service Azure](http://status.azure.com).

Lors de hello [portail Azure](https://portal.azure.com) collecte les informations d’intégrité à l’intérieur de hello centres de données Azure (analyse intégrale), vous pouvez également envisager d’adopter des transactions de synthèse toogenerate approche extérieur régulièrement accéder à votre application web hébergé par Azure à partir de plusieurs emplacements. Hello services proposés par [Dynatrace](http://www.dynatrace.com/en/synthetic-monitoring) et Application Insights pour Visual Studio Team Services sont des exemples de cette approche de l’extérieur. Pour plus d’informations sur Application Insights pour Visual Studio Team Services, consultez l’annexe de hello »[annexe 5 : surveiller avec Application Insights pour Visual Studio Team Services](#appendix-5). »

### <a name="monitoring-capacity"></a>Analyse de la capacité
Métriques de stockage stocke uniquement les métriques de capacité pour le service d’objets blob hello parce que BLOB généralement proportion de plus grande hello des données stockées (au moment de hello d’écriture, il n’est pas possible toouse Storage Metrics toomonitor hello capacité vos tables et les files d’attente) . Vous pouvez trouver ces données Bonjour **$MetricsCapacityBlob** table si vous avez activé l’analyse pour hello service Blob. Storage Metrics enregistre les données une fois par jour, et vous pouvez utiliser la valeur hello hello **RowKey** toodetermine indique si les lignes hello contient une entité qui lie les données toouser (valeur **données**) ou (de données analytique valeur **analytique**). Chaque entité stockée contient des informations sur la quantité de hello de stockage utilisé (**capacité** mesurée en octets) et le nombre actuel de hello de conteneurs (**ContainerCount**) et les objets BLOB ( **ObjectCount**) en cours d’utilisation dans le compte de stockage hello. Pour plus d’informations sur les métriques de capacité hello stockées Bonjour **$MetricsCapacityBlob** de table, consultez [schéma de Table de métriques Storage Analytique](http://msdn.microsoft.com/library/azure/hh343264.aspx).

> [!NOTE]
> Vous devez surveiller ces valeurs pour un avertissement que vous vous rapprochez des limites de capacité hello de votre compte de stockage. Bonjour portail Azure, vous pouvez ajouter toonotify de règles d’alerte si l’utilisation du stockage d’agrégation dépasse ou tombe en dessous des seuils que vous spécifiez.
> 
> 

Pour l’estimation de taille hello des différents objets de stockage tels que les objets BLOB, consultez hello blog post [présentation stockage de la facturation Azure – bande passante, Transactions et capacité](http://blogs.msdn.com/b/windowsazurestorage/archive/2010/07/09/understanding-windows-azure-storage-billing-bandwidth-transactions-and-capacity.aspx).

### <a name="monitoring-availability"></a>Analyse de la disponibilité
Vous devez surveiller la disponibilité hello hello de services de stockage dans votre compte de stockage en surveillant la valeur hello Bonjour **disponibilité** colonne hello tables de métriques par heure ou minute : **$ MetricsHourPrimaryTransactionsBlob**, **$MetricsHourPrimaryTransactionsTable**, **$MetricsHourPrimaryTransactionsQueue**, **$ MetricsMinutePrimaryTransactionsBlob**, **$MetricsMinutePrimaryTransactionsTable**, **$MetricsMinutePrimaryTransactionsQueue**, **$ MetricsCapacityBlob**. Hello **disponibilité** colonne contient une valeur de pourcentage qui indique la disponibilité hello hello service d’ou opération hello API représenté par hello ligne (hello **RowKey** indique si les lignes hello contient métriques pour service hello dans son ensemble ou pour une opération d’API spécifique).

Toute valeur inférieure à 100 % indique que certaines demandes de stockage échouent. Vous pouvez voir pourquoi elles échouent en examinant hello des autres colonnes de données de métriques hello qui affichent les hello un nombre de demandes avec différents types d’erreur tel que **ServerTimeoutError**. Vous devriez toosee **disponibilité** automne temporairement inférieure à 100 % pour des raisons telles que des délais d’attente du serveur temporaire pendant que le service de hello déplace les partitions toobetter équilibrer la charge demande ; hello logique dans votre application cliente de nouvelle tentative doit gérer ces conditions transitoires. article de Hello [les Messages d’état et les opérations de journalisation de stockage Analytique](http://msdn.microsoft.com/library/azure/hh343260.aspx) listes hello des types de transactions qui inclut des métriques de stockage dans son **disponibilité** calcul.

Bonjour [portail Azure](https://portal.azure.com), vous pouvez ajouter des règles d’alerte toonotify vous si **disponibilité** pour un service tombe en dessous d’un seuil que vous spécifiez.

Hello »[conseils de dépannage]» dans ce guide décrit certaines système stockage service problèmes connexes tooavailability courantes.

### <a name="monitoring-performance"></a>Analyse des performances
performances de hello toomonitor hello de services de stockage, vous pouvez utiliser hello suivant des métriques à partir de hello toutes les heures et minutes des tables de métriques.

* Hello valeurs Bonjour **AverageE2ELatency** et **AverageServerLatency** colonnes indiquent le service de stockage hello hello temps moyen ou le type d’opération API prend tooprocess demandes. **AverageE2ELatency** est une mesure de la latence de bout en bout qui inclut la durée hello de la demande de hello tooread et envoyer une réponse de hello dans la demande hello tooprocess Ajout toohello temps nécessaire (par conséquent inclut latence du réseau une fois la demande de hello atteint de service de stockage hello) ; **AverageServerLatency** est une mesure du temps de traitement simplement hello et par conséquent exclut toute latence du réseau associé toocommunicating avec le client de hello. Consultez la section de hello »[mesures affichent AverageE2ELatency haute et basse AverageServerLatency]» plus loin dans ce guide pour une présentation de la raison pour laquelle il peut y avoir une différence significative entre ces deux valeurs.
* Hello valeurs Bonjour **TotalIngress** et **TotalEgress** colonnes indiquent la quantité totale de hello de données, en octets, à venir de tooand passe hors de votre service de stockage ou à un type d’opération API spécifique.
* Hello valeurs Bonjour **TotalRequests** colonne Afficher hello nombre de demandes de service de stockage de l’opération de l’API de hello reçoit. **TotalRequests** hello le nombre total de demandes de service de stockage hello reçoit.

Toute modification inattendue de ces valeurs est généralement l’indicateur d’un problème qui doit faire l’objet d’une enquête.

Bonjour [portail Azure](https://portal.azure.com), vous pouvez ajouter des règles d’alerte toonotify vous si une des mesures de performances hello pour ce service passent en dessous ou dépassez un seuil que vous spécifiez.

Hello »[conseils de dépannage]» dans ce guide décrit certaines système stockage service problèmes connexes tooperformance courantes.

## <a name="diagnosing-storage-issues"></a>Diagnostic des problèmes de stockage
Il existe différentes façons de savoir si votre application a rencontré un problème, dont :

* Une défaillance majeure qui provoque le fonctionnement de toocrash ou toostop l’application hello.
* Des modifications significatives à partir des valeurs de ligne de base de métriques hello vous analysez comme décrit dans la section précédente de hello »[votre service de stockage de surveillance]. »
* Rapports des utilisateurs de votre application indiquant qu'une certaine opération ne s'est pas effectuée comme prévu ou qu'une fonctionnalité est défectueuse.
* Erreurs générées au sein de votre application et affichées dans les fichiers journaux ou via d'autres méthodes de notification.

En règle générale, les services de stockage de problèmes connexes tooAzure se répartissent dans quatre grandes catégories :

* Votre application rencontre un problème de performances, signalées par vos utilisateurs, ou révélées par les modifications des métriques de performances hello.
* Il existe un problème avec l’infrastructure de stockage Azure hello dans une ou plusieurs régions.
* Votre application rencontre une erreur, signalées par vos utilisateurs, ou révélées par une augmentation de l’une des mesures de comptage erreur hello analysées.
* Au cours de développement et de test, vous pouvez utiliser l’émulateur de stockage local hello ; Vous pouvez rencontrer certains problèmes qui se rapportent spécifiquement toousage de l’émulateur de stockage hello.

Hello sections suivantes décrivent les étapes hello doit suivre toodiagnose et résoudre les problèmes dans chacun de ces quatre catégories. Hello la section «[conseils de dépannage]» plus loin dans ce guide fournit plus de détails pour certains problèmes courants que vous pouvez rencontrer.

### <a name="service-health-issues"></a>Problèmes d’état d’intégrité du service
Les problèmes d’état du service sont généralement des problèmes sur lesquels vous n’avez pas de contrôle. Hello [portail Azure](https://portal.azure.com) fournit des informations sur les problèmes en cours avec les services Azure, y compris les services de stockage. Si vous avez opté pour le stockage géo-redondant avec accès en lecture lorsque vous avez créé votre compte de stockage, puis dans l’événement hello de vos données n’est pas disponible dans l’emplacement principal de hello, votre application peut basculer temporairement copie en lecture seule de toohello dans l’emplacement secondaire de hello. toodo, votre application doit être en mesure de tooswitch entre l’utilisation des emplacements de stockage principal et secondaire hello et être en mesure de toowork dans un mode de fonctionnalité réduite avec des données en lecture seule. bibliothèques de Client de stockage Azure Hello autorisent toodefine une stratégie de nouvelle tentative qui permettre lire à partir du stockage secondaire en cas d’échec d’une lecture à partir du stockage principal. Votre application doit également toobe savoir que les données hello dans l’emplacement secondaire de hello soient finalement cohérentes. Pour plus d’informations, voir blog de hello [Options de redondance de stockage Azure et Read Access Geo Redundant Storage](https://blogs.msdn.microsoft.com/windowsazurestorage/2013/12/11/windows-azure-storage-redundancy-options-and-read-access-geo-redundant-storage/).

### <a name="performance-issues"></a>Problèmes de performances
performances Hello d’une application peuvent être subjective, en particulier à partir d’une perspective de l’utilisateur. Par conséquent, il est important toohave toohelp de ligne de base des métriques disponibles vous identifiez où il existe un problème de performances. De nombreux facteurs peuvent affecter les performances de hello d’un service de stockage Azure à partir de la perspective d’application client hello. Ces facteurs peuvent avoir lieu dans le service de stockage hello, dans le client de hello ou dans l’infrastructure de réseau hello ; Par conséquent, il est important toohave une stratégie pour identifier l’origine hello du problème de performances hello.

Après avoir identifié l’emplacement probable hello de cause hello du problème de performances hello de métriques de hello, vous pouvez ensuite utiliser hello journal fichiers toofind détaillées toodiagnose d’informations et résoudre les problème hello.

Hello la section «[conseils de dépannage]» plus loin dans ce guide fournit plus d’informations sur certaines des performances courants liés les problèmes qui vous pouvez rencontrer.

### <a name="diagnosing-errors"></a>Erreurs de diagnostic
Les utilisateurs de votre application peuvent vous avertir des erreurs signalées par l’application cliente de hello. Les métriques de stockage enregistrent également les décomptes des différents types d’erreurs de vos services de stockage, tels que **NetworkError**, **ClientTimeoutError** ou **AuthorizationError**. Les métriques de stockage enregistrent uniquement les décomptes des différents types d'erreurs, mais vous pouvez obtenir des informations plus détaillées concernant les demandes individuelles en examinant les journaux côté serveur, côté client et réseau. En règle générale, code d’état HTTP hello retourné par le service de stockage hello donnent une indication de l’échec de demande de hello.

> [!NOTE]
> Souvenez-vous que vous devriez toosee certaines erreurs intermittentes : par exemple, les erreurs en raison de conditions de réseau tootransient, ou les erreurs d’application.
> 
> 

Hello ressources suivantes sont utiles pour comprendre les codes d’état et d’erreur liés au stockage :

* [Codes d'erreur API REST communs](http://msdn.microsoft.com/library/azure/dd179357.aspx)
* [Codes d’erreur de service BLOB](http://msdn.microsoft.com/library/azure/dd179439.aspx)
* [Codes d’erreur de service de File d’attente](http://msdn.microsoft.com/library/azure/dd179446.aspx)
* [Codes d'erreur de service de table](http://msdn.microsoft.com/library/azure/dd179438.aspx)
* [Codes d’erreur de service de fichier](https://msdn.microsoft.com/library/azure/dn690119.aspx)

### <a name="storage-emulator-issues"></a>Problèmes liés à l’émulateur de stockage
Bonjour Azure SDK comprend un émulateur de stockage que vous pouvez exécuter sur une station de travail de développement. Cet émulateur simule la majeure partie du comportement hello de services de stockage Azure hello et est utile lors du développement et de test, ce qui vous toorun les applications qui utilisent les services de stockage Azure sans hello ont besoin pour un abonnement Azure et un compte de stockage Azure.

Hello »[conseils de dépannage]» dans ce guide décrit certains problèmes courants rencontrés à l’aide de l’émulateur de stockage hello.

### <a name="storage-logging-tools"></a>Outils de journalisation du stockage
La journalisation du stockage permet de journaliser côté serveur les demandes de stockage dans votre compte de stockage Azure. Pour plus d’informations sur la journalisation du côté serveur tooenable et hello d’accès aux données du journal, consultez [l’activation de la journalisation du stockage et l’accès aux données du journal](http://go.microsoft.com/fwlink/?LinkId=510867).

Hello bibliothèque cliente de stockage pour .NET vous permet de toocollect les données de journal côté client qui associe les opérations toostorage effectuées par votre application. Pour plus d’informations, consultez [journalisation avec hello bibliothèque cliente de stockage .NET côté Client](http://go.microsoft.com/fwlink/?LinkId=510868).

> [!NOTE]
> Dans certains cas (par exemple, les échecs d’autorisation SAP), un utilisateur peut signaler une erreur pour laquelle vous ne pouvez trouver aucune donnée de requête dans hello journaux de stockage côté serveur. Vous pouvez utiliser des fonctionnalités de journalisation hello de hello bibliothèque cliente de stockage tooinvestigate si hello hello provient du fait de client de hello ou réseau de hello tooinvestigate outils d’analyse de réseau.
> 
> 

### <a name="using-network-logging-tools"></a>Utilisation des outils de journalisation réseau
Vous pouvez capturer le trafic de hello entre hello client et serveur tooprovide détaillée des informations sur hello données hello client et serveur sont l’échange et hello sous-jacent des conditions du réseau. Parmi les outils de journalisation réseau utiles, on retrouve :

* [Fiddler](http://www.telerik.com/fiddler) est un proxy qui vous permet d’en-têtes de hello tooexamine et les données de charge utile des messages de demande et de réponse HTTP et HTTPS de débogage gratuitement sur Internet. Pour plus d’informations, consultez [annexe 1 : trafic HTTP et HTTPS à l’aide de Fiddler toocapture](#appendix-1).
* [Microsoft Network Monitor (Netmon)](http://www.microsoft.com/download/details.aspx?id=4865) et [Wireshark](http://www.wireshark.org/) est des analyseurs de protocole qui vous permettent de tooview réseau libre paquet des informations détaillées sur un large éventail de protocoles réseau. Pour plus d’informations sur Wireshark, consultez «[annexe 2 : le trafic de réseau à l’aide de Wireshark toocapture](#appendix-2)».
* Microsoft Message Analyzer est un outil de Microsoft qui remplace Netmon et qui, en outre, toocapturing réseau données du paquet, vous aide à tooview et analyser les données de journal hello capturées à partir d’autres outils. Pour plus d’informations, consultez «[annexe 3 : le trafic de réseau à l’aide de l’Analyseur de Message Microsoft toocapture](#appendix-3)».
* Si vous voulez tooperform un toocheck de test de connectivité de base que votre ordinateur client peut se connecter service de stockage Azure toohello réseau hello, cela est impossible à l’aide de la norme de hello **ping** outil sur le client de hello. Toutefois, vous pouvez utiliser hello [ **tcping** outil](http://www.elifulkerson.com/projects/tcping.php) toocheck connectivité.

Dans de nombreux cas, les données de journal hello de Storage Logging et hello bibliothèque cliente de stockage seront suffisante toodiagnose un problème, mais dans certains scénarios, vous devrez peut-être hello plus d’informations sur ces outils de journalisation de réseau pouvant fournir. Par exemple, permet de messages HTTP et HTTPS tooview en-tête et la charge utile de données envoyées tooand hello à partir de services de stockage, ce qui vous permettrait tooexamine comment une application cliente à l’aide de Fiddler tooview retente les opérations de stockage. Les analyseurs de protocole tels que Wireshark fonctionnent au niveau de paquets hello l’activation de données TCP tooview, ce qui permettraient tootroubleshoot perdu de paquets et les problèmes de connectivité. L’analyseur de message est capable de fonctionner au niveau des couches HTTP et TCP.

## <a name="end-to-end-tracing"></a>Suivi de bout en bout
Le suivi de bout en bout basé sur plusieurs fichiers journaux est une technique utile pour l’identification des problèmes potentiels. Vous pouvez utiliser les informations de date/heure hello à partir de vos données métriques comme une indication d’où toostart recherche dans les fichiers journaux hello hello détaillées des informations qui vous aideront à résoudre les problème de hello.

### <a name="correlating-log-data"></a>Corrélation des données de journalisation
Lorsque vous affichez les journaux des applications clientes, les traces de réseau et stockage côté serveur enregistrement est critique toobe toocorrelate en mesure de demandes sur hello différents fichiers journaux. les fichiers journaux Hello incluent un nombre de champs différents qui sont utiles en tant qu’identificateurs de corrélation. id de demande client Hello est hello plus utiles toouse toocorrelate entrées de champ dans différents journaux de hello. Toutefois dans certains cas, il peut être utile toouse id de demande de serveur hello ou les horodatages. Hello sections suivantes fournissent plus de détails sur ces options.

### <a name="client-request-id"></a>ID de la demande client
Bibliothèque cliente de stockage de Hello génère automatiquement un id de demande client unique pour chaque demande.

* Bonjour journal côté client qui hello bibliothèque cliente de stockage crée, id de demande client hello s’affiche dans hello **ID de demande Client** champ de chaque entrée de journal relative toohello demande.
* Dans une trace réseau tel que celui capturé par Fiddler, id de demande client hello est visible dans les messages de demande comme hello **x-ms-client-request-id** valeur d’en-tête HTTP.
* Dans le journal de Storage Logging hello côté serveur, l’id de demande client hello s’affiche dans la colonne d’ID de demande Client hello.

> [!NOTE]
> Il est possible pour plusieurs demandes tooshare hello même id de demande client, car le client de hello permettre affecter cette valeur (bien que la bibliothèque cliente de stockage de hello assigne une nouvelle valeur automatiquement). Dans les cas de hello de nouvelles tentatives à partir du client de hello, toutes les tentatives de partagent hello même id de demande client. Dans les cas de hello d’un lot envoyé à partir du client de hello, lot de hello a un id de demande client unique.
> 
> 

### <a name="server-request-id"></a>ID de la demande serveur
service de stockage Hello génère automatiquement un ID de demande de serveur.

* Dans le journal de Storage Logging hello côté serveur, id de demande de serveur hello apparaît hello **en-tête d’ID de demande** colonne.
* Dans une trace réseau tel que celui capturé par Fiddler, id de demande de serveur hello apparaît dans les messages de réponse comme hello **x-ms-request-id** valeur d’en-tête HTTP.
* Bonjour journal côté client qui hello bibliothèque cliente de stockage crée, id de demande de serveur hello s’affiche dans hello **opération texte** colonne d’entrée du journal hello présentant les détails de la réponse du serveur hello.

> [!NOTE]
> service de stockage Hello toujours attribue à un serveur unique demande id tooevery demande qu’il reçoit, par conséquent, chaque nouvelle tentative à partir du client de hello et chaque opération inclus dans un lot a un id de demande de serveur unique.
> 
> 

Si hello bibliothèque cliente de stockage lève une **StorageException** dans le client de hello, hello **RequestInformation** propriété contient un **RequestResult** objet qui inclut un **%%ServiceRequestID%%** propriété. Vous pouvez également accéder à un objet **RequestResult** à partir d’une instance **OperationContext**.

Hello, exemple de code ci-dessous montre comment tooset personnalisé **ClientRequestId** valeur en attachant une **OperationContext** service de stockage toohello hello demande de l’objet. Il montre également comment tooretrieve hello **ServerRequestId** valeur à partir du message de réponse hello.

```csharp
//Parse hello connection string for hello storage account.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Create an Operation Context that includes custom ClientRequestId string based on constants defined within hello application along with a Guid.
OperationContext oc = new OperationContext();
oc.ClientRequestID = String.Format("{0} {1} {2} {3}", HOSTNAME, APPNAME, USERID, Guid.NewGuid().ToString());

try
{
    CloudBlobContainer container = blobClient.GetContainerReference("democontainer");
    ICloudBlob blob = container.GetBlobReferenceFromServer("testImage.jpg", null, null, oc);  
    var downloadToPath = string.Format("./{0}", blob.Name);
    using (var fs = File.OpenWrite(downloadToPath))
    {
        blob.DownloadToStream(fs, null, null, oc);
        Console.WriteLine("\t Blob downloaded toofile: {0}", downloadToPath);
    }
}
catch (StorageException storageException)
{
    Console.WriteLine("Storage exception {0} occurred", storageException.Message);
    // Multiple results may exist due tooclient side retry logic - each retried operation will have a unique ServiceRequestId
    foreach (var result in oc.RequestResults)
    {
            Console.WriteLine("HttpStatus: {0}, ServiceRequestId {1}", result.HttpStatusCode, result.ServiceRequestID);
    }
}
```

### <a name="timestamps"></a>Horodatages
Vous pouvez également utiliser les horodatages toolocate liées des entrées de journal, mais soyez prudent de n’importe quel horloge maximal autorisé entre le client de hello et le serveur qui peut-être exister. Vous devez rechercher plus ou moins de 15 minutes pour les entrées de côté serveur en fonction de l’horodatage hello sur le client de hello correspondantes. N’oubliez pas que hello blob les métadonnées pour les objets BLOB de hello contenant des mesures indiquent la plage de temps hello pour les métriques hello stockées dans l’objet blob de hello ; Cela est utile si vous avez de nombreux objets BLOB de métriques pour hello même heures ou minutes.

## <a name="troubleshooting-guidance"></a>Instructions pour la résolution des problèmes
Cette section vous aidera à faire de diagnostic hello et résolution des problèmes de certains des problèmes courants de hello votre application peuvent rencontrer lors de l’utilisation des services de stockage Azure hello. Utiliser la liste hello ci-dessous un problème spécifique de toolocate hello informations tooyour pertinentes.

**Arbre de décision pour la résolution des problèmes**

---
Le problème rapport toohello les performances de l’un des services de stockage hello ?

* [mesures affichent AverageE2ELatency haute et basse AverageServerLatency]
* [Affichent les métriques AverageE2ELatency basse et AverageServerLatency basse mais hello client rencontre une latence élevée]
* [Les métriques indiquent une valeur AverageServerLatency élevée]
* [Vous constatez des retards inattendus dans la livraison des messages d’une file d’attente]

---
Le problème rapport Disponibilité toohello de l’un des services de stockage hello ?

* [métriques indiquent une augmentation dans PercentThrottlingError]
* [métriques indiquent une augmentation dans PercentTimeoutError]
* [Les métriques indiquent une augmentation de la valeur PercentNetworkError]

---
 Votre application client reçoit-elle une réponse HTTP 4XX (telle que 404) d’un service de stockage ?

* [Hello client reçoit les messages HTTP 403 (interdit)]
* [Hello client reçoit les messages HTTP 404 (introuvable)]
* [Hello client reçoit les messages HTTP 409 (conflit)]

---
[PercentSuccess basse affichent les métriques ou les entrées de journal analytique ont des opérations avec état de la transaction de ClientOtherErrors]

---
[Les métriques de capacité indiquent une augmentation inattendue de l’utilisation de la capacité de stockage]

---
[Vous constatez des redémarrages inattendus des machines virtuelles associées à un grand nombre de disques durs virtuels]

---
[Votre problème survient à l’aide de l’émulateur de stockage hello pour le développement ou de test]

---
[Vous rencontrez des problèmes d’installation Bonjour Azure SDK pour .NET]

---
[Vous rencontrez un autre problème avec un service de stockage]

---
### <a name="metrics-show-high-AverageE2ELatency-and-low-AverageServerLatency"></a>Les métriques indiquent une valeur AverageE2ELatency élevée et une valeur AverageServerLatency faible
Hello l’illustration ci-dessous à partir de hello [portail Azure](https://portal.azure.com) outil d’analyse montre un exemple où hello **AverageE2ELatency** est beaucoup plus importante que hello **AverageServerLatency**.

![][4]

Notez que service de stockage hello ne calcule des mesures de hello **AverageE2ELatency** pour des demandes réussies et, contrairement aux **AverageServerLatency**, inclut hello temps client de hello toosend hello données et recevoir l’accusé de réception à partir du service de stockage hello. Par conséquent, une différence entre **AverageE2ELatency** et **AverageServerLatency** est peut-être en raison de l’application toohello client en cours lents toorespond ou échéance tooconditions sur le réseau de hello.

> [!NOTE]
> Vous pouvez également afficher **E2ELatency** et **ServerLatency** les données du journal pour les opérations de stockage individuel Bonjour Storage Logging.
> 
> 

#### <a name="investigating-client-performance-issues"></a>Enquête sur les problèmes de performances client
Les raisons possibles pour le client hello répond lentement sont ayant un nombre limité de connexions disponibles ou les threads ou faible sur les ressources, telles que la bande passante processeur, mémoire ou le réseau. Vous pouvez être problème de hello en mesure de tooresolve en modifiant toobe de code hello client plus efficace (par exemple en utilisant le service de stockage de toohello appels asynchrones) ou à l’aide d’une Machine virtuelle supérieure (avec davantage de cœurs et de la mémoire).

Pour les services de table et de la file d’attente hello, algorithme de Nagle hello peut également provoquer haute **AverageE2ELatency** rapport trop**AverageServerLatency**: pour plus d’informations consultez hello [de Nagle Algorithme n’est pas convivial aux petites requêtes](http://blogs.msdn.com/b/windowsazurestorage/archive/2010/06/25/nagle-s-algorithm-is-not-friendly-towards-small-requests.aspx). Vous pouvez désactiver l’algorithme Nagle de hello dans le code à l’aide de hello **ServicePointManager** classe Bonjour **System.Net** espace de noms. Vous devez le faire avant de vous rendre n’importe quelle table de toohello appelle ou les services de file d’attente dans votre application, car cela n’affecte pas les connexions qui sont déjà ouverts. Hello exemple suivant provient de hello **Application_Start** méthode dans un rôle de travail.

```csharp
var storageAccount = CloudStorageAccount.Parse(connStr);
ServicePoint tableServicePoint = ServicePointManager.FindServicePoint(storageAccount.TableEndpoint);
tableServicePoint.UseNagleAlgorithm = false;
ServicePoint queueServicePoint = ServicePointManager.FindServicePoint(storageAccount.QueueEndpoint);
queueServicePoint.UseNagleAlgorithm = false;
```

Vous devez vérifier hello côté client journaux toosee combien votre application cliente soumet des demandes et .NET générales liées à des goulots d’étranglement de performances dans votre client telles que le processeur, le garbage collection .NET, l’utilisation du réseau ou mémoire. La première étape pour la résolution des problèmes des applications clientes .NET consiste à consulter la section [Débogage, suivi et profilage](http://msdn.microsoft.com/library/7fe0dd2y).

#### <a name="investigating-network-latency-issues"></a>Enquête sur les problèmes de latence du réseau
Latence de bout en bout élevée hello réseau à l’origine est généralement en raison de conditions de tootransient. Vous pouvez enquêter sur les problèmes de réseau provisoires et permanents (par ex., les paquets perdus) à l'aide d'outils tels que Wireshark ou l'analyseur de message Microsoft.

Pour plus d’informations sur l’utilisation des problèmes de réseau tootroubleshoot Wireshark, consultez «[annexe 2 : à l’aide d’un trafic réseau Wireshark toocapture]. »

Pour plus d’informations sur l’utilisation des problèmes de réseau Microsoft Message Analyzer tootroubleshoot, consultez «[annexe 3 : à l’aide de trafic de réseau Microsoft Message Analyzer toocapture]. »

### <a name="metrics-show-low-AverageE2ELatency-and-low-AverageServerLatency"></a>Affichent les métriques AverageE2ELatency basse et AverageServerLatency basse mais hello client rencontre une latence élevée
Dans ce scénario, la cause la plus probable hello est un retard dans les demandes de stockage hello atteindre le service de stockage hello. Vous devez examiner la raison pour laquelle les requêtes hello client ne sont pas rendant via le service d’objets blob toohello.

Pour retarder l’envoi de demandes de client de hello fait qu’il n’y a un nombre limité de connexions disponibles ou les threads.

Vous devez également vérifier si les client hello exécute après plusieurs tentatives et étudier la raison de hello hello cas. toodetermine si hello client effectue plusieurs tentatives, vous pouvez :

* Examinez les journaux de stockage Analytique hello. Si plusieurs tentatives sont produisent, vous verrez plusieurs opérations avec hello même ID de demande client, mais avec un autre serveur ID de demande.
* Examinez les journaux du client hello. Les nouvelles tentatives apparaissent dans la journalisation documentée.
* Déboguer votre code et vérifiez les propriétés de hello Hello **OperationContext** objet associé à la demande de hello. Si l’opération de hello a tenté d’exécuter, hello **RequestResults** inclut plusieurs demande de serveur unique ID de propriété. Vous pouvez également vérifier le début de hello et mettre fin à la fois pour chaque demande. Pour plus d’informations, voir l’exemple de code hello dans la section de hello [ID demande serveur].

S’il n’y a aucun problème dans le client de hello, vous devez examiner les problèmes potentiels de réseau telles qu’une perte de paquets. Vous pouvez utiliser des outils tels que des problèmes de réseau tooinvestigate Wireshark ou Microsoft Message Analyzer.

Pour plus d’informations sur l’utilisation des problèmes de réseau tootroubleshoot Wireshark, consultez «[annexe 2 : à l’aide d’un trafic réseau Wireshark toocapture]. »

Pour plus d’informations sur l’utilisation des problèmes de réseau Microsoft Message Analyzer tootroubleshoot, consultez «[annexe 3 : à l’aide de trafic de réseau Microsoft Message Analyzer toocapture]. »

### <a name="metrics-show-high-AverageServerLatency"></a>Les métriques indiquent une valeur AverageServerLatency élevée
Dans les cas de hello élevée **AverageServerLatency** pour les demandes de téléchargement d’objet blob, vous devez utiliser hello Storage Logging consigne toosee s’il existe des requêtes répétées pour hello même d’objets blob (ou ensemble d’objets BLOB). Demandes de téléchargement pour l’objet blob, vous devez examiner les blocs client hello de taille utilise (par exemple, moins de 64 Ko peut entraîner de frais généraux, sauf si hello lit se trouvent également dans les blocs inférieure à 64 Ko segments), et si plusieurs clients sont téléchargement bloque toohello même objet BLOB en parallèle. Vous devez également vérifier les métriques par minute de hello des pics de nombre hello de demandes entraîner le dépassement hello par seconde objectifs d’évolutivité : consultez également «[métriques indiquent une augmentation dans PercentTimeoutError]. »

Si vous voyez haute **AverageServerLatency** pour les demandes de téléchargement d’objet blob lorsqu’il sont répétés demandes hello même objet blob ou un ensemble d’objets BLOB, puis vous devez prendre en compte la mise en cache de ces objets BLOB à l’aide d’Azure Cache ou hello de diffusion de contenu Azure Network (CDN). Pour les demandes de téléchargement, vous pouvez améliorer le débit de hello à l’aide d’une plus grande taille de bloc. Pour les requêtes tootables, il est également possible tooimplement cache côté client sur les clients qui effectuent hello même des opérations de requête et où hello données ne changent pas fréquemment.

Haute **AverageServerLatency** valeurs peuvent également être un symptôme de tables mal conçus au début ou à des requêtes que les résultats dans les opérations d’analyse, ou qui suivent hello ajouter/anti-modèle. Voir la section «[métriques indiquent une augmentation dans PercentThrottlingError]» pour plus d'informations.

> [!NOTE]
> Pour obtenir une liste de contrôle exhaustive des performances, consultez [Liste de contrôle des performances et de l’extensibilité de Microsoft Azure Storage](storage-performance-checklist.md).
> 
> 

### <a name="you-are-experiencing-unexpected-delays-in-message-delivery"></a>Vous constatez des retards inattendus dans la livraison des messages d’une file d’attente
Si vous rencontrez un délai entre hello une application ajoute un message tooa file d’attente et hello le temps qu’il devient tooread disponible à partir de la file d’attente hello, puis hello suivant le problème de hello toodiagnose étapes à suivre :

* Vérifiez l’application hello est ajouté avec succès la file d’attente de toohello de messages hello. Vérifiez qu’application hello n’est pas une nouvelle tentative hello **AddMessage** méthode plusieurs fois avant de réussir. journaux de bibliothèque cliente de stockage Hello affichera les tentatives répétées d’opérations de stockage.
* Vérifiez qu’il n’existe aucune horloge maximal autorisé entre le rôle de travail hello qui ajoute la file d’attente toohello hello et rôle de travail hello qui lit le message de type hello à partir de la file d’attente de hello qui rend apparaissent comme s’il existe un décalage dans le traitement.
* Vérifiez si le rôle de travail hello qui lit des messages hello à partir de la file d’attente hello est défectueux. Si un client de file d’attente appelle hello **GetMessage** méthode échoue mais toorespond avec un accusé de réception, le message de type hello reste invisible sur la file d’attente hello jusqu'à hello **invisibilityTimeout** expiration. À ce stade, le message de type hello devient disponible pour traiter à nouveau.
* Vérifiez si la longueur de file d’attente hello augmente au fil du temps. Cela peut se produire si vous n’avez pas suffisamment tooprocess disponible travailleurs hello tous messages placement des informations sur les autres processus de travail sur la file d’attente hello. Vous devez également vérifier hello métriques toosee si le nombre de messages, ce qui peut indiquer de retrait de supprimer les requêtes échouent et hello répété message de type hello toodelete tentatives ayant échoué.
* Examinez les journaux de Storage Logging hello pour les opérations de file d’attente qui ont plus que prévu **E2ELatency** et **ServerLatency** valeurs sur une longue période de temps que d’habitude.

### <a name="metrics-show-an-increase-in-PercentThrottlingError"></a>Les métriques indiquent une augmentation de la valeur PercentThrottlingError
Erreurs de limitation se produisent quand vous dépassez les objectifs d’évolutivité hello d’un service de stockage. service de stockage Hello fait cette tooensure que sans un client ou un client peut utiliser hello service à des frais de hello d’autres personnes. Pour plus d’informations sur les cibles d’évolutivité des comptes de stockage et les cibles de performances des partitions dans les comptes de stockage, voir [Objectifs de performance et évolutivité d'Azure Storage](storage-scalability-targets.md).

Si hello **PercentThrottlingError** mesures montrent une augmentation en pourcentage hello de demandes qui ont échoué avec une erreur de limitation, vous devez tooinvestigate un des deux scénarios :

* [Augmentation provisoire de la valeur PercentThrottlingError]
* [Augmentation permanente de l’erreur PercentThrottlingError]

Une augmentation de **PercentThrottlingError** se produit souvent à hello en même temps qu’une augmentation du nombre hello de demandes de stockage, ou lorsque vous avez initialement votre application de test de charge. Cela peut également se manifester dans client hello en tant que « 503 serveur occupé » ou des messages d’état HTTP de « 500 opération Timeout » à partir d’opérations de stockage.

#### <a name="transient-increase-in-PercentThrottlingError"></a>Augmentation provisoire de la valeur PercentThrottlingError
Si vous rencontrez des pics de valeur hello **PercentThrottlingError** qui coïncident avec des périodes de forte activité de l’application hello, vous devez implémenter une (non linéaire) exponentiel et stratégie des nouvelles tentatives dans votre client : cela est de réduire la charge d’immédiate de hello sur la partition de hello et d’aide toosmooth de votre application les pics de trafic. Pour plus d’informations sur la façon dont les stratégies de nouvelle tentative tooimplement à l’aide de hello bibliothèque cliente de stockage, consultez [Microsoft.WindowsAzure.Storage.RetryPolicies Namespace](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.retrypolicies.aspx).

> [!NOTE]
> Vous pouvez également voir les pics de valeur hello **PercentThrottlingError** qui coïncident pas avec des périodes de forte activité de l’application hello : hello probable ici est le service de stockage de hello déplacement de partitions tooimprove charge l’équilibrage de la.
> 
> 

#### <a name="permanent-increase-in-PercentThrottlingError"></a>Augmentation permanente de l’erreur PercentThrottlingError
Si vous voyez une valeur élevée pour **PercentThrottlingError** suivant une augmentation permanente de vos volumes de transactions, ou lorsque vous exécutez votre charge initiale des tests sur votre application, il vous suffit de tooevaluate comment votre application est l’utilisation de partitions de stockage, et si elle est proche des objectifs d’évolutivité hello pour un compte de stockage. Par exemple, si vous rencontrez le problème de limitation sur une file d’attente (compte comme une seule partition), puis vous devez envisager d’utiliser les transactions hello toospread files d’attente supplémentaires sur plusieurs partitions. Si vous rencontrez le problème de limitation sur une table, vous devez tooconsider à l’aide d’un autre toospread de schéma de partitionnement vos transactions sur plusieurs partitions à l’aide d’une plus large gamme de valeurs de clé de partition. Une des causes courantes de ce problème sont hello ajouter/ajouter anti-modèle où vous sélectionnez la date de hello en tant que clé de partition hello et ensuite toutes les données sur un jour donné est écrit tooone partition : lors du chargement, cela peut provoquer un goulot d’étranglement de l’écriture. Vous devez envisager une conception de partitionnement différente ou évaluer s'il ne vaudrait pas mieux utiliser un stockage d'objets blob. Vous devez également vérifier si hello limitation se produit suite à des pics de votre trafic et examiner les méthodes de votre modèle de demandes de lissage.

Si vous distribuez vos transactions sur plusieurs partitions, vous devez connaître toujours des limites de l’évolutivité de hello définies pour le compte de stockage hello. Par exemple, si vous avez utilisé les files de dix attente chaque maximum hello de traitement de 2 000 messages de 1 Ko par seconde, vous serez à hello limite globale de 20 000 messages par seconde pour le compte de stockage hello. Si vous devez tooprocess plus de 20 000 entités par seconde, vous devez envisager d’utiliser plusieurs comptes de stockage. Vous devez également garder à l’esprit que taille hello de vos demandes et entités a un impact sur lorsque le service de stockage hello limite vos clients : Si vous avez supérieure des demandes et des entités, vous pouvez être limitée plus tôt.

Création de requête inefficace peut également expliquer limites d’extensibilité toohit hello pour les partitions de table. Par exemple, une requête avec un filtre qui sélectionne uniquement un pour cent des entités de hello dans une partition mais qui analyse toutes les entités hello dans une partition devez tooaccess chaque entité. Chaque entité lire sera comptabilisée nombre total de hello de transactions dans cette partition ; Par conséquent, vous pouvez facilement atteindre les objectifs d’évolutivité hello.

> [!NOTE]
> Vos tests de performances doivent mettre à jour toutes les requêtes mal conçues dans votre application.
> 
> 

### <a name="metrics-show-an-increase-in-PercentTimeoutError"></a>Les métriques indiquent une augmentation de la valeur PercentTimeoutError
Vos métriques indiquent une augmentation de la valeur **PercentTimeoutError** pour un de vos services de stockage. À hello même moment, hello client reçoit un volume important de messages d’état HTTP de « 500 opération Timeout » à partir d’opérations de stockage.

> [!NOTE]
> Vous pouvez voir des erreurs de délai d’attente temporairement en tant que service de stockage hello charge des demandes de soldes en déplaçant un serveur tooa partition.
> 
> 

Hello **PercentTimeoutError** métrique est une agrégation de hello suivant des métriques : **erreur ClientTimeoutError**, **erreur AnonymousClientTimeoutError**,  **Erreur SASClientTimeoutError**, **ServerTimeoutError**, **AnonymousServerTimeoutError**, et **SASServerTimeoutError**.

délais d’attente du serveur Hello sont dus à une erreur sur le serveur de hello. délais d’attente du client Hello se produisent car une opération sur le serveur de hello a dépassé le délai d’attente hello spécifié par hello client ; par exemple, un client à l’aide de la bibliothèque cliente de stockage de hello peut définir un délai d’attente pour une opération à l’aide de hello **ServerTimeout** propriété Hello **QueueRequestOptions** classe.

Délais d’attente du serveur indiquent un problème avec le service de stockage hello requiert une investigation. Vous pouvez utiliser des mesures toosee si vous atteignez les limites d’extensibilité hello pour le service de hello et tooidentify des pics d’activité dans le trafic qui peut être la cause du problème. Si le problème de hello est intermittent, il peut être dû équilibrage tooload d’activité dans le service hello. Si le problème de hello est persistant et n’est pas dû à votre application en appuyant sur les limites d’extensibilité hello du service de hello, vous devez déclencher un problème de prise en charge. Pour les délais d’attente du client, vous devez décider si hello timeout est valeur tooan approprié dans le client de hello et : valeur de délai d’attente de modification hello définies dans hello client ou examiner comment vous pouvez améliorer les performances de hello d’opérations hello dans le service de stockage hello, pour exemple en optimisant les requêtes de votre table ou de la réduction de taille hello de vos messages.

### <a name="metrics-show-an-increase-in-PercentNetworkError"></a>Les métriques indiquent une augmentation de la valeur PercentNetworkError
Vos métriques indiquent une augmentation de la valeur **PercentNetworkError** pour un de vos services de stockage. Hello **PercentNetworkError** métrique est une agrégation de hello suivant des métriques : **erreur NetworkError**, **erreur AnonymousNetworkError**, et  **Erreur SASNetworkError**. Ces modifications se produisent lorsque le service de stockage hello détecte une erreur réseau lorsque le client de hello effectue une demande de stockage.

Bonjour cause la plus courante de cette erreur est un client déconnexion avant l’expiration d’un délai d’attente dans le service de stockage hello. Vous devez examiner le code de hello dans votre toounderstand client quand et pourquoi hello client se déconnecte service de stockage hello. Vous pouvez également utiliser Wireshark, Microsoft Message Analyzer ou problèmes de connectivité réseau Tcping tooinvestigate à partir du client de hello. Ces outils sont décrits dans hello [annexes].

### <a name="the-client-is-receiving-403-messages"></a>Hello client reçoit les messages HTTP 403 (interdit)
Si votre application cliente qui émet les erreurs HTTP 403 (interdit), une cause possible est que le client hello utilise une Signature d’accès partagé (SAS) a expiré lorsqu’il envoie une demande de stockage (bien que les autres causes possibles incluent l’horloge inclinaison, valide les clés et vide en-têtes). Si une clé SAS expirée est la cause de hello, vous ne verrez pas toutes les entrées dans les données de journal Storage Logging hello côté serveur. Hello tableau suivant montre un exemple à partir du journal hello côté client généré par hello bibliothèque cliente de stockage qui illustre ce problème :

| Source | Commentaires | Commentaires | ID de la demande client | Operation Text |
| --- | --- | --- | --- | --- |
| Microsoft.WindowsAzure.Storage |Information |3 |85d077ab-… |Démarrage de l'opération avec l'emplacement Primary par mode d'emplacement PrimaryOnly. |
| Microsoft.WindowsAzure.Storage |Information |3 |85d077ab-… |Démarrage synchrone demande toohttps://domemaildist.blob.core.windows.netazureimblobcontainer/blobCreatedViaSAS.txt?sv=2014-02-14&amp;sr = c&amp;si = mypolicy&amp;sig = OFnd4Rd7z01fIvh % 2BmcR6zbudIH2F5Ikm % 2FyhNYZEmJNQ % 3D&amp;api-version = 2014-02-14. |
| Microsoft.WindowsAzure.Storage |Information |3 |85d077ab-… |Attente de la réponse. |
| Microsoft.WindowsAzure.Storage |Avertissement |2 |85d077ab-… |Exception levée pendant l’attente de réponse : serveur hello a renvoyé une erreur : (403) interdit... |
| Microsoft.WindowsAzure.Storage |Information |3 |85d077ab-… |Réponse reçue. Code d'état = 403, ID de la demande = 9d67c64a-64ed-4b0d-9515-3b14bbcdc63d, Content-MD5 = , ETag = . |
| Microsoft.WindowsAzure.Storage |Avertissement |2 |85d077ab-… |Exception levée pendant l’opération de hello : serveur hello a renvoyé une erreur : (403) interdit... |
| Microsoft.WindowsAzure.Storage |Information |3 |85d077ab-… |Vérifie si l’opération de hello doit être retentée. Nombre de tentatives = 0, le code d’état HTTP = 403, Exception = hello de serveur distant a retourné une erreur : (403) interdit... |
| Microsoft.WindowsAzure.Storage |Information |3 |85d077ab-… |emplacement de Hello suivant a été défini tooPrimary, selon le mode d’emplacement hello. |
| Microsoft.WindowsAzure.Storage |Error |1 |85d077ab-… |La stratégie de nouvelle tentative n’a pas autorisé de nouvelle tentative. Échec avec le serveur distant de hello a renvoyé une erreur : (403) interdit. |

Dans ce scénario, vous devez examiner la raison pour laquelle un jeton SAS hello arrive à expiration avant que les clients hello envoyant server de jeton toohello hello :

* En règle générale, vous ne devez pas définir une heure de début lorsque vous créez un SAS pour un client de toouse immédiatement. S’il existe de petites différences d’horloge entre l’hôte hello génération à l’aide de SAS hello hello heure actuelle et le service de stockage hello, il est possible pour tooreceive de service de stockage hello un SAS qui n’est pas valide.
* Vous ne devez pas définir une durée d'expiration très courte pour une SAS. Là encore, les différences de petite horloge entre l’hôte hello génération hello SAS et service de stockage hello peut entraîner tooa SAS apparemment expire le plus tôt que prévu.
* De hello le paramètre de version dans la clé SAS hello (par exemple **sv = 2015-04-05**) faire correspondre la version hello Hello bibliothèque cliente de stockage que vous utilisez ? Nous vous recommandons de toujours utiliser la version la plus récente de hello hello [bibliothèque cliente de stockage](https://www.nuget.org/packages/WindowsAzure.Storage/).
* Si vous régénérez vos clés d’accès de stockage, cela peut invalider tous les jetons SAS existants. Cela peut être un problème si vous générez des jetons SAP avec un délai d’expiration longs pour toocache d’applications client.

Si vous utilisez des jetons de SAP toogenerate hello bibliothèque cliente de stockage, il est facile toobuild un jeton valide. Toutefois, si vous êtes à l’aide des API REST de stockage de hello et construire des jetons SAS hello manuellement Lisez attentivement les rubrique hello [déléguer l’accès avec une Signature d’accès partagé](http://msdn.microsoft.com/library/azure/ee395415.aspx).

### <a name="the-client-is-receiving-404-messages"></a>Hello client reçoit les messages HTTP 404 (introuvable)
Si l’application cliente de hello reçoit un message HTTP 404 (introuvable) à partir du serveur de hello, cela implique que hello objet hello le client a tenté de toouse (par exemple, une entité, table, blob, conteneur ou file d’attente) n’existe pas dans le service de stockage hello. Il existe un certain nombre de raisons possibles à ce problème, dont :

* [Hello objet client ou un autre processus supprimés hello]
* [Problème d’autorisation de signature d’accès partagé (SAS)]
* [Code JavaScript côté client n’a pas l’objet d’autorisation tooaccess hello]
* [Défaillance réseau]

#### <a name="client-previously-deleted-the-object"></a>Hello objet client ou un autre processus supprimés hello
Dans les scénarios où hello client tente de tooread, mise à jour ou supprimer des données dans un service de stockage qu’il est généralement facile tooidentify dans hello côté serveur connecte à une opération précédente qui a supprimé l’objet hello en question à partir du service de stockage hello. Très souvent, les données de journal hello illustre cet objet de hello supprimé un autre utilisateur ou processus. Dans le journal de Storage Logging hello côté serveur, hello-type d’opération et les colonnes de clé objet demandé affichent lorsqu’un client supprimé un objet.

Dans le scénario hello dans lequel un client tente de tooinsert un objet, il ne peut pas être immédiatement évident pourquoi cela entraîne une réponse HTTP 404 (introuvable), étant donné que hello client crée un nouvel objet. Toutefois, si le client de hello consiste à créer un objet blob de que celle-ci doit être en mesure de toofind conteneur d’objets blob hello, si le client de hello crée un message, qu'il doit être en mesure de toofind une file d’attente, et si le client de hello consiste à ajouter une ligne il doit être table de hello toofind en mesure de.

Vous pouvez utiliser le journal côté client hello toogain de bibliothèque cliente de stockage hello que plus détaillée de comprendre quand hello en envoyant des requêtes spécifiques service de stockage toohello.

Hello suivant de journal côté client généré par la bibliothèque cliente de stockage de hello illustre hello problème lorsque le client de hello ne trouve pas le conteneur de hello pour blob hello que création. Ce journal inclut des détails de hello après les opérations de stockage :

| ID de la demande | Opération |
| --- | --- |
| 07b26a5d-... |**DeleteIfExists** conteneur d’objets blob méthode toodelete hello. Notez que cette opération inclut un **HEAD** demande toocheck existence hello du conteneur de hello. |
| e2d06d78… |**CreateIfNotExists** conteneur d’objets blob méthode toocreate hello. Notez que cette opération inclut un **HEAD** demande qui vérifie l’existence de hello du conteneur de hello. Hello **HEAD** renvoie un message 404, mais continue. |
| de8b1c3c-... |**UploadFromStream** objet blob de méthode toocreate hello. Hello **PUT** demande échoue avec un message 404 |

Entrées du journal :

| ID de la demande | Operation Text |
| --- | --- |
| 07b26a5d-... |Démarrage de la demande synchrone toohttps://domemaildist.blob.core.windows.net/azuremmblobcontainer. |
| 07b26a5d-... |StringToSign = HEAD............x-ms-client-request-id:07b26a5d-....x-ms-date:Tue, 03 Jun 2014 10:33:11 GMT.x-ms-version:2014-02-14./domemaildist/azuremmblobcontainer.restype:container. |
| 07b26a5d-... |Attente de la réponse. |
| 07b26a5d-... |Réponse reçue. Code d’état = 200, ID de la demande = eeead849-...Content-MD5 = , ETag =    &quot;0x8D14D2DC63D059B&quot;. |
| 07b26a5d-... |En-têtes de réponse ont été traités avec succès, d’autres hello d’opération de hello. |
| 07b26a5d-... |Téléchargement du corps de la réponse. |
| 07b26a5d-... |Opération exécutée avec succès. |
| 07b26a5d-... |Démarrage de la demande synchrone toohttps://domemaildist.blob.core.windows.net/azuremmblobcontainer. |
| 07b26a5d-... |StringToSign = DELETE............x-ms-client-request-id:07b26a5d-....x-ms-date:Tue, 03 Jun 2014 10:33:12    GMT.x-ms-version:2014-02-14./domemaildist/azuremmblobcontainer.restype:container. |
| 07b26a5d-... |Attente de la réponse. |
| 07b26a5d-... |Réponse reçue. Code d'état = 202, ID de la demande = 6ab2a4cf-..., Content-MD5 = , ETag = . |
| 07b26a5d-... |En-têtes de réponse ont été traités avec succès, d’autres hello d’opération de hello. |
| 07b26a5d-... |Téléchargement du corps de la réponse. |
| 07b26a5d-... |Opération exécutée avec succès. |
| e2d06d78-... |Démarrage de la requête asynchrone toohttps://domemaildist.blob.core.windows.net/azuremmblobcontainer.</td> |
| e2d06d78-... |StringToSign = HEAD............x-ms-client-request-id:e2d06d78-....x-ms-date:Tue, 03 Jun 2014 10:33:12 GMT.x-ms-version:2014-02-14./domemaildist/azuremmblobcontainer.restype:container. |
| e2d06d78-... |Attente de la réponse. |
| de8b1c3c-... |Démarrage de la demande synchrone toohttps://domemaildist.blob.core.windows.net/azuremmblobcontainer/blobCreated.txt. |
| de8b1c3c-... |StringToSign = PUT...64.qCmF+TQLPhq/YYK50mP9ZQ==........x-ms-blob-type:BlockBlob.x-ms-client-request-id:de8b1c3c-....x-ms-date:Tue, 03 Jun 2014 10:33:12 GMT.x-ms-version:2014-02-14./domemaildist/azuremmblobcontainer/blobCreated.txt. |
| de8b1c3c-... |Préparation des données de la demande toowrite. |
| e2d06d78-... |Exception levée pendant l’attente de réponse : serveur hello a renvoyé une erreur : (404) introuvable... |
| e2d06d78-... |Réponse reçue. Code d'état = 404, ID de la demande = 353ae3bc-..., Content-MD5 = , ETag = . |
| e2d06d78-... |En-têtes de réponse ont été traités avec succès, d’autres hello d’opération de hello. |
| e2d06d78-... |Téléchargement du corps de la réponse. |
| e2d06d78-... |Opération exécutée avec succès. |
| e2d06d78-... |Démarrage de la requête asynchrone toohttps://domemaildist.blob.core.windows.net/azuremmblobcontainer. |
| e2d06d78-... |StringToSign = PUT...0.........x-ms-client-request-id:e2d06d78-....x-ms-date:Tue, 03 Jun 2014 10:33:12 GMT.x-ms-version:2014-02-14./domemaildist/azuremmblobcontainer.restype:container. |
| e2d06d78-... |Attente de la réponse. |
| de8b1c3c-... |Écriture des données de la demande. |
| de8b1c3c-... |Attente de la réponse. |
| e2d06d78-... |Exception levée pendant l’attente de réponse : serveur hello a renvoyé une erreur : (409) conflit... |
| e2d06d78-... |Réponse reçue. Code d’état = 409, ID de la demande = c27da20e-..., Content-MD5 = , ETag = . |
| e2d06d78-... |Erreur de téléchargement du corps de la réponse. |
| de8b1c3c-... |Exception levée pendant l’attente de réponse : serveur hello a renvoyé une erreur : (404) introuvable... |
| de8b1c3c-... |Réponse reçue. Code d’état = 404, ID de la demande = 0eaeab3e-..., Content-MD5 = , ETag = . |
| de8b1c3c-... |Exception levée pendant l’opération de hello : serveur hello a renvoyé une erreur : (404) introuvable... |
| de8b1c3c-... |La stratégie de nouvelle tentative n’a pas autorisé de nouvelle tentative. Échec avec le serveur distant de hello a renvoyé une erreur : (404) introuvable... |
| e2d06d78-... |La stratégie de nouvelle tentative n’a pas autorisé de nouvelle tentative. Échec avec le serveur distant de hello a renvoyé une erreur : (409) conflit... |

Dans cet exemple, les journaux hello montre que le client hello est entrelacement des demandes à partir de hello **CreateIfNotExists** (méthode) (demande id e2d06d78...) avec les requêtes hello de hello **UploadFromStream** () (méthode) de8b1c3c-...) ; Cela se produit, car l’application cliente de hello consiste à appeler ces méthodes de façon asynchrone. Vous devez modifier le code asynchrone hello hello tooensure de client qu’il crée le conteneur de hello avant de tenter de tooupload tout objet blob tooa de données dans le conteneur. Idéalement, vous devriez créer tous vos conteneurs à l’avance.

#### <a name="SAS-authorization-issue"></a>Problème d’autorisation de signature d’accès partagé (SAP)
Si l’application cliente de hello tente toouse une clé SAS qui n’inclut pas les autorisations nécessaires hello pour l’opération de hello, le service de stockage hello retourne un client toohello du message HTTP 404 (introuvable). À hello même moment, vous verrez également une valeur différente de zéro pour **erreur SASAuthorizationError** dans les mesures hello.

Hello tableau suivant montre un exemple de message de journal côté serveur à partir du fichier journal de Storage Logging hello :

| Nom | Valeur |
| --- | --- |
| Heure de début de la demande | 2014-05-30T06:17:48.4473697Z |
| Type d'opération     | GetBlobProperties            |
| État de la demande     | SASAuthorizationError        |
| Code d'état HTTP   | 404                          |
| Type d'authentification| Sas                          |
| Type de service       | Blob                         |
| URL de la demande        | https://domemaildist.blob.core.windows.net/azureimblobcontainer/blobCreatedViaSAS.txt |
| nbsp;              |   ?sv=2014-02-14&sr=c&si=mypolicy&sig=XXXXX&;api-version=2014-02-14 |
| Request ID header  | a1f348d5-8032-4912-93ef-b393e5252a3b |
| ID de la demande client  | 2d064953-8436-4ee0-aa0c-65cb874f7929 |


Vous devez examiner la raison pour laquelle votre application cliente tente de tooperform une opération n’a pas été accordé des autorisations pour.

#### <a name="JavaScript-code-does-not-have-permission"></a>Code JavaScript côté client n’a pas l’objet d’autorisation tooaccess hello
Si vous utilisez un client JavaScript et le service de stockage hello renvoie les messages HTTP 404, vous recherchez hello erreurs JavaScript dans le navigateur de hello suivantes :

```
SEC7120: Origin http://localhost:56309 not found in Access-Control-Allow-Origin header.
SCRIPT7002: XMLHttpRequest: Network Error 0x80070005, Access is denied.
```

> [!NOTE]
> Vous pouvez utiliser les outils de développement F12 hello dans Internet Explorer tootrace hello messages échangés entre le navigateur de hello et le service de stockage hello lors de la résolution des problèmes de JavaScript côté client.
> 
> 

Ces erreurs se produisent, car le navigateur web de hello implémente hello [stratégie d’origine](http://www.w3.org/Security/wiki/Same_Origin_Policy) provient de la restriction de sécurité qui empêche une page web à partir de l’appel d’une API dans un autre domaine à partir de la page de hello domaine hello.

toowork autour hello problème de JavaScript, vous pouvez configurer Cross-origine partage de ressources (CORS) pour hello stockage service hello client accède. Pour plus d’informations, voir [Prise en charge du service Partage des ressources cross-origine (CORS) pour les services Azure Storage](http://msdn.microsoft.com/library/azure/dn535601.aspx).

Hello suivant l’exemple de code montre comment tooconfigure votre service blob tooallow JavaScript qui s’exécute dans hello tooaccess du domaine Contoso un objet blob dans votre service de stockage d’objets blob :

```csharp
CloudBlobClient client = new CloudBlobClient(blobEndpoint, new StorageCredentials(accountName, accountKey));
// Set hello service properties.
ServiceProperties sp = client.GetServiceProperties();
sp.DefaultServiceVersion = "2013-08-15";
CorsRule cr = new CorsRule();
cr.AllowedHeaders.Add("*");
cr.AllowedMethods = CorsHttpMethods.Get | CorsHttpMethods.Put;
cr.AllowedOrigins.Add("http://www.contoso.com");
cr.ExposedHeaders.Add("x-ms-*");
cr.MaxAgeInSeconds = 5;
sp.Cors.CorsRules.Clear();
sp.Cors.CorsRules.Add(cr);
client.SetServiceProperties(sp);
```

#### <a name="network-failure"></a>Défaillance réseau
Dans certains cas, les paquets réseau perdue peuvent entraîner des service de stockage toohello retournant cliente de toohello de messages HTTP 404. Par exemple, lorsque votre application cliente est suppression d’une entité de service de table hello vous voyez hello client lève une exception de stockage reporting une « HTTP 404 (introuvable) » le message d’état à partir du service de table hello. Lorsque vous examinez la table hello dans le service de stockage de table hello, vous consultez que service de hello n’a supprimé l’entité de hello comme demandé.

Détails de l’exception dans le client de hello Hello incluent l’id de demande hello (7e84f12d...) affecté par le service de table hello pour demande de hello : vous pouvez utiliser cette détails de la demande d’informations toolocate hello dans les journaux de stockage côté serveur hello en recherchant dans hello  **en-tête de l’id de demande** colonne dans le fichier journal de hello. Vous pouvez également utiliser hello métriques tooidentify lors de défaillances tel que cela se produisent et ensuite rechercher les fichiers de journaux hello selon hello hello ponctualité enregistrement cette erreur. Ce journal de saisie indique que hello delete a échoué avec un message d’état HTTP (404) « Client » autre erreur. Hello même entrée de journal inclut également les id de demande hello généré par le client hello Bonjour **client-request-id** colonne (813ea74f...).

Hello côté serveur inclut également une autre entrée par hello même **client-request-id** valeur (813ea74f...) pour une suppression pour hello même entité et de hello même client. Cette opération de suppression réussie a eu lieu très peu de temps avant la demande d’échec de la suppression de hello.

cause la plus probable Hello de ce scénario est que le client hello a envoyé une demande de suppression pour hello entité toohello service de table, ce qui a réussi, mais n’a pas reçu d’accusé de réception du serveur hello (peut-être en raison d’un problème de réseau temporaire tooa). client de Hello automatiquement retentée opération de hello (à l’aide de hello même **client-request-id**), et cette nouvelle tentative a échoué, car l’entité de hello a déjà été supprimée.

Si ce problème se produit fréquemment, vous devez examiner pourquoi les clients hello échoue tooreceive les accusés de réception à partir du service de table hello. Si le problème de hello est intermittent, vous devez intercepter l’erreur « HTTP (404) introuvable » de hello et consigner dans le client de hello, mais autoriser hello client toocontinue.

### <a name="the-client-is-receiving-409-messages"></a>Hello client reçoit les messages HTTP 409 (conflit)
Hello tableau suivant montre un extrait de journal côté serveur hello deux opérations du client : **DeleteIfExists** suivie immédiatement de **CreateIfNotExists** à l’aide de hello le même nom de conteneur d’objets blob. Notez que chaque opération du client génère deux demandes envoyées toohello server, tout d’abord un **GetContainerProperties** toocheck de demande si le conteneur de hello existe, suivie de hello **DeleteContainer** ou  **CreateContainer** demande.

| Timestamp | Opération | Résultat | Nom du conteneur | ID de la demande client |
| --- | --- | --- | --- | --- |
| 05:10:13.7167225 |GetContainerProperties |200 |mmcont |c9f52c89-… |
| 05:10:13.8167325 |DeleteContainer |202 |mmcont |c9f52c89-… |
| 05:10:13.8987407 |GetContainerProperties |404 |mmcont |bc881924-… |
| 05:10:14.2147723 |CreateContainer |409 |mmcont |bc881924-… |

Hello code dans l’application cliente de hello supprime et recrée ensuite immédiatement un conteneur d’objets blob à l’aide de hello même nom : hello **CreateIfNotExists** (méthode) (Client demande ID bc881924-...) finit par échouer avec hello HTTP 409 (conflit) erreur. Lorsqu’un client supprime les conteneurs d’objets blob, tables ou les files d’attente qu'est une brève période avant le nom de hello redevient disponible.

application cliente de Hello doit utiliser des noms de conteneur unique chaque fois qu’il crée de nouveaux conteneurs si le modèle de suppression/recréez hello est courant.

### <a name="metrics-show-low-percent-success"></a>Les métriques indiquent une valeur PercentSuccess faible ou les entrées du journal d’analyse incluent des opérations avec un statut de transaction ClientOtherErrors
Hello **PercentSuccess** métrique capture % hello des opérations qui ont réussi, en fonction de leur Code d’état HTTP. Opérations avec des codes d’état de 2XX count comme réussies, tandis que les opérations avec des codes d’état dans les plages 3XX, 4XX et 5XX sont comptées comme ayant échoué et inférieure hello **PercentSucess** valeur métrique. Dans les fichiers journaux de stockage côté serveur hello, ces opérations sont enregistrées avec un statut de transaction **ClientOtherErrors**.

Il est important toonote que ces opérations sont terminées et par conséquent n’affectent pas les autres métriques telles que la disponibilité. Voici quelques exemples d'opérations qui s'exécutent avec succès, mais qui génèrent des codes d'état HTTP d'échec :

* **ResourceNotFound** (pas trouvé 404), par exemple à partir d’une commande GET demande tooa d’objets blob qui n’existe pas.
* **ResouceAlreadyExists** (409 conflit), par exemple à partir d’un **CreateIfNotExist** opération où les ressources hello existant déjà.
* **ConditionNotMet** (non modifié 304), par exemple à partir d’une opération conditionnelle telles que lorsqu’un client envoie une **ETag** valeur et HTTP **If-None-Match** en-tête toorequest une image uniquement se Il a été mis à jour depuis la dernière opération de hello.

Vous trouverez une liste de codes d’erreur courants API REST qui retournent des services de stockage hello sur la page de hello [Codes d’erreur courants REST API](http://msdn.microsoft.com/library/azure/dd179357.aspx).

### <a name="capacity-metrics-show-an-unexpected-increase"></a>Les métriques de capacité indiquent une augmentation inattendue de l’utilisation de la capacité de stockage
Si vous voyez soudaine, des modifications inattendues dans l’utilisation des capacités de votre compte de stockage, vous pouvez examiner les raisons de hello en examinant en premier vos métriques de disponibilité ; par exemple, une augmentation nombre hello de demandes d’échec de la suppression peut entraîner des tooan augmentation montant hello du stockage blob que vous utilisez en tant qu’opérations de nettoyage spécifique d’application pour que vous attendent toobe la libération de l’espace ne fonctionne pas comme prévu ( exemple, car il est utilisés pour la libération de l’espace des jetons SAS hello ont expiré).

### <a name="you-are-experiencing-unexpected-reboots"></a>Vous constatez des redémarrages inattendus des machines virtuelles Azure associées à un grand nombre de disques durs virtuels
Si une Machine virtuelle Azure (VM) a un grand nombre de disques durs virtuels attachés qui sont Bonjour même compte de stockage, vous pourriez dépasser les objectifs d’évolutivité hello pour un compte de stockage individuel à l’origine de hello VM toofail. Vous devez vérifier les métriques par minute hello pour le compte de stockage hello (**TotalRequests**/**TotalIngress**/**TotalEgress**) pour les pics d’activité qui dépassent les objectifs d’évolutivité hello pour un compte de stockage. Consultez la section de hello »[métriques indiquent une augmentation dans PercentThrottlingError]» pour obtenir de l’aide à déterminer si la limitation s’est produite sur votre compte de stockage.

En général, chaque entrée individuelle ou une opération de sortie sur un disque dur virtuel à partir d’un ordinateur virtuel traduit trop**Page obtenir** ou **Put Page** opérations sur hello sous-jacent d’objet blob de pages. Par conséquent, vous pouvez utiliser hello estimé IOPS pour votre environnement tootune le nombre de disques durs virtuels vous pouvez avoir dans un seul compte de stockage basé sur le comportement de hello spécifiques de votre application. Nous déconseillons d’avoir plus de 40 disques dans un compte de stockage unique. Consultez [évolutivité du stockage Azure et les objectifs de performances](storage-scalability-targets.md) pour plus d’informations des objectifs d’évolutivité actuelle hello pour les comptes de stockage, notamment hello demande totale taux total de bande passante et de type hello du compte de stockage vous utilisez .
Si vous dépassez les cibles d’extensibilité hello pour votre compte de stockage, vous devez placer vos disques durs virtuels plusieurs autre activité de stockage comptes tooreduce hello dans chaque compte.

### <a name="your-issue-arises-from-using-the-storage-emulator"></a>Votre problème survient à l’aide de l’émulateur de stockage hello pour le développement ou de test
En général, vous utilisez l’émulateur de stockage hello pendant le développement et testez exigence de hello tooavoid pour un compte de stockage Azure. Hello les problèmes courants qui peuvent se produire lorsque vous utilisez l’émulateur de stockage hello sont :

* [Fonction « X » ne fonctionne pas dans l’émulateur de stockage hello]
* [Erreur « les valeur hello pour un des en-têtes de hello HTTP n’est pas le format correct de hello » lorsque l’utilisation hello émulateur de stockage]
* [L’émulateur de stockage hello en cours d’exécution nécessite des privilèges d’administrateur]

#### <a name="feature-X-is-not-working"></a>Fonction « X » ne fonctionne pas dans l’émulateur de stockage hello
l’émulateur de stockage Hello ne prend pas en charge toutes les fonctionnalités de hello de services de stockage Azure hello comme service de fichiers hello. Pour plus d’informations, consultez [hello d’utilisation émulateur de stockage pour le développement et le test](storage-use-emulator.md).

Pour les fonctionnalités hello stockage émulateur ne pas en charge, utilisez le service de stockage Azure hello dans le cloud de hello.

#### <a name="error-HTTP-header-not-correct-format"></a>Erreur « les valeur hello pour un des en-têtes de hello HTTP n’est pas le format correct de hello » lorsque l’utilisation hello émulateur de stockage
Vous testez votre application qui utilisent hello bibliothèque cliente de stockage par rapport à hello stockage local émulateur et appels de méthodes comme **CreateIfNotExists** échec avec l’erreur de hello un message « hello valeur pour un des en-têtes de hello HTTP n’est pas dans format correct Hello. » Cela indique que hello version de l’émulateur de stockage hello que vous utilisez ne prend pas en charge la version hello de bibliothèque cliente de hello stockage que vous utilisez. Hello bibliothèque cliente de stockage ajoute l’en-tête de hello **x-ms-version** tooall hello rend les demandes. Si l’émulateur de stockage hello ne reconnaît pas la valeur hello Bonjour **x-ms-version** en-tête, il rejette la demande de hello.

Vous pouvez utiliser hello Client de bibliothèque de stockage des journaux toosee hello valeur Hello **en-tête x-ms-version** qu’il envoie. Vous pouvez également afficher la valeur hello hello **en-tête x-ms-version** si vous utilisez des demandes de Fiddler tootrace hello à partir de votre application cliente.

Ce scénario se produit généralement si vous installez et utilisez la version la plus récente hello Hello bibliothèque cliente de stockage sans mettre à jour de l’émulateur de stockage hello. Vous devez installer la version la plus récente de l’émulateur de stockage hello hello ou utiliser le stockage cloud au lieu de l’émulateur de hello pour le développement et de test.

#### <a name="storage-emulator-requires-administrative-privileges"></a>L’émulateur de stockage hello en cours d’exécution nécessite des privilèges d’administrateur
Vous êtes invité pour les informations d’identification d’administrateur lorsque vous exécutez l’émulateur de stockage hello. Cela se produit uniquement lorsque vous initialisez l’émulateur de stockage hello pour hello première fois. Après avoir initialisé l’émulateur de stockage hello, vous n’avez pas besoin des privilèges d’administrateur toorun nouveau.

Pour plus d’informations, consultez [hello d’utilisation émulateur de stockage pour le développement et le test](storage-use-emulator.md). Notez que vous pouvez également initialiser l’émulateur de stockage hello dans Visual Studio, qui nécessite également des privilèges d’administrateur.

### <a name="you-are-encountering-problems-installing-the-Windows-Azure-SDK"></a>Vous rencontrez des problèmes d’installation Bonjour Azure SDK pour .NET
Lorsque vous essayez tooinstall hello SDK, il échoue lors de l’émulateur de stockage hello tooinstall sur votre ordinateur local. journal d’installation Hello contient hello suivant des messages :

* CAQuietExec : Erreur : Impossible de tooaccess l’instance SQL
* CAQuietExec : Erreur : Impossible de toocreate la base de données

cause de Hello est un problème avec une installation existante de la base de données locale. Par défaut, l’émulateur de stockage hello utilise LocalDB toopersist données lors de la simulation des services de stockage Azure hello. Vous pouvez réinitialiser votre instance de base de données locale en exécutant hello suivant de commandes dans une fenêtre d’invite de commandes avant d’essayer de tooinstall hello SDK.

```
sqllocaldb stop v11.0
sqllocaldb delete v11.0
delete %USERPROFILE%\WAStorageEmulatorDb3*.*
sqllocaldb create v11.0
```

Hello **supprimer** commande supprime les anciens fichiers de base de données à partir des précédentes installations de l’émulateur de stockage hello.

### <a name="you-have-a-different-issue-with-a-storage-service"></a>Vous rencontrez un autre problème avec un service de stockage
Si les sections de résolution précédente hello n’incluent pas de problème hello que vous rencontrez avec un service de stockage, vous devez adopter hello suivant approche toodiagnosing et résoudre vos problèmes.

* Vérifiez votre toosee métriques s’il en existe toute modification à partir de votre comportement attendu de la ligne de base. À partir des mesures hello, vous pouvez être en mesure de toodetermine si le problème de hello est temporaire ou définitive et les opérations de stockage hello problème affecte.
* Vous pouvez utiliser les informations de métriques hello toohelp recherche de vos données de journal côté serveur pour des informations détaillées sur les erreurs qui se produisent. Ces informations peuvent vous aider à dépanner et résoudre le problème de hello.
* Si informations hello dans les journaux côté serveur hello ne sont pas suffisant problème de hello tootroubleshoot avec succès, vous pouvez utiliser hello bibliothèque cliente de stockage des journaux de côté client tooinvestigate hello comportement de votre application cliente et des outils tels que Fiddler, Wireshark, et Microsoft Message Analyzer tooinvestigate votre réseau.

Pour plus d’informations sur l’utilisation de Fiddler, consultez «[annexe 1 : à l’aide du trafic HTTP et HTTPS du toocapture Fiddler]. »

Pour plus d’informations sur l’utilisation de Wireshark, consultez «[annexe 2 : à l’aide d’un trafic réseau Wireshark toocapture]. »

Pour plus d’informations sur l’utilisation de Microsoft Message Analyzer, consultez «[annexe 3 : à l’aide de trafic de réseau Microsoft Message Analyzer toocapture]. »

## <a name="appendices"></a>Annexes
les annexes Hello décrivent plusieurs outils qui peuvent s’avérer utile lorsque le diagnostic et la résolution des problèmes de stockage Azure (et d’autres services). Ces outils ne font pas partie de Azure Storage, et certains d'entre eux sont des produits tiers. Par conséquent, les outils hello présentées dans ces annexes ne sont pas couvertes par un contrat de prise en charge que vous auriez conclus avec Microsoft Azure ou le stockage Azure, et par conséquent, dans le cadre de votre processus d’évaluation, vous devez examiner hello licences et prise en charge des options disponibles à partir de fournisseurs de Hello de ces outils.

### <a name="appendix-1"></a>Annexe 1 : À l’aide de Fiddler toocapture HTTP et le trafic HTTPS
[Fiddler](http://www.telerik.com/fiddler) est un outil utile pour l’analyse du trafic HTTP et HTTPS hello entre votre application cliente et le hello service de stockage Azure que vous utilisez.

> [!NOTE]
> Fiddler peut décoder le trafic HTTPS ; Vous devez lire attentivement documentation de Fiddler hello toounderstand comment il le fait et les implications de sécurité toounderstand hello.
> 
> 

Cette annexe fournit une brève procédure pas à pas comment tooconfigure Fiddler toocapture le trafic entre l’ordinateur local de hello où vous avez installé Fiddler et hello des services de stockage Azure.

Après avoir lancé Fiddler, il commence à capturer le trafic HTTP et HTTPS de votre ordinateur local. Hello Voici certaines commandes utiles pour le contrôle Fiddler :

* Arrêt et démarrage de la capture du trafic. Sur le menu principal de hello, accédez trop**fichier** puis cliquez sur **capturer le trafic** tootoggle capture et désactiver.
* Enregistrement des données de trafic capturées. Sur le menu principal de hello, accédez trop**fichier**, cliquez sur **enregistrer**, puis cliquez sur **toutes les Sessions**: cela vous permet du trafic de hello toosave dans un fichier d’Archive de la Session. Vous pouvez recharger une Archive de Session pour l’analyse, ou l’envoyer demande de prise en charge tooMicrosoft.

quantité de hello toolimit de trafic que Fiddler capture, vous pouvez utiliser des filtres que vous configurez dans hello **filtres** hello onglet suivant capture d’écran montre un filtre qui capture uniquement le trafic envoyé toohello  **contosoemaildist.table.Core.Windows.NET** point de terminaison de stockage :

![][5]

### <a name="appendix-2"></a>Annexe 2 : À l’aide du trafic réseau Wireshark toocapture
[Wireshark](http://www.wireshark.org/) est un analyseur de protocole réseau qui vous permet de tooview paquet des informations détaillées sur un large éventail de protocoles réseau.

Hello procédure suivante vous montre comment toocapture paquet des informations détaillées sur le trafic à partir de l’ordinateur local de hello où vous avez installé le service de table Wireshark toohello dans votre compte de stockage Azure.

1. Lancez Wireshark sur votre ordinateur local.
2. Bonjour **Démarrer** section, d’une interface de réseau local sélectionnez hello ou d’interfaces qui sont connecté toohello internet.
3. Cliquez sur **Capture Options**.
4. Ajouter un filtre toohello **filtre de Capture** zone de texte. Par exemple, **héberger contosoemaildist.table.core.windows.net** configurera Wireshark toocapture uniquement tooor les paquets envoyés à partir du point de terminaison du service hello table Bonjour **contosoemaildist** stockage compte. Extraire hello [la liste complète des filtres de Capture](http://wiki.wireshark.org/CaptureFilters).
   
   ![][6]
5. Cliquez sur **Start**. Wireshark est prêt à capturer toutes les tooor envoi de paquets hello à partir du point de terminaison de service hello table que vous utilisez votre application cliente sur votre ordinateur local.
6. Lorsque vous avez terminé, cliquez sur le menu principal hello **Capture** , puis **arrêter**.
7. toosave hello capturées dans un Wireshark capturer fichier, cliquez sur le menu principal hello **fichier** , puis **enregistrer**.

WireShark met en surbrillance toutes les erreurs qui existent dans hello **packetlist** fenêtre. Vous pouvez également utiliser hello **Expert Info** fenêtre (cliquez sur **analyser**, puis **Expert Info**) tooview un résumé des erreurs et avertissements.

![][7]

Vous pouvez également choisir les données TCP tooview hello comme couche d’application hello peut la voir en cliquant sur hello données TCP et en sélectionnant **suivez le flux TCP**. Cette option est particulièrement utile si vous avez capturé votre image mémoire sans filtre de capture. Pour plus d’informations, consultez [Following TCP Streams](http://www.wireshark.org/docs/wsug_html_chunked/ChAdvFollowTCPSection.html)(Suivi du flux TCP).

![][8]

> [!NOTE]
> Pour plus d’informations sur l’utilisation de Wireshark, consultez hello [Guide de l’utilisateur Wireshark](http://www.wireshark.org/docs/wsug_html_chunked).
> 
> 

### <a name="appendix-3"></a>Annexe 3 : À l’aide de trafic de réseau Microsoft Message Analyzer toocapture
Vous pouvez utiliser Microsoft Message Analyzer toocapture HTTP et le trafic HTTPS dans un tooFiddler de manière similaire et capturer le trafic réseau dans un tooWireshark de façon similaire.

#### <a name="configure-a-web-tracing-session-using-microsoft-message-analyzer"></a>Configuration d'une nouvelle session de suivi Web à l'aide de l'analyseur de message Microsoft
tooconfigure une session web pour le trafic HTTP et HTTPS à l’aide de Microsoft Message Analyzer, exécuter l’application de l’Analyseur de Message Microsoft hello, puis sur hello **fichier** menu, cliquez sur **/Trace de Capture**. Dans la liste hello des scénarios de trace disponibles, sélectionnez **Proxy Web**. Puis Bonjour **Configuration du scénario Trace** Panneau de configuration, Bonjour **HostnameFilter** zone de texte, ajouter des noms de vos points de terminaison de stockage hello (vous pouvez rechercher ces noms Bonjour [portail Azure](https://portal.azure.com)). Par exemple, si hello nom de votre compte de stockage Azure est **contosodata**, vous devez ajouter hello suivant toohello **HostnameFilter** zone de texte :

```
contosodata.blob.core.windows.net contosodata.table.core.windows.net contosodata.queue.core.windows.net
```

> [!NOTE]
> Un caractère d’espace sépare les noms d’hôtes hello.
> 
> 

Lorsque vous êtes prêt toostart collecte des données de trace, cliquez sur hello **Start With** bouton.

Pour plus d’informations sur hello Microsoft Message Analyzer **Proxy Web** de trace, consultez [Microsoft-PEF-WebProxy fournisseur](http://technet.microsoft.com/library/jj674814.aspx).

Hello intégré **Proxy Web** trace dans l’Analyseur de Message de Microsoft est basée sur Fiddler ; il peut capturer le trafic HTTPS côté client et afficher les messages non chiffrés de HTTPS. Hello **Proxy Web** fonctionnement de trace en configurant un proxy local pour tout le trafic HTTP et HTTPS qui lui donne un accès toounencrypted messages.

#### <a name="diagnosing-network-issues-using-microsoft-message-analyzer"></a>Diagnostic des problèmes de réseau à l'aide de l'analyseur de message Microsoft
En outre toousing hello Microsoft Message Analyzer **Proxy Web** détails toocapture de suivi de hello le trafic HTTP/HTTPs entre l’application cliente de hello et le service de stockage hello, vous pouvez également utiliser intégrées de hello  **Couche de liaison locale** suivi des informations relatives aux paquets réseau toocapture. Cela permet de vous toocapture données similaires toothat que vous pouvez capturer avec Wireshark et diagnostiquer les problèmes de réseau telles que les paquets ignorés.

Hello capture d’écran suivante montre un exemple **couche de liaison locale** trace avec certaines **d’information** messages Bonjour **DiagnosisTypes** colonne. En cliquant sur une icône dans hello **DiagnosisTypes** colonne affiche les détails de hello de message de type hello. Dans cet exemple, le serveur de hello retransmis message #305, car il n’a pas reçu d’accusé de réception à partir du client de hello :

![][9]

Lorsque vous créez la session de trace hello dans l’Analyseur de Message de Microsoft, vous pouvez spécifier des filtres tooreduce hello quantité bruit dans la trace de hello. Sur hello **capturer /trace** page où vous définissez la trace de hello, cliquez sur hello **configurer** lier ensuite trop**Microsoft-Windows-NDIS-PacketCapture**. Hello suivant capture d’écran montre une configuration qui permet de filtrer le trafic TCP pour les adresses IP de hello des trois services de stockage :

![][10]

Pour plus d’informations sur la trace de la couche de liaison locale de Microsoft Message Analyzer de hello, consultez [Microsoft-PEF-NDIS-PacketCapture fournisseur](http://technet.microsoft.com/library/jj659264.aspx).

### <a name="appendix-4"></a>Annexe 4 : À l’aide de données de journaux et de métriques tooview Excel
De nombreux outils permettent de données de métriques de stockage hello toodownload à partir du stockage de table Windows Azure dans un format délimité qui rend les données de salutation tooload facile dans Excel pour consultation et l’analyse. Les données de journalisation du stockage d’objets blob Azure sont déjà dans un format délimité qui peut être chargé dans Excel. Toutefois, vous devrez tooadd les en-têtes de colonnes appropriés en fonction des informations hello à [le Format de journal Analytique stockage](http://msdn.microsoft.com/library/azure/hh343259.aspx) et [schéma de Table de métriques Storage Analytique](http://msdn.microsoft.com/library/azure/hh343264.aspx).

tooimport vos données Storage Logging dans Excel après avoir le télécharger depuis le stockage blob :

* Sur hello **données** menu, cliquez sur **à partir du texte**.
* Parcourir le fichier de journal toohello tooview et cliquez sur **importation**.
* À l’étape 1 de hello **Assistant Importation de texte**, sélectionnez **délimité**.

À l’étape 1 de hello **Assistant Importation de texte**, sélectionnez **point-virgule** comme hello seul délimiteur et choisissez les guillemets doubles comme hello **qualificateur de texte**. Puis cliquez sur **Terminer** et choisissez où tooplace hello des données dans votre classeur.

### <a name="appendix-5"></a>Annexe 5 : analyse avec Application Insights pour Visual Studio Team Services
Vous pouvez également utiliser les fonctionnalités d’Application Insights hello pour Visual Studio Team Services dans le cadre de votre analyse des performances et disponibilité. Cet outil permet de :

* Vous assurer que votre service Web est disponible et réactif. Si votre application est un site web ou une application de périphérique qui utilise un service web, il peut tester votre URL de quelques minutes à partir d’emplacements monde hello et vous permettent de savoir il s'existe un problème.
* Rapidement diagnostiquer tous les problèmes ou exceptions de performances rencontrés par votre service Web. Découvrez si l'UC ou d'autres ressources sont en difficulté, obtenez les traces de la pile à partir des exceptions et effectuez des recherches aisées dans les suivis de journalisation. Si hello chutes de performances de l’application sous les limites acceptables, nous puissions vous envoyer un message électronique. Vous pouvez analyser les services Web .NET et Java.

Vous trouverez plus d’informations dans la [Présentation d’Application Insights](../../application-insights/app-insights-overview.md).

<!--Anchors-->
[Introduction]: #introduction
[Organisation de ce guide]: #how-this-guide-is-organized

[votre service de stockage de surveillance]: #monitoring-your-storage-service
[Analyse de l’état d’intégrité du service]: #monitoring-service-health
[Analyse de la capacité]: #monitoring-capacity
[Analyse de la disponibilité]: #monitoring-availability
[Analyse des performances]: #monitoring-performance

[diagnostiquer les problèmes de stockage]: #diagnosing-storage-issues
[Problèmes d’état d’intégrité du service]: #service-health-issues
[Problèmes de performances]: #performance-issues
[Erreurs de diagnostic]: #diagnosing-errors
[Problèmes d’émulateur de stockage]: #storage-emulator-issues
[Outils de journalisation du stockage]: #storage-logging-tools
[Utilisation des outils de journalisation réseau]: #using-network-logging-tools

[le suivi de bout en bout]: #end-to-end-tracing
[Corrélation des données de journalisation]: #correlating-log-data
[ID de la demande client]: #client-request-id
[ID demande serveur]: #server-request-id
[Horodatages]: #timestamps

[conseils de dépannage]: #troubleshooting-guidance
[mesures affichent AverageE2ELatency haute et basse AverageServerLatency]: #metrics-show-high-AverageE2ELatency-and-low-AverageServerLatency
[Affichent les métriques AverageE2ELatency basse et AverageServerLatency basse mais hello client rencontre une latence élevée]: #metrics-show-low-AverageE2ELatency-and-low-AverageServerLatency
[Les métriques indiquent une valeur AverageServerLatency élevée]: #metrics-show-high-AverageServerLatency
[Vous constatez des retards inattendus dans la livraison des messages d’une file d’attente]: #you-are-experiencing-unexpected-delays-in-message-delivery

[métriques indiquent une augmentation dans PercentThrottlingError]: #metrics-show-an-increase-in-PercentThrottlingError
[Augmentation provisoire de la valeur PercentThrottlingError]: #transient-increase-in-PercentThrottlingError
[Augmentation permanente de l’erreur PercentThrottlingError]: #permanent-increase-in-PercentThrottlingError
[métriques indiquent une augmentation dans PercentTimeoutError]: #metrics-show-an-increase-in-PercentTimeoutError
[Les métriques indiquent une augmentation de la valeur PercentNetworkError]: #metrics-show-an-increase-in-PercentNetworkError

[Hello client reçoit les messages HTTP 403 (interdit)]: #the-client-is-receiving-403-messages
[Hello client reçoit les messages HTTP 404 (introuvable)]: #the-client-is-receiving-404-messages
[Hello objet client ou un autre processus supprimés hello]: #client-previously-deleted-the-object
[Problème d’autorisation de signature d’accès partagé (SAS)]: #SAS-authorization-issue
[Code JavaScript côté client n’a pas l’objet d’autorisation tooaccess hello]: #JavaScript-code-does-not-have-permission
[Défaillance réseau]: #network-failure
[Hello client reçoit les messages HTTP 409 (conflit)]: #the-client-is-receiving-409-messages

[PercentSuccess basse affichent les métriques ou les entrées de journal analytique ont des opérations avec état de la transaction de ClientOtherErrors]: #metrics-show-low-percent-success
[Les métriques de capacité indiquent une augmentation inattendue de l’utilisation de la capacité de stockage]: #capacity-metrics-show-an-unexpected-increase
[Vous constatez des redémarrages inattendus des machines virtuelles associées à un grand nombre de disques durs virtuels]: #you-are-experiencing-unexpected-reboots
[Votre problème survient à l’aide de l’émulateur de stockage hello pour le développement ou de test]: #your-issue-arises-from-using-the-storage-emulator
[Fonction « X » ne fonctionne pas dans l’émulateur de stockage hello]: #feature-X-is-not-working
[Erreur « les valeur hello pour un des en-têtes de hello HTTP n’est pas le format correct de hello » lorsque l’utilisation hello émulateur de stockage]: #error-HTTP-header-not-correct-format
[L’émulateur de stockage hello en cours d’exécution nécessite des privilèges d’administrateur]: #storage-emulator-requires-administrative-privileges
[Vous rencontrez des problèmes d’installation Bonjour Azure SDK pour .NET]: #you-are-encountering-problems-installing-the-Windows-Azure-SDK
[Vous rencontrez un autre problème avec un service de stockage]: #you-have-a-different-issue-with-a-storage-service

[annexes]: #appendices
[annexe 1 : à l’aide du trafic HTTP et HTTPS du toocapture Fiddler]: #appendix-1
[annexe 2 : à l’aide d’un trafic réseau Wireshark toocapture]: #appendix-2
[annexe 3 : à l’aide de trafic de réseau Microsoft Message Analyzer toocapture]: #appendix-3
[Annexe 4 : À l’aide de données de journaux et de métriques tooview Excel]: #appendix-4
[Annexe 5 : analyse avec Application Insights pour Visual Studio Team Services]: #appendix-5

<!--Image references-->
[1]: ./media/storage-monitoring-diagnosing-troubleshooting/overview.png
[3]: ./media/storage-monitoring-diagnosing-troubleshooting/hour-minute-metrics.png
[4]: ./media/storage-monitoring-diagnosing-troubleshooting/high-e2e-latency.png
[5]: ./media/storage-monitoring-diagnosing-troubleshooting/fiddler-screenshot.png
[6]: ./media/storage-monitoring-diagnosing-troubleshooting/wireshark-screenshot-1.png
[7]: ./media/storage-monitoring-diagnosing-troubleshooting/wireshark-screenshot-2.png
[8]: ./media/storage-monitoring-diagnosing-troubleshooting/wireshark-screenshot-3.png
[9]: ./media/storage-monitoring-diagnosing-troubleshooting/mma-screenshot-1.png
[10]: ./media/storage-monitoring-diagnosing-troubleshooting/mma-screenshot-2.png
