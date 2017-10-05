---
title: "Utiliser la passerelle Azure Application Gateway avec équilibreur de charge interne | Microsoft Docs"
description: "Cette page fournit des instructions pour configurer une passerelle Application Gateway Azure avec un point de terminaison d'équilibrage de charge interne"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 7403d28e-909f-46a2-b282-43a8e942f53c
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: d6f3af61934c8c645be1f2c6b4c056fc7ee2e3aa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-application-gateway-with-an-internal-load-balancer-ilb"></a><span data-ttu-id="0a98a-103">Création d'une passerelle Application Gateway avec un équilibrage de charge interne (ILB)</span><span class="sxs-lookup"><span data-stu-id="0a98a-103">Create an Application Gateway with an Internal Load Balancer (ILB)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="0a98a-104">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="0a98a-104">Azure Classic PowerShell</span></span>](application-gateway-ilb.md)
> * [<span data-ttu-id="0a98a-105">Commandes PowerShell pour Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0a98a-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ilb-arm.md)

<span data-ttu-id="0a98a-106">Vous pouvez configurer une passerelle Application Gateway avec une adresse IP virtuelle côté Internet ou avec un point de terminaison interne non exposé à Internet, également appelé point de terminaison d'équilibrage de charge interne (ILB).</span><span class="sxs-lookup"><span data-stu-id="0a98a-106">Application Gateway can be configured with an internet facing virtual IP or with an internal end-point not exposed to the internet, also known as Internal Load Balancer (ILB) endpoint.</span></span> <span data-ttu-id="0a98a-107">La configuration de la passerelle avec un équilibrage de charge interne est utile pour les applications métier internes non exposées à Internet.</span><span class="sxs-lookup"><span data-stu-id="0a98a-107">Configuring the gateway with an ILB is useful for internal line-of-business applications not exposed to internet.</span></span> <span data-ttu-id="0a98a-108">C’est également utile pour les services/niveaux au sein d’une application multiniveau qui se trouve dans une limite de sécurité non exposée à Internet, mais la distribution de charge par tourniquet, l’adhérence de session ou la terminaison SSL sont tout de mêmes requises.</span><span class="sxs-lookup"><span data-stu-id="0a98a-108">It's also useful for services/tiers within a multi-tier application, which sits in a security boundary not exposed to internet, but still require round robin load distribution, session stickiness, or SSL termination.</span></span> <span data-ttu-id="0a98a-109">Cet article vous guidera au cours des étapes de configuration d’une passerelle Application Gateway avec un équilibrage de charge interne.</span><span class="sxs-lookup"><span data-stu-id="0a98a-109">This article walks you through the steps to configure an application gateway with an ILB.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="0a98a-110">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="0a98a-110">Before you begin</span></span>

1. <span data-ttu-id="0a98a-111">Installez la version la plus récente des applets de commande PowerShell Azure à l'aide de Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="0a98a-111">Install latest version of the Azure PowerShell cmdlets using the Web Platform Installer.</span></span> <span data-ttu-id="0a98a-112">Vous pouvez télécharger et installer la dernière version à partir de la section **Windows PowerShell** de la [page Téléchargements](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="0a98a-112">You can download and install the latest version from the **Windows PowerShell** section of the [Download page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="0a98a-113">Vérifiez que vous disposez d'un réseau virtuel qui fonctionne avec un sous-réseau valide.</span><span class="sxs-lookup"><span data-stu-id="0a98a-113">Verify that you have a working virtual network with valid subnet.</span></span>
3. <span data-ttu-id="0a98a-114">Vérifiez que vous disposez de serveurs principaux dans le réseau virtuel ou avec une adresse IP/VIP affectée.</span><span class="sxs-lookup"><span data-stu-id="0a98a-114">Verify that you have backend servers either in the virtual network, or with a public IP/VIP assigned.</span></span>

<span data-ttu-id="0a98a-115">Pour créer une passerelle Application Gateway, exécutez les étapes suivantes dans l'ordre indiqué.</span><span class="sxs-lookup"><span data-stu-id="0a98a-115">To create an application gateway, perform the following steps in the order listed.</span></span> 

