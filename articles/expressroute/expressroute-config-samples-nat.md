---
title: Exemples de configuration des routeurs clients ExpressRoute | Microsoft Docs
description: Cette page fournit des exemples de configuration pour les routeurs Cisco et Juniper.
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
ms.assetid: d6ea716f-d5ee-4a61-92b0-640d6e7d6974
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/10/2016
ms.author: cherylmc
ms.openlocfilehash: 83a7da2db537a3c900e90432455d59e8ac56d917
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="router-configuration-samples-to-set-up-and-manage-nat"></a><span data-ttu-id="77a56-103">Exemples de configuration de routeur pour configurer et gérer des NAT</span><span class="sxs-lookup"><span data-stu-id="77a56-103">Router configuration samples to set up and manage NAT</span></span>
<span data-ttu-id="77a56-104">Cette page fournit des exemples de configuration NAT pour les routeurs des séries Cisco ASA et Juniper SRX.</span><span class="sxs-lookup"><span data-stu-id="77a56-104">This page provides NAT configuration samples for Cisco ASA and Juniper SRX series routers.</span></span> <span data-ttu-id="77a56-105">Ces exemples sont fournis à titre indicatif uniquement et ne doivent pas être utilisés en l’état.</span><span class="sxs-lookup"><span data-stu-id="77a56-105">These are intended to be samples for guidance only and must not be used as is.</span></span> <span data-ttu-id="77a56-106">Vous pouvez vous adresser au fournisseur pour rechercher les configurations adaptées à votre réseau.</span><span class="sxs-lookup"><span data-stu-id="77a56-106">You can work with your vendor to come up with appropriate configurations for your network.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="77a56-107">Les exemples de cette page sont fournis à titre purement indicatif.</span><span class="sxs-lookup"><span data-stu-id="77a56-107">Samples in this page are intended to be purely for guidance.</span></span> <span data-ttu-id="77a56-108">Vous devez vous adresser à l’équipe commerciale/technique de votre fournisseur et à votre équipe de mise en réseau pour rechercher les configurations adaptées à vos besoins.</span><span class="sxs-lookup"><span data-stu-id="77a56-108">You must work with your vendor's sales / technical team and your networking team to come up with appropriate configurations to meet your needs.</span></span> <span data-ttu-id="77a56-109">Microsoft ne prend pas en charge les problèmes liés aux configurations répertoriées dans cette page.</span><span class="sxs-lookup"><span data-stu-id="77a56-109">Microsoft will not support issues related to configurations listed in this page.</span></span> <span data-ttu-id="77a56-110">Vous devez contacter le fournisseur de votre périphérique pour la prise en charge des problèmes.</span><span class="sxs-lookup"><span data-stu-id="77a56-110">You must contact your device vendor for support issues.</span></span>
> 
> 

* <span data-ttu-id="77a56-111">Les exemples de configuration de routeur ci-dessous s'appliquent aux homologations Azure Public et Microsoft.</span><span class="sxs-lookup"><span data-stu-id="77a56-111">Router configuration samples below apply to Azure Public and Microsoft peerings.</span></span> <span data-ttu-id="77a56-112">Vous ne devez pas configurer un système NAT pour l'homologation privée Azure.</span><span class="sxs-lookup"><span data-stu-id="77a56-112">You must not configure NAT for Azure private peering.</span></span> <span data-ttu-id="77a56-113">Pour plus d’informations, voir [Homologations ExpressRoute](expressroute-circuit-peerings.md) et [Configuration NAT requise pour ExpressRoute](expressroute-nat.md).</span><span class="sxs-lookup"><span data-stu-id="77a56-113">Review [ExpressRoute peerings](expressroute-circuit-peerings.md) and [ExpressRoute NAT requirements](expressroute-nat.md) for more details.</span></span>

* <span data-ttu-id="77a56-114">Vous DEVEZ utiliser des pools IP NAT distincts pour la connectivité à Internet et ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="77a56-114">You MUST use separate NAT IP pools for connectivity to the internet and ExpressRoute.</span></span> <span data-ttu-id="77a56-115">L’utilisation du même pool IP NAT via internet et ExpressRoute entraîne un routage asymétrique et une perte de connectivité.</span><span class="sxs-lookup"><span data-stu-id="77a56-115">Using the same NAT IP pool across the internet and ExpressRoute will result in asymmetric routing and loss of connectivity.</span></span>


