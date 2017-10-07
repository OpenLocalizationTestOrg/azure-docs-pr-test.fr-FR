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
# <a name="manage-azure-cdn-with-powershell"></a>Gérer Azure CDN avec PowerShell
PowerShell fournit un des toomanage de méthodes plus flexible hello vos profils d’Azure CDN et les points de terminaison.  Vous pouvez utiliser PowerShell ou de façon interactive en écrivant des scripts tooautomate les tâches de gestion.  Ce didacticiel illustre plusieurs des tâches les plus courantes de hello que vous pouvez effectuer avec PowerShell toomanage vos profils d’Azure CDN et les points de terminaison.

## <a name="prerequisites"></a>Composants requis
toouse PowerShell toomanage vos profils d’Azure CDN et les points de terminaison, vous devez disposer de module d’Azure PowerShell hello installé.  toolearn comment tooinstall Azure PowerShell et connectez-vous tooAzure à l’aide de hello `Login-AzureRmAccount` applet de commande, consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).

> [!IMPORTANT]
> Vous devez vous connecter avec `Login-AzureRmAccount` avant de pouvoir exécuter les applets de commande Azure PowerShell.
> 
> 

## <a name="listing-hello-azure-cdn-cmdlets"></a>Liste des applets de commande hello CDN Azure
Vous pouvez répertorier toutes les cmdlets d’Azure CDN hello à l’aide de hello `Get-Command` applet de commande.

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

## <a name="getting-help"></a>Obtenir de l’aide
Vous pouvez obtenir une aide avec un de ces applets de commande à l’aide de hello `Get-Help` applet de commande.  `Get-Help` fournit des informations sur l’utilisation et la syntaxe et présente des exemples.

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

## <a name="listing-existing-azure-cdn-profiles"></a>Liste des profils Azure CDN existants
Hello `Get-AzureRmCdnProfile` applet de commande sans aucun paramètre récupère tous vos profils CDN existants.

```powershell
Get-AzureRmCdnProfile
```

Cette sortie peut être dirigée toocmdlets pour l’énumération.

```powershell
# Output hello name of all profiles on this subscription.
Get-AzureRmCdnProfile | ForEach-Object { Write-Host $_.Name }

# Return only **Azure CDN from Verizon** profiles.
Get-AzureRmCdnProfile | Where-Object { $_.Sku.Name -eq "StandardVerizon" }
```

Vous pouvez également retourner un seul profil en spécifiant le groupe de ressources et de nom de profils hello.

```powershell
Get-AzureRmCdnProfile -ProfileName CdnDemo -ResourceGroupName CdnDemoRG
```

> [!TIP]
> Il est possible de toohave CDN plusieurs profils avec le même nom, de hello pour qu’ils se trouvent dans différents groupes de ressources.  L’omission de hello `ResourceGroupName` paramètre retourne tous les profils avec un nom correspondant.
> 
> 

## <a name="listing-existing-cdn-endpoints"></a>Liste des points de terminaison CDN existants
`Get-AzureRmCdnEndpoint`peut récupérer un point de terminaison individuel ou tous les points de terminaison hello sur un profil.  

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

## <a name="creating-cdn-profiles-and-endpoints"></a>Création de profils et points de terminaison CDN
`New-AzureRmCdnProfile`et `New-AzureRmCdnEndpoint` sont utilisés toocreate CDN profils et les points de terminaison.

```powershell
# Create a new profile
New-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -Sku StandardAkamai -Location "Central US"

# Create a new endpoint
New-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -Location "Central US" -EndpointName cdnposhdoc -OriginName "Contoso" -OriginHostName "www.contoso.com"

# Create a new profile and endpoint (same as above) in one line
New-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -Sku StandardAkamai -Location "Central US" | New-AzureRmCdnEndpoint -EndpointName cdnposhdoc -OriginName "Contoso" -OriginHostName "www.contoso.com"

```

