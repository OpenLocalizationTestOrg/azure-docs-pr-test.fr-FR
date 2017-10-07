---
title: "aaaMonitor opérations, les événements et les compteurs pour les groupes de sécurité réseau | Documents Microsoft"
description: "Découvrez comment tooenable compteurs, événements et la journalisation opérationnelle pour les groupes de sécurité réseau"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 2e699078-043f-48bd-8aa8-b011a32d98ca
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/31/2017
ms.author: jdial
ms.openlocfilehash: f16f1a0ad693028ee7aba21574b5c8ddfcd27096
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-for-network-security-groups-nsgs"></a>Analyse de journaux pour les groupes de sécurité réseau (NSG)

Vous pouvez activer hello suivant des catégories du journal de diagnostic pour les groupes de sécurité réseau :

* **Événement :** contient des entrées pour le groupe de sécurité réseau, les règles sont tooVMs appliqués et les rôles d’instance en fonction de l’adresse MAC. état Hello pour ces règles est collecté toutes les 60 secondes.
* **Compteur de règle :** contient des entrées pour le nombre de fois où chaque groupe de sécurité réseau de règles est appliqué toodeny ou autoriser le trafic.

> [!NOTE]
> Journaux de diagnostic sont uniquement disponibles pour les groupes de sécurité réseau déployés via le modèle de déploiement du Gestionnaire de ressources Azure hello. Vous ne pouvez pas activer la journalisation des diagnostics pour les groupes de sécurité réseau déployés via le modèle de déploiement classique hello. Pour mieux comprendre les modèles hello deux, référence hello [modèles de déploiement Azure de présentation](../resource-manager-deployment-model.md) l’article.

La journalisation des activités (anciennement appelée audit ou journaux des opérations) est activé par défaut pour les groupes de sécurité réseau créés via un modèle de déploiement d’Azure. toodetermine quelles opérations ont été effectuées sur les groupes de sécurité réseau dans le journal d’activité hello, recherchez les entrées qui contiennent le hello les types de ressources suivants : 

- Microsoft.ClassicNetwork/networkSecurityGroups 
- Microsoft.ClassicNetwork/networkSecurityGroups/securityRules
- Microsoft.Network/networkSecurityGroups
- Microsoft.Network/networkSecurityGroups/securityRules 

Hello de lecture [vue d’ensemble du journal des activités Azure de hello](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md) toolearn article plus d’informations sur les journaux d’activité. 

## <a name="enable-diagnostic-logging"></a>Activer la journalisation des diagnostics

Journalisation des diagnostics doit être activée pour *chaque* groupe de sécurité réseau que vous voulez toocollect de données pour. Hello [vue d’ensemble de Azure des journaux de Diagnostic](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) explique où les journaux de diagnostic peuvent être envoyés. Si vous n’avez pas un groupe de sécurité réseau existant, hello terminé les étapes Bonjour [créer un groupe de sécurité réseau](virtual-networks-create-nsg-arm-pportal.md) toocreate article un. Vous pouvez activer le groupe de sécurité réseau diagnostic journalisation à l’aide d’une des méthodes suivantes de hello :

### <a name="azure-portal"></a>Portail Azure

