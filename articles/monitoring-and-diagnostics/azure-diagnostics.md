---
title: aaaOverview des Diagnostics Azure | Documents Microsoft
description: "Utilisation des diagnostics Azure pour le débogage, la mesure des performances, la surveillance, l’analyse du trafic dans Cloud Services, Virtual Machines et Service Fabric"
services: multiple
documentationcenter: .net
author: rboucher
manager: 
editor: 
ms.assetid: baad40d8-c915-4f93-b486-8b160bf33463
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/18/2017
ms.author: robb
ms.openlocfilehash: 2a03a96a37091894d7ab16120c125116e4bf462a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-diagnostics"></a>Que sont les diagnostics Azure ?
Les Diagnostics Azure sont fonction hello dans Azure qui active la collecte de hello de données de diagnostic sur une application déployée. Vous pouvez utiliser l’extension de diagnostics hello provenant de sources différentes. Les sources actuellement prises en charge sont les rôles Web et les rôles de travail Azure Cloud Service, Azure Virtual Machines sous Microsoft Windows et Service Fabric. Les autres services Azure ont leurs propres diagnostics distincts.

## <a name="data-you-can-collect"></a>Données que vous pouvez collecter
Azure Diagnostics peut collecter hello les types de données suivants :

| source de données | Description |
| --- | --- |
| Compteurs de performances |Système d’exploitation et compteurs de performances personnalisés |
| Journaux d’application |Messages de trace écrits par votre application |
| Journaux d’événements Windows |Informations envoyées du système de journalisation des événements Windows toohello |
| .NET EventSource |Code de l’écriture d’événements à l’aide de hello .NET [EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) classe |
| Journaux IIS |Informations au sujet des sites Web IIS |
| ETW basé sur les manifestes |Événements de suivi d’événements pour Windows générés par n’importe quel processus |
| Vidages sur incident |Informations sur l’état hello du processus hello dans les événements hello d’incident d’application |
| Journaux d'erreurs personnalisés |Journaux créés par votre application ou service |
| Journaux d’infrastructure Azure Diagnostic |Informations au sujet des diagnostics eux-mêmes |

Hello extension Azure diagnostics peut transférer cette tooan données compte de stockage Azure ou envoyez-le tooservices comme [Application Insights](../application-insights/app-insights-cloudservices.md). Vous pouvez utiliser les données de salutation pour le débogage et dépannage de mesurer les performances, l’utilisation des ressources, analyse du trafic et planification des capacités d’analyse et l’audit.

## <a name="versioning"></a>Contrôle de version
Voir [Historique de contrôle de version des diagnostics Azure](azure-diagnostics-versioning-history.md).

## <a name="next-steps"></a>Étapes suivantes
Choisissez le service qui vous essayez de toocollect diagnostics et utiliser hello suivant tooget articles a démarré. Utilisez les liens de diagnostics Azure généraux de hello de référence pour des tâches spécifiques.

## <a name="web-apps"></a>Web Apps
Notez que Web Apps n'utilise pas les diagnostics Azure. Savoir hello équivalent à [Web Apps](../app-service-web/web-sites-enable-diagnostic-log.md)

## <a name="cloud-services-using-azure-diagnostics"></a>Cloud Services avec les diagnostics Azure
* Si vous utilisez Visual Studio, consultez [utilisez Visual Studio tootrace une application de Services de cloud computing](../vs-azure-tools-debug-cloud-services-virtual-machines.md) tooget a démarré. Sinon, voir
* [Comment toomonitor Cloud services à l’aide des Diagnostics Windows Azure](../cloud-services/cloud-services-how-to-monitor.md)
* [Configuration des diagnostics Azure dans une application Cloud Services](../cloud-services/cloud-services-dotnet-diagnostics.md)

Pour des rubriques plus avancées, voir

* [Utilisation des diagnostics avec Application Insights pour Cloud Services](../application-insights/app-insights-cloudservices.md)
* [Flux de hello de trace d’une application de Services de Cloud avec Azure Diagnostics](../cloud-services/cloud-services-dotnet-diagnostics-trace-flow.md)
* [Utilisez tooset PowerShell des diagnostics sur les Services Cloud](../virtual-machines/windows/ps-extensions-diagnostics.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="virtual-machines-using-azure-diagnostics"></a>Virtual Machines avec les diagnostics Azure
* Si vous utilisez Visual Studio, consultez [utilisez Visual Studio tootrace des Machines virtuelles Azure](../vs-azure-tools-debug-cloud-services-virtual-machines.md) tooget a démarré. Sinon, voir
* [Configurer les diagnostics Azure sur une machine virtuelle Azure](../virtual-machines-dotnet-diagnostics.md)

Pour des rubriques plus avancées, voir

* [Utilisez tooset PowerShell des diagnostics sur des Machines virtuelles Azure](../virtual-machines/windows/ps-extensions-diagnostics.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Créer une machine virtuelle Windows avec des fonctionnalités de surveillance et de diagnostics à l’aide d’un modèle Azure Resource Manager](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="service-fabric-using-azure-diagnostics"></a>Service Fabric avec les diagnostics Azure
Commencez avec [Surveillance d’une application Service Fabric](../service-fabric/service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md). De nombreux autres articles de diagnostics Service Fabric sont disponibles dans l’arborescence de navigation hello sur hello gauche une fois que vous avez toothis article.

## <a name="general-azure-diagnostics-articles"></a>Articles généraux sur les diagnostics Azure
* [Configuration de schéma Azure Diagnostics](https://msdn.microsoft.com/library/azure/mt634524.aspx) : Découvrez comment toochange hello toocollect de fichier de schéma et de router les données de diagnostic. Notez que vous pouvez également utiliser un fichier de schéma de Visual Studio toochange hello.
* [Stockage des données de Diagnostics Azure dans le stockage Azure](../cloud-services/cloud-services-dotnet-diagnostics-storage.md) -connaître hello les noms des tables de hello et des objets BLOB où les données de diagnostic hello sont écrit.
* En savoir trop[utiliser des compteurs de Performance dans les Diagnostics Azure](../cloud-services/cloud-services-dotnet-diagnostics-performance-counters.md).
* En savoir trop[tooApplication informations de diagnostics itinéraire Azure Insights](azure-diagnostics-configure-application-insights.md)
* Si vous rencontrez des difficultés avec le lancement des diagnostics ou la recherche des données dans les tables de stockage Azure, consultez [Résolution des problèmes des diagnostics Azure](azure-diagnostics-troubleshooting.md)
