---
title: aaaFrequently aux questions sur la pile de Azure | Documents Microsoft
description: "Pile Azure les questions fréquemment posées."
services: azure-stack
documentationcenter: 
author: HeathL17
manager: byronr
editor: 
ms.assetid: 028479e4-a17e-43c7-885c-cb2130f850d2
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/17/2017
ms.author: helaw
ms.openlocfilehash: aa6f8afbb319e7c8999ce35edcb7ef968f34a0c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-azure-stack"></a><span data-ttu-id="1bdbe-103">Forum aux questions sur la pile de Azure</span><span class="sxs-lookup"><span data-stu-id="1bdbe-103">Frequently asked questions for Azure Stack</span></span>
## <a name="deployment"></a><span data-ttu-id="1bdbe-104">Déploiement</span><span class="sxs-lookup"><span data-stu-id="1bdbe-104">Deployment</span></span>
### <a name="do-i-need-tooformat-my-data-disks-before-starting-or-restarting-an-installation"></a><span data-ttu-id="1bdbe-105">Dois-je tooformat mes disques de données avant de démarrer ou redémarrer une installation ?</span><span class="sxs-lookup"><span data-stu-id="1bdbe-105">Do I need tooformat my data disks before starting or restarting an installation?</span></span>
<span data-ttu-id="1bdbe-106">Disques doivent être au format brut.</span><span class="sxs-lookup"><span data-stu-id="1bdbe-106">Disks should be in raw format.</span></span> <span data-ttu-id="1bdbe-107">Si vous réinstallez le système d’exploitation de hello, devez toocheck si le pool de stockage ancien hello est encore présent, vous supprimer à l’aide de hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="1bdbe-107">If you reinstall hello operating system, you may need toocheck if hello old storage pool is still present and delete using hello following steps:</span></span>

1. <span data-ttu-id="1bdbe-108">Ouvrez le Gestionnaire de serveurs.</span><span class="sxs-lookup"><span data-stu-id="1bdbe-108">Open Server Manager.</span></span>
2. <span data-ttu-id="1bdbe-109">Sélectionnez les Pools de stockage.</span><span class="sxs-lookup"><span data-stu-id="1bdbe-109">Select Storage Pools.</span></span>
3. <span data-ttu-id="1bdbe-110">Voir si un pool de stockage est répertorié.</span><span class="sxs-lookup"><span data-stu-id="1bdbe-110">See if a storage pool is listed.</span></span>
4. <span data-ttu-id="1bdbe-111">Avec le bouton droit **pool de stockage** si répertoriés et activer en lecture / écriture.</span><span class="sxs-lookup"><span data-stu-id="1bdbe-111">Right-click **storage pool** if listed and enable read / write.</span></span>
5. <span data-ttu-id="1bdbe-112">Avec le bouton droit **disque dur virtuel** (en bas à gauche), puis sélectionnez Supprimer.</span><span class="sxs-lookup"><span data-stu-id="1bdbe-112">Right-click **Virtual Hard Disk** (Lower left corner) and select delete.</span></span>
6. <span data-ttu-id="1bdbe-113">Avec le bouton droit **Pool de stockage** et cliquez sur Supprimer.</span><span class="sxs-lookup"><span data-stu-id="1bdbe-113">Right-click **Storage Pool** and click delete.</span></span>
7. <span data-ttu-id="1bdbe-114">Relancez le script de la pile d’Azure et vérifiez que passe la vérification de disque hello.</span><span class="sxs-lookup"><span data-stu-id="1bdbe-114">Launch Azure Stack script again and verify that hello disk verification passes.</span></span>

<span data-ttu-id="1bdbe-115">Si vous le souhaitez, hello script suivant peut être utilisé :</span><span class="sxs-lookup"><span data-stu-id="1bdbe-115">Optionally, hello following script can be used:</span></span>

```PowerShell
$pools = Get-StoragePool -IsPrimordial $False -ErrorVariable Err -ErrorAction SilentlyContinue
if ($pools -ne $null) {
  $pools| Set-StoragePool -IsReadOnly $False -ErrorVariable Err -ErrorAction SilentlyContinue
  $pools = Get-StoragePool -IsPrimordial $False -ErrorVariable Err -ErrorAction SilentlyContinue
  $pools | Get-VirtualDisk | Remove-VirtualDisk -Confirm:$False
  $pools | Remove-StoragePool -Confirm:$False
}
```

