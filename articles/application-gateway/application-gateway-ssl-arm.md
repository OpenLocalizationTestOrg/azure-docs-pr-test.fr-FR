---
title: "Configurer le déchargement SSL - Passerelle Azure Application Gateway - PowerShell | Microsoft Docs"
description: "Cette page fournit des instructions pour la création d’une passerelle Application Gateway pour le déchargement SSL à l’aide d’Azure Resource Manager"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 3c3681e0-f928-4682-9d97-567f8e278e13
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: gwallace
ms.openlocfilehash: ededabc7c665d6bb05b91e4d21d01fb1379add32
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-azure-resource-manager"></a><span data-ttu-id="35191-103">Configuration d’une passerelle Application Gateway pour le déchargement SSL à l’aide d’Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="35191-103">Configure an application gateway for SSL offload by using Azure Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="35191-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="35191-104">Azure portal</span></span>](application-gateway-ssl-portal.md)
> * [<span data-ttu-id="35191-105">Commandes PowerShell pour Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="35191-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ssl-arm.md)
> * [<span data-ttu-id="35191-106">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="35191-106">Azure Classic PowerShell</span></span>](application-gateway-ssl.md)
> * [<span data-ttu-id="35191-107">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="35191-107">Azure CLI 2.0</span></span>](application-gateway-ssl-cli.md)

<span data-ttu-id="35191-108">Il est possible de configurer Azure Application Gateway de façon à mettre fin à la session SSL (Secure Sockets Layer) sur la passerelle pour éviter les tâches de déchiffrement SSL coûteuses au niveau de la batterie de serveurs web.</span><span class="sxs-lookup"><span data-stu-id="35191-108">Azure Application Gateway can be configured to terminate the Secure Sockets Layer (SSL) session at the gateway to avoid costly SSL decryption tasks to happen at the web farm.</span></span> <span data-ttu-id="35191-109">Le déchargement SSL simplifie aussi la configuration de serveur principal et la gestion de l’application web.</span><span class="sxs-lookup"><span data-stu-id="35191-109">SSL offload also simplifies the front-end server setup and management of the web application.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="35191-110">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="35191-110">Before you begin</span></span>

1. <span data-ttu-id="35191-111">Installez la dernière version des applets de commande Azure PowerShell à l’aide de Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="35191-111">Install the latest version of the Azure PowerShell cmdlets by using the Web Platform Installer.</span></span> <span data-ttu-id="35191-112">Vous pouvez télécharger et installer la dernière version à partir de la section **Windows PowerShell** de la [page Téléchargements](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="35191-112">You can download and install the latest version from the **Windows PowerShell** section of the [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="35191-113">Vous créez un réseau virtuel et un sous-réseau pour la passerelle Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="35191-113">You create a virtual network and a subnet for the application gateway.</span></span> <span data-ttu-id="35191-114">Assurez-vous qu’aucun ordinateur virtuel ou déploiement cloud n’utilise le sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="35191-114">Make sure that no virtual machines or cloud deployments are using the subnet.</span></span> <span data-ttu-id="35191-115">La passerelle Application Gateway doit être seule sur un sous-réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="35191-115">Application Gateway must be by itself in a virtual network subnet.</span></span>
3. <span data-ttu-id="35191-116">Les serveurs que vous configurez pour utiliser la passerelle Application Gateway doivent exister ou vous devez créer leurs points de terminaison sur le réseau virtuel ou avec une adresse IP/VIP publique affectée.</span><span class="sxs-lookup"><span data-stu-id="35191-116">The servers you configure to use the application gateway must exist or have their endpoints created either in the virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-to-create-an-application-gateway"></a><span data-ttu-id="35191-117">Quels sont les éléments nécessaires pour créer une passerelle Application Gateway ?</span><span class="sxs-lookup"><span data-stu-id="35191-117">What is required to create an application gateway?</span></span>

* <span data-ttu-id="35191-118">**Pool de serveurs principaux :** liste des adresses IP des serveurs principaux.</span><span class="sxs-lookup"><span data-stu-id="35191-118">**Back-end server pool:** The list of IP addresses of the back-end servers.</span></span> <span data-ttu-id="35191-119">Les adresses IP répertoriées doivent appartenir au sous-réseau de réseau virtuel ou doivent correspondre à une adresse IP/VIP publique.</span><span class="sxs-lookup"><span data-stu-id="35191-119">The IP addresses listed should either belong to the virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="35191-120">**Paramètres du pool de serveurs principaux :** chaque pool comporte des paramètres tels que le port, le protocole et une affinité basée sur des cookies.</span><span class="sxs-lookup"><span data-stu-id="35191-120">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="35191-121">Ces paramètres sont liés à un pool et sont appliqués à tous les serveurs du pool.</span><span class="sxs-lookup"><span data-stu-id="35191-121">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="35191-122">**Port frontal :** il s’agit du port public ouvert sur la passerelle Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="35191-122">**Front-end port:** This port is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="35191-123">Le trafic atteint ce port, puis il est redirigé vers l’un des serveurs principaux.</span><span class="sxs-lookup"><span data-stu-id="35191-123">Traffic hits this port, and then gets redirected to one of the back-end servers.</span></span>
* <span data-ttu-id="35191-124">**Écouteur :** l’écouteur a un port frontal, un protocole (Http ou Https, avec respect de la casse) et le nom du certificat SSL (en cas de configuration du déchargement SSL).</span><span class="sxs-lookup"><span data-stu-id="35191-124">**Listener:** The listener has a front-end port, a protocol (Http or Https, these settings are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="35191-125">**Règle :** la règle lie l’écouteur et le pool de serveurs principaux et définit vers quel pool de serveurs principaux le trafic doit être dirigé quand il atteint un écouteur spécifique.</span><span class="sxs-lookup"><span data-stu-id="35191-125">**Rule:** The rule binds the listener and the back-end server pool and defines which back-end server pool the traffic should be directed to when it hits a particular listener.</span></span> <span data-ttu-id="35191-126">Actuellement, seule la règle *de base* est prise en charge.</span><span class="sxs-lookup"><span data-stu-id="35191-126">Currently, only the *basic* rule is supported.</span></span> <span data-ttu-id="35191-127">La règle de *base* est la distribution de charge par tourniquet.</span><span class="sxs-lookup"><span data-stu-id="35191-127">The *basic* rule is round-robin load distribution.</span></span>

<span data-ttu-id="35191-128">**Notes de configuration supplémentaires :**</span><span class="sxs-lookup"><span data-stu-id="35191-128">**Additional configuration notes**</span></span>

<span data-ttu-id="35191-129">Pour configurer des certificats SSL, le protocole dans **HttpListener** doit passer à *Https* (sensible à la casse).</span><span class="sxs-lookup"><span data-stu-id="35191-129">For SSL certificates configuration, the protocol in **HttpListener** should change to *Https* (case sensitive).</span></span> <span data-ttu-id="35191-130">L’élément **SslCertificate** doit être ajouté à **HttpListener** avec la valeur de variable configurée pour le certificat SSL.</span><span class="sxs-lookup"><span data-stu-id="35191-130">The **SslCertificate** element is added to **HttpListener** with the variable value configured for the SSL certificate.</span></span> <span data-ttu-id="35191-131">Le port du serveur frontal doit être mis à jour sur 443.</span><span class="sxs-lookup"><span data-stu-id="35191-131">The front-end port should be updated to 443.</span></span>

<span data-ttu-id="35191-132">**Pour activer l’affinité basée sur les cookies**: une passerelle Application Gateway peut être configurée pour garantir qu’une requête d’une session client est toujours dirigée vers la même machine virtuelle dans la batterie de serveurs web.</span><span class="sxs-lookup"><span data-stu-id="35191-132">**To enable cookie-based affinity**: An application gateway can be configured to ensure that a request from a client session is always directed to the same VM in the web farm.</span></span> <span data-ttu-id="35191-133">Ce scénario est réalisé par l’injection d’un cookie de session, qui permet à la passerelle de diriger le trafic de manière appropriée.</span><span class="sxs-lookup"><span data-stu-id="35191-133">This scenario is done by injection of a session cookie that allows the gateway to direct traffic appropriately.</span></span> <span data-ttu-id="35191-134">Pour activer l’affinité basée sur les cookies, définissez **CookieBasedAffinity** sur *Activé* dans l’élément **BackendHttpSettings**.</span><span class="sxs-lookup"><span data-stu-id="35191-134">To enable cookie-based affinity, set **CookieBasedAffinity** to *Enabled* in the **BackendHttpSettings** element.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="35191-135">Créer une passerelle Application Gateway</span><span class="sxs-lookup"><span data-stu-id="35191-135">Create an application gateway</span></span>

<span data-ttu-id="35191-136">La différence entre l’utilisation du modèle de déploiement Azure Classic et celle d’Azure Resource Manager réside dans l’ordre de création de la passerelle Application Gateway et des éléments à configurer.</span><span class="sxs-lookup"><span data-stu-id="35191-136">The difference between using the Azure Classic deployment model and Azure Resource Manager is the order that you create an application gateway and the items that need to be configured.</span></span>

<span data-ttu-id="35191-137">Avec Resource Manager, tous les composants d’une passerelle Application Gateway sont configurés individuellement, puis regroupés pour créer une ressource Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="35191-137">With Resource Manager, all components of an application gateway are configured individually and then put together to create an application gateway resource.</span></span>

<span data-ttu-id="35191-138">La procédure de création d’une passerelle Application Gateway comporte les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="35191-138">Here are the steps needed to create an application gateway:</span></span>

1. <span data-ttu-id="35191-139">Créer un groupe de ressources pour Resource Manager</span><span class="sxs-lookup"><span data-stu-id="35191-139">Create a resource group for Resource Manager</span></span>
2. <span data-ttu-id="35191-140">Créer un réseau virtuel, un sous-réseau et une adresse IP publique pour la passerelle Application Gateway</span><span class="sxs-lookup"><span data-stu-id="35191-140">Create virtual network, subnet, and public IP for the application gateway</span></span>
3. <span data-ttu-id="35191-141">Créer un objet de configuration de passerelle Application Gateway</span><span class="sxs-lookup"><span data-stu-id="35191-141">Create an application gateway configuration object</span></span>
4. <span data-ttu-id="35191-142">Créer une ressource de passerelle d’application</span><span class="sxs-lookup"><span data-stu-id="35191-142">Create an application gateway resource</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="35191-143">Créer un groupe de ressources pour Resource Manager</span><span class="sxs-lookup"><span data-stu-id="35191-143">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="35191-144">Veillez à passer en mode PowerShell pour utiliser les applets de commande d’Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="35191-144">Make sure that you switch PowerShell mode to use the Azure Resource Manager cmdlets.</span></span> <span data-ttu-id="35191-145">Pour plus d’informations, voir l’article [Utilisation de Windows Powershell avec Azure Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="35191-145">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="35191-146">Étape 1</span><span class="sxs-lookup"><span data-stu-id="35191-146">Step 1</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a><span data-ttu-id="35191-147">Étape 2</span><span class="sxs-lookup"><span data-stu-id="35191-147">Step 2</span></span>

<span data-ttu-id="35191-148">Vérifiez les abonnements associés au compte.</span><span class="sxs-lookup"><span data-stu-id="35191-148">Check the subscriptions for the account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="35191-149">Vous êtes invité à saisir vos informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="35191-149">You are prompted to authenticate with your credentials.</span></span>

### <a name="step-3"></a><span data-ttu-id="35191-150">Étape 3 :</span><span class="sxs-lookup"><span data-stu-id="35191-150">Step 3</span></span>

<span data-ttu-id="35191-151">Parmi vos abonnements Azure, choisissez celui que vous souhaitez utiliser.</span><span class="sxs-lookup"><span data-stu-id="35191-151">Choose which of your Azure subscriptions to use.</span></span>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a><span data-ttu-id="35191-152">Étape 4</span><span class="sxs-lookup"><span data-stu-id="35191-152">Step 4</span></span>

<span data-ttu-id="35191-153">Créez un groupe de ressources (ignorez cette étape si vous utilisez un groupe de ressources existant).</span><span class="sxs-lookup"><span data-stu-id="35191-153">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

<span data-ttu-id="35191-154">Azure Resource Manager requiert que tous les groupes de ressources spécifient un emplacement.</span><span class="sxs-lookup"><span data-stu-id="35191-154">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="35191-155">Ce paramètre est utilisé comme emplacement par défaut des ressources de ce groupe.</span><span class="sxs-lookup"><span data-stu-id="35191-155">This setting is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="35191-156">Assurez-vous que toutes les commandes pour la création d’une passerelle Application Gateway utilisent le même groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="35191-156">Make sure that all commands to create an application gateway uses the same resource group.</span></span>

<span data-ttu-id="35191-157">Dans l’exemple ci-dessus, nous avons créé un groupe de ressources appelé **appgw-RG**, ainsi que l’emplacement **West US**.</span><span class="sxs-lookup"><span data-stu-id="35191-157">In the example above, we created a resource group called **appgw-RG** and location **West US**.</span></span>

## <a name="create-a-virtual-network-and-a-subnet-for-the-application-gateway"></a><span data-ttu-id="35191-158">Créer un réseau virtuel et un sous-réseau pour la passerelle Application Gateway</span><span class="sxs-lookup"><span data-stu-id="35191-158">Create a virtual network and a subnet for the application gateway</span></span>

<span data-ttu-id="35191-159">L’exemple ci-après indique comment créer un réseau virtuel à l’aide de Resource Manager :</span><span class="sxs-lookup"><span data-stu-id="35191-159">The following example shows how to create a virtual network by using Resource Manager:</span></span>

### <a name="step-1"></a><span data-ttu-id="35191-160">Étape 1</span><span class="sxs-lookup"><span data-stu-id="35191-160">Step 1</span></span>

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

<span data-ttu-id="35191-161">Cet exemple attribue la plage d’adresses 10.0.0.0/24 à une variable subnet à utiliser pour créer un réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="35191-161">This sample assigns the address range 10.0.0.0/24 to a subnet variable to be used to create a virtual network.</span></span>

### <a name="step-2"></a><span data-ttu-id="35191-162">Étape 2 :</span><span class="sxs-lookup"><span data-stu-id="35191-162">Step 2</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet
```

<span data-ttu-id="35191-163">Cet exemple crée un réseau virtuel nommé **appgwvnet** dans le groupe de ressources **appw-rg** pour la région États-Unis de l’Ouest à l’aide du préfixe 10.0.0.0/16 avec le sous-réseau 10.0.0.0/24.</span><span class="sxs-lookup"><span data-stu-id="35191-163">This sample creates a virtual network named **appgwvnet** in resource group **appgw-rg** for the West US region using the prefix 10.0.0.0/16 with subnet 10.0.0.0/24.</span></span>

### <a name="step-3"></a><span data-ttu-id="35191-164">Étape 3</span><span class="sxs-lookup"><span data-stu-id="35191-164">Step 3</span></span>

```powershell
$subnet = $vnet.Subnets[0]
```

<span data-ttu-id="35191-165">Cet exemple assigne l’objet de sous-réseau à la variable $subnet pour les étapes suivantes.</span><span class="sxs-lookup"><span data-stu-id="35191-165">This sample assigns the subnet object to variable $subnet for the next steps.</span></span>

## <a name="create-a-public-ip-address-for-the-front-end-configuration"></a><span data-ttu-id="35191-166">Création d'une adresse IP publique pour la configuration frontale</span><span class="sxs-lookup"><span data-stu-id="35191-166">Create a public IP address for the front-end configuration</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

<span data-ttu-id="35191-167">Cet exemple crée une ressource IP publique **publicIP01** dans le groupe de ressources **appw-rg** pour la région États-Unis de l’Ouest.</span><span class="sxs-lookup"><span data-stu-id="35191-167">This sample creates a public IP resource **publicIP01** in resource group **appgw-rg** for the West US region.</span></span>

## <a name="create-an-application-gateway-configuration-object"></a><span data-ttu-id="35191-168">Créer un objet de configuration de passerelle Application Gateway</span><span class="sxs-lookup"><span data-stu-id="35191-168">Create an application gateway configuration object</span></span>

### <a name="step-1"></a><span data-ttu-id="35191-169">Étape 1</span><span class="sxs-lookup"><span data-stu-id="35191-169">Step 1</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

<span data-ttu-id="35191-170">Cet exemple crée une configuration IP de passerelle Application Gateway nommée **gatewayIP01**.</span><span class="sxs-lookup"><span data-stu-id="35191-170">This sample creates an application gateway IP configuration named **gatewayIP01**.</span></span> <span data-ttu-id="35191-171">Lorsque la passerelle Application Gateway démarre, elle sélectionne une adresse IP à partir du sous-réseau configuré et achemine le trafic réseau vers les adresses IP du pool IP principal.</span><span class="sxs-lookup"><span data-stu-id="35191-171">When Application Gateway starts, it picks up an IP address from the subnet configured and route network traffic to the IP addresses in the back-end IP pool.</span></span> <span data-ttu-id="35191-172">Gardez à l’esprit que chaque instance utilise une adresse IP unique.</span><span class="sxs-lookup"><span data-stu-id="35191-172">Keep in mind that each instance takes one IP address.</span></span>

### <a name="step-2"></a><span data-ttu-id="35191-173">Étape 2 :</span><span class="sxs-lookup"><span data-stu-id="35191-173">Step 2</span></span>

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221,134.170.185.50
```

<span data-ttu-id="35191-174">Cet exemple configure le pool d’adresses IP principal nommé **pool01** avec les adresses IP **134.170.185.46**, **134.170.188.221** et **134.170.185.50**.</span><span class="sxs-lookup"><span data-stu-id="35191-174">This sample configures the back-end IP address pool named **pool01** with IP addresses **134.170.185.46**, **134.170.188.221**, **134.170.185.50**.</span></span> <span data-ttu-id="35191-175">Ces valeurs correspondent aux adresses IP qui recevront le trafic réseau provenant du point de terminaison IP frontal.</span><span class="sxs-lookup"><span data-stu-id="35191-175">Those values are the IP addresses that receive the network traffic that comes from the front-end IP endpoint.</span></span> <span data-ttu-id="35191-176">Remplacez les adresses IP de l’exemple précédent par les adresses IP des points de terminaison de votre application web.</span><span class="sxs-lookup"><span data-stu-id="35191-176">Replace the IP addresses from the preceding example with the IP addresses of your web application endpoints.</span></span>

### <a name="step-3"></a><span data-ttu-id="35191-177">Étape 3</span><span class="sxs-lookup"><span data-stu-id="35191-177">Step 3</span></span>

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Enabled
```

<span data-ttu-id="35191-178">Cet exemple configure le paramètre de passerelle Application Gateway **poolsetting01** pour le trafic réseau à charge équilibrée dans le pool principal.</span><span class="sxs-lookup"><span data-stu-id="35191-178">This sample configures application gateway setting **poolsetting01** to load-balanced network traffic in the back-end pool.</span></span>

### <a name="step-4"></a><span data-ttu-id="35191-179">Étape 4</span><span class="sxs-lookup"><span data-stu-id="35191-179">Step 4</span></span>

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 443
```

<span data-ttu-id="35191-180">Cet exemple configure le port IP frontal nommé **frontendport01** pour le point de terminaison IP public.</span><span class="sxs-lookup"><span data-stu-id="35191-180">This sample configures the front-end IP port named **frontendport01** for the public IP endpoint.</span></span>

### <a name="step-5"></a><span data-ttu-id="35191-181">Étape 5</span><span class="sxs-lookup"><span data-stu-id="35191-181">Step 5</span></span>

```powershell
$cert = New-AzureRmApplicationGatewaySslCertificate -Name cert01 -CertificateFile <full path for certificate file> -Password "<password>"
```

<span data-ttu-id="35191-182">Cet exemple configure le certificat utilisé pour la connexion SSL.</span><span class="sxs-lookup"><span data-stu-id="35191-182">This sample configures the certificate used for SSL connection.</span></span> <span data-ttu-id="35191-183">Le certificat doit être au format .pfx et le mot de passe contenir entre 4 et 12 caractères.</span><span class="sxs-lookup"><span data-stu-id="35191-183">The certificate needs to be in .pfx format, and the password must be between 4 to 12 characters.</span></span>

### <a name="step-6"></a><span data-ttu-id="35191-184">Étape 6</span><span class="sxs-lookup"><span data-stu-id="35191-184">Step 6</span></span>

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip
```

<span data-ttu-id="35191-185">Cet exemple crée la configuration IP frontale nommée **fipconfig01** et associe l’adresse IP publique à cette configuration.</span><span class="sxs-lookup"><span data-stu-id="35191-185">This sample creates the front-end IP configuration named **fipconfig01** and associates the public IP address with the front-end IP configuration.</span></span>

### <a name="step-7"></a><span data-ttu-id="35191-186">Étape 7</span><span class="sxs-lookup"><span data-stu-id="35191-186">Step 7</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SslCertificate $cert
```

<span data-ttu-id="35191-187">Cet exemple crée l’écouteur nommé **listener01** et associe le port frontal à la configuration IP et au certificat du serveur frontal.</span><span class="sxs-lookup"><span data-stu-id="35191-187">This sample creates the listener name **listener01** and associates the front-end port to the front-end IP configuration and certificate.</span></span>

### <a name="step-8"></a><span data-ttu-id="35191-188">Étape 8</span><span class="sxs-lookup"><span data-stu-id="35191-188">Step 8</span></span>

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

<span data-ttu-id="35191-189">Cet exemple crée la règle d’acheminement d’équilibrage de charge nommée **rule01** qui configure le comportement d’équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="35191-189">This sample creates the load balancer routing rule named **rule01** that configures the load balancer behavior.</span></span>

### <a name="step-9"></a><span data-ttu-id="35191-190">Étape 9</span><span class="sxs-lookup"><span data-stu-id="35191-190">Step 9</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

<span data-ttu-id="35191-191">Cet exemple configure la taille d’instance de la passerelle Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="35191-191">This sample configures the instance size of the application gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="35191-192">La valeur par défaut du paramètre *InstanceCount* est de 2, avec une valeur maximale de 10.</span><span class="sxs-lookup"><span data-stu-id="35191-192">The default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="35191-193">La valeur par défaut du paramètre *GatewaySize* est Medium.</span><span class="sxs-lookup"><span data-stu-id="35191-193">The default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="35191-194">Vous pouvez choisir entre Standard_Small, Standard_Medium et Standard_Large.</span><span class="sxs-lookup"><span data-stu-id="35191-194">You can choose between Standard_Small, Standard_Medium, and Standard_Large.</span></span>

### <a name="step-10"></a><span data-ttu-id="35191-195">Étape 10</span><span class="sxs-lookup"><span data-stu-id="35191-195">Step 10</span></span>

```powershell
$policy = New-AzureRmApplicationGatewaySslPolicy -PolicyType Predefined -PolicyName AppGwSslPolicy20170401S
```

<span data-ttu-id="35191-196">Cette étape permet de définir la stratégie SSL à utiliser sur la passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="35191-196">This step defines the SSL policy to use on the application gateway.</span></span> <span data-ttu-id="35191-197">Visitez la page [Configurer les versions de stratégie SSL et les suites de chiffrement sur Application Gateway](application-gateway-configure-ssl-policy-powershell.md) pour en savoir plus.</span><span class="sxs-lookup"><span data-stu-id="35191-197">Visit [Configure SSL policy versions and cipher suites on Application Gateway](application-gateway-configure-ssl-policy-powershell.md) to learn more.</span></span>

## <a name="create-an-application-gateway-by-using-new-azureapplicationgateway"></a><span data-ttu-id="35191-198">Créer une passerelle Application Gateway avec New-AzureApplicationGateway</span><span class="sxs-lookup"><span data-stu-id="35191-198">Create an application gateway by using New-AzureApplicationGateway</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -SslCertificates $cert -SslPolicy $policy
```

<span data-ttu-id="35191-199">Cet exemple crée une passerelle Application Gateway avec tous les éléments de configuration de la procédure précédente.</span><span class="sxs-lookup"><span data-stu-id="35191-199">This sample creates an application gateway with all configuration items from the preceding steps.</span></span> <span data-ttu-id="35191-200">Dans notre exemple, la passerelle Application Gateway est appelée **appgwtest**.</span><span class="sxs-lookup"><span data-stu-id="35191-200">In the example, the application gateway is called **appgwtest**.</span></span>

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="35191-201">Obtenir le nom DNS d’une passerelle Application Gateway</span><span class="sxs-lookup"><span data-stu-id="35191-201">Get application gateway DNS name</span></span>

<span data-ttu-id="35191-202">Une fois la passerelle créée, l’étape suivante consiste à configurer le serveur frontal pour la communication.</span><span class="sxs-lookup"><span data-stu-id="35191-202">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="35191-203">Lorsque vous utilisez une adresse IP publique, la passerelle Application Gateway requiert un nom DNS attribué dynamiquement, ce qui n’est pas convivial.</span><span class="sxs-lookup"><span data-stu-id="35191-203">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="35191-204">Pour s’assurer que les utilisateurs finaux peuvent atteindre la passerelle d’application, un enregistrement CNAME peut être utilisé pour pointer vers le point de terminaison public de la passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="35191-204">To ensure end users can hit the application gateway, a CNAME record can be used to point to the public endpoint of the application gateway.</span></span> <span data-ttu-id="35191-205">[Configuration d’un nom de domaine personnalisé pour Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="35191-205">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="35191-206">Pour ce faire, récupérez les détails de la passerelle Application Gateway et de son nom IP/DNS associé à l’aide de l’élément PublicIPAddress attaché à la passerelle Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="35191-206">To do this, retrieve details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span></span> <span data-ttu-id="35191-207">Le nom DNS de la passerelle Application Gateway doit être utilisé pour créer un enregistrement CNAME qui pointe les deux applications web sur ce nom DNS.</span><span class="sxs-lookup"><span data-stu-id="35191-207">The application gateway's DNS name should be used to create a CNAME record, which points the two web applications to this DNS name.</span></span> <span data-ttu-id="35191-208">L’utilisation de A-records n’est pas recommandée étant donné que l’adresse IP virtuelle peut changer lors du redémarrage de la passerelle Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="35191-208">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span></span>


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

## <a name="next-steps"></a><span data-ttu-id="35191-209">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="35191-209">Next steps</span></span>

<span data-ttu-id="35191-210">Si vous souhaitez configurer une passerelle Application Gateway à utiliser avec l’équilibreur de charge interne (ILB), consultez [Création d’une passerelle Application Gateway avec un équilibrage de charge interne (ILB)](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="35191-210">If you want to configure an application gateway to use with an internal load balancer (ILB), see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="35191-211">Si vous souhaitez plus d'informations sur les options d'équilibrage de charge en général, consultez :</span><span class="sxs-lookup"><span data-stu-id="35191-211">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="35191-212">Équilibrage de charge Azure</span><span class="sxs-lookup"><span data-stu-id="35191-212">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="35191-213">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="35191-213">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

