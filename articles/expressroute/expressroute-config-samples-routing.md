---
title: exemples de configuration de routeur de clients aaaExpressRoute | Documents Microsoft
description: Cette page fournit des exemples de configuration pour les routeurs Cisco et Juniper.
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
ms.assetid: 564826bc-017a-4683-a385-37c9fa814948
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/10/2016
ms.author: cherylmc
ms.openlocfilehash: 5c91f24e6082e01c3e8df91b4fcfda46a6c29fa8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="router-configuration-samples-tooset-up-and-manage-routing"></a><span data-ttu-id="fcbc8-103">Configuration du routeur exemples tooset haut et gérer le routage</span><span class="sxs-lookup"><span data-stu-id="fcbc8-103">Router configuration samples tooset up and manage routing</span></span>
<span data-ttu-id="fcbc8-104">Cette page fournit une interface et des exemples de configuration de routage pour les routeurs des séries Cisco IOS-XE et Juniper MX.</span><span class="sxs-lookup"><span data-stu-id="fcbc8-104">This page provides interface and routing configuration samples for Cisco IOS-XE and Juniper MX series routers.</span></span> <span data-ttu-id="fcbc8-105">Ces exemples toobe prévue à titre indicatif et ne doivent pas être utilisés en l’état.</span><span class="sxs-lookup"><span data-stu-id="fcbc8-105">These are intended toobe samples for guidance only and must not be used as is.</span></span> <span data-ttu-id="fcbc8-106">Vous pouvez travailler avec votre fournisseur toocome configurations appropriées pour votre réseau.</span><span class="sxs-lookup"><span data-stu-id="fcbc8-106">You can work with your vendor toocome up with appropriate configurations for your network.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="fcbc8-107">Les exemples dans cette page sont toobe prévu uniquement pour obtenir des conseils.</span><span class="sxs-lookup"><span data-stu-id="fcbc8-107">Samples in this page are intended toobe purely for guidance.</span></span> <span data-ttu-id="fcbc8-108">Vous devez collaborer avec l’équipe de vente / technique de votre fournisseur et votre toocome équipe mise en réseau haut avec toomeet de configurations appropriées à vos besoins.</span><span class="sxs-lookup"><span data-stu-id="fcbc8-108">You must work with your vendor's sales / technical team and your networking team toocome up with appropriate configurations toomeet your needs.</span></span> <span data-ttu-id="fcbc8-109">Microsoft ne prendra pas en charge des problèmes liés tooconfigurations répertoriées dans cette page.</span><span class="sxs-lookup"><span data-stu-id="fcbc8-109">Microsoft will not support issues related tooconfigurations listed in this page.</span></span> <span data-ttu-id="fcbc8-110">Vous devez contacter le fournisseur de votre périphérique pour la prise en charge des problèmes.</span><span class="sxs-lookup"><span data-stu-id="fcbc8-110">You must contact your device vendor for support issues.</span></span>
> 
> 

## <a name="mtu-and-tcp-mss-settings-on-router-interfaces"></a><span data-ttu-id="fcbc8-111">Paramètres MTU et TCP MSS sur les interfaces de routeur</span><span class="sxs-lookup"><span data-stu-id="fcbc8-111">MTU and TCP MSS settings on router interfaces</span></span>
* <span data-ttu-id="fcbc8-112">Hello MTU pour l’interface de ExpressRoute hello est 1500, hello classique MTU par défaut pour une interface Ethernet sur un routeur.</span><span class="sxs-lookup"><span data-stu-id="fcbc8-112">hello MTU for hello ExpressRoute interface is 1500, which is hello typical default MTU for an Ethernet interface on a router.</span></span> <span data-ttu-id="fcbc8-113">À moins que votre routeur possède une MTU différentes par défaut, il n’existe aucune toospecify besoin une valeur sur l’interface de routeur hello.</span><span class="sxs-lookup"><span data-stu-id="fcbc8-113">Unless your router has a different MTU by default, there is no need toospecify a value on hello router interface.</span></span>
* <span data-ttu-id="fcbc8-114">Contrairement à une passerelle VPN Azure, hello MSS de TCP pour un circuit ExpressRoute n’a pas besoin toobe spécifié.</span><span class="sxs-lookup"><span data-stu-id="fcbc8-114">Unlike an Azure VPN Gateway, hello TCP MSS for an ExpressRoute circuit does not need toobe specified.</span></span>

