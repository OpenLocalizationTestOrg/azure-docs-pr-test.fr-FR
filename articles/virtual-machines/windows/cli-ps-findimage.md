---
title: les images aaaSelect machine virtuelle Windows dans Azure | Documents Microsoft
description: "Découvrez comment toouse Azure PowerSHell toodetermine hello publisher, offre, référence (SKU) et la version pour les images de machine virtuelle du Marketplace."
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 188b8974-fabd-4cd3-b7dc-559cbb86b98a
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/12/2017
ms.author: danlep
ms.openlocfilehash: 752edcd0935f5141832e49503ae800ea0145e219
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toofind-windows-vm-images-in-hello-azure-marketplace-with-azure-powershell"></a>Comment toofind machine virtuelle Windows images Bonjour Azure Marketplace avec Azure PowerShell

Cette rubrique décrit comment toouse Azure PowerShell toofind VM images Bonjour Azure Marketplace. Utilisez cette toospecify informations une image de Marketplace lorsque vous créez une machine virtuelle Windows.

Assurez-vous que vous installé et configuré hello dernières [module Azure PowerShell](/powershell/azure/install-azurerm-ps).



## <a name="table-of-commonly-used-windows-images"></a>Tableau des images système Windows couramment utilisées
| PublisherName | Offer | Sku |
|:--- |:--- |:--- |:--- |
| MicrosoftWindowsServer |WindowsServer |2016-centre-de-données |
| MicrosoftWindowsServer |WindowsServer |2016-Datacenter-Server-Core |
| MicrosoftWindowsServer |WindowsServer |2016-centre-de-données-avec-conteneurs |
| MicrosoftWindowsServer |WindowsServer |2016-Nano-Server |
| MicrosoftWindowsServer |WindowsServer |2012-R2-Datacenter |
| MicrosoftWindowsServer |WindowsServer |2008-R2-SP1 |
| MicrosoftDynamicsNAV |DynamicsNAV |2017 |
| MicrosoftSharePoint |MicrosoftSharePointServer |2016 |
| MicrosoftSQLServer |SQL2016-WS2016 |Entreprise |
| MicrosoftSQLServer |SQL2014SP2-WS2012R2 |Entreprise |
| MicrosoftWindowsServerHPCPack |WindowsServerHPCPack |2012R2 |
| MicrosoftWindowsServerEssentials |WindowsServerEssentials |WindowsServerEssentials |

## <a name="find-specific-images"></a>Recherche d’images spécifiques


Lorsque vous créez une machine virtuelle avec Azure Resource Manager, dans certains cas vous devez toospecify une image avec une combinaison de hello de hello image propriétés suivantes :

* Éditeur
* Offer
* SKU

Par exemple, utilisez ces valeurs avec hello [Set-AzureRMVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) applet de commande PowerShell ou avec un modèle de groupe de ressources dans lequel vous devez spécifier le type hello de toobe de machine virtuelle créée.

Si vous devez toodetermine ces valeurs, vous pouvez exécuter hello [Get-AzureRMVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher), [Get-AzureRMVMImageOffer](/powershell/module/azurerm.compute/get-azurermvmimageoffer), et [Get-AzureRMVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku) applets de commande images hello toonavigate. Vous déterminez ces valeurs :

1. Serveurs de publication liste hello image.
2. pour un éditeur donné, en répertoriant ses offres ;
3. pour une offre donnée, en répertoriant ses références SKU.

Tout d’abord, la liste des éditeurs de hello avec hello suivant les commandes :

```powershell
$locName="<Azure location, such as West US>"
Get-AzureRMVMImagePublisher -Location $locName | Select PublisherName
```

Renseignez le nom de votre serveur de publication choisie et exécutez hello suivant les commandes :

```powershell
$pubName="<publisher>"
Get-AzureRMVMImageOffer -Location $locName -Publisher $pubName | Select Offer
```

Renseignez le nom de votre offre choisie et exécutez hello suivant les commandes :

```powershell
$offerName="<offer>"
Get-AzureRMVMImageSku -Location $locName -Publisher $pubName -Offer $offerName | Select Skus
```

À partir de la sortie de hello Hello `Get-AzureRMVMImageSku` de commande, vous disposez de toutes les informations de hello vous avez besoin d’une image de hello toospecify pour une machine virtuelle.

Hello Voici un exemple complet :

```powershell
$locName="West US"
Get-AzureRMVMImagePublisher -Location $locName | Select PublisherName

```

Output:

```
PublisherName
-------------
a10networks
aiscaler-cache-control-ddos-and-url-rewriting-
alertlogic
AlertLogic.Extension
Barracuda.Azure.ConnectivityAgent
barracudanetworks
basho
boxless
bssw
Canonical
...
```

Pour le serveur de publication « MicrosoftWindowsServer » hello :

```powershell
$pubName="MicrosoftWindowsServer"
Get-AzureRMVMImageOffer -Location $locName -Publisher $pubName | Select Offer
```

Output:

```
Offer
-----
Windows-HUB
WindowsServer
WindowsServer-HUB
```

Pour l’offre de « Windows Server » hello :

```powershell
$offerName="WindowsServer"
Get-AzureRMVMImageSku -Location $locName -Publisher $pubName -Offer $offerName | Select Skus
```

Output:

```
Skus
----
2008-R2-SP1
2008-R2-SP1-smalldisk
2012-Datacenter
2012-Datacenter-smalldisk
2012-R2-Datacenter
2012-R2-Datacenter-smalldisk
2016-Datacenter
2016-Datacenter-Server-Core
2016-Datacenter-Server-Core-smalldisk
2016-Datacenter-smalldisk
2016-Datacenter-with-Containers
2016-Nano-Server
```

À partir de cette liste, copiez hello choisi le nom de référence (SKU), et que toutes les informations de hello pour hello `Set-AzureRMVMSourceImage` applet de commande PowerShell ou d’un modèle de groupe de ressources.

## <a name="next-steps"></a>Étapes suivantes
À présent, vous pouvez choisir précisément hello image lequel toouse. voir d’un ordinateur virtuel rapidement en utilisant les informations d’image de hello, qui vous venez de trouver, toocreate [créer une machine virtuelle Windows avec PowerShell](quick-create-powershell.md).
