---
title: "Configuration du chiffrement SSL de bout en bout avec Azure Application Gateway | Microsoft Docs"
description: "Cet article explique comment configurer le chiffrement SSL de bout en bout avec la passerelle Application Gateway à l’aide d’Azure Resource Manager PowerShell"
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
ms.openlocfilehash: 6d969d6a0c649c263e1d5bb99bdbceec484cb9a3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="configure-end-to-end-ssl-with-application-gateway-using-powershell"></a><span data-ttu-id="2cd67-103">Configuration du chiffrement SSL de bout en bout avec Application Gateway à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="2cd67-103">Configure end to end SSL with Application Gateway using PowerShell</span></span>

## <a name="overview"></a><span data-ttu-id="2cd67-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="2cd67-104">Overview</span></span>

<span data-ttu-id="2cd67-105">La passerelle Application Gateway prend en charge le chiffrement de bout en bout du trafic.</span><span class="sxs-lookup"><span data-stu-id="2cd67-105">Application Gateway supports end to end encryption of traffic.</span></span> <span data-ttu-id="2cd67-106">Pour cela, la passerelle Application Gateway arrête la connexion SSL au niveau de la passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="2cd67-106">Application Gateway does this by terminating the SSL connection at the application gateway.</span></span> <span data-ttu-id="2cd67-107">La passerelle applique ensuite les règles de routage au trafic, chiffre à nouveau le paquet puis transfère le paquet au serveur principal approprié selon les règles de routage définies.</span><span class="sxs-lookup"><span data-stu-id="2cd67-107">The gateway then applies the routing rules to the traffic, re-encrypts the packet, and forwards the packet to the appropriate backend based on the routing rules defined.</span></span> <span data-ttu-id="2cd67-108">Toute réponse du serveur web passe par le même processus vers l’utilisateur final.</span><span class="sxs-lookup"><span data-stu-id="2cd67-108">Any response from the web server goes through the same process back to the end user.</span></span>

