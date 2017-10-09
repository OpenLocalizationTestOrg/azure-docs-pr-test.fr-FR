---
title: aaaAbout des images pour les machines virtuelles Windows | Documents Microsoft
description: En savoir plus sur l'utilisation des images avec des machines virtuelles Windows dans Azure.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 66ff3fab-8e7f-4dff-b8da-ab1c9c9c9af8
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: cynthn
ms.openlocfilehash: c7cfa1d018a5e99d5b68f559ec9ae1f14e4dec8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="about-images-for-windows-virtual-machines"></a>À propos des images pour les machines virtuelles Windows
> [!IMPORTANT]
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../resource-manager-deployment-model.md). Cet article décrit à l’aide du modèle de déploiement classique hello. Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello. Pour plus d’informations sur la recherche et l’utilisation d’images dans le modèle de gestionnaire de ressources hello, consultez [ici](../../virtual-machines-windows-cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

[!INCLUDE [virtual-machines-common-classic-about-images](../../../../includes/virtual-machines-common-classic-about-images.md)]

## <a name="working-with-images"></a>Utilisation des images

Vous pouvez utiliser le module PowerShell Azure de hello et hello toomanage portail Azure hello images disponibles tooyour abonnement Azure. module d’Azure PowerShell Hello fournit plus d’options de commande, donc vous pouvez identifier exactement ce que vous voulez toosee ou que vous effectuez. Hello portail Azure fournit une interface graphique utilisateur pour la plupart des tâches d’administration quotidiennes hello.

Voici quelques exemples qui utilisent le module Azure PowerShell de hello.

* **Obtenir toutes les images**:`Get-AzureVMImage`renvoie une liste de toutes les images de hello disponibles dans votre abonnement actuel : vos images et celles fournies par Azure ou les partenaires. liste résultante de Hello peut être volumineux. Hello suivant exemples montrent comment tooget une liste plus courte.
* **Obtenir des familles d’images** : `Get-AzureVMImage | select ImageFamily` obtient la liste des familles d’images en affichant des propriétés de chaînes **ImageFamily**.
* **Obtenir toutes les images dans une famille spécifique** : `Get-AzureVMImage | Where-Object {$_.ImageFamily -eq $family}`
* **Rechercher des Images de machine virtuelle**: `Get-AzureVMImage | where {(gm –InputObject $_ -Name DataDiskConfigurations) -ne $null} | Select -Property Label, ImageName` cette applet de commande fonctionne en filtrant la propriété hello DataDiskConfiguration, qui s’applique uniquement les Images de tooVM. Cet exemple filtre aussi hello tooonly hello étiquette et image de nom de sortie.
* **Enregistrer une image généralisée** : `Save-AzureVMImage –ServiceName "myServiceName" –Name "MyVMtoCapture" –OSState "Generalized" –ImageName "MyVmImage" –ImageLabel "This is my generalized image"`
* **Enregistrer une image spécialisée** : `Save-AzureVMImage –ServiceName "mySvc2" –Name "MyVMToCapture2" –ImageName "myFirstVMImageSP" –OSState "Specialized" -Verbose`

  > [!TIP]
  > paramètre de Hello OSState est requis toocreate une image de machine virtuelle, qui inclut le disque du système d’exploitation hello et de disques de données associés. Si vous n’utilisez pas de paramètre hello hello applet de commande crée une image de système d’exploitation. la valeur Hello paramètre hello indique si l’image de hello est généralisée ou spécialisée, selon que disque de système d’exploitation hello a été préparé pour une réutilisation.

* **Supprimer une image** : `Remove-AzureVMImage –ImageName "MyOldVmImage"`

## <a name="next-steps"></a>Étapes suivantes
Vous pouvez également [créer un ordinateur Windows à l’aide de hello Azure portal](tutorial.md).
