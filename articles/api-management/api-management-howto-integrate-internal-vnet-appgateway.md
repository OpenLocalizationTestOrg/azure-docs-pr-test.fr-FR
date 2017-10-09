---
title: "aaaHow toouse gestion des API Azure dans un réseau virtuel avec la passerelle d’Application | Documents Microsoft"
description: "Découvrez comment toosetup et configurer la gestion des API Azure dans un réseau virtuel interne avec Application Gateway (WAF) en tant que serveur frontal"
services: api-management
documentationcenter: 
author: solankisamir
manager: kjoshi
editor: antonba
ms.assetid: a8c982b2-bca5-4312-9367-4a0bbc1082b1
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/16/2017
ms.author: sasolank
ms.openlocfilehash: 74303a2ee8a10db633ab1740ec7267728eacb473
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-api-management-in-an-internal-vnet-with-application-gateway"></a><span data-ttu-id="f556c-103">Intégrer le service Gestion des API dans un réseau virtuel interne avec Application Gateway</span><span class="sxs-lookup"><span data-stu-id="f556c-103">Integrate API Management in an internal VNET with Application Gateway</span></span> 

##<span data-ttu-id="f556c-104"><a name="overview"></a> Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="f556c-104"><a name="overview"> </a> Overview</span></span>
 
<span data-ttu-id="f556c-105">service de gestion des API de Hello peut être configuré dans un réseau virtuel en mode interne, ce qui le rend accessible uniquement à partir de hello réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="f556c-105">hello API Management service can be configured in a Virtual Network in internal mode which makes it accessible only from within hello Virtual Network.</span></span> <span data-ttu-id="f556c-106">La passerelle Azure Application Gateway est un service PAAS qui propose un équilibreur de charge de couche 7.</span><span class="sxs-lookup"><span data-stu-id="f556c-106">Azure Application Gateway is a PAAS Service which provides a Layer-7 load balancer.</span></span> <span data-ttu-id="f556c-107">Il agit comme un service proxy inverse et fournit dans son offre un pare-feu d’applications web (WAF).</span><span class="sxs-lookup"><span data-stu-id="f556c-107">It acts as a reverse-proxy service and provides among its offering a Web Application Firewall (WAF).</span></span>

<span data-ttu-id="f556c-108">Combinaison de gestion des API configuré dans un réseau interne avec un serveur frontal de passerelle d’Application hello permet hello les scénarios suivants :</span><span class="sxs-lookup"><span data-stu-id="f556c-108">Combining API Management provisioned in an internal VNET with hello Application Gateway frontend enables hello following scenarios:</span></span>

* <span data-ttu-id="f556c-109">Utilisez hello même ressource de gestion des API pour la consommation par les consommateurs internes et externes aux consommateurs.</span><span class="sxs-lookup"><span data-stu-id="f556c-109">Use hello same API Management resource for consumption by both internal consumers and external consumers.</span></span>
* <span data-ttu-id="f556c-110">Utilisez une seule ressource de gestion des API et mettez à disposition un sous-ensemble d’API défini dans la gestion des API pour les consommateurs externes.</span><span class="sxs-lookup"><span data-stu-id="f556c-110">Use a single API Management resource and have a subset of APIs defined in API Management available for external consumers.</span></span>
* <span data-ttu-id="f556c-111">Fournir un accès tooAPI gestion de clés en main moyen tooswitch de hello Internet public et désactiver.</span><span class="sxs-lookup"><span data-stu-id="f556c-111">Provide a turn-key way tooswitch access tooAPI Management from hello public Internet on and off.</span></span> 

##<span data-ttu-id="f556c-112"><a name="scenario"></a> Scénario</span><span class="sxs-lookup"><span data-stu-id="f556c-112"><a name="scenario"> </a> Scenario</span></span>
<span data-ttu-id="f556c-113">Cet article couvre comment toouse un unique de gestion des API de service par les utilisateurs internes et externes et rendre agissent comme un seul serveur frontal pour à la fois localement et dans le cloud d’API.</span><span class="sxs-lookup"><span data-stu-id="f556c-113">This article will cover how toouse a single API Management service for both internal and external consumers and make it act as a single frontend for both on-prem and cloud APIs.</span></span> <span data-ttu-id="f556c-114">Vous verrez également comment tooexpose uniquement un sous-ensemble de votre API (dans l’exemple hello qu’ils sont mis en surbrillance en vert) pour la consommation externe à l’aide de la fonctionnalité de PathBasedRouting hello disponible dans la passerelle d’Application.</span><span class="sxs-lookup"><span data-stu-id="f556c-114">You will also see how tooexpose only a subset of your APIs (in hello example they are highlighted in green) for External Consumption using hello PathBasedRouting functionality available in Application Gateway.</span></span>

<span data-ttu-id="f556c-115">Dans le premier exemple de programme d’installation hello tous vos API sont gérés uniquement à partir de votre réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="f556c-115">In hello first setup example all your APIs are managed only from within your Virtual Network.</span></span> <span data-ttu-id="f556c-116">Les consommateurs internes (mis en surbrillance en orange) peuvent accéder à toutes vos API internes et externes.</span><span class="sxs-lookup"><span data-stu-id="f556c-116">Internal consumers (highlighted in orange) can access all your internal and external APIs.</span></span> <span data-ttu-id="f556c-117">Le trafic est jamais tooInternet qu'une haute performance est remis via des circuits Expressroute.</span><span class="sxs-lookup"><span data-stu-id="f556c-117">Traffic never goes out tooInternet a high performance is delivered via Express Route circuits.</span></span>

![itinéraire d’URL](./media/api-management-howto-integrate-internal-vnet-appgateway/api-management-howto-integrate-internal-vnet-appgateway.png)

## <span data-ttu-id="f556c-119"><a name="before-you-begin"></a> Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="f556c-119"><a name="before-you-begin"> </a> Before you begin</span></span>

