---
title: "aaaUsing passerelle d’Application Azure avec équilibrage de charge interne | Documents Microsoft"
description: "Cette page fournit des instructions tooconfigure une passerelle d’Application Azure avec un point de terminaison d’équilibrage de charge interne"
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
ms.openlocfilehash: 272ef84a02f92a8521c35aad6f1d9f9bf1675718
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-with-an-internal-load-balancer-ilb"></a><span data-ttu-id="029e1-103">Création d'une passerelle Application Gateway avec un équilibrage de charge interne (ILB)</span><span class="sxs-lookup"><span data-stu-id="029e1-103">Create an Application Gateway with an Internal Load Balancer (ILB)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="029e1-104">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="029e1-104">Azure Classic PowerShell</span></span>](application-gateway-ilb.md)
> * [<span data-ttu-id="029e1-105">Commandes PowerShell pour Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="029e1-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ilb-arm.md)

<span data-ttu-id="029e1-106">Passerelle d’application peut être configurée avec un ordinateur à adresse IP virtuelle d’internet ou avec un toohello de point de terminaison internes non exposée internet, également appelé point de terminaison équilibreur de charge interne (ILB).</span><span class="sxs-lookup"><span data-stu-id="029e1-106">Application Gateway can be configured with an internet facing virtual IP or with an internal end-point not exposed toohello internet, also known as Internal Load Balancer (ILB) endpoint.</span></span> <span data-ttu-id="029e1-107">Configuration de passerelle hello avec un équilibrage de charge interne est utile pour des applications line-of-business internes ne pas exposées toointernet.</span><span class="sxs-lookup"><span data-stu-id="029e1-107">Configuring hello gateway with an ILB is useful for internal line-of-business applications not exposed toointernet.</span></span> <span data-ttu-id="029e1-108">Il est également utile pour les services/niveaux au sein d’une application à plusieurs niveaux, qui se trouve dans un toointernet n'exposée pas de limite de sécurité, mais nécessitent toujours de répartition de charge de tourniquet (Round Robin), caractère collant de session ou l’arrêt de SSL.</span><span class="sxs-lookup"><span data-stu-id="029e1-108">It's also useful for services/tiers within a multi-tier application, which sits in a security boundary not exposed toointernet, but still require round robin load distribution, session stickiness, or SSL termination.</span></span> <span data-ttu-id="029e1-109">Cet article vous guide tout au long des étapes de hello tooconfigure une passerelle d’application avec un équilibrage de charge interne.</span><span class="sxs-lookup"><span data-stu-id="029e1-109">This article walks you through hello steps tooconfigure an application gateway with an ILB.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="029e1-110">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="029e1-110">Before you begin</span></span>

1. <span data-ttu-id="029e1-111">Installez la version la plus récente des applets de commande PowerShell Azure hello à l’aide de hello Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="029e1-111">Install latest version of hello Azure PowerShell cmdlets using hello Web Platform Installer.</span></span> <span data-ttu-id="029e1-112">Vous pouvez télécharger et installer la version la plus récente hello de hello **Windows PowerShell** section Hello [page de téléchargement](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="029e1-112">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Download page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="029e1-113">Vérifiez que vous disposez d'un réseau virtuel qui fonctionne avec un sous-réseau valide.</span><span class="sxs-lookup"><span data-stu-id="029e1-113">Verify that you have a working virtual network with valid subnet.</span></span>
3. <span data-ttu-id="029e1-114">Vérifiez que vous disposez de serveurs principaux dans le réseau virtuel de hello, ou avec une adresse IP publique/VIP attribué.</span><span class="sxs-lookup"><span data-stu-id="029e1-114">Verify that you have backend servers either in hello virtual network, or with a public IP/VIP assigned.</span></span>

<span data-ttu-id="029e1-115">toocreate une passerelle d’application, effectuez hello comme suit dans l’ordre de hello.</span><span class="sxs-lookup"><span data-stu-id="029e1-115">toocreate an application gateway, perform hello following steps in hello order listed.</span></span> 

1. [<span data-ttu-id="029e1-116">Créer une passerelle Application Gateway</span><span class="sxs-lookup"><span data-stu-id="029e1-116">Create an application gateway</span></span>](#create-a-new-application-gateway)
2. [<span data-ttu-id="029e1-117">Configurer la passerelle de hello</span><span class="sxs-lookup"><span data-stu-id="029e1-117">Configure hello gateway</span></span>](#configure-the-gateway)
3. [<span data-ttu-id="029e1-118">Jeu de configuration de la passerelle hello</span><span class="sxs-lookup"><span data-stu-id="029e1-118">Set hello gateway configuration</span></span>](#set-the-gateway-configuration)
4. [<span data-ttu-id="029e1-119">Démarrer hello passerelle</span><span class="sxs-lookup"><span data-stu-id="029e1-119">Start hello gateway</span></span>](#start-the-gateway)
5. [<span data-ttu-id="029e1-120">Vérifiez que la passerelle de hello</span><span class="sxs-lookup"><span data-stu-id="029e1-120">Verify hello gateway</span></span>](#verify-the-gateway-status)

## <a name="create-an-application-gateway"></a><span data-ttu-id="029e1-121">Créer une passerelle Application Gateway :</span><span class="sxs-lookup"><span data-stu-id="029e1-121">Create an application gateway:</span></span>

<span data-ttu-id="029e1-122">**passerelle de hello toocreate**, utilisez hello `New-AzureApplicationGateway` applet de commande, en remplaçant les valeurs hello par les vôtres.</span><span class="sxs-lookup"><span data-stu-id="029e1-122">**toocreate hello gateway**, use hello `New-AzureApplicationGateway` cmdlet, replacing hello values with your own.</span></span> <span data-ttu-id="029e1-123">Notez que la facturation pour la passerelle de hello ne démarre pas à ce stade.</span><span class="sxs-lookup"><span data-stu-id="029e1-123">Note that billing for hello gateway does not start at this point.</span></span> <span data-ttu-id="029e1-124">La facturation commence dans une étape ultérieure, lorsque la passerelle de hello a démarré correctement.</span><span class="sxs-lookup"><span data-stu-id="029e1-124">Billing begins in a later step, when hello gateway is successfully started.</span></span>

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

<span data-ttu-id="029e1-125">**toovalidate** que passerelle de hello a été créé, vous pouvez utiliser hello `Get-AzureApplicationGateway` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="029e1-125">**toovalidate** that hello gateway was created, you can use hello `Get-AzureApplicationGateway` cmdlet.</span></span> 

<span data-ttu-id="029e1-126">Dans l’exemple hello, *Description*, *InstanceCount*, et *GatewaySize* sont des paramètres facultatifs.</span><span class="sxs-lookup"><span data-stu-id="029e1-126">In hello sample, *Description*, *InstanceCount*, and *GatewaySize* are optional parameters.</span></span> <span data-ttu-id="029e1-127">Hello la valeur par défaut de *InstanceCount* est 2, avec une valeur maximale de 10.</span><span class="sxs-lookup"><span data-stu-id="029e1-127">hello default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="029e1-128">Hello la valeur par défaut de *GatewaySize* est moyenne.</span><span class="sxs-lookup"><span data-stu-id="029e1-128">hello default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="029e1-129">Les autres valeurs disponibles sont Small et Large.</span><span class="sxs-lookup"><span data-stu-id="029e1-129">Small and Large are other available values.</span></span> <span data-ttu-id="029e1-130">*Adresse IP virtuelle* et *DnsName* sont affichés comme vide, car la passerelle de hello n’a pas encore démarré.</span><span class="sxs-lookup"><span data-stu-id="029e1-130">*Vip* and *DnsName* are shown as blank because hello gateway has not started yet.</span></span> <span data-ttu-id="029e1-131">Ceux-ci sont créés une fois la passerelle de hello en hello état en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="029e1-131">These are created once hello gateway is in hello running state.</span></span> 

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

## <a name="configure-hello-gateway"></a><span data-ttu-id="029e1-132">Configurer la passerelle de hello</span><span class="sxs-lookup"><span data-stu-id="029e1-132">Configure hello gateway</span></span>
<span data-ttu-id="029e1-133">La configuration d'une passerelle Application Gateway se compose de plusieurs valeurs.</span><span class="sxs-lookup"><span data-stu-id="029e1-133">An application gateway configuration consists of multiple values.</span></span> <span data-ttu-id="029e1-134">les valeurs Hello peuvent être liées configuration de hello tooconstruct ensemble.</span><span class="sxs-lookup"><span data-stu-id="029e1-134">hello values can be tied together tooconstruct hello configuration.</span></span>

<span data-ttu-id="029e1-135">les valeurs Hello sont :</span><span class="sxs-lookup"><span data-stu-id="029e1-135">hello values are:</span></span>

* <span data-ttu-id="029e1-136">**Pool de serveurs principaux :** liste hello d’adresses IP des serveurs principaux de hello.</span><span class="sxs-lookup"><span data-stu-id="029e1-136">**Backend server pool:** hello list of IP addresses of hello backend servers.</span></span> <span data-ttu-id="029e1-137">adresses IP de Hello répertoriés doivent appartenir soit de sous-réseau de réseau virtuel toohello ou doivent être une adresse IP/VIP publique.</span><span class="sxs-lookup"><span data-stu-id="029e1-137">hello IP addresses listed should either belong toohello VNet subnet, or should be a public IP/VIP.</span></span> 
* <span data-ttu-id="029e1-138">**Paramètres du pool de serveurs principaux** : chaque pool comporte des paramètres comme le port, le protocole et une affinité basée sur les cookies.</span><span class="sxs-lookup"><span data-stu-id="029e1-138">**Backend server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="029e1-139">Ces paramètres sont lié tooa pool et sont des serveurs tooall appliqué dans le pool de hello.</span><span class="sxs-lookup"><span data-stu-id="029e1-139">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="029e1-140">**Port de serveur frontal :** ce port est le port public de hello ouvert sur la passerelle d’application hello.</span><span class="sxs-lookup"><span data-stu-id="029e1-140">**Frontend Port:** This port is hello public port opened on hello application gateway.</span></span> <span data-ttu-id="029e1-141">Le trafic atteint ce port et obtient ensuite redirigé tooone des serveurs principaux de hello.</span><span class="sxs-lookup"><span data-stu-id="029e1-141">Traffic hits this port, and then gets redirected tooone of hello backend servers.</span></span>
* <span data-ttu-id="029e1-142">**Écouteur :** écouteur de hello possède un port de serveur frontal, un protocole (Http ou Https, ils respectent la casse) et le nom du certificat SSL hello (si le déchargement de la configuration de SSL).</span><span class="sxs-lookup"><span data-stu-id="029e1-142">**Listener:** hello listener has a frontend port, a protocol (Http or Https, these are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span> 
* <span data-ttu-id="029e1-143">**La règle :** règle de hello lie le port d’écoute hello et pool de serveurs principaux hello et définit le principal serveur pool hello le trafic doit être dirigée toowhen il atteint un écouteur particulier.</span><span class="sxs-lookup"><span data-stu-id="029e1-143">**Rule:** hello rule binds hello listener and hello backend server pool and defines which backend server pool hello traffic should be directed toowhen it hits a particular listener.</span></span> <span data-ttu-id="029e1-144">Actuellement, seuls hello *base* règle est pris en charge.</span><span class="sxs-lookup"><span data-stu-id="029e1-144">Currently, only hello *basic* rule is supported.</span></span> <span data-ttu-id="029e1-145">Hello *base* règle est la distribution de la charge de tourniquet.</span><span class="sxs-lookup"><span data-stu-id="029e1-145">hello *basic* rule is round-robin load distribution.</span></span>

<span data-ttu-id="029e1-146">Vous pouvez construire votre configuration en créant un objet de configuration ou en utilisant un fichier XML de configuration.</span><span class="sxs-lookup"><span data-stu-id="029e1-146">You can construct your configuration either by creating a configuration object, or by using a configuration XML file.</span></span> <span data-ttu-id="029e1-147">votre configuration à l’aide d’un fichier XML de configuration, l’utilisation hello tooconstruct les exemples ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="029e1-147">tooconstruct your configuration by using a configuration XML file, use hello sample below.</span></span>

<span data-ttu-id="029e1-148">Notez hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="029e1-148">Note hello following:</span></span>

* <span data-ttu-id="029e1-149">Hello *configurations IP frontales adresse* élément décrit en détail équilibrage de charge interne hello pour la configuration de passerelle d’Application avec un équilibrage de charge interne.</span><span class="sxs-lookup"><span data-stu-id="029e1-149">hello *FrontendIPConfigurations* element describes hello ILB details relevant for configuring Application Gateway with an ILB.</span></span> 
* <span data-ttu-id="029e1-150">IP de serveur frontal Hello *Type* doit être défini too'Private'</span><span class="sxs-lookup"><span data-stu-id="029e1-150">hello Frontend IP *Type* should be set too'Private'</span></span>
* <span data-ttu-id="029e1-151">Hello *StaticIPAddress* doit indiquer l’adresse IP interne toohello souhaitée sur le hello passerelle reçoit le trafic.</span><span class="sxs-lookup"><span data-stu-id="029e1-151">hello *StaticIPAddress* should be set toohello desired internal IP on which hello gateway receives traffic.</span></span> <span data-ttu-id="029e1-152">Notez que hello *StaticIPAddress* élément est facultatif.</span><span class="sxs-lookup"><span data-stu-id="029e1-152">Note that hello *StaticIPAddress* element is optional.</span></span> <span data-ttu-id="029e1-153">Si ce n’est pas le cas, ensemble, une adresse IP interne disponible à partir du sous-réseau de hello déployé est choisie.</span><span class="sxs-lookup"><span data-stu-id="029e1-153">If not set, an available internal IP from hello deployed subnet is chosen.</span></span> 
* <span data-ttu-id="029e1-154">Hello valeur Hello *nom* élément spécifié dans *configuration IP frontale* doit être utilisé dans hello HTTPListener *FrontendIP* élément toorefer toohello Configuration IP frontale.</span><span class="sxs-lookup"><span data-stu-id="029e1-154">hello value of hello *Name* element specified in *FrontendIPConfiguration* should be used in hello HTTPListener's *FrontendIP* element toorefer toohello FrontendIPConfiguration.</span></span>
  
  <span data-ttu-id="029e1-155">**Exemple de configuration XML**</span><span class="sxs-lookup"><span data-stu-id="029e1-155">**Configuration XML sample**</span></span>
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


## <a name="set-hello-gateway-configuration"></a><span data-ttu-id="029e1-156">Jeu de configuration de la passerelle hello</span><span class="sxs-lookup"><span data-stu-id="029e1-156">Set hello gateway configuration</span></span>
<span data-ttu-id="029e1-157">Ensuite, vous allez définir la passerelle d’application hello.</span><span class="sxs-lookup"><span data-stu-id="029e1-157">Next, you'll set hello application gateway.</span></span> <span data-ttu-id="029e1-158">Vous pouvez utiliser hello `Set-AzureApplicationGatewayConfig` applet de commande avec un objet de configuration, ou avec un fichier XML de configuration.</span><span class="sxs-lookup"><span data-stu-id="029e1-158">You can use hello `Set-AzureApplicationGatewayConfig` cmdlet with a configuration object, or with a configuration XML file.</span></span> 

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

## <a name="start-hello-gateway"></a><span data-ttu-id="029e1-159">Démarrer hello passerelle</span><span class="sxs-lookup"><span data-stu-id="029e1-159">Start hello gateway</span></span>

<span data-ttu-id="029e1-160">Une fois que la passerelle de hello a été configurée, utilisez hello `Start-AzureApplicationGateway` passerelle de hello toostart applet de commande.</span><span class="sxs-lookup"><span data-stu-id="029e1-160">Once hello gateway has been configured, use hello `Start-AzureApplicationGateway` cmdlet toostart hello gateway.</span></span> <span data-ttu-id="029e1-161">Le coût d’une passerelle d’application commence une fois la passerelle de hello a démarré.</span><span class="sxs-lookup"><span data-stu-id="029e1-161">Billing for an application gateway begins after hello gateway has been successfully started.</span></span> 

> [!NOTE]
> <span data-ttu-id="029e1-162">Hello `Start-AzureApplicationGateway` applet de commande peut prendre les toocomplete too15 à 20 minutes.</span><span class="sxs-lookup"><span data-stu-id="029e1-162">hello `Start-AzureApplicationGateway` cmdlet might take up too15-20 minutes toocomplete.</span></span> 
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

## <a name="verify-hello-gateway-status"></a><span data-ttu-id="029e1-163">Vérifiez l’état de la passerelle hello</span><span class="sxs-lookup"><span data-stu-id="029e1-163">Verify hello gateway status</span></span>

<span data-ttu-id="029e1-164">Hello d’utilisation `Get-AzureApplicationGateway` état de hello toocheck applet de commande de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="029e1-164">Use hello `Get-AzureApplicationGateway` cmdlet toocheck hello status of gateway.</span></span> <span data-ttu-id="029e1-165">Si `Start-AzureApplicationGateway` a réussi à l’étape précédente de hello, hello état doit être *en cours d’exécution*, hello Vip et DnsName doit avoir des entrées valides.</span><span class="sxs-lookup"><span data-stu-id="029e1-165">If `Start-AzureApplicationGateway` succeeded in hello previous step, hello State should be *Running*, and hello Vip and DnsName should have valid entries.</span></span> <span data-ttu-id="029e1-166">Cet exemple montre l’applet de commande hello sur la première ligne de hello, suivi par la sortie hello.</span><span class="sxs-lookup"><span data-stu-id="029e1-166">This sample shows hello cmdlet on hello first line, followed by hello output.</span></span> <span data-ttu-id="029e1-167">Dans cet exemple, la passerelle de hello est en cours d’exécution et correspond au trafic tootake prêt.</span><span class="sxs-lookup"><span data-stu-id="029e1-167">In this sample, hello gateway is running, and is ready tootake traffic.</span></span> 

> [!NOTE]
> <span data-ttu-id="029e1-168">configuration de la passerelle application Hello trafic tooaccept à hello configuré le point de terminaison d’équilibrage de charge interne de 10.0.0.10 dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="029e1-168">hello application gateway is configured tooaccept traffic at hello configured ILB endpoint of 10.0.0.10 in this example.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="029e1-169">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="029e1-169">Next steps</span></span>
<span data-ttu-id="029e1-170">Si vous souhaitez plus d'informations sur les options d'équilibrage de charge en général, consultez :</span><span class="sxs-lookup"><span data-stu-id="029e1-170">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="029e1-171">Équilibrage de charge Azure</span><span class="sxs-lookup"><span data-stu-id="029e1-171">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="029e1-172">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="029e1-172">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

