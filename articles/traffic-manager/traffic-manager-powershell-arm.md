---
title: aaaUsing PowerShell toomanage Traffic Manager dans Azure | Documents Microsoft
description: Utilisation de Powershell pour Traffic Manager avec Azure Resource Manager
services: traffic-manager
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: bc247448-1d2e-4104-ac03-42b59ebde065
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/16/2017
ms.author: kumud
ms.openlocfilehash: 018c37db63beb82fdad54cfd7e13ab3cb645723a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-powershell-toomanage-traffic-manager"></a><span data-ttu-id="2b22f-103">À l’aide de PowerShell toomanage Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="2b22f-103">Using PowerShell toomanage Traffic Manager</span></span>

<span data-ttu-id="2b22f-104">Le Gestionnaire de ressources Azure est l’interface de gestion préférés hello pour les services dans Azure.</span><span class="sxs-lookup"><span data-stu-id="2b22f-104">Azure Resource Manager is hello preferred management interface for services in Azure.</span></span> <span data-ttu-id="2b22f-105">Les outils et API d’Azure Resource Manager permettent de gérer les profils Azure Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="2b22f-105">Azure Traffic Manager profiles can be managed using Azure Resource Manager-based APIs and tools.</span></span>

## <a name="resource-model"></a><span data-ttu-id="2b22f-106">Modèle de ressource</span><span class="sxs-lookup"><span data-stu-id="2b22f-106">Resource model</span></span>

<span data-ttu-id="2b22f-107">Azure Traffic Manager est configuré à l'aide d'un ensemble de paramètres appelé profil Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="2b22f-107">Azure Traffic Manager is configured using a collection of settings called a Traffic Manager profile.</span></span> <span data-ttu-id="2b22f-108">Ce profil contient les paramètres DNS, les paramètres de routage du trafic, les paramètres de surveillance de point de terminaison, et une liste de trafic de toowhich de points de terminaison de service est routée.</span><span class="sxs-lookup"><span data-stu-id="2b22f-108">This profile contains DNS settings, traffic routing settings, endpoint monitoring settings, and a list of service endpoints toowhich traffic is routed.</span></span>

<span data-ttu-id="2b22f-109">Chaque profil Traffic Manager est représenté par une ressource de type « TrafficManagerProfiles ».</span><span class="sxs-lookup"><span data-stu-id="2b22f-109">Each Traffic Manager profile is represented by a resource of type 'TrafficManagerProfiles'.</span></span> <span data-ttu-id="2b22f-110">Au niveau de l’API REST de hello, hello URI pour chaque profil est la suivante :</span><span class="sxs-lookup"><span data-stu-id="2b22f-110">At hello REST API level, hello URI for each profile is as follows:</span></span>

    https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Network/trafficManagerProfiles/{profile-name}?api-version={api-version}

## <a name="setting-up-azure-powershell"></a><span data-ttu-id="2b22f-111">Configuration d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="2b22f-111">Setting up Azure PowerShell</span></span>

<span data-ttu-id="2b22f-112">Ces instructions utilisent Microsoft Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2b22f-112">These instructions use Microsoft Azure PowerShell.</span></span> <span data-ttu-id="2b22f-113">Hello suivant explique comment tooinstall et configurer Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2b22f-113">hello following article explains how tooinstall and configure Azure PowerShell.</span></span>

* [<span data-ttu-id="2b22f-114">Comment tooinstall et configurer Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="2b22f-114">How tooinstall and configure Azure PowerShell</span></span>](/powershell/azure/overview)

<span data-ttu-id="2b22f-115">exemples de Hello dans cet article supposent que vous disposez d’un groupe de ressources existant.</span><span class="sxs-lookup"><span data-stu-id="2b22f-115">hello examples in this article assume that you have an existing resource group.</span></span> <span data-ttu-id="2b22f-116">Vous pouvez créer un groupe de ressources à l’aide de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="2b22f-116">You can create a resource group using hello following command:</span></span>

```powershell
New-AzureRmResourceGroup -Name MyRG -Location "West US"
```

> [!NOTE]
> <span data-ttu-id="2b22f-117">Azure Resource Manager exige des groupes de ressources qu’ils disposent tous d’un emplacement.</span><span class="sxs-lookup"><span data-stu-id="2b22f-117">Azure Resource Manager requires that all resource groups have a location.</span></span> <span data-ttu-id="2b22f-118">Cet emplacement est utilisé comme valeur par défaut hello pour les ressources créées dans ce groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="2b22f-118">This location is used as hello default for resources created in that resource group.</span></span> <span data-ttu-id="2b22f-119">Toutefois, étant donné que les ressources du profil Traffic Manager sont globales, pas régional, choix hello de l’emplacement du groupe de ressources n’a aucun impact sur Azure Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="2b22f-119">However, since Traffic Manager profile resources are global, not regional, hello choice of resource group location has no impact on Azure Traffic Manager.</span></span>

## <a name="create-a-traffic-manager-profile"></a><span data-ttu-id="2b22f-120">Créer un profil Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="2b22f-120">Create a Traffic Manager Profile</span></span>

<span data-ttu-id="2b22f-121">toocreate un profil Traffic Manager, utilisez hello `New-AzureRmTrafficManagerProfile` applet de commande :</span><span class="sxs-lookup"><span data-stu-id="2b22f-121">toocreate a Traffic Manager profile, use hello `New-AzureRmTrafficManagerProfile` cmdlet:</span></span>

```powershell
$profile = New-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName contoso -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
```

<span data-ttu-id="2b22f-122">Hello tableau suivant décrit les paramètres de hello :</span><span class="sxs-lookup"><span data-stu-id="2b22f-122">hello following table describes hello parameters:</span></span>

