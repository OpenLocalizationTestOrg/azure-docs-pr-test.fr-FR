---
title: "Différences et considérations relatives aux machines virtuelles dans Azure Stack | Microsoft Docs"
description: "Découvrez les différences et les éléments à prendre en compte lors de l’utilisation de machines virtuelles dans Azure Stack."
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 9/25/2017
ms.author: sngun
ms.openlocfilehash: 7d841dba798c2b706c26dcf51361ce0447710b12
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/11/2017
---
# <a name="considerations-for-virtual-machines-in-azure-stack"></a>Considérations relatives aux machines virtuelles dans Azure Stack

*S’applique à : systèmes intégrés Azure Stack et Kit de développement Azure Stack*

Les machines virtuelles sont des ressources de calcul évolutives et à la demande qui sont mises à la disposition des utilisateurs dans Azure Stack. Quand vous utilisez des machines virtuelles, sachez qu’il existe des différences entre les fonctionnalités disponibles dans Azure et dans Azure Stack. Cet article offre une vue d’ensemble des considérations propres aux machines virtuelles et à leurs fonctionnalités dans Azure Stack. Pour connaître les différences majeures entre Azure Stack et Azure, consultez la rubrique [Principales considérations](azure-stack-considerations.md).

## <a name="cheat-sheet-virtual-machine-differences"></a>Aide-mémoire : différences sur le plan des machines virtuelles

