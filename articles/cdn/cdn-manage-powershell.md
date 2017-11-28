---
title: aaaManage CDN Azure avec PowerShell | Documents Microsoft
description: "Découvrez comment toouse hello toomanage d’applets de commande PowerShell d’Azure CDN Azure."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: fb6f57a5-6e26-4847-8fd9-b51fb05a79eb
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 269373136d4ef018e4d31f147456b4be2253b463
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-cdn-with-powershell"></a><span data-ttu-id="ddb06-103">Gérer Azure CDN avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="ddb06-103">Manage Azure CDN with PowerShell</span></span>
<span data-ttu-id="ddb06-104">PowerShell fournit un des toomanage de méthodes plus flexible hello vos profils d’Azure CDN et les points de terminaison.</span><span class="sxs-lookup"><span data-stu-id="ddb06-104">PowerShell provides one of hello most flexible methods toomanage your Azure CDN profiles and endpoints.</span></span>  <span data-ttu-id="ddb06-105">Vous pouvez utiliser PowerShell ou de façon interactive en écrivant des scripts tooautomate les tâches de gestion.</span><span class="sxs-lookup"><span data-stu-id="ddb06-105">You can use PowerShell interactively or by writing scripts tooautomate management tasks.</span></span>  <span data-ttu-id="ddb06-106">Ce didacticiel illustre plusieurs des tâches les plus courantes de hello que vous pouvez effectuer avec PowerShell toomanage vos profils d’Azure CDN et les points de terminaison.</span><span class="sxs-lookup"><span data-stu-id="ddb06-106">This tutorial demonstrates several of hello most common tasks you can accomplish with PowerShell toomanage your Azure CDN profiles and endpoints.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ddb06-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="ddb06-107">Prerequisites</span></span>
<span data-ttu-id="ddb06-108">toouse PowerShell toomanage vos profils d’Azure CDN et les points de terminaison, vous devez disposer de module d’Azure PowerShell hello installé.</span><span class="sxs-lookup"><span data-stu-id="ddb06-108">toouse PowerShell toomanage your Azure CDN profiles and endpoints, you must have hello Azure PowerShell module installed.</span></span>  <span data-ttu-id="ddb06-109">toolearn comment tooinstall Azure PowerShell et connectez-vous tooAzure à l’aide de hello `Login-AzureRmAccount` applet de commande, consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ddb06-109">toolearn how tooinstall Azure PowerShell and connect tooAzure using hello `Login-AzureRmAccount` cmdlet, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ddb06-110">Vous devez vous connecter avec `Login-AzureRmAccount` avant de pouvoir exécuter les applets de commande Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ddb06-110">You must log in with `Login-AzureRmAccount` before you can execute Azure PowerShell cmdlets.</span></span>
> 
> 

## <a name="listing-hello-azure-cdn-cmdlets"></a><span data-ttu-id="ddb06-111">Liste des applets de commande hello CDN Azure</span><span class="sxs-lookup"><span data-stu-id="ddb06-111">Listing hello Azure CDN cmdlets</span></span>
<span data-ttu-id="ddb06-112">Vous pouvez répertorier toutes les cmdlets d’Azure CDN hello à l’aide de hello `Get-Command` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="ddb06-112">You can list all hello Azure CDN cmdlets using hello `Get-Command` cmdlet.</span></span>