<span data-ttu-id="fcbc8-115">Exemples de configuration du routeur ci-dessous s’appliquent tooall homologations.</span><span class="sxs-lookup"><span data-stu-id="fcbc8-115">Router configuration samples below apply tooall peerings.</span></span> <span data-ttu-id="fcbc8-116">Pour plus d’informations sur le routage, voir [Homologations ExpressRoute](expressroute-circuit-peerings.md) et [Configuration requise pour le routage ExpressRoute](expressroute-routing.md).</span><span class="sxs-lookup"><span data-stu-id="fcbc8-116">Review [ExpressRoute peerings](expressroute-circuit-peerings.md) and [ExpressRoute routing requirements](expressroute-routing.md) for more details on routing.</span></span>


## <a name="cisco-ios-xe-based-routers"></a><span data-ttu-id="fcbc8-117">Routeurs Cisco IOS-XE</span><span class="sxs-lookup"><span data-stu-id="fcbc8-117">Cisco IOS-XE based routers</span></span>
<span data-ttu-id="fcbc8-118">exemples de Hello dans cette section s’appliquent à tous les routeurs de famille du système d’exploitation IOS-XE hello en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="fcbc8-118">hello samples in this section apply for any router running hello IOS-XE OS family.</span></span>

### <a name="1-configuring-interfaces-and-sub-interfaces"></a><span data-ttu-id="fcbc8-119">1. Configuration des interfaces et des sous-interfaces</span><span class="sxs-lookup"><span data-stu-id="fcbc8-119">1. Configuring interfaces and sub-interfaces</span></span>
<span data-ttu-id="fcbc8-120">Vous aurez besoin d’une interface sub par homologation dans chaque routeur, vous connecter tooMicrosoft.</span><span class="sxs-lookup"><span data-stu-id="fcbc8-120">You will require a sub interface per peering in every router you connect tooMicrosoft.</span></span> <span data-ttu-id="fcbc8-121">Une sous-interface peut être identifiée avec un ID de réseau local virtuel ou une paire empilée d’ID de réseau local virtuel, et une adresse IP.</span><span class="sxs-lookup"><span data-stu-id="fcbc8-121">A sub interface can be identified with a VLAN ID or a stacked pair of VLAN IDs and an IP address.</span></span>

<span data-ttu-id="fcbc8-122">**Définition de l’interface Dot1Q**</span><span class="sxs-lookup"><span data-stu-id="fcbc8-122">**Dot1Q interface definition**</span></span>

<span data-ttu-id="fcbc8-123">Cet exemple fournit la définition de l’interface sous-chemin hello pour une interface secondaire avec un ID de réseau local virtuel unique.</span><span class="sxs-lookup"><span data-stu-id="fcbc8-123">This sample provides hello sub-interface definition for a sub-interface with a single VLAN ID.</span></span> <span data-ttu-id="fcbc8-124">Hello, ID de VLAN est unique pour chaque d’homologation.</span><span class="sxs-lookup"><span data-stu-id="fcbc8-124">hello VLAN ID is unique per peering.</span></span> <span data-ttu-id="fcbc8-125">Hello dernier octet de votre adresse IPv4 sera toujours un nombre impair.</span><span class="sxs-lookup"><span data-stu-id="fcbc8-125">hello last octet of your IPv4 address will always be an odd number.</span></span>

    interface GigabitEthernet<Interface_Number>.<Number>
     encapsulation dot1Q <VLAN_ID>
     ip address <IPv4_Address><Subnet_Mask>

<span data-ttu-id="fcbc8-126">**Définition de l’interface QinQ**</span><span class="sxs-lookup"><span data-stu-id="fcbc8-126">**QinQ interface definition**</span></span>

<span data-ttu-id="fcbc8-127">Cet exemple fournit la définition de l’interface sous-chemin hello pour une interface secondaire avec un ID de VLAN deux.</span><span class="sxs-lookup"><span data-stu-id="fcbc8-127">This sample provides hello sub-interface definition for a sub-interface with a two VLAN IDs.</span></span> <span data-ttu-id="fcbc8-128">Hello ID VLAN externe (s-tag), si utilisé reste hello même sur tous les homologations de hello.</span><span class="sxs-lookup"><span data-stu-id="fcbc8-128">hello outer VLAN ID (s-tag), if used remains hello same across all hello peerings.</span></span> <span data-ttu-id="fcbc8-129">interne de Hello ID de VLAN (c-tag) est unique pour chaque d’homologation.</span><span class="sxs-lookup"><span data-stu-id="fcbc8-129">hello inner VLAN ID (c-tag) is unique per peering.</span></span> <span data-ttu-id="fcbc8-130">Hello dernier octet de votre adresse IPv4 sera toujours un nombre impair.</span><span class="sxs-lookup"><span data-stu-id="fcbc8-130">hello last octet of your IPv4 address will always be an odd number.</span></span>

    interface GigabitEthernet<Interface_Number>.<Number>
     encapsulation dot1Q <s-tag> seconddot1Q <c-tag>
     ip address <IPv4_Address><Subnet_Mask>

