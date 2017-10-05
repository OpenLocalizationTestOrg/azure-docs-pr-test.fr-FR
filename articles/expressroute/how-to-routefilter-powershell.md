---
title: "Configurer des filtres de routage pour l’homologation d’Azure ExpressRoute Microsoft : PowerShell | Microsoft Docs"
description: "Cet article décrit comment configurer des filtres de routage pour l’homologation Microsoft à l’aide de PowerShell."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/16/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: de3550c20439fa809869d98b8a57ea3be9c03e7c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="configure-route-filters-for-microsoft-peering"></a><span data-ttu-id="091e7-103">Configurer des filtres de routage pour l’homologation Microsoft</span><span class="sxs-lookup"><span data-stu-id="091e7-103">Configure route filters for Microsoft peering</span></span>

<span data-ttu-id="091e7-104">Les filtres de routage permettent d’utiliser un sous-ensemble de services pris en charge via l’homologation Microsoft.</span><span class="sxs-lookup"><span data-stu-id="091e7-104">Route filters are a way to consume a subset of supported services through Microsoft peering.</span></span> <span data-ttu-id="091e7-105">Les étapes décrites dans cet article vous aident à configurer et à gérer des filtres de routage pour les circuits ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="091e7-105">The steps in this article help you configure and manage route filters for ExpressRoute circuits.</span></span>

