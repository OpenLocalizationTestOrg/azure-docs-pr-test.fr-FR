---
title: "Résoudre les problèmes de connexion VPN de site à site Azure | Microsoft Docs"
description: "Découvrez comment résoudre un problème de connexion VPN de site à site qui cesse soudainement de fonctionner sans possibilité de reconnexion."
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
ms.openlocfilehash: e7a3da64895f0307e5d6c3563672205a2f93a7d2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshooting-an-azure-site-to-site-vpn-connection-cannot-connect-and-stops-working"></a><span data-ttu-id="cdaff-103">Résolution de problèmes : une connexion VPN de site à site Azure cesse de fonctionner</span><span class="sxs-lookup"><span data-stu-id="cdaff-103">Troubleshooting: An Azure site-to-site VPN connection cannot connect and stops working</span></span>

<span data-ttu-id="cdaff-104">Après avoir configuré une connexion VPN de site à site entre un réseau local et un réseau virtuel Azure, la connexion VPN cesse soudainement de fonctionner et la reconnexion est impossible.</span><span class="sxs-lookup"><span data-stu-id="cdaff-104">After you configure a site-to-site VPN connection between an on-premises network and an Azure virtual network, the VPN connection suddenly stops working and cannot be reconnected.</span></span> <span data-ttu-id="cdaff-105">Cet article fournit les étapes requises pour vous aider à résoudre ce problème.</span><span class="sxs-lookup"><span data-stu-id="cdaff-105">This article provides troubleshooting steps to help you resolve this problem.</span></span> 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-steps"></a><span data-ttu-id="cdaff-106">Étapes de dépannage</span><span class="sxs-lookup"><span data-stu-id="cdaff-106">Troubleshooting steps</span></span>

<span data-ttu-id="cdaff-107">Pour résoudre le problème, essayez d’abord de [réinitialiser la passerelle VPN Azure](vpn-gateway-resetgw-classic.md) et de réinitialiser le tunnel à partir du périphérique VPN local.</span><span class="sxs-lookup"><span data-stu-id="cdaff-107">To resolve the problem, first try to [reset the Azure VPN gateway](vpn-gateway-resetgw-classic.md) and reset the tunnel from the on-premises VPN device.</span></span> <span data-ttu-id="cdaff-108">Si le problème persiste, procédez comme suit pour en identifier la cause.</span><span class="sxs-lookup"><span data-stu-id="cdaff-108">If the problem persists, follow these steps to identify the cause of the problem.</span></span>

### <a name="prerequisite-step"></a><span data-ttu-id="cdaff-109">Étape des conditions préalables</span><span class="sxs-lookup"><span data-stu-id="cdaff-109">Prerequisite step</span></span>

<span data-ttu-id="cdaff-110">Vérifiez le type de passerelle VPN Azure utilisée.</span><span class="sxs-lookup"><span data-stu-id="cdaff-110">Check the type of the Azure VPN gateway.</span></span>

1. <span data-ttu-id="cdaff-111">Accédez au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="cdaff-111">Go to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="cdaff-112">Vérifiez les informations de type dans la page **Vue d’ensemble** de la passerelle VPN.</span><span class="sxs-lookup"><span data-stu-id="cdaff-112">Check the **Overview** page of the VPN gateway for the type information.</span></span>
    
    ![Vue d’ensemble de la passerelle](media\vpn-gateway-troubleshoot-site-to-site-cannot-connect\gatewayoverview.png)

### <a name="step-1-check-whether-the-on-premises-vpn-device-is-validated"></a><span data-ttu-id="cdaff-114">Étape 1.</span><span class="sxs-lookup"><span data-stu-id="cdaff-114">Step 1.</span></span> <span data-ttu-id="cdaff-115">Vérifier si le périphérique VPN local est validé</span><span class="sxs-lookup"><span data-stu-id="cdaff-115">Check whether the on-premises VPN device is validated</span></span>