## <a name="checking-endpoint-name-availability"></a>Vérification de la disponibilité du nom de point de terminaison
`Get-AzureRmCdnEndpointNameAvailability` renvoie un objet qui indique si un nom de point de terminaison est disponible.

```powershell
# Retrieve availability
$availability = Get-AzureRmCdnEndpointNameAvailability -EndpointName "cdnposhdoc"

# If available, write a message toohello console.
If($availability.NameAvailable) { Write-Host "Yes, that endpoint name is available." }
Else { Write-Host "No, that endpoint name is not available." }
```

## <a name="adding-a-custom-domain"></a>Ajout d’un domaine personnalisé
`New-AzureRmCdnCustomDomain`Ajoute un point de terminaison de domaine personnalisé nom tooan existant.

> [!IMPORTANT]
> Vous devez configurer hello CNAME avec votre fournisseur DNS comme décrit dans [comment point de terminaison du réseau de distribution (CDN) de tooContent toomap un domaine personnalisé](cdn-map-content-to-custom-domain.md).  Vous pouvez tester le mappage hello avant de modifier votre point de terminaison à l’aide de `Test-AzureRmCdnCustomDomain`.
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

## <a name="modifying-an-endpoint"></a>Modification d’un point de terminaison
`Set-AzureRmCdnEndpoint` modifie un point de terminaison existant.

```powershell
# Get an existing endpoint
$endpoint = Get-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -EndpointName cdnposhdoc

# Set up content compression
$endpoint.IsCompressionEnabled = $true
$endpoint.ContentTypesToCompress = "text/javascript","text/css","application/json"

# Save hello changed endpoint and apply hello changes
Set-AzureRmCdnEndpoint -CdnEndpoint $endpoint
```

## <a name="purgingpre-loading-cdn-assets"></a>Purge/pré-chargement des ressources CDN
`Unpublish-AzureRmCdnEndpointContent` purge les ressources mises en cache, tandis que `Publish-AzureRmCdnEndpointContent` précharge les ressources sur les points de terminaison pris en charge.

```powershell
# Purge some assets.
Unpublish-AzureRmCdnEndpointContent -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo -PurgeContent "/images/kitten.png","/video/rickroll.mp4"

# Pre-load some assets.
Publish-AzureRmCdnEndpointContent -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo -LoadContent "/images/kitten.png","/video/rickroll.mp4"

# Purge everything in /images/ on all endpoints.
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Unpublish-AzureRmCdnEndpointContent -PurgeContent "/images/*"
```

## <a name="startingstopping-cdn-endpoints"></a>Démarrage/arrêt des points de terminaison CDN
`Start-AzureRmCdnEndpoint`et `Stop-AzureRmCdnEndpoint` peut être toostart utilisé et arrêter les points de terminaison individuels ou des groupes de points de terminaison.

```powershell
# Stop hello cdndocdemo endpoint
Stop-AzureRmCdnEndpoint -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo

# Stop all endpoints
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Stop-AzureRmCdnEndpoint

# Start all endpoints
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Start-AzureRmCdnEndpoint
```

## <a name="deleting-cdn-resources"></a>Suppression des ressources CDN
`Remove-AzureRmCdnProfile`et `Remove-AzureRmCdnEndpoint` peut être utilisé tooremove profils et les points de terminaison.

```powershell
# Remove a single endpoint
Remove-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -EndpointName cdnposhdoc

# Remove all hello endpoints on a profile and skip confirmation (-Force)
Get-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG | Get-AzureRmCdnEndpoint | Remove-AzureRmCdnEndpoint -Force

# Remove a single profile
Remove-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG
```

## <a name="next-steps"></a>Étapes suivantes
Découvrez comment tooautomate CDN Azure avec [.NET](cdn-app-dev-net.md) ou [Node.js](cdn-app-dev-node.md).

toolearn sur les fonctionnalités du CDN, consultez [vue d’ensemble du CDN](cdn-overview.md).

