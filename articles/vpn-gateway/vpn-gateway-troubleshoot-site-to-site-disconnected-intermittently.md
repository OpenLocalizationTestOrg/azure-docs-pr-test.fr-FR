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
# <a name="troubleshooting-azure-site-to-site-vpn-disconnects-intermittently"></a><span data-ttu-id="6f510-103">Résolution des problèmes : déconnexion intermittente du VPN de site à site Azure</span><span class="sxs-lookup"><span data-stu-id="6f510-103">Troubleshooting: Azure Site-to-Site VPN disconnects intermittently</span></span>

<span data-ttu-id="6f510-104">Vous pouvez rencontrer le problème hello qu’une connexion VPN de Azure de Microsoft Point-to-Site nouveau ou existante n’est pas stable ou se déconnecte régulièrement.</span><span class="sxs-lookup"><span data-stu-id="6f510-104">You might experience hello problem that a new or existing Microsoft Azure Point-to-Site VPN connection is not stable or disconnects regularly.</span></span> <span data-ttu-id="6f510-105">Cet article fournit des étapes toohelp identifier et résoudre les problème de hello provoqué hello de résoudre les problèmes.</span><span class="sxs-lookup"><span data-stu-id="6f510-105">This article provides troubleshoot steps toohelp you identify and resolve hello cause of hello problem.</span></span> 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-steps"></a><span data-ttu-id="6f510-106">Étapes de dépannage</span><span class="sxs-lookup"><span data-stu-id="6f510-106">Troubleshooting steps</span></span>

### <a name="prerequisite-step"></a><span data-ttu-id="6f510-107">Étape des conditions préalables</span><span class="sxs-lookup"><span data-stu-id="6f510-107">Prerequisite step</span></span>

<span data-ttu-id="6f510-108">Vérification de type hello de passerelle de réseau virtuel Azure :</span><span class="sxs-lookup"><span data-stu-id="6f510-108">Check hello type of Azure  virtual network gateway:</span></span>

