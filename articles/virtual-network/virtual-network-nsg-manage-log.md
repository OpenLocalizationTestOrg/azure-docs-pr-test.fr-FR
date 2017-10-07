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
# <a name="log-analytics-for-network-security-groups-nsgs"></a><span data-ttu-id="d779c-103">Analyse de journaux pour les groupes de sécurité réseau (NSG)</span><span class="sxs-lookup"><span data-stu-id="d779c-103">Log analytics for network security groups (NSGs)</span></span>

<span data-ttu-id="d779c-104">Vous pouvez activer hello suivant des catégories du journal de diagnostic pour les groupes de sécurité réseau :</span><span class="sxs-lookup"><span data-stu-id="d779c-104">You can enable hello following diagnostic log categories for NSGs:</span></span>

* <span data-ttu-id="d779c-105">**Événement :** contient des entrées pour le groupe de sécurité réseau, les règles sont tooVMs appliqués et les rôles d’instance en fonction de l’adresse MAC.</span><span class="sxs-lookup"><span data-stu-id="d779c-105">**Event:** Contains entries for which NSG rules are applied tooVMs and instance roles based on MAC address.</span></span> <span data-ttu-id="d779c-106">état Hello pour ces règles est collecté toutes les 60 secondes.</span><span class="sxs-lookup"><span data-stu-id="d779c-106">hello status for these rules is collected every 60 seconds.</span></span>
* <span data-ttu-id="d779c-107">**Compteur de règle :** contient des entrées pour le nombre de fois où chaque groupe de sécurité réseau de règles est appliqué toodeny ou autoriser le trafic.</span><span class="sxs-lookup"><span data-stu-id="d779c-107">**Rule counter:** Contains entries for how many times each NSG rule is applied toodeny or allow traffic.</span></span>

