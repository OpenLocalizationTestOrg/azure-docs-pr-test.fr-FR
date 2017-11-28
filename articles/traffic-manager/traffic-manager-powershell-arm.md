---
title: "Utilisation de PowerShell pour gérer Traffic Manager dans Azure | Microsoft Docs"
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
ms.openlocfilehash: 1cd7bd7e32c96398d72c7cd3b51e2b456d60f01d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="using-powershell-to-manage-traffic-manager"></a><span data-ttu-id="fe068-103">Utilisation de PowerShell pour gérer Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="fe068-103">Using PowerShell to manage Traffic Manager</span></span>

<span data-ttu-id="fe068-104">Azure Resource Manager est l’interface de gestion par défaut des services Azure.</span><span class="sxs-lookup"><span data-stu-id="fe068-104">Azure Resource Manager is the preferred management interface for services in Azure.</span></span> <span data-ttu-id="fe068-105">Les outils et API d’Azure Resource Manager permettent de gérer les profils Azure Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="fe068-105">Azure Traffic Manager profiles can be managed using Azure Resource Manager-based APIs and tools.</span></span>

## <a name="resource-model"></a><span data-ttu-id="fe068-106">Modèle de ressource</span><span class="sxs-lookup"><span data-stu-id="fe068-106">Resource model</span></span>

<span data-ttu-id="fe068-107">Azure Traffic Manager est configuré à l'aide d'un ensemble de paramètres appelé profil Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="fe068-107">Azure Traffic Manager is configured using a collection of settings called a Traffic Manager profile.</span></span> <span data-ttu-id="fe068-108">Ce profil contient les paramètres DNS, les paramètres de routage du trafic, les paramètres de surveillance des points de terminaison et la liste des points de terminaison de service vers lesquels le trafic est acheminé.</span><span class="sxs-lookup"><span data-stu-id="fe068-108">This profile contains DNS settings, traffic routing settings, endpoint monitoring settings, and a list of service endpoints to which traffic is routed.</span></span>

<span data-ttu-id="fe068-109">Chaque profil Traffic Manager est représenté par une ressource de type « TrafficManagerProfiles ».</span><span class="sxs-lookup"><span data-stu-id="fe068-109">Each Traffic Manager profile is represented by a resource of type 'TrafficManagerProfiles'.</span></span> <span data-ttu-id="fe068-110">Au niveau de l'API REST, l'URI de chaque profil est la suivante :</span><span class="sxs-lookup"><span data-stu-id="fe068-110">At the REST API level, the URI for each profile is as follows:</span></span>

    https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Network/trafficManagerProfiles/{profile-name}?api-version={api-version}

## <a name="setting-up-azure-powershell"></a><span data-ttu-id="fe068-111">Configuration d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="fe068-111">Setting up Azure PowerShell</span></span>

<span data-ttu-id="fe068-112">Ces instructions utilisent Microsoft Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fe068-112">These instructions use Microsoft Azure PowerShell.</span></span> <span data-ttu-id="fe068-113">L’article suivant explique comment installer et configurer Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fe068-113">The following article explains how to install and configure Azure PowerShell.</span></span>

* [<span data-ttu-id="fe068-114">Installation et configuration d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="fe068-114">How to install and configure Azure PowerShell</span></span>](/powershell/azure/overview)

<span data-ttu-id="fe068-115">Les exemples de cet article supposent que vous disposez déjà d’un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="fe068-115">The examples in this article assume that you have an existing resource group.</span></span> <span data-ttu-id="fe068-116">Vous pouvez en créer un à l’aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="fe068-116">You can create a resource group using the following command:</span></span>

```powershell
New-AzureRmResourceGroup -Name MyRG -Location "West US"
```

> [!NOTE]
> <span data-ttu-id="fe068-117">Azure Resource Manager exige des groupes de ressources qu’ils disposent tous d’un emplacement.</span><span class="sxs-lookup"><span data-stu-id="fe068-117">Azure Resource Manager requires that all resource groups have a location.</span></span> <span data-ttu-id="fe068-118">Celui-ci est utilisé comme emplacement par défaut pour les ressources créées dans ce groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="fe068-118">This location is used as the default for resources created in that resource group.</span></span> <span data-ttu-id="fe068-119">Cependant, étant donné que les ressources de profil Traffic Manager sont mondiales et non régionales, le choix de l’emplacement du groupe de ressources n’a aucune incidence sur Azure Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="fe068-119">However, since Traffic Manager profile resources are global, not regional, the choice of resource group location has no impact on Azure Traffic Manager.</span></span>

## <a name="create-a-traffic-manager-profile"></a><span data-ttu-id="fe068-120">Créer un profil Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="fe068-120">Create a Traffic Manager Profile</span></span>

<span data-ttu-id="fe068-121">Pour créer un profil Traffic Manager, utilisez l’applet de commande `New-AzureRmTrafficManagerProfile` :</span><span class="sxs-lookup"><span data-stu-id="fe068-121">To create a Traffic Manager profile, use the `New-AzureRmTrafficManagerProfile` cmdlet:</span></span>

```powershell
$profile = New-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName contoso -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
```

<span data-ttu-id="fe068-122">Le tableau suivant décrit les paramètres :</span><span class="sxs-lookup"><span data-stu-id="fe068-122">The following table describes the parameters:</span></span>