1. <span data-ttu-id="6f510-109">Accédez trop[portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6f510-109">Go too[Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="6f510-110">Vérifiez hello **vue d’ensemble** page de passerelle de réseau virtuel hello pour les informations de type hello.</span><span class="sxs-lookup"><span data-stu-id="6f510-110">Check hello **Overview** page of hello virtual network gateway for hello type information.</span></span>
    
    ![vue d’ensemble de Hello de passerelle de hello](media\vpn-gateway-troubleshoot-site-to-site-disconnected-intermittently\gatewayoverview.png)

### <a name="step-1-check-whether-hello-on-premises-vpn-device-is-validated"></a><span data-ttu-id="6f510-112">Étape 1 Vérifiez si hello local périphérique VPN est validé.</span><span class="sxs-lookup"><span data-stu-id="6f510-112">Step 1 Check whether hello on-premises VPN device is validated</span></span>

1. <span data-ttu-id="6f510-113">Vérifiez si vous utilisez un [appareil VPN et une version de système d’exploitation validés](vpn-gateway-about-vpn-devices.md#devicetable).</span><span class="sxs-lookup"><span data-stu-id="6f510-113">Check whether you are using a [validated VPN device and operating system version](vpn-gateway-about-vpn-devices.md#devicetable).</span></span> <span data-ttu-id="6f510-114">Si le périphérique VPN de hello n’est pas validé, vous avez peut-être toocontact hello appareil fabricant toosee s’il existe des problèmes de compatibilité.</span><span class="sxs-lookup"><span data-stu-id="6f510-114">If hello VPN device is not validated, you may have toocontact hello device manufacturer toosee if there is any compatibility issue.</span></span>
2. <span data-ttu-id="6f510-115">Assurez-vous que le périphérique VPN hello est correctement configuré.</span><span class="sxs-lookup"><span data-stu-id="6f510-115">Make sure that hello VPN device is correctly configured.</span></span> <span data-ttu-id="6f510-116">Pour plus d’informations, consultez [Modification des exemples de configuration de périphérique](vpn-gateway-about-vpn-devices.md#editing).</span><span class="sxs-lookup"><span data-stu-id="6f510-116">For more information, see [Editing device configuration samples](vpn-gateway-about-vpn-devices.md#editing).</span></span>

### <a name="step-2-check-hello-security-association-settingsfor-policy-based-azure-virtual-network-gateways"></a><span data-ttu-id="6f510-117">Étape 2 Vérifiez les paramètres hello Association de sécurité (pour les passerelles de réseau virtuel Azure basée sur des stratégies)</span><span class="sxs-lookup"><span data-stu-id="6f510-117">Step 2 Check hello Security Association settings(for policy-based Azure virtual network gateways)</span></span>

1. <span data-ttu-id="6f510-118">Assurez-vous que ce réseau virtuel hello, sous-réseaux et des plages de hello **passerelle de réseau Local** définition dans Microsoft Azure sont les mêmes que configuration hello sur le périphérique VPN local hello.</span><span class="sxs-lookup"><span data-stu-id="6f510-118">Make sure that hello virtual network, subnets and, ranges in hello **Local network gateway** definition in Microsoft Azure are same as hello configuration on hello on-premises VPN device.</span></span>
2. <span data-ttu-id="6f510-119">Vérifiez qui correspondent aux paramètres de sécurité Association hello.</span><span class="sxs-lookup"><span data-stu-id="6f510-119">Verify that hello Security Association settings match.</span></span>

### <a name="step-3-check-for-user-defined-routes-or-network-security-groups-on-gateway-subnet"></a><span data-ttu-id="6f510-120">Étape 3 : Vérifier les itinéraires définis par l’utilisateur ou les groupes de sécurité réseau sur le sous-réseau de passerelle</span><span class="sxs-lookup"><span data-stu-id="6f510-120">Step 3 Check for User-Defined Routes or Network Security Groups on Gateway Subnet</span></span>

<span data-ttu-id="6f510-121">Un itinéraire défini par l’utilisateur sur le sous-réseau de passerelle hello peut restreindre certains types de trafic et autorisant le reste du trafic.</span><span class="sxs-lookup"><span data-stu-id="6f510-121">A user-defined route on hello gateway subnet may be restricting some traffic and allowing other traffic.</span></span> <span data-ttu-id="6f510-122">Cela donne l’impression que la connexion VPN de hello est peu fiable pour certains types de trafic et de bonnes pour d’autres.</span><span class="sxs-lookup"><span data-stu-id="6f510-122">This makes it appear that hello VPN connection is unreliable for some traffic and good for others.</span></span> 

### <a name="step-4-check-hello-one-vpn-tunnel-per-subnet-pair-setting-for-policy-based-virtual-network-gateways"></a><span data-ttu-id="6f510-123">Vérification de l’étape 4 hello « un Tunnel VPN par paire de sous-réseau » paramètre (pour les passerelles de réseau virtuel basée sur une stratégie)</span><span class="sxs-lookup"><span data-stu-id="6f510-123">Step 4 Check hello "one VPN Tunnel per Subnet Pair" setting (for policy-based virtual network gateways)</span></span>

<span data-ttu-id="6f510-124">Vérifiez que hello local périphérique VPN a la valeur toohave **un tunnel VPN par paire de sous-réseau** pour les passerelles basée sur des stratégies de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="6f510-124">Make sure that hello on-premises VPN device is set toohave **one VPN tunnel per subnet pair** for policy-based virtual network gateways.</span></span>

### <a name="step-5-check-for-security-association-limitation-for-policy-based-virtual-network-gateways"></a><span data-ttu-id="6f510-125">Étape 5 : Vérifier la limite d’association de sécurité (pour les passerelles de réseau virtuel Azure basées sur une stratégie)</span><span class="sxs-lookup"><span data-stu-id="6f510-125">Step 5 Check for Security Association Limitation (for policy-based virtual network gateways)</span></span>

<span data-ttu-id="6f510-126">passerelle de réseau virtuel basée sur une stratégie Hello est limitée à 200 paires d’Association de sécurité de sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="6f510-126">hello Policy-based virtual network gateway has limit of 200 subnet Security Association pairs.</span></span> <span data-ttu-id="6f510-127">Si hello le nombre de sous-réseaux du réseau virtuel Azure multiplié fois par hello nombre de sous-réseaux locaux est supérieur à 200, vous voyez les sous-réseaux sporadiques déconnexion.</span><span class="sxs-lookup"><span data-stu-id="6f510-127">If hello number of Azure virtual network subnets multiplied times by hello number of local subnets is greater than 200, you see sporadic subnets disconnecting.</span></span>

### <a name="step-6-check-on-premises-vpn-device-external-interface-address"></a><span data-ttu-id="6f510-128">Étape 6 : Vérifier l’adresse d’interface externe de l’appareil VPN local</span><span class="sxs-lookup"><span data-stu-id="6f510-128">Step 6 Check on-premises VPN device external interface address</span></span>

- <span data-ttu-id="6f510-129">Si hello exposés à adresse IP du périphérique VPN de hello Internet est inclus dans hello **passerelle de réseau Local** définition dans Azure, vous pouvez rencontrer des déconnexions sporadiques.</span><span class="sxs-lookup"><span data-stu-id="6f510-129">If hello Internet facing IP address of hello VPN device is included in hello **Local network gateway** definition in Azure, you may experience sporadic disconnections.</span></span>
- <span data-ttu-id="6f510-130">Hello interface externe de l’appareil doit être directement sur Internet de hello.</span><span class="sxs-lookup"><span data-stu-id="6f510-130">hello device's external interface must be directly on hello Internet.</span></span> <span data-ttu-id="6f510-131">Il ne doit y avoir aucune traduction d’adresses réseau (NAT) ou un pare-feu entre hello Internet et les appareils hello.</span><span class="sxs-lookup"><span data-stu-id="6f510-131">There should be no Network Address Translation (NAT) or firewall between hello Internet and hello device.</span></span>
-  <span data-ttu-id="6f510-132">Si vous configurez une adresse IP virtuelle à toohave de Clustering de pare-feu, vous devez arrêter le cluster de hello et exposer un équipement VPN hello directement l’interface publique tooa hello passerelle pouvant communiquer avec.</span><span class="sxs-lookup"><span data-stu-id="6f510-132">If you configure Firewall Clustering toohave a virtual IP, you must break hello cluster and expose hello VPN appliance directly tooa public interface that hello gateway can interface with.</span></span>

### <a name="step-7-check-whether-hello-on-premises-vpn-device-has-perfect-forward-secrecy-enabled"></a><span data-ttu-id="6f510-133">Étape 7 vérification si hello local périphérique VPN a Perfect Forward Secrecy activé</span><span class="sxs-lookup"><span data-stu-id="6f510-133">Step 7 Check whether hello on-premises VPN device has Perfect Forward Secrecy enabled</span></span>

<span data-ttu-id="6f510-134">Hello **Perfect Forward Secrecy** fonctionnalité peut entraîner des problèmes de déconnexion de hello.</span><span class="sxs-lookup"><span data-stu-id="6f510-134">hello **Perfect Forward Secrecy** feature can cause hello disconnection problems.</span></span> <span data-ttu-id="6f510-135">Si le périphérique VPN de hello a **parfaite** activé, désactiver la fonctionnalité de hello.</span><span class="sxs-lookup"><span data-stu-id="6f510-135">If hello VPN device has **Perfect forward Secrecy** enabled, disable hello feature.</span></span> <span data-ttu-id="6f510-136">Puis [mise à jour de la stratégie de passerelle de réseau virtuel hello](vpn-gateway-ipsecikepolicy-rm-powershell.md#managepolicy).</span><span class="sxs-lookup"><span data-stu-id="6f510-136">Then [update hello virtual network gateway IPsec policy](vpn-gateway-ipsecikepolicy-rm-powershell.md#managepolicy).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6f510-137">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6f510-137">Next steps</span></span>

- [<span data-ttu-id="6f510-138">Configurer un réseau virtuel de Site à Site connexion tooa</span><span class="sxs-lookup"><span data-stu-id="6f510-138">Configure a Site-to-Site connection tooa virtual network</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
- <span data-ttu-id="6f510-139">[Configure IPsec/IKE policy for S2S VPN or VNet-to-VNet connections](vpn-gateway-ipsecikepolicy-rm-powershell.md) (Configurer la stratégie IPsec/IKE pour les connexions VPN de site à site ou de réseau virtuel à réseau virtuel)</span><span class="sxs-lookup"><span data-stu-id="6f510-139">[Configure IPsec/IKE policy for Site-to-Site VPN connections](vpn-gateway-ipsecikepolicy-rm-powershell.md)</span></span>

