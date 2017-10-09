---
title: "configuration aaaSample - périphériques Cisco ASA connexion des passerelles VPN tooAzure | Documents Microsoft"
description: "Cet article fournit un exemple de configuration pour les périphériques Cisco ASA connexion des passerelles VPN tooAzure."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: 
ms.assetid: a8bfc955-de49-4172-95ac-5257e262d7ea
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/20/2017
ms.author: yushwang
ms.openlocfilehash: dad13e02afe8dad2379db750eb09602e08e8ea99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="sample-configuration-cisco-asa-device-ikev2no-bgp"></a><span data-ttu-id="90fca-103">Exemple de configuration : appareil Cisco ASA (IKEv2/sans BGP)</span><span class="sxs-lookup"><span data-stu-id="90fca-103">Sample configuration: Cisco ASA device (IKEv2/no BGP)</span></span>
<span data-ttu-id="90fca-104">Cet article fournit des exemples de configurations pour les périphériques Cisco ASA connexion des passerelles VPN tooAzure.</span><span class="sxs-lookup"><span data-stu-id="90fca-104">This article provides sample configurations for Cisco ASA devices connecting tooAzure VPN gateways.</span></span>

## <a name="device-at-a-glance"></a><span data-ttu-id="90fca-105">Aperçu de l’appareil</span><span class="sxs-lookup"><span data-stu-id="90fca-105">Device at a glance</span></span>

|                        |                                   |
| ---                    | ---                               |
| <span data-ttu-id="90fca-106">Fournisseur de l’appareil</span><span class="sxs-lookup"><span data-stu-id="90fca-106">Device vendor</span></span>          | <span data-ttu-id="90fca-107">Cisco</span><span class="sxs-lookup"><span data-stu-id="90fca-107">Cisco</span></span>                             |
| <span data-ttu-id="90fca-108">Modèle de l'appareil</span><span class="sxs-lookup"><span data-stu-id="90fca-108">Device model</span></span>           | <span data-ttu-id="90fca-109">ASA (Adaptive Security Appliance)</span><span class="sxs-lookup"><span data-stu-id="90fca-109">ASA (Adaptive Security Appliance)</span></span> |
| <span data-ttu-id="90fca-110">Version cible</span><span class="sxs-lookup"><span data-stu-id="90fca-110">Target version</span></span>         | <span data-ttu-id="90fca-111">8.4+</span><span class="sxs-lookup"><span data-stu-id="90fca-111">8.4+</span></span>                              |
| <span data-ttu-id="90fca-112">Modèle testé</span><span class="sxs-lookup"><span data-stu-id="90fca-112">Tested model</span></span>           | <span data-ttu-id="90fca-113">ASA 5505</span><span class="sxs-lookup"><span data-stu-id="90fca-113">ASA 5505</span></span>                          |
| <span data-ttu-id="90fca-114">Version testée</span><span class="sxs-lookup"><span data-stu-id="90fca-114">Tested version</span></span>         | <span data-ttu-id="90fca-115">9.2</span><span class="sxs-lookup"><span data-stu-id="90fca-115">9.2</span></span>                               |
| <span data-ttu-id="90fca-116">Version IKE</span><span class="sxs-lookup"><span data-stu-id="90fca-116">IKE version</span></span>            | <span data-ttu-id="90fca-117">**IKEv2**</span><span class="sxs-lookup"><span data-stu-id="90fca-117">**IKEv2**</span></span>                         |
| <span data-ttu-id="90fca-118">BGP</span><span class="sxs-lookup"><span data-stu-id="90fca-118">BGP</span></span>                    | <span data-ttu-id="90fca-119">**Non**</span><span class="sxs-lookup"><span data-stu-id="90fca-119">**No**</span></span>                            |
| <span data-ttu-id="90fca-120">Type de passerelle VPN Azure</span><span class="sxs-lookup"><span data-stu-id="90fca-120">Azure VPN gateway type</span></span> | <span data-ttu-id="90fca-121">Passerelle VPN **basée sur le routage**</span><span class="sxs-lookup"><span data-stu-id="90fca-121">**Route-based** VPN gateway</span></span>       |
|                        |                                   |

