---
title: "aaaConfigure SSL décharger - passerelle d’Application Azure - PowerShell | Documents Microsoft"
description: "Cette page fournit toocreate instructions déchargement d’une passerelle d’application avec SSL à l’aide du Gestionnaire de ressources Azure"
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
ms.openlocfilehash: c2855d8d3caaa97ec05475c67ff0f8dce72ef2a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-azure-resource-manager"></a><span data-ttu-id="211e9-103">Configuration d’une passerelle Application Gateway pour le déchargement SSL à l’aide d’Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="211e9-103">Configure an application gateway for SSL offload by using Azure Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="211e9-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="211e9-104">Azure portal</span></span>](application-gateway-ssl-portal.md)
> * [<span data-ttu-id="211e9-105">Commandes PowerShell pour Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="211e9-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ssl-arm.md)
> * [<span data-ttu-id="211e9-106">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="211e9-106">Azure Classic PowerShell</span></span>](application-gateway-ssl.md)
> * [<span data-ttu-id="211e9-107">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="211e9-107">Azure CLI 2.0</span></span>](application-gateway-ssl-cli.md)

<span data-ttu-id="211e9-108">Passerelle d’Application Azure peut être configuré tooterminate hello Secure Sockets Layer (SSL) session à hello passerelle tooavoid coûteux SSL déchiffrement tâches toohappen au niveau de la batterie de serveurs web hello.</span><span class="sxs-lookup"><span data-stu-id="211e9-108">Azure Application Gateway can be configured tooterminate hello Secure Sockets Layer (SSL) session at hello gateway tooavoid costly SSL decryption tasks toohappen at hello web farm.</span></span> <span data-ttu-id="211e9-109">Déchargement SSL simplifie également la configuration de serveur frontal de hello et la gestion d’application web de hello.</span><span class="sxs-lookup"><span data-stu-id="211e9-109">SSL offload also simplifies hello front-end server setup and management of hello web application.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="211e9-110">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="211e9-110">Before you begin</span></span>

1. <span data-ttu-id="211e9-111">Installer version la plus récente des applets de commande PowerShell Azure hello hello à l’aide de hello Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="211e9-111">Install hello latest version of hello Azure PowerShell cmdlets by using hello Web Platform Installer.</span></span> <span data-ttu-id="211e9-112">Vous pouvez télécharger et installer la version la plus récente hello de hello **Windows PowerShell** section Hello [page Téléchargements](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="211e9-112">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="211e9-113">Vous créez un réseau virtuel et un sous-réseau pour la passerelle d’application hello.</span><span class="sxs-lookup"><span data-stu-id="211e9-113">You create a virtual network and a subnet for hello application gateway.</span></span> <span data-ttu-id="211e9-114">Assurez-vous qu’aucun ordinateur virtuel ou les déploiements de cloud ne sont à l’aide de sous-réseau de hello.</span><span class="sxs-lookup"><span data-stu-id="211e9-114">Make sure that no virtual machines or cloud deployments are using hello subnet.</span></span> <span data-ttu-id="211e9-115">La passerelle Application Gateway doit être seule sur un sous-réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="211e9-115">Application Gateway must be by itself in a virtual network subnet.</span></span>
3. <span data-ttu-id="211e9-116">serveurs Hello vous configurez la passerelle d’application toouse hello doivent exister ou ont créé leurs points de terminaison dans le réseau virtuel de hello ou avec une adresse IP publique/VIP attribué.</span><span class="sxs-lookup"><span data-stu-id="211e9-116">hello servers you configure toouse hello application gateway must exist or have their endpoints created either in hello virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-toocreate-an-application-gateway"></a><span data-ttu-id="211e9-117">Qu’est requis toocreate une passerelle d’application ?</span><span class="sxs-lookup"><span data-stu-id="211e9-117">What is required toocreate an application gateway?</span></span>

* <span data-ttu-id="211e9-118">**Pool de serveur principal :** liste hello des adresses IP des serveurs principaux de hello.</span><span class="sxs-lookup"><span data-stu-id="211e9-118">**Back-end server pool:** hello list of IP addresses of hello back-end servers.</span></span> <span data-ttu-id="211e9-119">adresses IP de Hello répertoriés doivent appartenir soit de sous-réseau de réseau virtuel toohello ou doivent être une adresse IP/VIP publique.</span><span class="sxs-lookup"><span data-stu-id="211e9-119">hello IP addresses listed should either belong toohello virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="211e9-120">**Paramètres du pool de serveurs principaux :** chaque pool comporte des paramètres tels que le port, le protocole et une affinité basée sur des cookies.</span><span class="sxs-lookup"><span data-stu-id="211e9-120">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="211e9-121">Ces paramètres sont lié tooa pool et sont des serveurs tooall appliqué dans le pool de hello.</span><span class="sxs-lookup"><span data-stu-id="211e9-121">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="211e9-122">**Port frontal :** ce port est le port public hello qui est ouvert sur la passerelle d’application hello.</span><span class="sxs-lookup"><span data-stu-id="211e9-122">**Front-end port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="211e9-123">Le trafic atteint ce port et obtient redirigés tooone de hello sur les serveurs principaux.</span><span class="sxs-lookup"><span data-stu-id="211e9-123">Traffic hits this port, and then gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="211e9-124">**Écouteur :** hello port d’écoute utilise un port frontal, un protocole (Http ou Https, ces paramètres respectent la casse) et le nom du certificat SSL hello (si le déchargement de la configuration de SSL).</span><span class="sxs-lookup"><span data-stu-id="211e9-124">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these settings are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="211e9-125">**La règle :** règle de hello lie le port d’écoute hello et pool de serveur principal hello et définit le trafic de hello de pool de serveur principal doit être dirigée toowhen il atteint un écouteur particulier.</span><span class="sxs-lookup"><span data-stu-id="211e9-125">**Rule:** hello rule binds hello listener and hello back-end server pool and defines which back-end server pool hello traffic should be directed toowhen it hits a particular listener.</span></span> <span data-ttu-id="211e9-126">Actuellement, seuls hello *base* règle est pris en charge.</span><span class="sxs-lookup"><span data-stu-id="211e9-126">Currently, only hello *basic* rule is supported.</span></span> <span data-ttu-id="211e9-127">Hello *base* règle est la distribution de la charge de tourniquet.</span><span class="sxs-lookup"><span data-stu-id="211e9-127">hello *basic* rule is round-robin load distribution.</span></span>

<span data-ttu-id="211e9-128">**Notes de configuration supplémentaires :**</span><span class="sxs-lookup"><span data-stu-id="211e9-128">**Additional configuration notes**</span></span>

<span data-ttu-id="211e9-129">Pour configurer des certificats SSL, hello protocole dans **HttpListener** doit également modifier*Https* (sensible à la casse).</span><span class="sxs-lookup"><span data-stu-id="211e9-129">For SSL certificates configuration, hello protocol in **HttpListener** should change too*Https* (case sensitive).</span></span> <span data-ttu-id="211e9-130">Hello **certificat SSL** l’élément est ajouté trop**HttpListener** avec la valeur de la variable hello configuré pour le certificat SSL de hello.</span><span class="sxs-lookup"><span data-stu-id="211e9-130">hello **SslCertificate** element is added too**HttpListener** with hello variable value configured for hello SSL certificate.</span></span> <span data-ttu-id="211e9-131">le port frontal Hello doit être too443 mis à jour.</span><span class="sxs-lookup"><span data-stu-id="211e9-131">hello front-end port should be updated too443.</span></span>

<span data-ttu-id="211e9-132">**affinité basé sur cookie de tooenable**: une passerelle d’application peut être configurée tooensure qu’une demande à partir d’une session cliente est toujours dirigée toohello même machine virtuelle dans la batterie de serveurs web hello.</span><span class="sxs-lookup"><span data-stu-id="211e9-132">**tooenable cookie-based affinity**: An application gateway can be configured tooensure that a request from a client session is always directed toohello same VM in hello web farm.</span></span> <span data-ttu-id="211e9-133">Ce scénario est effectué par injection d’un cookie de session qui autorise le trafic toodirect de passerelle de hello de manière appropriée.</span><span class="sxs-lookup"><span data-stu-id="211e9-133">This scenario is done by injection of a session cookie that allows hello gateway toodirect traffic appropriately.</span></span> <span data-ttu-id="211e9-134">l’affinité basé sur cookie tooenable, définie **CookieBasedAffinity** trop*activé* Bonjour **paramètres** élément.</span><span class="sxs-lookup"><span data-stu-id="211e9-134">tooenable cookie-based affinity, set **CookieBasedAffinity** too*Enabled* in hello **BackendHttpSettings** element.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="211e9-135">Créer une passerelle Application Gateway</span><span class="sxs-lookup"><span data-stu-id="211e9-135">Create an application gateway</span></span>

<span data-ttu-id="211e9-136">Hello différence du modèle de déploiement Azure Classic hello et Gestionnaire de ressources Azure est commande hello que vous créez une application passerelle et hello éléments nécessitant toobe configuré.</span><span class="sxs-lookup"><span data-stu-id="211e9-136">hello difference between using hello Azure Classic deployment model and Azure Resource Manager is hello order that you create an application gateway and hello items that need toobe configured.</span></span>

<span data-ttu-id="211e9-137">Avec le Gestionnaire de ressources, tous les composants d’une passerelle d’application sont configurées individuellement et ensuite placer toocreate ensemble une ressource de passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="211e9-137">With Resource Manager, all components of an application gateway are configured individually and then put together toocreate an application gateway resource.</span></span>

<span data-ttu-id="211e9-138">Voici une passerelle d’application hello étapes nécessaires toocreate :</span><span class="sxs-lookup"><span data-stu-id="211e9-138">Here are hello steps needed toocreate an application gateway:</span></span>

1. <span data-ttu-id="211e9-139">Créer un groupe de ressources pour Resource Manager</span><span class="sxs-lookup"><span data-stu-id="211e9-139">Create a resource group for Resource Manager</span></span>
2. <span data-ttu-id="211e9-140">Créer le réseau virtuel, sous-réseau et adresse IP publique pour la passerelle d’application hello</span><span class="sxs-lookup"><span data-stu-id="211e9-140">Create virtual network, subnet, and public IP for hello application gateway</span></span>
3. <span data-ttu-id="211e9-141">Créer un objet de configuration de passerelle Application Gateway</span><span class="sxs-lookup"><span data-stu-id="211e9-141">Create an application gateway configuration object</span></span>
4. <span data-ttu-id="211e9-142">Créer une ressource de passerelle d’application</span><span class="sxs-lookup"><span data-stu-id="211e9-142">Create an application gateway resource</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="211e9-143">Créer un groupe de ressources pour Resource Manager</span><span class="sxs-lookup"><span data-stu-id="211e9-143">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="211e9-144">Assurez-vous que vous basculez des applets de commande PowerShell en mode toouse hello Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="211e9-144">Make sure that you switch PowerShell mode toouse hello Azure Resource Manager cmdlets.</span></span> <span data-ttu-id="211e9-145">Pour plus d’informations, voir [Utilisation de Windows PowerShell avec Azure Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="211e9-145">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="211e9-146">Étape 1</span><span class="sxs-lookup"><span data-stu-id="211e9-146">Step 1</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a><span data-ttu-id="211e9-147">Étape 2</span><span class="sxs-lookup"><span data-stu-id="211e9-147">Step 2</span></span>

<span data-ttu-id="211e9-148">Vérifiez les abonnements hello pour le compte de hello.</span><span class="sxs-lookup"><span data-stu-id="211e9-148">Check hello subscriptions for hello account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="211e9-149">Vous êtes invité à tooauthenticate avec vos informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="211e9-149">You are prompted tooauthenticate with your credentials.</span></span>

### <a name="step-3"></a><span data-ttu-id="211e9-150">Étape 3 :</span><span class="sxs-lookup"><span data-stu-id="211e9-150">Step 3</span></span>

<span data-ttu-id="211e9-151">Choisissez parmi vos toouse abonnements Azure.</span><span class="sxs-lookup"><span data-stu-id="211e9-151">Choose which of your Azure subscriptions toouse.</span></span>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a><span data-ttu-id="211e9-152">Étape 4</span><span class="sxs-lookup"><span data-stu-id="211e9-152">Step 4</span></span>

<span data-ttu-id="211e9-153">Créez un groupe de ressources (ignorez cette étape si vous utilisez un groupe de ressources existant).</span><span class="sxs-lookup"><span data-stu-id="211e9-153">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

<span data-ttu-id="211e9-154">Azure Resource Manager requiert que tous les groupes de ressources spécifient un emplacement.</span><span class="sxs-lookup"><span data-stu-id="211e9-154">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="211e9-155">Ce paramètre est utilisé comme emplacement par défaut de hello pour les ressources dans ce groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="211e9-155">This setting is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="211e9-156">Assurez-vous que toutes les commandes toocreate une passerelle d’application utilise hello même groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="211e9-156">Make sure that all commands toocreate an application gateway uses hello same resource group.</span></span>

<span data-ttu-id="211e9-157">Dans l’exemple hello ci-dessus, nous avons créé un groupe de ressources appelé **appgw-RG** et l’emplacement **ouest des États-Unis**.</span><span class="sxs-lookup"><span data-stu-id="211e9-157">In hello example above, we created a resource group called **appgw-RG** and location **West US**.</span></span>

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a><span data-ttu-id="211e9-158">Créer un réseau virtuel et un sous-réseau pour la passerelle d’application hello</span><span class="sxs-lookup"><span data-stu-id="211e9-158">Create a virtual network and a subnet for hello application gateway</span></span>

<span data-ttu-id="211e9-159">Hello suivant montre l’exemple de comment toocreate un réseau virtuel à l’aide du Gestionnaire de ressources :</span><span class="sxs-lookup"><span data-stu-id="211e9-159">hello following example shows how toocreate a virtual network by using Resource Manager:</span></span>

### <a name="step-1"></a><span data-ttu-id="211e9-160">Étape 1</span><span class="sxs-lookup"><span data-stu-id="211e9-160">Step 1</span></span>

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

<span data-ttu-id="211e9-161">Cet exemple assigne hello adresse plage 10.0.0.0/24 tooa sous-réseau toobe variable utilisée toocreate un réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="211e9-161">This sample assigns hello address range 10.0.0.0/24 tooa subnet variable toobe used toocreate a virtual network.</span></span>

### <a name="step-2"></a><span data-ttu-id="211e9-162">Étape 2</span><span class="sxs-lookup"><span data-stu-id="211e9-162">Step 2</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet
```

<span data-ttu-id="211e9-163">Cet exemple crée un réseau virtuel nommé **appgwvnet** dans le groupe de ressources **appgw-rg** pour la région ouest des États-Unis hello à l’aide de hello préfixe 10.0.0.0/16 avec le sous-réseau 10.0.0.0/24.</span><span class="sxs-lookup"><span data-stu-id="211e9-163">This sample creates a virtual network named **appgwvnet** in resource group **appgw-rg** for hello West US region using hello prefix 10.0.0.0/16 with subnet 10.0.0.0/24.</span></span>

### <a name="step-3"></a><span data-ttu-id="211e9-164">Étape 3 :</span><span class="sxs-lookup"><span data-stu-id="211e9-164">Step 3</span></span>

```powershell
$subnet = $vnet.Subnets[0]
```

<span data-ttu-id="211e9-165">Cet exemple assigne hello sous-réseau objet toovariable $subnet pour les étapes suivantes de hello.</span><span class="sxs-lookup"><span data-stu-id="211e9-165">This sample assigns hello subnet object toovariable $subnet for hello next steps.</span></span>

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a><span data-ttu-id="211e9-166">Créer une adresse IP publique pour la configuration frontale de hello</span><span class="sxs-lookup"><span data-stu-id="211e9-166">Create a public IP address for hello front-end configuration</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

<span data-ttu-id="211e9-167">Cet exemple crée une ressource IP publique **publicIP01** dans le groupe de ressources **appgw-rg** pour la région ouest des États-Unis hello.</span><span class="sxs-lookup"><span data-stu-id="211e9-167">This sample creates a public IP resource **publicIP01** in resource group **appgw-rg** for hello West US region.</span></span>

## <a name="create-an-application-gateway-configuration-object"></a><span data-ttu-id="211e9-168">Créer un objet de configuration de passerelle Application Gateway</span><span class="sxs-lookup"><span data-stu-id="211e9-168">Create an application gateway configuration object</span></span>

### <a name="step-1"></a><span data-ttu-id="211e9-169">Étape 1</span><span class="sxs-lookup"><span data-stu-id="211e9-169">Step 1</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

<span data-ttu-id="211e9-170">Cet exemple crée une configuration IP de passerelle Application Gateway nommée **gatewayIP01**.</span><span class="sxs-lookup"><span data-stu-id="211e9-170">This sample creates an application gateway IP configuration named **gatewayIP01**.</span></span> <span data-ttu-id="211e9-171">Au démarrage de la passerelle d’Application, il récupère une adresse IP du sous-réseau hello configuré et acheminer les adresses IP de réseau du trafic toohello dans le pool d’adresses IP hello back-end.</span><span class="sxs-lookup"><span data-stu-id="211e9-171">When Application Gateway starts, it picks up an IP address from hello subnet configured and route network traffic toohello IP addresses in hello back-end IP pool.</span></span> <span data-ttu-id="211e9-172">Gardez à l’esprit que chaque instance utilise une adresse IP unique.</span><span class="sxs-lookup"><span data-stu-id="211e9-172">Keep in mind that each instance takes one IP address.</span></span>

### <a name="step-2"></a><span data-ttu-id="211e9-173">Étape 2</span><span class="sxs-lookup"><span data-stu-id="211e9-173">Step 2</span></span>

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221,134.170.185.50
```

<span data-ttu-id="211e9-174">Cet exemple configure le pool d’adresses IP principal hello nommé **pool01** avec des adresses IP **134.170.185.46**, **134.170.188.221**, **134.170.185.50** .</span><span class="sxs-lookup"><span data-stu-id="211e9-174">This sample configures hello back-end IP address pool named **pool01** with IP addresses **134.170.185.46**, **134.170.188.221**, **134.170.185.50**.</span></span> <span data-ttu-id="211e9-175">Ces valeurs sont des adresses IP hello qui reçoivent le trafic réseau hello qui provient d’un point de terminaison IP frontale hello.</span><span class="sxs-lookup"><span data-stu-id="211e9-175">Those values are hello IP addresses that receive hello network traffic that comes from hello front-end IP endpoint.</span></span> <span data-ttu-id="211e9-176">Remplacer les adresses IP hello hello précédent exemple avec des adresses IP hello de points de terminaison de votre application web.</span><span class="sxs-lookup"><span data-stu-id="211e9-176">Replace hello IP addresses from hello preceding example with hello IP addresses of your web application endpoints.</span></span>

### <a name="step-3"></a><span data-ttu-id="211e9-177">Étape 3 :</span><span class="sxs-lookup"><span data-stu-id="211e9-177">Step 3</span></span>

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Enabled
```

<span data-ttu-id="211e9-178">Cet exemple configure le paramètre de passerelle d’application **poolsetting01** tooload équilibrée de trafic réseau dans le pool principal d’hello.</span><span class="sxs-lookup"><span data-stu-id="211e9-178">This sample configures application gateway setting **poolsetting01** tooload-balanced network traffic in hello back-end pool.</span></span>

### <a name="step-4"></a><span data-ttu-id="211e9-179">Étape 4</span><span class="sxs-lookup"><span data-stu-id="211e9-179">Step 4</span></span>

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 443
```

<span data-ttu-id="211e9-180">Cet exemple configure le port IP frontal hello nommé **frontendport01** pour le point de terminaison IP public hello.</span><span class="sxs-lookup"><span data-stu-id="211e9-180">This sample configures hello front-end IP port named **frontendport01** for hello public IP endpoint.</span></span>

### <a name="step-5"></a><span data-ttu-id="211e9-181">Étape 5</span><span class="sxs-lookup"><span data-stu-id="211e9-181">Step 5</span></span>

```powershell
$cert = New-AzureRmApplicationGatewaySslCertificate -Name cert01 -CertificateFile <full path for certificate file> -Password "<password>"
```

<span data-ttu-id="211e9-182">Cet exemple configure un certificat hello utilisée pour la connexion SSL.</span><span class="sxs-lookup"><span data-stu-id="211e9-182">This sample configures hello certificate used for SSL connection.</span></span> <span data-ttu-id="211e9-183">certificat de Hello doit toobe au format .pfx et hello le mot de passe doit être comprise entre 4 too12 caractères.</span><span class="sxs-lookup"><span data-stu-id="211e9-183">hello certificate needs toobe in .pfx format, and hello password must be between 4 too12 characters.</span></span>

### <a name="step-6"></a><span data-ttu-id="211e9-184">Étape 6</span><span class="sxs-lookup"><span data-stu-id="211e9-184">Step 6</span></span>

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip
```

<span data-ttu-id="211e9-185">Cet exemple crée la configuration IP frontale hello nommée **fipconfig01** et associe hello adresse IP publique avec une configuration IP frontale hello.</span><span class="sxs-lookup"><span data-stu-id="211e9-185">This sample creates hello front-end IP configuration named **fipconfig01** and associates hello public IP address with hello front-end IP configuration.</span></span>

### <a name="step-7"></a><span data-ttu-id="211e9-186">Étape 7</span><span class="sxs-lookup"><span data-stu-id="211e9-186">Step 7</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SslCertificate $cert
```

<span data-ttu-id="211e9-187">Cet exemple crée le nom de l’écouteur hello **listener01** et associe hello configuration IP frontale de port frontal toohello et le certificat.</span><span class="sxs-lookup"><span data-stu-id="211e9-187">This sample creates hello listener name **listener01** and associates hello front-end port toohello front-end IP configuration and certificate.</span></span>

### <a name="step-8"></a><span data-ttu-id="211e9-188">Étape 8</span><span class="sxs-lookup"><span data-stu-id="211e9-188">Step 8</span></span>

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

<span data-ttu-id="211e9-189">Cet exemple crée hello règle équilibreur de charge routage nommé **rule01** qui configure le comportement de programme d’équilibrage de charge hello.</span><span class="sxs-lookup"><span data-stu-id="211e9-189">This sample creates hello load balancer routing rule named **rule01** that configures hello load balancer behavior.</span></span>

### <a name="step-9"></a><span data-ttu-id="211e9-190">Étape 9</span><span class="sxs-lookup"><span data-stu-id="211e9-190">Step 9</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

<span data-ttu-id="211e9-191">Cet exemple configure la taille de l’instance de la passerelle d’application hello hello.</span><span class="sxs-lookup"><span data-stu-id="211e9-191">This sample configures hello instance size of hello application gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="211e9-192">Hello la valeur par défaut de *InstanceCount* est 2, avec une valeur maximale de 10.</span><span class="sxs-lookup"><span data-stu-id="211e9-192">hello default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="211e9-193">Hello la valeur par défaut de *GatewaySize* est moyenne.</span><span class="sxs-lookup"><span data-stu-id="211e9-193">hello default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="211e9-194">Vous pouvez choisir entre Standard_Small, Standard_Medium et Standard_Large.</span><span class="sxs-lookup"><span data-stu-id="211e9-194">You can choose between Standard_Small, Standard_Medium, and Standard_Large.</span></span>

### <a name="step-10"></a><span data-ttu-id="211e9-195">Étape 10</span><span class="sxs-lookup"><span data-stu-id="211e9-195">Step 10</span></span>

```powershell
$policy = New-AzureRmApplicationGatewaySslPolicy -PolicyType Predefined -PolicyName AppGwSslPolicy20170401S
```

<span data-ttu-id="211e9-196">Cette étape définit toouse de stratégie SSL hello sur la passerelle d’application hello.</span><span class="sxs-lookup"><span data-stu-id="211e9-196">This step defines hello SSL policy toouse on hello application gateway.</span></span> <span data-ttu-id="211e9-197">Visitez [versions de stratégie de configuration de SSL et les suites de chiffrement sur la passerelle d’Application](application-gateway-configure-ssl-policy-powershell.md) toolearn plus.</span><span class="sxs-lookup"><span data-stu-id="211e9-197">Visit [Configure SSL policy versions and cipher suites on Application Gateway](application-gateway-configure-ssl-policy-powershell.md) toolearn more.</span></span>

## <a name="create-an-application-gateway-by-using-new-azureapplicationgateway"></a><span data-ttu-id="211e9-198">Créer une passerelle Application Gateway avec New-AzureApplicationGateway</span><span class="sxs-lookup"><span data-stu-id="211e9-198">Create an application gateway by using New-AzureApplicationGateway</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -SslCertificates $cert -SslPolicy $policy
```

<span data-ttu-id="211e9-199">Cet exemple crée une passerelle d’application avec tous les éléments de configuration à partir de hello étapes précédentes.</span><span class="sxs-lookup"><span data-stu-id="211e9-199">This sample creates an application gateway with all configuration items from hello preceding steps.</span></span> <span data-ttu-id="211e9-200">Dans l’exemple de hello, la passerelle d’application hello est appelé **appgwtest**.</span><span class="sxs-lookup"><span data-stu-id="211e9-200">In hello example, hello application gateway is called **appgwtest**.</span></span>

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="211e9-201">Obtenir le nom DNS d’une passerelle Application Gateway</span><span class="sxs-lookup"><span data-stu-id="211e9-201">Get application gateway DNS name</span></span>

<span data-ttu-id="211e9-202">Après la création de la passerelle de hello, hello prochaine étape consiste tooconfigure hello frontal pour la communication.</span><span class="sxs-lookup"><span data-stu-id="211e9-202">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="211e9-203">Lorsque vous utilisez une adresse IP publique, la passerelle Application Gateway requiert un nom DNS attribué dynamiquement, ce qui n’est pas convivial.</span><span class="sxs-lookup"><span data-stu-id="211e9-203">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="211e9-204">les utilisateurs finaux de tooensure pouvez atteindre la passerelle d’application hello, un enregistrement CNAME peut être le point de terminaison utilisé toopoint toohello public de la passerelle d’application hello.</span><span class="sxs-lookup"><span data-stu-id="211e9-204">tooensure end users can hit hello application gateway, a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="211e9-205">[Configuration d’un nom de domaine personnalisé pour Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="211e9-205">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="211e9-206">toodo, détails de récupération de la passerelle d’application hello et son nom IP/DNS associé à l’aide de la passerelle d’application hello PublicIPAddress élément attaché toohello.</span><span class="sxs-lookup"><span data-stu-id="211e9-206">toodo this, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="211e9-207">nom DNS de la passerelle d’application Hello doit être utilisé toocreate un enregistrement CNAME, le nom DNS de points hello deux web applications toothis.</span><span class="sxs-lookup"><span data-stu-id="211e9-207">hello application gateway's DNS name should be used toocreate a CNAME record, which points hello two web applications toothis DNS name.</span></span> <span data-ttu-id="211e9-208">les utilisation de Hello d’enregistrements d’un n’est pas recommandée étant donné que l’adresse IP virtuelle hello peut changer lors du redémarrage de la passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="211e9-208">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>


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

## <a name="next-steps"></a><span data-ttu-id="211e9-209">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="211e9-209">Next steps</span></span>

<span data-ttu-id="211e9-210">Si vous souhaitez tooconfigure un toouse de passerelle d’application avec un équilibreur de charge interne (ILB), consultez [créer une passerelle d’application avec un équilibreur de charge interne (ILB)](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="211e9-210">If you want tooconfigure an application gateway toouse with an internal load balancer (ILB), see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="211e9-211">Si vous souhaitez plus d'informations sur les options d'équilibrage de charge en général, consultez :</span><span class="sxs-lookup"><span data-stu-id="211e9-211">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="211e9-212">Équilibrage de charge Azure</span><span class="sxs-lookup"><span data-stu-id="211e9-212">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="211e9-213">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="211e9-213">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

