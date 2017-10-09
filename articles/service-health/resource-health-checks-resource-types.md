---
title: "aaaSupported des Types de ressources à l’intégrité des ressources Azure | Documents Microsoft"
description: Types de ressource pris en charge par Azure Resource Health
services: Resource health
documentationcenter: 
author: BernardoAMunoz
manager: 
editor: 
ms.assetid: 85cc88a4-80fd-4b9b-a30a-34ff3782855f
ms.service: service-health
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Supportability
ms.date: 03/19/2017
ms.author: BernardoAMunoz
ms.openlocfilehash: fc7bef214702f8ba6954b5aca62236b38023d27a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="resource-types-and-health-checks-in-azure-resource-health"></a>Types de ressources et les contrôles d’intégrité dans Azure Resource Health
Voici une liste complète de toutes les vérifications hello exécutées via l’intégrité des ressources par les types de ressources.

## <a name="microsoftcacheredisredis"></a>Microsoft.CacheRedis/Redis
|Vérifications exécutées|
|---|
|<ul><li>Sont tous les nœuds de Cache hello et en cours d’exécution ?</li><li>Hello du Cache est accessible à partir de dans le centre de données hello ?</li><li>A hello que cache atteint le nombre maximal de hello de connexions ?</li><li> Cache de hello épuisé sa mémoire disponible ? </li><li>Hello Cache rencontre un grand nombre de défauts de page ?</li><li>Est de hello Cache sous une charge importante ?</li></ul>|

## <a name="microsoftcdnprofile"></a>Microsoft.CDN/profile
|Vérifications exécutées|
|---|
|<ul> <li>Un des points de terminaison hello arrêté, supprimé ou mal configuré ?</li><li>Portail supplémentaire du hello n’est accessible pour les opérations de configuration CDN ?</li><li>Existe-t-il des problèmes de livraison continue avec hello points de terminaison CDN ?</li><li>Les utilisateurs peuvent modifier les configuration hello de leurs ressources CDN ?</li><li>Modifications de configuration sont propagées au taux de hello attendu ?</li><li>Les utilisateurs peuvent gérer les configuration de CDN hello utilisant hello portail Azure, PowerShell ou hello API ?</li> </ul>|

## <a name="microsoftclassiccomputevirtualmachines"></a>Microsoft.classiccompute/virtualmachines
|Vérifications exécutées|
|---|
|<ul><li>Est le serveur hôte de hello activé et en cours d’exécution ?</li><li>Démarrage du système d’exploitation hello hôte terminée ?</li><li>Conteneur d’ordinateur virtuel hello est configuré et sous tension ?</li><li>Existe-t-il une connectivité réseau entre les hôtes hello et compte de stockage hello ?</li><li>Hello le démarrage du système d’exploitation invité de hello terminée ?</li><li>Y a-t-il une maintenance planifiée régulière ?</li></ul>|

## <a name="microsoftcognitiveservicesaccounts"></a>Microsoft.cognitiveservices/accounts
|Vérifications exécutées|
|---|
|<ul><li>Compte de hello est accessible à partir de dans le centre de données hello ?</li><li>Est hello cognitifs fournisseur de ressources Services disponibles ?</li><li>Est hello cognitifs Service disponible dans la région de hello approprié ?</li><li>Peut lire les opérations effectuées sur le compte de stockage hello contenant les métadonnées des ressources hello ?</li><li>Quota d’appel hello API a été atteinte ?</li><li>Appel de hello API en lecture-limite a été atteinte ?</li></ul>|

## <a name="microsoftcomputevirtualmachines"></a>Microsoft.compute/virtualmachines
|Vérifications exécutées|
|---|
|<ul><li>Serveur de hello héberge cet ordinateur virtuel haut et en cours d’exécution ?</li><li>Démarrage du système d’exploitation hello hôte terminée ?</li><li>Conteneur d’ordinateur virtuel hello est configuré et sous tension ?</li><li>Existe-t-il une connectivité réseau entre les hôtes hello et compte de stockage hello ?</li><li>Hello le démarrage du système d’exploitation invité de hello terminée ?</li><li>Y a-t-il une maintenance planifiée régulière ?</li></ul>|

## <a name="microsoftdatalakeanalyticsaccounts"></a>Microsoft.datalakeanalytics/accounts
|Vérifications exécutées|
|---|
|<ul><li>Peuvent envoyer des travaux Analytique tooData Lake dans des utilisateurs hello région ?</li><li>Faire la région de hello exécution et terminé avec succès en projets de base ?</li><li>Les utilisateurs peuvent liste des éléments de catalogue dans la région de hello ?</li>|


## <a name="microsoftdatalakestoreaccounts"></a>Microsoft.datalakestore/accounts
|Vérifications exécutées|
|---|
|<ul><li>Les utilisateurs peuvent télécharger des tooData de data Lake Store dans une région de hello ?</li><li>Les utilisateurs peuvent télécharger des données de Data Lake Store dans une région de hello ?</li></ul>|

