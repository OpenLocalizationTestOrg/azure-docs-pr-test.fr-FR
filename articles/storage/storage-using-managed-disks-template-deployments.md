---
title: "aaaUsing gérés disques dans les modèles Azure Resource Manager | Documents Microsoft"
description: "Décrit en détail comment toouse gérées misks dans les modèles Azure Resource Manager"
services: storage
documentationcenter: 
author: jboeshart
manager: 
ms.service: storage
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage
ms.date: 06/01/2017
ms.author: jaboes
ms.openlocfilehash: ea83f4ed11acfd8f642dbc8331fa8cf077ef577c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-managed-disks-in-azure-resource-manager-templates"></a><span data-ttu-id="42080-103">Utilisation de disques gérés dans les modèles Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="42080-103">Using Managed Disks in Azure Resource Manager Templates</span></span>

<span data-ttu-id="42080-104">Ce document décrit les différences de hello entre disques managées et non managées, avec des machines virtuelles du tooprovision de modèles Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="42080-104">This document walks through hello differences between managed and unmanaged disks when using Azure Resource Manager templates tooprovision virtual machines.</span></span> <span data-ttu-id="42080-105">Cela vous permet de tooupdate les modèles existants qui utilisent des disques toomanaged disques non managés.</span><span class="sxs-lookup"><span data-stu-id="42080-105">This will help you tooupdate existing templates that are using unmanaged Disks toomanaged disks.</span></span> <span data-ttu-id="42080-106">Pour référence, nous utilisons hello [101-vm-simple-windows](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows) modèle comme guide.</span><span class="sxs-lookup"><span data-stu-id="42080-106">For reference, we are using hello [101-vm-simple-windows](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows) template as a guide.</span></span> <span data-ttu-id="42080-107">Vous pouvez voir le modèle hello à l’aide de deux [des disques gérés par](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows/azuredeploy.json) une version antérieure à l’aide de [non managée disques](https://github.com/Azure/azure-quickstart-templates/tree/93b5f72a9857ea9ea43e87d2373bf1b4f724c6aa/101-vm-simple-windows/azuredeploy.json) si vous souhaitez que toodirectly les comparer.</span><span class="sxs-lookup"><span data-stu-id="42080-107">You can see hello template using both [managed Disks](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows/azuredeploy.json) and a prior version using [unmanaged disks](https://github.com/Azure/azure-quickstart-templates/tree/93b5f72a9857ea9ea43e87d2373bf1b4f724c6aa/101-vm-simple-windows/azuredeploy.json) if you'd like toodirectly compare them.</span></span>

## <a name="unmanaged-disks-template-formatting"></a><span data-ttu-id="42080-108">Mise en forme de modèle de disques non gérés</span><span class="sxs-lookup"><span data-stu-id="42080-108">Unmanaged Disks template formatting</span></span>

<span data-ttu-id="42080-109">toobegin, nous nous intéressons à des disques comment non managées sont déployés.</span><span class="sxs-lookup"><span data-stu-id="42080-109">toobegin, we take a look at how unmanaged disks are deployed.</span></span> <span data-ttu-id="42080-110">Lorsque vous créez des disques non managés, vous avez besoin d’un fichier de disque dur virtuel de stockage compte toohold hello.</span><span class="sxs-lookup"><span data-stu-id="42080-110">When creating unmanaged disks, you need a storage account toohold hello VHD files.</span></span> <span data-ttu-id="42080-111">Vous pouvez créer un compte de stockage ou en utiliser un existant.</span><span class="sxs-lookup"><span data-stu-id="42080-111">You can create a new storage account or use one that already exists.</span></span> <span data-ttu-id="42080-112">Cet article vous indiquent comment toocreate un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="42080-112">This article will show you how toocreate a new storage account.</span></span> <span data-ttu-id="42080-113">tooaccomplish, vous avez besoin d’une ressource de compte de stockage dans le bloc de ressources hello comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="42080-113">tooaccomplish this, you need a storage account resource in hello resources block as shown below.</span></span>

```
{
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[variables('storageAccountName')]",
    "apiVersion": "2016-01-01",
    "location": "[resourceGroup().location]",
    "sku": {
        "name": "Standard_LRS"
    },
    "kind": "Storage",
    "properties": {}
}
```

<span data-ttu-id="42080-114">Au sein de l’objet ordinateur virtuel de hello, nous avons besoin d’une dépendance sur tooensure de compte de stockage hello qu’il a créé avant que hello virtual machine.</span><span class="sxs-lookup"><span data-stu-id="42080-114">Within hello virtual machine object, we need a dependency on hello storage account tooensure that it's created before hello virtual machine.</span></span> <span data-ttu-id="42080-115">Au sein de hello `storageProfile` section, nous spécifions puis hello URI complet de hello emplacement de disque dur virtuel, ce qui fait référence à compte de stockage hello et est nécessaire pour les disques de hello du système d’exploitation et les disques de données.</span><span class="sxs-lookup"><span data-stu-id="42080-115">Within hello `storageProfile` section, we then specify hello full URI of hello VHD location, which references hello storage account and is needed for hello OS disk and any data disks.</span></span> 

```
{
    "apiVersion": "2015-06-15",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[variables('vmName')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
    "[resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))]",
    "[resourceId('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
    ],
    "properties": {
        "hardwareProfile": {...},
        "osProfile": {...},
        "storageProfile": {
            "imageReference": {
                "publisher": "MicrosoftWindowsServer",
                "offer": "WindowsServer",
                "sku": "[parameters('windowsOSVersion')]",
                "version": "latest"
            },
            "osDisk": {
                "name": "osdisk",
                "vhd": {
                    "uri": "[concat(reference(resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))).primaryEndpoints.blob, 'vhds/osdisk.vhd')]"
                },
                "caching": "ReadWrite",
                "createOption": "FromImage"
            },
            "dataDisks": [
                {
                    "name": "datadisk1",
                    "diskSizeGB": 1023,
                    "lun": 0,
                    "vhd": {
                        "uri": "[concat(reference(resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))).primaryEndpoints.blob, 'vhds/datadisk1.vhd')]"
                    },
                    "createOption": "Empty"
                }
            ]
        },
        "networkProfile": {...},
        "diagnosticsProfile": {...}
    }
}
```

## <a name="managed-disks-template-formatting"></a><span data-ttu-id="42080-116">Mise en forme de modèle de disques gérés</span><span class="sxs-lookup"><span data-stu-id="42080-116">Managed disks template formatting</span></span>

<span data-ttu-id="42080-117">Avec des disques Azure géré, disque de hello devient une ressource de niveau supérieur et ne requiert plus un toobe de compte de stockage créé par l’utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="42080-117">With Azure Managed Disks, hello disk becomes a top-level resource and no longer requires a storage account toobe created by hello user.</span></span> <span data-ttu-id="42080-118">Disques gérés ont été exposées tout d’abord Bonjour `2016-04-30-preview` version de l’API, ils sont disponibles dans toutes les versions ultérieures de API et sont désormais de type de disque par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="42080-118">Managed disks were first exposed in hello `2016-04-30-preview` API version, they are available in all subsequent API versions and are now hello default disk type.</span></span> <span data-ttu-id="42080-119">Bonjour sections suivantes parcourir les paramètres par défaut de hello et décrit en détail comment toofurther personnaliser vos disques.</span><span class="sxs-lookup"><span data-stu-id="42080-119">hello following sections walk through hello default settings and detail how toofurther customize your disks.</span></span>

> [!NOTE]
> <span data-ttu-id="42080-120">Il est recommandé de toouse une API version postérieure à `2016-04-30-preview` en raison de modifications avec rupture entre `2016-04-30-preview` et `2017-03-30`.</span><span class="sxs-lookup"><span data-stu-id="42080-120">It is recommended toouse an API version later than `2016-04-30-preview` as there were breaking changes between `2016-04-30-preview` and `2017-03-30`.</span></span>
>
>

### <a name="default-managed-disk-settings"></a><span data-ttu-id="42080-121">Paramètres de disque géré par défaut</span><span class="sxs-lookup"><span data-stu-id="42080-121">Default managed disk settings</span></span>

<span data-ttu-id="42080-122">toocreate une machine virtuelle avec des disques gérés, vous n’avez plus besoin de ressources de compte de stockage de hello toocreate et peut mettre à jour votre ressource de machine virtuelle comme suit.</span><span class="sxs-lookup"><span data-stu-id="42080-122">toocreate a VM with managed disks, you no longer need toocreate hello storage account resource and can update your virtual machine resource as follows.</span></span> <span data-ttu-id="42080-123">Notez en particulier les que hello `apiVersion` reflète `2017-03-30` et hello `osDisk` et `dataDisks` ne sont plus faire référence tooa URI spécifique pour hello disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="42080-123">Specifically note that hello `apiVersion` reflects `2017-03-30` and hello `osDisk` and `dataDisks` no longer refer tooa specific URI for hello VHD.</span></span> <span data-ttu-id="42080-124">Lors du déploiement sans spécifier de propriétés supplémentaires, disque de hello utilisera [les stockage LRS Standard](storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="42080-124">When deploying without specifying additional properties, hello disk will use [Standard LRS storage](storage-redundancy.md).</span></span> <span data-ttu-id="42080-125">Si aucun nom n’est spécifié, il prend format hello `<VMName>_OsDisk_1_<randomstring>` pour le disque de hello du système d’exploitation et `<VMName>_disk<#>_<randomstring>` pour chaque disque de données.</span><span class="sxs-lookup"><span data-stu-id="42080-125">If no name is specified, it takes hello format of `<VMName>_OsDisk_1_<randomstring>` for hello OS disk and `<VMName>_disk<#>_<randomstring>` for each data disk.</span></span> <span data-ttu-id="42080-126">Par défaut, le chiffrement de disque Azure est désactivé ; la mise en cache d’est en lecture/écriture pour les disques de hello du système d’exploitation et None pour les disques de données.</span><span class="sxs-lookup"><span data-stu-id="42080-126">By default, Azure disk encryption is disabled; caching is Read/Write for hello OS disk and None for data disks.</span></span> <span data-ttu-id="42080-127">Vous pouvez le remarquer dans l’exemple hello ci-dessous qu'est toujours une dépendance de compte de stockage, bien que cela est uniquement pour le stockage de diagnostics et n’est pas nécessaire pour le stockage sur disque.</span><span class="sxs-lookup"><span data-stu-id="42080-127">You may notice in hello example below there is still a storage account dependency, though this is only for storage of diagnostics and is not needed for disk storage.</span></span>

```
{
    "apiVersion": "2017-03-30",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[variables('vmName')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))]",
        "[resourceId('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
    ],
    "properties": {
        "hardwareProfile": {...},
        "osProfile": {...},
        "storageProfile": {
            "imageReference": {
                "publisher": "MicrosoftWindowsServer",
                "offer": "WindowsServer",
                "sku": "[parameters('windowsOSVersion')]",
                "version": "latest"
            },
            "osDisk": {
                "createOption": "FromImage"
            },
            "dataDisks": [
                {
                    "diskSizeGB": 1023,
                    "lun": 0,
                    "createOption": "Empty"
                }
            ]
        },
        "networkProfile": {...},
        "diagnosticsProfile": {...}
    }
}
```

### <a name="using-a-top-level-managed-disk-resource"></a><span data-ttu-id="42080-128">Utilisation d’une ressource de disque géré de niveau supérieur</span><span class="sxs-lookup"><span data-stu-id="42080-128">Using a top-level managed disk resource</span></span>

<span data-ttu-id="42080-129">Comme une configuration de disque toospecifying autre hello dans l’objet d’ordinateur virtuel hello, vous pouvez créer une ressource de disque de niveau supérieur et attacher en tant que partie de la création de machine virtuelle hello.</span><span class="sxs-lookup"><span data-stu-id="42080-129">As an alternative toospecifying hello disk configuration in hello virtual machine object, you can create a top-level disk resource and attach it as part of hello virtual machine creation.</span></span> <span data-ttu-id="42080-130">Par exemple, nous pouvons créer une ressource de disque comme suit toouse comme disque de données.</span><span class="sxs-lookup"><span data-stu-id="42080-130">For example, we can create a disk resource as follows toouse as a data disk.</span></span>

```
{
    "type": "Microsoft.Compute/disks",
    "name": "[concat(variables('vmName'),'-datadisk1')]",
    "apiVersion": "2017-03-30",
    "location": "[resourceGroup().location]",
    "sku": {
        "name": "Standard_LRS"
    },
    "properties": {
        "creationData": {
            "createOption": "Empty"
        },
        "diskSizeGB": 1023
    }
}
```

<span data-ttu-id="42080-131">Au sein de l’objet d’ordinateur virtuel hello, nous pouvons ensuite référencer cette toobe d’objet de disque attaché.</span><span class="sxs-lookup"><span data-stu-id="42080-131">Within hello VM object, we can then reference this disk object toobe attached.</span></span> <span data-ttu-id="42080-132">Spécifier l’ID de ressource hello Hello gérés disque que nous avons créé dans hello `managedDisk` propriété permet de hello pièce jointe du disque de hello hello machine virtuelle est créée.</span><span class="sxs-lookup"><span data-stu-id="42080-132">Specifying hello resource ID of hello managed disk we created in hello `managedDisk` property allows hello attachment of hello disk as hello VM is created.</span></span> <span data-ttu-id="42080-133">Notez que hello `apiVersion` pour hello ressource d’ordinateur virtuel est défini trop`2017-03-30`.</span><span class="sxs-lookup"><span data-stu-id="42080-133">Note that hello `apiVersion` for hello VM resource is set too`2017-03-30`.</span></span> <span data-ttu-id="42080-134">Notez également que nous avons créé une dépendance sur tooensure de ressource de disque hello qu'il est créé avec succès avant la création d’ordinateurs virtuels.</span><span class="sxs-lookup"><span data-stu-id="42080-134">Also note that we've created a dependency on hello disk resource tooensure it's successfully created before VM creation.</span></span> 

```
{
    "apiVersion": "2017-03-30",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[variables('vmName')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))]",
        "[resourceId('Microsoft.Network/networkInterfaces/', variables('nicName'))]",
        "[resourceId('Microsoft.Compute/disks/', concat(variables('vmName'),'-datadisk1'))]"
    ],
    "properties": {
        "hardwareProfile": {...},
        "osProfile": {...},
        "storageProfile": {
            "imageReference": {
                "publisher": "MicrosoftWindowsServer",
                "offer": "WindowsServer",
                "sku": "[parameters('windowsOSVersion')]",
                "version": "latest"
            },
            "osDisk": {
                "createOption": "FromImage"
            },
            "dataDisks": [
                {
                    "lun": 0,
                    "name": "[concat(variables('vmName'),'-datadisk1')]",
                    "createOption": "attach",
                    "managedDisk": {
                        "id": "[resourceId('Microsoft.Compute/disks/', concat(variables('vmName'),'-datadisk1'))]"
                    }
                }
            ]
        },
        "networkProfile": {...},
        "diagnosticsProfile": {...}
    }
}
```

### <a name="create-managed-availability-sets-with-vms-using-managed-disks"></a><span data-ttu-id="42080-135">Créer des groupes à haute disponibilité gérés avec des machines virtuelles à l’aide de disques gérés</span><span class="sxs-lookup"><span data-stu-id="42080-135">Create managed availability sets with VMs using managed disks</span></span>

<span data-ttu-id="42080-136">toocreate gérés disponibilité jeux avec des machines virtuelles à l’aide de disques gérés, ajoutez hello `sku` disponibilité toohello de l’objet défini des ressources et hello `name` propriété trop`Aligned`.</span><span class="sxs-lookup"><span data-stu-id="42080-136">toocreate managed availability sets with VMs using managed disks, add hello `sku` object toohello availability set resource and set hello `name` property too`Aligned`.</span></span> <span data-ttu-id="42080-137">Cela garantit que les disques hello pour chaque machine virtuelle sont suffisamment isolées les uns des autres tooavoid points de défaillance uniques.</span><span class="sxs-lookup"><span data-stu-id="42080-137">This ensures that hello disks for each VM are sufficiently isolated from each other tooavoid single points of failure.</span></span> <span data-ttu-id="42080-138">Notez également que hello `apiVersion` pour la ressource à haute disponibilité de hello est défini trop`2017-03-30`.</span><span class="sxs-lookup"><span data-stu-id="42080-138">Also note that hello `apiVersion` for hello availability set resource is set too`2017-03-30`.</span></span>

```
{
    "apiVersion": "2017-03-30",
    "type": "Microsoft.Compute/availabilitySets",
    "location": "[resourceGroup().location]",
    "name": "[variables('avSetName')]",
    "properties": {
        "PlatformUpdateDomainCount": 3,
        "PlatformFaultDomainCount": 2
    },
    "sku": {
        "name": "Aligned"
    }
}
```

### <a name="additional-scenarios-and-customizations"></a><span data-ttu-id="42080-139">Personnalisations et scénarios supplémentaires</span><span class="sxs-lookup"><span data-stu-id="42080-139">Additional scenarios and customizations</span></span>

<span data-ttu-id="42080-140">toofind des informations complètes sur les spécifications des API REST hello, passez en revue hello [créer un documentation de l’API REST de disque géré](/rest/api/manageddisks/disks/disks-create-or-update).</span><span class="sxs-lookup"><span data-stu-id="42080-140">toofind full information on hello REST API specifications, please review hello [create a managed disk REST API documentation](/rest/api/manageddisks/disks/disks-create-or-update).</span></span> <span data-ttu-id="42080-141">Vous trouverez d’autres scénarios, ainsi que par défaut et les valeurs acceptables qui peuvent être des API toohello soumis par le biais des déploiements de modèle.</span><span class="sxs-lookup"><span data-stu-id="42080-141">You will find additional scenarios, as well as default and acceptable values that can be submitted toohello API through template deployments.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="42080-142">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="42080-142">Next steps</span></span>

* <span data-ttu-id="42080-143">Pour les modèles complètes qui utilisent des disques gérés visitez hello suivant les liens de dépôt de démarrage rapide d’Azure.</span><span class="sxs-lookup"><span data-stu-id="42080-143">For full templates that use managed disks visit hello following Azure Quickstart Repo links.</span></span>
    * [<span data-ttu-id="42080-144">Machine virtuelle Windows avec disques gérés</span><span class="sxs-lookup"><span data-stu-id="42080-144">Windows VM with managed disk</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows)
    * [<span data-ttu-id="42080-145">Machine virtuelle Linux avec disques gérés</span><span class="sxs-lookup"><span data-stu-id="42080-145">Linux VM with managed disk</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-linux)
    * [<span data-ttu-id="42080-146">Liste complète des modèles de disque géré</span><span class="sxs-lookup"><span data-stu-id="42080-146">Full list of managed disk templates</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md)
* <span data-ttu-id="42080-147">Visitez hello [vue d’ensemble des disques Azure administrés](storage-managed-disks-overview.md) toolearn document savoir plus sur des disques gérés.</span><span class="sxs-lookup"><span data-stu-id="42080-147">Visit hello [Azure Managed Disks Overview](storage-managed-disks-overview.md) document toolearn more about managed disks.</span></span>
* <span data-ttu-id="42080-148">Passez en revue la documentation de référence de modèle hello pour les ressources de l’ordinateur virtuel en visitant hello [référence de modèle Microsoft.Compute/virtualMachines](/templates/microsoft.compute/virtualmachines) document.</span><span class="sxs-lookup"><span data-stu-id="42080-148">Review hello template reference documentation for virtual machine resources by visiting hello [Microsoft.Compute/virtualMachines template reference](/templates/microsoft.compute/virtualmachines) document.</span></span>
* <span data-ttu-id="42080-149">Passez en revue la documentation de référence de modèle hello pour les ressources de disque en visitant hello [référence de modèle Microsoft.Compute/disks](/templates/microsoft.compute/disks) document.</span><span class="sxs-lookup"><span data-stu-id="42080-149">Review hello template reference documentation for disk resources by visiting hello [Microsoft.Compute/disks template reference](/templates/microsoft.compute/disks) document.</span></span>
 
