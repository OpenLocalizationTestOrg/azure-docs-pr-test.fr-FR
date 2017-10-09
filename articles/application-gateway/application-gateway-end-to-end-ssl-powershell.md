---
title: "aaaConfigure fin tooend SSL avec la passerelle d’Application Azure | Documents Microsoft"
description: "Cet article décrit comment tooconfigure fin tooend SSL avec la passerelle d’Application à l’aide de PowerShell du Gestionnaire de ressources Azure"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: e6d80a33-4047-4538-8c83-e88876c8834e
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: gwallace
ms.openlocfilehash: 7c280478e143d309e7665219441cbee8c81d9a80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-end-tooend-ssl-with-application-gateway-using-powershell"></a><span data-ttu-id="c5e8e-103">Configurer fin tooend SSL avec la passerelle d’Application à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="c5e8e-103">Configure end tooend SSL with Application Gateway using PowerShell</span></span>

## <a name="overview"></a><span data-ttu-id="c5e8e-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="c5e8e-104">Overview</span></span>

<span data-ttu-id="c5e8e-105">Prend en charge l’application passerelle fin tooend le chiffrement du trafic.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-105">Application Gateway supports end tooend encryption of traffic.</span></span> <span data-ttu-id="c5e8e-106">Pour cela, passerelle d’application termine la connexion SSL de hello au niveau de la passerelle d’application hello.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-106">Application Gateway does this by terminating hello SSL connection at hello application gateway.</span></span> <span data-ttu-id="c5e8e-107">passerelle de Hello applique ensuite des règles de routage hello toohello trafic, rechiffre les paquets hello et transfère hello principal paquet toohello approprié en fonction des règles de routage hello définis.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-107">hello gateway then applies hello routing rules toohello traffic, re-encrypts hello packet, and forwards hello packet toohello appropriate backend based on hello routing rules defined.</span></span> <span data-ttu-id="c5e8e-108">Une réponse de serveur web de hello traverse hello même processus utilisateur toohello précédent.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-108">Any response from hello web server goes through hello same process back toohello end user.</span></span>