<span data-ttu-id="091e7-106">Les services Dynamics 365 services et les services Office 365, comme Exchange Online, SharePoint Online et Skype pour entreprises, sont accessibles via l’homologation Microsoft.</span><span class="sxs-lookup"><span data-stu-id="091e7-106">Dynamics 365 services, and Office 365 services such as Exchange Online, SharePoint Online, and Skype for Business, are accessible through the Microsoft peering.</span></span> <span data-ttu-id="091e7-107">Lorsque l’homologation Microsoft est configurée dans un circuit ExpressRoute, tous les préfixes liés à ces services sont publiés via les sessions BGP établies.</span><span class="sxs-lookup"><span data-stu-id="091e7-107">When Microsoft peering is configured in an ExpressRoute circuit, all prefixes related to these services are advertised through the BGP sessions that are established.</span></span> <span data-ttu-id="091e7-108">Une valeur de communauté BGP est attachée à chaque préfixe pour identifier le service qui est proposé par le biais du préfixe.</span><span class="sxs-lookup"><span data-stu-id="091e7-108">A BGP community value is attached to every prefix to identify the service that is offered through the prefix.</span></span> <span data-ttu-id="091e7-109">Pour obtenir la liste de valeurs de communauté BGP et des services auxquels elles sont mappées, consultez les [communautés BGP](expressroute-routing.md#bgp).</span><span class="sxs-lookup"><span data-stu-id="091e7-109">For a list of the BGP community values and the services they  map to, see [BGP communities](expressroute-routing.md#bgp).</span></span>

<span data-ttu-id="091e7-110">Si vous avez besoin de connectivité à tous les services, de nombreux préfixes sont publiés via BGP.</span><span class="sxs-lookup"><span data-stu-id="091e7-110">If you require connectivity to all services, a large number of prefixes are advertised through BGP.</span></span> <span data-ttu-id="091e7-111">Cela augmente considérablement la taille des tables de routage gérées par les routeurs au sein de votre réseau.</span><span class="sxs-lookup"><span data-stu-id="091e7-111">This significantly increases the size of the route tables maintained by routers within your network.</span></span> <span data-ttu-id="091e7-112">Si vous envisagez d’utiliser uniquement un sous-ensemble des services offerts par le biais de l’homologation de Microsoft, vous pouvez réduire la taille de vos tables de routage de deux manières.</span><span class="sxs-lookup"><span data-stu-id="091e7-112">If you plan to consume only a subset of services offered through Microsoft peering, you can reduce the size of your route tables in two ways.</span></span> <span data-ttu-id="091e7-113">Vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="091e7-113">You can:</span></span>

- <span data-ttu-id="091e7-114">Filtrer les préfixes indésirables en appliquant des filtres de routage sur les communautés BGP.</span><span class="sxs-lookup"><span data-stu-id="091e7-114">Filter out unwanted prefixes by applying route filters on BGP communities.</span></span> <span data-ttu-id="091e7-115">Ceci est une pratique standard et très courante de mise en réseau.</span><span class="sxs-lookup"><span data-stu-id="091e7-115">This is a standard networking practice and is used commonly within many networks.</span></span>

- <span data-ttu-id="091e7-116">Définir des filtres de routage et les appliquer à votre circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="091e7-116">Define route filters and apply them to your ExpressRoute circuit.</span></span> <span data-ttu-id="091e7-117">Un filtre de routage est une ressource qui vous permet de sélectionner la liste des services que vous envisagez d’utiliser via l’homologation Microsoft.</span><span class="sxs-lookup"><span data-stu-id="091e7-117">A route filter is a new resource that lets you select the list of services you plan to consume through Microsoft peering.</span></span> <span data-ttu-id="091e7-118">Les routeurs ExpressRoute envoient uniquement la liste des préfixes qui appartiennent aux services identifiés dans le filtre de routage.</span><span class="sxs-lookup"><span data-stu-id="091e7-118">ExpressRoute routers only send the list of prefixes that belong to the services identified in the route filter.</span></span>

### <span data-ttu-id="091e7-119"><a name="about"></a>À propos des filtres de routage</span><span class="sxs-lookup"><span data-stu-id="091e7-119"><a name="about"></a>About route filters</span></span>

<span data-ttu-id="091e7-120">Lorsque l’homologation Microsoft est configurée sur votre circuit ExpressRoute, les routeurs de périphérie Microsoft établissent une paire de sessions BGP avec les routeurs de périphérie (les vôtres ou ceux de votre fournisseur de connectivité).</span><span class="sxs-lookup"><span data-stu-id="091e7-120">When Microsoft peering is configured on your ExpressRoute circuit, the Microsoft edge routers establish a pair of BGP sessions with the edge routers (yours or your connectivity provider's).</span></span> <span data-ttu-id="091e7-121">Aucun routage n’est publié sur votre réseau.</span><span class="sxs-lookup"><span data-stu-id="091e7-121">No routes are advertised to your network.</span></span> <span data-ttu-id="091e7-122">Pour activer les annonces de routage sur votre réseau, vous devez associer un filtre de routage.</span><span class="sxs-lookup"><span data-stu-id="091e7-122">To enable route advertisements to your network, you must associate a route filter.</span></span>

<span data-ttu-id="091e7-123">Un filtre de routage vous permet d’identifier les services que vous souhaitez utiliser via l’homologation Microsoft de votre circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="091e7-123">A route filter lets you identify services you want to consume through your ExpressRoute circuit's Microsoft peering.</span></span> <span data-ttu-id="091e7-124">Il s’agit essentiellement d’une liste blanche de toutes les valeurs de communauté BGP.</span><span class="sxs-lookup"><span data-stu-id="091e7-124">It is essentially a white list of all the BGP community values.</span></span> <span data-ttu-id="091e7-125">Une fois qu’une ressource de filtre de routage est définie et jointe à un circuit ExpressRoute, tous les préfixes qui mappent aux valeurs de communauté BGP sont publiés sur votre réseau.</span><span class="sxs-lookup"><span data-stu-id="091e7-125">Once a route filter resource is defined and attached to an ExpressRoute circuit, all prefixes that map to the BGP community values are advertised to your network.</span></span>

<span data-ttu-id="091e7-126">Pour être en mesure de joindre des filtres de routage à des services Office 365, vous devez être autorisé à utiliser les services Office 365 via ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="091e7-126">To be able to attach route filters with Office 365 services on them, you must have authorization to consume Office 365 services through ExpressRoute.</span></span> <span data-ttu-id="091e7-127">Si vous n’êtes pas autorisé à utiliser les services Office 365 via ExpressRoute, la jointure des filtres de routage échoue.</span><span class="sxs-lookup"><span data-stu-id="091e7-127">If you are not authorized to consume Office 365 services through ExpressRoute, the operation to attach route filters fails.</span></span> <span data-ttu-id="091e7-128">Pour plus d’informations sur le processus d’autorisation, consultez [Azure ExpressRoute pour Office 365](https://support.office.com/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd).</span><span class="sxs-lookup"><span data-stu-id="091e7-128">For more information about the authorization process, see [Azure ExpressRoute for Office 365](https://support.office.com/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd).</span></span> <span data-ttu-id="091e7-129">La connectivité aux services Dynamics 365 ne nécessite pas d’autorisation préalable.</span><span class="sxs-lookup"><span data-stu-id="091e7-129">Connectivity to Dynamics 365 services does NOT require any prior authorization.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="091e7-130">L’homologation Microsoft des circuits ExpressRoute configurés avant le 1er août 2017 entraînera la publication de tous les préfixes de service via l’homologation Microsoft, même si les filtres de routage ne sont pas définis.</span><span class="sxs-lookup"><span data-stu-id="091e7-130">Microsoft peering of ExpressRoute circuits that were configured prior to August 1, 2017 will have all service prefixes advertised through Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="091e7-131">L’homologation Microsoft des circuits ExpressRoute configurés à compter du 1er août 2017 n’entraînera la publication d’aucun préfixe tant qu’un filtre de routage n’aura pas été joint au circuit.</span><span class="sxs-lookup"><span data-stu-id="091e7-131">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached to the circuit.</span></span>
> 
> 

### <span data-ttu-id="091e7-132"><a name="workflow"></a>Flux de travail</span><span class="sxs-lookup"><span data-stu-id="091e7-132"><a name="workflow"></a>Workflow</span></span>

<span data-ttu-id="091e7-133">Pour pouvoir vous connecter aux services par le biais de l’homologation Microsoft, vous devez effectuer les étapes de configuration suivantes :</span><span class="sxs-lookup"><span data-stu-id="091e7-133">To be able to successfully connect to services through Microsoft peering, you must complete the following configuration steps:</span></span>

- <span data-ttu-id="091e7-134">Vous devez disposer d’un circuit ExpressRoute actif où l’homologation Microsoft est approvisionnée.</span><span class="sxs-lookup"><span data-stu-id="091e7-134">You must have an active ExpressRoute circuit that has Microsoft peering provisioned.</span></span> <span data-ttu-id="091e7-135">Vous pouvez utiliser les instructions suivantes pour accomplir ces tâches :</span><span class="sxs-lookup"><span data-stu-id="091e7-135">You can use the following instructions to accomplish these tasks:</span></span>
  - <span data-ttu-id="091e7-136">[Créez un circuit ExpressRoute](expressroute-howto-circuit-arm.md) et faites-le activer par votre fournisseur de connectivité avant de poursuivre.</span><span class="sxs-lookup"><span data-stu-id="091e7-136">[Create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have the circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="091e7-137">Le circuit ExpressRoute doit être approvisionné et activé.</span><span class="sxs-lookup"><span data-stu-id="091e7-137">The ExpressRoute circuit must be in a provisioned and enabled state.</span></span>
  - <span data-ttu-id="091e7-138">[Créez l’homologation Microsoft](expressroute-circuit-peerings.md) si vous gérez la session BGP directement.</span><span class="sxs-lookup"><span data-stu-id="091e7-138">[Create Microsoft peering](expressroute-circuit-peerings.md) if you manage the BGP session directly.</span></span> <span data-ttu-id="091e7-139">Sinon, demandez à votre fournisseur de connectivité de configurer l’homologation Microsoft pour votre circuit.</span><span class="sxs-lookup"><span data-stu-id="091e7-139">Or, have your connectivity provider provision Microsoft peering for your circuit.</span></span>

-  <span data-ttu-id="091e7-140">Vous devez créer et configurer un filtre de routage.</span><span class="sxs-lookup"><span data-stu-id="091e7-140">You must create and configure a route filter.</span></span>
    - <span data-ttu-id="091e7-141">Identifiez les services que vous souhaitez utiliser via l’homologation Microsoft.</span><span class="sxs-lookup"><span data-stu-id="091e7-141">Identify the services you with to consume through Microsoft peering</span></span>
    - <span data-ttu-id="091e7-142">Identifiez la liste des valeurs de communauté BGP associées aux services.</span><span class="sxs-lookup"><span data-stu-id="091e7-142">Identify the list of BGP community values associated with the services</span></span>
    - <span data-ttu-id="091e7-143">Créez une règle pour autoriser la liste de préfixes correspondant aux valeurs de communauté BGP.</span><span class="sxs-lookup"><span data-stu-id="091e7-143">Create a rule to allow the prefix list matching the BGP community values</span></span>

-  <span data-ttu-id="091e7-144">Vous devez joindre le filtre de routage au circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="091e7-144">You must attach the route filter to the ExpressRoute circuit.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="091e7-145">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="091e7-145">Before you begin</span></span>

<span data-ttu-id="091e7-146">Avant de commencer la configuration, assurez-vous que les critères suivants sont respectés :</span><span class="sxs-lookup"><span data-stu-id="091e7-146">Before you begin configuration, make sure you meet the following criteria:</span></span>

 - <span data-ttu-id="091e7-147">Installez la dernière version des applets de commande PowerShell Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="091e7-147">Install the latest version of the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="091e7-148">Pour plus d’informations, voir [Installer et configurer Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="091e7-148">For more information, see [Install and configure Azure PowerShelll](/powershell/azure/install-azurerm-ps).</span></span>

  > [!NOTE]
  > <span data-ttu-id="091e7-149">Téléchargez la dernière version à partir de PowerShell Gallery, au lieu d’utiliser le programme d’installation.</span><span class="sxs-lookup"><span data-stu-id="091e7-149">Download the latest version from the PowerShell Gallery, rather than using the Installer.</span></span> <span data-ttu-id="091e7-150">Actuellement, le programme d’installation ne prend pas en charge les cmdlets requises.</span><span class="sxs-lookup"><span data-stu-id="091e7-150">The Installer currently does not support the required cmdlets.</span></span>
  > 

 - <span data-ttu-id="091e7-151">Examinez les [conditions préalables](expressroute-prerequisites.md) et les [flux de travail](expressroute-workflows.md) avant de commencer la configuration.</span><span class="sxs-lookup"><span data-stu-id="091e7-151">Review the [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

 - <span data-ttu-id="091e7-152">Vous devez disposer d’un circuit ExpressRoute actif.</span><span class="sxs-lookup"><span data-stu-id="091e7-152">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="091e7-153">Suivez les instructions permettant de [créer un circuit ExpressRoute](expressroute-howto-circuit-arm.md) et faites-le activer par votre fournisseur de connectivité avant de poursuivre.</span><span class="sxs-lookup"><span data-stu-id="091e7-153">Follow the instructions to [Create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have the circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="091e7-154">Le circuit ExpressRoute doit être approvisionné et activé.</span><span class="sxs-lookup"><span data-stu-id="091e7-154">The ExpressRoute circuit must be in a provisioned and enabled state.</span></span>

 - <span data-ttu-id="091e7-155">Vous devez disposer d’une homologation Microsoft active.</span><span class="sxs-lookup"><span data-stu-id="091e7-155">You must have an active Microsoft peering.</span></span> <span data-ttu-id="091e7-156">Suivez les instructions de [création et modification de la configuration d’homologation](expressroute-circuit-peerings.md).</span><span class="sxs-lookup"><span data-stu-id="091e7-156">Follow instructions at [Create and modifying peering configuration](expressroute-circuit-peerings.md)</span></span>

### <a name="log-in-to-your-azure-account"></a><span data-ttu-id="091e7-157">Connexion à votre compte Azure</span><span class="sxs-lookup"><span data-stu-id="091e7-157">Log in to your Azure account</span></span>

<span data-ttu-id="091e7-158">Avant de commencer cette configuration, vous devez vous connecter à votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="091e7-158">Before beginning this configuration, you must log in to your Azure account.</span></span> <span data-ttu-id="091e7-159">Les applets de commande vous invitent à entrer les informations d’identification de connexion pour votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="091e7-159">The cmdlet prompts you for the login credentials for your Azure account.</span></span> <span data-ttu-id="091e7-160">Une fois que vous êtes connecté, l’applet de commande télécharge vos paramètres de compte pour qu’ils soient reconnus par Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="091e7-160">After logging in, it downloads your account settings so they are available to Azure PowerShell.</span></span>

<span data-ttu-id="091e7-161">Ouvrez la console PowerShell avec des privilèges élevés et connectez-vous à votre compte.</span><span class="sxs-lookup"><span data-stu-id="091e7-161">Open your PowerShell console with elevated privileges, and connect to your account.</span></span> <span data-ttu-id="091e7-162">Utilisez l’exemple suivant pour faciliter votre connexion :</span><span class="sxs-lookup"><span data-stu-id="091e7-162">Use the following example to help you connect:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="091e7-163">Si vous disposez de plusieurs abonnements Azure, vérifiez les abonnements associés au compte.</span><span class="sxs-lookup"><span data-stu-id="091e7-163">If you have multiple Azure subscriptions, check the subscriptions for the account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="091e7-164">Spécifiez l’abonnement que vous souhaitez utiliser.</span><span class="sxs-lookup"><span data-stu-id="091e7-164">Specify the subscription that you want to use.</span></span>

```powershell
Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
```

## <span data-ttu-id="091e7-165"><a name="prefixes"></a>Étape 1.</span><span class="sxs-lookup"><span data-stu-id="091e7-165"><a name="prefixes"></a>Step 1.</span></span> <span data-ttu-id="091e7-166">Obtenir la liste des préfixes et des valeurs de communauté BGP</span><span class="sxs-lookup"><span data-stu-id="091e7-166">Get a list of prefixes and BGP community values</span></span>

### <a name="1-get-a-list-of-bgp-community-values"></a><span data-ttu-id="091e7-167">1. Obtenir la liste des valeurs de communauté BGP</span><span class="sxs-lookup"><span data-stu-id="091e7-167">1. Get a list of BGP community values</span></span>

<span data-ttu-id="091e7-168">Pour obtenir la liste des valeurs de communauté BGP liées aux services accessibles par le biais de l’homologation Microsoft et la liste des préfixes associés, utilisez la cmdlet suivante :</span><span class="sxs-lookup"><span data-stu-id="091e7-168">Use the following cmdlet to get the list of BGP community values associated with services accessible through Microsoft peering, and the list of prefixes associated with them:</span></span>

```powershell
Get-AzureRmBgpServiceCommunity
```
### <a name="2-make-a-list-of-the-values-that-you-want-to-use"></a><span data-ttu-id="091e7-169">2. Dresser la liste des valeurs que vous souhaitez utiliser</span><span class="sxs-lookup"><span data-stu-id="091e7-169">2. Make a list of the values that you want to use</span></span>

<span data-ttu-id="091e7-170">Dressez la liste des valeurs de communauté BGP que vous souhaitez utiliser dans le filtre de routage.</span><span class="sxs-lookup"><span data-stu-id="091e7-170">Make a list of BGP community values you want to use in the route filter.</span></span> <span data-ttu-id="091e7-171">Par exemple, la valeur de communauté BGP pour les services Dynamics 365 est 12076:5040.</span><span class="sxs-lookup"><span data-stu-id="091e7-171">As an example, the BGP community value for Dynamics 365 services is 12076:5040.</span></span>

## <span data-ttu-id="091e7-172"><a name="filter"></a>Étape 2.</span><span class="sxs-lookup"><span data-stu-id="091e7-172"><a name="filter"></a>Step 2.</span></span> <span data-ttu-id="091e7-173">Créer un filtre de routage et une règle de filtre</span><span class="sxs-lookup"><span data-stu-id="091e7-173">Create a route filter and a filter rule</span></span>

<span data-ttu-id="091e7-174">Un filtre de routage ne peut avoir qu’une seule règle, et cette règle doit être de type « Autoriser ».</span><span class="sxs-lookup"><span data-stu-id="091e7-174">A route filter can have only one rule, and the rule must be of type 'Allow'.</span></span> <span data-ttu-id="091e7-175">Cette règle peut être associée à une liste des valeurs de communauté BGP.</span><span class="sxs-lookup"><span data-stu-id="091e7-175">This rule can have a list of BGP community values associated with it.</span></span>

### <a name="1-create-a-route-filter"></a><span data-ttu-id="091e7-176">1. Créer un filtre de routage</span><span class="sxs-lookup"><span data-stu-id="091e7-176">1. Create a route filter</span></span>

<span data-ttu-id="091e7-177">Commencez par créer le filtre de routage.</span><span class="sxs-lookup"><span data-stu-id="091e7-177">First, create the route filter.</span></span> <span data-ttu-id="091e7-178">La commande « New-AzureRmRouteFilter » crée uniquement une ressource de filtre de routage.</span><span class="sxs-lookup"><span data-stu-id="091e7-178">The command 'New-AzureRmRouteFilter' only creates a route filter resource.</span></span> <span data-ttu-id="091e7-179">Après avoir créé la ressource, vous devez créer une règle et la joindre à l’objet de filtre de routage.</span><span class="sxs-lookup"><span data-stu-id="091e7-179">After you create the resource, you must then create a rule and attach it to the route filter object.</span></span> <span data-ttu-id="091e7-180">Utilisez la commande suivante pour créer une ressource de filtre de routage :</span><span class="sxs-lookup"><span data-stu-id="091e7-180">Run the following command to create a route filter resource:</span></span>

```powershell
New-AzureRmRouteFilter -Name "MyRouteFilter" -ResourceGroupName "MyResourceGroup" -Location "West US"
```

### <a name="2-create-a-filter-rule"></a><span data-ttu-id="091e7-181">2. Créer une règle de filtre</span><span class="sxs-lookup"><span data-stu-id="091e7-181">2. Create a filter rule</span></span>

<span data-ttu-id="091e7-182">Vous pouvez spécifier un ensemble de communautés BGP sous forme de liste séparée par des virgules, comme dans l’exemple.</span><span class="sxs-lookup"><span data-stu-id="091e7-182">You can specify a set of BGP communities as a comma-separated list, as shown in the example.</span></span> <span data-ttu-id="091e7-183">Exécutez la commande suivante pour créer une règle :</span><span class="sxs-lookup"><span data-stu-id="091e7-183">Run the following command to create a new rule:</span></span>
 
```powershell
$rule = New-AzureRmRouteFilterRuleConfig -Name "Allow-EXO-D365" -Access Allow -RouteFilterRuleType Community -CommunityList "12076:5010,12076:5040"
```

### <a name="3-add-the-rule-to-the-route-filter"></a><span data-ttu-id="091e7-184">3. Ajouter la règle au filtre de routage</span><span class="sxs-lookup"><span data-stu-id="091e7-184">3. Add the rule to the route filter</span></span>

<span data-ttu-id="091e7-185">Exécutez la commande suivante pour ajouter la règle de routage au groupe de routage :</span><span class="sxs-lookup"><span data-stu-id="091e7-185">Run the following command to add the filter rule to the route filter:</span></span>
 
```powershell
$routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
$routefilter.Rules.Add($rule)
Set-AzureRmRouteFilter -RouteFilter $routefilter
```

## <span data-ttu-id="091e7-186"><a name="attach"></a>Étape 3.</span><span class="sxs-lookup"><span data-stu-id="091e7-186"><a name="attach"></a>Step 3.</span></span> <span data-ttu-id="091e7-187">Joindre le filtre de routage à un circuit ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="091e7-187">Attach the route filter to an ExpressRoute circuit</span></span>

<span data-ttu-id="091e7-188">Exécutez la commande suivante pour joindre le filtre de routage au circuit ExpressRoute, en admettant que vous n’avez que l’homologation Microsoft :</span><span class="sxs-lookup"><span data-stu-id="091e7-188">Run the following command to attach the route filter to the ExpressRoute circuit, assuming you have only Microsoft peering:</span></span>

```powershell
$ckt.Peerings[0].RouteFilter = $routefilter 
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <span data-ttu-id="091e7-189"><a name="getproperties"></a>Obtenir les propriétés d’un filtre de routage</span><span class="sxs-lookup"><span data-stu-id="091e7-189"><a name="getproperties"></a>To get the properties of a route filter</span></span>

<span data-ttu-id="091e7-190">Pour obtenir les propriétés d’un filtre de routage, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="091e7-190">To get the properties of a route filter, use the following steps:</span></span>

1. <span data-ttu-id="091e7-191">Utilisez la commande suivante pour obtenir la ressource de filtre de routage :</span><span class="sxs-lookup"><span data-stu-id="091e7-191">Run the following command to get the route filter resource:</span></span>

  ```powershell
  $routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
  ```
2. <span data-ttu-id="091e7-192">Obtenez les règles de filtre de routage pour la ressource de filtre de routage en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="091e7-192">Get the route filter rules for the route-filter resource by running the following command:</span></span>

  ```powershell
  $routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
  $rule = $routefilter.Rules[0]
  ```

## <span data-ttu-id="091e7-193"><a name="updateproperties"></a>Mettre à jour les propriétés d’un filtre de routage</span><span class="sxs-lookup"><span data-stu-id="091e7-193"><a name="updateproperties"></a>To update the properties of a route filter</span></span>

<span data-ttu-id="091e7-194">Si le filtre de routage est déjà joint à un circuit, les mises à jour de la liste de communautés BGP propagent automatiquement les modifications de publication de préfixe appropriées via les sessions BGP établies.</span><span class="sxs-lookup"><span data-stu-id="091e7-194">If the route filter is already attached to a circuit, updates to the BGP community list automatically propagates appropriate prefix advertisement changes through the established BGP sessions.</span></span> <span data-ttu-id="091e7-195">Vous pouvez mettre à jour la liste de communautés BGP de votre filtre de routage à l’aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="091e7-195">You can update the BGP community list of your route filter using the following command:</span></span>

```powershell
$routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
$routefilter.rules[0].Communities = "12076:5030", "12076:5040"
Set-AzureRmRouteFilter -RouteFilter $routefilter
```

## <span data-ttu-id="091e7-196"><a name="detach"></a>Détacher un filtre de routage d’un circuit ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="091e7-196"><a name="detach"></a>To detach a route filter from an ExpressRoute circuit</span></span>

<span data-ttu-id="091e7-197">Une fois qu’un filtre de routage est détaché du circuit ExpressRoute, aucun préfixe n’est publié via la session BGP.</span><span class="sxs-lookup"><span data-stu-id="091e7-197">Once a route filter is detached from the ExpressRoute circuit, no prefixes are advertised through the BGP session.</span></span> <span data-ttu-id="091e7-198">Vous pouvez détacher un filtre de routage d’un circuit ExpressRoute à l’aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="091e7-198">You can detach a route filter from an ExpressRoute circuit using the following command:</span></span>
  
```powershell
$ckt.Peerings[0].RouteFilter = $null
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <span data-ttu-id="091e7-199"><a name="delete"></a>Supprimer un filtre de routage</span><span class="sxs-lookup"><span data-stu-id="091e7-199"><a name="delete"></a>To delete a route filter</span></span>

<span data-ttu-id="091e7-200">Vous ne pouvez supprimer un filtre de routage que s’il n’est attaché à aucun circuit.</span><span class="sxs-lookup"><span data-stu-id="091e7-200">You can only delete a route filter if it is not attached to any circuit.</span></span> <span data-ttu-id="091e7-201">Assurez-vous que le filtre de routage n’est pas attaché à un circuit avant de tenter de le supprimer.</span><span class="sxs-lookup"><span data-stu-id="091e7-201">Ensure that the route filter is not attached to any circuit before attempting to delete it.</span></span> <span data-ttu-id="091e7-202">Vous pouvez supprimer un filtre de routage à l’aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="091e7-202">You can delete a route filter using the following command:</span></span>

```powershell
Remove-AzureRmRouteFilter -Name "MyRouteFilter" -ResourceGroupName "MyResourceGroup"
```

## <a name="next-steps"></a><span data-ttu-id="091e7-203">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="091e7-203">Next steps</span></span>

<span data-ttu-id="091e7-204">Pour plus d'informations sur ExpressRoute, consultez le [FAQ sur ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="091e7-204">For more information about ExpressRoute, see the [ExpressRoute FAQ](expressroute-faqs.md).</span></span>