---
title: "aaaHow toouse gestion des API Azure avec un réseau virtuel interne | Documents Microsoft"
description: "Découvrez comment toosetup et configurer la gestion des API Azure dans un réseau virtuel interne."
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
ms.openlocfilehash: 8d25de14e0c0bebe7ba7b47ca432ea4e45dde312
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-api-management-service-with-internal-virtual-network"></a><span data-ttu-id="fbcc8-103">Utiliser le service Gestion des API Azure avec un réseau virtuel interne</span><span class="sxs-lookup"><span data-stu-id="fbcc8-103">Using Azure API Management service with Internal Virtual Network</span></span>
<span data-ttu-id="fbcc8-104">Réseaux virtuels Azure (réseaux virtuels), gestion des API permet de gérer les API non accessibles sur Internet de hello.</span><span class="sxs-lookup"><span data-stu-id="fbcc8-104">With Azure Virtual Networks (VNETs), API Management can manage APIs not accessible on hello Internet.</span></span> <span data-ttu-id="fbcc8-105">Un nombre de technologies VPN est des connexions de hello toomake disponibles et gestion des API peut être déployée dans deux modes principales à l’intérieur de hello réseau virtuel :</span><span class="sxs-lookup"><span data-stu-id="fbcc8-105">A number of VPN technologies are available toomake hello connection and API Management can be deployed in two main modes inside hello VNET:</span></span>
* <span data-ttu-id="fbcc8-106">Externe</span><span class="sxs-lookup"><span data-stu-id="fbcc8-106">External</span></span>
* <span data-ttu-id="fbcc8-107">Interne</span><span class="sxs-lookup"><span data-stu-id="fbcc8-107">Internal</span></span>

## <span data-ttu-id="fbcc8-108"><a name="overview"></a>Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="fbcc8-108"><a name="overview"> </a>Overview</span></span>
<span data-ttu-id="fbcc8-109">Lors de la gestion des API est déployée dans un mode de réseau virtuel interne, tous les hello service points de terminaison (passerelle, portail des développeurs, portail de publication, la gestion directe et Git) sont uniquement visibles à l’intérieur d’un réseau virtuel que vous contrôlez l’accès à.</span><span class="sxs-lookup"><span data-stu-id="fbcc8-109">When API Management is deployed in an Internal Virtual network mode, all hello service endpoints (gateway, developer portal, publisher portal, direct management and Git) are only visible inside a Virtual network that you control access to.</span></span> <span data-ttu-id="fbcc8-110">Aucun des points de terminaison de service hello sont inscrits sur le serveur DNS Public de hello.</span><span class="sxs-lookup"><span data-stu-id="fbcc8-110">None of hello service endpoints are registered on hello Public DNS Server.</span></span>

<span data-ttu-id="fbcc8-111">À l’aide de gestion des API en mode interne, vous pouvez obtenir hello les scénarios suivants</span><span class="sxs-lookup"><span data-stu-id="fbcc8-111">Using API Management in Internal mode, you can achieve hello following scenarios</span></span>
* <span data-ttu-id="fbcc8-112">Rendre les API hébergées dans votre centre de données privé accessibles de l’extérieur en toute sécurité à des tiers à l’aide de connexions VPN ExpressRoute ou de site à site.</span><span class="sxs-lookup"><span data-stu-id="fbcc8-112">Securely make APIs hosted in your private datacenter accessible by 3rd parties outside of it using Site-to-Site or ExpressRoute VPN connections.</span></span>
* <span data-ttu-id="fbcc8-113">Activer les scénarios de cloud hybride en exposant vos API cloud et locales par le biais d’une passerelle commune.</span><span class="sxs-lookup"><span data-stu-id="fbcc8-113">Enable hybrid cloud scenarios by exposing your cloud-based APIs and on-prem APIs through a common gateway.</span></span>
* <span data-ttu-id="fbcc8-114">Gérer vos API hébergées dans plusieurs emplacements géographiques à l’aide d’un seul point de terminaison de passerelle.</span><span class="sxs-lookup"><span data-stu-id="fbcc8-114">Manage your APIs hosted in multiple geographic locations using a single Gateway endpoint.</span></span> 

