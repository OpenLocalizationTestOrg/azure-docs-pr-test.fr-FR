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
# <a name="router-configuration-samples-tooset-up-and-manage-routing"></a>Configuration du routeur exemples tooset haut et gérer le routage
Cette page fournit une interface et des exemples de configuration de routage pour les routeurs des séries Cisco IOS-XE et Juniper MX. Ces exemples toobe prévue à titre indicatif et ne doivent pas être utilisés en l’état. Vous pouvez travailler avec votre fournisseur toocome configurations appropriées pour votre réseau. 

> [!IMPORTANT]
> Les exemples dans cette page sont toobe prévu uniquement pour obtenir des conseils. Vous devez collaborer avec l’équipe de vente / technique de votre fournisseur et votre toocome équipe mise en réseau haut avec toomeet de configurations appropriées à vos besoins. Microsoft ne prendra pas en charge des problèmes liés tooconfigurations répertoriées dans cette page. Vous devez contacter le fournisseur de votre périphérique pour la prise en charge des problèmes.
> 
> 

## <a name="mtu-and-tcp-mss-settings-on-router-interfaces"></a>Paramètres MTU et TCP MSS sur les interfaces de routeur
* Hello MTU pour l’interface de ExpressRoute hello est 1500, hello classique MTU par défaut pour une interface Ethernet sur un routeur. À moins que votre routeur possède une MTU différentes par défaut, il n’existe aucune toospecify besoin une valeur sur l’interface de routeur hello.
* Contrairement à une passerelle VPN Azure, hello MSS de TCP pour un circuit ExpressRoute n’a pas besoin toobe spécifié.

Exemples de configuration du routeur ci-dessous s’appliquent tooall homologations. Pour plus d’informations sur le routage, voir [Homologations ExpressRoute](expressroute-circuit-peerings.md) et [Configuration requise pour le routage ExpressRoute](expressroute-routing.md).


## <a name="cisco-ios-xe-based-routers"></a>Routeurs Cisco IOS-XE
exemples de Hello dans cette section s’appliquent à tous les routeurs de famille du système d’exploitation IOS-XE hello en cours d’exécution.

### <a name="1-configuring-interfaces-and-sub-interfaces"></a>1. Configuration des interfaces et des sous-interfaces
Vous aurez besoin d’une interface sub par homologation dans chaque routeur, vous connecter tooMicrosoft. Une sous-interface peut être identifiée avec un ID de réseau local virtuel ou une paire empilée d’ID de réseau local virtuel, et une adresse IP.

**Définition de l’interface Dot1Q**

Cet exemple fournit la définition de l’interface sous-chemin hello pour une interface secondaire avec un ID de réseau local virtuel unique. Hello, ID de VLAN est unique pour chaque d’homologation. Hello dernier octet de votre adresse IPv4 sera toujours un nombre impair.

    interface GigabitEthernet<Interface_Number>.<Number>
     encapsulation dot1Q <VLAN_ID>
     ip address <IPv4_Address><Subnet_Mask>

**Définition de l’interface QinQ**

Cet exemple fournit la définition de l’interface sous-chemin hello pour une interface secondaire avec un ID de VLAN deux. Hello ID VLAN externe (s-tag), si utilisé reste hello même sur tous les homologations de hello. interne de Hello ID de VLAN (c-tag) est unique pour chaque d’homologation. Hello dernier octet de votre adresse IPv4 sera toujours un nombre impair.

    interface GigabitEthernet<Interface_Number>.<Number>
     encapsulation dot1Q <s-tag> seconddot1Q <c-tag>
     ip address <IPv4_Address><Subnet_Mask>

