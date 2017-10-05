---
title: "Gérer Azure CDN avec PowerShell | Microsoft Docs"
description: "Apprenez à utiliser des applets de commande Azure PowerShell pour gérer Azure CDN."
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
ms.openlocfilehash: 5bd2eed7b34cafa43e8f38279890405d4ae55568
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-azure-cdn-with-powershell"></a><span data-ttu-id="004a2-103">Gérer Azure CDN avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="004a2-103">Manage Azure CDN with PowerShell</span></span>
<span data-ttu-id="004a2-104">PowerShell fournit une des méthodes les plus flexibles pour gérer vos points de terminaison et profils Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="004a2-104">PowerShell provides one of the most flexible methods to manage your Azure CDN profiles and endpoints.</span></span>  <span data-ttu-id="004a2-105">Vous pouvez utiliser PowerShell de manière interactive ou en écrivant des scripts pour automatiser les tâches de gestion.</span><span class="sxs-lookup"><span data-stu-id="004a2-105">You can use PowerShell interactively or by writing scripts to automate management tasks.</span></span>  <span data-ttu-id="004a2-106">Ce didacticiel illustre plusieurs des tâches les plus courantes que vous pouvez accomplir avec PowerShell pour gérer vos points de terminaison et profils Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="004a2-106">This tutorial demonstrates several of the most common tasks you can accomplish with PowerShell to manage your Azure CDN profiles and endpoints.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="004a2-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="004a2-107">Prerequisites</span></span>
<span data-ttu-id="004a2-108">Pour utiliser PowerShell pour gérer vos points de terminaison et profils Azure CDN, vous devez avoir installé le module Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="004a2-108">To use PowerShell to manage your Azure CDN profiles and endpoints, you must have the Azure PowerShell module installed.</span></span>  <span data-ttu-id="004a2-109">Pour savoir comment installer Azure PowerShell et vous connecter à Azure à l’aide de l’applet de commande `Login-AzureRmAccount` , consultez [Installation et configuration d’Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="004a2-109">To learn how to install Azure PowerShell and connect to Azure using the `Login-AzureRmAccount` cmdlet, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="004a2-110">Vous devez vous connecter avec `Login-AzureRmAccount` avant de pouvoir exécuter les applets de commande Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="004a2-110">You must log in with `Login-AzureRmAccount` before you can execute Azure PowerShell cmdlets.</span></span>
> 
> 

## <a name="listing-the-azure-cdn-cmdlets"></a><span data-ttu-id="004a2-111">Liste des applets de commande Azure CDN</span><span class="sxs-lookup"><span data-stu-id="004a2-111">Listing the Azure CDN cmdlets</span></span>
<span data-ttu-id="004a2-112">Vous pouvez répertorier toutes les applets de commande Azure CDN à l’aide de l’applet de commande `Get-Command` .</span><span class="sxs-lookup"><span data-stu-id="004a2-112">You can list all the Azure CDN cmdlets using the `Get-Command` cmdlet.</span></span>

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

## <a name="getting-help"></a><span data-ttu-id="004a2-113">Obtenir de l’aide</span><span class="sxs-lookup"><span data-stu-id="004a2-113">Getting help</span></span>
<span data-ttu-id="004a2-114">Vous pouvez obtenir de l’aide pour ces applets de commande à l’aide de l’applet de commande `Get-Help` .</span><span class="sxs-lookup"><span data-stu-id="004a2-114">You can get help with any of these cmdlets using the `Get-Help` cmdlet.</span></span>  <span data-ttu-id="004a2-115">`Get-Help` fournit des informations sur l’utilisation et la syntaxe et présente des exemples.</span><span class="sxs-lookup"><span data-stu-id="004a2-115">`Get-Help` provides usage and syntax, and optionally shows examples.</span></span>

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
    To see the examples, type: "get-help Get-AzureRmCdnProfile -examples".
    For more information, type: "get-help Get-AzureRmCdnProfile -detailed".
    For technical information, type: "get-help Get-AzureRmCdnProfile -full".

```

## <a name="listing-existing-azure-cdn-profiles"></a><span data-ttu-id="004a2-116">Liste des profils Azure CDN existants</span><span class="sxs-lookup"><span data-stu-id="004a2-116">Listing existing Azure CDN profiles</span></span>
<span data-ttu-id="004a2-117">L’applet de commande `Get-AzureRmCdnProfile` sans aucun paramètre récupère tous vos profils CDN existants.</span><span class="sxs-lookup"><span data-stu-id="004a2-117">The `Get-AzureRmCdnProfile` cmdlet without any parameters retrieves all your existing CDN profiles.</span></span>

```powershell
Get-AzureRmCdnProfile
```

<span data-ttu-id="004a2-118">Cette sortie peut être transmise aux applets de commande pour l’énumération.</span><span class="sxs-lookup"><span data-stu-id="004a2-118">This output can be piped to cmdlets for enumeration.</span></span>

```powershell
# Output the name of all profiles on this subscription.
Get-AzureRmCdnProfile | ForEach-Object { Write-Host $_.Name }

# Return only **Azure CDN from Verizon** profiles.
Get-AzureRmCdnProfile | Where-Object { $_.Sku.Name -eq "StandardVerizon" }
```

<span data-ttu-id="004a2-119">Vous pouvez également renvoyer un seul profil en spécifiant le groupe de ressources et le nom du profil.</span><span class="sxs-lookup"><span data-stu-id="004a2-119">You can also return a single profile by specifying the profile name and resource group.</span></span>

```powershell
Get-AzureRmCdnProfile -ProfileName CdnDemo -ResourceGroupName CdnDemoRG
```

> [!TIP]
> <span data-ttu-id="004a2-120">Il est possible d’avoir plusieurs profils CDN portant le même nom, tant qu’ils se trouvent dans différents groupes de ressources.</span><span class="sxs-lookup"><span data-stu-id="004a2-120">It is possible to have multiple CDN profiles with the same name, so long as they are in different resource groups.</span></span>  <span data-ttu-id="004a2-121">Si vous omettez le paramètre `ResourceGroupName` , cela renvoie tous les profils dont le nom correspond.</span><span class="sxs-lookup"><span data-stu-id="004a2-121">Omitting the `ResourceGroupName` parameter returns all profiles with a matching name.</span></span>
> 
> 

## <a name="listing-existing-cdn-endpoints"></a><span data-ttu-id="004a2-122">Liste des points de terminaison CDN existants</span><span class="sxs-lookup"><span data-stu-id="004a2-122">Listing existing CDN endpoints</span></span>
<span data-ttu-id="004a2-123">`Get-AzureRmCdnEndpoint` peut récupérer un point de terminaison individuel ou tous les points de terminaison d’un profil.</span><span class="sxs-lookup"><span data-stu-id="004a2-123">`Get-AzureRmCdnEndpoint` can retrieve an individual endpoint or all the endpoints on a profile.</span></span>  

```powershell
# Get a single endpoint.
Get-AzureRmCdnEndpoint -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo

# Get all of the endpoints on a given profile. 
Get-AzureRmCdnEndpoint -ProfileName CdnDemo -ResourceGroupName CdnDemoRG

# Return all of the endpoints on all of the profiles.
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint

# Return all of the endpoints in this subscription that are currently running.
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Where-Object { $_.ResourceState -eq "Running" }
```

## <a name="creating-cdn-profiles-and-endpoints"></a><span data-ttu-id="004a2-124">Création de profils et points de terminaison CDN</span><span class="sxs-lookup"><span data-stu-id="004a2-124">Creating CDN profiles and endpoints</span></span>
<span data-ttu-id="004a2-125">`New-AzureRmCdnProfile` et `New-AzureRmCdnEndpoint` sont utilisés pour créer des profils et des points de terminaison CDN.</span><span class="sxs-lookup"><span data-stu-id="004a2-125">`New-AzureRmCdnProfile` and `New-AzureRmCdnEndpoint` are used to create CDN profiles and endpoints.</span></span>

```powershell
# Create a new profile
New-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -Sku StandardAkamai -Location "Central US"

# Create a new endpoint
New-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -Location "Central US" -EndpointName cdnposhdoc -OriginName "Contoso" -OriginHostName "www.contoso.com"

# Create a new profile and endpoint (same as above) in one line
New-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -Sku StandardAkamai -Location "Central US" | New-AzureRmCdnEndpoint -EndpointName cdnposhdoc -OriginName "Contoso" -OriginHostName "www.contoso.com"

```

## <a name="checking-endpoint-name-availability"></a><span data-ttu-id="004a2-126">Vérification de la disponibilité du nom de point de terminaison</span><span class="sxs-lookup"><span data-stu-id="004a2-126">Checking endpoint name availability</span></span>
<span data-ttu-id="004a2-127">`Get-AzureRmCdnEndpointNameAvailability` renvoie un objet qui indique si un nom de point de terminaison est disponible.</span><span class="sxs-lookup"><span data-stu-id="004a2-127">`Get-AzureRmCdnEndpointNameAvailability` returns an object indicating if an endpoint name is available.</span></span>

```powershell
# Retrieve availability
$availability = Get-AzureRmCdnEndpointNameAvailability -EndpointName "cdnposhdoc"

# If available, write a message to the console.
If($availability.NameAvailable) { Write-Host "Yes, that endpoint name is available." }
Else { Write-Host "No, that endpoint name is not available." }
```

## <a name="adding-a-custom-domain"></a><span data-ttu-id="004a2-128">Ajout d’un domaine personnalisé</span><span class="sxs-lookup"><span data-stu-id="004a2-128">Adding a custom domain</span></span>
<span data-ttu-id="004a2-129">`New-AzureRmCdnCustomDomain` ajoute un nom de domaine personnalisé à un point de terminaison existant.</span><span class="sxs-lookup"><span data-stu-id="004a2-129">`New-AzureRmCdnCustomDomain` adds a custom domain name to an existing endpoint.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="004a2-130">Vous devez configurer le CNAME avec votre fournisseur DNS comme décrit dans [Comment mapper un domaine personnalisé à un point de terminaison de réseau de distribution de contenu (CDN)](cdn-map-content-to-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="004a2-130">You must set up the CNAME with your DNS provider as described in [How to map Custom Domain to Content Delivery Network (CDN) endpoint](cdn-map-content-to-custom-domain.md).</span></span>  <span data-ttu-id="004a2-131">Vous pouvez tester le mappage avant de modifier votre point de terminaison à l’aide de `Test-AzureRmCdnCustomDomain`.</span><span class="sxs-lookup"><span data-stu-id="004a2-131">You can test the mapping before modifying your endpoint using `Test-AzureRmCdnCustomDomain`.</span></span>
> 
> 

```powershell
# Get an existing endpoint
$endpoint = Get-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -EndpointName cdnposhdoc

# Check the mapping
$result = Test-AzureRmCdnCustomDomain -CdnEndpoint $endpoint -CustomDomainHostName "cdn.contoso.com"

# Create the custom domain on the endpoint
If($result.CustomDomainValidated){ New-AzureRmCdnCustomDomain -CustomDomainName Contoso -HostName "cdn.contoso.com" -CdnEndpoint $endpoint }
```

## <a name="modifying-an-endpoint"></a><span data-ttu-id="004a2-132">Modification d’un point de terminaison</span><span class="sxs-lookup"><span data-stu-id="004a2-132">Modifying an endpoint</span></span>
<span data-ttu-id="004a2-133">`Set-AzureRmCdnEndpoint` modifie un point de terminaison existant.</span><span class="sxs-lookup"><span data-stu-id="004a2-133">`Set-AzureRmCdnEndpoint` modifies an existing endpoint.</span></span>

```powershell
# Get an existing endpoint
$endpoint = Get-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -EndpointName cdnposhdoc

# Set up content compression
$endpoint.IsCompressionEnabled = $true
$endpoint.ContentTypesToCompress = "text/javascript","text/css","application/json"

# Save the changed endpoint and apply the changes
Set-AzureRmCdnEndpoint -CdnEndpoint $endpoint
```

## <a name="purgingpre-loading-cdn-assets"></a><span data-ttu-id="004a2-134">Purge/pré-chargement des ressources CDN</span><span class="sxs-lookup"><span data-stu-id="004a2-134">Purging/Pre-loading CDN assets</span></span>
<span data-ttu-id="004a2-135">`Unpublish-AzureRmCdnEndpointContent` purge les ressources mises en cache, tandis que `Publish-AzureRmCdnEndpointContent` précharge les ressources sur les points de terminaison pris en charge.</span><span class="sxs-lookup"><span data-stu-id="004a2-135">`Unpublish-AzureRmCdnEndpointContent` purges cached assets, while `Publish-AzureRmCdnEndpointContent` pre-loads assets on supported endpoints.</span></span>

```powershell
# Purge some assets.
Unpublish-AzureRmCdnEndpointContent -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo -PurgeContent "/images/kitten.png","/video/rickroll.mp4"

# Pre-load some assets.
Publish-AzureRmCdnEndpointContent -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo -LoadContent "/images/kitten.png","/video/rickroll.mp4"

# Purge everything in /images/ on all endpoints.
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Unpublish-AzureRmCdnEndpointContent -PurgeContent "/images/*"
```

## <a name="startingstopping-cdn-endpoints"></a><span data-ttu-id="004a2-136">Démarrage/arrêt des points de terminaison CDN</span><span class="sxs-lookup"><span data-stu-id="004a2-136">Starting/Stopping CDN endpoints</span></span>
<span data-ttu-id="004a2-137">`Start-AzureRmCdnEndpoint` et `Stop-AzureRmCdnEndpoint` peuvent être utilisés pour démarrer et arrêter des points de terminaison individuels ou des groupes de points de terminaison.</span><span class="sxs-lookup"><span data-stu-id="004a2-137">`Start-AzureRmCdnEndpoint` and `Stop-AzureRmCdnEndpoint` can be used to start and stop individual endpoints or groups of endpoints.</span></span>

```powershell
# Stop the cdndocdemo endpoint
Stop-AzureRmCdnEndpoint -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo

# Stop all endpoints
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Stop-AzureRmCdnEndpoint

# Start all endpoints
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Start-AzureRmCdnEndpoint
```

## <a name="deleting-cdn-resources"></a><span data-ttu-id="004a2-138">Suppression des ressources CDN</span><span class="sxs-lookup"><span data-stu-id="004a2-138">Deleting CDN resources</span></span>
<span data-ttu-id="004a2-139">`Remove-AzureRmCdnProfile` et `Remove-AzureRmCdnEndpoint` peuvent être utilisés pour supprimer des profils et des points de terminaison.</span><span class="sxs-lookup"><span data-stu-id="004a2-139">`Remove-AzureRmCdnProfile` and `Remove-AzureRmCdnEndpoint` can be used to remove profiles and endpoints.</span></span>

```powershell
# Remove a single endpoint
Remove-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -EndpointName cdnposhdoc

# Remove all the endpoints on a profile and skip confirmation (-Force)
Get-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG | Get-AzureRmCdnEndpoint | Remove-AzureRmCdnEndpoint -Force

# Remove a single profile
Remove-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG
```

## <a name="next-steps"></a><span data-ttu-id="004a2-140">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="004a2-140">Next Steps</span></span>
<span data-ttu-id="004a2-141">Apprenez à automatiser Azure CDN avec [.NET](cdn-app-dev-net.md) ou [Node.js](cdn-app-dev-node.md).</span><span class="sxs-lookup"><span data-stu-id="004a2-141">Learn how to automate Azure CDN with [.NET](cdn-app-dev-net.md) or [Node.js](cdn-app-dev-node.md).</span></span>

<span data-ttu-id="004a2-142">Pour en savoir plus sur les fonctionnalités CDN, consultez [Présentation du CDN](cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="004a2-142">To learn about CDN features, see [CDN Overview](cdn-overview.md).</span></span>

