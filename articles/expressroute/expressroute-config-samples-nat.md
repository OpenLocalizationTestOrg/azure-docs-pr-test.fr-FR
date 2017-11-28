---
title: exemples de configuration de routeur de clients aaaExpressRoute | Documents Microsoft
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
ms.openlocfilehash: b5faca0666bda6173e54abb0b6560d5f8bf8bfc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="router-configuration-samples-tooset-up-and-manage-nat"></a><span data-ttu-id="0d4ce-103">Configuration du routeur exemples tooset haut et gérer des NAT</span><span class="sxs-lookup"><span data-stu-id="0d4ce-103">Router configuration samples tooset up and manage NAT</span></span>
<span data-ttu-id="0d4ce-104">Cette page fournit des exemples de configuration NAT pour les routeurs des séries Cisco ASA et Juniper SRX.</span><span class="sxs-lookup"><span data-stu-id="0d4ce-104">This page provides NAT configuration samples for Cisco ASA and Juniper SRX series routers.</span></span> <span data-ttu-id="0d4ce-105">Ces exemples toobe prévue à titre indicatif et ne doivent pas être utilisés en l’état.</span><span class="sxs-lookup"><span data-stu-id="0d4ce-105">These are intended toobe samples for guidance only and must not be used as is.</span></span> <span data-ttu-id="0d4ce-106">Vous pouvez travailler avec votre fournisseur toocome configurations appropriées pour votre réseau.</span><span class="sxs-lookup"><span data-stu-id="0d4ce-106">You can work with your vendor toocome up with appropriate configurations for your network.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="0d4ce-107">Les exemples dans cette page sont toobe prévu uniquement pour obtenir des conseils.</span><span class="sxs-lookup"><span data-stu-id="0d4ce-107">Samples in this page are intended toobe purely for guidance.</span></span> <span data-ttu-id="0d4ce-108">Vous devez collaborer avec l’équipe de vente / technique de votre fournisseur et votre toocome équipe mise en réseau haut avec toomeet de configurations appropriées à vos besoins.</span><span class="sxs-lookup"><span data-stu-id="0d4ce-108">You must work with your vendor's sales / technical team and your networking team toocome up with appropriate configurations toomeet your needs.</span></span> <span data-ttu-id="0d4ce-109">Microsoft ne prendra pas en charge des problèmes liés tooconfigurations répertoriées dans cette page.</span><span class="sxs-lookup"><span data-stu-id="0d4ce-109">Microsoft will not support issues related tooconfigurations listed in this page.</span></span> <span data-ttu-id="0d4ce-110">Vous devez contacter le fournisseur de votre périphérique pour la prise en charge des problèmes.</span><span class="sxs-lookup"><span data-stu-id="0d4ce-110">You must contact your device vendor for support issues.</span></span>
> 
> 

* <span data-ttu-id="0d4ce-111">Exemples de configuration du routeur ci-dessous s’appliquent tooAzure des homologations Public et Microsoft.</span><span class="sxs-lookup"><span data-stu-id="0d4ce-111">Router configuration samples below apply tooAzure Public and Microsoft peerings.</span></span> <span data-ttu-id="0d4ce-112">Vous ne devez pas configurer un système NAT pour l'homologation privée Azure.</span><span class="sxs-lookup"><span data-stu-id="0d4ce-112">You must not configure NAT for Azure private peering.</span></span> <span data-ttu-id="0d4ce-113">Pour plus d’informations, voir [Homologations ExpressRoute](expressroute-circuit-peerings.md) et [Configuration NAT requise pour ExpressRoute](expressroute-nat.md).</span><span class="sxs-lookup"><span data-stu-id="0d4ce-113">Review [ExpressRoute peerings](expressroute-circuit-peerings.md) and [ExpressRoute NAT requirements](expressroute-nat.md) for more details.</span></span>

* <span data-ttu-id="0d4ce-114">Vous devez utiliser distinct des pools IP NAT pour toohello de connectivité internet et ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="0d4ce-114">You MUST use separate NAT IP pools for connectivity toohello internet and ExpressRoute.</span></span> <span data-ttu-id="0d4ce-115">À l’aide de hello même IP NAT pool sur hello internet et ExpressRoute entraîne la perte de connectivité et routage asymétrique.</span><span class="sxs-lookup"><span data-stu-id="0d4ce-115">Using hello same NAT IP pool across hello internet and ExpressRoute will result in asymmetric routing and loss of connectivity.</span></span>


