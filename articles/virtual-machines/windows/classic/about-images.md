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
# <a name="about-images-for-windows-virtual-machines"></a><span data-ttu-id="180ef-103">À propos des images pour les machines virtuelles Windows</span><span class="sxs-lookup"><span data-stu-id="180ef-103">About images for Windows virtual machines</span></span>
> [!IMPORTANT]
> <span data-ttu-id="180ef-104">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="180ef-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="180ef-105">Cet article décrit à l’aide du modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="180ef-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="180ef-106">Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="180ef-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="180ef-107">Pour plus d’informations sur la recherche et l’utilisation d’images dans le modèle de gestionnaire de ressources hello, consultez [ici](../../virtual-machines-windows-cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="180ef-107">For information about finding and using images in hello Resource Manager model, see [here](../../virtual-machines-windows-cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-classic-about-images](../../../../includes/virtual-machines-common-classic-about-images.md)]

## <a name="working-with-images"></a><span data-ttu-id="180ef-108">Utilisation des images</span><span class="sxs-lookup"><span data-stu-id="180ef-108">Working with images</span></span>

<span data-ttu-id="180ef-109">Vous pouvez utiliser le module PowerShell Azure de hello et hello toomanage portail Azure hello images disponibles tooyour abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="180ef-109">You can use hello Azure PowerShell module and hello Azure portal toomanage hello images available tooyour Azure subscription.</span></span> <span data-ttu-id="180ef-110">module d’Azure PowerShell Hello fournit plus d’options de commande, donc vous pouvez identifier exactement ce que vous voulez toosee ou que vous effectuez.</span><span class="sxs-lookup"><span data-stu-id="180ef-110">hello Azure PowerShell module provides more command options, so you can pinpoint exactly what you want toosee or do.</span></span> <span data-ttu-id="180ef-111">Hello portail Azure fournit une interface graphique utilisateur pour la plupart des tâches d’administration quotidiennes hello.</span><span class="sxs-lookup"><span data-stu-id="180ef-111">hello Azure portal provides a GUI for many of hello everyday administrative tasks.</span></span>

<span data-ttu-id="180ef-112">Voici quelques exemples qui utilisent le module Azure PowerShell de hello.</span><span class="sxs-lookup"><span data-stu-id="180ef-112">Here are some examples that use hello Azure PowerShell module.</span></span>

