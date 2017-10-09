---
title: "aaaIntroduction tooAzure Observateur réseau | Documents Microsoft"
description: "Cette page fournit une vue d’ensemble de hello service Observateur réseau pour l’analyse et la visualisation connecté ressources dans Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 14bc2266-99e3-42a2-8d19-bd7257fec35e
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/11/2017
ms.author: gwallace
ms.openlocfilehash: 283b3fa6add05d9bad6d5dbdae1524344d1bfc7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-network-monitoring-overview"></a>Vue d’ensemble de la surveillance réseau Azure

Les clients créent un réseau de bout en bout dans Azure en orchestrant et composant diverses ressources réseau telles qu’un réseau virtuel, ExpressRoute, Application Gateway, des équilibrages de charge, etc. Analyse est disponible sur chacune des ressources du réseau hello. Nous nous référons toothis surveillance surveillance au niveau des ressources.

réseau tooend Hello peut avoir des configurations complexes et les interactions entre les ressources, créer des scénarios complexes qui doivent basée sur un scénario d’analyse via l’Observateur réseau.

Cet article présente la surveillance au niveau des ressources et la surveillance basée sur des scénarios. La surveillance réseau dans Azure est complète et couvre deux grandes catégories :

* [**Observateur de réseau** ](#network-watcher) -surveillance basée sur un scénario est fourni avec les fonctions hello dans l’Observateur réseau. Ce service inclut la capture de paquets, le tronçon saut suivant, la vérification des flux IP, l’affichage de groupe de sécurité, les journaux de flux de groupe de sécurité réseau. Surveillance au niveau du scénario présente une fin tooend des ressources réseau dans l’analyse de ressource contraste tooindividual réseau.
* [**Surveillance des ressources**](#network-resource-level-monitoring) - La surveillance au niveau des ressources se compose de quatre fonctionnalités : journaux de diagnostic, mesures, résolution des problèmes et intégrité des ressources. Toutes ces fonctionnalités sont créées au niveau de ressources réseau hello.

## <a name="network-watcher"></a>Network Watcher

Observateur réseau est un service régional qui permet de vous toomonitor et diagnostiquer des conditions à un niveau de scénario réseau, vers et depuis Azure. Diagnostic de réseau et les outils de visualisation disponibles avec l’Observateur réseau vous aider à comprendre, de diagnostiquer et de mieux réseau de tooyour insights dans Azure.

Observateur réseau a actuellement hello suivant de fonctionnalités :

* **[Topologie](network-watcher-topology-overview.md)**  -fournit un Bonjour montrant de vue de niveau réseau différents interconnexions et les associations entre les ressources réseau dans un groupe de ressources.
* **[Capture de paquets variables](network-watcher-packet-capture-overview.md)** - Capture des données de paquets dans et en dehors d’une machine virtuelle. Advanced options de filtrage et des contrôles ajustées par exemple, tooset en mesure de temps et les limitations de taille fournissent des raisons de souplesse. données de paquet de Hello peuvent être stockées dans un magasin d’objets blob ou sur le disque local dans un format de .cap hello.
* **[Vérification des flux IP](network-watcher-ip-flow-verify-overview.md)** - Vérifie si un paquet est autorisé ou refusé en fonction des paramètres de paquet des informations à 5 tuples de flux (adresse IP de destination, adresse IP source, port de destination, port source et protocole). Si les paquets hello sont refusée par un groupe de sécurité, hello règle et groupe qui a refusé les paquets hello est retournée.
* **[Tronçon suivant](network-watcher-next-hop-overview.md)**  -détermine le saut suivant de hello pour les paquets routés Bonjour Azure Fabric de réseau, ce qui vous les itinéraires toodiagnose toute mauvaise configuration définie par l’utilisateur.
* **[Affichage de groupe de sécurité](network-watcher-security-group-view-overview.md)**  -Obtient les règles de sécurité efficace et appliquées hello qui sont appliquées sur une machine virtuelle.
* **[Enregistrement de flux de groupe de sécurité réseau](network-watcher-nsg-flow-logging-overview.md)**  -journaux de flux pour les groupes de sécurité réseau permettent de tootraffic connexes toocapture journaux qui sont autorisés ou refusés par des règles de sécurité hello dans le groupe de hello. flux de Hello est défini par une 5-tuple d’informations : l’adresse IP Source, adresse IP de Destination, Port Source, le Port de Destination et protocole.
* **[Passerelle de réseau virtuel et la résolution des problèmes de connexion](network-watcher-troubleshoot-manage-rest.md)**  -hello capacité tootroubleshoot fournit des connexions et des passerelles de réseau virtuel.
* **[Limites de l’abonnement du réseau](#network-subscription-limits)**  -vous permet de l’utilisation des ressources réseau tooview par rapport aux limites.
* **[Configuration du journal de diagnostic](#diagnostic-logs)**  – fournit un tooenable un seul volet ou désactivez des journaux de Diagnostics pour les ressources réseau dans un groupe de ressources.
* **[Connectivité (version préliminaire)](network-watcher-connectivity-overview.md)**  -vérifie la possibilité de hello d’établir une connexion TCP directe à partir d’un tooa de machine virtuelle donné du point de terminaison.

### <a name="role-based-access-control-rbac-in-network-watcher"></a>Contrôle d’accès basé sur les rôles dans Network Watcher

Observateur réseau utilise hello [modèle de contrôle d’accès du (RBAC)](../active-directory/role-based-access-control-what-is.md). Hello les autorisations suivantes est requises par hello Observateur réseau. Il est important toomake que ce rôle hello utilisé pour initialiser l’API de l’Observateur réseau ou à l’aide de l’Observateur de réseau à partir du portail de hello a accès de hello requis.

|Ressource| Autorisation|
|---|---| 
|Microsoft.Storage/ |Lire|
|Microsoft.Authorization/| Lire| 
|Microsoft.Resources/subscriptions/resourceGroups/| Lire|
|Microsoft.Storage/storageAccounts/listServiceSas/ | Action|
|Microsoft.Storage/storageAccounts/listAccountSas/ |Action|
|Microsoft.Storage/storageAccounts/listKeys/ | Action|
|Microsoft.Compute/virtualMachines/ |Lire|
|Microsoft.Compute/virtualMachines/ |Écrire|
|Microsoft.Compute/virtualMachineScaleSets/ |Lire|
|Microsoft.Compute/virtualMachineScaleSets/ |Écrire|
|Microsoft.Network/networkWatchers/packetCaptures/ |Lire|
|Microsoft.Network/networkWatchers/packetCaptures/| Écrire|
|Microsoft.Network/networkWatchers/packetCaptures/| Supprimer|
|Microsoft.Network/networkWatchers/ |Écrire |
|Microsoft.Network/networkWatchers/| Lire |
|Microsoft.Insights/alertRules/ |*|
|Microsoft.Support/ | *|

### <a name="network-subscription-limits"></a>Limites d’abonnement réseau

Limites d’abonnement de réseau vous permet de fournir des détails d’utilisation hello de chacune des ressources du réseau hello dans un abonnement dans une région de nombre maximal de hello des ressources disponibles.

![limite d’abonnement réseau][nsl]

## <a name="network-resource-level-monitoring"></a>Surveillance au niveau des ressources réseau

Hello suivant les fonctionnalités est disponible pour l’analyse au niveau des ressources :

### <a name="audit-log"></a>Journal d’audit

Opérations effectuées dans le cadre de la configuration de hello des réseaux sont enregistrées. Ces journaux peuvent être consultées dans hello portail Azure ou récupérées à l’aide des outils de Microsoft, telles que Power BI ou des outils tiers. Journaux d’audit sont disponibles via le portail de hello, PowerShell, CLI et les API Rest. Pour plus d’informations sur les journaux d’audit, consultez [Afficher les journaux d’activité pour auditer les actions sur les ressources](../resource-group-audit.md).

Les journaux d’audit sont disponibles pour les opérations effectuées sur toutes les ressources réseau.

### <a name="metrics"></a>Mesures

Les mesures sont des indicateurs et des compteurs de performances collectés sur une période donnée. Les mesures sont disponibles pour Application Gateway. Métriques peuvent être des alertes tootrigger utilisé selon le seuil. Consultez [Application Diagnostics de passerelle](../application-gateway/application-gateway-diagnostics.md) tooview comment les métriques peuvent être utilisés toocreate alertes.

![affichage des mesures][metrics]

### <a name="diagnostic-logs"></a>Journaux de diagnostic

Événements périodiques et spontanées sont créées par les ressources réseau et enregistrées dans les comptes de stockage, envoyés tooan concentrateur d’événements ou Analytique de journal. Ces journaux fournissent des analyses d’intégrité de hello d’une ressource. Ces journaux peuvent être affichés dans des outils tels que Power BI et Log Analytics. toolearn comment tooview journaux de diagnostic, visitez [Analytique de journal](../log-analytics/log-analytics-azure-networking-analytics.md).

Les journaux de diagnostic sont disponibles pour [l’équilibrage de charge](../load-balancer/load-balancer-monitor-log.md), [les groupes de sécurité réseau](../virtual-network/virtual-network-nsg-manage-log.md), les itinéraires, et [Application Gateway](../application-gateway/application-gateway-diagnostics.md).

Network Watcher permet d’afficher les journaux de diagnostic. Cet affichage contient toutes les ressources réseau qui prennent en charge la journalisation des diagnostics. À partir de celui-ci, vous pouvez activer et désactiver les ressources réseau facilement et rapidement.

![journaux][logs]

### <a name="troubleshooting"></a>Résolution des problèmes

Hello panneau, une expérience dans le portail hello, de résolution des problèmes est fourni sur les ressources réseau aujourd'hui toodiagnose les problèmes courants associés à une ressource individuelle. Cette expérience est disponible pour hello suivant des ressources réseau - ExpressRoute, passerelle VPN, passerelle d’Application, les journaux de sécurité réseau, itinéraires, DNS, équilibrage de charge et Traffic Manager. toolearn savoir plus sur la ressource de la résolution des problèmes au niveau, visitez [diagnostiquer et résoudre les problèmes avec la résolution des problèmes de Azure](https://azure.microsoft.com/blog/azure-troubleshoot-diagonse-resolve-issues/)

![informations sur la résolution des problèmes][TS]

### <a name="resource-health"></a>Intégrité des ressources

contrôle d’intégrité Hello d’une ressource réseau est fourni sur une base périodique. Ces ressources incluent la passerelle VPN et le tunnel VPN. L’intégrité des ressources est accessible sur hello portail Azure. toolearn en savoir plus sur l’intégrité des ressources, visitez [vue d’ensemble du contrôle d’intégrité de ressource](../resource-health/resource-health-overview.md)

## <a name="next-steps"></a>Étapes suivantes

Après avoir découvert Network Watcher, vous pouvez apprendre à :

Effectuez une capture de paquets sur votre machine virtuelle en vous rendant sur [capture des paquets Variable Bonjour portail Azure](network-watcher-packet-capture-manage-portal.md)

Mener une surveillance et faire des diagnostics de manière proactive à l’aide [des captures de paquets déclenchées par des alertes](network-watcher-alert-triggered-packet-capture.md).

Détecter les vulnérabilités de sécurité avec [l’analyse des captures des paquets au moyen de Wireshark](network-watcher-deep-packet-inspection.md), à l’aide d’outils open source.

En savoir plus sur certaines des hello autre clé [fonctionnalités de réseau](../networking/networking-overview.md) de Azure.

<!--Image references-->
[TS]: ./media/network-watcher-monitoring-overview/troubleshooting.png
[logs]: ./media/network-watcher-monitoring-overview/logs.png
[metrics]: ./media/network-watcher-monitoring-overview/metrics.png
[nsl]: ./media/network-watcher-monitoring-overview/nsl.png











