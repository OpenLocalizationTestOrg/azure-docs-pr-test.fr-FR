---
title: "ensemble d’une échelle de machine virtuelle Azure aaaUpgrade | Documents Microsoft"
description: "Mettre à niveau un groupe de machines virtuelles identiques Azure"
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e229664e-ee4e-4f12-9d2e-a4f456989e5d
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: guybo
ms.openlocfilehash: 068e98503f8d37ea71e45b8673a01da2e814f521
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-a-virtual-machine-scale-set"></a><span data-ttu-id="afe17-103">Mettre à niveau un jeu de mise à l’échelle de machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="afe17-103">Upgrade a virtual machine scale set</span></span>
<span data-ttu-id="afe17-104">Cet article décrit comment vous pouvez déployer une échelle de machine virtuelle Azure du système d’exploitation mise à jour tooan définir sans interruption de service.</span><span class="sxs-lookup"><span data-stu-id="afe17-104">This article describes how you can roll out an OS update tooan Azure virtual machine scale set without any downtime.</span></span> <span data-ttu-id="afe17-105">Dans ce contexte, une mise à jour du système d’exploitation implique la modification de la version de hello ou référence (SKU) de hello du système d’exploitation ou la modification de hello URI d’une image personnalisée.</span><span class="sxs-lookup"><span data-stu-id="afe17-105">In this context, an OS update involves changing hello version or SKU of hello OS or changing hello URI of a custom image.</span></span> <span data-ttu-id="afe17-106">Une mise à jour sans interruption de service consiste à mettre à jour des machines virtuelles une par une, ou dans des groupes (par exemple, un domaine d’erreur à la fois), plutôt que toutes simultanément.</span><span class="sxs-lookup"><span data-stu-id="afe17-106">Updating without downtime means updating virtual machines one at a time or in groups (such as one fault domain at a time) rather than all at once.</span></span> <span data-ttu-id="afe17-107">En procédant de la sorte, les machines virtuelles qui ne sont pas mises à niveau peuvent continuer à opérer.</span><span class="sxs-lookup"><span data-stu-id="afe17-107">By doing so, any virtual machines that are not being upgraded can keep running.</span></span>

<span data-ttu-id="afe17-108">tooavoid ambiguïté, nous allons faire la distinction quatre types de mise à jour du système d’exploitation vous pourriez tooperform :</span><span class="sxs-lookup"><span data-stu-id="afe17-108">tooavoid ambiguity, let’s distinguish four types of OS update you might want tooperform:</span></span>

* <span data-ttu-id="afe17-109">Modification de version de hello ou référence (SKU) d’une image de plateforme.</span><span class="sxs-lookup"><span data-stu-id="afe17-109">Changing hello version or SKU of a platform image.</span></span> <span data-ttu-id="afe17-110">Par exemple, la modification Ubuntu version 14.04.2-LTS 14.04.201506100 too14.04.201507060 ou la modification de hello Ubuntu 15.10 ou la dernière référence (SKU) too16.04.0-LTS/latest.</span><span class="sxs-lookup"><span data-stu-id="afe17-110">For example, changing Ubuntu 14.04.2-LTS version from 14.04.201506100 too14.04.201507060, or changing hello Ubuntu 15.10/latest SKU too16.04.0-LTS/latest.</span></span> <span data-ttu-id="afe17-111">Ce scénario est décrit dans cet article.</span><span class="sxs-lookup"><span data-stu-id="afe17-111">This scenario is covered in this article.</span></span>
* <span data-ttu-id="afe17-112">La modification hello URI qui pointe de tooa une nouvelle version d’une image personnalisée que vous avez créé (**propriétés** > **virtualMachineProfile** > **storageProfile**  >  **osDisk** > **image** > **uri**).</span><span class="sxs-lookup"><span data-stu-id="afe17-112">Changing hello URI that points tooa new version of a custom image you built (**properties** > **virtualMachineProfile** > **storageProfile** > **osDisk** > **image** > **uri**).</span></span> <span data-ttu-id="afe17-113">Ce scénario est décrit dans cet article.</span><span class="sxs-lookup"><span data-stu-id="afe17-113">This scenario is covered in this article.</span></span>
* <span data-ttu-id="afe17-114">Modification de référence à l’image d’un ensemble d’échelle qui a été créé à l’aide de disques gérés d’Azure hello.</span><span class="sxs-lookup"><span data-stu-id="afe17-114">Changing hello image reference of a scale set that was created using Azure Managed Disks.</span></span>
* <span data-ttu-id="afe17-115">Mise à jour corrective hello du système d’exploitation à partir d’un ordinateur virtuel (des exemples l’installation d’un correctif de sécurité et de mise à jour de Windows en cours d’exécution).</span><span class="sxs-lookup"><span data-stu-id="afe17-115">Patching hello OS from within a virtual machine (examples of this include installing a security patch and running Windows Update).</span></span> <span data-ttu-id="afe17-116">Ce scénario est pris en charge mais n’est pas traité dans cet article.</span><span class="sxs-lookup"><span data-stu-id="afe17-116">This scenario is supported but not covered in this article.</span></span>

