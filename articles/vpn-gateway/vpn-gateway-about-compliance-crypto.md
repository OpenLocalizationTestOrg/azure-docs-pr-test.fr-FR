---
title: aaaAbout exigences de chiffrement et les passerelles VPN Azure | Documents Microsoft
description: Cet article aborde les exigences de chiffrement et les passerelles VPN Azure
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 238cd9b3-f1ce-4341-b18e-7390935604fa
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/22/2017
ms.author: yushwang
ms.openlocfilehash: af5f14d66beeea5316218f9788c4ad7876826162
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="about-cryptographic-requirements-and-azure-vpn-gateways"></a>À propos des exigences de chiffrement et des passerelles VPN Azure

Cet article explique comment vous pouvez configurer les toosatisfy des passerelles VPN Azure vos exigences de chiffrement pour les tunnels VPN de S2S entre différents locaux et les connexions de réseau virtuel à réseau virtuel dans Azure. 

## <a name="about-ipsec-and-ike-policy-parameters-for-azure-vpn-gateways"></a>À propos des paramètres de stratégie IPsec et IKE pour les passerelles VPN Azure
La norme de protocole IPsec et IKE standard prend en charge un vaste éventail d’algorithmes de chiffrement dans différentes combinaisons. Si les clients ne demandent pas une combinaison spécifique de paramètres et d’algorithmes de chiffrement, les passerelles VPN Azure utilisent un ensemble de propositions par défaut. jeux de stratégie par défaut Hello ont été choisies interopérabilité toomaximize avec une large gamme de périphériques VPN de tiers dans les configurations par défaut. Par conséquent, les stratégies de hello et nombre hello des propositions ne peuvent pas couvrir toutes les combinaisons possibles des algorithmes de chiffrement disponibles et atouts.

Hello stratégie par défaut définie pour la passerelle VPN Azure est répertorié dans le document de hello : [propos des périphériques VPN et les paramètres IPsec/IKE pour les connexions de passerelle VPN Site à Site](vpn-gateway-about-vpn-devices.md).

## <a name="cryptographic-requirements"></a>Exigences de chiffrement
Pour les communications qui requièrent des algorithmes de chiffrement spécifiques ou des paramètres, généralement en raison d’exigences de sécurité ou toocompliance, clients peuvent désormais configurer leur toouse de passerelles VPN Azure une stratégie IPsec/IKE personnalisée présentant des services de chiffrement algorithmes et des avantages clés, plutôt que jeux de stratégie par défaut Azure hello.

Par exemple, stratégies de mode principal hello IKEv2 pour les passerelles VPN Azure utilisent uniquement Diffie-Hellman groupe 2 (1 024 bits), tandis que les clients peut-être toospecify toobe de groupes plus fort utilisé dans IKE, comme ECP (elliptique, groupe 24 (groupe MODP de 2048 bits) ou groupe 14 (2048 bits) courbe de groupes) 256 ou 384 bits (groupe 19 et groupe de 20, respectivement). Des configurations similaires s’appliquent également les stratégies de mode rapide tooIPsec.

## <a name="custom-ipsecike-policy-with-azure-vpn-gateways"></a>Stratégie IPsec/IKE personnalisée avec des passerelles VPN Azure
Les passerelles VPN Azure prennent désormais en charge la stratégie IPsec/IKE personnalisée par connexion. Pour une connexion de réseau virtuel à réseau virtuel ou d’un Site à Site, vous pouvez choisir une combinaison spécifique d’algorithmes de chiffrement pour IPsec et IKE avec la puissance de clé hello souhaitée, comme indiqué dans hello l’exemple suivant :

![stratégie IPSec/IKE](./media/vpn-gateway-about-compliance-crypto/ipsecikepolicy.png)

Vous pouvez créer une stratégie IPsec/IKE et appliquer la connexion existante ou nouvelle de tooa. 

### <a name="workflow"></a>Workflow

1. Créer des réseaux virtuels hello, passerelles VPN ou des passerelles de réseau local pour votre topologie de la connectivité comme décrit dans les autres toodocuments de procédure
2. Créez une stratégie IPsec/IKE.
3. Vous pouvez appliquer la stratégie de hello lorsque vous créez une connexion au réseau ou de S2S
4. Si la connexion de hello existe déjà, vous pouvez appliquer ou mettre à jour la connexion à la stratégie hello tooan existante


## <a name="ipsecike-policy-faq"></a>Questions fréquentes (FAQ) relatives à la stratégie IPsec/IKE

[!INCLUDE [vpn-gateway-ipsecikepolicy-faq-include](../../includes/vpn-gateway-ipsecikepolicy-faq-include.md)]


## <a name="next-steps"></a>Étapes suivantes
Consultez [Configurer la stratégie IPsec/IKE](vpn-gateway-ipsecikepolicy-rm-powershell.md) pour obtenir des instructions détaillées sur la configuration d’une stratégie IPsec/IKE personnalisée sur une connexion.

Voir aussi [connecter plusieurs périphériques VPN basée sur des stratégies](vpn-gateway-connect-multiple-policybased-rm-ps.md) toolearn plus hello UsePolicyBasedTrafficSelectors option.