### <a name="2-setting-up-ebgp-sessions"></a>2. Configuration de sessions eBGP
Vous devez configurer une session BGP avec Microsoft pour chaque homologation. exemple Hello ci-dessous vous permet de toosetup une session BGP avec Microsoft. Si hello adresse IPv4 que vous avez utilisé pour votre interface sub était a.b.c.d, hello est adresse IP du voisin BGP de hello (Microsoft) est a.b.c.d+1. dernier octet de Hello d’adresse IPv4 du voisin hello BGP sera toujours un nombre pair.

    router bgp <Customer_ASN>
     bgp log-neighbor-changes
     neighbor <IP#2_used_by_Azure> remote-as 12076
     !        
     address-family ipv4
     neighbor <IP#2_used_by_Azure> activate
     exit-address-family
    !

### <a name="3-setting-up-prefixes-toobe-advertised-over-hello-bgp-session"></a>3. Configuration des préfixes toobe publiés sur la session BGP de hello
Vous pouvez configurer votre tooMicrosoft de préfixes sélectionnez tooadvertise routeur. Cela à l’aide de hello exemple ci-dessous.

    router bgp <Customer_ASN>
     bgp log-neighbor-changes
     neighbor <IP#2_used_by_Azure> remote-as 12076
     !        
     address-family ipv4
      network <Prefix_to_be_advertised> mask <Subnet_mask>
      neighbor <IP#2_used_by_Azure> activate
     exit-address-family
    !

### <a name="4-route-maps"></a>4. Cartes d’itinéraire
Vous pouvez utiliser les mappages de l’itinéraire et préfixe répertorie les préfixes toofilter propagés dans votre réseau. Vous pouvez utiliser l’exemple hello sous la tâche de hello tooaccomplish. Assurez-vous d’avoir configuré les listes de préfixe appropriées.

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


## <a name="juniper-mx-series-routers"></a>Routeurs de la série Juniper MX
exemples de Hello dans cette section s’appliquent à tous les routeurs de série Juniper MX.

### <a name="1-configuring-interfaces-and-sub-interfaces"></a>1. Configuration des interfaces et des sous-interfaces

**Définition de l’interface Dot1Q**

Cet exemple fournit la définition de l’interface sous-chemin hello pour une interface secondaire avec un ID de réseau local virtuel unique. Hello, ID de VLAN est unique pour chaque d’homologation. Hello dernier octet de votre adresse IPv4 sera toujours un nombre impair.

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


**Définition de l’interface QinQ**

Cet exemple fournit la définition de l’interface sous-chemin hello pour une interface secondaire avec un ID de VLAN deux. Hello ID VLAN externe (s-tag), si utilisé reste hello même sur tous les homologations de hello. interne de Hello ID de VLAN (c-tag) est unique pour chaque d’homologation. Hello dernier octet de votre adresse IPv4 sera toujours un nombre impair.

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

### <a name="2-setting-up-ebgp-sessions"></a>2. Configuration de sessions eBGP
Vous devez configurer une session BGP avec Microsoft pour chaque homologation. exemple Hello ci-dessous vous permet de toosetup une session BGP avec Microsoft. Si hello adresse IPv4 que vous avez utilisé pour votre interface sub était a.b.c.d, hello est adresse IP du voisin BGP de hello (Microsoft) est a.b.c.d+1. dernier octet de Hello d’adresse IPv4 du voisin hello BGP sera toujours un nombre pair.

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

### <a name="3-setting-up-prefixes-toobe-advertised-over-hello-bgp-session"></a>3. Configuration des préfixes toobe publiés sur la session BGP de hello
Vous pouvez configurer votre tooMicrosoft de préfixes sélectionnez tooadvertise routeur. Cela à l’aide de hello exemple ci-dessous.

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


### <a name="4-route-maps"></a>4. Cartes d’itinéraire
Vous pouvez utiliser les mappages de l’itinéraire et préfixe répertorie les préfixes toofilter propagés dans votre réseau. Vous pouvez utiliser l’exemple hello sous la tâche de hello tooaccomplish. Assurez-vous d’avoir configuré les listes de préfixe appropriées.

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

## <a name="next-steps"></a>Étapes suivantes
Consultez hello [FAQ sur ExpressRoute](expressroute-faqs.md) pour plus d’informations.