| <span data-ttu-id="fe068-123">Paramètre</span><span class="sxs-lookup"><span data-stu-id="fe068-123">Parameter</span></span> | <span data-ttu-id="fe068-124">Description</span><span class="sxs-lookup"><span data-stu-id="fe068-124">Description</span></span> |
| --- | --- |
| <span data-ttu-id="fe068-125">Name</span><span class="sxs-lookup"><span data-stu-id="fe068-125">Name</span></span> |<span data-ttu-id="fe068-126">Nom de la ressource de profil Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="fe068-126">The resource name for the Traffic Manager profile resource.</span></span> <span data-ttu-id="fe068-127">Les profils d’un même groupe de ressources doivent avoir un nom unique.</span><span class="sxs-lookup"><span data-stu-id="fe068-127">Profiles in the same resource group must have unique names.</span></span> <span data-ttu-id="fe068-128">Ce nom est différent du nom DNS utilisé pour les requêtes DNS.</span><span class="sxs-lookup"><span data-stu-id="fe068-128">This name is separate from the DNS name used for DNS queries.</span></span> |
| <span data-ttu-id="fe068-129">ResourceGroupName</span><span class="sxs-lookup"><span data-stu-id="fe068-129">ResourceGroupName</span></span> |<span data-ttu-id="fe068-130">Nom du groupe de ressources contenant la ressource de profil.</span><span class="sxs-lookup"><span data-stu-id="fe068-130">The name of the resource group containing the profile resource.</span></span> |
| <span data-ttu-id="fe068-131">TrafficRoutingMethod</span><span class="sxs-lookup"><span data-stu-id="fe068-131">TrafficRoutingMethod</span></span> |<span data-ttu-id="fe068-132">Spécifie la méthode de routage du trafic utilisée pour identifier le point de terminaison qui est retourné en réponse à une requête DNS.</span><span class="sxs-lookup"><span data-stu-id="fe068-132">Specifies the traffic-routing method used to determine which endpoint is returned in response a DNS query.</span></span> <span data-ttu-id="fe068-133">Les valeurs possibles sont « Performance », « Weighted » ou « Priority ».</span><span class="sxs-lookup"><span data-stu-id="fe068-133">Possible values are 'Performance', 'Weighted' or 'Priority'.</span></span> |
| <span data-ttu-id="fe068-134">RelativeDnsName</span><span class="sxs-lookup"><span data-stu-id="fe068-134">RelativeDnsName</span></span> |<span data-ttu-id="fe068-135">Spécifie la partie nom d’hôte du nom DNS fourni par ce profil Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="fe068-135">Specifies the hostname portion of the DNS name provided by this Traffic Manager profile.</span></span> <span data-ttu-id="fe068-136">Cette valeur est combinée au nom de domaine DNS utilisé par Azure Traffic Manager pour former le nom de domaine complet (FQDN) du profil.</span><span class="sxs-lookup"><span data-stu-id="fe068-136">This value is combined with the DNS domain name used by Azure Traffic Manager to form the fully qualified domain name (FQDN) of the profile.</span></span> <span data-ttu-id="fe068-137">Par exemple, la valeur définie « contoso » devient « contoso.trafficmanager.net ».</span><span class="sxs-lookup"><span data-stu-id="fe068-137">For example, setting the value of 'contoso' becomes 'contoso.trafficmanager.net.'</span></span> |
| <span data-ttu-id="fe068-138">TTL</span><span class="sxs-lookup"><span data-stu-id="fe068-138">TTL</span></span> |<span data-ttu-id="fe068-139">Spécifie la durée de vie (TTL) du DNS en secondes.</span><span class="sxs-lookup"><span data-stu-id="fe068-139">Specifies the DNS Time-to-Live (TTL), in seconds.</span></span> <span data-ttu-id="fe068-140">Ce paramètre indique aux programmes de résolution DNS locaux et aux clients DNS la durée de mise en cache des réponses DNS pour ce profil Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="fe068-140">This TTL informs the Local DNS resolvers and DNS clients how long to cache DNS responses for this Traffic Manager profile.</span></span> |
| <span data-ttu-id="fe068-141">MonitorProtocol</span><span class="sxs-lookup"><span data-stu-id="fe068-141">MonitorProtocol</span></span> |<span data-ttu-id="fe068-142">Spécifie le protocole à utiliser pour surveiller l’intégrité des points de terminaison.</span><span class="sxs-lookup"><span data-stu-id="fe068-142">Specifies the protocol to use to monitor endpoint health.</span></span> <span data-ttu-id="fe068-143">Les valeurs possibles sont « HTTP » et « HTTPS ».</span><span class="sxs-lookup"><span data-stu-id="fe068-143">Possible values are 'HTTP' and 'HTTPS'.</span></span> |
| <span data-ttu-id="fe068-144">MonitorPort</span><span class="sxs-lookup"><span data-stu-id="fe068-144">MonitorPort</span></span> |<span data-ttu-id="fe068-145">Spécifie le port TCP utilisé pour surveiller l’intégrité des points de terminaison.</span><span class="sxs-lookup"><span data-stu-id="fe068-145">Specifies the TCP port used to monitor endpoint health.</span></span> |
| <span data-ttu-id="fe068-146">MonitorPort</span><span class="sxs-lookup"><span data-stu-id="fe068-146">MonitorPath</span></span> |<span data-ttu-id="fe068-147">Spécifie le chemin relatif du nom de domaine de point de terminaison utilisé pour évaluer l’intégrité des points de terminaison.</span><span class="sxs-lookup"><span data-stu-id="fe068-147">Specifies the path relative to the endpoint domain name used to probe for endpoint health.</span></span> |

<span data-ttu-id="fe068-148">L’applet de commande crée un profil Traffic Manager dans Azure et retourne un objet de profil correspondant à PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fe068-148">The cmdlet creates a Traffic Manager profile in Azure and returns a corresponding profile object to PowerShell.</span></span> <span data-ttu-id="fe068-149">À ce stade, le profil ne contient aucun point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="fe068-149">At this point, the profile does not contain any endpoints.</span></span> <span data-ttu-id="fe068-150">Pour plus d’informations sur l’ajout de points de terminaison à un profil Traffic Manager, consultez [Ajout de points de terminaison Traffic Manager](#adding-traffic-manager-endpoints).</span><span class="sxs-lookup"><span data-stu-id="fe068-150">For more information about adding endpoints to a Traffic Manager profile, see [Adding Traffic Manager Endpoints](#adding-traffic-manager-endpoints).</span></span>

## <a name="get-a-traffic-manager-profile"></a><span data-ttu-id="fe068-151">Récupérer un profil Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="fe068-151">Get a Traffic Manager Profile</span></span>

