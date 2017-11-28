---
title: "aaaAzure Machine virtuelle échelle jeux attachés des disques de données | Documents Microsoft"
description: "Découvrez comment toouse attachés des disques de données avec des machines virtuelles identiques"
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 4/25/2017
ms.author: guybo
ms.openlocfilehash: 77b66f80934c0aaf7bb1ad0de00a738052a878ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-vm-scale-sets-and-attached-data-disks"></a><span data-ttu-id="2f749-103">Groupes de machines virtuelles identiques Azure et disques de données associés</span><span class="sxs-lookup"><span data-stu-id="2f749-103">Azure VM scale sets and attached data disks</span></span>
<span data-ttu-id="2f749-104">Les [groupes de machines virtuelles identiques](/azure/virtual-machine-scale-sets/) Azure prennent désormais en charge les machines virtuelles avec des disques de données associés.</span><span class="sxs-lookup"><span data-stu-id="2f749-104">Azure [virtual machine scale sets](/azure/virtual-machine-scale-sets/) now support virtual machines with attached data disks.</span></span> <span data-ttu-id="2f749-105">Disques de données peuvent être définies dans le profil de stockage hello pour les jeux de mise à l’échelle qui ont été créés avec des disques gérés Azure.</span><span class="sxs-lookup"><span data-stu-id="2f749-105">Data disks can be defined in hello storage profile for scale sets that have been created with Azure Managed Disks.</span></span> <span data-ttu-id="2f749-106">Précédemment hello options de stockage directement connecté uniquement disponible avec des machines virtuelles dans le jeu de mise à l’échelle ont été les lecteurs de hello du système d’exploitation et les lecteurs temporaires.</span><span class="sxs-lookup"><span data-stu-id="2f749-106">Previously hello only directly attached storage options available with VMs in scale sets were hello OS drive and temp drives.</span></span>

> [!NOTE]
>  <span data-ttu-id="2f749-107">Lorsque vous créez une échelle avec des disques de données attaché définis, vous devez toujours toomount et hello du format disques à partir d’au sein d’une machine virtuelle toouse les (comme pour la version autonome de machines virtuelles Azure).</span><span class="sxs-lookup"><span data-stu-id="2f749-107">When you create a scale set with attached data disks defined, you still need toomount and format hello disks from within a VM toouse them (just like for standalone Azure VMs).</span></span> <span data-ttu-id="2f749-108">Un moyen pratique de toodo il s’agit de toouse une extension de script personnalisé qui appelle une toopartition script standard et de mettre en forme tous les disques de données hello sur une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="2f749-108">A convenient way toodo this is toouse a custom script extension which calls a standard script toopartition and format all hello data disks on a VM.</span></span>

