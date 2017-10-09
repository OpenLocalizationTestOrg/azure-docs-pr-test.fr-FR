---
title: "vue d’ensemble du moniteur d’aaaAzure | Documents Microsoft"
description: "Azure Monitor collecte des statistiques qui peuvent être utilisées dans les alertes, les webhooks, la mise à l’échelle automatique et l’automatisation. L’article liste également les autres options de surveillance de Microsoft."
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/12/2017
ms.author: robb
ms.openlocfilehash: ffa304e7b158f0fceb7f60ab88fab291976aa0e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-azure-monitor"></a>Vue d’ensemble d’Azure Monitor
Cet article fournit une vue d’ensemble de hello service Moniteur de Windows Azure dans Microsoft Azure. Il décrit ce que fait moniteur de Windows Azure et fournit des pointeurs tooadditional plus d’informations sur la façon de toouse moniteur de Windows Azure.  Si vous préférez une vidéo de présentation, consultez les liens étapes suivants en bas de hello de cet article. 

## <a name="why-monitor-your-application-or-system"></a>Pourquoi surveiller votre application ou système
Les applications cloud sont complexes, et se composent de nombreux éléments mobiles. L’analyse fournit des données tooensure que votre application reste opérationnel et en cours d’exécution dans un état sain. Cela permet également vous toostave désactivé des problèmes potentiels ou de dépanner au-delà de celles. En outre, vous pouvez utiliser l’analyse données toogain des informations détaillées relatives à votre application. Ces connaissances peuvent vous aider à tooimprove des performances des applications ou facilité de maintenance, ou automatiser des actions qui nécessiteraient sinon une intervention manuelle.


## <a name="azure-monitor-and-microsofts-other-monitoring-products"></a>Azure Monitor et autres produits de surveillance de Microsoft
Azure Monitor fournit des métriques de niveau de base d’infrastructure et des journaux pour la plupart des services Microsoft Azure. Services Azure que vous ne placez pas encore de leurs données dans le moniteur de Windows Azure seront placer Bonjour futures.

Microsoft libre des produits et services supplémentaires qui fournissent de nouvelles fonctionnalités de surveillance pour les développeurs, DevOps ou opérateurs informatiques qui ont également des installations locales. Pour une vue d’ensemble et mieux comprendre comment ces différents produits et services fonctionnent ensemble, consultez [Surveillance dans Microsoft Azure](monitoring-overview.md).

## <a name="monitoring-sources---compute"></a>Sources d’analyse - Calcul

![Modèle pour l’analyse et le diagnostic pour les ressources non liées au calcul](./media/monitoring-overview-azure-monitor/Monitoring_Azure_Resources-compute_v6.png)

incluent des services de calcul Hello 
- Services cloud 
- Machines virtuelles 
- Jeux de mise à l’échelle de machine virtuelle 
- Service Fabric

### <a name="application---diagnostics-logs-application-logs-and-metrics"></a>Application - Journaux de diagnostic, journaux d’Application et métriques
Applications peuvent être exécutées sur hello du système d’exploitation invité dans un modèle de calcul hello. Elles émettent leur propre ensemble de journaux et de métriques. Moniteur de Azure s’appuie sur hello Azure diagnostics extension (Windows ou Linux) toocollect la plupart des métriques de niveau application et les journaux. incluent des types de Hello

* Compteurs de performances
* Journaux d’application
* Journaux des événements Windows
* .NET EventSource
* Journaux IIS
* ETW basé sur les manifestes
* Vidages sur incident
* Journaux d'erreurs client

Sans l’extension de diagnostics hello, seules quelques métriques telles que l’utilisation du processeur sont disponibles. 

### <a name="host-and-guest-vm-metrics"></a>Métriques d’hôte et machine virtuelle invitée
Hello ressources de calcul précédemment répertoriés ont un hôte dédié machine virtuelle et l’invité du système d’exploitation qu’ils interagissent avec. machine virtuelle d’hôte Hello et de système d’exploitation invité sont équivalent hello de racine de l’ordinateur virtuel et l’ordinateur virtuel invité dans le modèle d’hyperviseur hello Hyper-V. Vous pouvez collecter des métriques sur les deux. Vous pouvez également collecter les journaux de diagnostic sur le système d’exploitation invité de hello.   

### <a name="activity-log"></a>Journal d’activité
Vous pouvez rechercher hello journal d’activité (précédemment appelé opérationnelle ou les journaux d’Audit) pour plus d’informations sur votre ressource, comme indiqué par hello infrastructure Azure. journal de Hello contient des informations comme les heures lorsque les ressources sont créées ou détruites.  Pour plus d’informations, voir [Présentation du journal d’activité](monitoring-overview-activity-logs.md). 

## <a name="monitoring-sources---everything-else"></a>Surveillance des sources - Tout le reste

![Modèle pour l’analyse et le diagnostic pour les ressources liées au calcul](./media/monitoring-overview-azure-monitor/Monitoring_Azure_Resources-non-compute_v6.png)


### <a name="resource---metrics-and-diagnostics-logs"></a>Ressources - Métriques et journaux de diagnostics
Des journaux de diagnostics et de métriques SINV à regrouper varient selon le type de ressource hello. Par exemple, les applications Web fournit des statistiques sur hello e/s disque et % de l’UC. Ces métriques n’existent pas pour une file d’attente Service Bus, qui fournit à la place des métriques telles que la taille de la file d’attente et le débit des messages. Une liste des métriques actuellement collectables pour chaque ressource est disponible sur [Mesures prises en charge](monitoring-supported-metrics.md). 

### <a name="host-and-guest-vm-metrics"></a>Métriques d’hôte et machine virtuelle invitée
Le routage 1:1 entre votre ressource et un hôte ou une machine virtuelle invitée spécifique n’est pas systématiquement appliqué, les métriques ne sont donc pas disponibles.