```text
PS C:\> Get-Command -Module AzureRM.Cdn

CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Cmdlet          Get-AzureRmCdnCustomDomain                         2.0.0      AzureRm.Cdn
Cmdlet          Get-AzureRmCdnEndpoint                             2.0.0      AzureRm.Cdn
Cmdlet          Get-AzureRmCdnEndpointNameAvailability             2.0.0      AzureRm.Cdn
Cmdlet          Get-AzureRmCdnOrigin                               2.0.0      AzureRm.Cdn
Cmdlet          Get-AzureRmCdnProfile                              2.0.0      AzureRm.Cdn
Cmdlet          Get-AzureRmCdnProfileSsoUrl                        2.0.0      AzureRm.Cdn
Cmdlet          New-AzureRmCdnCustomDomain                         2.0.0      AzureRm.Cdn
Cmdlet          New-AzureRmCdnEndpoint                             2.0.0      AzureRm.Cdn
Cmdlet          New-AzureRmCdnProfile                              2.0.0      AzureRm.Cdn
Cmdlet          Publish-AzureRmCdnEndpointContent                  2.0.0      AzureRm.Cdn
Cmdlet          Remove-AzureRmCdnCustomDomain                      2.0.0      AzureRm.Cdn
Cmdlet          Remove-AzureRmCdnEndpoint                          2.0.0      AzureRm.Cdn
Cmdlet          Remove-AzureRmCdnProfile                           2.0.0      AzureRm.Cdn
Cmdlet          Set-AzureRmCdnEndpoint                             2.0.0      AzureRm.Cdn
Cmdlet          Set-AzureRmCdnOrigin                               2.0.0      AzureRm.Cdn
Cmdlet          Set-AzureRmCdnProfile                              2.0.0      AzureRm.Cdn
Cmdlet          Start-AzureRmCdnEndpoint                           2.0.0      AzureRm.Cdn
Cmdlet          Stop-AzureRmCdnEndpoint                            2.0.0      AzureRm.Cdn
Cmdlet          Test-AzureRmCdnCustomDomain                        2.0.0      AzureRm.Cdn
Cmdlet          Unpublish-AzureRmCdnEndpointContent                2.0.0      AzureRm.Cdn
```

## <a name="getting-help"></a><span data-ttu-id="ddb06-113">Obtenir de l’aide</span><span class="sxs-lookup"><span data-stu-id="ddb06-113">Getting help</span></span>
<span data-ttu-id="ddb06-114">Vous pouvez obtenir une aide avec un de ces applets de commande à l’aide de hello `Get-Help` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="ddb06-114">You can get help with any of these cmdlets using hello `Get-Help` cmdlet.</span></span>  <span data-ttu-id="ddb06-115">`Get-Help` fournit des informations sur l’utilisation et la syntaxe et présente des exemples.</span><span class="sxs-lookup"><span data-stu-id="ddb06-115">`Get-Help` provides usage and syntax, and optionally shows examples.</span></span>

```text
PS C:\> Get-Help Get-AzureRmCdnProfile

NAME
    Get-AzureRmCdnProfile

SYNOPSIS
    Gets an Azure CDN profile.


SYNTAX
    Get-AzureRmCdnProfile [-ProfileName <String>] [-ResourceGroupName <String>] [-InformationAction
    <ActionPreference>] [-InformationVariable <String>] [<CommonParameters>]


DESCRIPTION
    Gets an Azure CDN profile and all related information.


RELATED LINKS

REMARKS
    toosee hello examples, type: "get-help Get-AzureRmCdnProfile -examples".
    For more information, type: "get-help Get-AzureRmCdnProfile -detailed".
    For technical information, type: "get-help Get-AzureRmCdnProfile -full".

```

## <a name="listing-existing-azure-cdn-profiles"></a><span data-ttu-id="ddb06-116">Liste des profils Azure CDN existants</span><span class="sxs-lookup"><span data-stu-id="ddb06-116">Listing existing Azure CDN profiles</span></span>
<span data-ttu-id="ddb06-117">Hello `Get-AzureRmCdnProfile` applet de commande sans aucun paramètre récupère tous vos profils CDN existants.</span><span class="sxs-lookup"><span data-stu-id="ddb06-117">hello `Get-AzureRmCdnProfile` cmdlet without any parameters retrieves all your existing CDN profiles.</span></span>

```powershell
Get-AzureRmCdnProfile
```