## <span data-ttu-id="fbcc8-115"><a name="enable-vpn"></a>Créer une Gestion des API dans un réseau virtuel interne</span><span class="sxs-lookup"><span data-stu-id="fbcc8-115"><a name="enable-vpn"> </a>Creating an API Management in Internal Virtual network</span></span>
<span data-ttu-id="fbcc8-116">Hello service de gestion des API dans le réseau virtuel interne est hébergé derrière un Balancer(ILB) de charge interne.</span><span class="sxs-lookup"><span data-stu-id="fbcc8-116">hello API Management service in Internal Virtual network is hosted behind an Internal Load Balancer(ILB).</span></span> <span data-ttu-id="fbcc8-117">Hello, adresse IP de hello équilibrage de charge interne est Bonjour [RFC1918](http://www.faqs.org/rfcs/rfc1918.html) plage.</span><span class="sxs-lookup"><span data-stu-id="fbcc8-117">hello IP Address of hello ILB is in hello [RFC1918](http://www.faqs.org/rfcs/rfc1918.html) range.</span></span>  

### <a name="enable-vnet-connection-using-azure-portal"></a><span data-ttu-id="fbcc8-118">Activer la connexion au réseau virtuel à l’aide du Portail Azure</span><span class="sxs-lookup"><span data-stu-id="fbcc8-118">Enable VNET connection using Azure portal</span></span>
<span data-ttu-id="fbcc8-119">Tout d’abord créer le service de gestion des API de hello en suivant les étapes de hello [service de gestion des API créer][Create API Management service].</span><span class="sxs-lookup"><span data-stu-id="fbcc8-119">First create hello API Management service by following hello steps [Create API Management service][Create API Management service].</span></span> <span data-ttu-id="fbcc8-120">Puis les toobe de gestion des API configuration déployé à l’intérieur d’un réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="fbcc8-120">Then set-up API Management toobe deployed inside a Virtual network.</span></span>

![Menu de configuration de la Gestion des API dans un réseau virtuel interne][api-management-using-internal-vnet-menu]

<span data-ttu-id="fbcc8-122">Après la réussite du déploiement de hello, vous devez voir hello une adresse IP virtuelle interne de votre service sur le tableau de bord hello.</span><span class="sxs-lookup"><span data-stu-id="fbcc8-122">After hello deployment succeeds, you should see hello Internal Virtual IP Address of your service on hello dashboard.</span></span>

![Tableau de bord Gestion des API avec réseau virtuel interne configuré][api-management-internal-vnet-dashboard]

### <a name="enable-vnet-connection-using-powershell-cmdlets"></a><span data-ttu-id="fbcc8-124">Activer la connexion au réseau virtuel à l’aide d’applets de commande PowerShell</span><span class="sxs-lookup"><span data-stu-id="fbcc8-124">Enable VNET connection using Powershell cmdlets</span></span>
<span data-ttu-id="fbcc8-125">Vous pouvez également activer la connectivité de réseau virtuel à l’aide des applets de commande PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="fbcc8-125">You can also enable VNET connectivity using hello PowerShell cmdlets.</span></span>

* <span data-ttu-id="fbcc8-126">**Créer un service de gestion des API à l’intérieur d’un réseau virtuel**: utiliser l’applet de commande hello [New-AzureRmApiManagement](/powershell/module/azurerm.apimanagement/new-azurermapimanagement) toocreate une gestion des API Azure à l’intérieur d’un réseau virtuel de service et configurez le type de réseau virtuel interne toouse hello.</span><span class="sxs-lookup"><span data-stu-id="fbcc8-126">**Create an API Management service inside a VNET**: Use hello cmdlet [New-AzureRmApiManagement](/powershell/module/azurerm.apimanagement/new-azurermapimanagement) toocreate an Azure API Management service inside a VNET and configure it toouse hello Internal VNET type.</span></span>

* <span data-ttu-id="fbcc8-127">**Déployer un service de gestion des API existant à l’intérieur d’un réseau virtuel**: utiliser l’applet de commande hello [AzureRmApiManagementDeployment de mise à jour](/powershell/module/azurerm.apimanagement/update-azurermapimanagementdeployment) toomove une gestion des API Azure existante de service à l’intérieur d’un réseau virtuel et le configurer toouse Type de réseau virtuel interne.</span><span class="sxs-lookup"><span data-stu-id="fbcc8-127">**Deploy an existing API Management service inside a VNET**: Use hello cmdlet [Update-AzureRmApiManagementDeployment](/powershell/module/azurerm.apimanagement/update-azurermapimanagementdeployment) toomove an existing Azure API Management service inside a Virtual network and configure it toouse Internal VNET type.</span></span>

## <span data-ttu-id="fbcc8-128"><a name="apim-dns-configuration"></a>Configuration DNS</span><span class="sxs-lookup"><span data-stu-id="fbcc8-128"><a name="apim-dns-configuration"></a>DNS configuration</span></span>
<span data-ttu-id="fbcc8-129">Lorsque vous utilisez la Gestion des API en mode réseau virtuel externe, DNS est géré par Azure.</span><span class="sxs-lookup"><span data-stu-id="fbcc8-129">When using API Management in External Virtual network mode, DNS is managed by Azure.</span></span> <span data-ttu-id="fbcc8-130">Pour le mode réseau virtuel interne, vous avez toomanage votre propre serveur DNS.</span><span class="sxs-lookup"><span data-stu-id="fbcc8-130">For Internal Virtual network mode, you have toomanage your own DNS.</span></span>

> [!NOTE]
> <span data-ttu-id="fbcc8-131">Service de gestion des API n’écoute pas toorequests provenant des adresses IP.</span><span class="sxs-lookup"><span data-stu-id="fbcc8-131">API Management service does not listen toorequests coming on IP addresses.</span></span> <span data-ttu-id="fbcc8-132">Il ne répond que toorequests toohello nom d’hôte configuré sur ses points de terminaison de service (qui inclut la passerelle, portail des développeurs, l’éditeur Portal, point de terminaison de la gestion directe et git).</span><span class="sxs-lookup"><span data-stu-id="fbcc8-132">It only responds toorequests toohello Hostname configured on its service endpoints (which includes gateway, developer portal, publisher Portal, direct management endpoint, and git).</span></span>

### <a name="access-on-default-host-names"></a><span data-ttu-id="fbcc8-133">Accès sur les noms d’hôtes par défaut :</span><span class="sxs-lookup"><span data-stu-id="fbcc8-133">Access on default host names:</span></span>
<span data-ttu-id="fbcc8-134">Lorsque vous créez un service de gestion des API dans le cloud public Azure, nommé « contoso » par exemple, hello points de terminaison de service suivants sont configurés par défaut.</span><span class="sxs-lookup"><span data-stu-id="fbcc8-134">When you create an API Management service in public Azure cloud, named "contoso" for example, hello following service endpoints are configured by default.</span></span>

>   <span data-ttu-id="fbcc8-135">Passerelle / Proxy : contoso.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="fbcc8-135">Gateway / Proxy - contoso.azure-api.net</span></span>

> <span data-ttu-id="fbcc8-136">Portail des éditeurs et portail des développeurs : contoso.portal.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="fbcc8-136">Publisher Portal and Developer Portal - contoso.portal.azure-api.net</span></span>

> <span data-ttu-id="fbcc8-137">Point de terminaison de gestion directe : contoso.management.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="fbcc8-137">Direct Management Endpoint - contoso.management.azure-api.net</span></span>

>   <span data-ttu-id="fbcc8-138">Git : contoso.scm.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="fbcc8-138">GIT - contoso.scm.azure-api.net</span></span>

<span data-ttu-id="fbcc8-139">tooaccess ces points de terminaison du service de gestion des API, vous pouvez créer un ordinateur virtuel dans un réseau virtuel de toohello sous-réseau connecté dans lequel la gestion des API est déployée.</span><span class="sxs-lookup"><span data-stu-id="fbcc8-139">tooaccess these API Management service endpoints, you can create a Virtual Machine in a subnet connected toohello Virtual network in which API Management is deployed.</span></span> <span data-ttu-id="fbcc8-140">En supposant que hello interne adresse IP virtuelle pour votre service est 10.0.0.5, vous pouvez effectuer hello le mappage de fichier hôtes (% SystemDrive%\drivers\etc\hosts) comme suit :</span><span class="sxs-lookup"><span data-stu-id="fbcc8-140">Assuming hello Internal Virtual IP Address for your service is 10.0.0.5, you can do hello hosts file mapping (%SystemDrive%\drivers\etc\hosts) as follows:</span></span>

> <span data-ttu-id="fbcc8-141">10.0.0.5    contoso.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="fbcc8-141">10.0.0.5    contoso.azure-api.net</span></span>

> <span data-ttu-id="fbcc8-142">10.0.0.5    contoso.portal.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="fbcc8-142">10.0.0.5    contoso.portal.azure-api.net</span></span>

> <span data-ttu-id="fbcc8-143">10.0.0.5    contoso.management.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="fbcc8-143">10.0.0.5    contoso.management.azure-api.net</span></span>

> <span data-ttu-id="fbcc8-144">10.0.0.5    contoso.scm.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="fbcc8-144">10.0.0.5    contoso.scm.azure-api.net</span></span>

<span data-ttu-id="fbcc8-145">Vous pouvez ensuite accéder à tous les points de terminaison de service hello de hello Machine virtuelle que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="fbcc8-145">You can then access all hello service endpoints from hello Virtual Machine you created.</span></span> <span data-ttu-id="fbcc8-146">Si vous utilisez un serveur DNS personnalisé dans un réseau virtuel, vous pouvez également créer des enregistrements DNS A et accéder à ces points de terminaison à partir de l’endroit de votre choix dans votre réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="fbcc8-146">If using a Custom DNS server in a Virtual network, you can also create A DNS records and access these endpoints from anywhere in your Virtual network.</span></span> 

### <a name="access-on-custom-domain-names"></a><span data-ttu-id="fbcc8-147">Accès sur des noms de domaines personnalisés :</span><span class="sxs-lookup"><span data-stu-id="fbcc8-147">Access on custom domain names:</span></span>
<span data-ttu-id="fbcc8-148">Si vous ne souhaitez pas tooaccess hello service Gestion des noms d’hôte par défaut hello API, vous pouvez configurer des noms de domaine personnalisé pour tous vos points de terminaison service comme ci-dessous</span><span class="sxs-lookup"><span data-stu-id="fbcc8-148">If you don’t want tooaccess hello API Management service with hello default host names, you can setup custom domain names for all your service endpoints like below</span></span>

![Configuration d’un domaine personnalisé pour la Gestion des API][api-management-custom-domain-name]

<span data-ttu-id="fbcc8-150">Puis vous pouvez créer un enregistrements dans votre serveur DNS de tooaccess ces points de terminaison qui sont uniquement accessibles à partir de votre réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="fbcc8-150">Then you can create A records in your DNS Server tooaccess these endpoints which are only accessible from within your Virtual network.</span></span>

## <span data-ttu-id="fbcc8-151"><a name="related-content"></a>Contenu connexe</span><span class="sxs-lookup"><span data-stu-id="fbcc8-151"><a name="related-content"> </a>Related content</span></span>
* <span data-ttu-id="fbcc8-152">[Problèmes courants de configuration réseau lors de l’installation de la Gestion des API dans un réseau virtuel][Common Network Configuration Issues]</span><span class="sxs-lookup"><span data-stu-id="fbcc8-152">[Common Network configuration issues while setting up APIM in VNET][Common Network Configuration Issues]</span></span>
* [<span data-ttu-id="fbcc8-153">FAQ des réseaux virtuels</span><span class="sxs-lookup"><span data-stu-id="fbcc8-153">Virtual Network faqs</span></span>](../virtual-network/virtual-networks-faq.md)
* [<span data-ttu-id="fbcc8-154">Création d’un enregistrement A dans DNS</span><span class="sxs-lookup"><span data-stu-id="fbcc8-154">Creating A record in DNS</span></span>](https://msdn.microsoft.com/en-us/library/bb727018.aspx)

[api-management-using-internal-vnet-menu]: ./media/api-management-using-with-internal-vnet/api-management-internal-vnet-menu.png
[api-management-internal-vnet-dashboard]: ./media/api-management-using-with-internal-vnet/api-management-internal-vnet-dashboard.png
[api-management-custom-domain-name]: ./media/api-management-using-with-internal-vnet/api-management-custom-domain-name.png

[Create API Management service]: api-management-get-started.md#create-service-instance
[Common Network Configuration Issues]: api-management-using-with-vnet.md#network-configuration-issues