## <a name="cisco-asa-firewalls"></a><span data-ttu-id="77a56-116">Pare-feu Cisco ASA</span><span class="sxs-lookup"><span data-stu-id="77a56-116">Cisco ASA firewalls</span></span>
### <a name="pat-configuration-for-traffic-from-customer-network-to-microsoft"></a><span data-ttu-id="77a56-117">Configuration PAT pour le trafic du réseau client à Microsoft</span><span class="sxs-lookup"><span data-stu-id="77a56-117">PAT configuration for traffic from customer network to Microsoft</span></span>
    object network MSFT-PAT
      range <SNAT-START-IP> <SNAT-END-IP>


    object-group network MSFT-Range
      network-object <IP> <Subnet_Mask>

    object-group network on-prem-range-1
      network-object <IP> <Subnet-Mask>

    object-group network on-prem-range-2
      network-object <IP> <Subnet-Mask>

    object-group network on-prem
      network-object object on-prem-range-1
      network-object object on-prem-range-2

    nat (outside,inside) source dynamic on-prem pat-pool MSFT-PAT destination static MSFT-Range MSFT-Range

### <a name="pat-configuration-for-traffic-from-microsoft-to-customer-network"></a><span data-ttu-id="77a56-118">Configuration PAT pour le trafic de Microsoft au réseau client</span><span class="sxs-lookup"><span data-stu-id="77a56-118">PAT configuration for traffic from Microsoft to customer network</span></span>

<span data-ttu-id="77a56-119">**Interfaces et sens :**</span><span class="sxs-lookup"><span data-stu-id="77a56-119">**Interfaces and Direction:**</span></span>

    Source Interface (where the traffic enters the ASA): inside
    Destination Interface (where the traffic exits the ASA): outside

<span data-ttu-id="77a56-120">**Configuration :**</span><span class="sxs-lookup"><span data-stu-id="77a56-120">**Configuration:**</span></span>

<span data-ttu-id="77a56-121">Pool NAT :</span><span class="sxs-lookup"><span data-stu-id="77a56-121">NAT Pool:</span></span>

    object network outbound-PAT
        host <NAT-IP>

<span data-ttu-id="77a56-122">Serveur cible :</span><span class="sxs-lookup"><span data-stu-id="77a56-122">Target Server:</span></span>

    object network Customer-Network
        network-object <IP> <Subnet-Mask>

<span data-ttu-id="77a56-123">Groupe d’objets pour les adresses IP de clients</span><span class="sxs-lookup"><span data-stu-id="77a56-123">Object Group for Customer IP Addresses</span></span>

    object-group network MSFT-Network-1
        network-object <MSFT-IP> <Subnet-Mask>

    object-group network MSFT-PAT-Networks
        network-object object MSFT-Network-1

<span data-ttu-id="77a56-124">Commandes NAT :</span><span class="sxs-lookup"><span data-stu-id="77a56-124">NAT Commands:</span></span>

    nat (inside,outside) source dynamic MSFT-PAT-Networks pat-pool outbound-PAT destination static Customer-Network Customer-Network


## <a name="juniper-srx-series-routers"></a><span data-ttu-id="77a56-125">Routeurs de la série Juniper SRX</span><span class="sxs-lookup"><span data-stu-id="77a56-125">Juniper SRX series routers</span></span>
### <a name="1-create-redundant-ethernet-interfaces-for-the-cluster"></a><span data-ttu-id="77a56-126">1. Création d’interfaces Ethernet redondantes pour le cluster</span><span class="sxs-lookup"><span data-stu-id="77a56-126">1. Create redundant Ethernet interfaces for the cluster</span></span>
    interfaces {
        reth0 {
            description "To Internal Network";
            vlan-tagging;
            redundant-ether-options {
                redundancy-group 1;
            }
            unit 100 {
                vlan-id 100;
                family inet {
                    address <IP-Address/Subnet-mask>;
                }
            }
        }
        reth1 {
            description "To Microsoft via Edge Router";
            vlan-tagging;
            redundant-ether-options {
                redundancy-group 2;
            }
            unit 100 {
                description "To Microsoft via Edge Router";
                vlan-id 100;
                family inet {
                    address <IP-Address/Subnet-mask>;
                }
            }
        }
    }