### <a name="can-i-use-all-ssd-disks-for-hello-storage-pool-in-hello-poc-installation"></a><span data-ttu-id="1bdbe-116">Puis-je utiliser tous les disques SSD pour le pool de stockage hello Bonjour installation de preuve de concept ?</span><span class="sxs-lookup"><span data-stu-id="1bdbe-116">Can I use all SSD disks for hello storage pool in hello POC installation?</span></span>
<span data-ttu-id="1bdbe-117">Pour plus d’informations sur les configurations de stockage, consultez hello [guide des spécifications](azure-stack-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="1bdbe-117">For more information on storage configurations, see hello [requirements guide](azure-stack-deploy.md).</span></span>

### <a name="can-i-use-nvme-data-disks-for-hello-microsoft-azure-stack-poc"></a><span data-ttu-id="1bdbe-118">Puis-je utiliser des disques de données NVMe pour hello preuve de concept pile Microsoft Azure ?</span><span class="sxs-lookup"><span data-stu-id="1bdbe-118">Can I use NVMe data disks for hello Microsoft Azure Stack POC?</span></span>
<span data-ttu-id="1bdbe-119">Espaces de stockage Direct prend en charge les disques NVMe, pile de Azure ne prend en charge un sous-ensemble des types de lecteurs de hello et combinaisons possibles des espaces de stockage Direct.</span><span class="sxs-lookup"><span data-stu-id="1bdbe-119">While Storage Spaces Direct supports NVMe disks, Azure Stack only supports a subset of hello possible drive types and combinations possible for Storage Spaces Direct.</span></span>  <span data-ttu-id="1bdbe-120">Consultez hello [guide des spécifications](azure-stack-deploy.md) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="1bdbe-120">See hello [requirements guide](azure-stack-deploy.md) for more information.</span></span> 

### <a name="how-can-i-reinstall-azure-stack"></a><span data-ttu-id="1bdbe-121">Comment puis-je réinstaller Azure pile ?</span><span class="sxs-lookup"><span data-stu-id="1bdbe-121">How can I reinstall Azure Stack?</span></span>
<span data-ttu-id="1bdbe-122">Vous pouvez suivre les étapes de hello Bonjour [guide de redéploiement](azure-stack-redeploy.md).</span><span class="sxs-lookup"><span data-stu-id="1bdbe-122">You can follow hello steps in hello [redeployment guide](azure-stack-redeploy.md).</span></span>  

## <a name="tenant"></a><span data-ttu-id="1bdbe-123">Locataire</span><span class="sxs-lookup"><span data-stu-id="1bdbe-123">Tenant</span></span>
### <a name="can-i-deploy-my-own-images-as-a-tenant"></a><span data-ttu-id="1bdbe-124">Puis-je déployer mon propre images en tant que client ?</span><span class="sxs-lookup"><span data-stu-id="1bdbe-124">Can I deploy my own images as a tenant?</span></span>
<span data-ttu-id="1bdbe-125">Oui, tout comme dans Azure, un client peut télécharger des images dans la pile d’Azure, en outre images hello toousing hello administrateur de service.</span><span class="sxs-lookup"><span data-stu-id="1bdbe-125">Yes, just like in Azure, a tenant can upload images in Azure Stack, in addition toousing hello images from hello service administrator.</span></span> <span data-ttu-id="1bdbe-126">Pour une vue d’ensemble, consultez hello [Ajout d’une Image de machine virtuelle](azure-stack-add-vm-image.md).</span><span class="sxs-lookup"><span data-stu-id="1bdbe-126">For an overview, see hello [Adding a VM Image](azure-stack-add-vm-image.md).</span></span> 

## <a name="testing"></a><span data-ttu-id="1bdbe-127">Test</span><span class="sxs-lookup"><span data-stu-id="1bdbe-127">Testing</span></span>
### <a name="can-i-use-nested-virtualization-tootest-hello-microsoft-azure-stack-poc"></a><span data-ttu-id="1bdbe-128">Puis-je utiliser hello tootest de virtualisation imbriquée preuve de concept pile Microsoft Azure ?</span><span class="sxs-lookup"><span data-stu-id="1bdbe-128">Can I use Nested Virtualization tootest hello Microsoft Azure Stack POC?</span></span>
<span data-ttu-id="1bdbe-129">La virtualisation imbriquée n’est pas pris en charge ou n’est pas testée avec Azure pile Technical Preview 3.</span><span class="sxs-lookup"><span data-stu-id="1bdbe-129">Nested virtualization is not supported or tested with Azure Stack Technical Preview 3.</span></span>

## <a name="virtual-machines"></a><span data-ttu-id="1bdbe-130">Machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="1bdbe-130">Virtual machines</span></span>
### <a name="does-azure-stack-support-dynamic-disks-for-virtual-machines"></a><span data-ttu-id="1bdbe-131">Pile de Azure prend-il en charge les disques dynamiques pour les ordinateurs virtuels ?</span><span class="sxs-lookup"><span data-stu-id="1bdbe-131">Does Azure Stack support dynamic disks for virtual machines?</span></span>
<span data-ttu-id="1bdbe-132">Pile Azure ne prend pas en charge les disques dynamiques.</span><span class="sxs-lookup"><span data-stu-id="1bdbe-132">Azure Stack does not support dynamic disks.</span></span>


## <a name="next-steps"></a><span data-ttu-id="1bdbe-133">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1bdbe-133">Next steps</span></span>
[<span data-ttu-id="1bdbe-134">Dépannage</span><span class="sxs-lookup"><span data-stu-id="1bdbe-134">Troubleshooting</span></span>](azure-stack-troubleshooting.md)

