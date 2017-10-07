---
title: "Configurer des filtres de routage pour l’homologation d’Azure ExpressRoute Microsoft : PowerShell | Microsoft Docs"
description: "Cet article décrit comment tooconfigure itinéraire filtres pour Peering Microsoft à l’aide de PowerShell"
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
ms.openlocfilehash: 395bcf7d6ad43c643ff041b154f8e4b797083e7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-route-filters-for-microsoft-peering"></a><span data-ttu-id="a9dba-103">Configurer des filtres de routage pour l’homologation Microsoft</span><span class="sxs-lookup"><span data-stu-id="a9dba-103">Configure route filters for Microsoft peering</span></span>

<span data-ttu-id="a9dba-104">Filtres de routage sont un moyen de tooconsume un sous-ensemble de services pris en charge via l’homologation Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a9dba-104">Route filters are a way tooconsume a subset of supported services through Microsoft peering.</span></span> <span data-ttu-id="a9dba-105">les étapes dans cette article vous aident à configurez et gérez des filtres de routage pour les circuits ExpressRoute Hello.</span><span class="sxs-lookup"><span data-stu-id="a9dba-105">hello steps in this article help you configure and manage route filters for ExpressRoute circuits.</span></span>

<span data-ttu-id="a9dba-106">Dynamics 365 services et les services Office 365 comme Exchange Online, SharePoint Online et Skype pour entreprises, sont accessibles via l’homologation de Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="a9dba-106">Dynamics 365 services, and Office 365 services such as Exchange Online, SharePoint Online, and Skype for Business, are accessible through hello Microsoft peering.</span></span> <span data-ttu-id="a9dba-107">Lors de l’homologation Microsoft est configuré dans un circuit ExpressRoute, tous les services connexes toothese de préfixes sont publiés via des sessions BGP hello établies.</span><span class="sxs-lookup"><span data-stu-id="a9dba-107">When Microsoft peering is configured in an ExpressRoute circuit, all prefixes related toothese services are advertised through hello BGP sessions that are established.</span></span> <span data-ttu-id="a9dba-108">Une BGP Communauté valeur est attaché tooevery préfixe tooidentify hello du service qui vous est proposé via le préfixe de hello.</span><span class="sxs-lookup"><span data-stu-id="a9dba-108">A BGP community value is attached tooevery prefix tooidentify hello service that is offered through hello prefix.</span></span> <span data-ttu-id="a9dba-109">Pour obtenir la liste des valeurs de communauté BGP hello et services hello auxquels elles sont mappées à, consultez [les Communautés BGP](expressroute-routing.md#bgp).</span><span class="sxs-lookup"><span data-stu-id="a9dba-109">For a list of hello BGP community values and hello services they  map to, see [BGP communities](expressroute-routing.md#bgp).</span></span>

<span data-ttu-id="a9dba-110">Si vous avez besoin des services de connectivité de tooall, un grand nombre de préfixes est publié via BGP.</span><span class="sxs-lookup"><span data-stu-id="a9dba-110">If you require connectivity tooall services, a large number of prefixes are advertised through BGP.</span></span> <span data-ttu-id="a9dba-111">Cela augmente considérablement la taille de hello hello de tables d’itinéraires gérées par les routeurs au sein de votre réseau.</span><span class="sxs-lookup"><span data-stu-id="a9dba-111">This significantly increases hello size of hello route tables maintained by routers within your network.</span></span> <span data-ttu-id="a9dba-112">Si vous envisagez tooconsume uniquement un sous-ensemble des services offerts via l’homologation Microsoft, vous pouvez réduire la taille hello de vos tables d’itinéraires de deux manières.</span><span class="sxs-lookup"><span data-stu-id="a9dba-112">If you plan tooconsume only a subset of services offered through Microsoft peering, you can reduce hello size of your route tables in two ways.</span></span> <span data-ttu-id="a9dba-113">Vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="a9dba-113">You can:</span></span>

- <span data-ttu-id="a9dba-114">Filtrer les préfixes indésirables en appliquant des filtres de routage sur les communautés BGP.</span><span class="sxs-lookup"><span data-stu-id="a9dba-114">Filter out unwanted prefixes by applying route filters on BGP communities.</span></span> <span data-ttu-id="a9dba-115">Ceci est une pratique standard et très courante de mise en réseau.</span><span class="sxs-lookup"><span data-stu-id="a9dba-115">This is a standard networking practice and is used commonly within many networks.</span></span>

- <span data-ttu-id="a9dba-116">Définir des filtres de routage et de les appliquer de circuit ExpressRoute de tooyour.</span><span class="sxs-lookup"><span data-stu-id="a9dba-116">Define route filters and apply them tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="a9dba-117">Un filtre d’itinéraire est une ressource que vous permet de sélectionner la liste hello des services que vous prévoyez tooconsume via l’homologation Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a9dba-117">A route filter is a new resource that lets you select hello list of services you plan tooconsume through Microsoft peering.</span></span> <span data-ttu-id="a9dba-118">ExpressRoute les routeurs n’envoient liste hello de préfixes qui font partie des services de toohello identifiés dans le filtre de routage hello.</span><span class="sxs-lookup"><span data-stu-id="a9dba-118">ExpressRoute routers only send hello list of prefixes that belong toohello services identified in hello route filter.</span></span>

### <span data-ttu-id="a9dba-119"><a name="about"></a>À propos des filtres de routage</span><span class="sxs-lookup"><span data-stu-id="a9dba-119"><a name="about"></a>About route filters</span></span>

<span data-ttu-id="a9dba-120">Lors de l’homologation Microsoft est configuré sur votre circuit ExpressRoute, routeurs de bord Microsoft hello établissent une paire de sessions BGP avec les routeurs de périphérie hello (la vôtre ou votre fournisseur de connectivité).</span><span class="sxs-lookup"><span data-stu-id="a9dba-120">When Microsoft peering is configured on your ExpressRoute circuit, hello Microsoft edge routers establish a pair of BGP sessions with hello edge routers (yours or your connectivity provider's).</span></span> <span data-ttu-id="a9dba-121">Aucun itinéraire n’est publiés tooyour réseau.</span><span class="sxs-lookup"><span data-stu-id="a9dba-121">No routes are advertised tooyour network.</span></span> <span data-ttu-id="a9dba-122">réseau de tooyour tooenable itinéraire publications, vous devez associer un filtre de routage.</span><span class="sxs-lookup"><span data-stu-id="a9dba-122">tooenable route advertisements tooyour network, you must associate a route filter.</span></span>

<span data-ttu-id="a9dba-123">Un filtre de routage vous permet d’identifier les services auxquels vous souhaitez tooconsume via votre circuit ExpressRoute homologation de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a9dba-123">A route filter lets you identify services you want tooconsume through your ExpressRoute circuit's Microsoft peering.</span></span> <span data-ttu-id="a9dba-124">Il est essentiellement une liste blanche de toutes les valeurs de communauté hello BGP.</span><span class="sxs-lookup"><span data-stu-id="a9dba-124">It is essentially a white list of all hello BGP community values.</span></span> <span data-ttu-id="a9dba-125">Une fois qu’une ressource de filtre d’itinéraire est définie et attaché tooan circuit ExpressRoute, tous les préfixes qui mappent les valeurs de communauté toohello BGP sont publiés tooyour réseau.</span><span class="sxs-lookup"><span data-stu-id="a9dba-125">Once a route filter resource is defined and attached tooan ExpressRoute circuit, all prefixes that map toohello BGP community values are advertised tooyour network.</span></span>

<span data-ttu-id="a9dba-126">toobe tooattach en mesure des filtres de routage avec les services Office 365, vous devez disposer de services d’Office 365 tooconsume d’autorisation via ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="a9dba-126">toobe able tooattach route filters with Office 365 services on them, you must have authorization tooconsume Office 365 services through ExpressRoute.</span></span> <span data-ttu-id="a9dba-127">Si vous n’êtes pas autorisé tooconsume Office 365 des services via ExpressRoute, filtres de routage tooattach hello opération échoue.</span><span class="sxs-lookup"><span data-stu-id="a9dba-127">If you are not authorized tooconsume Office 365 services through ExpressRoute, hello operation tooattach route filters fails.</span></span> <span data-ttu-id="a9dba-128">Pour plus d’informations sur le processus d’autorisation de hello, consultez [Azure ExpressRoute pour Office 365](https://support.office.com/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd).</span><span class="sxs-lookup"><span data-stu-id="a9dba-128">For more information about hello authorization process, see [Azure ExpressRoute for Office 365](https://support.office.com/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd).</span></span> <span data-ttu-id="a9dba-129">Services de connectivité de 365 tooDynamics ne nécessite pas l’autorisation préalable.</span><span class="sxs-lookup"><span data-stu-id="a9dba-129">Connectivity tooDynamics 365 services does NOT require any prior authorization.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a9dba-130">Homologation Microsoft des circuits ExpressRoute qui ont été configurés préalable tooAugust 1, 2017 aura tous les préfixes de service publiés via l’homologation Microsoft, même si les filtres de routage ne sont pas définis.</span><span class="sxs-lookup"><span data-stu-id="a9dba-130">Microsoft peering of ExpressRoute circuits that were configured prior tooAugust 1, 2017 will have all service prefixes advertised through Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="a9dba-131">Homologation Microsoft des circuits ExpressRoute qui sont configurés sur ou après le 1er août 2017 n’aura pas de préfixes publiés jusqu'à ce qu’un filtre de routage est attaché toohello circuit.</span><span class="sxs-lookup"><span data-stu-id="a9dba-131">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached toohello circuit.</span></span>
> 
> 

### <span data-ttu-id="a9dba-132"><a name="workflow"></a>Flux de travail</span><span class="sxs-lookup"><span data-stu-id="a9dba-132"><a name="workflow"></a>Workflow</span></span>

<span data-ttu-id="a9dba-133">toobe les toosuccessfully en mesure de se connecter à tooservices via l’homologation Microsoft, vous devez effectuer les hello configuration comme suit :</span><span class="sxs-lookup"><span data-stu-id="a9dba-133">toobe able toosuccessfully connect tooservices through Microsoft peering, you must complete hello following configuration steps:</span></span>

- <span data-ttu-id="a9dba-134">Vous devez disposer d’un circuit ExpressRoute actif où l’homologation Microsoft est approvisionnée.</span><span class="sxs-lookup"><span data-stu-id="a9dba-134">You must have an active ExpressRoute circuit that has Microsoft peering provisioned.</span></span> <span data-ttu-id="a9dba-135">Vous pouvez utiliser hello suivant les instructions tooaccomplish ces tâches :</span><span class="sxs-lookup"><span data-stu-id="a9dba-135">You can use hello following instructions tooaccomplish these tasks:</span></span>
  - <span data-ttu-id="a9dba-136">[Créer un circuit ExpressRoute](expressroute-howto-circuit-arm.md) et circuit hello activé par votre fournisseur de connectivité avant de continuer.</span><span class="sxs-lookup"><span data-stu-id="a9dba-136">[Create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have hello circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="a9dba-137">Hello circuit ExpressRoute doit être dans un état configuré et activé.</span><span class="sxs-lookup"><span data-stu-id="a9dba-137">hello ExpressRoute circuit must be in a provisioned and enabled state.</span></span>
  - <span data-ttu-id="a9dba-138">[Créer l’homologation Microsoft](expressroute-circuit-peerings.md) si vous gérez la session BGP hello directement.</span><span class="sxs-lookup"><span data-stu-id="a9dba-138">[Create Microsoft peering](expressroute-circuit-peerings.md) if you manage hello BGP session directly.</span></span> <span data-ttu-id="a9dba-139">Sinon, demandez à votre fournisseur de connectivité de configurer l’homologation Microsoft pour votre circuit.</span><span class="sxs-lookup"><span data-stu-id="a9dba-139">Or, have your connectivity provider provision Microsoft peering for your circuit.</span></span>

-  <span data-ttu-id="a9dba-140">Vous devez créer et configurer un filtre de routage.</span><span class="sxs-lookup"><span data-stu-id="a9dba-140">You must create and configure a route filter.</span></span>
    - <span data-ttu-id="a9dba-141">Identifier hello services vous avec tooconsume via l’homologation Microsoft</span><span class="sxs-lookup"><span data-stu-id="a9dba-141">Identify hello services you with tooconsume through Microsoft peering</span></span>
    - <span data-ttu-id="a9dba-142">Identifier la liste des valeurs de communauté BGP associés aux services de hello de hello</span><span class="sxs-lookup"><span data-stu-id="a9dba-142">Identify hello list of BGP community values associated with hello services</span></span>
    - <span data-ttu-id="a9dba-143">Créer une règle tooallow hello préfixe liste correspondance hello valeurs de communauté BGP</span><span class="sxs-lookup"><span data-stu-id="a9dba-143">Create a rule tooallow hello prefix list matching hello BGP community values</span></span>

-  <span data-ttu-id="a9dba-144">Vous devez joindre le circuit ExpressRoute toohello hello itinéraire filtre.</span><span class="sxs-lookup"><span data-stu-id="a9dba-144">You must attach hello route filter toohello ExpressRoute circuit.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="a9dba-145">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="a9dba-145">Before you begin</span></span>

<span data-ttu-id="a9dba-146">Avant de commencer la configuration, assurez-vous que vous remplissez hello suivant des critères :</span><span class="sxs-lookup"><span data-stu-id="a9dba-146">Before you begin configuration, make sure you meet hello following criteria:</span></span>

 - <span data-ttu-id="a9dba-147">Installer la version la plus récente hello Hello applets de commande PowerShell de gestionnaire de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="a9dba-147">Install hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="a9dba-148">Pour plus d’informations, voir [Installer et configurer Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="a9dba-148">For more information, see [Install and configure Azure PowerShelll](/powershell/azure/install-azurerm-ps).</span></span>

  > [!NOTE]
  > <span data-ttu-id="a9dba-149">Téléchargez hello dernière version à partir de hello PowerShell Gallery, au lieu d’utiliser hello programme d’installation.</span><span class="sxs-lookup"><span data-stu-id="a9dba-149">Download hello latest version from hello PowerShell Gallery, rather than using hello Installer.</span></span> <span data-ttu-id="a9dba-150">actuellement Hello programme d’installation ne prend pas en charge les applets de commande hello requis.</span><span class="sxs-lookup"><span data-stu-id="a9dba-150">hello Installer currently does not support hello required cmdlets.</span></span>
  > 

 - <span data-ttu-id="a9dba-151">Hello de révision [conditions préalables](expressroute-prerequisites.md) et [workflows](expressroute-workflows.md) avant de commencer la configuration.</span><span class="sxs-lookup"><span data-stu-id="a9dba-151">Review hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

 - <span data-ttu-id="a9dba-152">Vous devez disposer d’un circuit ExpressRoute actif.</span><span class="sxs-lookup"><span data-stu-id="a9dba-152">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="a9dba-153">Suivez les instructions de hello trop[créer un circuit ExpressRoute](expressroute-howto-circuit-arm.md) et circuit hello activé par votre fournisseur de connectivité avant de continuer.</span><span class="sxs-lookup"><span data-stu-id="a9dba-153">Follow hello instructions too[Create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have hello circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="a9dba-154">Hello circuit ExpressRoute doit être dans un état configuré et activé.</span><span class="sxs-lookup"><span data-stu-id="a9dba-154">hello ExpressRoute circuit must be in a provisioned and enabled state.</span></span>

 - <span data-ttu-id="a9dba-155">Vous devez disposer d’une homologation Microsoft active.</span><span class="sxs-lookup"><span data-stu-id="a9dba-155">You must have an active Microsoft peering.</span></span> <span data-ttu-id="a9dba-156">Suivez les instructions de [création et modification de la configuration d’homologation](expressroute-circuit-peerings.md).</span><span class="sxs-lookup"><span data-stu-id="a9dba-156">Follow instructions at [Create and modifying peering configuration](expressroute-circuit-peerings.md)</span></span>

### <a name="log-in-tooyour-azure-account"></a><span data-ttu-id="a9dba-157">Ouvrez une session dans tooyour compte Azure</span><span class="sxs-lookup"><span data-stu-id="a9dba-157">Log in tooyour Azure account</span></span>

<span data-ttu-id="a9dba-158">Avant de commencer cette configuration, vous devez vous connecter tooyour compte Azure.</span><span class="sxs-lookup"><span data-stu-id="a9dba-158">Before beginning this configuration, you must log in tooyour Azure account.</span></span> <span data-ttu-id="a9dba-159">applet de commande Hello vous demande des informations d’identification de connexion hello pour votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="a9dba-159">hello cmdlet prompts you for hello login credentials for your Azure account.</span></span> <span data-ttu-id="a9dba-160">Une fois connecté, il télécharge les paramètres de votre compte afin qu’ils soient disponible tooAzure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a9dba-160">After logging in, it downloads your account settings so they are available tooAzure PowerShell.</span></span>

<span data-ttu-id="a9dba-161">Ouvrez la console PowerShell avec des privilèges élevés et tooyour compte de connexion.</span><span class="sxs-lookup"><span data-stu-id="a9dba-161">Open your PowerShell console with elevated privileges, and connect tooyour account.</span></span> <span data-ttu-id="a9dba-162">Utilisez hello suivant toohelp exemple que vous connectez :</span><span class="sxs-lookup"><span data-stu-id="a9dba-162">Use hello following example toohelp you connect:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="a9dba-163">Si vous avez plusieurs abonnements Azure, vérifiez les abonnements hello pour le compte de hello.</span><span class="sxs-lookup"><span data-stu-id="a9dba-163">If you have multiple Azure subscriptions, check hello subscriptions for hello account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="a9dba-164">Spécifiez un abonnement hello que vous souhaitez toouse.</span><span class="sxs-lookup"><span data-stu-id="a9dba-164">Specify hello subscription that you want toouse.</span></span>

```powershell
Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
```

## <span data-ttu-id="a9dba-165"><a name="prefixes"></a>Étape 1.</span><span class="sxs-lookup"><span data-stu-id="a9dba-165"><a name="prefixes"></a>Step 1.</span></span> <span data-ttu-id="a9dba-166">Obtenir la liste des préfixes et des valeurs de communauté BGP</span><span class="sxs-lookup"><span data-stu-id="a9dba-166">Get a list of prefixes and BGP community values</span></span>

### <a name="1-get-a-list-of-bgp-community-values"></a><span data-ttu-id="a9dba-167">1. Obtenir la liste des valeurs de communauté BGP</span><span class="sxs-lookup"><span data-stu-id="a9dba-167">1. Get a list of BGP community values</span></span>

<span data-ttu-id="a9dba-168">Utilisez hello suivant applet de commande tooget hello liste de valeurs de communauté BGP associés aux services accessibles via l’homologation Microsoft et hello liste des préfixes associés :</span><span class="sxs-lookup"><span data-stu-id="a9dba-168">Use hello following cmdlet tooget hello list of BGP community values associated with services accessible through Microsoft peering, and hello list of prefixes associated with them:</span></span>

```powershell
Get-AzureRmBgpServiceCommunity
```
### <a name="2-make-a-list-of-hello-values-that-you-want-toouse"></a><span data-ttu-id="a9dba-169">2. Dressez la liste des valeurs de hello que vous souhaitez toouse</span><span class="sxs-lookup"><span data-stu-id="a9dba-169">2. Make a list of hello values that you want toouse</span></span>

<span data-ttu-id="a9dba-170">Dressez la liste des valeurs de communauté BGP souhaité toouse dans un filtre d’itinéraire hello.</span><span class="sxs-lookup"><span data-stu-id="a9dba-170">Make a list of BGP community values you want toouse in hello route filter.</span></span> <span data-ttu-id="a9dba-171">Par exemple, hello valeur communautaire BGP pour les services de Dynamics 365 est 12076:5040.</span><span class="sxs-lookup"><span data-stu-id="a9dba-171">As an example, hello BGP community value for Dynamics 365 services is 12076:5040.</span></span>

## <span data-ttu-id="a9dba-172"><a name="filter"></a>Étape 2.</span><span class="sxs-lookup"><span data-stu-id="a9dba-172"><a name="filter"></a>Step 2.</span></span> <span data-ttu-id="a9dba-173">Créer un filtre de routage et une règle de filtre</span><span class="sxs-lookup"><span data-stu-id="a9dba-173">Create a route filter and a filter rule</span></span>

<span data-ttu-id="a9dba-174">Un filtre de routage peut avoir qu’une seule règle, et la règle de hello doit être de type « Autoriser ».</span><span class="sxs-lookup"><span data-stu-id="a9dba-174">A route filter can have only one rule, and hello rule must be of type 'Allow'.</span></span> <span data-ttu-id="a9dba-175">Cette règle peut être associée à une liste des valeurs de communauté BGP.</span><span class="sxs-lookup"><span data-stu-id="a9dba-175">This rule can have a list of BGP community values associated with it.</span></span>

### <a name="1-create-a-route-filter"></a><span data-ttu-id="a9dba-176">1. Créer un filtre de routage</span><span class="sxs-lookup"><span data-stu-id="a9dba-176">1. Create a route filter</span></span>

<span data-ttu-id="a9dba-177">Commencez par créer un filtre d’itinéraire hello.</span><span class="sxs-lookup"><span data-stu-id="a9dba-177">First, create hello route filter.</span></span> <span data-ttu-id="a9dba-178">commande de Hello 'New-AzureRmRouteFilter' crée uniquement une ressource de filtre d’itinéraire.</span><span class="sxs-lookup"><span data-stu-id="a9dba-178">hello command 'New-AzureRmRouteFilter' only creates a route filter resource.</span></span> <span data-ttu-id="a9dba-179">Après avoir créé la ressource de hello, vous devez ensuite créer une règle et attachez-le toohello objet filter à itinéraire.</span><span class="sxs-lookup"><span data-stu-id="a9dba-179">After you create hello resource, you must then create a rule and attach it toohello route filter object.</span></span> <span data-ttu-id="a9dba-180">Exécutez hello suivant commande toocreate une ressource de filtre de routage :</span><span class="sxs-lookup"><span data-stu-id="a9dba-180">Run hello following command toocreate a route filter resource:</span></span>

```powershell
New-AzureRmRouteFilter -Name "MyRouteFilter" -ResourceGroupName "MyResourceGroup" -Location "West US"
```

### <a name="2-create-a-filter-rule"></a><span data-ttu-id="a9dba-181">2. Créer une règle de filtre</span><span class="sxs-lookup"><span data-stu-id="a9dba-181">2. Create a filter rule</span></span>

<span data-ttu-id="a9dba-182">Vous pouvez spécifier un ensemble de communautés BGP sous forme de liste séparée par des virgules, comme indiqué dans l’exemple de hello.</span><span class="sxs-lookup"><span data-stu-id="a9dba-182">You can specify a set of BGP communities as a comma-separated list, as shown in hello example.</span></span> <span data-ttu-id="a9dba-183">Exécutez hello suivant commande toocreate une nouvelle règle :</span><span class="sxs-lookup"><span data-stu-id="a9dba-183">Run hello following command toocreate a new rule:</span></span>
 
```powershell
$rule = New-AzureRmRouteFilterRuleConfig -Name "Allow-EXO-D365" -Access Allow -RouteFilterRuleType Community -CommunityList "12076:5010,12076:5040"
```

### <a name="3-add-hello-rule-toohello-route-filter"></a><span data-ttu-id="a9dba-184">3. Ajouter un filtre d’itinéraire hello règle toohello</span><span class="sxs-lookup"><span data-stu-id="a9dba-184">3. Add hello rule toohello route filter</span></span>

<span data-ttu-id="a9dba-185">Exécutez hello suivant filtre de routage toohello règle de filtre de commande tooadd hello :</span><span class="sxs-lookup"><span data-stu-id="a9dba-185">Run hello following command tooadd hello filter rule toohello route filter:</span></span>
 
```powershell
$routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
$routefilter.Rules.Add($rule)
Set-AzureRmRouteFilter -RouteFilter $routefilter
```

## <span data-ttu-id="a9dba-186"><a name="attach"></a>Étape 3.</span><span class="sxs-lookup"><span data-stu-id="a9dba-186"><a name="attach"></a>Step 3.</span></span> <span data-ttu-id="a9dba-187">Attacher le circuit ExpressRoute tooan hello itinéraire filtre</span><span class="sxs-lookup"><span data-stu-id="a9dba-187">Attach hello route filter tooan ExpressRoute circuit</span></span>

<span data-ttu-id="a9dba-188">Exécutez hello suivant commande tooattach hello itinéraire filtre toohello circuit ExpressRoute, en supposant que vous disposez uniquement d’homologation de Microsoft :</span><span class="sxs-lookup"><span data-stu-id="a9dba-188">Run hello following command tooattach hello route filter toohello ExpressRoute circuit, assuming you have only Microsoft peering:</span></span>

```powershell
$ckt.Peerings[0].RouteFilter = $routefilter 
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <span data-ttu-id="a9dba-189"><a name="getproperties"></a>propriétés de hello tooget d’un filtre de routage</span><span class="sxs-lookup"><span data-stu-id="a9dba-189"><a name="getproperties"></a>tooget hello properties of a route filter</span></span>

<span data-ttu-id="a9dba-190">propriétés de hello tooget d’un filtre de routage, utilisez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="a9dba-190">tooget hello properties of a route filter, use hello following steps:</span></span>

1. <span data-ttu-id="a9dba-191">Exécutez hello suivant la ressource de filtre de l’itinéraire de commande tooget hello :</span><span class="sxs-lookup"><span data-stu-id="a9dba-191">Run hello following command tooget hello route filter resource:</span></span>

  ```powershell
  $routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
  ```
2. <span data-ttu-id="a9dba-192">Obtenir des règles de filtre de routage hello pour la ressource de filtre de routage hello en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="a9dba-192">Get hello route filter rules for hello route-filter resource by running hello following command:</span></span>

  ```powershell
  $routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
  $rule = $routefilter.Rules[0]
  ```

## <span data-ttu-id="a9dba-193"><a name="updateproperties"></a>propriétés de hello tooupdate d’un filtre de routage</span><span class="sxs-lookup"><span data-stu-id="a9dba-193"><a name="updateproperties"></a>tooupdate hello properties of a route filter</span></span>

<span data-ttu-id="a9dba-194">Si le filtre de routage hello est déjà attaché liste communautaire de mises à jour toohello BGP, un circuit tooa propage automatiquement les modifications de publication de préfixe approprié via des sessions BGP hello établie.</span><span class="sxs-lookup"><span data-stu-id="a9dba-194">If hello route filter is already attached tooa circuit, updates toohello BGP community list automatically propagates appropriate prefix advertisement changes through hello established BGP sessions.</span></span> <span data-ttu-id="a9dba-195">Vous pouvez mettre à jour de liste de communauté BGP hello de votre filtre de routage à l’aide de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="a9dba-195">You can update hello BGP community list of your route filter using hello following command:</span></span>

```powershell
$routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
$routefilter.rules[0].Communities = "12076:5030", "12076:5040"
Set-AzureRmRouteFilter -RouteFilter $routefilter
```

## <span data-ttu-id="a9dba-196"><a name="detach"></a>toodetach un filtre d’itinéraire à partir d’un circuit ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="a9dba-196"><a name="detach"></a>toodetach a route filter from an ExpressRoute circuit</span></span>

<span data-ttu-id="a9dba-197">Une fois qu’un filtre de routage est détaché de hello circuit ExpressRoute, aucuns préfixes ne sont publiés via la session BGP de hello.</span><span class="sxs-lookup"><span data-stu-id="a9dba-197">Once a route filter is detached from hello ExpressRoute circuit, no prefixes are advertised through hello BGP session.</span></span> <span data-ttu-id="a9dba-198">Vous pouvez détacher un filtre d’itinéraire à partir d’un circuit ExpressRoute à l’aide de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="a9dba-198">You can detach a route filter from an ExpressRoute circuit using hello following command:</span></span>
  
```powershell
$ckt.Peerings[0].RouteFilter = $null
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <span data-ttu-id="a9dba-199"><a name="delete"></a>toodelete un filtre de routage</span><span class="sxs-lookup"><span data-stu-id="a9dba-199"><a name="delete"></a>toodelete a route filter</span></span>

<span data-ttu-id="a9dba-200">Vous pouvez uniquement supprimer un filtre d’itinéraire si elle n’est pas attaché tooany circuit.</span><span class="sxs-lookup"><span data-stu-id="a9dba-200">You can only delete a route filter if it is not attached tooany circuit.</span></span> <span data-ttu-id="a9dba-201">Vérifiez que le filtre hello itinéraire n’est pas attaché tooany circuit avant de tenter de toodelete il.</span><span class="sxs-lookup"><span data-stu-id="a9dba-201">Ensure that hello route filter is not attached tooany circuit before attempting toodelete it.</span></span> <span data-ttu-id="a9dba-202">Vous pouvez supprimer un filtre de routage à l’aide de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="a9dba-202">You can delete a route filter using hello following command:</span></span>

```powershell
Remove-AzureRmRouteFilter -Name "MyRouteFilter" -ResourceGroupName "MyResourceGroup"
```

## <a name="next-steps"></a><span data-ttu-id="a9dba-203">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a9dba-203">Next steps</span></span>

<span data-ttu-id="a9dba-204">Pour plus d’informations sur ExpressRoute, consultez hello [FAQ sur ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="a9dba-204">For more information about ExpressRoute, see hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>
