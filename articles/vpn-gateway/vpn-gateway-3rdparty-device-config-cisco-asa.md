---
title: "Exemple de configuration - Appareil Cisco ASA se connectant à des passerelles VPN Azure | Microsoft Docs"
description: "Cet article fournit un exemple de configuration d’appareil Cisco ASA se connectant à des passerelles VPN Azure."
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
ms.openlocfilehash: 10466b8928e2cd687f7961a2956b6d60823b82be
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="sample-configuration-cisco-asa-device-ikev2no-bgp"></a><span data-ttu-id="a6f85-103">Exemple de configuration : appareil Cisco ASA (IKEv2/sans BGP)</span><span class="sxs-lookup"><span data-stu-id="a6f85-103">Sample configuration: Cisco ASA device (IKEv2/no BGP)</span></span>
<span data-ttu-id="a6f85-104">Cet article fournit des exemples de configuration d’appareil Cisco ASA se connectant à des passerelles VPN Azure.</span><span class="sxs-lookup"><span data-stu-id="a6f85-104">This article provides sample configurations for Cisco ASA devices connecting to Azure VPN gateways.</span></span>

## <a name="device-at-a-glance"></a><span data-ttu-id="a6f85-105">Aperçu de l’appareil</span><span class="sxs-lookup"><span data-stu-id="a6f85-105">Device at a glance</span></span>

|                        |                                   |
| ---                    | ---                               |
| <span data-ttu-id="a6f85-106">Fournisseur de l’appareil</span><span class="sxs-lookup"><span data-stu-id="a6f85-106">Device vendor</span></span>          | <span data-ttu-id="a6f85-107">Cisco</span><span class="sxs-lookup"><span data-stu-id="a6f85-107">Cisco</span></span>                             |
| <span data-ttu-id="a6f85-108">Modèle de l'appareil</span><span class="sxs-lookup"><span data-stu-id="a6f85-108">Device model</span></span>           | <span data-ttu-id="a6f85-109">ASA (Adaptive Security Appliance)</span><span class="sxs-lookup"><span data-stu-id="a6f85-109">ASA (Adaptive Security Appliance)</span></span> |
| <span data-ttu-id="a6f85-110">Version cible</span><span class="sxs-lookup"><span data-stu-id="a6f85-110">Target version</span></span>         | <span data-ttu-id="a6f85-111">8.4+</span><span class="sxs-lookup"><span data-stu-id="a6f85-111">8.4+</span></span>                              |
| <span data-ttu-id="a6f85-112">Modèle testé</span><span class="sxs-lookup"><span data-stu-id="a6f85-112">Tested model</span></span>           | <span data-ttu-id="a6f85-113">ASA 5505</span><span class="sxs-lookup"><span data-stu-id="a6f85-113">ASA 5505</span></span>                          |
| <span data-ttu-id="a6f85-114">Version testée</span><span class="sxs-lookup"><span data-stu-id="a6f85-114">Tested version</span></span>         | <span data-ttu-id="a6f85-115">9.2</span><span class="sxs-lookup"><span data-stu-id="a6f85-115">9.2</span></span>                               |
| <span data-ttu-id="a6f85-116">Version IKE</span><span class="sxs-lookup"><span data-stu-id="a6f85-116">IKE version</span></span>            | <span data-ttu-id="a6f85-117">**IKEv2**</span><span class="sxs-lookup"><span data-stu-id="a6f85-117">**IKEv2**</span></span>                         |
| <span data-ttu-id="a6f85-118">BGP</span><span class="sxs-lookup"><span data-stu-id="a6f85-118">BGP</span></span>                    | <span data-ttu-id="a6f85-119">**Non**</span><span class="sxs-lookup"><span data-stu-id="a6f85-119">**No**</span></span>                            |
| <span data-ttu-id="a6f85-120">Type de passerelle VPN Azure</span><span class="sxs-lookup"><span data-stu-id="a6f85-120">Azure VPN gateway type</span></span> | <span data-ttu-id="a6f85-121">Passerelle VPN **basée sur le routage**</span><span class="sxs-lookup"><span data-stu-id="a6f85-121">**Route-based** VPN gateway</span></span>       |
|                        |                                   |

