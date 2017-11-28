---
title: "Utilisation du service Gestion des API Azure dans un réseau virtuel avec Application Gateway | Microsoft Docs"
description: "Découvrez comment installer et configurer le service Gestion des API Azure dans un réseau virtuel interne avec Application Gateway (WAF) en tant que FrontEnd"
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
ms.openlocfilehash: 8131ded6b74e9c544bf70b1a4659ed07e5def04d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="integrate-api-management-in-an-internal-vnet-with-application-gateway"></a><span data-ttu-id="f55f3-103">Intégrer le service Gestion des API dans un réseau virtuel interne avec Application Gateway</span><span class="sxs-lookup"><span data-stu-id="f55f3-103">Integrate API Management in an internal VNET with Application Gateway</span></span> 

##<span data-ttu-id="f55f3-104"><a name="overview"> </a> Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="f55f3-104"><a name="overview"> </a> Overview</span></span>
 
<span data-ttu-id="f55f3-105">Le service Gestion des API peut être configuré dans un réseau virtuel en mode interne, ce qui le rend uniquement accessible à partir du réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="f55f3-105">The API Management service can be configured in a Virtual Network in internal mode which makes it accessible only from within the Virtual Network.</span></span> <span data-ttu-id="f55f3-106">La passerelle Azure Application Gateway est un service PAAS qui propose un équilibreur de charge de couche 7.</span><span class="sxs-lookup"><span data-stu-id="f55f3-106">Azure Application Gateway is a PAAS Service which provides a Layer-7 load balancer.</span></span> <span data-ttu-id="f55f3-107">Il agit comme un service proxy inverse et fournit dans son offre un pare-feu d’applications web (WAF).</span><span class="sxs-lookup"><span data-stu-id="f55f3-107">It acts as a reverse-proxy service and provides among its offering a Web Application Firewall (WAF).</span></span>

<span data-ttu-id="f55f3-108">Combiner la gestion des API configurée dans un réseau virtuel interne avec le frontal Application Gateway permet les scénarios suivants :</span><span class="sxs-lookup"><span data-stu-id="f55f3-108">Combining API Management provisioned in an internal VNET with the Application Gateway frontend enables the following scenarios:</span></span>

* <span data-ttu-id="f55f3-109">Utilisez la même ressource de gestion des API pour la consommation à la fois par les consommateurs internes et externes.</span><span class="sxs-lookup"><span data-stu-id="f55f3-109">Use the same API Management resource for consumption by both internal consumers and external consumers.</span></span>
* <span data-ttu-id="f55f3-110">Utilisez une seule ressource de gestion des API et mettez à disposition un sous-ensemble d’API défini dans la gestion des API pour les consommateurs externes.</span><span class="sxs-lookup"><span data-stu-id="f55f3-110">Use a single API Management resource and have a subset of APIs defined in API Management available for external consumers.</span></span>
* <span data-ttu-id="f55f3-111">Fournissez un moyen clé en main d’activer et désactiver l’accès à la gestion des API à partir de l’Internet public.</span><span class="sxs-lookup"><span data-stu-id="f55f3-111">Provide a turn-key way to switch access to API Management from the public Internet on and off.</span></span> 

##<span data-ttu-id="f55f3-112"><a name="scenario"> </a> Scénario</span><span class="sxs-lookup"><span data-stu-id="f55f3-112"><a name="scenario"> </a> Scenario</span></span>
<span data-ttu-id="f55f3-113">Dans cet article, nous allons étudier comment utiliser un seul et même service Gestion des API pour les consommateurs internes et externes, et l’utiliser comme serveur frontal sur les API locales et cloud.</span><span class="sxs-lookup"><span data-stu-id="f55f3-113">This article will cover how to use a single API Management service for both internal and external consumers and make it act as a single frontend for both on-prem and cloud APIs.</span></span> <span data-ttu-id="f55f3-114">Vous allez également voir comment exposer uniquement un sous-ensemble de vos API (dans cet exemple, elles sont mises en surbrillance en vert) pour une consommation externe, à l’aide de la fonctionnalité PathBasedRouting disponible dans Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="f55f3-114">You will also see how to expose only a subset of your APIs (in the example they are highlighted in green) for External Consumption using the PathBasedRouting functionality available in Application Gateway.</span></span>

<span data-ttu-id="f55f3-115">Dans le premier exemple de configuration, toutes vos API sont gérées uniquement à partir de votre réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="f55f3-115">In the first setup example all your APIs are managed only from within your Virtual Network.</span></span> <span data-ttu-id="f55f3-116">Les consommateurs internes (mis en surbrillance en orange) peuvent accéder à toutes vos API internes et externes.</span><span class="sxs-lookup"><span data-stu-id="f55f3-116">Internal consumers (highlighted in orange) can access all your internal and external APIs.</span></span> <span data-ttu-id="f55f3-117">Le trafic ne sort jamais vers Internet et une performance élevée est fournie via les circuits ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="f55f3-117">Traffic never goes out to Internet a high performance is delivered via Express Route circuits.</span></span>

![itinéraire d’URL](./media/api-management-howto-integrate-internal-vnet-appgateway/api-management-howto-integrate-internal-vnet-appgateway.png)

## <span data-ttu-id="f55f3-119"><a name="before-you-begin"> </a> Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="f55f3-119"><a name="before-you-begin"> </a> Before you begin</span></span>