1. <span data-ttu-id="cdaff-116">Vérifiez si vous utilisez un [appareil VPN et une version de système d’exploitation validés](vpn-gateway-about-vpn-devices.md#devicetable).</span><span class="sxs-lookup"><span data-stu-id="cdaff-116">Check whether you are using a [validated VPN device and operating system version](vpn-gateway-about-vpn-devices.md#devicetable).</span></span> <span data-ttu-id="cdaff-117">Si l’appareil n’est pas un périphérique VPN validé, vous devez contacter son fabricant pour en vérifier la compatibilité.</span><span class="sxs-lookup"><span data-stu-id="cdaff-117">If the device is not a validated VPN device, you might have to contact the device manufacturer to see if there is a compatibility issue.</span></span>

2. <span data-ttu-id="cdaff-118">Assurez-vous que l’appareil VPN est correctement configuré.</span><span class="sxs-lookup"><span data-stu-id="cdaff-118">Make sure that the VPN device is correctly configured.</span></span> <span data-ttu-id="cdaff-119">Pour plus d’informations, consultez la page [Modification des exemples de configuration de périphérique](/vpn-gateway-about-vpn-devices.md#editing).</span><span class="sxs-lookup"><span data-stu-id="cdaff-119">For more information, see [Edit device configuration samples](/vpn-gateway-about-vpn-devices.md#editing).</span></span>

### <a name="step-2-verify-the-shared-key"></a><span data-ttu-id="cdaff-120">Étape 2.</span><span class="sxs-lookup"><span data-stu-id="cdaff-120">Step 2.</span></span> <span data-ttu-id="cdaff-121">Vérifier la clé partagée</span><span class="sxs-lookup"><span data-stu-id="cdaff-121">Verify the shared key</span></span>

<span data-ttu-id="cdaff-122">Comparez la clé partagée du périphérique VPN local et celle du VPN de réseau virtuel pour vous assurer que les clés correspondent.</span><span class="sxs-lookup"><span data-stu-id="cdaff-122">Compare the shared key for the on-premises VPN device to the Azure Virtual Network VPN to make sure that the keys match.</span></span> 

<span data-ttu-id="cdaff-123">Pour afficher la clé partagée dans l’optique de la connexion VPN Azure, utilisez l’une des méthodes suivantes :</span><span class="sxs-lookup"><span data-stu-id="cdaff-123">To view the shared key for the Azure VPN connection, use one of the following methods:</span></span>

<span data-ttu-id="cdaff-124">**Portail Azure**</span><span class="sxs-lookup"><span data-stu-id="cdaff-124">**Azure portal**</span></span>

1. <span data-ttu-id="cdaff-125">Accédez à la connexion de site à site de passerelle VPN que vous avez créée.</span><span class="sxs-lookup"><span data-stu-id="cdaff-125">Go to the VPN gateway site-to-site connection that you created.</span></span>

2. <span data-ttu-id="cdaff-126">Dans la section **Paramètres**, cliquez sur **Clé partagée**.</span><span class="sxs-lookup"><span data-stu-id="cdaff-126">In the **Settings** section, click **Shared key**.</span></span>
    
    ![Clé partagée](media/vpn-gateway-troubleshoot-site-to-site-cannot-connect/sharedkey.png)

<span data-ttu-id="cdaff-128">**Azure PowerShell**</span><span class="sxs-lookup"><span data-stu-id="cdaff-128">**Azure PowerShell**</span></span>

<span data-ttu-id="cdaff-129">Pour le modèle de déploiement Azure Resource Manager :</span><span class="sxs-lookup"><span data-stu-id="cdaff-129">For the Azure Resource Manager deployment model:</span></span>

    Get-AzureRmVirtualNetworkGatewayConnectionSharedKey -Name <Connection name> -ResourceGroupName <Resource group name>

<span data-ttu-id="cdaff-130">Pour le modèle de déploiement classique :</span><span class="sxs-lookup"><span data-stu-id="cdaff-130">For the classic deployment model:</span></span>

    Get-AzureVNetGatewayKey -VNetName -LocalNetworkSiteName

### <a name="step-3-verify-the-vpn-peer-ips"></a><span data-ttu-id="cdaff-131">Étape 3.</span><span class="sxs-lookup"><span data-stu-id="cdaff-131">Step 3.</span></span> <span data-ttu-id="cdaff-132">Vérifier les adresses IP d’homologue VPN</span><span class="sxs-lookup"><span data-stu-id="cdaff-132">Verify the VPN peer IPs</span></span>

-   <span data-ttu-id="cdaff-133">La définition de l’adresse IP dans l’objet **Passerelle de réseau local** dans Azure doit correspondre à l’adresse IP de l’appareil local.</span><span class="sxs-lookup"><span data-stu-id="cdaff-133">The IP definition in the **Local Network Gateway** object in Azure should match the on-premises device IP.</span></span>
-   <span data-ttu-id="cdaff-134">La définition de l’adresse IP de la passerelle Azure qui est configurée sur l’appareil local doit correspondre à l’adresse IP de la passerelle Azure.</span><span class="sxs-lookup"><span data-stu-id="cdaff-134">The Azure gateway IP definition that is set on the on-premises device should match the Azure gateway IP.</span></span>

### <a name="step-4-check-udr-and-nsgs-on-the-gateway-subnet"></a><span data-ttu-id="cdaff-135">Étape 4.</span><span class="sxs-lookup"><span data-stu-id="cdaff-135">Step 4.</span></span> <span data-ttu-id="cdaff-136">Vérifier les paramètres d’itinéraire défini par l’utilisateur et des groupes de sécurité réseau sur le sous-réseau de passerelle</span><span class="sxs-lookup"><span data-stu-id="cdaff-136">Check UDR and NSGs on the gateway subnet</span></span>

<span data-ttu-id="cdaff-137">Recherchez et supprimez l’itinéraire défini par l’utilisateur (UDR) ou les groupes de sécurité réseau (NSG) sur le sous-réseau de passerelle, puis testez le résultat.</span><span class="sxs-lookup"><span data-stu-id="cdaff-137">Check for and remove user-defined routing (UDR) or Network Security Groups (NSGs) on the gateway subnet, and then test the result.</span></span> <span data-ttu-id="cdaff-138">Si le problème est résolu, validez les paramètres de l’itinéraire défini par l’utilisateur ou des groupes de sécurité réseau appliqués.</span><span class="sxs-lookup"><span data-stu-id="cdaff-138">If the problem is resolved, validate the settings that UDR or NSG applied.</span></span>

### <a name="step-5-check-the-on-premises-vpn-device-external-interface-address"></a><span data-ttu-id="cdaff-139">Étape 5.</span><span class="sxs-lookup"><span data-stu-id="cdaff-139">Step 5.</span></span> <span data-ttu-id="cdaff-140">Vérifier l’adresse d’interface externe du périphérique VPN local</span><span class="sxs-lookup"><span data-stu-id="cdaff-140">Check the on-premises VPN device external interface address</span></span>

- <span data-ttu-id="cdaff-141">Si l’adresse IP du périphérique VPN, accessible sur Internet, est incluse dans la définition du **réseau local** dans Azure, il se peut que vous subissiez des déconnexions occasionnelles.</span><span class="sxs-lookup"><span data-stu-id="cdaff-141">If the Internet-facing IP address of the VPN device is included in the **Local network** definition in Azure, you might experience sporadic disconnections.</span></span>
- <span data-ttu-id="cdaff-142">L’interface externe de l’appareil doit être directement liée à Internet.</span><span class="sxs-lookup"><span data-stu-id="cdaff-142">The device's external interface must be directly on the Internet.</span></span> <span data-ttu-id="cdaff-143">Il ne doit y avoir aucune traduction d’adresses réseau (NAT) ni aucun pare-feu entre Internet et l’appareil.</span><span class="sxs-lookup"><span data-stu-id="cdaff-143">There should be no network address translation or firewall between the Internet and the device.</span></span>
- <span data-ttu-id="cdaff-144">Pour configurer le clustering de pare-feu dans le but d’obtenir une adresse IP virtuelle, vous devez détruire le cluster et exposer l’appliance VPN directement à une interface publique susceptible de s’interfacer avec la passerelle.</span><span class="sxs-lookup"><span data-stu-id="cdaff-144">To configure firewall clustering to have a virtual IP, you must break the cluster and expose the VPN appliance directly to a public interface that the gateway can interface with.</span></span>

### <a name="step-6-verify-that-the-subnets-match-exactly-azure-policy-based-gateways"></a><span data-ttu-id="cdaff-145">Étape 6.</span><span class="sxs-lookup"><span data-stu-id="cdaff-145">Step 6.</span></span> <span data-ttu-id="cdaff-146">Vérifier la correspondance des sous-réseaux (passerelles Azure basées sur des stratégies)</span><span class="sxs-lookup"><span data-stu-id="cdaff-146">Verify that the subnets match exactly (Azure policy-based gateways)</span></span>

-   <span data-ttu-id="cdaff-147">Vérifiez que les sous-réseaux correspondent exactement dans le réseau virtuel Azure et dans les définitions locales pour le réseau virtuel Azure.</span><span class="sxs-lookup"><span data-stu-id="cdaff-147">Verify that the subnets match exactly between the Azure virtual network and on-premises definitions for the Azure virtual network.</span></span>
-   <span data-ttu-id="cdaff-148">Vérifiez que les sous-réseaux correspondent exactement dans **la passerelle réseau locale** et dans les définitions locales pour le réseau local.</span><span class="sxs-lookup"><span data-stu-id="cdaff-148">Verify that the subnets match exactly between the **Local Network Gateway** and on-premises definitions for the on-premises network.</span></span>

### <a name="step-7-verify-the-azure-gateway-health-probe"></a><span data-ttu-id="cdaff-149">Étape 7.</span><span class="sxs-lookup"><span data-stu-id="cdaff-149">Step 7.</span></span> <span data-ttu-id="cdaff-150">Vérifier la sonde d’intégrité de la passerelle Azure</span><span class="sxs-lookup"><span data-stu-id="cdaff-150">Verify the Azure gateway health probe</span></span>

1. <span data-ttu-id="cdaff-151">Accédez à la [sonde d’intégrité](https://&lt;YourVirtualNetworkGatewayIP&gt;:8081/healthprobe).</span><span class="sxs-lookup"><span data-stu-id="cdaff-151">Go to the [health probe](https://&lt;YourVirtualNetworkGatewayIP&gt;:8081/healthprobe).</span></span>

2. <span data-ttu-id="cdaff-152">Cliquez sur l’avertissement de certificat.</span><span class="sxs-lookup"><span data-stu-id="cdaff-152">Click through the certificate warning.</span></span>
3. <span data-ttu-id="cdaff-153">Si vous recevez une réponse, cela signifie que la passerelle VPN est considérée comme saine.</span><span class="sxs-lookup"><span data-stu-id="cdaff-153">If you receive a response, the VPN gateway is considered healthy.</span></span> <span data-ttu-id="cdaff-154">Vous ne recevez pas de réponse, cela signifie que la passerelle n’est peut-être pas saine ou qu’un groupe de sécurité réseau sur le sous-réseau de passerelle pose problème.</span><span class="sxs-lookup"><span data-stu-id="cdaff-154">If you don't receive a response, the gateway might not be healthy or an NSG on the gateway subnet is causing the problem.</span></span> <span data-ttu-id="cdaff-155">Voici un exemple de réponse :</span><span class="sxs-lookup"><span data-stu-id="cdaff-155">The following text is a sample response:</span></span>

    <span data-ttu-id="cdaff-156">&lt;?xml version="1.0"?>  <string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">Primary Instance: GatewayTenantWorker_IN_1 GatewayTenantVersion: 14.7.24.6</string&gt;</span><span class="sxs-lookup"><span data-stu-id="cdaff-156">&lt;?xml version="1.0"?>  <string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">Primary Instance: GatewayTenantWorker_IN_1 GatewayTenantVersion: 14.7.24.6</string&gt;</span></span>

### <a name="step-8-check-whether-the-on-premises-vpn-device-has-the-perfect-forward-secrecy-feature-enabled"></a><span data-ttu-id="cdaff-157">Étape 8 :</span><span class="sxs-lookup"><span data-stu-id="cdaff-157">Step 8.</span></span> <span data-ttu-id="cdaff-158">Vérifier l’activation de la fonctionnalité PFS (Perfect Forward Secrecy) sur le périphérique VPN local</span><span class="sxs-lookup"><span data-stu-id="cdaff-158">Check whether the on-premises VPN device has the perfect forward secrecy feature enabled</span></span>

<span data-ttu-id="cdaff-159">La fonctionnalité Perfect Forward Secrecy peut provoquer des problèmes de déconnexion.</span><span class="sxs-lookup"><span data-stu-id="cdaff-159">The perfect forward secrecy feature can cause disconnection problems.</span></span> <span data-ttu-id="cdaff-160">Si la fonctionnalité Perfect Forward Secrecy du périphérique VPN est activée, désactivez-la.</span><span class="sxs-lookup"><span data-stu-id="cdaff-160">If the VPN device has perfect forward secrecy enabled, disable the feature.</span></span> <span data-ttu-id="cdaff-161">Mettez ensuite à jour la stratégie IPsec de la passerelle de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="cdaff-161">Then update the VPN gateway IPsec policy.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cdaff-162">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="cdaff-162">Next steps</span></span>

-   [<span data-ttu-id="cdaff-163">Création d’une connexion de site à site dans le portail Azure</span><span class="sxs-lookup"><span data-stu-id="cdaff-163">Configure a site-to-site connection to a virtual network</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
-   [<span data-ttu-id="cdaff-164">Configurer la stratégie IPsec/IKE pour des connexions VPN S2S ou de réseau virtuel à réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="cdaff-164">Configure an IPsec/IKE policy for site-to-site VPN connections</span></span>](vpn-gateway-ipsecikepolicy-rm-powershell.md)
