---
title: "aaaTroubleshoot VPN de Site à Site Azure se déconnecte de façon intermittente | Documents Microsoft"
description: "Découvrez comment tootroubleshoot hello problème de connexion VPN de Site à Site hello déconnectée régulièrement."
services: vpn-gateway
documentationcenter: na
author: chadmath
manager: cshepard
editor: 
tags: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/21/2017
ms.author: genli
ms.openlocfilehash: 1ce3c4ff9d8f650312e45f33b760ebcc6597fc13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-site-to-site-vpn-disconnects-intermittently"></a>Résolution des problèmes : déconnexion intermittente du VPN de site à site Azure

Vous pouvez rencontrer le problème hello qu’une connexion VPN de Azure de Microsoft Point-to-Site nouveau ou existante n’est pas stable ou se déconnecte régulièrement. Cet article fournit des étapes toohelp identifier et résoudre les problème de hello provoqué hello de résoudre les problèmes. 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-steps"></a>Étapes de dépannage

### <a name="prerequisite-step"></a>Étape des conditions préalables

Vérification de type hello de passerelle de réseau virtuel Azure :

1. Accédez trop[portail Azure](https://portal.azure.com).
2. Vérifiez hello **vue d’ensemble** page de passerelle de réseau virtuel hello pour les informations de type hello.
    
    ![vue d’ensemble de Hello de passerelle de hello](media\vpn-gateway-troubleshoot-site-to-site-disconnected-intermittently\gatewayoverview.png)

### <a name="step-1-check-whether-hello-on-premises-vpn-device-is-validated"></a>Étape 1 Vérifiez si hello local périphérique VPN est validé.

1. Vérifiez si vous utilisez un [appareil VPN et une version de système d’exploitation validés](vpn-gateway-about-vpn-devices.md#devicetable). Si le périphérique VPN de hello n’est pas validé, vous avez peut-être toocontact hello appareil fabricant toosee s’il existe des problèmes de compatibilité.
2. Assurez-vous que le périphérique VPN hello est correctement configuré. Pour plus d’informations, consultez [Modification des exemples de configuration de périphérique](vpn-gateway-about-vpn-devices.md#editing).

### <a name="step-2-check-hello-security-association-settingsfor-policy-based-azure-virtual-network-gateways"></a>Étape 2 Vérifiez les paramètres hello Association de sécurité (pour les passerelles de réseau virtuel Azure basée sur des stratégies)

1. Assurez-vous que ce réseau virtuel hello, sous-réseaux et des plages de hello **passerelle de réseau Local** définition dans Microsoft Azure sont les mêmes que configuration hello sur le périphérique VPN local hello.
2. Vérifiez qui correspondent aux paramètres de sécurité Association hello.

### <a name="step-3-check-for-user-defined-routes-or-network-security-groups-on-gateway-subnet"></a>Étape 3 : Vérifier les itinéraires définis par l’utilisateur ou les groupes de sécurité réseau sur le sous-réseau de passerelle

Un itinéraire défini par l’utilisateur sur le sous-réseau de passerelle hello peut restreindre certains types de trafic et autorisant le reste du trafic. Cela donne l’impression que la connexion VPN de hello est peu fiable pour certains types de trafic et de bonnes pour d’autres. 

### <a name="step-4-check-hello-one-vpn-tunnel-per-subnet-pair-setting-for-policy-based-virtual-network-gateways"></a>Vérification de l’étape 4 hello « un Tunnel VPN par paire de sous-réseau » paramètre (pour les passerelles de réseau virtuel basée sur une stratégie)

Vérifiez que hello local périphérique VPN a la valeur toohave **un tunnel VPN par paire de sous-réseau** pour les passerelles basée sur des stratégies de réseau virtuel.

### <a name="step-5-check-for-security-association-limitation-for-policy-based-virtual-network-gateways"></a>Étape 5 : Vérifier la limite d’association de sécurité (pour les passerelles de réseau virtuel Azure basées sur une stratégie)

passerelle de réseau virtuel basée sur une stratégie Hello est limitée à 200 paires d’Association de sécurité de sous-réseau. Si hello le nombre de sous-réseaux du réseau virtuel Azure multiplié fois par hello nombre de sous-réseaux locaux est supérieur à 200, vous voyez les sous-réseaux sporadiques déconnexion.

### <a name="step-6-check-on-premises-vpn-device-external-interface-address"></a>Étape 6 : Vérifier l’adresse d’interface externe de l’appareil VPN local

- Si hello exposés à adresse IP du périphérique VPN de hello Internet est inclus dans hello **passerelle de réseau Local** définition dans Azure, vous pouvez rencontrer des déconnexions sporadiques.
- Hello interface externe de l’appareil doit être directement sur Internet de hello. Il ne doit y avoir aucune traduction d’adresses réseau (NAT) ou un pare-feu entre hello Internet et les appareils hello.
-  Si vous configurez une adresse IP virtuelle à toohave de Clustering de pare-feu, vous devez arrêter le cluster de hello et exposer un équipement VPN hello directement l’interface publique tooa hello passerelle pouvant communiquer avec.

### <a name="step-7-check-whether-hello-on-premises-vpn-device-has-perfect-forward-secrecy-enabled"></a>Étape 7 vérification si hello local périphérique VPN a Perfect Forward Secrecy activé

Hello **Perfect Forward Secrecy** fonctionnalité peut entraîner des problèmes de déconnexion de hello. Si le périphérique VPN de hello a **parfaite** activé, désactiver la fonctionnalité de hello. Puis [mise à jour de la stratégie de passerelle de réseau virtuel hello](vpn-gateway-ipsecikepolicy-rm-powershell.md#managepolicy).

## <a name="next-steps"></a>Étapes suivantes

- [Configurer un réseau virtuel de Site à Site connexion tooa](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
- [Configure IPsec/IKE policy for S2S VPN or VNet-to-VNet connections](vpn-gateway-ipsecikepolicy-rm-powershell.md) (Configurer la stratégie IPsec/IKE pour les connexions VPN de site à site ou de réseau virtuel à réseau virtuel)