<span data-ttu-id="c5e8e-109">La passerelle Application Gateway prend également en charge la définition d’options SSL personnalisées.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-109">Another feature that application gateway supports defining custom SSL options.</span></span> <span data-ttu-id="c5e8e-110">Passerelle d’application prend en charge la désactivation hello suivant la version de protocole ; **TLSv1.0**, **TLSv1.1**, et **TLSv1.2** ainsi définir hello suites toouse et hello l’ordre de préférence de chiffrement.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-110">Application Gateway supports disabling hello following protocol version; **TLSv1.0**, **TLSv1.1**, and **TLSv1.2** as well defining hello which cipher suites toouse and hello order of preference.</span></span>  <span data-ttu-id="c5e8e-111">toolearn savoir plus sur les options SSL configurables, visitez [vue d’ensemble de la stratégie SSL](application-gateway-SSL-policy-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c5e8e-111">toolearn more about configurable SSL options, visit [SSL Policy overview](application-gateway-SSL-policy-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="c5e8e-112">SSL 2.0 et SSL 3.0 sont désactivés par défaut et ne peuvent pas être activés.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-112">SSL 2.0 and SSL 3.0 are disabled by default and cannot be enabled.</span></span> <span data-ttu-id="c5e8e-113">Ils sont considérés comme non sécurisées et ne sont pas en mesure de toobe utilisé avec la passerelle d’Application.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-113">They are considered unsecure and are not able toobe used with Application Gateway.</span></span>

![image du scénario][scenario]

## <a name="scenario"></a><span data-ttu-id="c5e8e-115">Scénario</span><span class="sxs-lookup"><span data-stu-id="c5e8e-115">Scenario</span></span>

<span data-ttu-id="c5e8e-116">Dans ce scénario, vous apprendrez comment toocreate une passerelle d’application à l’aide de fin tooend SSL à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-116">In this scenario, you learn how toocreate an application gateway using end tooend SSL using PowerShell.</span></span>

<span data-ttu-id="c5e8e-117">Ce scénario va :</span><span class="sxs-lookup"><span data-stu-id="c5e8e-117">This scenario will:</span></span>

* <span data-ttu-id="c5e8e-118">créer un groupe de ressources nommé **appgw-rg** ;</span><span class="sxs-lookup"><span data-stu-id="c5e8e-118">Create a resource group named **appgw-rg**</span></span>
* <span data-ttu-id="c5e8e-119">créer un réseau virtuel nommé **appgwvnet** avec un espace d’adresse de 10.0.0.0/16 ;</span><span class="sxs-lookup"><span data-stu-id="c5e8e-119">Create a virtual network named **appgwvnet** with an address space of 10.0.0.0/16.</span></span>
* <span data-ttu-id="c5e8e-120">créer deux sous-réseaux appelés **appgwsubnet** et **appsubnet** ;</span><span class="sxs-lookup"><span data-stu-id="c5e8e-120">Create two subnets called **appgwsubnet** and **appsubnet**.</span></span>
* <span data-ttu-id="c5e8e-121">Créer un petite application passerelle prise en charge fin tooend le chiffrement SSL qui limite les versions de protocoles SSL et des suites de chiffrement.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-121">Create a small application gateway supporting end tooend SSL encryption that limits SSL protocols versions and cipher suites.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="c5e8e-122">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="c5e8e-122">Before you begin</span></span>

<span data-ttu-id="c5e8e-123">tooconfigure fin tooend SSL avec une passerelle d’application, un certificat est requis pour la passerelle de hello et les certificats sont requis pour les serveurs principaux de hello.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-123">tooconfigure end tooend SSL with an application gateway, a certificate is required for hello gateway and certificates are required for hello backend servers.</span></span> <span data-ttu-id="c5e8e-124">certificat de passerelle Hello est utilisé tooencrypt et decrypt hello le trafic envoyé tooit à l’aide de SSL.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-124">hello gateway certificate is used tooencrypt and decrypt hello traffic sent tooit using SSL.</span></span> <span data-ttu-id="c5e8e-125">certificat de passerelle Hello doit toobe au format d’échange d’informations personnelles (pfx).</span><span class="sxs-lookup"><span data-stu-id="c5e8e-125">hello gateway certificate needs toobe in Personal Information Exchange (pfx) format.</span></span> <span data-ttu-id="c5e8e-126">Ce format de fichier permet hello privé toobe clé exporté requis par hello application passerelle tooperform hello chiffrement et de déchiffrement du trafic.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-126">This file format allows for hello private key toobe exported which is required by hello application gateway tooperform hello encryption and decryption of traffic.</span></span>

<span data-ttu-id="c5e8e-127">Pour l’end tooend SSL chiffrement hello principal doit être dans la liste approuvée avec la passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-127">For end tooend SSL encryption hello backend must be whitelisted with application gateway.</span></span> <span data-ttu-id="c5e8e-128">Pour cela, vous devez téléchargement hello le certificat public de la passerelle d’application toohello hello les serveurs principaux.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-128">This is done by uploading hello public certificate of hello backends toohello application gateway.</span></span> <span data-ttu-id="c5e8e-129">Cela garantit que cette passerelle d’application hello communique uniquement avec des instances de principal connu.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-129">This ensures that hello application gateway only communicates with known backend instances.</span></span> <span data-ttu-id="c5e8e-130">Cela permet de sécuriser davantage hello fin tooend de communication.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-130">This further secures hello end tooend communication.</span></span>

<span data-ttu-id="c5e8e-131">Ce processus est décrit dans hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="c5e8e-131">This process is described in hello following steps:</span></span>

## <a name="create-hello-resource-group"></a><span data-ttu-id="c5e8e-132">Créer hello groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="c5e8e-132">Create hello Resource Group</span></span>

<span data-ttu-id="c5e8e-133">Cette section vous guide tout au long de la création d’un groupe de ressources, qui contient la passerelle d’application hello.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-133">This section walks you through creating a resource group, that contains hello application gateway.</span></span>

### <a name="step-1"></a><span data-ttu-id="c5e8e-134">Étape 1</span><span class="sxs-lookup"><span data-stu-id="c5e8e-134">Step 1</span></span>

<span data-ttu-id="c5e8e-135">Ouvrez une session dans tooyour compte Azure.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-135">Log in tooyour Azure Account.</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a><span data-ttu-id="c5e8e-136">Étape 2</span><span class="sxs-lookup"><span data-stu-id="c5e8e-136">Step 2</span></span>

<span data-ttu-id="c5e8e-137">Sélectionnez toouse d’abonnement hello pour ce scénario.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-137">Select hello subscription toouse for this scenario.</span></span>

```powershell
Select-AzureRmsubscription -SubscriptionName "<Subscription name>"
```

### <a name="step-3"></a><span data-ttu-id="c5e8e-138">Étape 3 :</span><span class="sxs-lookup"><span data-stu-id="c5e8e-138">Step 3</span></span>

<span data-ttu-id="c5e8e-139">Créez un groupe de ressources (ignorez cette étape si vous utilisez un groupe de ressources existant).</span><span class="sxs-lookup"><span data-stu-id="c5e8e-139">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a><span data-ttu-id="c5e8e-140">Créer un réseau virtuel et un sous-réseau pour la passerelle d’application hello</span><span class="sxs-lookup"><span data-stu-id="c5e8e-140">Create a virtual network and a subnet for hello application gateway</span></span>

<span data-ttu-id="c5e8e-141">Hello exemple suivant crée un réseau virtuel et deux sous-réseaux.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-141">hello following example creates a virtual network and two subnets.</span></span> <span data-ttu-id="c5e8e-142">Un sous-réseau est la passerelle d’application hello toohold utilisé.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-142">One subnet is used toohold hello application gateway.</span></span> <span data-ttu-id="c5e8e-143">Hello autre sous-réseau est utilisé pour hello les serveurs principaux hello web l’application d’hébergement.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-143">hello other subnet is used for hello backends hosting hello web application.</span></span>

### <a name="step-1"></a><span data-ttu-id="c5e8e-144">Étape 1</span><span class="sxs-lookup"><span data-stu-id="c5e8e-144">Step 1</span></span>

<span data-ttu-id="c5e8e-145">Affecter une plage d’adresses pour les sous-réseaux hello être utilisé pour hello passerelle d’Application lui-même.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-145">Assign an address range for hello subnet be used for hello Application Gateway itself.</span></span>

```powershell
$gwSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -AddressPrefix 10.0.0.0/24
```

> [!NOTE]
> <span data-ttu-id="c5e8e-146">Les sous-réseaux configurés pour la passerelle d’application doivent être correctement dimensionnés.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-146">Subnets configured for application gateway should be properly sized.</span></span> <span data-ttu-id="c5e8e-147">Une passerelle d’application peut être configurée pour des instances de too10.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-147">An application gateway can be configured for up too10 instances.</span></span> <span data-ttu-id="c5e8e-148">Chaque instance est une adresse IP du sous-réseau de hello.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-148">Each instance takes one IP address from hello subnet.</span></span> <span data-ttu-id="c5e8e-149">Un sous-réseau trop petit peut nuire à la montée en charge d’une passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-149">Too small of a subnet can adversely affect scaling out an application gateway.</span></span>
> 
> 

### <a name="step-2"></a><span data-ttu-id="c5e8e-150">Étape 2</span><span class="sxs-lookup"><span data-stu-id="c5e8e-150">Step 2</span></span>

<span data-ttu-id="c5e8e-151">Affecter un toobe de plage d’adresse utilisé pour hello pool d’adresses principales.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-151">Assign an address range toobe used for hello Backend address pool.</span></span>

```powershell
$nicSubnet = New-AzureRmVirtualNetworkSubnetConfig  -Name 'appsubnet' -AddressPrefix 10.0.2.0/24
```

### <a name="step-3"></a><span data-ttu-id="c5e8e-152">Étape 3 :</span><span class="sxs-lookup"><span data-stu-id="c5e8e-152">Step 3</span></span>

<span data-ttu-id="c5e8e-153">Créez un réseau virtuel avec les sous-réseaux hello définis dans les étapes précédentes de hello.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-153">Create a virtual network with hello subnets defined in hello preceding steps.</span></span>

```powershell
$vnet = New-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $gwSubnet, $nicSubnet
```

### <a name="step-4"></a><span data-ttu-id="c5e8e-154">Étape 4</span><span class="sxs-lookup"><span data-stu-id="c5e8e-154">Step 4</span></span>

<span data-ttu-id="c5e8e-155">Récupérer hello réseau virtuel ressource et le sous-réseau ressources toobe utilisé Bonjour comme suit :</span><span class="sxs-lookup"><span data-stu-id="c5e8e-155">Retrieve hello virtual network resource and subnet resources toobe used in hello following steps:</span></span>

```powershell
$vnet = Get-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg
$gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -VirtualNetwork $vnet
$nicSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'appsubnet' -VirtualNetwork $vnet
```

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a><span data-ttu-id="c5e8e-156">Créer une adresse IP publique pour la configuration frontale de hello</span><span class="sxs-lookup"><span data-stu-id="c5e8e-156">Create a public IP address for hello front-end configuration</span></span>

<span data-ttu-id="c5e8e-157">Créer un toobe de ressource IP publique utilisée pour la passerelle d’application hello.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-157">Create a public IP resource toobe used for hello application gateway.</span></span> <span data-ttu-id="c5e8e-158">Cette adresse IP publique est utilisée dans une prochaine étape.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-158">This public IP address is used a following step.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -Name 'publicIP01' -Location "West US" -AllocationMethod Dynamic
```

> [!IMPORTANT]
> <span data-ttu-id="c5e8e-159">Passerelle d’application ne prend pas en charge hello une adresse IP publique créée avec un nom de domaine défini.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-159">Application Gateway does not support hello use of a public IP address created with a domain label defined.</span></span> <span data-ttu-id="c5e8e-160">Seule une adresse IP publique avec un nom de domaine créé dynamiquement est prise en charge.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-160">Only a public IP address with a dynamically created domain label is supported.</span></span> <span data-ttu-id="c5e8e-161">Si vous avez besoin d’un nom convivial dns pour la passerelle d’application hello, il est recommandé de toouse un enregistrement CNAME enregistrer en tant qu’alias.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-161">If you require a friendly dns name for hello application gateway, it is recommended toouse a CNAME record as an alias.</span></span>

## <a name="create-an-application-gateway-configuration-object"></a><span data-ttu-id="c5e8e-162">Créer un objet de configuration de passerelle Application Gateway</span><span class="sxs-lookup"><span data-stu-id="c5e8e-162">Create an application gateway configuration object</span></span>

<span data-ttu-id="c5e8e-163">Tous les éléments de configuration sont définies avant de créer la passerelle d’application hello.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-163">All configuration items are set before creating hello application gateway.</span></span> <span data-ttu-id="c5e8e-164">Hello étapes suivantes créent hello des éléments de configuration qui sont nécessaires pour une ressource de passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-164">hello following steps create hello configuration items that are needed for an application gateway resource.</span></span>

### <a name="step-1"></a><span data-ttu-id="c5e8e-165">Étape 1</span><span class="sxs-lookup"><span data-stu-id="c5e8e-165">Step 1</span></span>

<span data-ttu-id="c5e8e-166">Créer une configuration IP de passerelle l’application, ce paramètre détermine quel sous-réseau hello application passerelle utilise.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-166">Create an application gateway IP configuration, this setting configures what subnet hello application gateway uses.</span></span> <span data-ttu-id="c5e8e-167">Au démarrage de la passerelle d’application, il récupère une adresse IP du sous-réseau hello configuré et achemine les adresses IP de réseau du trafic toohello dans le pool d’adresses IP hello back-end.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-167">When application gateway starts, it picks up an IP address from hello subnet configured and routes network traffic toohello IP addresses in hello back-end IP pool.</span></span> <span data-ttu-id="c5e8e-168">Gardez à l’esprit que chaque instance utilise une adresse IP unique.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-168">Keep in mind that each instance takes one IP address.</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name 'gwconfig' -Subnet $gwSubnet
```

### <a name="step-2"></a><span data-ttu-id="c5e8e-169">Étape 2</span><span class="sxs-lookup"><span data-stu-id="c5e8e-169">Step 2</span></span>

<span data-ttu-id="c5e8e-170">Créer une configuration IP frontale, ce paramètre est mappé à un ip privé ou public adresse toohello frontal de la passerelle d’application hello.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-170">Create a front-end IP configuration, this setting maps a private or public ip address toohello front end of hello application gateway.</span></span> <span data-ttu-id="c5e8e-171">Hello suivant l’étape associe l’adresse IP publique de hello Bonjour précédant l’étape de configuration IP frontale de hello.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-171">hello following step associates hello public IP address in hello preceding step with hello front-end IP configuration.</span></span>

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name 'fip01' -PublicIPAddress $publicip
```

### <a name="step-3"></a><span data-ttu-id="c5e8e-172">Étape 3 :</span><span class="sxs-lookup"><span data-stu-id="c5e8e-172">Step 3</span></span>

<span data-ttu-id="c5e8e-173">Configurer un pool d’adresses IP hello principal avec des adresses IP hello des serveurs web de principaux hello.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-173">Configure hello back-end IP address pool with hello IP addresses of hello backend web servers.</span></span> <span data-ttu-id="c5e8e-174">Ces adresses IP sont des adresses IP hello qui reçoivent le trafic réseau hello qui provient d’un point de terminaison IP frontale hello.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-174">These IP addresses are hello IP addresses that receive hello network traffic that comes from hello front-end IP endpoint.</span></span> <span data-ttu-id="c5e8e-175">Vous remplacez hello suivant tooadd d’adresses IP de vos propres points de terminaison application IP adresse.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-175">You replace hello following IP addresses tooadd your own application IP address endpoints.</span></span>

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name 'pool01' -BackendIPAddresses 1.1.1.1, 2.2.2.2, 3.3.3.3
```

> [!NOTE]
> <span data-ttu-id="c5e8e-176">Un nom de domaine complet (FQDN) est également une valeur valide à la place d’une adresse ip pour les serveurs principaux de hello à l’aide du commutateur - BackendFqdns de hello.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-176">A fully qualified domain name (FQDN) is also a valid value in place of an ip address for hello backend servers by using hello -BackendFqdns switch.</span></span> 

### <a name="step-4"></a><span data-ttu-id="c5e8e-177">Étape 4</span><span class="sxs-lookup"><span data-stu-id="c5e8e-177">Step 4</span></span>

<span data-ttu-id="c5e8e-178">Configurer les ports IP front-end hello pour le point de terminaison IP public hello.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-178">Configure hello front-end IP port for hello public IP endpoint.</span></span> <span data-ttu-id="c5e8e-179">Ce port est le port hello qui les utilisateurs finaux se connectent à.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-179">This port is hello port that end users connect to.</span></span>

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name 'port01'  -Port 443
```

### <a name="step-5"></a><span data-ttu-id="c5e8e-180">Étape 5</span><span class="sxs-lookup"><span data-stu-id="c5e8e-180">Step 5</span></span>

<span data-ttu-id="c5e8e-181">Configurer le certificat hello pour la passerelle d’application hello.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-181">Configure hello certificate for hello application gateway.</span></span> <span data-ttu-id="c5e8e-182">Ce certificat est utilisé toodecrypt et rechiffrez le trafic sur la passerelle d’application hello hello.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-182">This certificate is used toodecrypt and re-encrypt hello traffic on hello application gateway.</span></span>

```powershell
$cert = New-AzureRmApplicationGatewaySSLCertificate -Name cert01 -CertificateFile <full path too.pfx file> -Password <password for certificate file>
```

> [!NOTE]
> <span data-ttu-id="c5e8e-183">Cet exemple configure un certificat hello utilisée pour la connexion SSL.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-183">This sample configures hello certificate used for SSL connection.</span></span> <span data-ttu-id="c5e8e-184">certificat de Hello doit toobe au format .pfx et hello le mot de passe doit être comprise entre 4 too12 caractères.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-184">hello certificate needs toobe in .pfx format, and hello password must be between 4 too12 characters.</span></span>

### <a name="step-6"></a><span data-ttu-id="c5e8e-185">Étape 6</span><span class="sxs-lookup"><span data-stu-id="c5e8e-185">Step 6</span></span>

<span data-ttu-id="c5e8e-186">Créer l’écouteur HTTP pour la passerelle d’application hello hello.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-186">Create hello HTTP listener for hello application gateway.</span></span> <span data-ttu-id="c5e8e-187">Affecter la configuration ip frontale de hello, le port et toouse du certificat SSL.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-187">Assign hello front-end ip configuration, port, and SSL certificate toouse.</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SSLCertificate $cert
```

### <a name="step-7"></a><span data-ttu-id="c5e8e-188">Étape 7</span><span class="sxs-lookup"><span data-stu-id="c5e8e-188">Step 7</span></span>

<span data-ttu-id="c5e8e-189">Téléchargez le certificat hello toobe utilisé sur hello SSL activé principal des ressources.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-189">Upload hello certificate toobe used on hello SSL enabled backend pool resources.</span></span>

> [!NOTE]
> <span data-ttu-id="c5e8e-190">Sonde Hello Obtient la clé publique de hello de hello **par défaut** liaison SSL sur hello d’adresse IP de fin-back et compare hello valeur de clé publique qu’il reçoit la valeur de clé publique de toohello vous fournissez ici.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-190">hello default probe gets hello public key from hello **default** SSL binding on hello back-end's IP address and compares hello public key value it receives toohello public key value you provide here.</span></span> <span data-ttu-id="c5e8e-191">Hello récupérées de clé publique peut ne pas être flux de trafic hello destiné site toowhich **si** vous utilisez SNI et les en-têtes d’hôtes sur hello back-end.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-191">hello retrieved public key may not necessarily be hello intended site toowhich traffic flows **if** you are using host headers and SNI on hello back-end.</span></span> <span data-ttu-id="c5e8e-192">En cas de doute, visitez https://127.0.0.1/ sur tooconfirm de back end hello quel certificat est utilisé pour hello **par défaut** liaison SSL.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-192">If in doubt, visit https://127.0.0.1/ on hello back-ends tooconfirm which certificate is used for hello **default** SSL binding.</span></span> <span data-ttu-id="c5e8e-193">Utilisez la clé publique de hello à partir de cette demande dans cette section.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-193">Use hello public key from that request in this section.</span></span> <span data-ttu-id="c5e8e-194">Si vous utilisez des en-têtes d’hôte et SNI sur les liaisons HTTPS et vous ne recevez pas une réponse et un certificat à partir d’un navigateur manuel demande toohttps://127.0.0.1/ sur hello principaux, vous devez configurer une liaison SSL de valeur par défaut sur les systèmes principaux hello.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-194">If you are using host-headers and SNI on HTTPS bindings and you do not receive a response and certificate from a manual browser request toohttps://127.0.0.1/ on hello back-ends, you must set up a default SSL binding on hello back-ends.</span></span> <span data-ttu-id="c5e8e-195">Si vous ne le faites pas, l’échec de sondes et hello principal n’est pas dans la liste approuvée.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-195">If you do not do so, probes fail and hello back-end is not whitelisted.</span></span>

```powershell
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name 'whitelistcert1' -CertificateFile C:\users\gwallace\Desktop\cert.cer
```

> [!NOTE]
> <span data-ttu-id="c5e8e-196">certificat de Hello fourni dans cette étape doit être hello de clé publique cert de pfx hello présent sur hello principal.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-196">hello certificate provided in this step should be hello public key of hello pfx cert present on hello backend.</span></span> <span data-ttu-id="c5e8e-197">Exporter hello certificat (pas hello racine) installé sur le serveur principal de hello dans. CER mettre en forme et l’utiliser dans cette étape.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-197">Export hello certificate (not hello root certificate) installed on hello backend server in .CER format and use it in this step.</span></span> <span data-ttu-id="c5e8e-198">Cette étape de blocage hello principal avec la passerelle d’application hello.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-198">This step whitelists hello backend with hello application gateway.</span></span>

### <a name="step-8"></a><span data-ttu-id="c5e8e-199">Étape 8</span><span class="sxs-lookup"><span data-stu-id="c5e8e-199">Step 8</span></span>

<span data-ttu-id="c5e8e-200">Configurer les paramètres de hello application passerelle http du serveur principal.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-200">Configure hello application gateway back-end http settings.</span></span> <span data-ttu-id="c5e8e-201">Attribuer certificat hello téléchargé Bonjour précédant les paramètres d’étape toohello http.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-201">Assign hello certificate uploaded in hello preceding step toohello http settings.</span></span>

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name 'setting01' -Port 443 -Protocol Https -CookieBasedAffinity Enabled -AuthenticationCertificates $authcert
```

### <a name="step-9"></a><span data-ttu-id="c5e8e-202">Étape 9</span><span class="sxs-lookup"><span data-stu-id="c5e8e-202">Step 9</span></span>

<span data-ttu-id="c5e8e-203">Créer une règle de routage de l’équilibreur de charge qui configure le comportement de programme d’équilibrage de charge hello.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-203">Create a load balancer routing rule that configures hello load balancer behavior.</span></span> <span data-ttu-id="c5e8e-204">Dans cet exemple, une simple règle de type tourniquet (round robin) est créée.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-204">In this example, a basic round robin rule is created.</span></span>

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name 'rule01' -RuleType basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

### <a name="step-10"></a><span data-ttu-id="c5e8e-205">Étape 10</span><span class="sxs-lookup"><span data-stu-id="c5e8e-205">Step 10</span></span>

<span data-ttu-id="c5e8e-206">Configurer la taille de l’instance de la passerelle d’application hello hello.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-206">Configure hello instance size of hello application gateway.</span></span>  <span data-ttu-id="c5e8e-207">les tailles disponibles Hello sont **Standard\_petit**, **Standard\_support**, et **Standard\_grande**.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-207">hello available sizes are **Standard\_Small**, **Standard\_Medium**, and **Standard\_Large**.</span></span>  <span data-ttu-id="c5e8e-208">De la capacité, les valeurs disponibles hello vont de 1 à 10.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-208">For capacity, hello available values are 1 through 10.</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

> [!NOTE]
> <span data-ttu-id="c5e8e-209">Vous pouvez choisir un nombre d’instances de 1 à des fins de test.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-209">An instance count of 1 can be chosen for testing purposes.</span></span> <span data-ttu-id="c5e8e-210">Il est important que n’importe quelle instance compte dans les deux instances de tooknow n’est pas couverte par un contrat SLA de hello et ne sont donc pas recommandée.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-210">It is important tooknow that any instance count under two instances is not covered by hello SLA and are therefore not recommended.</span></span> <span data-ttu-id="c5e8e-211">Les passerelles Small sont toobe utilisé pour le développement de test et non à des fins de production.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-211">Small gateways are toobe used for dev test and not for production purposes.</span></span>

### <a name="step-11"></a><span data-ttu-id="c5e8e-212">Étape 11</span><span class="sxs-lookup"><span data-stu-id="c5e8e-212">Step 11</span></span>

<span data-ttu-id="c5e8e-213">Configurer toobe de stratégie SSL hello utilisé sur hello passerelle d’Application.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-213">Configure hello SSL policy toobe used on hello Application Gateway.</span></span> <span data-ttu-id="c5e8e-214">Passerelle d’application prend en charge hello capacité tooset une version minimale pour les versions du protocole SSL.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-214">Application Gateway supports hello ability tooset a minimum version for SSL protocol versions.</span></span>

<span data-ttu-id="c5e8e-215">Hello les valeurs suivantes sont une liste des versions de protocole qui peuvent être définis.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-215">hello following values are a list of protocol versions that can be defined.</span></span>

* <span data-ttu-id="c5e8e-216">**TLSv1_0**</span><span class="sxs-lookup"><span data-stu-id="c5e8e-216">**TLSv1_0**</span></span>
* <span data-ttu-id="c5e8e-217">**TLSv1_1**</span><span class="sxs-lookup"><span data-stu-id="c5e8e-217">**TLSv1_1**</span></span>
* <span data-ttu-id="c5e8e-218">**TLSv1_2**</span><span class="sxs-lookup"><span data-stu-id="c5e8e-218">**TLSv1_2**</span></span>

<span data-ttu-id="c5e8e-219">Jeux hello version du protocole minimale trop**TLSv1_2** et **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_ SHA256**, **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**et **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** uniquement.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-219">Sets hello minimum protocol version too**TLSv1_2** and enables **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256**, **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**, and **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** only.</span></span>

```powershell
$SSLPolicy = New-AzureRmApplicationGatewaySSLPolicy -MinProtocolVersion TLSv1_2 -CipherSuite "TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256", "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384", "TLS_RSA_WITH_AES_128_GCM_SHA256"
```

## <a name="create-hello-application-gateway"></a><span data-ttu-id="c5e8e-220">Créer hello Application Gateway</span><span class="sxs-lookup"><span data-stu-id="c5e8e-220">Create hello Application Gateway</span></span>

<span data-ttu-id="c5e8e-221">Hello toutes les étapes précédentes, créez hello passerelle d’Application.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-221">Using all hello preceding steps, create hello Application Gateway.</span></span> <span data-ttu-id="c5e8e-222">Création de Hello de passerelle de hello est un processus à long terme.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-222">hello creation of hello gateway is a long running process.</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgateway -SSLCertificates $cert -ResourceGroupName "appgw-rg" -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -SSLPolicy $SSLPolicy -AuthenticationCertificates $authcert -Verbose
```

## <a name="limit-ssl-protocol-versions-on-an-existing-application-gateway"></a><span data-ttu-id="c5e8e-223">Limiter les versions du protocole SSL sur une passerelle Application Gateway existante</span><span class="sxs-lookup"><span data-stu-id="c5e8e-223">Limit SSL protocol versions on an existing Application Gateway</span></span>

<span data-ttu-id="c5e8e-224">Hello précédentes étapes vous guide dans la création d’applications à la fin tooend SSL et la désactivation de certaines versions du protocole SSL.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-224">hello preceding steps take you through creating an application with end tooend SSL and disabling certain SSL protocol versions.</span></span> <span data-ttu-id="c5e8e-225">Hello exemple suivant désactive certaines stratégies SSL sur une passerelle d’application existant.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-225">hello following example disables certain SSL policies on an existing application gateway.</span></span>

### <a name="step-1"></a><span data-ttu-id="c5e8e-226">Étape 1</span><span class="sxs-lookup"><span data-stu-id="c5e8e-226">Step 1</span></span>

<span data-ttu-id="c5e8e-227">Récupérer tooupdate de passerelle d’application hello.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-227">Retrieve hello application gateway tooupdate.</span></span>

```powershell
$gw = Get-AzureRmApplicationGateway -Name AdatumAppGateway -ResourceGroupName AdatumAppGatewayRG
```

### <a name="step-2"></a><span data-ttu-id="c5e8e-228">Étape 2</span><span class="sxs-lookup"><span data-stu-id="c5e8e-228">Step 2</span></span>

<span data-ttu-id="c5e8e-229">Définissez une stratégie SSL.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-229">Define an SSL policy.</span></span> <span data-ttu-id="c5e8e-230">Dans l’exemple suivant de hello, TLSv1.0 et TLSv1.1 sont désactivées et hello suites de chiffrement **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256** , **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**, et  **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** est hello seules autorisées.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-230">In hello following example, TLSv1.0 and TLSv1.1 are disabled and hello cipher suites **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256**, **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**, and **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** are hello only ones allowed.</span></span>

```powershell
Set-AzureRmApplicationGatewaySSLPolicy -MinProtocolVersion -PolicyType Custom -CipherSuite "TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256", "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384", "TLS_RSA_WITH_AES_128_GCM_SHA256" -ApplicationGateway $gw

```

### <a name="step-3"></a><span data-ttu-id="c5e8e-231">Étape 3 :</span><span class="sxs-lookup"><span data-stu-id="c5e8e-231">Step 3</span></span>

<span data-ttu-id="c5e8e-232">Enfin, mettre à jour de passerelle de hello.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-232">Finally, update hello gateway.</span></span> <span data-ttu-id="c5e8e-233">Il est important toonote que cette dernière étape est une tâche de longue durée.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-233">It is important toonote that this last step is a long running task.</span></span> <span data-ttu-id="c5e8e-234">Lorsqu’il est terminé, fin tooend SSL est configuré sur la passerelle d’application hello.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-234">When it is done, end tooend SSL is configured on hello application gateway.</span></span>

```powershell
$gw | Set-AzureRmApplicationGateway
```

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="c5e8e-235">Obtenir le nom DNS d’une passerelle Application Gateway</span><span class="sxs-lookup"><span data-stu-id="c5e8e-235">Get application gateway DNS name</span></span>

<span data-ttu-id="c5e8e-236">Après la création de la passerelle de hello, hello prochaine étape consiste tooconfigure hello frontal pour la communication.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-236">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="c5e8e-237">Lorsque vous utilisez une adresse IP publique, la passerelle Application Gateway requiert un nom DNS attribué dynamiquement, ce qui n’est pas convivial.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-237">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="c5e8e-238">les utilisateurs finaux de tooensure pouvez atteindre la passerelle d’application hello, un enregistrement CNAME peut être le point de terminaison utilisé toopoint toohello public de la passerelle d’application hello.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-238">tooensure end users can hit hello application gateway, a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="c5e8e-239">[Configuration d’un nom de domaine personnalisé pour Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c5e8e-239">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="c5e8e-240">toodo, détails de récupération de la passerelle d’application hello et son nom IP/DNS associé à l’aide de la passerelle d’application hello PublicIPAddress élément attaché toohello.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-240">toodo this, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="c5e8e-241">nom DNS de la passerelle d’application Hello doit être utilisé toocreate un enregistrement CNAME, le nom DNS de points hello deux web applications toothis.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-241">hello application gateway's DNS name should be used toocreate a CNAME record, which points hello two web applications toothis DNS name.</span></span> <span data-ttu-id="c5e8e-242">les utilisation de Hello d’enregistrements d’un n’est pas recommandée étant donné que l’adresse IP virtuelle hello peut changer lors du redémarrage de la passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="c5e8e-242">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -Name publicIP01
```

```
Name                     : publicIP01
ResourceGroupName        : appgw-RG
Location                 : westus
Id                       : /subscriptions/<subscription_id>/resourceGroups/appgw-RG/providers/Microsoft.Network/publicIPAddresses/publicIP01
Etag                     : W/"00000d5b-54ed-4907-bae8-99bd5766d0e5"
ResourceGuid             : 00000000-0000-0000-0000-000000000000
ProvisioningState        : Succeeded
Tags                     : 
PublicIpAllocationMethod : Dynamic
IpAddress                : xx.xx.xxx.xx
PublicIpAddressVersion   : IPv4
IdleTimeoutInMinutes     : 4
IpConfiguration          : {
                                "Id": "/subscriptions/<subscription_id>/resourceGroups/appgw-RG/providers/Microsoft.Network/applicationGateways/appgwtest/frontendIP
                            Configurations/frontend1"
                            }
DnsSettings              : {
                                "Fqdn": "00000000-0000-xxxx-xxxx-xxxxxxxxxxxx.cloudapp.net"
                            }
```

## <a name="next-steps"></a><span data-ttu-id="c5e8e-243">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c5e8e-243">Next steps</span></span>

<span data-ttu-id="c5e8e-244">En savoir plus sur la sécurisation renforcée de sécurité hello de vos applications web avec des pare-feu d’applications Web via la passerelle d’Application en vous rendant sur [vue d’ensemble du pare-feu d’Application Web](application-gateway-webapplicationfirewall-overview.md)</span><span class="sxs-lookup"><span data-stu-id="c5e8e-244">Learn about hardening hello security of your web applications with Web Application Firewall through Application Gateway by visiting [Web Application Firewall Overview](application-gateway-webapplicationfirewall-overview.md)</span></span>

[scenario]: ./media/application-gateway-end-to-end-SSL-powershell/scenario.png