| Fonctionnalité | Azure (global) | Azure Stack |
| --- | --- | --- |
| Images de machine virtuelle | La Place de marché Azure contient des images que vous pouvez utiliser pour créer une machine virtuelle. Consultez la page [Place de marché Azure](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/compute?subcategories=virtual-machine-images&page=1) pour obtenir la liste des images disponibles sur la Place de marché Azure. | Par défaut, il n’y a pas d’images disponibles sur la Place de marché Azure Stack. L’administrateur du cloud Azure Stack doit publier ou télécharger des images sur la Place de marché Azure Stack pour les mettre à la disposition des utilisateurs. |
| Tailles de machines virtuelles | Azure prend en charge de nombreuses tailles de machine virtuelle. Pour connaître les options et les tailles disponibles, consultez les rubriques [Tailles des machines virtuelles Windows](../../virtual-machines/virtual-machines-windows-sizes.md) et [Tailles des machines virtuelles Linux](../../virtual-machines/linux/sizes.md). | Azure Stack prend en charge certaines des tailles de machine virtuelle qui sont disponibles dans Azure. Pour obtenir la liste des tailles prises en charge, consultez la section [Tailles de machine virtuelle](#virtual-machine-sizes) dans cet article. |
| Quotas de machine virtuelle | Les [limites de quota](../../azure-subscription-service-limits.md#service-specific-limits) sont définies par Microsoft. | L’administrateur du cloud Azure Stack doit assigner des quotas avant de mettre des machines virtuelles à la disposition des utilisateurs. |
| Extensions de machine virtuelle |Azure prend en charge de nombreuses extensions de machine virtuelle. Pour connaître les extensions disponibles, consultez la rubrique [Extensions et fonctionnalités de machine virtuelle](../../virtual-machines/windows/extensions-features.md).| Azure Stack prend en charge certaines des extensions disponibles dans Azure. Notez que chaque extension a des versions spécifiques. L’administrateur du cloud Azure Stack peut choisir les extensions qu’il veut mettre à la disposition des utilisateurs. Pour obtenir la liste des extensions prises en charge, consultez la section [Extensions de machine virtuelle](#virtual-machine-extensions) dans cet article. |
| Réseau de machines virtuelles | Les adresses IP publiques assignées à une machine virtuelle locataire sont accessibles via Internet.<br><br><br>Les machines virtuelles Azure ont un nom DNS fixe. | Les adresses IP publiques assignées à une machine virtuelle locataire sont accessibles uniquement au sein de l’environnement du Kit de développement Azure Stack. Un utilisateur doit pouvoir accéder au Kit de développement Azure Stack par le biais du [RDP](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop) ou du [VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn) pour se connecter à une machine virtuelle créée dans Azure Stack.<br><br>Les machines virtuelles créées dans une instance Azure Stack spécifique ont un nom DNS basé sur la valeur définie par l’administrateur du cloud. |
| Stockage de machine virtuelle | Prend en charge les [disques managés](../../virtual-machines/windows/managed-disks-overview.md). | Les disques managés ne sont pas encore pris en charge dans Azure Stack. |
| Versions d’API | Azure utilise toujours les dernières versions d’API pour toutes les fonctionnalités de machine virtuelle. | Azure Stack prend en charge certains services Azure et des versions d’API spécifiques pour ces services. Pour obtenir la liste des versions d’API prises en charge, consultez la section [Versions d’API](#api-versions) dans cet article. |
|Groupes à haute disponibilité de machines virtuelles|Plusieurs domaines d’erreur (2 ou 3 par région)<br>Plusieurs domaines de mise à jour<br>Prise en charge des disques managés|Un seul domaine d’erreur<br>Un seul domaine de mise à jour<br>Pas de prise en charge des disques managés|
|Groupes identiques de machines virtuelles |Prise en charge du dimensionnement automatique des instances|Pas de prise en charge du dimensionnement automatique des instances.<br>Pour ajouter d’autres instances à un groupe identique, utilisez le portail, les modèles Resource Manager ou PowerShell.

## <a name="virtual-machine-sizes"></a>Tailles de machines virtuelles 

Le Kit de développement Azure Stack prend en charge les tailles suivantes : 

| Type | Taille | Plage de tailles prises en charge |
| --- | --- | --- |
|Usage général |De base A|A0-A4|
|Usage général |Standard A|A0-A7|
|Usage général |Standard D|D1-D4|
|Usage général |Standard Dv2|D1v2-D5v2|
|Mémoire optimisée|Série D|D11-D14|
|Mémoire optimisée |Série Dv2|D11v2-D14v2|

Les tailles de machine virtuelle et les quantités de ressources associées sont cohérentes entre Azure Stack et Azure. Par exemple, cela inclut la quantité de mémoire, le nombre de cœurs et le nombre ou la taille des disques de données qui peuvent être créés. Toutefois, les performances d’une même taille de machine virtuelle dans Azure Stack dépendent des caractéristiques sous-jacentes de chaque environnement Azure Stack.

## <a name="virtual-machine-extensions"></a>Extensions de machine virtuelle 

 Le Kit de développement Azure Stack prend en charge les versions d’extension de machine virtuelle suivantes :

![Extensions de machine virtuelle](media/azure-stack-vm-considerations/vm-extensions.png)

Utilisez le script PowerShell suivant pour obtenir la liste des extensions de machine virtuelle qui sont disponibles dans votre environnement Azure Stack :

```powershell 
Get-AzureRmVmImagePublisher -Location local | `
  Get-AzureRmVMExtensionImageType | `
  Get-AzureRmVMExtensionImage | `
  Select Type, Version | `
  Format-Table -Property * -AutoSize 
```

## <a name="api-versions"></a>Versions d’API 

Les fonctionnalités de machine virtuelle dans le Kit de développement Azure Stack prennent en charge les versions d’API suivantes :

![Types de ressources de machine virtuelle](media/azure-stack-vm-considerations/vm-resoource-types.png)

Utilisez le script PowerShell suivant pour obtenir la liste des versions d’API des fonctionnalités de machine virtuelle qui sont disponibles dans votre environnement Azure Stack :

```powershell 
Get-AzureRmResourceProvider | `
  Select ProviderNamespace -Expand ResourceTypes | `
  Select * -Expand ApiVersions | `
  Select ProviderNamespace, ResourceTypeName, @{Name="ApiVersion"; Expression={$_}} | `
  where-Object {$_.ProviderNamespace -like “Microsoft.compute”}
```
La liste des types de ressources et des versions d’API pris en charge peut varier si l’opérateur du cloud met à jour votre environnement Azure Stack avec une version plus récente.

## <a name="next-steps"></a>Étapes suivantes

[Créer une machine virtuelle Windows à l’aide de PowerShell dans Azure Stack](azure-stack-quick-create-vm-windows-powershell.md)
