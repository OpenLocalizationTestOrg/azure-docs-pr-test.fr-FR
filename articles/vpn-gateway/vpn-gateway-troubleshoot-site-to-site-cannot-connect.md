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
# <a name="troubleshooting-an-azure-site-to-site-vpn-connection-cannot-connect-and-stops-working"></a><span data-ttu-id="cb453-103">Résolution de problèmes : une connexion VPN de site à site Azure cesse de fonctionner</span><span class="sxs-lookup"><span data-stu-id="cb453-103">Troubleshooting: An Azure site-to-site VPN connection cannot connect and stops working</span></span>

<span data-ttu-id="cb453-104">Après avoir configuré une connexion VPN de site à site entre un réseau local et un réseau virtuel Azure, hello connexion VPN soudain cesse de fonctionner et ne peut pas être reconnecté.</span><span class="sxs-lookup"><span data-stu-id="cb453-104">After you configure a site-to-site VPN connection between an on-premises network and an Azure virtual network, hello VPN connection suddenly stops working and cannot be reconnected.</span></span> <span data-ttu-id="cb453-105">Cet article fournit la résolution des problèmes étapes toohelp vous résolvez ce problème.</span><span class="sxs-lookup"><span data-stu-id="cb453-105">This article provides troubleshooting steps toohelp you resolve this problem.</span></span> 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-steps"></a><span data-ttu-id="cb453-106">Étapes de dépannage</span><span class="sxs-lookup"><span data-stu-id="cb453-106">Troubleshooting steps</span></span>

<span data-ttu-id="cb453-107">problème de hello tooresolve, essayez tout d’abord de trop[passerelle VPN Azure de hello réinitialisation](vpn-gateway-resetgw-classic.md) et réinitialiser tunnel hello à partir de l’appareil VPN local hello.</span><span class="sxs-lookup"><span data-stu-id="cb453-107">tooresolve hello problem, first try too[reset hello Azure VPN gateway](vpn-gateway-resetgw-classic.md) and reset hello tunnel from hello on-premises VPN device.</span></span> <span data-ttu-id="cb453-108">Si hello problème persiste, suivez ces cause de hello tooidentify étapes du problème de hello.</span><span class="sxs-lookup"><span data-stu-id="cb453-108">If hello problem persists, follow these steps tooidentify hello cause of hello problem.</span></span>

### <a name="prerequisite-step"></a><span data-ttu-id="cb453-109">Étape des conditions préalables</span><span class="sxs-lookup"><span data-stu-id="cb453-109">Prerequisite step</span></span>

<span data-ttu-id="cb453-110">Vérifiez le type hello de passerelle VPN Azure de hello.</span><span class="sxs-lookup"><span data-stu-id="cb453-110">Check hello type of hello Azure VPN gateway.</span></span>

1. <span data-ttu-id="cb453-111">Accédez toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="cb453-111">Go toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="cb453-112">Vérifiez hello **vue d’ensemble** page de passerelle VPN de hello pour les informations de type hello.</span><span class="sxs-lookup"><span data-stu-id="cb453-112">Check hello **Overview** page of hello VPN gateway for hello type information.</span></span>
    
    ![Vue d’ensemble de la passerelle de hello](media\vpn-gateway-troubleshoot-site-to-site-cannot-connect\gatewayoverview.png)

### <a name="step-1-check-whether-hello-on-premises-vpn-device-is-validated"></a><span data-ttu-id="cb453-114">Étape 1.</span><span class="sxs-lookup"><span data-stu-id="cb453-114">Step 1.</span></span> <span data-ttu-id="cb453-115">Vérifiez si l’appareil VPN local hello est validé</span><span class="sxs-lookup"><span data-stu-id="cb453-115">Check whether hello on-premises VPN device is validated</span></span>

