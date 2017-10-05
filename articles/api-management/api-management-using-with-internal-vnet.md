---
title: "Guide pratique de la Gestion des API Azure avec un réseau virtuel interne | Microsoft Docs"
description: "Découvrez comment installer et configurer la Gestion des API Azure dans un réseau virtuel interne."
services: api-management
documentationcenter: 
author: solankisamir
manager: kjoshi
editor: 
ms.assetid: dac28ccf-2550-45a5-89cf-192d87369bc3
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 55248387c7e78d05c1cf1afd615b7b921e9669d5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="using-azure-api-management-service-with-internal-virtual-network"></a><span data-ttu-id="40b38-103">Utiliser le service Gestion des API Azure avec un réseau virtuel interne</span><span class="sxs-lookup"><span data-stu-id="40b38-103">Using Azure API Management service with Internal Virtual Network</span></span>
<span data-ttu-id="40b38-104">Avec les réseaux virtuels Azure (VNET), la Gestion des API peut gérer des API inaccessibles sur Internet.</span><span class="sxs-lookup"><span data-stu-id="40b38-104">With Azure Virtual Networks (VNETs), API Management can manage APIs not accessible on the Internet.</span></span> <span data-ttu-id="40b38-105">Un certain nombre de technologies VPN sont disponibles pour établir la connexion et la Gestion des API peut être déployée selon deux modes principaux à l’intérieur du réseau virtuel :</span><span class="sxs-lookup"><span data-stu-id="40b38-105">A number of VPN technologies are available to make the connection and API Management can be deployed in two main modes inside the VNET:</span></span>
* <span data-ttu-id="40b38-106">Externe</span><span class="sxs-lookup"><span data-stu-id="40b38-106">External</span></span>
* <span data-ttu-id="40b38-107">Interne</span><span class="sxs-lookup"><span data-stu-id="40b38-107">Internal</span></span>

## <span data-ttu-id="40b38-108"><a name="overview"> </a>Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="40b38-108"><a name="overview"> </a>Overview</span></span>
<span data-ttu-id="40b38-109">Lorsque la Gestion des API est déployée en mode réseau virtuel interne, tous les points de terminaison de service (passerelle, portail des développeurs, portail des éditeurs, gestion directe et git) ne sont visibles que dans un réseau virtuel auquel vous contrôlez l’accès.</span><span class="sxs-lookup"><span data-stu-id="40b38-109">When API Management is deployed in an Internal Virtual network mode, all the service endpoints (gateway, developer portal, publisher portal, direct management and Git) are only visible inside a Virtual network that you control access to.</span></span> <span data-ttu-id="40b38-110">Aucun point de terminaison de service n’est inscrit sur le serveur DNS Public.</span><span class="sxs-lookup"><span data-stu-id="40b38-110">None of the service endpoints are registered on the Public DNS Server.</span></span>

<span data-ttu-id="40b38-111">Avec la Gestion des API en mode interne, vous pouvez effectuer les scénarios suivants :</span><span class="sxs-lookup"><span data-stu-id="40b38-111">Using API Management in Internal mode, you can achieve the following scenarios</span></span>
* <span data-ttu-id="40b38-112">Rendre les API hébergées dans votre centre de données privé accessibles de l’extérieur en toute sécurité à des tiers à l’aide de connexions VPN ExpressRoute ou de site à site.</span><span class="sxs-lookup"><span data-stu-id="40b38-112">Securely make APIs hosted in your private datacenter accessible by 3rd parties outside of it using Site-to-Site or ExpressRoute VPN connections.</span></span>
* <span data-ttu-id="40b38-113">Activer les scénarios de cloud hybride en exposant vos API cloud et locales par le biais d’une passerelle commune.</span><span class="sxs-lookup"><span data-stu-id="40b38-113">Enable hybrid cloud scenarios by exposing your cloud-based APIs and on-prem APIs through a common gateway.</span></span>
* <span data-ttu-id="40b38-114">Gérer vos API hébergées dans plusieurs emplacements géographiques à l’aide d’un seul point de terminaison de passerelle.</span><span class="sxs-lookup"><span data-stu-id="40b38-114">Manage your APIs hosted in multiple geographic locations using a single Gateway endpoint.</span></span> 