### <a name="2-setting-up-ebgp-sessions"></a><span data-ttu-id="fcbc8-131">2. Configuration de sessions eBGP</span><span class="sxs-lookup"><span data-stu-id="fcbc8-131">2. Setting up eBGP sessions</span></span>
<span data-ttu-id="fcbc8-132">Vous devez configurer une session BGP avec Microsoft pour chaque homologation.</span><span class="sxs-lookup"><span data-stu-id="fcbc8-132">You must setup a BGP session with Microsoft for every peering.</span></span> <span data-ttu-id="fcbc8-133">exemple Hello ci-dessous vous permet de toosetup une session BGP avec Microsoft.</span><span class="sxs-lookup"><span data-stu-id="fcbc8-133">hello sample below enables you toosetup a BGP session with Microsoft.</span></span> <span data-ttu-id="fcbc8-134">Si hello adresse IPv4 que vous avez utilisé pour votre interface sub était a.b.c.d, hello est adresse IP du voisin BGP de hello (Microsoft) est a.b.c.d+1.</span><span class="sxs-lookup"><span data-stu-id="fcbc8-134">If hello IPv4 address you used for your sub interface was a.b.c.d, hello IP address of hello BGP neighbor (Microsoft) will be a.b.c.d+1.</span></span> <span data-ttu-id="fcbc8-135">dernier octet de Hello d’adresse IPv4 du voisin hello BGP sera toujours un nombre pair.</span><span class="sxs-lookup"><span data-stu-id="fcbc8-135">hello last octet of hello BGP neighbor's IPv4 address will always be an even number.</span></span>

    router bgp <Customer_ASN>
     bgp log-neighbor-changes
     neighbor <IP#2_used_by_Azure> remote-as 12076
     !        
     address-family ipv4
     neighbor <IP#2_used_by_Azure> activate
     exit-address-family
    !

### <a name="3-setting-up-prefixes-toobe-advertised-over-hello-bgp-session"></a><span data-ttu-id="fcbc8-136">3. Configuration des préfixes toobe publiés sur la session BGP de hello</span><span class="sxs-lookup"><span data-stu-id="fcbc8-136">3. Setting up prefixes toobe advertised over hello BGP session</span></span>
<span data-ttu-id="fcbc8-137">Vous pouvez configurer votre tooMicrosoft de préfixes sélectionnez tooadvertise routeur.</span><span class="sxs-lookup"><span data-stu-id="fcbc8-137">You can configure your router tooadvertise select prefixes tooMicrosoft.</span></span> <span data-ttu-id="fcbc8-138">Cela à l’aide de hello exemple ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="fcbc8-138">You can do so using hello sample below.</span></span>

    router bgp <Customer_ASN>
     bgp log-neighbor-changes
     neighbor <IP#2_used_by_Azure> remote-as 12076
     !        
     address-family ipv4
      network <Prefix_to_be_advertised> mask <Subnet_mask>
      neighbor <IP#2_used_by_Azure> activate
     exit-address-family
    !

### <a name="4-route-maps"></a><span data-ttu-id="fcbc8-139">4. Cartes d’itinéraire</span><span class="sxs-lookup"><span data-stu-id="fcbc8-139">4. Route maps</span></span>
<span data-ttu-id="fcbc8-140">Vous pouvez utiliser les mappages de l’itinéraire et préfixe répertorie les préfixes toofilter propagés dans votre réseau.</span><span class="sxs-lookup"><span data-stu-id="fcbc8-140">You can use route-maps and prefix lists toofilter prefixes propagated into your network.</span></span> <span data-ttu-id="fcbc8-141">Vous pouvez utiliser l’exemple hello sous la tâche de hello tooaccomplish.</span><span class="sxs-lookup"><span data-stu-id="fcbc8-141">You can use hello sample below tooaccomplish hello task.</span></span> <span data-ttu-id="fcbc8-142">Assurez-vous d’avoir configuré les listes de préfixe appropriées.</span><span class="sxs-lookup"><span data-stu-id="fcbc8-142">Ensure that you have appropriate prefix lists setup.</span></span>

    router bgp <Customer_ASN>
     bgp log-neighbor-changes
     neighbor <IP#2_used_by_Azure> remote-as 12076
     !        
     address-family ipv4
      network <Prefix_to_be_advertised> mask <Subnet_mask>
      neighbor <IP#2_used_by_Azure> activate
      neighbor <IP#2_used_by_Azure> route-map <MS_Prefixes_Inbound> in
     exit-address-family
    !
    route-map <MS_Prefixes_Inbound> permit 10
     match ip address prefix-list <MS_Prefixes>
    !