| <span data-ttu-id="2b22f-123">Paramètre</span><span class="sxs-lookup"><span data-stu-id="2b22f-123">Parameter</span></span> | <span data-ttu-id="2b22f-124">Description</span><span class="sxs-lookup"><span data-stu-id="2b22f-124">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2b22f-125">Nom</span><span class="sxs-lookup"><span data-stu-id="2b22f-125">Name</span></span> |<span data-ttu-id="2b22f-126">nom de la ressource Hello pour hello ressource de profil Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="2b22f-126">hello resource name for hello Traffic Manager profile resource.</span></span> <span data-ttu-id="2b22f-127">Profils Bonjour même groupe de ressources doive avoir des noms uniques.</span><span class="sxs-lookup"><span data-stu-id="2b22f-127">Profiles in hello same resource group must have unique names.</span></span> <span data-ttu-id="2b22f-128">Ce nom est différent du nom DNS de hello utilisé pour les requêtes DNS.</span><span class="sxs-lookup"><span data-stu-id="2b22f-128">This name is separate from hello DNS name used for DNS queries.</span></span> |
| <span data-ttu-id="2b22f-129">ResourceGroupName</span><span class="sxs-lookup"><span data-stu-id="2b22f-129">ResourceGroupName</span></span> |<span data-ttu-id="2b22f-130">nom de Hello de hello groupe conteneur hello profil ressource.</span><span class="sxs-lookup"><span data-stu-id="2b22f-130">hello name of hello resource group containing hello profile resource.</span></span> |
| <span data-ttu-id="2b22f-131">TrafficRoutingMethod</span><span class="sxs-lookup"><span data-stu-id="2b22f-131">TrafficRoutingMethod</span></span> |<span data-ttu-id="2b22f-132">Spécifie les hello de routage du trafic méthode utilisée toodetermine point de terminaison qui est retourné en réponse à une requête DNS.</span><span class="sxs-lookup"><span data-stu-id="2b22f-132">Specifies hello traffic-routing method used toodetermine which endpoint is returned in response a DNS query.</span></span> <span data-ttu-id="2b22f-133">Les valeurs possibles sont « Performance », « Weighted » ou « Priority ».</span><span class="sxs-lookup"><span data-stu-id="2b22f-133">Possible values are 'Performance', 'Weighted' or 'Priority'.</span></span> |
| <span data-ttu-id="2b22f-134">RelativeDnsName</span><span class="sxs-lookup"><span data-stu-id="2b22f-134">RelativeDnsName</span></span> |<span data-ttu-id="2b22f-135">Spécifie la partie du nom d’hôte hello du nom DNS de hello fournie par ce profil Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="2b22f-135">Specifies hello hostname portion of hello DNS name provided by this Traffic Manager profile.</span></span> <span data-ttu-id="2b22f-136">Cette valeur est combinée avec le nom de domaine DNS hello utilisé par Azure Traffic Manager tooform hello nom de domaine complet (FQDN) du profil de hello.</span><span class="sxs-lookup"><span data-stu-id="2b22f-136">This value is combined with hello DNS domain name used by Azure Traffic Manager tooform hello fully qualified domain name (FQDN) of hello profile.</span></span> <span data-ttu-id="2b22f-137">Par exemple, la définition de valeur hello de « contoso » devient « contoso.trafficmanager.net ».</span><span class="sxs-lookup"><span data-stu-id="2b22f-137">For example, setting hello value of 'contoso' becomes 'contoso.trafficmanager.net.'</span></span> |
| <span data-ttu-id="2b22f-138">TTL</span><span class="sxs-lookup"><span data-stu-id="2b22f-138">TTL</span></span> |<span data-ttu-id="2b22f-139">Spécifie les hello DNS Time-to-Live (TTL), en secondes.</span><span class="sxs-lookup"><span data-stu-id="2b22f-139">Specifies hello DNS Time-to-Live (TTL), in seconds.</span></span> <span data-ttu-id="2b22f-140">Cette durée de vie indique aux résolutions DNS locales de hello et les clients DNS les réponses DNS la durée pendant laquelle toocache pour ce profil Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="2b22f-140">This TTL informs hello Local DNS resolvers and DNS clients how long toocache DNS responses for this Traffic Manager profile.</span></span> |
| <span data-ttu-id="2b22f-141">MonitorProtocol</span><span class="sxs-lookup"><span data-stu-id="2b22f-141">MonitorProtocol</span></span> |<span data-ttu-id="2b22f-142">Spécifie le contrôle d’intégrité du point de terminaison de toomonitor toouse hello protocole.</span><span class="sxs-lookup"><span data-stu-id="2b22f-142">Specifies hello protocol toouse toomonitor endpoint health.</span></span> <span data-ttu-id="2b22f-143">Les valeurs possibles sont « HTTP » et « HTTPS ».</span><span class="sxs-lookup"><span data-stu-id="2b22f-143">Possible values are 'HTTP' and 'HTTPS'.</span></span> |
| <span data-ttu-id="2b22f-144">MonitorPort</span><span class="sxs-lookup"><span data-stu-id="2b22f-144">MonitorPort</span></span> |<span data-ttu-id="2b22f-145">Spécifie hello le port TCP utilisé d’intégrité du point de terminaison toomonitor.</span><span class="sxs-lookup"><span data-stu-id="2b22f-145">Specifies hello TCP port used toomonitor endpoint health.</span></span> |
| <span data-ttu-id="2b22f-146">MonitorPort</span><span class="sxs-lookup"><span data-stu-id="2b22f-146">MonitorPath</span></span> |<span data-ttu-id="2b22f-147">Spécifie le nom de domaine de point de terminaison hello chemin d’accès relatif toohello utilisé tooprobe pour le contrôle d’intégrité du point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="2b22f-147">Specifies hello path relative toohello endpoint domain name used tooprobe for endpoint health.</span></span> |

