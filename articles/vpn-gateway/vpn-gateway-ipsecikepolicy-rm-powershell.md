---
title: "Configurer la stratégie IPSec/IKE pour des connexions VPN S2S ou de réseau virtuel à réseau virtuel : Azure Resource Manager : PowerShell | Microsoft Docs"
description: "Cet article vous guide dans la configuration de stratégie IPSec/IKE pour des connexions VPN S2S ou de réseau virtuel à réseau virtuel avec des passerelles VPN Azure à l’aide d’Azure Resource Manager et de PowerShell."
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
ms.date: 05/12/2017
ms.author: yushwang
ms.openlocfilehash: f8d2e29276efdec7071f2aa0d463b1abd64a5253
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-ipsecike-policy-for-s2s-vpn-or-vnet-to-vnet-connections"></a><span data-ttu-id="00477-103">Configurer la stratégie IPsec/IKE pour des connexions VPN S2S ou de réseau virtuel à réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="00477-103">Configure IPsec/IKE policy for S2S VPN or VNet-to-VNet connections</span></span>

<span data-ttu-id="00477-104">Cet article vous guide tout au long des étapes de hello tooconfigure stratégie IPsec/IKE pour les connexions VPN de Site à Site ou au réseau à l’aide du modèle de déploiement du Gestionnaire de ressources hello et PowerShell.</span><span class="sxs-lookup"><span data-stu-id="00477-104">This article walks you through hello steps tooconfigure IPsec/IKE policy for Site-to-Site VPN or VNet-to-VNet connections using hello Resource Manager deployment model and PowerShell.</span></span>

## <span data-ttu-id="00477-105"><a name="about"></a>À propos des paramètres de stratégie IPsec et IKE pour les passerelles VPN Azure</span><span class="sxs-lookup"><span data-stu-id="00477-105"><a name="about"></a>About IPsec and IKE policy parameters for Azure VPN gateways</span></span>
<span data-ttu-id="00477-106">La norme de protocole IPsec et IKE standard prend en charge un vaste éventail d’algorithmes de chiffrement dans différentes combinaisons.</span><span class="sxs-lookup"><span data-stu-id="00477-106">IPsec and IKE protocol standard supports a wide range of cryptographic algorithms in various combinations.</span></span> <span data-ttu-id="00477-107">Consultez trop[sur les exigences de chiffrement et les passerelles VPN Azure](vpn-gateway-about-compliance-crypto.md) toosee comment cela peut aider à s’assurer qu’entre différents locaux et connectivité de réseau pour satisfaire vos exigences de conformité ou la sécurité.</span><span class="sxs-lookup"><span data-stu-id="00477-107">Refer too[About cryptographic requirements and Azure VPN gateways](vpn-gateway-about-compliance-crypto.md) toosee how this can help ensuring cross-premises and VNet-to-VNet connectivity satisfy your compliance or security requirements.</span></span>

<span data-ttu-id="00477-108">Cet article fournit des instructions toocreate et configurer une stratégie IPsec/IKE et appliquer la connexion existante ou nouvelle de tooa :</span><span class="sxs-lookup"><span data-stu-id="00477-108">This article provides instructions toocreate and configure an IPsec/IKE policy and apply tooa new or existing connection:</span></span>