> [!NOTE]
> 1. <span data-ttu-id="90fca-122">configuration de Hello ci-dessous connecte à un tooan de périphériques Cisco ASA Azure **basée sur un itinéraire** passerelle VPN à l’aide de stratégie IPsec/IKE personnalisée avec l’option de « UserPolicyBasedTrafficSelectors », comme décrit dans [cet article](vpn-gateway-connect-multiple-policybased-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="90fca-122">hello configuration below connects a Cisco ASA device tooan Azure **route-based** VPN gateway using custom IPsec/IKE policy with "UserPolicyBasedTrafficSelectors" option, as described in [this article](vpn-gateway-connect-multiple-policybased-rm-ps.md).</span></span>
> 2. <span data-ttu-id="90fca-123">Il requiert ASA appareils toouse **IKEv2** avec des configurations d’accès-list-based, pas des VTI.</span><span class="sxs-lookup"><span data-stu-id="90fca-123">It requires ASA devices toouse **IKEv2** with access-list-based configurations, not VTI-based.</span></span>
> 3. <span data-ttu-id="90fca-124">Consultez vos spécifications de fournisseur de périphérique VPN stratégie de hello tooensure est pris en charge sur les appareils de votre VPN sur site.</span><span class="sxs-lookup"><span data-stu-id="90fca-124">Please consult with your VPN device vendor specifications tooensure hello policy is supported on your on-premises VPN devices.</span></span>

## <a name="vpn-device-requirements"></a><span data-ttu-id="90fca-125">Configuration requise du périphérique VPN</span><span class="sxs-lookup"><span data-stu-id="90fca-125">VPN device requirements</span></span>
<span data-ttu-id="90fca-126">Les passerelles VPN Azure utilisent IPsec/IKE protocole suites tooestablish S2S VPN tunnels standards.</span><span class="sxs-lookup"><span data-stu-id="90fca-126">Azure VPN gateways use standard IPsec/IKE protocol suites tooestablish S2S VPN tunnels.</span></span> <span data-ttu-id="90fca-127">Consultez trop[propos des périphériques VPN](vpn-gateway-about-vpn-devices.md) pour hello plus les paramètres de protocole IPsec/IKE et les algorithmes de chiffrement par défaut pour les passerelles VPN Azure.</span><span class="sxs-lookup"><span data-stu-id="90fca-127">Refer too[About VPN devices](vpn-gateway-about-vpn-devices.md) for hello detailed IPsec/IKE protocol parameters and default cryptographic algorithms for Azure VPN gateways.</span></span> <span data-ttu-id="90fca-128">Vous pouvez éventuellement spécifier la combinaison de hello exacte des algorithmes de chiffrement et des avantages clés pour une connexion spécifique comme décrit dans [sur les exigences de chiffrement](vpn-gateway-about-compliance-crypto.md).</span><span class="sxs-lookup"><span data-stu-id="90fca-128">You can optionally specify hello exact combination of cryptographic algorithms and key strengths for a specific connection as described in [About cryptographic requirements](vpn-gateway-about-compliance-crypto.md).</span></span> <span data-ttu-id="90fca-129">Si vous sélectionnez une combinaison spécifique d’algorithmes de chiffrement et des avantages clés, assurez-vous que vous utilisez les spécifications correspondantes hello sur vos périphériques VPN.</span><span class="sxs-lookup"><span data-stu-id="90fca-129">If you select a specific combination of cryptographic algorithms and key strengths, please make sure you use hello corresponding specifications on your VPN devices.</span></span>

## <a name="single-vpn-tunnel"></a><span data-ttu-id="90fca-130">Tunnel VPN unique</span><span class="sxs-lookup"><span data-stu-id="90fca-130">Single VPN tunnel</span></span>
<span data-ttu-id="90fca-131">Cette topologie présente un tunnel VPN S2S unique entre une passerelle VPN Azure et votre périphérique VPN local.</span><span class="sxs-lookup"><span data-stu-id="90fca-131">This topology consists of a single S2S VPN tunnel between an Azure VPN gateway and your on-premises VPN device.</span></span> <span data-ttu-id="90fca-132">Vous pouvez éventuellement configurer BGP via un tunnel VPN de hello.</span><span class="sxs-lookup"><span data-stu-id="90fca-132">You can optionally configure BGP across hello VPN tunnel.</span></span>

![tunnel unique](./media/vpn-gateway-3rdparty-device-config-cisco-asa/singletunnel.png)

<span data-ttu-id="90fca-134">Consultez trop[le programme d’installation unique tunnel](vpn-gateway-3rdparty-device-config-overview.md#singletunnel) pour détaillées, des instructions détaillées toobuild hello configurations Azure.</span><span class="sxs-lookup"><span data-stu-id="90fca-134">Refer too[Single tunnel setup](vpn-gateway-3rdparty-device-config-overview.md#singletunnel) for detailed, step-by-step instructions toobuild hello Azure configurations.</span></span>

### <a name="network-and-vpn-gateway-information"></a><span data-ttu-id="90fca-135">Informations sur le réseau et la passerelle VPN</span><span class="sxs-lookup"><span data-stu-id="90fca-135">Network and VPN gateway information</span></span>
<span data-ttu-id="90fca-136">Cette section répertorie les paramètres hello pour hello cet exemple.</span><span class="sxs-lookup"><span data-stu-id="90fca-136">This section list hello parameters for hello this sample.</span></span>

| <span data-ttu-id="90fca-137">**Paramètre**</span><span class="sxs-lookup"><span data-stu-id="90fca-137">**Parameter**</span></span>                | <span data-ttu-id="90fca-138">**Valeur**</span><span class="sxs-lookup"><span data-stu-id="90fca-138">**Value**</span></span>                    |
| ---                          | ---                          |
| <span data-ttu-id="90fca-139">Préfixes d’adresse du réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="90fca-139">VNet address prefixes</span></span>        | <span data-ttu-id="90fca-140">10.11.0.0/16</span><span class="sxs-lookup"><span data-stu-id="90fca-140">10.11.0.0/16</span></span><br><span data-ttu-id="90fca-141">10.12.0.0/16</span><span class="sxs-lookup"><span data-stu-id="90fca-141">10.12.0.0/16</span></span> |
| <span data-ttu-id="90fca-142">IP de la passerelle VPN Azure</span><span class="sxs-lookup"><span data-stu-id="90fca-142">Azure VPN gateway IP</span></span>         | <span data-ttu-id="90fca-143">Azure_Gateway_Public_IP</span><span class="sxs-lookup"><span data-stu-id="90fca-143">Azure_Gateway_Public_IP</span></span>      |
| <span data-ttu-id="90fca-144">Préfixes d’adresse locale</span><span class="sxs-lookup"><span data-stu-id="90fca-144">On-premises address prefixes</span></span> | <span data-ttu-id="90fca-145">10.51.0.0/16</span><span class="sxs-lookup"><span data-stu-id="90fca-145">10.51.0.0/16</span></span><br><span data-ttu-id="90fca-146">10.52.0.0/16</span><span class="sxs-lookup"><span data-stu-id="90fca-146">10.52.0.0/16</span></span> |
| <span data-ttu-id="90fca-147">IP du périphérique VPN local</span><span class="sxs-lookup"><span data-stu-id="90fca-147">On-premises VPN device IP</span></span>    | <span data-ttu-id="90fca-148">OnPrem_Device_Public_IP</span><span class="sxs-lookup"><span data-stu-id="90fca-148">OnPrem_Device_Public_IP</span></span>     |
| <span data-ttu-id="90fca-149">* ASN BGP du réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="90fca-149">*VNet BGP ASN</span></span>                | <span data-ttu-id="90fca-150">65010</span><span class="sxs-lookup"><span data-stu-id="90fca-150">65010</span></span>                        |
| <span data-ttu-id="90fca-151">* IP d’homologue BGP Azure</span><span class="sxs-lookup"><span data-stu-id="90fca-151">*Azure BGP peer IP</span></span>           | <span data-ttu-id="90fca-152">10.12.255.30</span><span class="sxs-lookup"><span data-stu-id="90fca-152">10.12.255.30</span></span>                 |
| <span data-ttu-id="90fca-153">* ASN BGP local</span><span class="sxs-lookup"><span data-stu-id="90fca-153">*On-premises BGP ASN</span></span>         | <span data-ttu-id="90fca-154">65050</span><span class="sxs-lookup"><span data-stu-id="90fca-154">65050</span></span>                        |
| <span data-ttu-id="90fca-155">* IP d’homologue BGP local</span><span class="sxs-lookup"><span data-stu-id="90fca-155">*On-premises BGP peer IP</span></span>     | <span data-ttu-id="90fca-156">10.52.255.254</span><span class="sxs-lookup"><span data-stu-id="90fca-156">10.52.255.254</span></span>                |
|                              |                              |

* <span data-ttu-id="90fca-157">(*) Paramètres facultatifs pour BGP uniquement.</span><span class="sxs-lookup"><span data-stu-id="90fca-157">(*) Optional parameters for BGP only.</span></span>

### <a name="ipsecike-policy--parameters"></a><span data-ttu-id="90fca-158">Stratégie et paramètres IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="90fca-158">IPsec/IKE policy & parameters</span></span>

<span data-ttu-id="90fca-159">Hello ci-dessous répertorie les algorithmes IPsec/IKE hello et paramètres utilisés dans l’exemple hello.</span><span class="sxs-lookup"><span data-stu-id="90fca-159">hello table below lists hello IPsec/IKE algorithms and parameters used in hello sample.</span></span> <span data-ttu-id="90fca-160">Veuillez consulter votre toomake de spécifications de périphérique VPN que tous les algorithmes répertoriés ci-dessus sont pris en charge par vos modèles de périphérique VPN et les versions du microprogramme.</span><span class="sxs-lookup"><span data-stu-id="90fca-160">Please consult your VPN device specifications toomake sure all algorithms listed above are supported by your VPN device models and firmware versions.</span></span>

| <span data-ttu-id="90fca-161">**IPsec/IKEv2**</span><span class="sxs-lookup"><span data-stu-id="90fca-161">**IPsec/IKEv2**</span></span>  | <span data-ttu-id="90fca-162">**Valeur**</span><span class="sxs-lookup"><span data-stu-id="90fca-162">**Value**</span></span>                            |
| ---              | ---                                  |
| <span data-ttu-id="90fca-163">Chiffrement IKEv2</span><span class="sxs-lookup"><span data-stu-id="90fca-163">IKEv2 Encryption</span></span> | <span data-ttu-id="90fca-164">AES256</span><span class="sxs-lookup"><span data-stu-id="90fca-164">AES256</span></span>                               |
| <span data-ttu-id="90fca-165">Intégrité IKEv2</span><span class="sxs-lookup"><span data-stu-id="90fca-165">IKEv2 Integrity</span></span>  | <span data-ttu-id="90fca-166">SHA384</span><span class="sxs-lookup"><span data-stu-id="90fca-166">SHA384</span></span>                               |
| <span data-ttu-id="90fca-167">Groupe DH</span><span class="sxs-lookup"><span data-stu-id="90fca-167">DH Group</span></span>         | <span data-ttu-id="90fca-168">DHGroup24</span><span class="sxs-lookup"><span data-stu-id="90fca-168">DHGroup24</span></span>                            |
| <span data-ttu-id="90fca-169">Chiffrement IPsec</span><span class="sxs-lookup"><span data-stu-id="90fca-169">IPsec Encryption</span></span> | <span data-ttu-id="90fca-170">AES256</span><span class="sxs-lookup"><span data-stu-id="90fca-170">AES256</span></span>                               |
| <span data-ttu-id="90fca-171">Intégrité IPsec</span><span class="sxs-lookup"><span data-stu-id="90fca-171">IPsec Integrity</span></span>  | <span data-ttu-id="90fca-172">SHA1</span><span class="sxs-lookup"><span data-stu-id="90fca-172">SHA1</span></span>                                 |
| <span data-ttu-id="90fca-173">Groupe PFS</span><span class="sxs-lookup"><span data-stu-id="90fca-173">PFS Group</span></span>        | <span data-ttu-id="90fca-174">PFS24</span><span class="sxs-lookup"><span data-stu-id="90fca-174">PFS24</span></span>                                |
| <span data-ttu-id="90fca-175">Durée de vie de l’AS en mode rapide</span><span class="sxs-lookup"><span data-stu-id="90fca-175">QM SA Lifetime</span></span>   | <span data-ttu-id="90fca-176">7200 seconds</span><span class="sxs-lookup"><span data-stu-id="90fca-176">7200 seconds</span></span>                         |
| <span data-ttu-id="90fca-177">Sélecteur de trafic</span><span class="sxs-lookup"><span data-stu-id="90fca-177">Traffic Selector</span></span> | <span data-ttu-id="90fca-178">UsePolicyBasedTrafficSelectors $True</span><span class="sxs-lookup"><span data-stu-id="90fca-178">UsePolicyBasedTrafficSelectors $True</span></span> |
| <span data-ttu-id="90fca-179">Clé prépartagée</span><span class="sxs-lookup"><span data-stu-id="90fca-179">Pre-Shared Key</span></span>   | <span data-ttu-id="90fca-180">PreSharedKey</span><span class="sxs-lookup"><span data-stu-id="90fca-180">PreSharedKey</span></span>                         |
|                  |                                      |

- <span data-ttu-id="90fca-181">(*) Sur certains appareils, l’intégrité IPsec doit être « null » si GCM-AES est utilisé comme algorithme de chiffrement IPsec.</span><span class="sxs-lookup"><span data-stu-id="90fca-181">(*) On some device, IPsec integrity must be "null" if GCM-AES is used as IPsec encryption algorithm.</span></span>

### <a name="device-notes"></a><span data-ttu-id="90fca-182">Remarques sur l’appareil</span><span class="sxs-lookup"><span data-stu-id="90fca-182">Device notes</span></span>

>[!NOTE]
>
> 1. <span data-ttu-id="90fca-183">La prise en charge du protocole IKEv2 fonctionne avec les versions 8.4 et ultérieures d’ASA.</span><span class="sxs-lookup"><span data-stu-id="90fca-183">IKEv2 support requires ASA version 8.4 and above.</span></span>
> 2. <span data-ttu-id="90fca-184">La prise en charge des groupes Diffie-Hellman et PFS supérieurs (au-delà du groupe 5) nécessitent la version 9.x d’ASA.</span><span class="sxs-lookup"><span data-stu-id="90fca-184">Higher DH and PFS group support (beyond Group 5) requires ASA version 9.x.</span></span>
> 3. <span data-ttu-id="90fca-185">La prise en charge du chiffrement IPsec avec AES-GCM et de l’intégrité IPsec avec SHA-256, SHA-384, SHA-512 nécessite ASA 9.x sur le matériel ASA récent ; les modèles ASA 5505, 5510, 5520, 5540, 5550, 5580 ne sont **pas** pris en charge.</span><span class="sxs-lookup"><span data-stu-id="90fca-185">IPsec encryption with AES-GCM and IPsec integrity with SHA-256, SHA-384, SHA-512 support requires ASA version 9.x on newer ASA hardware; ASA 5505, 5510, 5520, 5540, 5550, 5580 are **not** supported.</span></span> <span data-ttu-id="90fca-186">(Vérifiez hello fournisseur spécifications tooconfirm.)</span><span class="sxs-lookup"><span data-stu-id="90fca-186">(Please check hello vendor specifications tooconfirm.)</span></span>
>


### <a name="sample-device-configurations"></a><span data-ttu-id="90fca-187">Exemples de configurations de périphérique</span><span class="sxs-lookup"><span data-stu-id="90fca-187">Sample device configurations</span></span>
<span data-ttu-id="90fca-188">script Hello ci-dessous fournit un exemple de configuration en fonction de la topologie de hello et des paramètres énumérés ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="90fca-188">hello script below provides a sample configuration based on hello topology and parameters listed above.</span></span> <span data-ttu-id="90fca-189">configuration de tunnel VPN de S2S Hello comprend hello composants suivants :</span><span class="sxs-lookup"><span data-stu-id="90fca-189">hello S2S VPN tunnel configuration consists of hello following parts:</span></span>

1. <span data-ttu-id="90fca-190">Interfaces et itinéraires</span><span class="sxs-lookup"><span data-stu-id="90fca-190">Interfaces & routes</span></span>
2. <span data-ttu-id="90fca-191">Listes d’accès</span><span class="sxs-lookup"><span data-stu-id="90fca-191">Access lists</span></span>
3. <span data-ttu-id="90fca-192">Stratégie et paramètres IKE (Phase 1 ou Mode principal)</span><span class="sxs-lookup"><span data-stu-id="90fca-192">IKE policy and parameters (Phase 1 or Main Mode)</span></span>
4. <span data-ttu-id="90fca-193">Stratégie et paramètres IPsec (Phase 2 ou Mode rapide)</span><span class="sxs-lookup"><span data-stu-id="90fca-193">IPsec policy and parameters (Phase 2 or Quick Mode)</span></span>
5. <span data-ttu-id="90fca-194">Autres paramètres (clamping du MSS TCP, etc.)</span><span class="sxs-lookup"><span data-stu-id="90fca-194">Other parameters (TCP MSS clamping, etc.)</span></span>

>[!IMPORTANT] 
><span data-ttu-id="90fca-195">Vérifiez que vous modifiiez davantage votre configuration hello répertoriée ci-dessous et remplacez les espaces réservés de hello avec les valeurs réelles hello :</span><span class="sxs-lookup"><span data-stu-id="90fca-195">Please make sure you complete hello additional configuration listed below and replace hello placeholders with hello actual values:</span></span>
> 
> - <span data-ttu-id="90fca-196">Configuration d’interfaces internes et externes</span><span class="sxs-lookup"><span data-stu-id="90fca-196">Interface configuration for both inside and outside interfaces</span></span>
> - <span data-ttu-id="90fca-197">Itinéraires pour vos réseaux internes/privés et externes/publics</span><span class="sxs-lookup"><span data-stu-id="90fca-197">Routes for your inside/private and outside/public networks</span></span>
> - <span data-ttu-id="90fca-198">Garantir que tous les noms et les numéros de stratégie sont uniques sur l’appareil de hello</span><span class="sxs-lookup"><span data-stu-id="90fca-198">Ensure all names and policy numbers are unique on hello device</span></span>
> - <span data-ttu-id="90fca-199">Vérifiez les algorithmes de chiffrement hello sont pris en charge sur votre appareil</span><span class="sxs-lookup"><span data-stu-id="90fca-199">Ensure hello cryptographic algorithms are supported on your device</span></span>
> - <span data-ttu-id="90fca-200">Remplacez hello suivant des espaces réservés par des valeurs réelles de hello</span><span class="sxs-lookup"><span data-stu-id="90fca-200">Replace hello following place holders with hello actual values</span></span>
>   - <span data-ttu-id="90fca-201">Nom de l’interface externe : « outside »</span><span class="sxs-lookup"><span data-stu-id="90fca-201">Outside interface name: "outside"</span></span>
>   - <span data-ttu-id="90fca-202">Azure_Gateway_Public_IP</span><span class="sxs-lookup"><span data-stu-id="90fca-202">Azure_Gateway_Public_IP</span></span>
>   - <span data-ttu-id="90fca-203">OnPrem_Device_Public_IP</span><span class="sxs-lookup"><span data-stu-id="90fca-203">OnPrem_Device_Public_IP</span></span>
>   - <span data-ttu-id="90fca-204">Pre_Shared_Key IKE</span><span class="sxs-lookup"><span data-stu-id="90fca-204">IKE Pre_Shared_Key</span></span>
>   - <span data-ttu-id="90fca-205">Noms du réseau virtuel et de la passerelle de réseau local (VNetName, LNGName)</span><span class="sxs-lookup"><span data-stu-id="90fca-205">VNet and local network gateway names (VNetName, LNGName)</span></span>
>   - <span data-ttu-id="90fca-206">Préfixes d’adresse du réseau virtuel et du réseau local</span><span class="sxs-lookup"><span data-stu-id="90fca-206">VNet and on-premises network address prefixes</span></span>
>   - <span data-ttu-id="90fca-207">Masques de réseau appropriés</span><span class="sxs-lookup"><span data-stu-id="90fca-207">Proper netmasks</span></span>

#### <a name="sample-configuration"></a><span data-ttu-id="90fca-208">Exemple de configuration</span><span class="sxs-lookup"><span data-stu-id="90fca-208">Sample configuration</span></span>

```
! Sample ASA configuration for connecting tooAzure VPN gateway
!
! Tested hardware: ASA 5505
! Tested version:  ASA version 9.2(4)
!
! Replace hello following place holders with your actual values:
!   - Interface names - default are "outside" and "inside"
!   - <Azure_Gateway_Public_IP>
!   - <OnPrem_Device_Public_IP>
!   - <Pre_Shared_Key>
!   - <VNetName>*
!   - <LNGName>* ==> LocalNetworkGateway - hello Azure resource that represents the
!     on-premises network, specifies network prefixes, device public IP, BGP info, etc.
!   - <PrivateIPAddress> ==> Replace it with a private IP address if applicable
!   - <Netmask> ==> Replace it with appropriate netmasks
!   - <Nexthop> ==> Replace it with hello actual nexthop IP address
!
! (*) Must be unique names in hello device configuration
!
! ==> Interface & route configurations
!
!     > <OnPrem_Device_Public_IP> address on hello outside interface or vlan
!     > <PrivateIPAddress> on hello inside interface or vlan; e.g., 10.51.0.1/24
!     > Route tooconnect too<Azure_Gateway_Public_IP> address
!
!     > Example:
!
!       interface Ethernet0/0
!        switchport access vlan 2
!       exit
!
!       interface vlan 1
!        nameif inside
!        security-level 100
!        ip address <PrivateIPAddress> <Netmask>
!       exit
!
!       interface vlan 2
!        nameif outside
!        security-level 0
!        ip address <OnPrem_Device_Public_IP> <Netmask>
!       exit
!
!       route outside 0.0.0.0 0.0.0.0 <NextHop IP> 1
!
! ==> Access lists
!
!     > Most firewall devices deny all traffic by default. Create access lists to
!       (1) Allow S2S VPN tunnels between hello ASA and hello Azure gateway public IP address
!       (2) Construct traffic selectors as part of IPsec policy or proposal
!
access-list outside_access_in extended permit ip host <Azure_Gateway_Public_IP> host <OnPrem_Device_Public_IP>
!
!     > Object group that consists of all VNet prefixes (e.g., 10.11.0.0/16 &
!       10.12.0.0/16)
!
object-group network Azure-<VNetName>
 description Azure virtual network <VNetName> prefixes
 network-object 10.11.0.0 255.255.0.0
 network-object 10.12.0.0 255.255.0.0
exit
!
!     > Object group that corresponding toohello <LNGName> prefixes.
!       E.g., 10.51.0.0/16 and 10.52.0.0/16. Note that LNG = "local network gateway".
!       In Azure network resource, a local network gateway defines hello on-premises
!       network properties (address prefixes, VPN device IP, BGP ASN, etc.)
!
object-group network <LNGName>
 description On-Premises network <LNGName> prefixes
 network-object 10.51.0.0 255.255.0.0
 network-object 10.52.0.0 255.255.0.0
exit
!
!     > Specify hello access-list between hello Azure VNet and your on-premises network.
!       This access list defines hello IPsec SA traffic selectors.
!
access-list Azure-<VNetName>-acl extended permit ip object-group <LNGName> object-group Azure-<VNetName>
!
!     > No NAT required between hello on-premises network and Azure VNet
!
nat (inside,outside) source static <LNGName> <LNGName> destination static Azure-<VNetName> Azure-<VNetName>
!
! ==> IKEv2 configuration
!
!     > General IKEv2 configuration - enable IKEv2 for VPN
!
group-policy DfltGrpPolicy attributes
 vpn-tunnel-protocol ikev1 ikev2
exit
!
crypto isakmp identity address
crypto ikev2 enable outside
!
!     > Define IKEv2 Phase 1/Main Mode policy
!       - Make sure hello policy number is not used
!       - integrity and prf must be hello same
!       - DH group 14 and above require ASA version 9.x.
!
crypto ikev2 policy 1
 encryption       aes-256
 integrity        sha384
 prf              sha384
 group            24
 lifetime seconds 86400
exit
!
!     > Set connection type and pre-shared key
!
tunnel-group <Azure_Gateway_Public_IP> type ipsec-l2l
tunnel-group <Azure_Gateway_Public_IP> ipsec-attributes
 ikev2 remote-authentication pre-shared-key <Pre_Shared_Key> 
 ikev2 local-authentication  pre-shared-key <Pre_Shared_Key> 
exit
!
! ==> IPsec configuration
!
!     > IKEv2 Phase 2/Quick Mode proposal
!       - AES-GCM and SHA-2 requires ASA version 9.x on newer ASA models. ASA
!         5505, 5510, 5520, 5540, 5550, 5580 are not supported.
!       - ESP integrity must be null if AES-GCM is configured as ESP encryption
!
crypto ipsec ikev2 ipsec-proposal AES-256
 protocol esp encryption aes-256
 protocol esp integrity  sha-1
exit
!
!     > Set access list & traffic selectors, PFS, IPsec protposal, SA lifetime
!       - This sample uses "Azure-<VNetName>-map" as hello crypto map name
!       - ASA supports only one crypto map per interface, if you already have
!         an existing crypto map assigned tooyour outside interface, you must use
!         hello same crypto map name, but with a different sequence number for
!         this policy
!       - "match address" policy uses hello access-list "Azure-<VNetName>-acl" defined 
!         previously
!       - "ipsec-proposal" uses hello proposal "AES-256" defined previously 
!       - PFS groups 14 and beyond requires ASA version 9.x.
!
crypto map Azure-<VNetName>-map 1 match address Azure-<VNetName>-acl
crypto map Azure-<VNetName>-map 1 set pfs group24
crypto map Azure-<VNetName>-map 1 set peer <Azure_Gateway_Public_IP>
crypto map Azure-<VNetName>-map 1 set ikev2 ipsec-proposal AES-256
crypto map Azure-<VNetName>-map 1 set security-association lifetime seconds 7200
crypto map Azure-<VNetName>-map interface outside
!
! ==> Set TCP MSS too1350
!
sysopt connection tcpmss 1350
!
```

## <a name="simple-debugging-commands"></a><span data-ttu-id="90fca-209">Commandes de débogage simples</span><span class="sxs-lookup"><span data-stu-id="90fca-209">Simple debugging commands</span></span>

<span data-ttu-id="90fca-210">Voici quelques commandes ASA de débogage :</span><span class="sxs-lookup"><span data-stu-id="90fca-210">Here are some ASA commands for debugging purposes:</span></span>

1. <span data-ttu-id="90fca-211">Afficher hello IPsec et IKE SA</span><span class="sxs-lookup"><span data-stu-id="90fca-211">Show hello IPsec and IKE SA's</span></span>
    - <span data-ttu-id="90fca-212">« show crypto ipsec sa »</span><span class="sxs-lookup"><span data-stu-id="90fca-212">"show crypto ipsec sa"</span></span>
    - <span data-ttu-id="90fca-213">« show crypto ikev2 sa »</span><span class="sxs-lookup"><span data-stu-id="90fca-213">"show crypto ikev2 sa"</span></span>
2. <span data-ttu-id="90fca-214">Passer en mode de débogage - il peut obtenir très bruyant sur console de hello</span><span class="sxs-lookup"><span data-stu-id="90fca-214">Entering debug mode - this can get very noisy on hello console</span></span>
    - <span data-ttu-id="90fca-215">« debug crypto ikev2 platform <level> »</span><span class="sxs-lookup"><span data-stu-id="90fca-215">"debug crypto ikev2 platform <level>"</span></span>
    - <span data-ttu-id="90fca-216">« debug crypto ikev2 protocol <level> »</span><span class="sxs-lookup"><span data-stu-id="90fca-216">"debug crypto ikev2 protocol <level>"</span></span>
3. <span data-ttu-id="90fca-217">Répertorier les configurations actuelles</span><span class="sxs-lookup"><span data-stu-id="90fca-217">List current configurations</span></span>
    - <span data-ttu-id="90fca-218">« Afficher exécution » - affiche hello configurations actuelles sur l’appareil de hello ; Vous pouvez utiliser hello plusieurs sous-commandes toolist des parties spécifiques de la configuration de hello.</span><span class="sxs-lookup"><span data-stu-id="90fca-218">"show run" - shows hello current configurations on hello device; you can use hello various sub-commands toolist specific parts of hello configuration.</span></span> <span data-ttu-id="90fca-219">Par exemple, « show run crypto », « show run access-list », « show run tunnel-group », etc.</span><span class="sxs-lookup"><span data-stu-id="90fca-219">E.g., "show run crypto", "show run access-list", "show run tunnel-group", etc.</span></span>


## <a name="next-steps"></a><span data-ttu-id="90fca-220">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="90fca-220">Next steps</span></span>
<span data-ttu-id="90fca-221">Consultez [configuration des passerelles VPN actif pour entre différents locaux et les connexions de réseau à](vpn-gateway-activeactive-rm-powershell.md) pour les étapes tooconfigure actif entre différents locaux et les connexions au réseau.</span><span class="sxs-lookup"><span data-stu-id="90fca-221">See [Configuring Active-Active VPN Gateways for Cross-Premises and VNet-to-VNet Connections](vpn-gateway-activeactive-rm-powershell.md) for steps tooconfigure active-active cross-premises and VNet-to-VNet connections.</span></span>