### <a name="2-create-two-security-zones"></a><span data-ttu-id="77a56-127">2. Création de deux zones de sécurité</span><span class="sxs-lookup"><span data-stu-id="77a56-127">2. Create two security zones</span></span>
* <span data-ttu-id="77a56-128">Zone approuvée pour le réseau interne et zone non approuvée pour les routeurs accessibles depuis le réseau externe</span><span class="sxs-lookup"><span data-stu-id="77a56-128">Trust Zone for internal network and Untrust Zone for external network facing Edge Routers</span></span>
* <span data-ttu-id="77a56-129">Affectation des interfaces appropriées aux zones</span><span class="sxs-lookup"><span data-stu-id="77a56-129">Assign appropriate interfaces to the zones</span></span>
* <span data-ttu-id="77a56-130">Autorisation des services sur les interfaces</span><span class="sxs-lookup"><span data-stu-id="77a56-130">Allow services on the interfaces</span></span>

    <span data-ttu-id="77a56-131">security {       zones {           security-zone Trust {               host-inbound-traffic {                   system-services {                       ping;                   }                   protocols {                       bgp;                   }               }               interfaces {                   reth0.100;               }           }           security-zone Untrust {               host-inbound-traffic {                   system-services {                       ping;                   }                   protocols {                       bgp;                   }               }               interfaces {                   reth1.100;               }           }       }   }</span><span class="sxs-lookup"><span data-stu-id="77a56-131">security {       zones {           security-zone Trust {               host-inbound-traffic {                   system-services {                       ping;                   }                   protocols {                       bgp;                   }               }               interfaces {                   reth0.100;               }           }           security-zone Untrust {               host-inbound-traffic {                   system-services {                       ping;                   }                   protocols {                       bgp;                   }               }               interfaces {                   reth1.100;               }           }       }   }</span></span>


### <a name="3-create-security-policies-between-zones"></a><span data-ttu-id="77a56-132">3. Création des stratégies de sécurité entre les zones</span><span class="sxs-lookup"><span data-stu-id="77a56-132">3. Create security policies between zones</span></span>
    security {
        policies {
            from-zone Trust to-zone Untrust {
                policy allow-any {
                    match {
                        source-address any;
                        destination-address any;
                        application any;
                    }
                    then {
                        permit;
                    }
                }
            }
            from-zone Untrust to-zone Trust {
                policy allow-any {
                    match {
                        source-address any;
                        destination-address any;
                        application any;
                    }
                    then {
                        permit;
                    }
                }
            }
        }
    }


### <a name="4-configure-nat-policies"></a><span data-ttu-id="77a56-133">4. Configuration des stratégies NAT</span><span class="sxs-lookup"><span data-stu-id="77a56-133">4. Configure NAT policies</span></span>
* <span data-ttu-id="77a56-134">Créez deux pools NAT.</span><span class="sxs-lookup"><span data-stu-id="77a56-134">Create two NAT pools.</span></span> <span data-ttu-id="77a56-135">Un pool servira au trafic NAT sortant vers Microsoft et un autre au trafic de Microsoft vers le client.</span><span class="sxs-lookup"><span data-stu-id="77a56-135">One will be used to NAT traffic outbound to Microsoft and other from Microsoft to the customer.</span></span>
* <span data-ttu-id="77a56-136">Création des règles NAT pour le trafic respectif</span><span class="sxs-lookup"><span data-stu-id="77a56-136">Create rules to NAT the respective traffic</span></span>
  
       security {
           nat {
               source {
                   pool SNAT-To-ExpressRoute {
                       routing-instance {
                           External-ExpressRoute;
                       }
                       address {
                           <NAT-IP-address/Subnet-mask>;
                       }
                   }
                   pool SNAT-From-ExpressRoute {
                       routing-instance {
                           Internal;
                       }
                       address {
                           <NAT-IP-address/Subnet-mask>;
                       }
                   }
                   rule-set Outbound_NAT {
                       from routing-instance Internal;
                       to routing-instance External-ExpressRoute;
                       rule SNAT-Out {
                           match {
                               source-address 0.0.0.0/0;
                           }
                           then {
                               source-nat {
                                   pool {
                                       SNAT-To-ExpressRoute;
                                   }
                               }
                           }
                       }
                   }
                   rule-set Inbound-NAT {
                       from routing-instance External-ExpressRoute;
                       to routing-instance Internal;
                       rule SNAT-In {
                           match {
                               source-address 0.0.0.0/0;
                           }
                           then {
                               source-nat {
                                   pool {
                                       SNAT-From-ExpressRoute;
                                   }
                               }
                           }
                       }
                   }
               }
           }
       }