<span data-ttu-id="fe068-152">Pour récupérer un objet de profil Traffic Manager existant, utilisez l’applet de commande `Get-AzureRmTrafficManagerProfle` :</span><span class="sxs-lookup"><span data-stu-id="fe068-152">To retrieve an existing Traffic Manager profile object, use the `Get-AzureRmTrafficManagerProfle` cmdlet:</span></span>

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG
```

<span data-ttu-id="fe068-153">Cette applet de commande renvoie un objet de profil Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="fe068-153">This cmdlet returns a Traffic Manager profile object.</span></span>

## <a name="update-a-traffic-manager-profile"></a><span data-ttu-id="fe068-154">Mettre à jour un profil Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="fe068-154">Update a Traffic Manager Profile</span></span>

<span data-ttu-id="fe068-155">La modification des profils Traffic Manager est un processus en 3 étapes :</span><span class="sxs-lookup"><span data-stu-id="fe068-155">Modifying Traffic Manager profiles follows a 3-step process:</span></span>

1. <span data-ttu-id="fe068-156">Récupérez le profil à l’aide de `Get-AzureRmTrafficManagerProfile` ou utilisez le profil retourné par `New-AzureRmTrafficManagerProfile`.</span><span class="sxs-lookup"><span data-stu-id="fe068-156">Retrieve the profile using `Get-AzureRmTrafficManagerProfile` or use the profile returned by `New-AzureRmTrafficManagerProfile`.</span></span>
2. <span data-ttu-id="fe068-157">Modifiez le profil.</span><span class="sxs-lookup"><span data-stu-id="fe068-157">Modify the profile.</span></span> <span data-ttu-id="fe068-158">Vous pouvez ajouter et supprimer des points de terminaison ou modifier les paramètres des points de terminaison ou du profil.</span><span class="sxs-lookup"><span data-stu-id="fe068-158">You can add and remove endpoints or change endpoint or profile parameters.</span></span> <span data-ttu-id="fe068-159">Ces modifications sont des opérations hors connexion.</span><span class="sxs-lookup"><span data-stu-id="fe068-159">These changes are off-line operations.</span></span> <span data-ttu-id="fe068-160">Vous modifiez seulement l’objet local en mémoire qui représente le profil.</span><span class="sxs-lookup"><span data-stu-id="fe068-160">You are only changing the local object in memory that represents the profile.</span></span>
3. <span data-ttu-id="fe068-161">Validez vos modifications à l’aide de l’applet de commande `Set-AzureRmTrafficManagerProfile`.</span><span class="sxs-lookup"><span data-stu-id="fe068-161">Commit your changes using the `Set-AzureRmTrafficManagerProfile` cmdlet.</span></span>

<span data-ttu-id="fe068-162">Toutes les propriétés de profil peuvent être modifiées à l’exception de RelativeDnsName.</span><span class="sxs-lookup"><span data-stu-id="fe068-162">All profile properties can be changed except the profile's RelativeDnsName.</span></span> <span data-ttu-id="fe068-163">Pour modifier la propriété RelativeDnsName, vous devez supprimer le profil et en créer un sous un nouveau nom.</span><span class="sxs-lookup"><span data-stu-id="fe068-163">To change the RelativeDnsName, you must delete profile and a new profile with a new name.</span></span>

<span data-ttu-id="fe068-164">L’exemple suivant montre comment modifier la durée de vie (TTL) du profil :</span><span class="sxs-lookup"><span data-stu-id="fe068-164">The following example demonstrates how to change the profile's TTL:</span></span>

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG
$profile.Ttl = 300
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

<span data-ttu-id="fe068-165">Il existe trois types de points de terminaison Traffic Manager :</span><span class="sxs-lookup"><span data-stu-id="fe068-165">There are three types of Traffic Manager endpoints:</span></span>

1. <span data-ttu-id="fe068-166">Les **points de terminaison Azure** sont des services hébergés dans Azure.</span><span class="sxs-lookup"><span data-stu-id="fe068-166">**Azure endpoints** are services hosted in Azure</span></span>
2. <span data-ttu-id="fe068-167">Les **points de terminaison externes** sont des services hébergés en dehors d’Azure.</span><span class="sxs-lookup"><span data-stu-id="fe068-167">**External endpoints** are services hosted outside of Azure</span></span>
3. <span data-ttu-id="fe068-168">Les **points de terminaison imbriqués** servent à construire des hiérarchies imbriquées de profils Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="fe068-168">**Nested endpoints** are used to construct nested hierarchies of Traffic Manager profiles.</span></span> <span data-ttu-id="fe068-169">Ils permettent de définir des configurations de routage du trafic avancées pour les applications complexes.</span><span class="sxs-lookup"><span data-stu-id="fe068-169">Nested endpoints enable advanced traffic-routing configurations for complex applications.</span></span>

<span data-ttu-id="fe068-170">Dans ces trois cas, les points de terminaison peuvent être ajoutés de deux manières :</span><span class="sxs-lookup"><span data-stu-id="fe068-170">In all three cases, endpoints can be added in two ways:</span></span>

1. <span data-ttu-id="fe068-171">En suivant le processus en 3 étapes décrit précédemment.</span><span class="sxs-lookup"><span data-stu-id="fe068-171">Using a 3-step process described previously.</span></span> <span data-ttu-id="fe068-172">L’avantage de cette méthode est que plusieurs modifications de point de terminaison peuvent être apportées en une seule mise à jour.</span><span class="sxs-lookup"><span data-stu-id="fe068-172">The advantage of this method is that several endpoint changes can be made in a single update.</span></span>
2. <span data-ttu-id="fe068-173">En utilisant l’applet de commande New-AzureRmTrafficManagerEndpoint.</span><span class="sxs-lookup"><span data-stu-id="fe068-173">Using the New-AzureRmTrafficManagerEndpoint cmdlet.</span></span> <span data-ttu-id="fe068-174">Celle-ci permet d’ajouter un point de terminaison à un profil Traffic Manager existant en une seule opération.</span><span class="sxs-lookup"><span data-stu-id="fe068-174">This cmdlet adds an endpoint to an existing Traffic Manager profile in a single operation.</span></span>

## <a name="adding-azure-endpoints"></a><span data-ttu-id="fe068-175">Ajout de points de terminaison Azure</span><span class="sxs-lookup"><span data-stu-id="fe068-175">Adding Azure Endpoints</span></span>

<span data-ttu-id="fe068-176">Les points de terminaison Azure font référence à des services hébergés dans Azure.</span><span class="sxs-lookup"><span data-stu-id="fe068-176">Azure endpoints reference services hosted in Azure.</span></span> <span data-ttu-id="fe068-177">Les types de point de terminaison Azure pris en charge sont au nombre de deux :</span><span class="sxs-lookup"><span data-stu-id="fe068-177">Two types of Azure endpoints are supported:</span></span>

1. <span data-ttu-id="fe068-178">Azure Web Apps </span><span class="sxs-lookup"><span data-stu-id="fe068-178">Azure Web Apps</span></span>
2. <span data-ttu-id="fe068-179">Ressources PublicIpAddress Azure (peuvent être attachées à un équilibreur de charge ou à une carte réseau de machine virtuelle).</span><span class="sxs-lookup"><span data-stu-id="fe068-179">Azure PublicIpAddress resources (which can be attached to a load-balancer or a virtual machine NIC).</span></span> <span data-ttu-id="fe068-180">PublicIpAddress doit se voir affecter un nom DNS pour être utilisé dans Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="fe068-180">The PublicIpAddress must have a DNS name assigned to be used in Traffic Manager.</span></span>

<span data-ttu-id="fe068-181">Dans chaque cas :</span><span class="sxs-lookup"><span data-stu-id="fe068-181">In each case:</span></span>

* <span data-ttu-id="fe068-182">Le service est spécifié à l’aide du paramètre « targetResourceId » de `Add-AzureRmTrafficManagerEndpointConfig` ou `New-AzureRmTrafficManagerEndpoint`.</span><span class="sxs-lookup"><span data-stu-id="fe068-182">The service is specified using the 'targetResourceId' parameter of `Add-AzureRmTrafficManagerEndpointConfig` or `New-AzureRmTrafficManagerEndpoint`.</span></span>
* <span data-ttu-id="fe068-183">« Target » et « EndpointLocation » sont définis implicitement selon TargetResourceId.</span><span class="sxs-lookup"><span data-stu-id="fe068-183">The 'Target' and 'EndpointLocation' are implied by the TargetResourceId.</span></span>
* <span data-ttu-id="fe068-184">La spécification du paramètre « Pondération » est facultative.</span><span class="sxs-lookup"><span data-stu-id="fe068-184">Specifying the 'Weight' is optional.</span></span> <span data-ttu-id="fe068-185">Les pondérations ne sont utilisées que si le profil est configuré pour utiliser la méthode de routage du trafic « Weighted ».</span><span class="sxs-lookup"><span data-stu-id="fe068-185">Weights are only used if the profile is configured to use the 'Weighted' traffic-routing method.</span></span> <span data-ttu-id="fe068-186">Autrement, elles sont ignorées.</span><span class="sxs-lookup"><span data-stu-id="fe068-186">Otherwise, they are ignored.</span></span> <span data-ttu-id="fe068-187">S’il est spécifié, le paramètre doit avoir une valeur numérique comprise entre 1 et 1 000.</span><span class="sxs-lookup"><span data-stu-id="fe068-187">If specified, the value must be a number between 1 and 1000.</span></span> <span data-ttu-id="fe068-188">La valeur par défaut est « 1 ».</span><span class="sxs-lookup"><span data-stu-id="fe068-188">The default value is '1'.</span></span>
* <span data-ttu-id="fe068-189">La spécification du paramètre « Priorité » est facultative.</span><span class="sxs-lookup"><span data-stu-id="fe068-189">Specifying the 'Priority' is optional.</span></span> <span data-ttu-id="fe068-190">Les priorités ne sont utilisées que si le profil est configuré pour utiliser la méthode d’acheminement de trafic « Priority ».</span><span class="sxs-lookup"><span data-stu-id="fe068-190">Priorities are only used if the profile is configured to use the 'Priority' traffic-routing method.</span></span> <span data-ttu-id="fe068-191">Autrement, elles sont ignorées.</span><span class="sxs-lookup"><span data-stu-id="fe068-191">Otherwise, they are ignored.</span></span> <span data-ttu-id="fe068-192">Les valeurs valides vont de 1 à 1 000, les valeurs basses indiquant une priorité élevée.</span><span class="sxs-lookup"><span data-stu-id="fe068-192">Valid values are from 1 to 1000 with lower values indicating a higher priority.</span></span> <span data-ttu-id="fe068-193">Si elles sont spécifiées pour un point de terminaison, elles doivent l’être pour tous les points de terminaison.</span><span class="sxs-lookup"><span data-stu-id="fe068-193">If specified for one endpoint, they must be specified for all endpoints.</span></span> <span data-ttu-id="fe068-194">En cas d’omission, les valeurs par défaut à partir de « 1 » sont appliquées dans l’ordre où les points de terminaison sont répertoriés.</span><span class="sxs-lookup"><span data-stu-id="fe068-194">If omitted, default values starting from '1' are applied in the order that the endpoints are listed.</span></span>

### <a name="example-1-adding-web-app-endpoints-using-add-azurermtrafficmanagerendpointconfig"></a><span data-ttu-id="fe068-195">Exemple 1 : ajout de points de terminaison d’application web à l’aide de `Add-AzureRmTrafficManagerEndpointConfig`</span><span class="sxs-lookup"><span data-stu-id="fe068-195">Example 1: Adding Web App endpoints using `Add-AzureRmTrafficManagerEndpointConfig`</span></span>

<span data-ttu-id="fe068-196">Dans cet exemple, nous créons un profil Traffic Manager et ajoutons deux points de terminaison d’application web à l’aide de l’applet de commande `Add-AzureRmTrafficManagerEndpointConfig`.</span><span class="sxs-lookup"><span data-stu-id="fe068-196">In this example, we create a Traffic Manager profile and add two Web App endpoints using the `Add-AzureRmTrafficManagerEndpointConfig` cmdlet.</span></span>

```powershell
$profile = New-AzureRmTrafficManagerProfile -Name myprofile -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName myapp -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
$webapp1 = Get-AzureRMWebApp -Name webapp1
Add-AzureRmTrafficManagerEndpointConfig -EndpointName webapp1ep -TrafficManagerProfile $profile -Type AzureEndpoints -TargetResourceId $webapp1.Id -EndpointStatus Enabled
$webapp2 = Get-AzureRMWebApp -Name webapp2
Add-AzureRmTrafficManagerEndpointConfig -EndpointName webapp2ep -TrafficManagerProfile $profile -Type AzureEndpoints -TargetResourceId $webapp2.Id -EndpointStatus Enabled
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```
### <a name="example-2-adding-a-publicipaddress-endpoint-using-new-azurermtrafficmanagerendpoint"></a><span data-ttu-id="fe068-197">Exemple 2 : ajout d’un point de terminaison publicIpAddress à l’aide de `New-AzureRmTrafficManagerEndpoint`</span><span class="sxs-lookup"><span data-stu-id="fe068-197">Example 2: Adding a publicIpAddress endpoint using `New-AzureRmTrafficManagerEndpoint`</span></span>

<span data-ttu-id="fe068-198">Dans cet exemple, une ressource d’adresse IP publique est ajoutée au profil Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="fe068-198">In this example, a public IP address resource is added to the Traffic Manager profile.</span></span> <span data-ttu-id="fe068-199">L’adresse IP publique doit avoir un nom DNS configuré et peut être liée à la carte réseau d’une machine virtuelle ou à un équilibreur de charge.</span><span class="sxs-lookup"><span data-stu-id="fe068-199">The public IP address must have a DNS name configured, and can be bound either to the NIC of a VM or to a load balancer.</span></span>

```powershell
$ip = Get-AzureRmPublicIpAddress -Name MyPublicIP -ResourceGroupName MyRG
New-AzureRmTrafficManagerEndpoint -Name MyIpEndpoint -ProfileName MyProfile -ResourceGroupName MyRG -Type AzureEndpoints -TargetResourceId $ip.Id -EndpointStatus Enabled
```

## <a name="adding-external-endpoints"></a><span data-ttu-id="fe068-200">Ajout de points de terminaison externes</span><span class="sxs-lookup"><span data-stu-id="fe068-200">Adding External Endpoints</span></span>

<span data-ttu-id="fe068-201">Traffic Manager utilise les points de terminaison externes pour diriger le trafic vers les services hébergés en dehors d’Azure.</span><span class="sxs-lookup"><span data-stu-id="fe068-201">Traffic Manager uses external endpoints to direct traffic to services hosted outside of Azure.</span></span> <span data-ttu-id="fe068-202">Comme les points de terminaison Azure, les points de terminaison externes peuvent être ajoutés à l’aide de `Add-AzureRmTrafficManagerEndpointConfig` suivi de `Set-AzureRmTrafficManagerProfile`, ou avec `New-AzureRMTrafficManagerEndpoint`.</span><span class="sxs-lookup"><span data-stu-id="fe068-202">As with Azure endpoints, external endpoints can be added either using `Add-AzureRmTrafficManagerEndpointConfig` followed by `Set-AzureRmTrafficManagerProfile`, or `New-AzureRMTrafficManagerEndpoint`.</span></span>

<span data-ttu-id="fe068-203">Lors de la spécification de points de terminaison externes :</span><span class="sxs-lookup"><span data-stu-id="fe068-203">When specifying external endpoints:</span></span>

* <span data-ttu-id="fe068-204">Le nom de domaine du point de terminaison doit être spécifié en utilisant le paramètre « Target »</span><span class="sxs-lookup"><span data-stu-id="fe068-204">The endpoint domain name must be specified using the 'Target' parameter</span></span>
* <span data-ttu-id="fe068-205">Si la méthode de routage du trafic « Performance » est utilisée, le paramètre « EndpointLocation » doit être renseigné.</span><span class="sxs-lookup"><span data-stu-id="fe068-205">If the 'Performance' traffic-routing method is used, the 'EndpointLocation' is required.</span></span> <span data-ttu-id="fe068-206">Sinon, il est facultatif.</span><span class="sxs-lookup"><span data-stu-id="fe068-206">Otherwise it is optional.</span></span> <span data-ttu-id="fe068-207">La valeur doit être un [nom de région Azure valide](https://azure.microsoft.com/regions/).</span><span class="sxs-lookup"><span data-stu-id="fe068-207">The value must be a [valid Azure region name](https://azure.microsoft.com/regions/).</span></span>
* <span data-ttu-id="fe068-208">Les paramètres « Weight » et « Priority » sont facultatifs.</span><span class="sxs-lookup"><span data-stu-id="fe068-208">The 'Weight' and 'Priority' are optional.</span></span>

### <a name="example-1-adding-external-endpoints-using-add-azurermtrafficmanagerendpointconfig-and-set-azurermtrafficmanagerprofile"></a><span data-ttu-id="fe068-209">Exemple 1 : ajout de points de terminaison externes à l’aide de `Add-AzureRmTrafficManagerEndpointConfig` et `Set-AzureRmTrafficManagerProfile`</span><span class="sxs-lookup"><span data-stu-id="fe068-209">Example 1: Adding external endpoints using `Add-AzureRmTrafficManagerEndpointConfig` and `Set-AzureRmTrafficManagerProfile`</span></span>

<span data-ttu-id="fe068-210">Dans cet exemple, nous créons un profil Traffic Manager, ajoutons deux points de terminaison externes et validons les modifications.</span><span class="sxs-lookup"><span data-stu-id="fe068-210">In this example, we create a Traffic Manager profile, add two external endpoints, and commit the changes.</span></span>

```powershell
$profile = New-AzureRmTrafficManagerProfile -Name myprofile -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName myapp -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
Add-AzureRmTrafficManagerEndpointConfig -EndpointName eu-endpoint -TrafficManagerProfile $profile -Type ExternalEndpoints -Target app-eu.contoso.com -EndpointLocation "North Europe" -EndpointStatus Enabled
Add-AzureRmTrafficManagerEndpointConfig -EndpointName us-endpoint -TrafficManagerProfile $profile -Type ExternalEndpoints -Target app-us.contoso.com -EndpointLocation "Central US" -EndpointStatus Enabled
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