## <a name="create-a-scale-set-with-attached-data-disks"></a><span data-ttu-id="2f749-109">Créer un groupe identique avec des disques de données associés</span><span class="sxs-lookup"><span data-stu-id="2f749-109">Create a scale set with attached data disks</span></span>
<span data-ttu-id="2f749-110">Un toocreate facilement une échelle définie avec les disques attachés est toouse hello [CLI d’Azure](https://github.com/Azure/azure-cli) _mise créer_ commande.</span><span class="sxs-lookup"><span data-stu-id="2f749-110">A simple way toocreate a scale set with attached disks is toouse hello [Azure CLI](https://github.com/Azure/azure-cli) _vmss create_ command.</span></span> <span data-ttu-id="2f749-111">Bonjour à l’exemple suivant crée un groupe de ressources Azure et un ensemble d’échelle de machine virtuelle de machines virtuelles Ubuntu 10, chacun avec des disques de données attaché 2 de 50 et 100 Go respectivement.</span><span class="sxs-lookup"><span data-stu-id="2f749-111">hello following example creates an Azure resource group, and a VM scale set of 10 Ubuntu VMs, each with 2 attached data disks, of 50 GB and 100 GB respectively.</span></span>
```bash
az group create -l southcentralus -n dsktest
az vmss create -g dsktest -n dskvmss --image ubuntults --instance-count 10 --data-disk-sizes-gb 50 100
```
<span data-ttu-id="2f749-112">Notez que hello _mise créer_ commande par défaut de certaines valeurs de configuration si vous ne spécifiez pas les.</span><span class="sxs-lookup"><span data-stu-id="2f749-112">Note that hello _vmss create_ command defaults certain configuration values if you do not specify them.</span></span> <span data-ttu-id="2f749-113">toosee hello options disponibles que vous pouvez remplacer try :</span><span class="sxs-lookup"><span data-stu-id="2f749-113">toosee hello available options that you can override try:</span></span>
```bash
az vmss create --help
```
<span data-ttu-id="2f749-114">Une autre façon toocreate une échelle avec des disques de données attachés est toodefine une échelle définie dans un modèle Azure Resource Manager, incluez un _dataDisks_ section Bonjour _storageProfile_et déployer hello modèle.</span><span class="sxs-lookup"><span data-stu-id="2f749-114">Another way toocreate a scale set with attached data disks is toodefine a scale set in an Azure Resource Manager template, include a _dataDisks_ section in hello _storageProfile_, and deploy hello template.</span></span> <span data-ttu-id="2f749-115">Hello 50 et 100 Go disque exemple ci-dessus est défini comme suit dans le modèle de hello :</span><span class="sxs-lookup"><span data-stu-id="2f749-115">hello 50 GB and 100 GB disk example above would be defined like this in hello template:</span></span>
```json
"dataDisks": [
    {
    "lun": 1,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 50
    },
    {
    "lun": 2,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 100
    }
]
```
<span data-ttu-id="2f749-116">Vous pouvez voir un exemple de toodeploy terminé, prêt d’un modèle de jeu de mise à l’échelle avec un disque connecté défini ici : [https://github.com/chagarw/MDPP/tree/master/101-vmss-os-data](https://github.com/chagarw/MDPP/tree/master/101-vmss-os-data).</span><span class="sxs-lookup"><span data-stu-id="2f749-116">You can see a complete, ready toodeploy example of a scale set template with an attached disk defined here: [https://github.com/chagarw/MDPP/tree/master/101-vmss-os-data](https://github.com/chagarw/MDPP/tree/master/101-vmss-os-data).</span></span>

## <a name="adding-a-data-disk-tooan-existing-scale-set"></a><span data-ttu-id="2f749-117">Ajout d’une échelle existant de tooan de disque de données définie</span><span class="sxs-lookup"><span data-stu-id="2f749-117">Adding a data disk tooan existing scale set</span></span>
> [!NOTE]
>  <span data-ttu-id="2f749-118">Vous pouvez joindre uniquement les données des disques tooa identiques qui a été créé avec [disques gérés d’Azure](./virtual-machine-scale-sets-managed-disks.md).</span><span class="sxs-lookup"><span data-stu-id="2f749-118">You can only attach data disks tooa scale set which has been created with [Azure Managed Disks](./virtual-machine-scale-sets-managed-disks.md).</span></span>

<span data-ttu-id="2f749-119">Vous pouvez ajouter une échelle de machine virtuelle données disque tooa définie à l’aide d’Azure CLI _attacher de disque de mise az_ commande.</span><span class="sxs-lookup"><span data-stu-id="2f749-119">You can add a data disk tooa VM scale set using Azure CLI _az vmss disk attach_ command.</span></span> <span data-ttu-id="2f749-120">Assurez-vous de spécifier un numéro d’unité logique (LUN) qui n’est pas déjà utilisé.</span><span class="sxs-lookup"><span data-stu-id="2f749-120">Make sure you specify a lun which is not already in use.</span></span> <span data-ttu-id="2f749-121">Hello CLI l’exemple suivant ajoute un toolun de lecteur 50 Go 3 :</span><span class="sxs-lookup"><span data-stu-id="2f749-121">hello following CLI example adds a 50 GB drive toolun 3:</span></span>
```bash
az vmss disk attach -g dsktest -n dskvmss --size-gb 50 --lun 3
```

<span data-ttu-id="2f749-122">Hello PowerShell l’exemple suivant ajoute un toolun de lecteur 50 Go 3 :</span><span class="sxs-lookup"><span data-stu-id="2f749-122">hello following PowerShell example adds a 50 GB drive toolun 3:</span></span>
```powershell
$vmss = Get-AzureRmVmss -ResourceGroupName myvmssrg -VMScaleSetName myvmss
$vmss = Add-AzureRmVmssDataDisk -VirtualMachineScaleSet $vmss -Lun 3 -Caching 'ReadWrite' -CreateOption Empty -DiskSizeGB 50 -StorageAccountType StandardLRS
Update-AzureRmVmss -ResourceGroupName myvmssrg -Name myvmss -VirtualMachineScaleSet $vmss
```

> [!NOTE]
> <span data-ttu-id="2f749-123">Différentes tailles de machine virtuelle ont des limites différentes sur les numéros de hello de disques attachés, qu'ils prennent en charge.</span><span class="sxs-lookup"><span data-stu-id="2f749-123">Different VM sizes have different limits on hello numbers of attached drives they support.</span></span> <span data-ttu-id="2f749-124">Vérifiez hello [caractéristiques de taille de machine virtuelle](../virtual-machines/windows/sizes.md) avant d’ajouter un nouveau disque.</span><span class="sxs-lookup"><span data-stu-id="2f749-124">Check hello [virtual machine size characteristics](../virtual-machines/windows/sizes.md) before adding a new disk.</span></span>

<span data-ttu-id="2f749-125">Vous pouvez également ajouter un disque en ajoutant un nouveau toohello d’entrée _dataDisks_ propriété Bonjour _storageProfile_ d’une échelle de définir la définition et l’application hello modification.</span><span class="sxs-lookup"><span data-stu-id="2f749-125">You can also add a disk by adding a new entry toohello _dataDisks_ property in hello _storageProfile_ of a scale set definition and applying hello change.</span></span> <span data-ttu-id="2f749-126">tootest, rechercher une définition de jeu de mise à l’échelle existante Bonjour [Explorateur de ressources Azure](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="2f749-126">tootest this, find an existing scale set definition in hello [Azure Resource Explorer](https://resources.azure.com/).</span></span> <span data-ttu-id="2f749-127">Sélectionnez _modifier_ et ajouter une nouvelle liste de disque toohello de disques de données.</span><span class="sxs-lookup"><span data-stu-id="2f749-127">Select _Edit_ and add a new disk toohello list of data disks.</span></span> <span data-ttu-id="2f749-128">Par exemple,</span><span class="sxs-lookup"><span data-stu-id="2f749-128">E.g.</span></span> <span data-ttu-id="2f749-129">à l’aide d’exemple hello ci-dessus :</span><span class="sxs-lookup"><span data-stu-id="2f749-129">using hello example above:</span></span>
```json
"dataDisks": [
    {
    "lun": 1,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 50
    },
    {
    "lun": 2,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 100
    },
    {
    "lun": 3,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 20
    }          
]
```

<span data-ttu-id="2f749-130">Puis sélectionnez _PUT_ tooapply hello modifie l’ensemble d’échelle tooyour.</span><span class="sxs-lookup"><span data-stu-id="2f749-130">Then select _PUT_ tooapply hello changes tooyour scale set.</span></span> <span data-ttu-id="2f749-131">Cet exemple doit fonctionner tant que vous utilisez une taille de machine virtuelle qui prend en charge plus de deux disques de données associés.</span><span class="sxs-lookup"><span data-stu-id="2f749-131">This example would work as long as you are using a VM size which supports more than two attached data disks.</span></span>

> [!NOTE]
> <span data-ttu-id="2f749-132">Lorsque vous effectuez une tooa modifier l’échelle définition telle que l’ajout ou la suppression d’un disque de données, il applique des machines virtuelles de tooall nouvellement créé, mais s’applique uniquement tooexisting VMs si hello _upgradePolicy_ propriété a la valeur trop « automatique ».</span><span class="sxs-lookup"><span data-stu-id="2f749-132">When you make a change tooa scale set definition such as adding or removing a data disk, it applies tooall newly created VMs, but only applies tooexisting VMs if hello _upgradePolicy_ property is set too"Automatic".</span></span> <span data-ttu-id="2f749-133">S’il est défini trop « manuel », vous devez toomanually appliquer hello nouveau modèle tooexisting machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="2f749-133">If it is set too"Manual", you need toomanually apply hello new model tooexisting VMs.</span></span> <span data-ttu-id="2f749-134">Vous pouvez faire cela dans portail de hello, à l’aide de hello _AzureRmVmssInstance de mise à jour_ PowerShell commande ou à l’aide de hello _mise à jour-les instances az mise_ commande CLI.</span><span class="sxs-lookup"><span data-stu-id="2f749-134">You can do this in hello portal, using hello _Update-AzureRmVmssInstance_ PowerShell command, or using hello _az vmss update-instances_ CLI command.</span></span>

## <a name="adding-pre-populated-data-disks-tooan-existent-scale-set"></a><span data-ttu-id="2f749-135">Ajout des données préremplie disques tooan inexistant identiques</span><span class="sxs-lookup"><span data-stu-id="2f749-135">Adding pre-populated data disks tooan existent scale set</span></span> 
> <span data-ttu-id="2f749-136">Lorsque vous ajoutez tooan disques inexistant ensemble d’échelle de modèle, par conception, disque de hello est toujours créé vide.</span><span class="sxs-lookup"><span data-stu-id="2f749-136">When you add disks tooan existent scale set model, by design, hello disk will always be created empty.</span></span> <span data-ttu-id="2f749-137">Ce scénario inclut également les nouvelles instances créées par un ensemble d’échelle hello.</span><span class="sxs-lookup"><span data-stu-id="2f749-137">This scenario also includes new instances created by hello scale set.</span></span> <span data-ttu-id="2f749-138">Ce comportement est, car la définition de scaleset hello possède un disque de données vide.</span><span class="sxs-lookup"><span data-stu-id="2f749-138">This behaviour is because hello scaleset definition has an empty data disk.</span></span> <span data-ttu-id="2f749-139">Dans l’ordre toocreate préremplie lecteurs de données pour un modèle de jeu de mise à l’échelle inexistant, vous pouvez choisir une des deux options suivantes :</span><span class="sxs-lookup"><span data-stu-id="2f749-139">In order toocreate pre-populated data drives for an existent scale set model, you can choose either of next two options:</span></span>

* <span data-ttu-id="2f749-140">Copier les données à partir de disques de données hello instance 0 machine virtuelle toohello Bonjour autres machines virtuelles en exécutant un script personnalisé.</span><span class="sxs-lookup"><span data-stu-id="2f749-140">Copy data from hello instance 0 VM toohello data disk(s) in hello other VMs by running a custom script.</span></span>
* <span data-ttu-id="2f749-141">Créer une image managée avec un disque de hello du système d’exploitation plus de disque de données (avec des données hello requis) et créer un nouveau scaleset avec l’image de hello.</span><span class="sxs-lookup"><span data-stu-id="2f749-141">Create a managed image with hello OS disk plus data disk (with hello required data) and create a new scaleset with hello image.</span></span> <span data-ttu-id="2f749-142">Ainsi, chaque nouvelle machine virtuelle créée aura une donnée de disque qui est fourni dans la définition de hello de hello scaleset.</span><span class="sxs-lookup"><span data-stu-id="2f749-142">This way every new VM created will have a data disk that that is provided in hello definition of hello scaleset.</span></span> <span data-ttu-id="2f749-143">Étant donné que cette définition fait référence image tooan avec un disque de données qui a des données personnalisées, chaque ordinateur virtuel sur hello scaleset automatiquement s’avec ces modifications.</span><span class="sxs-lookup"><span data-stu-id="2f749-143">Since this definition will refer tooan image with a data disk that has customized data, every virtual machine on hello scaleset will automatically come up with these changes.</span></span>

> <span data-ttu-id="2f749-144">Hello toocreate façon une image personnalisée se trouve ici : [créer une image managée d’une machine virtuelle généralisée dans Azure](/azure/virtual-machines/windows/capture-image-resource/)</span><span class="sxs-lookup"><span data-stu-id="2f749-144">hello way toocreate a custom image can be found here: [Create a managed image of a generalized VM in Azure](/azure/virtual-machines/windows/capture-image-resource/)</span></span> 

> <span data-ttu-id="2f749-145">utilisateur Hello doit toocapture hello d’instance 0 machine virtuelle qui a hello les données requises et ensuite utiliser ce disque dur virtuel pour la définition d’image hello.</span><span class="sxs-lookup"><span data-stu-id="2f749-145">hello user needs toocapture hello instance 0 VM which has hello required data, and then use that vhd for hello image definition.</span></span>

## <a name="removing-a-data-disk-from-a-scale-set"></a><span data-ttu-id="2f749-146">Supprimer un disque de données d’un groupe identique</span><span class="sxs-lookup"><span data-stu-id="2f749-146">Removing a data disk from a scale set</span></span>
<span data-ttu-id="2f749-147">Vous pouvez supprimer un disque de données d’un groupe de machines virtuelles identiques à l’aide de la commande _az vmss disk detach_ d’Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="2f749-147">You can remove a data disk from a VM scale set using Azure CLI _az vmss disk detach_ command.</span></span> <span data-ttu-id="2f749-148">Par exemple hello commande suivante supprime hello disque défini au numéro d’unité logique 2 :</span><span class="sxs-lookup"><span data-stu-id="2f749-148">For example hello following command removes hello disk defined at lun 2:</span></span>
```bash
az vmss disk detach -g dsktest -n dskvmss --lun 2
```  
<span data-ttu-id="2f749-149">De même, vous pouvez également supprimer un disque à partir d’une mise à l’échelle en supprimant une entrée à partir de hello _dataDisks_ propriété Bonjour _storageProfile_ et l’application des modifications de hello.</span><span class="sxs-lookup"><span data-stu-id="2f749-149">Similarly you can also remove a disk from a scale set by removing an entry from hello _dataDisks_ property in hello _storageProfile_ and applying hello change.</span></span> 

## <a name="additional-notes"></a><span data-ttu-id="2f749-150">Remarques supplémentaires</span><span class="sxs-lookup"><span data-stu-id="2f749-150">Additional notes</span></span>
<span data-ttu-id="2f749-151">Prise en charge pour disques de données associés de jeu de disques gérés par Azure et l’échelle est disponible dans la version de l’API [ _2016-04-30-preview_ ](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-compute/2016-04-30-preview/swagger/compute.json) ou version ultérieure de hello Microsoft.Compute API.</span><span class="sxs-lookup"><span data-stu-id="2f749-151">Support for Azure Managed disks and scale set attached data disks is available in API version [_2016-04-30-preview_](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-compute/2016-04-30-preview/swagger/compute.json) or later of hello Microsoft.Compute API.</span></span>

<span data-ttu-id="2f749-152">Dans l’implémentation initiale de hello de prise en charge des disques attachés pour les jeux de mise à l’échelle, vous ne peut pas attacher ou détacher des disques de données vers ou depuis des ordinateurs virtuels individuels dans un ensemble d’échelle.</span><span class="sxs-lookup"><span data-stu-id="2f749-152">In hello initial implementation of attached disk support for scale sets, you cannot attach or detach data disks to/from individual VMs in a scale set.</span></span>

<span data-ttu-id="2f749-153">La prise en charge du portail Azure pour les disques de données associés dans des groupes identiques est initialement limitée.</span><span class="sxs-lookup"><span data-stu-id="2f749-153">Azure portal support for attached data disks in scale sets is initially limited.</span></span> <span data-ttu-id="2f749-154">Selon vos besoins, que vous pouvez utiliser les modèles Azure, toomanage CLI, PowerShell, kits de développement logiciel et API REST de disques attachés.</span><span class="sxs-lookup"><span data-stu-id="2f749-154">Depending on your requirements you can use Azure templates, CLI, PowerShell, SDKs, and REST API toomanage attached disks.</span></span>