### <a name="5-configure-bgp-to-advertise-selective-prefixes-in-each-direction"></a><span data-ttu-id="77a56-137">5. Configuration de BGP pour publier les préfixes sélectifs dans chaque direction</span><span class="sxs-lookup"><span data-stu-id="77a56-137">5. Configure BGP to advertise selective prefixes in each direction</span></span>
<span data-ttu-id="77a56-138">Consultez les exemples de la page [Exemples de configuration de routage ](expressroute-config-samples-routing.md) .</span><span class="sxs-lookup"><span data-stu-id="77a56-138">Refer to samples in [Routing configuration samples ](expressroute-config-samples-routing.md) page.</span></span>

### <a name="6-create-policies"></a><span data-ttu-id="77a56-139">6. Création des stratégies</span><span class="sxs-lookup"><span data-stu-id="77a56-139">6. Create policies</span></span>
    routing-options {
                  autonomous-system <Customer-ASN>;
    }
    policy-options {
        prefix-list Microsoft-Prefixes {
            <IP-Address/Subnet-Mask;
            <IP-Address/Subnet-Mask;
        }
        prefix-list private-ranges {
            10.0.0.0/8;
            172.16.0.0/12;
            192.168.0.0/16;
            100.64.0.0/10;
        }
        policy-statement Advertise-NAT-Pools {
            from {
                protocol static;
                route-filter <NAT-Pool-Address/Subnet-mask> prefix-length-range /32-/32;
            }
            then accept;
        }
        policy-statement Accept-from-Microsoft {
            term 1 {
                from {
                    instance External-ExpressRoute;
                    prefix-list-filter Microsoft-Prefixes orlonger;
                }
                then accept;
            }
            term deny {
                then reject;
            }
        }
        policy-statement Accept-from-Internal {
            term no-private {
                from {
                    instance Internal;
                    prefix-list-filter private-ranges orlonger;
                }
                then reject;
            }
            term bgp {
                from {
                    instance Internal;
                    protocol bgp;
                }
                then accept;
            }
            term deny {
                then reject;
            }
        }
    }
    routing-instances {
        Internal {
            instance-type virtual-router;
            interface reth0.100;
            routing-options {
                static {
                    route <NAT-Pool-IP-Address/Subnet-mask> discard;
                }
                instance-import Accept-from-Microsoft;
            }
            protocols {
                bgp {
                    group customer {
                        export <Advertise-NAT-Pools>;
                        peer-as <Customer-ASN-1>;
                        neighbor <BGP-Neighbor-IP-Address>;
                    }
                }
            }
        }
        External-ExpressRoute {
            instance-type virtual-router;
            interface reth1.100;
            routing-options {
                static {
                    route <NAT-Pool-IP-Address/Subnet-mask> discard;
                }
                instance-import Accept-from-Internal;
            }
            protocols {
                bgp {
                    group edge-router {
                        export <Advertise-NAT-Pools>;
                        peer-as <Customer-Public-ASN>;
                        neighbor <BGP-Neighbor-IP-Address>;
                    }
                }
            }
        }
    }

## <a name="next-steps"></a><span data-ttu-id="77a56-140">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="77a56-140">Next steps</span></span>
<span data-ttu-id="77a56-141">Pour plus d’informations, consultez le [Forum Aux Questions sur ExpressRoute](expressroute-faqs.md) .</span><span class="sxs-lookup"><span data-stu-id="77a56-141">See the [ExpressRoute FAQ](expressroute-faqs.md) for more details.</span></span>