### <a name="example-2-adding-external-endpoints-using-new-azurermtrafficmanagerendpoint"></a><span data-ttu-id="fe068-211">Exemple 2 : ajout de points de terminaison externes à l’aide de `New-AzureRmTrafficManagerEndpoint`</span><span class="sxs-lookup"><span data-stu-id="fe068-211">Example 2: Adding external endpoints using `New-AzureRmTrafficManagerEndpoint`</span></span>

<span data-ttu-id="fe068-212">Dans cet exemple, nous ajoutons un point de terminaison externe à un profil existant.</span><span class="sxs-lookup"><span data-stu-id="fe068-212">In this example, we add an external endpoint to an existing profile.</span></span> <span data-ttu-id="fe068-213">Le profil est spécifié en utilisant les noms de profil et de groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="fe068-213">The profile is specified using the profile and resource group names.</span></span>

```powershell
New-AzureRmTrafficManagerEndpoint -Name eu-endpoint -ProfileName MyProfile -ResourceGroupName MyRG -Type ExternalEndpoints -Target app-eu.contoso.com -EndpointStatus Enabled
```

## <a name="adding-nested-endpoints"></a><span data-ttu-id="fe068-214">Ajout de points de terminaison « imbriqués »</span><span class="sxs-lookup"><span data-stu-id="fe068-214">Adding 'Nested' endpoints</span></span>