<span data-ttu-id="2cd67-109">La passerelle Application Gateway prend également en charge la définition d’options SSL personnalisées.</span><span class="sxs-lookup"><span data-stu-id="2cd67-109">Another feature that application gateway supports defining custom SSL options.</span></span> <span data-ttu-id="2cd67-110">Application Gateway prend en charge la désactivation des versions suivantes du protocole : **TLSv1.0**, **TLSv1.1** et **TLSv1.2** ; elle permet aussi de définir les suites de chiffrement à utiliser et l’ordre de préférence.</span><span class="sxs-lookup"><span data-stu-id="2cd67-110">Application Gateway supports disabling the following protocol version; **TLSv1.0**, **TLSv1.1**, and **TLSv1.2** as well defining the which cipher suites to use and the order of preference.</span></span>  <span data-ttu-id="2cd67-111">Pour en savoir plus sur les options SSL configurables, consultez cette [vue d’ensemble de la stratégie SSL](application-gateway-SSL-policy-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2cd67-111">To learn more about configurable SSL options, visit [SSL Policy overview](application-gateway-SSL-policy-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="2cd67-112">SSL 2.0 et SSL 3.0 sont désactivés par défaut et ne peuvent pas être activés.</span><span class="sxs-lookup"><span data-stu-id="2cd67-112">SSL 2.0 and SSL 3.0 are disabled by default and cannot be enabled.</span></span> <span data-ttu-id="2cd67-113">Considérés comme non sécurisés, ils ne peuvent pas être utilisés avec Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="2cd67-113">They are considered unsecure and are not able to be used with Application Gateway.</span></span>

![image du scénario][scenario]

## <a name="scenario"></a><span data-ttu-id="2cd67-115">Scénario</span><span class="sxs-lookup"><span data-stu-id="2cd67-115">Scenario</span></span>

<span data-ttu-id="2cd67-116">Dans ce scénario, vous allez apprendre à créer une passerelle d’application en utilisant un chiffrement SSL de bout en bout avec PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2cd67-116">In this scenario, you learn how to create an application gateway using end to end SSL using PowerShell.</span></span>

<span data-ttu-id="2cd67-117">Ce scénario va :</span><span class="sxs-lookup"><span data-stu-id="2cd67-117">This scenario will:</span></span>

* <span data-ttu-id="2cd67-118">créer un groupe de ressources nommé **appgw-rg** ;</span><span class="sxs-lookup"><span data-stu-id="2cd67-118">Create a resource group named **appgw-rg**</span></span>
* <span data-ttu-id="2cd67-119">créer un réseau virtuel nommé **appgwvnet** avec un espace d’adresse de 10.0.0.0/16 ;</span><span class="sxs-lookup"><span data-stu-id="2cd67-119">Create a virtual network named **appgwvnet** with an address space of 10.0.0.0/16.</span></span>
* <span data-ttu-id="2cd67-120">créer deux sous-réseaux appelés **appgwsubnet** et **appsubnet** ;</span><span class="sxs-lookup"><span data-stu-id="2cd67-120">Create two subnets called **appgwsubnet** and **appsubnet**.</span></span>
* <span data-ttu-id="2cd67-121">créer une petite passerelle d’application prenant en charge le chiffrement SSL de bout en bout qui limite les versions de protocoles SSL et les suites de chiffrement.</span><span class="sxs-lookup"><span data-stu-id="2cd67-121">Create a small application gateway supporting end to end SSL encryption that limits SSL protocols versions and cipher suites.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="2cd67-122">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="2cd67-122">Before you begin</span></span>

<span data-ttu-id="2cd67-123">Pour configurer un chiffrement SSL de bout en bout avec une passerelle d’application, un certificat est requis pour la passerelle et des certificats sont requis pour les serveurs principaux.</span><span class="sxs-lookup"><span data-stu-id="2cd67-123">To configure end to end SSL with an application gateway, a certificate is required for the gateway and certificates are required for the backend servers.</span></span> <span data-ttu-id="2cd67-124">Le certificat de la passerelle sert à chiffrer et à déchiffrer le trafic envoyé à l’aide de SSL.</span><span class="sxs-lookup"><span data-stu-id="2cd67-124">The gateway certificate is used to encrypt and decrypt the traffic sent to it using SSL.</span></span> <span data-ttu-id="2cd67-125">Le certificat de passerelle doit être partagé au format Personal Information Exchange (.pfx).</span><span class="sxs-lookup"><span data-stu-id="2cd67-125">The gateway certificate needs to be in Personal Information Exchange (pfx) format.</span></span> <span data-ttu-id="2cd67-126">Ce format de fichier permet d’exporter la clé privée requise par la passerelle d’application pour effectuer le chiffrement et le déchiffrement du trafic.</span><span class="sxs-lookup"><span data-stu-id="2cd67-126">This file format allows for the private key to be exported which is required by the application gateway to perform the encryption and decryption of traffic.</span></span>

<span data-ttu-id="2cd67-127">Pour le chiffrement SSL de bout en bout, le serveur principal doit figurer sur la liste approuvée par la passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="2cd67-127">For end to end SSL encryption the backend must be whitelisted with application gateway.</span></span> <span data-ttu-id="2cd67-128">Pour cela, vous devez charger le certificat public des serveurs principaux sur la passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="2cd67-128">This is done by uploading the public certificate of the backends to the application gateway.</span></span> <span data-ttu-id="2cd67-129">Ainsi, la passerelle d’application communique uniquement avec des instances de serveur principal connues,</span><span class="sxs-lookup"><span data-stu-id="2cd67-129">This ensures that the application gateway only communicates with known backend instances.</span></span> <span data-ttu-id="2cd67-130">ce qui sécurise la communication de bout en bout.</span><span class="sxs-lookup"><span data-stu-id="2cd67-130">This further secures the end to end communication.</span></span>

<span data-ttu-id="2cd67-131">Ce processus est décrit dans les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="2cd67-131">This process is described in the following steps:</span></span>

## <a name="create-the-resource-group"></a><span data-ttu-id="2cd67-132">Créer le groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="2cd67-132">Create the Resource Group</span></span>

<span data-ttu-id="2cd67-133">Cette section vous guide lors de la création d’un groupe de ressources contenant la passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="2cd67-133">This section walks you through creating a resource group, that contains the application gateway.</span></span>

### <a name="step-1"></a><span data-ttu-id="2cd67-134">Étape 1 :</span><span class="sxs-lookup"><span data-stu-id="2cd67-134">Step 1</span></span>

<span data-ttu-id="2cd67-135">Connectez-vous à votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="2cd67-135">Log in to your Azure Account.</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a><span data-ttu-id="2cd67-136">Étape 2 :</span><span class="sxs-lookup"><span data-stu-id="2cd67-136">Step 2</span></span>

<span data-ttu-id="2cd67-137">Sélectionnez l’abonnement à utiliser pour ce scénario.</span><span class="sxs-lookup"><span data-stu-id="2cd67-137">Select the subscription to use for this scenario.</span></span>

```powershell
Select-AzureRmsubscription -SubscriptionName "<Subscription name>"
```

### <a name="step-3"></a><span data-ttu-id="2cd67-138">Étape 3</span><span class="sxs-lookup"><span data-stu-id="2cd67-138">Step 3</span></span>

<span data-ttu-id="2cd67-139">Créez un groupe de ressources (ignorez cette étape si vous utilisez un groupe de ressources existant).</span><span class="sxs-lookup"><span data-stu-id="2cd67-139">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

## <a name="create-a-virtual-network-and-a-subnet-for-the-application-gateway"></a><span data-ttu-id="2cd67-140">Créer un réseau virtuel et un sous-réseau pour la passerelle Application Gateway</span><span class="sxs-lookup"><span data-stu-id="2cd67-140">Create a virtual network and a subnet for the application gateway</span></span>

<span data-ttu-id="2cd67-141">L’exemple suivant crée un réseau virtuel et deux sous-réseaux.</span><span class="sxs-lookup"><span data-stu-id="2cd67-141">The following example creates a virtual network and two subnets.</span></span> <span data-ttu-id="2cd67-142">Un sous-réseau sert à héberger la passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="2cd67-142">One subnet is used to hold the application gateway.</span></span> <span data-ttu-id="2cd67-143">Le second sous-réseau est utilisé pour les serveurs principaux hébergeant l’application web.</span><span class="sxs-lookup"><span data-stu-id="2cd67-143">The other subnet is used for the backends hosting the web application.</span></span>

### <a name="step-1"></a><span data-ttu-id="2cd67-144">Étape 1</span><span class="sxs-lookup"><span data-stu-id="2cd67-144">Step 1</span></span>

<span data-ttu-id="2cd67-145">Affectez une plage d’adresses au sous-réseau utilisé pour la passerelle Application Gateway elle-même.</span><span class="sxs-lookup"><span data-stu-id="2cd67-145">Assign an address range for the subnet be used for the Application Gateway itself.</span></span>

```powershell
$gwSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -AddressPrefix 10.0.0.0/24
```

> [!NOTE]
> <span data-ttu-id="2cd67-146">Les sous-réseaux configurés pour la passerelle d’application doivent être correctement dimensionnés.</span><span class="sxs-lookup"><span data-stu-id="2cd67-146">Subnets configured for application gateway should be properly sized.</span></span> <span data-ttu-id="2cd67-147">Une passerelle d’application peut être configurée pour 10 instances maximum.</span><span class="sxs-lookup"><span data-stu-id="2cd67-147">An application gateway can be configured for up to 10 instances.</span></span> <span data-ttu-id="2cd67-148">Chaque instance prend une adresse IP du sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="2cd67-148">Each instance takes one IP address from the subnet.</span></span> <span data-ttu-id="2cd67-149">Un sous-réseau trop petit peut nuire à la montée en charge d’une passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="2cd67-149">Too small of a subnet can adversely affect scaling out an application gateway.</span></span>
> 
> 

### <a name="step-2"></a><span data-ttu-id="2cd67-150">Étape 2</span><span class="sxs-lookup"><span data-stu-id="2cd67-150">Step 2</span></span>

<span data-ttu-id="2cd67-151">Affectez une plage d’adresses au pool d’adresses principales.</span><span class="sxs-lookup"><span data-stu-id="2cd67-151">Assign an address range to be used for the Backend address pool.</span></span>

```powershell
$nicSubnet = New-AzureRmVirtualNetworkSubnetConfig  -Name 'appsubnet' -AddressPrefix 10.0.2.0/24
```

### <a name="step-3"></a><span data-ttu-id="2cd67-152">Étape 3 :</span><span class="sxs-lookup"><span data-stu-id="2cd67-152">Step 3</span></span>

<span data-ttu-id="2cd67-153">Créez un réseau virtuel avec les sous-réseaux définis dans les étapes précédentes.</span><span class="sxs-lookup"><span data-stu-id="2cd67-153">Create a virtual network with the subnets defined in the preceding steps.</span></span>

```powershell
$vnet = New-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $gwSubnet, $nicSubnet
```

### <a name="step-4"></a><span data-ttu-id="2cd67-154">Étape 4</span><span class="sxs-lookup"><span data-stu-id="2cd67-154">Step 4</span></span>

<span data-ttu-id="2cd67-155">Récupérez les ressources de réseau virtuel et les ressources de sous-réseau à utiliser dans les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="2cd67-155">Retrieve the virtual network resource and subnet resources to be used in the following steps:</span></span>

```powershell
$vnet = Get-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg
$gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -VirtualNetwork $vnet
$nicSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'appsubnet' -VirtualNetwork $vnet
```

## <a name="create-a-public-ip-address-for-the-front-end-configuration"></a><span data-ttu-id="2cd67-156">Création d'une adresse IP publique pour la configuration frontale</span><span class="sxs-lookup"><span data-stu-id="2cd67-156">Create a public IP address for the front-end configuration</span></span>

<span data-ttu-id="2cd67-157">Créez une ressource IP publique à utiliser pour la passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="2cd67-157">Create a public IP resource to be used for the application gateway.</span></span> <span data-ttu-id="2cd67-158">Cette adresse IP publique est utilisée dans une prochaine étape.</span><span class="sxs-lookup"><span data-stu-id="2cd67-158">This public IP address is used a following step.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -Name 'publicIP01' -Location "West US" -AllocationMethod Dynamic
```

> [!IMPORTANT]
> <span data-ttu-id="2cd67-159">La passerelle Application Gateway ne prend pas en charge l’utilisation d’une adresse IP publique créée avec un nom de domaine défini.</span><span class="sxs-lookup"><span data-stu-id="2cd67-159">Application Gateway does not support the use of a public IP address created with a domain label defined.</span></span> <span data-ttu-id="2cd67-160">Seule une adresse IP publique avec un nom de domaine créé dynamiquement est prise en charge.</span><span class="sxs-lookup"><span data-stu-id="2cd67-160">Only a public IP address with a dynamically created domain label is supported.</span></span> <span data-ttu-id="2cd67-161">Si vous avez besoin d’un nom DNS convivial pour la passerelle Application Gateway, il est recommandé d’utiliser un enregistrement CNAME comme alias.</span><span class="sxs-lookup"><span data-stu-id="2cd67-161">If you require a friendly dns name for the application gateway, it is recommended to use a CNAME record as an alias.</span></span>

## <a name="create-an-application-gateway-configuration-object"></a><span data-ttu-id="2cd67-162">Créer un objet de configuration de passerelle Application Gateway</span><span class="sxs-lookup"><span data-stu-id="2cd67-162">Create an application gateway configuration object</span></span>

<span data-ttu-id="2cd67-163">Tous les éléments de configuration sont définis avant la création de la passerelle Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="2cd67-163">All configuration items are set before creating the application gateway.</span></span> <span data-ttu-id="2cd67-164">Les étapes suivantes permettent de créer les éléments de configuration nécessaires à une ressource Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="2cd67-164">The following steps create the configuration items that are needed for an application gateway resource.</span></span>

### <a name="step-1"></a><span data-ttu-id="2cd67-165">Étape 1 :</span><span class="sxs-lookup"><span data-stu-id="2cd67-165">Step 1</span></span>

<span data-ttu-id="2cd67-166">Créez une configuration IP de passerelle application : ce paramètre détermine quel sous-réseau utilise la passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="2cd67-166">Create an application gateway IP configuration, this setting configures what subnet the application gateway uses.</span></span> <span data-ttu-id="2cd67-167">Au démarrage, la passerelle Application Gateway sélectionne une adresse IP du sous-réseau configuré et achemine le trafic réseau vers les adresses IP du pool IP principal.</span><span class="sxs-lookup"><span data-stu-id="2cd67-167">When application gateway starts, it picks up an IP address from the subnet configured and routes network traffic to the IP addresses in the back-end IP pool.</span></span> <span data-ttu-id="2cd67-168">Gardez à l’esprit que chaque instance utilise une adresse IP unique.</span><span class="sxs-lookup"><span data-stu-id="2cd67-168">Keep in mind that each instance takes one IP address.</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name 'gwconfig' -Subnet $gwSubnet
```

### <a name="step-2"></a><span data-ttu-id="2cd67-169">Étape 2</span><span class="sxs-lookup"><span data-stu-id="2cd67-169">Step 2</span></span>

<span data-ttu-id="2cd67-170">Créez une configuration IP frontale : ce paramètre mappe une adresse IP privée ou publique au composant frontal de la passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="2cd67-170">Create a front-end IP configuration, this setting maps a private or public ip address to the front end of the application gateway.</span></span> <span data-ttu-id="2cd67-171">L’étape suivante associe l’adresse IP publique à l’étape précédente à la configuration IP frontale.</span><span class="sxs-lookup"><span data-stu-id="2cd67-171">The following step associates the public IP address in the preceding step with the front-end IP configuration.</span></span>

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name 'fip01' -PublicIPAddress $publicip
```

### <a name="step-3"></a><span data-ttu-id="2cd67-172">Étape 3</span><span class="sxs-lookup"><span data-stu-id="2cd67-172">Step 3</span></span>

<span data-ttu-id="2cd67-173">Configurez le pool d’adresses IP principales avec les adresses IP des serveurs web principaux.</span><span class="sxs-lookup"><span data-stu-id="2cd67-173">Configure the back-end IP address pool with the IP addresses of the backend web servers.</span></span> <span data-ttu-id="2cd67-174">Il s’agit des adresses IP qui recevront le trafic réseau provenant du point de terminaison IP frontal.</span><span class="sxs-lookup"><span data-stu-id="2cd67-174">These IP addresses are the IP addresses that receive the network traffic that comes from the front-end IP endpoint.</span></span> <span data-ttu-id="2cd67-175">Remplacez les adresses IP suivantes pour ajouter vos propres points de terminaison d’adresse IP d’application.</span><span class="sxs-lookup"><span data-stu-id="2cd67-175">You replace the following IP addresses to add your own application IP address endpoints.</span></span>

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name 'pool01' -BackendIPAddresses 1.1.1.1, 2.2.2.2, 3.3.3.3
```

> [!NOTE]
> <span data-ttu-id="2cd67-176">Un nom de domaine complet (FQDN) est également une valeur valide pour remplacer une adresse IP dans les serveurs principaux à l’aide du commutateur -BackendFqdns.</span><span class="sxs-lookup"><span data-stu-id="2cd67-176">A fully qualified domain name (FQDN) is also a valid value in place of an ip address for the backend servers by using the -BackendFqdns switch.</span></span> 

### <a name="step-4"></a><span data-ttu-id="2cd67-177">Étape 4</span><span class="sxs-lookup"><span data-stu-id="2cd67-177">Step 4</span></span>

<span data-ttu-id="2cd67-178">Configurez le port IP frontal pour le point de terminaison IP public.</span><span class="sxs-lookup"><span data-stu-id="2cd67-178">Configure the front-end IP port for the public IP endpoint.</span></span> <span data-ttu-id="2cd67-179">Ce port est le port auquel les utilisateurs finaux se connectent.</span><span class="sxs-lookup"><span data-stu-id="2cd67-179">This port is the port that end users connect to.</span></span>

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name 'port01'  -Port 443
```

### <a name="step-5"></a><span data-ttu-id="2cd67-180">Étape 5</span><span class="sxs-lookup"><span data-stu-id="2cd67-180">Step 5</span></span>

<span data-ttu-id="2cd67-181">Configurez le certificat pour la passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="2cd67-181">Configure the certificate for the application gateway.</span></span> <span data-ttu-id="2cd67-182">Ce certificat sert à chiffrer et à chiffrer à nouveau le trafic sur la passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="2cd67-182">This certificate is used to decrypt and re-encrypt the traffic on the application gateway.</span></span>

```powershell
$cert = New-AzureRmApplicationGatewaySSLCertificate -Name cert01 -CertificateFile <full path to .pfx file> -Password <password for certificate file>
```

> [!NOTE]
> <span data-ttu-id="2cd67-183">Cet exemple configure le certificat utilisé pour la connexion SSL.</span><span class="sxs-lookup"><span data-stu-id="2cd67-183">This sample configures the certificate used for SSL connection.</span></span> <span data-ttu-id="2cd67-184">Le certificat doit être au format .pfx et le mot de passe contenir entre 4 et 12 caractères.</span><span class="sxs-lookup"><span data-stu-id="2cd67-184">The certificate needs to be in .pfx format, and the password must be between 4 to 12 characters.</span></span>

### <a name="step-6"></a><span data-ttu-id="2cd67-185">Étape 6</span><span class="sxs-lookup"><span data-stu-id="2cd67-185">Step 6</span></span>

<span data-ttu-id="2cd67-186">Créez l’écouteur HTTP pour la passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="2cd67-186">Create the HTTP listener for the application gateway.</span></span> <span data-ttu-id="2cd67-187">Affectez la configuration IP frontale, le port et le certificat SSL à utiliser.</span><span class="sxs-lookup"><span data-stu-id="2cd67-187">Assign the front-end ip configuration, port, and SSL certificate to use.</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SSLCertificate $cert
```

### <a name="step-7"></a><span data-ttu-id="2cd67-188">Étape 7</span><span class="sxs-lookup"><span data-stu-id="2cd67-188">Step 7</span></span>

<span data-ttu-id="2cd67-189">Chargez le certificat à utiliser sur les ressources du pool principal pour lequel le chiffrement SSL est activé.</span><span class="sxs-lookup"><span data-stu-id="2cd67-189">Upload the certificate to be used on the SSL enabled backend pool resources.</span></span>

> [!NOTE]
> <span data-ttu-id="2cd67-190">La sonde par défaut obtient la clé publique de la liaison SSL **par défaut** sur l’adresse IP du serveur principal et compare la valeur de clé publique reçue à celle que vous fournissez ici.</span><span class="sxs-lookup"><span data-stu-id="2cd67-190">The default probe gets the public key from the **default** SSL binding on the back-end's IP address and compares the public key value it receives to the public key value you provide here.</span></span> <span data-ttu-id="2cd67-191">La clé publique récupérée n’est pas nécessairement le site vers lequel vous souhaitez que le trafic soit dirigé **si** vous utilisez des en-têtes d’hôte et SNI sur le serveur principal.</span><span class="sxs-lookup"><span data-stu-id="2cd67-191">The retrieved public key may not necessarily be the intended site to which traffic flows **if** you are using host headers and SNI on the back-end.</span></span> <span data-ttu-id="2cd67-192">En cas de doute, visitez https://127.0.0.1/ sur les serveurs principaux pour confirmer le certificat utilisé pour la liaison SSL **par défaut**.</span><span class="sxs-lookup"><span data-stu-id="2cd67-192">If in doubt, visit https://127.0.0.1/ on the back-ends to confirm which certificate is used for the **default** SSL binding.</span></span> <span data-ttu-id="2cd67-193">Utilisez la clé publique de cette demande dans cette section.</span><span class="sxs-lookup"><span data-stu-id="2cd67-193">Use the public key from that request in this section.</span></span> <span data-ttu-id="2cd67-194">Si vous utilisez des en-têtes d’hôte et SNI sur les liaisons HTTPS et que vous ne recevez pas une réponse et un certificat à partir d’une demande de navigateur manuelle vers https://127.0.0.1/ sur les serveurs principaux, vous devez configurer une liaison SSL par défaut sur les serveurs principaux.</span><span class="sxs-lookup"><span data-stu-id="2cd67-194">If you are using host-headers and SNI on HTTPS bindings and you do not receive a response and certificate from a manual browser request to https://127.0.0.1/ on the back-ends, you must set up a default SSL binding on the back-ends.</span></span> <span data-ttu-id="2cd67-195">Si vous ne le faites pas, les sondes échouent et le serveur principal ne figure pas dans la liste approuvée.</span><span class="sxs-lookup"><span data-stu-id="2cd67-195">If you do not do so, probes fail and the back-end is not whitelisted.</span></span>

```powershell
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name 'whitelistcert1' -CertificateFile C:\users\gwallace\Desktop\cert.cer
```

> [!NOTE]
> <span data-ttu-id="2cd67-196">Le certificat fourni dans cette étape doit être la clé publique du certificat pfx présent sur le serveur principal.</span><span class="sxs-lookup"><span data-stu-id="2cd67-196">The certificate provided in this step should be the public key of the pfx cert present on the backend.</span></span> <span data-ttu-id="2cd67-197">Exportez le certificat (pas le certificat racine) installé sur le serveur principal au format .CER et utilisez-le dans cette étape.</span><span class="sxs-lookup"><span data-stu-id="2cd67-197">Export the certificate (not the root certificate) installed on the backend server in .CER format and use it in this step.</span></span> <span data-ttu-id="2cd67-198">Cette étape permet d’ajouter le serveur principal à la liste approuvée par la passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="2cd67-198">This step whitelists the backend with the application gateway.</span></span>

### <a name="step-8"></a><span data-ttu-id="2cd67-199">Étape 8</span><span class="sxs-lookup"><span data-stu-id="2cd67-199">Step 8</span></span>

<span data-ttu-id="2cd67-200">Configurez les paramètres http principaux de la passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="2cd67-200">Configure the application gateway back-end http settings.</span></span> <span data-ttu-id="2cd67-201">Affectez le certificat téléchargé à l’étape précédente aux paramètres http.</span><span class="sxs-lookup"><span data-stu-id="2cd67-201">Assign the certificate uploaded in the preceding step to the http settings.</span></span>

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name 'setting01' -Port 443 -Protocol Https -CookieBasedAffinity Enabled -AuthenticationCertificates $authcert
```

### <a name="step-9"></a><span data-ttu-id="2cd67-202">Étape 9</span><span class="sxs-lookup"><span data-stu-id="2cd67-202">Step 9</span></span>

<span data-ttu-id="2cd67-203">Créez une règle d'acheminement d'équilibrage de charge nommée qui configure le comportement d'équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="2cd67-203">Create a load balancer routing rule that configures the load balancer behavior.</span></span> <span data-ttu-id="2cd67-204">Dans cet exemple, une simple règle de type tourniquet (round robin) est créée.</span><span class="sxs-lookup"><span data-stu-id="2cd67-204">In this example, a basic round robin rule is created.</span></span>

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name 'rule01' -RuleType basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

### <a name="step-10"></a><span data-ttu-id="2cd67-205">Étape 10</span><span class="sxs-lookup"><span data-stu-id="2cd67-205">Step 10</span></span>

<span data-ttu-id="2cd67-206">Configurez la taille d'instance de la passerelle Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="2cd67-206">Configure the instance size of the application gateway.</span></span>  <span data-ttu-id="2cd67-207">Les tailles disponibles sont **Standard\_Small**, **Standard\_Medium** et **Standard\_Large**.</span><span class="sxs-lookup"><span data-stu-id="2cd67-207">The available sizes are **Standard\_Small**, **Standard\_Medium**, and **Standard\_Large**.</span></span>  <span data-ttu-id="2cd67-208">Pour la capacité, les valeurs disponibles sont 1 à 10.</span><span class="sxs-lookup"><span data-stu-id="2cd67-208">For capacity, the available values are 1 through 10.</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

> [!NOTE]
> <span data-ttu-id="2cd67-209">Vous pouvez choisir un nombre d’instances de 1 à des fins de test.</span><span class="sxs-lookup"><span data-stu-id="2cd67-209">An instance count of 1 can be chosen for testing purposes.</span></span> <span data-ttu-id="2cd67-210">Il est important de savoir que n’importe quel nombre d’instances inférieur à 2 n’est pas couvert par le contrat SLA et n’est donc pas recommandé.</span><span class="sxs-lookup"><span data-stu-id="2cd67-210">It is important to know that any instance count under two instances is not covered by the SLA and are therefore not recommended.</span></span> <span data-ttu-id="2cd67-211">Les petites passerelles doivent être utilisées pour les tests de développement et non à des fins de production.</span><span class="sxs-lookup"><span data-stu-id="2cd67-211">Small gateways are to be used for dev test and not for production purposes.</span></span>

### <a name="step-11"></a><span data-ttu-id="2cd67-212">Étape 11</span><span class="sxs-lookup"><span data-stu-id="2cd67-212">Step 11</span></span>

<span data-ttu-id="2cd67-213">Configurez la stratégie SSL à utiliser sur la passerelle Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="2cd67-213">Configure the SSL policy to be used on the Application Gateway.</span></span> <span data-ttu-id="2cd67-214">La passerelle Application Gateway prend en charge la possibilité de définir une version minimale pour les versions du protocole SSL.</span><span class="sxs-lookup"><span data-stu-id="2cd67-214">Application Gateway supports the ability to set a minimum version for SSL protocol versions.</span></span>

<span data-ttu-id="2cd67-215">Les valeurs suivantes représentent une liste des versions de protocole pouvant être définies.</span><span class="sxs-lookup"><span data-stu-id="2cd67-215">The following values are a list of protocol versions that can be defined.</span></span>

* <span data-ttu-id="2cd67-216">**TLSv1_0**</span><span class="sxs-lookup"><span data-stu-id="2cd67-216">**TLSv1_0**</span></span>
* <span data-ttu-id="2cd67-217">**TLSv1_1**</span><span class="sxs-lookup"><span data-stu-id="2cd67-217">**TLSv1_1**</span></span>
* <span data-ttu-id="2cd67-218">**TLSv1_2**</span><span class="sxs-lookup"><span data-stu-id="2cd67-218">**TLSv1_2**</span></span>

<span data-ttu-id="2cd67-219">Définit la version minimale de protocole sur **TLSv1_2** et active **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256**, **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384** et **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** uniquement.</span><span class="sxs-lookup"><span data-stu-id="2cd67-219">Sets the minimum protocol version to **TLSv1_2** and enables **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256**, **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**, and **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** only.</span></span>

```powershell
$SSLPolicy = New-AzureRmApplicationGatewaySSLPolicy -MinProtocolVersion TLSv1_2 -CipherSuite "TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256", "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384", "TLS_RSA_WITH_AES_128_GCM_SHA256"
```

## <a name="create-the-application-gateway"></a><span data-ttu-id="2cd67-220">Créer la passerelle Application Gateway</span><span class="sxs-lookup"><span data-stu-id="2cd67-220">Create the Application Gateway</span></span>

<span data-ttu-id="2cd67-221">À l’aide des étapes précédentes, créez la passerelle Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="2cd67-221">Using all the preceding steps, create the Application Gateway.</span></span> <span data-ttu-id="2cd67-222">La création de la passerelle est un processus à long terme.</span><span class="sxs-lookup"><span data-stu-id="2cd67-222">The creation of the gateway is a long running process.</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgateway -SSLCertificates $cert -ResourceGroupName "appgw-rg" -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -SSLPolicy $SSLPolicy -AuthenticationCertificates $authcert -Verbose
```

## <a name="limit-ssl-protocol-versions-on-an-existing-application-gateway"></a><span data-ttu-id="2cd67-223">Limiter les versions du protocole SSL sur une passerelle Application Gateway existante</span><span class="sxs-lookup"><span data-stu-id="2cd67-223">Limit SSL protocol versions on an existing Application Gateway</span></span>

<span data-ttu-id="2cd67-224">Les étapes précédentes vous guident dans la création d’une application en utilisant un chiffrement SSL de bout en bout et en désactivant certaines versions du protocole SSL.</span><span class="sxs-lookup"><span data-stu-id="2cd67-224">The preceding steps take you through creating an application with end to end SSL and disabling certain SSL protocol versions.</span></span> <span data-ttu-id="2cd67-225">L’exemple suivant désactive certaines stratégies SSL sur une passerelle d’application existante.</span><span class="sxs-lookup"><span data-stu-id="2cd67-225">The following example disables certain SSL policies on an existing application gateway.</span></span>

### <a name="step-1"></a><span data-ttu-id="2cd67-226">Étape 1 :</span><span class="sxs-lookup"><span data-stu-id="2cd67-226">Step 1</span></span>

<span data-ttu-id="2cd67-227">Récupérez la passerelle d’application à mettre à jour.</span><span class="sxs-lookup"><span data-stu-id="2cd67-227">Retrieve the application gateway to update.</span></span>

```powershell
$gw = Get-AzureRmApplicationGateway -Name AdatumAppGateway -ResourceGroupName AdatumAppGatewayRG
```

### <a name="step-2"></a><span data-ttu-id="2cd67-228">Étape 2 :</span><span class="sxs-lookup"><span data-stu-id="2cd67-228">Step 2</span></span>

<span data-ttu-id="2cd67-229">Définissez une stratégie SSL.</span><span class="sxs-lookup"><span data-stu-id="2cd67-229">Define an SSL policy.</span></span> <span data-ttu-id="2cd67-230">Dans l’exemple suivant, TLSv1.0 et TLSv1.1 sont désactivées et les suites de chiffrement **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256**, **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384** et **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** sont les seules autorisées.</span><span class="sxs-lookup"><span data-stu-id="2cd67-230">In the following example, TLSv1.0 and TLSv1.1 are disabled and the cipher suites **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256**, **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**, and **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** are the only ones allowed.</span></span>

```powershell
Set-AzureRmApplicationGatewaySSLPolicy -MinProtocolVersion -PolicyType Custom -CipherSuite "TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256", "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384", "TLS_RSA_WITH_AES_128_GCM_SHA256" -ApplicationGateway $gw

```

### <a name="step-3"></a><span data-ttu-id="2cd67-231">Étape 3 :</span><span class="sxs-lookup"><span data-stu-id="2cd67-231">Step 3</span></span>

<span data-ttu-id="2cd67-232">Pour finir, mettez à jour la passerelle.</span><span class="sxs-lookup"><span data-stu-id="2cd67-232">Finally, update the gateway.</span></span> <span data-ttu-id="2cd67-233">Il est important de noter que cette dernière étape représente une tâche à long terme.</span><span class="sxs-lookup"><span data-stu-id="2cd67-233">It is important to note that this last step is a long running task.</span></span> <span data-ttu-id="2cd67-234">Une fois l’opération terminée, le chiffrement SSL de bout en bout est configuré sur la passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="2cd67-234">When it is done, end to end SSL is configured on the application gateway.</span></span>

```powershell
$gw | Set-AzureRmApplicationGateway
```

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="2cd67-235">Obtenir le nom DNS d’une passerelle Application Gateway</span><span class="sxs-lookup"><span data-stu-id="2cd67-235">Get application gateway DNS name</span></span>

<span data-ttu-id="2cd67-236">Une fois la passerelle créée, l’étape suivante consiste à configurer le serveur frontal pour la communication.</span><span class="sxs-lookup"><span data-stu-id="2cd67-236">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="2cd67-237">Lorsque vous utilisez une adresse IP publique, la passerelle Application Gateway requiert un nom DNS attribué dynamiquement, ce qui n’est pas convivial.</span><span class="sxs-lookup"><span data-stu-id="2cd67-237">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="2cd67-238">Pour s’assurer que les utilisateurs finaux peuvent atteindre la passerelle d’application, un enregistrement CNAME peut être utilisé pour pointer vers le point de terminaison public de la passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="2cd67-238">To ensure end users can hit the application gateway, a CNAME record can be used to point to the public endpoint of the application gateway.</span></span> <span data-ttu-id="2cd67-239">[Configuration d’un nom de domaine personnalisé pour Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="2cd67-239">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="2cd67-240">Pour ce faire, récupérez les détails de la passerelle Application Gateway et de son nom IP/DNS associé à l’aide de l’élément PublicIPAddress attaché à la passerelle Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="2cd67-240">To do this, retrieve details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span></span> <span data-ttu-id="2cd67-241">Le nom DNS de la passerelle Application Gateway doit être utilisé pour créer un enregistrement CNAME qui pointe les deux applications web sur ce nom DNS.</span><span class="sxs-lookup"><span data-stu-id="2cd67-241">The application gateway's DNS name should be used to create a CNAME record, which points the two web applications to this DNS name.</span></span> <span data-ttu-id="2cd67-242">L’utilisation de A-records n’est pas recommandée étant donné que l’adresse IP virtuelle peut changer lors du redémarrage de la passerelle Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="2cd67-242">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="2cd67-243">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2cd67-243">Next steps</span></span>

<span data-ttu-id="2cd67-244">Pour en savoir plus sur le renforcement de la sécurité de vos applications web avec un pare-feu d’applications Web via la passerelle Application Gateway, consultez la rubrique [Vue d’ensemble du pare-feu d'applications web](application-gateway-webapplicationfirewall-overview.md)</span><span class="sxs-lookup"><span data-stu-id="2cd67-244">Learn about hardening the security of your web applications with Web Application Firewall through Application Gateway by visiting [Web Application Firewall Overview](application-gateway-webapplicationfirewall-overview.md)</span></span>

[scenario]: ./media/application-gateway-end-to-end-SSL-powershell/scenario.png
