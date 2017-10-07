---
title: "journalisation de tooflow aaaIntroduction pour les groupes de sécurité réseau avec l’Observateur de réseau Azure | Documents Microsoft"
description: "Cette page explique comment les flux de groupe de sécurité réseau toouse connecte à une fonctionnalité de l’Observateur de réseau Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 47d91341-16f1-45ac-85a5-e5a640f5d59e
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: da85e946147b14717144cb47d1c742057c6dfa24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooflow-logging-for-network-security-groups"></a>Journalisation de tooflow de présentation pour les groupes de sécurité réseau

Journaux du groupe de sécurité réseau de flux sont une fonctionnalité de l’Observateur réseau qui vous permet de tooview d’informations sur le trafic IP entrant et sortant via un groupe de sécurité réseau. Ces flux de journaux est écrits au format json et affiche sortant des flux entrants sur une base par la règle, hello flux hello de carte réseau s’applique, 5-tuple d’informations sur le flux hello (protocole IP Source et de Destination, Port Source et de Destination) et si hello le trafic a été autorisé ou refusé.

![vue d’ensemble des journaux des flux][1]

Flux enregistre les groupes de sécurité réseau cible, ils ne sont pas affichés même hello comme hello autres journaux. Flux de journaux sont stockés uniquement dans un compte de stockage et le chemin d’accès de journalisation de hello suivant comme indiqué dans hello l’exemple suivant :

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

Hello même des stratégies de rétention comme sur les autres journaux appliquent les journaux de tooflow. Les journaux ont une stratégie de rétention peut être définie de jours too365 de 1 jour. Si une stratégie de rétention n’est pas définie, les journaux de hello sont conservées indéfiniment.

## <a name="log-file"></a>Fichier journal

Les journaux de flux ont plusieurs propriétés. Bonjour liste suivante est une liste de propriétés hello qui sont retournés dans le journal de flux de groupe de sécurité réseau hello :

* **heure** - temps lorsque hello événement a été enregistré
* **systemId** - L’ID de la ressource du groupe de sécurité réseau.
* **catégorie** -catégorie de hello d’événement de hello, il est toujours être NetworkSecurityGroupFlowEvent
* **ID de ressource** -hello Id de ressource de hello NSG
* **operationName** - Toujours NetworkSecurityGroupFlowEvents.
* **propriétés** -une collection de propriétés de flux de hello
    * **Version** -numéro de Version du schéma d’événement de flux de journal hello
    * **flow** - Une collection de flux. Cette propriété a plusieurs entrées pour différentes règles.
        * **règle** -règle pour le hello flux sont répertoriés
            * **flows** - Une collection de flux.
                * **Mac** -hello adresse MAC de hello NIC pour hello où les flux hello a été collecté de machine virtuelle
                * **flowTuples** -chaîne qui contient plusieurs propriétés pour le tuple de flux hello dans un format séparé par des virgules
                    * **Horodatage** -cette valeur est l’horodatage hello de lorsque les flux hello s’est produite dans le format de l’époque de UNIX
                    * **Adresse IP source** hello - adresse IP source
                    * **Destination IP** -hello IP de destination
                    * **Port source** hello - port source
                    * **Port de destination** -hello du Port de destination
                    * **Protocole** -hello protocole de flux de hello. Les valeurs valides sont **T** pour TCP et **U** pour UDP.
                    * **Flux de trafic** -hello direction hello du flux de trafic. Les valeurs valides sont **I** pour le trafic entrant et **O** pour le trafic sortant.
                    * **Traffic** - Indique si le trafic a été autorisé ou refusé. Les valeurs valides sont **A** pour autorisé et **D** pour refusé.


Hello Voici un exemple d’un flux de journal. Comme vous pouvez le voir, il existe plusieurs enregistrements qui suivent la liste de propriétés hello décrite dans hello précédant la section. 

> [!NOTE]
> Valeurs de propriété de flowTuples hello sont une liste séparée par des virgules.
 