### <a name="activity-log"></a>Journal d’activité
journal d’activité Hello est hello identique pour les ressources de calcul.  

## <a name="uses-for-monitoring-data"></a>Utilisations de l’analyse de données
Une fois que vous collectez vos données, vous pouvez effectuer hello suivant avec celui-ci dans le moniteur de Azure

### <a name="route"></a>Routage
Vous pouvez diffuser des emplacements tooother analyse des données en temps réel.

Voici quelques exemples :

- Envoyer tooApplication Insights afin de pouvoir utiliser ses outils de visualisation et d’analyse plus riches.
- Envoyez des concentrateurs de tooEvent afin que vous pouvez acheminer des outils tiers toothird. 

### <a name="store-and-archive"></a>Stockage et archivage
Certaines données de surveillance sont déjà disponibles dans Azure Monitor et enregistrées pendant un laps de temps défini. 
- Les métriques sont stockées pendant 30 jours. 
- Les entrées de journal d’activité sont conservées pendant 90 jours. 
- Les journaux de diagnostic ne sont pas stockés du tout. 

Si vous souhaitez que les données toostore plues de hello périodes répertoriés ci-dessus, vous pouvez utiliser un stockage Azure. Les données de surveillance sont conservées dans votre compte de stockage sur la base d’une stratégie de rétention que vous définissez. Vous n’avez pas toopay pour hello d’espace hello données occupent dans le stockage Azure. 

Quelques façons toouse ces données :

- Une fois les données écrites, vous pouvez les lire et les traiter à l’aide d’outils internes ou externes à Azure.
- Télécharger des données hello localement pour un archivage local ou de modifier votre stratégie de rétention de données de tookeep hello cloud pour de longues périodes.  
- Vous laisser les données de salutation dans le stockage Azure indéfiniment à des fins d’archivage. 

### <a name="query"></a>Interroger
Vous pouvez utiliser hello API REST de Azure moniteur, commandes d’Interface de ligne de commande (CLI) inter-plateformes, les applets de commande PowerShell ou hello .NET SDK tooaccess hello des données dans le système de hello ou le stockage Azure

Voici quelques exemples :

* Obtention de données pour une application d’analyse personnalisée que vous avez écrite
* Création de requêtes personnalisées et l’envoi de cette application de tiers de tooa de données.

### <a name="visualize"></a>Visualisation
Visualiser vos données dans les graphiques et les diagrammes d’analyse permet de rechercher des tendances plus rapide que la recherche dans les données hello lui-même.  

Il existe quelques méthodes de visualisation, qui sont les suivantes :

* Utilisez hello portail Azure
* Itinéraire données tooAzure Application Insights
* Itinéraire données tooMicrosoft Power BI
* L’itinéraire hello données tooa tiers visualisation outil à l’aide de la diffusion en continu ou à un outil de hello lire à partir d’une archive dans le stockage Azure


### <a name="automate"></a>Automatisation
Vous pouvez utiliser les alertes d’analyse données tootrigger ou même tous les processus. Voici quelques exemples :

* Utilisez des instances de calcul tooautoscale données vers le haut ou vers le bas en fonction de la charge de l’application.
* Envoi de messages électroniques lorsqu’une mesure dépasse un seuil prédéfini.
* Appeler un tooexecute d’URL (webhook) web d’une action dans un système en dehors d’Azure
* Démarrer un runbook dans Azure automation tooperform un large éventail de tâches

## <a name="methods-of-accessing-azure-monitor"></a>Méthodes d’accès à Azure Monitor
En règle générale, vous pouvez manipuler le suivi des données, le routage et la récupération à l’aide d’une des méthodes suivantes de hello. Toutes les méthodes ne sont pas disponibles pour toutes les actions ou tous les types de données.

* [Portail Azure](https://portal.azure.com)
* [PowerShell](insights-powershell-samples.md)  
* [Interface de ligne de commande interplateforme (CLI)](insights-cli-samples.md)
* [API REST](https://docs.microsoft.com/rest/api/monitor/)
* [Kit SDK .NET](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor)

## <a name="next-steps"></a>Étapes suivantes
En savoir plus sur
- Une vidéo de procédure pas à pas uniquement pour Azure Monitor est disponible à l’adresse  
[Prise en main d’Azure Monitor](https://channel9.msdn.com/Blogs/Azure-Monitoring/Get-Started-with-Azure-Monitor). Une vidéo supplémentaire décrivant un scénario dans lequel vous pouvez utiliser Azure Monitor est disponible sur [Découvrir Microsoft Azure Monitoring et Diagnostic](https://channel9.msdn.com/events/Ignite/2016/BRK2234) et [Azure Monitor dans une vidéo de l’Ignite 2016](https://myignite.microsoft.com/videos/4977)
- Exécuter via l’interface du moniteur de Windows Azure hello dans [mise en route avec l’Analyseur de Azure](monitoring-get-started.md)
- Configurer hello [Extensions de diagnostic Azure](../azure-diagnostics.md) si vous essayez de toodiagnose des problèmes dans votre Service Cloud, l’ordinateur virtuel, ordinateur virtuel à l’échelle jeux, ou une application de Service Fabric.
- [Application Insights](https://azure.microsoft.com/documentation/services/application-insights/) si vous essayez de toodiagnostic des problèmes dans votre application de Service Web de l’application.
- [Résolution des problèmes du stockage Azure](../storage/common/storage-e2e-troubleshooting.md) lorsque vous utilisez le stockage d’objets blob, de tables ou de files d’attente
- [Ouvrez une session Analytique](https://azure.microsoft.com/documentation/services/log-analytics/) et hello [Operations Management Suite](https://www.microsoft.com/oms/)