> [!NOTE]
> 1. <span data-ttu-id="a6f85-122">La configuration ci-dessous connecte un appareil Cisco ASA à une passerelle VPN Azure **basée sur le routage** à l’aide d’une stratégie IPsec/IKE personnalisée avec l’option « UserPolicyBasedTrafficSelectors », comme décrit dans [cet article](vpn-gateway-connect-multiple-policybased-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="a6f85-122">The configuration below connects a Cisco ASA device to an Azure **route-based** VPN gateway using custom IPsec/IKE policy with "UserPolicyBasedTrafficSelectors" option, as described in [this article](vpn-gateway-connect-multiple-policybased-rm-ps.md).</span></span>
> 2. <span data-ttu-id="a6f85-123">Les appareils ASA doivent utiliser la version **IKEv2** avec les configurations basées sur des listes d’accès, pas celles basées sur une interface virtuelle de tunnel (VTI).</span><span class="sxs-lookup"><span data-stu-id="a6f85-123">It requires ASA devices to use **IKEv2** with access-list-based configurations, not VTI-based.</span></span>
> 3. <span data-ttu-id="a6f85-124">Veuillez consulter les spécifications de votre fournisseur de périphérique VPN pour vous assurer que la stratégie est prise en charge sur vos périphériques VPN locaux.</span><span class="sxs-lookup"><span data-stu-id="a6f85-124">Please consult with your VPN device vendor specifications to ensure the policy is supported on your on-premises VPN devices.</span></span>

## <a name="vpn-device-requirements"></a><span data-ttu-id="a6f85-125">Configuration requise du périphérique VPN</span><span class="sxs-lookup"><span data-stu-id="a6f85-125">VPN device requirements</span></span>
<span data-ttu-id="a6f85-126">Les passerelles VPN Azure utilisent des suites de protocoles IPsec/IKE standard pour établir des tunnels VPN site à site (S2S).</span><span class="sxs-lookup"><span data-stu-id="a6f85-126">Azure VPN gateways use standard IPsec/IKE protocol suites to establish S2S VPN tunnels.</span></span> <span data-ttu-id="a6f85-127">Reportez-vous à la page [À propos des périphériques VPN](vpn-gateway-about-vpn-devices.md) pour connaître les paramètres détaillés du protocole IPsec/IKE et les algorithmes de chiffrement par défaut des passerelles VPN Azure.</span><span class="sxs-lookup"><span data-stu-id="a6f85-127">Refer to [About VPN devices](vpn-gateway-about-vpn-devices.md) for the detailed IPsec/IKE protocol parameters and default cryptographic algorithms for Azure VPN gateways.</span></span> <span data-ttu-id="a6f85-128">Vous pouvez éventuellement spécifier la combinaison exacte d’algorithmes de chiffrement et les forces de clé souhaitée d’une connexion spécifique, comme décrit dans la rubrique [À propos des exigences de chiffrement](vpn-gateway-about-compliance-crypto.md).</span><span class="sxs-lookup"><span data-stu-id="a6f85-128">You can optionally specify the exact combination of cryptographic algorithms and key strengths for a specific connection as described in [About cryptographic requirements](vpn-gateway-about-compliance-crypto.md).</span></span> <span data-ttu-id="a6f85-129">Si vous sélectionnez une combinaison spécifique d’algorithmes de chiffrement et de forces de clé, assurez-vous que vous utilisez les spécifications correspondantes sur vos périphériques VPN.</span><span class="sxs-lookup"><span data-stu-id="a6f85-129">If you select a specific combination of cryptographic algorithms and key strengths, please make sure you use the corresponding specifications on your VPN devices.</span></span>

## <a name="single-vpn-tunnel"></a><span data-ttu-id="a6f85-130">Tunnel VPN unique</span><span class="sxs-lookup"><span data-stu-id="a6f85-130">Single VPN tunnel</span></span>
<span data-ttu-id="a6f85-131">Cette topologie présente un tunnel VPN S2S unique entre une passerelle VPN Azure et votre périphérique VPN local.</span><span class="sxs-lookup"><span data-stu-id="a6f85-131">This topology consists of a single S2S VPN tunnel between an Azure VPN gateway and your on-premises VPN device.</span></span> <span data-ttu-id="a6f85-132">Vous pouvez éventuellement configurer le protocole BGP sur le tunnel VPN.</span><span class="sxs-lookup"><span data-stu-id="a6f85-132">You can optionally configure BGP across the VPN tunnel.</span></span>

![tunnel unique](./media/vpn-gateway-3rdparty-device-config-cisco-asa/singletunnel.png)

<span data-ttu-id="a6f85-134">Reportez-vous à la section [Tunnel VPN unique](vpn-gateway-3rdparty-device-config-overview.md#singletunnel) afin de connaître les instructions étape par étape pour créer les configurations Azure.</span><span class="sxs-lookup"><span data-stu-id="a6f85-134">Refer to [Single tunnel setup](vpn-gateway-3rdparty-device-config-overview.md#singletunnel) for detailed, step-by-step instructions to build the Azure configurations.</span></span>

### <a name="network-and-vpn-gateway-information"></a><span data-ttu-id="a6f85-135">Informations sur le réseau et la passerelle VPN</span><span class="sxs-lookup"><span data-stu-id="a6f85-135">Network and VPN gateway information</span></span>
<span data-ttu-id="a6f85-136">Cette section répertorie les paramètres de cet exemple.</span><span class="sxs-lookup"><span data-stu-id="a6f85-136">This section list the parameters for the this sample.</span></span>

| <span data-ttu-id="a6f85-137">**Paramètre**</span><span class="sxs-lookup"><span data-stu-id="a6f85-137">**Parameter**</span></span>                | <span data-ttu-id="a6f85-138">**Valeur**</span><span class="sxs-lookup"><span data-stu-id="a6f85-138">**Value**</span></span>                    |
| ---                          | ---                          |
| <span data-ttu-id="a6f85-139">Préfixes d’adresse du réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="a6f85-139">VNet address prefixes</span></span>        | <span data-ttu-id="a6f85-140">10.11.0.0/16</span><span class="sxs-lookup"><span data-stu-id="a6f85-140">10.11.0.0/16</span></span><br><span data-ttu-id="a6f85-141">10.12.0.0/16</span><span class="sxs-lookup"><span data-stu-id="a6f85-141">10.12.0.0/16</span></span> |
| <span data-ttu-id="a6f85-142">IP de la passerelle VPN Azure</span><span class="sxs-lookup"><span data-stu-id="a6f85-142">Azure VPN gateway IP</span></span>         | <span data-ttu-id="a6f85-143">Azure_Gateway_Public_IP</span><span class="sxs-lookup"><span data-stu-id="a6f85-143">Azure_Gateway_Public_IP</span></span>      |
| <span data-ttu-id="a6f85-144">Préfixes d’adresse locale</span><span class="sxs-lookup"><span data-stu-id="a6f85-144">On-premises address prefixes</span></span> | <span data-ttu-id="a6f85-145">10.51.0.0/16</span><span class="sxs-lookup"><span data-stu-id="a6f85-145">10.51.0.0/16</span></span><br><span data-ttu-id="a6f85-146">10.52.0.0/16</span><span class="sxs-lookup"><span data-stu-id="a6f85-146">10.52.0.0/16</span></span> |
| <span data-ttu-id="a6f85-147">IP du périphérique VPN local</span><span class="sxs-lookup"><span data-stu-id="a6f85-147">On-premises VPN device IP</span></span>    | <span data-ttu-id="a6f85-148">OnPrem_Device_Public_IP</span><span class="sxs-lookup"><span data-stu-id="a6f85-148">OnPrem_Device_Public_IP</span></span>     |
| <span data-ttu-id="a6f85-149">* ASN BGP du réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="a6f85-149">*VNet BGP ASN</span></span>                | <span data-ttu-id="a6f85-150">65010</span><span class="sxs-lookup"><span data-stu-id="a6f85-150">65010</span></span>                        |
| <span data-ttu-id="a6f85-151">* IP d’homologue BGP Azure</span><span class="sxs-lookup"><span data-stu-id="a6f85-151">*Azure BGP peer IP</span></span>           | <span data-ttu-id="a6f85-152">10.12.255.30</span><span class="sxs-lookup"><span data-stu-id="a6f85-152">10.12.255.30</span></span>                 |
| <span data-ttu-id="a6f85-153">* ASN BGP local</span><span class="sxs-lookup"><span data-stu-id="a6f85-153">*On-premises BGP ASN</span></span>         | <span data-ttu-id="a6f85-154">65050</span><span class="sxs-lookup"><span data-stu-id="a6f85-154">65050</span></span>                        |
| <span data-ttu-id="a6f85-155">* IP d’homologue BGP local</span><span class="sxs-lookup"><span data-stu-id="a6f85-155">*On-premises BGP peer IP</span></span>     | <span data-ttu-id="a6f85-156">10.52.255.254</span><span class="sxs-lookup"><span data-stu-id="a6f85-156">10.52.255.254</span></span>                |
|                              |                              |

* <span data-ttu-id="a6f85-157">(*) Paramètres facultatifs pour BGP uniquement.</span><span class="sxs-lookup"><span data-stu-id="a6f85-157">(*) Optional parameters for BGP only.</span></span>

### <a name="ipsecike-policy--parameters"></a><span data-ttu-id="a6f85-158">Stratégie et paramètres IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="a6f85-158">IPsec/IKE policy & parameters</span></span>

<span data-ttu-id="a6f85-159">Le tableau ci-dessous répertorie les algorithmes et paramètres IPsec/IKE utilisés dans l’exemple.</span><span class="sxs-lookup"><span data-stu-id="a6f85-159">The table below lists the IPsec/IKE algorithms and parameters used in the sample.</span></span> <span data-ttu-id="a6f85-160">Consultez les spécifications de votre périphérique VPN pour vous assurer que tous les algorithmes répertoriés ci-dessus sont pris en charge par vos modèles de périphérique VPN et les versions du microprogramme.</span><span class="sxs-lookup"><span data-stu-id="a6f85-160">Please consult your VPN device specifications to make sure all algorithms listed above are supported by your VPN device models and firmware versions.</span></span>

| <span data-ttu-id="a6f85-161">**IPsec/IKEv2**</span><span class="sxs-lookup"><span data-stu-id="a6f85-161">**IPsec/IKEv2**</span></span>  | <span data-ttu-id="a6f85-162">**Valeur**</span><span class="sxs-lookup"><span data-stu-id="a6f85-162">**Value**</span></span>                            |
| ---              | ---                                  |
| <span data-ttu-id="a6f85-163">Chiffrement IKEv2</span><span class="sxs-lookup"><span data-stu-id="a6f85-163">IKEv2 Encryption</span></span> | <span data-ttu-id="a6f85-164">AES256</span><span class="sxs-lookup"><span data-stu-id="a6f85-164">AES256</span></span>                               |
| <span data-ttu-id="a6f85-165">Intégrité IKEv2</span><span class="sxs-lookup"><span data-stu-id="a6f85-165">IKEv2 Integrity</span></span>  | <span data-ttu-id="a6f85-166">SHA384</span><span class="sxs-lookup"><span data-stu-id="a6f85-166">SHA384</span></span>                               |
| <span data-ttu-id="a6f85-167">Groupe DH</span><span class="sxs-lookup"><span data-stu-id="a6f85-167">DH Group</span></span>         | <span data-ttu-id="a6f85-168">DHGroup24</span><span class="sxs-lookup"><span data-stu-id="a6f85-168">DHGroup24</span></span>                            |
| <span data-ttu-id="a6f85-169">Chiffrement IPsec</span><span class="sxs-lookup"><span data-stu-id="a6f85-169">IPsec Encryption</span></span> | <span data-ttu-id="a6f85-170">AES256</span><span class="sxs-lookup"><span data-stu-id="a6f85-170">AES256</span></span>                               |
| <span data-ttu-id="a6f85-171">Intégrité IPsec</span><span class="sxs-lookup"><span data-stu-id="a6f85-171">IPsec Integrity</span></span>  | <span data-ttu-id="a6f85-172">SHA1</span><span class="sxs-lookup"><span data-stu-id="a6f85-172">SHA1</span></span>                                 |
| <span data-ttu-id="a6f85-173">Groupe PFS</span><span class="sxs-lookup"><span data-stu-id="a6f85-173">PFS Group</span></span>        | <span data-ttu-id="a6f85-174">PFS24</span><span class="sxs-lookup"><span data-stu-id="a6f85-174">PFS24</span></span>                                |
| <span data-ttu-id="a6f85-175">Durée de vie de l’AS en mode rapide</span><span class="sxs-lookup"><span data-stu-id="a6f85-175">QM SA Lifetime</span></span>   | <span data-ttu-id="a6f85-176">7200 seconds</span><span class="sxs-lookup"><span data-stu-id="a6f85-176">7200 seconds</span></span>                         |
| <span data-ttu-id="a6f85-177">Sélecteur de trafic</span><span class="sxs-lookup"><span data-stu-id="a6f85-177">Traffic Selector</span></span> | <span data-ttu-id="a6f85-178">UsePolicyBasedTrafficSelectors $True</span><span class="sxs-lookup"><span data-stu-id="a6f85-178">UsePolicyBasedTrafficSelectors $True</span></span> |
| <span data-ttu-id="a6f85-179">Clé prépartagée</span><span class="sxs-lookup"><span data-stu-id="a6f85-179">Pre-Shared Key</span></span>   | <span data-ttu-id="a6f85-180">PreSharedKey</span><span class="sxs-lookup"><span data-stu-id="a6f85-180">PreSharedKey</span></span>                         |
|                  |                                      |

- <span data-ttu-id="a6f85-181">(*) Sur certains appareils, l’intégrité IPsec doit être « null » si GCM-AES est utilisé comme algorithme de chiffrement IPsec.</span><span class="sxs-lookup"><span data-stu-id="a6f85-181">(*) On some device, IPsec integrity must be "null" if GCM-AES is used as IPsec encryption algorithm.</span></span>

### <a name="device-notes"></a><span data-ttu-id="a6f85-182">Remarques sur l’appareil</span><span class="sxs-lookup"><span data-stu-id="a6f85-182">Device notes</span></span>

>[!NOTE]
>
> 1. <span data-ttu-id="a6f85-183">La prise en charge du protocole IKEv2 fonctionne avec les versions 8.4 et ultérieures d’ASA.</span><span class="sxs-lookup"><span data-stu-id="a6f85-183">IKEv2 support requires ASA version 8.4 and above.</span></span>
> 2. <span data-ttu-id="a6f85-184">La prise en charge des groupes Diffie-Hellman et PFS supérieurs (au-delà du groupe 5) nécessitent la version 9.x d’ASA.</span><span class="sxs-lookup"><span data-stu-id="a6f85-184">Higher DH and PFS group support (beyond Group 5) requires ASA version 9.x.</span></span>
> 3. <span data-ttu-id="a6f85-185">La prise en charge du chiffrement IPsec avec AES-GCM et de l’intégrité IPsec avec SHA-256, SHA-384, SHA-512 nécessite ASA 9.x sur le matériel ASA récent ; les modèles ASA 5505, 5510, 5520, 5540, 5550, 5580 ne sont **pas** pris en charge.</span><span class="sxs-lookup"><span data-stu-id="a6f85-185">IPsec encryption with AES-GCM and IPsec integrity with SHA-256, SHA-384, SHA-512 support requires ASA version 9.x on newer ASA hardware; ASA 5505, 5510, 5520, 5540, 5550, 5580 are **not** supported.</span></span> <span data-ttu-id="a6f85-186">(Consultez les spécifications du fournisseur pour confirmer ce point.)</span><span class="sxs-lookup"><span data-stu-id="a6f85-186">(Please check the vendor specifications to confirm.)</span></span>
>


### <a name="sample-device-configurations"></a><span data-ttu-id="a6f85-187">Exemples de configurations de périphérique</span><span class="sxs-lookup"><span data-stu-id="a6f85-187">Sample device configurations</span></span>
<span data-ttu-id="a6f85-188">Le script ci-dessous fournit un exemple de configuration basé sur la topologie et les paramètres répertoriés ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="a6f85-188">The script below provides a sample configuration based on the topology and parameters listed above.</span></span> <span data-ttu-id="a6f85-189">La configuration du tunnel VPN S2S comprend les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="a6f85-189">The S2S VPN tunnel configuration consists of the following parts:</span></span>

1. <span data-ttu-id="a6f85-190">Interfaces et itinéraires</span><span class="sxs-lookup"><span data-stu-id="a6f85-190">Interfaces & routes</span></span>
2. <span data-ttu-id="a6f85-191">Listes d’accès</span><span class="sxs-lookup"><span data-stu-id="a6f85-191">Access lists</span></span>
3. <span data-ttu-id="a6f85-192">Stratégie et paramètres IKE (Phase 1 ou Mode principal)</span><span class="sxs-lookup"><span data-stu-id="a6f85-192">IKE policy and parameters (Phase 1 or Main Mode)</span></span>
4. <span data-ttu-id="a6f85-193">Stratégie et paramètres IPsec (Phase 2 ou Mode rapide)</span><span class="sxs-lookup"><span data-stu-id="a6f85-193">IPsec policy and parameters (Phase 2 or Quick Mode)</span></span>
5. <span data-ttu-id="a6f85-194">Autres paramètres (clamping du MSS TCP, etc.)</span><span class="sxs-lookup"><span data-stu-id="a6f85-194">Other parameters (TCP MSS clamping, etc.)</span></span>

>[!IMPORTANT] 
><span data-ttu-id="a6f85-195">Veillez à bien effectuer la configuration des éléments supplémentaires ci-dessous et à remplacer les espaces réservés par les valeurs réelles :</span><span class="sxs-lookup"><span data-stu-id="a6f85-195">Please make sure you complete the additional configuration listed below and replace the placeholders with the actual values:</span></span>
> 
> - <span data-ttu-id="a6f85-196">Configuration d’interfaces internes et externes</span><span class="sxs-lookup"><span data-stu-id="a6f85-196">Interface configuration for both inside and outside interfaces</span></span>
> - <span data-ttu-id="a6f85-197">Itinéraires pour vos réseaux internes/privés et externes/publics</span><span class="sxs-lookup"><span data-stu-id="a6f85-197">Routes for your inside/private and outside/public networks</span></span>
> - <span data-ttu-id="a6f85-198">Veiller à ce que tous les noms et les numéros de stratégie soient uniques sur l’appareil</span><span class="sxs-lookup"><span data-stu-id="a6f85-198">Ensure all names and policy numbers are unique on the device</span></span>
> - <span data-ttu-id="a6f85-199">Vérifier que les algorithmes de chiffrement sont pris en charge sur votre appareil</span><span class="sxs-lookup"><span data-stu-id="a6f85-199">Ensure the cryptographic algorithms are supported on your device</span></span>
> - <span data-ttu-id="a6f85-200">Remplacer les espaces réservés suivants avec les valeurs réelles</span><span class="sxs-lookup"><span data-stu-id="a6f85-200">Replace the following place holders with the actual values</span></span>
>   - <span data-ttu-id="a6f85-201">Nom de l’interface externe : « outside »</span><span class="sxs-lookup"><span data-stu-id="a6f85-201">Outside interface name: "outside"</span></span>
>   - <span data-ttu-id="a6f85-202">Azure_Gateway_Public_IP</span><span class="sxs-lookup"><span data-stu-id="a6f85-202">Azure_Gateway_Public_IP</span></span>
>   - <span data-ttu-id="a6f85-203">OnPrem_Device_Public_IP</span><span class="sxs-lookup"><span data-stu-id="a6f85-203">OnPrem_Device_Public_IP</span></span>
>   - <span data-ttu-id="a6f85-204">Pre_Shared_Key IKE</span><span class="sxs-lookup"><span data-stu-id="a6f85-204">IKE Pre_Shared_Key</span></span>
>   - <span data-ttu-id="a6f85-205">Noms du réseau virtuel et de la passerelle de réseau local (VNetName, LNGName)</span><span class="sxs-lookup"><span data-stu-id="a6f85-205">VNet and local network gateway names (VNetName, LNGName)</span></span>
>   - <span data-ttu-id="a6f85-206">Préfixes d’adresse du réseau virtuel et du réseau local</span><span class="sxs-lookup"><span data-stu-id="a6f85-206">VNet and on-premises network address prefixes</span></span>
>   - <span data-ttu-id="a6f85-207">Masques de réseau appropriés</span><span class="sxs-lookup"><span data-stu-id="a6f85-207">Proper netmasks</span></span>

#### <a name="sample-configuration"></a><span data-ttu-id="a6f85-208">Exemple de configuration</span><span class="sxs-lookup"><span data-stu-id="a6f85-208">Sample configuration</span></span>

```
! Sample ASA configuration for connecting to Azure VPN gateway
!
! Tested hardware: ASA 5505
! Tested version:  ASA version 9.2(4)
!
! Replace the following place holders with your actual values:
!   - Interface names - default are "outside" and "inside"
!   - <Azure_Gateway_Public_IP>
!   - <OnPrem_Device_Public_IP>
!   - <Pre_Shared_Key>
!   - <VNetName>*
!   - <LNGName>* ==> LocalNetworkGateway - the Azure resource that represents the
!     on-premises network, specifies network prefixes, device public IP, BGP info, etc.
!   - <PrivateIPAddress> ==> Replace it with a private IP address if applicable
!   - <Netmask> ==> Replace it with appropriate netmasks
!   - <Nexthop> ==> Replace it with the actual nexthop IP address
!
! (*) Must be unique names in the device configuration
!
! ==> Interface & route configurations
!
!     > <OnPrem_Device_Public_IP> address on the outside interface or vlan
!     > <PrivateIPAddress> on the inside interface or vlan; e.g., 10.51.0.1/24
!     > Route to connect to <Azure_Gateway_Public_IP> address
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
!       (1) Allow S2S VPN tunnels between the ASA and the Azure gateway public IP address
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
!     > Object group that corresponding to the <LNGName> prefixes.
!       E.g., 10.51.0.0/16 and 10.52.0.0/16. Note that LNG = "local network gateway".
!       In Azure network resource, a local network gateway defines the on-premises
!       network properties (address prefixes, VPN device IP, BGP ASN, etc.)
!
object-group network <LNGName>
 description On-Premises network <LNGName> prefixes
 network-object 10.51.0.0 255.255.0.0
 network-object 10.52.0.0 255.255.0.0
exit
!
!     > Specify the access-list between the Azure VNet and your on-premises network.
!       This access list defines the IPsec SA traffic selectors.
!
access-list Azure-<VNetName>-acl extended permit ip object-group <LNGName> object-group Azure-<VNetName>
!
!     > No NAT required between the on-premises network and Azure VNet
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
!       - Make sure the policy number is not used
!       - integrity and prf must be the same
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
!       - This sample uses "Azure-<VNetName>-map" as the crypto map name
!       - ASA supports only one crypto map per interface, if you already have
!         an existing crypto map assigned to your outside interface, you must use
!         the same crypto map name, but with a different sequence number for
!         this policy
!       - "match address" policy uses the access-list "Azure-<VNetName>-acl" defined 
!         previously
!       - "ipsec-proposal" uses the proposal "AES-256" defined previously 
!       - PFS groups 14 and beyond requires ASA version 9.x.
!
crypto map Azure-<VNetName>-map 1 match address Azure-<VNetName>-acl
crypto map Azure-<VNetName>-map 1 set pfs group24
crypto map Azure-<VNetName>-map 1 set peer <Azure_Gateway_Public_IP>
crypto map Azure-<VNetName>-map 1 set ikev2 ipsec-proposal AES-256
crypto map Azure-<VNetName>-map 1 set security-association lifetime seconds 7200
crypto map Azure-<VNetName>-map interface outside
!
! ==> Set TCP MSS to 1350
!
sysopt connection tcpmss 1350
!
```

## <a name="simple-debugging-commands"></a><span data-ttu-id="a6f85-209">Commandes de débogage simples</span><span class="sxs-lookup"><span data-stu-id="a6f85-209">Simple debugging commands</span></span>

<span data-ttu-id="a6f85-210">Voici quelques commandes ASA de débogage :</span><span class="sxs-lookup"><span data-stu-id="a6f85-210">Here are some ASA commands for debugging purposes:</span></span>

1. <span data-ttu-id="a6f85-211">Afficher les associations de sécurité IPsec et IKE</span><span class="sxs-lookup"><span data-stu-id="a6f85-211">Show the IPsec and IKE SA's</span></span>
    - <span data-ttu-id="a6f85-212">« show crypto ipsec sa »</span><span class="sxs-lookup"><span data-stu-id="a6f85-212">"show crypto ipsec sa"</span></span>
    - <span data-ttu-id="a6f85-213">« show crypto ikev2 sa »</span><span class="sxs-lookup"><span data-stu-id="a6f85-213">"show crypto ikev2 sa"</span></span>
2. <span data-ttu-id="a6f85-214">Passer en mode de débogage - ce qui peut provoquer beaucoup de bruit au niveau de la console</span><span class="sxs-lookup"><span data-stu-id="a6f85-214">Entering debug mode - this can get very noisy on the console</span></span>
    - <span data-ttu-id="a6f85-215">« debug crypto ikev2 platform <level> »</span><span class="sxs-lookup"><span data-stu-id="a6f85-215">"debug crypto ikev2 platform <level>"</span></span>
    - <span data-ttu-id="a6f85-216">« debug crypto ikev2 protocol <level> »</span><span class="sxs-lookup"><span data-stu-id="a6f85-216">"debug crypto ikev2 protocol <level>"</span></span>
3. <span data-ttu-id="a6f85-217">Répertorier les configurations actuelles</span><span class="sxs-lookup"><span data-stu-id="a6f85-217">List current configurations</span></span>
    - <span data-ttu-id="a6f85-218">« show run » - Affiche les configurations actuelles sur l’appareil ; vous pouvez utiliser les diverses sous-commandes pour répertorier des parties spécifiques de la configuration.</span><span class="sxs-lookup"><span data-stu-id="a6f85-218">"show run" - shows the current configurations on the device; you can use the various sub-commands to list specific parts of the configuration.</span></span> <span data-ttu-id="a6f85-219">Par exemple, « show run crypto », « show run access-list », « show run tunnel-group », etc.</span><span class="sxs-lookup"><span data-stu-id="a6f85-219">E.g., "show run crypto", "show run access-list", "show run tunnel-group", etc.</span></span>


## <a name="next-steps"></a><span data-ttu-id="a6f85-220">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a6f85-220">Next steps</span></span>
<span data-ttu-id="a6f85-221">Pour connaître les étapes de configuration des connexions en mode actif-actif entre des réseaux locaux ou entre deux réseaux virtuels, consultez la page [Configuring Active-Active VPN Gateways for Cross-Premises and VNet-to-VNet Connections](vpn-gateway-activeactive-rm-powershell.md) (Configuration des passerelles VPN actif-actif pour des connexions entre des réseaux locaux et entre deux réseaux virtuels).</span><span class="sxs-lookup"><span data-stu-id="a6f85-221">See [Configuring Active-Active VPN Gateways for Cross-Premises and VNet-to-VNet Connections](vpn-gateway-activeactive-rm-powershell.md) for steps to configure active-active cross-premises and VNet-to-VNet connections.</span></span>