## <a name="cisco-asa-firewalls"></a><span data-ttu-id="0d4ce-116">Pare-feu Cisco ASA</span><span class="sxs-lookup"><span data-stu-id="0d4ce-116">Cisco ASA firewalls</span></span>
### <a name="pat-configuration-for-traffic-from-customer-network-toomicrosoft"></a><span data-ttu-id="0d4ce-117">Configuration de PAT pour le trafic de client réseau tooMicrosoft</span><span class="sxs-lookup"><span data-stu-id="0d4ce-117">PAT configuration for traffic from customer network tooMicrosoft</span></span>
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

### <a name="pat-configuration-for-traffic-from-microsoft-toocustomer-network"></a><span data-ttu-id="0d4ce-118">Configuration de PAT pour le trafic réseau de toocustomer Microsoft</span><span class="sxs-lookup"><span data-stu-id="0d4ce-118">PAT configuration for traffic from Microsoft toocustomer network</span></span>

<span data-ttu-id="0d4ce-119">**Interfaces et sens :**</span><span class="sxs-lookup"><span data-stu-id="0d4ce-119">**Interfaces and Direction:**</span></span>

    Source Interface (where hello traffic enters hello ASA): inside
    Destination Interface (where hello traffic exits hello ASA): outside

<span data-ttu-id="0d4ce-120">**Configuration :**</span><span class="sxs-lookup"><span data-stu-id="0d4ce-120">**Configuration:**</span></span>

<span data-ttu-id="0d4ce-121">Pool NAT :</span><span class="sxs-lookup"><span data-stu-id="0d4ce-121">NAT Pool:</span></span>

    object network outbound-PAT
        host <NAT-IP>

<span data-ttu-id="0d4ce-122">Serveur cible :</span><span class="sxs-lookup"><span data-stu-id="0d4ce-122">Target Server:</span></span>

    object network Customer-Network
        network-object <IP> <Subnet-Mask>

<span data-ttu-id="0d4ce-123">Groupe d’objets pour les adresses IP de clients</span><span class="sxs-lookup"><span data-stu-id="0d4ce-123">Object Group for Customer IP Addresses</span></span>

    object-group network MSFT-Network-1
        network-object <MSFT-IP> <Subnet-Mask>

    object-group network MSFT-PAT-Networks
        network-object object MSFT-Network-1

<span data-ttu-id="0d4ce-124">Commandes NAT :</span><span class="sxs-lookup"><span data-stu-id="0d4ce-124">NAT Commands:</span></span>

    nat (inside,outside) source dynamic MSFT-PAT-Networks pat-pool outbound-PAT destination static Customer-Network Customer-Network


## <a name="juniper-srx-series-routers"></a><span data-ttu-id="0d4ce-125">Routeurs de la série Juniper SRX</span><span class="sxs-lookup"><span data-stu-id="0d4ce-125">Juniper SRX series routers</span></span>
### <a name="1-create-redundant-ethernet-interfaces-for-hello-cluster"></a><span data-ttu-id="0d4ce-126">1. Créer des interfaces Ethernet redondant pour un cluster de hello</span><span class="sxs-lookup"><span data-stu-id="0d4ce-126">1. Create redundant Ethernet interfaces for hello cluster</span></span>
    interfaces {
        reth0 {
            description "tooInternal Network";
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
            description "tooMicrosoft via Edge Router";
            vlan-tagging;
            redundant-ether-options {
                redundancy-group 2;
            }
            unit 100 {
                description "tooMicrosoft via Edge Router";
                vlan-id 100;
                family inet {
                    address <IP-Address/Subnet-mask>;
                }
            }
        }
    }


