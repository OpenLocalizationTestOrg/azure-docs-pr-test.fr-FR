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
# <a name="about-cryptographic-requirements-and-azure-vpn-gateways"></a><span data-ttu-id="e0901-103">À propos des exigences de chiffrement et des passerelles VPN Azure</span><span class="sxs-lookup"><span data-stu-id="e0901-103">About cryptographic requirements and Azure VPN gateways</span></span>

<span data-ttu-id="e0901-104">Cet article explique comment vous pouvez configurer les toosatisfy des passerelles VPN Azure vos exigences de chiffrement pour les tunnels VPN de S2S entre différents locaux et les connexions de réseau virtuel à réseau virtuel dans Azure.</span><span class="sxs-lookup"><span data-stu-id="e0901-104">This article discusses how you can configure Azure VPN gateways toosatisfy your cryptographic requirements for both cross-premises S2S VPN tunnels and VNet-to-VNet connections within Azure.</span></span> 

## <a name="about-ipsec-and-ike-policy-parameters-for-azure-vpn-gateways"></a><span data-ttu-id="e0901-105">À propos des paramètres de stratégie IPsec et IKE pour les passerelles VPN Azure</span><span class="sxs-lookup"><span data-stu-id="e0901-105">About IPsec and IKE policy parameters for Azure VPN gateways</span></span>
<span data-ttu-id="e0901-106">La norme de protocole IPsec et IKE standard prend en charge un vaste éventail d’algorithmes de chiffrement dans différentes combinaisons.</span><span class="sxs-lookup"><span data-stu-id="e0901-106">IPsec and IKE protocol standard supports a wide range of cryptographic algorithms in various combinations.</span></span> <span data-ttu-id="e0901-107">Si les clients ne demandent pas une combinaison spécifique de paramètres et d’algorithmes de chiffrement, les passerelles VPN Azure utilisent un ensemble de propositions par défaut.</span><span class="sxs-lookup"><span data-stu-id="e0901-107">If customers do not request a specific combination of cryptographic algorithms and parameters, Azure VPN gateways use a set of default proposals.</span></span> <span data-ttu-id="e0901-108">jeux de stratégie par défaut Hello ont été choisies interopérabilité toomaximize avec une large gamme de périphériques VPN de tiers dans les configurations par défaut.</span><span class="sxs-lookup"><span data-stu-id="e0901-108">hello default policy sets were chosen toomaximize interoperability with a wide range of third-party VPN devices in default configurations.</span></span> <span data-ttu-id="e0901-109">Par conséquent, les stratégies de hello et nombre hello des propositions ne peuvent pas couvrir toutes les combinaisons possibles des algorithmes de chiffrement disponibles et atouts.</span><span class="sxs-lookup"><span data-stu-id="e0901-109">As a result, hello policies and hello number of proposals cannot cover all possible combinations of available cryptographic algorithms and key strengths.</span></span>

<span data-ttu-id="e0901-110">Hello stratégie par défaut définie pour la passerelle VPN Azure est répertorié dans le document de hello : [propos des périphériques VPN et les paramètres IPsec/IKE pour les connexions de passerelle VPN Site à Site](vpn-gateway-about-vpn-devices.md).</span><span class="sxs-lookup"><span data-stu-id="e0901-110">hello default policy set for Azure VPN gateway is listed in hello document: [About VPN devices and IPsec/IKE parameters for Site-to-Site VPN Gateway connections](vpn-gateway-about-vpn-devices.md).</span></span>

## <a name="cryptographic-requirements"></a><span data-ttu-id="e0901-111">Exigences de chiffrement</span><span class="sxs-lookup"><span data-stu-id="e0901-111">Cryptographic requirements</span></span>
<span data-ttu-id="e0901-112">Pour les communications qui requièrent des algorithmes de chiffrement spécifiques ou des paramètres, généralement en raison d’exigences de sécurité ou toocompliance, clients peuvent désormais configurer leur toouse de passerelles VPN Azure une stratégie IPsec/IKE personnalisée présentant des services de chiffrement algorithmes et des avantages clés, plutôt que jeux de stratégie par défaut Azure hello.</span><span class="sxs-lookup"><span data-stu-id="e0901-112">For communications that require specific cryptographic algorithms or parameters, typically due toocompliance or security requirements, customers can now configure their Azure VPN gateways toouse a custom IPsec/IKE policy with specific cryptographic algorithms and key strengths, rather than hello Azure default policy sets.</span></span>

<span data-ttu-id="e0901-113">Par exemple, stratégies de mode principal hello IKEv2 pour les passerelles VPN Azure utilisent uniquement Diffie-Hellman groupe 2 (1 024 bits), tandis que les clients peut-être toospecify toobe de groupes plus fort utilisé dans IKE, comme ECP (elliptique, groupe 24 (groupe MODP de 2048 bits) ou groupe 14 (2048 bits) courbe de groupes) 256 ou 384 bits (groupe 19 et groupe de 20, respectivement).</span><span class="sxs-lookup"><span data-stu-id="e0901-113">For example, hello IKEv2 main mode policies for Azure VPN gateways utilize only Diffie-Hellman Group 2 (1024 bits), whereas customers may need toospecify stronger groups toobe used in IKE, such as Group 14 (2048-bit), Group 24 (2048-bit MODP Group), or ECP (elliptic curve groups) 256 or 384 bit (Group 19 and Group 20, respectively).</span></span> <span data-ttu-id="e0901-114">Des configurations similaires s’appliquent également les stratégies de mode rapide tooIPsec.</span><span class="sxs-lookup"><span data-stu-id="e0901-114">Similar requirements apply tooIPsec quick mode policies as well.</span></span>

