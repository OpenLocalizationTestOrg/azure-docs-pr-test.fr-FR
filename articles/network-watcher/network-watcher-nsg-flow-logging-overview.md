---
title: "Présentation de la journalisation des flux pour les groupes de sécurité réseau avec Azure Network Watcher | Microsoft Docs"
description: "Cette page explique comment utiliser les journaux de flux de groupe de sécurité réseau, une fonctionnalité d’Azure Network Watcher"
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
ms.openlocfilehash: b7a9162d6c6219b6b1c51a49cd34b9616e9d3e8f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-flow-logging-for-network-security-groups"></a><span data-ttu-id="04384-103">Présentation de la journalisation des flux pour les groupes de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="04384-103">Introduction to flow logging for Network Security Groups</span></span>

<span data-ttu-id="04384-104">Les journaux de flux de groupe de sécurité réseau désignent une fonctionnalité de Network Watcher qui vous permet d’afficher des informations sur le trafic IP entrant et sortant d’un groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="04384-104">Network Security Group flow logs are a feature of Network Watcher that allows you to view information about ingress and egress IP traffic through a Network Security Group.</span></span> <span data-ttu-id="04384-105">Ces journaux de flux sont écrits au format json et affichent les flux entrants et sortants en fonction de règles, de la carte réseau à laquelle le flux s’applique, des informations à 5 tuples sur le flux (adresse IP source/de destination, port source/de destination, protocole), et de l’autorisation ou du refus du trafic.</span><span class="sxs-lookup"><span data-stu-id="04384-105">These flow logs are written in json format and show outbound and inbound flows on a per rule basis, the NIC the flow applies to, 5-tuple information about the flow (Source/Destination IP, Source/Destination Port, Protocol), and if the traffic was allowed or denied.</span></span>

![vue d’ensemble des journaux de flux][1]

<span data-ttu-id="04384-107">Même si les journaux de flux ciblent les groupes de sécurité réseau, ils ne sont pas affichés de la même façon que les autres journaux.</span><span class="sxs-lookup"><span data-stu-id="04384-107">While flow logs target Network Security Groups, they are not displayed the same as the other logs.</span></span> <span data-ttu-id="04384-108">Les journaux de flux sont uniquement stockés dans un compte de stockage et suivent le chemin de journalisation comme indiqué dans l’exemple ci-après :</span><span class="sxs-lookup"><span data-stu-id="04384-108">Flow logs are stored only within a storage account and following the logging path as shown in the following example:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

<span data-ttu-id="04384-109">Les mêmes stratégies de rétention que celles des autres journaux s’appliquent aux journaux de flux.</span><span class="sxs-lookup"><span data-stu-id="04384-109">The same retention policies as seen on other logs apply to flow logs.</span></span> <span data-ttu-id="04384-110">Les journaux ont une stratégie de rétention qui peut être définie dans une plage comprise entre 1 et 365 jours.</span><span class="sxs-lookup"><span data-stu-id="04384-110">Logs have a retention policy that can be set from 1 day to 365 days.</span></span> <span data-ttu-id="04384-111">Si aucune stratégie de rétention n’est définie, les journaux sont conservés indéfiniment.</span><span class="sxs-lookup"><span data-stu-id="04384-111">If a retention policy is not set, the logs are maintained forever.</span></span>

## <a name="log-file"></a><span data-ttu-id="04384-112">Fichier journal</span><span class="sxs-lookup"><span data-stu-id="04384-112">Log file</span></span>

<span data-ttu-id="04384-113">Les journaux de flux ont plusieurs propriétés.</span><span class="sxs-lookup"><span data-stu-id="04384-113">Flow logs have multiple properties.</span></span> <span data-ttu-id="04384-114">La liste suivante répertorie les propriétés qui sont renvoyées dans le journal de flux de groupe de sécurité réseau :</span><span class="sxs-lookup"><span data-stu-id="04384-114">The following list is a listing of the properties that are returned within the NSG flow log:</span></span>