```json
{
    "records": 
    [
        
        {
             "time": "2017-02-16T22:00:32.8950000Z",
             "systemId": "2c002c16-72f3-4dc5-b391-3444c3527434",
             "category": "NetworkSecurityGroupFlowEvent",
             "resourceId": "/SUBSCRIPTIONS/00000000-0000-0000-0000-000000000000/RESOURCEGROUPS/FABRIKAMRG/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/FABRIAKMVM1-NSG",
             "operationName": "NetworkSecurityGroupFlowEvents",
             "properties": {"Version":1,"flows":[{"rule":"DefaultRule_DenyAllInBound","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282421,42.119.146.95,10.1.0.4,51529,5358,T,I,D"]}]},{"rule":"UserRule_default-allow-rdp","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282370,163.28.66.17,10.1.0.4,61771,3389,T,I,A","1487282393,5.39.218.34,10.1.0.4,58596,3389,T,I,A","1487282393,91.224.160.154,10.1.0.4,61540,3389,T,I,A","1487282423,13.76.89.229,10.1.0.4,53163,3389,T,I,A"]}]}]}
        }
        ,
        {
             "time": "2017-02-16T22:01:32.8960000Z",
             "systemId": "2c002c16-72f3-4dc5-b391-3444c3527434",
             "category": "NetworkSecurityGroupFlowEvent",
             "resourceId": "/SUBSCRIPTIONS/00000000-0000-0000-0000-000000000000/RESOURCEGROUPS/FABRIKAMRG/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/FABRIAKMVM1-NSG",
             "operationName": "NetworkSecurityGroupFlowEvents",
             "properties": {"Version":1,"flows":[{"rule":"DefaultRule_DenyAllInBound","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282481,195.78.210.194,10.1.0.4,53,1732,U,I,D"]}]},{"rule":"UserRule_default-allow-rdp","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282435,61.129.251.68,10.1.0.4,57776,3389,T,I,A","1487282454,84.25.174.170,10.1.0.4,59085,3389,T,I,A","1487282477,77.68.9.50,10.1.0.4,65078,3389,T,I,A"]}]}]}
        }
        ,
        {
             "time": "2017-02-16T22:02:32.9040000Z",
             "systemId": "2c002c16-72f3-4dc5-b391-3444c3527434",
             "category": "NetworkSecurityGroupFlowEvent",
             "resourceId": "/SUBSCRIPTIONS/00000000-0000-0000-0000-000000000000/RESOURCEGROUPS/FABRIKAMRG/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/FABRIAKMVM1-NSG",
             "operationName": "NetworkSecurityGroupFlowEvents",
             "properties": {"Version":1,"flows":[{"rule":"DefaultRule_DenyAllInBound","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282492,175.182.69.29,10.1.0.4,28918,5358,T,I,D","1487282505,71.6.216.55,10.1.0.4,8080,8080,T,I,D"]}]},{"rule":"UserRule_default-allow-rdp","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282512,91.224.160.154,10.1.0.4,59046,3389,T,I,A"]}]}]}
        }
        ,
        ...
```

## <a name="next-steps"></a>Étapes suivantes

Découvrez comment tooenable flux se connecte en vous rendant sur [de flux de l’activation de la journalisation](network-watcher-nsg-flow-logging-portal.md).

Pour en savoir plus sur la journalisation du groupe de sécurité réseau, consultez [Analyse de journaux pour les groupes de sécurité réseau (NSG)](../virtual-network/virtual-network-nsg-manage-log.md).

Déterminez si le trafic est autorisé ou refusé sur une machine virtuelle en consultant [Vérifier si le trafic est autorisé ou refusé en direction ou en provenance d’une machine virtuelle avec le composant de vérification des flux IP d’Azure Network Watcher](network-watcher-check-ip-flow-verify-portal.md).

<!-- Image references -->
[1]: ./media/network-watcher-nsg-flow-logging-overview/figure1.png