## <span data-ttu-id="40b38-115"><a name="enable-vpn"> </a>Créer une Gestion des API dans un réseau virtuel interne</span><span class="sxs-lookup"><span data-stu-id="40b38-115"><a name="enable-vpn"> </a>Creating an API Management in Internal Virtual network</span></span>
<span data-ttu-id="40b38-116">Le service Gestion des API dans un réseau virtuel interne est hébergé derrière un équilibreur de charge interne.</span><span class="sxs-lookup"><span data-stu-id="40b38-116">The API Management service in Internal Virtual network is hosted behind an Internal Load Balancer(ILB).</span></span> <span data-ttu-id="40b38-117">L’adresse IP de l’équilibreur se trouve dans la plage [RFC1918](http://www.faqs.org/rfcs/rfc1918.html).</span><span class="sxs-lookup"><span data-stu-id="40b38-117">The IP Address of the ILB is in the [RFC1918](http://www.faqs.org/rfcs/rfc1918.html) range.</span></span>  

### <a name="enable-vnet-connection-using-azure-portal"></a><span data-ttu-id="40b38-118">Activer la connexion au réseau virtuel à l’aide du Portail Azure</span><span class="sxs-lookup"><span data-stu-id="40b38-118">Enable VNET connection using Azure portal</span></span>
<span data-ttu-id="40b38-119">Tout d’abord, créez le service Gestion des API en suivant les étapes de la section [Créer un service Gestion des API][Create API Management service].</span><span class="sxs-lookup"><span data-stu-id="40b38-119">First create the API Management service by following the steps [Create API Management service][Create API Management service].</span></span> <span data-ttu-id="40b38-120">Ensuite, configurez la Gestion des API de façon à la déployer à l’intérieur d’un réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="40b38-120">Then set-up API Management to be deployed inside a Virtual network.</span></span>

![Menu de configuration de la Gestion des API dans un réseau virtuel interne][api-management-using-internal-vnet-menu]

<span data-ttu-id="40b38-122">Une fois le déploiement réussi, l’adresse IP virtuelle interne de votre service apparaît sur le tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="40b38-122">After the deployment succeeds, you should see the Internal Virtual IP Address of your service on the dashboard.</span></span>

![Tableau de bord Gestion des API avec réseau virtuel interne configuré][api-management-internal-vnet-dashboard]

### <a name="enable-vnet-connection-using-powershell-cmdlets"></a><span data-ttu-id="40b38-124">Activer la connexion au réseau virtuel à l’aide d’applets de commande PowerShell</span><span class="sxs-lookup"><span data-stu-id="40b38-124">Enable VNET connection using Powershell cmdlets</span></span>
<span data-ttu-id="40b38-125">Vous pouvez également activer la connectivité de réseau virtuel à l’aide d’applets de commande PowerShell.</span><span class="sxs-lookup"><span data-stu-id="40b38-125">You can also enable VNET connectivity using the PowerShell cmdlets.</span></span>

* <span data-ttu-id="40b38-126">**Créer un service Gestion des API au sein d’un réseau virtuel** : utilisez l’applet de commande [New-AzureRmApiManagement](/powershell/module/azurerm.apimanagement/new-azurermapimanagement) pour créer un service Gestion des API Azure au sein d’un réseau virtuel et le configurer de sorte qu’il utilise le type réseau virtuel interne.</span><span class="sxs-lookup"><span data-stu-id="40b38-126">**Create an API Management service inside a VNET**: Use the cmdlet [New-AzureRmApiManagement](/powershell/module/azurerm.apimanagement/new-azurermapimanagement) to create an Azure API Management service inside a VNET and configure it to use the Internal VNET type.</span></span>

* <span data-ttu-id="40b38-127">**Déployer un service Gestion des API existant au sein d’un réseau virtuel** : utilisez l’applet de commande [Update-AzureRmApiManagementDeployment](/powershell/module/azurerm.apimanagement/update-azurermapimanagementdeployment) pour déplacer un service Gestion des API Azure existant au sein d’un réseau virtuel et le configurer de sorte qu’il utilise le type réseau virtuel interne.</span><span class="sxs-lookup"><span data-stu-id="40b38-127">**Deploy an existing API Management service inside a VNET**: Use the cmdlet [Update-AzureRmApiManagementDeployment](/powershell/module/azurerm.apimanagement/update-azurermapimanagementdeployment) to move an existing Azure API Management service inside a Virtual network and configure it to use Internal VNET type.</span></span>

## <span data-ttu-id="40b38-128"><a name="apim-dns-configuration"></a>Configuration DNS</span><span class="sxs-lookup"><span data-stu-id="40b38-128"><a name="apim-dns-configuration"></a>DNS configuration</span></span>
<span data-ttu-id="40b38-129">Lorsque vous utilisez la Gestion des API en mode réseau virtuel externe, DNS est géré par Azure.</span><span class="sxs-lookup"><span data-stu-id="40b38-129">When using API Management in External Virtual network mode, DNS is managed by Azure.</span></span> <span data-ttu-id="40b38-130">En mode réseau virtuel interne, vous devez gérer votre propre serveur DNS.</span><span class="sxs-lookup"><span data-stu-id="40b38-130">For Internal Virtual network mode, you have to manage your own DNS.</span></span>

> [!NOTE]
> <span data-ttu-id="40b38-131">Le service Gestion des API n’écoute pas les demandes entrantes sur les adresses IP.</span><span class="sxs-lookup"><span data-stu-id="40b38-131">API Management service does not listen to requests coming on IP addresses.</span></span> <span data-ttu-id="40b38-132">Il répond uniquement aux demandes envoyées au nom d’hôte configuré sur ses points de terminaison de service (à savoir la passerelle, le portail des développeurs, le portail des éditeurs, le point de terminaison de gestion directe et git).</span><span class="sxs-lookup"><span data-stu-id="40b38-132">It only responds to requests to the Hostname configured on its service endpoints (which includes gateway, developer portal, publisher Portal, direct management endpoint, and git).</span></span>

### <a name="access-on-default-host-names"></a><span data-ttu-id="40b38-133">Accès sur les noms d’hôtes par défaut :</span><span class="sxs-lookup"><span data-stu-id="40b38-133">Access on default host names:</span></span>
<span data-ttu-id="40b38-134">Lorsque vous créez un service Gestion des API dans le cloud public Azure, nommé « contoso » par exemple, les points de terminaison de service suivants sont configurés par défaut.</span><span class="sxs-lookup"><span data-stu-id="40b38-134">When you create an API Management service in public Azure cloud, named "contoso" for example, the following service endpoints are configured by default.</span></span>

>   <span data-ttu-id="40b38-135">Passerelle / Proxy : contoso.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="40b38-135">Gateway / Proxy - contoso.azure-api.net</span></span>

> <span data-ttu-id="40b38-136">Portail des éditeurs et portail des développeurs : contoso.portal.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="40b38-136">Publisher Portal and Developer Portal - contoso.portal.azure-api.net</span></span>

> <span data-ttu-id="40b38-137">Point de terminaison de gestion directe : contoso.management.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="40b38-137">Direct Management Endpoint - contoso.management.azure-api.net</span></span>

>   <span data-ttu-id="40b38-138">Git : contoso.scm.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="40b38-138">GIT - contoso.scm.azure-api.net</span></span>

<span data-ttu-id="40b38-139">Pour accéder à ces points de terminaison de service Gestion des API, vous pouvez créer une machine virtuelle dans un sous-réseau connecté au réseau virtuel dans lequel la Gestion des API est déployée.</span><span class="sxs-lookup"><span data-stu-id="40b38-139">To access these API Management service endpoints, you can create a Virtual Machine in a subnet connected to the Virtual network in which API Management is deployed.</span></span> <span data-ttu-id="40b38-140">En supposant que l’adresse IP virtuelle interne de votre service est 10.0.0.5, vous pouvez effectuer le mappage des fichiers hôtes (%SystemDrive%\drivers\etc\hosts) de la façon suivante :</span><span class="sxs-lookup"><span data-stu-id="40b38-140">Assuming the Internal Virtual IP Address for your service is 10.0.0.5, you can do the hosts file mapping (%SystemDrive%\drivers\etc\hosts) as follows:</span></span>

> <span data-ttu-id="40b38-141">10.0.0.5    contoso.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="40b38-141">10.0.0.5    contoso.azure-api.net</span></span>

> <span data-ttu-id="40b38-142">10.0.0.5    contoso.portal.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="40b38-142">10.0.0.5    contoso.portal.azure-api.net</span></span>

> <span data-ttu-id="40b38-143">10.0.0.5    contoso.management.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="40b38-143">10.0.0.5    contoso.management.azure-api.net</span></span>

> <span data-ttu-id="40b38-144">10.0.0.5    contoso.scm.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="40b38-144">10.0.0.5    contoso.scm.azure-api.net</span></span>

<span data-ttu-id="40b38-145">Vous pouvez alors accéder à tous les points de terminaison de service à partir de la machine virtuelle que vous avez créée.</span><span class="sxs-lookup"><span data-stu-id="40b38-145">You can then access all the service endpoints from the Virtual Machine you created.</span></span> <span data-ttu-id="40b38-146">Si vous utilisez un serveur DNS personnalisé dans un réseau virtuel, vous pouvez également créer des enregistrements DNS A et accéder à ces points de terminaison à partir de l’endroit de votre choix dans votre réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="40b38-146">If using a Custom DNS server in a Virtual network, you can also create A DNS records and access these endpoints from anywhere in your Virtual network.</span></span> 

### <a name="access-on-custom-domain-names"></a><span data-ttu-id="40b38-147">Accès sur des noms de domaines personnalisés :</span><span class="sxs-lookup"><span data-stu-id="40b38-147">Access on custom domain names:</span></span>
<span data-ttu-id="40b38-148">Si vous ne souhaitez pas accéder au service Gestion des API avec les noms d’hôtes par défaut, vous pouvez configurer des noms de domaines personnalisés pour tous vos points de terminaison de service, comme ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="40b38-148">If you don’t want to access the API Management service with the default host names, you can setup custom domain names for all your service endpoints like below</span></span>

![Configuration d’un domaine personnalisé pour la Gestion des API][api-management-custom-domain-name]

<span data-ttu-id="40b38-150">Vous pouvez ensuite créer des enregistrements A dans votre serveur DNS de façon à accéder à ces points de terminaison, qui ne sont accessibles qu’à partir de votre réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="40b38-150">Then you can create A records in your DNS Server to access these endpoints which are only accessible from within your Virtual network.</span></span>

## <span data-ttu-id="40b38-151"><a name="related-content"> </a>Contenu connexe</span><span class="sxs-lookup"><span data-stu-id="40b38-151"><a name="related-content"> </a>Related content</span></span>
* <span data-ttu-id="40b38-152">[Problèmes courants de configuration réseau lors de l’installation de la Gestion des API dans un réseau virtuel][Common Network Configuration Issues]</span><span class="sxs-lookup"><span data-stu-id="40b38-152">[Common Network configuration issues while setting up APIM in VNET][Common Network Configuration Issues]</span></span>
* [<span data-ttu-id="40b38-153">FAQ des réseaux virtuels</span><span class="sxs-lookup"><span data-stu-id="40b38-153">Virtual Network faqs</span></span>](../virtual-network/virtual-networks-faq.md)
* [<span data-ttu-id="40b38-154">Création d’un enregistrement A dans DNS</span><span class="sxs-lookup"><span data-stu-id="40b38-154">Creating A record in DNS</span></span>](https://msdn.microsoft.com/en-us/library/bb727018.aspx)

[api-management-using-internal-vnet-menu]: ./media/api-management-using-with-internal-vnet/api-management-internal-vnet-menu.png
[api-management-internal-vnet-dashboard]: ./media/api-management-using-with-internal-vnet/api-management-internal-vnet-dashboard.png
[api-management-custom-domain-name]: ./media/api-management-using-with-internal-vnet/api-management-custom-domain-name.png

[Create API Management service]: api-management-get-started.md#create-service-instance
[Common Network Configuration Issues]: api-management-using-with-vnet.md#network-configuration-issues