<span data-ttu-id="ddb06-118">Cette sortie peut être dirigée toocmdlets pour l’énumération.</span><span class="sxs-lookup"><span data-stu-id="ddb06-118">This output can be piped toocmdlets for enumeration.</span></span>

```powershell
# Output hello name of all profiles on this subscription.
Get-AzureRmCdnProfile | ForEach-Object { Write-Host $_.Name }

# Return only **Azure CDN from Verizon** profiles.
Get-AzureRmCdnProfile | Where-Object { $_.Sku.Name -eq "StandardVerizon" }
```

<span data-ttu-id="ddb06-119">Vous pouvez également retourner un seul profil en spécifiant le groupe de ressources et de nom de profils hello.</span><span class="sxs-lookup"><span data-stu-id="ddb06-119">You can also return a single profile by specifying hello profile name and resource group.</span></span>

```powershell
Get-AzureRmCdnProfile -ProfileName CdnDemo -ResourceGroupName CdnDemoRG
```

> [!TIP]
> <span data-ttu-id="ddb06-120">Il est possible de toohave CDN plusieurs profils avec le même nom, de hello pour qu’ils se trouvent dans différents groupes de ressources.</span><span class="sxs-lookup"><span data-stu-id="ddb06-120">It is possible toohave multiple CDN profiles with hello same name, so long as they are in different resource groups.</span></span>  <span data-ttu-id="ddb06-121">L’omission de hello `ResourceGroupName` paramètre retourne tous les profils avec un nom correspondant.</span><span class="sxs-lookup"><span data-stu-id="ddb06-121">Omitting hello `ResourceGroupName` parameter returns all profiles with a matching name.</span></span>
> 
> 

## <a name="listing-existing-cdn-endpoints"></a><span data-ttu-id="ddb06-122">Liste des points de terminaison CDN existants</span><span class="sxs-lookup"><span data-stu-id="ddb06-122">Listing existing CDN endpoints</span></span>
<span data-ttu-id="ddb06-123">`Get-AzureRmCdnEndpoint`peut récupérer un point de terminaison individuel ou tous les points de terminaison hello sur un profil.</span><span class="sxs-lookup"><span data-stu-id="ddb06-123">`Get-AzureRmCdnEndpoint` can retrieve an individual endpoint or all hello endpoints on a profile.</span></span>  

```powershell
# Get a single endpoint.
Get-AzureRmCdnEndpoint -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo

# Get all of hello endpoints on a given profile. 
Get-AzureRmCdnEndpoint -ProfileName CdnDemo -ResourceGroupName CdnDemoRG

# Return all of hello endpoints on all of hello profiles.
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint

# Return all of hello endpoints in this subscription that are currently running.
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Where-Object { $_.ResourceState -eq "Running" }
```

## <a name="creating-cdn-profiles-and-endpoints"></a><span data-ttu-id="ddb06-124">Création de profils et points de terminaison CDN</span><span class="sxs-lookup"><span data-stu-id="ddb06-124">Creating CDN profiles and endpoints</span></span>
<span data-ttu-id="ddb06-125">`New-AzureRmCdnProfile`et `New-AzureRmCdnEndpoint` sont utilisés toocreate CDN profils et les points de terminaison.</span><span class="sxs-lookup"><span data-stu-id="ddb06-125">`New-AzureRmCdnProfile` and `New-AzureRmCdnEndpoint` are used toocreate CDN profiles and endpoints.</span></span>

```powershell
# Create a new profile
New-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -Sku StandardAkamai -Location "Central US"

# Create a new endpoint
New-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -Location "Central US" -EndpointName cdnposhdoc -OriginName "Contoso" -OriginHostName "www.contoso.com"

# Create a new profile and endpoint (same as above) in one line
New-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -Sku StandardAkamai -Location "Central US" | New-AzureRmCdnEndpoint -EndpointName cdnposhdoc -OriginName "Contoso" -OriginHostName "www.contoso.com"

```