1. <span data-ttu-id="f556c-120">Installer version la plus récente des applets de commande PowerShell Azure hello hello à l’aide de hello Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="f556c-120">Install hello latest version of hello Azure PowerShell cmdlets by using hello Web Platform Installer.</span></span> <span data-ttu-id="f556c-121">Vous pouvez télécharger et installer la version la plus récente hello de hello **Windows PowerShell** section Hello [page Téléchargements](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="f556c-121">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="f556c-122">Créez un réseau virtuel et des sous-réseaux distincts pour le service Gestion des API et Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="f556c-122">Create a Virtual Network and create separate subnets for API Management and Application Gateway.</span></span> 
3. <span data-ttu-id="f556c-123">Si vous envisagez de toocreate un serveur DNS personnalisé pour hello réseau virtuel, le faire avant de commencer le déploiement de hello.</span><span class="sxs-lookup"><span data-stu-id="f556c-123">If you intend toocreate a custom DNS server for hello Virtual Network, do so before starting hello deployment.</span></span> <span data-ttu-id="f556c-124">Vérifiez qu’il fonctionne en garantissant une machine virtuelle créée dans un nouveau sous-réseau Bonjour réseau virtuel peut résoudre et accéder à tous les points de terminaison de service Azure.</span><span class="sxs-lookup"><span data-stu-id="f556c-124">Double check it works by ensuring a virtual machine created in a new subnet in hello Virtual Network can resolve and access all Azure service endpoints.</span></span>

## <a name="what-is-required-toocreate-an-integration-between-api-management-and-application-gateway"></a><span data-ttu-id="f556c-125">Qu’est requis toocreate une intégration entre la gestion des API et la passerelle d’Application ?</span><span class="sxs-lookup"><span data-stu-id="f556c-125">What is required toocreate an integration between API Management and Application Gateway?</span></span>

* <span data-ttu-id="f556c-126">**Pool de serveur principal :** hello interne adresse IP virtuelle de hello service de gestion des API.</span><span class="sxs-lookup"><span data-stu-id="f556c-126">**Back-end server pool:** This is hello internal virtual IP address of hello API Management service.</span></span>
* <span data-ttu-id="f556c-127">**Paramètres du pool de serveurs principaux :** chaque pool comporte des paramètres tels que le port, le protocole et une affinité basée sur des cookies.</span><span class="sxs-lookup"><span data-stu-id="f556c-127">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="f556c-128">Ces paramètres sont appliqués tooall des serveurs au sein du pool de hello.</span><span class="sxs-lookup"><span data-stu-id="f556c-128">These settings are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="f556c-129">**Port frontal :** hello port public qui est ouvert sur la passerelle d’application hello.</span><span class="sxs-lookup"><span data-stu-id="f556c-129">**Front-end port:** This is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="f556c-130">Le trafic en appuyant sur elle obtient tooone redirigé Hello serveurs principaux.</span><span class="sxs-lookup"><span data-stu-id="f556c-130">Traffic hitting it gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="f556c-131">**Écouteur :** hello port d’écoute utilise un port frontal, un protocole (Http ou Https, ces valeurs respectent la casse) et le nom du certificat SSL hello (si le déchargement de la configuration de SSL).</span><span class="sxs-lookup"><span data-stu-id="f556c-131">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="f556c-132">**La règle :** règle de hello lie un pool de serveur principal tooa écouteur.</span><span class="sxs-lookup"><span data-stu-id="f556c-132">**Rule:** hello rule binds a listener tooa back-end server pool.</span></span>
* <span data-ttu-id="f556c-133">**Sonde d’intégrité personnalisé :** passerelle d’Application, par défaut, utilise toofigure de sondes en fonction des adresses IP quels serveurs Bonjour BackendAddressPool sont actifs.</span><span class="sxs-lookup"><span data-stu-id="f556c-133">**Custom Health Probe:** Application Gateway, by default, uses IP address based probes toofigure out which servers in hello BackendAddressPool are active.</span></span> <span data-ttu-id="f556c-134">Hello service de gestion des API répond uniquement toorequests qui présentent l’en-tête d’hôte correct hello, par conséquent, les sondes par défaut de hello échouent.</span><span class="sxs-lookup"><span data-stu-id="f556c-134">hello API Management service only responds toorequests which have hello correct host header, hence hello default probes fail.</span></span> <span data-ttu-id="f556c-135">Une sonde d’intégrité personnalisé doit toobe défini passerelle d’application toohelp déterminer que hello service est actif et il doit transférer les demandes.</span><span class="sxs-lookup"><span data-stu-id="f556c-135">A custom health probe needs toobe defined toohelp application gateway determine that hello service is alive and it should forward requests.</span></span>
* <span data-ttu-id="f556c-136">**Certificat de domaine personnalisé :** tooaccess gestion des API de hello internet, vous devez toocreate un mappage CNAME de son nom DNS nom d’hôte toohello passerelle d’Application frontale.</span><span class="sxs-lookup"><span data-stu-id="f556c-136">**Custom domain certificate:** tooaccess API Management from hello internet you need toocreate a CNAME mapping of its hostname toohello Application Gateway front-end DNS name.</span></span> <span data-ttu-id="f556c-137">Cela garantit qu’en-tête de nom d’hôte hello et certificat envoyé tooApplication passerelle est transféré tooAPI gestion une QU'APIM peut reconnaître comme valide.</span><span class="sxs-lookup"><span data-stu-id="f556c-137">This ensures that hello hostname header and certificate sent tooApplication Gateway that is forwarded tooAPI Management is one APIM can recognize as valid.</span></span>

## <span data-ttu-id="f556c-138"><a name="overview-steps"></a> Étapes requises pour l’intégration de la gestion des API et d’Application Gateway</span><span class="sxs-lookup"><span data-stu-id="f556c-138"><a name="overview-steps"> </a> Steps required for integrating API Management and Application Gateway</span></span> 

1. <span data-ttu-id="f556c-139">Créer un groupe de ressources pour Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f556c-139">Create a resource group for Resource Manager.</span></span>
2. <span data-ttu-id="f556c-140">Créer un réseau virtuel, un sous-réseau et une adresse IP publique pour hello passerelle d’Application.</span><span class="sxs-lookup"><span data-stu-id="f556c-140">Create a Virtual Network, subnet, and public IP for hello Application Gateway.</span></span> <span data-ttu-id="f556c-141">Créer un autre sous-réseau pour le service Gestion des API</span><span class="sxs-lookup"><span data-stu-id="f556c-141">Create another subnet for API Management.</span></span>
3. <span data-ttu-id="f556c-142">Créer un service de gestion des API à l’intérieur du sous-réseau de réseau virtuel hello créé ci-dessus et assurez-vous que vous utilisez le mode interne hello.</span><span class="sxs-lookup"><span data-stu-id="f556c-142">Create an API Management service inside hello VNET subnet created above and ensure you use hello Internal mode.</span></span>
4. <span data-ttu-id="f556c-143">Le programme d’installation de nom de domaine personnalisé hello Bonjour service de gestion des API.</span><span class="sxs-lookup"><span data-stu-id="f556c-143">Setup hello custom domain name in hello API Management service.</span></span>
5. <span data-ttu-id="f556c-144">Créer un objet de configuration de passerelle Application Gateway</span><span class="sxs-lookup"><span data-stu-id="f556c-144">Create an Application Gateway configuration object.</span></span>
6. <span data-ttu-id="f556c-145">Créer une ressource Application Gateway</span><span class="sxs-lookup"><span data-stu-id="f556c-145">Create an Application Gateway resource.</span></span>
7. <span data-ttu-id="f556c-146">Créer un enregistrement CNAME à partir de hello nom DNS public du nom d’hôte du serveur proxy de gestion des API toohello hello passerelle d’Application.</span><span class="sxs-lookup"><span data-stu-id="f556c-146">Create a CNAME from hello public DNS name of hello Application Gateway toohello API Management proxy hostname.</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="f556c-147">Créer un groupe de ressources pour Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f556c-147">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="f556c-148">Assurez-vous que vous utilisez la version la plus récente d’Azure PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="f556c-148">Make sure that you are using hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="f556c-149">Pour plus d’informations, voir [Utilisation de Windows PowerShell avec Azure Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="f556c-149">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="f556c-150">Étape 1</span><span class="sxs-lookup"><span data-stu-id="f556c-150">Step 1</span></span>

<span data-ttu-id="f556c-151">Connectez-vous à tooAzure</span><span class="sxs-lookup"><span data-stu-id="f556c-151">Log in tooAzure</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="f556c-152">Authentifiez-vous à l’aide de vos informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="f556c-152">Authenticate with your credentials.</span></span><BR>

### <a name="step-2"></a><span data-ttu-id="f556c-153">Étape 2</span><span class="sxs-lookup"><span data-stu-id="f556c-153">Step 2</span></span>

<span data-ttu-id="f556c-154">Vérifiez les abonnements hello pour le compte de hello et sélectionnez-le.</span><span class="sxs-lookup"><span data-stu-id="f556c-154">Check hello subscriptions for hello account and select it.</span></span>

```powershell
Get-AzureRmSubscription -Subscriptionid "GUID of subscription" | Select-AzureRmSubscription
```

### <a name="step-3"></a><span data-ttu-id="f556c-155">Étape 3 :</span><span class="sxs-lookup"><span data-stu-id="f556c-155">Step 3</span></span>

<span data-ttu-id="f556c-156">Créez un groupe de ressources (ignorez cette étape si vous utilisez un groupe de ressources existant).</span><span class="sxs-lookup"><span data-stu-id="f556c-156">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name "apim-appGw-RG" -Location "West US"
```
<span data-ttu-id="f556c-157">Azure Resource Manager requiert que tous les groupes de ressources spécifient un emplacement.</span><span class="sxs-lookup"><span data-stu-id="f556c-157">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="f556c-158">Cela est utilisé comme emplacement par défaut de hello pour les ressources dans ce groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="f556c-158">This is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="f556c-159">Assurez-vous que toutes les commandes toocreate un hello d’utilisation de passerelle application même groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="f556c-159">Make sure that all commands toocreate an application gateway use hello same resource group.</span></span>

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a><span data-ttu-id="f556c-160">Créer un réseau virtuel et un sous-réseau pour la passerelle d’application hello</span><span class="sxs-lookup"><span data-stu-id="f556c-160">Create a Virtual Network and a subnet for hello application gateway</span></span>

<span data-ttu-id="f556c-161">Bonjour à l’exemple suivant montre comment un réseau virtuel à l’aide de toocreate hello Gestionnaire de ressources.</span><span class="sxs-lookup"><span data-stu-id="f556c-161">hello following example shows how toocreate a Virtual Network using hello resource manager.</span></span>

### <a name="step-1"></a><span data-ttu-id="f556c-162">Étape 1</span><span class="sxs-lookup"><span data-stu-id="f556c-162">Step 1</span></span>

<span data-ttu-id="f556c-163">Affecter hello adresse plage 10.0.0.0/24 toohello sous-réseau variable toobe utilisé pour la passerelle d’Application lors de la création d’un réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="f556c-163">Assign hello address range 10.0.0.0/24 toohello subnet variable toobe used for Application Gateway while creating a Virtual Network.</span></span>

```powershell
$appgatewaysubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "apim01" -AddressPrefix "10.0.0.0/24"
```

### <a name="step-2"></a><span data-ttu-id="f556c-164">Étape 2</span><span class="sxs-lookup"><span data-stu-id="f556c-164">Step 2</span></span>

<span data-ttu-id="f556c-165">Affecter hello adresse plage 10.0.1.0/24 toohello sous-réseau variable toobe utilisé pour la gestion de l’API lors de la création d’un réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="f556c-165">Assign hello address range 10.0.1.0/24 toohello subnet variable toobe used for API Management while creating a Virtual Network.</span></span>

```powershell
$apimsubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "apim02" -AddressPrefix "10.0.1.0/24"
```

### <a name="step-3"></a><span data-ttu-id="f556c-166">Étape 3 :</span><span class="sxs-lookup"><span data-stu-id="f556c-166">Step 3</span></span>

<span data-ttu-id="f556c-167">Créer un réseau virtuel nommé **appgwvnet** dans le groupe de ressources **apim-appGw-RG** pour la région ouest des États-Unis hello à l’aide de hello préfixe 10.0.0.0/16 avec les sous-réseaux 10.0.0.0/24 et 10.0.1.0/24.</span><span class="sxs-lookup"><span data-stu-id="f556c-167">Create a Virtual Network named **appgwvnet** in resource group **apim-appGw-RG** for hello West US region using hello prefix 10.0.0.0/16 with subnets 10.0.0.0/24 and 10.0.1.0/24.</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name "appgwvnet" -ResourceGroupName "apim-appGw-RG" -Location "West US" -AddressPrefix "10.0.0.0/16" -Subnet $appgatewaysubnet,$apimsubnet
```

### <a name="step-4"></a><span data-ttu-id="f556c-168">Étape 4</span><span class="sxs-lookup"><span data-stu-id="f556c-168">Step 4</span></span>

<span data-ttu-id="f556c-169">Attribuer une variable de sous-réseau pour les étapes suivantes de hello</span><span class="sxs-lookup"><span data-stu-id="f556c-169">Assign a subnet variable for hello next steps</span></span>

```powershell
$appgatewaysubnetdata=$vnet.Subnets[0]
$apimsubnetdata=$vnet.Subnets[1]
```
## <a name="create-an-api-management-service-inside-a-vnet-configured-in-internal-mode"></a><span data-ttu-id="f556c-170">Créer un service Gestion des API dans un réseau virtuel configuré en mode interne</span><span class="sxs-lookup"><span data-stu-id="f556c-170">Create an API Management service inside a VNET configured in internal mode</span></span>

<span data-ttu-id="f556c-171">Hello suivant montre comment toocreate un service de gestion des API dans un réseau virtuel configuré pour l’accès interne uniquement.</span><span class="sxs-lookup"><span data-stu-id="f556c-171">hello following example shows how toocreate an API Management service in a VNET configured for internal access only.</span></span>

### <a name="step-1"></a><span data-ttu-id="f556c-172">Étape 1</span><span class="sxs-lookup"><span data-stu-id="f556c-172">Step 1</span></span>
<span data-ttu-id="f556c-173">Créez un objet de réseau virtuel de gestion des API à l’aide de sous-réseau de hello $apimsubnetdata créé ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="f556c-173">Create an API Management Virtual Network object using hello subnet $apimsubnetdata created above.</span></span>

```powershell
$apimVirtualNetwork = New-AzureRmApiManagementVirtualNetwork -Location "West US" -SubnetResourceId $apimsubnetdata.Id
```
### <a name="step-2"></a><span data-ttu-id="f556c-174">Étape 2</span><span class="sxs-lookup"><span data-stu-id="f556c-174">Step 2</span></span>
<span data-ttu-id="f556c-175">Créer un service de gestion des API à l’intérieur de hello réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="f556c-175">Create an API Management service inside hello Virtual Network.</span></span>

```powershell
$apimService = New-AzureRmApiManagement -ResourceGroupName "apim-appGw-RG" -Location "West US" -Name "ContosoApi" -Organization "Contoso" -AdminEmail "admin@contoso.com" -VirtualNetwork $apimVirtualNetwork -VpnType "Internal" -Sku "Developer"
```
<span data-ttu-id="f556c-176">Après hello ci-dessus commande réussit consultez trop[Configuration DNS requise service de gestion des API réseau virtuel interne tooaccess](api-management-using-with-internal-vnet.md#apim-dns-configuration) tooaccess il.</span><span class="sxs-lookup"><span data-stu-id="f556c-176">After hello above command succeeds refer too[DNS Configuration required tooaccess internal VNET API Management service](api-management-using-with-internal-vnet.md#apim-dns-configuration) tooaccess it.</span></span>

## <a name="set-up-a-custom-domain-name-in-api-management"></a><span data-ttu-id="f556c-177">Configurer un nom de domaine personnalisé dans le service Gestion des API</span><span class="sxs-lookup"><span data-stu-id="f556c-177">Set-up a custom domain name in API Management</span></span>

### <a name="step-1"></a><span data-ttu-id="f556c-178">Étape 1</span><span class="sxs-lookup"><span data-stu-id="f556c-178">Step 1</span></span>
<span data-ttu-id="f556c-179">Téléchargez le certificat de hello avec une clé privée pour le domaine de hello.</span><span class="sxs-lookup"><span data-stu-id="f556c-179">Upload hello certificate with private key for hello domain.</span></span> <span data-ttu-id="f556c-180">Pour cet exemple, c’est `*.contoso.net`.</span><span class="sxs-lookup"><span data-stu-id="f556c-180">For this example it will be `*.contoso.net`.</span></span> 

```powershell
$certUploadResult = Import-AzureRmApiManagementHostnameCertificate -ResourceGroupName "apim-appGw-RG" -Name "ContosoApi" -HostnameType "Proxy" -PfxPath <full path too.pfx file> -PfxPassword <password for certificate file> -PassThru
```

### <a name="step-2"></a><span data-ttu-id="f556c-181">Étape 2</span><span class="sxs-lookup"><span data-stu-id="f556c-181">Step 2</span></span>
<span data-ttu-id="f556c-182">Une fois que le certificat de hello est téléchargé, créer un objet de configuration de nom d’hôte pour le proxy de hello avec un nom d’hôte de `api.contoso.net`, comme le certificat d’exemple hello prévoit autorité hello `*.contoso.net` domaine.</span><span class="sxs-lookup"><span data-stu-id="f556c-182">Once hello certificate is uploaded, create a hostname configuration object for hello proxy with a hostname of `api.contoso.net`, as hello example certificate provides authority for hello  `*.contoso.net` domain.</span></span> 

```powershell
$proxyHostnameConfig = New-AzureRmApiManagementHostnameConfiguration -CertificateThumbprint $certUploadResult.Thumbprint -Hostname "api.contoso.net"
$result = Set-AzureRmApiManagementHostnames -Name "ContosoApi" -ResourceGroupName "apim-appGw-RG" -ProxyHostnameConfiguration $proxyHostnameConfig
```

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a><span data-ttu-id="f556c-183">Créer une adresse IP publique pour la configuration frontale de hello</span><span class="sxs-lookup"><span data-stu-id="f556c-183">Create a public IP address for hello front-end configuration</span></span>

<span data-ttu-id="f556c-184">Créer une ressource IP publique **publicIP01** dans le groupe de ressources **apim-appGw-RG** pour la région ouest des États-Unis hello.</span><span class="sxs-lookup"><span data-stu-id="f556c-184">Create a public IP resource **publicIP01** in resource group **apim-appGw-RG** for hello West US region.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName "apim-appGw-RG" -name "publicIP01" -location "West US" -AllocationMethod Dynamic
```

<span data-ttu-id="f556c-185">Une adresse IP est attribuée toohello passerelle d’application au démarrage du service de hello.</span><span class="sxs-lookup"><span data-stu-id="f556c-185">An IP address is assigned toohello application gateway when hello service starts.</span></span>

## <a name="create-application-gateway-configuration"></a><span data-ttu-id="f556c-186">Créer une configuration de passerelle Application Gateway</span><span class="sxs-lookup"><span data-stu-id="f556c-186">Create application gateway configuration</span></span>

<span data-ttu-id="f556c-187">Tous les éléments de configuration doivent être configurés avant de créer la passerelle d’application hello.</span><span class="sxs-lookup"><span data-stu-id="f556c-187">All configuration items must be set up before creating hello application gateway.</span></span> <span data-ttu-id="f556c-188">Hello étapes suivantes créent hello des éléments de configuration qui sont nécessaires pour une ressource de passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="f556c-188">hello following steps create hello configuration items that are needed for an application gateway resource.</span></span>

### <a name="step-1"></a><span data-ttu-id="f556c-189">Étape 1</span><span class="sxs-lookup"><span data-stu-id="f556c-189">Step 1</span></span>

<span data-ttu-id="f556c-190">Créez une configuration IP de passerelle Application Gateway nommée **gatewayIP01**.</span><span class="sxs-lookup"><span data-stu-id="f556c-190">Create an application gateway IP configuration named **gatewayIP01**.</span></span> <span data-ttu-id="f556c-191">Au démarrage de la passerelle d’Application, il récupère une adresse IP du sous-réseau hello configuré et acheminer les adresses IP de réseau du trafic toohello dans le pool d’adresses IP hello back-end.</span><span class="sxs-lookup"><span data-stu-id="f556c-191">When Application Gateway starts, it picks up an IP address from hello subnet configured and route network traffic toohello IP addresses in hello back-end IP pool.</span></span> <span data-ttu-id="f556c-192">Gardez à l’esprit que chaque instance utilise une adresse IP unique.</span><span class="sxs-lookup"><span data-stu-id="f556c-192">Keep in mind that each instance takes one IP address.</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name "gatewayIP01" -Subnet $appgatewaysubnetdata
```

### <a name="step-2"></a><span data-ttu-id="f556c-193">Étape 2</span><span class="sxs-lookup"><span data-stu-id="f556c-193">Step 2</span></span>

<span data-ttu-id="f556c-194">Configurer les ports IP front-end hello pour le point de terminaison IP public hello.</span><span class="sxs-lookup"><span data-stu-id="f556c-194">Configure hello front-end IP port for hello public IP endpoint.</span></span> <span data-ttu-id="f556c-195">Ce port est le port hello qui les utilisateurs finaux se connectent à.</span><span class="sxs-lookup"><span data-stu-id="f556c-195">This port is hello port that end users connect to.</span></span>

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "port01"  -Port 443
```
### <a name="step-3"></a><span data-ttu-id="f556c-196">Étape 3 :</span><span class="sxs-lookup"><span data-stu-id="f556c-196">Step 3</span></span>

<span data-ttu-id="f556c-197">Configuration IP frontale de hello avec le point de terminaison IP public.</span><span class="sxs-lookup"><span data-stu-id="f556c-197">Configure hello front-end IP with public IP endpoint.</span></span>

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-4"></a><span data-ttu-id="f556c-198">Étape 4</span><span class="sxs-lookup"><span data-stu-id="f556c-198">Step 4</span></span>

<span data-ttu-id="f556c-199">Configurer le certificat de hello pour Application Gateway, hello utilisé toodecrypt et re-chiffrer le trafic hello en passant par.</span><span class="sxs-lookup"><span data-stu-id="f556c-199">Configure hello certificate for hello Application Gateway, used toodecrypt and re-encrypt hello traffic passing through.</span></span>

```powershell
$cert = New-AzureRmApplicationGatewaySslCertificate -Name "cert01" -CertificateFile <full path too.pfx file> -Password <password for certificate file>
```

### <a name="step-5"></a><span data-ttu-id="f556c-200">Étape 5</span><span class="sxs-lookup"><span data-stu-id="f556c-200">Step 5</span></span>

<span data-ttu-id="f556c-201">Créer l’écouteur HTTP hello pour hello passerelle d’Application.</span><span class="sxs-lookup"><span data-stu-id="f556c-201">Create hello HTTP listener for hello Application Gateway.</span></span> <span data-ttu-id="f556c-202">Affecter la configuration IP frontale de hello, le port et tooit du certificat ssl.</span><span class="sxs-lookup"><span data-stu-id="f556c-202">Assign hello front-end IP configuration, port, and ssl certificate tooit.</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol "Https" -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -SslCertificate $cert
```

### <a name="step-6"></a><span data-ttu-id="f556c-203">Étape 6</span><span class="sxs-lookup"><span data-stu-id="f556c-203">Step 6</span></span>

<span data-ttu-id="f556c-204">Créer un service de gestion des API de toohello sonde personnalisée `ContosoApi` le point de terminaison proxy domaine.</span><span class="sxs-lookup"><span data-stu-id="f556c-204">Create a custom probe toohello API Management service `ContosoApi` proxy domain endpoint.</span></span> <span data-ttu-id="f556c-205">chemin d’accès Hello `/status-0123456789abcdef` est un point de terminaison de contrôle d’intégrité par défaut hébergée sur tous les services de gestion des API hello.</span><span class="sxs-lookup"><span data-stu-id="f556c-205">hello path `/status-0123456789abcdef` is a default health endpoint hosted on all hello API Management services.</span></span> <span data-ttu-id="f556c-206">Définir `api.contoso.net` comme un toosecure de nom d’hôte de sonde personnalisée avec un certificat SSL.</span><span class="sxs-lookup"><span data-stu-id="f556c-206">Set `api.contoso.net` as a custom probe hostname toosecure it with SSL certificate.</span></span>

> [!NOTE]
> <span data-ttu-id="f556c-207">nom d’hôte de Hello `contosoapi.azure-api.net` est le nom d’hôte proxy hello par défaut configuré lorsqu’un service nommé `contosoapi` est créé dans Azure publique.</span><span class="sxs-lookup"><span data-stu-id="f556c-207">hello hostname `contosoapi.azure-api.net` is hello default proxy hostname configured when a service named `contosoapi` is created in public Azure.</span></span> 
> 

```powershell
$apimprobe = New-AzureRmApplicationGatewayProbeConfig -Name "apimproxyprobe" -Protocol "Https" -HostName "api.contoso.net" -Path "/status-0123456789abcdef" -Interval 30 -Timeout 120 -UnhealthyThreshold 8
```

### <a name="step-7"></a><span data-ttu-id="f556c-208">Étape 7</span><span class="sxs-lookup"><span data-stu-id="f556c-208">Step 7</span></span>

<span data-ttu-id="f556c-209">Téléchargez le certificat hello toobe utilisé sur les ressources de pool hello SSL activé le serveur principal.</span><span class="sxs-lookup"><span data-stu-id="f556c-209">Upload hello certificate toobe used on hello SSL-enabled backend pool resources.</span></span> <span data-ttu-id="f556c-210">Il s’agit de hello même certificat que vous avez fournies à l’étape 4 ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="f556c-210">This is hello same certificate which you provided in Step 4 above.</span></span>

```powershell
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name "whitelistcert1" -CertificateFile <full path too.cer file>
```

### <a name="step-8"></a><span data-ttu-id="f556c-211">Étape 8</span><span class="sxs-lookup"><span data-stu-id="f556c-211">Step 8</span></span>

<span data-ttu-id="f556c-212">Configurer les paramètres de serveur principal HTTP pour hello passerelle d’Application.</span><span class="sxs-lookup"><span data-stu-id="f556c-212">Configure HTTP backend settings for hello Application Gateway.</span></span> <span data-ttu-id="f556c-213">Définissez notamment une limite de délai d’expiration pour les demandes de serveur principal après laquelle elles sont annulées.</span><span class="sxs-lookup"><span data-stu-id="f556c-213">This includes setting a time-out limit for backend request after which they are cancelled.</span></span> <span data-ttu-id="f556c-214">Cette valeur est différente de délai d’attente de la sonde hello.</span><span class="sxs-lookup"><span data-stu-id="f556c-214">This value is different from hello probe time-out.</span></span>

```powershell
$apimPoolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name "apimPoolSetting" -Port 443 -Protocol "Https" -CookieBasedAffinity "Disabled" -Probe $apimprobe -AuthenticationCertificates $authcert -RequestTimeout 180
```

### <a name="step-9"></a><span data-ttu-id="f556c-215">Étape 9</span><span class="sxs-lookup"><span data-stu-id="f556c-215">Step 9</span></span>

<span data-ttu-id="f556c-216">Configurer un pool d’adresses IP principal nommé **apimbackend** avec l’adresse IP virtuelle interne, hello adresse du service de gestion des API de hello créé ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="f556c-216">Configure a back-end IP address pool named **apimbackend**  with hello internal virtual IP address of hello API Management service created above.</span></span>

```powershell
$apimProxyBackendPool = New-AzureRmApplicationGatewayBackendAddressPool -Name "apimbackend" -BackendIPAddresses $apimService.StaticIPs[0]
```

### <a name="step-10"></a><span data-ttu-id="f556c-217">Étape 10</span><span class="sxs-lookup"><span data-stu-id="f556c-217">Step 10</span></span>

<span data-ttu-id="f556c-218">Créez des paramètres pour un serveur principal factice (inexistant).</span><span class="sxs-lookup"><span data-stu-id="f556c-218">Create settings for a dummy (non-existent) backend.</span></span> <span data-ttu-id="f556c-219">Demandes tooAPI chemins d’accès que nous ne souhaitez pas tooexpose à partir de la gestion des API via une passerelle d’Application sera atteint ce serveur principal et de renvoyer l’erreur 404.</span><span class="sxs-lookup"><span data-stu-id="f556c-219">Requests tooAPI paths that we do not want tooexpose from API Management via Application Gateway will hit this backend and return 404.</span></span>

<span data-ttu-id="f556c-220">Configurez les paramètres HTTP pour les principaux factice hello.</span><span class="sxs-lookup"><span data-stu-id="f556c-220">Configure HTTP settings for hello dummy backend.</span></span>

```powershell
$dummyBackendSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name "dummySetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled
```

<span data-ttu-id="f556c-221">Configurer un serveur principal factice **dummyBackendPool**, qui pointe l’adresse du nom de domaine complet tooa **dummybackend.com**. Cette adresse de nom de domaine complet n’existe pas dans le réseau virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="f556c-221">Configure a dummy backend **dummyBackendPool**, which points tooa FQDN address **dummybackend.com**. This FQDN address does not exist in hello virtual network.</span></span>

```powershell
$dummyBackendPool = New-AzureRmApplicationGatewayBackendAddressPool -Name "dummyBackendPool" -BackendFqdns "dummybackend.com"
```

<span data-ttu-id="f556c-222">Créer une règle de définition que hello passerelle d’Application utilisera par défaut qui pointe toohello inexistant principal **dummybackend.com** Bonjour réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="f556c-222">Create a rule setting that hello Application Gateway will use by default which points toohello non-existent backend **dummybackend.com** in hello Virtual Network.</span></span>

```powershell
$dummyPathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "nonexistentapis" -Paths "/*" -BackendAddressPool $dummyBackendPool -BackendHttpSettings $dummyBackendSetting
```

### <a name="step-11"></a><span data-ttu-id="f556c-223">Étape 11</span><span class="sxs-lookup"><span data-stu-id="f556c-223">Step 11</span></span>

<span data-ttu-id="f556c-224">Configurer les chemins d’accès de la règle URL pour les pools principaux hello.</span><span class="sxs-lookup"><span data-stu-id="f556c-224">Configure URL rule paths for hello back-end pools.</span></span> <span data-ttu-id="f556c-225">Cela permet de sélectionner uniquement certaines des hello API de gestion des API pour pouvoir être exposés toohello public.</span><span class="sxs-lookup"><span data-stu-id="f556c-225">This enables selecting only some of hello APIs from API Management for being exposed toohello public.</span></span> <span data-ttu-id="f556c-226">(Par exemple, pour `Echo API` (/echo/), `Calculator API` (/calc/), etc., rendez uniquement `Echo API` accessible à partir d’Internet).</span><span class="sxs-lookup"><span data-stu-id="f556c-226">For example, if there are `Echo API` (/echo/), `Calculator API` (/calc/) etc. make only `Echo API` accessible from Internet).</span></span> 

<span data-ttu-id="f556c-227">Hello exemple suivant crée une règle simple pour hello « / echo / » chemin d’accès routage du trafic toohello principal « apimProxyBackendPool ».</span><span class="sxs-lookup"><span data-stu-id="f556c-227">hello following example creates a simple rule for hello "/echo/" path routing traffic toohello back-end "apimProxyBackendPool".</span></span>

```powershell
$echoapiRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "externalapis" -Paths "/echo/*" -BackendAddressPool $apimProxyBackendPool -BackendHttpSettings $apimPoolSetting
```

<span data-ttu-id="f556c-228">Si le chemin d’accès hello ne correspond pas à les règles de chemin d’accès hello nous souhaitons tooenable à partir de la gestion des API, règle hello configuration de mappage de chemin d’accès configure également un pool d’adresses principal par défaut nommé **dummyBackendPool**.</span><span class="sxs-lookup"><span data-stu-id="f556c-228">If hello path doesn't match hello path rules we want tooenable from API Management, hello rule path map configuration also configures a default back-end address pool named **dummyBackendPool**.</span></span> <span data-ttu-id="f556c-229">Par exemple, http://api.contoso.net/calc/ * devient trop**dummyBackendPool** telle qu’elle est définie en tant que pool par défaut de hello pour le trafic sans correspondance.</span><span class="sxs-lookup"><span data-stu-id="f556c-229">For example, http://api.contoso.net/calc/* goes too**dummyBackendPool** as it is defined as hello default pool for un-matched traffic.</span></span>

```powershell
$urlPathMap = New-AzureRmApplicationGatewayUrlPathMapConfig -Name "urlpathmap" -PathRules $echoapiRule, $dummyPathRule -DefaultBackendAddressPool $dummyBackendPool -DefaultBackendHttpSettings $dummyBackendSetting
```

<span data-ttu-id="f556c-230">Hello ci-dessus étape garantit que les demandes uniquement pour le chemin d’accès hello « / echo » sont autorisés via hello passerelle d’Application.</span><span class="sxs-lookup"><span data-stu-id="f556c-230">hello above step ensures that only requests for hello path "/echo" are allowed through hello Application Gateway.</span></span> <span data-ttu-id="f556c-231">Tooother demandes Qu'api configurés dans la gestion des API lève des 404 erreurs à partir de la passerelle d’Application à partir de hello Internet.</span><span class="sxs-lookup"><span data-stu-id="f556c-231">Requests tooother APIs configured in API Management will throw 404 errors from Application Gateway when accessed from hello Internet.</span></span> 

### <a name="step-12"></a><span data-ttu-id="f556c-232">Étape 12</span><span class="sxs-lookup"><span data-stu-id="f556c-232">Step 12</span></span>

<span data-ttu-id="f556c-233">Créer un paramètre de règle pour le routage basé sur le chemin d’accès hello Application Gateway toouse URL.</span><span class="sxs-lookup"><span data-stu-id="f556c-233">Create a rule setting for hello Application Gateway toouse URL path-based routing.</span></span>

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule1" -RuleType PathBasedRouting -HttpListener $listener -UrlPathMap $urlPathMap
```

### <a name="step-13"></a><span data-ttu-id="f556c-234">Étape 13</span><span class="sxs-lookup"><span data-stu-id="f556c-234">Step 13</span></span>

<span data-ttu-id="f556c-235">Configurer hello instances et de la taille de hello passerelle d’Application.</span><span class="sxs-lookup"><span data-stu-id="f556c-235">Configure hello number of instances and size for hello Application Gateway.</span></span> <span data-ttu-id="f556c-236">Ici, nous utilisons hello [WAF SKU](../application-gateway/application-gateway-webapplicationfirewall-overview.md) pour renforcer la sécurité de hello ressource de gestion des API.</span><span class="sxs-lookup"><span data-stu-id="f556c-236">Here we are using hello [WAF SKU](../application-gateway/application-gateway-webapplicationfirewall-overview.md) for increased security of hello API Management resource.</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "WAF_Medium" -Tier "WAF" -Capacity 2
```

### <a name="step-14"></a><span data-ttu-id="f556c-237">Étape 14</span><span class="sxs-lookup"><span data-stu-id="f556c-237">Step 14</span></span>

<span data-ttu-id="f556c-238">Configurer WAF toobe en mode de « Prévention ».</span><span class="sxs-lookup"><span data-stu-id="f556c-238">Configure WAF toobe in "Prevention" mode.</span></span>
```powershell
$config = New-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode "Prevention"
```

## <a name="create-application-gateway"></a><span data-ttu-id="f556c-239">Créer une passerelle Application Gateway</span><span class="sxs-lookup"><span data-stu-id="f556c-239">Create Application Gateway</span></span>

<span data-ttu-id="f556c-240">Créer une passerelle d’Application avec tous les objets de configuration de hello de hello étapes précédentes.</span><span class="sxs-lookup"><span data-stu-id="f556c-240">Create an Application Gateway with all hello configuration objects from hello preceding steps.</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name $applicationGatewayName -ResourceGroupName $resourceGroupName  -Location $location -BackendAddressPools $apimProxyBackendPool, $dummyBackendPool -BackendHttpSettingsCollection $apimPoolSetting, $dummyBackendSetting  -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener -UrlPathMaps $urlPathMap -RequestRoutingRules $rule01 -Sku $sku -WebApplicationFirewallConfig $config -SslCertificates $cert -AuthenticationCertificates $authcert -Probes $apimprobe
```

## <a name="cname-hello-api-management-proxy-hostname-toohello-public-dns-name-of-hello-application-gateway-resource"></a><span data-ttu-id="f556c-241">CNAME hello gestion des API proxy nom d’hôte toohello nom DNS public du hello ressource de la passerelle d’Application</span><span class="sxs-lookup"><span data-stu-id="f556c-241">CNAME hello API Management proxy hostname toohello public DNS name of hello Application Gateway resource</span></span>

<span data-ttu-id="f556c-242">Après la création de la passerelle de hello, hello prochaine étape consiste tooconfigure hello frontal pour la communication.</span><span class="sxs-lookup"><span data-stu-id="f556c-242">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="f556c-243">Lorsque vous utilisez une adresse IP publique, passerelle d’Application requiert un nom DNS affecté dynamiquement, ce qui ne peut pas être facilement toouse.</span><span class="sxs-lookup"><span data-stu-id="f556c-243">When using a public IP, Application Gateway requires a dynamically assigned DNS name, which may not be easy toouse.</span></span> 

<span data-ttu-id="f556c-244">Hello nom DNS de la passerelle d’Application doit être utilisé toocreate un enregistrement CNAME qui pointe le nom d’hôte proxy hello APIM (par exemple, `api.contoso.net` dans les exemples hello ci-dessus) nom DNS toothis.</span><span class="sxs-lookup"><span data-stu-id="f556c-244">hello Application Gateway's DNS name should be used toocreate a CNAME record which points hello APIM proxy host name (e.g. `api.contoso.net` in hello examples above) toothis DNS name.</span></span> <span data-ttu-id="f556c-245">tooconfigure hello frontal enregistrement IP CNAME, récupérer les détails hello Hello passerelle d’Application et son nom IP/DNS associé à l’aide d’élément d’adresse IP publique hello.</span><span class="sxs-lookup"><span data-stu-id="f556c-245">tooconfigure hello frontend IP CNAME record, retrieve hello details of hello Application Gateway and its associated IP/DNS name using hello PublicIPAddress element.</span></span> <span data-ttu-id="f556c-246">les utilisation de Hello d’enregistrements d’un n’est pas recommandée étant donné que l’adresse IP virtuelle hello peut changer lors du redémarrage de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="f556c-246">hello use of A-records is not recommended since hello VIP may change on restart of gateway.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName "apim-appGw-RG" -Name "publicIP01"
```

##<span data-ttu-id="f556c-247"><a name="summary"></a> Résumé</span><span class="sxs-lookup"><span data-stu-id="f556c-247"><a name="summary"> </a> Summary</span></span>
<span data-ttu-id="f556c-248">Gestion des API Azure configuré dans un réseau virtuel fournit une interface de passerelle unique pour toutes les API configurés, qu’ils soient hébergé localement ou dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="f556c-248">Azure API Management configured in a VNET provides a single gateway interface for all configured APIs, whether they are hosted on-prem or in hello cloud.</span></span> <span data-ttu-id="f556c-249">Intégration de passerelle d’Application avec gestion des API souplesse hello d’activer de manière sélective particulier toobe API accessible sur Internet de hello, mais aussi en fournissant un pare-feu d’applications Web comme une instance de gestion des API de serveur frontal tooyour.</span><span class="sxs-lookup"><span data-stu-id="f556c-249">Integrating Application Gateway with API Management provides hello flexibility of selectively enabling particular APIs toobe accessible on hello Internet, as well as providing a Web Application Firewall as a frontend tooyour API Management instance.</span></span>

##<span data-ttu-id="f556c-250"><a name="next-steps"></a> Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f556c-250"><a name="next-steps"> </a> Next steps</span></span>
* <span data-ttu-id="f556c-251">En savoir plus sur Azure Application Gateway</span><span class="sxs-lookup"><span data-stu-id="f556c-251">Learn more about Azure Application Gateway</span></span>
  * [<span data-ttu-id="f556c-252">Vue d’ensemble d’Application Gateway</span><span class="sxs-lookup"><span data-stu-id="f556c-252">Application Gateway Overview</span></span>](../application-gateway/application-gateway-introduction.md)
  * [<span data-ttu-id="f556c-253">Pare-feu d’applications web sur Application Gateway</span><span class="sxs-lookup"><span data-stu-id="f556c-253">Application Gateway Web Application Firewall</span></span>](../application-gateway/application-gateway-webapplicationfirewall-overview.md)
  * [<span data-ttu-id="f556c-254">Application Gateway à l’aide du routage basé sur le chemin</span><span class="sxs-lookup"><span data-stu-id="f556c-254">Application Gateway using Path-based Routing</span></span>](../application-gateway/application-gateway-create-url-route-arm-ps.md)
* <span data-ttu-id="f556c-255">En savoir plus sur le service Gestion des API et les réseaux virtuels</span><span class="sxs-lookup"><span data-stu-id="f556c-255">Learn more about API Management and VNETs</span></span>
  * [<span data-ttu-id="f556c-256">À l’aide de la gestion des API disponible uniquement dans hello réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="f556c-256">Using API Management available only within hello VNET</span></span>](api-management-using-with-internal-vnet.md)
  * [<span data-ttu-id="f556c-257">Avec la gestion des API dans le réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="f556c-257">Using API Management in VNET</span></span>](api-management-using-with-vnet.md)