### <a name="2-create-two-security-zones"></a><span data-ttu-id="0d4ce-127">2. Création de deux zones de sécurité</span><span class="sxs-lookup"><span data-stu-id="0d4ce-127">2. Create two security zones</span></span>
* <span data-ttu-id="0d4ce-128">Zone approuvée pour le réseau interne et zone non approuvée pour les routeurs accessibles depuis le réseau externe</span><span class="sxs-lookup"><span data-stu-id="0d4ce-128">Trust Zone for internal network and Untrust Zone for external network facing Edge Routers</span></span>
* <span data-ttu-id="0d4ce-129">Attribuer les interfaces appropriées toohello zones</span><span class="sxs-lookup"><span data-stu-id="0d4ce-129">Assign appropriate interfaces toohello zones</span></span>
* <span data-ttu-id="0d4ce-130">Autoriser les services sur des interfaces de hello</span><span class="sxs-lookup"><span data-stu-id="0d4ce-130">Allow services on hello interfaces</span></span>

    <span data-ttu-id="0d4ce-131">security {       zones {           security-zone Trust {               host-inbound-traffic {                   system-services {                       ping;                   }                   protocols {                       bgp;                   }               }               interfaces {                   reth0.100;               }           }           security-zone Untrust {               host-inbound-traffic {                   system-services {                       ping;                   }                   protocols {                       bgp;                   }               }               interfaces {                   reth1.100;               }           }       }   }</span><span class="sxs-lookup"><span data-stu-id="0d4ce-131">security {       zones {           security-zone Trust {               host-inbound-traffic {                   system-services {                       ping;                   }                   protocols {                       bgp;                   }               }               interfaces {                   reth0.100;               }           }           security-zone Untrust {               host-inbound-traffic {                   system-services {                       ping;                   }                   protocols {                       bgp;                   }               }               interfaces {                   reth1.100;               }           }       }   }</span></span>


### <a name="3-create-security-policies-between-zones"></a><span data-ttu-id="0d4ce-132">3. Création des stratégies de sécurité entre les zones</span><span class="sxs-lookup"><span data-stu-id="0d4ce-132">3. Create security policies between zones</span></span>
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


### <a name="4-configure-nat-policies"></a><span data-ttu-id="0d4ce-133">4. Configuration des stratégies NAT</span><span class="sxs-lookup"><span data-stu-id="0d4ce-133">4. Configure NAT policies</span></span>
* <span data-ttu-id="0d4ce-134">Créez deux pools NAT.</span><span class="sxs-lookup"><span data-stu-id="0d4ce-134">Create two NAT pools.</span></span> <span data-ttu-id="0d4ce-135">Sera tooMicrosoft de tooNAT utilisé le trafic sortant et l’autre à partir de toohello service clientèle Microsoft.</span><span class="sxs-lookup"><span data-stu-id="0d4ce-135">One will be used tooNAT traffic outbound tooMicrosoft and other from Microsoft toohello customer.</span></span>
* <span data-ttu-id="0d4ce-136">Créer des règles de trafic respectifs de hello tooNAT</span><span class="sxs-lookup"><span data-stu-id="0d4ce-136">Create rules tooNAT hello respective traffic</span></span>
  
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
                       toorouting-instance External-ExpressRoute;
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
                       toorouting-instance Internal;
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

### <a name="5-configure-bgp-tooadvertise-selective-prefixes-in-each-direction"></a><span data-ttu-id="0d4ce-137">5. Configurer les préfixes BGP tooadvertise sélectives dans chaque direction</span><span class="sxs-lookup"><span data-stu-id="0d4ce-137">5. Configure BGP tooadvertise selective prefixes in each direction</span></span>
<span data-ttu-id="0d4ce-138">Consultez toosamples dans [exemples de configuration de routage ](expressroute-config-samples-routing.md) page.</span><span class="sxs-lookup"><span data-stu-id="0d4ce-138">Refer toosamples in [Routing configuration samples ](expressroute-config-samples-routing.md) page.</span></span>

### <a name="6-create-policies"></a><span data-ttu-id="0d4ce-139">6. Création des stratégies</span><span class="sxs-lookup"><span data-stu-id="0d4ce-139">6. Create policies</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="0d4ce-140">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0d4ce-140">Next steps</span></span>
<span data-ttu-id="0d4ce-141">Consultez hello [FAQ sur ExpressRoute](expressroute-faqs.md) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="0d4ce-141">See hello [ExpressRoute FAQ](expressroute-faqs.md) for more details.</span></span>