## <a name="checking-endpoint-name-availability"></a><span data-ttu-id="ddb06-126">Vérification de la disponibilité du nom de point de terminaison</span><span class="sxs-lookup"><span data-stu-id="ddb06-126">Checking endpoint name availability</span></span>
<span data-ttu-id="ddb06-127">`Get-AzureRmCdnEndpointNameAvailability` renvoie un objet qui indique si un nom de point de terminaison est disponible.</span><span class="sxs-lookup"><span data-stu-id="ddb06-127">`Get-AzureRmCdnEndpointNameAvailability` returns an object indicating if an endpoint name is available.</span></span>

```powershell
# Retrieve availability
$availability = Get-AzureRmCdnEndpointNameAvailability -EndpointName "cdnposhdoc"

# If available, write a message toohello console.
If($availability.NameAvailable) { Write-Host "Yes, that endpoint name is available." }
Else { Write-Host "No, that endpoint name is not available." }
```

## <a name="adding-a-custom-domain"></a><span data-ttu-id="ddb06-128">Ajout d’un domaine personnalisé</span><span class="sxs-lookup"><span data-stu-id="ddb06-128">Adding a custom domain</span></span>
<span data-ttu-id="ddb06-129">`New-AzureRmCdnCustomDomain`Ajoute un point de terminaison de domaine personnalisé nom tooan existant.</span><span class="sxs-lookup"><span data-stu-id="ddb06-129">`New-AzureRmCdnCustomDomain` adds a custom domain name tooan existing endpoint.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ddb06-130">Vous devez configurer hello CNAME avec votre fournisseur DNS comme décrit dans [comment point de terminaison du réseau de distribution (CDN) de tooContent toomap un domaine personnalisé](cdn-map-content-to-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="ddb06-130">You must set up hello CNAME with your DNS provider as described in [How toomap Custom Domain tooContent Delivery Network (CDN) endpoint](cdn-map-content-to-custom-domain.md).</span></span>  <span data-ttu-id="ddb06-131">Vous pouvez tester le mappage hello avant de modifier votre point de terminaison à l’aide de `Test-AzureRmCdnCustomDomain`.</span><span class="sxs-lookup"><span data-stu-id="ddb06-131">You can test hello mapping before modifying your endpoint using `Test-AzureRmCdnCustomDomain`.</span></span>
> 
> 

```powershell
# Get an existing endpoint
$endpoint = Get-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -EndpointName cdnposhdoc

# Check hello mapping
$result = Test-AzureRmCdnCustomDomain -CdnEndpoint $endpoint -CustomDomainHostName "cdn.contoso.com"

# Create hello custom domain on hello endpoint
If($result.CustomDomainValidated){ New-AzureRmCdnCustomDomain -CustomDomainName Contoso -HostName "cdn.contoso.com" -CdnEndpoint $endpoint }
```

## <a name="modifying-an-endpoint"></a><span data-ttu-id="ddb06-132">Modification d’un point de terminaison</span><span class="sxs-lookup"><span data-stu-id="ddb06-132">Modifying an endpoint</span></span>
<span data-ttu-id="ddb06-133">`Set-AzureRmCdnEndpoint` modifie un point de terminaison existant.</span><span class="sxs-lookup"><span data-stu-id="ddb06-133">`Set-AzureRmCdnEndpoint` modifies an existing endpoint.</span></span>

```powershell
# Get an existing endpoint
$endpoint = Get-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -EndpointName cdnposhdoc

# Set up content compression
$endpoint.IsCompressionEnabled = $true
$endpoint.ContentTypesToCompress = "text/javascript","text/css","application/json"

# Save hello changed endpoint and apply hello changes
Set-AzureRmCdnEndpoint -CdnEndpoint $endpoint
```