<span data-ttu-id="2b22f-148">applet de commande Hello crée un profil Traffic Manager dans Azure et renvoie un tooPowerShell objet de profil correspondant.</span><span class="sxs-lookup"><span data-stu-id="2b22f-148">hello cmdlet creates a Traffic Manager profile in Azure and returns a corresponding profile object tooPowerShell.</span></span> <span data-ttu-id="2b22f-149">À ce stade, le profil hello ne contient aucun point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="2b22f-149">At this point, hello profile does not contain any endpoints.</span></span> <span data-ttu-id="2b22f-150">Pour plus d’informations sur l’ajout du profil Traffic Manager tooa points de terminaison, consultez [Ajout de points de terminaison de Traffic Manager](#adding-traffic-manager-endpoints).</span><span class="sxs-lookup"><span data-stu-id="2b22f-150">For more information about adding endpoints tooa Traffic Manager profile, see [Adding Traffic Manager Endpoints](#adding-traffic-manager-endpoints).</span></span>

## <a name="get-a-traffic-manager-profile"></a><span data-ttu-id="2b22f-151">Récupérer un profil Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="2b22f-151">Get a Traffic Manager Profile</span></span>

<span data-ttu-id="2b22f-152">tooretrieve un objet de profil Traffic Manager existant, utilisez hello `Get-AzureRmTrafficManagerProfle` applet de commande :</span><span class="sxs-lookup"><span data-stu-id="2b22f-152">tooretrieve an existing Traffic Manager profile object, use hello `Get-AzureRmTrafficManagerProfle` cmdlet:</span></span>

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG
```

<span data-ttu-id="2b22f-153">Cette applet de commande renvoie un objet de profil Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="2b22f-153">This cmdlet returns a Traffic Manager profile object.</span></span>

## <a name="update-a-traffic-manager-profile"></a><span data-ttu-id="2b22f-154">Mettre à jour un profil Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="2b22f-154">Update a Traffic Manager Profile</span></span>

<span data-ttu-id="2b22f-155">La modification des profils Traffic Manager est un processus en 3 étapes :</span><span class="sxs-lookup"><span data-stu-id="2b22f-155">Modifying Traffic Manager profiles follows a 3-step process:</span></span>

1. <span data-ttu-id="2b22f-156">À l’aide de profil récupérer hello `Get-AzureRmTrafficManagerProfile` ou utiliser le profil hello retourné par `New-AzureRmTrafficManagerProfile`.</span><span class="sxs-lookup"><span data-stu-id="2b22f-156">Retrieve hello profile using `Get-AzureRmTrafficManagerProfile` or use hello profile returned by `New-AzureRmTrafficManagerProfile`.</span></span>
2. <span data-ttu-id="2b22f-157">Modifier le profil de hello.</span><span class="sxs-lookup"><span data-stu-id="2b22f-157">Modify hello profile.</span></span> <span data-ttu-id="2b22f-158">Vous pouvez ajouter et supprimer des points de terminaison ou modifier les paramètres des points de terminaison ou du profil.</span><span class="sxs-lookup"><span data-stu-id="2b22f-158">You can add and remove endpoints or change endpoint or profile parameters.</span></span> <span data-ttu-id="2b22f-159">Ces modifications sont des opérations hors connexion.</span><span class="sxs-lookup"><span data-stu-id="2b22f-159">These changes are off-line operations.</span></span> <span data-ttu-id="2b22f-160">Vous ne modifiez objet local de hello en mémoire qui représente le profil de hello.</span><span class="sxs-lookup"><span data-stu-id="2b22f-160">You are only changing hello local object in memory that represents hello profile.</span></span>
3. <span data-ttu-id="2b22f-161">Valider les modifications apportées à l’aide de hello `Set-AzureRmTrafficManagerProfile` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="2b22f-161">Commit your changes using hello `Set-AzureRmTrafficManagerProfile` cmdlet.</span></span>

<span data-ttu-id="2b22f-162">Toutes les propriétés de profil peuvent être modifiées à l’exception RelativeDnsName du profil hello.</span><span class="sxs-lookup"><span data-stu-id="2b22f-162">All profile properties can be changed except hello profile's RelativeDnsName.</span></span> <span data-ttu-id="2b22f-163">toochange hello RelativeDnsName, vous devez supprimer le profil et un nouveau profil avec un nouveau nom.</span><span class="sxs-lookup"><span data-stu-id="2b22f-163">toochange hello RelativeDnsName, you must delete profile and a new profile with a new name.</span></span>

<span data-ttu-id="2b22f-164">Bonjour à l’exemple suivant montre comment toochange hello durée de vie du profil :</span><span class="sxs-lookup"><span data-stu-id="2b22f-164">hello following example demonstrates how toochange hello profile's TTL:</span></span>

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG
$profile.Ttl = 300
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

<span data-ttu-id="2b22f-165">Il existe trois types de points de terminaison Traffic Manager :</span><span class="sxs-lookup"><span data-stu-id="2b22f-165">There are three types of Traffic Manager endpoints:</span></span>

1. <span data-ttu-id="2b22f-166">Les **points de terminaison Azure** sont des services hébergés dans Azure.</span><span class="sxs-lookup"><span data-stu-id="2b22f-166">**Azure endpoints** are services hosted in Azure</span></span>
2. <span data-ttu-id="2b22f-167">Les **points de terminaison externes** sont des services hébergés en dehors d’Azure.</span><span class="sxs-lookup"><span data-stu-id="2b22f-167">**External endpoints** are services hosted outside of Azure</span></span>
3. <span data-ttu-id="2b22f-168">**Imbriqué des points de terminaison** sont des hiérarchies utilisé tooconstruct imbriqué de profils Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="2b22f-168">**Nested endpoints** are used tooconstruct nested hierarchies of Traffic Manager profiles.</span></span> <span data-ttu-id="2b22f-169">Ils permettent de définir des configurations de routage du trafic avancées pour les applications complexes.</span><span class="sxs-lookup"><span data-stu-id="2b22f-169">Nested endpoints enable advanced traffic-routing configurations for complex applications.</span></span>

<span data-ttu-id="2b22f-170">Dans ces trois cas, les points de terminaison peuvent être ajoutés de deux manières :</span><span class="sxs-lookup"><span data-stu-id="2b22f-170">In all three cases, endpoints can be added in two ways:</span></span>

1. <span data-ttu-id="2b22f-171">En suivant le processus en 3 étapes décrit précédemment.</span><span class="sxs-lookup"><span data-stu-id="2b22f-171">Using a 3-step process described previously.</span></span> <span data-ttu-id="2b22f-172">avantage Hello de cette méthode est que plusieurs modifications de point de terminaison peuvent être effectuées dans une seule mise à jour.</span><span class="sxs-lookup"><span data-stu-id="2b22f-172">hello advantage of this method is that several endpoint changes can be made in a single update.</span></span>
2. <span data-ttu-id="2b22f-173">À l’aide d’applet de commande New-AzureRmTrafficManagerEndpoint hello.</span><span class="sxs-lookup"><span data-stu-id="2b22f-173">Using hello New-AzureRmTrafficManagerEndpoint cmdlet.</span></span> <span data-ttu-id="2b22f-174">Cette applet de commande ajoute un point de terminaison tooan existant du profil Traffic Manager en une seule opération.</span><span class="sxs-lookup"><span data-stu-id="2b22f-174">This cmdlet adds an endpoint tooan existing Traffic Manager profile in a single operation.</span></span>

## <a name="adding-azure-endpoints"></a><span data-ttu-id="2b22f-175">Ajout de points de terminaison Azure</span><span class="sxs-lookup"><span data-stu-id="2b22f-175">Adding Azure Endpoints</span></span>

<span data-ttu-id="2b22f-176">Les points de terminaison Azure font référence à des services hébergés dans Azure.</span><span class="sxs-lookup"><span data-stu-id="2b22f-176">Azure endpoints reference services hosted in Azure.</span></span> <span data-ttu-id="2b22f-177">Les types de point de terminaison Azure pris en charge sont au nombre de deux :</span><span class="sxs-lookup"><span data-stu-id="2b22f-177">Two types of Azure endpoints are supported:</span></span>

1. <span data-ttu-id="2b22f-178">Azure Web Apps </span><span class="sxs-lookup"><span data-stu-id="2b22f-178">Azure Web Apps</span></span>
2. <span data-ttu-id="2b22f-179">Ressources d’adresse IP publique Azure (qui peuvent être attaché tooa équilibreur de charge ou une carte réseau de machine virtuelle).</span><span class="sxs-lookup"><span data-stu-id="2b22f-179">Azure PublicIpAddress resources (which can be attached tooa load-balancer or a virtual machine NIC).</span></span> <span data-ttu-id="2b22f-180">Hello adresse IP publique doit avoir un nom DNS assigné toobe utilisé dans le Gestionnaire de trafic.</span><span class="sxs-lookup"><span data-stu-id="2b22f-180">hello PublicIpAddress must have a DNS name assigned toobe used in Traffic Manager.</span></span>

<span data-ttu-id="2b22f-181">Dans chaque cas :</span><span class="sxs-lookup"><span data-stu-id="2b22f-181">In each case:</span></span>

* <span data-ttu-id="2b22f-182">service de Hello est spécifié à l’aide du paramètre de « targetResourceId » hello de `Add-AzureRmTrafficManagerEndpointConfig` ou `New-AzureRmTrafficManagerEndpoint`.</span><span class="sxs-lookup"><span data-stu-id="2b22f-182">hello service is specified using hello 'targetResourceId' parameter of `Add-AzureRmTrafficManagerEndpointConfig` or `New-AzureRmTrafficManagerEndpoint`.</span></span>
* <span data-ttu-id="2b22f-183">Hello 'Target' et 'EndpointLocation' sont implicitement hello TargetResourceId.</span><span class="sxs-lookup"><span data-stu-id="2b22f-183">hello 'Target' and 'EndpointLocation' are implied by hello TargetResourceId.</span></span>
* <span data-ttu-id="2b22f-184">Spécification de hello « Weight » est facultative.</span><span class="sxs-lookup"><span data-stu-id="2b22f-184">Specifying hello 'Weight' is optional.</span></span> <span data-ttu-id="2b22f-185">Poids sont uniquement utilisés si le profil de hello est la méthode de routage du trafic toouse configuré hello 'Weighted'.</span><span class="sxs-lookup"><span data-stu-id="2b22f-185">Weights are only used if hello profile is configured toouse hello 'Weighted' traffic-routing method.</span></span> <span data-ttu-id="2b22f-186">Autrement, elles sont ignorées.</span><span class="sxs-lookup"><span data-stu-id="2b22f-186">Otherwise, they are ignored.</span></span> <span data-ttu-id="2b22f-187">Si spécifié, la valeur de hello doit être un nombre compris entre 1 et 1000.</span><span class="sxs-lookup"><span data-stu-id="2b22f-187">If specified, hello value must be a number between 1 and 1000.</span></span> <span data-ttu-id="2b22f-188">valeur par défaut de Hello est '1'.</span><span class="sxs-lookup"><span data-stu-id="2b22f-188">hello default value is '1'.</span></span>
* <span data-ttu-id="2b22f-189">En spécifiant hello 'Priority' est facultatif.</span><span class="sxs-lookup"><span data-stu-id="2b22f-189">Specifying hello 'Priority' is optional.</span></span> <span data-ttu-id="2b22f-190">Les priorités sont uniquement utilisées si le profil de hello est la méthode de routage du trafic toouse configuré hello 'Priority'.</span><span class="sxs-lookup"><span data-stu-id="2b22f-190">Priorities are only used if hello profile is configured toouse hello 'Priority' traffic-routing method.</span></span> <span data-ttu-id="2b22f-191">Autrement, elles sont ignorées.</span><span class="sxs-lookup"><span data-stu-id="2b22f-191">Otherwise, they are ignored.</span></span> <span data-ttu-id="2b22f-192">Les valeurs valides sont de 1 too1000 ayant des valeurs inférieures indiquant une priorité plus élevée.</span><span class="sxs-lookup"><span data-stu-id="2b22f-192">Valid values are from 1 too1000 with lower values indicating a higher priority.</span></span> <span data-ttu-id="2b22f-193">Si elles sont spécifiées pour un point de terminaison, elles doivent l’être pour tous les points de terminaison.</span><span class="sxs-lookup"><span data-stu-id="2b22f-193">If specified for one endpoint, they must be specified for all endpoints.</span></span> <span data-ttu-id="2b22f-194">Si omis, les valeurs par défaut à partir de '1' sont appliquées dans l’ordre de hello que les points de terminaison hello sont répertoriés.</span><span class="sxs-lookup"><span data-stu-id="2b22f-194">If omitted, default values starting from '1' are applied in hello order that hello endpoints are listed.</span></span>

### <a name="example-1-adding-web-app-endpoints-using-add-azurermtrafficmanagerendpointconfig"></a><span data-ttu-id="2b22f-195">Exemple 1 : ajout de points de terminaison d’application web à l’aide de `Add-AzureRmTrafficManagerEndpointConfig`</span><span class="sxs-lookup"><span data-stu-id="2b22f-195">Example 1: Adding Web App endpoints using `Add-AzureRmTrafficManagerEndpointConfig`</span></span>

<span data-ttu-id="2b22f-196">Dans cet exemple, nous créons un profil Traffic Manager et ajouter deux points de terminaison de l’application Web à l’aide de hello `Add-AzureRmTrafficManagerEndpointConfig` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="2b22f-196">In this example, we create a Traffic Manager profile and add two Web App endpoints using hello `Add-AzureRmTrafficManagerEndpointConfig` cmdlet.</span></span>

```powershell
$profile = New-AzureRmTrafficManagerProfile -Name myprofile -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName myapp -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
$webapp1 = Get-AzureRMWebApp -Name webapp1
Add-AzureRmTrafficManagerEndpointConfig -EndpointName webapp1ep -TrafficManagerProfile $profile -Type AzureEndpoints -TargetResourceId $webapp1.Id -EndpointStatus Enabled
$webapp2 = Get-AzureRMWebApp -Name webapp2
Add-AzureRmTrafficManagerEndpointConfig -EndpointName webapp2ep -TrafficManagerProfile $profile -Type AzureEndpoints -TargetResourceId $webapp2.Id -EndpointStatus Enabled
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```
### <a name="example-2-adding-a-publicipaddress-endpoint-using-new-azurermtrafficmanagerendpoint"></a><span data-ttu-id="2b22f-197">Exemple 2 : ajout d’un point de terminaison publicIpAddress à l’aide de `New-AzureRmTrafficManagerEndpoint`</span><span class="sxs-lookup"><span data-stu-id="2b22f-197">Example 2: Adding a publicIpAddress endpoint using `New-AzureRmTrafficManagerEndpoint`</span></span>

<span data-ttu-id="2b22f-198">Dans cet exemple, une ressource d’adresse IP publique est ajoutée le profil Traffic Manager toohello.</span><span class="sxs-lookup"><span data-stu-id="2b22f-198">In this example, a public IP address resource is added toohello Traffic Manager profile.</span></span> <span data-ttu-id="2b22f-199">adresse IP publique de Hello doit avoir un nom DNS configuré et peut être lié soit toohello carte réseau d’un équilibrage de charge de machine virtuelle ou tooa.</span><span class="sxs-lookup"><span data-stu-id="2b22f-199">hello public IP address must have a DNS name configured, and can be bound either toohello NIC of a VM or tooa load balancer.</span></span>

```powershell
$ip = Get-AzureRmPublicIpAddress -Name MyPublicIP -ResourceGroupName MyRG
New-AzureRmTrafficManagerEndpoint -Name MyIpEndpoint -ProfileName MyProfile -ResourceGroupName MyRG -Type AzureEndpoints -TargetResourceId $ip.Id -EndpointStatus Enabled
```

## <a name="adding-external-endpoints"></a><span data-ttu-id="2b22f-200">Ajout de points de terminaison externes</span><span class="sxs-lookup"><span data-stu-id="2b22f-200">Adding External Endpoints</span></span>

<span data-ttu-id="2b22f-201">Traffic Manager utilise des points de terminaison externe toodirect trafic tooservices hébergé en dehors d’Azure.</span><span class="sxs-lookup"><span data-stu-id="2b22f-201">Traffic Manager uses external endpoints toodirect traffic tooservices hosted outside of Azure.</span></span> <span data-ttu-id="2b22f-202">Comme les points de terminaison Azure, les points de terminaison externes peuvent être ajoutés à l’aide de `Add-AzureRmTrafficManagerEndpointConfig` suivi de `Set-AzureRmTrafficManagerProfile`, ou avec `New-AzureRMTrafficManagerEndpoint`.</span><span class="sxs-lookup"><span data-stu-id="2b22f-202">As with Azure endpoints, external endpoints can be added either using `Add-AzureRmTrafficManagerEndpointConfig` followed by `Set-AzureRmTrafficManagerProfile`, or `New-AzureRMTrafficManagerEndpoint`.</span></span>

<span data-ttu-id="2b22f-203">Lors de la spécification de points de terminaison externes :</span><span class="sxs-lookup"><span data-stu-id="2b22f-203">When specifying external endpoints:</span></span>

* <span data-ttu-id="2b22f-204">nom de domaine du point de terminaison Hello doit être spécifié à l’aide du paramètre de 'Target' hello</span><span class="sxs-lookup"><span data-stu-id="2b22f-204">hello endpoint domain name must be specified using hello 'Target' parameter</span></span>
* <span data-ttu-id="2b22f-205">Si hello méthode de routage du trafic « Performance » est utilisé, hello 'EndpointLocation' est requis.</span><span class="sxs-lookup"><span data-stu-id="2b22f-205">If hello 'Performance' traffic-routing method is used, hello 'EndpointLocation' is required.</span></span> <span data-ttu-id="2b22f-206">Sinon, il est facultatif.</span><span class="sxs-lookup"><span data-stu-id="2b22f-206">Otherwise it is optional.</span></span> <span data-ttu-id="2b22f-207">la valeur Hello doit être un [nom de la région Azure valide](https://azure.microsoft.com/regions/).</span><span class="sxs-lookup"><span data-stu-id="2b22f-207">hello value must be a [valid Azure region name](https://azure.microsoft.com/regions/).</span></span>
* <span data-ttu-id="2b22f-208">Hello 'Poids' et 'Priority' est facultatif.</span><span class="sxs-lookup"><span data-stu-id="2b22f-208">hello 'Weight' and 'Priority' are optional.</span></span>

### <a name="example-1-adding-external-endpoints-using-add-azurermtrafficmanagerendpointconfig-and-set-azurermtrafficmanagerprofile"></a><span data-ttu-id="2b22f-209">Exemple 1 : ajout de points de terminaison externes à l’aide de `Add-AzureRmTrafficManagerEndpointConfig` et `Set-AzureRmTrafficManagerProfile`</span><span class="sxs-lookup"><span data-stu-id="2b22f-209">Example 1: Adding external endpoints using `Add-AzureRmTrafficManagerEndpointConfig` and `Set-AzureRmTrafficManagerProfile`</span></span>

<span data-ttu-id="2b22f-210">Dans cet exemple, nous créer un profil Traffic Manager, ajoutez les deux points de terminaison externes et valider les modifications de hello.</span><span class="sxs-lookup"><span data-stu-id="2b22f-210">In this example, we create a Traffic Manager profile, add two external endpoints, and commit hello changes.</span></span>

```powershell
$profile = New-AzureRmTrafficManagerProfile -Name myprofile -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName myapp -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
Add-AzureRmTrafficManagerEndpointConfig -EndpointName eu-endpoint -TrafficManagerProfile $profile -Type ExternalEndpoints -Target app-eu.contoso.com -EndpointLocation "North Europe" -EndpointStatus Enabled
Add-AzureRmTrafficManagerEndpointConfig -EndpointName us-endpoint -TrafficManagerProfile $profile -Type ExternalEndpoints -Target app-us.contoso.com -EndpointLocation "Central US" -EndpointStatus Enabled
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

### <a name="example-2-adding-external-endpoints-using-new-azurermtrafficmanagerendpoint"></a><span data-ttu-id="2b22f-211">Exemple 2 : ajout de points de terminaison externes à l’aide de `New-AzureRmTrafficManagerEndpoint`</span><span class="sxs-lookup"><span data-stu-id="2b22f-211">Example 2: Adding external endpoints using `New-AzureRmTrafficManagerEndpoint`</span></span>

<span data-ttu-id="2b22f-212">Dans cet exemple, nous ajouter un profil existant tooan de point de terminaison externe.</span><span class="sxs-lookup"><span data-stu-id="2b22f-212">In this example, we add an external endpoint tooan existing profile.</span></span> <span data-ttu-id="2b22f-213">profil de Hello est spécifié à l’aide de noms de groupe de ressources et un profil de hello.</span><span class="sxs-lookup"><span data-stu-id="2b22f-213">hello profile is specified using hello profile and resource group names.</span></span>

```powershell
New-AzureRmTrafficManagerEndpoint -Name eu-endpoint -ProfileName MyProfile -ResourceGroupName MyRG -Type ExternalEndpoints -Target app-eu.contoso.com -EndpointStatus Enabled
```

## <a name="adding-nested-endpoints"></a><span data-ttu-id="2b22f-214">Ajout de points de terminaison « imbriqués »</span><span class="sxs-lookup"><span data-stu-id="2b22f-214">Adding 'Nested' endpoints</span></span>

<span data-ttu-id="2b22f-215">Chaque profil Traffic Manager spécifie une seule méthode de routage du trafic.</span><span class="sxs-lookup"><span data-stu-id="2b22f-215">Each Traffic Manager profile specifies a single traffic-routing method.</span></span> <span data-ttu-id="2b22f-216">Toutefois, il existe des scénarios qui requièrent que le routage hello fournis par un seul profil Traffic Manager le routage du trafic plus sophistiquées.</span><span class="sxs-lookup"><span data-stu-id="2b22f-216">However, there are scenarios that require more sophisticated traffic routing than hello routing provided by a single Traffic Manager profile.</span></span> <span data-ttu-id="2b22f-217">Vous pouvez imbriquer des avantages de hello de toocombine de profils Traffic Manager de plusieurs méthodes de routage du trafic.</span><span class="sxs-lookup"><span data-stu-id="2b22f-217">You can nest Traffic Manager profiles toocombine hello benefits of more than one traffic-routing method.</span></span> <span data-ttu-id="2b22f-218">Profils imbriqués permettent toooverride hello par défaut Traffic Manager comportement toosupport plus volumineux et les déploiements d’applications plus complexes.</span><span class="sxs-lookup"><span data-stu-id="2b22f-218">Nested profiles allow you toooverride hello default Traffic Manager behavior toosupport larger and more complex application deployments.</span></span> <span data-ttu-id="2b22f-219">Pour obtenir des informations plus détaillées, consultez [Profils Traffic Manager imbriqués](traffic-manager-nested-profiles.md).</span><span class="sxs-lookup"><span data-stu-id="2b22f-219">For more detailed examples, see [Nested Traffic Manager profiles](traffic-manager-nested-profiles.md).</span></span>

<span data-ttu-id="2b22f-220">Points de terminaison imbriquées sont configurées au profil parent de hello, à l’aide d’un type de point de terminaison spécifique, 'NestedEndpoints'.</span><span class="sxs-lookup"><span data-stu-id="2b22f-220">Nested endpoints are configured at hello parent profile, using a specific endpoint type, 'NestedEndpoints'.</span></span> <span data-ttu-id="2b22f-221">Lors de la spécification de points de terminaison imbriqués :</span><span class="sxs-lookup"><span data-stu-id="2b22f-221">When specifying nested endpoints:</span></span>

* <span data-ttu-id="2b22f-222">point de terminaison Hello doit être spécifié à l’aide du paramètre de 'targetResourceId' hello</span><span class="sxs-lookup"><span data-stu-id="2b22f-222">hello endpoint must be specified using hello 'targetResourceId' parameter</span></span>
* <span data-ttu-id="2b22f-223">Si hello méthode de routage du trafic « Performance » est utilisé, hello 'EndpointLocation' est requis.</span><span class="sxs-lookup"><span data-stu-id="2b22f-223">If hello 'Performance' traffic-routing method is used, hello 'EndpointLocation' is required.</span></span> <span data-ttu-id="2b22f-224">Sinon, il est facultatif.</span><span class="sxs-lookup"><span data-stu-id="2b22f-224">Otherwise it is optional.</span></span> <span data-ttu-id="2b22f-225">la valeur Hello doit être un [nom de la région Azure valide](http://azure.microsoft.com/regions/).</span><span class="sxs-lookup"><span data-stu-id="2b22f-225">hello value must be a [valid Azure region name](http://azure.microsoft.com/regions/).</span></span>
* <span data-ttu-id="2b22f-226">Hello 'Poids' et 'Priority' est facultatif, comme pour les points de terminaison Azure.</span><span class="sxs-lookup"><span data-stu-id="2b22f-226">hello 'Weight' and 'Priority' are optional, as for Azure endpoints.</span></span>
* <span data-ttu-id="2b22f-227">paramètre de 'MinChildEndpoints' Hello est facultatif.</span><span class="sxs-lookup"><span data-stu-id="2b22f-227">hello 'MinChildEndpoints' parameter is optional.</span></span> <span data-ttu-id="2b22f-228">valeur par défaut de Hello est '1'.</span><span class="sxs-lookup"><span data-stu-id="2b22f-228">hello default value is '1'.</span></span> <span data-ttu-id="2b22f-229">Si le nombre de hello de points de terminaison disponibles tombe sous ce seuil, profil parent de hello considère que le profil enfant hello « dégradé » et dévie le trafic toohello autres points de terminaison dans le profil de hello parent.</span><span class="sxs-lookup"><span data-stu-id="2b22f-229">If hello number of available endpoints falls below this threshold, hello parent profile considers hello child profile 'degraded' and diverts traffic toohello other endpoints in hello parent profile.</span></span>

### <a name="example-1-adding-nested-endpoints-using-add-azurermtrafficmanagerendpointconfig-and-set-azurermtrafficmanagerprofile"></a><span data-ttu-id="2b22f-230">Exemple 1 : ajout de points de terminaison imbriqués à l’aide de `Add-AzureRmTrafficManagerEndpointConfig` et `Set-AzureRmTrafficManagerProfile`</span><span class="sxs-lookup"><span data-stu-id="2b22f-230">Example 1: Adding nested endpoints using `Add-AzureRmTrafficManagerEndpointConfig` and `Set-AzureRmTrafficManagerProfile`</span></span>

<span data-ttu-id="2b22f-231">Dans cet exemple, nous créer des profils de parent et enfant Traffic Manager, ajouter un enfant de hello en tant que point de terminaison imbriquée toohello parent et valider les modifications de hello.</span><span class="sxs-lookup"><span data-stu-id="2b22f-231">In this example, we create new Traffic Manager child and parent profiles, add hello child as a nested endpoint toohello parent, and commit hello changes.</span></span>

```powershell
$child = New-AzureRmTrafficManagerProfile -Name child -ResourceGroupName MyRG -TrafficRoutingMethod Priority -RelativeDnsName child -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
$parent = New-AzureRmTrafficManagerProfile -Name parent -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName parent -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
Add-AzureRmTrafficManagerEndpointConfig -EndpointName child-endpoint -TrafficManagerProfile $parent -Type NestedEndpoints -TargetResourceId $child.Id -EndpointStatus Enabled -EndpointLocation "North Europe" -MinChildEndpoints 2
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

<span data-ttu-id="2b22f-232">Par souci de concision dans cet exemple, nous n’avez pas ajouté de tous les autres points de terminaison toohello enfant ou parent profils.</span><span class="sxs-lookup"><span data-stu-id="2b22f-232">For brevity in this example, we did not add any other endpoints toohello child or parent profiles.</span></span>

### <a name="example-2-adding-nested-endpoints-using-new-azurermtrafficmanagerendpoint"></a><span data-ttu-id="2b22f-233">Exemple 2 : ajout de points de terminaison imbriqués à l’aide de `New-AzureRmTrafficManagerEndpoint`</span><span class="sxs-lookup"><span data-stu-id="2b22f-233">Example 2: Adding nested endpoints using `New-AzureRmTrafficManagerEndpoint`</span></span>

<span data-ttu-id="2b22f-234">Dans cet exemple, nous ajouter un profil enfant existant comme point de terminaison imbriquée tooan existant parent profil.</span><span class="sxs-lookup"><span data-stu-id="2b22f-234">In this example, we add an existing child profile as a nested endpoint tooan existing parent profile.</span></span> <span data-ttu-id="2b22f-235">profil de Hello est spécifié à l’aide de noms de groupe de ressources et un profil de hello.</span><span class="sxs-lookup"><span data-stu-id="2b22f-235">hello profile is specified using hello profile and resource group names.</span></span>

```powershell
$child = Get-AzureRmTrafficManagerEndpoint -Name child -ResourceGroupName MyRG
New-AzureRmTrafficManagerEndpoint -Name child-endpoint -ProfileName parent -ResourceGroupName MyRG -Type NestedEndpoints -TargetResourceId $child.Id -EndpointStatus Enabled -EndpointLocation "North Europe" -MinChildEndpoints 2
```

## <a name="update-a-traffic-manager-endpoint"></a><span data-ttu-id="2b22f-236">Mettre à jour un point de terminaison Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="2b22f-236">Update a Traffic Manager Endpoint</span></span>

<span data-ttu-id="2b22f-237">Il existe deux façons tooupdate un point de terminaison Traffic Manager existant :</span><span class="sxs-lookup"><span data-stu-id="2b22f-237">There are two ways tooupdate an existing Traffic Manager endpoint:</span></span>

1. <span data-ttu-id="2b22f-238">Obtenir à l’aide de profil Traffic Manager hello `Get-AzureRmTrafficManagerProfile`, mettre à jour les propriétés du point de terminaison hello dans le profil de hello et valider les modifications hello à l’aide de `Set-AzureRmTrafficManagerProfile`.</span><span class="sxs-lookup"><span data-stu-id="2b22f-238">Get hello Traffic Manager profile using `Get-AzureRmTrafficManagerProfile`, update hello endpoint properties within hello profile, and commit hello changes using `Set-AzureRmTrafficManagerProfile`.</span></span> <span data-ttu-id="2b22f-239">Cette méthode présente un avantage hello d’être en mesure de tooupdate plus d’un point de terminaison en une seule opération.</span><span class="sxs-lookup"><span data-stu-id="2b22f-239">This method has hello advantage of being able tooupdate more than one endpoint in a single operation.</span></span>
2. <span data-ttu-id="2b22f-240">Obtenir à l’aide de point de terminaison de Traffic Manager hello `Get-AzureRmTrafficManagerEndpoint`, mettre à jour les propriétés du point de terminaison hello et valider les modifications hello à l’aide de `Set-AzureRmTrafficManagerEndpoint`.</span><span class="sxs-lookup"><span data-stu-id="2b22f-240">Get hello Traffic Manager endpoint using `Get-AzureRmTrafficManagerEndpoint`, update hello endpoint properties, and commit hello changes using `Set-AzureRmTrafficManagerEndpoint`.</span></span> <span data-ttu-id="2b22f-241">Cette méthode est plus simple, car il ne nécessite pas l’indexation dans un tableau de points de terminaison hello dans le profil de hello.</span><span class="sxs-lookup"><span data-stu-id="2b22f-241">This method is simpler, since it does not require indexing into hello Endpoints array in hello profile.</span></span>

### <a name="example-1-updating-endpoints-using-get-azurermtrafficmanagerprofile-and-set-azurermtrafficmanagerprofile"></a><span data-ttu-id="2b22f-242">Exemple 1 : mise à jour des points de terminaison à l’aide de `Get-AzureRmTrafficManagerProfile` et `Set-AzureRmTrafficManagerProfile`</span><span class="sxs-lookup"><span data-stu-id="2b22f-242">Example 1: Updating endpoints using `Get-AzureRmTrafficManagerProfile` and `Set-AzureRmTrafficManagerProfile`</span></span>

<span data-ttu-id="2b22f-243">Dans cet exemple, nous modifions la priorité de hello deux points de terminaison au sein d’un profil existant.</span><span class="sxs-lookup"><span data-stu-id="2b22f-243">In this example, we modify hello priority on two endpoints within an existing profile.</span></span>

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name myprofile -ResourceGroupName MyRG
$profile.Endpoints[0].Priority = 2
$profile.Endpoints[1].Priority = 1
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

### <a name="example-2-updating-an-endpoint-using-get-azurermtrafficmanagerendpoint-and-set-azurermtrafficmanagerendpoint"></a><span data-ttu-id="2b22f-244">Exemple 2 : mise à jour d’un point de terminaison à l’aide de `Get-AzureRmTrafficManagerEndpoint` et `Set-AzureRmTrafficManagerEndpoint`</span><span class="sxs-lookup"><span data-stu-id="2b22f-244">Example 2: Updating an endpoint using `Get-AzureRmTrafficManagerEndpoint` and `Set-AzureRmTrafficManagerEndpoint`</span></span>

<span data-ttu-id="2b22f-245">Dans cet exemple, nous modifions poids hello d’un point de terminaison unique dans un profil existant.</span><span class="sxs-lookup"><span data-stu-id="2b22f-245">In this example, we modify hello weight of a single endpoint in an existing profile.</span></span>

```powershell
$endpoint = Get-AzureRmTrafficManagerEndpoint -Name myendpoint -ProfileName myprofile -ResourceGroupName MyRG -Type ExternalEndpoints
$endpoint.Weight = 20
Set-AzureRmTrafficManagerEndpoint -TrafficManagerEndpoint $endpoint
```

## <a name="enabling-and-disabling-endpoints-and-profiles"></a><span data-ttu-id="2b22f-246">Activation et désactivation des points de terminaison et des profils</span><span class="sxs-lookup"><span data-stu-id="2b22f-246">Enabling and Disabling Endpoints and Profiles</span></span>

<span data-ttu-id="2b22f-247">Traffic Manager permet de points de terminaison individuels toobe activé et désactivé, tout en permettant l’activation et désactivation des profils de l’ensemble.</span><span class="sxs-lookup"><span data-stu-id="2b22f-247">Traffic Manager allows individual endpoints toobe enabled and disabled, as well as allowing enabling and disabling of entire profiles.</span></span>
<span data-ttu-id="2b22f-248">Ces modifications peuvent être apportées par les ressources de point de terminaison ou le profil de l’obtention/la mise à jour/définition hello.</span><span class="sxs-lookup"><span data-stu-id="2b22f-248">These changes can be made by getting/updating/setting hello endpoint or profile resources.</span></span> <span data-ttu-id="2b22f-249">toostreamline ces opérations courantes, elles sont également prises en charge via les applets de commande dédiées.</span><span class="sxs-lookup"><span data-stu-id="2b22f-249">toostreamline these common operations, they are also supported via dedicated cmdlets.</span></span>

### <a name="example-1-enabling-and-disabling-a-traffic-manager-profile"></a><span data-ttu-id="2b22f-250">Exemple 1 : activation et désactivation d’un profil Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="2b22f-250">Example 1: Enabling and disabling a Traffic Manager profile</span></span>

<span data-ttu-id="2b22f-251">tooenable un profil Traffic Manager, utilisez `Enable-AzureRmTrafficManagerProfile`.</span><span class="sxs-lookup"><span data-stu-id="2b22f-251">tooenable a Traffic Manager profile, use `Enable-AzureRmTrafficManagerProfile`.</span></span> <span data-ttu-id="2b22f-252">profil de Hello peut être spécifié à l’aide d’un objet de profil.</span><span class="sxs-lookup"><span data-stu-id="2b22f-252">hello profile can be specified using a profile object.</span></span> <span data-ttu-id="2b22f-253">Hello objet de profil peut être transmis via le pipeline de hello ou à l’aide de hello '-TrafficManagerProfile' paramètre.</span><span class="sxs-lookup"><span data-stu-id="2b22f-253">hello profile object can be passed via hello pipeline or by using hello '-TrafficManagerProfile' parameter.</span></span> <span data-ttu-id="2b22f-254">Dans cet exemple, nous spécifions le profil de hello par nom de groupe de ressources et un profil de hello.</span><span class="sxs-lookup"><span data-stu-id="2b22f-254">In this example, we specify hello profile by hello profile and resource group name.</span></span>

```powershell
Enable-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyResourceGroup
```

<span data-ttu-id="2b22f-255">toodisable un profil Traffic Manager :</span><span class="sxs-lookup"><span data-stu-id="2b22f-255">toodisable a Traffic Manager profile:</span></span>

```powershell
Disable-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyResourceGroup
```

<span data-ttu-id="2b22f-256">applet de commande Disable-AzureRmTrafficManagerProfile Hello demande confirmation.</span><span class="sxs-lookup"><span data-stu-id="2b22f-256">hello Disable-AzureRmTrafficManagerProfile cmdlet prompts for confirmation.</span></span> <span data-ttu-id="2b22f-257">Ce message peut être supprimé à l’aide de hello '-Force' paramètre.</span><span class="sxs-lookup"><span data-stu-id="2b22f-257">This prompt can be suppressed using hello '-Force' parameter.</span></span>

### <a name="example-2-enabling-and-disabling-a-traffic-manager-endpoint"></a><span data-ttu-id="2b22f-258">Exemple 2 : activation et désactivation d’un point de terminaison Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="2b22f-258">Example 2: Enabling and disabling a Traffic Manager endpoint</span></span>

<span data-ttu-id="2b22f-259">tooenable un point de terminaison Traffic Manager, utilisez `Enable-AzureRmTrafficManagerEndpoint`.</span><span class="sxs-lookup"><span data-stu-id="2b22f-259">tooenable a Traffic Manager endpoint, use `Enable-AzureRmTrafficManagerEndpoint`.</span></span> <span data-ttu-id="2b22f-260">Il existe deux points de terminaison hello de toospecify façons</span><span class="sxs-lookup"><span data-stu-id="2b22f-260">There are two ways toospecify hello endpoint</span></span>

1. <span data-ttu-id="2b22f-261">À l’aide d’un objet TrafficManagerEndpoint transmis via le pipeline de hello ou hello '-TrafficManagerEndpoint' paramètre</span><span class="sxs-lookup"><span data-stu-id="2b22f-261">Using a TrafficManagerEndpoint object passed via hello pipeline or using hello '-TrafficManagerEndpoint' parameter</span></span>
2. <span data-ttu-id="2b22f-262">À l’aide du nom de point de terminaison hello, type de point de terminaison, nom du profil et nom de groupe de ressources :</span><span class="sxs-lookup"><span data-stu-id="2b22f-262">Using hello endpoint name, endpoint type, profile name, and resource group name:</span></span>

```powershell
Enable-AzureRmTrafficManagerEndpoint -Name MyEndpoint -Type AzureEndpoints -ProfileName MyProfile -ResourceGroupName MyRG
```

<span data-ttu-id="2b22f-263">De même, toodisable un point de terminaison Traffic Manager :</span><span class="sxs-lookup"><span data-stu-id="2b22f-263">Similarly, toodisable a Traffic Manager endpoint:</span></span>

```powershell
Disable-AzureRmTrafficManagerEndpoint -Name MyEndpoint -Type AzureEndpoints -ProfileName MyProfile -ResourceGroupName MyRG -Force
```

<span data-ttu-id="2b22f-264">Comme avec `Disable-AzureRmTrafficManagerProfile`, hello `Disable-AzureRmTrafficManagerEndpoint` applet de commande vous demande confirmation.</span><span class="sxs-lookup"><span data-stu-id="2b22f-264">As with `Disable-AzureRmTrafficManagerProfile`, hello `Disable-AzureRmTrafficManagerEndpoint` cmdlet prompts for confirmation.</span></span> <span data-ttu-id="2b22f-265">Ce message peut être supprimé à l’aide de hello '-Force' paramètre.</span><span class="sxs-lookup"><span data-stu-id="2b22f-265">This prompt can be suppressed using hello '-Force' parameter.</span></span>

## <a name="delete-a-traffic-manager-endpoint"></a><span data-ttu-id="2b22f-266">Supprimer un point de terminaison Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="2b22f-266">Delete a Traffic Manager Endpoint</span></span>

<span data-ttu-id="2b22f-267">tooremove des points de terminaison individuels, utilisez hello `Remove-AzureRmTrafficManagerEndpoint` applet de commande :</span><span class="sxs-lookup"><span data-stu-id="2b22f-267">tooremove individual endpoints, use hello `Remove-AzureRmTrafficManagerEndpoint` cmdlet:</span></span>

```powershell
Remove-AzureRmTrafficManagerEndpoint -Name MyEndpoint -Type AzureEndpoints -ProfileName MyProfile -ResourceGroupName MyRG
```

<span data-ttu-id="2b22f-268">Cette applet de commande vous demande de confirmer l’opération.</span><span class="sxs-lookup"><span data-stu-id="2b22f-268">This cmdlet prompts for confirmation.</span></span> <span data-ttu-id="2b22f-269">Ce message peut être supprimé à l’aide de hello '-Force' paramètre.</span><span class="sxs-lookup"><span data-stu-id="2b22f-269">This prompt can be suppressed using hello '-Force' parameter.</span></span>

## <a name="delete-a-traffic-manager-profile"></a><span data-ttu-id="2b22f-270">Supprimer un profil Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="2b22f-270">Delete a Traffic Manager Profile</span></span>

<span data-ttu-id="2b22f-271">toodelete un profil Traffic Manager, utilisez hello `Remove-AzureRmTrafficManagerProfile` applet de commande, en spécifiant les noms de groupe de ressources et un profil de hello :</span><span class="sxs-lookup"><span data-stu-id="2b22f-271">toodelete a Traffic Manager profile, use hello `Remove-AzureRmTrafficManagerProfile` cmdlet, specifying hello profile and resource group names:</span></span>

```powershell
Remove-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG [-Force]
```

<span data-ttu-id="2b22f-272">Cette applet de commande vous demande de confirmer l’opération.</span><span class="sxs-lookup"><span data-stu-id="2b22f-272">This cmdlet prompts for confirmation.</span></span> <span data-ttu-id="2b22f-273">Ce message peut être supprimé à l’aide de hello '-Force' paramètre.</span><span class="sxs-lookup"><span data-stu-id="2b22f-273">This prompt can be suppressed using hello '-Force' parameter.</span></span>

<span data-ttu-id="2b22f-274">toobe de profil Hello supprimé peut également être spécifié à l’aide d’un objet de profil :</span><span class="sxs-lookup"><span data-stu-id="2b22f-274">hello profile toobe deleted can also be specified using a profile object:</span></span>

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG
Remove-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile [-Force]
```

<span data-ttu-id="2b22f-275">Cette séquence peut également être canalisée :</span><span class="sxs-lookup"><span data-stu-id="2b22f-275">This sequence can also be piped:</span></span>

```powershell
Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG | Remove-AzureRmTrafficManagerProfile [-Force]
```

## <a name="next-steps"></a><span data-ttu-id="2b22f-276">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2b22f-276">Next steps</span></span>

[<span data-ttu-id="2b22f-277">Surveillance avec Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="2b22f-277">Traffic Manager monitoring</span></span>](traffic-manager-monitoring.md)

[<span data-ttu-id="2b22f-278">Considérations sur les performances de Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="2b22f-278">Traffic Manager performance considerations</span></span>](traffic-manager-performance-considerations.md)
