---
title: "aaaTroubleshoot une connexion VPN site à site Azure qui ne peut pas se connecter | Documents Microsoft"
description: "Découvrez comment tootroubleshoot une connexion VPN site à site qui soudain cesse de fonctionner et ne peut pas être reconnecté."
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
ms.openlocfilehash: 632c75bfcfb93a532eeead2855d43e6614569a99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-an-azure-site-to-site-vpn-connection-cannot-connect-and-stops-working"></a>Résolution de problèmes : une connexion VPN de site à site Azure cesse de fonctionner

Après avoir configuré une connexion VPN de site à site entre un réseau local et un réseau virtuel Azure, hello connexion VPN soudain cesse de fonctionner et ne peut pas être reconnecté. Cet article fournit la résolution des problèmes étapes toohelp vous résolvez ce problème. 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-steps"></a>Étapes de dépannage

problème de hello tooresolve, essayez tout d’abord de trop[passerelle VPN Azure de hello réinitialisation](vpn-gateway-resetgw-classic.md) et réinitialiser tunnel hello à partir de l’appareil VPN local hello. Si hello problème persiste, suivez ces cause de hello tooidentify étapes du problème de hello.

### <a name="prerequisite-step"></a>Étape des conditions préalables

Vérifiez le type hello de passerelle VPN Azure de hello.

1. Accédez toohello [portail Azure](https://portal.azure.com).

2. Vérifiez hello **vue d’ensemble** page de passerelle VPN de hello pour les informations de type hello.
    
    ![Vue d’ensemble de la passerelle de hello](media\vpn-gateway-troubleshoot-site-to-site-cannot-connect\gatewayoverview.png)

### <a name="step-1-check-whether-hello-on-premises-vpn-device-is-validated"></a>Étape 1. Vérifiez si l’appareil VPN local hello est validé

1. Vérifiez si vous utilisez un [appareil VPN et une version de système d’exploitation validés](vpn-gateway-about-vpn-devices.md#devicetable). Si l’appareil de hello n’est pas un périphérique VPN validé, peut avoir toocontact hello appareil fabricant toosee s’il existe un problème de compatibilité.

2. Assurez-vous que le périphérique VPN hello est correctement configuré. Pour plus d’informations, consultez la page [Modification des exemples de configuration de périphérique](/vpn-gateway-about-vpn-devices.md#editing).

### <a name="step-2-verify-hello-shared-key"></a>Étape 2. Vérifiez la clé partagée de hello

Comparer la clé partagée de hello pour hello local VPN appareil toohello VPN de réseau virtuel Azure toomake assurer que les clés hello correspondent. 

clé partagée de tooview hello pour hello connexion VPN d’Azure, utilisez une des méthodes suivantes de hello :

**Portail Azure**

1. Accédez toohello passerelle site-à-site réseau VPN que vous avez créé.

2. Bonjour **paramètres** , cliquez sur **clé partagée**.
    
    ![Clé partagée](media/vpn-gateway-troubleshoot-site-to-site-cannot-connect/sharedkey.png)

**Azure PowerShell**

Pour le modèle de déploiement du Gestionnaire de ressources Azure hello :

    Get-AzureRmVirtualNetworkGatewayConnectionSharedKey -Name <Connection name> -ResourceGroupName <Resource group name>

Pour le modèle de déploiement classique de hello :

    Get-AzureVNetGatewayKey -VNetName -LocalNetworkSiteName

### <a name="step-3-verify-hello-vpn-peer-ips"></a>Étape 3. Vérifier les adresses IP d’homologue VPN hello

-   Hello définition IP Bonjour **passerelle de réseau Local** objet dans Azure doit correspondre à l’IP du périphérique local hello.
-   Hello définition IP de passerelle Azure qui est définie sur hello local appareil doit correspondre à l’IP de la passerelle Azure hello.

### <a name="step-4-check-udr-and-nsgs-on-hello-gateway-subnet"></a>Étape 4. Vérifiez UDR et les groupes de sécurité réseau sur le sous-réseau de passerelle hello

Recherchez et supprimez routage défini par l’utilisateur (UDR) ou des groupes de sécurité réseau (NSG) sur le sous-réseau de passerelle hello ensuite tester le résultat de hello. Si le problème de hello est résolu, valider les paramètres de hello UDR ou groupe de sécurité réseau appliqués.

### <a name="step-5-check-hello-on-premises-vpn-device-external-interface-address"></a>Étape 5. Vérification hello adresse interface externe du périphérique VPN sur site

- Si hello adresse IP de côté Internet du périphérique VPN de hello est inclus dans hello **réseau Local** définition dans Azure, vous pouvez rencontrer des déconnexions sporadiques.
- Hello interface externe de l’appareil doit être directement sur Internet de hello. Il ne doit y avoir aucune traduction d’adresses réseau ou un pare-feu entre hello Internet et les appareils hello.
- tooconfigure pare-feu clustering toohave une adresse IP virtuelle, vous devez arrêter le cluster de hello et exposer un équipement VPN hello directement l’interface publique de tooa cette passerelle hello pouvant communiquer avec.

### <a name="step-6-verify-that-hello-subnets-match-exactly-azure-policy-based-gateways"></a>Étape 6. Vérifiez que les sous-réseaux hello correspondent exactement (passerelles Azure basée sur des stratégies)

-   Vérifiez que les sous-réseaux hello correspondent exactement entre hello réseau virtuel Azure et locaux pour hello réseau virtuel Azure.
-   Vérifiez que les sous-réseaux hello correspondent exactement entre hello **passerelle de réseau Local** et définitions de réseau local de hello en local.

### <a name="step-7-verify-hello-azure-gateway-health-probe"></a>Étape 7. Vérifiez que la sonde d’intégrité de passerelle Azure hello

1. Accédez toohello [sonde d’intégrité](https://&lt;YourVirtualNetworkGatewayIP&gt;:8081/healthprobe).

2. Cliquez sur Avertissement de certificat hello.
3. Si vous recevez une réponse, passerelle VPN de hello est considéré comme sain. Si vous ne recevez pas de réponse, passerelle de hello ne peut pas être sain ou un groupe de sécurité réseau sur le sous-réseau de passerelle hello problème hello. Hello suivant le texte est un exemple de réponse :

    &lt;?xml version="1.0"?&gt;  <string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">Primary Instance: GatewayTenantWorker_IN_1 GatewayTenantVersion: 14.7.24.6&lt;/string&gt;

### <a name="step-8-check-whether-hello-on-premises-vpn-device-has-hello-perfect-forward-secrecy-feature-enabled"></a>Étape 8 : Vérifiez si hello local périphérique VPN avec la fonctionnalité de transmission parfaite de hello activée

fonctionnalité de transmission parfaite Hello peut entraîner des problèmes de déconnexion. Si le périphérique VPN de hello a parfaite activé, désactiver la fonctionnalité de hello. Puis, mettez à jour de stratégie IPsec de hello VPN gateway.

## <a name="next-steps"></a>Étapes suivantes

-   [Configurer un réseau virtuel tooa de connexion de site à site](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
-   [Configurer la stratégie IPsec/IKE pour des connexions VPN S2S ou de réseau virtuel à réseau virtuel](vpn-gateway-ipsecikepolicy-rm-powershell.md)