* <span data-ttu-id="04384-115">**time** - L’heure à laquelle l’événement a été journalisé.</span><span class="sxs-lookup"><span data-stu-id="04384-115">**time** - Time when the event was logged</span></span>
* <span data-ttu-id="04384-116">**systemId** - L’ID de la ressource du groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="04384-116">**systemId** - Network Security Group resource Id.</span></span>
* <span data-ttu-id="04384-117">**category** - La catégorie de l’événement ; il s’agit toujours de NetworkSecurityGroupFlowEvent.</span><span class="sxs-lookup"><span data-stu-id="04384-117">**category** - The category of the event, this is always be NetworkSecurityGroupFlowEvent</span></span>
* <span data-ttu-id="04384-118">**resourceid** - L’ID de la ressource du groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="04384-118">**resourceid** - The resource Id of the NSG</span></span>
* <span data-ttu-id="04384-119">**operationName** - Toujours NetworkSecurityGroupFlowEvents.</span><span class="sxs-lookup"><span data-stu-id="04384-119">**operationName** - Always NetworkSecurityGroupFlowEvents</span></span>
* <span data-ttu-id="04384-120">**properties** - Une collection des propriétés du flux.</span><span class="sxs-lookup"><span data-stu-id="04384-120">**properties** - A collection of properties of the flow</span></span>
    * <span data-ttu-id="04384-121">**Version** - Le numéro de version du schéma d’événement du journal de flux.</span><span class="sxs-lookup"><span data-stu-id="04384-121">**Version** - Version number of the Flow Log event schema</span></span>
    * <span data-ttu-id="04384-122">**flow** - Une collection de flux.</span><span class="sxs-lookup"><span data-stu-id="04384-122">**flows** - A collection of flows.</span></span> <span data-ttu-id="04384-123">Cette propriété a plusieurs entrées pour différentes règles.</span><span class="sxs-lookup"><span data-stu-id="04384-123">This property has multiple entries for different rules</span></span>
        * <span data-ttu-id="04384-124">**rule** - La règle pour laquelle les flux sont répertoriés.</span><span class="sxs-lookup"><span data-stu-id="04384-124">**rule** - Rule for which the flows are listed</span></span>
            * <span data-ttu-id="04384-125">**flows** - Une collection de flux.</span><span class="sxs-lookup"><span data-stu-id="04384-125">**flows** - a collection of flows</span></span>
                * <span data-ttu-id="04384-126">**mac** - L’adresse MAC de la carte réseau de la machine virtuelle où le flux a été collecté.</span><span class="sxs-lookup"><span data-stu-id="04384-126">**mac** - The MAC address of the NIC for the VM where the flow was collected</span></span>
                * <span data-ttu-id="04384-127">**flowTuples** - Une chaîne qui contient plusieurs propriétés séparées par des virgules pour le tuple de flux.</span><span class="sxs-lookup"><span data-stu-id="04384-127">**flowTuples** - A string that contains multiple properties for the flow tuple in comma-separated format</span></span>
                    * <span data-ttu-id="04384-128">**Time Stamp** - Cette valeur indique la date et l’heure du flux au format UNIX EPOCH.</span><span class="sxs-lookup"><span data-stu-id="04384-128">**Time Stamp** - This value is the time stamp of when the flow occurred in UNIX EPOCH format</span></span>
                    * <span data-ttu-id="04384-129">**Source IP** - L’adresse IP source.</span><span class="sxs-lookup"><span data-stu-id="04384-129">**Source IP** - The source IP</span></span>
                    * <span data-ttu-id="04384-130">**Destination IP** - L’adresse IP de destination.</span><span class="sxs-lookup"><span data-stu-id="04384-130">**Destination IP** - The destination IP</span></span>
                    * <span data-ttu-id="04384-131">**Source Port** - Le port source.</span><span class="sxs-lookup"><span data-stu-id="04384-131">**Source Port** - The source port</span></span>
                    * <span data-ttu-id="04384-132">**Destination Port** - Le port de destination.</span><span class="sxs-lookup"><span data-stu-id="04384-132">**Destination Port** - The destination Port</span></span>
                    * <span data-ttu-id="04384-133">**Protocol** - Le protocole du flux.</span><span class="sxs-lookup"><span data-stu-id="04384-133">**Protocol** - The protocol of the flow.</span></span> <span data-ttu-id="04384-134">Les valeurs valides sont **T** pour TCP et **U** pour UDP.</span><span class="sxs-lookup"><span data-stu-id="04384-134">Valid values are **T** for TCP and **U** for UDP</span></span>
                    * <span data-ttu-id="04384-135">**Traffic Flow** - La direction du flux de trafic.</span><span class="sxs-lookup"><span data-stu-id="04384-135">**Traffic Flow** - The direction of the traffic flow.</span></span> <span data-ttu-id="04384-136">Les valeurs valides sont **I** pour le trafic entrant et **O** pour le trafic sortant.</span><span class="sxs-lookup"><span data-stu-id="04384-136">Valid values are **I** for inbound and **O** for outbound.</span></span>
                    * <span data-ttu-id="04384-137">**Traffic** - Indique si le trafic a été autorisé ou refusé.</span><span class="sxs-lookup"><span data-stu-id="04384-137">**Traffic** - Whether traffic was allowed or denied.</span></span> <span data-ttu-id="04384-138">Les valeurs valides sont **A** pour autorisé et **D** pour refusé.</span><span class="sxs-lookup"><span data-stu-id="04384-138">Valid values are **A** for allowed and **D** for denied.</span></span>


