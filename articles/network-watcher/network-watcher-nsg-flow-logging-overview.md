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
# <a name="introduction-tooflow-logging-for-network-security-groups"></a><span data-ttu-id="37204-103">Journalisation de tooflow de présentation pour les groupes de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="37204-103">Introduction tooflow logging for Network Security Groups</span></span>

<span data-ttu-id="37204-104">Journaux du groupe de sécurité réseau de flux sont une fonctionnalité de l’Observateur réseau qui vous permet de tooview d’informations sur le trafic IP entrant et sortant via un groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="37204-104">Network Security Group flow logs are a feature of Network Watcher that allows you tooview information about ingress and egress IP traffic through a Network Security Group.</span></span> <span data-ttu-id="37204-105">Ces flux de journaux est écrits au format json et affiche sortant des flux entrants sur une base par la règle, hello flux hello de carte réseau s’applique, 5-tuple d’informations sur le flux hello (protocole IP Source et de Destination, Port Source et de Destination) et si hello le trafic a été autorisé ou refusé.</span><span class="sxs-lookup"><span data-stu-id="37204-105">These flow logs are written in json format and show outbound and inbound flows on a per rule basis, hello NIC hello flow applies to, 5-tuple information about hello flow (Source/Destination IP, Source/Destination Port, Protocol), and if hello traffic was allowed or denied.</span></span>

![vue d’ensemble des journaux des flux][1]

<span data-ttu-id="37204-107">Flux enregistre les groupes de sécurité réseau cible, ils ne sont pas affichés même hello comme hello autres journaux.</span><span class="sxs-lookup"><span data-stu-id="37204-107">While flow logs target Network Security Groups, they are not displayed hello same as hello other logs.</span></span> <span data-ttu-id="37204-108">Flux de journaux sont stockés uniquement dans un compte de stockage et le chemin d’accès de journalisation de hello suivant comme indiqué dans hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="37204-108">Flow logs are stored only within a storage account and following hello logging path as shown in hello following example:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

<span data-ttu-id="37204-109">Hello même des stratégies de rétention comme sur les autres journaux appliquent les journaux de tooflow.</span><span class="sxs-lookup"><span data-stu-id="37204-109">hello same retention policies as seen on other logs apply tooflow logs.</span></span> <span data-ttu-id="37204-110">Les journaux ont une stratégie de rétention peut être définie de jours too365 de 1 jour.</span><span class="sxs-lookup"><span data-stu-id="37204-110">Logs have a retention policy that can be set from 1 day too365 days.</span></span> <span data-ttu-id="37204-111">Si une stratégie de rétention n’est pas définie, les journaux de hello sont conservées indéfiniment.</span><span class="sxs-lookup"><span data-stu-id="37204-111">If a retention policy is not set, hello logs are maintained forever.</span></span>

## <a name="log-file"></a><span data-ttu-id="37204-112">Fichier journal</span><span class="sxs-lookup"><span data-stu-id="37204-112">Log file</span></span>

<span data-ttu-id="37204-113">Les journaux de flux ont plusieurs propriétés.</span><span class="sxs-lookup"><span data-stu-id="37204-113">Flow logs have multiple properties.</span></span> <span data-ttu-id="37204-114">Bonjour liste suivante est une liste de propriétés hello qui sont retournés dans le journal de flux de groupe de sécurité réseau hello :</span><span class="sxs-lookup"><span data-stu-id="37204-114">hello following list is a listing of hello properties that are returned within hello NSG flow log:</span></span>