## <a name="juniper-mx-series-routers"></a><span data-ttu-id="fcbc8-143">Routeurs de la série Juniper MX</span><span class="sxs-lookup"><span data-stu-id="fcbc8-143">Juniper MX series routers</span></span>
<span data-ttu-id="fcbc8-144">exemples de Hello dans cette section s’appliquent à tous les routeurs de série Juniper MX.</span><span class="sxs-lookup"><span data-stu-id="fcbc8-144">hello samples in this section apply for any Juniper MX series routers.</span></span>

### <a name="1-configuring-interfaces-and-sub-interfaces"></a><span data-ttu-id="fcbc8-145">1. Configuration des interfaces et des sous-interfaces</span><span class="sxs-lookup"><span data-stu-id="fcbc8-145">1. Configuring interfaces and sub-interfaces</span></span>

<span data-ttu-id="fcbc8-146">**Définition de l’interface Dot1Q**</span><span class="sxs-lookup"><span data-stu-id="fcbc8-146">**Dot1Q interface definition**</span></span>

<span data-ttu-id="fcbc8-147">Cet exemple fournit la définition de l’interface sous-chemin hello pour une interface secondaire avec un ID de réseau local virtuel unique.</span><span class="sxs-lookup"><span data-stu-id="fcbc8-147">This sample provides hello sub-interface definition for a sub-interface with a single VLAN ID.</span></span> <span data-ttu-id="fcbc8-148">Hello, ID de VLAN est unique pour chaque d’homologation.</span><span class="sxs-lookup"><span data-stu-id="fcbc8-148">hello VLAN ID is unique per peering.</span></span> <span data-ttu-id="fcbc8-149">Hello dernier octet de votre adresse IPv4 sera toujours un nombre impair.</span><span class="sxs-lookup"><span data-stu-id="fcbc8-149">hello last octet of your IPv4 address will always be an odd number.</span></span>

    interfaces {
        vlan-tagging;
        <Interface_Number> {
            unit <Number> {
                vlan-id <VLAN_ID>;
                family inet {
                    address <IPv4_Address/Subnet_Mask>;
                }
            }
        }
    }


<span data-ttu-id="fcbc8-150">**Définition de l’interface QinQ**</span><span class="sxs-lookup"><span data-stu-id="fcbc8-150">**QinQ interface definition**</span></span>

<span data-ttu-id="fcbc8-151">Cet exemple fournit la définition de l’interface sous-chemin hello pour une interface secondaire avec un ID de VLAN deux.</span><span class="sxs-lookup"><span data-stu-id="fcbc8-151">This sample provides hello sub-interface definition for a sub-interface with a two VLAN IDs.</span></span> <span data-ttu-id="fcbc8-152">Hello ID VLAN externe (s-tag), si utilisé reste hello même sur tous les homologations de hello.</span><span class="sxs-lookup"><span data-stu-id="fcbc8-152">hello outer VLAN ID (s-tag), if used remains hello same across all hello peerings.</span></span> <span data-ttu-id="fcbc8-153">interne de Hello ID de VLAN (c-tag) est unique pour chaque d’homologation.</span><span class="sxs-lookup"><span data-stu-id="fcbc8-153">hello inner VLAN ID (c-tag) is unique per peering.</span></span> <span data-ttu-id="fcbc8-154">Hello dernier octet de votre adresse IPv4 sera toujours un nombre impair.</span><span class="sxs-lookup"><span data-stu-id="fcbc8-154">hello last octet of your IPv4 address will always be an odd number.</span></span>

    interfaces {
        <Interface_Number> {
            flexible-vlan-tagging;
            unit <Number> {
                vlan-tags outer <S-tag> inner <C-tag>;
                family inet {
                    address <IPv4_Address/Subnet_Mask>;
                }                           
            }                               
        }                                   
    }                           