<span data-ttu-id="fe068-215">Chaque profil Traffic Manager spécifie une seule méthode de routage du trafic.</span><span class="sxs-lookup"><span data-stu-id="fe068-215">Each Traffic Manager profile specifies a single traffic-routing method.</span></span> <span data-ttu-id="fe068-216">Cependant, certains scénarios exigent une méthode de routage du trafic plus sophistiquée que celle proposée par un profil Traffic Manager unique.</span><span class="sxs-lookup"><span data-stu-id="fe068-216">However, there are scenarios that require more sophisticated traffic routing than the routing provided by a single Traffic Manager profile.</span></span> <span data-ttu-id="fe068-217">Vous pouvez imbriquer des profils Traffic Manager pour combiner les avantages de plusieurs méthodes de routage du trafic.</span><span class="sxs-lookup"><span data-stu-id="fe068-217">You can nest Traffic Manager profiles to combine the benefits of more than one traffic-routing method.</span></span> <span data-ttu-id="fe068-218">Les profils imbriqués permettent de modifier le comportement par défaut de Traffic Manager pour prendre en charge des déploiements d’applications plus importants et plus complexes.</span><span class="sxs-lookup"><span data-stu-id="fe068-218">Nested profiles allow you to override the default Traffic Manager behavior to support larger and more complex application deployments.</span></span> <span data-ttu-id="fe068-219">Pour obtenir des informations plus détaillées, consultez [Profils Traffic Manager imbriqués](traffic-manager-nested-profiles.md).</span><span class="sxs-lookup"><span data-stu-id="fe068-219">For more detailed examples, see [Nested Traffic Manager profiles](traffic-manager-nested-profiles.md).</span></span>