<span data-ttu-id="04384-139">Vous trouverez ci-dessous un exemple de journal de flux.</span><span class="sxs-lookup"><span data-stu-id="04384-139">The following is an example of a Flow log.</span></span> <span data-ttu-id="04384-140">Comme vous pouvez le voir, il existe plusieurs enregistrements qui suivent la liste des propriétés décrite dans la section précédente.</span><span class="sxs-lookup"><span data-stu-id="04384-140">As you can see there are multiple records that follow the property list described in the preceding section.</span></span> 

> [!NOTE]
> <span data-ttu-id="04384-141">Les valeurs de la propriété flowTuples sont une liste séparée par des virgules.</span><span class="sxs-lookup"><span data-stu-id="04384-141">Values in the flowTuples property are a comma-separated list.</span></span>
 
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

## <a name="next-steps"></a><span data-ttu-id="04384-142">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="04384-142">Next steps</span></span>

<span data-ttu-id="04384-143">Découvrez comment activer les journaux de flux en consultant [Enable flow logs](network-watcher-nsg-flow-logging-portal.md) (Activer les journaux de flux).</span><span class="sxs-lookup"><span data-stu-id="04384-143">Learn how to enable Flow logs by visiting [Enabling Flow logging](network-watcher-nsg-flow-logging-portal.md).</span></span>

<span data-ttu-id="04384-144">Pour en savoir plus sur la journalisation du groupe de sécurité réseau, consultez [Analyse de journaux pour les groupes de sécurité réseau (NSG)](../virtual-network/virtual-network-nsg-manage-log.md).</span><span class="sxs-lookup"><span data-stu-id="04384-144">Learn about NSG logging by visiting [Log analytics for network security groups (NSGs)](../virtual-network/virtual-network-nsg-manage-log.md).</span></span>

<span data-ttu-id="04384-145">Déterminez si le trafic est autorisé ou refusé sur une machine virtuelle en consultant [Vérifier si le trafic est autorisé ou refusé en direction ou en provenance d’une machine virtuelle avec le composant de vérification des flux IP d’Azure Network Watcher](network-watcher-check-ip-flow-verify-portal.md).</span><span class="sxs-lookup"><span data-stu-id="04384-145">Find out if traffic is allowed or denied on a VM by visiting [Verify traffic with IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->
[1]: ./media/network-watcher-nsg-flow-logging-overview/figure1.png