### <a name="2-setting-up-ebgp-sessions"></a><span data-ttu-id="fcbc8-155">2. Configuration de sessions eBGP</span><span class="sxs-lookup"><span data-stu-id="fcbc8-155">2. Setting up eBGP sessions</span></span>
<span data-ttu-id="fcbc8-156">Vous devez configurer une session BGP avec Microsoft pour chaque homologation.</span><span class="sxs-lookup"><span data-stu-id="fcbc8-156">You must setup a BGP session with Microsoft for every peering.</span></span> <span data-ttu-id="fcbc8-157">exemple Hello ci-dessous vous permet de toosetup une session BGP avec Microsoft.</span><span class="sxs-lookup"><span data-stu-id="fcbc8-157">hello sample below enables you toosetup a BGP session with Microsoft.</span></span> <span data-ttu-id="fcbc8-158">Si hello adresse IPv4 que vous avez utilisé pour votre interface sub était a.b.c.d, hello est adresse IP du voisin BGP de hello (Microsoft) est a.b.c.d+1.</span><span class="sxs-lookup"><span data-stu-id="fcbc8-158">If hello IPv4 address you used for your sub interface was a.b.c.d, hello IP address of hello BGP neighbor (Microsoft) will be a.b.c.d+1.</span></span> <span data-ttu-id="fcbc8-159">dernier octet de Hello d’adresse IPv4 du voisin hello BGP sera toujours un nombre pair.</span><span class="sxs-lookup"><span data-stu-id="fcbc8-159">hello last octet of hello BGP neighbor's IPv4 address will always be an even number.</span></span>

    routing-options {
        autonomous-system <Customer_ASN>;
    }
    }
    protocols {
        bgp { 
            group <Group_Name> { 
                peer-as 12076;              
                neighbor <IP#2_used_by_Azure>;
            }                               
        }                                   
    }

### <a name="3-setting-up-prefixes-toobe-advertised-over-hello-bgp-session"></a><span data-ttu-id="fcbc8-160">3. Configuration des préfixes toobe publiés sur la session BGP de hello</span><span class="sxs-lookup"><span data-stu-id="fcbc8-160">3. Setting up prefixes toobe advertised over hello BGP session</span></span>
<span data-ttu-id="fcbc8-161">Vous pouvez configurer votre tooMicrosoft de préfixes sélectionnez tooadvertise routeur.</span><span class="sxs-lookup"><span data-stu-id="fcbc8-161">You can configure your router tooadvertise select prefixes tooMicrosoft.</span></span> <span data-ttu-id="fcbc8-162">Cela à l’aide de hello exemple ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="fcbc8-162">You can do so using hello sample below.</span></span>

    policy-options {
        policy-statement <Policy_Name> {
            term 1 {
                from protocol OSPF;
        route-filter <Prefix_to_be_advertised/Subnet_Mask> exact;
                then {
                    accept;
                }
            }
        }
    }
    protocols {
        bgp { 
            group <Group_Name> { 
                export <Policy_Name>
                peer-as 12076;              
                neighbor <IP#2_used_by_Azure>;
            }                               
        }                                   
    }


### <a name="4-route-maps"></a><span data-ttu-id="fcbc8-163">4. Cartes d’itinéraire</span><span class="sxs-lookup"><span data-stu-id="fcbc8-163">4. Route maps</span></span>
<span data-ttu-id="fcbc8-164">Vous pouvez utiliser les mappages de l’itinéraire et préfixe répertorie les préfixes toofilter propagés dans votre réseau.</span><span class="sxs-lookup"><span data-stu-id="fcbc8-164">You can use route-maps and prefix lists toofilter prefixes propagated into your network.</span></span> <span data-ttu-id="fcbc8-165">Vous pouvez utiliser l’exemple hello sous la tâche de hello tooaccomplish.</span><span class="sxs-lookup"><span data-stu-id="fcbc8-165">You can use hello sample below tooaccomplish hello task.</span></span> <span data-ttu-id="fcbc8-166">Assurez-vous d’avoir configuré les listes de préfixe appropriées.</span><span class="sxs-lookup"><span data-stu-id="fcbc8-166">Ensure that you have appropriate prefix lists setup.</span></span>

    policy-options {
        prefix-list MS_Prefixes {
            <IP_Prefix_1/Subnet_Mask>;
            <IP_Prefix_2/Subnet_Mask>;
        }
        policy-statement <MS_Prefixes_Inbound> {
            term 1 {
                from {
        prefix-list MS_Prefixes;
                }
                then {
                    accept;
                }
            }
        }
    }
    protocols {
        bgp { 
            group <Group_Name> { 
                export <Policy_Name>
                import <MS_Prefixes_Inbound>
                peer-as 12076;              
                neighbor <IP#2_used_by_Azure>;
            }                               
        }                                   
    }

## <a name="next-steps"></a><span data-ttu-id="fcbc8-167">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="fcbc8-167">Next Steps</span></span>
<span data-ttu-id="fcbc8-168">Consultez hello [FAQ sur ExpressRoute](expressroute-faqs.md) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="fcbc8-168">See hello [ExpressRoute FAQ](expressroute-faqs.md) for more details.</span></span>