## <a name="purgingpre-loading-cdn-assets"></a><span data-ttu-id="ddb06-134">Purge/pré-chargement des ressources CDN</span><span class="sxs-lookup"><span data-stu-id="ddb06-134">Purging/Pre-loading CDN assets</span></span>
<span data-ttu-id="ddb06-135">`Unpublish-AzureRmCdnEndpointContent` purge les ressources mises en cache, tandis que `Publish-AzureRmCdnEndpointContent` précharge les ressources sur les points de terminaison pris en charge.</span><span class="sxs-lookup"><span data-stu-id="ddb06-135">`Unpublish-AzureRmCdnEndpointContent` purges cached assets, while `Publish-AzureRmCdnEndpointContent` pre-loads assets on supported endpoints.</span></span>

```powershell
# Purge some assets.
Unpublish-AzureRmCdnEndpointContent -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo -PurgeContent "/images/kitten.png","/video/rickroll.mp4"

# Pre-load some assets.
Publish-AzureRmCdnEndpointContent -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo -LoadContent "/images/kitten.png","/video/rickroll.mp4"

# Purge everything in /images/ on all endpoints.
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Unpublish-AzureRmCdnEndpointContent -PurgeContent "/images/*"
```

## <a name="startingstopping-cdn-endpoints"></a><span data-ttu-id="ddb06-136">Démarrage/arrêt des points de terminaison CDN</span><span class="sxs-lookup"><span data-stu-id="ddb06-136">Starting/Stopping CDN endpoints</span></span>
<span data-ttu-id="ddb06-137">`Start-AzureRmCdnEndpoint`et `Stop-AzureRmCdnEndpoint` peut être toostart utilisé et arrêter les points de terminaison individuels ou des groupes de points de terminaison.</span><span class="sxs-lookup"><span data-stu-id="ddb06-137">`Start-AzureRmCdnEndpoint` and `Stop-AzureRmCdnEndpoint` can be used toostart and stop individual endpoints or groups of endpoints.</span></span>

```powershell
# Stop hello cdndocdemo endpoint
Stop-AzureRmCdnEndpoint -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo

# Stop all endpoints
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Stop-AzureRmCdnEndpoint

# Start all endpoints
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Start-AzureRmCdnEndpoint
```

## <a name="deleting-cdn-resources"></a><span data-ttu-id="ddb06-138">Suppression des ressources CDN</span><span class="sxs-lookup"><span data-stu-id="ddb06-138">Deleting CDN resources</span></span>
<span data-ttu-id="ddb06-139">`Remove-AzureRmCdnProfile`et `Remove-AzureRmCdnEndpoint` peut être utilisé tooremove profils et les points de terminaison.</span><span class="sxs-lookup"><span data-stu-id="ddb06-139">`Remove-AzureRmCdnProfile` and `Remove-AzureRmCdnEndpoint` can be used tooremove profiles and endpoints.</span></span>

```powershell
# Remove a single endpoint
Remove-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -EndpointName cdnposhdoc

# Remove all hello endpoints on a profile and skip confirmation (-Force)
Get-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG | Get-AzureRmCdnEndpoint | Remove-AzureRmCdnEndpoint -Force

# Remove a single profile
Remove-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG
```

## <a name="next-steps"></a><span data-ttu-id="ddb06-140">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ddb06-140">Next Steps</span></span>
<span data-ttu-id="ddb06-141">Découvrez comment tooautomate CDN Azure avec [.NET](cdn-app-dev-net.md) ou [Node.js](cdn-app-dev-node.md).</span><span class="sxs-lookup"><span data-stu-id="ddb06-141">Learn how tooautomate Azure CDN with [.NET](cdn-app-dev-net.md) or [Node.js](cdn-app-dev-node.md).</span></span>

<span data-ttu-id="ddb06-142">toolearn sur les fonctionnalités du CDN, consultez [vue d’ensemble du CDN](cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ddb06-142">toolearn about CDN features, see [CDN Overview](cdn-overview.md).</span></span>