journalisation de portail tooenable toouse hello, connexion toohello [portal](https://portal.azure.com). Cliquez sur **Plus de services**, puis tapez *groupes de sécurité réseau*. Sélectionnez hello NSG souhaité tooenable journalisation pour. Suivez les instructions de hello pour les ressources de calcul non Bonjour [activer les journaux de diagnostic dans le portail de hello](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) l’article. Sélectionnez **NetworkSecurityGroupEvent**, **NetworkSecurityGroupRuleCounter**, ou les deux catégories de journaux.

### <a name="powershell"></a>PowerShell

tooenable de PowerShell toouse journalisation, suivez les instructions de hello Bonjour [activer les journaux de diagnostic via PowerShell](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) l’article. Évaluer hello informations avant d’entrer une commande à partir de l’article de hello suivantes :

- Vous pouvez déterminer toouse de valeur hello pour hello `-ResourceId` paramètre en remplaçant hello suivant [texte], si nécessaire, puis entrez la commande hello `Get-AzureRmNetworkSecurityGroup -Name [nsg-name] -ResourceGroupName [resource-group-name]`. Hello ID sortie à partir de la commande hello ressemble trop*/subscriptions/ [nom de l’abonnement Id]/resourceGroups/[resource-group]/providers/Microsoft.Network/networkSecurityGroups/[NSG]*.
- Si vous souhaitez uniquement toocollect des données à partir de la catégorie de journal ajouter `-Categories [category]` fin toohello de commande hello dans article hello, où la catégorie est soit *NetworkSecurityGroupEvent* ou *NetworkSecurityGroupRuleCounter*. Si vous n’utilisez pas hello `-Categories` paramètre, collecte de données est activée pour les deux catégories du journal.

### <a name="azure-command-line-interface-cli"></a>Interface de ligne de commande Microsoft Azure

toouse hello la journalisation tooenable CLI, suivez les instructions de hello Bonjour [activer les journaux de diagnostic via l’interface CLI](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) l’article. Évaluer hello informations avant d’entrer une commande à partir de l’article de hello suivantes :

- Vous pouvez déterminer toouse de valeur hello pour hello `-ResourceId` paramètre en remplaçant hello suivant [texte], si nécessaire, puis entrez la commande hello `azure network nsg show [resource-group-name] [nsg-name]`. Hello ID sortie à partir de la commande hello ressemble trop*/subscriptions/ [nom de l’abonnement Id]/resourceGroups/[resource-group]/providers/Microsoft.Network/networkSecurityGroups/[NSG]*.
- Si vous souhaitez uniquement toocollect des données à partir de la catégorie de journal ajouter `-Categories [category]` fin toohello de commande hello dans article hello, où la catégorie est soit *NetworkSecurityGroupEvent* ou *NetworkSecurityGroupRuleCounter*. Si vous n’utilisez pas hello `-Categories` paramètre, collecte de données est activée pour les deux catégories du journal.

## <a name="logged-data"></a>Données enregistrées

Les données sont écrites au format JSON pour les deux journaux. les données spécifiques Hello écrites pour chaque type de journal sont répertoriées dans hello les sections suivantes :

### <a name="event-log"></a>Journal des événements
Ce journal contient des informations sur le groupe de sécurité réseau règles sont appliquées tooVMs et instances de rôle de service, en fonction de l’adresse MAC de cloud computing. Hello suivant l’exemple de données est enregistrée pour chaque événement :

```json
{
    "time": "[DATE-TIME]",
    "systemId": "007d0441-5d6b-41f6-8bfd-930db640ec03",
    "category": "NetworkSecurityGroupEvent",
    "resourceId": "/SUBSCRIPTIONS/[SUBSCRIPTION-ID]/RESOURCEGROUPS/[RESOURCE-GROUP-NAME]/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/[NSG-NAME]",
    "operationName": "NetworkSecurityGroupEvents",
    "properties": {
        "vnetResourceGuid":"{5E8AEC16-C728-441F-B0CA-B791E1DBC2F4}",
        "subnetPrefix":"192.168.1.0/24",
        "macAddress":"00-0D-3A-92-6A-7C",
        "primaryIPv4Address":"192.168.1.4",
        "ruleName":"UserRule_default-allow-rdp",
        "direction":"In",
        "priority":1000,
        "type":"allow",
        "conditions":{
            "protocols":"6",
            "destinationPortRange":"3389-3389",
            "sourcePortRange":"0-65535",
            "sourceIP":"0.0.0.0/0",
            "destinationIP":"0.0.0.0/0"
            }
        }
}
```

### <a name="rule-counter-log"></a>Journal des compteurs de règle

Ce journal contient des informations sur chaque tooresources règle soit appliquée. Hello des données d’exemple suivant sont enregistrées chaque fois qu’une règle est appliquée :

```json
{
    "time": "[DATE-TIME]",
    "systemId": "007d0441-5d6b-41f6-8bfd-930db640ec03",
    "category": "NetworkSecurityGroupRuleCounter",
    "resourceId": "/SUBSCRIPTIONS/[SUBSCRIPTION ID]/RESOURCEGROUPS/[RESOURCE-GROUP-NAME]TESTRG/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/[NSG-NAME]",
    "operationName": "NetworkSecurityGroupCounters",
    "properties": {
        "vnetResourceGuid":"{5E8AEC16-C728-441F-B0CA-791E1DBC2F4}",
        "subnetPrefix":"192.168.1.0/24",
        "macAddress":"00-0D-3A-92-6A-7C",
        "primaryIPv4Address":"192.168.1.4",
        "ruleName":"UserRule_default-allow-rdp",
        "direction":"In",
        "type":"allow",
        "matchedConnections":125
        }
}
```

## <a name="view-and-analyze-logs"></a>Afficher et analyser les journaux

toolearn comment les données de journalisation tooview activité lire hello [vue d’ensemble du journal des activités Azure de hello](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) l’article. toolearn comment les données de journalisation de diagnostic de tooview lire hello [vue d’ensemble de Azure des journaux de Diagnostic](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) l’article. Si vous envoyez des données de diagnostics tooLog Analytique, vous pouvez utiliser hello [analytique de groupe de sécurité réseau Azure](../log-analytics/log-analytics-azure-networking-analytics.md) solution de gestion (version préliminaire) pour une meilleure insights. 
