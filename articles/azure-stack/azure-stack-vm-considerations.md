---
title: "aaaDifferences et considérations relatives à des machines virtuelles dans Azure pile | Documents Microsoft"
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
ms.date: 8/4/2017
ms.author: sngun
ms.openlocfilehash: cee03e3e83b54efabaecd2647ec7defe371ee870
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="considerations-for-virtual-machines-in-azure-stack"></a>Considérations relatives aux machines virtuelles dans Azure Stack

Les machines virtuelles sont des ressources de calcul évolutives et à la demande qui sont mises à la disposition des utilisateurs dans Azure Stack. Lorsque vous utilisez des Machines virtuelles, vous devez comprendre qu’il existe des différences entre les fonctionnalités de hello qui sont disponibles dans Azure et de la pile de Azure. Cet article fournit une vue d’ensemble des considérations spécifiques de hello pour les Machines virtuelles et de ses fonctionnalités dans la pile de Azure. toolearn sur les principales différences entre la pile d’Azure et d’Azure, consultez hello [considérations relatives à la clé](azure-stack-considerations.md) rubrique.

## <a name="cheat-sheet-virtual-machine-differences"></a>Aide-mémoire : différences sur le plan des machines virtuelles

| Fonctionnalité | Azure (global) | Azure Stack |
| --- | --- | --- |
| Images de machine virtuelle | Bonjour Azure Marketplace contient les images que vous pouvez utiliser toocreate une machine virtuelle. Consultez hello [Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/compute?subcategories=virtual-machine-images&page=1) liste hello tooview des pages d’images qui sont disponibles dans hello Azure Marketplace. | Par défaut, il ne sont pas toutes les images disponibles dans le marketplace d’Azure pile hello. administrateur du cloud Azure pile Hello doit [publier](azure-stack-add-default-image.md) ou [télécharger des images](azure-stack-download-azure-marketplace-item.md) marketplace d’Azure pile toohello avant que les utilisateurs peuvent les utiliser. |
| Tailles de machines virtuelles | Azure prend en charge de nombreuses tailles de machine virtuelle. toolearn sur les tailles disponibles hello et les options, consultez toohello [tailles de machines virtuelles Windows](../virtual-machines/virtual-machines-windows-sizes.md) et [tailles de machine virtuelle Linux](../virtual-machines/linux/sizes.md) rubriques. | Azure Stack prend en charge certaines des tailles de machine virtuelle qui sont disponibles dans Azure. liste de hello tooview de prise en charge des tailles, consultez le toohello [tailles de machine virtuelle](#virtual-machine-sizes) section de cet article. |
| Quotas de machine virtuelle | Les [limites de quota](../azure-subscription-service-limits.md#service-specific-limits) sont définies par Microsoft. | administrateur du cloud Azure pile Hello doit [affecter des quotas](azure-stack-setting-quotas.md) avant qu’ils offrent aux utilisateurs de machines virtuelles tootheir. |
| Extensions de machine virtuelle |Azure prend en charge de nombreuses extensions de machine virtuelle. toolearn sur les extensions disponibles de hello, consultez toohello [extensions de machine virtuelle et de fonctionnalités](../virtual-machines/windows/extensions-features.md) rubrique.| Pile Azure prend en charge un sous-ensemble des extensions qui sont disponibles dans Azure et chaque extension de hello des versions spécifiques. administrateur du cloud Azure pile Hello pouvez choisir quels toobe extensions apportées toofor disponible aux utilisateurs. liste de hello tooview de prise en charge les extensions, consultez toohello [extensions de machine virtuelle](#virtual-machine-extensions) section de cet article. |
| Réseau de machines virtuelles | Les adresses IP publiques affectées tootenant virtuels sont accessibles via hello Internet.<br><br><br>Les machines virtuelles Azure ont un nom DNS fixe. | Les adresses IP publiques affectés l’ordinateur virtuel de tooa du client sont accessibles au sein de l’environnement de Kit de développement de pile Azure hello. Un utilisateur doit avoir accès toohello Kit de développement de pile Azure via [RDP](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop) ou [VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn) tooconnect tooa virtuels qui est créé dans la pile de Azure.<br><br>Machines virtuelles créées au sein d’une instance spécifique de la pile de Azure ont un nom DNS en fonction de valeur hello qui est configuré par l’administrateur du cloud hello. |
| Stockage de machine virtuelle | Prend en charge les [disques managés](../virtual-machines/windows/managed-disks-overview.md). | Les disques managés ne sont pas encore pris en charge dans Azure Stack. |
| Versions d’API | Azure a toujours hello API les plus récents pour toutes les fonctionnalités de machine virtuelle hello. | Azure Stack prend en charge certains services Azure et des versions d’API spécifiques pour ces services. liste de hello tooview de prise en charge les versions d’API, consultez toohello [versions d’API](#api-versions) section de cet article. |
|Groupes à haute disponibilité de machines virtuelles|Plusieurs domaines d’erreur (2 ou 3 par région)<br>Plusieurs domaines de mise à jour<br>Prise en charge des disques managés|Un seul domaine d’erreur<br>Un seul domaine de mise à jour<br>Pas de prise en charge des disques managés|
|Groupes identiques de machines virtuelles |Prise en charge du dimensionnement automatique des instances|Pas de prise en charge du dimensionnement automatique des instances.<br>Ajouter plusieurs instances tooa un ensemble d’échelle à l’aide du portail de hello, des modèles de gestionnaire de ressources ou PowerShell.

## <a name="virtual-machine-sizes"></a>Tailles de machines virtuelles 

Hello Kit de développement de pile Azure prend en charge hello suivant tailles : 

| Type | Taille | Plage de tailles prises en charge |
| --- | --- | --- |
|Usage général |De base A|A0-A4|
|Usage général |Standard A|A0-A7|
|Usage général |Standard D|D1-D4|
|Usage général |Standard Dv2|D1v2-D5v2|
|Mémoire optimisée|Série D|D11-D14|
|Mémoire optimisée |Série Dv2|D11v2-D14v2|

Tailles de machine virtuelle dans la pile de Azure et Azure sont cohérentes en termes de mémoire de hello, processeur cœurs, la bande passante réseau, les performances de disque et d’autres facteurs qui définissent la taille de hello. Par exemple, taille D Standard hello virtuels dans Azure et Azure pile est cohérent. 

## <a name="virtual-machine-extensions"></a>Extensions de machine virtuelle 

 Hello Kit de développement de pile Azure prend en charge hello versions d’extension de machine virtuelle suivantes :

![Extensions de machine virtuelle](media/azure-stack-vm-considerations/vm-extensions.png)

Utilisez hello suivant PowerShell script tooget hello liste d’extensions de machine virtuelle qui sont disponibles dans votre environnement de la pile de Azure :

```powershell 
Get-AzureRmVmImagePublisher -Location local | `
  Get-AzureRmVMExtensionImageType | `
  Get-AzureRmVMExtensionImage | `
  Select Type, Version | `
  Format-Table -Property * -AutoSize 
```

## <a name="api-versions"></a>Versions d’API 

Fonctionnalités de machine virtuelle dans le Kit de développement de pile Azure prennent en charge hello versions d’API suivantes :

![Types de ressources de machine virtuelle](media/azure-stack-vm-considerations/vm-resoource-types.png)

Vous pouvez utiliser hello PowerShell script tooget hello API versions pour les fonctionnalités de machine virtuelle hello qui sont disponibles dans votre environnement Azure pile suivantes :

```powershell 
Get-AzureRmResourceProvider | `
  Select ProviderNamespace -Expand ResourceTypes | `
  Select * -Expand ApiVersions | `
  Select ProviderNamespace, ResourceTypeName, @{Name="ApiVersion"; Expression={$_}} | `
  where-Object {$_.ProviderNamespace -like “Microsoft.compute”}
```
liste Hello de prise en charge les types de ressources et les versions d’API peuvent varier si l’opérateur de cloud hello met à jour votre version plus récente de Azure pile environnement tooa.

## <a name="next-steps"></a>Étapes suivantes

[Créer une machine virtuelle Windows à l’aide de PowerShell dans Azure Stack](azure-stack-quick-create-vm-powershell.md)