1. [<span data-ttu-id="0a98a-116">Créer une passerelle Application Gateway</span><span class="sxs-lookup"><span data-stu-id="0a98a-116">Create an application gateway</span></span>](#create-a-new-application-gateway)
2. [<span data-ttu-id="0a98a-117">Configurer la passerelle</span><span class="sxs-lookup"><span data-stu-id="0a98a-117">Configure the gateway</span></span>](#configure-the-gateway)
3. [<span data-ttu-id="0a98a-118">Définir la configuration de la passerelle</span><span class="sxs-lookup"><span data-stu-id="0a98a-118">Set the gateway configuration</span></span>](#set-the-gateway-configuration)
4. [<span data-ttu-id="0a98a-119">Démarrer la passerelle</span><span class="sxs-lookup"><span data-stu-id="0a98a-119">Start the gateway</span></span>](#start-the-gateway)
5. [<span data-ttu-id="0a98a-120">Vérifier la passerelle</span><span class="sxs-lookup"><span data-stu-id="0a98a-120">Verify the gateway</span></span>](#verify-the-gateway-status)

## <a name="create-an-application-gateway"></a><span data-ttu-id="0a98a-121">Créer une passerelle Application Gateway :</span><span class="sxs-lookup"><span data-stu-id="0a98a-121">Create an application gateway:</span></span>

<span data-ttu-id="0a98a-122">**Pour créer la passerelle**, utilisez l’applet de commande `New-AzureApplicationGateway` en remplaçant les valeurs par les vôtres.</span><span class="sxs-lookup"><span data-stu-id="0a98a-122">**To create the gateway**, use the `New-AzureApplicationGateway` cmdlet, replacing the values with your own.</span></span> <span data-ttu-id="0a98a-123">Notez que la facturation de la passerelle ne démarre pas à ce stade.</span><span class="sxs-lookup"><span data-stu-id="0a98a-123">Note that billing for the gateway does not start at this point.</span></span> <span data-ttu-id="0a98a-124">La facturation commence à une étape ultérieure, lorsque la passerelle a démarré correctement.</span><span class="sxs-lookup"><span data-stu-id="0a98a-124">Billing begins in a later step, when the gateway is successfully started.</span></span>

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

```
VERBOSE: 4:31:35 PM - Begin Operation: New-AzureApplicationGateway 
VERBOSE: 4:32:37 PM - Completed Operation: New-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error 
----       ----------------     ------------                             ----
Successful OK                   55ef0460-825d-2981-ad20-b9a8af41b399
```

<span data-ttu-id="0a98a-125">**Pour valider** la création de la passerelle, vous pouvez utiliser l’applet de commande `Get-AzureApplicationGateway`.</span><span class="sxs-lookup"><span data-stu-id="0a98a-125">**To validate** that the gateway was created, you can use the `Get-AzureApplicationGateway` cmdlet.</span></span> 

<span data-ttu-id="0a98a-126">Dans l’exemple, *Description*, *InstanceCount* et *GatewaySize* sont des paramètres facultatifs.</span><span class="sxs-lookup"><span data-stu-id="0a98a-126">In the sample, *Description*, *InstanceCount*, and *GatewaySize* are optional parameters.</span></span> <span data-ttu-id="0a98a-127">La valeur par défaut pour *InstanceCount* est 2, avec une valeur maximale de 10.</span><span class="sxs-lookup"><span data-stu-id="0a98a-127">The default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="0a98a-128">La valeur par défaut pour *GatewaySize* est Medium.</span><span class="sxs-lookup"><span data-stu-id="0a98a-128">The default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="0a98a-129">Les autres valeurs disponibles sont Small et Large.</span><span class="sxs-lookup"><span data-stu-id="0a98a-129">Small and Large are other available values.</span></span> <span data-ttu-id="0a98a-130">*Vip* et *DnsName* s’affichent sans valeur car la passerelle n’a pas encore démarré.</span><span class="sxs-lookup"><span data-stu-id="0a98a-130">*Vip* and *DnsName* are shown as blank because the gateway has not started yet.</span></span> <span data-ttu-id="0a98a-131">Ces valeurs seront créées une fois la passerelle en cours d'exécution.</span><span class="sxs-lookup"><span data-stu-id="0a98a-131">These are created once the gateway is in the running state.</span></span> 

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 4:39:39 PM - Begin Operation:
Get-AzureApplicationGateway VERBOSE: 4:39:40 PM - Completed 
Operation: Get-AzureApplicationGateway
Name: AppGwTest    
Description: 
VnetName: testvnet1 
Subnets: {Subnet-1} 
InstanceCount: 2 
GatewaySize: Medium 
State: Stopped 
VirtualIPs: 
DnsName:
```

## <a name="configure-the-gateway"></a><span data-ttu-id="0a98a-132">Configurer la passerelle</span><span class="sxs-lookup"><span data-stu-id="0a98a-132">Configure the gateway</span></span>
<span data-ttu-id="0a98a-133">La configuration d'une passerelle Application Gateway se compose de plusieurs valeurs.</span><span class="sxs-lookup"><span data-stu-id="0a98a-133">An application gateway configuration consists of multiple values.</span></span> <span data-ttu-id="0a98a-134">Les valeurs peuvent être liées ensemble pour construire la configuration.</span><span class="sxs-lookup"><span data-stu-id="0a98a-134">The values can be tied together to construct the configuration.</span></span>

<span data-ttu-id="0a98a-135">Les valeurs sont :</span><span class="sxs-lookup"><span data-stu-id="0a98a-135">The values are:</span></span>

* <span data-ttu-id="0a98a-136">**Pool de serveurs principaux :** la liste des adresses IP des serveurs principaux.</span><span class="sxs-lookup"><span data-stu-id="0a98a-136">**Backend server pool:** The list of IP addresses of the backend servers.</span></span> <span data-ttu-id="0a98a-137">Les adresses IP répertoriées doivent appartenir au sous-réseau de réseau virtuel ou elles doivent être une adresse IP/VIP publique.</span><span class="sxs-lookup"><span data-stu-id="0a98a-137">The IP addresses listed should either belong to the VNet subnet, or should be a public IP/VIP.</span></span> 
* <span data-ttu-id="0a98a-138">**Paramètres du pool de serveurs principaux** : chaque pool comporte des paramètres comme le port, le protocole et une affinité basée sur les cookies.</span><span class="sxs-lookup"><span data-stu-id="0a98a-138">**Backend server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="0a98a-139">Ces paramètres sont liés à un pool et sont appliqués à tous les serveurs du pool.</span><span class="sxs-lookup"><span data-stu-id="0a98a-139">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="0a98a-140">**Port frontal :** ce port est le port public ouvert sur la passerelle Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="0a98a-140">**Frontend Port:** This port is the public port opened on the application gateway.</span></span> <span data-ttu-id="0a98a-141">Le trafic atteint ce port, puis il est redirigé vers l'un des serveurs principaux.</span><span class="sxs-lookup"><span data-stu-id="0a98a-141">Traffic hits this port, and then gets redirected to one of the backend servers.</span></span>
* <span data-ttu-id="0a98a-142">**Écouteur :** l'écouteur a un port frontal, un protocole (Http ou Https, sensibles à la casse) et le nom du certificat SSL (en cas de configuration du déchargement SSL).</span><span class="sxs-lookup"><span data-stu-id="0a98a-142">**Listener:** The listener has a frontend port, a protocol (Http or Https, these are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span> 
* <span data-ttu-id="0a98a-143">**Règle** : la règle lie l’écouteur et le pool de serveurs principaux et définit le pool de serveurs principaux vers lequel le trafic doit être dirigé lorsqu’il atteint un écouteur spécifique.</span><span class="sxs-lookup"><span data-stu-id="0a98a-143">**Rule:** The rule binds the listener and the backend server pool and defines which backend server pool the traffic should be directed to when it hits a particular listener.</span></span> <span data-ttu-id="0a98a-144">Actuellement, seule la règle de *base* est prise en charge.</span><span class="sxs-lookup"><span data-stu-id="0a98a-144">Currently, only the *basic* rule is supported.</span></span> <span data-ttu-id="0a98a-145">La règle *basic* est la distribution de charge par tourniquet (round robin).</span><span class="sxs-lookup"><span data-stu-id="0a98a-145">The *basic* rule is round-robin load distribution.</span></span>

<span data-ttu-id="0a98a-146">Vous pouvez construire votre configuration en créant un objet de configuration ou en utilisant un fichier XML de configuration.</span><span class="sxs-lookup"><span data-stu-id="0a98a-146">You can construct your configuration either by creating a configuration object, or by using a configuration XML file.</span></span> <span data-ttu-id="0a98a-147">Pour construire votre configuration à l'aide d'un fichier XML de configuration, utilisez l'exemple ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="0a98a-147">To construct your configuration by using a configuration XML file, use the sample below.</span></span>

<span data-ttu-id="0a98a-148">Notez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="0a98a-148">Note the following:</span></span>

* <span data-ttu-id="0a98a-149">L’élément *FrontendIPConfigurations* décrit les détails de l’équilibrage de charge interne pertinents pour la configuration de la passerelle Application Gateway avec un équilibrage de charge interne.</span><span class="sxs-lookup"><span data-stu-id="0a98a-149">The *FrontendIPConfigurations* element describes the ILB details relevant for configuring Application Gateway with an ILB.</span></span> 
* <span data-ttu-id="0a98a-150">Le paramètre *Type* de l’adresse IP frontale doit présenter la valeur « Private ».</span><span class="sxs-lookup"><span data-stu-id="0a98a-150">The Frontend IP *Type* should be set to 'Private'</span></span>
* <span data-ttu-id="0a98a-151">Le paramètre *StaticIPAddress* doit être défini sur l’adresse IP interne souhaitée sur laquelle la passerelle reçoit le trafic.</span><span class="sxs-lookup"><span data-stu-id="0a98a-151">The *StaticIPAddress* should be set to the desired internal IP on which the gateway receives traffic.</span></span> <span data-ttu-id="0a98a-152">Notez que l’élément *StaticIPAddress* est facultatif.</span><span class="sxs-lookup"><span data-stu-id="0a98a-152">Note that the *StaticIPAddress* element is optional.</span></span> <span data-ttu-id="0a98a-153">S'il n'est pas défini, une adresse IP interne disponible du sous-réseau déployé est choisie.</span><span class="sxs-lookup"><span data-stu-id="0a98a-153">If not set, an available internal IP from the deployed subnet is chosen.</span></span> 
* <span data-ttu-id="0a98a-154">La valeur de l’élément *Name* spécifié dans *FrontendIPConfiguration* doit être utilisée dans l’élément *FrontendIP* de HTTPListener pour faire référence à FrontendIPConfiguration.</span><span class="sxs-lookup"><span data-stu-id="0a98a-154">The value of the *Name* element specified in *FrontendIPConfiguration* should be used in the HTTPListener's *FrontendIP* element to refer to the FrontendIPConfiguration.</span></span>
  
  <span data-ttu-id="0a98a-155">**Exemple de configuration XML**</span><span class="sxs-lookup"><span data-stu-id="0a98a-155">**Configuration XML sample**</span></span>
```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
    <FrontendIPConfigurations>
        <FrontendIPConfiguration>
            <Name>fip1</Name> 
            <Type>Private</Type> 
            <StaticIPAddress>10.0.0.10</StaticIPAddress> 
        </FrontendIPConfiguration>
    </FrontendIPConfigurations>
    <FrontendPorts>
        <FrontendPort>
            <Name>FrontendPort1</Name>
            <Port>80</Port>
        </FrontendPort>
    </FrontendPorts>
    <BackendAddressPools>
        <BackendAddressPool>
            <Name>BackendPool1</Name>
            <IPAddresses>
                <IPAddress>10.0.0.1</IPAddress>
                <IPAddress>10.0.0.2</IPAddress>
            </IPAddresses>
        </BackendAddressPool>
    </BackendAddressPools>
    <BackendHttpSettingsList>
        <BackendHttpSettings>
            <Name>BackendSetting1</Name>
            <Port>80</Port>
            <Protocol>Http</Protocol>
            <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        </BackendHttpSettings>
    </BackendHttpSettingsList>
    <HttpListeners>
        <HttpListener>
            <Name>HTTPListener1</Name>
            <FrontendIP>fip1</FrontendIP>
            <FrontendPort>FrontendPort1</FrontendPort>
            <Protocol>Http</Protocol>
        </HttpListener>
    </HttpListeners>
    <HttpLoadBalancingRules>
        <HttpLoadBalancingRule>
            <Name>HttpLBRule1</Name>
            <Type>basic</Type>
            <BackendHttpSettings>BackendSetting1</BackendHttpSettings>
            <Listener>HTTPListener1</Listener>
            <BackendAddressPool>BackendPool1</BackendAddressPool>
        </HttpLoadBalancingRule>
    </HttpLoadBalancingRules>
</ApplicationGatewayConfiguration>
```


## <a name="set-the-gateway-configuration"></a><span data-ttu-id="0a98a-156">Définir la configuration de la passerelle</span><span class="sxs-lookup"><span data-stu-id="0a98a-156">Set the gateway configuration</span></span>
<span data-ttu-id="0a98a-157">Ensuite, vous allez définir la passerelle Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="0a98a-157">Next, you'll set the application gateway.</span></span> <span data-ttu-id="0a98a-158">Vous pouvez utiliser l’applet de commande `Set-AzureApplicationGatewayConfig` avec un objet de configuration ou avec un fichier XML de configuration.</span><span class="sxs-lookup"><span data-stu-id="0a98a-158">You can use the `Set-AzureApplicationGatewayConfig` cmdlet with a configuration object, or with a configuration XML file.</span></span> 

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -ConfigFile D:\config.xml
```

```
VERBOSE: 7:54:59 PM - Begin Operation: Set-AzureApplicationGatewayConfig 
VERBOSE: 7:55:32 PM - Completed Operation: Set-AzureApplicationGatewayConfig
Name       HTTP Status Code     Operation ID                             Error 
----       ----------------     ------------                             ----
Successful OK                   9b995a09-66fe-2944-8b67-9bb04fcccb9d
```

## <a name="start-the-gateway"></a><span data-ttu-id="0a98a-159">Démarrer la passerelle</span><span class="sxs-lookup"><span data-stu-id="0a98a-159">Start the gateway</span></span>

<span data-ttu-id="0a98a-160">Une fois la passerelle configurée, utilisez l’applet de commande `Start-AzureApplicationGateway` pour démarrer la passerelle.</span><span class="sxs-lookup"><span data-stu-id="0a98a-160">Once the gateway has been configured, use the `Start-AzureApplicationGateway` cmdlet to start the gateway.</span></span> <span data-ttu-id="0a98a-161">La facturation pour une passerelle Application Gateway commence une fois la passerelle démarrée avec succès.</span><span class="sxs-lookup"><span data-stu-id="0a98a-161">Billing for an application gateway begins after the gateway has been successfully started.</span></span> 

> [!NOTE]
> <span data-ttu-id="0a98a-162">La règle `Start-AzureApplicationGateway` peut prendre jusqu’à 15 à 20 minutes.</span><span class="sxs-lookup"><span data-stu-id="0a98a-162">The `Start-AzureApplicationGateway` cmdlet might take up to 15-20 minutes to complete.</span></span> 
> 
> 

```powershell
Start-AzureApplicationGateway AppGwTest 
```

```
VERBOSE: 7:59:16 PM - Begin Operation: Start-AzureApplicationGateway 
VERBOSE: 8:05:52 PM - Completed Operation: Start-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error 
----       ----------------     ------------                             ----
Successful OK                   fc592db8-4c58-2c8e-9a1d-1c97880f0b9b
```

## <a name="verify-the-gateway-status"></a><span data-ttu-id="0a98a-163">Vérifier l'état de la passerelle</span><span class="sxs-lookup"><span data-stu-id="0a98a-163">Verify the gateway status</span></span>

<span data-ttu-id="0a98a-164">Utilisez l’applet de commande `Get-AzureApplicationGateway` pour vérifier l’état de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="0a98a-164">Use the `Get-AzureApplicationGateway` cmdlet to check the status of gateway.</span></span> <span data-ttu-id="0a98a-165">Si `Start-AzureApplicationGateway` a réussi à l’étape précédente, l’état doit être *En cours d’exécution*, et les paramètres Vip et DnsName doivent posséder des entrées valides.</span><span class="sxs-lookup"><span data-stu-id="0a98a-165">If `Start-AzureApplicationGateway` succeeded in the previous step, the State should be *Running*, and the Vip and DnsName should have valid entries.</span></span> <span data-ttu-id="0a98a-166">Cet exemple montre l'applet de commande sur la première ligne, suivie de la sortie.</span><span class="sxs-lookup"><span data-stu-id="0a98a-166">This sample shows the cmdlet on the first line, followed by the output.</span></span> <span data-ttu-id="0a98a-167">Dans cet exemple, la passerelle est en cours d’exécution et prête à prendre le trafic.</span><span class="sxs-lookup"><span data-stu-id="0a98a-167">In this sample, the gateway is running, and is ready to take traffic.</span></span> 

> [!NOTE]
> <span data-ttu-id="0a98a-168">Remarque : la passerelle Application Gateway est configurée pour accepter le trafic sur le point de terminaison de l’équilibrage de charge interne configuré de 10.0.0.10 dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="0a98a-168">The application gateway is configured to accept traffic at the configured ILB endpoint of 10.0.0.10 in this example.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest 
```

```
VERBOSE: 8:09:28 PM - Begin Operation: Get-AzureApplicationGateway 
VERBOSE: 8:09:30 PM - Completed Operation: Get-AzureApplicationGateway
Name          : AppGwTest
Description   : 
VnetName      : testvnet1
Subnets       : {Subnet-1}
InstanceCount : 2
GatewaySize   : Medium
State         : Running
VirtualIPs    : {10.0.0.10}
DnsName       : appgw-b2a11563-2b3a-4172-a4aa-226ee4c23eed.cloudapp.net
```

## <a name="next-steps"></a><span data-ttu-id="0a98a-169">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0a98a-169">Next steps</span></span>
<span data-ttu-id="0a98a-170">Si vous souhaitez plus d'informations sur les options d'équilibrage de charge en général, consultez :</span><span class="sxs-lookup"><span data-stu-id="0a98a-170">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="0a98a-171">Équilibrage de charge Azure</span><span class="sxs-lookup"><span data-stu-id="0a98a-171">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="0a98a-172">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="0a98a-172">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