<span data-ttu-id="afe17-117">Les jeux de mise à l’échelle de machine virtuelle déployés en tant que partie d’un cluster [Azure Service Fabric](https://azure.microsoft.com/services/service-fabric/) ne sont pas abordés ici.</span><span class="sxs-lookup"><span data-stu-id="afe17-117">Virtual machine scale sets that are deployed as part of an [Azure Service Fabric](https://azure.microsoft.com/services/service-fabric/) cluster are not covered here.</span></span> <span data-ttu-id="afe17-118">Pour plus d’informations sur la mise à jour corrective de Service Fabric, consultez [Application pour appliquer des correctifs au système d’exploitation Windows dans votre cluster Service Fabric](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-patch-orchestration-application).</span><span class="sxs-lookup"><span data-stu-id="afe17-118">See [Patch Windows OS in your Service Fabric cluster](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-patch-orchestration-application) for more information about patching Service Fabric.</span></span>

<span data-ttu-id="afe17-119">Hello base séquence pour la modification hello du système d’exploitation version/référence (SKU) d’une image de plateforme ou hello URI d’une image personnalisée se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="afe17-119">hello basic sequence for changing hello OS version/SKU of a platform image or hello URI of a custom image looks as follows:</span></span>

1. <span data-ttu-id="afe17-120">Obtenir le modèle du jeu de mise à l’échelle hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="afe17-120">Get hello virtual machine scale set model.</span></span>
2. <span data-ttu-id="afe17-121">Modifier la version hello, référence (SKU), référence d’image ou valeur de l’URI dans le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="afe17-121">Change hello version, SKU, image reference, or URI value in hello model.</span></span>
3. <span data-ttu-id="afe17-122">Modèle de mise à jour hello.</span><span class="sxs-lookup"><span data-stu-id="afe17-122">Update hello model.</span></span>
4. <span data-ttu-id="afe17-123">Effectuez un *manualUpgrade* appeler sur des machines virtuelles de hello dans un ensemble d’échelle hello.</span><span class="sxs-lookup"><span data-stu-id="afe17-123">Do a *manualUpgrade* call on hello virtual machines in hello scale set.</span></span> <span data-ttu-id="afe17-124">Cette étape est uniquement pertinente si *upgradePolicy* est défini trop**manuel** dans votre échelle définie.</span><span class="sxs-lookup"><span data-stu-id="afe17-124">This step is only relevant if *upgradePolicy* is set too**Manual** in your scale set.</span></span> <span data-ttu-id="afe17-125">S’il est défini trop**automatique**, tous les ordinateurs virtuels hello sont mis à niveau à la fois, provoquant ainsi des temps d’arrêt.</span><span class="sxs-lookup"><span data-stu-id="afe17-125">If it is set too**Automatic**, all hello virtual machines are upgraded at once, thus causing downtime.</span></span>

<span data-ttu-id="afe17-126">Avec ces informations à l’esprit, voyons comment vous pourriez mettre à jour la version hello d’une échelle définie dans PowerShell et à l’aide des API REST de hello.</span><span class="sxs-lookup"><span data-stu-id="afe17-126">With this information in mind, let’s see how you could update hello version of a scale set in PowerShell, and by using hello REST API.</span></span> <span data-ttu-id="afe17-127">Ces exemples couvrent les cas de hello d’une image de plateforme, mais cet article fournit suffisamment d’informations pour vous tooadapt cette image personnalisée de tooa de processus.</span><span class="sxs-lookup"><span data-stu-id="afe17-127">These examples cover hello case of a platform image, but this article provides enough information for you tooadapt this process tooa custom image.</span></span>

## <a name="powershell"></a><span data-ttu-id="afe17-128">PowerShell</span><span class="sxs-lookup"><span data-stu-id="afe17-128">PowerShell</span></span>
<span data-ttu-id="afe17-129">Cet exemple met à jour un ensemble d’échelle de machine virtuelle Windows (création toohello utitlisez 4.0.20160229.</span><span class="sxs-lookup"><span data-stu-id="afe17-129">This example updates a Windows virtual machine scale set (creating toohello new version 4.0.20160229.</span></span> <span data-ttu-id="afe17-130">Après la mise à jour du modèle de hello, il effectue une mise à jour une instance de machine virtuelle à la fois.</span><span class="sxs-lookup"><span data-stu-id="afe17-130">After updating hello model, it does an update one virtual machine instance at a time.</span></span>

```powershell
$rgname = "myrg"
$vmssname = "myvmss"
$newversion = "4.0.20160229"
$instanceid = "1"

# get hello VMSS model
$vmss = Get-AzureRmVmss -ResourceGroupName $rgname -VMScaleSetName $vmssname

# set hello new version in hello model data
$vmss.virtualMachineProfile.storageProfile.imageReference.version = $newversion

# update hello virtual machine scale set model
Update-AzureRmVmss -ResourceGroupName $rgname -Name $vmssname -VirtualMachineScaleSet $vmss

# now start updating instances
Update-AzureRmVmssInstance -ResourceGroupName $rgname -VMScaleSetName $vmssname -InstanceId $instanceId
```

<span data-ttu-id="afe17-131">Si vous mettez à jour hello URI pour une image personnalisée au lieu de modifier une version d’image de plateforme, remplacez hello « jeu hello nouvelle version » ligne avec une commande qui met à jour hello URI de l’image source.</span><span class="sxs-lookup"><span data-stu-id="afe17-131">If you are updating hello URI for a custom image instead of changing a platform image version, replace hello “set hello new version” line with a command that will update hello source image URI.</span></span> <span data-ttu-id="afe17-132">Par exemple, si un ensemble d’échelle hello a été créé sans l’aide de disques gérés d’Azure, mise à jour hello ressemble à cela :</span><span class="sxs-lookup"><span data-stu-id="afe17-132">For example, if hello scale set was created without using Azure Managed Disks, hello update would look like this:</span></span>

```powershell
# set hello new version in hello model data
$vmss.virtualMachineProfile.storageProfile.osDisk.image.uri= $newURI
```

<span data-ttu-id="afe17-133">Si une image personnalisée en fonction de l’ensemble d’échelle a été créé à l’aide de disques gérés Azure, référence d’image hello est mise à jour.</span><span class="sxs-lookup"><span data-stu-id="afe17-133">If a custom image based scale set was created using Azure Managed Disks, then hello image reference would be updated.</span></span> <span data-ttu-id="afe17-134">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="afe17-134">For example:</span></span>

```powershell
# set hello new version in hello model data
$vmss.virtualMachineProfile.storageProfile.imageReference.id = $newImageReference
```

## <a name="hello-rest-api"></a><span data-ttu-id="afe17-135">Hello API REST</span><span class="sxs-lookup"><span data-stu-id="afe17-135">hello REST API</span></span>
<span data-ttu-id="afe17-136">Voici quelques exemples de Python qui utilisent tooroll d’API REST Azure hello une mise à jour de la version du système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="afe17-136">Here are a couple of Python examples that use hello Azure REST API tooroll out an OS version update.</span></span> <span data-ttu-id="afe17-137">Les deux utilisent lightweight de hello [azurerm](https://pypi.python.org/pypi/azurerm) bibliothèque d’API REST Azure wrapper fonctions toodo une opération GET sur l’échelle de hello définie le modèle, suivie d’une commande PUT avec un modèle mis à jour.</span><span class="sxs-lookup"><span data-stu-id="afe17-137">Both use hello lightweight [azurerm](https://pypi.python.org/pypi/azurerm) library of Azure REST API wrapper functions toodo a GET on hello scale set model, followed by a PUT with an updated model.</span></span> <span data-ttu-id="afe17-138">Elles apparaîtront également dans les vues des instances de machine virtuelle virtuels tooidentify hello par domaine de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="afe17-138">They also look at virtual machine instances views tooidentify hello virtual machines by update domain.</span></span>

### <a name="vmssupgrade"></a><span data-ttu-id="afe17-139">vmssupgrade</span><span class="sxs-lookup"><span data-stu-id="afe17-139">Vmssupgrade</span></span>
 <span data-ttu-id="afe17-140">[Vmssupgrade](https://github.com/gbowerman/vmsstools) est un script Python qui a utilisé tooroll out une tooa de mise à niveau du système d’exploitation en cours d’exécution échelle de machines virtuelles définie un domaine de mise à jour à la fois.</span><span class="sxs-lookup"><span data-stu-id="afe17-140">[Vmssupgrade](https://github.com/gbowerman/vmsstools) is a Python script that's used tooroll out an OS upgrade tooa running virtual machine scale set one update domain at a time.</span></span>

![Script Vmssupgrade pour le choix de machines virtuelles ou d’un domaine de mise à jour](./media/virtual-machine-scale-sets-upgrade-scale-set/vmssupgrade-screenshot.png)

<span data-ttu-id="afe17-142">Ce script vous permet de choisir les ordinateurs virtuels spécifiques tooupdate ou spécifier un domaine de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="afe17-142">This script lets you choose specific virtual machines tooupdate or specify an update domain.</span></span> <span data-ttu-id="afe17-143">Il prend en charge la modification d’une version d’image de plateforme ou la modification de hello URI d’une image personnalisée.</span><span class="sxs-lookup"><span data-stu-id="afe17-143">It supports changing a platform image version or changing hello URI of a custom image.</span></span>

### <a name="vmsseditor"></a><span data-ttu-id="afe17-144">Vmsseditor</span><span class="sxs-lookup"><span data-stu-id="afe17-144">Vmsseditor</span></span>
<span data-ttu-id="afe17-145">[Vmsseditor](https://github.com/gbowerman/vmssdashboard) est un éditeur d’usage général pour les jeux de mise à l’échelle de machine virtuelle qui montre un état de machine virtuelle sous la forme d’une carte thermique où une ligne représente un domaine de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="afe17-145">[Vmsseditor](https://github.com/gbowerman/vmssdashboard) is a general-purpose editor for virtual machine scale sets that shows virtual machine status as a heatmap where one row represents one update domain.</span></span> <span data-ttu-id="afe17-146">Entre autres choses, vous pouvez mettre à jour le modèle hello pour un ensemble d’échelle avec une nouvelle version, une référence (SKU) ou un URI d’image personnalisée et choisissez tooupgrade de domaines d’erreur.</span><span class="sxs-lookup"><span data-stu-id="afe17-146">Among other things, you can update hello model for a scale set with a new version, SKU, or custom image URI, and then pick fault domains tooupgrade.</span></span> <span data-ttu-id="afe17-147">Lorsque vous procédez ainsi, tous les ordinateurs virtuels hello dans ce domaine de mise à jour sont mis à niveau toohello nouveau modèle.</span><span class="sxs-lookup"><span data-stu-id="afe17-147">When you do so, all hello virtual machines in that update domain are upgraded toohello new model.</span></span> <span data-ttu-id="afe17-148">Vous pouvez également effectuer une mise à niveau propagée, selon la taille de lot hello de votre choix.</span><span class="sxs-lookup"><span data-stu-id="afe17-148">Alternatively, you can do a rolling upgrade based on hello batch size of your choice.</span></span>  

<span data-ttu-id="afe17-149">Hello capture d’écran suivante montre un modèle d’une échelle définie pour Ubuntu 14.04-2LTS version 14.04.201507060.</span><span class="sxs-lookup"><span data-stu-id="afe17-149">hello following screenshot shows a model of a scale set for Ubuntu 14.04-2LTS version 14.04.201507060.</span></span> <span data-ttu-id="afe17-150">Toothis outil ont été ajoutées aux nombreuses autres options dans la mesure où cette capture d’écran a été effectuée.</span><span class="sxs-lookup"><span data-stu-id="afe17-150">Many more options have been added toothis tool since this screenshot was taken.</span></span>

![Modèle Vmsseditor d’un ensemble d’échelle pour Ubuntu 14.04-2LTS](./media/virtual-machine-scale-sets-upgrade-scale-set/vmssEditor1.png)

<span data-ttu-id="afe17-152">Après avoir cliqué sur **mise à niveau** , puis **obtenir les détails**, machines virtuelles dans UD 0 démarrer tooupdate.</span><span class="sxs-lookup"><span data-stu-id="afe17-152">After you click **Upgrade** and then **Get Details**, virtual machines in UD 0 start tooupdate.</span></span>

![Vmsseditor montrant la progression de la mise à jour](./media/virtual-machine-scale-sets-upgrade-scale-set/vmssEditor2.png)