* [<span data-ttu-id="00477-109">Partie 1 - toocreate de flux de travail et de définir la stratégie IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="00477-109">Part 1 - Workflow toocreate and set IPsec/IKE policy</span></span>](#workflow)
* [<span data-ttu-id="00477-110">Partie 2 : algorithmes de chiffrement pris en charge et avantages clés</span><span class="sxs-lookup"><span data-stu-id="00477-110">Part 2 - Supported cryptographic algorithms and key strengths</span></span>](#params)
* [<span data-ttu-id="00477-111">Partie 3 : création d’une connexion VPN S2S avec une stratégie IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="00477-111">Part 3 - Create a new S2S VPN connection with IPsec/IKE policy</span></span>](#crossprem)
* [<span data-ttu-id="00477-112">Partie 4 : création d’une connexion de réseau virtuel à réseau virtuel avec une stratégie IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="00477-112">Part 4 - Create a new VNet-to-VNet connection with IPsec/IKE policy</span></span>](#vnet2vnet)
* [<span data-ttu-id="00477-113">Partie 5 : gestion (créer, ajouter, supprimer) de la stratégie IPsec/IKE pour une connexion</span><span class="sxs-lookup"><span data-stu-id="00477-113">Part 5 - Manage (create, add, remove) IPsec/IKE policy for a connection</span></span>](#managepolicy)

> [!IMPORTANT]
> 1. <span data-ttu-id="00477-114">Notez que les stratégies IPsec/IKE ne fonctionnement que sur hello suivant SKU de passerelle :</span><span class="sxs-lookup"><span data-stu-id="00477-114">Note that IPsec/IKE policy only works on hello following gateway SKUs:</span></span>
>    * <span data-ttu-id="00477-115">***VpnGw1, VpnGw2, VpnGw3*** (basée sur le routage)</span><span class="sxs-lookup"><span data-stu-id="00477-115">***VpnGw1, VpnGw2, VpnGw3*** (route-based)</span></span>
>    * <span data-ttu-id="00477-116">***Standard*** et ***HighPerformance*** (basée sur le routage)</span><span class="sxs-lookup"><span data-stu-id="00477-116">***Standard*** and ***HighPerformance*** (route-based)</span></span>
> 2. <span data-ttu-id="00477-117">Vous pouvez uniquement spécifier ***une*** combinaison de stratégie pour une connexion donnée.</span><span class="sxs-lookup"><span data-stu-id="00477-117">You can only specify ***one*** policy combination for a given connection.</span></span>
> 3. <span data-ttu-id="00477-118">Vous devez spécifier tous les algorithmes et paramètres pour IKE (mode principal) et IPsec (mode rapide).</span><span class="sxs-lookup"><span data-stu-id="00477-118">You must specify all algorithms and parameters for both IKE (Main Mode) and IPsec (Quick Mode).</span></span> <span data-ttu-id="00477-119">Vous n’êtes pas en droit de spécifier de stratégie partielle.</span><span class="sxs-lookup"><span data-stu-id="00477-119">Partial policy specification is not allowed.</span></span>
> 4. <span data-ttu-id="00477-120">Consultez vos spécifications de fournisseur de périphérique VPN stratégie de hello tooensure est pris en charge sur les appareils de votre VPN sur site.</span><span class="sxs-lookup"><span data-stu-id="00477-120">Consult with your VPN device vendor specifications tooensure hello policy is supported on your on-premises VPN devices.</span></span> <span data-ttu-id="00477-121">S2S ou des connexions de réseau virtuel à réseau virtuel ne peut pas établir si les stratégies hello ne sont pas compatibles.</span><span class="sxs-lookup"><span data-stu-id="00477-121">S2S or VNet-to-VNet connections cannot establish if hello policies are incompatible.</span></span>

## <span data-ttu-id="00477-122"><a name ="workflow"></a>Partie 1 - toocreate de flux de travail et de définir la stratégie IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="00477-122"><a name ="workflow"></a>Part 1 - Workflow toocreate and set IPsec/IKE policy</span></span>
<span data-ttu-id="00477-123">Cette section souligne hello toocreate et mise à jour IPsec/IKE stratégie de workflow sur une connexion VPN de S2S ou de réseau virtuel à réseau virtuel :</span><span class="sxs-lookup"><span data-stu-id="00477-123">This section outlines hello workflow toocreate and update IPsec/IKE policy on a S2S VPN or VNet-to-VNet connection:</span></span>
1. <span data-ttu-id="00477-124">créer un réseau virtuel et une passerelle VPN ;</span><span class="sxs-lookup"><span data-stu-id="00477-124">Create a virtual network and a VPN gateway</span></span>
2. <span data-ttu-id="00477-125">créer une passerelle de réseau local pour une connexion entre sites locaux, ou un autre réseau virtuel et une passerelle pour une connexion de réseau virtuel à réseau virtuel ;</span><span class="sxs-lookup"><span data-stu-id="00477-125">Create a local network gateway for cross premises connection, or another virtual network and gateway for VNet-to-VNet connection</span></span>
3. <span data-ttu-id="00477-126">créer une stratégie IPsec/IKE avec des algorithmes et paramètres sélectionnés ;</span><span class="sxs-lookup"><span data-stu-id="00477-126">Create an IPsec/IKE policy with selected algorithms and parameters</span></span>
4. <span data-ttu-id="00477-127">Créer une connexion (IPsec ou VNet2VNet) avec la stratégie IPsec/IKE de hello</span><span class="sxs-lookup"><span data-stu-id="00477-127">Create a connection (IPsec or VNet2VNet) with hello IPsec/IKE policy</span></span>
5. <span data-ttu-id="00477-128">ajouter/mettre à jour/supprimer une stratégie IPsec/IKE pour une connexion existante.</span><span class="sxs-lookup"><span data-stu-id="00477-128">Add/update/remove an IPsec/IKE policy for an existing connection</span></span>

<span data-ttu-id="00477-129">instructions Hello dans cet article vous aide à installer et configurer des stratégies IPsec/IKE comme indiqué dans le diagramme de hello :</span><span class="sxs-lookup"><span data-stu-id="00477-129">hello instructions in this article helps you set up and configure IPsec/IKE policies as shown in hello diagram:</span></span>

![stratégie IPSec/IKE](./media/vpn-gateway-ipsecikepolicy-rm-powershell/ipsecikepolicy.png)

## <span data-ttu-id="00477-131"><a name ="params"></a>Partie 2 : algorithmes de chiffrement pris en charge et avantages clés</span><span class="sxs-lookup"><span data-stu-id="00477-131"><a name ="params"></a>Part 2 - Supported cryptographic algorithms & key strengths</span></span>

<span data-ttu-id="00477-132">Hello tableau suivant répertorie les algorithmes de chiffrement pris en charge de hello et atouts configurables par les clients de hello :</span><span class="sxs-lookup"><span data-stu-id="00477-132">hello following table lists hello supported cryptographic algorithms and key strengths configurable by hello customers:</span></span>

| <span data-ttu-id="00477-133">**IPsec/IKEv2**</span><span class="sxs-lookup"><span data-stu-id="00477-133">**IPsec/IKEv2**</span></span>  | <span data-ttu-id="00477-134">**Options**</span><span class="sxs-lookup"><span data-stu-id="00477-134">**Options**</span></span>    |
| ---  | --- 
| <span data-ttu-id="00477-135">Chiffrement IKEv2</span><span class="sxs-lookup"><span data-stu-id="00477-135">IKEv2 Encryption</span></span> | <span data-ttu-id="00477-136">AES256, AES192, AES128, DES3, DES</span><span class="sxs-lookup"><span data-stu-id="00477-136">AES256, AES192, AES128, DES3, DES</span></span>  
| <span data-ttu-id="00477-137">Intégrité IKEv2</span><span class="sxs-lookup"><span data-stu-id="00477-137">IKEv2 Integrity</span></span>  | <span data-ttu-id="00477-138">SHA384, SHA256, SHA1, MD5</span><span class="sxs-lookup"><span data-stu-id="00477-138">SHA384, SHA256, SHA1, MD5</span></span>  |
| <span data-ttu-id="00477-139">Groupe DH</span><span class="sxs-lookup"><span data-stu-id="00477-139">DH Group</span></span>         | <span data-ttu-id="00477-140">DHGroup24, ECP384, ECP256, DHGroup14, DHGroup2048, DHGroup2, DHGroup1, Aucun</span><span class="sxs-lookup"><span data-stu-id="00477-140">DHGroup24, ECP384, ECP256, DHGroup14, DHGroup2048, DHGroup2, DHGroup1, None</span></span> |
| <span data-ttu-id="00477-141">Chiffrement IPsec</span><span class="sxs-lookup"><span data-stu-id="00477-141">IPsec Encryption</span></span> | <span data-ttu-id="00477-142">GCMAES256, GCMAES192, GCMAES128, AES256, AES192, AES128, DES3, DES, Aucun</span><span class="sxs-lookup"><span data-stu-id="00477-142">GCMAES256, GCMAES192, GCMAES128, AES256, AES192, AES128, DES3, DES, None</span></span>    |
| <span data-ttu-id="00477-143">Intégrité IPsec</span><span class="sxs-lookup"><span data-stu-id="00477-143">IPsec Integrity</span></span>  | <span data-ttu-id="00477-144">GCMASE256, GCMAES192, GCMAES128, SHA256, SHA1, MD5</span><span class="sxs-lookup"><span data-stu-id="00477-144">GCMASE256, GCMAES192, GCMAES128, SHA256, SHA1, MD5</span></span> |
| <span data-ttu-id="00477-145">Groupe PFS</span><span class="sxs-lookup"><span data-stu-id="00477-145">PFS Group</span></span>        | <span data-ttu-id="00477-146">PFS24, ECP384, ECP256, PFS2048, PFS2, PFS1, Aucun</span><span class="sxs-lookup"><span data-stu-id="00477-146">PFS24, ECP384, ECP256, PFS2048, PFS2, PFS1, None</span></span> 
| <span data-ttu-id="00477-147">Durée de vie de l’AS en mode rapide</span><span class="sxs-lookup"><span data-stu-id="00477-147">QM SA Lifetime</span></span>   | <span data-ttu-id="00477-148">(**Facultatif** : les valeurs par défaut sont utilisées si aucun valeur n’est indiquée)</span><span class="sxs-lookup"><span data-stu-id="00477-148">(**Optional**: default values are used if not specified)</span></span><br><span data-ttu-id="00477-149">Secondes (entier ; **min 300**  /par défaut 27 000 secondes)</span><span class="sxs-lookup"><span data-stu-id="00477-149">Seconds (integer; **min. 300**/default 27000 seconds)</span></span><br><span data-ttu-id="00477-150">Kilo-octets (entier ; **min 1 024**  /par défaut 102 400 000 Ko)</span><span class="sxs-lookup"><span data-stu-id="00477-150">KBytes (integer; **min. 1024**/default 102400000 KBytes)</span></span>   |
| <span data-ttu-id="00477-151">Sélecteur de trafic</span><span class="sxs-lookup"><span data-stu-id="00477-151">Traffic Selector</span></span> | <span data-ttu-id="00477-152">UsePolicyBasedTrafficSelectors** ($True/$False ; **facultatif**, $False par défaut si aucune valeur n’est indiquée)</span><span class="sxs-lookup"><span data-stu-id="00477-152">UsePolicyBasedTrafficSelectors** ($True/$False; **Optional**, default $False if not specified)</span></span>    |
|  |  |

> [!IMPORTANT]
> 1. <span data-ttu-id="00477-153">**Si GCMAES est utilisé pour l’algorithme de chiffrement d’IPsec, vous devez sélectionner hello même algorithme GCMAES et la longueur de clé pour l’intégrité IPsec ; par exemple, à l’aide de GCMAES128 pour les deux**</span><span class="sxs-lookup"><span data-stu-id="00477-153">**If GCMAES is used as for IPsec Encryption algorithm, you must select hello same GCMAES algorithm and key length for IPsec Integrity; for example, using GCMAES128 for both**</span></span>
> 2. <span data-ttu-id="00477-154">Durée de vie de SA de Mode principal IKEv2 est fixée à 28 800 secondes sur les passerelles VPN Azure hello</span><span class="sxs-lookup"><span data-stu-id="00477-154">IKEv2 Main Mode SA lifetime is fixed at 28,800 seconds on hello Azure VPN gateways</span></span>
> 3. <span data-ttu-id="00477-155">Définition de « UsePolicyBasedTrafficSelectors » trop$ True sur une connexion configurera hello VPN Azure passerelle tooconnect toopolicy pare-feu basé sur VPN sur site.</span><span class="sxs-lookup"><span data-stu-id="00477-155">Setting "UsePolicyBasedTrafficSelectors" too$True on a connection will configure hello Azure VPN gateway tooconnect toopolicy-based VPN firewall on premises.</span></span> <span data-ttu-id="00477-156">Si vous activez PolicyBasedTrafficSelectors, vous devez tooensure que votre périphérique VPN a défini toutes les combinaisons de vos préfixes de (passerelle de réseau local) de réseau local à partir de préfixes de réseau virtuel Azure hello, les sélecteurs le trafic correspondant hello au lieu de tout.</span><span class="sxs-lookup"><span data-stu-id="00477-156">If you enable PolicyBasedTrafficSelectors, you need tooensure your VPN device has hello matching traffic selectors defined with all combinations of your on-premises network (local network gateway) prefixes to/from hello Azure virtual network prefixes, instead of any-to-any.</span></span> <span data-ttu-id="00477-157">Par exemple, si les préfixes de votre réseau local sont 10.1.0.0/16 et 10.2.0.0/16, et les préfixes de votre réseau virtuel sont 192.168.0.0/16 et 172.16.0.0/16, vous devez hello toospecify suivant des sélecteurs de trafic :</span><span class="sxs-lookup"><span data-stu-id="00477-157">For example, if your on-premises network prefixes are 10.1.0.0/16 and 10.2.0.0/16, and your virtual network prefixes are 192.168.0.0/16 and 172.16.0.0/16, you need toospecify hello following traffic selectors:</span></span>
>    * <span data-ttu-id="00477-158">10.1.0.0/16 <====> 192.168.0.0/16</span><span class="sxs-lookup"><span data-stu-id="00477-158">10.1.0.0/16 <====> 192.168.0.0/16</span></span>
>    * <span data-ttu-id="00477-159">10.1.0.0/16 <====> 172.16.0.0/16</span><span class="sxs-lookup"><span data-stu-id="00477-159">10.1.0.0/16 <====> 172.16.0.0/16</span></span>
>    * <span data-ttu-id="00477-160">10.2.0.0/16 <====> 192.168.0.0/16</span><span class="sxs-lookup"><span data-stu-id="00477-160">10.2.0.0/16 <====> 192.168.0.0/16</span></span>
>    * <span data-ttu-id="00477-161">10.2.0.0/16 <====> 172.16.0.0/16</span><span class="sxs-lookup"><span data-stu-id="00477-161">10.2.0.0/16 <====> 172.16.0.0/16</span></span>

<span data-ttu-id="00477-162">Pour plus d’informations sur les sélecteurs de trafic basés sur une stratégie, voir [Connecter plusieurs périphériques VPN basés sur une stratégie locale](vpn-gateway-connect-multiple-policybased-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="00477-162">For more information regarding policy-based traffic selectors, see [Connect multiple on-premises policy-based VPN devices](vpn-gateway-connect-multiple-policybased-rm-ps.md).</span></span>

<span data-ttu-id="00477-163">Hello tableau ci-dessous répertorie hello groupes Diffie-Hellman correspondants pris en charge par la stratégie personnalisée de hello :</span><span class="sxs-lookup"><span data-stu-id="00477-163">hello following table lists hello corresponding Diffie-Hellman Groups supported by hello custom policy:</span></span>

| <span data-ttu-id="00477-164">**Groupe Diffie-Hellman**</span><span class="sxs-lookup"><span data-stu-id="00477-164">**Diffie-Hellman Group**</span></span>  | <span data-ttu-id="00477-165">**DHGroup**</span><span class="sxs-lookup"><span data-stu-id="00477-165">**DHGroup**</span></span>              | <span data-ttu-id="00477-166">**PFSGroup**</span><span class="sxs-lookup"><span data-stu-id="00477-166">**PFSGroup**</span></span> | <span data-ttu-id="00477-167">**Longueur de clé**</span><span class="sxs-lookup"><span data-stu-id="00477-167">**Key length**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="00477-168">1</span><span class="sxs-lookup"><span data-stu-id="00477-168">1</span></span>                         | <span data-ttu-id="00477-169">DHGroup1</span><span class="sxs-lookup"><span data-stu-id="00477-169">DHGroup1</span></span>                 | <span data-ttu-id="00477-170">PFS1</span><span class="sxs-lookup"><span data-stu-id="00477-170">PFS1</span></span>         | <span data-ttu-id="00477-171">MODP 768 bits</span><span class="sxs-lookup"><span data-stu-id="00477-171">768-bit MODP</span></span>   |
| <span data-ttu-id="00477-172">2</span><span class="sxs-lookup"><span data-stu-id="00477-172">2</span></span>                         | <span data-ttu-id="00477-173">DHGroup2</span><span class="sxs-lookup"><span data-stu-id="00477-173">DHGroup2</span></span>                 | <span data-ttu-id="00477-174">PFS2</span><span class="sxs-lookup"><span data-stu-id="00477-174">PFS2</span></span>         | <span data-ttu-id="00477-175">MODP 1 024 bits</span><span class="sxs-lookup"><span data-stu-id="00477-175">1024-bit MODP</span></span>  |
| <span data-ttu-id="00477-176">14</span><span class="sxs-lookup"><span data-stu-id="00477-176">14</span></span>                        | <span data-ttu-id="00477-177">DHGroup14</span><span class="sxs-lookup"><span data-stu-id="00477-177">DHGroup14</span></span><br><span data-ttu-id="00477-178">DHGroup2048</span><span class="sxs-lookup"><span data-stu-id="00477-178">DHGroup2048</span></span> | <span data-ttu-id="00477-179">PFS2048</span><span class="sxs-lookup"><span data-stu-id="00477-179">PFS2048</span></span>      | <span data-ttu-id="00477-180">MODP 2 048 bits</span><span class="sxs-lookup"><span data-stu-id="00477-180">2048-bit MODP</span></span>  |
| <span data-ttu-id="00477-181">19</span><span class="sxs-lookup"><span data-stu-id="00477-181">19</span></span>                        | <span data-ttu-id="00477-182">ECP256</span><span class="sxs-lookup"><span data-stu-id="00477-182">ECP256</span></span>                   | <span data-ttu-id="00477-183">ECP256</span><span class="sxs-lookup"><span data-stu-id="00477-183">ECP256</span></span>       | <span data-ttu-id="00477-184">ECP 256 bits</span><span class="sxs-lookup"><span data-stu-id="00477-184">256-bit ECP</span></span>    |
| <span data-ttu-id="00477-185">20</span><span class="sxs-lookup"><span data-stu-id="00477-185">20</span></span>                        | <span data-ttu-id="00477-186">ECP384</span><span class="sxs-lookup"><span data-stu-id="00477-186">ECP384</span></span>                   | <span data-ttu-id="00477-187">ECP284</span><span class="sxs-lookup"><span data-stu-id="00477-187">ECP284</span></span>       | <span data-ttu-id="00477-188">ECP 384 bits</span><span class="sxs-lookup"><span data-stu-id="00477-188">384-bit ECP</span></span>    |
| <span data-ttu-id="00477-189">24</span><span class="sxs-lookup"><span data-stu-id="00477-189">24</span></span>                        | <span data-ttu-id="00477-190">DHGroup24</span><span class="sxs-lookup"><span data-stu-id="00477-190">DHGroup24</span></span>                | <span data-ttu-id="00477-191">PFS24</span><span class="sxs-lookup"><span data-stu-id="00477-191">PFS24</span></span>        | <span data-ttu-id="00477-192">MODP 2 048 bits</span><span class="sxs-lookup"><span data-stu-id="00477-192">2048-bit MODP</span></span>  |

<span data-ttu-id="00477-193">Consultez trop[RFC3526](https://tools.ietf.org/html/rfc3526) et [RFC5114](https://tools.ietf.org/html/rfc5114) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="00477-193">Refer too[RFC3526](https://tools.ietf.org/html/rfc3526) and [RFC5114](https://tools.ietf.org/html/rfc5114) for more details.</span></span>

## <span data-ttu-id="00477-194"><a name ="crossprem"></a>Partie 3 : création d’une connexion VPN S2S avec une stratégie IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="00477-194"><a name ="crossprem"></a>Part 3 - Create a new S2S VPN connection with IPsec/IKE policy</span></span>

<span data-ttu-id="00477-195">Cette section vous guide tout au long des étapes de création d’une connexion VPN de S2S avec une stratégie IPsec/IKE de hello.</span><span class="sxs-lookup"><span data-stu-id="00477-195">This section walks you through hello steps of creating a S2S VPN connection with an IPsec/IKE policy.</span></span> <span data-ttu-id="00477-196">Hello suit crée hello connexion comme indiqué dans le diagramme de hello :</span><span class="sxs-lookup"><span data-stu-id="00477-196">hello following steps create hello connection as shown in hello diagram:</span></span>

![stratégie S2S](./media/vpn-gateway-ipsecikepolicy-rm-powershell/s2spolicy.png)

<span data-ttu-id="00477-198">Pour des instructions détaillées concernant la création d’une connexion VPN S2S, voir [Créer une connexion VPN S2S](vpn-gateway-create-site-to-site-rm-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="00477-198">See [Create a S2S VPN connection](vpn-gateway-create-site-to-site-rm-powershell.md) for more detailed step-by-step instructions for creating a S2S VPN connection.</span></span>

### <span data-ttu-id="00477-199"><a name="before"></a>Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="00477-199"><a name="before"></a>Before you begin</span></span>

* <span data-ttu-id="00477-200">Assurez-vous de disposer d’un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="00477-200">Verify that you have an Azure subscription.</span></span> <span data-ttu-id="00477-201">Si vous ne disposez pas déjà d’un abonnement Azure, vous pouvez activer vos [avantages abonnés MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ou créer un [compte gratuit](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="00477-201">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="00477-202">Installer les applets de commande Azure Resource Manager PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="00477-202">Install hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="00477-203">Consultez [vue d’ensemble de Azure PowerShell](/powershell/azure/overview) pour plus d’informations sur l’installation des applets de commande PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="00477-203">See [Overview of Azure PowerShell](/powershell/azure/overview) for more information about installing hello PowerShell cmdlets.</span></span>

### <span data-ttu-id="00477-204"><a name="createvnet1"></a>Étape 1 : créer le réseau virtuel de hello, passerelle VPN et passerelle de réseau local</span><span class="sxs-lookup"><span data-stu-id="00477-204"><a name="createvnet1"></a>Step 1 - Create hello virtual network, VPN gateway, and local network gateway</span></span>

#### <a name="1-declare-your-variables"></a><span data-ttu-id="00477-205">1. Déclarer vos variables</span><span class="sxs-lookup"><span data-stu-id="00477-205">1. Declare your variables</span></span>

<span data-ttu-id="00477-206">Dans cet exercice, nous allons commencer par déclarer les variables.</span><span class="sxs-lookup"><span data-stu-id="00477-206">For this exercise, we start by declaring our variables.</span></span> <span data-ttu-id="00477-207">Être des valeurs de hello tooreplace que par les vôtres lors de la configuration pour la production.</span><span class="sxs-lookup"><span data-stu-id="00477-207">Be sure tooreplace hello values with your own when configuring for production.</span></span>

```powershell
$Sub1          = "<YourSubscriptionName>"
$RG1           = "TestPolicyRG1"
$Location1     = "East US 2"
$VNetName1     = "TestVNet1"
$FESubName1    = "FrontEnd"
$BESubName1    = "Backend"
$GWSubName1    = "GatewaySubnet"
$VNetPrefix11  = "10.11.0.0/16"
$VNetPrefix12  = "10.12.0.0/16"
$FESubPrefix1  = "10.11.0.0/24"
$BESubPrefix1  = "10.12.0.0/24"
$GWSubPrefix1  = "10.12.255.0/27"
$DNS1          = "8.8.8.8"
$GWName1       = "VNet1GW"
$GW1IPName1    = "VNet1GWIP1"
$GW1IPconf1    = "gw1ipconf1"
$Connection16  = "VNet1toSite6"

$LNGName6      = "Site6"
$LNGPrefix61   = "10.61.0.0/16"
$LNGPrefix62   = "10.62.0.0/16"
$LNGIP6        = "131.107.72.22"
```

#### <a name="2-connect-tooyour-subscription-and-create-a-new-resource-group"></a><span data-ttu-id="00477-208">2. Se connecter tooyour abonnement et créer un nouveau groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="00477-208">2. Connect tooyour subscription and create a new resource group</span></span>

<span data-ttu-id="00477-209">Veillez à que basculer hello de toouse mode tooPowerShell applets de commande Gestionnaire de ressources.</span><span class="sxs-lookup"><span data-stu-id="00477-209">Make sure you switch tooPowerShell mode toouse hello Resource Manager cmdlets.</span></span> <span data-ttu-id="00477-210">Pour plus d’informations, consultez la page [Utilisation de Windows PowerShell avec Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="00477-210">For more information, see [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="00477-211">Ouvrez la console PowerShell et tooyour compte de connexion.</span><span class="sxs-lookup"><span data-stu-id="00477-211">Open your PowerShell console and connect tooyour account.</span></span> <span data-ttu-id="00477-212">Utilisez hello suivant toohelp exemple que vous connectez :</span><span class="sxs-lookup"><span data-stu-id="00477-212">Use hello following sample toohelp you connect:</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="3-create-hello-virtual-network-vpn-gateway-and-local-network-gateway"></a><span data-ttu-id="00477-213">3. Créer le réseau virtuel de hello, passerelle VPN et passerelle de réseau local</span><span class="sxs-lookup"><span data-stu-id="00477-213">3. Create hello virtual network, VPN gateway, and local network gateway</span></span>

<span data-ttu-id="00477-214">Hello suivant l’exemple crée un réseau virtuel hello, TestVNet1, avec trois sous-réseaux et de passerelle VPN de hello.</span><span class="sxs-lookup"><span data-stu-id="00477-214">hello following sample creates hello virtual network, TestVNet1, with three subnets, and hello VPN gateway.</span></span> <span data-ttu-id="00477-215">Lorsque vous remplacez les valeurs, pensez à toujours nommer votre sous-réseau de passerelle « GatewaySubnet ».</span><span class="sxs-lookup"><span data-stu-id="00477-215">When substituting values, it's important that you always name your gateway subnet specifically GatewaySubnet.</span></span> <span data-ttu-id="00477-216">Si vous le nommez autrement, la création de votre passerelle échoue.</span><span class="sxs-lookup"><span data-stu-id="00477-216">If you name it something else, your gateway creation fails.</span></span>

```powershell
$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1
$besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1

$gw1pip1    = New-AzureRmPublicIpAddress -Name $GW1IPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic
$vnet1      = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1    = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gw1ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW1IPconf1 -Subnet $subnet1 -PublicIpAddress $gw1pip1

New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gw1ipconf1 -GatewayType Vpn -VpnType RouteBased -GatewaySku HighPerformance

New-AzureRmLocalNetworkGateway -Name $LNGName6 -ResourceGroupName $RG1 -Location $Location1 -GatewayIpAddress $LNGIP6 -AddressPrefix $LNGPrefix61,$LNGPrefix62
```

### <span data-ttu-id="00477-217"><a name="s2sconnection"></a>Étape 2 : création d’une connexion VPN S2S avec une stratégie IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="00477-217"><a name="s2sconnection"></a>Step 2 - Create a S2S VPN connection with an IPsec/IKE policy</span></span>

#### <a name="1-create-an-ipsecike-policy"></a><span data-ttu-id="00477-218">1. Créez une stratégie IPsec/IKE.</span><span class="sxs-lookup"><span data-stu-id="00477-218">1. Create an IPsec/IKE policy</span></span>

<span data-ttu-id="00477-219">Hello script de l’exemple suivant crée une stratégie IPsec/IKE avec hello suite d’algorithmes et paramètres :</span><span class="sxs-lookup"><span data-stu-id="00477-219">hello following sample script creates an IPsec/IKE policy with hello following algorithms and parameters:</span></span>

* <span data-ttu-id="00477-220">IKEv2: AES256, SHA384, DHGroup24</span><span class="sxs-lookup"><span data-stu-id="00477-220">IKEv2: AES256, SHA384, DHGroup24</span></span>
* <span data-ttu-id="00477-221">IPsec: AES256, SHA256, PFS24, SA Lifetime 7200 seconds & 2048KB</span><span class="sxs-lookup"><span data-stu-id="00477-221">IPsec: AES256, SHA256, PFS24, SA Lifetime 7200 seconds & 2048KB</span></span>

```powershell
$ipsecpolicy6 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption AES256 -IpsecIntegrity SHA256 -PfsGroup PFS24 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 2048
```

<span data-ttu-id="00477-222">Si vous utilisez GCMAES pour IPsec, vous devez utiliser hello le même algorithme GCMAES et la longueur de clé de chiffrement de sécurité IPsec et l’intégrité, par exemple :</span><span class="sxs-lookup"><span data-stu-id="00477-222">If you use GCMAES for IPsec, you must use hello same GCMAES algorithm and key length for both IPsec encryption and integrity, for example:</span></span>

* <span data-ttu-id="00477-223">IKEv2: AES256, SHA384, DHGroup24</span><span class="sxs-lookup"><span data-stu-id="00477-223">IKEv2: AES256, SHA384, DHGroup24</span></span>
* <span data-ttu-id="00477-224">IPsec: **GCMAES256, GCMAES256**, PFS24, SA Lifetime 7200 seconds & 2048KB</span><span class="sxs-lookup"><span data-stu-id="00477-224">IPsec: **GCMAES256, GCMAES256**, PFS24, SA Lifetime 7200 seconds & 2048KB</span></span>

```powershell
$ipsecpolicy6 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption GCMAES256 -IpsecIntegrity GCMAES256 -PfsGroup PFS24 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 2048
```

#### <a name="2-create-hello-s2s-vpn-connection-with-hello-ipsecike-policy"></a><span data-ttu-id="00477-225">2. Créer un réseau VPN S2S hello avec hello stratégie IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="00477-225">2. Create hello S2S VPN connection with hello IPsec/IKE policy</span></span>

<span data-ttu-id="00477-226">Créer un réseau VPN S2S et appliquer la stratégie IPsec/IKE de hello créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="00477-226">Create an S2S VPN connection and apply hello IPsec/IKE policy created earlier.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng6 = Get-AzureRmLocalNetworkGateway  -Name $LNGName6 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng6 -Location $Location1 -ConnectionType IPsec -IpsecPolicies $ipsecpolicy6 -SharedKey 'AzureA1b2C3'
```

<span data-ttu-id="00477-227">Vous pouvez éventuellement ajouter «-UsePolicyBasedTrafficSelectors $True » toohello créer connexion applet de commande tooenable VPN Azure passerelle tooconnect toopolicy VPN périphériques basés sur local, comme décrit ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="00477-227">You can optionally add "-UsePolicyBasedTrafficSelectors $True" toohello create connection cmdlet tooenable Azure VPN gateway tooconnect toopolicy-based VPN devices on premises, as described above.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="00477-228">Une fois qu’une stratégie IPsec/IKE est spécifiée sur une connexion, passerelle VPN Azure de hello sera uniquement envoyer ou accepter hello IPsec/IKE avec les algorithmes de chiffrement spécifiés et des avantages clés sur cette connexion particulière.</span><span class="sxs-lookup"><span data-stu-id="00477-228">Once an IPsec/IKE policy is specified on a connection, hello Azure VPN gateway will only send or accept hello IPsec/IKE proposal with specified cryptographic algorithms and key strengths on that particular connection.</span></span> <span data-ttu-id="00477-229">Assurez-vous que votre appareil VPN locaux pour la connexion de hello utilise ou accepte une combinaison de stratégie exacte hello, sinon tunnel de VPN de S2S hello établira pas.</span><span class="sxs-lookup"><span data-stu-id="00477-229">Make sure your on-premises VPN device for hello connection uses or accepts hello exact policy combination, otherwise hello S2S VPN tunnel will not establish.</span></span>


## <span data-ttu-id="00477-230"><a name ="vnet2vnet"></a>Partie 4 : création d’une connexion de réseau virtuel à réseau virtuel avec une stratégie IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="00477-230"><a name ="vnet2vnet"></a>Part 4 - Create a new VNet-to-VNet connection with IPsec/IKE policy</span></span>

<span data-ttu-id="00477-231">étapes de Hello de création d’une connexion au réseau avec une stratégie IPsec/IKE sont similaires toothat d’une connexion VPN de S2S.</span><span class="sxs-lookup"><span data-stu-id="00477-231">hello steps of creating a VNet-to-VNet connection with an IPsec/IKE policy are similar toothat of a S2S VPN connection.</span></span> <span data-ttu-id="00477-232">Hello exemples de scripts suivants créent hello connexion comme indiqué dans le diagramme de hello :</span><span class="sxs-lookup"><span data-stu-id="00477-232">hello following sample scripts create hello connection as shown in hello diagram:</span></span>

![Stratégie de réseau virtuel à réseau virtuel](./media/vpn-gateway-ipsecikepolicy-rm-powershell/v2vpolicy.png)

<span data-ttu-id="00477-234">Pour plus d’informations sur les étapes de création d’une connexion de réseau virtuel à réseau virtuel, voir [Créer une connexion de réseau virtuel à réseau virtuel](vpn-gateway-vnet-vnet-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="00477-234">See [Create a VNet-to-VNet connection](vpn-gateway-vnet-vnet-rm-ps.md) for more detailed steps for creating a VNet-to-VNet connection.</span></span> <span data-ttu-id="00477-235">Vous devez effectuer [partie 3](#crossprem) toocreate hello passerelle VPN et configurer TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="00477-235">You must complete [Part 3](#crossprem) toocreate and configure TestVNet1 and hello VPN Gateway.</span></span>

### <span data-ttu-id="00477-236"><a name="createvnet2"></a>Étape 1 : créer le réseau virtuel deuxième de hello et passerelle VPN</span><span class="sxs-lookup"><span data-stu-id="00477-236"><a name="createvnet2"></a>Step 1 - Create hello second virtual network and VPN gateway</span></span>

#### <a name="1-declare-your-variables"></a><span data-ttu-id="00477-237">1. Déclarer vos variables</span><span class="sxs-lookup"><span data-stu-id="00477-237">1. Declare your variables</span></span>

<span data-ttu-id="00477-238">Être tooreplace que les valeurs hello avec hello ceux que vous souhaitez toouse pour votre configuration.</span><span class="sxs-lookup"><span data-stu-id="00477-238">Be sure tooreplace hello values with hello ones that you want toouse for your configuration.</span></span>

```powershell
$RG2          = "TestPolicyRG2"
$Location2    = "East US 2"
$VNetName2    = "TestVNet2"
$FESubName2   = "FrontEnd"
$BESubName2   = "Backend"
$GWSubName2   = "GatewaySubnet"
$VNetPrefix21 = "10.21.0.0/16"
$VNetPrefix22 = "10.22.0.0/16"
$FESubPrefix2 = "10.21.0.0/24"
$BESubPrefix2 = "10.22.0.0/24"
$GWSubPrefix2 = "10.22.255.0/27"
$DNS2         = "8.8.8.8"
$GWName2      = "VNet2GW"
$GW2IPName1   = "VNet2GWIP1"
$GW2IPconf1   = "gw2ipconf1"
$Connection21 = "VNet2toVNet1"
$Connection12 = "VNet1toVNet2"
```

#### <a name="2-create-hello-second-virtual-network-and-vpn-gateway-in-hello-new-resource-group"></a><span data-ttu-id="00477-239">2. Créer des réseaux deuxième hello et passerelle VPN dans le nouveau groupe de ressources hello</span><span class="sxs-lookup"><span data-stu-id="00477-239">2. Create hello second virtual network and VPN gateway in hello new resource group</span></span>

```powershell
New-AzureRmResourceGroup -Name $RG2 -Location $Location2

$fesub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName2 -AddressPrefix $FESubPrefix2
$besub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName2 -AddressPrefix $BESubPrefix2
$gwsub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName2 -AddressPrefix $GWSubPrefix2

New-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2 -Location $Location2 -AddressPrefix $VNetPrefix21,$VNetPrefix22 -Subnet $fesub2,$besub2,$gwsub2

$gw2pip1    = New-AzureRmPublicIpAddress -Name $GW2IPName1 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic
$vnet2      = Get-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2
$subnet2    = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet2
$gw2ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW2IPconf1 -Subnet $subnet2 -PublicIpAddress $gw2pip1

New-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2 -Location $Location2 -IpConfigurations $gw2ipconf1 -GatewayType Vpn -VpnType RouteBased -GatewaySku HighPerformance
```

### <a name="step-2---create-a-vnet-tovnet-connection-with-hello-ipsecike-policy"></a><span data-ttu-id="00477-240">Étape 2 : créer une connexion de réseau virtuel-toVNet avec hello stratégie IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="00477-240">Step 2 - Create a VNet-toVNet connection with hello IPsec/IKE policy</span></span>

<span data-ttu-id="00477-241">Toohello similaire réseau VPN S2S, créer une stratégie IPsec/IKE, puis appliquer les toopolicy toohello nouvelle connexion.</span><span class="sxs-lookup"><span data-stu-id="00477-241">Similar toohello S2S VPN connection, create an IPsec/IKE policy then apply toopolicy toohello new connection.</span></span>

#### <a name="1-create-an-ipsecike-policy"></a><span data-ttu-id="00477-242">1. Créez une stratégie IPsec/IKE.</span><span class="sxs-lookup"><span data-stu-id="00477-242">1. Create an IPsec/IKE policy</span></span>

<span data-ttu-id="00477-243">Hello script de l’exemple suivant crée une autre stratégie IPsec/IKE avec hello suite d’algorithmes et paramètres :</span><span class="sxs-lookup"><span data-stu-id="00477-243">hello following sample script creates a different IPsec/IKE policy with hello following algorithms and parameters:</span></span>
* <span data-ttu-id="00477-244">IKEv2: AES128, SHA1, DHGroup14</span><span class="sxs-lookup"><span data-stu-id="00477-244">IKEv2: AES128, SHA1, DHGroup14</span></span>
* <span data-ttu-id="00477-245">IPsec: GCMAES128, GCMAES128, PFS14, SA Lifetime 7200 seconds & 4096KB</span><span class="sxs-lookup"><span data-stu-id="00477-245">IPsec: GCMAES128, GCMAES128, PFS14, SA Lifetime 7200 seconds & 4096KB</span></span>

```powershell
$ipsecpolicy2 = New-AzureRmIpsecPolicy -IkeEncryption AES128 -IkeIntegrity SHA1 -DhGroup DHGroup14 -IpsecEncryption GCMAES128 -IpsecIntegrity GCMAES128 -PfsGroup PFS14 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 4096
```

#### <a name="2-create-vnet-to-vnet-connections-with-hello-ipsecike-policy"></a><span data-ttu-id="00477-246">2. Créer des connexions de réseau virtuel à réseau virtuel avec hello stratégie IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="00477-246">2. Create VNet-to-VNet connections with hello IPsec/IKE policy</span></span>

<span data-ttu-id="00477-247">Créer une connexion au réseau et appliquer la stratégie IPsec/IKE de hello que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="00477-247">Create a VNet-to-VNet connection and apply hello IPsec/IKE policy you created.</span></span> <span data-ttu-id="00477-248">Dans cet exemple, les deux passerelles sont Bonjour même abonnement.</span><span class="sxs-lookup"><span data-stu-id="00477-248">In this example, both gateways are in hello same subscription.</span></span> <span data-ttu-id="00477-249">Il est donc possible toocreate et configurez les deux connexions avec hello même stratégie IPsec/IKE Bonjour même session PowerShell.</span><span class="sxs-lookup"><span data-stu-id="00477-249">So it is possible toocreate and configure both connections with hello same IPsec/IKE policy in hello same PowerShell session.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$vnet2gw = Get-AzureRmVirtualNetworkGateway -Name $GWName2  -ResourceGroupName $RG2

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection12 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet2gw -Location $Location1 -ConnectionType Vnet2Vnet -IpsecPolicies $ipsecpolicy2 -SharedKey 'AzureA1b2C3'

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection21 -ResourceGroupName $RG2 -VirtualNetworkGateway1 $vnet2gw -VirtualNetworkGateway2 $vnet1gw -Location $Location2 -ConnectionType Vnet2Vnet -IpsecPolicies $ipsecpolicy2 -SharedKey 'AzureA1b2C3'
```

> [!IMPORTANT]
> <span data-ttu-id="00477-250">Une fois qu’une stratégie IPsec/IKE est spécifiée sur une connexion, passerelle VPN Azure de hello sera uniquement envoyer ou accepter hello IPsec/IKE avec les algorithmes de chiffrement spécifiés et des avantages clés sur cette connexion particulière.</span><span class="sxs-lookup"><span data-stu-id="00477-250">Once an IPsec/IKE policy is specified on a connection, hello Azure VPN gateway will only send or accept hello IPsec/IKE proposal with specified cryptographic algorithms and key strengths on that particular connection.</span></span> <span data-ttu-id="00477-251">Vérifiez que hello stratégies IPsec pour les deux connexions sont hello identiques, sinon établit pas la connexion au réseau.</span><span class="sxs-lookup"><span data-stu-id="00477-251">Make sure hello IPsec policies for both connections are hello same, otherwise the VNet-to-VNet connection will not establish.</span></span>

<span data-ttu-id="00477-252">Après avoir effectué ces étapes, hello est établie dans quelques minutes, et vous aurez hello suivant la topologie du réseau comme indiqué dans le début de hello :</span><span class="sxs-lookup"><span data-stu-id="00477-252">After completing these steps, hello connection is established in a few minutes, and you will have hello following network topology as shown in hello beginning:</span></span>

![stratégie IPSec/IKE](./media/vpn-gateway-ipsecikepolicy-rm-powershell/ipsecikepolicy.png)


## <span data-ttu-id="00477-254"><a name ="managepolicy"></a>Partie 5 : mise à jour de la stratégie IPsec/IKE pour une connexion</span><span class="sxs-lookup"><span data-stu-id="00477-254"><a name ="managepolicy"></a>Part 5 - Update IPsec/IKE policy for a connection</span></span>

<span data-ttu-id="00477-255">dernière section de Hello vous montre comment toomanage stratégie IPsec/IKE pour une connexion existante de S2S ou au réseau.</span><span class="sxs-lookup"><span data-stu-id="00477-255">hello last section shows you how toomanage IPsec/IKE policy for an existing S2S or VNet-to-VNet connection.</span></span> <span data-ttu-id="00477-256">exercice Hello ci-dessous vous guide tout au long de hello opérations sur une connexion suivantes :</span><span class="sxs-lookup"><span data-stu-id="00477-256">hello exercise below walks you through hello following operations on a connection:</span></span>

1. <span data-ttu-id="00477-257">Afficher la stratégie IPsec/IKE de hello d’une connexion</span><span class="sxs-lookup"><span data-stu-id="00477-257">Show hello IPsec/IKE policy of a connection</span></span>
2. <span data-ttu-id="00477-258">Ajouter ou mettre à jour hello IPsec/IKE stratégie tooa connexion</span><span class="sxs-lookup"><span data-stu-id="00477-258">Add or update hello IPsec/IKE policy tooa connection</span></span>
3. <span data-ttu-id="00477-259">Supprimer la stratégie IPsec/IKE de hello à partir d’une connexion</span><span class="sxs-lookup"><span data-stu-id="00477-259">Remove hello IPsec/IKE policy from a connection</span></span>

<span data-ttu-id="00477-260">Hello même procédure s’applique tooboth S2S et les connexions de réseau virtuel à réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="00477-260">hello same steps apply tooboth S2S and VNet-to-VNet connections.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="00477-261">Une stratégie IPsec/IKE est prise en charge uniquement sur des passerelles VPN *Standard* et *HighPerformance* basées sur itinéraires.</span><span class="sxs-lookup"><span data-stu-id="00477-261">IPsec/IKE policy is supported on *Standard* and *HighPerformance* route-based VPN gateways only.</span></span> <span data-ttu-id="00477-262">Il ne fonctionne pas sur la passerelle de base hello référence (SKU) ou une passerelle VPN basée sur des stratégies hello.</span><span class="sxs-lookup"><span data-stu-id="00477-262">It does not work on hello Basic gateway SKU or hello policy-based VPN gateway.</span></span>

#### <a name="1-show-hello-ipsecike-policy-of-a-connection"></a><span data-ttu-id="00477-263">1. Afficher la stratégie IPsec/IKE de hello d’une connexion</span><span class="sxs-lookup"><span data-stu-id="00477-263">1. Show hello IPsec/IKE policy of a connection</span></span>

<span data-ttu-id="00477-264">Bonjour à l’exemple suivant montre comment tooget hello stratégie IPsec/IKE configuré sur une connexion.</span><span class="sxs-lookup"><span data-stu-id="00477-264">hello following example shows how tooget hello IPsec/IKE policy configured on a connection.</span></span> <span data-ttu-id="00477-265">les scripts Hello également continuent à partir des exercices hello ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="00477-265">hello scripts also continue from hello exercises above.</span></span>

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1
$connection6.IpsecPolicies
```

<span data-ttu-id="00477-266">la dernière commande Hello répertorie la stratégie IPsec/IKE actuelle hello configuré sur la connexion de hello, s’il en existe une.</span><span class="sxs-lookup"><span data-stu-id="00477-266">hello last command lists hello current IPsec/IKE policy configured on hello connection, if there is any.</span></span> <span data-ttu-id="00477-267">Hello suivant le résultat de l’exemple est pour la connexion de hello :</span><span class="sxs-lookup"><span data-stu-id="00477-267">hello following sample output is for hello connection:</span></span>

```powershell
SALifeTimeSeconds   : 3600
SADataSizeKilobytes : 2048
IpsecEncryption     : AES256
IpsecIntegrity      : SHA256
IkeEncryption       : AES256
IkeIntegrity        : SHA384
DhGroup             : DHGroup24
PfsGroup            : PFS24
```

<span data-ttu-id="00477-268">S’il n’existe aucune stratégie IPsec/IKE configuré, hello commande (PS > $connection6.policy) Obtient vide retour.</span><span class="sxs-lookup"><span data-stu-id="00477-268">If there is no IPsec/IKE policy configured, hello command (PS> $connection6.policy) gets an empty return.</span></span> <span data-ttu-id="00477-269">Cela ne signifie pas IPsec/IKE n’est pas configuré sur la connexion de hello, mais qu’il n’existe aucune stratégie IPsec/IKE personnalisée.</span><span class="sxs-lookup"><span data-stu-id="00477-269">It does not mean IPsec/IKE is not configured on hello connection, but that there is no custom IPsec/IKE policy.</span></span> <span data-ttu-id="00477-270">connexion réelle de Hello utilise une stratégie de valeur par défaut hello négocié entre votre périphérique VPN sur site et la passerelle VPN Azure de hello.</span><span class="sxs-lookup"><span data-stu-id="00477-270">hello actual connection uses hello default policy negotiated between your on-premises VPN device and hello Azure VPN gateway.</span></span>

#### <a name="2-add-or-update-an-ipsecike-policy-for-a-connection"></a><span data-ttu-id="00477-271">2. Ajouter ou mettre à jour une stratégie IPsec/IKE pour une connexion</span><span class="sxs-lookup"><span data-stu-id="00477-271">2. Add or update an IPsec/IKE policy for a connection</span></span>

<span data-ttu-id="00477-272">les étapes Hello tooadd une nouvelle stratégie ou mise à jour une stratégie existante sur une connexion sont hello même : créer une nouvelle stratégie, puis appliquer la nouvelle connexion de toohello stratégie hello.</span><span class="sxs-lookup"><span data-stu-id="00477-272">hello steps tooadd a new policy or update an existing policy on a connection are hello same: create a new policy then apply hello new policy toohello connection.</span></span>

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

$newpolicy6   = New-AzureRmIpsecPolicy -IkeEncryption AES128 -IkeIntegrity SHA1 -DhGroup DHGroup14 -IpsecEncryption GCMAES128 -IpsecIntegrity GCMAES128 -PfsGroup None -SALifeTimeSeconds 3600 -SADataSizeKilobytes 2048

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -IpsecPolicies $newpolicy6
```

<span data-ttu-id="00477-273">tooenable « UsePolicyBasedTrafficSelectors » lors de la connexion tooan basée sur des stratégies VPN appareil local, ajoutez hello »-UsePolicyBaseTrafficSelectors « paramètre toohello applet de commande, ou définissez-la trop option de hello $False toodisable :</span><span class="sxs-lookup"><span data-stu-id="00477-273">tooenable "UsePolicyBasedTrafficSelectors" when connecting tooan on-premises policy-based VPN device, add hello "-UsePolicyBaseTrafficSelectors" parameter toohello cmdlet, or set it too$False toodisable hello option:</span></span>

```powershell
Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -IpsecPolicies $newpolicy6 -UsePolicyBasedTrafficSelectors $True
```

<span data-ttu-id="00477-274">Vous pouvez obtenir la connexion de hello toocheck à nouveau si la mise à jour de stratégie de hello.</span><span class="sxs-lookup"><span data-stu-id="00477-274">You can get hello connection again toocheck if hello policy is updated.</span></span>

```powershell
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1
$connection6.IpsecPolicies
```

<span data-ttu-id="00477-275">Vous devez voir la sortie hello à partir de la dernière ligne de hello, comme indiqué dans hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="00477-275">You should see hello output from hello last line, as shown in hello following example:</span></span>

```powershell
SALifeTimeSeconds   : 3600
SADataSizeKilobytes : 2048
IpsecEncryption     : GCMAES128
IpsecIntegrity      : GCMAES128
IkeEncryption       : AES128
IkeIntegrity        : SHA1
DhGroup             : DHGroup14--
PfsGroup            : None
```

#### <a name="3-remove-an-ipsecike-policy-from-a-connection"></a><span data-ttu-id="00477-276">3. Supprimer une stratégie IPsec/IKE d’une connexion</span><span class="sxs-lookup"><span data-stu-id="00477-276">3. Remove an IPsec/IKE policy from a connection</span></span>

<span data-ttu-id="00477-277">Lorsque vous supprimez une connexion de stratégie personnalisée de hello, passerelle VPN Azure de hello revient arrière toohello [liste par défaut des propositions de IPsec/IKE](vpn-gateway-about-vpn-devices.md) et renégocie à nouveau avec votre périphérique VPN sur site.</span><span class="sxs-lookup"><span data-stu-id="00477-277">Once you remove hello custom policy from a connection, hello Azure VPN gateway reverts back toohello [default list of IPsec/IKE proposals](vpn-gateway-about-vpn-devices.md) and renegotiates again with your on-premises VPN device.</span></span>

```powershell
$RG1           = "TestPolicyRG1"
$Connection16  = "VNet1toSite6"
$connection6   = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

$currentpolicy = $connection6.IpsecPolicies[0]
$connection6.IpsecPolicies.Remove($currentpolicy)

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6
```

<span data-ttu-id="00477-278">Vous pouvez utiliser hello toocheck de script même si la stratégie de hello a été supprimée à partir de la connexion de hello.</span><span class="sxs-lookup"><span data-stu-id="00477-278">You can use hello same script toocheck if hello policy has been removed from hello connection.</span></span>

## <a name="next-steps"></a><span data-ttu-id="00477-279">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="00477-279">Next steps</span></span>

<span data-ttu-id="00477-280">Pour plus d’informations sur les sélecteurs de trafic basés sur une stratégie, voir [Connecter plusieurs périphériques VPN basés sur un stratégie locale](vpn-gateway-connect-multiple-policybased-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="00477-280">See [Connect multiple on-premises policy-based VPN devices](vpn-gateway-connect-multiple-policybased-rm-ps.md) for more details regarding policy-based traffic selectors.</span></span>

<span data-ttu-id="00477-281">Une fois que votre connexion est terminée, vous pouvez ajouter des machines virtuelles tooyour des réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="00477-281">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="00477-282">Consultez [Création d’une machine virtuelle](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) pour connaître les différentes étapes.</span><span class="sxs-lookup"><span data-stu-id="00477-282">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>