* <span data-ttu-id="37204-115">**heure** - temps lorsque hello événement a été enregistré</span><span class="sxs-lookup"><span data-stu-id="37204-115">**time** - Time when hello event was logged</span></span>
* <span data-ttu-id="37204-116">**systemId** - L’ID de la ressource du groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="37204-116">**systemId** - Network Security Group resource Id.</span></span>
* <span data-ttu-id="37204-117">**catégorie** -catégorie de hello d’événement de hello, il est toujours être NetworkSecurityGroupFlowEvent</span><span class="sxs-lookup"><span data-stu-id="37204-117">**category** - hello category of hello event, this is always be NetworkSecurityGroupFlowEvent</span></span>
* <span data-ttu-id="37204-118">**ID de ressource** -hello Id de ressource de hello NSG</span><span class="sxs-lookup"><span data-stu-id="37204-118">**resourceid** - hello resource Id of hello NSG</span></span>
* <span data-ttu-id="37204-119">**operationName** - Toujours NetworkSecurityGroupFlowEvents.</span><span class="sxs-lookup"><span data-stu-id="37204-119">**operationName** - Always NetworkSecurityGroupFlowEvents</span></span>
* <span data-ttu-id="37204-120">**propriétés** -une collection de propriétés de flux de hello</span><span class="sxs-lookup"><span data-stu-id="37204-120">**properties** - A collection of properties of hello flow</span></span>
    * <span data-ttu-id="37204-121">**Version** -numéro de Version du schéma d’événement de flux de journal hello</span><span class="sxs-lookup"><span data-stu-id="37204-121">**Version** - Version number of hello Flow Log event schema</span></span>
    * <span data-ttu-id="37204-122">**flow** - Une collection de flux.</span><span class="sxs-lookup"><span data-stu-id="37204-122">**flows** - A collection of flows.</span></span> <span data-ttu-id="37204-123">Cette propriété a plusieurs entrées pour différentes règles.</span><span class="sxs-lookup"><span data-stu-id="37204-123">This property has multiple entries for different rules</span></span>
        * <span data-ttu-id="37204-124">**règle** -règle pour le hello flux sont répertoriés</span><span class="sxs-lookup"><span data-stu-id="37204-124">**rule** - Rule for which hello flows are listed</span></span>
            * <span data-ttu-id="37204-125">**flows** - Une collection de flux.</span><span class="sxs-lookup"><span data-stu-id="37204-125">**flows** - a collection of flows</span></span>
                * <span data-ttu-id="37204-126">**Mac** -hello adresse MAC de hello NIC pour hello où les flux hello a été collecté de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="37204-126">**mac** - hello MAC address of hello NIC for hello VM where hello flow was collected</span></span>
                * <span data-ttu-id="37204-127">**flowTuples** -chaîne qui contient plusieurs propriétés pour le tuple de flux hello dans un format séparé par des virgules</span><span class="sxs-lookup"><span data-stu-id="37204-127">**flowTuples** - A string that contains multiple properties for hello flow tuple in comma-separated format</span></span>
                    * <span data-ttu-id="37204-128">**Horodatage** -cette valeur est l’horodatage hello de lorsque les flux hello s’est produite dans le format de l’époque de UNIX</span><span class="sxs-lookup"><span data-stu-id="37204-128">**Time Stamp** - This value is hello time stamp of when hello flow occurred in UNIX EPOCH format</span></span>
                    * <span data-ttu-id="37204-129">**Adresse IP source** hello - adresse IP source</span><span class="sxs-lookup"><span data-stu-id="37204-129">**Source IP** - hello source IP</span></span>
                    * <span data-ttu-id="37204-130">**Destination IP** -hello IP de destination</span><span class="sxs-lookup"><span data-stu-id="37204-130">**Destination IP** - hello destination IP</span></span>
                    * <span data-ttu-id="37204-131">**Port source** hello - port source</span><span class="sxs-lookup"><span data-stu-id="37204-131">**Source Port** - hello source port</span></span>
                    * <span data-ttu-id="37204-132">**Port de destination** -hello du Port de destination</span><span class="sxs-lookup"><span data-stu-id="37204-132">**Destination Port** - hello destination Port</span></span>
                    * <span data-ttu-id="37204-133">**Protocole** -hello protocole de flux de hello.</span><span class="sxs-lookup"><span data-stu-id="37204-133">**Protocol** - hello protocol of hello flow.</span></span> <span data-ttu-id="37204-134">Les valeurs valides sont **T** pour TCP et **U** pour UDP.</span><span class="sxs-lookup"><span data-stu-id="37204-134">Valid values are **T** for TCP and **U** for UDP</span></span>
                    * <span data-ttu-id="37204-135">**Flux de trafic** -hello direction hello du flux de trafic.</span><span class="sxs-lookup"><span data-stu-id="37204-135">**Traffic Flow** - hello direction of hello traffic flow.</span></span> <span data-ttu-id="37204-136">Les valeurs valides sont **I** pour le trafic entrant et **O** pour le trafic sortant.</span><span class="sxs-lookup"><span data-stu-id="37204-136">Valid values are **I** for inbound and **O** for outbound.</span></span>
                    * <span data-ttu-id="37204-137">**Traffic** - Indique si le trafic a été autorisé ou refusé.</span><span class="sxs-lookup"><span data-stu-id="37204-137">**Traffic** - Whether traffic was allowed or denied.</span></span> <span data-ttu-id="37204-138">Les valeurs valides sont **A** pour autorisé et **D** pour refusé.</span><span class="sxs-lookup"><span data-stu-id="37204-138">Valid values are **A** for allowed and **D** for denied.</span></span>


<span data-ttu-id="37204-139">Hello Voici un exemple d’un flux de journal.</span><span class="sxs-lookup"><span data-stu-id="37204-139">hello following is an example of a Flow log.</span></span> <span data-ttu-id="37204-140">Comme vous pouvez le voir, il existe plusieurs enregistrements qui suivent la liste de propriétés hello décrite dans hello précédant la section.</span><span class="sxs-lookup"><span data-stu-id="37204-140">As you can see there are multiple records that follow hello property list described in hello preceding section.</span></span> 

> [!NOTE]
> <span data-ttu-id="37204-141">Valeurs de propriété de flowTuples hello sont une liste séparée par des virgules.</span><span class="sxs-lookup"><span data-stu-id="37204-141">Values in hello flowTuples property are a comma-separated list.</span></span>
 
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

## <a name="next-steps"></a><span data-ttu-id="37204-142">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="37204-142">Next steps</span></span>

<span data-ttu-id="37204-143">Découvrez comment tooenable flux se connecte en vous rendant sur [de flux de l’activation de la journalisation](network-watcher-nsg-flow-logging-portal.md).</span><span class="sxs-lookup"><span data-stu-id="37204-143">Learn how tooenable Flow logs by visiting [Enabling Flow logging](network-watcher-nsg-flow-logging-portal.md).</span></span>

<span data-ttu-id="37204-144">Pour en savoir plus sur la journalisation du groupe de sécurité réseau, consultez [Analyse de journaux pour les groupes de sécurité réseau (NSG)](../virtual-network/virtual-network-nsg-manage-log.md).</span><span class="sxs-lookup"><span data-stu-id="37204-144">Learn about NSG logging by visiting [Log analytics for network security groups (NSGs)](../virtual-network/virtual-network-nsg-manage-log.md).</span></span>

<span data-ttu-id="37204-145">Déterminez si le trafic est autorisé ou refusé sur une machine virtuelle en consultant [Vérifier si le trafic est autorisé ou refusé en direction ou en provenance d’une machine virtuelle avec le composant de vérification des flux IP d’Azure Network Watcher](network-watcher-check-ip-flow-verify-portal.md).</span><span class="sxs-lookup"><span data-stu-id="37204-145">Find out if traffic is allowed or denied on a VM by visiting [Verify traffic with IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->
[1]: ./media/network-watcher-nsg-flow-logging-overview/figure1.png