## <a name="custom-ipsecike-policy-with-azure-vpn-gateways"></a><span data-ttu-id="e0901-115">Stratégie IPsec/IKE personnalisée avec des passerelles VPN Azure</span><span class="sxs-lookup"><span data-stu-id="e0901-115">Custom IPsec/IKE policy with Azure VPN gateways</span></span>
<span data-ttu-id="e0901-116">Les passerelles VPN Azure prennent désormais en charge la stratégie IPsec/IKE personnalisée par connexion.</span><span class="sxs-lookup"><span data-stu-id="e0901-116">Azure VPN gateways now support per-connection, custom IPsec/IKE policy.</span></span> <span data-ttu-id="e0901-117">Pour une connexion de réseau virtuel à réseau virtuel ou d’un Site à Site, vous pouvez choisir une combinaison spécifique d’algorithmes de chiffrement pour IPsec et IKE avec la puissance de clé hello souhaitée, comme indiqué dans hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="e0901-117">For a Site-to-Site or VNet-to-VNet connection, you can choose a specific combination of cryptographic algorithms for IPsec and IKE with hello desired key strength, as shown in hello following example:</span></span>

![stratégie IPSec/IKE](./media/vpn-gateway-about-compliance-crypto/ipsecikepolicy.png)

<span data-ttu-id="e0901-119">Vous pouvez créer une stratégie IPsec/IKE et appliquer la connexion existante ou nouvelle de tooa.</span><span class="sxs-lookup"><span data-stu-id="e0901-119">You can create an IPsec/IKE policy and apply tooa new or existing connection.</span></span> 

### <a name="workflow"></a><span data-ttu-id="e0901-120">Workflow</span><span class="sxs-lookup"><span data-stu-id="e0901-120">Workflow</span></span>

1. <span data-ttu-id="e0901-121">Créer des réseaux virtuels hello, passerelles VPN ou des passerelles de réseau local pour votre topologie de la connectivité comme décrit dans les autres toodocuments de procédure</span><span class="sxs-lookup"><span data-stu-id="e0901-121">Create hello virtual networks, VPN gateways, or local network gateways for your connectivity topology as described in other how-toodocuments</span></span>
2. <span data-ttu-id="e0901-122">Créez une stratégie IPsec/IKE.</span><span class="sxs-lookup"><span data-stu-id="e0901-122">Create an IPsec/IKE policy</span></span>
3. <span data-ttu-id="e0901-123">Vous pouvez appliquer la stratégie de hello lorsque vous créez une connexion au réseau ou de S2S</span><span class="sxs-lookup"><span data-stu-id="e0901-123">You can apply hello policy when you create a S2S or VNet-to-VNet connection</span></span>
4. <span data-ttu-id="e0901-124">Si la connexion de hello existe déjà, vous pouvez appliquer ou mettre à jour la connexion à la stratégie hello tooan existante</span><span class="sxs-lookup"><span data-stu-id="e0901-124">If hello connection is already created, you can apply or update hello policy tooan existing connection</span></span>


## <a name="ipsecike-policy-faq"></a><span data-ttu-id="e0901-125">Questions fréquentes (FAQ) relatives à la stratégie IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="e0901-125">IPsec/IKE policy FAQ</span></span>

[!INCLUDE [vpn-gateway-ipsecikepolicy-faq-include](../../includes/vpn-gateway-ipsecikepolicy-faq-include.md)]


## <a name="next-steps"></a><span data-ttu-id="e0901-126">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e0901-126">Next steps</span></span>
<span data-ttu-id="e0901-127">Consultez [Configurer la stratégie IPsec/IKE](vpn-gateway-ipsecikepolicy-rm-powershell.md) pour obtenir des instructions détaillées sur la configuration d’une stratégie IPsec/IKE personnalisée sur une connexion.</span><span class="sxs-lookup"><span data-stu-id="e0901-127">See [Configure IPsec/IKE policy](vpn-gateway-ipsecikepolicy-rm-powershell.md) for step-by-step instructions on configuring custom IPsec/IKE policy on a connection.</span></span>

<span data-ttu-id="e0901-128">Voir aussi [connecter plusieurs périphériques VPN basée sur des stratégies](vpn-gateway-connect-multiple-policybased-rm-ps.md) toolearn plus hello UsePolicyBasedTrafficSelectors option.</span><span class="sxs-lookup"><span data-stu-id="e0901-128">See also [Connect multiple policy-based VPN devices](vpn-gateway-connect-multiple-policybased-rm-ps.md) toolearn more about hello UsePolicyBasedTrafficSelectors option.</span></span>