1. <span data-ttu-id="f55f3-120">Installez la dernière version des applets de commande Azure PowerShell à l’aide de Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="f55f3-120">Install the latest version of the Azure PowerShell cmdlets by using the Web Platform Installer.</span></span> <span data-ttu-id="f55f3-121">Vous pouvez télécharger et installer la dernière version à partir de la section **Windows PowerShell** de la [page Téléchargements](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="f55f3-121">You can download and install the latest version from the **Windows PowerShell** section of the [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="f55f3-122">Créez un réseau virtuel et des sous-réseaux distincts pour le service Gestion des API et Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="f55f3-122">Create a Virtual Network and create separate subnets for API Management and Application Gateway.</span></span> 
3. <span data-ttu-id="f55f3-123">Si vous envisagez de créer un serveur DNS personnalisé pour le réseau virtuel, faites-le avant de commencer le déploiement.</span><span class="sxs-lookup"><span data-stu-id="f55f3-123">If you intend to create a custom DNS server for the Virtual Network, do so before starting the deployment.</span></span> <span data-ttu-id="f55f3-124">Vérifiez qu’il fonctionne en vous assurant qu’une machine virtuelle créée dans un nouveau sous-réseau du réseau virtuel peut résoudre tous les points de terminaison de service Azure et y accéder.</span><span class="sxs-lookup"><span data-stu-id="f55f3-124">Double check it works by ensuring a virtual machine created in a new subnet in the Virtual Network can resolve and access all Azure service endpoints.</span></span>

## <a name="what-is-required-to-create-an-integration-between-api-management-and-application-gateway"></a><span data-ttu-id="f55f3-125">Qu’est-ce qui est nécessaire pour créer une intégration entre le service Gestion des API et Application Gateway ?</span><span class="sxs-lookup"><span data-stu-id="f55f3-125">What is required to create an integration between API Management and Application Gateway?</span></span>

* <span data-ttu-id="f55f3-126">**Pool de serveurs principaux :** adresse IP virtuelle interne du service Gestion des API.</span><span class="sxs-lookup"><span data-stu-id="f55f3-126">**Back-end server pool:** This is the internal virtual IP address of the API Management service.</span></span>
* <span data-ttu-id="f55f3-127">**Paramètres du pool de serveurs principaux :** chaque pool comporte des paramètres tels que le port, le protocole et une affinité basée sur des cookies.</span><span class="sxs-lookup"><span data-stu-id="f55f3-127">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="f55f3-128">Ces paramètres sont appliqués à tous les serveurs du pool.</span><span class="sxs-lookup"><span data-stu-id="f55f3-128">These settings are applied to all servers within the pool.</span></span>
* <span data-ttu-id="f55f3-129">**Port frontal :** port public ouvert sur la passerelle Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="f55f3-129">**Front-end port:** This is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="f55f3-130">Le trafic l’atteignant est redirigé vers l’un des serveurs principaux.</span><span class="sxs-lookup"><span data-stu-id="f55f3-130">Traffic hitting it gets redirected to one of the back-end servers.</span></span>
* <span data-ttu-id="f55f3-131">**Écouteur :** l’écouteur a un port frontal, un protocole (Http ou Https, avec respect de la casse) et le nom du certificat SSL (en cas de configuration du déchargement SSL).</span><span class="sxs-lookup"><span data-stu-id="f55f3-131">**Listener:** The listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="f55f3-132">**Règle :** la règle relie un écouteur à un pool de serveurs principaux.</span><span class="sxs-lookup"><span data-stu-id="f55f3-132">**Rule:** The rule binds a listener to a back-end server pool.</span></span>
* <span data-ttu-id="f55f3-133">**Sonde d’intégrité personnalisée :** Application Gateway, par défaut, utilise des sondes basées sur des adresses IP pour déterminer les serveurs actifs dans le BackendAddressPool.</span><span class="sxs-lookup"><span data-stu-id="f55f3-133">**Custom Health Probe:** Application Gateway, by default, uses IP address based probes to figure out which servers in the BackendAddressPool are active.</span></span> <span data-ttu-id="f55f3-134">Le service Gestion des API répond uniquement aux demandes dont l’en-tête d’hôte est correct. C’est pourquoi les sondes par défaut échouent.</span><span class="sxs-lookup"><span data-stu-id="f55f3-134">The API Management service only responds to requests which have the correct host header, hence the default probes fail.</span></span> <span data-ttu-id="f55f3-135">Une sonde d’intégrité personnalisée doit être définie pour aider Application Gateway à déterminer que le service est actif et qu’il doit transférer les demandes.</span><span class="sxs-lookup"><span data-stu-id="f55f3-135">A custom health probe needs to be defined to help application gateway determine that the service is alive and it should forward requests.</span></span>
* <span data-ttu-id="f55f3-136">**Certificat de domaine personnalisé :** pour accéder au service Gestion des API à partir d’Internet, vous devez créer un mappage CNAME de son nom d’hôte au nom DNS frontal d’Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="f55f3-136">**Custom domain certificate:** To access API Management from the internet you need to create a CNAME mapping of its hostname to the Application Gateway front-end DNS name.</span></span> <span data-ttu-id="f55f3-137">Cela garantit que l’en-tête de nom d’hôte et le certificat envoyé à Application Gateway qui est transféré au service Gestion des API peuvent être reconnus comme valides par l’APIM.</span><span class="sxs-lookup"><span data-stu-id="f55f3-137">This ensures that the hostname header and certificate sent to Application Gateway that is forwarded to API Management is one APIM can recognize as valid.</span></span>

## <span data-ttu-id="f55f3-138"><a name="overview-steps"> </a> Étapes requises pour l’intégration de la gestion des API et d’Application Gateway</span><span class="sxs-lookup"><span data-stu-id="f55f3-138"><a name="overview-steps"> </a> Steps required for integrating API Management and Application Gateway</span></span> 

1. <span data-ttu-id="f55f3-139">Créer un groupe de ressources pour Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f55f3-139">Create a resource group for Resource Manager.</span></span>
2. <span data-ttu-id="f55f3-140">Créer un réseau virtuel, un sous-réseau et une adresse IP publique pour la passerelle Application Gateway</span><span class="sxs-lookup"><span data-stu-id="f55f3-140">Create a Virtual Network, subnet, and public IP for the Application Gateway.</span></span> <span data-ttu-id="f55f3-141">Créer un autre sous-réseau pour le service Gestion des API</span><span class="sxs-lookup"><span data-stu-id="f55f3-141">Create another subnet for API Management.</span></span>
3. <span data-ttu-id="f55f3-142">Créer un service Gestion des API dans le sous-réseau de réseau virtuel créé ci-dessus et veiller à l’utiliser en mode interne</span><span class="sxs-lookup"><span data-stu-id="f55f3-142">Create an API Management service inside the VNET subnet created above and ensure you use the Internal mode.</span></span>
4. <span data-ttu-id="f55f3-143">Configurer le nom de domaine personnalisé dans le service Gestion des API</span><span class="sxs-lookup"><span data-stu-id="f55f3-143">Setup the custom domain name in the API Management service.</span></span>
5. <span data-ttu-id="f55f3-144">Créer un objet de configuration de passerelle Application Gateway</span><span class="sxs-lookup"><span data-stu-id="f55f3-144">Create an Application Gateway configuration object.</span></span>
6. <span data-ttu-id="f55f3-145">Créer une ressource Application Gateway</span><span class="sxs-lookup"><span data-stu-id="f55f3-145">Create an Application Gateway resource.</span></span>
7. <span data-ttu-id="f55f3-146">Créer un CNAME à partir du nom DNS public de la passerelle Application Gateway pour le nom d’hôte proxy du service Gestion des API</span><span class="sxs-lookup"><span data-stu-id="f55f3-146">Create a CNAME from the public DNS name of the Application Gateway to the API Management proxy hostname.</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="f55f3-147">Créer un groupe de ressources pour Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f55f3-147">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="f55f3-148">Assurez-vous que vous disposez de la version la plus récente d’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f55f3-148">Make sure that you are using the latest version of Azure PowerShell.</span></span> <span data-ttu-id="f55f3-149">Pour plus d’informations, voir [Utilisation de Windows PowerShell avec Azure Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="f55f3-149">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="f55f3-150">Étape 1 :</span><span class="sxs-lookup"><span data-stu-id="f55f3-150">Step 1</span></span>

<span data-ttu-id="f55f3-151">Connexion à Azure</span><span class="sxs-lookup"><span data-stu-id="f55f3-151">Log in to Azure</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="f55f3-152">Authentifiez-vous à l’aide de vos informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="f55f3-152">Authenticate with your credentials.</span></span><BR>

### <a name="step-2"></a><span data-ttu-id="f55f3-153">Étape 2</span><span class="sxs-lookup"><span data-stu-id="f55f3-153">Step 2</span></span>

<span data-ttu-id="f55f3-154">Vérifiez les abonnements associés au compte et sélectionnez-le.</span><span class="sxs-lookup"><span data-stu-id="f55f3-154">Check the subscriptions for the account and select it.</span></span>

```powershell
Get-AzureRmSubscription -Subscriptionid "GUID of subscription" | Select-AzureRmSubscription
```

### <a name="step-3"></a><span data-ttu-id="f55f3-155">Étape 3 :</span><span class="sxs-lookup"><span data-stu-id="f55f3-155">Step 3</span></span>

<span data-ttu-id="f55f3-156">Créez un groupe de ressources (ignorez cette étape si vous utilisez un groupe de ressources existant).</span><span class="sxs-lookup"><span data-stu-id="f55f3-156">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name "apim-appGw-RG" -Location "West US"
```
<span data-ttu-id="f55f3-157">Azure Resource Manager requiert que tous les groupes de ressources spécifient un emplacement.</span><span class="sxs-lookup"><span data-stu-id="f55f3-157">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="f55f3-158">Ce dernier est utilisé comme emplacement par défaut des ressources de ce groupe.</span><span class="sxs-lookup"><span data-stu-id="f55f3-158">This is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="f55f3-159">Assurez-vous que toutes les commandes pour la création d'une passerelle Application Gateway utiliseront le même groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="f55f3-159">Make sure that all commands to create an application gateway use the same resource group.</span></span>

## <a name="create-a-virtual-network-and-a-subnet-for-the-application-gateway"></a><span data-ttu-id="f55f3-160">Créer un réseau virtuel et un sous-réseau pour la passerelle Application Gateway</span><span class="sxs-lookup"><span data-stu-id="f55f3-160">Create a Virtual Network and a subnet for the application gateway</span></span>

<span data-ttu-id="f55f3-161">L’exemple ci-dessous indique comment créer un réseau virtuel à l’aide de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f55f3-161">The following example shows how to create a Virtual Network using the resource manager.</span></span>

### <a name="step-1"></a><span data-ttu-id="f55f3-162">Étape 1 :</span><span class="sxs-lookup"><span data-stu-id="f55f3-162">Step 1</span></span>

<span data-ttu-id="f55f3-163">Affectez la plage d’adresses 10.0.0.0/24 à la variable subnet à utiliser pour la passerelle Application Gateway lors de la création d’un réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="f55f3-163">Assign the address range 10.0.0.0/24 to the subnet variable to be used for Application Gateway while creating a Virtual Network.</span></span>

```powershell
$appgatewaysubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "apim01" -AddressPrefix "10.0.0.0/24"
```

### <a name="step-2"></a><span data-ttu-id="f55f3-164">Étape 2</span><span class="sxs-lookup"><span data-stu-id="f55f3-164">Step 2</span></span>

<span data-ttu-id="f55f3-165">Affectez la plage d’adresses 10.0.1.0/24 à la variable subnet à utiliser pour le service Gestion des API lors de la création d’un réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="f55f3-165">Assign the address range 10.0.1.0/24 to the subnet variable to be used for API Management while creating a Virtual Network.</span></span>

```powershell
$apimsubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "apim02" -AddressPrefix "10.0.1.0/24"
```

### <a name="step-3"></a><span data-ttu-id="f55f3-166">Étape 3</span><span class="sxs-lookup"><span data-stu-id="f55f3-166">Step 3</span></span>

<span data-ttu-id="f55f3-167">Créez un réseau virtuel nommé **appgwvnet** dans le groupe de ressources **apim-appGw-RG** pour la région États-Unis de l’Ouest utilisant le préfixe 10.0.0.0/16 avec les sous-réseaux 10.0.0.0/24 et 10.0.1.0/24.</span><span class="sxs-lookup"><span data-stu-id="f55f3-167">Create a Virtual Network named **appgwvnet** in resource group **apim-appGw-RG** for the West US region using the prefix 10.0.0.0/16 with subnets 10.0.0.0/24 and 10.0.1.0/24.</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name "appgwvnet" -ResourceGroupName "apim-appGw-RG" -Location "West US" -AddressPrefix "10.0.0.0/16" -Subnet $appgatewaysubnet,$apimsubnet
```

### <a name="step-4"></a><span data-ttu-id="f55f3-168">Étape 4</span><span class="sxs-lookup"><span data-stu-id="f55f3-168">Step 4</span></span>

<span data-ttu-id="f55f3-169">Attribution d’une variable de sous-réseau pour les étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f55f3-169">Assign a subnet variable for the next steps</span></span>

```powershell
$appgatewaysubnetdata=$vnet.Subnets[0]
$apimsubnetdata=$vnet.Subnets[1]
```
## <a name="create-an-api-management-service-inside-a-vnet-configured-in-internal-mode"></a><span data-ttu-id="f55f3-170">Créer un service Gestion des API dans un réseau virtuel configuré en mode interne</span><span class="sxs-lookup"><span data-stu-id="f55f3-170">Create an API Management service inside a VNET configured in internal mode</span></span>

<span data-ttu-id="f55f3-171">L’exemple ci-dessous montre comment créer un service Gestion des API dans un réseau virtuel configuré pour un accès interne uniquement.</span><span class="sxs-lookup"><span data-stu-id="f55f3-171">The following example shows how to create an API Management service in a VNET configured for internal access only.</span></span>

### <a name="step-1"></a><span data-ttu-id="f55f3-172">Étape 1 :</span><span class="sxs-lookup"><span data-stu-id="f55f3-172">Step 1</span></span>
<span data-ttu-id="f55f3-173">Créez un objet de réseau virtuel du service Gestion des API via le sous-réseau $apimsubnetdata créé ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="f55f3-173">Create an API Management Virtual Network object using the subnet $apimsubnetdata created above.</span></span>

```powershell
$apimVirtualNetwork = New-AzureRmApiManagementVirtualNetwork -Location "West US" -SubnetResourceId $apimsubnetdata.Id
```
### <a name="step-2"></a><span data-ttu-id="f55f3-174">Étape 2</span><span class="sxs-lookup"><span data-stu-id="f55f3-174">Step 2</span></span>
<span data-ttu-id="f55f3-175">Créez un service Gestion des API dans le réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="f55f3-175">Create an API Management service inside the Virtual Network.</span></span>

```powershell
$apimService = New-AzureRmApiManagement -ResourceGroupName "apim-appGw-RG" -Location "West US" -Name "ContosoApi" -Organization "Contoso" -AdminEmail "admin@contoso.com" -VirtualNetwork $apimVirtualNetwork -VpnType "Internal" -Sku "Developer"
```
<span data-ttu-id="f55f3-176">Après la réussite de la commande ci-dessus, consultez la [configuration DNS requise pour accéder au service Gestion des API du réseau virtuel interne](api-management-using-with-internal-vnet.md#apim-dns-configuration) pour y accéder.</span><span class="sxs-lookup"><span data-stu-id="f55f3-176">After the above command succeeds refer to [DNS Configuration required to access internal VNET API Management service](api-management-using-with-internal-vnet.md#apim-dns-configuration) to access it.</span></span>

## <a name="set-up-a-custom-domain-name-in-api-management"></a><span data-ttu-id="f55f3-177">Configurer un nom de domaine personnalisé dans le service Gestion des API</span><span class="sxs-lookup"><span data-stu-id="f55f3-177">Set-up a custom domain name in API Management</span></span>

### <a name="step-1"></a><span data-ttu-id="f55f3-178">Étape 1 :</span><span class="sxs-lookup"><span data-stu-id="f55f3-178">Step 1</span></span>
<span data-ttu-id="f55f3-179">Chargez le certificat avec la clé privée correspondant au domaine.</span><span class="sxs-lookup"><span data-stu-id="f55f3-179">Upload the certificate with private key for the domain.</span></span> <span data-ttu-id="f55f3-180">Pour cet exemple, c’est `*.contoso.net`.</span><span class="sxs-lookup"><span data-stu-id="f55f3-180">For this example it will be `*.contoso.net`.</span></span> 

```powershell
$certUploadResult = Import-AzureRmApiManagementHostnameCertificate -ResourceGroupName "apim-appGw-RG" -Name "ContosoApi" -HostnameType "Proxy" -PfxPath <full path to .pfx file> -PfxPassword <password for certificate file> -PassThru
```

### <a name="step-2"></a><span data-ttu-id="f55f3-181">Étape 2</span><span class="sxs-lookup"><span data-stu-id="f55f3-181">Step 2</span></span>
<span data-ttu-id="f55f3-182">Une fois le certificat chargé, créez un objet de configuration de nom d’hôte pour le proxy avec le nom d’hôte `api.contoso.net`, car l’exemple de certificat fournit une autorité pour le domaine `*.contoso.net`.</span><span class="sxs-lookup"><span data-stu-id="f55f3-182">Once the certificate is uploaded, create a hostname configuration object for the proxy with a hostname of `api.contoso.net`, as the example certificate provides authority for the  `*.contoso.net` domain.</span></span> 

```powershell
$proxyHostnameConfig = New-AzureRmApiManagementHostnameConfiguration -CertificateThumbprint $certUploadResult.Thumbprint -Hostname "api.contoso.net"
$result = Set-AzureRmApiManagementHostnames -Name "ContosoApi" -ResourceGroupName "apim-appGw-RG" -ProxyHostnameConfiguration $proxyHostnameConfig
```

## <a name="create-a-public-ip-address-for-the-front-end-configuration"></a><span data-ttu-id="f55f3-183">Création d'une adresse IP publique pour la configuration frontale</span><span class="sxs-lookup"><span data-stu-id="f55f3-183">Create a public IP address for the front-end configuration</span></span>

<span data-ttu-id="f55f3-184">Créez une ressource IP publique **publicIP01** dans le groupe de ressources **appGw-RG** pour la région « West US ».</span><span class="sxs-lookup"><span data-stu-id="f55f3-184">Create a public IP resource **publicIP01** in resource group **apim-appGw-RG** for the West US region.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName "apim-appGw-RG" -name "publicIP01" -location "West US" -AllocationMethod Dynamic
```

<span data-ttu-id="f55f3-185">Une adresse IP est affectée à la passerelle Application Gateway au démarrage du service.</span><span class="sxs-lookup"><span data-stu-id="f55f3-185">An IP address is assigned to the application gateway when the service starts.</span></span>

## <a name="create-application-gateway-configuration"></a><span data-ttu-id="f55f3-186">Créer une configuration de passerelle Application Gateway</span><span class="sxs-lookup"><span data-stu-id="f55f3-186">Create application gateway configuration</span></span>

<span data-ttu-id="f55f3-187">Tous les éléments de configuration doivent être installés avant de créer la passerelle Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="f55f3-187">All configuration items must be set up before creating the application gateway.</span></span> <span data-ttu-id="f55f3-188">Les étapes suivantes permettent de créer les éléments de configuration nécessaires à une ressource Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="f55f3-188">The following steps create the configuration items that are needed for an application gateway resource.</span></span>

### <a name="step-1"></a><span data-ttu-id="f55f3-189">Étape 1</span><span class="sxs-lookup"><span data-stu-id="f55f3-189">Step 1</span></span>

<span data-ttu-id="f55f3-190">Créez une configuration IP de passerelle Application Gateway nommée **gatewayIP01**.</span><span class="sxs-lookup"><span data-stu-id="f55f3-190">Create an application gateway IP configuration named **gatewayIP01**.</span></span> <span data-ttu-id="f55f3-191">Lorsque la passerelle Application Gateway démarre, elle sélectionne une adresse IP à partir du sous-réseau configuré et achemine le trafic réseau vers les adresses IP du pool IP principal.</span><span class="sxs-lookup"><span data-stu-id="f55f3-191">When Application Gateway starts, it picks up an IP address from the subnet configured and route network traffic to the IP addresses in the back-end IP pool.</span></span> <span data-ttu-id="f55f3-192">Gardez à l’esprit que chaque instance utilise une adresse IP unique.</span><span class="sxs-lookup"><span data-stu-id="f55f3-192">Keep in mind that each instance takes one IP address.</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name "gatewayIP01" -Subnet $appgatewaysubnetdata
```

### <a name="step-2"></a><span data-ttu-id="f55f3-193">Étape 2 :</span><span class="sxs-lookup"><span data-stu-id="f55f3-193">Step 2</span></span>

<span data-ttu-id="f55f3-194">Configurez le port IP frontal pour le point de terminaison IP public.</span><span class="sxs-lookup"><span data-stu-id="f55f3-194">Configure the front-end IP port for the public IP endpoint.</span></span> <span data-ttu-id="f55f3-195">Ce port est le port auquel les utilisateurs finaux se connectent.</span><span class="sxs-lookup"><span data-stu-id="f55f3-195">This port is the port that end users connect to.</span></span>

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "port01"  -Port 443
```
### <a name="step-3"></a><span data-ttu-id="f55f3-196">Étape 3 :</span><span class="sxs-lookup"><span data-stu-id="f55f3-196">Step 3</span></span>

<span data-ttu-id="f55f3-197">Configurez l’adresse IP frontale avec un point de terminaison IP public.</span><span class="sxs-lookup"><span data-stu-id="f55f3-197">Configure the front-end IP with public IP endpoint.</span></span>

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-4"></a><span data-ttu-id="f55f3-198">Étape 4</span><span class="sxs-lookup"><span data-stu-id="f55f3-198">Step 4</span></span>

<span data-ttu-id="f55f3-199">Configurez le certificat pour la passerelle Application Gateway utilisée pour déchiffrer et rechiffrer le trafic transitant par celle-ci.</span><span class="sxs-lookup"><span data-stu-id="f55f3-199">Configure the certificate for the Application Gateway, used to decrypt and re-encrypt the traffic passing through.</span></span>

```powershell
$cert = New-AzureRmApplicationGatewaySslCertificate -Name "cert01" -CertificateFile <full path to .pfx file> -Password <password for certificate file>
```

### <a name="step-5"></a><span data-ttu-id="f55f3-200">Étape 5</span><span class="sxs-lookup"><span data-stu-id="f55f3-200">Step 5</span></span>

<span data-ttu-id="f55f3-201">Créez l’écouteur HTTP pour la passerelle Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="f55f3-201">Create the HTTP listener for the Application Gateway.</span></span> <span data-ttu-id="f55f3-202">Affectez-lui la configuration IP frontale, le port et le certificat SSL.</span><span class="sxs-lookup"><span data-stu-id="f55f3-202">Assign the front-end IP configuration, port, and ssl certificate to it.</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol "Https" -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -SslCertificate $cert
```

### <a name="step-6"></a><span data-ttu-id="f55f3-203">Étape 6</span><span class="sxs-lookup"><span data-stu-id="f55f3-203">Step 6</span></span>

<span data-ttu-id="f55f3-204">Créez une sonde personnalisée pour le point de terminaison de domaine de proxy `ContosoApi` du service Gestion des API.</span><span class="sxs-lookup"><span data-stu-id="f55f3-204">Create a custom probe to the API Management service `ContosoApi` proxy domain endpoint.</span></span> <span data-ttu-id="f55f3-205">Le chemin d’accès `/status-0123456789abcdef` est un point de terminaison d’intégrité par défaut hébergé sur tous les services de gestion des API.</span><span class="sxs-lookup"><span data-stu-id="f55f3-205">The path `/status-0123456789abcdef` is a default health endpoint hosted on all the API Management services.</span></span> <span data-ttu-id="f55f3-206">Définissez `api.contoso.net` comme nom d’hôte de sonde personnalisée pour la protéger à l’aide du certificat SSL.</span><span class="sxs-lookup"><span data-stu-id="f55f3-206">Set `api.contoso.net` as a custom probe hostname to secure it with SSL certificate.</span></span>

> [!NOTE]
> <span data-ttu-id="f55f3-207">Le nom d’hôte `contosoapi.azure-api.net` est le nom d’hôte du proxy par défaut configuré lorsqu’un service nommé `contosoapi` est créé dans la version publique d’Azure.</span><span class="sxs-lookup"><span data-stu-id="f55f3-207">The hostname `contosoapi.azure-api.net` is the default proxy hostname configured when a service named `contosoapi` is created in public Azure.</span></span> 
> 

```powershell
$apimprobe = New-AzureRmApplicationGatewayProbeConfig -Name "apimproxyprobe" -Protocol "Https" -HostName "api.contoso.net" -Path "/status-0123456789abcdef" -Interval 30 -Timeout 120 -UnhealthyThreshold 8
```

### <a name="step-7"></a><span data-ttu-id="f55f3-208">Étape 7</span><span class="sxs-lookup"><span data-stu-id="f55f3-208">Step 7</span></span>

<span data-ttu-id="f55f3-209">Chargez le certificat à utiliser sur les ressources du pool principal pour lequel le chiffrement SSL est activé.</span><span class="sxs-lookup"><span data-stu-id="f55f3-209">Upload the certificate to be used on the SSL-enabled backend pool resources.</span></span> <span data-ttu-id="f55f3-210">Il s’agit du certificat que vous avez fourni à l’étape 4 ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="f55f3-210">This is the same certificate which you provided in Step 4 above.</span></span>

```powershell
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name "whitelistcert1" -CertificateFile <full path to .cer file>
```

### <a name="step-8"></a><span data-ttu-id="f55f3-211">Étape 8</span><span class="sxs-lookup"><span data-stu-id="f55f3-211">Step 8</span></span>

<span data-ttu-id="f55f3-212">Configurez les paramètres de serveur principal HTTP de la passerelle Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="f55f3-212">Configure HTTP backend settings for the Application Gateway.</span></span> <span data-ttu-id="f55f3-213">Définissez notamment une limite de délai d’expiration pour les demandes de serveur principal après laquelle elles sont annulées.</span><span class="sxs-lookup"><span data-stu-id="f55f3-213">This includes setting a time-out limit for backend request after which they are cancelled.</span></span> <span data-ttu-id="f55f3-214">Cette valeur est différente du délai d’expiration de la sonde.</span><span class="sxs-lookup"><span data-stu-id="f55f3-214">This value is different from the probe time-out.</span></span>

```powershell
$apimPoolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name "apimPoolSetting" -Port 443 -Protocol "Https" -CookieBasedAffinity "Disabled" -Probe $apimprobe -AuthenticationCertificates $authcert -RequestTimeout 180
```

### <a name="step-9"></a><span data-ttu-id="f55f3-215">Étape 9</span><span class="sxs-lookup"><span data-stu-id="f55f3-215">Step 9</span></span>

<span data-ttu-id="f55f3-216">Configurez un pool d’adresses IP du serveur principal nommé **apimbackend** avec l’adresse IP virtuelle interne du service Gestion des API créé ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="f55f3-216">Configure a back-end IP address pool named **apimbackend**  with the internal virtual IP address of the API Management service created above.</span></span>

```powershell
$apimProxyBackendPool = New-AzureRmApplicationGatewayBackendAddressPool -Name "apimbackend" -BackendIPAddresses $apimService.StaticIPs[0]
```

### <a name="step-10"></a><span data-ttu-id="f55f3-217">Étape 10</span><span class="sxs-lookup"><span data-stu-id="f55f3-217">Step 10</span></span>

<span data-ttu-id="f55f3-218">Créez des paramètres pour un serveur principal factice (inexistant).</span><span class="sxs-lookup"><span data-stu-id="f55f3-218">Create settings for a dummy (non-existent) backend.</span></span> <span data-ttu-id="f55f3-219">Les demandes de chemins d’accès aux API que nous ne souhaitons pas exposer dans Gestion des API via Application Gateway atteignent ce serveur principal et retournent l’erreur 404.</span><span class="sxs-lookup"><span data-stu-id="f55f3-219">Requests to API paths that we do not want to expose from API Management via Application Gateway will hit this backend and return 404.</span></span>

<span data-ttu-id="f55f3-220">Configurez les paramètres HTTP du serveur principal factice.</span><span class="sxs-lookup"><span data-stu-id="f55f3-220">Configure HTTP settings for the dummy backend.</span></span>

```powershell
$dummyBackendSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name "dummySetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled
```

<span data-ttu-id="f55f3-221">Configurez un serveur principal factice **dummyBackendPool**, qui pointe vers une adresse de nom de domaine complet **dummybackend.com**. Cette adresse de nom de domaine complet n’existe pas dans le réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="f55f3-221">Configure a dummy backend **dummyBackendPool**, which points to a FQDN address **dummybackend.com**. This FQDN address does not exist in the virtual network.</span></span>

```powershell
$dummyBackendPool = New-AzureRmApplicationGatewayBackendAddressPool -Name "dummyBackendPool" -BackendFqdns "dummybackend.com"
```

<span data-ttu-id="f55f3-222">Créez un paramètre de règle que la passerelle Application Gateway utilisera par défaut pour pointer vers le serveur principal inexistant **dummybackend.com** dans le réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="f55f3-222">Create a rule setting that the Application Gateway will use by default which points to the non-existent backend **dummybackend.com** in the Virtual Network.</span></span>

```powershell
$dummyPathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "nonexistentapis" -Paths "/*" -BackendAddressPool $dummyBackendPool -BackendHttpSettings $dummyBackendSetting
```

### <a name="step-11"></a><span data-ttu-id="f55f3-223">Étape 11</span><span class="sxs-lookup"><span data-stu-id="f55f3-223">Step 11</span></span>

<span data-ttu-id="f55f3-224">Configurez les chemins de règles d’URL pour les pools principaux.</span><span class="sxs-lookup"><span data-stu-id="f55f3-224">Configure URL rule paths for the back-end pools.</span></span> <span data-ttu-id="f55f3-225">Vous pouvez ainsi sélectionner uniquement certaines des API du service Gestion des API pour les exposer au public.</span><span class="sxs-lookup"><span data-stu-id="f55f3-225">This enables selecting only some of the APIs from API Management for being exposed to the public.</span></span> <span data-ttu-id="f55f3-226">(Par exemple, pour `Echo API` (/echo/), `Calculator API` (/calc/), etc., rendez uniquement `Echo API` accessible à partir d’Internet).</span><span class="sxs-lookup"><span data-stu-id="f55f3-226">For example, if there are `Echo API` (/echo/), `Calculator API` (/calc/) etc. make only `Echo API` accessible from Internet).</span></span> 

<span data-ttu-id="f55f3-227">L’exemple suivant crée une règle simple pour le chemin d’accès « /echo/ » acheminant le trafic vers le serveur principal « apimProxyBackendPool ».</span><span class="sxs-lookup"><span data-stu-id="f55f3-227">The following example creates a simple rule for the "/echo/" path routing traffic to the back-end "apimProxyBackendPool".</span></span>

```powershell
$echoapiRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "externalapis" -Paths "/echo/*" -BackendAddressPool $apimProxyBackendPool -BackendHttpSettings $apimPoolSetting
```

<span data-ttu-id="f55f3-228">Si le chemin d’accès ne correspond aux règles de chemins d’accès que nous voulons activer dans Gestion des API, la configuration de mappage des chemins de règles configure également un pool d’adresses de serveurs principaux par défaut nommé **dummyBackendPool**.</span><span class="sxs-lookup"><span data-stu-id="f55f3-228">If the path doesn't match the path rules we want to enable from API Management, the rule path map configuration also configures a default back-end address pool named **dummyBackendPool**.</span></span> <span data-ttu-id="f55f3-229">Par exemple, http://api.contoso.net/calc/ * permet d’accéder à **dummyBackendPool**, car il est défini comme pool par défaut pour le trafic sans correspondance.</span><span class="sxs-lookup"><span data-stu-id="f55f3-229">For example, http://api.contoso.net/calc/* goes to **dummyBackendPool** as it is defined as the default pool for un-matched traffic.</span></span>

```powershell
$urlPathMap = New-AzureRmApplicationGatewayUrlPathMapConfig -Name "urlpathmap" -PathRules $echoapiRule, $dummyPathRule -DefaultBackendAddressPool $dummyBackendPool -DefaultBackendHttpSettings $dummyBackendSetting
```

<span data-ttu-id="f55f3-230">L’étape ci-dessus garantit que seules les demandes correspondant au chemin d’accès « /echo » sont autorisées via Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="f55f3-230">The above step ensures that only requests for the path "/echo" are allowed through the Application Gateway.</span></span> <span data-ttu-id="f55f3-231">Les demandes pour d’autres API configurées dans le service Gestion des API lèvent des erreurs 404 dans la passerelle Application Gateway en cas d’accès à partir d’Internet.</span><span class="sxs-lookup"><span data-stu-id="f55f3-231">Requests to other APIs configured in API Management will throw 404 errors from Application Gateway when accessed from the Internet.</span></span> 

### <a name="step-12"></a><span data-ttu-id="f55f3-232">Étape 12</span><span class="sxs-lookup"><span data-stu-id="f55f3-232">Step 12</span></span>

<span data-ttu-id="f55f3-233">Créez un paramètre de règle pour la passerelle Application Gateway pour utiliser le routage basé sur le chemin d’URL.</span><span class="sxs-lookup"><span data-stu-id="f55f3-233">Create a rule setting for the Application Gateway to use URL path-based routing.</span></span>

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule1" -RuleType PathBasedRouting -HttpListener $listener -UrlPathMap $urlPathMap
```

### <a name="step-13"></a><span data-ttu-id="f55f3-234">Étape 13</span><span class="sxs-lookup"><span data-stu-id="f55f3-234">Step 13</span></span>

<span data-ttu-id="f55f3-235">Configurez le nombre d’instances et la taille de la passerelle Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="f55f3-235">Configure the number of instances and size for the Application Gateway.</span></span> <span data-ttu-id="f55f3-236">Ici, nous utilisons la [référence WAF](../application-gateway/application-gateway-webapplicationfirewall-overview.md) pour renforcer la sécurité de la ressource du service Gestion des API.</span><span class="sxs-lookup"><span data-stu-id="f55f3-236">Here we are using the [WAF SKU](../application-gateway/application-gateway-webapplicationfirewall-overview.md) for increased security of the API Management resource.</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "WAF_Medium" -Tier "WAF" -Capacity 2
```

### <a name="step-14"></a><span data-ttu-id="f55f3-237">Étape 14</span><span class="sxs-lookup"><span data-stu-id="f55f3-237">Step 14</span></span>

<span data-ttu-id="f55f3-238">Configurez WAF pour passer en mode Prévention.</span><span class="sxs-lookup"><span data-stu-id="f55f3-238">Configure WAF to be in "Prevention" mode.</span></span>
```powershell
$config = New-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode "Prevention"
```

## <a name="create-application-gateway"></a><span data-ttu-id="f55f3-239">Créer une passerelle Application Gateway</span><span class="sxs-lookup"><span data-stu-id="f55f3-239">Create Application Gateway</span></span>

<span data-ttu-id="f55f3-240">Créez une passerelle Application Gateway avec tous les objets de configuration des étapes précédentes.</span><span class="sxs-lookup"><span data-stu-id="f55f3-240">Create an Application Gateway with all the configuration objects from the preceding steps.</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name $applicationGatewayName -ResourceGroupName $resourceGroupName  -Location $location -BackendAddressPools $apimProxyBackendPool, $dummyBackendPool -BackendHttpSettingsCollection $apimPoolSetting, $dummyBackendSetting  -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener -UrlPathMaps $urlPathMap -RequestRoutingRules $rule01 -Sku $sku -WebApplicationFirewallConfig $config -SslCertificates $cert -AuthenticationCertificates $authcert -Probes $apimprobe
```

## <a name="cname-the-api-management-proxy-hostname-to-the-public-dns-name-of-the-application-gateway-resource"></a><span data-ttu-id="f55f3-241">Définition du CNAME du nom d’hôte du proxy du service Gestion des API sur le nom DNS public de la ressource Application Gateway</span><span class="sxs-lookup"><span data-stu-id="f55f3-241">CNAME the API Management proxy hostname to the public DNS name of the Application Gateway resource</span></span>

<span data-ttu-id="f55f3-242">Une fois la passerelle créée, l’étape suivante consiste à configurer le serveur frontal pour la communication.</span><span class="sxs-lookup"><span data-stu-id="f55f3-242">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="f55f3-243">Lorsque vous utilisez une adresse IP publique, la passerelle Application Gateway requiert un nom DNS attribué dynamiquement, qui risque de ne pas être facile à utiliser.</span><span class="sxs-lookup"><span data-stu-id="f55f3-243">When using a public IP, Application Gateway requires a dynamically assigned DNS name, which may not be easy to use.</span></span> 

<span data-ttu-id="f55f3-244">Le nom DNS de la passerelle Application Gateway doit être utilisé pour créer un enregistrement CNAME qui pointe le nom d’hôte proxy APIM (`api.contoso.net` dans les exemples ci-dessus) vers ce nom DNS.</span><span class="sxs-lookup"><span data-stu-id="f55f3-244">The Application Gateway's DNS name should be used to create a CNAME record which points the APIM proxy host name (e.g. `api.contoso.net` in the examples above) to this DNS name.</span></span> <span data-ttu-id="f55f3-245">Pour configurer l’enregistrement CNAME d’adresses IP frontales, récupérez les détails de la passerelle Application Gateway et de son nom IP/DNS associé à l’aide de l’élément PublicIPAddress.</span><span class="sxs-lookup"><span data-stu-id="f55f3-245">To configure the frontend IP CNAME record, retrieve the details of the Application Gateway and its associated IP/DNS name using the PublicIPAddress element.</span></span> <span data-ttu-id="f55f3-246">L’utilisation de A-records n’est pas recommandée étant donné que l’adresse IP virtuelle peut changer lors du redémarrage de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="f55f3-246">The use of A-records is not recommended since the VIP may change on restart of gateway.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName "apim-appGw-RG" -Name "publicIP01"
```

##<span data-ttu-id="f55f3-247"><a name="summary"> </a> Résumé</span><span class="sxs-lookup"><span data-stu-id="f55f3-247"><a name="summary"> </a> Summary</span></span>
<span data-ttu-id="f55f3-248">Le service Gestion des API Azure configuré dans un réseau virtuel fournit une interface de passerelle unique pour l’ensemble des API configurées, qu’elles soient hébergées en local ou dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="f55f3-248">Azure API Management configured in a VNET provides a single gateway interface for all configured APIs, whether they are hosted on-prem or in the cloud.</span></span> <span data-ttu-id="f55f3-249">L’intégration d’Application Gateway au service Gestion des API vous permet d’activer facilement l’accessibilité d’API particulières sur Internet, tout en fournissant un pare-feu d’applications web en tant que pare-feu frontal pour votre instance de service Gestion des API.</span><span class="sxs-lookup"><span data-stu-id="f55f3-249">Integrating Application Gateway with API Management provides the flexibility of selectively enabling particular APIs to be accessible on the Internet, as well as providing a Web Application Firewall as a frontend to your API Management instance.</span></span>

##<span data-ttu-id="f55f3-250"><a name="next-steps"> </a> Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f55f3-250"><a name="next-steps"> </a> Next steps</span></span>
* <span data-ttu-id="f55f3-251">En savoir plus sur Azure Application Gateway</span><span class="sxs-lookup"><span data-stu-id="f55f3-251">Learn more about Azure Application Gateway</span></span>
  * [<span data-ttu-id="f55f3-252">Vue d’ensemble d’Application Gateway</span><span class="sxs-lookup"><span data-stu-id="f55f3-252">Application Gateway Overview</span></span>](../application-gateway/application-gateway-introduction.md)
  * [<span data-ttu-id="f55f3-253">Pare-feu d’applications web sur Application Gateway</span><span class="sxs-lookup"><span data-stu-id="f55f3-253">Application Gateway Web Application Firewall</span></span>](../application-gateway/application-gateway-webapplicationfirewall-overview.md)
  * [<span data-ttu-id="f55f3-254">Application Gateway à l’aide du routage basé sur le chemin</span><span class="sxs-lookup"><span data-stu-id="f55f3-254">Application Gateway using Path-based Routing</span></span>](../application-gateway/application-gateway-create-url-route-arm-ps.md)
* <span data-ttu-id="f55f3-255">En savoir plus sur le service Gestion des API et les réseaux virtuels</span><span class="sxs-lookup"><span data-stu-id="f55f3-255">Learn more about API Management and VNETs</span></span>
  * [<span data-ttu-id="f55f3-256">Utilisation de Gestion des API disponible uniquement dans le réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="f55f3-256">Using API Management available only within the VNET</span></span>](api-management-using-with-internal-vnet.md)
  * [<span data-ttu-id="f55f3-257">Avec la gestion des API dans le réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="f55f3-257">Using API Management in VNET</span></span>](api-management-using-with-vnet.md)