1. <span data-ttu-id="cb453-116">Vérifiez si vous utilisez un [appareil VPN et une version de système d’exploitation validés](vpn-gateway-about-vpn-devices.md#devicetable).</span><span class="sxs-lookup"><span data-stu-id="cb453-116">Check whether you are using a [validated VPN device and operating system version](vpn-gateway-about-vpn-devices.md#devicetable).</span></span> <span data-ttu-id="cb453-117">Si l’appareil de hello n’est pas un périphérique VPN validé, peut avoir toocontact hello appareil fabricant toosee s’il existe un problème de compatibilité.</span><span class="sxs-lookup"><span data-stu-id="cb453-117">If hello device is not a validated VPN device, you might have toocontact hello device manufacturer toosee if there is a compatibility issue.</span></span>

2. <span data-ttu-id="cb453-118">Assurez-vous que le périphérique VPN hello est correctement configuré.</span><span class="sxs-lookup"><span data-stu-id="cb453-118">Make sure that hello VPN device is correctly configured.</span></span> <span data-ttu-id="cb453-119">Pour plus d’informations, consultez la page [Modification des exemples de configuration de périphérique](/vpn-gateway-about-vpn-devices.md#editing).</span><span class="sxs-lookup"><span data-stu-id="cb453-119">For more information, see [Edit device configuration samples](/vpn-gateway-about-vpn-devices.md#editing).</span></span>

### <a name="step-2-verify-hello-shared-key"></a><span data-ttu-id="cb453-120">Étape 2.</span><span class="sxs-lookup"><span data-stu-id="cb453-120">Step 2.</span></span> <span data-ttu-id="cb453-121">Vérifiez la clé partagée de hello</span><span class="sxs-lookup"><span data-stu-id="cb453-121">Verify hello shared key</span></span>

<span data-ttu-id="cb453-122">Comparer la clé partagée de hello pour hello local VPN appareil toohello VPN de réseau virtuel Azure toomake assurer que les clés hello correspondent.</span><span class="sxs-lookup"><span data-stu-id="cb453-122">Compare hello shared key for hello on-premises VPN device toohello Azure Virtual Network VPN toomake sure that hello keys match.</span></span> 

<span data-ttu-id="cb453-123">clé partagée de tooview hello pour hello connexion VPN d’Azure, utilisez une des méthodes suivantes de hello :</span><span class="sxs-lookup"><span data-stu-id="cb453-123">tooview hello shared key for hello Azure VPN connection, use one of hello following methods:</span></span>

<span data-ttu-id="cb453-124">**Portail Azure**</span><span class="sxs-lookup"><span data-stu-id="cb453-124">**Azure portal**</span></span>

1. <span data-ttu-id="cb453-125">Accédez toohello passerelle site-à-site réseau VPN que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="cb453-125">Go toohello VPN gateway site-to-site connection that you created.</span></span>

2. <span data-ttu-id="cb453-126">Bonjour **paramètres** , cliquez sur **clé partagée**.</span><span class="sxs-lookup"><span data-stu-id="cb453-126">In hello **Settings** section, click **Shared key**.</span></span>
    
    ![Clé partagée](media/vpn-gateway-troubleshoot-site-to-site-cannot-connect/sharedkey.png)

<span data-ttu-id="cb453-128">**Azure PowerShell**</span><span class="sxs-lookup"><span data-stu-id="cb453-128">**Azure PowerShell**</span></span>

<span data-ttu-id="cb453-129">Pour le modèle de déploiement du Gestionnaire de ressources Azure hello :</span><span class="sxs-lookup"><span data-stu-id="cb453-129">For hello Azure Resource Manager deployment model:</span></span>

    Get-AzureRmVirtualNetworkGatewayConnectionSharedKey -Name <Connection name> -ResourceGroupName <Resource group name>

<span data-ttu-id="cb453-130">Pour le modèle de déploiement classique de hello :</span><span class="sxs-lookup"><span data-stu-id="cb453-130">For hello classic deployment model:</span></span>

    Get-AzureVNetGatewayKey -VNetName -LocalNetworkSiteName

### <a name="step-3-verify-hello-vpn-peer-ips"></a><span data-ttu-id="cb453-131">Étape 3.</span><span class="sxs-lookup"><span data-stu-id="cb453-131">Step 3.</span></span> <span data-ttu-id="cb453-132">Vérifier les adresses IP d’homologue VPN hello</span><span class="sxs-lookup"><span data-stu-id="cb453-132">Verify hello VPN peer IPs</span></span>

-   <span data-ttu-id="cb453-133">Hello définition IP Bonjour **passerelle de réseau Local** objet dans Azure doit correspondre à l’IP du périphérique local hello.</span><span class="sxs-lookup"><span data-stu-id="cb453-133">hello IP definition in hello **Local Network Gateway** object in Azure should match hello on-premises device IP.</span></span>
-   <span data-ttu-id="cb453-134">Hello définition IP de passerelle Azure qui est définie sur hello local appareil doit correspondre à l’IP de la passerelle Azure hello.</span><span class="sxs-lookup"><span data-stu-id="cb453-134">hello Azure gateway IP definition that is set on hello on-premises device should match hello Azure gateway IP.</span></span>

### <a name="step-4-check-udr-and-nsgs-on-hello-gateway-subnet"></a><span data-ttu-id="cb453-135">Étape 4.</span><span class="sxs-lookup"><span data-stu-id="cb453-135">Step 4.</span></span> <span data-ttu-id="cb453-136">Vérifiez UDR et les groupes de sécurité réseau sur le sous-réseau de passerelle hello</span><span class="sxs-lookup"><span data-stu-id="cb453-136">Check UDR and NSGs on hello gateway subnet</span></span>

<span data-ttu-id="cb453-137">Recherchez et supprimez routage défini par l’utilisateur (UDR) ou des groupes de sécurité réseau (NSG) sur le sous-réseau de passerelle hello ensuite tester le résultat de hello.</span><span class="sxs-lookup"><span data-stu-id="cb453-137">Check for and remove user-defined routing (UDR) or Network Security Groups (NSGs) on hello gateway subnet, and then test hello result.</span></span> <span data-ttu-id="cb453-138">Si le problème de hello est résolu, valider les paramètres de hello UDR ou groupe de sécurité réseau appliqués.</span><span class="sxs-lookup"><span data-stu-id="cb453-138">If hello problem is resolved, validate hello settings that UDR or NSG applied.</span></span>

### <a name="step-5-check-hello-on-premises-vpn-device-external-interface-address"></a><span data-ttu-id="cb453-139">Étape 5.</span><span class="sxs-lookup"><span data-stu-id="cb453-139">Step 5.</span></span> <span data-ttu-id="cb453-140">Vérification hello adresse interface externe du périphérique VPN sur site</span><span class="sxs-lookup"><span data-stu-id="cb453-140">Check hello on-premises VPN device external interface address</span></span>

- <span data-ttu-id="cb453-141">Si hello adresse IP de côté Internet du périphérique VPN de hello est inclus dans hello **réseau Local** définition dans Azure, vous pouvez rencontrer des déconnexions sporadiques.</span><span class="sxs-lookup"><span data-stu-id="cb453-141">If hello Internet-facing IP address of hello VPN device is included in hello **Local network** definition in Azure, you might experience sporadic disconnections.</span></span>
- <span data-ttu-id="cb453-142">Hello interface externe de l’appareil doit être directement sur Internet de hello.</span><span class="sxs-lookup"><span data-stu-id="cb453-142">hello device's external interface must be directly on hello Internet.</span></span> <span data-ttu-id="cb453-143">Il ne doit y avoir aucune traduction d’adresses réseau ou un pare-feu entre hello Internet et les appareils hello.</span><span class="sxs-lookup"><span data-stu-id="cb453-143">There should be no network address translation or firewall between hello Internet and hello device.</span></span>
- <span data-ttu-id="cb453-144">tooconfigure pare-feu clustering toohave une adresse IP virtuelle, vous devez arrêter le cluster de hello et exposer un équipement VPN hello directement l’interface publique de tooa cette passerelle hello pouvant communiquer avec.</span><span class="sxs-lookup"><span data-stu-id="cb453-144">tooconfigure firewall clustering toohave a virtual IP, you must break hello cluster and expose hello VPN appliance directly tooa public interface that hello gateway can interface with.</span></span>

### <a name="step-6-verify-that-hello-subnets-match-exactly-azure-policy-based-gateways"></a><span data-ttu-id="cb453-145">Étape 6.</span><span class="sxs-lookup"><span data-stu-id="cb453-145">Step 6.</span></span> <span data-ttu-id="cb453-146">Vérifiez que les sous-réseaux hello correspondent exactement (passerelles Azure basée sur des stratégies)</span><span class="sxs-lookup"><span data-stu-id="cb453-146">Verify that hello subnets match exactly (Azure policy-based gateways)</span></span>

-   <span data-ttu-id="cb453-147">Vérifiez que les sous-réseaux hello correspondent exactement entre hello réseau virtuel Azure et locaux pour hello réseau virtuel Azure.</span><span class="sxs-lookup"><span data-stu-id="cb453-147">Verify that hello subnets match exactly between hello Azure virtual network and on-premises definitions for hello Azure virtual network.</span></span>
-   <span data-ttu-id="cb453-148">Vérifiez que les sous-réseaux hello correspondent exactement entre hello **passerelle de réseau Local** et définitions de réseau local de hello en local.</span><span class="sxs-lookup"><span data-stu-id="cb453-148">Verify that hello subnets match exactly between hello **Local Network Gateway** and on-premises definitions for hello on-premises network.</span></span>

### <a name="step-7-verify-hello-azure-gateway-health-probe"></a><span data-ttu-id="cb453-149">Étape 7.</span><span class="sxs-lookup"><span data-stu-id="cb453-149">Step 7.</span></span> <span data-ttu-id="cb453-150">Vérifiez que la sonde d’intégrité de passerelle Azure hello</span><span class="sxs-lookup"><span data-stu-id="cb453-150">Verify hello Azure gateway health probe</span></span>

1. <span data-ttu-id="cb453-151">Accédez toohello [sonde d’intégrité](https://&lt;YourVirtualNetworkGatewayIP&gt;:8081/healthprobe).</span><span class="sxs-lookup"><span data-stu-id="cb453-151">Go toohello [health probe](https://&lt;YourVirtualNetworkGatewayIP&gt;:8081/healthprobe).</span></span>

2. <span data-ttu-id="cb453-152">Cliquez sur Avertissement de certificat hello.</span><span class="sxs-lookup"><span data-stu-id="cb453-152">Click through hello certificate warning.</span></span>
3. <span data-ttu-id="cb453-153">Si vous recevez une réponse, passerelle VPN de hello est considéré comme sain.</span><span class="sxs-lookup"><span data-stu-id="cb453-153">If you receive a response, hello VPN gateway is considered healthy.</span></span> <span data-ttu-id="cb453-154">Si vous ne recevez pas de réponse, passerelle de hello ne peut pas être sain ou un groupe de sécurité réseau sur le sous-réseau de passerelle hello problème hello.</span><span class="sxs-lookup"><span data-stu-id="cb453-154">If you don't receive a response, hello gateway might not be healthy or an NSG on hello gateway subnet is causing hello problem.</span></span> <span data-ttu-id="cb453-155">Hello suivant le texte est un exemple de réponse :</span><span class="sxs-lookup"><span data-stu-id="cb453-155">hello following text is a sample response:</span></span>

    <span data-ttu-id="cb453-156">&lt;?xml version="1.0"?&gt;  <string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">Primary Instance: GatewayTenantWorker_IN_1 GatewayTenantVersion: 14.7.24.6&lt;/string&gt;</span><span class="sxs-lookup"><span data-stu-id="cb453-156">&lt;?xml version="1.0"?>  <string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">Primary Instance: GatewayTenantWorker_IN_1 GatewayTenantVersion: 14.7.24.6</string&gt;</span></span>

### <a name="step-8-check-whether-hello-on-premises-vpn-device-has-hello-perfect-forward-secrecy-feature-enabled"></a><span data-ttu-id="cb453-157">Étape 8 :</span><span class="sxs-lookup"><span data-stu-id="cb453-157">Step 8.</span></span> <span data-ttu-id="cb453-158">Vérifiez si hello local périphérique VPN avec la fonctionnalité de transmission parfaite de hello activée</span><span class="sxs-lookup"><span data-stu-id="cb453-158">Check whether hello on-premises VPN device has hello perfect forward secrecy feature enabled</span></span>

<span data-ttu-id="cb453-159">fonctionnalité de transmission parfaite Hello peut entraîner des problèmes de déconnexion.</span><span class="sxs-lookup"><span data-stu-id="cb453-159">hello perfect forward secrecy feature can cause disconnection problems.</span></span> <span data-ttu-id="cb453-160">Si le périphérique VPN de hello a parfaite activé, désactiver la fonctionnalité de hello.</span><span class="sxs-lookup"><span data-stu-id="cb453-160">If hello VPN device has perfect forward secrecy enabled, disable hello feature.</span></span> <span data-ttu-id="cb453-161">Puis, mettez à jour de stratégie IPsec de hello VPN gateway.</span><span class="sxs-lookup"><span data-stu-id="cb453-161">Then update hello VPN gateway IPsec policy.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cb453-162">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="cb453-162">Next steps</span></span>

-   [<span data-ttu-id="cb453-163">Configurer un réseau virtuel tooa de connexion de site à site</span><span class="sxs-lookup"><span data-stu-id="cb453-163">Configure a site-to-site connection tooa virtual network</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
-   [<span data-ttu-id="cb453-164">Configurer la stratégie IPsec/IKE pour des connexions VPN S2S ou de réseau virtuel à réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="cb453-164">Configure an IPsec/IKE policy for site-to-site VPN connections</span></span>](vpn-gateway-ipsecikepolicy-rm-powershell.md)