<span data-ttu-id="fe068-220">Les points de terminaison imbriqués sont configurés sur le profil parent, à l’aide d’un type de point de terminaison spécifique, « NestedEndpoints ».</span><span class="sxs-lookup"><span data-stu-id="fe068-220">Nested endpoints are configured at the parent profile, using a specific endpoint type, 'NestedEndpoints'.</span></span> <span data-ttu-id="fe068-221">Lors de la spécification de points de terminaison imbriqués :</span><span class="sxs-lookup"><span data-stu-id="fe068-221">When specifying nested endpoints:</span></span>

* <span data-ttu-id="fe068-222">Le point de terminaison doit être spécifié à l’aide du paramètre « targetResourceId ».</span><span class="sxs-lookup"><span data-stu-id="fe068-222">The endpoint must be specified using the 'targetResourceId' parameter</span></span>
* <span data-ttu-id="fe068-223">Si la méthode de routage du trafic « Performance » est utilisée, le paramètre « EndpointLocation » doit être renseigné.</span><span class="sxs-lookup"><span data-stu-id="fe068-223">If the 'Performance' traffic-routing method is used, the 'EndpointLocation' is required.</span></span> <span data-ttu-id="fe068-224">Sinon, il est facultatif.</span><span class="sxs-lookup"><span data-stu-id="fe068-224">Otherwise it is optional.</span></span> <span data-ttu-id="fe068-225">La valeur doit être un [nom de région Azure valide](http://azure.microsoft.com/regions/).</span><span class="sxs-lookup"><span data-stu-id="fe068-225">The value must be a [valid Azure region name](http://azure.microsoft.com/regions/).</span></span>
* <span data-ttu-id="fe068-226">Les paramètres « Pondération » et « Priorité » sont facultatifs, comme pour les points de terminaison Azure.</span><span class="sxs-lookup"><span data-stu-id="fe068-226">The 'Weight' and 'Priority' are optional, as for Azure endpoints.</span></span>
* <span data-ttu-id="fe068-227">Le paramètre « MinChildEndpoints » est facultatif.</span><span class="sxs-lookup"><span data-stu-id="fe068-227">The 'MinChildEndpoints' parameter is optional.</span></span> <span data-ttu-id="fe068-228">La valeur par défaut est « 1 ».</span><span class="sxs-lookup"><span data-stu-id="fe068-228">The default value is '1'.</span></span> <span data-ttu-id="fe068-229">Si le nombre de points de terminaison disponibles tombe sous ce seuil, le profil parent considère le profil enfant comme étant « dégradé » et dirige le trafic vers les autres points de terminaison du profil parent.</span><span class="sxs-lookup"><span data-stu-id="fe068-229">If the number of available endpoints falls below this threshold, the parent profile considers the child profile 'degraded' and diverts traffic to the other endpoints in the parent profile.</span></span>

### <a name="example-1-adding-nested-endpoints-using-add-azurermtrafficmanagerendpointconfig-and-set-azurermtrafficmanagerprofile"></a><span data-ttu-id="fe068-230">Exemple 1 : ajout de points de terminaison imbriqués à l’aide de `Add-AzureRmTrafficManagerEndpointConfig` et `Set-AzureRmTrafficManagerProfile`</span><span class="sxs-lookup"><span data-stu-id="fe068-230">Example 1: Adding nested endpoints using `Add-AzureRmTrafficManagerEndpointConfig` and `Set-AzureRmTrafficManagerProfile`</span></span>

<span data-ttu-id="fe068-231">Dans cet exemple, nous créons des profils Traffic Manager enfant et parent, ajoutons l’enfant en tant que point de terminaison imbriqué au parent et validons les modifications.</span><span class="sxs-lookup"><span data-stu-id="fe068-231">In this example, we create new Traffic Manager child and parent profiles, add the child as a nested endpoint to the parent, and commit the changes.</span></span>

```powershell
$child = New-AzureRmTrafficManagerProfile -Name child -ResourceGroupName MyRG -TrafficRoutingMethod Priority -RelativeDnsName child -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
$parent = New-AzureRmTrafficManagerProfile -Name parent -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName parent -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
Add-AzureRmTrafficManagerEndpointConfig -EndpointName child-endpoint -TrafficManagerProfile $parent -Type NestedEndpoints -TargetResourceId $child.Id -EndpointStatus Enabled -EndpointLocation "North Europe" -MinChildEndpoints 2
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

<span data-ttu-id="fe068-232">Par souci de concision, dans cet exemple, nous n’avons pas ajouté d’autres points de terminaison aux profils enfant ou parent.</span><span class="sxs-lookup"><span data-stu-id="fe068-232">For brevity in this example, we did not add any other endpoints to the child or parent profiles.</span></span>

### <a name="example-2-adding-nested-endpoints-using-new-azurermtrafficmanagerendpoint"></a><span data-ttu-id="fe068-233">Exemple 2 : ajout de points de terminaison imbriqués à l’aide de `New-AzureRmTrafficManagerEndpoint`</span><span class="sxs-lookup"><span data-stu-id="fe068-233">Example 2: Adding nested endpoints using `New-AzureRmTrafficManagerEndpoint`</span></span>

<span data-ttu-id="fe068-234">Dans cet exemple, nous ajoutons un profil enfant existant en tant que point de terminaison imbriqué à un profil parent existant.</span><span class="sxs-lookup"><span data-stu-id="fe068-234">In this example, we add an existing child profile as a nested endpoint to an existing parent profile.</span></span> <span data-ttu-id="fe068-235">Le profil est spécifié en utilisant les noms de profil et de groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="fe068-235">The profile is specified using the profile and resource group names.</span></span>

```powershell
$child = Get-AzureRmTrafficManagerEndpoint -Name child -ResourceGroupName MyRG
New-AzureRmTrafficManagerEndpoint -Name child-endpoint -ProfileName parent -ResourceGroupName MyRG -Type NestedEndpoints -TargetResourceId $child.Id -EndpointStatus Enabled -EndpointLocation "North Europe" -MinChildEndpoints 2
```

## <a name="update-a-traffic-manager-endpoint"></a><span data-ttu-id="fe068-236">Mettre à jour un point de terminaison Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="fe068-236">Update a Traffic Manager Endpoint</span></span>

<span data-ttu-id="fe068-237">Il existe deux façons de mettre à jour un point de terminaison Traffic Manager existant :</span><span class="sxs-lookup"><span data-stu-id="fe068-237">There are two ways to update an existing Traffic Manager endpoint:</span></span>

1. <span data-ttu-id="fe068-238">Obtenir le profil Traffic Manager à l’aide de `Get-AzureRmTrafficManagerProfile`, mettre à jour les propriétés de point de terminaison dans le profil et valider les modifications apportées à l’aide de `Set-AzureRmTrafficManagerProfile`.</span><span class="sxs-lookup"><span data-stu-id="fe068-238">Get the Traffic Manager profile using `Get-AzureRmTrafficManagerProfile`, update the endpoint properties within the profile, and commit the changes using `Set-AzureRmTrafficManagerProfile`.</span></span> <span data-ttu-id="fe068-239">Cette méthode présente l’avantage de pouvoir mettre à jour plusieurs points de terminaison en une seule opération.</span><span class="sxs-lookup"><span data-stu-id="fe068-239">This method has the advantage of being able to update more than one endpoint in a single operation.</span></span>
2. <span data-ttu-id="fe068-240">Obtenir le point de terminaison Traffic Manager à l’aide de `Get-AzureRmTrafficManagerEndpoint`, mettre à jour les propriétés de point de terminaison et valider les modifications apportées à l’aide de `Set-AzureRmTrafficManagerEndpoint`.</span><span class="sxs-lookup"><span data-stu-id="fe068-240">Get the Traffic Manager endpoint using `Get-AzureRmTrafficManagerEndpoint`, update the endpoint properties, and commit the changes using `Set-AzureRmTrafficManagerEndpoint`.</span></span> <span data-ttu-id="fe068-241">Cette méthode est plus simple, car elle ne nécessite pas d’indexation dans le tableau de points de terminaison dans le profil.</span><span class="sxs-lookup"><span data-stu-id="fe068-241">This method is simpler, since it does not require indexing into the Endpoints array in the profile.</span></span>

### <a name="example-1-updating-endpoints-using-get-azurermtrafficmanagerprofile-and-set-azurermtrafficmanagerprofile"></a><span data-ttu-id="fe068-242">Exemple 1 : mise à jour des points de terminaison à l’aide de `Get-AzureRmTrafficManagerProfile` et `Set-AzureRmTrafficManagerProfile`</span><span class="sxs-lookup"><span data-stu-id="fe068-242">Example 1: Updating endpoints using `Get-AzureRmTrafficManagerProfile` and `Set-AzureRmTrafficManagerProfile`</span></span>

<span data-ttu-id="fe068-243">Dans cet exemple, nous modifions l’ordre de priorité de deux points de terminaison dans un profil existant.</span><span class="sxs-lookup"><span data-stu-id="fe068-243">In this example, we modify the priority on two endpoints within an existing profile.</span></span>

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name myprofile -ResourceGroupName MyRG
$profile.Endpoints[0].Priority = 2
$profile.Endpoints[1].Priority = 1
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

### <a name="example-2-updating-an-endpoint-using-get-azurermtrafficmanagerendpoint-and-set-azurermtrafficmanagerendpoint"></a><span data-ttu-id="fe068-244">Exemple 2 : mise à jour d’un point de terminaison à l’aide de `Get-AzureRmTrafficManagerEndpoint` et `Set-AzureRmTrafficManagerEndpoint`</span><span class="sxs-lookup"><span data-stu-id="fe068-244">Example 2: Updating an endpoint using `Get-AzureRmTrafficManagerEndpoint` and `Set-AzureRmTrafficManagerEndpoint`</span></span>

<span data-ttu-id="fe068-245">Dans cet exemple, nous modifions le poids d’un point de terminaison unique dans un profil existant.</span><span class="sxs-lookup"><span data-stu-id="fe068-245">In this example, we modify the weight of a single endpoint in an existing profile.</span></span>

```powershell
$endpoint = Get-AzureRmTrafficManagerEndpoint -Name myendpoint -ProfileName myprofile -ResourceGroupName MyRG -Type ExternalEndpoints
$endpoint.Weight = 20
Set-AzureRmTrafficManagerEndpoint -TrafficManagerEndpoint $endpoint
```

## <a name="enabling-and-disabling-endpoints-and-profiles"></a><span data-ttu-id="fe068-246">Activation et désactivation des points de terminaison et des profils</span><span class="sxs-lookup"><span data-stu-id="fe068-246">Enabling and Disabling Endpoints and Profiles</span></span>

<span data-ttu-id="fe068-247">Traffic Manager permet d’activer et de désactiver des points de terminaison individuels, tout en permettant l’activation et la désactivation des profils complets.</span><span class="sxs-lookup"><span data-stu-id="fe068-247">Traffic Manager allows individual endpoints to be enabled and disabled, as well as allowing enabling and disabling of entire profiles.</span></span>
<span data-ttu-id="fe068-248">Ces modifications peuvent être effectuées par obtention/mise à jour/définition du point de terminaison ou de ressources de profil.</span><span class="sxs-lookup"><span data-stu-id="fe068-248">These changes can be made by getting/updating/setting the endpoint or profile resources.</span></span> <span data-ttu-id="fe068-249">Pour rationaliser les opérations courantes, elles sont également prises en charge via les applets de commande dédiées.</span><span class="sxs-lookup"><span data-stu-id="fe068-249">To streamline these common operations, they are also supported via dedicated cmdlets.</span></span>

### <a name="example-1-enabling-and-disabling-a-traffic-manager-profile"></a><span data-ttu-id="fe068-250">Exemple 1 : activation et désactivation d’un profil Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="fe068-250">Example 1: Enabling and disabling a Traffic Manager profile</span></span>

<span data-ttu-id="fe068-251">Pour activer un profil Traffic Manager, utilisez `Enable-AzureRmTrafficManagerProfile`.</span><span class="sxs-lookup"><span data-stu-id="fe068-251">To enable a Traffic Manager profile, use `Enable-AzureRmTrafficManagerProfile`.</span></span> <span data-ttu-id="fe068-252">Le profil peut être spécifié à l’aide d’un objet de profil.</span><span class="sxs-lookup"><span data-stu-id="fe068-252">The profile can be specified using a profile object.</span></span> <span data-ttu-id="fe068-253">L’objet de profil peut être transmis via le pipeline ou en utilisant le paramètre « -TrafficManagerProfile ».</span><span class="sxs-lookup"><span data-stu-id="fe068-253">The profile object can be passed via the pipeline or by using the '-TrafficManagerProfile' parameter.</span></span> <span data-ttu-id="fe068-254">Dans cet exemple, nous spécifions le profil avec le nom de profil et le nom de groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="fe068-254">In this example, we specify the profile by the profile and resource group name.</span></span>

```powershell
Enable-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyResourceGroup
```

<span data-ttu-id="fe068-255">Pour désactiver un profil Traffic Manager :</span><span class="sxs-lookup"><span data-stu-id="fe068-255">To disable a Traffic Manager profile:</span></span>

```powershell
Disable-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyResourceGroup
```

<span data-ttu-id="fe068-256">L’applet de commande Disable-AzureRmTrafficManagerProfile vous demande de confirmer l’opération.</span><span class="sxs-lookup"><span data-stu-id="fe068-256">The Disable-AzureRmTrafficManagerProfile cmdlet prompts for confirmation.</span></span> <span data-ttu-id="fe068-257">Ce message peut être supprimé en utilisant le paramètre « -Force ».</span><span class="sxs-lookup"><span data-stu-id="fe068-257">This prompt can be suppressed using the '-Force' parameter.</span></span>

### <a name="example-2-enabling-and-disabling-a-traffic-manager-endpoint"></a><span data-ttu-id="fe068-258">Exemple 2 : activation et désactivation d’un point de terminaison Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="fe068-258">Example 2: Enabling and disabling a Traffic Manager endpoint</span></span>

<span data-ttu-id="fe068-259">Pour activer un point de terminaison Traffic Manager, utilisez `Enable-AzureRmTrafficManagerEndpoint`.</span><span class="sxs-lookup"><span data-stu-id="fe068-259">To enable a Traffic Manager endpoint, use `Enable-AzureRmTrafficManagerEndpoint`.</span></span> <span data-ttu-id="fe068-260">Il existe deux façons de spécifier le point de terminaison :</span><span class="sxs-lookup"><span data-stu-id="fe068-260">There are two ways to specify the endpoint</span></span>

1. <span data-ttu-id="fe068-261">en utilisant un objet TrafficManagerEndpoint, qui est transmis via le pipeline ou en utilisant le paramètre « -TrafficManagerEndpoint » ;</span><span class="sxs-lookup"><span data-stu-id="fe068-261">Using a TrafficManagerEndpoint object passed via the pipeline or using the '-TrafficManagerEndpoint' parameter</span></span>
2. <span data-ttu-id="fe068-262">en utilisant le nom du point de terminaison, le type du point de terminaison, le nom du profil et le nom du groupe de ressources :</span><span class="sxs-lookup"><span data-stu-id="fe068-262">Using the endpoint name, endpoint type, profile name, and resource group name:</span></span>

```powershell
Enable-AzureRmTrafficManagerEndpoint -Name MyEndpoint -Type AzureEndpoints -ProfileName MyProfile -ResourceGroupName MyRG
```

<span data-ttu-id="fe068-263">De même, pour désactiver un point de terminaison Traffic Manager :</span><span class="sxs-lookup"><span data-stu-id="fe068-263">Similarly, to disable a Traffic Manager endpoint:</span></span>

```powershell
Disable-AzureRmTrafficManagerEndpoint -Name MyEndpoint -Type AzureEndpoints -ProfileName MyProfile -ResourceGroupName MyRG -Force
```

<span data-ttu-id="fe068-264">Comme `Disable-AzureRmTrafficManagerProfile`, l’applet de commande `Disable-AzureRmTrafficManagerEndpoint` vous demande de confirmer l’opération.</span><span class="sxs-lookup"><span data-stu-id="fe068-264">As with `Disable-AzureRmTrafficManagerProfile`, the `Disable-AzureRmTrafficManagerEndpoint` cmdlet prompts for confirmation.</span></span> <span data-ttu-id="fe068-265">Ce message peut être supprimé en utilisant le paramètre « -Force ».</span><span class="sxs-lookup"><span data-stu-id="fe068-265">This prompt can be suppressed using the '-Force' parameter.</span></span>

## <a name="delete-a-traffic-manager-endpoint"></a><span data-ttu-id="fe068-266">Supprimer un point de terminaison Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="fe068-266">Delete a Traffic Manager Endpoint</span></span>

<span data-ttu-id="fe068-267">Pour supprimer des points de terminaison individuels, utilisez l’applet de commande `Remove-AzureRmTrafficManagerEndpoint` :</span><span class="sxs-lookup"><span data-stu-id="fe068-267">To remove individual endpoints, use the `Remove-AzureRmTrafficManagerEndpoint` cmdlet:</span></span>

```powershell
Remove-AzureRmTrafficManagerEndpoint -Name MyEndpoint -Type AzureEndpoints -ProfileName MyProfile -ResourceGroupName MyRG
```

<span data-ttu-id="fe068-268">Cette applet de commande vous demande de confirmer l’opération.</span><span class="sxs-lookup"><span data-stu-id="fe068-268">This cmdlet prompts for confirmation.</span></span> <span data-ttu-id="fe068-269">Ce message peut être supprimé en utilisant le paramètre « -Force ».</span><span class="sxs-lookup"><span data-stu-id="fe068-269">This prompt can be suppressed using the '-Force' parameter.</span></span>

## <a name="delete-a-traffic-manager-profile"></a><span data-ttu-id="fe068-270">Supprimer un profil Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="fe068-270">Delete a Traffic Manager Profile</span></span>

<span data-ttu-id="fe068-271">Pour supprimer un profil Traffic Manager, utilisez l’applet de commande `Remove-AzureRmTrafficManagerProfile` en indiquant les noms de profil et de groupe de ressources :</span><span class="sxs-lookup"><span data-stu-id="fe068-271">To delete a Traffic Manager profile, use the `Remove-AzureRmTrafficManagerProfile` cmdlet, specifying the profile and resource group names:</span></span>

```powershell
Remove-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG [-Force]
```

<span data-ttu-id="fe068-272">Cette applet de commande vous demande de confirmer l’opération.</span><span class="sxs-lookup"><span data-stu-id="fe068-272">This cmdlet prompts for confirmation.</span></span> <span data-ttu-id="fe068-273">Ce message peut être supprimé en utilisant le paramètre « -Force ».</span><span class="sxs-lookup"><span data-stu-id="fe068-273">This prompt can be suppressed using the '-Force' parameter.</span></span>

<span data-ttu-id="fe068-274">Le profil à supprimer peut également être spécifié par un objet de profil :</span><span class="sxs-lookup"><span data-stu-id="fe068-274">The profile to be deleted can also be specified using a profile object:</span></span>

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG
Remove-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile [-Force]
```

<span data-ttu-id="fe068-275">Cette séquence peut également être canalisée :</span><span class="sxs-lookup"><span data-stu-id="fe068-275">This sequence can also be piped:</span></span>

```powershell
Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG | Remove-AzureRmTrafficManagerProfile [-Force]
```

## <a name="next-steps"></a><span data-ttu-id="fe068-276">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="fe068-276">Next steps</span></span>

[<span data-ttu-id="fe068-277">Surveillance avec Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="fe068-277">Traffic Manager monitoring</span></span>](traffic-manager-monitoring.md)

[<span data-ttu-id="fe068-278">Considérations sur les performances de Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="fe068-278">Traffic Manager performance considerations</span></span>](traffic-manager-performance-considerations.md)