## <a name="microsoftdocumentdbdatabaseaccounts"></a>Microsoft.documentdb/databaseAccounts
|Vérifications exécutées|
|---|
|<ul><li>Toutes les demandes de base de données ou une collection non pris en charge en raison d’une indisponibilité de service tooa DocumentDB ont-elles été ?</li><li>Toutes les demandes de document non pris en charge en raison d’une indisponibilité de service tooa DocumentDB ont-elles été ?</li></ul>|

## <a name="microsoftnetworkconnections"></a>Microsoft.network/connections
|Vérifications exécutées|
|---|
|<ul><li>Tunnel VPN de hello est connecté ?</li><li>Existe-t-il des conflits de configuration de la connexion de hello ?</li><li>Les clés prépartagées hello sont correctement configurés ?</li><li>Appareil de hello VPN sur site n’est accessible ?</li><li>Existe-t-il des différences dans la stratégie de sécurité IPSec/IKE hello ?</li><li>Réseau VPN S2S hello n’est correctement configuré ou dans un état d’échec ?</li><li>Hello réseau à connexion est-elle correctement configuré ou dans un état d’échec ?</li></ul>|

## <a name="microsoftnetworkvirtualnetworkgateways"></a>Microsoft.network/virtualNetworkGateways
|Vérifications exécutées|
|---|
|<ul><li>Passerelle VPN de hello n’est accessible à partir de hello internet ?</li><li>Est de hello passerelle VPN en mode veille ?</li><li>Est-ce que hello service VPN est en cours d’exécution sur la passerelle hello ?</li></ul>|

## <a name="microsoftnotificationhubsnamespace"></a>Microsoft.NotificationHubs/namespace
|Vérifications exécutées|
|---|
|<ul><li> Opérations d’exécution, comme l’inscription, l’installation ou envoi peuvent être exécutées sur l’espace de noms hello ?</li></ul>|

## <a name="microsoftpowerbiworkspacecollections"></a>Microsoft.PowerBI/workspaceCollections
|Vérifications exécutées|
|---|
|<ul><li>Est un système d’exploitation hôte de hello activé et en cours d’exécution ?</li><li>Hello workspaceCollection n’est accessible à partir d’en dehors du centre de données hello ?</li><li>Est hello PowerBI fournisseur de ressources disponibles ?</li><li>Est hello PowerBI Service disponible dans la région de hello approprié ?</li></ul>|

## <a name="microsoftsearchsearchservices"></a>Microsoft.search/searchServices
|Vérifications exécutées|
|---|
|<ul><li>Opérations de diagnostics peuvent être exécutées sur le cluster de hello ?</li></ul>|

## <a name="microsoftsqlserverdatabase"></a>Microsoft.SQL/Server/database
|Vérifications exécutées|
|---|
|<ul><li> Base de données de connexions toohello ont-elles été ?</li></ul>|

## <a name="microsoftstreamanalyticsstreamingjobs"></a>Microsoft.StreamAnalytics/streamingjobs
|Vérifications exécutées|
|---|
|<ul><li>Sont tous les ordinateurs hôtes hello où le travail de hello est l’exécution des et en cours d’exécution ?</li><li>A été toostart impossible du travail hello ?</li><li>Y a-t-il des mises à niveau du runtime en cours ?</li><li>Est la tâche hello dans un état attendu (par exemple en cours d’exécution ou arrêté par le client) ?</li><li>A hello travail a rencontré des exceptions de mémoire insuffisante ?</li><li>Y a-t-il des mises à jour de calcul planifiées en cours ?</li><li>Est hello Gestionnaire d’exécution (plan de contrôle) disponibles ?</li></ul>|

## <a name="microsoftwebserverfarms"></a>Microsoft.web/serverFarms
|Vérifications exécutées|
|---|
|<ul><li>Est le serveur hôte de hello activé et en cours d’exécution ?</li><li>Internet Information Services (IIS) est-il en cours d’exécution ?</li><li>Équilibrage de charge hello est en cours d’exécution ?</li><li>Hello Plan de Service Web peut être atteint à partir de dans le centre de données hello ?</li><li>Est disponible hello stockage hébergement hello sites le contenu du compte de batterie de serveurs hello ??</li></ul>|

## <a name="microsoftwebsites"></a>Microsoft.web/sites
|Vérifications exécutées|
|---|
|<ul><li>Est le serveur hôte de hello activé et en cours d’exécution ?</li><li>Le serveur Internet Information est-il en cours d’exécution ?</li><li>Équilibrage de charge hello est en cours d’exécution ?</li><li>Hello application Web peut être atteint à partir de dans le centre de données hello ?</li><li>Compte de stockage hello héberge le contenu de site hello disponible ?</li></ul>|

# <a name="next-steps"></a>Étapes suivantes
-  Consultez [Introduction tooAzure l’intégrité du Service](service-health-overview.md) et [Introduction tooAzure l’intégrité des ressources](resource-health-overview.md) toounderstand plus à leur sujet. 
-  [Forum aux questions sur Azure Resource Health](resource-health-faq.md)
- Configurez des alertes afin d’être averti des problèmes d’intégrité. Pour plus d’informations sur la configuration d’alertes pour Service Health, consultez [cet article](../monitoring-and-diagnostics/monitoring-activity-log-alerts-on-service-notifications.md). 