* <span data-ttu-id="180ef-113">**Obtenir toutes les images**:`Get-AzureVMImage`renvoie une liste de toutes les images de hello disponibles dans votre abonnement actuel : vos images et celles fournies par Azure ou les partenaires.</span><span class="sxs-lookup"><span data-stu-id="180ef-113">**Get all images**:`Get-AzureVMImage`returns a list of all hello images available in your current subscription: your images and those provided by Azure or partners.</span></span> <span data-ttu-id="180ef-114">liste résultante de Hello peut être volumineux.</span><span class="sxs-lookup"><span data-stu-id="180ef-114">hello resulting list could be large.</span></span> <span data-ttu-id="180ef-115">Hello suivant exemples montrent comment tooget une liste plus courte.</span><span class="sxs-lookup"><span data-stu-id="180ef-115">hello next examples show how tooget a shorter list.</span></span>
* <span data-ttu-id="180ef-116">**Obtenir des familles d’images** : `Get-AzureVMImage | select ImageFamily` obtient la liste des familles d’images en affichant des propriétés de chaînes **ImageFamily**.</span><span class="sxs-lookup"><span data-stu-id="180ef-116">**Get image families**:`Get-AzureVMImage | select ImageFamily` gets a list of image families by showing strings **ImageFamily** property.</span></span>
* <span data-ttu-id="180ef-117">**Obtenir toutes les images dans une famille spécifique** : `Get-AzureVMImage | Where-Object {$_.ImageFamily -eq $family}`</span><span class="sxs-lookup"><span data-stu-id="180ef-117">**Get all images in a specific family**: `Get-AzureVMImage | Where-Object {$_.ImageFamily -eq $family}`</span></span>
* <span data-ttu-id="180ef-118">**Rechercher des Images de machine virtuelle**: `Get-AzureVMImage | where {(gm –InputObject $_ -Name DataDiskConfigurations) -ne $null} | Select -Property Label, ImageName` cette applet de commande fonctionne en filtrant la propriété hello DataDiskConfiguration, qui s’applique uniquement les Images de tooVM.</span><span class="sxs-lookup"><span data-stu-id="180ef-118">**Find VM Images**: `Get-AzureVMImage | where {(gm –InputObject $_ -Name DataDiskConfigurations) -ne $null} | Select -Property Label, ImageName` This cmdlet works by filtering hello DataDiskConfiguration property, which only applies tooVM Images.</span></span> <span data-ttu-id="180ef-119">Cet exemple filtre aussi hello tooonly hello étiquette et image de nom de sortie.</span><span class="sxs-lookup"><span data-stu-id="180ef-119">This example also filters hello output tooonly hello label and image name.</span></span>
* <span data-ttu-id="180ef-120">**Enregistrer une image généralisée** : `Save-AzureVMImage –ServiceName "myServiceName" –Name "MyVMtoCapture" –OSState "Generalized" –ImageName "MyVmImage" –ImageLabel "This is my generalized image"`</span><span class="sxs-lookup"><span data-stu-id="180ef-120">**Save a generalized image**: `Save-AzureVMImage –ServiceName "myServiceName" –Name "MyVMtoCapture" –OSState "Generalized" –ImageName "MyVmImage" –ImageLabel "This is my generalized image"`</span></span>
* <span data-ttu-id="180ef-121">**Enregistrer une image spécialisée** : `Save-AzureVMImage –ServiceName "mySvc2" –Name "MyVMToCapture2" –ImageName "myFirstVMImageSP" –OSState "Specialized" -Verbose`</span><span class="sxs-lookup"><span data-stu-id="180ef-121">**Save a specialized image**: `Save-AzureVMImage –ServiceName "mySvc2" –Name "MyVMToCapture2" –ImageName "myFirstVMImageSP" –OSState "Specialized" -Verbose`</span></span>

  > [!TIP]
  > <span data-ttu-id="180ef-122">paramètre de Hello OSState est requis toocreate une image de machine virtuelle, qui inclut le disque du système d’exploitation hello et de disques de données associés.</span><span class="sxs-lookup"><span data-stu-id="180ef-122">hello OSState parameter is required toocreate a VM image, which includes hello operating system disk and attached data disks.</span></span> <span data-ttu-id="180ef-123">Si vous n’utilisez pas de paramètre hello hello applet de commande crée une image de système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="180ef-123">If you don’t use hello parameter, hello cmdlet creates an OS image.</span></span> <span data-ttu-id="180ef-124">la valeur Hello paramètre hello indique si l’image de hello est généralisée ou spécialisée, selon que disque de système d’exploitation hello a été préparé pour une réutilisation.</span><span class="sxs-lookup"><span data-stu-id="180ef-124">hello value of hello parameter indicates whether hello image is generalized or specialized, based on whether hello operating system disk has been prepared for reuse.</span></span>

* <span data-ttu-id="180ef-125">**Supprimer une image** : `Remove-AzureVMImage –ImageName "MyOldVmImage"`</span><span class="sxs-lookup"><span data-stu-id="180ef-125">**Delete an image**: `Remove-AzureVMImage –ImageName "MyOldVmImage"`</span></span>

## <a name="next-steps"></a><span data-ttu-id="180ef-126">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="180ef-126">Next Steps</span></span>
<span data-ttu-id="180ef-127">Vous pouvez également [créer un ordinateur Windows à l’aide de hello Azure portal](tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="180ef-127">You can also [create a Windows machine using hello Azure portal](tutorial.md).</span></span>