> [!NOTE]
> <span data-ttu-id="d779c-108">Journaux de diagnostic sont uniquement disponibles pour les groupes de sécurité réseau déployés via le modèle de déploiement du Gestionnaire de ressources Azure hello.</span><span class="sxs-lookup"><span data-stu-id="d779c-108">Diagnostic logs are only available for NSGs deployed through hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="d779c-109">Vous ne pouvez pas activer la journalisation des diagnostics pour les groupes de sécurité réseau déployés via le modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="d779c-109">You cannot enable diagnostic logging for NSGs deployed through hello classic deployment model.</span></span> <span data-ttu-id="d779c-110">Pour mieux comprendre les modèles hello deux, référence hello [modèles de déploiement Azure de présentation](../resource-manager-deployment-model.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="d779c-110">For a better understanding of hello two models, reference hello [Understanding Azure deployment models](../resource-manager-deployment-model.md) article.</span></span>

<span data-ttu-id="d779c-111">La journalisation des activités (anciennement appelée audit ou journaux des opérations) est activé par défaut pour les groupes de sécurité réseau créés via un modèle de déploiement d’Azure.</span><span class="sxs-lookup"><span data-stu-id="d779c-111">Activity logging (previously known as audit or operational logs) is enabled by default for NSGs created through either Azure deployment model.</span></span> <span data-ttu-id="d779c-112">toodetermine quelles opérations ont été effectuées sur les groupes de sécurité réseau dans le journal d’activité hello, recherchez les entrées qui contiennent le hello les types de ressources suivants :</span><span class="sxs-lookup"><span data-stu-id="d779c-112">toodetermine which operations were completed on NSGs in hello activity log, look for entries that contain hello following resource types:</span></span> 

- <span data-ttu-id="d779c-113">Microsoft.ClassicNetwork/networkSecurityGroups</span><span class="sxs-lookup"><span data-stu-id="d779c-113">Microsoft.ClassicNetwork/networkSecurityGroups</span></span> 
- <span data-ttu-id="d779c-114">Microsoft.ClassicNetwork/networkSecurityGroups/securityRules</span><span class="sxs-lookup"><span data-stu-id="d779c-114">Microsoft.ClassicNetwork/networkSecurityGroups/securityRules</span></span>
- <span data-ttu-id="d779c-115">Microsoft.Network/networkSecurityGroups</span><span class="sxs-lookup"><span data-stu-id="d779c-115">Microsoft.Network/networkSecurityGroups</span></span>
- <span data-ttu-id="d779c-116">Microsoft.Network/networkSecurityGroups/securityRules</span><span class="sxs-lookup"><span data-stu-id="d779c-116">Microsoft.Network/networkSecurityGroups/securityRules</span></span> 

<span data-ttu-id="d779c-117">Hello de lecture [vue d’ensemble du journal des activités Azure de hello](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md) toolearn article plus d’informations sur les journaux d’activité.</span><span class="sxs-lookup"><span data-stu-id="d779c-117">Read hello [Overview of hello Azure Activity Log](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md) article toolearn more about activity logs.</span></span> 

## <a name="enable-diagnostic-logging"></a><span data-ttu-id="d779c-118">Activer la journalisation des diagnostics</span><span class="sxs-lookup"><span data-stu-id="d779c-118">Enable diagnostic logging</span></span>

<span data-ttu-id="d779c-119">Journalisation des diagnostics doit être activée pour *chaque* groupe de sécurité réseau que vous voulez toocollect de données pour.</span><span class="sxs-lookup"><span data-stu-id="d779c-119">Diagnostic logging must be enabled for *each* NSG you want toocollect data for.</span></span> <span data-ttu-id="d779c-120">Hello [vue d’ensemble de Azure des journaux de Diagnostic](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) explique où les journaux de diagnostic peuvent être envoyés.</span><span class="sxs-lookup"><span data-stu-id="d779c-120">hello [Overview of Azure Diagnostic Logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) article explains where diagnostic logs can be sent.</span></span> <span data-ttu-id="d779c-121">Si vous n’avez pas un groupe de sécurité réseau existant, hello terminé les étapes Bonjour [créer un groupe de sécurité réseau](virtual-networks-create-nsg-arm-pportal.md) toocreate article un.</span><span class="sxs-lookup"><span data-stu-id="d779c-121">If you don't have an existing NSG, complete hello steps in hello [Create a network security group](virtual-networks-create-nsg-arm-pportal.md) article toocreate one.</span></span> <span data-ttu-id="d779c-122">Vous pouvez activer le groupe de sécurité réseau diagnostic journalisation à l’aide d’une des méthodes suivantes de hello :</span><span class="sxs-lookup"><span data-stu-id="d779c-122">You can enable NSG diagnostic logging using any of hello following methods:</span></span>

### <a name="azure-portal"></a><span data-ttu-id="d779c-123">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="d779c-123">Azure portal</span></span>

<span data-ttu-id="d779c-124">journalisation de portail tooenable toouse hello, connexion toohello [portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d779c-124">toouse hello portal tooenable logging, login toohello [portal](https://portal.azure.com).</span></span> <span data-ttu-id="d779c-125">Cliquez sur **Plus de services**, puis tapez *groupes de sécurité réseau*.</span><span class="sxs-lookup"><span data-stu-id="d779c-125">Click **More services**, then type *network security groups*.</span></span> <span data-ttu-id="d779c-126">Sélectionnez hello NSG souhaité tooenable journalisation pour.</span><span class="sxs-lookup"><span data-stu-id="d779c-126">Select hello NSG you want tooenable logging for.</span></span> <span data-ttu-id="d779c-127">Suivez les instructions de hello pour les ressources de calcul non Bonjour [activer les journaux de diagnostic dans le portail de hello](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) l’article.</span><span class="sxs-lookup"><span data-stu-id="d779c-127">Follow hello instructions for non-compute resources in hello [Enable diagnostic logs in hello portal](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) article.</span></span> <span data-ttu-id="d779c-128">Sélectionnez **NetworkSecurityGroupEvent**, **NetworkSecurityGroupRuleCounter**, ou les deux catégories de journaux.</span><span class="sxs-lookup"><span data-stu-id="d779c-128">Select **NetworkSecurityGroupEvent**, **NetworkSecurityGroupRuleCounter**, or both categories of logs.</span></span>

### <a name="powershell"></a><span data-ttu-id="d779c-129">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d779c-129">PowerShell</span></span>

<span data-ttu-id="d779c-130">tooenable de PowerShell toouse journalisation, suivez les instructions de hello Bonjour [activer les journaux de diagnostic via PowerShell](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) l’article.</span><span class="sxs-lookup"><span data-stu-id="d779c-130">toouse PowerShell tooenable logging, follow hello instructions in hello [Enable diagnostic logs via PowerShell](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) article.</span></span> <span data-ttu-id="d779c-131">Évaluer hello informations avant d’entrer une commande à partir de l’article de hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="d779c-131">Evaluate hello following information before entering a command from hello article:</span></span>

- <span data-ttu-id="d779c-132">Vous pouvez déterminer toouse de valeur hello pour hello `-ResourceId` paramètre en remplaçant hello suivant [texte], si nécessaire, puis entrez la commande hello `Get-AzureRmNetworkSecurityGroup -Name [nsg-name] -ResourceGroupName [resource-group-name]`.</span><span class="sxs-lookup"><span data-stu-id="d779c-132">You can determine hello value toouse for hello `-ResourceId` parameter by replacing hello following [text], as appropriate, then entering hello command `Get-AzureRmNetworkSecurityGroup -Name [nsg-name] -ResourceGroupName [resource-group-name]`.</span></span> <span data-ttu-id="d779c-133">Hello ID sortie à partir de la commande hello ressemble trop*/subscriptions/ [nom de l’abonnement Id]/resourceGroups/[resource-group]/providers/Microsoft.Network/networkSecurityGroups/[NSG]*.</span><span class="sxs-lookup"><span data-stu-id="d779c-133">hello ID output from hello command looks similar too*/subscriptions/[Subscription Id]/resourceGroups/[resource-group]/providers/Microsoft.Network/networkSecurityGroups/[NSG name]*.</span></span>
- <span data-ttu-id="d779c-134">Si vous souhaitez uniquement toocollect des données à partir de la catégorie de journal ajouter `-Categories [category]` fin toohello de commande hello dans article hello, où la catégorie est soit *NetworkSecurityGroupEvent* ou *NetworkSecurityGroupRuleCounter*.</span><span class="sxs-lookup"><span data-stu-id="d779c-134">If you only want toocollect data from log category add `-Categories [category]` toohello end of hello command in hello article, where category is either *NetworkSecurityGroupEvent* or *NetworkSecurityGroupRuleCounter*.</span></span> <span data-ttu-id="d779c-135">Si vous n’utilisez pas hello `-Categories` paramètre, collecte de données est activée pour les deux catégories du journal.</span><span class="sxs-lookup"><span data-stu-id="d779c-135">If you don't use hello `-Categories` parameter, data collection is enabled for both log categories.</span></span>

### <a name="azure-command-line-interface-cli"></a><span data-ttu-id="d779c-136">Interface de ligne de commande Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="d779c-136">Azure command-line interface (CLI)</span></span>

<span data-ttu-id="d779c-137">toouse hello la journalisation tooenable CLI, suivez les instructions de hello Bonjour [activer les journaux de diagnostic via l’interface CLI](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) l’article.</span><span class="sxs-lookup"><span data-stu-id="d779c-137">toouse hello CLI tooenable logging, follow hello instructions in hello [Enable diagnostic logs via CLI](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) article.</span></span> <span data-ttu-id="d779c-138">Évaluer hello informations avant d’entrer une commande à partir de l’article de hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="d779c-138">Evaluate hello following information before entering a command from hello article:</span></span>

- <span data-ttu-id="d779c-139">Vous pouvez déterminer toouse de valeur hello pour hello `-ResourceId` paramètre en remplaçant hello suivant [texte], si nécessaire, puis entrez la commande hello `azure network nsg show [resource-group-name] [nsg-name]`.</span><span class="sxs-lookup"><span data-stu-id="d779c-139">You can determine hello value toouse for hello `-ResourceId` parameter by replacing hello following [text], as appropriate, then entering hello command `azure network nsg show [resource-group-name] [nsg-name]`.</span></span> <span data-ttu-id="d779c-140">Hello ID sortie à partir de la commande hello ressemble trop*/subscriptions/ [nom de l’abonnement Id]/resourceGroups/[resource-group]/providers/Microsoft.Network/networkSecurityGroups/[NSG]*.</span><span class="sxs-lookup"><span data-stu-id="d779c-140">hello ID output from hello command looks similar too*/subscriptions/[Subscription Id]/resourceGroups/[resource-group]/providers/Microsoft.Network/networkSecurityGroups/[NSG name]*.</span></span>
- <span data-ttu-id="d779c-141">Si vous souhaitez uniquement toocollect des données à partir de la catégorie de journal ajouter `-Categories [category]` fin toohello de commande hello dans article hello, où la catégorie est soit *NetworkSecurityGroupEvent* ou *NetworkSecurityGroupRuleCounter*.</span><span class="sxs-lookup"><span data-stu-id="d779c-141">If you only want toocollect data from log category add `-Categories [category]` toohello end of hello command in hello article, where category is either *NetworkSecurityGroupEvent* or *NetworkSecurityGroupRuleCounter*.</span></span> <span data-ttu-id="d779c-142">Si vous n’utilisez pas hello `-Categories` paramètre, collecte de données est activée pour les deux catégories du journal.</span><span class="sxs-lookup"><span data-stu-id="d779c-142">If you don't use hello `-Categories` parameter, data collection is enabled for both log categories.</span></span>

## <a name="logged-data"></a><span data-ttu-id="d779c-143">Données enregistrées</span><span class="sxs-lookup"><span data-stu-id="d779c-143">Logged data</span></span>

<span data-ttu-id="d779c-144">Les données sont écrites au format JSON pour les deux journaux.</span><span class="sxs-lookup"><span data-stu-id="d779c-144">JSON-formatted data is written for both logs.</span></span> <span data-ttu-id="d779c-145">les données spécifiques Hello écrites pour chaque type de journal sont répertoriées dans hello les sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="d779c-145">hello specific data written for each log type is listed in hello following sections:</span></span>

### <a name="event-log"></a><span data-ttu-id="d779c-146">Journal des événements</span><span class="sxs-lookup"><span data-stu-id="d779c-146">Event log</span></span>
<span data-ttu-id="d779c-147">Ce journal contient des informations sur le groupe de sécurité réseau règles sont appliquées tooVMs et instances de rôle de service, en fonction de l’adresse MAC de cloud computing.</span><span class="sxs-lookup"><span data-stu-id="d779c-147">This log contains information about which NSG rules are applied tooVMs and cloud service role instances, based on MAC address.</span></span> <span data-ttu-id="d779c-148">Hello suivant l’exemple de données est enregistrée pour chaque événement :</span><span class="sxs-lookup"><span data-stu-id="d779c-148">hello following example data is logged for each event:</span></span>

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

### <a name="rule-counter-log"></a><span data-ttu-id="d779c-149">Journal des compteurs de règle</span><span class="sxs-lookup"><span data-stu-id="d779c-149">Rule counter log</span></span>

<span data-ttu-id="d779c-150">Ce journal contient des informations sur chaque tooresources règle soit appliquée.</span><span class="sxs-lookup"><span data-stu-id="d779c-150">This log contains information about each rule applied tooresources.</span></span> <span data-ttu-id="d779c-151">Hello des données d’exemple suivant sont enregistrées chaque fois qu’une règle est appliquée :</span><span class="sxs-lookup"><span data-stu-id="d779c-151">hello following example data is logged each time a rule is applied:</span></span>

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

## <a name="view-and-analyze-logs"></a><span data-ttu-id="d779c-152">Afficher et analyser les journaux</span><span class="sxs-lookup"><span data-stu-id="d779c-152">View and analyze logs</span></span>

<span data-ttu-id="d779c-153">toolearn comment les données de journalisation tooview activité lire hello [vue d’ensemble du journal des activités Azure de hello](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="d779c-153">toolearn how tooview activity log data, read hello [Overview of hello Azure Activity Log](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) article.</span></span> <span data-ttu-id="d779c-154">toolearn comment les données de journalisation de diagnostic de tooview lire hello [vue d’ensemble de Azure des journaux de Diagnostic](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="d779c-154">toolearn how tooview diagnostic log data, read hello [Overview of Azure Diagnostic Logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) article.</span></span> <span data-ttu-id="d779c-155">Si vous envoyez des données de diagnostics tooLog Analytique, vous pouvez utiliser hello [analytique de groupe de sécurité réseau Azure](../log-analytics/log-analytics-azure-networking-analytics.md) solution de gestion (version préliminaire) pour une meilleure insights.</span><span class="sxs-lookup"><span data-stu-id="d779c-155">If you send diagnostics data tooLog Analytics, you can use hello [Azure Network Security Group analytics](../log-analytics/log-analytics-azure-networking-analytics.md) (preview) management solution for enhanced insights.</span></span> 
