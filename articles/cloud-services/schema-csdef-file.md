---
title: "Schéma de définition Microsoft Azure Cloud Services (fichier .csdef) | Microsoft Docs"
ms.custom: 
ms.date: 04/14/2015
ms.prod: azure
ms.reviewer: 
ms.service: cloud-services
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: b7735dbf-8e91-4d1b-89f7-2f17e9302469
caps.latest.revision: "42"
author: thraka
ms.author: adegeo
manager: timlt
ms.openlocfilehash: b833fdc06e4193c1b478028733c336feb6d8b9ba
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/11/2017
---
# <a name="azure-cloud-services-definition-schema-csdef-file"></a>Schéma de définition Microsoft Azure Cloud Services (fichier .csdef)
Le fichier de définition de service définit le modèle de service d’une application. Le fichier contient les définitions des rôles disponibles pour un service cloud, spécifie les points de terminaison de service et établit les paramètres de configuration du service. Les valeurs des paramètres de configuration sont définies dans le fichier de configuration de service, comme indiqué dans le [schéma de configuration de services cloud (classique)](http://msdn.microsoft.com/library/b1ae68cd-cc95-48cb-a4a4-da91dc708a35).

Par défaut, le fichier de schéma de configuration Azure Diagnostics est installé dans le répertoire `C:\Program Files\Microsoft SDKs\Windows Azure\.NET SDK\<version>\schemas`. Remplacez `<version>` par la version installée du [Kit de développement logiciel (SDK) Azure](http://www.windowsazure.com/develop/downloads/).

L’extension par défaut du fichier de définition de service est .csdef.

## <a name="basic-service-definition-schema"></a>Schéma de définition de service de base
Le fichier de configuration de service doit contenir un élément `ServiceDefinition`. La définition de service doit contenir au moins un élément de rôle (`WebRole` ou `WorkerRole`). Elle peut contenir jusqu’à 25 rôles définis dans une seule définition ; vous pouvez associer des types de rôles. La définition du service contient également l’élément facultatif `NetworkTrafficRules`, qui limite les rôles pouvant communiquer avec les points de terminaison internes spécifiés. La définition du service contient également l’élément facultatif `LoadBalancerProbes`, qui contient les sondes d’intégrité définies par les clients pour les points de terminaison.

Le format de base du fichier de définition de service se présente comme suit.

```xml
<ServiceDefinition name="<service-name>" topologyChangeDiscovery="<change-type>" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition" upgradeDomainCount="<number-of-upgrade-domains>" schemaVersion="<version>">
  
  <LoadBalancerProbes>
         …
  </LoadBalancerProbes>
  
  <WebRole …>
         …
  </WebRole>
  
  <WorkerRole …>
         …
  </WorkerRole>
  
  <NetworkTrafficRules>
         …
  </NetworkTrafficRules>

</ServiceDefinition>
```

## <a name="schema-definitions"></a>Définitions de schéma
Les rubriques suivantes décrivent le schéma :

- [Schéma LoadBalancerProbe](schema-csdef-loadbalancerprobe.md)
- [Schéma WebRole](schema-csdef-webrole.md)
- [Schéma WorkerRole](schema-csdef-workerrole.md)
- [Schéma NetworkTrafficRules](schema-csdef-networktrafficrules.md)

##  <a name="ServiceDefinition"></a> Élément ServiceDefinition
L’élément `ServiceDefinition` correspond à l’élément de niveau supérieur du fichier de définition de service.

Le tableau suivant décrit les attributs de l’élément `ServiceDefinition`.

| Attribut               | Description |
| ----------------------- | ----------- |
| name                    |Obligatoire. Nom du service. Ce nom doit être unique au sein du compte de service.|
| topologyChangeDiscovery | facultatif. Spécifie le type de notification de modification de la topologie. Les valeurs possibles sont les suivantes :<br /><br /> -   `Blast` : envoie la mise à jour à toutes les instances de rôle, dès que possible. Si vous choisissez l’option, le rôle doit être en mesure de gérer la mise à jour de la topologie sans devoir redémarrer.<br />-   `UpgradeDomainWalk` : envoie la mise à jour à chaque instance de rôle, de manière séquentielle, une fois que l’instance précédente a accepté la mise à jour.|
| schemaVersion           | facultatif. Spécifie la version du schéma de définition de service. La version du schéma permet à Visual Studio de sélectionner les outils du Kit de développement logiciel (SDK) appropriés à utiliser pour la validation du schéma, si plusieurs versions de ce Kit sont installées côte à côte.|
| upgradeDomainCount      | facultatif. Spécifie le nombre de domaines de mise à niveau sur lesquels les rôles de ce service sont alloués. Les instances de rôle sont allouées à un domaine de mise à niveau lorsque le service est déployé. Pour en savoir plus, voir [Mise à jour d’un rôle ou d’un déploiement de service cloud](cloud-services-how-to-manage-portal.md#how-to-update-a-cloud-service-role-or-deployment).<br /><br /> Vous pouvez spécifier jusqu’à 20 domaines de mise à niveau. Si aucune valeur n’est spécifiée, le nombre de domaines de mise à niveau par défaut est de 5.|